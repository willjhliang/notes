# Problem
Also called the 3D-3D correspondence problem, given $N$ point correspondences $(A, B)$, find rotation $R$ and translation $T$.

# Solution
Note that we only need $3$ points to find the transformation. We'll solve the $N=3$ problem first, then generalize to any $N$.

We have $3$ correspondences, $(A_1, B_1), (A_2, B_2), (A_3, B_3)$. First, form an orthogonal basis $(a_1, a_2, a_3) = (A_2 - A_1, A_3 - A_1, (A_2 - A_1) \times (A_3 - A_1))$ and same for $(b_1, b_2, b_3)$.

Then, observe that an orthonormal basis is only affected by rotation. Thus, $$\begin{pmatrix} \frac{a_1}{\Vert a_1 \Vert} & \frac{a_2}{\Vert a_2 \Vert} & \frac{a_3}{\Vert a_3 \Vert} \end{pmatrix} = R\begin{pmatrix} \frac{b_1}{\Vert b_1 \Vert} & \frac{b_2}{\Vert b_2 \Vert} & \frac{b_3}{\Vert b_3 \Vert} \end{pmatrix}$$
Solve for $R = B^TA$, then find $T$ accordingly.

## General Solution
For $N$ points, we'll find $$\arg\min_{R, T} \sum_{i = 1}^N \Vert A_i - RB_i + T\Vert^2$$

Let centroids $\bar{A} = \frac{1}{N}\sum_{i = 1}^N A_i$ and $\bar{B} = \frac{1}{N}\sum_{i = 1}^N B_i$.

Translation is given by the difference between centroids after rotating $B_i$. $$T = \bar{A} - R\bar{B}$$

Then, subtract the centroids from each point to get $$A = \begin{pmatrix}A_1 - \bar{A} & \ldots A_N - \bar{A}\end{pmatrix}, \ B = \begin{pmatrix}B_1 - \bar{B} & \ldots B_N - \bar{B}\end{pmatrix}$$
We want to find $$\arg\min_R \Vert A-RB\Vert_F^2$$
This can be done with [[📎 Singular Value Decomposition]], setting $BA^T = USV^T$, then let $$R = V \begin{pmatrix}1 & 0 & 0 \\ 0 & 1 & 0 \\ 0 & 0 & \det VU^T\end{pmatrix}U^T$$