Pixels $(x, y)$ in $\mathbb{R}^2$ space correspond with $\begin{pmatrix} x \\ y \\ 1 \end{pmatrix}$ in $\mathbb{P}^2$ space, and vice versa. Projective equivalence states that in $\mathbb{P}^2$, two elements are projectively equivalent if they satisfy $$\begin{pmatrix} u \\ v \\ w \end{pmatrix} = \lambda \begin{pmatrix} u' \\ v' \\ w' \end{pmatrix}$$
This can alternatively be written as $$\begin{pmatrix} u \\ v \\ w \end{pmatrix} \sim \begin{pmatrix} u' \\ v' \\ w' \end{pmatrix}$$
Each set of equivalence classes constitutes a ray, and $\mathbb{P}^2$ consists of all rays.

The set of points at infinity, or points that aren't projected onto the image plane, have the form $\begin{pmatrix} u \\ v \\ 0 \end{pmatrix}$.

# Image Line
A line on the image plane crossing $p_1$ and $p_2$ is also a plane in projective space; thus, it's defined by its orthogonal vector $l$. Then, since the rays going to $p_1$ and $p_2$ are in the plane, $l^Tp_1 = l^Tp_2 = 0$, and we get that $$l \sim p_1 \times p_2$$
If the third coordinate is $0$, $l$ passes through the origin. Otherwise, if the third coordinate is non-zero, the line is not in $\mathbb{R}^2$, and all points along it have the third coordinate equal to $0$; this is thus the line containing all points at infinity.

Furthermore, using the same reasoning as above, two lines $l_1$ and $l_2$ intersect at point $p \sim l_1 \times l_2$.

# Projective Transformation
Projective transformations, or homographies, project points from a plane onto another plane and is defined by an invertible matrix transformation from $\mathbb{P}^2$ to $\mathbb{P}^2$. Specifically, the 3x3 transformation matrix $H$ with $\det H = 0$ maps $$p' \sim Hp$$

The [[🖼️ Projective Transformation Problem]] maps a world plane to image plane using $4$ correspondences.
The [[🌞 Horizon Problem]] finds the horizon line using the transformation from ground plane to image plane.