# Theory
[[🦾 Transformer]]s work extremely well for sequence processing, and its advantages can also be applied to image data. For classification, we use a slightly-modified transformer encoder and feed it a sequence of image patches that partition the image.

# Model
We first split the image into multiple patches, then treat each patch as a token in the sequence; note that we also need to first convert these patches into embeddings before feeding it into the encoder. Positional encodings are also learned during training.

![[20221230172047.png|600]]

Instead of the standard feed-forward block, we use multilayer perceptrons. Finally, note that we completely remove the decoder as the encoder is responsible for capturing information from the patches, and the MLP head at the end finds the correct class.

## Swin Transformers
Swin transformers modify the standard vision transformer by adding patch-merging layers in between the standard encoder block. It also modifies the standard multi-head attention module with a shifted windows variant that limits the self-attention computation, increasing speed. These changes allow it to better handle scale invariance with a strategy akin to traditional [[👁️ Convolutional Neural Network]]s.

The following is the small swin architecture.
![[20221231144920.png]]

Each patch merging layer concatenates 2-by-2 blocks of patches (equivalent to tokens in the transformer) followed with a linear layer.

The shifted window self-attention module computes self-attention in each window. The window split alternates between two partitions, which allows the model to extract inter-window information.