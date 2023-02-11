# Theory
Deep Q-Learning generalizes [[🔭 Q-Learning]] with neural networks. Instead of a table $Q(s, a)$, it represents $Q(s, a)$ with a neural network. The loss function is the squared TD loss $$(R+\gamma\max_{a'}Q(s',a') - Q(s,a))^2$$ Note that this is the term contained within $\alpha$ in Q-Learning from the update rule $$Q(S,A) = Q(S,A) + \alpha[R + \gamma \max_a Q(S', a) - Q(S, A)]$$
The policy can then be derived with $\pi(a \vert s) = \arg\max_a Q(s, a)$.

One problem with the loss function is that it includes $Q(s', a')$. If we update our network to decrease the error for $Q(s, a)$, we're also changing the target $Q(s', a')$, making it harder to converge. There are two main solutions.
1. Keep another neural network, called the target network, to compute $Q(s', a')$. The weights of this network are older versions of the weights of our current network; they're updated occasionally during training to "catch up" to the current network. With this, we perform gradient descent after every action, similar to [[🔭 Q-Learning]].
2. Use [[🎲 Monte Carlo Tree Search]] to empirically find values for $Q$ using the policy derived from our network. Then, perform gradient descent after all episodes are finished to shift $Q(s, a)$ closer to the average values found during the episodes.

For games with opponents, $Q(s', a')$ is instead the opponent network, which has negated values. Our update now checks each action's result given that the opponent (an older version of our current network) plays optimally, similar to mini-max. Using two networks in this fashion is called self-play.

Another addition to Q-Learning is the use of replay memory $\mathcal{D}$. Instead of optimizing the network with the most recent action, the algorithm instead chooses a random subset of $(s, a, r, s')$ pairs in $\mathcal{D}$ for gradient updates. This allows each episode step to be used for multiple weight updates and also breaks the correlation between consecutive actions, which reduces the variance of the updates.

> Correlation between actions increases variance because a slight change in earlier actions can have huge impacts on the states and actions we see in the future.

# Model
The model consists of a $Q$-network representing the $Q(s, a)$ function. In some models, we also maintain a target network to decrease instability.

Traditionally, a $Q$-network takes as input the most recent frames of the environment (history) and action, then outputs the $Q$ value. A more optimized approach uses the $Q$-network to take in only the history, then output $Q$ values for each possible action; therefore, we only require one forward pass instead of one per action.

# Training
Initialize replay memory $\mathcal{D}$ and $Q$-network weights $\theta$. Then, run for $M$ episodes.
1. Initialize state $s_t$.
2. For $T$ steps,
	1. Choose an action $a_t$ using the $Q$-network with [[🧧 Epsilon-Greedy]]
	2. Take action $a_t$, observe $r_t$ and $s_{t+1}$.
	3. Store $(s_t, a_t, r_t, s_{t+1})$ in $\mathcal{D}$.
	4. Sample a random mini-batch of transitions from $\mathcal{D}$, and for each, let $$y_j = r_j + \gamma\max_{a'}Q(s_{j+1}, a_{j+1}; \theta)$$ and perform gradient descent on $$(y_j - Q(s_j, a_j; \theta))^2$$