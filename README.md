# CNN_based_classification
![Python Badge](https://badges.aleen42.com/src/python.svg)
## Overview

### CNN based classification of Cat and Dog
Neural Network is a computing system inspired by biological neural networks that constitute the animal brains. Such systems “learn” to perform tasks by considering examples, generally without being programmed with any task-specific rules.


The Neural Network is constructed from 3 types of layers:
1. Input layer: initial data for the neural network.
2. Hidden layers: an intermediate layer between input and output layer and place where all the computation is done.
3. Output layer: produce the result for given inputs.


## Abstract

The purpose of this script is to understand various stages of building a good CNN model. Using transfer learning techniques, one can achieve nearly 100% accuracy for this task. However, in this script I will try to build a model from scratch that leads a reasonable accuracy. The final result shows close to 95% on validation dataset.

Key highlights:
- Create a model from scratch without transfer learning.
- Gain insights on how the depth and width of the model affects the loss curve
- Create your own data feeder
- Write custom callbacks for saving best model or early stopper
- Prediction on any online/downloaded images

![image](https://user-images.githubusercontent.com/57152712/170843920-d5fc08ac-ce52-43f3-8a89-69252304a9ac.png)

## Set path of the dataset

The images are under two folders, /Cat and /Dog. I do not wish to create separate train and validation folders and copy the images into it. Instead, I will write a custom data feeder that will read images, perform preprocessing and feed to the model. We will perform on-the-fly augmentation within the model (by adding extra layers at the start).

Use the data set: https://www.kaggle.com/pybear/cats-vs-dogs

Move the data to working directory, because input directory is read-only.

![image](https://user-images.githubusercontent.com/57152712/170844042-e686264a-e72c-4d48-aaa6-daa2509840cf.png)
 
![image](https://user-images.githubusercontent.com/57152712/170844046-0183b351-3da2-4440-9ef9-e2044c6ce625.png)
 
The 1st folder as Cat folder has 12470 images and 2nd folder as Dog folder has 12491 images. 

## Delete corrupted images.

![image](https://user-images.githubusercontent.com/57152712/170844060-50ec20d1-ad8e-40dc-871e-854bc7f08296.png)

There are almost 1568 corrupt images.
 
![image](https://user-images.githubusercontent.com/57152712/170844069-6ecc68c4-447c-49ab-bf9d-096a25a0a37d.png)

Remove 2 images for 0 size or non jpg images.

## Create data feeder

-	Resize images
-	define data split fraction
-	batch size
-	seed to shuffle and randomly dividing the training and validation dataset

 ![image](https://user-images.githubusercontent.com/57152712/170844081-6b3018a1-08b2-42f3-af6c-ec792ad63d80.png)

 ![image](https://user-images.githubusercontent.com/57152712/170844088-af79335e-5cd4-45a0-bb7b-2e3fdf5d7966.png)

## Inspect some images

Take 1 batch from the validation dataset and plot.

![image](https://user-images.githubusercontent.com/57152712/170844095-e9cc7183-50b5-43e5-9e19-32864652b048.png)
 
## Create model

Use at least 3 layers. We will try two models, first a shallow one, second with more layers. For this task should expect the shallow model causing an under fit. It is indicative in the loss curve. Here we see that the training_loss and accuracy does not improve after a while.

Note also that, we have included on-the-fly image augmentation in the first two layers. Furthermore, we use dropout for regularization, to avoid over fitting. We do not want high dropout in the initial layers. It is set to a relatively higher value after flattening the convolution layer outputs.

And finally, since we are using ReLu activation function, using kernel_initializer='he_uniform' is highly recommended.
 
![image](https://user-images.githubusercontent.com/57152712/170844099-4ce8bdd7-cbc7-49ed-a4e0-87804d651958.png)

![image](https://user-images.githubusercontent.com/57152712/170844103-e7c618ac-a13c-4732-8907-91263e9b6444.png)

Total params: 1,362,049
Trainable params: 1,361,249
Non-trainable params: 800

## Create callbacks

 ![image](https://user-images.githubusercontent.com/57152712/170844110-c396e3ef-ed22-4cee-a8b3-c3565ec17507.png)

 ![image](https://user-images.githubusercontent.com/57152712/170844112-8d209716-a253-44b5-a7e6-3ef3f2f7d5b0.png)
 
## Accuracy
 
![image](https://user-images.githubusercontent.com/57152712/170844121-b2712ee0-ea84-477c-b64d-03a696fb0d02.png)

 
