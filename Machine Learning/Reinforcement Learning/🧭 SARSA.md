# Theory
SARSA is a model-free, on-policy temporal difference learning method. Its policy is inherently exploratory, using [[🧧 Epsilon-Greedy]] to choose its next move.

To end up with a policy that plays as best as possible, we need to anneal $\epsilon$, which decreases the probability of our target policy choosing a random exploratory move.

# Model
Our model includes the policy $\pi$ and the q-value function $Q_{\pi}(s, a)$.

# Training
First, initialize $Q(s, a)$ arbitrarily except for $Q(\text{terminal}, \cdot) = 0$. Then, repeat the following for $M$ episodes.
1. Initialize $S$ and choose $A$ using policy derived from $Q$ with $\epsilon$-greedy.
2. Repeat until $S$ is terminal.
	1. Take action $A$, observe $R$ and $S'$.
	2. Choose $A'$ from $S'$ using policy derived from $Q$ with $\epsilon$-greedy.
	3. Update $$Q(S, A) = Q(S, A) + \alpha [R + \gamma Q(S', A') - Q(S, A)]$$
	4. Update $S = S'$ and $A = A'$.