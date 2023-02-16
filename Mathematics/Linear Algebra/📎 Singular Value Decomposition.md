SVD decomposes a matrix $$X = UDV^T$$where $U$ and $V$, both orthonormal, contain left and right singular vectors respectively and diagonal $D$ contains singular values. The singular values $\sigma_i$ are roots of the eigenvalues of $X^TX$, and the right singular vectors in $V$ are the eigenvectors of $X^TX$.

# Thin SVD
Thin SVD approximates $X$ by keeping the $k$ largest singular values and their associated vectors. This is the best approximation of $X$, minimizing distortion 
$\Vert X−\hat{X}\Vert_F$.

In [[🗜️ Principle Component Analysis]], we use this idea to perform dimensionality reduction. Each $m$-dimensional $x$ can be approximated by a $k$-dimensional vector of scores with respect to the basis vectors $V_k$, called loadings.

# Pseudo-Inverse
We can also calculate a pseudo-inverse (”Moore-Penrose” inverse) $$X^+ = V_kD^{-1}_kU_k^T$$with Thin SVD, which is much less expensive than other calculations.

In linear regression, we have weights $w = X^+y$, which initially used to be $X^+ = (X^TX)^{-1}X^T$.

# Power Method
Power method is used to find eigenvalues of square matrix $A$.

Any vector $x$ can be written as a summation over scaled eigenvectors, $x = \sum_i z_i v_i$. Then, we have the following observation.
$$ Ax = \sum_{i=1}^n z_i Av_i = \sum_{i=1}^n z_i \lambda_i v_i $$
Every time we multiply $x$ by $A$, the eigenvector corresponding the largest eigenvalue gets bigger; multiplying $x$ by $A$ multiple times, we approach this eigenvector.

After multiplying $x$ multiple times by $A$, we find this eigenvector $v_1$, project it off, and continue to find $v_2\ldots v_k$.