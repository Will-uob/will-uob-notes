---
title: What is implicit differentation?
date: 2023-09-27
published: true
tags: Maths Calculus
---

# What is implicit differentation?
## Explanation via example

Let us consider the equation $3y^2 - y + 6x^4 - 2x^2 = 7$. Usually, we have explicit functions
of $y$, such as $y = x^2$, for which it is easy to find $\frac{dy}{dx}$. However, like in our
equation above, it is often difficult to make $y$ the subject of our equality.

As a result, we use implicit differentation, where we differentate both sides of our equation
with respect to our non-subject variable, $x$ in this case, and then rearrange to find the
formula for the derivative of our subject variable, $y$.

$$
\frac{d}{dx} (3y^2 - y + 6x^4 - 2x^2) = \frac{d}{dx} (7) \\\
\iff 3\frac{d}{dx}(y^2) - \frac{d}{dx}(y) + 6\frac{d}{dx}(x^4) - 2\frac{d}{dx}(x^2) = \frac{d}{dx}(7)
\iff 3\frac{d}{dx}(y^2) - \frac{d}{dx}(y) + 24x^3 - 4x = 0
$$

How do we deal with the $y$ terms? Well, we use the fact that:

$$
\frac{d}{dx} = \frac{dy}{dx}\frac{d}{dy}.
$$

which gives us:

$$
6y\frac{dy}{dx} - \frac{dy}{dx} + 24x^3 - 4x = 0
\iff 6y\frac{dy}{dx} - \frac{dy}{dx} = 4x - 24x^3
\iff \frac{dy}{dx} = \frac{4x - 24x^3}{6y - 1}

## Intuition behind implicit differentation
We use another example. Take the equation
$$
x^2 + y^2 = 25.
$$

where we're trying to find the slope of the tangent line of the circle at a point $(x,y)$, which
is exactly $\frac{dy}{dx}$.

Our aim is to find the rate of change of $y$ with respect to $x$, $\frac{dy}{dx}$, using implicit
differentation. We breakup this problem into two parts.

We see it's easy to calculate $\frac{d}{dx} (x^2) = 2x$. However, to find $\frac{d}{dx} (y^2)$, keep
in mind that $y$ is secretly a function of $x$. This is like writing $y = f(x)$, and finding the
derivative of $(f(x))^2$ with the chain rule to be $2(f(x))f'(x)$. Thus, we get
$$
\frac{d}{dx}(y^2) = 2y \cdot \frac{dy}{dx}
$$.

Putting this together, we get
$$ 
2x + 2y \cdot \frac{dy}{dx} = 0, \\\
\iff \frac{dy}{dx} = \frac{-x}{y}.
$$

## More examples:
- $x^3 + y^3 = 8$,
- $x^2 + 2xy + y^2 = 5$,
- $5xy - y^3 = 8$,
- $tan(xy) = 7$,
- $36 = \sqrt{x^2 + y^2}$
