EM is a general algorithm that trains models with hidden variables; it alternates between the expectation (E) and maximization (M) steps, iteratively improving the model.

For each iteration, we first estimate the hidden variables given the model, then estimate the model given the hidden variables. The formal procedure is as follows.

Given training data $D$ and a model with hidden variables $z$ and parameters $\theta$, iterate until convergence.
1. E-step estimates $P(z = k \vert D)$, the probability of hidden variables being a specific value, to find the expected value of each hidden variable $z$.
2. M-step estimates $P(\theta \vert z)$ using the probabilities of $z$ calculated above and similarly  finds the MLE or MAP of the parameters.