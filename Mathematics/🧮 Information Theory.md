# Entropy
Entropy is the average level of "surprise" or "uncertainty" in a probability distribution. The surprise of an individual event $y$ is inversely correlated with the probability of the event happening (we would be surprised if an improbable event happened), so we quantify surprise as  $$\lg (1/P(Y=y)) = -\lg P(Y=y)$$
> Applying log to the inverse changes the bound from $[1, \infty)$ to $[0, \infty]$.

By combining all events together with an expected value, we get the entropy equation $$H(Y) = -\sum_y P(Y=y)\lg P(Y=y)$$
Another way to interpret this is the expected number of bits needed to encode $Y$ or number of questions needed to guess $Y$. Tying it all together: the more average surprise we have, the more uncertain we are about the results; the more uncertainty there is, the more bits we need to encode the distribution.

> Uncertainty is a measure of the variance of a distribution. A distribution with high entropy or uncertainty would be roughly uniform.

Below is a graph of the entropy of binary variable $X$. Highest entropy is when probability is $\frac{1}{2}$, and as probability goes toward one extreme, entropy decreases since $X$ becomes less random.

![[20221229103244.png|200]]

# Information Gain
If we're given more information about a distribution, entropy decreases. Specifically, for the distribution $Y$ that has some correlation with $X$, if we learn the value of $X = x$, we narrow the range of results of $Y$ and thereby decrease entropy.

Averaging over the probability of all $X = x$ that we can know, we get the equation for conditional entropy, $$H(Y \vert X) = \sum_x P(X=x)H(Y\vert X=x)$$
The decrease in entropy caused by us knowing $x$ is known as information gain. $$IG(X) = H(Y) - H(Y \vert X)$$

# Cross Entropy
Cross entropy applies entropy to two distributions: $P$ is the true distribution, and $Q$ is the predicted distribution. We now measure the entropy we get if we encode using our predicted distribution but have events happen according to the true distribution. In other words, our surprise is defined by our predicted probabilities while the expected value uses the actual, true probabilities of the event happening.

Putting $P$ and $Q$ in their respective spots in the original equation, we get $$H(P, Q) = -\sum_x P(X=x) \lg Q(X=x)$$
Note that if $P$ and $Q$ are equal, then cross entropy is equal to entropy. Otherwise, the cross entropy is higher than true entropy $H(P)$: if we use an imperfect predicted distribution, our bit encoding won't be as optimal as if we knew the true distribution.