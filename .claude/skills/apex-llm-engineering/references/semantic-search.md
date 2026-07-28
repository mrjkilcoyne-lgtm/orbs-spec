# Semantic Search

## Scope
Search systems that match meaning rather than keywords: dense retrieval, hybrid ranking, query understanding, and relevance evaluation for search as a product surface.

## Core principles
- Search is a ranking problem with an unforgiving UX: users judge the top 3 results; recall@100 is a pipeline metric, NDCG@10 and "did they click/stop searching?" are the product metrics.
- Dense and lexical retrieval fail differently, which is why hybrid wins: embeddings handle synonymy and paraphrase ("laptop won't start" → "boot failure") but miss exact codes, names, and negations; BM25 nails exact terms but misses paraphrase — fuse with RRF and let a cross-encoder reranker sort the union.
- Query understanding is half the system: real queries are short, misspelled, and underspecified — spell-correct, expand acronyms, classify intent, and rewrite before retrieval; garbage query in, garbage candidates out, regardless of index quality.
- Relevance is not similarity: the nearest vector may be a duplicate, an outdated version, or the question itself rather than its answer — production ranking must blend semantic score with freshness, popularity, source authority, and deduplication.
- You cannot tune what you don't judge: build a golden set of (query → graded results) from real logs, and re-judge as the corpus and users drift; offline NDCG plus online CTR/abandonment is the complete instrument panel.

## Apex practices
- Mine your search logs monthly for the three failure archetypes — zero-result queries, queries with no clicks, and query reformulation chains — each one is a labeled bug report from a real user.
- Use metadata filters as first-class citizens (date, type, ACL, product area) applied at retrieval time; most "bad relevance" complaints in enterprise search are actually permission or freshness misses.
- Tune the lexical/semantic balance per query class: identifier-like queries (SKUs, error codes, names) should weight BM25 heavily or bypass vectors entirely; natural-language questions lean dense — a query classifier that routes is worth more than a better embedding.
- Ship snippets and highlighting that show why a result matched; semantic matches without visible evidence read as random to users and destroy trust in the ranker.

## Pitfalls
- Replacing a tuned BM25 system wholesale with vectors and shipping a net relevance regression on the exact-match queries that dominate traffic — hybrid is the migration path, not big-bang.
- Evaluating with cosine-similarity spot checks instead of graded judgments; "the vectors look close" has no relationship to user-perceived relevance.
- Ignoring index freshness lag: minutes-old documents missing from results reads as data loss to users; know your embedding-to-searchable latency and surface it.

## Tools & references
BM25/Elasticsearch/OpenSearch, Vespa, Qdrant/Weaviate/pgvector, Reciprocal Rank Fusion (Cormack et al. 2009), cross-encoder rerankers (Cohere Rerank, BGE-reranker), BEIR benchmark, "Introduction to Information Retrieval" (Manning et al.).
