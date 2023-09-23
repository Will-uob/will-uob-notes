---
title: What is a u-net?
date: 2023-09-23
published: true
tags: AI ML
---

# What is a U-Net?

![An image of a U-Net](https://miro.medium.com/v2/resize:fit:1400/1*f7YOaE4TWubwaFF7Z1fzNw.png)

A U-Net is a convolutional neural network that consists of two paths; a contracting path and an
expansive path. The contracting path follows the typical architecture of a CNN. It consists of the
repeated usage of two 3x3 convolutions, each followed by a ReLU, and a 2x2 max pooling[^1] operation
with stride[^2] 2 for downsampling. Each downsampling step doubles the number of feature channels[^3].

Every step in the expansive path consists of an upsampling of the feature map, followed by a $2x2$
convolution that halves the number of feature channels, a concatenation with the correspondingly cropped
feature map[^4] from the contracting path, and two $3x3$ convolutions, each followed by a ReLU. The
cropping is needed, since there's a loss of border pixels in every convolution.

At the final layer, a $1x1$ convolution is used to map each 64-component feature vector to the desired
number of classes. In total we have 23 convolutional layers.

[^1]: What is max pooling?

[^2]: What is a stride?

[^3]: Was ist das?

[^4]: Ist das essen?
