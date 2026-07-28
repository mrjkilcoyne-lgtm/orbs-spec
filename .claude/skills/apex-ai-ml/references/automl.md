# AutoML

## Scope
Automating machine learning pipelines: algorithm selection, hyperparameter optimization, meta-learning, and neural architecture search (NAS). Reducing manual effort in model development.

## Core principles
- AutoML automates choices humans make: which algorithm to use, which features to engineer, which hyperparameters to set. Automation reduces bias and enables non-experts to build models.
- Meta-learning (learning what works for different datasets) accelerates AutoML: warm-start hyperparameter optimization using similar past tasks, or select algorithms likely to work based on data properties (meta-features).
- Neural Architecture Search (NAS) automates neural network design: generate candidate architectures, train them, rank by performance, keep the best. Expensive but can discover novel architectures.
- Pipeline optimization: end-to-end hyperparameter tuning (data preprocessing params + algorithm selection + algorithm hyperparams). Single objective function integrates all choices.
- AutoML trades compute for human effort: searching over architectures and hyperparameters requires lots of training. Worth it for recurring tasks (many datasets) or high-value applications.

## Apex practices
- Use AutoML frameworks (Auto-sklearn, TPOT, AutoGluon) for tabular data as a baseline. They often beat hand-tuned single models from non-specialists; compare against them.
- For neural networks, use Keras Tuner or Ray Tune with population-based training (evolve hyperparameters during training). NAS frameworks (ENAS, Darts) are more sophisticated but slower.
- Set realistic time budgets: AutoML can run forever. Define max computation time or max number of trials, not infinite search.
- Validate AutoML results: ensure the found model generalizes (cross-validation, test set) and isn't overfit to the specific dataset. AutoML can overfit the pipeline to the data.

## Pitfalls
- Assuming AutoML removes the need for domain knowledge; feature engineering and algorithm selection are easier with understanding of the data.
- Running AutoML on a small dataset (< 1K samples); hyperparameter tuning works better with more data. On small data, simpler models and careful validation matter more.
- Not monitoring AutoML results; found models can be unstable (high variance across runs) or uninterpretable (deep neural networks). Human review is still necessary.

## Tools & references
Auto-sklearn, AutoGluon, TPOT (genetic programming), Keras Tuner, Ray Tune, NAS frameworks (ENAS, DARTS), "AutoML: A Survey of the State-of-the-Art," "Benchmarking AutoML" (comparison studies).
