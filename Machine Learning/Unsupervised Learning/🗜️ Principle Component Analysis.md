# Theory
PCA is used for dimensionality reduction, decomposing datapoint vectors $x^{(i)}$ in terms of coefficients $z^{(i)}$ on $k$ orthogonal unit basis vectors $u_j$. There are infinite bases we can use for $v_i$, but PCA aims to maximize the variance of the projected points (so that projections don't collapse points into a single space) and minimize the distortion, or data loss.

> We first mean center the data, subtracting $\bar{x}$ from all datapoints. This is used later to relate our equations to covariance.

For an individual vector $x^{(i)}$, its projection onto the basis is defined by $$z^{(i)} = ((x^{(i)} - \bar{x})^Tu_1, \ldots, (x^{(i)} - \bar{x})u_k)$$
To reconstruct $x^{(i)}$ from $z^{(i)}$, we calculate $$\hat{x}^{(i)} = \bar{x} + \sum_{j=1}^k z^{(i)}_j u_j$$

> If our basis has $k = m$ dimensions, where $m$ is the number of original dimensions, $\hat{x}^{(i)}$ is a perfect reconstruction, $\hat{x}^{(i)} = x^{(i)}$.

For data $X$ arranged in a matrix (such that each row is one vector $x^{(i)}$),
$$ X = ZV^T $$
$Z$ containing $z^{(i)}$ are the principal component scores, $V$ containing $u_j$ are principal components, also called loadings.

We'll first analyze the latter. Distortion is defined as  $$\Vert X - ZV^T\Vert_F = \sum_{i=1}^n \Vert x^{(i)} - \hat{x}^{(i)}\Vert_2^2$$
Plugging in our definition for $x^{(i)}$ and $\hat{x}^{(i)}$ above, we get $$\Vert X-ZV^T\Vert_F = \sum_{i=1}^n \Vert(\bar{x}+\sum_{j=1}^mz_j^{(i)}u_j) - (\bar{x} + \sum_{j=1}^kz_j^{(i)}u_j)\Vert_2^2 = \sum_{i=1}^n \sum_{j=k+1}^m (z_j^{(i)})^2$$
This shows that distortion is the sum of squared scores that we leave out. Plugging in the equation for the scores as defined above, we find that distortion actually equals $$\sum_{i=1}^n\sum_{j=k+1}^m u^T (x^{(i)} - \bar{x})(x^{(i)} - \bar{x})^Tu_j = n\sum_{j=k+1}^m u_j^T\Sigma u_j$$where $\Sigma = \frac{1}{n}\sum_{i=1}^n (x^{(i)} - \bar{x})(x^{(i)} - \bar{x})^T = \frac{1}{n}X^TX$ is the covariance matrix of our data.

> Note that in the equation above, we also swap the projection equation, ${x^{(i)}}^T u_j = u_j^T x^{(i)}$, but the value remains equivalent.

To minimize this value, we first observe that the covariance matrix is symmetric and therefore diagonal in its eigenvector basis. Because it's diagonal, the axes are independent, and we minimize distortion by leaving out the dimensions that have minimum variance.

> For a more mathematical proof, we use Lagrange multipliers. To minimize $u^T\Sigma u$ with the constraint that $\Vert u\Vert = u^Tu = 1$, we differentiate the Lagrangian $u^T\Sigma u - \lambda(u^Tu - 1)$ to get $\Sigma u - \lambda u = 0$, the definition of an eigenvector.

Setting $u_j$ to be the eigenvectors of the covariance matrix, we see that distortion is  the sum of discarded eigenvalues. $$n\sum_{j=k+1}^m u_j^T\lambda_ju_j = n\sum_{j=k+1}^m \lambda_j$$

> Observe that by setting the basis in this way, our basis is orthogonal. In other words, the components are uncorrelated, and the transformation of $x^{(i)}$ into $z^{(i)}$ gives us uncorrelated features.

As for the former goal, variance is defined as $$\sum_{i=1}^n\sum_{j=1}^k (z^{(i)}_j)^2 = \sum_{i=1}^n\sum_{j=1}^k (u_j^Tx^{(i)} - u_j^T\bar{x})^2 = \sum_{j=1}^k u_j^T [\sum_{i=1}^n(x^{(i)}-\bar{x})(x^{(i)}-\bar{x})^T]u_j$$

> Since we subtract off the mean from $x^{(i)}$, $\bar{z} = 0$ and is excluded from the variance formula above.

Observe that the middle summation is again a form of $\Sigma$. The equation then tells us that variance is the sum of squared eigenvalues we do include. $$n \sum_{j=1}^k u_j^T\Sigma u_j = n\sum_{j=1}^k \lambda_j$$

Therefore, by maximizing variance, we're also minimizing distortion (and vice versa). If we add them together, we get their inverse relationship $$ \text{Variance}_k + \text{Distortion}_k = n\sum_{j=1}^m \lambda_j = n\text{tr}(\Sigma)$$

As for a visual example, in the image below, we can see that the eigenvectors and their associated eigenvalues (the eigenvector's magnitude) fit the distortion-minimization variance-maximization objective.
![[20221229103232.png|400]]
Projecting points onto the largest eigenvector (going from 2D to 1D) will maximize the spread since this axis has largest variance. It also minimizes the distortion, geometrically interpreted as the distance from each point to our new axis.

PCA has a few variants that add onto its basic functionality.
1. Sparse PCA adds an $L_1$ penalty to the size of the scores and components in our distortion equation, so the optimal values are no longer eigenvectors and require alternating gradient descent.
2. Kernelized PCA can model a nonlinear transformation of the original data.
3. Matrix factorization $\hat{X} = PQ^T$ ($P$ analogous to scores, $Q$ analogous to loadings) generalizes PCA to include other regularization losses and can be solved with alternating least squares. To solve, we fix $P$, solve for $Q$ with ridge regression and vice versa (similar to [[🎉 Expectation Maximization]]).

# Training
PCA can be calculated directly using eigenvectors of $\Sigma$ or via SVD, which avoids constructing $\Sigma$; each method is described below.

## Direct PCA
Given data $D$, compute $\bar{x} = \frac{1}{n}\sum_{i=1}^n x^{(i)}$, the average over $x$, and covariance matrix $\Sigma$.

Find the $k$ largest eigenvalues of $\Sigma$ and their associated eigenvectors $v_1 \ldots v_k$, which are our principal components.

Project $z^{(i)} = ((x^{(i)} - \bar{x}) \cdot v_1, \ldots, (x^{(i)} - \bar{x}) \cdot v_k)$ to get the scores.

## PCA via SVD
Given data $D$, compute $\bar{x} = \frac{1}{n}\sum_{i=1}^n x^{(i)}$, the average over $x$, and let $X_c$ contains rows $x^{(i)} - \bar{x}$.

Compute [[📎 Singular Value Decomposition]] $X_c = USV^T$, and take the $k$ rows of $V^T$ with the largest singular values as our principal components.

> Note that the singular values calculated by SVD for $X$ are roots of the eigenvalues of $X^TX$, and the right singular vectors form an orthonormal basis of $X^TX$. The SVD method therefore calculates our eigenvalues and eigenvectors for $\Sigma$.

Project $z^{(i)} = ((x^{(i)} - \bar{x}) \cdot v_1, \ldots, (x^{(i)} - \bar{x}) \cdot v_k)$ to get the scores.

# Prediction
To get the scores for $x^{(i)}$, project it onto each principal component.
$$z^{(i)} = ((x^{(i)} - \bar{x})^Tu_1, \ldots, (x^{(i)} - \bar{x})u_k)$$
To recreate $x_i$, we apply the scores to the principal components and add $\bar{x}$.
$$\hat{x}^{(i)} = \bar{x} + \sum_{j=1}^k z^{(i)}_j u_j$$