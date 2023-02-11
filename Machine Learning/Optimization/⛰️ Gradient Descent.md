Gradient Descent is a method of optimizing model weights, commonly used when there’s no direct closed form solution; other online methods also use gradient descent when closed form solutions are too expensive to compute.

$$ \theta := \theta - \alpha\frac{\partial}{\partial\theta}J(\theta) $$

Note that this formula is applied over all datapoints in the training data.

> Learning rate $\alpha$ must be carefully chosen. If it's too large, the model won't converge. If it's too small, the model will converge too slowly.

Below is a graphical representation with two weights $\theta_1$ and $\theta_2$, with the inner-most blue ring representing the global minimum $J(\theta)$
![[20221229103152.png|400]]
Due to computational costs, there are multiple strategies to update the weights $\theta$.
1.  Batch gradient descent updates weights after going through the entire dataset $X$
2.  Stochastic gradient descent updates weights after computing the derivative for a single datapoint $x^{(i)}$, resulting in oscillations but decreasing convergence duration
3.  Mini-batch gradient descent is a balance between the two, updating weights after checking $B$ datapoints