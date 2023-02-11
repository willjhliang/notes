# Theory
Dynamic programming trains a [[🌎 Markov Decision Process]] using Bellman's equation $$V_{\pi}(s) = \sum_a \pi(a \vert s) \sum_{s', r} p(s', r \vert s, a)[r + \gamma V_\pi(s')]$$ for policy iteration optimization and Bellman's optimality equation $$V_*(s) = \max_a \sum_{s', r} p(s', r \vert s, a)[r + \gamma V_*(s')]$$ for value iteration optimization.

# Model
We're given the MDP model, and dynamic programming can use policy or value iteration to find the optimal policy. We maintain the policy $\pi$ and value function $V_\pi(s)$.

# Training
Both policy and value iteration can find the optimal policy.

## Policy Iteration
Initialize value $V(s)$ and policy $\pi(s)$ arbitrarily. Then, we'll alternate between policy evaluation and improvement until the policy stops changing.

For policy evaluation, repeat the following until convergence.
1. For each state $s$, update $$V(s) = \sum_{s', r} p(s', r \vert s, \pi(s))[r + \gamma V(s')]$$
For policy improvement, go through each state $s$,
1. Update $$\pi(s) = \arg\max_a \sum_{s', r} p(s', r \vert s, a)[r + \gamma V(s')]$$

## Value Iteration
Instead of alternating between updating policies and values, we'll optimize values first and then derive a policy from it.

First, initialize value $V(s)$ arbitrarily. Then, repeat until convergence.
1. For each state $s$, update $$V(s) = \max_a\sum_{s', r} p(s', r \vert s, a)[r + \gamma V(s')]$$
Then, our policy is defined like above, $$\pi(s) = \arg\max_a \sum_{s', r} p(s', r\vert s, a) [r + \gamma V(s')]$$

# Prediction
With a trained policy, we simply act following it, performing $\pi(s)$ when we're at state $s$.