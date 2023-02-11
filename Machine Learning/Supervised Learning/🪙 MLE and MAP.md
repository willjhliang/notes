# Theory
Given historical data $D$, we can estimate the probabilities $\theta$ that generated this data.
1. With Maximum Likelihood Estimate (MLE), we find $\theta$ that maximizes the likelihood of generating $D$.
2. With Maximum A Posteriori (MAP), we already have some pre-existing hypothesis about our probabilities, termed a prior $P(\theta)$, and use our new data $D$ to update our hypothesis. In other words, we find $\theta$ that’s most likely explained by $D$ as well as our prior.

MLE and MAP are general ideas that can be applied to many machine learning algorithms. For the sake of illustration, the following uses a extremely simple problem: estimating the probability a coin lands heads.

Let $D$ be a set of coin-flip results, with $n_H$ heads and $n_T$ tails, and let $\theta$ be the probability of the coin landing heads.

# Training
For MLE, find $\theta$ that maximizes the probability of $D$ occurring, called the likelihood $P(D \vert \theta)$.
$$ \begin{align*} \hat{\theta}_{MLE} &= \arg\max_\theta(P(D \vert \theta)) \\ &= \arg\max_\theta(\log(P(D \vert \theta)) \\ &= \arg\max_\theta n_H\log(\theta) + n_T\log(1-\theta) \\ &= \frac{n_H}{n_H + n_T} \end{align*} $$

> Note that in the equation above, we find the $\arg\max$ over log-likelihood instead of likelihood. This works because log is monotonically increasing, and computing log-likelihood simplifies the math and avoids overflow errors.

For MAP, find $\theta$ that maximizes the probability of $\theta$ given that $D$ occurred, called the posterior $P(\theta \vert D)$ (since this is our revised prior after considering new data $D$). For conjugacy, let $$P(\theta) = Beta(\alpha, \beta) = \frac{\Gamma(\alpha + \beta)}{\Gamma(\alpha) \Gamma(\beta)} \theta^{\alpha-1} (1-\theta)^{\beta - 1}$$follow the same family of distributions as the likelihood and posterior. Then, we can maximize the posterior with [[🪙 Probability Theory#Bayes' Theorem]].
$$ \begin{align*} \hat{\theta}_{MAP} &= \arg\max_\theta(P(\theta \vert D)) \\ &= \arg\max_\theta(P(D \vert \theta)P(\theta)) \\ &= \arg\max_\theta(\log P(D \vert \theta) + \log P(\theta)) \\ &= \frac{n_H+\alpha-1}{n_H+n_T+\alpha+\beta-2} \end{align*} $$