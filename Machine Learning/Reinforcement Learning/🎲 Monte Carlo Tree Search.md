# Theory
Monte Carlo Tree Search is a model-free method that evaluates and improves a policy by directly sampling (playing) the environment through multiple episodes. In other words, our statistics are empirical.
1. $V_\pi(s)$ is the average of returns $G$ following all visits to $s$ in our episodes.
2. $Q_\pi(s, a)$ is the average of returns $G$ following all visits to $(s, a)$ in our episodes.

Like other methods, it alternates between evaluation and improvement.

We generally use [[🧧 Epsilon-Greedy]] off-policy play, exploring on our first move and exploiting the rest. However, there are better ways to choose random moves. Below are some ways to “rank” the non-greedy moves, and we pick the best.
1. Low visit count.
2. High move probability under policy $\pi$.
3. High value based on a neural network.

This optimization strategy is especially effective with self-play. In each episode, we let the opponent also play using the policy and evaluate the value of the policy playing against itself.

# Model
Our model includes the policy $\pi$ and the value or q-value functions $V_\pi(s)$ and $Q_{\pi}(s, a)$.

# Training
Policy learning alternatives between evaluation and improvement until the policy stops changing.

To evaluate a policy $\pi$, first initialize $V(s)$ arbitrarily, and let $Returns(s)$ be an empty list. Then, loop for $M$ episodes.
1. Generate an episode by acting with $\pi$ until termination.
2. Initialize $G = 0$.
3. Go backwards through the episode's steps, $t = T-1, \ldots, 0$.
	1. Update $G = \gamma G + R_{t+1}$, essentially calculating the long-term reward for the current state $S_t$.
	2. If $S_t$ does not appear again in a previous step (this is the earliest point in our episode where we see $S_t$), add $G$ to $Returns(S_t)$ and update $$V(S_t) = \text{average}(Returns(S_t))$$
The above algorithm can also be modified to record actions as well, which allows us to also calculate $Q(S_t, A_t)$.

Our new policy will greedily take the best action for each state, $$\pi(S_t) = \arg\max_a Q(S_t, a)$$