# Embeddings

## Scope
Dense vector representations of text (and other modalities): model selection, similarity metrics, vector storage, indexing, and lifecycle management.

## Core principles
- Embeddings encode the training objective, not "meaning" in general: a model trained for retrieval ranks query-document relevance, which is not the same space as clustering, classification, or semantic textual similarity — check MTEB scores for your task type, not the overall average.
- Cosine similarity scores are not calibrated probabilities and are not comparable across models; a 0.83 means nothing absolute, so set thresholds empirically per model per corpus, and expect the useful range to be narrow (often 0.6-0.9).
- Asymmetric retrieval needs asymmetric handling: short queries and long documents live in different distributions — use models with query/document prompt prefixes (e.g., "query:" / "passage:" in E5-style models) exactly as documented, or recall silently drops.
- ANN indexes trade recall for speed: HNSW gives ~95-99% recall at high QPS with high memory; IVF+PQ compresses at recall cost; brute force is exact and fine below ~100k vectors — measure recall against exact search before trusting any index.
- An embedding column is a derived cache of (model, version, preprocessing): change any of those and every vector must be re-computed; mixing vectors from two model versions in one index produces garbage similarities silently.

## Apex practices
- Store the raw text and metadata alongside vectors and record model+version per row, so re-embedding and A/B-ing a new model is a batch job, not an archaeology project.
- Use Matryoshka (MRL) embeddings or dimension truncation to cut storage and latency — many models lose only 1-2 points of recall at half dimensions; quantize to int8/binary with a rescoring pass for 4-32x savings.
- Fine-tune or train a lightweight adapter on your own click/label data when domain vocabulary is heavy (legal, medical, internal jargon) — off-the-shelf embeddings routinely miss domain-specific synonymy that 10k pairs of contrastive data fixes.
- Benchmark with your own golden set (query → relevant doc IDs) built from real logs; 200 labeled queries beats any public leaderboard for model selection.

## Pitfalls
- Embedding whole documents in one vector — long inputs get averaged into mush; embed chunks and aggregate at scoring time.
- Ignoring normalization: mixing dot product on unnormalized vectors with cosine assumptions, or forgetting some models require L2-normalization before storage.
- Vector DB sprawl for a 50k-document corpus that pgvector or even NumPy handles fine — infrastructure should follow scale, not hype.

## Tools & references
MTEB benchmark, sentence-transformers, OpenAI/Voyage/Cohere/Google embedding APIs, pgvector, FAISS, HNSW paper (Malkov & Yashunin 2016), Matryoshka Representation Learning (Kusupati et al. 2022).
