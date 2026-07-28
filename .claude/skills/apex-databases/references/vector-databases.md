# Vector Databases

## Scope
Storing and searching high-dimensional embeddings for semantic search, recommendations, and similarity. Vector indexes (HNSW, IVF, LSH). Milvus, Pinecone, Weaviate, and PostgreSQL pgvector.

## Core principles
- Embeddings are dense numerical vectors (768, 1536 dimensions) from neural networks (transformers, LLMs). Similarity (cosine, L2 distance) approximates semantic meaning: similar embeddings often represent semantically similar concepts.
- Exact nearest-neighbor search is O(N) (distance to every point); approximate nearest-neighbor (ANN) indexes reduce to O(log N) by sacrificing 1-5% accuracy. HNSW (Hierarchical Navigable Small World) and IVF (Inverted File) are common.
- HNSW builds a navigable graph where each point links to nearby neighbors at multiple scales (small-world property). Traversing the graph quickly finds approximate neighbors; no explicit quantization needed.
- IVF partitions vectors into clusters, then searches only relevant clusters. Coarser partitions = faster search but lower accuracy. Typically search top-k clusters, then exhaustive search within each.
- Dimensionality and cardinality matter: 768-dim embeddings are standard (BERT/sentence-transformers); 1536-dim for OpenAI embeddings. Millions to billions of vectors require distributed indexing or cloud services.

## Apex practices
- Normalize embeddings before indexing and querying; cosine similarity treats normalized vectors correctly (dot product = cosine). Preprocessing saves computation and enables optimizations.
- Batch insert; adding vectors one-by-one is slow (index updates are expensive). Bulk-insert and rebuild index periodically.
- Use metadata filtering in queries: "find nearest neighbors where source='wikipedia'" reduces search space. Most vector DBs support hybrid queries (vector similarity + metadata filter).
- Monitor recall vs latency tradeoff: parameter tuning (HNSW ef, IVF nprobe) trades accuracy for speed. Profile your workload and set parameters accordingly.

## Pitfalls
- Using vector databases for exact nearest-neighbor, where a simple sorted list is faster. Vector DBs shine at 100M+ vectors; for <1M, a relational DB with indexes may be cheaper.
- Assuming embeddings from different models are comparable (OpenAI and Hugging Face embeddings are incompatible); queries and stored vectors must use the same embedding model.
- Not reindexing after bulk data updates; the index becomes stale and recall degrades silently.

## Tools & references
Milvus documentation (HNSW, IVF tuning), Pinecone (serverless vector DB), Weaviate, pgvector (PostgreSQL extension), "Approximate Nearest Neighbor Algorithms" (survey), embedding models (Hugging Face, OpenAI).
