# Project: Deep Learning Project - Follow Me
### Introduction
In this project,  we'll build and train a Fully Convolutional Neural Network (FCN) to find a target in images from a simulated quad-copter.  The target in this case is a specific human character, namely "hero", in a an envirnoment where a lot of non-hero characters are moving around as well. The FCN is used to apply semantic segmentation of an image, where pixel-wise classification is utilised to seperate hero pixels from non-hero and background pixels.
![alt text][image1]

[image1]: ./writeup_images/following.png
[image2]: ./writeup_images/Arch.png
[image3]: ./writeup_images/loss.png

### FCN Architecture
The goal of the FCN is to classify pixels in an image into 3 main classes, hero, non-hero, and backgorund pixels. We use the basic encoder-1x1 convolution-decoder architecture of an FCN with different filter sizes as shown in the figure below. The encoder is basically a Convolutional Neural Network (CNN), while the decoder is a transposed CNN. As for the 1x1 convolution, this layer is used to maintain the spatial information throughout the entire architecture.
## Encoder
The encoder used in the FCN has the purpose of extracting features from the input images. The early layers identify basic features like edges, lines, and color blobs. The deeper layers try to learn more complicated shapes and finally objects.
In order to extract more features, we use a deeper network. This might lead to a rather large model, so the depth-wise separable convoluation is used instead. This reduces the training speed, and leads to a smaller model with a redudced number of parameters.
## Decoder
After the 1x1 convolution layer, the image is reduced to a much smaller size compared to the original. Hence, we use the decoder to upsample the features to the original image size.
The upsampling process is achieved by transpose convolution which is, in some sense, the reverse of the classic convolution process. In this project, the bilinear upsamping is used.
## Skip Connections
In addition, skip connections between layers of the encoder and layers of the decoder are used to enable the network to utilise multiple resolution scales from the different layers.
## Final Architecture
The final architecture used for this project is shown in the figure below:

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
## Learning Rate
For learning rate tuning, if the learning rate was too high, then the optimizer might overshoot the optimum solution and might not coverge. On the other hand, a very small learning rate would take a lot of time to coverge. After trying learning rates of 0.01, 0.0001, and 0.001, the best result was using the 0.001 learning rate.
## Number of Epochs
When tuning the number of epochs, I started of with 20-30, but that caused the accuracy to be below the required 0.4 target. So increasing the number of epochs to 45 did the the job.
## Final Hyper-parameters
After tuning the reminaing hyper-parameters by trial and error to get a good performance, the final hyper-parameters are in the table below:

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

### Discussion
The pipeline implemented in this project is genertic and can be used to segemnet other objects like cats, dogs, and even cars. To be able to detect other objects, we must use a different dataset where the pixels are segmented based on the objects that needs to be segemented. This means that the network needs to be re-trained to be able to detect and segment the features of the required objects.
