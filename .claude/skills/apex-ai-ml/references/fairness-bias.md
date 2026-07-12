# Fairness & Bias

## Scope
Detecting and mitigating bias in ML systems: demographic parity, fairness definitions, and bias mitigation strategies across the pipeline.

## Core principles
- Bias is pervasive: training data reflects historical inequities (loan denials, hiring discrimination). Models learn and amplify this bias unless explicitly prevented.
- No single definition of fairness: demographic parity (equal outcome rates across groups), equalized odds (equal error rates), individual fairness (similar individuals treated similarly). Trade-offs exist; no solution satisfies all simultaneously (impossibility theorems).
- Bias enters through data (underrepresented groups, label errors), features (using protected attributes or proxies), and evaluation (metrics hide disparities). Full pipeline requires auditing.
- Protected attributes (race, gender, age, disability) are often correlated with others; removing them doesn't remove bias. Removing correlates (zip code as proxy for race) is implicit discrimination and fails legally.
- Fairness is not only ethical; it's strategic: biased systems lose users, attract regulation, and break trust. A loan model denying loans to creditworthy minorities is leaving money on the table.

## Apex practices
- Audit fairness during data exploration: compare outcome rates, error rates, and feature distributions across demographic groups. Visualize disparities.
- Stratify test sets by protected attributes: ensure model performance is good for all groups, not just majority. Test with different thresholds (ROC curve per group).
- Implement bias mitigation: re-weight training data to balance groups (oversampling minorities, undersampling majorities), adjust decision thresholds per group to equalize error rates, or use fair representation learning.
- Involve affected communities: fairness is not a technical question alone. Talk to the groups your model affects; their concerns shape design.

## Pitfalls
- Thinking bias disappears by "not using" protected attributes; proxies encode protected information implicitly (zip code → race, name → gender).
- Assuming one-time audit is sufficient; as data and society change, bias evolves. Continuous monitoring is necessary.
- Prioritizing one fairness definition; understand stakeholder priorities and their tradeoffs before choosing.

## Tools & references
AI Fairness 360 (IBM), Fairlearn (Microsoft), FAT* conference, "Fairness and Machine Learning" (Barocas, Hardt, Narayanan, free online), COMPAS recidivism case study, ProPublica algorithms audit.
