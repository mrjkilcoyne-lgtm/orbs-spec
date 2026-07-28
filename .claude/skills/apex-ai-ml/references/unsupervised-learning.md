# Unsupervised Learning

## Scope
Learning from unlabeled data: clustering, dimensionality reduction, and representation learning. Discovering structure without explicit labels.

## Core principles
- Unsupervised learning finds patterns without ground truth: clustering groups similar points, dimensionality reduction projects high-dimensional data onto lower-dimensional manifolds, representation learning discovers useful features.
- Evaluation is subjective: no labels means no accuracy metric. Validity metrics (silhouette, Davies-Bouldin) measure cluster quality, but optimizing them doesn't guarantee the clustering makes sense for your domain.
- The number of clusters is a hyperparameter: k-means requires specifying k. Elbow method (plot inertia vs k, pick the "elbow") and silhouette analysis (pick k with highest silhouette score) are heuristics; domain knowledge is better.
- Dimensionality reduction trades accuracy for interpretability and speed. PCA (linear projection) is fast and interpretable; t-SNE and UMAP (nonlinear) preserve local structure but are slow and non-deterministic.
- Representation learning (autoencoders, contrastive learning) learns useful embeddings: features that capture semantic similarity. Better embeddings improve downstream supervised tasks (transfer learning).

## Apex practices
- Use clustering for exploratory data analysis: identify natural groupings, detect outliers (points far from any cluster), or segment customers. Then label clusters manually and convert to supervised learning.
- Normalize features before clustering (especially k-means, which is distance-based); different scales cause misleading results (one feature dominates).
- Evaluate clustering on labeled data (if available): compute adjusted Rand index (ARI) or normalized mutual information (NMI) against ground-truth labels. Purely unsupervised metrics are weak.
- Use hierarchical clustering (dendrograms) to explore cluster structure at multiple scales; don't commit to a single k upfront.

## Pitfalls
- Over-interpreting clusters: k-means partitions space mathematically but doesn't guarantee meaningful clusters. A cluster might be an artifact of the algorithm, not a true domain group.
- Not scaling features before clustering; if one feature ranges [0, 1] and another [0, 1000], the second dominates distance calculations.
- Using t-SNE/UMAP for clustering (they're visualization tools, not clustering algorithms); the 2D projections don't preserve global structure, only local neighborhoods.

## Tools & references
Scikit-learn (clustering: KMeans, DBSCAN, hierarchical; reduction: PCA, t-SNE; manifold learning), UMAP, "Unsupervised Learning" (course, Andrew Ng), elbow method, silhouette analysis, representation learning surveys.
