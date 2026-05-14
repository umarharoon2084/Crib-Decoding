# Crib-Decoding: Constraint-Aware Pruning for Efficient LLM Inference

**Turning "impossible tokens" into free speedups — inspired by Turing's Bombe and smartphone keyboards.**

---

## 🎯 The Idea

Large Language Models waste enormous computation evaluating **impossible or highly implausible** next tokens.

After the prompt *"The cat sat on the..."*, a model should **not** seriously consider tokens like `needle`, `supernova`, `democracy`, or `quantum entanglement`. Yet today's transformers compute logits over the entire vocabulary (50k–200k tokens) every single step.

This is the modern equivalent of the Bombe testing every possible Enigma setting instead of using known plaintext patterns ("cribs") to eliminate millions of impossibilities upfront.

**Crib-Decoding** proposes a practical two-stage architecture:

1. **Fast Crib Filter** (lightweight, symbolic + small neural net) — Eliminate 95–99% of impossible candidates using grammar, common-sense, physics, and context.
2. **Target LLM** — Run the heavy model **only** on the shortlist of plausible candidates.

This mirrors:
- Turing’s use of predictable repetitive phrases in Enigma messages.
- How smartphone keyboards (Gboard, SwiftKey, etc.) deliver instant next-word suggestions using tiny models + smart pruning.

---

## 🚀 Why This Matters

- **Massive efficiency gains** possible on edge devices, real-time applications, and high-volume serving.
- Complements existing techniques like **speculative decoding**, Medusa, lookahead decoding, and dynamic vocabulary pruning.
- Brings **hybrid neuro-symbolic** thinking back into modern LLM inference.

---

## 🧠 Core Insight

Language is **highly constrained**. Humans instantly reject absurd continuations. Current LLMs *know* these constraints statistically but still pay the full computational cost every time.

> "A cat cannot sit on a needle"  
> — Simple example of a hard world-knowledge constraint that should be filtered in microseconds.

---

## 📋 Proposed Architecture

| Stage | Method | Cost | Responsibility |
|-------|--------|------|----------------|
| 1. Fast Filter | N-gram + small NN + rule-based constraints | Negligible | Grammar, physics plausibility, user context, domain rules |
| 2. Candidate Ranking | Main LLM (or speculative draft) on shortlist (k=10–100) | 5–100x cheaper | Final probability distribution |
| 3. Verification | Standard acceptance (or speculative verification) | - | Maintain output quality |

---

## 🔍 Inspiration Sources

- **The Imitation Game** — Turing’s use of cribs to crack Enigma.
- **Smartphone Keyboards** — Real-world deployment of tiny, personalized, constraint-aware next-word prediction.
- Existing Research — Speculative decoding, dynamic vocabulary pruning, constrained decoding, neuro-symbolic hybrids.

---

## 🛠️ Project Goals

- Formalize the "Crib Filter" concept.
- Build minimal viable prototypes (starting with toy models and keyboard-style predictors).
- Integrate with existing engines (`llama.cpp`, `vLLM`, Hugging Face).
- Explore learnable vs rule-based vs hybrid filters.
- Benchmark real speed/quality tradeoffs.

---

## 📌 Current Status

**Idea stage with strong historical + practical grounding.**  
Looking for collaborators, feedback, and early implementers.

This is intentionally simple and actionable — the kind of insight that can evolve into production optimizations.

---

## 🤝 How to Contribute

1. **Discussion** — Open an issue with your thoughts, criticisms, or extensions.
2. **Prototyping** — Even a small proof-of-concept (e.g., n-gram + rule filter on top of a 1B model) would be valuable.
3. **Literature** — Help link this idea to related papers.
4. **Real-world examples** — Share more "cat on a needle" style constraints from your domain.

---

## 📚 Related Work

- Speculative Decoding (Leviathan et al., 2022 and many follow-ups)
- Dynamic Vocabulary Pruning in Early-Exit LLMs
- Constrained Decoding frameworks (Outlines, Guidance)
- Neuro-Symbolic AI approaches

*(We'll expand this section as the project grows)*

---

## 📄 License

MIT License — feel free to use, adapt, and build upon.

---

## 🙋‍♂️ Origin

This concept was developed in conversations highlighting inefficiencies in current LLM inference and drawing parallels from code-breaking history and everyday technology (smartphone keyboards).

**"The next leap won't come from brute force alone — it will come from intelligently pruning the impossible."**

---

**Star this repo if you believe intelligent constraints belong in the next generation of LLM architectures.**

---
