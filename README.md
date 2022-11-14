# Generative Adversarial Networks

## Introduction and concept

Generative Adversarial Networks (GANs) represent a class of Deep Learning Frameworks which have firstly been introduced by Ian Goodfellow in 2014. While their spectrum of application is becoming larger with research, the main focus of GANs has been image processing.

The main idea behind GANs consists in the competition between 2 neural networks in a zero-sum game, the scope of each network being to improve its prediction accuracy. One network is named the "Generator" and the other the "Discriminator". The Generator's goal is to create fake data, with the ultimate goal of its output to be perceived as real. The goal of the Discrimnator is to look at the data generated by the Generator and label the data as "real" or "fake". As the data that the application of Generative Adversarial Networks is mainly focused on, as well as the data in our study is represented by images, we will focus on implementing Deep Convolutional Generative Adversarial Networks (DCGANs).

## Data 

The dataset used in our study is the Celeba Dataset. It represents a collection of more than 200K photos of celebrities, which come in .jpg format.



## Deep Convolutional Generative Adversarial networks 

From a general point of view, Convolutional Neural Networks represent a particular type of neural networks that posess an ability to detect patterns in the data (for example, shapes, corners or edges in the case of images). Their hidden layers, called "Convolutional Layers", receive input, transform it and then pass it to the following layers. The operation that corresponds to the transformation is called a "Convolution".

### Convolution

The object at the basis of the convolution process is the kernel. Given the 3-dimensional characterisation of our data (height, width and values of the RGB channel), the kernel can be initialized as 3-dimensional, with the 3rd dimension representing the number of filters applied, or 2-dimensional, meaning that the same filter will be applied to each of the 3 color channels. The values that constitute the kernel are randomly initialized and will be further optimized according to the accuracy and loss of the convolution process.

The kernel is then passed along the image, row by row and column by column, until it has slid over all the pixels of the image. A dot product is applied between the kernel and the surface on the image on which it slides. The resulting image is the output matrix. In the case of a Convolutional Neural Network, the output obtained by the convolution inside a hidden layer is passed as input to the next hidden layer.

![convolution1](https://user-images.githubusercontent.com/114659655/200131876-4e9d595c-9ff9-4f57-9c58-b13382168a12.png)

### Convolutional Layers

The neural networks we are going to build are going to be formed of Convolutional Layers. Convolutional Layers are meant to process data that is correlated in space. The output of each convolutional layer is a feature map, which corresponds to a spatial projection where certain features are exposed, which have previously been found by the convolutional layer.

The layers are interconnected : the second layer takes as input the output from the first layer and so on. This can be seen in the values of the arguments that are passed onto each layer. For example, the number of output channels from the first layer will be the number of input channels of the second layer. We implement the layers using they torch.nn module.


## Generator and Discriminator

Throughout the implementation of our neural networks, we wil use the Pytorch framework. Both the Generator and the Discriminator are Neural Network Object Types. They are defined as classes who inherit from the nn.Module in Pytorch. The structure of both networks will be defined using the __init__() method and applied to computation using the forward() method.

###Weights initialization

In the case of Convolutional Neural Networks, weights represent the multiplicative values present in the kernel. A 3x3 kernel will therefore have 9 weights.

###Generator

The Generator Neural Network's initial input is represented by a latent 1-dimensional noise vector. The length of the latent vector is fixed and can be chosen artibtrarily, but we will choose 100 for our example. We will draw the latent vector from the Gaussian distribution. The dimension of the latent vector will represent the number of channels of the input of the first layer of the network. 

![1_ULAGAYoGGr5eEB2377ArYA](https://user-images.githubusercontent.com/114659655/201658929-c53960f3-1d5d-4e33-b6c6-f6f88d484100.png)


Convolution is then applied by sliding the kernel along the noise vector. We need to pass from a 1x100 dimensional vector to the size of the images in the dataset (3x64x64), the convolution applied is transposed. Each transposed convolution will produce a feature map inside the generator.

Batch Normalization :

