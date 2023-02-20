# Behavioral Cloning

## Introduction 

- The objective of this project is to create a model for an autonomous car that can drive using the data collected from a human driving behavior. 
- The data collected consists of images from three different cameras mounted on the vehicle along with the corresponding steering angles.
- To achieve this, a Convolutional Neural Network (CNN) has been developed using the Keras library, which provides a high-level API for deep learning networks, with Tensorflow as the backend.

## Project files description

There are several files included in this repository:

- **drive.py**: a Python script used to drive the car autonomously, it receives images as input for the CNN and sends back the predicted steering angle and speed.
- **model.py**: a script to create and train the CNN, and output the trained model.
- **model.h5**: contains the trained convolutional network.
- **video.py**: a script to create a video of the autonomous vehicle.

To use drive.py, the trained model must be saved as an h5 file, i.e. model.h5. This can be done using the "model.save(filepath)" command. Then, the model can be used with drive.py by running "python drive.py model.h5". The predictions made by the model will be sent back to the server via a websocket connection.

The video of the autonomous agent can be saved using "python drive.py model.h5 run1". The images seen by the agent will be saved in the specified directory, in this case "run1". The video.py script can then be used to create a video from these images, "python video.py run1". The FPS of the video can be specified as an optional argument.

## Project Aim:

The aim of the project was to train a Deep Network to replicate human steering behavior, allowing the vehicle to drive autonomously on the simulator provided by Udacity. The network inputs image data from the front camera and predicts the steering direction at each moment.

## Major steps:

The steps involved in the project are:

- **Data Collection**: Collecting driving data using the Udacity simulator in training mode.
- **Image Processing**: Analyzing, augmenting and processing the collected images.
- **Setting up a Neural Network**: Designing, training and validating a model that predicts steering angles from image data. Model is inspired from the following Nvidia model (https://images.nvidia.com/content/tegra/automotive/images/2016/solutions/pdf/end-to-end-dl-using-px.pdf)
- **Testing the Model in the Simulator**: Using the model to drive the vehicle autonomously around the track, keeping the vehicle on the road for an entire loop.

## Quick note on Data collection strategy:

- First download the simulator from the following link (https://github.com/udacity/self-driving-car-sim)
- Then click on training and drive the vehicle on simulator using keyboard.
- Click on Recording to record the images and corresponding steering angle.
- The data was collected in two ways: Controlled Driving and Recovery Driving. 
- Controlled driving involved driving the vehicle close to the center of the driving lane, while recovery driving involved special maneuvers to recover the vehicle back to the center from outside the lane. 
- The final dataset consisted of 1 loop of centered driving in a counter-clockwise direction, 1 loop in a clockwise direction, and additional maneuver for recovery, smooth driving in curves and critical waypoints.
