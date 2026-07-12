# Hyperparameter Tuning

## Scope
Optimizing model hyperparameters (learning rate, regularization, tree depth). Grid search, random search, Bayesian optimization, and early stopping.

## Core principles
- Hyperparameters are set before training (unlike weights learned during training). Examples: learning rate (α), regularization strength (λ), tree depth, batch size.
- Grid search tries all combinations of a discrete set of values (e.g., learning rate in {0.001, 0.01, 0.1}, depth in {3, 5, 10}). Exhaustive but expensive for many hyperparameters (curse of dimensionality: 3 params × 3 values each = 27 trials).
- Random search samples random points in the hyperparameter space. Often beats grid search because some hyperparameters matter more than others; random search allocates budget proportionally.
- Bayesian optimization (Hyperopt, Optuna) models the objective function and picks promising points to evaluate next. More efficient than grid/random search but more complex to implement.
- Learning rate schedules (decay over time, cosine annealing, warmup) and early stopping (stop when validation loss plateaus) reduce the effective hyperparameter space.

## Apex practices
- Start with reasonable defaults from literature; tuning from scratch is expensive. Most papers report hyperparameters; use them as starting points.
- Parallelize: run trials in parallel (multiple GPUs, distributed computing). Bayesian optimization benefits from parallelization (evaluate multiple candidates per iteration).
- Use validation curves (plot performance vs. hyperparameter value) to understand sensitivity. Focus tuning on sensitive parameters.
- Implement cross-validation within the tuning loop: estimate generalization error with k-fold CV, not a single validation set. Reduces overfitting to the validation set.

## Pitfalls
- Tuning on test data or training data; this overfits the hyperparameters to your specific dataset. Use a held-out validation set.
- Exhaustive search without prior knowledge; the space is too large. Use random search or Bayesian optimization.
- Not tracking the relationship between hyperparameters; some are correlated (large learning rate often pairs with large regularization). Interactions complicate tuning.

## Tools & references
Scikit-learn GridSearchCV/RandomizedSearchCV, Optuna, Ray Tune, Hyperopt, "Practical recommendations for gradient-based training of deep architectures" (Bengio et al.), learning rate finder (for neural networks).
