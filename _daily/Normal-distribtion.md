---
published: true
date: 2023-09-10
title: The normal distribution, and it's key properties
tags: Statistics Probability AI
---

# What is the Normal Distribution?
The Normal Distribution, also known as the Gaussian distribution, is a type of continuous probability
distribution[^1] for a real-valued random variable. The general form of its probability density
function[^2] is

$$
f(x) = \frac{1}{\theta \sqrt{2\pi}}e^{\frac{-1}{2}(\frac{x-\mu}{\theta})^2}
$$

The parameter $\mu$ is the mean, otherwise known as the expectation, of the distribution, while
the parameter $\theta$ is its standard deviation[^3]. The variance[^4] of the distribution is
$\theta^2$.

## Definitions for normal distributions
### The standard normal distribution
The simplest case, where $\mu = 0$ and $\theta = 1$, and it's probability density function is

$$
\varphi(z) = \frac{e^{\frac{-z^2}{2}}}{\sqrt{2\pi}}.
$$

The variable, $z$, has a mean of $0$ and a variance and standard deviation of $1$. I'm assuming
the formula corresponds to a certain shape, since they mention inflection points.

### The general normal distribution
Every normal distribution is a version of the standard normal distribution, whose domain has been
streched by a factor $\sigma$, and then translated by $\mu$:

$$ f(x \| \mu, \theta^2) = \frac{1}{\theta}\varphi(\frac{x-\mu}{\theta}) $$

The probability density must be scaled by $\frac{1}{\theta}$ so that the integral[^5] is still $1$.

If we define $Z$ to be a standard normal deviate[^6], then $X = \thetaZ + \mu$ will have a normal
distribution with expected value $\mu$ and standard deviation $\theta$.

### Notation
The standard Gaussian distribution is often denoted as either $\phi$ or $\varphi$. The normal
distribution is often referred to as $N(\mu, \theta^2)$ or $\mathcal{N}(\mu, \theta^2)$.

They then go over alternative parameterizations, cumulative distribution functions and many other
properties, which I don't really need to go over at the moment. But, holy crap, this stuff is
pretty cool to look at. Also, please do a section on the Central Limit Theorem!

### What is an isotropic gaussian?
One where the covariance matrix[^7] is represented by the simplified matrix, $\Sigma = \theta^2 I$.
That is, a multidimensional Gaussian distribution with its variance matrix as an identity matrix
multiplied by the same number on its diagonal. Each dimension can be seen as an independent
one-dimension Gaussian distribution.

Considering the traditional Gaussian distribution,

$$ N(\mu, \Sigma) $$

where $\mu$ is the mean and $\Sigma$ is the covariance matrix. As the number of dimensions grows, $\mu$
will have a linear growth, while $\Sigma$ will have a quadratic growth!

This growth can be very computationally expensive, so we often set $\Sigma = \theta^2 I$, where
$\theta^2 I$ is a scalar variance multiplied by an identiy matrix.

### The database
For the rest of what you'll need to understand stable diffusion, I recommend you to look into
[this](https://datascience.oneoffcoder.com/) article, which seems to be a gold mine for all things
relating to data science.

[^1]: An absolutely continuous probability distribution is a probability distribution on the
      real numbers with uncontably many possible balues, such as a whole interval in the real
      line, and where the probability of any event can be expressed as an integral.

[^2]: A probability density function is a function whose value at any given sample (or point)
      in the sample space can be interpreted as providing a relative likelihood that the value
      of the random variable would be equal to that sample.

[^3]: A standard deviation is a measure of the amount of variation or dispersion of a set of values.
      A low standard deviation indicates that the values tend to be close to the mean.

[^4]: The variance is the squared deviation from the mean of a random variable.

[^5]: An integral is the continuous analog of a sum, which is used to calculate areas, volumes, and
      their generalizations.

[^6]: Is a normally distributed deviate, where a deviate is a particular outcome of a random variable.

[^7]: A covariance matrix is a square matrix giving the covariance between each pair of elements of a
      given random vector.
