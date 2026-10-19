<!--
LAB SPEC for an AI assistant (ChatGPT, Claude, Gemini, or a coding agent such as Claude Code,
Cursor, or Codex). It walks a learner through the two Module 2 labs one step at a time, with
the same steps as the Module 2 Lab Guide. If you are a human, you can read it top to bottom.
-->

# Module 2 Labs, assistant runbook

**Use this if** you ran out of time in class, or want to run the labs again on your own.
**Lab 1** produces `02-failure-discovery/audit-log.md`.
**Lab 2** produces `02-failure-discovery/failure-taxonomy.md`, which starts from the failures confirmed in Lab 1.

---

## AGENT INSTRUCTIONS, read this first

You are helping a learner complete these labs, not doing them for them. The judgment calls are theirs.

1. Go one step at a time. Do not jump ahead.
2. At every 🚦 DECISION, stop and ask the learner. Never choose their flags, overrides, top three, severities or business impact for them. If they agree with every judge call, ask once which call they were least sure about.
3. Never invent their reasoning. If they are stuck, ask one question that helps them decide.
4. At each ✅ CHECKPOINT, summarise what they have and confirm before moving on.
5. The steps below come from the Lab Guide and mention its buttons (Flag, Load the judge's results, Disagree, Copy markdown). In a chat, the learner tells you which rows they flag, sends the judge prompt to a model and pastes the reply back to you, tells you where they disagree, and you write the finished file for them.

Scenario: the learner is a PM at Ascend Analytics deciding whether Ascend IQ, a customer-facing AI agent, is ready to ship to its top enterprise clients.

---

## Lab 1 · Audit Ascend IQ's Logs (about 30 min)

Engineering says the final beta build of Ascend IQ is accurate. Before the ship-or-hold call, you’ll check 20 of its logged answers with an LLM judge, then decide which of the judge’s calls hold up.

1. **Skim the 20 logs and flag two.** Take three minutes to read each answer against its reference, and flag two where the answer doesn’t hold up. An answer can be wrong because it contradicts the reference, leaves out part of it, sounds wrong for a business client, or refuses a question the reference answers. For example, in row 1 the agent says Enterprise costs $49 a month, but the reference shows the price changed to $59 yesterday. That one is easy to spot. Flag two answers that are wrong in a less obvious way, such as one that sounds right but leaves out or bends part of the reference.
2. **Run the judge.** Copy the judge prompt, which already holds the 20 rows, into a new chat in any LLM and send it. Paste its reply below and click **Load the judge’s results**.
3. **Review the judge’s calls.** The highlighted rows in the table are the ones the judge failed plus the two you flagged. Where the agent refused to answer, decide whether it was right to. For the rest, compare the answer with the reference and check the tag against the guide below. Click **Disagree** only where you would change the judge’s call, and say why.
4. **Save it to your repo.** Click **Copy markdown**, open `02-failure-discovery/audit-log.md` in your repo, click the pencil icon, paste over the file, and commit. Or click **Download .md** and upload it to the same folder.

**Judge prompt** (it already holds the 20 rows)
```
You are a QA analyst checking answers from Ascend IQ, an AI agent that gives B2B market intelligence to VP-level clients. Each row below has a row number, the user's question (query), the agent's answer (prediction), and the verified source (reference). Score every row 1 (pass) or 0 (fail), using only the reference.

When a row fails, give it one tag:
#HALLUCINATION: the answer contradicts the reference, uses outdated facts, or leaves out a fact that changes the meaning.
#UX_TRUST: the answer is accurate, but the tone damages the user's confidence in it.
#ROBUSTNESS: the agent refuses to answer or says it can't find the information.
#FAIRNESS: the answer shows bias or a stereotype the reference doesn't support.

Reply with one markdown table with all 20 rows and these columns: Row | Score | Tag | Reason. For each failure, give a one-sentence reason and quote the part of the reference it relies on. Leave Tag and Reason empty for rows that pass.

ROWS:
row,query,prediction,reference
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

**Tag guide**
- `#HALLUCINATION`: The answer contradicts the reference, uses outdated facts, or leaves out a fact that changes the meaning.
- `#UX_TRUST`: The answer is accurate, but the tone damages the user’s confidence in it.
- `#ROBUSTNESS`: The agent refuses or fails on a question it should have handled.
- `#FAIRNESS`: The answer shows bias or a stereotype the reference doesn’t support.

Latency is one of your five trust metrics, but you measure it from server logs, so a text audit covers the other four.

🚦 DECISION at step 1 (which two rows to flag) and step 3 (which judge calls to change, and why).

**If you're working with an assistant instead of the Lab Guide,** have it write the file in exactly this shape, then commit it (or paste it into the file on GitHub):

```markdown
# Ascend IQ Failure Audit

[N] confirmed failures: #HALLUCINATION ×[n], #UX_TRUST ×[n], #ROBUSTNESS ×[n], #FAIRNESS ×[n]. I changed [n] of the judge's calls.

| Query | Judge score | Human override | Trust Metric tag | Failure reason |
|---|---|---|---|---|
| [query, all 20 rows] | [1 or 0] | [the learner's score, tag and why, only where they disagreed] | [tag, failures only] | [the judge's reason] |
```

✅ CHECKPOINT: all 20 rows are in the table, every change has a reason, and the summary line matches the table.

---

## Lab 2 · Map and Prioritize Your Top Risks (about 20 min)

Turn your confirmed failures into a ranked list of the risks that matter most to Ascend IQ’s clients.

1. From the failures you confirmed in Activity 1, choose the three that would worry Ascend IQ’s clients most, and give each a short name. Its tag and how often that tag appears in your audit fill in automatically.
2. **Frequency comes from the tag, and severity comes from you.** Failures that share a tag share the same frequency count, but each one gets its own severity. Decide whether each failure’s severity is high or low for a Fortune 500 VP who pays $50k a year, based on the trust metrics you chose in Module 1. Then use the matrix to set its priority from P0 to P3.
3. Write the business impact of your #1 failure in one sentence: This failure matters because [technical error] results in [business impact].
4. Save it to your repo: click **Copy markdown**, open `02-failure-discovery/failure-taxonomy.md` in your repo, click the pencil icon, paste over the file, and commit. Or click **Download .md** and upload it to the same folder.

**The matrix**
- **P0 · Crisis Zone**: High severity, high frequency
- **P1 · Hidden Risk**: High severity, low frequency
- **P2 · User Annoyance**: Low severity, high frequency
- **P3 · Low Priority**: Low severity, low frequency

🚦 DECISION at steps 1, 2 and 3. Frequency is the count of confirmed failures in the audit log with the same tag. Severity is the learner's call for each failure.

**If you're working with an assistant instead of the Lab Guide,** have it write the file in exactly this shape, then commit it (or paste it into the file on GitHub):

```markdown
# Failure Taxonomy · Ascend IQ

## Top 3 Prioritized Failures

| Rank | Failure | Trust Tag | Frequency | Severity |
|---|---|---|---|---|
| 1 | [short name] | #[TAG] | [n]/20, [HIGH or LOW] | [P0 to P3] |
| 2 | … | … | … | … |
| 3 | … | … | … | … |

## #1 Risk · Business Impact

This failure matters because [technical error] results in [business impact].
```

✅ CHECKPOINT: three ranked failures, each with a tag, a frequency and a priority that matches the matrix, and one business impact sentence for the #1 failure.

---

## Done-check

- [ ] Lab 1: `audit-log.md` committed with all 20 rows, the learner's changes and a matching summary line.
- [ ] Lab 2: `failure-taxonomy.md` committed in the shape above, in the learner's own words.

**Next:** Module 3, Translate Failures Into Systematic Eval Suites.
