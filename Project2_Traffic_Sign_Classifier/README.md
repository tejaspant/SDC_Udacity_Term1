## Project: Build a Traffic Sign Recognition Program
[![Udacity - Self-Driving Car NanoDegree](https://s3.amazonaws.com/udacity-sdc/github/shield-carnd.svg)](http://www.udacity.com/drive)

## Overview
---
In this project, we use deep neural networks and convolutional neural networks to classify traffic signs. Specifically, we use the [LeNet-5](http://yann.lecun.com/exdb/publis/pdf/lecun-01a.pdf) convolutional neural network architecture to train and validate a model which can classify traffic sign images using the [German Traffic Sign Dataset](http://benchmark.ini.rub.de/?section=gtsrb&subsection=dataset). After training the model we test it on German traffic signs found on the web. The objectives of the project can be summarized as below:

* Load the German Traffic Sign data set
* Explore, summarize and visualize the data set
* Design, train and test a model architecture
* Use the model to make predictions on new images
* Analyze the softmax probabilities of the new images
* Summarize the results with a written report

[//]: # (Image References)

[image1]: ./write_up_images/org_dataset_train_image_bar_plot.png "Train Bar Plot Visualization"
[image2]: ./write_up_images/org_dataset_valid_image_bar_plot.png "Valid Bar Plot Visualization"
[image3]: ./write_up_images/org_dataset_test_image_bar_plot.png "Test Bar Plot Visualization"
[image4]: ./write_up_images/sample_grayscale.png "Sample Grayscale"
[image5]: ./write_up_images/sample_org_normalized.png "Sample Original and Normalized"
[image6]: ./write_up_images/final_dataset_train_image_bar_plot.png "Train Augmented Bar Plot Visualization"
[image7]: ./write_up_images/final_dataset_valid_image_bar_plot.png "Valid Augmented Bar Plot Visualization"
[image8]: ./write_up_images/web_images_test.png "Web Test Images"
[image9]: ./write_up_images/softmax_predictions.png "Softmax Prediction Row 1"
[image10]: ./write_up_images/softmax_predictions2.png "Softmax Prediction Row 2"
[image11]: ./write_up_images/softmax_predictions3.png "Softmax Prediction Row 3"
[image12]: ./write_up_images/softmax_predictions4.png "Softmax Prediction Row 4"
[image13]: ./write_up_images/softmax_predictions5.png "Softmax Prediction Row 5"
[image14]: ./write_up_images/softmax_predictions6.png "Softmax Prediction Row 6"
[image15]: ./write_up_images/sample_org_normalized.png "Compare Org and Normalized"

## Dataset Summary
---
Following is the information about the data set:
* The size of training set is 34799
* The size of the validation set is 4410
* The size of test set is 12630
* The shape of a traffic sign image is (32, 32, 3)
* The number of unique classes/labels in the data set is 43

## Visualization of Dataset
---
The distribution of the different classes of images for the training, validation and test set is shown below. This helps us get a brief idea about the statistics of the data
![alt text][image1]

![alt text][image2]

![alt text][image3]

## Preprocessing of Dataset
---
Preprocessing of the available data set involved two steps:

1. Convert the image to grayscale. This is done using the OpenCV library. Using grayscaling, the total number of parameters in the convolutional neural network can be reduced since the size of the image is reduced from (32, 32, 3) from (32, 32, 1). The reduced number of parameters help in increasing the rate of convergence for the gradient descent method. Here is a sample grayscale image:

![alt text][image4]

2. Normalize the grayscale so that the mean is zero. Normalizing the features in the training set in general helps the improve convergence rate of gradient descent. Here is a comparison between the original image and the final normalized grayscale image:

![alt text][image15]

## Model Architecture
---
As mentioned previously the architecture similar to LeNet-5.  The final model architecture is:

| Layer         		|     Description	        					|
|:---------------------:|:---------------------------------------------:|
| Input         		| 32x32x1 grayscale image   					|
| Convolution 5x5     	| 1x1 stride, valid padding, outputs 28x28x6 	|
| RELU					|												|
| Max pooling	      	| 2x2 stride,  outputs 14x14x6 					|
| Convolution 5x5	    | 2x2 stride, valid padding, outputs 10x10x16   |
| RELU					|												|
| Max pooling	      	| 2x2 stride,  outputs 5x5x16 					|
| Flatten			    | outputs 1x1x400    							|
| Fully connected		| input 400, output 120       					|
| RELU					|												|
| Fully connected		| input 120, output 84        					|
| RELU					|												|
| Fully connected		| input 84, output 43        					|

## Training the Model
---
To train the model, the following values of the hyperparameters are used:
1. Learning Rate for Adam Optimizer = 0.0009

2. Number of Epochs = 30

3. Batch Size = 128

## Solution Approach
---
Using the above hyperparameters and the convolutional neural network architecture, intially it was observed that the validation set accuracy did not reach the minimum 0.93 value as specified in the problem statement.
To resolve this issue, an augmented data set was developed. The development of this dataset is discussed below.

## Generating Augmented Dataset
---
Taking cue from the work done by [Sermanet and LeCunn](http://yann.lecun.com/exdb/publis/pdf/sermanet-ijcnn-11.pdf), an augmented data set is generated from the available training and validation data set. 
Two operations are carried out for generating the augmented dataset, rotating images randomly by [+15,-15] degrees and translating images by [-2,2] pixels.
After doing this the distribution of the data set for training and validation is shown below:
 
![alt text][image6]

![alt text][image7]

A more uniform distribution of the samples over all the classes can be seen for both the training and validation data set. This helps in training the model better. The final size of the training set is 89567.
With the augmented dataset, a validation set accuracy of around **98.8%** is achieved. The test set accuracy is **92.38%**.

## Acquiring New Images
---
6 new images are obtained from the web to test the trained model. The test images are shown below. The images had to be reshaped to (32,32,3) size. 
![alt text][image8]

As can be seen from the images, there are a few challenges in classifying these images
* Resing the images to (32, 32, 3) size makes the images blurred 
* The image in the second row and second column is not very clear to the naked eye
* The brightness for a few images is a bit low

## Performance on Images
---
The model is correctly able to classify all the images and the accuracy of the results is **100%**. Compared to the accuracy of the test dataset of **92.38%**, the accuracy of the trained model on the new images is much higher. There are many possible reasons for such a high accuracy on the test images for eg. number of images is low hence higher accuracy percentage, better quality of images in terms of brightness and visibility. A more detailed discussion on the possible reasons for the better accuracy would require looking into the test dataset more and comparing images with the images taken from the net. Currently, this has not been done.

## SoftMax Probabilities
---
The top 5 softmax probabilities for the test images have been outputted. The results for the prediction are shown below:
![alt text][image9]

![alt text][image10]

![alt text][image11]

![alt text][image12]

![alt text][image13]

![alt text][image14]
