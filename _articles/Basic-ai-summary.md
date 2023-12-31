---
published: true
topic: Theory of Artificial Intelligence so far
subtitle: 
date: 2023-08-03
tags: AI ML FastAI
---

<br>

This will be a summary of the theory and concepts introduced in the FastBook and FastAI course that I've covered so far. As for the practical, I suggest you visit
my [kaggle](https://www.kaggle.com/williamkasafir) page, where I'll be trying to build projects based on the concepts introduced in the course.

# Notes on the first chapter of the Fastbook
### What is machine learning? What is deep learning?

Machine learning is a discipline where we allow programs to learn, rather than explicitly writing them. Deep learning involves using neural networks with multiple layers.

For machine learning, we need four key properties:
 - The idea of weight assignment,
 - The fact that every weight assignment has some 'actual performance',
 - The requirement that there be an "automatic means" of testing this performance,
 - The need for a "mechanism" for improving the performance by changing the weight assignments,

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

To train a model, we find a set of parameter values (weights) that specialise the architecture for our data. In order to define how well our model performs for a single prediction, we use a loss function.
We may make training faster using pretrained models, which has been trained on someone else's data. We adapt this pretrained model to our data using fine-tuning.

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

A training data set is a data set of examples used during the learning process and is used to fit the parameters. It is the bulk of the data, around 80%.

The validation set is what we use to test for overfitting, that is, our model memorising the labels of items in our dataset. This implies that the model hasn't fully developed the necessary
functionality for our task, and will therefore be ineffective. The validation set as default is 20% of the data.

But what about the test set? Most models go through augmentations of their architectures, modifying learning rates, data augmentation strategies, and so on. These are known as *hyperparameters*.
The problem is that we can overfit these hyperparameters, so we use the test set (which has data unseen even to us) to prevent subconciously choosing hyperparameters to fit our validation data.

# Notes on the second chapter of the Fastbook
### Advice on building projects
Make sure to build your own projects, considering carefully the data avaliability, using end-to-end iterations. Each iteration should see both improvements and shifts in where difficulties lie.
Also, ensure that for beginner projects there already exist examples to learn from. There is also the drivetrain approach, which is described in detail in
["Designing Great Data Products"](https://www.oreilly.com/radar/drivetrain-approach-data-products/).

### Types of deep learning applications
There are many applications, including:
- NLP: Effective for generating, classifying and categorizing texts and documents,
- Images and text: This can be used in many areas, such as generating captions for images,
- Tabular data: In many contexts this may not result in improvement, and generally take longer to train than using random forests or GBM.

### Data Augmentation
Data augmentation is used to reduce overfitting when training a model, by training using slightly-modified copies of existing data. For example, randomly selecting a part of an image, and cropping it,
repating this process every epoch. It's important to note, however, that these methods don't change the meaning of data.

### Confusion Matrices and cleaning data
Show a matrix where the rows are the actual labels and the columns are the predictions, showing where the model went wrong. We can also plot these losses and clean them. For example, an
image prediction model will plot images with the highest loss. The loss in this case is a number that is higher if the model is incorrect and confident, or correct but unconfident.

One of the causes of this might be that the data you have contains data unsuitable for your task. In the example in the book, a bear classifier, some images were of teddy bears, which caused a high loss. In
this case, we unlink these images from the training, validation and data sets.

# Notes on the third chapter of the Fastbook
### Tensors, arrays and their properties
When working with deep learning in Python, we often store our data in either Numpy arrays or PyTorch tensors. Both these data structures possess intresting properties, but it's only worthwhile covering
tensors, as a tensor is acts as a Numpy array with extra restrictions, such as only being able to use simple, basic numeric types. This means that unlike Numpy arrays, tensors cannot be
[jagged](https://en.wikipedia.org/wiki/Jagged_array).

Tensors have many useful features which you'll see in my notebooks, such as stacking, broadcasting, calculating derivatives of operations and working on the GPU. Broadcasting is the automatic expansion
of smaller rank tensors [^1] to have the same size as the other during operations.

### Stochastic Gradient Descent and learning rates

In deep learning we use [SGD](https://realpython.com/gradient-descent-algorithm-python/) and learning rates to update our weights to make them better. The process goes as follows:

1. Initialise the weights, usually randomly,
2. We use these weights to inform our predictions,
3. We calculate our loss, based off our loss function,
4. We calculate our gradient, measures for each weights telling us how changing them would change the loss,
5. We change all of our weights based on step four,
6. We repeat steps 2-5 until we are satisfied.

![Diagram of the above process](/images/UpdateWeights.png)

The process of calculating gradients in PyTorch will be included in the notebooks. However, note two things. First, PyTorch is able to automatically compute the derivative of nearly any function.
Secondly, we need to understand [backpropagation](https://en.wikipedia.org/wiki/Backpropagation), the process of calculating the derivative of each layer.

The learning rate is used in nearly all approaches regarding changing parameters. It involves updating the weights using the operation ``` w -= gradient(w) * lr```. The learning rate is usually a small value,
between 0.1 and 0.001. Please be careful when choosing the learning rate, as choosing a nonoptimal learning rate can lead to many issues[^2].

In summary, our weights can either be randomly chosen or taken from a pretrained model. We then use the loss function to compare predictions to target labels. To improve our loss, we must use calculus to
calculate the gradients of our weights, so we may alter them. The gradient signifies how big a step we must take.

### How does a neural network function?

The practical implementation is covered in the notes, but this section will point to the following article which explains the theory.

# Notes on the fourth chapter of the Fastbook
### The lesson

In this lesson and chapter we discuss Natural Language Processing. In the lesson we use an API called [HuggingFace Transformers](https://huggingface.co/docs/transformers/index).
Transformers are explained in the [following](https://en.wikipedia.org/wiki/Transformer_(machine_learning_model) wiki article. First, a few definitions:

- Jargon: A pre-trained model is a bunch of parameters that have already been fitted, where some will be suitable, but others will need to be fine-tuned [^3] to fit our scenario!
- Jargon: A Recurrent Neural Network (RNN) is a type of artificial neural network which uses sequential data or time series data.

### Important libraries

The most important libraries in the realm of machine learning and deep learning, at least for Python, are Pandas, Numpy, Matplotlib and PyTorch. Tutorials for these can all be found within this
[book](https://wesmckinney.com/book/) suggested by the author. 

### Classification model

In the lesson, the author suggests people intrested in NLP first start with a classification model. In this case, we use the U.S. patent phrase to phrase matching problem, which can be found on Kaggle.
During this, he gives advice with regards to competing in Kaggle competitions, with special emphasis given to reading the competition website!

### How to deal with our data in NLP

Within NLP, our data will be stored as strings in most cases. This is a problem, as neural networks use numbers. We split each string into words using
a [tokenizer](https://en.wikipedia.org/wiki/Lexical_analysis#Tokenization). This, like it always does in CS, leads to issues, such as using pictographic langauages, such as Chinese or Japanese.

There is then the process of converting our tokens into numbers, (numericalisation)[https://www.linkedin.com/pulse/natural-language-processing-tokenization-anshu-sharaf-/]. This has two issues.
First, the bigger the vocabulary a model must deal with, the more space and training data there must be. Second, is that we must decide our model before we implement it, as the model, tokenization
and numericalisation methods must match!

The rest of the non-API related information is quite scattered, so I'll include it in one Q&A

### Q&A
#### How do we detect when overfitting occurs?
We take the original data set and remove 20% of the items within it. We then refit our model, and measure how good it is using the items we removed, our validation set.
We can also consider using [cross-validation](https://www.cs.cmu.edu/~schneide/tut5/node42.html), but we are warned against this by the author. We can also use a test set,
which is used to prevent overfitting of hyperparameters, that is creating a model that is good by coincidence. If your model screws up on the test set, you're back to 0.

#### Metrics and correlation
If we have a validation set, we measure metrics to determine the effectiveness of our model. Please note that metrics /= loss /= accuracy. Also note that the idea of metrics, and determining how
valid a metric actually is, is a massive problem in artificial intelligence. To understand this, consider that 1. [Goodhart's Law](https://en.wikipedia.org/wiki/Goodhart's_law) exists, and 2. that in real
life there isn't usually a metric good enough to use as a metric.

#### Pearson Correlation Coefficients
These are explained practially in the video, but the [theory](https://en.wikipedia.org/wiki/Pearson_correlation_coefficient) is not discussed. It's the most widely used measure of the degree of relationship
between two variables. For example, housing price and the number of rooms. Please note that this kind of analysis is very sensitive to outliers, so it is quite common to limit their impact.

#### How do you decide when it's okay to remove outliers?
Outliers should never just be removed, for modelling purposes. Usually, if outliers are such that they cannot be treated in the same way the rest of the data can, the author splits the data into two
seperate analyses.


[^1]: The rank of a tensor is the number of axes or dimensions in a tensor.
      On a similar note, the shape of a tensor is the size of each axis of a tensor.

[^2]: If the LR is too small, it will take many jumps to reach the optimal weight. If the LR is too big, we have two possibilities. Either:
      a. The weight's value will diverge away from the optimal value,
      b. The weight's value will bounce around the optimal value.

[^3]: In the fine-tuning process, we remove the final layer of the model, which gives the prediction for the label of our data, and stick a new random matrix as the new final layer.


