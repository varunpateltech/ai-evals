# Ship-or-Hold Memo · Ascend IQ

> **Decision:** HOLD

## The Answer

I recommend we hold the Ascend IQ launch to our top 50 accounts, because stale pricing, our P0 failure, does not yet meet the release bar we set, and shipping now would knowingly put wrong prices in front of our largest clients.

## The Arguments

### 1. Hallucination, the failure type behind our P0, is too frequent to ship: wrong facts like stale prices would reach clients regularly, not rarely.

Evidence: The only pricing question in our 20-answer audit returned a stale price (0 of 1 pricing answers passed, against a 100% release bar), and hallucinations overall hit 8 of 20 audited answers (HIGH frequency).

### 2. We can reliably detect the P0 before it reaches a client, so the fix can be verified before we launch.

Evidence: The rule and safety checks caught the stale-pricing answer with zero false alarms across all 20 answers, and the judge caught 7 of 8 hallucinations.

### 3. Our second-biggest risk has no check yet, so we can't yet say how often it would reach clients.

Evidence: The agent refused answerable questions in 2 of 20 audited answers (P1); its pass rate with a check is not measured yet.

## Next Step · Decision Needed

Approve the four-week hold by November 7, with engineering accountable for fixing pricing freshness and adding a robustness check by November 25, and authorize a staged rollout to 5 of the top 50 accounts on December 1 only if the Hard gate passes at 100%.
