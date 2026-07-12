# Supervised Learning

## Scope
Learning from labeled data: classification (discrete outputs) and regression (continuous outputs). Loss functions, gradient descent, and empirical risk minimization.

## Core principles
- Supervised learning is function approximation: given (input, label) pairs, find a function that predicts unseen inputs. The training loop minimizes a loss function (mean squared error for regression, cross-entropy for classification) over observed data.
- Generalization vs. memorization: a model memorizing training data (low training error, high test error) overfits. Regularization (L1/L2 penalties on weights, dropout, data augmentation) biases toward simpler models that generalize.
- The bias-variance tradeoff: high-bias models (linear regression) underfit (large train and test error), high-variance models (deep neural networks) overfit (small train error, large test error). Test error = bias^2 + variance + irreducible noise.
- Data splits (train, validation, test) are non-negotiable: train to fit the model, validation to tune hyperparameters, test to measure generalization. Leaking test data into training breaks generalization estimates.
- Loss function choice matters: MSE (regression) penalizes large errors quadratically (sensitive to outliers), MAE (regression) is robust. Cross-entropy (classification) is calibrated for probabilistic outputs; accuracy metric is brittle for imbalanced classes.

## Apex practices
- Start simple (linear regression, logistic regression) before complex models (neural networks). Simple models are faster, interpretable, and provide baselines; beating them with neural networks justifies added complexity.
- Use cross-validation (k-fold) to estimate generalization error without wasting data on a separate validation set. Particularly important for small datasets (<1K samples).
- Implement early stopping: monitor validation loss, stop training when it stops improving (prevents overfitting). Save the best model, not the final one.
- Collect more data when possible; machine learning rarely solves data problems (wrong distribution, label noise, missing features) — more data often beats better algorithms.

## Pitfalls
- Tuning hyperparameters on test data (even indirectly, by reporting test metrics and iterating). Test set must be sealed; evaluate on it once, at the end.
- Ignoring class imbalance: in binary classification with 99% negatives, a model predicting "always negative" gets 99% accuracy but is useless. Use precision-recall curve, F1-score, or weighted loss.
- Assuming one algorithm fits all: random forests, SVM, and neural networks have different inductive biases; try multiple and pick the best.

## Tools & references
Scikit-learn (classification, regression), TensorFlow/Keras, PyTorch, "Hands-On Machine Learning" (Aurelien Geron), "Introduction to Statistical Learning" (James, Witten, Hastie, Tibshirani).
