---
published: true
topic: Installing Gentoo
subtitle: 
date: 2022-10-25
tags: AI ML
---

<br>

# Notes on the first chapter and first lesson for FASTAI course

This will be a summary of the theory and concepts introduced in the first two chapters of the FastBook and FastAI course.

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

Two types of model are introduced in the first chapter, a classification model and a regression model. We also work with a specific architecture, resnet18, since it is the best performance for a simple model.

![Diagram of the model working](/images/modeljargon.png)

### Limitations of a model

There are some fundamental limitations to machine learning:
- A model cannot be created without data,
- A model can only learn to operate on patterns seen in the input data used to train it,
- This learning approach only creates predictions, not recommendations,
- It's not enough to only have examples of input data; we need labels for that data too.

Another limitation is bias, which can create positive feedback loops. For more information see [chapter 3](https://nbviewer.org/github/fastai/fastbook/blob/master/03_ethics.ipynb) of the FastBook.

### Sets of data we often use
Often, we use three distinct subsets of our training data:
- The training set: What the model learns from, what we use to fit the model,
- The validation set: We use this to frequently evaluate our model's effectiveness,
- The test set: We use this to provide an unbiased view of our model.

But why do we need these sets? The training set is, of course, needed, but what about the other two? The validation set is what we use to test for overfitting, that is, our model memorising the labels of items in our dataset.
This implies that the model hasn't fully developed the necessary functionality for our task, and will therefore be ineffective. But what about the test set? Most models go through augmentations of their architectures, modifying
learning rates, data augmentation strategies, and so on. These are known as *hyperparameters*. The problem is that we can overfit these hyperparameters, so we use the test set (which has data unseen even to us) to prevent
subconciously choosing hyperparameters to fit our validation data.

The remaining concepts introduced in this chapter can be introduced in the chapter summary:

Machine learning is a discipline where we allow programs to learn, rather than explicitly writing them. Deep learning involves using neural networks with multiple layers.

Every model begins with a choice of data and architecture. Most often we require labelled data, as this will inform the model of what the data is, allowing it to learn. An architecture is a template for a model.
To train a model, we find a set of parameter values (weights) that specialise the architecture for our data. In order to define how well our model performs for a single prediction, we use a loss function.

We may make training faster using pretrained models, which has been trained on someone else's data. We adapt this pretrained model to our data using fine-tuning.