<!--
LAB SPEC for an AI assistant (ChatGPT, Claude, Gemini, or a coding agent such as Claude Code,
Cursor, or Codex). It walks a learner through the two Module 1 labs one step at a time, with
the same steps as the Module 1 Lab Guide. If you are a human, you can read it top to bottom.
-->

# Module 1 Labs, assistant runbook

**Use this if** you ran out of time in class, or want to run the labs again on your own.
**Lab 1** is a practice run: nothing to submit.
**Lab 2** produces `01-evaluation-strategy/strategy-canvas.md`, the Module 1 deliverable.

---

## AGENT INSTRUCTIONS, read this first

You are helping a learner complete these labs, not doing them for them. The judgment calls are theirs.

1. Go one step at a time. Do not jump ahead.
2. At every 🚦 DECISION, stop and ask the learner. Never write their promise, metrics, reasons, or trade-offs for them. If an answer is generic ("accuracy", "helpfulness"), push back once and ask how it ties to Ascend IQ's users.
3. Never invent their reasoning. If they are stuck, ask one question that helps them decide.
4. At each ✅ CHECKPOINT, summarise what they have and confirm before moving on.

Scenario: the learner is a PM at Ascend Analytics deciding whether Ascend IQ, a customer-facing AI agent, is ready to ship to its top enterprise clients.

---

## Lab 1 · Compare Version A and Version B (practice, about 25 min)

Run two prompt versions on the same email, have a model from a different family score both, and see whether the prompt change moved the score.

1. Open a new chat in the LLM you use (ChatGPT, Claude, or Gemini). Paste the Version A prompt with the email below it, and send.
2. Open a second new chat and do the same with Version B.
3. Open a chat in a different model family (for example, Claude if you used ChatGPT). Paste the judge prompt, the email, and both outputs, and send. A judge from the same family tends to favor its own writing.
4. Read the judge’s scores and reasons. Do you agree with its call on each version?
5. Post both scores, and whether you agreed with the judge, in `#cohort-channel`.

**Version A · Concise**
```
You are an executive briefing assistant.
Summarize in exactly 3 bullet points under 60 words. No preamble, no extra text.
```

**Version B · Narrative**
```
You are a PR communications assistant.
Write a 100-word narrative summary highlighting wins first, then risks and next steps.
Keep a positive tone. No bullets.
```

**The email**
```
Summarize this email for the CEO.

Subject: Q4 Marketing Campaign Update

Hi team,

Social media engagement is up 25% month-over-month due to the new content calendar and paid ad experiments.

Newsletter open rate dropped from 42% to 35%; we'll test new subject lines next week.

The product video campaign is delayed until November, pending legal approval; creative assets are ready.

Please ensure all campaign tracking links are added by Friday.

Best,
Priya
```

**Judge prompt**
```
You are grading two email summaries written for a CEO. Give each summary a score of 1 (pass) or 0 (fail).

1 = pass: concise and faithful to the email. It keeps the key facts (results, problems, deadlines) and adds nothing that is not in the email.
0 = fail: wordy, drops a key fact, or invents one.

Reply in this format:
Version A: [1 or 0], [one-sentence reason]
Version B: [1 or 0], [one-sentence reason]

EMAIL:
[paste the email]

VERSION A:
[paste Version A's output]

VERSION B:
[paste Version B's output]
```

🚦 DECISION (step 4): ask the learner whether they agree with each score, and why.

✅ CHECKPOINT: they have both outputs, both scores with reasons, and their own call on each. Optional: they can paste their results into `01-evaluation-strategy/eval-harness-proof.md`.

---

## Lab 2 · Build Your Evaluation Strategy (about 20 min)

Define what “good” means for Ascend IQ: the promise it makes to users, the three trust metrics that protect it, and the trade-offs you’ll accept.

1. Read Section 1: who Ascend IQ is for, what they use it for, and what’s at stake. (From the Final Project Brief.)
   - **Who it’s for:** VP-level strategists and product leaders at Fortune 500 companies who pay upward of $50,000 a year for verified market intelligence.
   - **What they use it for:** Asking plain-language questions, like “Compare the pricing models of Stripe and Adyen,” and getting answers in seconds instead of digging through the platform.
   - **What’s at stake:** Engagement is dropping, Q4 retention is at risk, and the CPO wants Ascend IQ live for the top 50 enterprise accounts next month. One poor answer to the wrong client can do lasting damage to the relationship.
2. Write your user promise: “For [user], Ascend IQ promises to [outcome] so that [business value].” First decide the outcome Ascend IQ has to deliver: how fast, how accurate, how verifiable.
3. Click three of the five trust metrics, and write one line on why each one protects your promise.
   - **Latency**, Response speed (P95 / P99). Slow kills engagement.
   - **Hallucination Rate**, % of outputs that are confidently false or fabricated.
   - **Fairness**, Quality consistency across user groups, geos, languages.
   - **Robustness**, Coherence on messy, adversarial, out-of-scope inputs.
   - **UX Trust**, Subjective predictability and consistency over time.
4. From the trade-offs between your three metrics, click the two you’re most likely to face with Ascend IQ’s clients. Finish “We prioritize [X] over [Y] because…” for each.
5. Save it to your repo: click **Copy markdown**, open `01-evaluation-strategy/strategy-canvas.md` in your repo, click the pencil icon, paste over the file, and commit. Or click **Download .md** and upload it to the same folder.

🚦 DECISION at steps 2, 3 and 4. In step 4, only offer pairs of the three metrics they chose.

**If you're working with an assistant instead of the Lab Guide,** have it write the file in exactly this shape, then commit it (or paste it into the file on GitHub):

```markdown
# AI Evaluation Strategy Canvas

## 1. Product Strategy, The Context

**Who it's for:** …

**What they use it for:** …

**What's at stake:** …

## 2. Measurements, The Execution

**User promise.** …

**Top 3 trust metrics:**
- **[Metric]**, [definition]

**Why these three:** …

## 3. Strategic Trade-Offs, The Cost

### Trade-off 1 · [Metric A] ↔ [Metric B]
We prioritize … because …

### Trade-off 2 · [Metric C] ↔ [Metric D]
We prioritize … because …
```

✅ CHECKPOINT: the promise names a real user, an outcome, and a business value. There are exactly three metrics, each with a reason tied to the promise, and two trade-offs, each with a "because".

---

## Done-check

- [ ] Lab 1: both outputs scored by a judge from a different family, and the learner's own call on each.
- [ ] Lab 2: `strategy-canvas.md` committed in the shape above, in the learner's own words.

**Next:** Module 2, Build a Failure Taxonomy by Business Impact.
