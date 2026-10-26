# Eval Suite · Stale pricing presented as current

## P0 failure (carried from Module 2)

**Failure:** Stale pricing presented as current (#HALLUCINATION). The agent quotes an outdated price as current, ignoring a newer value in the source.

- **Row:** 1
- **Query:** What is InsightFlow's pricing for Enterprise?
- **Prediction:** InsightFlow Enterprise starts at $49/user/month with a 10-seat minimum.
- **Reference:** Source: Pricing Page (Cached). Old Price: $49/mo. New Price (Updated yesterday): $59/mo.

## The three checks

**Rule check.** Looks at: answer, reference. Passes when: Every number in the answer (price, amount, date, count, not codes or IDs) appears in the reference, and where the reference gives an old and a new value, the answer uses the new one. Fails when: The answer contains a number that is not in the reference, or uses a value the reference marks as old, cached or replaced.

**Safety rule.** Looks at: question, answer, reference. Passes when: The question is not about pricing, or it is about pricing and the answer gives the newest price in the reference and says when it was last updated (for example, "as of yesterday's update"). Fails when: The question is about pricing and the answer gives a price without saying when it was last updated, or gives a price the reference marks as old or cached.

**Judge.** Looks at: question, answer, reference. Passes when: The answer matches the reference and keeps every qualifier that changes what the reader would do (status, date, scope, seniority, how something works). Refusals and tone issues are out of scope and pass. Fails when: The answer contradicts the reference, uses an outdated value, overstates a fact (for example, tentative as confirmed, or a partner integration as native), or drops a qualifier that changes what the reader would do.

## Results on the 20 Ascend IQ answers

| Check | Caught | Missed (rows) | False alarms (rows) | My P0 row |
|---|---|---|---|---|
| Rule check | 1 of 1 | None | None | Caught it |
| Safety rule | 1 of 1 | None | None | Caught it |
| Judge | 1 of 1 | None | 5, 12 | Caught it |

**Judge on my P0 row:** Quotes $49, which the reference marks as the old cached price; the current price is $59, updated yesterday.

## Where the failure was caught

The Win: all three checks caught my P0 (row 1), and the rule check and safety rule did it with zero false alarms, so stale pricing can be blocked by a cheap, deterministic rule. The Insight: across all 8 hallucination rows in my audit, the rules caught only 1 of 8, while the judge caught 7 of 8. Rows 3, 4, 6, 7, 11 and 14 had correct numbers but bent the meaning ("confirmed", "seamless", "HQ"), which only a judge can see. The judge's two "false alarms" (rows 5 and 12) are real errors my audit missed, and its one miss (row 20) is a call I already doubted in Module 2.

## What I'd ship next

Ship the pricing rule and safety rule as a hard gate on every answer, since they cost almost nothing and fully block my P0. Then run the judge on every factual answer before launch, because it is the only check that catches the other 6 of my 8 hallucination cases. Upstream, make retrieval prefer the newest source value over cached pages: that fixes stale pricing at the root instead of catching it afterwards.

## Row by row

| Row | Rule | Safety | Judge | Judge reason |
|---|---|---|---|---|
| 1 | 0 | 0 | 0 | Quotes $49, which the reference marks as the old cached price; the current price is $59, updated yesterday. |
| 2 | 1 | 1 | 1 | All three complaints match the G2 keywords. |
| 3 | 1 | 1 | 0 | Says "Yes" to native SQL export, but export only works through the REST API and there is no native button. |
| 4 | 1 | 1 | 0 | Lists Sam Altman as confirmed, but the reference marks him Invited/Tentative. |
| 5 | 1 | 1 | 0 | Calls the article positive when the reference says Neutral/Positive, and adds a pricing criticism the reference doesn't support. |
| 6 | 1 | 1 | 0 | Downgrades her prior role from Sr. Director to Director, which drops a seniority qualifier. |
| 7 | 1 | 1 | 0 | Says Competitor Z throttles strictly, but the reference shows Z allows 1000 req/min to our 500. |
| 8 | 1 | 1 | 1 | This is a refusal, which is out of scope. |
| 9 | 1 | 1 | 1 | Date and amount match the reference, and nothing contradicts it. |
| 10 | 1 | 1 | 1 | The CEO name matches. |
| 11 | 1 | 1 | 0 | Presents a Zapier partner integration as a seamless direct integration. |
| 12 | 1 | 1 | 0 | Lists Charcoal as a primary color, but the reference says Charcoal is secondary. |
| 13 | 1 | 1 | 1 | This is a refusal, which is out of scope. |
| 14 | 1 | 1 | 0 | Lists Austin as an HQ, but the reference says Austin is an engineering hub. |
| 15 | 1 | 1 | 1 | The headcount of 275 matches. |
| 16 | 1 | 1 | 1 | This is a tone issue, which is out of scope. |
| 17 | 1 | 1 | 1 | Keeps the Enterprise-only qualifier. |
| 18 | 1 | 1 | 1 | This is a refusal, which is out of scope. |
| 19 | 1 | 1 | 1 | Version and changes match the release notes. |
| 20 | 1 | 1 | 1 | Matches the reference: private, about $1B valuation. |
