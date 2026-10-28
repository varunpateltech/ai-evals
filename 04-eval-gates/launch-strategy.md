# Module 4 · Launch Strategy · Ascend IQ Copilot

## 4.0 Release Criteria

| Gate | Failure | Metric | Threshold | Dataset | Method | Runs at |
|---|---|---|---|---|---|---|
| Hard | Stale pricing presented as current (#HALLUCINATION, Hallucination Rate). Output-level: Ascend IQ quotes an outdated price as current when the source shows a newer one. | Share of pricing answers that quote the newest source price and state when it was last updated | 100% of pricing answers must pass both the rule check and the safety rule (zero stale prices). Any single failure blocks the answer from reaching the client. | Ascend IQ golden set | Code-based check | Pull Request |
| Soft | Row 3 · Latency: exceeded the maximum response time | p95 response time on the golden set | p95 ≤ 2.0 seconds | Ascend IQ golden set | Code-based check | Staging |
| Advisory | Row 17 · Tone: slang detected | Share of drafted emails flagged for slang or off-brand words | ≤ 5% of drafts flagged (warn only, never blocks) | Ascend IQ golden set | Code-based check | Pull Request |

## CI Gate Request for Engineering

- **Hard gate · Stale pricing presented as current (#HALLUCINATION, Hallucination Rate). Output-level: Ascend IQ quotes an outdated price as current when the source shows a newer one.** Check: the code-based check, run on the Ascend IQ golden set at Pull Request. Measures: Share of pricing answers that quote the newest source price and state when it was last updated. Passes when: 100% of pricing answers must pass both the rule check and the safety rule (zero stale prices). Any single failure blocks the answer from reaching the client. On a fail: block the merge.
- **Soft gate · Row 3 · Latency: exceeded the maximum response time.** Check: the code-based check, run on the Ascend IQ golden set at Staging. Measures: p95 response time on the golden set. Passes when: p95 ≤ 2.0 seconds. On a fail: pause the release until the PM signs off on an override.
- **Advisory gate · Row 17 · Tone: slang detected.** Check: the code-based check, run on the Ascend IQ golden set at Pull Request. Measures: Share of drafted emails flagged for slang or off-brand words. Passes when: ≤ 5% of drafts flagged (warn only, never blocks). On a fail: post a warning, and don't block.

## Mitigation Plan · Soft Gate

If our Soft gate fails (p95 latency above 2.0 seconds), I recommend a staged rollout: launch to 5 of the top 50 accounts first, measure p95 on real traffic for two weeks, and expand only once it holds at 2.0 seconds or below, rolling back if it rises above 3.0 seconds. This limits slow answers to a few accounts while engineering fixes speed, instead of delaying the launch for everyone.
