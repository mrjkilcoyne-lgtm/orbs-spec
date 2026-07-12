# Small & Local Models

## Scope
Running small open-weight models (roughly 0.5B-70B) on your own hardware or edge devices: model selection, quantization, inference servers, and when local beats API.

## Core principles
- Local wins on four axes and loses on one: privacy/data-residency, latency floor (no network hop), marginal cost at sustained volume, and offline/edge operation — versus raw capability, where frontier APIs stay ahead; the decision is workload-shaped, not ideological.
- A small model on a narrow task with a good prompt (or a LoRA) can match a frontier model at 1/100th the cost: classification, extraction, routing, summarization, and PII redaction are the classic wins — open-ended reasoning and long-horizon agency are where small models visibly break.
- Quantization is the enabling technology and a quality dial: 4-bit (Q4_K_M, AWQ, GPTQ) typically costs 1-3% on benchmarks and cuts memory ~4x versus FP16 — rule of thumb: a larger model at 4-bit beats a smaller one at FP16 in the same VRAM; below 4-bit, degradation gets steep and task-dependent.
- Throughput lives in the serving layer, not the weights: continuous batching and PagedAttention (vLLM) give order-of-magnitude throughput gains over naive per-request inference; KV-cache memory — which grows with batch × context length — is usually the real capacity limit, not weight storage.
- You own the whole quality stack now: no provider safety layer, no silent upgrades, no fallback — chat-template correctness, sampling defaults, guardrails, and eval-gated model upgrades are all your responsibility.

## Apex practices
- Prototype on the API frontier model first to establish the quality ceiling and a working prompt, then step down (70B → 8B → 3B) with your eval suite until quality breaks — never start small and wonder if the task is impossible.
- Match the runtime to the deployment: llama.cpp/Ollama/MLX for laptops and edge, vLLM or SGLang with OpenAI-compatible endpoints for GPU servers — the compatible API keeps your application code portable between local and hosted.
- Distill deliberately: generate labeled data with a frontier model, fine-tune the small model on it (respecting the big model's license terms), and validate on held-out human-labeled data — teacher-student distillation is the standard route to small-model quality on narrow tasks.
- Verify the chat template and stop tokens against the model card exactly; a mismatched template silently degrades every response and is the most common "this local model is bad" misdiagnosis.

## Pitfalls
- Benchmark-chasing tiny models: leaderboard scores for sub-7B models are heavily contaminated/overfit; a 3B model that "beats GPT-4 on MMLU" will still fail your actual task — trust only your own eval.
- Ignoring total cost of ownership: GPU amortization, ops time, and utilization gaps often make self-hosting more expensive than APIs below sustained high volume — do the math with realistic utilization, not peak.
- Serving long-context traffic without KV-cache budgeting — the model fits, then OOMs at the first 32k-token request under concurrent load.

## Tools & references
llama.cpp/Ollama, vLLM, SGLang, MLX (Apple silicon), HuggingFace open-model hub, quantization methods (GGUF Q4_K_M, AWQ, GPTQ), Llama/Qwen/Gemma/Phi/Mistral model families, LMSYS Arena for rough capability ordering.
