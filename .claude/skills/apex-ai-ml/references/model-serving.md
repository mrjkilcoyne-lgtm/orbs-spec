# Model Serving

## Scope
Deploying trained models for inference: batch prediction, real-time serving, model compression, and scaling. APIs, containerization, and latency requirements.

## Core principles
- Batch inference (scoring a dataset nightly, storing results) is simple and cheap; real-time inference (scoring on-demand via API) has latency requirements (10-500ms typical).
- Model size vs. latency vs. accuracy tradeoff: larger models are more accurate but slower. Compression (quantization, distillation, pruning) reduces size and latency at accuracy cost.
- Serving infrastructure must handle load: single process can serve O(10-1000) requests/sec depending on latency requirement. Scale horizontally (multiple replicas) or vertically (faster hardware).
- Reproducibility in serving: model loaded, inference produces same outputs as training (accounting for precision differences, randomness in preprocessing). Versioning and artifact storage are critical.
- Inference optimization: batching requests (amortize overhead), caching (avoid recomputing for identical inputs), and model acceleration (GPU inference, TorchScript compilation) reduce latency.

## Apex practices
- Use model serving frameworks (TensorFlow Serving, Seldon, BentoML) to containerize and deploy. They handle versioning, A/B testing, and monitoring.
- Quantize models (int8, int4, fp16) for speed and size without major accuracy loss. INT8 quantization: 4x smaller, 2-4x faster.
- Batch requests during peak load; request queuing (queue size, timeout) prevents cascading failures.
- Implement feature preprocessing in the serving layer: same transformations as training, avoiding training-serving skew (a feature computed differently during training and serving).

## Pitfalls
- Slow inference (>10s per request) for real-time use cases: users wait, servers are overloaded. Profile and optimize.
- Forgetting to handle edge cases: missing inputs, out-of-distribution samples. Graceful degradation (fallback predictions, error messages) beats crashes.
- Model versioning issues: serving an old model by accident, or not being able to rollback to a working version quickly.

## Tools & references
TensorFlow Serving, Seldon Core, BentoML, PyTorch model serving, Docker for containerization, KServe (Kubernetes serving), Ray Serve (distributed serving), model compression libraries (TensorRT, ONNX).
