# Feature Engineering

## Scope
Creating and transforming features (input variables) to improve model performance. Handling missing data, encoding categorical features, scaling, and domain knowledge injection.

## Core principles
- "Garbage in, garbage out": model quality is ceiling'd by feature quality. Domain knowledge baked into features often beats raw input to a black-box model.
- Missing data requires a strategy: drop rows (loses information), impute with mean (assumes MCAR, loses variance), or use domain knowledge (email missing = unregistered user). Dropping biases if missingness is MCAR (missing completely at random); imputation introduces bias if data is MNAR (missing not at random).
- Categorical encoding transforms strings into numbers: one-hot encoding (binary column per category) for tree models, embedding (dense vector) for neural networks. High cardinality (thousands of categories) requires target encoding or hashing.
- Scaling (normalize to [-1, 1] or [0, 1], standardize to mean 0 std 1) is critical for distance-based models (KNN, SVM, neural networks) and regularized models (L1/L2 penalties). Tree models are scale-invariant.
- Temporal features (day of week, month, year, holiday indicator) from timestamps help models capture seasonality and trends. Interaction features (product of two features) capture nonlinearities.

## Apex practices
- Start with domain knowledge: talk to subject-matter experts about what features matter. Consult existing domain literature (studies, reports) for established signals.
- Create interaction features between important variables; models sometimes can't learn interactions from raw features efficiently. But explosion of features (curse of dimensionality) requires dimensionality reduction.
- Use pandas for simple transformations, and feature-engineering libraries (Featuretools for automated feature generation, tsfresh for time-series features).
- Monitor feature importance (model-agnostic: permutation importance; tree-based: gini/gain). Low-importance features waste memory and increase noise; drop them.

## Pitfalls
- Leakage: using information unavailable at prediction time (e.g., future prices to predict current trend). Subtle sources: target variable statistics, data from the future, information from later timesteps.
- Over-engineering: too many features cause overfitting (model fits noise). Start simple (raw features or basic transforms), add complexity as needed.
- Inconsistent preprocessing: training and inference must apply identical transformations (same scaling params, same encoding). Hardcode these constants.

## Tools & references
Pandas, scikit-learn preprocessing, Featuretools (automated feature generation), tsfresh (time-series features), "Feature Engineering for Machine Learning" (Zheng & Casari), domain-specific feature guides.
