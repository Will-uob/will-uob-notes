---
subtitle:
date: 2022-02-02
tags: AI ML 
---
# Notes on the "Linear model and neurel net from scratch" [notebook](https://www.kaggle.com/code/jhoward/linear-model-and-neural-net-from-scratch)
I'm focusing more on the key concepts than the coding itself, as this can be seen in the notebook
itself.
### Tabular data, we must clean the data!
We want to be able to multiply each column by some coefficients, but in certain columns there are
NaN values, which is how Pandas refers to missing values. We can't multiply something by a missing
value!

We check the columns for ```NaN``` values using ```isna()```[^1] from Pandas. We then replace
these ```NaN``` values. The values we choose generally don't matter much, but often we use the mode.

We can then summarise the numeric columns in the dataset using Numpy. Certain fields are long tail
distributed, meaning that we may fall into problems, due to that column being multiplied by a
coefficient later. We can visualise this using a [histogram](https://chartio.com/learn/charts/histogram-complete-guide/).

We can fix this problem by taking the logarithm of our values in this field, though be careful for
any errors resulting from the definition of the log function![^2]

Next, we must convert non-numeric columns in the dataset. We do this by creating new columns
containing dummy variables, which contains a 1 where a particular column contains a particular value
and 0 otherwise. Pandas can do this automatically using ```get_dummies```, which also removes the
original columns.

We can now create our matrix of independent and vector of dependent variables, which both need to be
stored in tensors. Our dependent variable is ```Survived```, while our independent variables are all
the continuous and dummy variables.

### Setting up a linear model
We can now work on calculating our predictions and our loss. We first pick random numbers in
```(-0.5, 0.5)```, which will act as coefficients for each column of our independent matrix.

We then calculate our predictions using ```t_indep * coeffs```, where ```t_indep``` is our
tensor of independent variables.[^3]

However, one problem that arises is that the sums of each row will be dominated by ```Age```, since
it's bigger than the rest. So, we force all columns to be in the range ```[0, 1]``` by dividing
them by their maximums.[^4]

Now, we need a loss function. We'll choose the average error of the rows to be our metric.

### Doing a gradient descent step
We get PyTorch to calculate our gradients using ```requires_grad_()``` on our coeffs. We
then calculate our loss, so we'll be able to get our gradients after using ```backward()```.[^5]

### Training the linear model
Before beginning, we create a validation set using fastai's ```Random Splitter```.
We then create methods for updating our coefficients, as well as doing one full gradient descent and
creating intial coefficients.

We then put these into a new function, ```train_model```, which goes as follows:
```
def train_model(epochs=30, lr=0.01):
    torch.manual_seed(442)
    coeffs = init_coeffs()
    for i in range(epochs): one_epoch(coeffs, lr=lr)
    return coeffs
```

### Measuring accuracy
We first see how accurate we were on the validation set, by calculating ```preds = calc_preds(coeffs, val_indep)```. We assume that a score over 0.5 is predicted to survive, and we then calculate our mean
accurary. We then create our accuracy function based on this.

However, there is one serious problem, our predictions aren't restricted to the domain [0, 1]. To
fix this, we use the sigmoid function on our predicted values.

The rest up to creating our neural network is simply making the code neater and more concise.

### A neural network
First, we need to create coefficients for each of our layers, where each layer takes in ```n_coeff```
and creates ```n_hidden``` outputs. They start with one layer and then go into "deep learning" with
multiple layers.

The key steps to creating a neural net are the two matrix products, ```indeps@l1``` and ```res@l2```.
The first layer output is passed to ```F.relu```, our non-linearity, and the second to sigmoid like
before. 


[^1] By the way, it's often a good idea to research an unknown function before using it.
[^2] To get more information about your dataset, it's helpful to use the describe method from
     pandas and to look at the Data Dictionary for your project!
[^3] The author pointed out that we don't need to add a bias term, because our dummy variables
     already cover the entire dataset.
[^4] In the notebook, he talks about how we used broadcasting to achieve this aim.
[^5] Note that when ```backward``` is called, it adds the calculated gradients to the .grad attribute,
     so this attribute must be set back to zero each time!

