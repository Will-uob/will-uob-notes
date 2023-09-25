---
title: What is attention?
date: 2023-09-25
published: true
tags: AI ML
---

# What is attention?
## What are encoders and decoders?
Sequence-to-sequence models have achieved a lot of success in areas such as translation, summarization
and image captioning. Under the hood of a sequence-to-sequence model is an **encoder** and a
**decoder**.

![The encoder and decoder](https://jalammar.github.io/images/seq2seq_3.mp4)

The encoder iterates of the input sequence, compiling the information of each element into a vector, called the context. After processing the entire input sequence, the encoder sends this context to the decoder, which produces the output sequence item by item.

The encoder and decoder tend to be RNNs. By design, these RNNs take two inputs at each time step: an
input, and a hidden state from the previous calculation. For example, in a machine translation model, the word needs to be represented by a vector. To transform it, we use [word embedding](https://machinelearningmastery.com/what-are-word-embeddings/) algorithms. These turn words into vector spaces that capture a lot of the meaning/semantic information of the words.

## How Recurrent Neural Network are involved
Both the encoder and decoder are both RNNs, and at each time step one of the RNNs does some processing, it updates it hidden state based on its input and previous inputs it has seen.

For example, below is a graphic of the hidden states for the encoder. Notice how the last state
is the context we pass along to the decoder.

![The encoder](https://jalammar.github.io/images/seq2seq_5.mp4)

The decoder also maintains it's hidden state, that it passes from one time step to the next. It's in
an "unrolled view", which means we show a copy of the encoder and decoder for each step.

![The encoder and decoder working together](https://jalammar.github.io/images/seq2seq_6.mp4)

## Let's pay attention
It turns out the context vector was the bottleneck for these models. A solution was proposed in the
following papers:
- [2014](https://arxiv.org/abs/1409.0473)
- [2015](https://arxiv.org/abs/1508.04025)

They defined attention, which allows the model to focus on the relevant parts of the input sequence as
needed. An attention model differs from those we've seen so far in two key ways:

First, the encoder passes a lot more data to the decoder. Instead of passing the last hidden state,
it passes all the hidden states to the decoder.

![The process of passing all attention](https://jalammar.github.io/images/seq2seq_7.mp4)

Second, an attention decoder does an extra step before producing it's output. The extra step, done in order to focus on the parts of the input that are, consists of:
1. Looking at the set of encoder hidden states it received, where each hidden state is most associated
   with a certain word in the input sequence,
2. Give each hidden state a score[^1],
3. Multiply each hidden state by its softmaxed score, thus amplifying hidden states with high scores,
   and drowning out hidden states with low scores.

Let's bring it all together:
1. The attention decoder RNN takes in the embedding[^2] of the ```<END>``` token, and an initial decoder
   hidden state.
2. The RNN processes its inputs, producing an output and a new hidden state vector, $h\_4$. The output
   is discarded.
3. Attention Step: We use the encoder hidden states and the $h\_4$ vector to calculate a context
   vector, $C\_4$, for this time step.
4. We concatenate $h\_4$ and $C\_4$ into one vector.
5. We pass this vector through a feedforward neural network[^3].
6. The output of the feedforward neural network indicates the output word of this time step.
7. Repeat for the next time steps.

![The above in action](https://jalammar.github.io/images/attention_tensor_dance.mp4)

The process of aligning words is learned in the training phase. How this is actually done is in the
papers above.

[^1]: How is this scoring achieved?

[^2]: What is embedding? I feel like a broken record.

[^3]: What is that?
