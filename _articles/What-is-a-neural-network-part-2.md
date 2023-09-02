---
published: true
topic: What are Neural Networks: Continued
subtitle:
date: 2023-09-01
tags: AI ML
---

## What is a neural network?
In this article we attempt to understand how the simplest form of neural network functions in detail. This is so we may, in the future, tackle harder types of neural networks, such as convolutional neural
networks.

### What are neural networks comprised of?
The most important part of a neural network is the neuron. A neuron is something that hold a number, $n \in [0,1]$. We refer to this number, $n$, as the neuron's activation. Everything else that comprises
a neural network is to do with manipulating the activations of neurons so that the neural network can adapt to our task.

This tutorial focuses on the MNIST dataset, as this is the example 3b1b used, the author who I drew most of this information from. Let's consider a simple network, with:
- one input layer, with each neuron representing a pixel in a 28x28 grid,
- two hidden layers, comprised of 16 neurons each,
- one output layer, comprised on ten nodes, each representing a prediction for one of our handwritten digits.

![Image of a neural network](/images/mnist_nn.png)

### Weights and Bias

The question now arises about how we can generate the activations of our neurons such that those in the output layer accurately represent our predictions. The answer is weights, which can be visually
represented as connections between neurons. Each neuron in a subsequent layer $K\_{k+1}$ has $n$ weights, where $n$ is the number of weights in $L\_{k}$. The activation of a neuron[^2] in a subsequent
layer is the defined as $\sigma(w\_1a\_1 + w\_2a\_2 + \dots + w\_na\_n)$. I love $5 + 5$. I love $5 + 10 + \dots$, where $\sigma$ is a function used to ensure the value of our neuron's activation
is $\in [0,1]$.[^1]

But, what if you want a neuron to become active only when it's beyond a certain threshold? This is where bias comes in, which we add in the case of inactivity. Hence, the activation of a neuron is defined
now as $\sigma(w\_1a\_1 + w\_2a\_2 + \dots + w\_na\_n + b)$, where $b$ is the bias. We will explain why bias is useful when we cover neurons as functions.

A neural network "learns" by automatically altering the weights and biases of each neuron, which leads to better predictions of data.

#### Notation
Please note we can represent the process of calculating the activations for a subsequent layer using matrix multiplication, that is

$$
\begin{bmatrix}
         w\_{0,0} & w\_{0,1} & \cdots & a\_{0,n}\\\
         a\_{1,0} & a\_{1,1} & \cdots & a\_{1,n}\\\
         \vdots & \vdots & \ddots & \vdots\\\
         a\_{k,0} & a\_{k,1} & \cdots & a\_{k,n}
     \end{bmatrix}
\times
\begin{bmatrix}
         a\_{0}^{(0)}\\\
         a\_{1}^{(0)}\\\
         \vdots\\\
         a\_{n}^{(0)}
     \end{bmatrix}
 =
 \begin{bmatrix}
    a\_{0}^{(1)}\\\
    a\_{1}^{(1)}\\\
    \vdots\\\
    a\_{n}^({1})
 \end{bmatrix}
$$

where, for example, $a_0^{(1)} = \sigma(w_{0,0}a_0`{(0)} + w_{0, 1}a_1^{(0)} + \dots + w_{0, n}a_n^{(0)} + b_0)$, which can be represented as,

$$ a^{(1)} = (\mathrm{W} a^{(0)} + b) $$

### Neurons as functions

A neuron can be viewed as a functions, as it takes all the ouputs of the previous layer's neurons and returns an activation value, $n \in [0,1]$. Indeed, we can view the entire neural network as a single 
function, $f$, where

$$f(a_0, a_1, \dots, a_{783}) = \begin{pmatrix} y_0 \\ y_1 \\ \vdots \\ y_9 \end{pmatrix}$$.


[^1]: Note that in industry we don't use sigmoids, but rather we use [ReLUs](https://en.wikipedia.org/wiki/Rectifier_(neural_networks)), since they are far easier to train.

[^2]: I believe this is the same as the neuron's [activation function](https://en.wikipedia.org/wiki/Rectifier_(neural_networks)).
