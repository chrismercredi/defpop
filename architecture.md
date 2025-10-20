# DefPop Core — Architecture and Research Design

## 1. Research Hypothesis

> **Primary Hypothesis:** Acronyms may pollute the contextual meaning of a sentence for machine-learning models, particularly during tokenization.  
> If text is sanitized to recognize and normalize acronyms *before* tokenization, the resulting token sequences will better preserve contextual relationships, improving model confidence and stability.

---

## 2. Background

Most tokenizers (BPE, Unigram, SentencePiece) segment text statistically, unaware of semantic units like acronyms.  
For example, “SDK” may become tokens ["S", "DK"], or “TLS/SSL” may split unpredictably.  
Such fragmentation introduces noise: models treat parts of an acronym as unrelated tokens.

**Goal:** design a deterministic acronym pre-processing layer that can be evaluated for its impact on token stability and embedding coherence.

---

## 3. Research Questions

1. How often do acronyms fragment under standard tokenization?  
2. Does locking acronyms as atomic tokens reduce sequence length without harming semantics?  
3. Does acronym stabilization improve embedding or classification consistency on technical corpora?  
4. What trade-offs appear (false positives, missed detections, compute overhead)?

---

## 4. Experimental Framework (Scientific Method)

| Step | Description |
|------|--------------|
| **Observation** | Acronyms appear frequently in technical text and may be mishandled by standard tokenizers. |
| **Hypothesis** | Acronym sanitization prior to tokenization improves contextual awareness. |
| **Prediction** | Sanitized text yields fewer fragmented tokens and more stable embeddings. |
| **Experiment** | Implement deterministic parser + dictionary → feed sanitized text into tokenizers → measure metrics. |
| **Evaluation Metrics** | Token stability rate, sequence length delta, embedding cosine similarity, downstream task accuracy. |
| **Conclusion (TBD)** | Compare results; accept, reject, or refine the hypothesis. |

---

## 5. Architecture Layers (Software View)

| Layer | Description | Status |
|--------|--------------|---------|
| **DefParser** | Regex-based acronym detection; pure Dart. | ✅ MVP |
| **DefDictionary** | Lookup table mapping codes to definitions. | ✅ MVP |
| **DefResolver** | Selects correct sense if multiple exist. | ✅ MVP |
| **DefCache** | Optional memoization (string hashes). | ⏳ Planned |
| **DefLexicon (ML)** | Exports canonical + variant forms. | 🔬 Future |
| **PreTokenizer (ML)** | Marks acronym spans as atomic. | 🔬 Future |
| **Evaluation Harness** | Runs tokenization experiments. | 🔬 Future |

All components remain **pure Dart** for reproducibility and clarity.

---

## 6. Data Flow (Conceptual)

Raw text  
  ↓  
DefParser → ParseHits  
  ↓  
DefResolver + DefDictionary → ResolvedTerms  
  ↓  
(Optional) DefCache  
  ↓  
Sanitized Text → Standard Tokenizer  
  ↓  
Evaluation / Embedding / Model

---

## 7. Caching & Hashing Strategy (Deterministic)

- **parseKey** = SHA256(`text + '|' + configString`)  
- **dictionarySignature** = `name@version#count`  
- **resolveKey** = SHA256(`parseKey + '|' + dictionarySignature`)  
- All keys stored as base16/base64 strings; no I/O or persistence required for MVP.

---

## 8. Planned Evaluation Metrics

| Metric | Description |
|---------|--------------|
| **Token Stability (%)** | % of acronym mentions forming a single token after pre-tokenization. |
| **Sequence Length Δ** | Avg. tokens per 1000 chars before vs. after sanitization. |
| **Embedding Drift** | Cosine distance between baseline and sanitized embeddings of same text. |
| **Downstream Accuracy** | Change in classification or QA performance on domain corpora. |
| **False Positives/Negatives** | Human-audited precision and recall of acronym detection. |

---

## 9. Literature Review Placeholder

*(Reserved for peer-reviewed references.)*

Suggested journals & sources:  
- ACL / EMNLP / NAACL papers on tokenization and subword segmentation.  
- IEEE / Springer NLP papers on abbreviation or acronym expansion.  
- “Tokenization in LLMs: Effects on Representation and Bias” (arXiv preprints).  
- “Abbreviation Normalization in Domain-Specific Corpora.”

Add citations in this format:

| Citation | Finding | Relevance |
|-----------|----------|-----------|
| [Author, Year] | Brief summary. | Relation to DefPop hypothesis. |

---

## 10. Risks & Limitations

- Rule-based parsers may over- or under-detect acronyms.  
- Dictionaries must stay curated; domain drift can cause bias.  
- Tokenization improvements might not generalize to all models.  
- Experiments may require external toolchains (Python, tokenizer libs).

---

## 11. Learning Objectives (for project owner)

- Reinforce Dart and algorithmic design through real research framing.  
- Understand the relationship between **text preprocessing** and **model confidence**.  
- Practice hypothesis formulation, experiment logging, and result analysis.  
- Publish reproducible, transparent code that others can verify or extend.

---

## 12. Ethical & Open Science Note

All code, data, and results should remain open and reproducible.  
This repository documents personal learning, not commercial research.  
Results should be shared humbly, acknowledging limitations and potential bias.

---

## 13. Milestones

| Milestone | Deliverable | Status |
|------------|-------------|--------|
| **M0** | Architecture & hypothesis written. | ✅ |
| **M1** | Pure Dart regex parser + dictionary. | 🧩 In progress |
| **M2** | Unit tests and initial metrics. | ⏳ |
| **M3** | Prototype pre-tokenizer + tokenizer adapter. | ⏳ |
| **M4** | Evaluation report & literature integration. | 🔬 Future |

---

> *DefPop Core is a research sandbox bridging human language clarity and machine understanding.  
> It asks a simple question — do acronyms muddy context? — and seeks to answer it through transparent, reproducible experiments in Dart.*
