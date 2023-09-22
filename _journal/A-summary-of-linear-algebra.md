---
title: Linear algebra in a nutshell
date: 20-09-2023
published: true
tags: LinAlg Maths
---

# Linear algebra notes
The following is a summary of the [essence of linear algebra](https://www.youtube.com/playlist?list=PLZHQObOWTQDPD3MizzM2xVFitgF8hE_ab) course, by [3b1b](https://www.youtube.com/@3blue1brown). I would highly
recommend you watch the original series, since it gives many amazing visualisations and examples, which I'll be skipping here. The hope is that by mentioning only the essentials, it'll force me to think
about the problems visually, without the aid of his videos, and give me a good intuitive understanding of the subject before I begin my second linear algebra course.

## What are vectors?
There are three points of view from which to answer this question, those of:
- The maths student, whose view we'll ignore for now, since it's more abstract than the other two,
- The computer science student, who views vectors as lists of numbers,
- The physics student, who views vectors as arrows in space, that represent magnitude and direction.

The two fundamental operations involving vectors are:
- Vector addition, where we add vectors "tip-to-tail". Picture a coordinate space, with any two vectors $\overrightarrow{v}$ and $\overrightarrow{w}$, and arrange them in this fashion, and you will get
  their sum, which we can verify numerically by thinking of vectors from the CS student's viewpoint.
- Scalar multiplication, where we manipulate the magnitude and direction of a vector using a real number $a \in \mathbb{R}$.

## Linear combinations, span and basis vectors
### Basis vectors
In a coordinate system with two dimensions, we have two special vectors, $\hat{i}$ and $\hat{j}$, which represent our basis vectors. For example, usually in a cartesian plane we have basis vectors,
$$
\mathbf{\hat{i}} = \begin{bmatrix} 1 \\\ 0 \end{bmatrix} \space \text{ and } \space \mathbf{\hat{j}} = \begin{bmatrix} 0 \\\ 1 \end{bmatrix}
$$

Please note that as long as our basis vectors span the space, the choice of our basis vectors doesn't matter. What do I mean by span?

### The span and linear combinations
The span of vectors $\overrightarrow{v}$ and $\overrightarrow{w}$ is the set of all their linear combinations, that is, the set $\{ a\overrightarrow{v} + b\overrightarrow{w} : a \in \mathbb{R}, b \in \mathbb{R}\}$. Hence, our basis vectors span the space if the set of their linear combinations can represent the entire space.

But what about in three dimensions? Well, in that case we add a third vector, which we can think of as a rope which we use to pull the two-dimensional plane through space. But, what if this third vector lies on
this plane?

### Linear (in)dependence
If we have three vectors, $\overrightarrow{v}$, $\overrightarrow{w}$ and $\overrightarrow{u}$, and each add a new dimension to the span, then they're said to be linearly independent. But, in the last
question, we have a vector what won't add another dimension to the space. This vector is said to be linearly dependent, since it is a redundant vector.

We now have the tools to define what a **basis** is: The basis of a vector space is a set of linearly independent vectors that span the full space. It should now be clear why $\hat{i}$ and $\hat{j}$ are
referred to as the basis vectors of our cartesian plane, since they are the simplest vectors that form our basis.

## Matrices and linear combinations
### What are linear transformations?
A linear transformation is a function that takes in a vector and outputs a vector. We informally define a function as being linear if, when drawing grid lines on a cartesian plane, the grid lines must remain
parallel and evenly spaced, and the origin must remain fixed.

How to we describe a linear transformation? All we need is to record the changes to the basis vectors. If we consider any vector as a linear combination of our basis vectors, then this linear combination won't
change after the transformation, only the values of our basis vectors. Hence, we have something akin to, in the two-dimensional space:

$$
\hat{v}\_{\text{new}} = v\_1 \begin{bmatrix} a \\\ c \end{bmatrix} + v\_2 \begin{bmatrix} b \\\ d \end{bmatrix} = \begin{bmatrix} a v\_1 + b v\_2 \\\ c v\_1 + d v\_2 \end{bmatrix}
$$

Where the vectors $\begin{bmatrix} a \\\ c \end{bmatrix}$ and $\begin{bmatrix} b \\\ d \end{bmatrix}$ are our transformed basis vectors, $\hat{i}$ and $\hat{j}$. We can represent this linear transformation
as a matrix multiplication between our original vector:

$$
\hat{v}\_{\text{new}} = \begin{bmatrix} a b \\\ c d \end{bmatrix} \begin{bmatrix} v\_1 \\\ v\_2 \end{bmatrix}
$$

where the columns of the matrix represent the positions where $\hat{i}$ and $\hat{j}$ will land, respectively.

#### What if our columns are linearly dependent?
If our columns in the linear transformation are linearly dependent, it means that the linear transformation will squish our space into a smaller dimension. In the case of two dimensional transformations,
it will squish all of two dimensional space into a line, which represents the span of those two vectors.

## Matrix multiplication as composition
This episode was simple. Essentially, if you want to describe subsequent linear transformations, $T\_1(\hat{v})$ and $T\_2(\hat{v})$, then you can write this in terms of matrices as
$$
T\_2(T\_1(\hat{v})) = T\_3(\hat{v})
$$

where $T\_3(\hat{v})$ is the composition of $T\_1$ and $T\_2$, which we got by multiplying the two matrices representing those transformations. This way of viewing linear transformations gives us a few ideas
about their properties, for example they're associative, but not commutative (that is, order matters).

## The determinant
The determinant of a linear transformation is the factor by which a given region's area or volume[^1] increases or decreases as a result of a linear transformation. If the determinant of the matrix of our transformation is 0, it means that the transformation has transformed space to a smaller dimension. One natural question is how can you have a negative determinant? The answer to this, geometrically, is that a negative determinant changes the orientation of our basis vectors, or "flips" the space. Usually, the standard orientation is for $\hat{i}$ to be to the right of $\hat{j}$.

## Inverse matrices, column space and null space
To begin, what is the purpose of linear algebra as a whole? The answer is to solve systems of linear equations, which can be represented in the form $A \overrightarrow{x} = \overrightarrow{v}$. That is,
we're looking for a vector $\overrightarrow{x}$ such that after our transformation $A$ it lands on $\overrightarrow{v}$. How we view our solutions to these equations depends on the value of $\det(A)$.

### When $\underline{\det(A) \neq 0}$
In this case, we know that there will be one, and only one, vector which lands on $v$, which we can find by finding the inverse of $A$, $A^{-1}$. This is done by finding a solution to the equation
$$
A^{-1}A = I
$$
and it's been proved that if $\det(A) \neq 0$, then $\det(A^{-1})$ exists.

### When $\underline{\det(A) = 0}$
In this case, $A^{-1}$ does not exist[^2]. It's still possible that a solution can exist, however you have to be lucky enough for the vector to exist in the new solution space. For example, if your solution
in 3-dimensions lies on a plane that the linear transformation squishes that 3-dimensional space into, then it would still be a solution.

We now introduce new termonology, beginning with **rank**. The rank of a transformation $A$ is the number of dimensions in the output. The **column space** of $A$ is the set of all possible outputs of
$A \overrightarrow{v}$, which is the span of columns of our matrix.[^3] When our rank is equal to the number of columns, we say the matrix is "full rank". The **null space** or **kernel** is the set of
vectors that lands on the origin during a linear transformation. For a full rank transformation, this will only contain the $0$ vector.

## Dot products and duality
The dot product is numerically defined as follows:
$$
\overrightarrow{v} \cdot \overrightarrow{w} = v\_1w\_1 + v\_2w\_2 + \dots + v\_nw\_n
$$
where $n$ is the length of the vector. However, geometrically we can view this as the product between the length of the projection of $\overrightarrow{w}$ on $\overrightarrow{v}$ and the length of
the vector $\overrightarrow{v}$. We geometrically signify a negative dot product as when $\overrightarrow{w}$ is pointing away from $\overrightarrow{v}$. The question arises as to how this has anything
to do with the numerical process. The answer is duality[^4]. The author, 3b1b, then goes into detail about duality. The main takeaway is that whenever you have a linear transformation, where the output
space is the number line, there's going to be some unique vector, $\overrightarrow{v}$, corresponding to that transformation, which will be indentical to taking the dot product.

## The cross product
The cross product is handly summed up in the following image:

![Picture of the cross product](https://i.ytimg.com/vi/WeS4J4-Psqs/maxresdefault.jpg)

The cross product of any two vectors $\overrightarrow{v}$ and $\overrightarrow{w}$ is the area of the parallelogram they form. We define the positive orientation to be when $\overrightarrow{v}$ is to the right
of $\overrightarrow{w}$. The direction of our resulting vector, $\overrightarrow{p}$, is perpendicular to the parallelogram. We determine this using the right-hand rule, where the forefinger aligns with
$\overrightarrow{v}$, the middle with $\overrightarrow{w}$ and the thumb with the direction of $\overrightarrow{p}$.

## Cramer's rule[^5]
We can find solutions to systems of linear equations in two dimensions by considering the signed areas of the two parallelograms formed by the vector we wish to find, $\overrightarrow{v}$, and the basis vectors, $\hat{i}$ and $\hat{j}$. Since these areas get scaled by $\det(A)$, we can find $v\_1$ and $v\_2$ by dividing the transformed areas of these parallelograms by the determinant. This can be scaled into higher
dimensions, for example in three-dimensions we consider the volume of a parallelepiped.

## Change of Basis
What if we were to use a different set of basis vectors for two different coordinate systems? What would we do then? We can translate their "language" to our "language" by using the linear transformation
with columns associated with their basis vectors, to get their coordinates in our format. Likewise, they could use the inverse of that matrix to translate our coordinates into a form their "language"
understands.

But what if you want to apply transformation using their basis vectors? You would use matrix multiplication, first converting their coordinates to ours, applying the transformation, and then convert back
into their coordinates.

## Eigenvectors and eigenvalues[^6]
An eigenvector is a vector which stays on it's span during a transformation, only being stretched or squished. Each eigenvector has an eigenvalue, which tells us the scale of the streching or squishing.[^7]
You can understand a linear transformation to by analysing the effects on our basis vectors, but this is specific to our coordinate system. Instead, you can find the eigenvectors and eigenvalues to see what
a transformation is doing.

### Computational ideas of linear transformations
We can go through the following derivation to find a way of determining whether an eigenvector exists:
$$
A \overrightarrow{v} = \lambda \overrightarrow{v} \iff A \overrightarrow{v} = (\lambda I) \overrightarrow{v} \iff (A - \lambda I) \overrightarrow{v} = \overrightarrow{0}
$$
If $\det(A - \lambda I)$, then we have an eigenvector. However, when $\det(A - \lambda I) = 0$, we get imaginary solutions, so we have no eigenvectors.[^8]

### What is an eigenbasis?
If we have a diagonal matrix representing our transformation, then all our basis vectors are eigenvectors, with the diagonal entries of this matrix being the associated eigenvalues. This is a nice property,
as it means we can calculate powers of matrices far easier. We can harness the power of this property by changing the bases we are working with, as long as the set of basis vectors we choose spans the full
space.

A set of basis vectors which are also eigenvectors is known as an eigenbasis.

## What are vectors?
Moving away from looking at vectors as either objects in space or as lists of numbers, there's a general sense of "vectoriness". For example, functions can be viewed in the same way as vectors, since it
can be proved that the same properties apply to functions as to vectors. This leads us to the idea of a vector space, which has the eight following properties:

![Properties of a vector space](/images/vector_space_axioms.png)

[^1]: The general term for length, area and volume is apparently "mensuration".

[^2]: Why? I didn't really catch this part well during the series.

[^3]: Review the relationship between rank and column space again.

[^4]: Which is an extremely ill-defined term, it makes me wanna die.

[^5]: In the video he goes over orthogonal linear transformations, which you should definitely keep in mind.

[^6]: An example of where considering eigenvectors is useful is 3D rotations, where it's easier to think of the
      rotation in terms of axis of rotation, then as a $3 \times 3$ transformation.

[^7]: In the video series there was a note attached to this.

[^8]: The video adds a caveat to this.
