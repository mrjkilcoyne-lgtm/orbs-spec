# Chunking Strategies

## Scope
Splitting documents into retrieval units for embedding and RAG: chunk sizing, boundaries, overlap, metadata, and structure-aware splitting.

## Core principles
- A chunk must stand alone: the retriever sees chunks, not documents, so a chunk that begins "It also supports this option" is unfindable — every chunk needs enough self-contained context (or injected context) to be interpretable in isolation.
- Chunking is a two-sided trade: small chunks (100-300 tokens) embed precisely but strip context; large chunks (800-1500) preserve context but dilute the vector and stuff the prompt — the resolution lies in decoupling retrieval size from generation size (retrieve small, expand to parent/neighbors).
- Structure beats arithmetic: splitting on document semantics — headings, sections, list items, code blocks, table boundaries — consistently outperforms fixed character windows; a chunk that severs a table from its header or a function from its signature is damaged goods.
- There is no universal chunk size: optimal chunking depends on document type (contracts vs. chat logs vs. code), query style, and embedding model context — it's a tunable hyperparameter that must be swept against your retrieval eval, not copied from a tutorial.
- Metadata is part of the chunk: title, section path ("Manual > Setup > Networking"), date, and source prepended to the chunk text improve both embedding quality and the generator's ability to cite — a bare paragraph loses its provenance.

## Apex practices
- Use contextual enrichment for corpora with heavy cross-references: prepend an LLM-generated one-line summary of where the chunk sits in its document (Anthropic's "contextual retrieval" cut retrieval failures ~35-49% combined with hybrid search+reranking).
- Parse before you split: run PDFs/HTML through a real structure parser (layout model, DOM-aware extractor) so headings, tables, and reading order survive; chunking unparsed extraction sludge caps your ceiling regardless of strategy.
- Keep modest overlap (10-20%) for prose to heal boundary cuts, but dedupe near-identical chunks at index time — overlap plus boilerplate is how five near-copies of the same paragraph fill all top-k slots.
- Chunk code by syntactic units (functions, classes) via AST or tree-sitter, keeping signatures with bodies and imports available via metadata; line-window chunking of code retrieves noise.

## Pitfalls
- Fixed 1000-char splits with a naive splitter that cuts mid-sentence, mid-table, mid-code-block — the default everyone ships first and the cause of a plurality of "RAG doesn't work" complaints.
- Optimizing chunking by eyeballing chunks instead of measuring retrieval recall on labeled query→chunk pairs; chunks that look tidy can retrieve terribly.
- Forgetting re-chunking is re-indexing: chunking strategy changes invalidate every stored vector and chunk ID; version your chunking pipeline like a schema.

## Tools & references
Anthropic "Contextual Retrieval" (2024), LangChain/LlamaIndex splitters (recursive, semantic, parent-document), unstructured/Docling for parsing, tree-sitter for code, chunk-size sweep via RAGAS or custom recall evals.
