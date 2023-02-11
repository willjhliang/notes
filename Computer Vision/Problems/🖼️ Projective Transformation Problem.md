# Problem
Our goal is to find the projective transformation between two planes. Given $4$ correspondences of the form $(x, y, x', y')$ with no collinear triplets, find the projective transformation that relates the planes defined by these points $$\begin{pmatrix} x' \\ y' \\ 1 \end{pmatrix} \sim H \begin{pmatrix} x \\ y \\ 1 \end{pmatrix}$$

For example, if the correspondences map a world plane to the image plane, we'll find $$\begin{pmatrix} u \\ v \\ 1 \end{pmatrix} \sim H \begin{pmatrix} X \\ Y \\ 1 \end{pmatrix}$$

# Solution
Solving for $x'$, we get $$x' = \frac{H_{11}x + H_{12}y + H_{13}}{H_{31}x + H_{32}y + H_{33}}$$
Rearranging terms, we can write this in matrix form as follows.
$$(H_{31}x + H_{32}y + H_{33})x' = H_{11}x + H_{12}y + H_{13}$$
$$\begin{pmatrix}-x & -y & 1 & 0 & 0 & 0 & x'x & x'y & x'\end{pmatrix}\begin{pmatrix}H_{11} \\ \ldots \\ H_{33}\end{pmatrix} = 0$$
We can do the same for $y'$ and for each of the $4$ correspondences. Then, stacking the rows together, we get a $8 \times 9$ matrix (or more generally a $2N \times 9$ matrix for $N$ points).

The vector form of $H$ can then be interpreted as the null space of our stacked matrix. We can find it with the [[📎 Singular Value Decomposition]] of the stacked matrix, and $H$ is given by the last column of $V$, or the last right singular vector.

# Four Points, No Collinear Triplet Proof
Below, we show that no triplet of the $4$ given correspondences can be collinear.

Assume the world plane has two pairs of parallel lines, $l_1 \parallel l_2$ and $l_3 \parallel l_4$ that are orthogonal to each other. Then, Let $A_s$ be the intersection of $l_1, l_2$, $B_s$ be the intersection of $l_3, l_4$, $C_s$ be the intersection of $l_1, l_3$, and $D_s$ be the intersection of $l_2, l_4$. Note that $A_s$ and $B_s$ are points at infinity.

Finally, let our correspondences be $(A_s, A_t), (B_s, B_t), (C_s, C_t), (D_s, D_t)$, and let $A_s = \begin{pmatrix} 1 \\ 0 \\ 0 \end{pmatrix}$, $B_s = \begin{pmatrix} 0 \\ 1 \\ 0 \end{pmatrix}$, $C_s = \begin{pmatrix} 0 \\ 0 \\ 1 \end{pmatrix}$, $D_s = \begin{pmatrix} 1 \\ 1 \\ 1 \end{pmatrix}$.

Now, observe that $A_t \sim HA$, $B_t \sim HB$, and $C_t \sim HC$ give us the columns of $H$. Thus, $$H = \begin{pmatrix} \alpha A_t & \beta B_t & \gamma C_t \end{pmatrix}$$
Since the determinant of $H$ must be nonzero, its columns must be linearly independent, so these three points cannot be collinear. We thus require this non-collinear triplet as well as one more point, which is used below.

$D_t$ gives us the constraint $D_t = \alpha A_t + \beta B_t + \gamma C_t$. Note that this is a simplification from $D_t = \lambda(\alpha'A_t + \beta'B_t + \gamma'C_t)$. Thus, we can solve for the coefficients with $$\begin{pmatrix} \alpha \\ \beta \\ \gamma \end{pmatrix} = \begin{pmatrix} A_t & B_t & C_t \end{pmatrix}^{-1} D_t$$

We have thus shown that we require $4$ correspondences with no collinear triplet to solve the projective transformation problem.