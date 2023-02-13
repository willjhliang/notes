> [!warning]
> Sorry, this note is under construction. Feel free to take a look at what I've got so far, and please come back later!

The evidence (or variational) lower bound (ELBO) operates on a joint distribution on observed data $x$ and latent variables $z$. With likelihood-based models, we want the model to maximize the likelihood of data $p(x)$. We can calculate likelihood by marginalizing over latent $z$ or using the chain rule.
1. $$p(x) = \int p(x, z) dz$$
2. $$p(x) = \frac{p(x, z)}{p(z \vert x)}$$
Both methods pose a challenge: the former requires us to integrate over all latent variables, which is often intractable, and the latter requires knowing the ground truth latents $p(z|x)$. The ELBO serves to lower bound the evidence, defined here as the log likelihood of $x$. *By maximizing the ELBO, we also optimize for $p(x)$.*

==The inequality below shows the evidence on the left bounded by the ELBO on the right. $$\log p(x) \geq \mathbb{E}_{q_\phi(z|x)}\left[\log \frac{p(x, z)}{q_\phi(z|x)}\right]$$ where==