# Sign-Language-Recognition-System

## Objective:

This project was done as a part of my Masters in computer science projects. This project aims to propose a system prototype that will automatically recognize signing for effective communication. The system will absorb a hand gesture as input and return the corresponding recognized character/word as output in real-time. For classification, the proposed system will use Deep Convolutional Neural Network and evaluate its performance in large-scale scenarios. The popularity of hand gestures is predicated on the detection of some shaped-based features like orientation, the middle of mass, centroid, finger status, thumbs in positions of raised or folded fingers of the hand. This technique might be used for day-to-day communication and as a learning module.

## Data set: 

The data set used is “Include” created by IIT madras. The dataset contains 4287 Videos, 263-word signs, and 15 different word categories.

## Challenges Faced:

There were mainly 3 challenges faced during the research work:

1. Average size of the video is 1-3 seconds: The video length makes it very difficult to extract meaningful features as the actions are performed very quickly. The speed of signing differs from person to person, it may also happen that a few parts of the sign are performed quickly while the rest are done slowly. 

2. Low Inter Class Difference:  Though the signs for particular words are different from each other. The differences are very subtle and may not get picked up by the trained system. This makes the training difficult and inefficient. For example, the sign for both black and white have the same arm motion, they both differ in palm movement.

3. High Intra Class Difference: It is already noticed that there are similarities between different signs and it was also noticed that for the same sign there was a comparable difference between how different signers were illustrating them. Just like how languages spoken by different individuals can have different accents, similarly, each signer has your accent while performing the gesture.

## Pre Processing of the dataset:

The following steps were done to clean the data set and prepare it for modelling.

1. Resizing the video
2. Converting the image to binary
3. Converting to correct color channels - RGB, YCrCb
4. Data Augmentation to increase the data set while considering all the potential cases while a sign is performed. For example:each sign can be done using the left or right hand depending on the dominant hand. It can be performed anywhere on the screen and can be done while moving. Mainly 2 types of data augumentation was used: Horizontal flipping of images and translation of images.
5. Morphological operations were performed to fill in the gaps in the frames of the video once converted to binary
6. Finding contours

## Feature Extraction and Selection:

Implemented HOG:
1. Resized the dataset to 150*150
2. Calculated Gradients and their direction (x and y)  for every pixel
3. Calculated the Magnitude and Orientation 
4. Calculated Histogram of Gradients in 50×50 cells 
5. Normalized gradients in 50×50 cell 
6. We have created features for 50x50 blocks of the image. These features are appended to create a feature vector for the final image.

Using Mediapipe:
1.	Get key points for Left hand
2.	Get key points for Right hand
3.	Get key points for Pose 
4.	FV = [flatten(pose), flatten(left), flatten(right)]
5.	Each frame generates an array of 258 lengths i.e., 258 features
6.	Using post-padding on videos for creating equal frame length
7.	Input key (154, 258)

## Classification Models:

Implemented the following models:
1. SVM
2. Simple LSTM
3. Bi-directional LSTM
4. CNN LSTM

Using the above the following systems were developed and their respective accuracies
1.	Using HOG for Feature extraction and SVM for Classification: 30-40%
2.	Using HOG for Feature extraction and LSTM for Classification: 32.3% 
3.	Using Mediapipe for FV extraction and Simple LSTM for Classification: 75.6%
4.	Using Mediapipe for FV extraction and Bidirectional LSTM for classification: 70.8%
5.	Using Mediapipe for FV extractions and CNN LSTM for classification: 60.7%
6.	Using Mediapipe for FV extraction and Ensemble of LSTM models for classification: 77.2%


![Screenshot 2021-12-08 070409](https://user-images.githubusercontent.com/129342521/231035641-173fc126-97c1-4c1f-9f81-fca018f3c273.png)

