# Sequence Models

## Scope
Processing sequential data (time series, text, audio): RNNs, LSTMs, GRUs, and attention mechanisms. Modeling temporal dependencies and variable-length inputs.

## Core principles
- Sequences have memory: the output depends on the entire history. RNNs maintain hidden state (recurrent connection) that propagates information forward. h_t = f(h_{t-1}, x_t).
- Vanishing gradients plague RNNs: backpropagation through time (BPTT) multiplies gradients over many steps; if gradient < 1, it shrinks exponentially. LSTMs (Long Short-Term Memory) solve this with gating mechanisms (forget, input, output gates) that preserve gradients.
- Attention mechanisms allow the model to focus on relevant parts of the input. Instead of compressing the sequence into a single vector (which loses information), attention computes a weighted combination of all timesteps.
- Transformer architecture (encoder-decoder with multi-head attention, no recurrence) replaced RNNs for most tasks. Transformers parallelize better (no sequential dependency), train faster, and scale to longer sequences.
- Sequence-to-sequence models (encoder reads input, decoder generates output) handle variable-length inputs and outputs (machine translation, summarization, question answering).

## Apex practices
- Use transformers (BERT, GPT-2, T5) for language tasks; they outperform RNNs consistently. Transfer learning from pre-trained models is the default.
- For time-series with known patterns (daily/seasonal), try traditional methods first (ARIMA, exponential smoothing); neural networks require more data and aren't always worth the complexity.
- Use beam search (explore multiple hypotheses during decoding) for generation tasks (machine translation, text generation) to improve output quality vs. greedy decoding.
- Handle variable-length sequences with masking: mark padding tokens so the model ignores them in attention and loss computation. Without masking, the model learns to attend to padding.

## Pitfalls
- Using simple RNNs instead of LSTMs/GRUs for long sequences; vanishing gradients cripple learning.
- Applying RNNs to tasks where transformers are better (NLP); transformers are faster and often outperform RNNs.
- Concatenating all timesteps into a flat vector for downstream tasks; this loses temporal structure. Use attention or pooling to aggregate.

## Tools & references
PyTorch (torch.nn.LSTM, torch.nn.Transformer), HuggingFace Transformers, "Attention Is All You Need" (Vaswani et al., 2017 paper), Karpathy's RNN blog post, sequence modeling surveys.
