# Interpretability

## Scope
Understanding model decisions: feature importance, saliency maps, LIME, SHAP, and explanation generation. Building trust in model predictions.

## Core principles
- Interpretability is not intrinsic; all models are interpretable to *someone*. Linear models are interpretable (coefficients show direction/magnitude of effect), neural networks are black boxes to most people.
- Local interpretability (explaining a single prediction): LIME (fit a simple model locally to mimic the black box), SHAP (game-theoretic contribution of each feature), saliency maps (gradient w.r.t. input).
- Global interpretability (understanding overall model behavior): feature importance (how much each feature contributes), partial dependence plots (how prediction changes with feature value).
- Post-hoc explanations are always incomplete: the explanation might be misleading or wrong, especially for complex models. Interpretable models (decision trees, linear regression) provide true explanations.
- Different audiences need different explanations: engineers want feature importance and error modes, business users want simple stories, regulators want model transparency.

## Apex practices
- Use inherently interpretable models (logistic regression, decision trees) when possible. If using neural networks, add interpretability techniques post-hoc.
- Implement SHAP (model-agnostic, game-theoretic fairness, handles feature interactions) for explanations. Interpret as: "feature x contributes Y to this prediction."
- Visualize saliency maps (gradient-based) for images: which pixels influence the prediction? Helps debug spurious correlations.
- Validate explanations: if an explanation says "high income → loan approved," verify this holds in the data. Bad explanations don't match reality.

## Pitfalls
- Trusting explanations uncritically; they can be misleading (correlation ≠ causation). Cross-check with domain knowledge.
- Assuming feature importance reflects true causation; importance measures correlation. A collinear feature shares importance with a true causal feature.
- Over-reliance on black-box models for high-stakes decisions (medical diagnosis, loan approval, criminal sentencing). Interpretability is non-negotiable for fairness and accountability.

## Tools & references
SHAP, LIME, Captum (PyTorch), feature importance (sklearn, XGBoost built-ins), "Interpretable Machine Learning" (Molnar, free online), "The Mythos of Model Interpretability" (Lipton).
