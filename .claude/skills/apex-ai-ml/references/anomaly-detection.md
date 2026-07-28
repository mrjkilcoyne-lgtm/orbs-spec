# Anomaly Detection

## Scope
Detecting unusual observations: statistical baselines, isolation forests, autoencoders, and one-class methods. Unsupervised learning without labeled anomalies.

## Core principles
- Anomalies are rare (few % of data) and diverse (different failure modes). No single model explains all; an ensemble catches more.
- Statistical methods (Gaussian, Poisson) assume a known distribution; they fail for complex distributions. Isolation-based methods (Isolation Forest) don't assume a distribution.
- Autoencoders (compress then reconstruct; anomalies reconstruct poorly) and one-class SVM (learn the boundary of normal data) are flexible; they adapt to the data.
- Evaluation without labels is hard: metrics like silhouette or Davies-Bouldin don't directly measure anomaly detection. Use domain experts to label a sample and measure precision-recall on that.
- Context matters: a spike in CPU load is normal during backups but anomalous at 3 AM. Time-dependent anomalies require adaptive thresholds or explicit seasonal modeling.

## Apex practices
- Start with simple statistical methods (z-score, MAD — median absolute deviation). If they work, deploy them; they're interpretable and fast.
- Use ensemble methods: combine multiple anomaly detectors (statistical, isolation-based, reconstruction-based) and flag points multiple detectors agree on. Reduces false positives.
- Implement online learning: retrain anomaly detectors periodically (daily, weekly) to adapt to changing data distributions. What's anomalous evolves.
- Handle false positives: anomaly detection thresholds are typically set empirically. Too low = false alarms (alert fatigue), too high = missed anomalies. Work with operators to find the sweet spot.

## Pitfalls
- Assuming anomalies are always far from the mean; some anomalies are subtle (small systematic deviations). Variance-based methods miss them.
- Not accounting for seasonality and trends; time-series anomaly detection requires detrending first (subtract trend, then detect anomalies in residuals).
- Deploying without human-in-the-loop: models produce scores, but thresholding and actions require human judgment. Integrate with alerting systems carefully.

## Tools & references
Scikit-learn (Isolation Forest, OneClassSVM, Elliptic Envelope), PyOD (Python Outlier Detection), Prophet (time-series anomaly detection), Z-score/IQR methods, autoencoders (TensorFlow), "Anomaly Detection" survey papers.
