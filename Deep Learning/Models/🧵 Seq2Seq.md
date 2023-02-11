# Theory
Sequence-to-sequence models are used for translation, outputting a sequence from an input sequence. It uses [[💬 Recurrent Neural Network]]s, [[🎥 Long Short Term Memory]], or [[⛩️ Gated Recurrent Unit]]s to encode the sequence into a hidden state and then decode it into another sequence.

The core idea is that the encoder's output summarizes the entire sequence, and the decoder can use this summary to generate a response. However, this approach struggles with long sequences as information earlier in the sequence tend to get lost. The[[🚨 Attention Mechanism]] addresses this weakness by passing on the hidden states as well.

# Model
The model consists of two recurrent architectures joined together, as pictured below.

![[20221229171943.png]]