**Advanced Lane Finding Project**

The goals / steps of this project are the following:

* Compute the camera calibration matrix and distortion coefficients given a set of chessboard images.
* Apply a distortion correction to raw images.
* Use color transforms, gradients, etc., to create a thresholded binary image.
* Apply a perspective transform to rectify binary image ("birds-eye view").
* Detect lane pixels and fit to find the lane boundary.
* Determine the curvature of the lane and vehicle position with respect to center.
* Warp the detected lane boundaries back onto the original image.
* Output visual display of the lane boundaries and numerical estimation of lane curvature and vehicle position.

[//]: # (References)

[source]		: ./adavanced_lane_detection.ipynb "Advanced Lane Finding implementation"
[input images]	: ./camera_cal/undistort_output.png "To compute the camera calibration"
[input images]	: ./test_images/test*.jpg "Input Imagesmages"
[input video]	: ./project_video.mp4 "input Video"
[output images]	: ./output_images/test*.jpg "Output Images"
[output video]	: ./output_project_video.mp4 "Output Video"

---
###Writeup 

###Camera Calibration

####1. Briefly state how you computed the camera matrix and distortion coefficients. Provide an example of a distortion corrected calibration image.

The code for this step is contained in the first code cell "calibrateCamera()" of the IPython notebook located in "./adavanced_lane_detection.ipynb"   

Example : "./output_images/camera_calibration_output.png"

####2. Describe how (and identify where in your code) you used color transforms, gradients or other methods to create a thresholded binary image.  Provide an example of a binary image result.
I used a combination of color and gradient thresholds to generate a binary image (function: binaryThreshold).  Here's an example of my output for this step.  
(note: this is not actually from one of the test images)

Example : "./output_images/test2_threshold_warped.png" => Right imgae

####3. Describe how (and identify where in your code) you performed a perspective transform and provide an example of a transformed image.

The code for my perspective transform includes a function called `perspectiveTransform()` function takes as inputs an image (`img`) and "inverse" bool .  
I chose the hardcode the source and destination points in the following manner:

```
    src = np.float32([[340,645],[575,465],[705,460],[975,635]])
    dst = np.float32([[340,645],[340,345],[975,340],[975,635]])
```

I verified that my perspective transform was working as expected by drawing the `src` and `dst` points onto a test image and its warped counterpart to verify that the lines appear parallel in the warped image.

Example : "./output_images/test2_threshold_warped.png" => Left image

####4. Describe how (and identify where in your code) you identified lane-line pixels and fit their positions with a polynomial?

Please look at functions : extractLeftAndRightPixels() and optimizedExtractLines() to fit the lane lines. Function extractLeftAndRightPixels is not called for all the frames only called for initial frame and when left and right curvature absolute difference is > 100 otherwise optimizedExtractLines() is called.

Example : "./output_images/test2_lane_boundaries.png"

####5. Describe how (and identify where in your code) you calculated the radius of curvature of the lane and the position of the vehicle with respect to center.

Please look at function findCurvature() returns left lane and right lane radius of curvature

####6. Provide an example image of your result plotted back down onto the road such that the lane area is identified clearly.

Please look at funtion test_images(), running the pipeline on all the test images. Please check the output in "output_images" folder.  

Here is an example of my result on a test image:

Example : "./output_images/test2_final_output.png"

---

###Pipeline (video)

####1. Provide a link to your final video output.  Your pipeline should perform reasonably well on the entire project video (wobbly lines are ok but no catastrophic failures that would cause the car to drive off the road!).

Here's a link to my video result(./output_project_video.mp4)

---

###Discussion

####1. Briefly discuss any problems / issues you faced in your implementation of this project.  Where will your pipeline likely fail?  What could you do to make it more robust?

The pipeline might fail when lanes are not detectable and when right radius of curvature are off than left one and vice-versa

To improve : remove hardcorded values, need to calculate radius of curvature of the lanes accurately and implement the "averaging frames" to reduce jitter. Also make the pipeline work for challenge videos

