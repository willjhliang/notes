# Theory
TD(0) is the most basic model-free policy evaluation algorithm. It learns the $V$ or $Q$ values of a policy by performing only one action.

To train an agent, we alternate between TD(0) to approximate the policy values, then construct a better policy based on these values.
1. Find more accurate value function $V_{\pi'}(s)$ given policy $\pi'$.
2. Find a better policy $\pi'$ given value function $V_{\pi}(s)$.

This is a general idea which can be extended to more concrete implementations. [[🔭 Q-Learning]] is a variant that uses off-policy updates whereas [[🧭 SARSA]] is a variant with on-policy exploratory updates.

# Model
Our model includes the policy $\pi$ and the value function $V_{\pi}(s)$. TD(0) can also be adapted to work with $Q_\pi(s, a)$ instead.

# Training
To optimize $\pi$ and $V_{\pi}(s)$, we alternate between value estimation and policy updates.

For value estimation, given a policy $\pi$, we want to find $V_{\pi}(s)$.

First, initialize $V_{\pi}(s)$ arbitrarily except for $V_{\pi}(\text{terminal}) = 0$. Then, loop for $M$ episodes.
1. Initialize $S$ to the starting state.
2. Loop until $S$ is terminal.
	1. Take action $A$ given by $\pi$ for $s$, observe $R$ and $S'$.
	2. Update $V_{\pi}(S) = V_{\pi}(S) + \alpha[R + \gamma V_{\pi}(S') - V_{\pi}(S)]$.
	3. Update current state $S = S'$.

Note that the value $R + \gamma V_{\pi}(S')$ is a "better" guess for $V_{\pi}(S)$, so we update $V_{\pi}(S)$ with the difference, or error, scaled by the learning rate.

The policy update step varies.
1. With $V$ values, it's commonly optimized using an idea analogous to stochastic gradient descent, checking if changing the policy in some way results a better initial value.
2. With $Q$ values, we simply take the action that maximizes $Q$ greedily or encourage exploration with [[🧧 Epsilon-Greedy]].