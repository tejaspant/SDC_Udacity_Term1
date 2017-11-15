## Project: Advanced Lane Finding
[![Udacity - Self-Driving Car NanoDegree](https://s3.amazonaws.com/udacity-sdc/github/shield-carnd.svg)](http://www.udacity.com/drive)

## Overview
---
In this project we create a pipeline to detect lane boundaries in a video using computer vision. The objectives of the project can be summarized as below:

* Calibrate camera
* Undistort the images taken by the camera
* Carry out a perspective transform to get a birds-eye view of the lane markings
* Identify lane markings using color or gradient thresholds or a combination of the two to get binary image
* Use a sliding window search to identify the lane markings and fit a second order polynomial to get equation of the lane marking
* Get the radius of curvature of the lane marking at a point closest to the camera
* Calculate car offset from the center of the lane 

[//]: # (Image References)

[image1]: ./write_up_images/chess_board_distort_undistort.png "Camera Matrix Chessboard"
[image2]: ./write_up_images/test_image_distort_undistort.png "Test Image Undistort"
[image3]: ./write_up_images/binary_image_example.png "Binary Image Test"
[image4]: ./write_up_images/birds_eye_view_image_example.png "Perspective Transform Image"
[image5]: ./write_up_images/binary_image_with_curve_fit.png "Binary Image Curve Fit"
[image6]: ./write_up_images/image_with_lane_lines_R_offset.png "Test Image with Lanes, Radius of Curvature and Offset from Lane Center"

## Briefly state how you computed the camera matrix and distortion coefficients. Provide an example of a distortion corrected calibration image
---
The camera matrix matrix and distortion coefficients are obtained using the OpenCV functions *findChessboardCorners*, *calibrateCamera*. An example of an undistorted calibration image is shown below,
![alt text][image1]

## Provide an example of a distortion-corrected image
---
After the camera matrix matrix and distortion coefficients are obtained, it is tested on one of the test images
![alt text][image2]

The difference between the original image and the undistorted image is evident in the deer crossing sign.

## Describe how (and identify where in your code) you performed a perspective transform and provide an example of a transformed image
---
The perspective transform is carried out using OpenCV function *getPerspectiveTransform*. Different combinations of source and destination points were tested and the set of points that provided the best results are:
source points = ([[585, 450], [200, 720], [1128, 720], [685, 450]])
destination points = ([[320, 0], [320, 720], [960,720], [960, 0]])
An example of the perspective transform on the test image is shown below,
![alt text][image4]
 
## Describe how (and identify where in your code) you used color transforms, gradients or other methods to create a thresholded binary image. Provide an example of a binary image result
---
A combination of B channel in RGB color space and L channel in LUV colorspace is used to obtain the binary image with the lane markings. Below is an example of a binary image,
![alt text][image3]

## Describe how (and identify where in your code) you identified lane-line pixels and fit their positions with a polynomial
---
The lane-line pixels are identified using the sliding window approach using 9 windows and a window margin of 100 pixels. After the pixels are identified a second degree polynomial is fit using the *polyfit* function in *numpy* to get equation of the curve. An example of the binary image with the lane-line identified is shown below  
![alt text][image5]

## Describe how (and identify where in your code) you calculated the radius of curvature of the lane and the position of the vehicle with respect to center
---
The radius of curvature is calculated for each lane line using the formula provided in Lecture 35. The maximum of the two radii is reported in the image. 
To calculate the position of the vehicle with respect to center of the lane, the center of the lane is calculated as the mean of *x* pixel value at maximum *y* pixel value. To locate the center of the lane in meters, a value of 3.7/100 in X direction is used for meters per pixel. The location of the car is the center of the image and is calculated from the shape of the image in terms of pixels 

## Provide an example image of your result plotted back down onto the road such that the lane area is identified clearly
---
Having calculated the fit for the lane lines and warped back onto the original image, the lane boundaries, radius of curvature and location from the center of the lane is calculated relatively accurately as can be seen below
![alt text][image6]

##Provide a link to your final video output. Your pipeline should perform reasonably well on the entire project video (wobbly lines are ok but no catastrophic failures that would cause the car to drive off the road!)
---
Here is the link to the project video:
[Project Video]()