Machine learning involves algorithms that "learn" from data. They take data as input and produce a model as output.

The field is split into three main forms of learning depending the problem type.
1. [[🎓 Supervised Learning]] deals with modeling inputs $x$ to output $y$.
2. [[🔍 Unsupervised Learning]] finds patterns in unlabeled inputs $x$.
3. [[🦾 Reinforcement Learning]] trains an agent to act in an environment.

All three problems share a general solution structure: model formulation and optimization.

# Models
Theoretically, models can be thought of as probability distributions. They can be either generative or discriminative.
1. Generative models $p(x, y) = p(x \vert y)p(y)$ capture the shape of the data distribution.
2. Discriminative models $p(y \vert x)$ draw boundaries in the data space.

Classical machine learning models generally have statistical and mathematical roots. [[🧠 Deep Learning]] works with biologically-inspired neural network architectures that are magnitudes more complex than classical methods.

# Optimization
Training these models involve optimizing their parameters, or weights.
1. [[⛰️ Gradient Descent]] gradually moves down a convex loss function.
2. [[🔎 Greedy Search]] performs feature selection for non-convex loss.
3. [[🎉 Expectation Maximization]] optimizes hidden variables in unsupervised models.

In practice, [[👕 Overfitting]] is a common problem where models learn noise in the training data that's not part of the real world. The solution is two-fold.
1. [[⚽️ Regularization Penalties]] in loss functions apply weight shrinkage or selection.
2. [[✅ Validation]] methods find hyperparameters that optimize model complexity.

[[👀 AutoML]] is a modern solution that automates both processes by automatically building a ensemble that maximizes performance for a given problem.

# Empirical Analysis
Finally, there are some more real-world practices to keep in mind.
1. [[❓ Imputation]] is required to address missing data.
2. [[💯 Evaluation]] is necessary to measure a model's performance.
3. [[🎙️ Interpretation and Explainability]] analyses the patterns our model learned and what the model actually tells us about the world.
