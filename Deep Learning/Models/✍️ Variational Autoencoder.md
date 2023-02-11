# Theory
VAE is a modification of the standard [[🧬 Autoencoder]] that uses probability distributions in the latent space instead of hard values. Our decoder samples from the latent distribution to generate the reconstruction.

We use a probability distribution to force the decoder to recognize that small changes in the sampled latent vector should result in minor changes to the final image. For example, on a single training image, we can have multiple slightly-different sampled latent vectors, and the decoder must learn that they all correspond to the same image.

However, with multiple training examples, it's still possible for the encoder to generate completely different distributions with low variance and different means, essentially acting as a normal autoencoder. We can mitigate this by regularizing the probability distribution in our loss function, forcing them all to be similar to the standard normal $\mathcal{N}(0, I)$.

By regularizing the distributions, we force the latent space to be a smooth distribution where any chosen point in the space can be meaningfully reconstructed. We can then use the VAE decoder as a generative model that can create novel samples.

The following picture represents the latent space for a model with only reconstruction loss, a model with only distribution regularization, and a successful VAE with both.
![[20230105112139.png]]

The third graph shows the smooth latent space that merges the distributions of all classes together. Any chosen point can be decoded, as exemplified below.

![[20230105112246.png]]

# Model
Our model consists of encoder and decoder neural networks. The encoder predicts the mean and variance of each variable's distribution in our latent space instead of the variable's actual value.

# Training
We optimize our networks on the reconstruction $L_2$ loss and regularization loss, defined as the [[📏 KL Divergence]] between the latent distribution and $\mathcal{N}(0, I$). We backpropagate the gradient through the decoder and encoder, using the reparameterization trick to propagate through the sampling process.

# Prediction
To generate a new sample, we pick a random spot in the latent space and send it through the decoder.