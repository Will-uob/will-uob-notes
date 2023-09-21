---
published: true
topic: What are Decision Trees?
subtitle:
date: 2023-08-30
tags: AI trees
---

## What is a decision tree?

A binary tree which recursively splits the data set until we are left with pure leaf nodes. This is the ideal. However, usually our leaf nodes are not 100% pure, so we use a majority vote.
We choose our optimal split based on maximising information gain.

Insert picture here

### How do we assess our information gain?

We measure it using entropy, a measure of information in a state. When our entropy is high, we have a high level of uncertainty.

Insert entropy formula here

In order to find the information gain for a specific split, we must subtract the combined entropy of the child nodes from those of the parents.

Insert formula here

## What is a Random Forest?
A random forest is a collection of multiple random decision trees, and is much less sensitive to the training data. We use them instead of decision trees because of the latter's sensitivity to training data,
which could result in high variance of outcomes.

We create a random forest using the following protocol:
- Build new dataset from the original. This is done with random sampling + replacement[^1],
- Train a decision tree on each of the bootstrapped datasets independently[^2],
- Combine our predictions[^3] and make a decision based on majority voting.

### Other important points
- Bootstrapping allows our model to be less sensitive to the original training data,
- Random feature selection helps to reduce correlation between the trees,
- Some trees will be trained on less important features, and give bad predictions,
  but the opposite is also true, so it balances out
- We consider the log or sqrt of the total number of factors for the number of features.


[^1]: This is referred to as bootstrapping.

[^2]: Note the we randomly select a subset of features for each tree.

[^3]: Combining our predictions is known as aggregation.
