The target tracking system is based on the relative distance between the UAV and the target vehicle. The detection algorithm is developed with the color marker the target vehicle, with morphological filter which can reduce the background noise in the image.

# Vision Detection System

1. Fish-eye lens

2. lightweight camera with high resolution

3. Nvidia Jetson TK1, with a 192-core Kepler GK20a GPU.

# Image Processing 

1. Resizing the raw image for reducing the calculation load;

2. Gaussian Smoothing Filter for noise reduction;

3. RGB2HSV

4. Binarization to get the region of interest, a red marker.

5. morphological filter

# Target Tracking

TODO
