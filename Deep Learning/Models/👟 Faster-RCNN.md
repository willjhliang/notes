# Theory
Faster-RCNN performs object detection using a feature network, region proposal network (RPN), and the Fast RCNN detection network.
1. Feature network generates a feature map from the input image.
2. Feature map is fed to RPN to generate proposals called regions of interest (RoIs).
3. RoIs and feature map are then used by detection network to classify regions.

# Model
## Feature Network
The feature network is usually constructed from a pre-trained classification network (like VGG) without the final layers. The output retains image structure, purpose is to extract good features from the image.

## Region Proposal Network (RPN)
RPN takes in the feature map and outputs convolutional layers for classification (0 or 1) and bounding box regression.

Each proposal is parameterized relative to an anchor box.
1. There are $k$ anchor boxes for every pixel in the feature map.
2. We'll use $k = 9$ for $3$ scales and $3$ aspect ratios.
3. Bounding box regression outputs $t_x, t_y, t_w, t_h$ for each anchor box that adjusts it to fit a RoI.

> What is "translation invariant" for the anchor boxes?

Classification calculates the probability of an object and not-object for each anchor box.

After prediction, use NMS to reduce duplicates and return the top $N$ ranked proposals.

## Detection Network
The detection network takes in feature map and RoIs and uses dense layers to calculate classification and bounding box regression.

For each RoI, use RoI pooling to extract corresponding region from feature map to a fixed $H \times W$ size.

Run this window through multiple dense layers, output class probabilities $p_0, \dots, p_K$ (including one for background class) and $t_y, t_y, t_w, t_h$ similar to RPN.

# Training
Feature network can be used pre-trained on a classification problem. RPN and detection network are trained separately.

## Region Proposal Network (RPN)
An anchor is positive if it has the highest IoU with a ground truth box or an IoU $\geq 0.7$, negative if it has IoU $< 0.3$, and ignored otherwise.

For an image, the loss is defined as $$L({p_i}, {t_i}) = \frac{1}{N_{cls}} \sum_i L_{cls}(p_i, p_i*) + \lambda \frac{1}{N_{reg}} \sum_i p_i* L_{reg}(t_i, t_i*)$$
1. $t_x = (x - x_a) / w_a$
2. $t_y = (y - y_a) / h_a$
3. $t_w = \log(w / w_a)$
4. $t_h = \log(h / h_a)$

## Detection Network

# Prediction