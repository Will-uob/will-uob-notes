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
A function is relation between variables. That is, a rule that assigns each element in a domain $D$ to exactly one element in a codomain $C$.

A function of single variable: $f: D \subseteq \mathbb{R} \space \rightarrow \space C \subseteq \mathbb{R}$.

A function $f$ of $n$ variables, for $n \subseteq \mathbb{N}$, is denoted:

$$
f: D \subseteq \mathbb{R}^n \rightarrow C \subseteq \mathbb{R}.[^1]
$$

which can be shortened to $f: \mathbb{R}^n \rightarrow \mathbb{R}$.

### What is the graph of a multivariable function?
We take the example of a real function of two variables first, $z = f(x,y)$, which is defined as:
$$
z = f(x,y), (x,y) \in D \subseteq \mathbb{R}^2, z \in C \subseteq \mathbb{R}.[^2]
$$

#### Notation
If we want to draw a plane in the XY, XZ and YZ axis respectively, we can denote this as the functions $z=z\_0$, $y=y\_0$ and $x=x\_0$. However, it's common to simply use the notation
$x=x$, $y=y$ and $z=z$ instead.

### What are vertical sections and level curves?
For a function, $z = f(x,y)$, the **vertical sections** are when we fix the value of either the
$x$ or $y$ variable.

More specifically, $z = f(x,c)$ is the intersection of the surface $z=f(x,y)$ and a vertical plane
$y=c$, and $z = f(c, y)$ is the intersection of the surface $z=f(x,y)$ and a vertical plane $x=c$.

For a function $z = f(x,y)$, the **level curves**, also known as **contours** are when we fix the value of $z$.

More specifically, the function $c = f(x,y)$, is the intersection of $z = f(x,y)$, the surface, and
a horizontal plane $z = c$.

The overall term for vertical sections and level curves seems to be a **cross-section**[^3].

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

#### Linearity, product and quotient rules
The rules for a partial derivative of a linear combination of functions, the partial dervivative of
the product of functions, and the partial derivative of the quotient of two functions $u=u(x,y)$
and $v=v(x,y)$ are the same for those in normal differentiation[^4].

#### What about a 3-variable function?

A function $f(x,y,z)$ is said to have a partial derivative to $y$ at the point $(x\_0, y\_0, z\_0)$
if the following limit exists:
$$
\frac{\partial f(x\_0, y\_0, z\_0)}{\partial y} \equiv \lim\_{\Delta y \rightarrow 0} \frac{f(x\_0, y\_0 + \Delta y, z\_0) - f(x\_0, y\_0, z\_0)}{\Delta y}.
$$

When calculating $f\_y$, $x$ and $z$ are treated as constants.

#### Higher order partial derivatives
These work exactly the same as in single-variable differentation, with the same notation, except
using $\partial$ instead of $d$.

Theorem. If partial derivatives concerned are continuous, the mixed derivatives commute to the order
of variables.[^5]

#### Differential functions

[^1]: Question: Are all the functions we deal with in this course bijective functions? I'm assuming so, since he said in lecture a function maps one element in codomain to exactly one in the
      codomain. Did he say for every element in the domain?

[^2]: When asked to draw the surface (graph) of a multivariable function, it's always a good idea to think about how it intersects with the coordinate axis, especially if it's a plane.
      In fact, when talking about level curves and vertical sections, it's often better to consider a surface in terms of the XY, XZ and YZ surfaces, at least that's my impression so far.

[^3]: From this section, please make notes on ellipses, parabola, hyperbola. I have a hunch it's going to come up a lot. Also, what is a contour? What is a contour integral? Christ, I've
      forgotten a lot. XD

[^4]: Be sure to know how to prove these results in both a single variable and multi-variable context.

[^5]: What?
