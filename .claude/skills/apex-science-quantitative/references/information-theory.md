# Information Theory

## Scope
Measuring information: entropy, mutual information, KL divergence, and applications to compression, channel capacity, and model comparison.

## Core principles
- Entropy H(X) = -Σ p(x) log p(x) measures average information (surprise) in a distribution; it's minimized for deterministic outcomes and maximized for uniform distributions.
- Mutual information I(X;Y) measures information X provides about Y; it's zero if independent, maximal if identical. Equivalently, reduction in uncertainty about Y given X.
- KL divergence D(P||Q) measures how different distribution Q is from true distribution P; it's asymmetric (D(P||Q) ≠ D(Q||P)) and zero only if P = Q.
- Channel capacity C = max I(X;Y) over all input distributions; it bounds reliable communication rate given noise. Shannon's fundamental limit.
- Cross-entropy H(P,Q) = H(P) + D(P||Q); minimizing cross-entropy is equivalent to minimizing KL divergence when P is fixed (as in supervised learning).

## Apex practices
- Use entropy to quantify feature informativeness; features with high mutual information with targets are valuable.
- In machine learning, the loss (cross-entropy or NLL) implicitly minimizes KL divergence between true and predicted distributions.
- For model selection, use information-theoretic criteria (AIC, BIC) that penalize complexity; they're approximations to leave-one-out cross-validation.
- Understand that lower entropy models (more confident predictions) are better only if calibrated; overconfident models have high entropy-in-practice if they're frequently wrong.

## Pitfalls
- Confusing mutual information with causation; high I(X;Y) doesn't mean X causes Y.
- Using entropy alone to judge decision trees or classifiers; maximize information gain, not entropy reduction, which are subtly different.
- Ignoring that KL divergence is asymmetric; reverse KL (mode-seeking) vs. forward KL (mean-seeking) behave very differently (important in variational inference).

## Tools & references
Cover-Thomas "Elements of Information Theory," Shannon's original 1948 paper, entropy packages (scikit-learn.metrics.mutual_info_score), ELBO in variational inference.
