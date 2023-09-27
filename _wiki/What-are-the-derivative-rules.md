---
title: Differentiation formulas
published: true
date: 27-09-2023
tags: Maths Calculus Differentation
---

# Differentiation Formulas
### Constants and powers
The following are some pretty basic formulae and identities you should know when dealing with
problems in differentation:
- \frac{d}{dx}(c) = 0
- \frac{d}{dx}(x) = 1
- \frac{d}{dx}(x^n) = n \cdot x^{n-1}
- \frac{d}{dx}(a^x) = a^x \cdot \ln(a) [^1]
- \frac{d}{dx}(a^u) = a^u \codt u' \cdot \ln(a)

If you ever get $x^x$, this is logarithmic differentiation, which there is a video for. Finally,
we have the constant product rule:

- \frac{d}{dx} [cf(x))] = c \cdot f(x)

### Chain, product and quotient rules
The product rule is defined as follows:
$$
\frac{d}{dx} [uv] = u'v + uv'.
$$

The quotient rule is defined as:
$$
\frac{d}{dx} \frac{u}{v} = \frac{vu' - uv'}{v^2}
$$

The derivative of a composition is solved using the chain rule:
$$
\frac{d}{dx} [f(g[u])] = f'(g[u]) \cdot g'(u) \codt u'
$$
where $u = h(x)$. When $u = x$, we get the following:
$$
\frac{d}{dx} [f[g(x)]] = f'[g(x)] \cdot g'(x)
$$

### Logarithmic and exponential functions
To find the derivative of a logarithm of base $a$, we have:
$$
\frac{d}{dx} [log\_a u] = \frac{u'}{u \ln a}.
$$
We also have the derivative of the natural logarithm, which is defined as:
$$
\frac{d}{dx} [\ln u] = \frac{u'}{u}
$$.

To find the derivative of the exponential function, we use the formula of footnote 1, that is:
$$
\frac{d}{dx} e^x = e^x
$$
and
$$
\frac{d}{dx} e^u = e^u \frac{du}{dx}.
$$

### Trigonometric functions
The derivatives of the basic trig functions are:
$$
\frac{d}{dx} [\sin u] = cos(u) u' \\\
\frac{d}{dx} [\cos u] = -sin(u) u' \\\
\frac{d}{dx} [\tan u] = \sec^2 (u) u'.
$$

When then have the following trig rules for the reciprocals of the above functions:
$$
\frac{d}{dx} [\cot u] = -\csc^2(u) u' \\
\frac{d}{dx} [\sec x] = \sec(u)\tan(u) u'  \\\
\frac{d}{dx} [\csc x] = -\csc(u)\cot(u) u'.
$$

We now go over the inverse trigonometric functions:
$$
\frac{d}{dx} [\sin^{-1} u] = \frac{u'}{\sqrt{1-u^2}} \\\
\frac{d}{dx} [\cos^{-1} u] = \frac{-u'}{\sqrt{1-u^2}} \\\
\frac{d}{dx} [\tan^{-1} u] = \frac{u'}{1+u^2} \\\
\frac{d}{dx} [\cot^{-1} u] = \frac{-u'}{1+u^2} \\\
\frac{d}{dx} [\sec^{-1} u] = \frac{u'}{u \sqrt{u^2 - 1}} \\\
\frac{d}{dx} [\csc^{-1} u] = \frac{-u'}{u \sqrt{u^2 - 1}}.
$$

[^1]: This is the one I always seem to forget
