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


Stable diffusion can be described as Denoising Diffusion Probabilistic Models, DDPMs, score-based generative models, or simply autoencoders. In the first article, they cover the original paper, implementing it
in PyTorch. There are multiple perspectives[^1] on diffusion models. In the first article, they use the discrete-time (latent variable model) perspective, but check out the others as well. Note that in this
article I'm primarily intrested in summarising the ideas and theoretical side of stable diffusion, to see the code, go onto my Kaggle or Google Colab.

## What is a diffusion model.
Like other generative models, such as GANs, VAEs or Normalisng Flows[^2], diffusion models convert noise from some sample data distribution to a data sample. Diffusion models also do this; the network learns
gradually to denoise the data, starting from pure noise.

The setup for a diffusion model is in two parts:
- A fixed forward process $q$, which we define, that gradually adds Gaussian noise[^3] to an image, until you end up with pure noise.
- A learned reverse denoising process $p_{\theta}$, where a neural network is trained to gradually denoise an image starting from pure noise, until you end up with an actual image.

Both processes are indexed by $t$, the time step, for some finite time steps $T$. With $t=0$, you sample a real image from your data distribution, and the forward process samples noise
from a Gaussian distribution at each time step $t$, which is added to the image of the previous timestep. Given a sufficiently large $T$ and well behaved schedule for adding noise at each
time step, you end up with an isotropic Gaussian distribution[^4], at $t=T$ via a gradual process.

## A mathematical viewpoint
Beware! The following is probably going to be very difficult to summarise, though I'll try my best. This also seems to be the most difficult aspect of understanding, the underlying maths behind these
networks seems to be quite advanced sometimes. Also, note that it's going to be very important to revise the normal distribution, since it seems to be coming up everywhere.

Ultimately we need a loss function which our neural network needs to optimize, so let's be a little more formal.

Let \\(q(\mathbf{x}_0)\\) be the real data distribution, say of "real images". We can sample from this distribution to get an image, \\(\mathbf{x}_0 \sim q(\mathbf{x}_0)\\). We define the forward diffusion process \\(q(\mathbf{x}_t | \mathbf{x}_{t-1})\\) which adds Gaussian noise at each time step \\(t\\), according to a known variance schedule \\(0 < \beta_1 < \beta_2 < ... < \beta_T < 1\\) as
$$
q(\mathbf{x}_t | \mathbf{x}_{t-1}) = \mathcal{N}(\mathbf{x}_t; \sqrt{1 - \beta_t} \mathbf{x}_{t-1}, \beta_t \mathbf{I}). 
$$

Recall that a normal distribution (also called Gaussian distribution) is defined by 2 parameters: a mean \\(\mu\\) and a variance \\(\sigma^2 \geq 0\\). Basically, each new (slightly noisier) image at time step \\(t\\) is drawn from a **conditional Gaussian distribution** with \\(\mathbf{\mu}_t = \sqrt{1 - \beta_t} \mathbf{x}_{t-1}\\) and \\(\sigma^2_t = \beta_t\\), which we can do by sampling \\(\mathbf{\epsilon} \sim \mathcal{N}(\mathbf{0}, \mathbf{I})\\) and then setting \\(\mathbf{x}_t = \sqrt{1 - \beta_t} \mathbf{x}_{t-1} +  \sqrt{\beta_t} \mathbf{\epsilon}\\). 

Note that the \\(\beta_t\\) aren't constant at each time step \\(t\\) (hence the subscript) --- in fact one defines a so-called **"variance schedule"**, which can be linear, quadratic, cosine, etc. as we will see further (a bit like a learning rate schedule). 

So starting from \\(\mathbf{x}_0\\), we end up with \\(\mathbf{x}_1,  ..., \mathbf{x}_t, ..., \mathbf{x}_T\\), where \\(\mathbf{x}_T\\) is pure Gaussian noise if we set the schedule appropriately.

Now, if we knew the conditional distribution \\(p(\mathbf{x}_{t-1} | \mathbf{x}_t)\\), then we could run the process in reverse: by sampling some random Gaussian noise \\(\mathbf{x}_T\\), and then gradually "denoise" it so that we end up with a sample from the real distribution \\(\mathbf{x}_0\\).

However, we don't know \\(p(\mathbf{x}_{t-1} | \mathbf{x}_t)\\). It's intractable since it requires knowing the distribution of all possible images in order to calculate this conditional probability. Hence, we're going to leverage a neural network to **approximate (learn) this conditional probability distribution**, let's call it \\(p_\theta (\mathbf{x}_{t-1} | \mathbf{x}_t)\\), with \\(\theta\\) being the parameters of the neural network, updated by gradient descent. 

Ok, so we need a neural network to represent a (conditional) probability distribution of the backward process. If we assume this reverse process is Gaussian as well, then recall that any Gaussian distribution is defined by 2 parameters:
* a mean parametrized by \\(\mu_\theta\\);
* a variance parametrized by \\(\Sigma_\theta\\);

so we can parametrize the process as 
$$ p_\theta (\mathbf{x}_{t-1} | \mathbf{x}_t) = \mathcal{N}(\mathbf{x}_{t-1}; \mu_\theta(\mathbf{x}_{t},t), \Sigma_\theta (\mathbf{x}_{t},t))$$
where the mean and variance are also conditioned on the noise level \\(t\\).

Hence, our neural network needs to learn/represent the mean and variance. However, the DDPM authors decided to **keep the variance fixed, and let the neural network only learn (represent) the mean \\(\mu_\theta\\) of this conditional probability distribution**. From the paper:

> First, we set \\(\Sigma_\theta ( \mathbf{x}_t, t) = \sigma^2_t \mathbf{I}\\) to untrained time dependent constants. Experimentally, both \\(\sigma^2_t = \beta_t\\) and \\(\sigma^2_t  = \tilde{\beta}_t\\) (see paper) had similar results. 

This was then later improved in the [Improved diffusion models](https://openreview.net/pdf?id=-NEXDKk8gZ) paper, where a neural network also learns the variance of this backwards process, besides the mean.

So we continue, assuming that our neural network only needs to learn/represent the mean of this conditional probability distribution.


[^1]: See the others, they could be useful.

[^2]: Ok, so it seems that there are multiple types of models in deep learning. I wonder what Perceptrons, CNNs and LSTSs are?

[^3]: What the hell is Gaussian noise?

[^4]: This seems to be a key point, since it links to another article.
