# Fine-Tuning

## Scope
Adapting pretrained models to a task or domain: SFT, LoRA/PEFT, preference optimization (DPO/RLHF), data curation, and the decision of whether to fine-tune at all.

## Core principles
- Fine-tuning teaches form and behavior, not facts: it excels at style, format, tone, and task-specific skills, but is a poor and lossy way to inject knowledge — use RAG for knowledge, fine-tuning for behavior.
- The decision ladder is prompting → few-shot → RAG → fine-tuning; fine-tune only when the cheaper rungs plateau on a measured eval, because a fine-tune couples you to a base model version and adds an ops burden forever.
- Data quality dominates data quantity: 1,000 meticulously curated, deduplicated, diverse examples beat 100,000 scraped ones (the LIMA result); every bad label is a behavior you are paying to install.
- LoRA is the default, full fine-tuning the exception: rank-8-to-64 adapters recover most of full fine-tuning quality at a fraction of VRAM (QLoRA fits 70B on a single 48GB GPU), and adapters are swappable per-tenant artifacts.
- Catastrophic forgetting is real: narrow SFT degrades general capabilities and safety behavior; mix in general instruction data (replay), keep learning rates low (1e-5 to 2e-4 for LoRA), and eval on general benchmarks before and after.

## Apex practices
- Build the eval before the training set: a held-out test set with clear grading criteria is the only way to know whether the fine-tune beat few-shot prompting on the same base model.
- Train on completions only (mask the prompt tokens from the loss) for instruction data, and match the training chat template exactly to the inference template — template mismatch is the #1 silent quality killer.
- Use DPO or KTO on preference pairs when "better vs. worse" is easier to label than "correct" — it is far simpler than full RLHF and fixes tone/verbosity/refusal patterns that SFT can't.
- Start with an overfit-one-batch sanity check, then watch train/val loss divergence; for LLMs, 1-3 epochs is typical and val loss rising while train loss falls means stop.

## Pitfalls
- Fine-tuning to fix what is actually a prompt or retrieval bug — teams burn weeks of GPU time before running the baseline eval that prompting alone would have won.
- Test-set contamination via near-duplicates between train and eval (or eval data that leaked into the base model's pretraining), producing beautiful numbers and a useless model.
- Shipping a fine-tune with no re-training pipeline: the base model deprecates, the provider sunsets the endpoint, and the "asset" becomes unreproducible if data and configs weren't versioned.

## Tools & references
HuggingFace TRL/PEFT, Axolotl, Unsloth, "LoRA" (Hu et al. 2021), "QLoRA" (Dettmers et al. 2023), "LIMA" (Zhou et al. 2023), "DPO" (Rafailov et al. 2023), OpenAI/Anthropic fine-tuning guides.
