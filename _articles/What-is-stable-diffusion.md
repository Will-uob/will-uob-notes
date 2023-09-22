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

A direct consequence of the constructed forward process $q$, we can sample $\mathbf{x_t}$ at any arbitrary noise level conditioned on $\mathbf{x\_0}$ (since the sums of Gaussians is also Gaussian). As a result, we don't
need to apply $q$ repeatedly in order to sample $\mathbf{x\_t}$. We have that

$$ q(\mathbf{x}\_i \| \mathbf{x}\_0) = N(\mathbf{x}\_t; \sqrt{\bar{\alpha\_t}}X_0, (1-\bar{\alpha\_t})I) $$

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

## The neural network
The following is to be treated as a companion to the code on the [annotated diffusion](https://colab.research.google.com/github/huggingface/notebooks/blob/main/examples/annotated_diffusion.ipynb) jupyter
notebook on Colab. It's mostly going to focus on explaining or linking to places which explain concepts introduced.

The neural network, in practice, takes a image of noise, a tensor, and is supposed to return the predicted amount of noise, another tensor, which are of the same shape. For this problem, we
use a concept similar to that of autoencoders. In autoencoders, there's a "bottleneck" inbetween the encoder and decoder, which forces the network to only keep the most important information
in the bottleneck layer.

The architecture used by the authors is a U-net[^10]. This is important to us because it introduced residual connections[^11] between the encoder and decoder, greatly improving gradient flow[^12].
As can be seen below, the model first downsamples the input, and then upsamples it.

![A picture of a u-net](/images/u-net.png)

## Notes on the implementation
The implementation of stable diffusion has a lot of concepts that I've either not come across, or don't know how to do in PyTorch. So, think of this more of a list of points that I need to work through to
truly appreciate what's going on here. Also, I won't mention any of the PyTorch methods that are seen in the article, since I'm still pretty new to PyTorch as a whole. It'd probably be good for me to take
a tutorial course using it later on.

### Position embeddings
Parameters of the neural network, the noise primarily, are shared across time, so the authors employ sinusoidal position embeddings to encode $t$, inspired by the transformer. The
idea of this is that it makes the neural network "know" at which particular noise level (time step) we're operation on for each batch. From this section, key observations are:
- I need to learn about **convolutions**,
- so that I can learn about **transformers**,
- so that I can learn about **position embeddings**.

Furthermore, I need to learn about residual blocks, which are probably connected to the next section.

### ResNet / ConvNeXT block
These form the core building block of our model. The DDPM authors employed a Wide ResNet block, but Phil Wang added support for a ConvNeXT block. Either can be used for the final U-Net architecture.

Notes from looking at the code:
- What is [group normalization](https://en.wikipedia.org/wiki/Convolutional_neural_network)?
- What is a SiLU?
- What is a [ConvNeXT block](https://arxiv.org/abs/2201.03545)?
- What is a ResNet block?

### Attention module
Attention modules were added in between convolutional blocks by the authors. "Attention is the building block of the famous [Transformer architecture](https://arxiv.org/abs/1706.03762). Phil Wang used
two variants of attention, regular multi-head self-attention (as used in the Transformer), and a [linear attention variant](https://github.com/lucidrains/linear-attention-transformer). The writers of the
article recommend to read [this](https://jalammar.github.io/illustrated-transformer/) to understand more about transformers and attention modules.

### Group normalization
The authors interleave the convolutional/attention layers of the U-Net with [group normalization](https://arxiv.org/abs/1803.08494). The writers of the article then define a ```Prenorm``` class, which
is used to apply groupnorm before the attention layer. However, note there's a [debate](https://tnq177.github.io/data/transformers_without_tears.pdf) about whether to apply normalization before or after
attention in Transformers.

### Conditional U-Net
We've now got the building blocks, so now we can define the whole neural network! Remember, the job of $\epsilon\_{\theta} (\mathbf{x}\_t , t)$ is to take in a batch of noisy images + noise levels, and
output the noise added to the input. More formally, we take in a batch of noisy images of size ```(batch_size, num_channels, height, width)``` as well as a batch of noise levels of size ```(batch_size, 1)```,
and then output a tensor of shape ```batch_size, num_channels, height, width)```.

The network is built up as follows:
- first, a convolutional layer is applied on the batch of noisy images, and position embeddings are computed for the noise levels
- next, a sequence of downsampling stages are applied. Each downsampling stage consists of 2 ResNet/ConvNeXT blocks + groupnorm + attention + residual connection + a downsample operation
  at the middle of the network, again ResNet or ConvNeXT blocks are applied, interleaved with attention
- next, a sequence of upsampling stages are applied. Each upsampling stage consists of 2 ResNet/ConvNeXT blocks + groupnorm + attention + residual connection + an upsample operation
- finally, a ResNet/ConvNeXT block followed by a convolutional layer is applied.

The writers of the article as suggest to read the [following](http://karpathy.github.io/2019/04/25/recipe/), to understand how to best create neural networks.

### Defining the forward process
We define the forward process by gradually adding noise to an image, in a number of time steps $T$, using a **variance schedule**. The original paper used a linear scheduler, but it was
revealed later on that a cosine schedule gave better results. Some key features of these schedulers seem to be:
- cumulative variance variable,
- an ```extract``` function, which allows us to extract the appropriate $t$ index for a batch of indicies,
- converting a PIL image to a tensor, so that we may add noise, using a transform and reverse transform function,

### Define a PyTorch Dataset + DataLoader
Really just read [this](https://pytorch.org/tutorials/beginner/basics/data_tutorial.html) article on PyTorch datasets, and [this](https://huggingface.co/docs/datasets/index) article for how to use the
HuggingFace datasets in the code. The rest is explaned in the Colab document.

### Sampling
The process for sampling is summarised in the following manner:

![Data sampling](/images/sampling.png)

To generate new images from a diffusion model, we reverse the diffusion process: we start from $T$, where we sample pure noise from a Gaussian distribution, and then use our neural network to gradually
denoise it, until $t=0$. Remember, the variance is known ahead of time.

### Train the model and inference
This is done using PyTorch. The training procedure seems to be pretty standard, similar to what was done
using fastai. Question: What is inference?

### Follow up reads
DDPM paper showed that diffusion models are promising for (un)conditional image generation. This has
since been immensely improved, most notably for text-conditional image generation. The following
are some important papers:
- Improved Denoising Diffusion Probabilistic Models [(Nichol et al., 2021)](https://arxiv.org/abs/2102.09672): finds that learning the variance of the conditional distribution (besides the mean) helps in improving performance
- Cascaded Diffusion Models for High Fidelity Image Generation [(Ho et al., 2021)](https://arxiv.org/abs/2106.15282): introduce cascaded diffusion, which comprises a pipeline of multiple diffusion models that generate images of increasing resolution for high-fidelity image synthesis
- Diffusion Models Beat GANs on Image Synthesis [(Dhariwal et al., 2021)](https://arxiv.org/abs/2105.05233): show that diffusion models can achieve image sample quality superior to the current state-of-the-art generative models by improving the U-Net architecture, as well as introducing classifier guidance
- Classifier-Free Diffusion Guidance [(Ho et al., 2021)](https://openreview.net/pdf?id=qw8AKxfYbI): shows that you don't need a classifier for guiding a diffusion model by jointly training a conditional and an unconditional diffusion model with a single neural network
- Hierarchical Text-Conditional Image Generation with CLIP Latents (DALL-E 2) [(Ramesh et al., 2022)](https://cdn.openai.com/papers/dall-e-2.pdf): use a prior to turn a text caption into a CLIP image embedding, after which a diffusion model decodes it into an image
- Photorealistic Text-to-Image Diffusion Models with Deep Language Understanding (ImageGen) [(Saharia et al., 2022)](https://arxiv.org/abs/2205.11487): shows that combining a large pre-trained language model (e.g. T5) with cascaded diffusion works well for text-to-image synthesis


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

[^10]: A [U-net](https://en.wikipedia.org/wiki/U-Net) is a [convolutional neural network](https://en.wikipedia.org/wiki/Convolutional_neural_network) that was developed for biomedical
       image segmentation at the Computer Science Department of the University of Freiburg.

[^11]: What are residual connections?

[^12]: What is gradient flow?
