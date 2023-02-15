# Theory
In reinforcement learning, the goal is to learn a policy function $p(a \vert s)$ that maximizes the agent's total reward. The feedback loop is below. Our environment includes both the game as well as an opponent, if it exists.

![[20221229103234.png|400]]

Reward is the result of taking an action at a certain state, $r(s, a)$. In some games, this is only nonzero at the end (for a win or loss). Most models also have a discount rate $\gamma$ that decreases the magnitude of future reward; this represents the importance of future gains with respect to current ones.

The sole exception to this format is [[🎰 Contextual Bandit]], which considers only immediate reward, ignoring the action's impact on its state and future reward.

Discounted reward, or long-term return, is defined as $$G_t = R_{t+1} + \gamma R_{t+2} + \gamma^2 R_{t+3} + \ldots = \sum_{k=0}^\infty \gamma^k R_{k+t+1}$$
## Value Functions
This idea is captured in $V_\pi(s_t)$ and $Q_\pi(s_t, a_t)$, the expected value of a state or state-action pair.
1. For $V$, expected value is discounted reward starting from $s_t$ and assuming we act according to policy $\pi$ in the future.
2. For $Q$, expected value is discounted reward starting from $s_t$ and taking action $a_t$, then assuming we act according to policy $\pi$ for all moves after $a_t$.

Learning algorithms optimize $V$ or $Q$ values to derive a policy. They can be model-based or model-free: the former learns a model of the world while the latter optimizes itself without it.

# Model-Based Learning
Model-based methods explicitly learn about the environment $p(s_{t+1} \vert s_t, a_t)$ and $r(s_t, a_t)$. Using this information, they derive a policy.
1. [[🌎 Markov Decision Process]] models the world using states, action transitions, and the resulting reward.
2. [[🧨 Dynamic Programming]] derives the policy by checking the possible moves for each state.

# Model-Free Learning
Model-free methods learn $V$ and $Q$ by directly playing in the environment.
1. [[⌛️ Temporal Difference (0)]] is a generalized algorithm that iteratively takes a single action and learns better $V$ or $Q$ values.
2. [[🧭 SARSA]] is a variant of TD(0) that uses on-policy, exploratory updates.
3. [[🔭 Q-Learning]] is another variant of TD(0) that uses off-policy exploratory actions to optimize a exploitative policy.
4. [[🌲 Monte Carlo Tree Search]] simulates entire games first before optimizing its values.

[[🛸 Deep Q-Learning]] is at the intersection of reinforcement learning and deep learning. Whereas SARSA and Q-Learning kept its $Q(s, a)$ values in a table, it can instead be interpreted as a function captured by a neural network. This generalization provides additional capabilities.
1. We can directly model the policy $\pi_\theta(a \vert s)$ with a neural network and optimize via policy gradients.
2. Imitation learning learns from the actions a human took at each state and computing a probability distribution via empirical data.
3. Self-play pits the learned policy against itself in games that have opponents.

One slightly different style of reinforcement learning, bridging the gap with active learning, is [[🚒 Response Surface Methods]], used to sample points for some objective.