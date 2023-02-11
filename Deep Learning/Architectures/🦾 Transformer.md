# Theory
Transformers are encoder-decoder models for sequence processing that only use the [[🚨 Attention Mechanism]], leaving out the recurrence connections found in [[💬 Recurrent Neural Network]]s. In other words, RNNs process sequences word by word whereas transformers look at them in parallel.

We use the scaled dot-product attention, a slightly modified version of the general attention mechanism, which is calculated as $$\text{softmax}(\frac{QK^T}{\sqrt{d_k}})V$$
where $d_k$ is the dimension of the key space.

> This scaling factor of $\frac{1}{\sqrt{d_k}}$ is introduced to keep the variance at $1$ (instead of scaling with the dimension size), which prevents vanishing gradients in extreme areas of the softmax.

This mechanism is used in the multi-headed self-attention component, which applies it $h$ times. Each time, we calculate $Q$, $K$, and $V$ by projecting the embedding by matrices $W^i_Q,W^i_K, W^i_V$, which the transformer learns, then applying the computation above. The $h$ outputs are concatenated together then projected with $W^O$ to linearly combine them into the final result. This process is illustrated below.

![[20221229194431.png]]

In the following example, we can see that when analyzing "it," one head focuses on "animal" and the other on "tired."

![[20221229194723.png|300]]

Transformers use multiple multi-head attention components in its encoders and decoders to extract sequence structure, which are then processed by feed-forward neural networks.

# Model
The model specification is below. Our encoder takes in the entire sequence at once to calculate $K$ and $V$, which are used in the decoder's multi-headed attention components.

![[20221229193419.png|400]]

Each encoder unit uses a single self-attention mechanism, which uses the embedding or previous encoder unit output as queries, keys, and values.

Each decoder unit uses a masked self-attention mechanism (bottom) and a standard attention mechanism (top) that uses queries from the previous decoder output and keys and values from the encoder. We mask all rightward information in the former since the decoder should only use its previous output.

The feed-forward blocks are simple neural networks that calculate $$\text{ReLU}(xW_1 + b_1)W_2 + b_2$$

Lastly, since we convert the each input token into an embedding, we maintain positional information for each token by adding a positional encoding, calculated with sines and cosines, that determine the distances between words.

# Training
Transformers are trained with backpropagation. The loss function is usually [[🧮 Information Theory#Cross Entropy]] or [[📏 KL Divergence]], comparing the predicted probability distribution with the one-hot encoded true label.

# Prediction
First, we run the entire input through the encoder to generate the keys and values used in the decoder.

To predict the next token, we give the decoder our previously generated sequence and receive softmax probabilities as output, which we use to get the token with highest probability.