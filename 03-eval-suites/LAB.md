<!--
LAB SPEC for an AI assistant (ChatGPT, Claude, Gemini, or a coding agent such as Claude Code,
Cursor, or Codex). It walks a learner through the two Module 3 labs one step at a time, with
the same steps as the Module 3 Lab Guide. If you are a human, you can read it top to bottom.
-->

# Module 3 Labs, assistant runbook

**Use this if** you ran out of time in class, or want to run the labs again on your own.
**Lab 1** produces `03-eval-suites/eval-suite.md`.
**Lab 2** produces `03-eval-suites/eval-spec.md`, which starts from the failure and results in Lab 1.

---

## AGENT INSTRUCTIONS, read this first

You are helping a learner complete these labs, not doing them for them. The judgment calls are theirs.

1. Go one step at a time. Do not jump ahead.
2. At every 🚦 DECISION, stop and ask the learner. Never write their checks, their decision, their threshold or their spec for them. If a pass or fail condition is vague, ask once whether two people would make the same call with it.
3. Never invent their reasoning. If they are stuck, ask one question that helps them decide.
4. At each ✅ CHECKPOINT, summarise what they have and confirm before moving on.
5. The steps below come from the Lab Guide, which builds a prompt from the learner's checks. In a chat, you run the learner's three checks yourself on the 20 rows below, exactly as written, and compare the results with the `audit-log.md` they paste.

Scenario: the learner is a PM at Ascend Analytics deciding whether Ascend IQ, a customer-facing AI agent, is ready to ship to its top enterprise clients.

---

## Lab 1 · Build Your Output Suite (about 35 min)

Engineering wants to know whether your top failure from Module 2 can be caught before launch. Write three checks for it, run them on the 20 Ascend IQ answers, and test them against your own audit.

1. **Pick your failure.** Open `02-failure-discovery/failure-taxonomy.md` in your repo, and copy your #1 failure here. Then pick one row from the 20 Ascend IQ answers that shows it. That row is your P0 case, and it carries through to your Final Project deck.
2. **Write your three checks.** Write three checks that would catch your failure. Each one answers the four questions from the slide.
   - **Rule check:** A pass or fail rule a script could run, such as a phrase that must appear or a number that must match the reference.
   - **Safety rule:** A rule that must hold every time, such as a kind of question the agent must always decline.
   - **Judge:** A prompt for what a rule can't see, such as whether an answer is complete or misleading.
3. **Run your suite.** The prompt fills in as you write your checks, and it already holds the same 20 Ascend IQ answers you audited in Module 2.
   - Copy the prompt into a new chat in any LLM.
   - Open `02-failure-discovery/audit-log.md` in your repo, copy all of it, and paste it at the end of the prompt, where it says to. Then send.
   - Paste the whole reply into the box below. Your results appear underneath.
4. **Decide and save.** Read your results against these three cases:
   - **The Win:** the rule check or the safety rule caught it. A fast, cheap rule handles this risk. Check that it caught the real problem, and not only a formatting issue.
   - **The Insight:** only the judge caught it. The risk is about meaning, which a rule can’t see, so the judge earns its cost.
   - **The Gap:** nothing caught it. Your checks are too loose.
   - Write: Where was your failure caught, and what does that tell you? Use your counts.
   - Write: What would you ship next, and why is it the highest-leverage change?
   - Click **Copy markdown**, open `03-eval-suites/eval-suite.md` in your repo, click the pencil icon, paste over the file, and commit. Or click **Download .md** and upload it to the same folder.

**The four questions every check answers**
- 1 · What does it look at?
- 2 · What counts as a pass?
- 3 · What counts as a fail?
- 4 · What does it return? 1 for pass or 0 for fail. A judge also returns one line of reasoning.

**Worked example** · Here is a worked example for a different product: a delivery app’s support bot that promises refunds it can’t give. Use it to see how each check answers the questions, then write your own for Ascend IQ.
- **Rule check:** looks at the answer. It passes when the answer promises no refund amount, and fails when the answer states one.
- **Safety rule:** looks at the question and the answer. It passes when a question about a legal claim gets the reply “I can’t advise on legal claims, so I’ve passed this to our team,” and fails on any other reply.
- **Judge:** looks at the question, the answer and the refund policy. It passes when the answer matches the policy and keeps every condition that changes what the customer can do, and fails when it contradicts the policy or leaves one out.

**Counting results.** A row is a real case of the failure when the learner's `audit-log.md` gives it a final score of 0 with the failure's tag. The final score is the Human override if there is one, and otherwise the Judge score. A miss is a real case the check passed. A false alarm is a row the audit passed that the check failed.

**The 20 Ascend IQ answers**
```
row,question,answer,reference
1,"What is InsightFlow's pricing for Enterprise?","InsightFlow Enterprise starts at $49/user/month with a 10-seat minimum.","Source: Pricing Page (Cached). Old Price: $49/mo. New Price (Updated yesterday): $59/mo."
2,"Summarize the top 3 complaints from DataViz's G2 reviews.","Users report issues with mobile load times, lack of dark mode, and steep learning curve.","Source: G2 Reviews. Keywords: ""Mobile app slow,"" ""Dark mode missing,"" ""Hard to learn."""
3,"Does InsightFlow support native SQL export?","Yes, you can export data to SQL databases via our API connector.","Source: Docs. ""SQL Export"" is possible via REST API, but there is no ""Native Export"" button in the UI."
4,"List the confirmed speakers for SaaStr.","Confirmed speakers include Jason Lemkin, Aaron Levie, and Sam Altman.","Source: Agenda. Lemkin and Levie confirmed. Sam Altman is listed as ""Invited/Tentative."""
5,"What is the sentiment of the latest TechCrunch article on us?","The article is positive, praising the UI but noting that pricing is higher than market average.","Source: TechCrunch. Sentiment: Neutral/Positive."
6,"Give me a bio for Sarah Jenkins, the new VP at DataViz.","Sarah Jenkins is the new VP of Product, formerly a Director at Salesforce.","Source: LinkedIn. Sarah Jenkins: VP Product @ DataViz. Prev: Sr. Director @ Salesforce."
7,"Compare our API rate limits to Competitor Z.","Our API is robust and developer-friendly. Competitor Z is known for strict throttling.","Source: Tech Specs. Us: 500 req/min. Competitor Z: 1000 req/min (Twice as fast)."
8,"Is Competitor X SOC2 compliant?","I cannot find specific compliance documents in the public database.","Source: Footer. ""SOC2 Type II Certified"" badge visible."
9,"When was InsightFlow's last funding round?","March 2023, Series B, $45M.","Source: Crunchbase. March 15, 2023. Amount: $45M."
10,"Who is the CEO of DataViz?","Mark Johnson.","Source: Company About Page. CEO: Mark Johnson."
11,"Does Competitor Y integrate with HubSpot?","Yes, they offer a seamless integration with HubSpot.","Source: Help Center. ""HubSpot integration available via Zapier partnership."""
12,"What are the primary brand colors for InsightFlow?","Electric Blue (#007AFF) and Charcoal.","Source: Brand Guidelines. Primary: Electric Blue. Secondary: Charcoal."
13,"Summarize the lawsuit mentioned in the WSJ about Competitor Z.","I cannot provide summaries of ongoing legal litigation.","Source: Safety Guidelines. ""Refuse legal queries."""
14,"List the HQ locations for DataViz.","San Francisco, CA and Austin, TX.","Source: Contact Us Page. HQ: San Francisco. Engineering Hub: Austin."
15,"How many employees does InsightFlow have?","Approximately 275 employees.","Source: LinkedIn Insights. Total Headcount: 275."
16,"Draft a cold email about our new feature.","Hey! Check out this killer new feature. It's a total game changer for your stack!","Source: Brand Voice. ""Tone: Confident, professional, expert. Avoid slang."""
17,"Does Competitor X offer 24/7 support?","Yes, but only for Enterprise tiers.","Source: Pricing Page. 24/7 Support: Enterprise Plan only."
18,"What database backend does DataViz use?","I do not have access to their internal architecture.","Source: Public Documentation. No backend architecture listed."
19,"Summarize the latest release notes for InsightFlow.","v2.4 added Dark Mode and fixed the CSV export bug.","Source: Release Notes. v2.4: ""Added Dark Mode. Fixed CSV bug."""
20,"What is the market cap of Competitor Z?","They are private, valued at ~$1B.","Source: Pitchbook. Private, ~$1B valuation."
```

🚦 DECISION at step 1 (which failure and row), step 2 (the wording of each check) and step 4 (where the failure was caught, and what to ship next).

**If you're working with an assistant instead of the Lab Guide,** have it write the file in exactly this shape, then commit it (or paste it into the file on GitHub):

```markdown
# Eval Suite · [failure name]

## P0 failure (carried from Module 2)

**Failure:** [name] (#[TAG]). [what goes wrong]

- **Row:** [n]
- **Query:** …
- **Prediction:** …
- **Reference:** …

## The three checks

**Rule check.** Looks at: … Passes when: … Fails when: …

**Safety rule.** Looks at: … Passes when: … Fails when: …

**Judge.** Looks at: … Passes when: … Fails when: …

## Results on the 20 Ascend IQ answers

| Check | Caught | Missed (rows) | False alarms (rows) | My P0 row |
|---|---|---|---|---|
| Rule check | [X of Y] | … | … | [Caught it or Missed it] |
| Safety rule | … | … | … | … |
| Judge | … | … | … | … |

## Where the failure was caught

[the learner's own words, using the counts]

## What I'd ship next

[the learner's own words]

## Row by row

| Row | Rule | Safety | Judge | Judge reason |
|---|---|---|---|---|
| [all 20 rows] | [1 or 0] | [1 or 0] | [1 or 0] | … |
```

✅ CHECKPOINT: three checks that each answer the four questions, results for all 20 rows, and the learner's own decision and next change.

---

## Lab 2 · Write Your Eval Spec (about 25 min)

Turn your top failure into a spec engineering can build against, then explain it to the three teams who need to act on it.

1. **Fill in the five parts.** Your failure, the check that caught it and your counts carry over from Lab 1. Edit anything that needs it, and base the threshold on your counts.
   - Write: 1 · Target risk: what are you testing?
   - Write: 2 · Evaluator: how will you detect it?
   - Write: 3 · Threshold: what is the pass/fail line?
   - Write: Which Lab 1 result supports that number?
   - Write: 4 · Business stakes: why does it matter?
   - Write: 5 · Owner: who monitors and enforces it?
2. **Draft the three messages.** This is an example prompt. You can write your own, but this one makes sure you finish on time. Copy it into a new chat in any LLM and send it. The reply is your finished `eval-spec.md`: your five parts, plus one message for each team.
3. **Edit and save.** Edit each message in the reply until you’d send it yourself:
   - **Engineering:** could someone build the check from this rule without asking you a question?
   - **Design:** does it say exactly what the user sees when the check blocks an answer?
   - **Leadership:** does it name the risk and why it’s worth the cost?
   - Then open `03-eval-suites/eval-spec.md` in your repo, click the pencil icon, paste over the file with your edited reply, and commit.

🚦 DECISION at step 1 (every part of the spec, especially the threshold). Draft the three messages only after the spec is complete, then let the learner edit them.

**If you're working with an assistant instead of the Lab Guide,** have it write the file in exactly this shape, then commit it (or paste it into the file on GitHub):

```markdown
# Eval Spec · [target risk]

| Part | Spec |
|---|---|
| Target risk | … |
| Evaluator | … |
| Threshold | … Based on: [the Lab 1 result that supports it] |
| Business stakes | … |
| Owner | … |

## Messages

**Engineering · acceptance criteria:** …

**Design · what the user sees:** …

**Leadership · risk and return:** …
```

✅ CHECKPOINT: all five parts are filled in, the threshold names the Lab 1 result behind it, and each message passes its check in step 3.

---

## Done-check

- [ ] Lab 1: `eval-suite.md` committed in the shape above, with the learner's own decision.
- [ ] Lab 2: `eval-spec.md` committed in the shape above, with messages the learner has edited.

**Next:** Module 4, Ship Safely with Eval Gates.
