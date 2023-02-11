The difference in [[🧮 Information Theory#Cross Entropy]] and [[🧮 Information Theory#Entropy]] is known as KL divergence $$\mathcal{D}(P \Vert Q) = H(P, Q) - H(P) = -\sum_x P(X = x) \lg \frac{Q(X=x)}{P(X=x)}$$
This value can be interpreted as the expected extra number of bits to transmit using our predicted $Q$ instead of true $P$. It's equal to $0$ if $P = Q$.

> Note that this value is non-symmetric, non-negative, and does not satisfy triangle inequality.

We commonly see KL divergence or cross entropy used as loss functions in categorization problems (for example, in [[🦠 Logistic Regression]]). The truth label $P$ is a one-hot encoding, and our prediction $Q$ consists of softmax probabilities. In this case, our KL divergence simplifies to $$\mathcal{D}(P \Vert Q) = -\lg Q(Y=k)$$
for a single datapoint where $k$ is the true label. Moreover, since the entropy of the true labels is constant regardless of our model's predictions, we can instead just use cross entropy $H(P, Q)$ as our loss function.

We can also apply KL divergence to [[🧮 Information Theory#Information Gain]]. Rather than computing it as the difference in entropies before and after knowing $X$, it can instead be interpreted as the difference in distributions $$IG(x) = \mathcal{D}(P(Y \vert X) \Vert P(Y))$$