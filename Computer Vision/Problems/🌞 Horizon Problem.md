# Problem
Given homography $H$ from the ground plane to the image plane, find the horizon of the image.

# Solution
Observe that $\begin{pmatrix} 1 \\ 0 \\ 0 \end{pmatrix}$ and $\begin{pmatrix} 0 \\ 1 \\ 0 \end{pmatrix}$ are points at infinity in the world plane. Then, their projection with $H$ to the image plane gives the location of their vanishing points $A \sim h_1$ and $B \sim h_2$ in the image where $h_1$ and $h_2$ are the first and second columns of $H$.

Connecting $A$ and $B$ gives us the horizon, which is defined as $$(h_1 \times h_2)^T \begin{pmatrix} x \\ y \\ 1\end{pmatrix} = 0$$
in the image, or by the normal vector $h_1 \times h_2$ in projective space.

> The horizon tells us exactly how the camera is oriented. If it moves to the top, we look downwards. If it moves to the bottom, we look upwards.