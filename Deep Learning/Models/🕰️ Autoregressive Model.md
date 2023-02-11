# Theory
Autoregressive models are often used to model time series data where the past gives some information about the present prediction.

We can think of the model as modeling a joint probability distribution $$p(x) = p(x_1,x_2,\ldots, x_n) = \prod_{i=1}^np(x_i \vert x_{<i})$$
where $p(x_i\vert x_{<i})$ means that our data at time $i$ is conditional on all data prior to time $i$.

An autoregressive model maps $x_1,\ldots, x_{i-1}$ to the mean of a Bernoulli distribution representing the probability of $x_i$.

# Model
Our model is usually an [[✏️ Artificial Neural Network]] that takes in the past data (usually a set window) and predicts the present.

# Training
Training is done by minimizing the [[📏 KL Divergence]] between the data and model probability distributions. In other words, from a generative sense, we want to maximize the chance that our model will generate our training data.

This loss can be directly optimizing via gradient descent.