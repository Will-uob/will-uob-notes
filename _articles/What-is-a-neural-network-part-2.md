
---
published: true
topic: What are Neural Networks? - 2
date: 2023-09-01
tags: AI ML
---

## What is a neural network?
In this article we attempt to understand how the simplest form of neural network, a multilayer perceptronm, functions in detail. This is so we may, in the future, tackle harder types of neural networks,
such as [convolutional neural networks](https://en.wikipedia.org/wiki/Convolutional_neural_network) and [LSTM](https://en.wikipedia.org/wiki/Long_short-term_memory).

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

$$\begin{pmatrix}w\_{0,0} & w\_{0,1} & \dots \\\ w\_{1,0} & w\_{1,1} \dots \\\ \vdots \ddots \vdots \\\ w\_{k,0} \dots w\_{k, n}\end{pmatrix} \times \begin{pmatrix}a & b \\\ c & d\end{pmatrix} = \begin{pmatrix}a & b \\\ c & d\end{pmatrix}$$


where, for example, $a_0^{(1)} = \sigma{w_{0,0}a_0{(0)} + w_{0, 1}a_1^{(0)} + \dots + w_{0, n}a_n^{(0)} + b_0}$, which can be represented as,

$$ a^{(1)} = (\mathbb{W} a^{(0)} + b) $$

### Neurons as functions

A neuron can be viewed as a function, in fact as it's own [linear regression model](https://www.ibm.com/topics/linear-regression), as it takes all the ouputs of the previous layer's neurons and
returns an activation value, $n \in [0,1]$. Indeed, we can view the entire neural network as a single function, $f$, where

$$f(a_0, a_1, \dots, a_{783}) = \begin{pmatrix} y_0 \\ y_1 \\ \vdots \\ y_9 \end{pmatrix}$$.

## How does a neural network learn?
Our goal is to adjust our weights and biases, using labelled training data, to improve our performance on validation / test data. [^3]
In order to go about this process of adjusting our weights and biases, we use a [cost (loss) function](https://en.wikipedia.org/wiki/Loss_function), which indicates our model's performance. In this example,
we use the [mean squared error](https://en.wikipedia.org/wiki/Mean_squared_error), where we add up the squares of the differences of each output, and the ideal output they should have. We then, for now,
consider the average cost over all training examples.

### What is gradient descent?
The process we use to tell the network how to change it's parameters is called gradient descent, where we calculate the vector of what the downhill direction is and how steep it is[^4].
The process of gradient descent is the idea of finding the local minimum of a function, by using the negative gradient of the current value as an indication of where and how much to step, and using
a learning rate to limit how far we can step in one go (this prevents overfitting and the diverging of the gradient descent). Note that in order for gradient descent to occur, we need a smooth output!

The algorithm we use for computing this efficiently is called backpropagation, which we'll talk about soon. We now can also change our definition of how a network learns. The process of learning for a network
is minimising it's cost function.

### We now have three functions
You'll notice now that we have three key functions for the operation of our neural network:
- The neural network itself,
- The cost function,
- The function to calculate the gradient of said cost function.

## What is backpropagation really doing?
### Notes on weights and biases
As described previously, we want the negative gradient of the cost function, so that we may change the weights and biases to minimize the cost function. This process is called backpropagation.
Imagine a vector:

Insert maths here,

The magnitude of each component represents how sensitive the cost function is to changes in the weights and values. For each neuron, we have that
- bias, which influences which neurons we want to fire the most, or indicate those which do already,
- weights, where neurons with the biggest impact on our results have the biggest weight,
- previous activations, which influence directly how active subsequent neurons will be

all influence the activation function's output. Remember, we want, if for example we gave the network an image of a 2, for it to be very active with the "2" neuron, and inactive everywhere else in the
last layer. Of course, however, the activation of our "2" neuron is dependent on the weights and biases of the $2^{\text{nd}}$ to last layer. This is the key idea we need to understand backpropagation!

### Backpropagation

Backpropagaption uses this key idea, by adding together the desired changes, we get a list of changes for our neurons for our $2^{\text{nd}}$ to last layer. We can then recursively apply this approach
to the relevant weights and biases that determine those values, moving backward throughout the network! We, in theory[^5] at least, repeat this process for all training examples and average together
the desired changes to each weight and bias, which is an approximation of our negative gradient of the cost function referred to in the previous section.

### Summary
In summary, we have that backpropagation is the algorithm responsible for determining how a single training example would like to nudge the weights and biases, which is done to minimize the cost.
We do this in practice using stochastic gradient descent, which is the process of splitting our data into mini-batches, and computing each step with respect to a mini-batch. Repeatedly going through
mini-batches and making adjustments, we converge to a local minimum of the cost function, which is how our network learns!

[^1]: Note that in industry we don't use sigmoids, but rather we use [ReLUs](https://en.wikipedia.org/wiki/Rectifier_(neural_networks)), since they are far easier to train.

[^2]: I believe this is the same as the neuron's [activation function](https://en.wikipedia.org/wiki/Rectifier_(neural_networks)).

[^3]: In deep learning, we usually refer to three sets of data:
      - Training sets: The set we actually use for training the data,
      - Validation set: A set to test the model on data it hasn't actually seen. This is required to prevent overfitting of parameters (weights),
      - Test set: A set hidden from the creator, which is used to ensure there isn't overfitting of hyperparameters (choice of learning rate, etc...)

[^4]: See multivariable analysis for more information!

[^5]: In practice, it is too inefficient to do this, so instead we:
    - Randomly shuffle our training data, and divide it into mini-batches of $x$ training samples.
    - We compute the gradient descent using backpropagation, according to our mini-batches,
    This process, known as stochastic gradient descent, is far faster.
