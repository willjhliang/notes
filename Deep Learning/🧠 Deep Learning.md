Deep Learning is a sub-field of [[๐ค Machine Learning]] that uses neural networks, which model non-linear functions using certain structures and layer types.

# Models
There are four primary model types, each serving a different purpose.
1. [[โ๏ธ Artificial Neural Network]] for general tabular data.
2. [[๐๏ธ Convolutional Neural Network]] for spatial data, commonly images.
3. [[๐ฌ Recurrent Neural Network]] for sequential data, commonly text.
4. [[๐ค Graph Neural Network]] for graph data, like molecules or networks.

The following are extensions of these architectures with added benefits.
1. [[๐ช Residual Network]]s add residual connections that allow greater network depth.
2. [[๐งฌ Autoencoder]]s learn dimensionality reduction with encoder and decoder networks.
3. [[๐ฏ๏ธ Diffusion Probabilistic Model]]s iteratively generate new images from random noise.
4. [[๐ฅ Long Short-Term Memory]] and [[โฉ๏ธ Gated Recurrent Unit]]s improve RNN performance for long sequences.

Using these architectures, we can build models that address specific problems.
1. [[๐ NeRF]] uses ANNs to create 3D scenes from multiple 2D sample images.
2. [[๐ YOLO]] and [[๐ Faster-RCNN]] tackle object detection, forming and classifying bounding boxes.
3. [[โ๏ธ Variational Autoencoder]]s, [[๐ฆ Normalizing Flow]], and [[๐ผ๏ธ Generative Adversarial Network]]s model the dataset distribution and generate new samples.
5. [[๐งต Seq2Seq]] performs sequence translation using encoder and decoder RNNs.
6. [[๐ฆพ Transformer]]s and [[๐ฆฟ Vision Transformer]]s combine the [[๐จ Attention Mechanism]] and networks for sequence translation.
7. [[๐ ConvNeXt]] mimics transformers using a pure CNN architecture.