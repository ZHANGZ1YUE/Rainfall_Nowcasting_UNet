# Application of Convolutional Encoder-Decoder for Radar Image-Based Rainfall Nowcasting

## Author
ZHANG Ziyue (Faculty of Engineering from Kyoto University, at the time of the project)

## Description
This is a project started from 2022/10 as an undergraduate graduation research for a Bachelor's degree in Engineering. The study explores the implementation of U-Net architecture in the rainfall nowcasting task with radar image extrapolation. The work has referred to both U-Net and RainNet (A study done by Ayzel Georgy), with sensitivity analysis in some hyperparameters, model structures, and prediction method (direct 30 minutes prediction). Original radar data is the X-band radar data for 7 rainfall events available from Japan Meterological Agency.

## Purpose of each file
* Model.ipynb gives the basic Unet model (code referred to https://github.com/zhixuhao/unet)
* pad.ipynb does exactly what the name suggests, padding the input data into larger dimension with symmetric padding
* predict.ipynb makes prediction for up to 3 models, it gives original input images, output image (predicted) and intensity prediction
* data_prep.ipynb prepares the training data by converting a continuous rainfall frames to a compacted shape. It 1:split the entire rainfall event by 5 mins interval, 2: takes first four frames (1,2,3,4)and compact it as first training input, and second four frames (2,3,4,5) as second training input, so on.. 3: prepare the output by taking the frame after 30 minutes. In this way, (for example)the training input is (0,1,2,3-from 0min to 15min) and the output is (9 - 45min) (The numbers refer to the the order from the original dataset) This becomes the training output data. 
* connect_events.ipynb connects several rainfall events into one dataset.Pretty straight forward.
* rainfall_info.ipynb is not important. it first visualizes the input rainfall data, then explore a little bit about weight initializer

## How to use
The entire study is done with Google Colab and keras as framework. The first step is to prepare the data, of course. The original data is collected as a continuous rainfall radar images for every 1 minute. Use data_prep to generate a input data and a output data (for each of the rainfall event). Then connect all of the separate dataset for each of the event as a complete training dataset (for both input and ouput) by using connect_events. Then pad the dataset into 192 128 from 180 120, since the encoder-decoder requires this to downsample and upsample for 4 times. Next, to train the model, simply run Model.ipynb, a .h5 file should be output as the trained model. Finally, to predict the with the trained model, use predict.ipynb directly by giving the trained model and prepared dataset. 

## Several things I want to try
* How to visualize the prediction result. I want to make a .gif for the prediction of all the frames from the entire prediction, rather than just displaying one single frame.
* I want to replace the convolutional layers to residual blocks (ResNet)
* Data augmentation or more data. 
* More input channels, or larger interval.
