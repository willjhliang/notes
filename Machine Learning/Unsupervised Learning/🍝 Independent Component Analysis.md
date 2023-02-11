# Theory
ICA is an alternative to [[🗜️ Principle Component Analysis]] where we find $S$ and $W$ such that embeddings or scores $s_j$, analogous to $z_j$ from PCA, are as independent as possible, with maximum [[📏 KL Divergence]] or low mutual information.
$$ X = SW^+ $$
$W^+$ is analogous to loadings, and $S$ are principal component scores.

Maximizing independence of embeddings is known as disentanglement; ideally, each feature in $s^{(i)}$ represents an independent source that formed the original $x^{(i)}$; one example is un-mixing two voices from two recordings.

# Training
Our loss function includes both reconstruction loss and mutual information. In other words, we want to both minimize the reconstruction error as well as mutual information between sources $s_j$, defined as $$I(s_1,\ldots s_k) = \sum_{j=1}^kH(s_j) - H(s)$$
Another interpretation of mutual information is with KL divergence, measuring the similarity between the joint distribution and combination of independent distributions $$KL(p(s_1, \ldots, s_k)\Vert p(s_1)p(s_2)\ldots p(s_k))$$

This loss function is not quadratic, so optimization cannot be done with [[📎 Singular Value Decomposition]]. The optimization method was not covered in class.

# Prediction
Similar to PCA, we project $x^{(i)}$ onto components to get the scores of our embedding, and apply them to our components to recreate $x^{(i)}$.