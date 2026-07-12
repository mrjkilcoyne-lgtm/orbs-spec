# Transformers

## Scope
Attention-based architecture (encoder, decoder, self-attention). Scaling to billions of parameters: language models (GPT, BERT), multimodal models (CLIP), and foundation models.

## Core principles
- Self-attention computes relationships between all positions in parallel: query (what to look for) and key (what's available) produce attention weights, applied to values (the information). Parallelism beats sequential RNNs.
- Multi-head attention uses multiple sets of (query, key, value) projections; each head learns different relationships (one head attends to nearby words, another to semantically similar words). Diversity improves expressiveness.
- Position encoding adds information about absolute or relative positions (RoPE, ALiBi); without it, the model is position-invariant ("dog the cat the" = "the dog the cat").
- Scaling laws govern transformer performance: loss improves smoothly with more data, parameters, and compute (Chinchilla, Scaling Laws for Neural Language Models). Training is expensive (billions of parameters, terabytes of data).
- Context window (maximum sequence length) is a hard limit: attending to 1M tokens is slower than 512 tokens. Sparse attention, retrieval-augmented generation, or hierarchical processing enable longer contexts.

## Apex practices
- Start with a pre-trained model (BERT for understanding, GPT for generation) and fine-tune on your task. Pre-training on billions of tokens captures language structure; fine-tuning adapts to specifics.
- Use instruction tuning (training on input-output examples formatted as instructions) for better few-shot behavior (Claude, ChatGPT). This is often better than traditional fine-tuning.
- Implement efficient attention (Flash Attention, grouped-query attention) and quantization (int8, int4) to reduce memory and latency. Standard attention is O(N^2) in sequence length.
- Monitor loss scaling and gradient norms during training; transformers are sensitive to learning rate and can diverge suddenly. Use learning rate schedules and gradient clipping.

## Pitfalls
- Training large transformers without data validation; if training data has duplicates or errors, the model learns them. Deduplicate and clean data carefully.
- Fine-tuning on small datasets (< 1K examples) often doesn't improve much over in-context learning (prompt engineering). Very small data risks overfitting.
- Assuming bigger is better; large models are slower and more expensive. Smaller models (DistilBERT, TinyLLaMA) are often sufficient and faster.

## Tools & references
HuggingFace Transformers library, PyTorch, "Attention Is All You Need" (Vaswani et al.), "Language Models are Unsupervised Multitask Learners" (GPT-2 paper), LLaMA, Megatron-LM for large-scale training.
