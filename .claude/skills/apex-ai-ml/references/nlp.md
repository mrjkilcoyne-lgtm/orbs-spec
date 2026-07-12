# Natural Language Processing

## Scope
Processing and generating natural language: tokenization, embeddings, language models, and downstream tasks (sentiment, named entity recognition, summarization, question answering).

## Core principles
- Tokenization splits text into tokens (words, subwords, characters). Word tokenization is simple but Out-of-vocabulary (OOV) words become [UNK]. Subword tokenization (BPE, WordPiece) balances vocabulary size and OOV rate.
- Word embeddings (Word2Vec, GloVe, contextual embeddings from transformers) represent words as vectors where semantically similar words are close. Non-contextual embeddings ("bank" always has the same vector) miss polysemy; contextual embeddings (BERT, GPT) embed based on context.
- Language models learn the probability distribution of text: P(word_t | context). Transformer language models (GPT) scale to billions of parameters and billions of tokens, achieving remarkable few-shot capabilities.
- Pre-training on large text corpora (books, web pages, Wikipedia) learns linguistic structure. Fine-tuning on task-specific data adapts the model. This paradigm (pre-train, fine-tune) dominates modern NLP.
- Sequence labeling tasks (NER, POS tagging) classify each token independently or generate sequences (machine translation, summarization). Decoder predictions depend on previous predictions (exposure bias): autoregressive generation, teacher forcing during training.

## Apex practices
- Use transformer-based models (BERT, RoBERTa, ELECTRA) for classification and understanding tasks. Most datasets need fine-tuning, not just prompting.
- For generation (summarization, translation), use encoder-decoder models (T5, BART, mBART) or generative models (GPT, LLaMA). Beam search improves output quality.
- Implement domain-specific pre-training if your text is specialized (medical, legal, scientific). General models miss specialized vocabulary and conventions.
- Monitor label quality: NLP datasets often have annotation disagreements or errors. Agreement metrics (inter-annotator agreement, Fleiss' kappa) catch issues.

## Pitfalls
- Using outdated embeddings (Word2Vec, GloVe) instead of contextual embeddings. Context matters; "bank" in "river bank" vs. "savings bank" need different vectors.
- Not handling rare words; OOV words become [UNK] and lose information. Subword tokenization or character-level models help.
- Assuming a model trained on general English (news, Wikipedia) generalizes to your domain (Reddit, tweets, technical docs). Domain shift is real; fine-tune or retrieve-augment.

## Tools & references
HuggingFace NLP, spaCy (lightweight NLP), NLTK, PyTorch-NLP, "Speech and Language Processing" (Jurafsky & Martin), "An Introduction to Natural Language Processing" (Eisenstein).
