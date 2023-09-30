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
f: D \subseteq \mathbb{R}^n \rightarrow C \subseteq \mathbb{R}.
$$ [^1]

which can be shortened to $f: \mathbb{R}^n \rightarrow \mathbb{R}$.

#### Example question
Determine the domain $D$ of the function
$$
f = \ln (4-x^2-y^2) + \sqrt{x^2 + 2x + y^2}.
$$

### What is the graph of a multivariable function?
We take the example of a real function of two variables first, $z = f(x,y)$, which is defined as:
$$
z = f(x,y), (x,y) \in D \subseteq \mathbb{R}^2, z \in C \subseteq \mathbb{R}.
$$ [^2]

#### Notation
If we want to draw a plane in the XY, XZ and YZ axis respectively, we can denote this as the functions $z=z\_0$, $y=y\_0$ and $x=x\_0$. However, it's common to simply use the notation
$x=x$, $y=y$ and $z=z$ instead.

#### Example questions
- Sketch a graph for the function, $\ = 1-x-y$.
- Sketch graphs for the functions: $x=x\_0, y=y\_0, z=z\_0$.

### What are vertical sections and level curves?
For a function, $z = f(x,y)$, the **vertical sections** are when we fix the value of either the
$x$ or $y$ variable.

More specifically, $z = f(x,c)$ is the intersection of the surface $z=f(x,y)$ and a vertical plane
$y=c$, and $z = f(c, y)$ is the intersection of the surface $z=f(x,y)$ and a vertical plane $x=c$.

For a function $z = f(x,y)$, the **level curves**, also known as **contours** are when we fix the value of $z$.

More specifically, the function $c = f(x,y)$, is the intersection of $z = f(x,y)$, the surface, and
a horizontal plane $z = c$.

The overall term for vertical sections and level curves seems to be a **cross-section**[^3].

#### Example questions
- Plot the vertical sections and level curves for $z = x^2 + y^2$,
- Sketch a graph in the real space for the function $z=x^2$,
- Sketch the graph for the function $y=x^2$ in the real space,
- Sketch a graph for the function $z = \sqrt{x^2 + y^2}$.

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
\left. \frac{d}{dx} f(x,b) \right\|\_{x=a} = \lim\_{\Delta x \rightarrow 0} \frac{f(a+\Delta x, b) - f(a,b)}{\Delta x}.
$$

This limit reflects how $f(x,y)$ changes with $x$ at $(a,b)$, while y is fixed. It is the **partial derivative** of $f$ with respect to $x$ at the point $(a,b)$, denoted:

$$
\frac{\partial f(a, b)}{\partial x} \equiv \lim\_{\Delta x \rightarrow 0} \frac{f(a+\Delta x, b) - f(a,b)}{\Delta x} = \left. \frac{d f(x,b)}{dx} \right\|\_{x=a}.
$$

#### Linearity, product and quotient rules
The rules for a partial derivative of a linear combination of functions, the partial dervivative of
the product of functions, and the partial derivative of the quotient of two functions $u=u(x,y)$
and $v=v(x,y)$ are the same for those in normal differentiation. [^4]

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

Examples of this notation are:
$$
\frac{\partial}{\partial x} (\frac{\partial f}{\partial x}) \equiv \frac{\partial^2 f}{\partial x^2} \equiv f\_{xx},
$$

and

$$
\frac{\partial}{\partial x} (\frac{\partial f}{\partial y}) \equiv \frac{\partial^2 f}{\partial x \partial y} \equiv f\_{yx}
$$

Theorem. If partial derivatives concerned are continuous, the mixed derivatives commute to the order
of variables. [^5]

#### Example questions
- Calculate $\frac{\partial f}{\partial x}$ and $\frac{\partial f}{\partial y}$ for $f = y^2 + x^2 y$,
- Calculate $\frac{\partial f}{\partial x}$ and $\frac{\partial f}{\partial y}$ for $f = x^y$,
- Calculate $f\_x, f\_y$ and $f\_z$ for $f = x\sin(y) + yz$,
- Calcualte $f\_xy$ and $f\_yx$ for $f=ye^x + x\sin y$,

### Differentiable functions
#### Little-o
If
$$
\lim\_{x \rightarrow c} \frac{f(x)}{g(x)} = 0
$$
we say "$f$ is little-oh of $g$ as $x$ approaches $c$", and we write:
$$
f(x) = o(g(x)) \space \text{ as } \space x \rightarrow c.
$$

The little-o notation indicates tat the decay rate of a certain function is faster than that
of another.


#### Differentiable functions of a single variable
A function $y = f(x)$ is differentiable at $x\_0$ if
$$
y - y\_0 = f\_x (x\_0) (x-x\_0) + o(x-x\_0),
$$

or

$$
\Delta y = f\_x (x\_0) \Delta x + o(\Delta x),
$$
where $y\_0 = f(x\_0)$, $\Delta x = x - x\_0$, $\Delta y = y - y\_0$.

As $x$ is near $x\_0$, $\| \Delta x \| << 1$: and so equation (1) becomes:

$$
\Delta y \approx f\_x (x\_0) \Delta x.
$$

In words, the change of the function in its neighbourhood is approximately linear to the changes
of the variable, with the coefficient being the derivative.

#### Geometric interpretation of differentiable functions
When a curve is differentiable at $x\_0$, the curve near $x\_0$ can be approximated by its
tangent line at $x\_0$.

![Put image here]()

#### Differentiable functions of two variables
A function $f(x,y)$ is called differentiable at $(x\_0, y\_0)$ if $\Delta f = f(x,y) - f(x\_0, y\_0)$
satisfies:
$$
\Delta f = f\_x(x\_0, y\_0) \Delta x + f\_y (x\_0, y\_0) \Delta y + o(\rho),
$$

where $\Delta x = x - x\_0$, $\Delta y = y - y\_0$, and $\rho = \sqrt{(\Delta x)^2 + (\Delta y)^2}.

As $(x,y)$ is near $(x\_0, y\_0)$, or $(x,y)$ is in the neighbourhood of $(x\_0, y\_0)$:

$$
o(\rho) << \rho << 1,
$$

and so $\Delta f \approx f\_x (x\_0, y\_0) \Delta x + f\_y (x\_0, y\_0) \Delta y$$.

Near a differentiable point, the change of a function is approximately linear to the changes of
variables, with the coefficients being the corresponding partial derivatives. As $\rho$ is infinitively
small, we have

$$
df (x,y) = f\_x (x,y) dx + f\_y (x,y) dy.
$$

#### Geometrical interpretation of differentiable functions
When a surface is differentiable at $(x\_0, y\_0)$, the surface near $(x\_0, y\_0)$ can be approximated
by its tangent plane at $(x\_0, y\_0)$.

#### Being differentiable and having derivatives
For single variable functions, being differentiable is equivalent to having a derivative, i.e.
$$
f \in D \iff \exists f\_x.
$$

For multi-variable functions, a differentiable function has all partial derivatives
$$
f(x,y) \in D \implies \exists f\_x, f\_y.
$$

But, the existance of all partial derivatives does not guarantee the function being differentiable.

### The chain rule
A function is said to be sufficiently smooth if the function and as many of it's derivatives as
required are continuous where they need to be.

#### The chain rule for functions of single variable
Suppose $y=y(x), x = x(u)$. Letting $y = Y(u)$, we have
$$
\frac{dY}{du} = \frac{dy}{dx}{dx}{du},
$$
which is conventionally written:
$$
\frac{dy}{du} = \frac{dy}{dx}{dx}{du}.
$$

We can derive the chain rule in the following way:

Suppose that $y = y(x)$ and $x = x(u)$ are differentiable:
$$
dy = y\_x dx, \\\\
dx = x\_u du, \\\\
\text{therefore} \space dy = y\_x x\_u du.
$$

We can rewrite this in terms of $Y(u)$, giving us:

$$
dy = Y\_u dy.
$$

From these two equation, we know that

$$
Y\_u du = y\_x x\_u du, \text{ or } \\\\
Y\_u = y\_x x\_u.
$$

#### The chain rule for functions of two variables
Suppose $f = f(x,y)$ and $x = x(u, v), y = y(u, v)$ and all are differentiable.

As $f(x,y)$ is differentiable, we must have that $df = f\_x dx + f\_y dy$.

As $x = x(u,v)$ and $y = y(u,v)$ are differentiable, we must have that
$$
dx = x\_u du + x\_v dv, \space dy = y\_u du + y\_v dv.
$$

When we combine these equations, we get
$$
\space df = f\_x (x\_u du + x\_v dv) + f\_y (y\_u du + y\_v dv) \\\\
= (f\_x x\_u du + f\_y y\_u du) + (f\_x x\_v dv + f\_y y\_v dv) \\\\
= (f\_x x\_u + f\_y y\_u) du + (f\_x x\_v + f\_y y\_v)dv.
$$

Since $f = f(x(u,v), y(u,v)) = f(u,v) \implies df = f\_u du + f\_v dv.$$

Given that $du \text{and} dv$ are arbitray and infinitessimally small, by setting
$du, dv = (\neq 0, 0)$, $du, dv = (0, \neq 0)$, we obtain the Chain Rule
$$
f\_u = f\_x x\_u + f\_y y\_u, f\_v = f\_x x\_v + f\_y y\_v.
$$

#### How can we remember the chain rule?
We start we an example:
$$
\text{For } \space f = f(x,y), x = x(u,v), y=y(u,v), \\\\

\frac{\partial f(x,y)}{\partial u} = \frac{\partial f}{\partial x} \frac{\partial f}{\partial u} + \frac{\partial f}{\partial y} \frac{\partial y}{\partial u} \\\\

\frac{\partial f(x,y)}{\partial v} = \frac{\partial f}{\partial x} \frac{\partial x}{\partial v} + \frac{\partial f}{\partial y} \frac{\partial y}{\partial v} \\\\
$$

In Step 1, we put the function and the target variables in correct positions. For two intermediate
variables, we will have two terms.

In Step 2, we add an intermediate variable for each term.

#### Chain rule for functions of multi-variables
In a general case, we have the following chain rule:

Let $f$ be a function of the variables $x\_1, \dots, x\_n$,
$$
f = f(x\_1, x\_2, \dots, x\_n),
$$
where each $x\_j$ is a function of the variables $t\_1, t\_2, \dots, t\_m$,
$$
x\_j = x\_j(t\_1, t\_2, \dots, t\_m), j=1,2,\dots,n.
$$

If $f$ and $x\_j$ are sufficiently smooth, then
$$
\frac{\partial f}{\partial t\_i} = \frac{\partial f}{\partial x\_1} \frac{x\_1}{\partial t\_i} + \dots +
\frac{\partial f}{\partial x\_n} \frac{\partial x\_n}{\partial t\_i}, \text{where } i=1,2,\dots,m.
$$

The summarization runs over all the intermediate variables.

#### Example questions
- If $f = e^x \sin y, x = uv^2 \text{ and } y=uv$, find $\frac{\partial f}{\partial u}$ at $(u,v) = (1,\pi)$,
- Assume $w = e^x yz$, $x = ts, y = s^2, z=t-s$. Find $w\_t$,
- Calculate $\frac{\partial^2 f}{\partial y}{\partial x}$ for $f=\sin (x \sin y)$,

### Implicit partial differentiation
Please note that we can also use implicit partial differentiation to solve certain problems.
For example, how would you solve the following problem?

Find $\frac{\partial z}{\partial x}$ and $\frac{\partial z}{\partial y}$, where $z(x,y)$ is defined by
$$
yz = \ln z = x+y.
$$

#### Example questions
- For the partial differential equation: $x \frac{\partial u}{\partial x} - y \frac{\partial u}{\partial y} = 2x^2$ change the variables $(x,y)$ to $s = xy$, $t = \frac{x}{y}$.

[^1]: Question: Are all the functions we deal with in this course bijective functions? I'm assuming so, since he said in lecture a function maps one element in codomain to exactly one in the
      codomain. Did he say for every element in the domain?

[^2]: When asked to draw the surface (graph) of a multivariable function, it's always a good idea to think about how it intersects with the coordinate axis, especially if it's a plane.
      In fact, when talking about level curves and vertical sections, it's often better to consider a surface in terms of the XY, XZ and YZ surfaces, at least that's my impression so far.

[^3]: From this section, please make notes on ellipses, parabola, hyperbola. I have a hunch it's going to come up a lot. Also, what is a contour? What is a contour integral? Christ, I've
      forgotten a lot. XD

[^4]: Be sure to know how to prove these results in both a single variable and multi-variable context.

[^5]: What?
