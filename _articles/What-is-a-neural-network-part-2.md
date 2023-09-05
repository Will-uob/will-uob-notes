---
published: true
topic: What are Neural Networks?
date: 2023-09-01
tags: AI ML
---

## What is a neural network?
In this article we attempt to understand how the simplest form of neural network, a multi-layer perceptron, works in detail. This is so we may, in the future, tackle harder types of neural networks,
such as [convolutional neural networks](https://en.wikipedia.org/wiki/Convolutional_neural_network) and [LSTMs](https://en.wikipedia.org/wiki/Long_short-term_memory).

### What are neural networks comprised of?
The most important part of a neural network is the neuron. A neuron is something that hold a number, $n \in [0,1]$. We refer to this number, $n$, as the neuron's activation. Everything else that comprises
a neural network is to do with manipulating the activations of neurons so that the neural network can adapt to our task. We then use these neurons to construct layers of neurons. The idea of layers is that,
overtime, each layer will be responsible for detecting and processing different tasks, such as detecting edges and lines in the example we have.

This tutorial focuses on the MNIST dataset, as this is the example 3b1b used, the author who I drew most of this information from. Let's consider a simple network, with:
- one input layer, with each neuron representing a pixel in a 28x28 grid,
- two hidden layers, comprised of 16 neurons each,
- one output layer, comprised on ten nodes, each representing a prediction for one of our handwritten digits.

which is depicted in the following image:

![Image of a neural network](/images/mnist_nn.png)

### Weights and Bias

The question now arises about how we can generate the activations of our neurons such that those in the output layer accurately represent our predictions, that is, how do we link our layers together?
The answer is by using weights and biases, where weights can be visually represented as connections between neurons, and biases a threshold to control whether or not a neuron is "active" (non-zero).
Each neuron in a subsequent layer $K\_{k+1}$ has $n$ weights, where $n$ is the number of neurons in $L\_{k}$.

The activation of a neuron[^2] in a subsequent layer is the defined as $\sigma(w\_1a\_1 + w\_2a\_2 + \dots + w\_na\_n - b)$, where $\sigma$ is a function used to ensure the value of our neuron's activation
is $\in [0,1]$ [^1], and b is our bias for our neuron.

A neural network "learns" by automatically altering the weights and biases of each neuron, which leads to better predictions of data.

#### Notation
Please note we can represent the process of calculating the activations for a subsequent layer using matrix multiplication, that is

$$ \begin{bmatrix} w\_{0,0} & w\_{0,1} & \dots \\\ w\_{1,0} & w\_{1,1} & \dots \\\ \vdots & \ddots & \vdots \\\ w\_{k,0} & \dots & w\_{k, n} \end{bmatrix} \times \begin{bmatrix} a\_0^{(0)} \\\ a\_1^{(0)} \\\ \vdots \\\ a\_n^{(0)} \end{bmatrix} = \begin{bmatrix} a\_0^{(1)} \\\ a\_1^{(1)} \\\ \vdots \\\ b\_n^{(1)} \end{bmatrix} $$

where, for example, $a_0^{(1)} = \sigma(w_{0,0}a_0{(0)} + w_{0, 1}a_1^{(0)} + \dots + w_{0, n}a_n^{(0)} + b_0)$, which can be represented as,

$$ a^{(1)} = (\mathbb{W} a^{(0)} + b) $$

The process of using matrix multiplication for this task is far more efficient that if we were to do the multiplication in the traditional way.
### Neurons as functions

A neuron can be viewed as a function, in fact as it's own [linear regression model](https://www.ibm.com/topics/linear-regression), as it takes all the ouputs of the previous layer's neurons and
returns an activation value, $n \in [0,1]$. Indeed, we can view the entire neural network as a single function, $f$, where

$$f(a\_0, a\_1, \dots, a\_{783}) = \begin{pmatrix} y\_0 \\\ y\_1 \\\ \vdots \\\ y\_9 \end{pmatrix}$$,

where we have $n$ activations as outputs and our predictions as outputs.

## How does a neural network learn?
Our goal is to adjust our weights and biases, using labelled training data, to improve our performance on validation / test data. [^3]
In order to go about this process of adjusting our weights and biases, we use a [cost function](https://en.wikipedia.org/wiki/Loss_function), also known as the loss function, which indicates our model's
performance. In this example, we use the [mean squared error](https://en.wikipedia.org/wiki/Mean_squared_error), where we add up the squares of the differences of each output, and the ideal output they should
have. We then, for now, consider the average cost over all training examples. It should be mentioned here that while the model uses the cost function to determine whether it is doing a good job or not, humans
do not. Indeed, we use metrics, such as accuracy, in order to determine whether or not a model is good. This shouldn't be forgotten, because if we use a poor loss function for our network, it is likely that
while the model will think it's doing a good job, it's not actually doing what we told it to do!

### What is gradient descent?
The process we use to minimize our cost function is known as gradient descent [^4]. To explain what gradient descent is, look at the following diagram:

![Picture of gradient descent](/images/gradientdescent.png)

Here, we have a function of two variables, $\theta\_0$ and $\theta\_1$, with the third axis showing the output. In our actual model, we would have as inputs as those we put into our cost function,
and the graph above our inputs the output of our cost function. We then see a line going from our initial point towards a local minimum of the function, in fixed size steps. The path to the local minimum is
determined by the direction and magnitude of the negative of the gradient of steepest ascent for our current values. For more information about gradient descent in practice, see <a class="wiki-link" href="/articles/fastai-summary">here</a>. One question immediately come to mind:

- Why not find the global minimum of our function instead? This is because finding the global minimum computationally less feasible.

The process of using gradient descent to modify our parameters efficiently, so as to minimize the cost function, is know as backpropagation, which we'll cover shortly. However, for now, think about what we're
trying to do here. We have some plane with $n$ axes, with our cost function mapped on another axis. Therefore, the path to the local minimum depends on where we start, i.e the values of our weights and biases.

So, if we create a vector of all our weights and biases, $\vec{\mathbb{W}}$, and a vector which represents the relative changes $- \delta C(\vec{\mathbb{W}})$, then we can add the values of the one to
the other to implement our step towards the local minimum. Furthermore, thinking about this visually, the relative changes of the highest values represent weights and biases with the most impact on the
direction of our step. Please keep these things in mind for the following section.

## What is backpropagation really doing?
### The 2 example
As described previously, we want to use backpropagation in order to simulate performing gradient descent on our loss function, in order to minimize it's value. That is, we want backpropagation to calculate all
of our weights' and biases' negative gradients, so that we can efficiently decrease the cost function. In the video, he uses 2 as input and describes how we can minimize the cost function for this output.
We consider the three factors responsible for a neuron's activation:

- bias,
- weights, where weights will have differing levels of influence, based on the neuron they stem from.
  If you increase the weight from a brighter neuron to the "2" neuron, it has a greater effect on the cost function. [^6]
- previous layer's activations, which influence directly the activation of subsequent neurons. For
  example, if neurons with negative weights to the "2" neuron had smaller activations, and visa versa for positive weights,
  then we'd increase the activation of our "2" neuron.

Note that when considering these factors, we want the most bang-for-our-buck with these changes. So, we would increase our weights relative to the activation it's attached to, or change the activation of
a neuron in proportion to the strength of it's weight to another. Below is a graphic illustrating what we mean by relative increases and decreases.

![Image of backpropagation](/images/backpropagation.png)

### The bigger picture
We continue to consider the 2 example. There are two still two things to consider:
- What about other predictions? How should we alter the network so that other predictions are less active when given a 2 as input?
- What about the other layers in the neural network? How do we go about changing their weights and biases?

This is where the idea of propagating backwards comes in. For each node in the last layer, we add together the desired effects to the second to last layer. This gives us a vector of values which we'll
use to improve the $2^{\text{nd}}$ to last layer. We then recursively apply this process for all the layers in the neural network, altering the weights and biases of all our neurons, so that we can minimize
the loss function.

However, all this was just for one training example. We do this backpropagation routine for every other training example, recording the desired changes to the weights and biases, and average these together.
This collection of averages is an approximation of the negative gradient of the cost function, $\eta \delta C(w\_1, w\_2, \dots, w\_n)$.

### Mini-batches and Stochastic Gradient Descent
In practice, adding up the influence of every single training example is very time intensive for every single gradient descent step. So, we use the following procedure:
- We randomly shuffle our training data, and divide it into mini-batches of size $x$,
- We then compute a gradient descent step, with the aid of backpropagation, according to the mini-batch,

This procedure is known as stochastic gradient descent, which is significantly faster than regular gradient descent.

[^1]: Note that in industry we don't use sigmoids, but rather we use [ReLUs](https://en.wikipedia.org/wiki/Rectifier_(neural_networks)), since they are far easier to train.

[^2]: I believe this is the same as the neuron's [activation function](https://en.wikipedia.org/wiki/Rectifier_(neural_networks)).

[^3]: In deep learning, we usually refer to three sets of data:
      - Training sets: The set we actually use for training the data,
      - Validation set: A set to test the model on data it hasn't actually seen. This is required to prevent overfitting of parameters (weights),
      - Test set: A set hidden from the creator, which is used to ensure there isn't overfitting of hyperparameters (choice of learning rate, etc...)

[^4]: See multivariable analysis for more information!

[^5]: At least, that is my understanding at the moment, I will make sure in a bit.

[^6]: This is reminiscent of [Hebbian](https://en.wikipedia.org/wiki/Hebbian_theory)

[^7]: In practice, it is too inefficient to do this, so instead we:
    - Randomly shuffle our training data, and divide it into mini-batches of $x$ training samples.
    - We compute the gradient descent using backpropagation, according to our mini-batches,
    This process, known as stochastic gradient descent, is far faster.
