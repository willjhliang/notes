# Bayes' Theorem
Given events $X$ and $Y$, the following always holds. $$P(Y \vert X) = \frac{P(X \vert Y)P(Y)}{P(X)}$$
This is commonly used to reverse the conditionals or incorporate extra probabilities that we can find.

In bayesian terms, each element in the equation has a name. $$\text{posterior} = \frac{\text{likelihood} \cdot \text{prior}}{\text{evidence}}$$
The posterior is our belief for $Y$ given evidence $X$. The likelihood is the reverse, the probability of $Y$ given a fixed $X$. Finally, the prior is our initial belief for $Y$.

# Jensen's Inequality
For random variable $X$, if $\varphi$ is a convex function, we have $$\varphi(\mathbb{E}(X)) \leq \mathbb{E}(\varphi(X))$$
In other words, applying the function to the expectation after gives us a smaller value than applying it first. If we apply this to two possible values $x_1$ and $x_2$ with weights $t$ and $(1-t$, we can view it as the difference between the middle point on the pink versus black lines. The pink represents applying the average after $\varphi$, and the black represents finding the average before.

![[20230209085548.png]]