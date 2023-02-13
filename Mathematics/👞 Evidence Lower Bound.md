We can think of observed data $x$ as generated from latent variables $z$. The evidence (or variational) lower bound (ELBO) deals with a joint distribution on observed data $x$ and latents $z$.

With likelihood-based models, we want to approximate the data distribution (such as a distribution of cat images) $p(x)$ with a model $p_\theta(x)$ that has parameters $\theta$. A good approximation has a high probability of generating our data $x$, so we optimize parameters $\theta$ to maximize $p_\theta(x)$, the likelihood of our model generating our data.

We can calculate likelihood in two ways.
*  By marginalizing over latent $z$. $$p_\theta(x) = \int p_\theta(x, z) dz$$
- By using the chain rule of probability. $$p_\theta(x) = \frac{p_\theta(x, z)}{p_\theta(z \vert x)}$$

Both methods pose a challenge: the former requires us to integrate over all latent variables, which is often intractable, and the latter requires knowing the ground truth latents $p(z \vert x)$. The ELBO serves to lower bound the evidence, defined here as the log likelihood of $x$. *By training a model to maximize the ELBO, we also maximize $p_\theta(x)$.*

The inequality below shows the evidence on the left bounded by the ELBO on the right. $$\log p_\theta(x) \geq \mathbb{E}_{q_\phi(z \vert x)}\left[\log \frac{p_\theta(x, z)}{q_\phi(z \vert x)}\right] = \text{ELBO}$$
where $q_\phi(z \vert x)$ is a distribution with parameters $\phi$ that we use to approximate $p_\theta(z \vert x)$. The inequality derivation is as follows.

$$\begin{align*}\log p_\theta(x) &= \log p_\theta(x) \int q_\phi(z \vert x) dz \\ &= \int q_\phi(z \vert x) \log p_\theta(x) \\ &= \mathbb{E}_{q_\phi(z \vert x)}[\log p_\theta(x)] \\ &= \mathbb{E}_{q_\phi(z \vert x)} \left[\log\frac{p_\theta(x, z)}{p_\theta(z \vert x)}\right] \\ &= \mathbb{E}_{q_\phi(z \vert x)} \left[ \log \frac{p_\theta(x, z)}{q_\phi(z \vert x)}\right] + \mathbb{E}_{q_\phi(z \vert x)} \left[\log \frac{q_\phi(z \vert x)}{p_\theta(z \vert x)}\right] \\ &= \mathbb{E}_{q_\phi(z \vert x)} \left[\log \frac{p_\theta(x, z)}{q_\phi(z \vert x)}\right] + D_{KL}(q_\phi(z \vert x) \Vert p(z \vert x)) \\ &\geq \mathbb{E}_{q_\phi(z \vert x)} \left[\log \frac{p_\theta(x, z)}{q_\phi(z \vert x)}\right]\end{align*}$$

From the second-to-last equation, we observe that the gap between the ELBO and evidence is exactly the [[📏 KL Divergence]] between our approximate posterior $q_\phi(z \vert x)$ and the true posterior $p(z \vert x)$.

Then, rewriting the equality, we get $$\text{ELBO} = \mathbb{E}_{q_\phi(z \vert x)} \left[\log\frac{p_\theta(x, z)}{q_\phi(z \vert x)}\right] = \log p_\theta(x) - D_{KL}(q_\phi(z \vert x) \Vert p(z \vert x))$$

Maximizing the ELBO is thus equivalent to maximizing $p_\theta(x)$ and minimizing our KL term; the latter outcome is equivalent to finding the best approximation $q_\phi(z \vert x)$ for $p_\theta(z \vert x)$. In other words, maximizing the ELBO gives us an accurate generative model $p_\theta(x)$ and an accurate discriminative model $q_\phi(z \vert x)$, where $p_\theta(x) \approx p(x)$ and $q_\phi(z \vert x) \approx p_\theta(z \vert x) \approx p(z \vert x)$.

> [!info]
> Assuming $p_\theta(x) = p(x)$, we can interpret the ELBO objective as fitting $q_\phi(z \vert x)$ to some true unknown distribution $p(z \vert x)$. Since $p(x)$ is fixed relative to $\phi$, maximizing the ELBO is equivalent to minimizing the KL term in the equality.