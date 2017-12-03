## Project: Behavioral Cloning
[![Udacity - Self-Driving Car NanoDegree](https://s3.amazonaws.com/udacity-sdc/github/shield-carnd.svg)](http://www.udacity.com/drive)

## Overview
---
The objectives of this project is to use End-to-End Deep Learning to train a self-driving car to drive autonomously along a track in a simulator.

[//]: # (Image References)

[image1]: ./write_up_images/hog_classify_example.png "hog_classify_example"
[image2]: ./write_up_images/test_image_classifier_example.png "test_image_classifier_example"

## Is the code functional?
---
The script used to train the model is *model.ipynb*. It generates the model *model.h5* which can be run using the script *drive.py*. The *drive.py* has been modified to pre-process the images taken by the center camera in the simulator. 

## Is the code usable and readable?
---
The code has been commented well so that a user can use it. A Python generator has been used to generate training data instead of storing the entire training data in memory. This helps to improve the efficiency of the code.

## Has an appropriate model architecture been employed for the task?
---
The exact model architecture from Nvidia's End-to-End for Self-Driving Cars(https://arxiv.org/abs/1604.07316) is used in this project. This architecture has 5 convolutional layers and 4 fully connected layers. The image is normalized before the convolutional layers.   

## Has an attempt been made to reduce overfitting of the model?
---
The dataset was split into 70% training data and 30% validation data. The model was trained for 5 epochs. Since the MSE error kept on decreasing for all the 5 epochs no effort was made to reduce overfitting.

## Have the model parameters been tuned appropriately?
---
The learning parameter for the Adam optimizer was tuned. Initially the default value of 0.001 was used. For this learning rate, the trained model was not able to navigate the car around the track without going off the track. The learning rate was then reduced to 0.0001 and the trained model performed very well.

## Is the training data chosen appropriately?
---
The training data used for training the model was obtained by driving the car around the track for three laps. For the first lap, the position of the car is maintained close to the center of the track. For the second and third lap, the car is forced to hug the left and right side of the track respectively.

## Is the car able to navigate correctly on test data?
---

The car is able to navigate Track 1 completely autonomously without any manual intervention. The video showing the car navigating Track 1 is *video.mp4*

