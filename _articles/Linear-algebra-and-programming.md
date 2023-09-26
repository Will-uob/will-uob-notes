---
title: Summary of my course on linear algebra and programming
published: true
date: 2023-09-25
tags: Maths LinAlg
---

# Summary of linear algebra and programming.
Linear algebra is the study of multi-dimensional space.
## 1. What are vector spaces?
### 1.1 What are fields and vector spaces?
####  1.1.1 Fields
Fields, for our purposes, are sets that contain our scalars. More formally:

Defintion 1.1.1: A field, whose elements may be referred to as numbers, is a set $\mathbb{F}$ on which we have binary operations addition and multiplication, $+ : \mathbb{F} \times \mathbb{F} \rightarrow \mathbb{F}$ and $\cdot : \mathbb{F} \times \mathbb{F} \rightarrow \mathbb{F}$, satisfying the following axioms:

![The axioms of a field](https://i.stack.imgur.com/DLUQp.png)

Examples of fields include:
- The real numbers,
- The complex numbers,
- Finite fields.

#### 1.1.2: What are finite fields?
Theorem 1.1.2: A field $\mathbb{F}$ is finite if $\| \mathbb{F} \| = p^{f}$ for some prime integer $p$ and a positive integer $f$. Furthermore, for each order[^1] $p^{f}$, there is exactly one field of that
order.

This tells us how many finite fields exist, and what are the possible orders. $\mathbb{F}\_q$ denotes
the only fields of order $q = p^f$.

##### Prime order

If the order of the field is $p$, that is $f=1$, then $\mathbb{F}\_p$ is $\mathbb{Z}\_p$, the integers
modulo[^2] $p$. Hence $\mathbb{F}\_p = \\{0, 1, \dots, p-1\\}$, and the operations of addition and
multiplication are modified to ensure that our result are within the interval $[0, p-1]$.

##### Non-prime order
The above method does not work in the non-prime case. Instead, giving $\mathbb{F}\_4$ as an example,
we cannot take $\mathbb{Z}\_4$, as this is not a field. Instead, we take $\mathbb{F}\_4 = \\{0, 1, a, b\\}.$

We can then construct tables to define the rules for the operations. Information about the construction
of these tables can be found in the Abstract Algebra course.

#### 1.1.3: Vector spaces
Definition 1.1.4: Suppose that $\mathbb{F}$ is a field. A **vector space** over $\mathbb{F}$ is a set
$\mathbb{V}$ together with operations addition and scalar multiplication, $+: V \times V \rightarrow V$, and $\cdot : \mathbb{F} \times V \rightarrow V$, satisfying the following axioms:

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
- Euclidean space
- Row space: $\mathbb{F}^n = \\{(a\_1, a\_2, \dots, a\_n) \space \| \space a\_1, a\_2, \dots, a\_n \in \mathbb{F}\\}$
- Column space: The same as above, except the values are in a column vector, not a row vector.
- Functional spaces in analysis: For example, $C[a,b] = \\{\text{all continous functions on the interval} [a,b] \in \mathbb{R}\\}$.
- Spaces of polynomials: For example, $p^n = \\{a\_n x^n + \dots + a\_1 x + a\_0 \| a\_0, a\_1, a\_2, \dots, a\_n \in \mathbb{R}\\}$.

### 1.2: What are subspaces, intersections and sum of subspaces?
#### 1.2.1: Subspaces
Defintion 1.2.1: Suppose $V$ is a vector space over $\mathbb{F}$. A subset $U \subseteq V$ is a
[subspace](https://textbooks.math.gatech.edu/ila/subspaces.html) if it is a vector space over $\mathbb{F}$ in its own right, with respect to addition and multiplication inherited from $V$.

She then goes over some examples of subspaces, such as:
1. $U=V$[^3],
2. $\{0\}$, the trivial subspace, denoted $0$,
3. The subspaces of $\mathbb{R}^2$ and $\mathbb{R}^3$,
4. Polynomial subspaces.

#### 1.2.2: Subspace criterion
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

#### 1.2.3: Intersection of subspaces
There are two operations, intersection and sum, that start from known sub-spaces and produce new ones.
The intersection is defined as follows:

Theorem 1.2.11 (Intersection of subspaces) If $\\{U\_i \| i \in I\\}$ is a collection of subspaces of a
vector space $V$, then the intersection $W := \cap\_{i \in I}U_i $ is again a subspace of $V$.

#### 1.2.4: The Span
Informally, the span of a set of vectors can be regarded as the set of all vectors that can be represented
by the linear combination of those vectors. If a set of vectors spans the entire $n^{\text{th}}$-dimensional plane
it is defined in, then we say that those vectors for a basis for that space.

The following theorem derives from the previous result:

Theorem 1.2.12 (Minimal subspace) Suppose $V$ is a vector space and $X \subseteq V$ is an arbitrary
subset. Then, there is a unique minimal subspace $U$ of $V$ containing $X$. This $U$ is contained in
any other subspace of $V$ containing $X$.

The claim leads to the following definition:

Definition 1.2.13 (Span) For a vector space $V$ and a subset $X \subseteq V$, the subspace generated
(or spanned) by $X$ is the unique minimal subspace of $V$ containing $X$. This subspace is denoted by
$\<X\>$. It is also known as the span of $X$.

For instance, if $X = A \cup B \cup C$, we can write this as $\<A, B, C\>$

#### 1.2.5: Sum of subspaces, direct sum
Definition 1.2.16 (Sum of subspaces): Suppose that $U$ and $W$ are two sub-spaces of a vector space V.
Then we define $U+W = \\{u+w \| u \in U, w \in W\\}$.

Theorem 1.2.17: If $U$ and $W$ are subspaces of a vector space $V$, then $U+W$ is also a subspace of
$V$.[^4]

Theorem 1.2.18: If $U$ and $W$ are subspaces of $V$, then $U+W = \<U, W\>$. More generally, if
$U\_1, \dots, U\_k$ are subspaces of $V$, then $U\_1 + \dots U\_k = \<U\_1, \dots, U\_k\>$.

If we have $U$ and $W$ as subspaces of $V$, and let $D=U+W$, then generally every vector $d \in D$ can
be written as $d=u+w, u \in U, w \in W$, in more than one way. This leads us to the concept of direct
sums.

Definition 1.2.19 (Direct sum): Suppose $U$ and $W$ are subspaces of a vector space $V$. $D = U + W$ is
the direct sum of $U$ and $W$, $D = U \oplus W$, if for every $d \in D$, there exists only one choice
of $u \in U$ and $w \in W$ such that $d = u + w$.

Theorem 1.2.20 (Direct sum criterion): For subspace $U$ and $W$ of a vector space $V$, we have that
$D = U + W$ is the direct sum of $U$ and $W$ iff $U \cup W = 0$.[^5]

Definition 1.2.21 (Direct sum, II): Suppose $U\_1, \dots, U\_k$ are subspaces of a vector space $V$.
We say that $D = U\_1 + \dots + U\_k$ is the direct sum of $U\_1, \dots, U\_k$ if every $d \in D$ can
be uniquely written as $d = u\_1 + \dots + u\_k$ for $u\_1 \in U\_1, \dots, u\_k \in U\_k$.

Theorem 1.2.22 (Direct sum criterion, II): For subspaces $U\_1, \dots, U\_k$ of a vector space $V$,
we have that $D = U\_1 + \dots + U\_k$ is the direct sum of the subspaces $U\_i$ iff
$(U\_1 + \dots + U\_{i-1}) \cup U\_i = 0$ for $i = 2,3,\dots,k$.

### 1.3: Linear combinations and independence
#### 1.3.1 Vectors in the span
Suppose that $V$ is a vector space over a field $\mathbb{F}$, and let $X \subseteq V$.

Definition 1.3.1 (Linear combination)[^6]: An expression of the form
$$
\sum\_{x \in X} a\_x x
$$
is called a linear combination of the vectors from $X$. Here, for each vector $x \in X$, $a\_x$ is a
scalar from $\mathbb{F}$. The numbers $a\_x$ are called the coefficients of the linear combination.

If $X$ is an infinite set, we additionally assume that only finitely many coefficients $a\_x$ are
non-zero, so that a linear combination is always a finite sum and evaluable.

Definition 1.3.2: By torture of terminology, a vector $v \in V$ is a linear combination of $X$ if
$$
v = \sum\_{x \in X} a\_x x
$$

for some coefficients $a\_x$. That is, if $v$ is the result of evaluation of some linear combination of
$X$.

Theorem 1.3.5 (The span): Suppose $V$ is a vector space over $\mathbb{F}$ and suppose $X \subseteq V$.
Then $\<X\>$ consists of all vectors that are linear combinations of $X$. That is,
$$
\<X\> = \{\sum\_{x \in X} a\_x x \| a\_x \in \mathbb{F} \forall x \in X\}.
$$[^6]

#### 1.3.2 Independent sets
Are there better and worse generating sets or are all generating sets roughly the same?

Definition 1.3.8 (Linear dependence): Suppose $X$ is a set of vectors of a vector space $V$. We say
that $X$ is linearly dependent if a non-trivial linear combination of $X$ evaluates to the zero vector.
We will call such a linear combination a non-trivial linear dependence or a non-trivial linear relation
on $X$.

Theorem 1.3.10 (Unique coefficients): Suppose that $X$ is a set of vectors in a vector space $V$
over $\mathbb{F}$. Let $U = \<X\>$ and $u \in U$. Then, for $u$, there exists a unique choice of
coefficients $a\_x \in \mathbb{F}$ such that $u = \sum\_{x \in X} a\_x x$ if and only if $X$ is
independent.[^7]

#### 1.3.3: Up and down
Can we find independent generating sets? Yes, all we need is to remove unnecessary vectors from a known
generating set.

Theorem 1.3.12 (Unnecessary vector): Suppose a set $X$ of vectors of a vector space $V$ is linearly
dependent, namely,
$$
\sum\_{x \in X} a\_x x = 0,
$$

where not all $a\_x$ are zero. Let $x \in X$ be such that $a\_x \neq 0$. Then $X' = X \\ \{x\}$ spans
the same subspace $U = \<X\>$.[^8]

Just like we can remove unncecessary vectors from generating sets, we can sometimes add new vectors
to independent sets:

Theorem 1.3.14 (Adding a vector): Suppose $X$ is a linearly independent set in a vector space $V$ and
$u \in V$. If $u$ is not a linear combination of the vectors from $X$, then $X' = X \cup \{x\}$ is
linearly independent.[^9]

### 1.4: Bases
#### 1.4.1: Bases
Defintion 1.4.1 (Basis): A basis in $V$ is a linearly independent generating set.

Theorem 1.4.2 (Existence of bases): Every vector space has a basis

##### How to prove the above theorem
Proposition 1.4.3 (Down to a basis): Every generating set $X$ in a vector space $V$ contains a basis.[^10]

Proposition 1.4.4 (Up to a basis): Every linearly independent set $X$ in a vector space $V$ is contained
in a basis.[^11]

#### 1.4.2: Standard bases
This part is skipped over for now, though contains many nice examples of how to prove a basis.

#### 1.4.3: Dimension
Definition 1.4.9 (Finite-dimensional spaces): A vector space is called finite-dimensional if it contains
a finite generating (spanning) set of vectors. Otherwise, we call the vector space infinite dimensional.

Proposition 1.4.10: Suppose that $V$ is a vector space, $X$ an independent set of vectors in $V$, and
$Y$ is a generating set of vectors, that is, $\<Y\> = V$. Then, $\| X \| \leq \| Y \|$.[^12]

Theorem 1.4.11 (Basis size): Any two bases in a vector space have the same size.[^13]

Definition 1.4.12 (Dimension): The dimension of a vector space $V$ is the size of an arbitrary basis of
$V$, and is denoted $\text{dim} V$.

For an infinite-dimensional vector space $V$, we just write $\dim V = \infty$.

Theorem 1.4.14: Suppose $V$ is a vector space and $U \leq V$ is a subspace. Then, $\dim U \leq \dim V$.
In particualar, if $V$ is finite-dimensional, so is $U$, and if both the last case, and $\dim U = \dim V$ are true, then $U = V$.[^14]

#### 1.4.4: Dimension of the sum of subspaces
Theorem 1.4.16 (Dimension of sum): Suppose $V$ is a vector space and suppose $U$ and $W$ are
finite-dimensional subspaces of $V$. Then $\dim(U+W) = \dim U + \dim W - \dim(U \cap W)$.[^15]

Theorem 1.4.19: Suppose $U$ and $W$ are finite-dimensional subspaces of a vector space $V$. Let
$S = U + W$. Then, $S = U \oplus W$ if and only if $\dim S = \dim U + \dim W$.

Which can be restated as:

Theorem 1.4.20: Suppose $U$ and $W$ are finite-dimensional subspaces of a vector space $V$. Let
$S = U + W$. Let $X$ be a basis in $U$ and $Y$ be a basis in $W$. Then $S = U \oplus W$ if and only if
$X \cap Y = \emptyset$ and $X \cup Y$ is linearly independent.

### 1.5: Coordinates
#### 1.5.1: Coordinates

[^1]: What does order mean in this context?

[^2]: What was the definition (mathematically) of modulo again?

[^3]: Note that we say a subspace $U \subseteq V$ is **proper** if $U \neq V$. Hence,
      $U =V$ is the only subspace of $V$ that is not proper.

[^4]: Proof is left as an exercise to the reader. Furthermore, this result can be generalised into
      Theorem 1.2.18

[^5]: Breakdown of the proof:

[^6]: The defintion in the lecture was as follows: Suppose $V$ is a vector space over a field \mathbb{F}. Given $u\_1, u\_2, \dots, u\_k \in V$,
      a linear combination of these vectors is
      $$
      a\_1u\_1 + a\_2u\_2 + \dots + a\_ku\_k = w
      $$
      for $a\_1, a\_2, \dots, a\_k \in \mathbb{F}$.

[^7]: Breakdown of the proof:

[^8]: Breakdown of the proof:

[^9]: Breakdown of the proof:

[^10]: Breakdown of the proof:

[^11]: Breakdown of the proof:

[^12]: Breakdown of the proof:

[^13]: Breakdown of the proof:

[^14]: Breakdown of the proof:

[^15]: Breakdown of the proof:

[^16]: Breakdown of the proof:
