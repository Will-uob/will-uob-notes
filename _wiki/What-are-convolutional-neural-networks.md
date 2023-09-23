---
published: true
title: What are convolutional neural networks
date: 23-09-2023
tags: AI ML
---

# What are convolutional neural networks?
A convolutional neural network is comprised of three main types of layers:
- Convolutional layer
- Pooling layer
- Fully-connected layer

### The convolutional layer
The convolutional layer converts the image into neumerical values, allowing the neural network to
interpret and extract relevant patterns. This layer consists of input data, a filter, and a feature map.
In an image example, our input data is a 3D matrix, representing the height, width and depth (RGB) of
our image. Our filter, also known as a kernel, will move across the image, checking if the feature
is present. This is a convolution.

The kernel is a 2D, usually $3 \times 3, $array of weights, representing part of the image[^1]. The filter
is applied to an area of the image, and the dot product is calculated between the pixels and filter.
This output is then fed into an output array. Afterwards, the filter shifts by a stride, repeating
until reaching the end of the image. The final output is known as a feature map.

There are three hyperparameters which affect the volume size of the output that must be considered:
- The number of filters affects the depth of the output[^2],
- The stride is the distance the kernel moves over the input matrix[^3],
- Zero-padding is usually used when the filters don't fit the input image[^4].

#### Additional convolution layer
The structure of the CNN becomes hierarchical, since later layers can see the pixels within the
feature maps of the previous layers. So, first the neural network will break down an image into it's
constituent parts (think edges, corners, then basic shapes, etc...), and use this information to guess
the object.

### Pooling layer
Pooling layers, otherwise known as downsampling, reduces the number of parameters in the input.
The pooling operation sweeps a filter across the input, but without any weights. Instead, the kernel
applies an aggregation function to the values within the receptive field, populating the output array.
There are two types of pooling:
- Max pooling: As the filter sweeps across the input, it selects the maximum pixel value to send to
  the output array[^5].
- Average pooling: As the filter sweeps across the input, it calculates the average value within
  the receptive field to send to the output array.

While some information is lost in this layer, it helps reduce complexity, improve efficiency and
limit risk of overfitting.

### Fully-connected layer
In the fully-connected layer, each node in the output layer connects directly to a node in the previous
layer. This layer preforms the task of classification, based on the features extracted through the
previous layers and their different filters. While convolutional and pooling layers tend to use ReLU
functions, FC layers usually leverage a softmax activation function[^6] to classify inputs
appropriately, producing a probablity from 0 to 1.

[^1]: Like weights and biases in a perceptron, the weights in the kernel can change.

[^2]: For example, three distinct filters would yield three different feature maps, a depth of three.

[^3]: A larger stride yields a smaller output.

[^4]: There are three types of padding:
    - Valid padding: The last convolution is dropped if dimensions do not align,
    - Same padding: This padding ensures that the output layer has the same size as the input,
    - Full padding: Increases the size of the ouput by adding zeros to the border of the input.

[^5]: This approach tends to be used more often than average pooling.

[^6]: What is a softmax function?
