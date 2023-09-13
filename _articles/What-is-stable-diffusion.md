---
published: true
topic: What is stable diffusion?
date: 2023-09-08
tags: AI ML
---

# What is stable diffusion?
The following are notes taken from the following sources:
- [The Annotated Diffusion Model](https://huggingface.co/blog/annotated-diffusion),
- [Diffusers](https://colab.research.google.com/github/huggingface/notebooks/blob/main/diffusers/diffusers_intro.ipynb),
- The [video](https://www.youtube.com/watch?v=1CIpzeNxIhU) by Computerphile.

## What is a diffusion model.
Like other generative models, such as GANs, VAEs or Normalisng Flows[^1], diffusion models (also known as Denoising Diffusion Probabilistic Models, DDPMs, score-based generative models, or simply
autoencoders) convert noise from some sample data distribution to a data sample. Diffusion models[^2] also do this; the network learns gradually to denoise the data, starting from pure noise.

The setup for a diffusion model is in two parts:
- A fixed forward process $q$, which we define, that gradually adds Gaussian noise[^3] to an image, until you end up with pure noise.
- A learned reverse denoising process $p_{\theta}$, where a neural network is trained to gradually denoise an image starting from pure noise, until you end up with an actual image.

Both processes are indexed by $t$, the time step, for some finite time steps $T$. With $t=0$, you sample a real image from your data distribution, and the forward process samples noise
from a Gaussian distribution at each time step $t$, which is added to the image of the previous timestep. Given a sufficiently large $T$ and well behaved schedule for adding noise at each
time step, you end up with an isotropic Gaussian distribution[^4], at $t=T$ via a gradual process.

## A mathematical viewpoint
Ultimately we need a loss function which our neural network needs to optimize, so let's be a little more formal.

Let $q(\mathbf{x}\_0)$ be the real data distribution. We can sample from this distribution to get an image, $\mathbf{x}\_0 \sim q(\mathbf{x}\_0)$. We define the forward diffusion process
$q(\mathbf{x}\_t | \mathbf{x}\_{t-1})$ which adds Gaussian noise at each time step $t$, according to a known variance schedule $0 < \beta\_1 < \beta\_2 < ... < \beta\_T < 1$ as

$$
q(\mathbf{x}\_t \| \mathbf{x}\_{t-1}) = \mathcal{N}(\mathbf{x}\_t; \sqrt{1 - \beta\_t} \mathbf{x}\_{t-1}, \beta_t \mathbf{I}).
$$ [^5]

Recall that a normal (Gaussian) distribution is defined by 2 parameters: a mean $\mu$ and a variance $\sigma^2 \geq 0$. Basically, each new (slightly noisier) image at time step $t$ is drawn from a
**conditional Gaussian distribution** with $\mathbf{\mu}\_t = \sqrt{1 - \beta\_t} \mathbf{x}\_{t-1}$ and $\sigma^2\_t = \beta\_t$, which we can do by sampling $\mathbf{\epsilon} \sim \mathcal{N}(\mathbf{0}, \mathbf{I})$ and then setting $\mathbf{x}\_t = \sqrt{1 - \beta\_t} \mathbf{x}\_{t-1} +  \sqrt{\beta_t} \mathbf{\epsilon}$.

Note that the $\beta_t$ aren't constant at each time step $t$ (hence the subscript) --- in fact one defines a so-called **"variance schedule"**, which can be linear, quadratic, cosine, etc...

So starting from $\mathbf{x}\_0$, we end up with $\mathbf{x}\_1,  ..., \mathbf{x}\_t, ..., \mathbf{x}\_T$, where $\mathbf{x}_T$ is pure Gaussian noise if we set the schedule appropriately.

Now, if we knew the conditional distribution $p(\mathbf{x}\_{t-1} | \mathbf{x}\_t)$, then we could run the process in reverse: by sampling some random Gaussian noise $\mathbf{x}\_T$, and then
gradually "denoise" it so that we end up with a sample from the real distribution $\mathbf{x}_0$.

However, we don't know $p(\mathbf{x}\_{t-1} | \mathbf{x}\_t)$. It's intractable [^6] since it requires knowing the distribution of all possible images in order to calculate this conditional probability. Hence,
we're going to leverage a neural network to **approximate (learn) this conditional probability distribution**, let's call it $p\_\theta (\mathbf{x}\_{t-1} | \mathbf{x}\_t)$, with $\theta$ being the
parameters of the neural network, updated by gradient descent.

Ok, so we need a neural network to represent a (conditional) probability distribution of the backward process. If we assume this reverse process is Gaussian as well, then recall that any Gaussian distribution
is defined by 2 parameters:
- a mean parametrized by $\mu\_\theta$;
- a variance parametrized by $\Sigma\_\theta$;

so we can parametrize the process as

$$ p\_\theta (\mathbf{x}\_{t-1} \mathbf{x}\_t) = \mathcal{N}(\mathbf{x}\_{t-1}; \mu\_\theta(\mathbf{x}\_{t},t), \Sigma\_\theta (\mathbf{x}_{t},t))$$

where the mean and variance are also conditioned on the noise level $t$.

Hence, our neural network needs to learn/represent the mean and variance. However, the DDPM authors decided to **keep the variance fixed, and let the neural network only learn (represent)
the mean $\mu\_{\theta}$ of this conditional probability distribution**. From the paper:

> First, we set $\Sigma\_\theta ( \mathbf{x}\_t, t) = \sigma^2\_t \mathbf{I}$ to untrained time dependent constants. Experimentally, both $\sigma^2\_t = \beta\_t$ and $\sigma^2\_t  = \tilde{\beta}_t$ (see paper) had similar results.

This was then later improved in the [Improved diffusion models](https://openreview.net/pdf?id=-NEXDKk8gZ) paper, where a neural network also learns the variance of this backwards process, besides the mean.

So we continue, assuming that our neural network only needs to learn/represent the mean of this conditional probability distribution.

## Defining an objective function (by reparametrizing the mean)
To learn the mean of the backward process, the authors observe that the combination of $q$ and $p\_\theta$ can be seen as a variational auto-encoder[^7]. Hence, the [**variational lower bound**](https://xyang35.github.io/2017/04/14/variational-lower-bound/) can be used to minimize the negative log-likelihood[^8] with respect to ground truth data sample **$x_0$**.

The evidence lower bound ([EBLO](https://en.wikipedia.org/wiki/Evidence_lower_bound)) for this process is a sum of losses at each time step $t$, where loss is defined as $L = L\_0 + L\_1 + \dots + L\_T$.
By construction of the forward $q$ process and backward process, each term, with the exception of $L_0$, of the loss is actually a KL divergence[^9] between 2 Gaussian distributions, which we can write
explicitly as an L2-loss with respect to the means!

A direct consequence of the constructed forward process $q$, we can sample **$X_t$** at any arbitrary noise level conditioned on **$X_0$** (since the sums of Gaussians is also Gaussian). As a result, we don't
need to apply $q$ repeatedly in order to sample **$X_t$**. We have that

$$ q(X\_i \| X\_0) = N(X\_t; \sqrt{\bar{\alpha\_t}}X_0, (1-\bar{\alpha\_t})I) $$

with $\alpha\_t := 1-\beta\_t$ and $\bar{\alpha\_t} := \prod\_{s=1}^{t} \alpha\_{s}$. This equation is the "nice property". It means that we can sample Gaussian noise, and scale it appropriatly and add
it to **$X_0$** to get **$X_t$** directly. Also, note that $\bar{\alpha\_t}$ are functions of the
$\beta\_t$ variance schedule, and are thus also known and can be precomputed. This allows us to randomly sample $t$ during training and optimize $L_t$.

Thanks to this property, we can, which is shown in [this](https://lilianweng.github.io/posts/2021-07-11-diffusion-models/) article, **reparametrize the mean to make the neural network learn the added noise**,
via a neural network $\epsilon\_{\theta} \mathbf{x}\_t, t)$, for noise level $t$ in the KL terms which constitute the losses. Hence, our neural network becomes a loss predictor, not a mean predictor.

The mean can be computed as:

$$ \mathbf{\mu}\_\theta(\mathbf{x}\_t, t) = \frac{1}{\sqrt{\alpha\_t}} \left( \mathbf{x}\_t - \frac{\beta\_t}{\sqrt{1- \bar{\alpha}t}} \mathbf{\epsilon}\theta(\mathbf{x}\_t, t) \right)$$

The final objective function $L_t$ for a random time step $t$ is now:

$$ \|\| \mathbf{\epsilon} - \mathbf{\epsilon}\_\theta(\mathbf{x}t, t) {\|\|}^2 = \|\| \mathbf{\epsilon} - \mathbf{\epsilon}\theta( \sqrt{\bar{\alpha}\_t} \mathbf{x}\_0 + \sqrt{(1- \bar{\alpha}\_t) } \mathbf{\epsilon}, t) {\|\|}^2.$$

Here, $\mathbf{x}\_0$ is the initial image, and we see the direct noise level $t$ sample given by the
fixed forward process. $\mathbf{\epsilon}$ is the pure noise sampled at $t$, and $\mathbf{\epsilon}\_\theta (\mathbf{x}\_t, t)$ is our neural network.

The neural network is optimized using a simple mean squared error (MSE) between the true and predicted
Gaussian noise.

Our algorithm is now, in words:
- take a random sample $\mathbf{x}\_0$ from the real unknwn and possibily complex data distribution,
  $q(\mathbf{x}\_0)$,
- we sample a noise level $t$ uniformally between $1$ and $T$,
- we sample some noise from a Gaussian distribution and corrupt the input by this noise at level $t$,
- the neural network is trained to predict this noise based on the corrupted image $\mathbf{x}\_t$.

In reality, this process is done on batched of data, as one uses stochastic gradient descent to optimize
neural networks.

[^1]: Ok, so it seems that there are multiple types of models in deep learning. I wonder what Perceptrons, CNNs and LSTSs are?

[^2]: See the other perspectives from the article later, they could be useful.

[^3]: Gaussian noise is a kind of signal noise (noise referring to random, troublesome, problematic,
      or unwanted signals, where a signal is a function that conveys information about a phenomenon),
      that has a probability density function equal to that of a Gaussian distribution.

[^4]: This seems to be a key point, since it links to another article. To see it's definition, look <a class="wiki-link" href="/articles/normal-distribution">here</a>.

[^5]: <a class="wiki-link" href="/articles/normal-distribution">See here.</a>

[^6]: Intractable problem: fom a computational complexity stance, intractable problems are problems for which there exist no efficient algorithms to solve them.

[^7]: An [autoencoder](https://en.wikipedia.org/wiki/Autoencoder) is a type of artificial neural network used to learn efficient codings of unlabeled data.
      An autoencoder learns two functions: an encoding function that transforms the input data, and a decoding function that recreates the input data from
      the encoded representation. [Variational autoencoders](https://en.wikipedia.org/wiki/Variational_autoencoder), meanwhile, are probabilistic generative
      models that require neural networks as only a part of their overall structure.

[^8]: The negative log-likelihood, indeed pretty much all of the maths in this article, is a subset of [Bayesian Statistics](https://en.wikipedia.org/wiki/Bayesian_statistics), where
      the log-likelihood can be seen in [this](https://en.wikipedia.org/wiki/Likelihood_function#Log-likelihood) article.

[^9]: KL-Divergence, [Kullback–Leibler divergence](https://en.wikipedia.org/wiki/Kullback%E2%80%93Leibler_divergence), is a type of statistical distance: a measure of how one probability distribution
       P is different from a second, reference probability distribution Q. A simple interpretation of the KL divergence of P from Q is the expected excess surprise from using Q as a model when the
       actual distribution is P.
