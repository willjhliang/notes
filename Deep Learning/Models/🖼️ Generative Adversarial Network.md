# Theory
GANs are generative models that learn via an adversarial process. It consists of a generative and a discriminative network; the former generates samples from a random latent space, and the latter ties to distinguish between generative outputs and samples from the training data.

# Model
Our model consists of generative and discriminative models, each usually implemented as a [[👁️ Convolutional Neural Network]].

# Training
We alternate between training the generative and discriminative models.

For the former, we get a random vector, generate the sample, and optimize the generative weights to decrease the discriminative model's predicted probability of fake. For the latter, we train it like a normal image classifier on training data and generative outputs.

# Prediction
To generate a new image, we feed random noise to the generative model.

We can also integrate conditions (male or female, for example) in the generation by modifying both models to also take in the condition as an input, then training on both the samples and outputs as well as conditions. For prediction, we can then give random noise and the condition to the generative model.