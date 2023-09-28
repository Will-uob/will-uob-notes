---
title: What is analytic geometry?
published: true
date: 2023-09-28
tags: Maths Geometry
---

# What is analytic geometry?
Analytic geometry, also known as coordinate geometry or Cartesian geometry, is the study of geometry
using a coordinate system. The following are notes taken from [this](https://math.libretexts.org/Bookshelves/Algebra/Algebra_and_Trigonometry_1e_(OpenStax)/12%3A_Analytic_Geometry) LibreTexts book.

## Coordinate systems
### Cartesian coordinates
The most common is the Cartesian coordinate system, where each point has an x-coordinate system, where
each point has an x-coordinate representing its horizontal position, and a y-coordinate representing
its vertical position.

These are usually an ordered pair $(x,y)$. This system can be expanded to 3-D space, where each point in
Euclidean space is represented by an ordered triple of coordinates $(x,y,z)$.

### Polar coordinates
In polar coordinates, every point of the pane is represented by its distance $r$ from the origin and
its angle $\theta$, with $\theta$ normally measured counterclockwise from the positive x-axis.

One may go to and from polar coordinates $(r, \theta)$ and Cartesian coordinates $(x,y)$ by using
the formulae:
$$
x = r \cos \theta, y = r \sin \theta; r = \sqrt(x^2 + y^2), \theta = \arctan(\frac{y}{x}).

This system may by generalized to three-dimensional space through the use of cylindrical or
spherical coordinates.

## Conic Sections
Conic sections are formed when a plane intersects two right circular cones aligned tip to tip,
and extending infinitely far in opposite directions, which we also call a cone.

The way in which we slice the cone will determine the type of conic section formed at the intersection.

### The Ellipse
A conic is a shape resulting from intersecting a right circular cone with a plane. Below is
an illustration:

![Ellipse, hyperbola, parabola](https://math.libretexts.org/@api/deki/files/6535/CNX_Precalc_Figure_10_01_002.jpg?revision=1&size=bestfit&width=725&height=328)

The sections can also be described analytically. We now fucus on an ellipse. An ellipse is a set of all
points $(x,y)$ in a plane such that the sum of their distances from two fixed points is a constant. Each
fixed point is called a focus.

Every ellipse has two axes of symmetry. The longer axis is called the major axis, and the shorter axis
is called the minor axis.

Each endpoint of the major axis is the vertex of the ellipse, while the endpoints of the minor axis
are it's co-vertices. The center of an ellipse is the midpoint of both the major and minor axes.

![An ellipse](https://math.libretexts.org/@api/deki/files/6537/CNX_Precalc_Figure_10_01_004.jpg?revision=1&size=bestfit&width=557&height=279)

We only consider ellipses that are positioned vertically of horizontally in the coordinate plane here.

### Deriving the Equation of an Ellipse Centered at the Origin
We begin with the foci, $(-c,0)$ and $(c,0)$. The ellipse if the set of all points $(x,y)$, such that
the sum of the distances from $(x,y)$ to the foci is a constant.

![Here](https://math.libretexts.org/@api/deki/files/6538/CNX_Precalc_Figure_10_01_014.jpg?revision=1)

If $(a,0)$ is a vertex of the ellipses, the distance from $(-c,0)$ to $(a,0)$ is $a+c$. The distance
from $(c,0)$ to $(a,0)$ is $a-c$. The sum of the distances from the foci to the vertex is
$$
(a+c) + (a-c) = 2a
$$
If $(x,y)$ is a point on the ellipse, then we can define the variables:
- $d1 = $ the distance from $(-c,0)$ to $(x,y)$,
- $d2 = $ the distance form $(c,0)$ to $(x,y)$.

By the definition of an ellipse, $d\_1 + d\_2$ is a constant. We know that the sum of these is
$2a$ for the vertex $(a,0)$. It follows that $d\_1 + d\_2 = 2a$ for any point on the ellipse.

We then are able to derive the equation of an ellipse from this observation
$$
d\_1 + d\_2 = 2a \\\
\text{ A lot of algebraic manipulation later...} \\\
\frac{x^2}{a^2} + \frac{y^2}{b^2} = 1.
$$

Hence, we now have the standard equation of an ellipse centred at the origin. If $a > b$, the ellipse is
stretched further in the horizontal direction, if $b > a$, the ellipse is stretched further in the
vertical direction. Note that the above equation is for ellipses with the major axis on the x-axis.
For ellipses with the major axis on the y-axis, we have standard form of the equation as:
$$
\frac{x^2}{b^2} + \frac{y^2}{a^2} = 1.
$$

#### Example question:
What is the standard form equation of the ellipse that has vertices $(\pm 8, 0)$ and foci $(\pm 5, 0)$.
The process:
- First, the foci are on the x-axis, so we have equation of the form $\frac{x^2}{a^2} + \frac{y^2}{b^2} = 1$.
- Second, the vertices are $(\pm 8, 0)$, so $a = 8$ and $a^2 = 64$.
- Third, our foci are $(\pm 5, 0)$, so $c=5$ and $c^2 = 25$.
- Fourth, we set $b^2 = a^2 - c^2$, and solve for $b^2$.
- Now, we substitute our values $a^2$ and $b^2$ into the standard equation.
- Hence, the equation of the ellipse is $\frac{x^2}{64} + \frac{y^2}{39} = 1$.

Another exercise is: What is the standard form equation of the ellipse that has
vertices $(0, \pm 4)$ and foci $(0, \pm \sqrt{15})$?

### What about when the Ellipse isn't centered at the Origin?
Like the graphs of other equations, the graph of an ellipse can be translated. If an ellipse is
translated $h$ units horizontally and $k$ units vertically, the center of the ellipse will
be $(h,k)$. Hence, we rewrite our standard form equation as:
$$
\frac{(x-h)^2}{a^2} + \frac{(y-k)^2}{b^2} = 1
$$

where the above equation is for an ellipse with major axis parallel to the x-axis. If the ellipse is
with major axis parallel to the y-axis, our equation becomes:
$$
\frac{(x-h)^2}{b^2} + \frac{(y-k)^2}{a^2} = 1
$$

The process is similar to finding an ellipse centered at the Origin, with the exception that we must
also find the centre of our ellipse, before we find $a$, $c$ and $b$.

#### Exercises
- What is the standard form equation of the ellipse that has vertices $(-2, -8)$ and $(-2, 2)$, and
foci $(-2, -7)$ and $(-2, 1)$?
- What is the standard form equation of the ellipse that has vertices $(-3, 3)$ and $(5, 3)$, and
foci $(1 - 2\sqrt{3}, 3)$ and $(1 + 2\sqrt{3}, 3)$?

### Graphing ellipses
This doesn't seem so bad, since we can draw any ellipse based on it's standard form. So, I'm skipping
this section until it becomes relevant to my studies in MVA.

### Solving applied problems involving ellipses
Many real world problems can be modelled by ellipses, including orbits of planets, satellites, moons
and comets, and shapes of boat keels, rudders and some airplane wings. In fact, whispering chambers are
designed with elliptical domes, so that a person whispering at one focus can easily be heard by someone
standing at the other focus.

### The Hyperbola
What do the paths of comets, supersonic booms, ancient Grecian pillars, and natural draft cooling towers
have in common? They can all be modelled by the same type of conic.

#### Locating the Vertices and Foci of a Hyperbola
A hyperbola is a conic section formed by intersecting a right circular cone with a plane at an angle,
such that both halves of the cone are intersected. This intersection produces two separate unbounded
curves that are mirror images of each other.

![Picture of a hyperbola](https://math.libretexts.org/@api/deki/files/7573/CNX_Precalc_Figure_10_02_002.jpg?revision=1)

A hyperbola is the set of all points $(x,y)$ in a plane such that the difference between $(x,y)$ and
the foci is a positive constant.

Notice that the definition of a hyperbola is very similar to that of an ellipse. The distinction is
that the hyperbola is defined in terms of the difference of two distances, whereas the ellipse
is defined in terms of the sum of two distances.

Every hyperbola has two axes of symmetry. The transverse axis, a line segment that passes through the
center of the hyperbola and has vertices as its endpoints, and the conjugate axis, perpendicular to the
transverse axis and has the co-vertices as its endpoints.

The center of a hyperbola is the midpoint of both the transverse and conjugate axes, where they
intersect. Every hyperbola also has two asymptotes that pass through its center. The central rectangle
of the hyperbola is centered at the origin with sides that pass through each vertex and co-vertex; it's
a useful tool for graphing the hyperbola and it's asymptotes.

![Image of a hyperbola's features](https://math.libretexts.org/@api/deki/files/7573/CNX_Precalc_Figure_10_02_002.jpg?revision=1)

### Deriving the equation for a hyperbola at the Origin
Let $(-c,0)$ and $(c,0)$ be the foci of a hyperbola centered at the origin. The hyperbola is the set of
all points $(x,y)$ such that the difference of the distances from $(x,y)$ to the foci is constant.

![Observe](https://math.libretexts.org/@api/deki/files/7573/CNX_Precalc_Figure_10_02_002.jpg?revision=1)

If $(x,y)$ is a point on a hyperbola, we can define the two variables:
- $d\_2$ = the distance from $(-c,0)$ to $(x,y)$,
- $d\_1$ = the distance from $(c,0)$ to $(x,y)$.

Notice that the sum of the distances from the foci to the vertex is
$$
(a+c) - (c-a) = 2a
$$

and it follows that $d\_2 = d\_1 = 2a$ for any point on the hyperbola. We then derive the formula
for the hyperbola at the origin by applying the distance formula:
$$
d\_2 - d\_1 = 2a \\\
\text{Application of the distance formula, algebraic manipulations} \\\
\frac{x^2}{a^2} - \frac{y^2}{b^2} = 1
$$

This equation defines a hyperbola centered at the origin with vertices $(\pm a, 0)$ and co-vertices
$(0, \pm b)$, where the transverse axis is on the x-axis.

If the transverse axis is on the y-axis, we have equation
$$
\frac{y^2}{a^2} - \frac{x^2}{b^2} = 1.
$$

Note that the vertices, co-vertices and foci are related by the equation $c^2 = a^2 + b^2$. When we are
given the equation of a hyperbola, we can use this relationship to identify its vertices and foci.

![The horizonal and vertical hyperbola types](https://math.libretexts.org/@api/deki/files/7576/CNX_Precalc_Figure_10_02_004.jpg?revision=1&size=bestfit&width=704&height=318)
