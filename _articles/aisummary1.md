---
published: true
topic: Installing Gentoo
subtitle: 
date: 2022-10-25
tags: AI, ML
---

<br>

# Notes on the first chapter and first lesson for FASTAI course

## The theory

### What is machine learning? What is a neural network?

Machine learning is allowing a computer to learn from experience, rather than explicitly telling it what to do. 

For machine learning, we need four key properties:
 - The idea of weight assignment,
 - The fact that every weight assignment has some 'actual performance',
 - The requirement that there be an "automatic means" of testing this performance,
 - The need for a "mechanism" for improving the performance by changing the weight assignments,

In order to facilitate these properties for deep learning, we need a neural network.

A neural network, practically, is a function that is so flexible that it could be used to solve any problem, just by varying the weights. This property has been proved by the
universal approximation theorem, and makes neural networks suitable for many kinds of applications in artificial intelligence. In order to adjust these weights, we need to use SGD.
These will be explained in later posts.

The programs we use as neural networks are called models. This leads us to preload some Jargon:
- The blueprint of a **model** is the **architecture**,
- *Weights* are called **parameters**,
- Predictions are calculated from the **independent variable**, data not including labels,
- Results of the model are predictions,
- The measure of **performance** is the **loss**,
- The loss depends not only on the predictions, but also the correct labels.

![Diagram of the model working](/images/modeljargon.png)
