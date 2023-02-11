# Theory
At its core, attention mechanisms compute a weighted sum of values, paying different levels of attention to each one. Given the queries $Q$ and key-value pairs represented by $K$ and $V$, we compute the generalized attention for each query $q$ as follows.
1. Dot $q$ with each key to get score $e_i = q \cdot k_i$, which we can interpret as the query's compatibility with the key.
2. Compute the softmax over scores to get weights $\alpha_i$.
3. Generalized attention is the weighted sum $\sum_{i=1}^n \alpha_i v_i$ of values.

## Seq2Seq Attention
Attention is especially useful in the [[🧵 Seq2Seq]] architecture. We add steps between the encoder and decoder, utilizing all hidden states from the encoder to figure out which hidden states are most relevant to each decoding time-step. In this application, the query is analogous to the previous decoder output $s_{t-1}$ and the keys and values are both analogous to the hidden states $h_i$.

# Model
In Seq2Seq, instead of passing the encoder output directly to the decoder, we instead compute a weighted average of all hidden encoder states at each decoder time-step.

Therefore, at time $t$ of the decoding process, we perform the following.
1. For each encoder hidden state $h_i$ and previous decoder output $s_{t-1}$, use a feed-forward neural network to compute the $i$-th alignment score $e_{t, i}$.
2. Then, calculate a softmax over all scores to get the weights $\alpha_{t,i}$.
3. Generate the context vector $c_t = \sum_{i=1}^p \alpha_{t,i} h_i$.

The context vector and previous decoder output are concatenated and given to the decoder to produce an output.