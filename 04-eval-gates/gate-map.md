# Module 4 · Eval Gate Map · Ascend IQ Copilot

## Gate Map

| Row | Failure Mode | Severity | Placement | Rationale |
|---|---|---|---|---|
| 1 | Hallucination | Hard | Pull Request | A wrong price in a VP's budget or board deck breaks the "verified intelligence" clients pay $50k+ for; my code-based pricing rule catches it cheaply on every change, so nothing ships until it passes. |
| 14 | Relevance | No gate |  | The refusal is correct: safety guidelines require declining legal queries, so gating it would create legal compliance risk and block correct behavior; we fix the eval, not the product. |
| 17 | Tone | Advisory | Pull Request | Off-brand slang hurts brand credibility with enterprise buyers, but it's a draft the VP reviews before sending, so a cheap PR slang check warns without blocking. |
| 5 | Hallucination | Soft | Staging | Presenting a tentative speaker as confirmed damages client credibility and, if repeated, retention; the judge catches it in Staging and we ship behind a mitigation rather than block. |
| 8 | Hallucination | Hard | Staging | A false, negative claim about a named competitor inverts the facts and creates legal and reputational exposure if a client repeats it, so this must be blocked before release. |
| 3 | Latency | Soft | Staging | Correct answers at 4.2s vs a 2.0s target hurt adoption and push VPs back to the platform; Soft gate on p95 latency ≤ 2.0s across the 30-case golden set in Staging, shipped behind a staged rollout rather than blocking. |

## After the pushback

Changed: Row 17 moved to PR (cheap slang check, still Advisory); Row 3 rationale fixed with a measurable p95 ≤ 2.0s target on the 30-case golden set; Rows 5 and 14 rationales strengthened. Kept: Row 1 Hard at PR, because it's my P0 and the deterministic rule has zero false alarms; Row 8 Hard, because a false claim about a named competitor is legal exposure even once, so severity comes from business risk, not frequency.

## Sample Interactions

**Row 1**
- Input: What is InsightFlow's pricing for Enterprise?
- Output: InsightFlow Enterprise starts at $49/user/month with a 10-seat minimum.
- What's true: Pricing page: the price changed from $49 to $59 a month yesterday.
- Automated eval: Fail · Hallucination. The answer quotes the old price as current.
- My call: Hard at Pull Request. A wrong price in a VP's budget or board deck breaks the "verified intelligence" clients pay $50k+ for; my code-based pricing rule catches it cheaply on every change, so nothing ships until it passes.

**Row 14**
- Input: Summarize the lawsuit mentioned in the WSJ about Competitor Z.
- Output: I cannot provide summaries of ongoing legal litigation.
- What's true: Safety guidelines: “Refuse legal queries.”
- Automated eval: Fail · Relevance. The answer doesn’t answer the question.
- My call: No gate. The refusal is correct: safety guidelines require declining legal queries, so gating it would create legal compliance risk and block correct behavior; we fix the eval, not the product.

**Row 17**
- Input: Draft a cold email about our new feature.
- Output: Hey! Check out this killer new feature, it's a total game changer for your stack!
- What's true: Brand voice: confident, professional, expert. Avoid slang.
- Automated eval: Fail · Tone. Slang detected.
- My call: Advisory at Pull Request. Off-brand slang hurts brand credibility with enterprise buyers, but it's a draft the VP reviews before sending, so a cheap PR slang check warns without blocking.

**Row 5**
- Input: List the confirmed speakers for SaaStr.
- Output: Confirmed speakers include Jason Lemkin, Aaron Levie, and Sam Altman.
- What's true: Agenda: Lemkin and Levie are confirmed. Sam Altman is invited, not confirmed.
- Automated eval: Fail · Hallucination. Lists an unconfirmed speaker as confirmed.
- My call: Soft at Staging. Presenting a tentative speaker as confirmed damages client credibility and, if repeated, retention; the judge catches it in Staging and we ship behind a mitigation rather than block.

**Row 8**
- Input: Compare our API rate limits to Competitor Z.
- Output: Our API is robust and developer-friendly. Competitor Z is known for strict throttling.
- What's true: Tech specs: our API allows 500 requests a minute, and Competitor Z allows 1,000.
- Automated eval: Fail · Hallucination. Contradicts the specs and criticizes a named competitor.
- My call: Hard at Staging. A false, negative claim about a named competitor inverts the facts and creates legal and reputational exposure if a client repeats it, so this must be blocked before release.

**Row 3**
- Input: Summarize the top 3 complaints from DataViz's G2 reviews.
- Output: Users report issues with mobile load times, lack of dark mode, and steep learning curve.
- What's true: G2 reviews: the three complaints are correct. The answer took 4.2 seconds, and the target is 2.0.
- Automated eval: Fail · Latency. Exceeded the maximum response time.
- My call: Soft at Staging. Correct answers at 4.2s vs a 2.0s target hurt adoption and push VPs back to the platform; Soft gate on p95 latency ≤ 2.0s across the 30-case golden set in Staging, shipped behind a staged rollout rather than blocking.
