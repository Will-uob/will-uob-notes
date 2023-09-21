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
