# AI Evaluation Strategy Canvas

> Repo file `ai-evals/01-evaluation-strategy/strategy-canvas.md` (the repo is your submission).

## 1. Product Strategy, The Context

**Who it's for:** VP-level strategists and product leaders at Fortune 500 companies who pay upward of $50,000 a year for verified market intelligence.

**What they use it for:** Asking plain-language questions, like “Compare the pricing models of Stripe and Adyen,” and getting answers in seconds instead of digging through the platform.

**What's at stake:** Engagement is dropping, Q4 retention is at risk, and the CPO wants Ascend IQ live for the top 50 enterprise accounts next month. One poor answer to the wrong client can do lasting damage to the relationship.

## 2. Measurements, The Execution

**User promise.** For VP-level strategists and product leaders at Fortune 500 companies, Ascend IQ promises to answer plain-language market questions in seconds with facts that match our verified sources, so that they can act on those answers in high-stakes decisions and keep renewing their $50k+ subscriptions.

**Top 3 trust metrics:**
- **Latency**, Response speed (P95 / P99). Slow kills engagement.
- **Hallucination Rate**, % of outputs that are confidently false or fabricated.
- **Robustness**, Coherence on messy, adversarial, out-of-scope inputs.

**Why these three:** They cover the three parts of the promise. Hallucination Rate covers verified, Robustness covers plain-language questions, and Latency covers in seconds. Fairness and UX Trust matter less for this launch, which is 50 accounts asking factual questions.

## 3. Strategic Trade-Offs, The Cost

### Trade-off 1 · Hallucination Rate ↔ Latency
We prioritize Hallucination Rate over Latency because a slower verified answer costs a VP a few seconds, while a fast wrong one in a board deck can cost us a $50k account.

### Trade-off 2 · Hallucination Rate ↔ Robustness
We prioritize Hallucination Rate over Robustness because saying “I can’t verify that” on an edge-case question is recoverable, while a confident fabrication is not. We’ll limit refusals to questions the data truly can’t answer.

---
_Generated from the AI Evaluation Strategy Canvas, M1 lab tool, AI Evals Certification._