---
published: true
topic: What is collaborative filtering?
subtitle:
date: 2023-08-30
tags: ML AI fastai
---

# What is collaborative filtering?
In my own words, collaborative filtering is using machine learning to provide recommendations. For
example, we could have a movie recommendation system, like Netflix.

### The data
Always read the dataset description before working on it! This seems to crop up again and again, so
I'll also mention it here. Furthermore, the author introduces the concept of latent factors for each
user and film, as well as using the dot product to calculate how good a match they are.

### What are latent factors?
To create our latent factors we follow the following protocol:
1. Randomly initialize some parameters, 
2. Calculate our predictions, using the dot product,
3. Calculate our loss, we'll use the MSE for now.

We can the optimize our parameters using stochastic gradient descent.

### Dataloaders and Embedding
While creading our dataloaders object we stumble upon a problem. We can't just use the crosstab representation directly! 
We therefore represent our latent factors as simple matrices, with the dimensions of the classes ```user``` and ```movie```, and the number of factors.

We then, however, stumble upon ***another*** problem, that is that we cannot just directly index our values, since our deep learning models don't know how. The solution to this
is to use one-hot-encoded vectors, which we use to index the target (embedding) matrix using matrix multiplication! This would be fine, but is very time consuming and memory costly. Hence, we
use a technique called embedding, which is doing one-hot-encoded matrix multiplication, but with a computational shortcut so it can be implemented directly.

For example, the ```nn.Embedding``` layer is a simple lookup table that maps an index value to a weight matrix of a certain dimension. 

### How do we decide upon our latent factors?
We don't, we let our model learn them! This is what embeddings are. We will attribute to each of our users and each of our movies a random vector of a certain length (here, n_factors=5), 
and we will make those learnable parameters. That means that at each step, when we compute the loss by comparing our predictions to our targets, we will compute the gradients of the loss
with respect to those embedding vectors and update them with the rules of SGD (or another optimizer).

### Creating the model
Note that creating a new PyTorch module requires inheriting the ```Module``` superclass. Further, note that when your module is called, a method called ```forward```` is called, and the module will
pass along any passed parameters to it. For example, in our code we have the following module:

```
class DotProduct(Module):
    def __init__(self, n_users, n_movies, n_factors):
        self.user_factors = Embedding(n_users, n_factors) # What is Embedding? https://pytorch.org/docs/stable/generated/torch.nn.Embedding.html
        self.movie_factors = Embedding(n_movies, n_factors)
        
    def forward(self, x):
        users = self.user_factors(x[:,0]) # First column, user ids
        movies = self.movie_factors(x[:,1]) # Second column, movie ids
        return (users * movies).sum(dim=1)
```

We then add other features, such as:
- Using the sigmoid function to restrict our predictions to between 0 and 5.5
- Adding bias, so there is also an objective sense of how good a movie is, regardless of how closely it fits to the user

### Weight decay
In the last example, the validation stops improving half-way through and then gets worse. This implies **overfitting**. A potential solution is to use another regularization technique, known as
weight decay, where we add to our loss function the sum of all our weights squared. We do this so that when computing our gradients, it adds a contribution to them that encourages our weights
to be as small as possible.

Put a parabola here!

The idea behind this is that the larger the weights, the sharper the curves they'll create in an increasingly complex graph, leading to overfitting. Limiting our weights will hinder the training of the
model, but will yield a better outcome.

### Interpreting Embeddings and Biases
It's easy to interpret biases. For example, if we see the movies with the lowest bias, they are
all terrible, and visa versa.

It is, however, more difficult to interpret the embedding matrices. However, we can pull out the
most important directions in such a matrix, using principal component analysis.

### Embedding Distance
If two movies are nearly identical, their embedding vectors would also be so. Hence, we can
see the similarity of movies by using Pythagoras's theorem to calculate the distance between
them in n-dimensional space.

### Bootstrapping a Collaborative Filtering model
What if you have no history, and no users? Even in a better scenario, suppose you have a new user, or a
new product? What then?

Common sense rules in these situations. For example, we could assign the mean of the embeddings, or
to pick a default user with average taste.

Another thing to be wary of, especially in recommendation systems, is a small number of extremely
enthusiastic users setting the recommendations for your whole user base. For example, anime watchers!

We should always keep in mind that these feedback loops are the norm, not the exception, and therefore
we must have methods of dealing with them.

### Deep Learning for Collaborative Filtering
The first step is to take the results of the embedding lookup and concatenate those activations
together, which will give us a matrix we can pass through linear layers and nonlinearities.

We then learn and fine-tune our model like normal.

