# Theory
Autoencoders generalize [[🗜️ Principle Component Analysis]] with an [[✏️ Artificial Neural Network]] or [[👁️ Convolutional Neural Network]]; the hidden layer of the neural network is analogous to $z_i$, the compressed form of $x_i$.

Using the neural network, we still optimize weights to minimize $L_2$ reconstruction error. However, with a standard neural network, it’s easy to perfectly fit the training data; therefore, we impose one or more constraints.
1.  Bottleneck, where the hidden layer has dimension $k < p$.
2.  Input noise, making a de-noising autoencoder.
3.  $L_1$ or $L_2$ regularization penalties.
4.  Forcing orthogonality or independence.

> Note that PCA uses the bottleneck and orthogonality constraints, and ICA uses the bottleneck and independence constraints.

Variational autoencoders employ encoder and decoder neural networks, but in between them is a sampling procedure. The encoder produces multiple normal distributions $\mathcal{N}(\mu_x, \sigma_x)$; we sample a point $z$, then pass it through the decoder to get $\hat{x}$. The loss is $$\Vert x - \hat{x}\Vert^2 + KL[\mathcal{N}(\mu_x, \sigma_x), \mathcal{N}(0, 1)]$$with the second part included for regularization.

# Model
Standard autoencoders are implemented as neural networks, following the same model structure and properties. Encoder and decoder segments are usually symmetric.

# Training
Given training data $D$, we can train using the same method as standard neural networks.

An alternative is the stacking method, which trains layers one at a time.
1. For each hidden layer $L_i$, take the values from $L_{i-1}$, then process it and feed it to $L_{i+1}$.
2. Optimize $L_i$ to reconstruct $L_{i-1}$ in $L_{i+1}$; in other words, we’re training $L_i$ to learn to reconstruct intermediate features in the neural network.

# Prediction
Given input $x$, run it through the neural network and take the hidden layer embedding that we designed in our model to be $z$.