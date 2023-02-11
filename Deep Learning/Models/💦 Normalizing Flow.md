# Theory
Normalizing flows transform a simple latent distribution into the distribution of a dataset. This allows us to sample new images from the dataset distribution.

> Unlike other generative models, normalizing flow models capture an exact, invertible transformation rather than an approximation.

Our transformation is the function $f$ such that $X = f_\theta(Z)$. Our goal is to maximize the likelihood $$p(x; \theta) = p_Z(f_\theta^{-1}(x)) \left\lvert \det \frac{\partial f_\theta^{-1}(x)}{\partial x} 
\right\rvert$$

# Model
The model consists of multiple invertible functions stacked on top of each other. By composing them together and training to maximize the likelihood of the data, we can generate new samples by feeding random noise into $f$.