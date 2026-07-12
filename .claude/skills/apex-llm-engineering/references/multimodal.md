# Multimodal

## Scope
LLM systems that consume or produce non-text modalities: vision (images, documents, screenshots), audio (speech-to-text, TTS), and video understanding.

## Core principles
- Images are tokens with a resolution economics: vision models tile images (e.g., ~512-768px tiles, hundreds of tokens each), so resizing and cropping strategy directly trades cost against the legibility of small text — a full-page scan at low detail loses the fine print.
- Vision-language models read like fast humans, not like OCR engines: they excel at layout, charts, and "what does this UI show?" but can misread dense tables, tiny fonts, and long serial numbers — for exact transcription of critical fields, pair with OCR or ask the model to flag low-confidence reads.
- Documents are a first-class modality: PDF-native pipelines (send page images to a VLM, or use document-parsing models) beat text-extraction-then-LLM whenever layout, tables, checkboxes, or stamps carry meaning.
- Speech pipelines are chains of loss: ASR word-error-rate compounds with downstream reasoning errors, and latency budgets are brutal — real-time voice UX needs streaming ASR, incremental LLM responses, and TTS starting on the first sentence, targeting sub-second turn-taking.
- Multimodal inputs are injection surfaces too: instructions embedded in images (visible or steganographic), audio, and screenshots bypass text-level filters; apply the same untrusted-content discipline as for retrieved text.

## Apex practices
- Preprocess images deliberately: correct orientation, crop to the region of interest, and split multi-page documents into per-page calls with page numbers in the prompt — dumping 50 pages as one blurry collage is a common self-inflicted failure.
- Anchor visual answers to evidence: ask for bounding-box coordinates, cell references, or quoted text from the image so hallucinated readings become checkable.
- Evaluate per-modality before end-to-end: measure ASR WER on your accents/domain terms, table-extraction accuracy on your documents — end-to-end evals can't tell you which stage failed.
- Cache expensive modality processing (transcripts, page renders, image descriptions) keyed by content hash; media re-processing is a silent budget destroyer.

## Pitfalls
- Sending screenshots where structured data exists — if you have the DOM, the CSV, or the API, text beats pixels in accuracy and cost every time.
- Trusting VLM reading of numbers/IDs without verification: transposed digits in an invoice total or meter reading are classic, expensive, and invisible in demos.
- Ignoring audio's real-world conditions: models eval'd on clean speech collapse on far-field mics, crosstalk, and code-switching; test on production-condition audio.

## Tools & references
Anthropic/OpenAI/Gemini vision docs, Whisper and Deepgram (ASR), provider TTS and realtime/voice APIs, DocVQA/ChartQA benchmarks, Tesseract/PaddleOCR and layout parsers (unstructured, Docling) for hybrid pipelines.
