The paper focuses on target detection and navigation. A downward-looking camera attached to a multirotor is used to find the target on the ground. The UAV descends to the target and hovers above the target for a few seconds to inspect the target. A high-level decision algorithm based on an OODA (observe, orient, decide, and act) loop was developed as a solution to address the problem. The proposed system performed hovering above the target in three different stages: locate, descend, and hover.

The main node receives the center coordinates of the detected target from the target detection node as an input. This is then converted to the target location in the inertial frame by using the pinhole camera model.

The typical mission is:

1. the UAV takes off;

2. searches for a ground target;

3. If a target is found, the UAV changes its original path and hovers above the target  for a few seconds for an action

4. After hovering, the UAV flies to the next waypoint and starts to search for other targets.


# Target Detection Algorithm

Hough circle method; color detection;

# Conversion of 2D Image Coordinates to World Coordinates

image plane => camera frame (a downward-looking frame, not the actual camera orientation) => body frame => inertial frame (world frame)

Note that no gimbal mechanism is used, meaning that the camera is not always looking downward, a correction is needed.

# Navigation Algorithm

```python
for img_i in frames:
    current_pose = get_current_UAV_pose()
    if istargetFound():                                       # detect and find the target
        img_seq_found = img_timestamp(img_i)
        target_centroid = compute_target_centroid(img_i)
        last_target_centroid = target_centroid
        target_pose = compute_target_pose(current_pose, target_centroid)
        
        if stage == 1: # locate and move to the target horizontally
            hover_pose = target_pose
            hover_pose.z = current_pose.z # but do not descend
            stage = 2  # enter descending stage
        else if stage == 2:
            if distanceXY(target_pose, current_pose) < t:   # already right over the target
                if hover_height < current_pose.z - descend_step:
                    hover_pose.z = current_pose.z - descend_step
                else:
                    hover_pose.z = hover_height
            else:
                stage = 1 # not at the right position, locate again
        else if stage == 3: # already at the hovering height, 
            # tweaking position            
            if abs(img_i.u - target_centroid.u) > g or abs(img_i.v - target_centroid.v) > g:
                dx = (img_i.u - target_centroid.u) / camera_resolution * horizontal_step 
                dy = (img_i.v - target_centroid.v) / camera_resolution * horizontal_step
                hover_pose.x = current_pose.x + dx
                hover_pose.y = current_pose.y + dy
            else: # hover for some time and leave
                wait(hover_time)
                break
    else:                                       # target not found
        img_seq_not_found = img_timestamp(img_i)
        if stage == 3 and img_seq_not_found - img_seq_found < timeout_detection:
                dx = (img_i.u - last_target_centroid.u) / camera_resolution * horizontal_step 
                dy = (img_i.v - last_target_centroid.v) / camera_resolution * horizontal_step
                hover_pose.x = current_pose.x + dx
                hover_pose.y = current_pose.y + dy

``
