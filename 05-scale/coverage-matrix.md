# Module 5 · Coverage Matrix · Competitor Signal Tracker

## Coverage Row

| Product | Hallucination Rate | Fairness | Latency | UX Trust | Robustness |
|---|---|---|---|---|---|
| Competitor Signal Tracker | ❌ Gap | ❌ Gap | ✅ Covered | ✅ Covered | ❌ Gap |

## What Runs Today

- A timer alerts if the nightly scoring run takes more than 2 hours.
- A style check flags summaries written in a casual or alarmist tone before they reach the sales team.

## Accepted Gap

**Fairness.** It's an internal tool: the sales and strategy teams read every score before acting, and nothing goes to clients directly, so uneven quality across competitors is caught by human judgment and costs us less than unchecked hallucination does.

We’ll look again: We run a baseline fairness review (comparing score quality across our top 10 competitors) before the tracker covers non-English sources or new regions, or within two weeks if sales reports that any competitor is consistently over- or under-scored. Otherwise we review it at the Q1 2027 eval budget planning.

## Critical Gap

We've flagged Hallucination Rate as the most critical gap for Competitor Signal Tracker because a made-up or misread competitor signal goes straight into sales pitches and strategy decisions with nothing checking it. The sales team would notice first, usually when a client or prospect corrects a claim we repeated, and the cost is lost deals, damaged credibility and strategy built on false signals. To close it, we'll add a new eval gate to the nightly run by November 30, 2026, owned by the Signal Tracker eng lead. On every signal, a rule check verifies that the source exists and that every quoted phrase and number actually appears in it, and holds back any failure from the sales feed. On a sample of 50 summaries a night, spread across competitors, sources and claim types, an LLM judge checks that the summary means what the source says; we first validate the judge against 100 human-labelled summaries. The PM pauses the feed if more than 5% of the week's ~350 judged summaries fail.

## After the Pressure Test

Changed: added a baseline fairness review before expanding sources; the rule check now explicitly verifies quoted text and numbers on every signal, not just that a source URL exists; the judge sample is stratified and validated against 100 human-labelled summaries first; the 5% threshold is now measured weekly across ~350 judged summaries instead of per night. Kept: Fairness as the accepted gap, because humans review every score internally, and Hallucination Rate as the critical gap.
