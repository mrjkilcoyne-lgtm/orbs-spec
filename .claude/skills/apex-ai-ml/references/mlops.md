# MLOps

## Scope
Operationalizing ML systems: versioning (code, data, models), experiment tracking, CI/CD for ML, and monitoring model drift in production.

## Core principles
- ML introduces variability: multiple random seeds, data shuffling, and hyperparameter choices cause different models from the same code. Reproducibility requires versioning and deterministic seeding.
- Data is a first-class artifact: track datasets (versions, checksums) and lineage (which raw data → processed data → training data). Data changes invalidate model results.
- Models drift in production: data distribution shifts, user behavior changes, or new patterns emerge. Monitor prediction distribution and performance; retrain when necessary.
- Experiment tracking (logging hyperparameters, metrics, artifacts) enables reproduction and comparison. A model trained in June with unknown hyperparameters is useless ("why does it fail now?").
- The ML pipeline: raw data → preprocessing → feature engineering → training → evaluation → deployment. Each step must be versioned, repeatable, and testable.

## Apex practices
- Use versioning systems (Git for code, DVC for large data/models, MLflow for tracking) to version everything: code, data, models, hyperparameters, metrics.
- Implement data validation: check schema, distributions, and for anomalies before training. Catch data quality issues early.
- Automate the pipeline (Airflow, Kubeflow, SageMaker Pipelines): data loading → preprocessing → training → evaluation → deployment. Reduces manual steps and errors.
- Monitor in production: log predictions, confidence scores, and user feedback. Detect model degradation and trigger retraining when performance drops.

## Pitfalls
- Manual model management: training models locally, committing .pkl files, and deploying via email. Scale with infrastructure (experiment tracking, model registry, deployment pipelines).
- Not reproducing experiments: code changed, hyperparameters forgotten, results diverge. Versioning and notebooks enable reproduction.
- Ignoring data drift: a model trained on 2020 data deployed in 2024 without monitoring. Distribution changes are inevitable; detect and adapt.

## Tools & references
MLflow (experiment tracking, model registry), DVC (data versioning), Airflow/Kubeflow (pipeline orchestration), Weights & Biases (experiment tracking), "Building Machine Learning Systems" (Domingos & Hulten).
