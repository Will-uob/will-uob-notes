---
title: What are autoencoders?
date: 2023-09-18
published: true
tags: ML AI
---

# What is an autoencoder?
An autoencoder is an unsupervised neural network that learns to recognise which aspects of the observable data are relevant, and limit noise in data that can be discarded. It works by using two functions:
- The encoder, which turns our input into "code", and
- The decoder, which takes our "code" and outputs something as similar to the original output data as possible.

## How does it work?
The autoencoder itself works by compressing the input into a latent space representation, the "code", and then using the decoder to predict the original output data based on this code. This process can be used
to find the key information and generate findings based on it, and can be used in areas such as fraud or intrusion detection.

![Image of the above process](https://miro.medium.com/v2/resize:fit:720/format:webp/1*44eDEuZBEsmG_TCAKRI3Kw@2x.png)
