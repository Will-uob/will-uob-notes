---
published: true
title: What are convolutions?
date: 2023-09-22
tags: Maths Probability Algorithms
---

# What are convolutions?
In this case we refer to convolutions in the discrete case, though the idea is similar when put into the continuous case. Mathematically, we define a convolution using the following formulae:

$$
(f \ast g)[n] := \sum_{m=-\infty}^{\infty} f[n-m]g[m].
$$

In words, the $n^{\text{th}}$ term of the convolution of two functions, $f$ and $g$, is the sum of the products of $f[n-m]$ and $g[m]$. This isn't very helpful for visualising or understanding why we might want to do this, so let's look at some examples.

### Example one: Convolutions in probability
Suppose we have two, fair, six-sided dice, and wish to calculate the probability of a certain combination of sums appearing. We all know the general method for this, which is to draw out a six-by-six grid,
and then using that figure out our probabilies. For notation, we call our dice $D\_1$ and $D\_2$, and their faces $(a\_i)$ and $(b\_i)$ respectively, for $i = \{1, 2, 3, 4, 5, 6 \}$.

![Image of the setup for dice](https://bestcase.files.wordpress.com/2011/01/dicediagram.jpg)

However, I propose another way of looking at this setup, which kind of looks like a sliding windows problem. Arrange one line of six boxes in increasing order, and the other in decreasing order, starting so that
the first dice of the top row is allinged with the last dice of the second. In this way, we immediately see that $P(D\_1 + D\_2 = 2) = a\_1 \cdot b\_1 = \frac{1}{36}$. Then, we slide the bottom window to the
right, and we can see that $P(D\_1 + D\_2 = 3) = a\_1 \cdot b\_2 + a\_2 \dot b\_1$. We continue in this manner to find our probabilities, which are in fact the $n^{\text{th}}$ terms of the convolutions of the
probabilities represented by the lists $(a\_i)$ and $(b\_i)$. For example, below shows the process
for calculating the probability of $P(D\_1 + D\_2 = 4)$.

![Amazing gif which illustrates what I mean](https://i.stack.imgur.com/rXTbw.gif)

### Example two: Mean blur and gaussian blur
In order to apply filters, such as blurring, we often use something called a kernel convolution. That is, we choose a matrix of size $n \times n$, with preselected values or random ones, and then take this grid
and pass it over the whole image, transforming it. The mean blur would use a kernel convolution consisting of $1$s, while a gaussian blur would use a kernel whose values have been sample like a Gaussian
distribution. The image below shows the Gaussian blur being applied to an image. As you can see, we can think of each element of the new image as the $n^{\text{th}}$ term of the convolution between the kernel
and the image, with some exceptions being made for the corners, which can be solved in a variety of ways.

![Image of the Gaussian blur](https://hackaday.com/wp-content/uploads/2021/06/gaussblurkernal-1.jpg)

### A brief mention of the FFT algorithm
The normal way of calculating a convolution is $O(n^2)$, which is not very efficient. Instead of this method, we can using Fourier transforms and the FFT algorithm to calculate the convolution using only
$O(N log(N))$ operations.

### Additional resources
The resources I used to write this were primarily:
- [This](https://www.youtube.com/watch?v=KuXjwB4LzSA&t=346s) video by 3b1b.
- [This](https://www.youtube.com/watch?v=C_zFhWdM4ic&t=0s) video by Computerphile.
