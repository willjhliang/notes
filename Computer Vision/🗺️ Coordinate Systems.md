We deal in three coordinate systems:
1. Image coordinate system, which is only 2-dimensional. The image plane is perpendicular to the optical axis of the camera.
2. Camera coordinate system, where the $z$ axis is the optical axis. The $z$ axis intersects the image coordinate system at $(u_0, v_0)$.
3. World coordinate system, which is arbitrary. The world and camera coordinate system share scale and are related by a rigid transformation consisting of rotation and translation.

![[20230206212501.png|400]]

The image and camera systems are related by the camera intrinsics, which are $f, u_0, v_0$. Their relation can be summarized as a matrix $$K = \begin{pmatrix}f & 0 & u_0 \\ 0 & f & v_0 \\ 0 & 0 & 1\end{pmatrix}$$
The camera and world coordinate systems are related by rotation and translation, which are matrices $R$ and $T$ respectively.

# Camera Coordinates to Image Coordinates
Using the equations from [[🔍 Projection Models#Pinhole Model]], we can convert coordinates to pixels with $$\begin{align} u &= f\frac{X_c}{Z_c} + u_0 \\ v &= f\frac{Y_c}{Z_c} + v_0 \end{align}$$

We can write this instead as a matrix equation, $$\lambda \begin{pmatrix} u \\ v \\ 1 \end{pmatrix} = \begin{pmatrix} f & 0 & u_0 \\ 0 & f & v_0 \\ 0 & 0 & 1 \end{pmatrix} \begin{pmatrix} 1 & 0 & 0 & 0 \\ 0 & 1 & 0 & 0 \\ 0 & 0 & 1 & 0 \end{pmatrix}\begin{pmatrix} X_c \\ Y_c \\ Z_c \\ 1 \end{pmatrix} = K \begin{pmatrix}X_c \\ Y_c \\ Z_c\end{pmatrix}$$
> We have the intermediate matrix in between because it's used when transforming from world to image coordinates. In this case, we just have $R = I$ and $T = 0$.

To go back from image coordinates to camera coordinates, we rearrange the above $$\begin{pmatrix}X_c \\ Y_c \\ Z_c\end{pmatrix} = \lambda K^{-1} \begin{pmatrix}u \\ v \\ 1\end{pmatrix}$$
Going from pixels to rays is known as calibration, and the rays are calibrated coordinates $$\begin{pmatrix}u - u_0 \\ v - v_0 \\ f\end{pmatrix} \sim \begin{pmatrix}(u - u_0)/f \\ (v - v_0)/f \\ 1\end{pmatrix}$$

# World Coordinates to Camera Coordinates
The world coordinate system is a rotated, translated camera coordinate system. The two are thus related by the equation $$\begin{pmatrix} X_c \\ Y_c \\ Z_c \\ 1 \end{pmatrix} = \begin{pmatrix} R & T \\ 0 & 1 \end{pmatrix} \begin{pmatrix} X_w \\ Y_w \\ Z_w \\ 1 \end{pmatrix}$$
Another form is $$\begin{pmatrix}X_c \\ Y_c \\ Z_c\end{pmatrix} = R\begin{pmatrix}X_w \\ Y_w \\ Z_w\end{pmatrix} + T$$
Notice that by setting $X_w = Y_w = Z_w = 0$, we can see that the world origin is at $\begin{pmatrix}X_c \\ Y_c \\ Z_c\end{pmatrix} = T$, in camera coordinates.
> The direction of $T$ is from camera origin to world origin using camera coordinates.

On the other hand, by setting $X_c = Y_c = Z_c = 0$, we observe that the camera origin is at $\begin{pmatrix}X_w \\ Y_w \\ Z_w\end{pmatrix} = -R^TT$, in world coordinates.

Finally, if we let $r_1, r_2, r_3$ be the columns of $R$, the equation above tells us that they are the world $x, y, z$ axes (respectively) in camera coordinate space.

# World Coordinates to Image Coordinates
Putting both equations together, we arrive at the projection from world to image, $$\lambda \begin{pmatrix} u \\ v \\ 1 \end{pmatrix} = \begin{pmatrix} f & 0 & u_0 \\ 0 & f & v_0 \\ 0 & 0 & 1 \end{pmatrix} \begin{pmatrix} R & T\end{pmatrix} \begin{pmatrix} X_w \\ Y_w \\ Z_w \\ 1 \end{pmatrix} = K \begin{pmatrix} R & T \end{pmatrix} \begin{pmatrix} X_w \\ Y_w \\ Z_w \\ 1 \end{pmatrix} = P \begin{pmatrix} X_w \\ Y_w \\ Z_w \\ 1 \end{pmatrix}$$
Notice that this can also be written as $$\lambda \begin{pmatrix}u \\ v \\ 1\end{pmatrix} = K(R \begin{pmatrix}X_w \\ Y_w \\ Z_w\end{pmatrix} + T)$$

Going backwards from image to world coordinates, we have $$\begin{pmatrix}X_w \\ Y_w \\ Z_w\end{pmatrix} = -R^TT + \lambda R^TK^{-1}\begin{pmatrix}u \\ v \\ 1\end{pmatrix}$$
This tells us at the camera origin, or the projection center, is at $-R^TT$, and our world coordinates go along the line with direction $R^T K^{-1} \begin{pmatrix}u \\ v \\ 1\end{pmatrix}$ that intersect $-R^TT$.

# Transformation Composition
Note that for a transformation $$M = \begin{pmatrix}& R & & T \\ 0 & 0 & 0 & 1\end{pmatrix}$$
the order of composition is $\text{LHS} = M_1 M_2 M_3 \text{RHS}$.

When we apply a rotation and translation, we translate first, then rotate. We can see this by finding the translation and rotation transformations $M_T$ and $M_R$, then observing that $$P_c = RP_w + T = M_T M_R P_w$$