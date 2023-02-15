# Theory
Unsupervised learning aims to capture patterns in input data $x$. In doing so, the algorithms find a low-dimensional projection of $x$, which captures most of the information but with less complexity.

# Dimensionality Reduction
In dimensionality reduction, we encode $x$ into an embedding.
1. [[🗜️ Principle Component Analysis]] is finds that embeddings that minimize distortion; in other words, these embeddings capture the most information from the original data.
2. [[🍝 Independent Component Analysis]] is similar to PCA but opts to maximize the variance of the projected data instead.

# Clustering
Another way to view dimensionality reduction is by grouping points together; each point can then be represented by the group it belongs to.
1. [[🎒 K-Means Clustering]] groups points into multiple clusters, which each point belonging to exactly one cluster.
2. [[📼 Gaussian Mixture Model]] is a generalization of this idea with soft clusters: each point has a probability of belonging to each group.

# Bayesian Networks
The models above hidden states that explained some underlying pattern in our data. We can capture these relationships using a [[🚨 Bayesian (Belief) Network]], which graphically represent complex joint probability distributions. Structuring these networks in certain ways and assigning each node a hidden or observable value, we get more advanced algorithms.
1. [[📄 Latent Dirichlet Allocation]] expands upon the mixture idea to classify documents, associating hidden topics with each document and word.
2. [[⛓️ Markov Chain]] models dynamic systems that transition between states.
3. [[☂️ Hidden Markov Model]]s convert an input sequence to an output sequence by moving between hidden states.