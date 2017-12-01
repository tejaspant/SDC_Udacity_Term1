## Project: Vehicle Detection and Tracking
[![Udacity - Self-Driving Car NanoDegree](https://s3.amazonaws.com/udacity-sdc/github/shield-carnd.svg)](http://www.udacity.com/drive)

## Overview
---
The objectives of the project can be summarized as below:

* Extract features from images to identify cars using color histograms, raw pixel values of training images and histogram of oriented gradients (HOG)
* Train a classifier
* Build a pipeline to identify vehicles in a video with minimum false positives


[//]: # (Image References)

[image1]: ./write_up_images/hog_classify_example.png "hog_classify_example"
[image2]: ./write_up_images/test_image_classifier_example.png "test_image_classifier_example"

## Explain how (and identify where in your code) you extracted HOG features from the training images. Explain how you settled on your final choice of HOG parameters
---
To get the best results for extraction of HOG features from the images, firstly different color spaces were experimented like RGB, HSV, LUV, HLS, YUV, YCrCb keeping the HOG parameters constant. Out of these different color spaces, LUV and YCrCb gave the least false positives. In general, YCrCb seemed to outperform LUV. Using the YCrCb color space, the HOG parameters were tuned.

The three HOG parameters 1) orientations 2) pixels_per_cell 3) cells_per_block were changed one at a time keeping the other two constant. The different values examined for the different paramters were: 

* orientations = 8, 10, 12
* pixels_per_cell = 6, 8, 10
* cells_per_block = 2, 3, 4

The combination of parameters which gave the least false positives on the test images and were finally used for extracting features from the images are:

* orientations = 10
* pixels_per_cell = 8
* cells_per_block = 2

Here is a sample car image with its extracted HOG image
![alt text][image1]

## Describe how (and identify where in your code) you trained a classifier using your selected HOG features (and color features if you used them)
---
A linear SVM is trained using the HOG features along with color histogram features and binned color features. 
The false positives predicted by the SVM are eliminated using a heat map. In the heat map (originally all pixel values are 0), 1 is added to the pixel value for every pixel within the boxes predicted by HOG sub sampling. Then a threshold is applied to the heat map which sets the local pixel value in the heat map to 0 if the local pixel value is less than the threshold. Currently the threshold value used in this study is 2. 

## Describe how (and identify where in your code) you implemented a sliding window search. How did you decide what scales to search and how much to overlap windows?
---
Instead of extracting HOG features for every window in the sliding window approach, the HOG subsampling is approach. Three different scales are used in the subsampling approach for different regions of the image to account for the fact that vehicles far away from the camera appear smaller. 

## Show some examples of test images to demonstrate how your pipeline is working. How did you optimize the performance of your classifier?
---
To optimize the performance of the classifier, different color spaces, number of HOG channels and HOG orientations were experimented. Here is an example of the performance of the final pipeline on one of the test images: 

![alt text][image2]

## Provide a link to your final video output. Your pipeline should perform reasonably well on the entire project video (somewhat wobbly or unstable bounding boxes are ok as long as you are identifying the vehicles most of the time with minimal false positives
---
The name of the final video is project_video_output.mp4. The pipeline seems to work reasonably well on the project video with very few false positives.

## Describe how (and identify where in your code) you implemented some kind of filter for false positives and some method for combining overlapping bounding boxes
---
By recording the history of the heat map, the number of false positives is reduced. This also helps to reduce the wobbling of the bounding boxes.

## Discussion and scope for future work
---
The current vehicle detection software pipeline is a rather crude implementation and there is scope for improvement. Firstly the pipeline detects vehicles on the other side of the lane as well. The HOG subsampling function needs to modififed to limit the search region in the X direction only to the driver's lane to remove these false positives. Besides this, when the two vehicles in the project video come closer, the bounding boxes merge into a single box. It would be a good idea associate a particular bounding box with a particular vehicle. The wobbling of the bounding boxes can also be reduced.  
