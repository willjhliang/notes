# Theory
Markov Decision Processes are used to model the environment, defining states, actions, transitions, and rewards.

They generalize Markov Chains, which use a transition matrix $M$ to move between states. Similar to [[☂️ Hidden Markov Model]], it also has emission matrix $B$ that produces observable outputs from the state. We now have a separate transition matrix $M^{(a)}$ for each action $a$, and our emission $x_t$ includes the reward $R_t$. 

Specifically, Partially Observable Markov Decision Processes (POMDPs) generalize Hidden Markov Models.

This model can be generalized with a neural network that outputs the next state given the current state and action, $s_{t+1} = f(s_{t}, a_t)$.

# Model
MDPs maintain a joint distribution combining transitions and emissions, $$p(s', r\vert s, a)$$
This can be split into separate transition probabilities and expected reward, $$p(s'\vert s, a) = Pr(S_{t+1}=s'\vert S_t=s, A_t = a) = \sum_r p(s', r\vert s, a)$$ $$r(s, a, s') = \mathbb{E}[R_{t+1}\vert S_t=s, A_t=a, S_{t+1}=s'] = \frac{\sum_r rp(s', r\vert s, a)}{p(s'\vert s, a)}$$
Using this information (along with the discount factor $\gamma$), we use an optimization strategy to find the policy $a_t = \pi(s_t)$ that maximizes $G_t$.

# Training
MDP probabilities are estimated through sampling as we optimize the policy. We can update the probabilities as we play by simply keeping track of the frequencies of each transition. If we instead use a neural network, we optimize it by pushing its predictions to be more similar to the state we end up in.

# Prediction
MDP is used with [[🧨 Dynamic Programming]] to learn a policy. It accurately predicts the states $s_{t+1}$ we can reach from $s$ and $a$ as well as the rewards; this information is used in the DP update step to estimate $Q$ values, which then gives us a policy.