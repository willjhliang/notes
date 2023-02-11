# Theory
Perceptrons are an online learning alternative to the [[🛩️ Support Vector Machine]]. We optimize a classifying hyperplane $w$, updating it if we get a prediction wrong and keeping it the same if we get a prediction right.

We update the plane by modifying its perpendicular vector to look more like the example we get wrong. In other words, our update step is $$w = w + \eta y^{(i)}x^{(i)}$$with a certain learning rate $\eta$.

> If the data is linearly separable, the algorithm will converge after $<\frac{R^2}{\gamma^2}$ mistakes where $R = \max_i \Vert x_i\Vert_2$ (size of biggest $x_i$) and margin $\gamma < y_iw^Tx_i$.

If the data is not linearly separable, the simple perceptron will keep updating $w$, we can need to manually stop training. After stopping, there are variations in the way we get our final model.
1.  Voted perceptron: keep track of all intermediate models, predict the majority vote of running input $x$ through all models
2.  Averaged perceptron: final model is average of all intermediate models, essentially an approximation of voted perceptron that has much faster prediction times

A nuanced variation is the Margin-Infused Relaxed Algorithm (MIRA), a type of passive-aggressive perceptron that which minimizes the hinge loss at each observation. It updates $w$ to be as close as possible to the old weights while setting hinge loss to $0$ (in case of misclassification or correct prediction within the margin); in other words, it makes the smallest change to $w$ for a correct prediction outside the margin.

# Model
Same as SVM, we maintain a hyperplane $w$ that splits the $x$ space, classifying each side. We update the hyperplane with learning rate $\eta$, which we can configure to be different for different loss functions; the passive-aggressive perceptron, for example, uses it to optimize hinge loss.

# Training
Given training data $D$, randomly initialize hyperplane $w$.

While $w$ incorrectly classifies datapoints in $D$, for each $x^{(i)}, y^{(i)}$,
1. Predict $\hat{y} = sign(w^Tx^{(i)})$.
2. If $\hat{y} \neq y_i$, update $$w = w + \eta y^{(i)}x^{(i)}$$

> For a multi-class perceptron, in case of a wrong class prediction, we update both the weights for the correct and incorrect classes; the former adds $\eta x^{(i)}$ while the latter subtracts it.

For simple perceptrons, $\eta = 1$; with passive-aggressive perceptrons, $$\eta = L(w \vert x_i, y_i) / \Vert x_i\Vert^2$$where $L$ is the hinge loss $L(w \vert x_i, y_i) = \max(0, 1 - y_iw^Tx_i)$.

# Prediction
As with SVM, given input $x$, our prediction is $\hat{y} = sign(w^Tx)$.