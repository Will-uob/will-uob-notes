---
title: 2MVAa
date: 2023-09-24
published: true
tags: Maths Analysis
---

# 2MVAa: Multivariable and Vector Analysis 1
The following is a breakdown of my lecture notes for my course on multivariable and vector analysis.
This won't include many examples, since these are in the notes, and in my copy of Calculus: A complete
course.

## Differential Calculus of multivariable functions
### What is a multi-variable function?
A function is a rule that assigns each element in a domain $D$ to exactly one element in a codomain $C$.

A function of single variable: $f: D \subseteq \mathbb{R} \space \rightarrow \space C \subseteq \mathbb{R}$.

A function $f$ of $n$ variables, for $n \subseteq \mathbb{N}$, is denoted:

$$
f: D \subseteq \mathbb{R}^n \rightarrow C \subseteq \mathbb{R}.
$$

which can be shortened to $f: \mathbb{R}^n \rightarrow \mathbb{R}$.

### What is the graph of a multivariable function?
We take the example of a real function of two variables first, $z = f(x,y)$, which is defined as:
$$
z = f(x,y), (x,y) \in D \subseteq \mathbb{R}^2, z \in C \subseteq \mathbb{R}.
$$

### What are vertical sections?
For a function, $z = f(x,y)$, **vertical sections** $z = f(x,c)$ is the intersection of the
surface $z=f(x,y)$ and a vertical plane $y=c$.

### What are level curves?
For a function $c = f(x,y)$, it's the intersection of $z = f(x,y)$, the surface, and a horizontal plane
$z = c$.

### What are partial derivatives?
#### What is the derivative of a single variable function?
The derivative of $y=f(x)$ at $x=a$ is defined as
$$
\frac{d}{dx}f(a) = \lim\_{\delta x \rightarrow 0} \frac{f(a + \delta x) - f(a)}{\delta x}
$$

where $f_{x}(a)$ is the slope of the tangent of the curve at $x=a$, and

$$
\frac{d}{dx} f(a) = \tan{\alpha}.
$$

#### What is a partial derivative?
