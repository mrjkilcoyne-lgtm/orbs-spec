# Model Evaluation

## Scope
Measuring model performance: train/validation/test splits, cross-validation, metrics (accuracy, precision, recall, F1, AUC-ROC), and statistical significance testing.

## Core principles
- Test set must be held out: train on data, tune hyperparameters on validation data, measure on test data never seen during training. Evaluating on training data (overly optimistic) or validation data (multiple evaluations inflate significance) is cheating.
- Class imbalance changes the problem: 99% negatives means 99% accuracy predicting "always negative." Use precision-recall curve (trades false positives vs. false negatives), F1-score (harmonic mean of precision and recall), or AUC-ROC (area under receiver-operating-characteristic curve).
- Different tasks need different metrics: classification uses accuracy/F1, regression uses MSE/MAE, ranking uses NDCG, clustering has no universal metric. Aligning metric with goal is crucial.
- Metric instability: statistical fluctuations mean a 1% improvement may just be noise. Estimate confidence intervals (bootstrap, cross-validation) and test for statistical significance (t-test, permutation test).
- Distribution shift breaks metrics: model trained on 2020 data evaluated on 2024 data faces domain shift (data distribution changed). Monitor train/test distributions and retrain when necessary.

## Apex practices
- Use k-fold cross-validation (k=5 typical) to estimate generalization error without wasting data on a separate validation set. Stratified k-fold preserves class ratios.
- Implement domain-specific metrics alongside standard ones: in healthcare, false negatives (missed diagnoses) are worse than false positives. Optimize for clinical relevance, not just accuracy.
- Track baseline performance (majority class predictor, simple model, human performance). If your model doesn't beat baselines significantly, question its utility.
- Bootstrap confidence intervals: resample training data, fit model on each resample, measure metric variation. Confidence intervals quantify uncertainty; report them.

## Pitfalls
- Optimizing for the wrong metric (accuracy on imbalanced data, AUC when precision-recall matters). Metric choice steers the model.
- Not reporting confidence intervals; a reported 85% accuracy without a margin of error is incomplete.
- Confusing statistical significance (p-value < 0.05) with practical significance (does the 1% improvement matter?). Statistical tests assume i.i.d. data; real data often has dependencies.

## Tools & references
Scikit-learn (metrics, cross-validation), Confusion matrix, ROC-AUC curve, precision-recall curve, "The Lack of A Priori Distinctions Between Learning Algorithms" (No Free Lunch theorem), Cochran's Q test, Bootstrap methods.
