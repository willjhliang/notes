# Theory
For some tasks, we don’t need each neuron to take in all outputs from the previous layer, as seen in an [[✏️ Artificial Neural Network]]; local receptive fields limits a neuron’s inputs to nearby neurons.

Convolutional neural networks apply this idea in 2D; instead of a flat layer of neurons, each convolutional layer consists of a structured 3D tensor consisting of multiple 2D matrices. Below is an illustration of this structure.

![[20221229103206.png|400]]

Each layer has multiple 3D filters, defined by its dimensions, stride, and padding; each filter consists of weights, and we apply these filters onto the activations of the previous layer. One filter results in one 2D matrix, and stacking these matrices gives us the 3D tensor.

## Max Pool
Max pool layers are used to reduce the first two dimensions of a 3D tensor, partitioning the input and getting the maximum value for each. This serves as dimension reduction and prevents overfitting. Below is an example.

> We use maximum instead of average because most of the input is zero, and we want to capture strong activations instead of muddying the signals with an average.

![[20221229103207.png|400]]

# Model
CNN consists of convolution, max pool, and dense layers; max pools usually go between convolutions, and for unstructured labels $y$, we flatten the 3D tensor near the end and pass it through dense layers before the final output.

For structured outputs, we don’t use dense layers.

> Due to using convolutions instead of dense layers, CNNs usually have much fewer weights than it would have if it used dense layers instead.

# Training
Training is the same as dense neural networks, using [[⛰️ Gradient Descent]] with backpropagation.

Data augmentation increases the dataset size without getting more data. Common strategies include flipping the image (usually horizontal, vertical breaks invariances), slightly cropping the image or translating it, or applying a color filter.

# Prediction
Prediction is also the same as artificial neural networks except that the input is structured as a 3D tensor (usually an RGB or greyscale image).