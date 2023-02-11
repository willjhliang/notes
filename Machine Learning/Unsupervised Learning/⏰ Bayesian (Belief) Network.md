# Theory
Bayesian networks are a graphical representation of conditional independence (and dependence) assertions over a complex joint distribution.
1. Each node is a random variable that has conditional distribution $p(x_i \vert \text{parents} (x_i))$. 
2. Each directed edge is an conditional dependence assertion.

The following is an illustration of a simple network.

![[20221229103135.png|500]]

The Local Markov Assumption states that every variable is independent of its non-descendants given its parents. Thus, each node in our network is only affected by certain other nodes depending on the edges between them. We can find these dependencies with active trails.

Active trails represent flow of information; variables connected by an active trail are not conditionally independent. For each triplet $X, Y, Z$ in the trail, one of the following must be true.
1.  $X \rightarrow Y \rightarrow Z$, $Y$ not observed.
2.  $X \leftarrow Y \leftarrow Z$, $Y$ not observed.
3.  $X \leftarrow Y \rightarrow Z$, $Y$ not observed.
4.  $X \rightarrow Y \leftarrow Z$, $Y$ observed or one of its descendants is observed.

If there is no active trail between $X_i$ and $X_j$ given a set of observed variables $O$, they are conditionally independent and are D-separated.

A more connected network represents a distribution with few conditional independences. Each conditional independence limits the size of the class of distributions that satisfy it, so a more connected network models a larger class of joint probability distributions.

# Model
Our model consists of nodes for random variables containing conditional probability distributions (usually discrete or Gaussian) and edges for conditional dependence assertions. The graph must be acyclic.

# Training
Belief nets can be manually built with prior information and by estimating probabilities from data.

Otherwise, its possible to “learn” a network given data $D$ through stochastic gradient descent (or annealing).
1. Randomly change the network by one link and re-estimate its parameters.
2. If the loss is lower, accept this change.

The network can also include hidden variables that can be optimized with [[🎉 Expectation Maximization]]: estimate model parameters given hidden variables, then find expected value of hidden variables given new parameters.

# Prediction
The probability of a certain random variable can be predicted by going up the network and computing the product mathematically.