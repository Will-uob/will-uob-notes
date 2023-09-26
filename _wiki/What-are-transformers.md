---
published: true
title: What are transformers?
date: 2023-09-18
tags: ML AI Transformers
---

# What are transformers?
Transformers, at their core, transform data into a new form, based on context. A transformer consists of two parts:
- An encoder, which works on the input seqeuence, and
- A decoder, which operates on the target output sequence.

They work on sequence-to-sequence learning, a form of [semi-supervised learning](https://machinelearningmastery.com/what-is-semi-supervised-learning/), where we take in a sequence of tokens and produce the next
token in the output sequence. It achieves this by iterating through encoder layers, where the encoder generates encodings, which define which part of the input sequence are relevant to eachother. The encoder
then passes these encodings to the next encoder layer.

The decoder then takes these encodings and uses their derived context to generate the output sequence. Please note that this is not a linear processing of data; transformers use an attention mechanism, which
provide context around items in the input sequence.

## Attention is all you need
This is a summary of this [article](https://arxiv.org/pdf/1706.03762.pdf)[^1].

Recurrent models factor computation along symbol positions of the input and output sequences. Aligning
the positions to steps in computation time, they generate a sequence of hidden states $h\_t$, as a
function of the previous state $h\_{t-1}, and input for position $t$. This leads to a fundamental
constraint of sequential, rather than parallel, computation.

The Transformer is a model architecture eschewing recurrence and instead relying entirely on an
attention mechanism[^2] to draw global dependencies between input and output. This allows for
significantly more parallelization, and is hence far faster.

## [The Illustrated transformer](https://jalammar.github.io/illustrated-transformer/
)

[^1]: To understand the article it's important to know what a recurrent neural network is. A recurrent
      neural network (RNN) is a type of artificial neural network which uses sequential data or time
      series data. The are common in ordinal or temportal problems, like NLP and image captioning.
      They use training data to learn, and are distinguished by their "memory", as they take
      information from prior inputs to influence the current input and output.

[2^]: Memory is attention through time. The concept emerged from problems that deal with time-varying
      data sequences.
