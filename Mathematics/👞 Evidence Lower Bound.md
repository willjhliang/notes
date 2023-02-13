> [!warning]
> Sorry, this note is under construction. Feel free to take a look at what I've got so far, and please come back later!

The evidence (or variational) lower bound (ELBO) operates on a joint distribution on observed data $x$ and latent variables $z$. With likelihood-based models, we want to find parameters that maximize the likelihood of our model generating our data, given by $p(x)$. We can calculate likelihood by marginalizing over latent $z$ or using the chain rule.
1. $$p(x) = \int p(x, z) dz$$
2. $$p(x) = \frac{p(x, z)}{p(z \vert x)}$$
Both methods pose a challenge: the former requires us to integrate over all latent variables, which is often intractable, and the latter requires knowing the ground truth latents $p(z|x)$. The ELBO serves to lower bound the evidence, defined here as the log likelihood of $x$. *By training a model to maximize the ELBO, we also maximize $p(x)$.*

The inequality below shows the evidence on the left bounded by the ELBO on the right. $$\log p(x) \geq \mathbb{E}_{q_\phi(z \vert x)}\left[\log \frac{p(x, z)}{q_\phi(z \vert x)}\right]$$
where $q_\phi(z \vert x)$ is an approximate variational distribution with parameters $\phi$ that we want to optimize. The ELBO derivation is as follows.

$$\begin{align*}\log p(x) &= \log p(x) \int q_\phi(z \vert x) dz \\ &= \int q_\phi(z \vert x) \log p(x) \\ &= \mathbb{E}_{q_\phi(z \vert x)}[\log p(x)] \\ &= \mathbb{E}_{q_\phi(z \vert x)} \left[\log\frac{p(x, z)}{p(z \vert x)}\right] \\ &= \mathbb{E}_{q_\phi(z \vert x)} \left[ \log \frac{p(x, z)}{q_\phi(z \vert x)}\right] + \mathbb{E}_{q_\phi(z \vert x)} \left[\log \frac{q_\phi(z \vert x)}{p(z \vert x)}\right] \\ &= \mathbb{E}_{q_\phi(z \vert x)} \left[\log \frac{p(x, z)}{q_\phi(z \vert x)}\right] + D_{KL}(q_\phi(z \vert x) \Vert p(z \vert x)) \\ &\geq \mathbb{E}_{q_\phi(z \vert x)} \left[\log \frac{p(x, z)}{q_\phi(z \vert x)}\right]\end{align*}$$

Notably, this derivation shows that the gap between the ELBO and evidence is exactly the [[📏 KL Divergence]] between our approximate posterior $q_\phi(z \vert x)$ and the true posterior $p(z \vert x)$. Moreover, by maximizing the ELBO, we not only maximize $p(x)$ but also minimize our KL term