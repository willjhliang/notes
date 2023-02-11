# Theory
Gaussian Mixtures are a soft form of [[🎒 K-Means Clustering]]; instead of assigning each point to an individual cluster, each point $x_i$ is assigned a probability distribution over clusters, $p(z_i = k \vert x)$.

Furthermore, each cluster, now called a gaussian mixture, is represented by both a centroid $\mu_k$ and covariance matrix $\Sigma_k$ as well as its size $\pi_k$; size is defined as the probability a simple is drawn from mixture $k$ (which all sum to $1$).

> In a generative sense, our data is generated from $k$ gaussians, $p(x) = \sum_k \pi_k \mathcal{N}(\mu_k, \Sigma_k)$.

Letting hidden variable $z$ denote the mixture assignment, our generative probability can be rewritten as $$p(x) = \sum_{k=1}^K p(z = k) p(x \vert z = k)$$with $p(z = k) = \pi_k$ and $p(x \vert z = k) = \mathcal{N}(\mu_k, \Sigma_k)$.

> Note that this equation is incredibly similar to [[👶 Naive Bayes]]. If Naive Bayes lets $p(x \vert y)$ be a Gaussian distribution (instead of discrete), we get a Gaussian Mixture with independent $x$ (diagonal covariance $\Sigma$).

Gaussian mixtures uses the [[🎉 Expectation Maximization]] algorithm in the same way as [[🎒 K-Means Clustering]], first finding the mixture distribution $p(z = k \vert x)$ and then recalculating the parameters for each mixture.

We always optimize centroids $\mu_k$, but $\pi_k$ and $\Sigma_k$ can be constant or calculated during optimization. If preset, $\pi_k = \frac{1}{K}$.

Variance $\Sigma_k$ can be one of multiple types, each with a different number of parameters and flexibilities.
1.  Full: arbitrary for each class
2.  Shared full: arbitrary but same for each class
3.  Diagonal (Naive Bayes): diagonal for each class
4.  Shared diagonal: diagonal but same for each class
5.  Spherical: diagonal with same value ($\Sigma_k = \sigma_kI$) for each class
6.  Shared spherical: diagonal with same value but same for each class

# Model
Each mixture is defined by size $\pi_k$, centroid $\mu_k$, and variance $\Sigma_k$; cluster assignment is determined probabilistically.

# Training
Given training data $D$, randomly choose $\pi_k$, $\mu_k$, $\Sigma_k$ (assuming we let sizes and variances vary).

Alternate until convergence.
1. For each data point $x_i$, estimate $p(z_i = k \vert x_i) \propto \pi_k \mathcal{N}(x_i \vert \mu_k, \Sigma_k)$
2. Calculate new parameters for each mixture
   $$ \mu_k = \frac{\sum_{i=1}^n p(z_i = k \vert x_i)x_i}{\sum_{i=1}^n p(z_i = k \vert x_i)} $$$$ \pi_k = \frac{1}{n}\sum_{i=1}^n p(z_i = k \vert x_i) $$$$ \Sigma_k = \frac{\sum_{i=1}^n p(z_i = k\vert x_i)(x_i - \mu_k)(x_i - \mu_k)^T}{\sum_{i=1}^n p(z_i = k \vert x_i)} $$

# Prediction
Given point $x$, calculate $p(z = k \vert x)$ for each mixture; this gives a probability distribution over clusters, which is a soft classification (to get the hard classification, take the class with highest probability).