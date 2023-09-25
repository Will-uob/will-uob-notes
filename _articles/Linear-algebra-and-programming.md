---
title: Summary of my course on linear algebra and programming
published: true
date: 2023-09-25
tags: Maths LinAlg
---

# Summary of linear algebra and programming.
## 1. What are vector spaces?
### 1.1 What are fields and vector spaces?
####  1.1.1 Fields
Defintion 1.1.1: A field, whose elements may be referred to as numbers, is a set $\mathbb{F}$ on which we have binary operations addition and multiplication, $+ : \mathbb{F} \times \mathbb{F} \rightarrow \mathbb{F}$ and $\cdot : \mathbb{F} \times \mathbb{F} \rightarrow \mathbb{F}$, satisfying the following axioms:

![The axioms of a field](https://i.stack.imgur.com/DLUQp.png)

#### 1.1.2: What are finite fields?
Theorem 1.1.2: A field $\mathbb{F}$ is finite if $\| \mathbb{F} \| = p^{f}$ for some prime integer $p$ and a positive integer $f$. Furthermore, for each order[^1] $p^{f}$, there is exactly one field of that
order.

This tells us how many finite fields exist, and what are the possible orders. $\mathbb{F}\_q$ denotes
the only fields of order $q = p^f$.

##### Prime order

If the order of the field is $p$, that is $f=1$, then $\mathbb{F}\_p$ is $\mathbb{Z}\_p$, the integers
modulo[^2] $p$. Hence $\mathbb{F}\_p = \{0, 1, \dots, p-1\}$, and the operations of addition and
multiplication are modified to ensure that our result are within the interval $[0, p-1]$.

##### Non-prime order
The above method does not work in the non-prime case. Instead, giving $\mathbb{F}\_4$ as an example,
we cannot take $\mathbb{Z}\_4$, as this is not a field. Instead, we take $\mathbb{F}\_4 = \{0, 1, a, b\}.$

We can then construct tables to define the rules for the operations. Information about the construction
of these tables can be found in the Abstract Algebra course.

#### 1.1.3: Vector spaces
Definition 1.1.4: Suppose that $\mathbb{F}$ is a field. A **vector space** over $\mathbb{F}$ is a set
$\mathbb{V}$ together with operations addition and scalar multiplication, $+: V \time V \rightarrow V$, and $\cdot : \mathbb{F} \times V \rightarrow V$, satisfying the following axioms:

![The axioms](/images/vectorspace.png)

#### 1.1.4: Basic properties of vector spaces
Theorem 1.1.5: Suppose $V$ is a vector space over a field of scalars $\mathbb{F}$. Then the following
hold:
1. (Cancellation in sums) For $u, v, w \in V$, if $u+v = u+w$, then $v=w$,
2. For all $u \in V$, $0u = 0$,
3. For all $u \in V$, $(-1)u = -u$,
4. For all $a \in \mathbb{F}$, $a0 = 0$.

Theorem 1.1.6: Suppose that $V$ is a vector space over $\mathbb{F}$. Then:
1. For $a \in \mathbb{F}$ and $u \in V$, if $au = 0$, then either $a = 0$ or $u = 0$.
2. a. For $0 \neq a \in \mathbb{F}$, and $u,v \in V$, if $au = av$, then $u=v$. \ 
   b. Also, for $a,b \in \mathbb{F}$ and $0 \neq u \in V$, if $au = bu$, then $a=b$.

#### 1.1.5: Examples of vector spaces
In the notes they mention the following vector spaces and their properties:
- Row space
- Column space
- Function vector spaces
- Subsets of a set

### 1.2: What are subspaces, intersections and sum of subspaces?
#### 1.2.1 Subspaces
Defintion 1.2.1: Suppose $V$ is a vector space over $\mathbb{F}$. A subset $U \subseteq V$ is a
[subspace](https://textbooks.math.gatech.edu/ila/subspaces.html) if it is a vector space over $\mathbb{F}$ in its own right, with respect to addition and multiplication inherited from $V$.

She then goes over some examples of subspaces, such as:
1. $U=V$[^3],
2. $\{0\}$, the trivial subspace, denoted $0$,
3. The subspaces of $\mathbb{R}^2$ and $\mathbb{R}^3$,
4. Polynomial subspaces.

#### 1.2.2 Subspace criterion
How can we verify if $U \subseteq V$ is a subspace of the vector space $V$? By definition,
$U$ must be a vector space, meaning it must carry out the addition of vectors and scalar multiplication.
Hence, we must have that:
1. Definition 1.2.5: $U \subseteq V$ is closed for addition, that is, $\forall u,v \in U, u+v \in U$,
2. Definition 1.2.6: $U \subseteq V$ is closed for scalar multiplication, $\forall u \in U$ and $\forall
   a \in \mathbb{F}, au \in U$.

This is almost sufficient, which leads us to the formal defintion. Theorem 1.2.7 (Subspace criterion):
Suppose $V$ is a vector space over $\mathbb{F}$. A **nonempty** subset $U \subseteq V$ is a subspace if
and only if $U$ is closed for addition and multiplication with scalars.

This can be replaced by a single theorem:
Theorem 1.2.8 (Subspace criterion II): A non-empty subset $U$ of a vector space $V$ over $\mathbb{F}$ is
a subspace of $V$ if and only if, $\forall u, v \in U$ and all $a \in \mathbb{F}$, we have that
$au + v \in U$.

#### Intersection of subspaces
There are two operations, intersection and sum, that start from known sub-spaces and produce new ones.
The intersection is defined as follows:
Theorem 1.2.11 (Intersection of subspaces) If $\{U\_i \| i \in I\}$ is a collection of subspaces of a
vector space $V$, then the intersection $W := \cap\_{i \in I}U_i $ is again a subspace of $V$.


[^1]: What does order mean in this context?

[^2]: What was the definition (mathematically) of modulo again?

[^3]: Note that we say a subspace $U \subseteq V$ is **proper** if $U \neq V$. Hence,
      $U =V$ is the only subspace of $V$ that is not proper.
