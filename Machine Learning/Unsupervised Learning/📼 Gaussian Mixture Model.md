# Theory
Gaussian mixture models structure datapoints $x$ into groups, or clusters. Each point $x^{(i)}$ is assigned a probability distribution over clusters, $p(z_i = k \vert x^{(i)})$; in other words, for each point $x^{(i)}$, we maintain the probabilities of $x^{(i)}$ belonging to each cluster.

> [!info]
> Gaussian mixture models are a form of soft clustering as opposed to the hard clustering in [[🎒 K-Means Clustering]].

Each cluster, also called a gaussian mixture, is represented by both a centroid $\mu_k$ and covariance matrix $\Sigma_k$ as well as its size $\pi_k$. Size is defined as the probability a sample is drawn from mixture $k$, and the sum of all cluster sizes is $1$.

We always optimize centroids $\mu_k$, but $\pi_k$ and $\Sigma_k$ can be constant or calculated during optimization. If preset, $\pi_k = \frac{1}{K}$. Variance $\Sigma_k$ can be restricted to fully-flexible, diagonal, or spherical.

In a generative sense, our data is generated from $k$ gaussians, $$p(x) = \sum_k \pi_k \mathcal{N}(\mu_k, \Sigma_k)$$

Letting hidden variable $z$ denote the mixture assignment, our generative probability can be rewritten as $$p(x) = \sum_{k=1}^K p(z = k) p(x \vert z = k)$$with $p(z = k) = \pi_k$ and $p(x \vert z = k) = \mathcal{N}(\mu_k, \Sigma_k)$.

> [!info]
> Note that this equation is incredibly similar to [[👶 Naive Bayes]]. If Naive Bayes lets $p(x \vert y)$ be a Gaussian distribution (instead of discrete), we get a Gaussian Mixture with independent $x$ (diagonal covariance $\Sigma$).

Gaussian mixtures uses the [[🎉 Expectation Maximization]] algorithm to optimize its mixtures. We first find the mixture distribution $p(z = k \vert x)$, then recalculate the parameters for each mixture. This optimization form is equivalent to maximizing the log likelihood $$\sum_{i=1}^n \log p(x^{(i)} \vert \mu, \Sigma, \pi) = \sum_{i=1}^n \log \sum_{k=1}^K p(x^{(i)} | z = k, \mu, \Sigma, \pi)p(z = k \vert \pi)$$



# Model
Each mixture is defined by size $\pi_k$, centroid $\mu_k$, and variance $\Sigma_k$; cluster assignment is determined probabilistically.

# Training
Given training data $D$, randomly choose $\pi_k$, $\mu_k$, $\Sigma_k$ (assuming we let sizes and variances vary).

Alternate until convergence.
1. For each data point $x_i$, estimate $p(z_i = k \vert x_i) \propto \pi_k \mathcal{N}(x_i \vert \mu_k, \Sigma_k)$.
2. Calculate new parameters for each mixture $$\begin{align*} \mu_k &= \frac{\sum_{i=1}^n p(z_i = k \vert x_i)x_i}{\sum_{i=1}^n p(z_i = k \vert x_i)} \\ \pi_k &= \frac{1}{n}\sum_{i=1}^n p(z_i = k \vert x_i) \\ \Sigma_k &= \frac{\sum_{i=1}^n p(z_i = k\vert x_i)(x_i - \mu_k)(x_i - \mu_k)^T}{\sum_{i=1}^n p(z_i = k \vert x_i)} \end{align*}$$

> [!info]
> Intuitively, the E-step calculates cluster assignments, and the M-step finds the most likely parameters based off the assignments.

# Prediction
Given point $x$, calculate $p(z = k \vert x)$ for each mixture; this gives a probability distribution over clusters, which is a soft classification (to get the hard classification, take the class with highest probability).