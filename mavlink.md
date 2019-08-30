# Overview

Read [Publish-subscribe Pattern](https://en.wikipedia.org/wiki/Publish–subscribe_pattern), [JMS Messeging Models](https://www.journaldev.com/9743/jms-messaging-models)


MAVLink is a very lightweight messaging protocol for communicating with drones (and between onboard drone components).

Messages are defined within XML files. Each XML file defines the message set supported by a particular MAVLink system, also referred to as a "dialect". The reference message set that is implemented by most ground control stations and autopilots is defined in common.xml (most dialects build on top of this definition).

There are two modes:

- topic mode: the protocol will not emit a target system and component ID for messages to save link bandwidth. 

- point-to-point mode: MAVLink uses a target ID and target component.

# MAVLink 2 Packet Format

```c
uint8_t magic;              ///< protocol magic marker
uint8_t len;                ///< Length of payload
uint8_t incompat_flags;     ///< flags that must be understood
uint8_t compat_flags;       ///< flags that can be ignored if not understood
uint8_t seq;                ///< Sequence of packet
uint8_t sysid;              ///< ID of message sender system/aircraft
uint8_t compid;             ///< ID of the message sender component
uint8_t msgid 0:7;          ///< first 8 bits of the ID of the message
uint8_t msgid 8:15;         ///< middle 8 bits of the ID of the message
uint8_t msgid 16:23;        ///< last 8 bits of the ID of the message
uint8_t payload[max 255];   ///< A maximum of 255 payload bytes
uint16_t checksum;          ///< X.25 CRC
```

```c
uint8_t signature[13];      ///< Signature which allows ensuring that the link is tamper-proof (optional)
```

MAVLink waits for the packet start sign, then reads the packet length and matches the checksum after n bytes. If the checksum matches, it returns the decoded packet and waits again for the start sign. If bytes are altered or lost, it will drop the current message and continue the next try on the following message.

The system ID represents the identity of a particular MAVLink system (vehicle, GCS, etc.). MAVLink can be used with up to 255 systems at the same time. The component ID reflects a component that is part of a larger system - for example a system might include an autopilot, companion computer and/or camera, which can be separately addressed. The component ID therefore lets MAVLink be used for both on- and off-board communication.

Having the sequence in the header allows MAVLink to continuously provide feedback about the packet drop rate and thus allows the aircraft or ground control station to take action.

# Usage

The C MAVLink library utilizes a "channel" metaphor to allow for simultaneous processing of multiple, independent MAVLink streams in the same program. All receiving and transmitting functions provided by this library require a channel, and it is important to use the correct channel for each operation.

MAVLink reception/decoding is done in a number of phases:

1. Parse the incoming stream into objects representing each packet (`mavlink_message_t`).

```c
mavlink_status_t status;
mavlink_message_t msg;
int chan = MAVLINK_COMM_0;

while(serial.bytesAvailable > 0)
{
  uint8_t byte = serial.getNextByte();
  if (mavlink_parse_char(chan, byte, &msg, &status))
    {
    printf("Received message with ID %d, sequence: %d from component %d of system %d\n", msg.msgid, msg.seq, msg.compid, msg.sysid);
    // ... DECODE THE MESSAGE PAYLOAD HERE ...
    }
}
```

2. Decode the MAVLink message contained in the packet payload into a C struct:

```c
if (mavlink_parse_char(chan, byte, &msg, &status)) {
...
  switch(msg.msgid) {
      case MAVLINK_MSG_ID_GLOBAL_POSITION_INT: // ID for GLOBAL_POSITION_INT
        {
          // Get all fields in payload (into global_position)
          mavlink_msg_global_position_int_decode(&msg, &global_position);

        }
        break;
      case MAVLINK_MSG_ID_GPS_STATUS:
        {
          // Get just one field from payload
          visible_sats = mavlink_msg_gps_status_get_satellites_visible(&msg);
        }
        break;
     default:
        break;
    }
...
} 
```


The most useful decoding function is named with the pattern `mavlink_msg_message_name_decode()`, and extracts the whole payload into a C struct.

Transmitting messages can be done by using the `mavlink_msg_*_pack()` function, where one is defined for every message. The packed message can then be serialized with `mavlink_helpers.h:mavlink_msg_to_send_buffer()` and then writing the resultant byte array out over the appropriate serial interface.
