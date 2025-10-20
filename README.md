# DefPop: Acronym-Aware Text Sanitization  
for Tokenization Research

**Repository Type:** Research / Experimental Learning Project  
**Primary Language:** Dart (pure)  
**Status:** Early-stage hypothesis testing  

---

## 1. Summary

**DefPop** (Definition Popups) is a continuation of  
[Dashronym](https://github.com/your-username/dashronym).  
Dashronym explored inline definitions for humans;  
DefPop explores how acronyms might affect *machines*.

This repository treats the problem scientifically:

> **Hypothesis:** Acronyms could pollute (sully/dirty)  
> the contextual meaning of a sentence for machine  
> learning models, especially during tokenization.  
> If text were sanitized for acronyms first, and  
> then tokenized, the resulting tokens might preserve  
> context better and yield higher confidence or  
> consistency in downstream tasks.

---

## 2. Objective

To test whether **acronym-aware preprocessing** can  
improve contextual stability in text representation  
and language-model behavior.  

The first phase is **pure Dart** — building deterministic  
tools to detect and standardize acronyms.  

Later phases may involve **empirical ML evaluation**  
using existing tokenizers and benchmarks.

---

## 3. Research Method (High Level)

| Phase | Goal | Method |
|-------|------|--------|
| **MVP (Phase 1)** | Implement deterministic acronym detection  
and dictionary lookup in pure Dart. | Regex parser → dictionary resolver → unit tests  
for precision/recall. |
| **Phase 2** | Integrate as a *pre-tokenizer* before a standard  
tokenizer (BPE, Unigram). | Measure token stability, sequence length,  
and meaning retention. |
| **Phase 3** | Evaluate effect on model outputs. | Compare baseline vs. sanitized text using  
small LLMs or open embeddings. |
| **Phase 4** | Publish findings, open the lexicon, and discuss  
results. | Prepare a short paper or blog post summarizing  
the data. |

---

## 4. Planned Deliverables

- `packages/defpop_core/` — Pure Dart implementation  
  (regex parser, dictionary, resolver, optional cache).  
- `packages/defpop_flutter/` — Visualization and  
  annotation tools (future).  
- `docs/ARCHITECTURE.md` — Architecture + research design.  
- `docs/ROADMAP.md` — Tasks, milestones, experiments.  
- `data/` — (Later) sample corpora or acronym dictionaries.

---

## 5. Literature & References

*(To be expanded — placeholder for peer-reviewed sources.)*

Search keywords:
- “tokenization stability in natural language processing”
- “subword segmentation bias”
- “acronyms in domain-specific corpora”
- “pre-tokenization for contextual embeddings”
- “abbreviation expansion and NLP accuracy”

Proposed structure for later inclusion:

| Citation | Summary | Notes |
|-----------|----------|-------|
| [Author, Year] | Key finding related to acronym or abbreviation  
handling in NLP. | Relation to DefPop hypothesis. |

---

## 6. Why Pure Dart?

- Dart is awesome!
- Easy to wrap in Flutter later for visualization.

---

## 7. Ethical Position & Humility

This is a **learning-driven research sandbox**,  
not a commercial product.  

All code, thoughts, and assumptions come from  
a personal exploration of text and meaning.  

Results may be anecdotal at first —  
the purpose is curiosity and skill growth,  
not authority.

---
