# Theory
Q-Learning is a model-free, off-policy temporal difference learning method. The policy for selecting the immediate action, $\mu$, is now different from the policy we want to optimize, $\pi$; the former is an exploratory action using [[🧧 Epsilon-Greedy]] while the latter plays out exploitative actions that are always greedy.

> Greedy action is the action that maximizes $Q$, $\arg\max_a Q(s, a)$.

This is different from [[🧭 SARSA]] where $\pi$ is also exploratory. Q-Learning is generally preferred since it ultimately learns a greedy policy instead of an $\epsilon$-greedy one.

# Model
Our model includes the policy $\pi$ and the q-value function $Q_{\pi}(s, a)$.

**Hyperparameters**
- $\alpha$ is the learning rate for value estimation.
- $\gamma$ is the discount factor for future reward. Smaller factor means we care about the future reward less.
- $M$ is the number of episodes to train on. More episodes means more convergence.

# Training
Initialize $Q(s,a)$ arbitrarily except for $Q(\text{terminal}, \cdot) = 0$. Then, repeat the following for $M$ episodes.
1. Initialize $S$, then repeat until $S$ is terminal.
	1. Choose $A$ using policy derived from $Q$ with $\epsilon$-greedy.
	2. Take action $A$, observe $R$ and $S'$.
	3. Update $$Q(S,A) = Q(S,A) + \alpha[R + \gamma \max_a Q(S', a) - Q(S, A)]$$
	4. Update $S = S'$.