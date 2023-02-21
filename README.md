# Behavioral Cloning

## Introduction 

- The objective of this project is to create a model for an autonomous car that can drive using the data collected from a human driving behavior. 
- The data collected consists of images from three different cameras mounted on the vehicle along with the corresponding steering angles.
- To achieve this, a Convolutional Neural Network (CNN) has been developed using the Keras library, which provides a high-level API for deep learning networks, with Tensorflow as the backend.

## Project Files Description

The following files are included in the project:

- [README.md](README.md): (writeup report) documentation of the results
- [Behavioral_Cloning_main.py](Behavioral_Cloning_main.py): containing the script to train the model
- [drive.py](drive.py): a Python script used to drive the car autonomously, it receives images as input for the CNN and sends back the predicted steering angle and speed.
- [Nvidia_model.py](Nvidia_model.py): containing the script to create the model
- [model.h5](model.h5): contains the trained convolution neural network

Using the Udacity provided simulator and my drive.py file, the car can be driven autonomously around the track by executing

```
python drive.py model.h5
```

The predictions made by the model will be sent back to the server via a websocket connection.


## Major Steps

### Data Collection
Collecting driving data using the Udacity simulator in training mode in 3 different camera angles (left, center, right).

![left_2023_02_14_16_05_13_493](https://user-images.githubusercontent.com/108230926/220438325-e275f59e-2437-4f1e-9e7d-429fbbaf79fd.jpg) ![center_2023_02_14_16_05_13_493](https://user-images.githubusercontent.com/108230926/220438223-489c0624-90f2-48fe-8e25-5c1b9559c6f8.jpg) ![right_2023_02_14_16_05_13_493](https://user-images.githubusercontent.com/108230926/220438421-4218ae78-d3cf-4506-a95d-aa16fa743e2c.jpg)


### Image Processing and Augmentation

For augmenting the image dataset, 4 techniques were implemented:
- **Zoom**: zooming a random image by upto 30%
<img width="794" alt="image" src="https://user-images.githubusercontent.com/108230926/220441218-1cc8fa06-3452-45bb-8b5f-3411df5737c4.png">


- **Pan**: translating the 'x' and 'y' of the image by 20%
<img width="796" alt="image" src="https://user-images.githubusercontent.com/108230926/220441361-92cbb270-a9d4-4327-94c6-76b87efc92d2.png">


- **Brightness**: altering the image brightness by 20%
<img width="796" alt="image" src="https://user-images.githubusercontent.com/108230926/220441616-481e580d-b537-49ef-bd9f-1afb12ed4ad1.png">


- **Image flipping**: flipping the image horizontally along with the steering angle
<img width="792" alt="image" src="https://user-images.githubusercontent.com/108230926/220441725-51e2c6dd-17e9-4438-89aa-2e2473330547.png">


### Setting up Neural Network Architecture
Designing, training and validating a deep learning model that predicts steering angles from image data. The model selected is inspired from the following [Nvidia convolution model](https://images.nvidia.com/content/tegra/automotive/images/2016/solutions/pdf/end-to-end-dl-using-px.pdf)

<img width="369" alt="image" src="https://user-images.githubusercontent.com/108230926/220442959-f170d25b-abb3-41ec-a4fd-3e897bb223f7.png">

In order to gauge how well the model was working, I split the image and steering angle data into a training and validation sets. The training dataset also included the augmented image data to train the model efficiently.

The activation function used was 'ELU' (Exponential Linear Unit) as it gave better accuracy and lower losses compared to the 'ReLU' (rectified linear unit). The model used an adam optimizer, so the learning rate was not tuned manually.

### Testing the Model in the Simulator

Using the model to drive the vehicle autonomously around the track, keeping the vehicle on the road for an entire loop.

## Data Collection Strategy from Udacity Simulator

- First download the simulator from the following link (https://github.com/udacity/self-driving-car-sim)
- Then click on training and drive the vehicle on simulator using keyboard.
- Click on Recording to record the images and corresponding steering angle.
- The data is to be collected in two ways: Controlled Driving and Recovery Driving. 
- Controlled driving involved driving the vehicle close to the center of the driving lane, while recovery driving involved special maneuvers to recover the vehicle back to the center from outside the lane. 
- The final dataset consisted of 1 loop of centered driving in a counter-clockwise direction, 1 loop in a clockwise direction, and additional maneuver for recovery, smooth driving in curves and critical waypoints.
