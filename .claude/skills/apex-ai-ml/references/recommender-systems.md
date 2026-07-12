# Recommender Systems

## Scope
Personalized recommendation: collaborative filtering, content-based filtering, matrix factorization, and deep learning approaches. Ranking, implicit feedback, and cold-start.

## Core principles
- Collaborative filtering: "users who liked X also liked Y." Learn latent factors (embeddings) for users and items; similar users/items have similar embeddings. No content knowledge needed.
- Content-based filtering: recommend based on item features and user preferences. Requires good item features but doesn't suffer cold-start for new items (they have features).
- Explicit feedback (ratings) vs. implicit feedback (clicks, purchases, watches). Implicit is noisier (clicks don't mean likes) but abundant. Weighted regression (confidence-weighted matrix factorization) handles this.
- The ranking problem: retrieve candidate items (thousands), score with expensive model, and rank top-k. Two-stage pipeline: retrieval for efficiency, ranking for quality.
- Cold-start: new users have no history, new items have no interactions. Mitigations: hybrid methods (content + collaborative), bandit algorithms (explore new items), or side information (user demographics, item tags).

## Apex practices
- Use factorization machines or neural collaborative filtering (embedding-based) for implicit feedback. They're faster and often better than explicit-only methods.
- Implement candidate retrieval (retrieval as a learned problem, not heuristic matching) using approximate nearest-neighbor search (HNSW, ALSH) on embeddings.
- Evaluate with ranking metrics: precision@k (top-k correct), recall@k (top-k coverage), NDCG (discounts lower ranks). Offline metrics correlate imperfectly with online metrics (CTR, conversions); A/B test recommendations.
- Handle diversity: pure collaborative filtering suffers filter bubbles (only recommending similar items to past likes). Add diversity objectives or diversity penalties in ranking.

## Pitfalls
- Evaluating offline without checking online metrics (CTR, conversion); offline metrics (ranking metrics, recall) don't always correlate with business goals.
- Ignoring feedback loops: recommendations influence user behavior, which influences training data, which influences future recommendations. Bias can spiral (rich-get-richer).
- Cold-start paralysis: without solving cold-start well, new users see generic recommendations and churn. Content-based or contextual bandits help.

## Tools & references
LightFM, Implicit (implicit feedback factorization), TensorFlow Recommenders, Spark MLlib, "Recommender Systems" (Ricci, Rokach, Shapira), Netflix Prize papers, user-based vs. item-based collaborative filtering.
