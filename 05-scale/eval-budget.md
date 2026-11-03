# Module 5 · Eval Budget · Ascend IQ

**Quarterly budget cap:** $200,000
**Online eval spend:** $175,000 (3 of at most 3 online evals)

## Budget

| Failure | Trust metric | Risk | Level | Cost |
| --- | --- | :---: | :---: | ---: |
| Data Fabrication | Hallucination Rate | P0 | Online eval | $85,000 |
| Context Specificity | Robustness | P1 | Periodic audit | $7,000 |
| Overconfident Tone | UX Trust | P1 | Online eval | $65,000 |
| Data Bias | Fairness | P2 | Periodic audit | $5,500 |
| Slow Answers | Latency | P3 | Online eval | $25,000 |

## Downgrades

### Periodic audit · Context Specificity (Robustness · P1)
- **Cheaper check:** On every answer, an automated check compares the filters in the question (region, date range, sentiment, source) with the filters actually applied in retrieval and blocks any answer that dropped one. Each week, a reviewer also samples 50 multi-part and filtered answers to catch subtler misses the automated check can't see.
- **Why it’s enough:** The automated filter check catches the dangerous case, an answer that quietly ignored "APAC" or "last 30 days", on every answer, not just in a sample; the weekly audit catches partial misses in meaning. What it misses is an answer that applied the right filters but still focused on the wrong part of the question, and we accept that until the audit shows it recurring, at which point we buy this an online eval next quarter.

### Periodic audit · Data Bias (Fairness · P2)
- **Cheaper check:** Each week, a reviewer samples 50 answers per region (US, EMEA, APAC) and scores coverage, data quality and sentiment-scoring consistency against the sources, comparing each region's scores with the US baseline.
- **Why it’s enough:** Bias is a pattern that shows up across many answers, which a per-region weekly sample is built to measure. It misses single skewed answers between audits; we move it to an online eval if any region's quality score falls more than 10 points below the US baseline in two consecutive audits.

