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
Different color spaces were experimented and *YCrCb* was finalized. The HOG parameters used were:
* orientations = 10
* pixels_per_cell = 8
* cells_per_block = 2

Here is a sample car image with its extracted HOG image
![alt text][image1]

## Describe how (and identify where in your code) you trained a classifier using your selected HOG features (and color features if you used them)
---
A linear SVM is trained using the HOG features along with color histogram features and binned colo features.

## Describe how (and identify where in your code) you implemented a sliding window search. How did you decide what scales to search and how much to overlap windows?
---
Instead of extracting HOG features for every window in the sliding window approach, the HOG subsampling is approach. Three different scales are used in the subsampling approach for different regions of the image to account for the fact that vehicles far away from the camera appear smaller. 

## Show some examples of test images to demonstrate how your pipeline is working. How did you optimize the performance of your classifier?
---
To optimize the performance of the classifier, different color spaces, number of HOG channels and HOG orientations were experimented. Here is an example of the performance of the final pipeline on one of the test images: 

![alt text][image2]

## Provide a link to your final video output. Your pipeline should perform reasonably well on the entire project video (somewhat wobbly or unstable bounding boxes are ok as long as you are identifying the vehicles most of the time with minimal false positives
---
The name of the finale video is project_video_output.mp4. The pipeline seems to work reasonably on the project video with very few false positives.

## Describe how (and identify where in your code) you implemented some kind of filter for false positives and some method for combining overlapping bounding boxes
---
By recording the history of the heat map, the number of false positives is reduced. This also helps to reduce the wobbling of the bounding boxes
