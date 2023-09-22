---
date: 18-09-2023
title: What are convolutions and convolutional neural networks
published: true
tags: AI ML ImageNets
---

# What are convolutions and convolutional neural networks?
## What is a convolution?
In this case we refer to convolutions in the discrete case, though the idea is similar when put into the continuous case. Mathematically, we define a convolution using the following formulae:

$$
(f \conv g)(t) := \int_{-\inf}^{\inf} f(\tau)g(t-\tau)d\tau,
$$

or

$$
(f \conv g)[n] := \sum_{m=-\inf}^{\inf} f[n-m]g[m].
$$

We focus, as said, on the latter formula. In words, the $n^{\text{th}}$ term of the convolution of two functions, $f$ and $g$, is the sum of the products of $f(n)$ and $f(n-m)$. This isn't very helpful
for visualising or understanding why we might want to do this, so let's look at some examples.

### Example one: Convolutions in probability
Suppose we have two, fair, six-sided dice, and wish to calculate the probability of a certain combination of sums appearing. We all know the general method for this, which is to draw out a six-by-six grid,
and then using that figure out our probabilies. For notation, we call our dice $D1$ and $D2$, and their faces $(a\_i)$ and $(b\_i)$ respectively, for $i = \{1, 2, 3, 4, 5, 6 \}$.

![Image of the setup for dice](/img/diceprob.png)

However, I propose another way of looking at this setup, which kind of looks like a sliding windows problem. Arrange one line of six boxes in increasing order, and the other in decreasing order, starting so that
the first dice of the top row is allinged with the last dice of the second. In this way, we immediately see that $P(D\_1 + D\_2 = 2) = a\_1 \dot b\_1 = \frac{1}{36}$. Then, we slide the bottom window to the
right, and we can see that $P(D\_1 + D\_2 = 3) = a\_1 \dot b\_2 + a\_2 \dot b\_1$. We continue in this manner to find our probabilities, which are in fact the $n^{\text{th}}$ terms of the convolutions of the
probabilities represented by the lists $(a\_i)$ and $(b\_i)$.

![Amazing gif which illustrates what I mean](https://i.stack.imgur.com/rXTbw.gif)

### Example two: Mean blur and gaussian blur
In order to apply filters, such as blurring, we often use something called a kernel convolution. That is, we choose a matrix of size $n \times n$, with preselected values or random ones, and then take this grid
and pass it over the whole image, transforming it. The mean blur would use a kernel convolution consisting of $1$s, while a gaussian blur would use a kernel whose values have been sample like a Gaussian
distribution. The image below shows the Gaussian blur being applied to an image. As you can see, we can think of each element of the new image as the $n^{\text{th}}$ term of the convolution between the kernel
and the image, with some exceptions being made for the corners, which can be solved in a variety of ways.

![Image of the Gaussian blur](https://hackaday.com/wp-content/uploads/2021/06/gaussblurkernal-1.jpg)

### How it works under the hood, the efficient algorithm for calculating convolutions
The normal way of calculating a convolution is $O(n^2)$, which is not very efficient. Instead of this method, we can using Fourier transforms and the FFT algorithm to calculate the convolution using only
$O(N log(N))$ operations.


## What is a convolutional neural network?
A convolution neural network is, essentially, a combination of a deep neural network, and kernel convolutions.

![Image of a convolutional neural network](https://uploads-ssl.webflow.com/614c82ed388d53640613982e/646218745ba944b514f8d350_lenet%20architecture.webp)

Instead of using neurons, CNNs replace each node with a kernel convolution.

