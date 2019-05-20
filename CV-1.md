# Computer Vision

Reference:

[1]Computer Vision: Algorithms and Applications. Chap. 1-4, 6, 11, 14

[2]Computer Vsion: A Modern Approach
Vision is an inverse probelem in which we seek to recover some unknowns given insufficient information to fully specify the solution, resorting to physics-based and prbabilistic models to disambiguate between potential problems.

> [forward and inverse modelling](https://astronomy.stackexchange.com/questions/19687/what-does-forward-modeling-mean)

In computer vision, we do the inverse modelling, i.e., to describe the world that we see in one or more images and to reconstruct its properties.

> cognitive: logic proving and planning _versus_ perceptual

It is better to think back from the problem at hand to suitable techniques rather than to  grab the first technique that you may have heard of. This kind of working back from problems to solutions is typical of an __engineering__ approach to the study of vision.

## A history

- 1970s: trying to recover the 3D structure of the world -> "blocks world" from edge detection, generalized cylinders, pictorial structures for elastic arrangements of parts; qualitative approach to understanding intensities and shading variations and explaining them by the effects of image formation phenomena -> intrisic images; many feature-based stereo correspondence algorithms; intensity-based optical flow algorithm

> Description of a visual information processing system
> - Computational theory: the goal and constraints
> - Representations and algorithms
> - Hardware implementation

- 1980s: more sophisticated mathematical techniques. Image pyramids for image blending and coarse-to-fine correspondence search; scale space processing; wavelets; a wide variety of shape-from-X techniques; better edge and contour detection. the unification of stereo, flow, shape-from-X and edge detection; Markov Random Field; Kalman filter;

- 1990s: _projective reconstructions_, which did not require knowledge of camera calibration. factorization techniques. Physics-based vision. Dense stereo correspondence algorithm. _Graph cut_ for global optitimazation. _multi-view steroe algorithms_ for producing complete 3D surfaces. _Active contours_; _particle filters_; _level sets_. _minimum energy_ and _minumu description length_, _normalized cuts_ and _mean shift_. _Statistical learning_. _Image morphing_, _view interpolation_.

- 200s: _Image stitching_, _high dynamic range image capture_, _exposure bracketing_, _tone mapping_, _texture synthesis_, "constrellation model". More efficient algorithms for complex global optimization problems. The application of sophisticaed _machine learning_ techniques to computer vision problem.

## Image Formation

## 
### Camera Models

