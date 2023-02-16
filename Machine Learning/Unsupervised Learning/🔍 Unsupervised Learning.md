# Theory
Unsupervised learning captures patterns in input data $x$; our model $f$ maps input $x$ to some form of structure.

> [!note]
> An alternative interpretation of the unsupervised objective is to find a low-dimensional projection of $x$ that captures most of the information but with less complexity. This compression implies some structure within the data.

# Clustering
One form of structuring is clusters, defined as groups of datapoints that are close together, with distance defined by some function $d$.
1. [[🎒 K-Means Clustering]] groups points into $k$ clusters so that each point belongs to exactly one cluster.
2. [[📼 Gaussian Mixture Model]] performs soft clustering, assigning each point a probability of belonging to each cluster.

# Dimensionality Reduction
Another type of structuring is dimensionality reduction, where we encode our feature space to into a lower-dimensional embedding space. [[🗜️ Principle Component Analysis]] finds embeddings that minimize distortion; these embeddings capture the most information from the original data.

# Disentanglement
Structure can also be thought of as "un-mixing" data to get back the original sources. [[🍝 Independent Component Analysis]] solves this problem by returning an output with maximum independence across its features.

# Bayesian Networks
Other structures are more artificial and can be specifically designed. We can capture them using a [[🚨 Bayesian (Belief) Network]], which graphically represent complex joint probability distributions over $x$ and latent $z$. Structuring these networks in certain ways and assigning each node a hidden or observable value, we get more advanced algorithms.
1. [[📄 Latent Dirichlet Allocation]] expands upon the mixture idea to classify documents, associating hidden topics with each document and word.
2. [[⛓️ Markov Chain]] models dynamic systems that transition between states.
3. [[☂️ Hidden Markov Model]]s convert an input sequence to an output sequence by moving between hidden states.