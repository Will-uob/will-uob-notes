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
For a function, $z = f(x,y)$, the **vertical sections** are when we fix the value of either the
$x$ or $y$ variable. 

More specifically, $z = f(x,c)$ is the intersection of the surface $z=f(x,y)$ and a vertical plane 
$y=c$, and $z = f(c, y)$ is the intersection of the surface $z=f(x,y)$ and a vertical plane $x=c$.

### What are level curves?

For a function $z = f(x,y)$, the **level curves** are when we fix the value of $z$.

More specifically, the function $c = f(x,y)$, is the intersection of $z = f(x,y)$, the surface, and 
a horizontal plane $z = c$.

### What are partial derivatives?
#### What is the derivative of a single variable function?
The derivative of $y=f(x)$ at $x=a$ is defined as
$$
\frac{d}{dx}f(a) = \lim\_{\Delta x \rightarrow 0} \frac{f(a + \Delta x) - f(a)}{\Delta x}
$$

where $f_{x}(a)$ is the slope of the tangent of the curve at $x=a$, and

$$
\frac{d}{dx} f(a) = \tan{\alpha}.
$$

#### What is a partial derivative?
For the function $z = f(x,y)$, let $y=b$, where $b \in \mathbb{R}$. Since $z=f(x,b)$ is the intersection
of the surface $z=f(x,y)$ and $y=b$, we can calculate the slope of the tangent to the intersection
curve $z=f(x,b)$ at $(a,b)$. That is,
$$
\left. \frac{d}{dx} f(x,b) \right\|\_{x=a} = \lim\_{\Delta x \rightarrow 0} \frac{f(a+\Delta x, b) - f(a,b){\Delta x}}.
$$

This limit reflects how $f(x,y)$ changes with $x$ at $(a,b)$, while y is fixed. It is the **partial derivative** of $f$ with respect to $x$ at the point $(a,b)$, denoted:

$$
\frac{\partial f(a, b)}{\partial x} \equiv \lim\_{\Delta x \rightarrow 0} \frac{f(a+\Delta x, b) - f(a,b){\Delta x}} = \left. \frac{d f(x,b)}{dx} \right\|\_{x=a}.
$$

### Linearity, product and quotient rules
