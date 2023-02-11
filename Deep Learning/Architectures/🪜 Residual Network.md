# Theory
ResNets tackle the vanishing/exploding gradient problem that plagues deep [[✏️ Artificial Neural Network]]s. It introduces the residual block, pictured below which makes it easier for the network to learn an identity mapping if the extra network depth is unneeded.

![[20221231155702.png|300]]

In the residual block, we save the input $x$ and apply element-wise addition between the layers' output $\mathcal{F}(x)$ and the original $x$ via the shortcut connection on the right.

If our desired transformation for these two layers is $\mathcal{H}(x)$, the residual block instead encourages it to learn $\mathcal{H}(x) - x$; if $\mathcal{H}(x)$ is the identity mapping, then it's much easier for the network to zero the layers than learn the identity.

# Model
ResNet models can be extremely deep, sometimes reaching over a hundred layers. Due to the residual connection, they converge better than standard deep networks.

## ResNeXt
ResNeXt models extend the residual idea by adding multiple stacked layers in parallel between the shortcut connection, forming the structure below.

![[20221231162401.png|400]]

Instead of expanding upon the depth of the network, it extends the cardinality of each block akin "network-in-neuron." This kind of parallel computation is also called grouped convolution.