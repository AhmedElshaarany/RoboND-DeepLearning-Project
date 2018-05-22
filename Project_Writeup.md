# Project: Deep Learning Project - Follow Me
### Introduction
In this project,  we'll build and train a Fully Convolutional Neural Network (FCN) to find a target in images from a simulated quad-copter.  The target in this case is a specific human character, namely "hero", in a an envirnoment where a lot of non-hero characters are moving around as well. The FCN is used to apply semantic segmentation of an image, where pixel-wise classification is utilised to seperate hero pixels from non-hero and background pixels.
![alt text][image1]

[image1]: ./writeup_images/following.png
[image2]: ./writeup_images/Arch.png
[image3]: ./writeup_images/loss.png


### FCN Architecture
The goal of the FCN is to classify pixels in an image into 3 main classes, hero, non-hero, and backgorund pixels. We use the basic encoder-1x1 convolution-decoder architecture of an FCN with different filter sizes as shown in the figure below. The encoder is basically a Convolutional Neural Network (CNN), while the decoder is a transposed CNN. As for the 1x1 convolution, this layer is used to maintain the spatial information throughout the entire architecture. 
In addition, skip connections between layers of the encoder and layers of the decoder are used to enable the network to utilise multiple resolution scales from the different layers.

![alt text][image2]

The filter sizes for the encoder and decoder are as follows:

| Block      	| Filter Size |
|:-----------------:|:-----:|
| Encoder1     | 128 |
| Encoder2          | 256 |
| Encoder3        | 512 |
| 1x1 Conv       | 128 |
| Decoder1            | 512 |
| Decoder2       | 256 |
| Decoder3  | 128 |

### Hyper-parameter Tuning
After tuning hyper-parameters to get a good performance, the final hyper-parameters are in the table below:

| Hyper-parameter  | Value |
|:-----------------:|:-----:|
| Learning Rate     | 0.001 |
| Batch Size          | 16 |
| Number of Epochs        | 45 |
| Steps per Epoch       | 50 |
| Workers            | 2 |

### Results
As shown in the figures below, the loss drops and reaches the value of 0.0387 for the validation set. The final score is 0.4478 as shown in the jupyter notebook.

![alt text][image3]