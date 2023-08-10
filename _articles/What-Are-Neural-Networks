---
published: true
topic: What are Neural Networks?
subtitle: 
date: 2023-08-09
tags: AI ML FastAI
---
# Neural Networks
### What is a neural network?
[Neural Networks](https://www.ibm.com/topics/neural-networks) are a subset of machine learning,
and at the heart of deep learning algorithms. They are comprised of node layers, containing an
input layer, one or more hidden layers, and an output layer. Each node connects to another, and
has an associated weight and threshold.

If the ouput of any node is above the specified threshold value, that node is activated, sending data
to the next layer of the network.

### How do neural networks work?
Each individual node is it's own [linear regression](https://www.ibm.com/topics/linear-regression)
model, a model that describes the relationship between a dependent variable and one or more
independent variables, which has inputs, weights, bias and an output.

Once an input layer is determined, weights are assigned. All inputs are then multiplied by their
respective weights and summed. Afterwards, the output is passed through an activation function,
which determines the output. If that output exceeds a threshold, it fires, passing on data to
the next layer in the network. This results in the output of one node becoming in the input of
the next node.

An example in the article used [perceptrons](https://en.wikipedia.org/wiki/Perceptron), but neural
networks leverage [sigmoid](https://en.wikipedia.org/wiki/Sigmoid_function) neurons. For more
practical applications, we leverage supervised learning to train the algorithm.

When training, we want to evalutate the accuracy using a loss function. Ultimately, the goal is
to minimize our cost function to ensure correctness of fit for any given observation. The process of
adjusting weights to meet this goal is called gradient descent. See [this](https://developer.ibm.com/articles/l-neural/?_gl=1*13r22ru*_ga*MjQyNDQ3MTk5LjE2ODg5NzY5ODQ.*_ga_FYECCCS21D*MTY5MTU2MDkxNi4yLjEuMTY5MTU2MTg5Ny4wLjAuMA..) article for more information.