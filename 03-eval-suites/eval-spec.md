# Eval Spec · Stale pricing presented as current

| Part | Spec |
|---|---|
| Target risk | Stale pricing presented as current (#HALLUCINATION, Hallucination Rate). Output-level: Ascend IQ quotes an outdated price as current when the source shows a newer one. |
| Evaluator | The rule check (every number in the answer must match the reference and use the newest value) plus the safety rule (every pricing answer must give the newest price and say when it was last updated). Both run on every answer. The LLM judge runs on every release to catch meaning-level hallucinations the rules can't see. |
| Threshold | 100% of pricing answers must pass both the rule check and the safety rule (zero stale prices). Any single failure blocks the answer from reaching the client. Based on: both rules caught the P0 (row 1) with zero false alarms across all 20 answers, so a 100% hard gate blocks the real failure without blocking correct answers. |
| Business stakes | One wrong price in a VP's budget or board deck breaks the "verified intelligence" clients pay $50k+ a year for, risking churn across the top 50 accounts and Q4 renewals. |
| Owner | Ascend IQ PM owns the threshold and the ship call. The ML engineering lead runs the checks in CI and production and reviews any blocked answers weekly. |

## Messages

**Engineering · acceptance criteria:** Treat an answer as a pricing answer when the question asks about price, cost, plans or tiers, or the answer contains a currency amount. A pricing answer passes only if (1) every price, amount, date and count in it appears in the retrieved source, (2) where the source holds more than one value, the answer uses the one with the latest timestamp, and (3) it states when that price was last updated. If any condition fails, do not return the answer: return the fallback message from Design instead, and log the question, the blocked answer and the source to the weekly review queue. Run both rules on every answer in production and on the full eval set in CI, with a 100% pass threshold; a single failure in CI blocks the release. Run the LLM judge on the eval set every release and report its hallucination catch rate; it does not block releases until we have tuned it on a larger labelled set.

**Design · what the user sees:** When the check blocks an answer, the user never sees the unconfirmed price. They see: "I couldn't confirm the current price for this, so I've held back my answer rather than risk an outdated figure. You can check the latest pricing in the source below or ask your Ascend analyst." The message sits where the answer would be, with a link to the source page and an "Ask an analyst" button, and uses the normal answer styling, not an error state, so it reads as a deliberate accuracy safeguard.

**Leadership · risk and return:** One stale price in a VP's budget or board deck is enough to break the "verified intelligence" our top 50 accounts pay $50k+ a year for, and with Q4 renewals at risk we can't absorb that. The fix is cheap: two simple rules caught the stale-price case with zero false alarms in our 20-answer audit, so the gate stops the failure without blocking good answers. The trade-off is that a client occasionally gets "I couldn't confirm the current price" instead of a number, which we judge far less damaging than a wrong one. We will confirm the false-alarm rate on a larger test set before launch.
