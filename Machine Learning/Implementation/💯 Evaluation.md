Classification performance has multiple metrics, many used in case the classes are asymmetric, with one class having more examples than the others.

Accuracy is the main symmetric measure.
$$\text{accuracy} = p(\text{correct}) = \frac{TP + TN}{TP + FP + TN + FN}$$

Asymmetric measures include precision, recall (sensitivity or true positive rate), and specificity (inverse of false positive rate).
$$\text{precision} = p(\text{yes } \vert \text{ predicted yes}) = \frac{TP}{TP + FP}$$
$$\text{recall} = p(\text{predicted yes } \vert \text{ yes}) = \frac{TP}{TP + FN}$$
$$\text{specificity} = p(\text{predicted no } \vert \text{ no}) = \frac{TN}{TN + FP}$$

F1 score combines precision and recall.
$$F1 = \frac{2 * \text{precision} * \text{recall}}{\text{precision} + \text{recall}}$$

The ROC curve, pictured below, sorts predictions in descending order of confidence and measures sensitivity, the true positive rate, over a confidence threshold. As threshold increases, we predict more “yes,” so sensitivity increases.

![[20221229103220.png|300]]

> The threshold can also be interpreted as $1 - \text{specificity}$, or the false positive rate.

The stronger the curve, the better the performance. Thus, area under curve (AUC) is another common metric for performance, varying between $0.5$ (random) and $1$ (perfect).

Finally, a confusion matrix shows counts of actual vs predicted class values.
![[20221229103221.png|400]]