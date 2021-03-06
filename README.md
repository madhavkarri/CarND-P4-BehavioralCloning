# **Project: Behavioral Cloning**

## MK

Overview
---
Develop a convolutional neural network model using keras to clone driving behavior. Train, validate and test a model using Keras. The model will output a steering angle to an autonomous vehicle.

The Project
---
The goals/steps for this project:
* Use simulator to collect data for good driving behavior
* Build convolution neural network in Keras, that predicts steering angles from images
* Train and validate the model with a training and validation set
* Test that the model successfully drives around track one without leaving the road


[//]: # (Image References)

[image1]: ./Writeup_IV/CNNModelSummary.png "CNNModelSummary"
[image2]: ./Writeup_IV/CNNArch.png "CNNArch"
[image3]: ./Writeup_IV/CLD_Fwd.png "CLD_Fwd"
[image4]: ./Writeup_IV/CLD_Rwd.png "CLD_Rwd"

#

#### 1. Files included with submission to run the simulator in autonomous mode

Project includes the following files:
* model.py containing the script to create and train the model
* drive.py for driving the car in autonomous mode
* model.h5 containing a trained convolution neural network 
* README.md summarizes the results
* Final output video [Link](./video.mp4)

#### 2. Functional code
Using the Udacity provided simulator and drive.py file, the car can be driven autonomously around the track by executing 
```sh
python drive.py model.h5
```

#### 3. Project code (model.py)

The model.py file contains the code for the following set of tasks.
* Load all images and steering angles from memory
* Data augumentation using vertical flip
* Data normilization and centering
* Image cropping to retain, only pixels that contain useful information
* Define and build convolution neural network model
* Training, validation, and saving the model

### Model Architecture and Training Strategy

#### 1. Model architecture 

Model consists of a convolution neural network with the following set of features 
![][image1]
![][image2]

#### 2. Model parameter tuning

The model used an adam optimizer, so the learning rate was not tuned manually

#### 3. Appropriate training data

Training data was collected with the objective to sustain vehicle driving within road boundaries. Used only center lane image data for training. For details on how training data was collected, refer to next section

### Model Architecture and Training Strategy

The CNN model used in this project has been replicated and based on the model developed by nvidia for similar work [Link](https://devblogs.nvidia.com/deep-learning-self-driving-cars/).

In order to gauge how well the model was working, image and steering angle data was split into a training and validation sets with a split ratio of 80% and 20% respectively. During the frist attempt itself, model had a low mean squared error on both the training and validation sets. Further, the validation error was lower than the training error. 

Final step was to run the simulator to see how well the car was driving around track one. There was only a single loctaion where the vehicle fell off the track. To improve driving behavior for this specific case, additional data was collected in the vicnity of this specific location.

At the end of the process, the vehicle is able to drive autonomously around the track without leaving the road.


#### Creation of the Training Set & Training Process

To capture good driving behavior the following steps were implemented for data collection:
* Recorded 8 laps on track one using center lane driving in forward direction
* Recorded 8 laps on track one using center lane driving in reverse direction. To minimize left-turn bias in the data.
* Further data augumentation was performed using "cv2" vertical flip on all of the images

Below are few random examples of center lane driving in forward direction

![][image3]


Below are few random examples of center lane driving in reverse direction

![][image4]

After collection and data augumentation process, a total of 34,660 number of data points represented the complete data set. Finally, the dataset was shuffled randomly and allocated 20% of the data into a validation set. 

Used this training data for training the model. The validation set helped determine if the model was over or under fitting. The ideal number of epochs was determined to be about 5. Used an adam optimizer so that manually training the learning rate wasn't necessary.
