# RAG (Retrieval-Augmented Generation)

## Scope
Grounding LLM answers in external knowledge via retrieve-then-generate pipelines: retrieval architecture, context assembly, and answer synthesis.

## Core principles
- RAG quality is retrieval quality: if the answer isn't in the retrieved chunks, no prompt will save you — debug retrieval (recall@k against a labeled set) before touching generation.
- Hybrid retrieval (dense vectors + BM25 keyword, fused with Reciprocal Rank Fusion) beats either alone; embeddings miss exact identifiers, part numbers, and rare terms that lexical search nails.
- Retrieval and reranking are different jobs: cast a wide net (top 50-100 by fast ANN search), then apply a cross-encoder reranker to pick the top 5-10 — bi-encoders trade accuracy for speed and rerankers buy it back.
- The generator must be allowed to abstain: "answer only from the provided context; if the context is insufficient, say so" plus citation requirements converts silent hallucination into detectable refusal.
- Freshness and permissions are retrieval-time concerns, not index-time: filter by ACL and recency at query time, because baking user permissions into the index leaks data on the first role change.

## Apex practices
- Transform queries before retrieval: rewrite conversational follow-ups into standalone queries, and use HyDE (hypothetical document embeddings) or multi-query expansion when raw user queries are short or vague.
- Evaluate the pipeline in layers with distinct metrics — retrieval (recall@k, MRR), grounding (faithfulness/attribution), and answer quality (correctness) — so you know which stage regressed.
- Include chunk metadata (title, section, date, source URL) in the context block and require inline citations like [1]; it improves grounding and gives users a trust anchor.
- Cache aggressively at the embedding and retrieval layers; identical or near-duplicate queries dominate real traffic, and semantic caching of final answers needs an explicit staleness policy.

## Pitfalls
- Treating "add more chunks" as the fix for bad answers — beyond ~10 chunks precision falls, contradictions creep in, and the model anchors on distractors.
- Skipping the null case: benchmarks where every question has an answer in the corpus hide the fact that production users constantly ask things the corpus doesn't cover.
- Indexing raw HTML/PDF sludge — boilerplate, nav bars, and headers/footers poison both embeddings and generation; parsing and cleaning is half the work of RAG.

## Tools & references
"Retrieval-Augmented Generation" (Lewis et al. 2020), RAGAS and promptfoo for evals, Cohere/Voyage/BGE rerankers, LlamaIndex and LangChain (patterns, not gospel), pgvector/Qdrant/Weaviate/Pinecone.
