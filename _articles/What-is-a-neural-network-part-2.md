---
published: true
topic: What are Neural Networks: Continued
subtitle:
date: 2023-09-01
tags: AI ML
---

## What is a neural network?
### We are focusing on the default form.
In this article we are focusing on neural networks as they appeared in the 70s and 80s. This is because the theory is still vital and will help us when we tackle more advanced neural networks, such
as CNNs.

### What are neural networks comprised of?
The most important part of a neural network is the neuron. A neuron is something that hold a number, $$n \in [0,1]$$. We refer to this number, $$n$$, as the neuron's activation. Everything else that comprises
a neural network is to do with manipulating the activations of neurons so that they neural network can adapt to our task.

This tutorial focuses on the MNIST dataset, as this is the example 3B1B used, the author who I drew most of this information from. Let's consider a simple network, with:
- one input layer, with each neuron representing a pixel in a 28x28 grid,
- two hidden layers, comprised of 16 neurons each,
- one output layer, comprised on ten nodes, each representing a prediction for one of our handwritten digits.

Put image here!

Throughout the rest of this tutorial we will describe the processes that allow this network to learn. I will also link at the bottom two implementations of this network, that I created myself,
one with fastai and the other with PyTorch.

### Weights and Bias

The question now arises about how we can generate the activations of our neurons such that those in the output layer accurately represent our predictions. The answer is weights, which can be visually
represented as connections between neurons. Each neuron in a subsequent layer \\(K_{n+1}\\) has \\(n\\) weights, where \\(n\\) is the number of weights in \\(L_{k-1}\\).
to calculate the activation of a particular neuron in the 2nd layer, while also ensuring the activation of the neuron is between 0 and 1.

Insert maths here.

But, what if you want a neuron to become active only when it's beyond a certain threshold? This is where bias comes in, which we add in the case of inactivity.

Insert maths here.

The effect of these neurons being manipulated by both weights and bias is that it gives us more room to tweak our model, so that it can generate more accurate predictions. We refer to this process as learning.

### The maths of neural networks and neurons as functions

Put image here!

