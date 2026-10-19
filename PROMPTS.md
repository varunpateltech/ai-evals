# Prompt pack, what to say to your AI assistant

> **Prefer the guided path?** Each module folder has a **`LAB.md`** runbook. Paste it into
> your assistant (*"walk me through `03-eval-suites/LAB.md` one step at a time"*) and it runs
> the whole module for you, asking your decisions, telling you exactly what to run,
> and writing each deliverable file. This prompt pack is the
> **quick-reference / fallback**: the same prompts, if you'd rather drive each step by hand.

You build your eval system by **directing an AI assistant** (ChatGPT, Claude, Gemini, or a coding agent
like Cursor / Claude Code / Codex). You describe your product and your judgement calls in plain English;
the assistant drafts the artifacts and, if it can edit files in your fork, writes and commits them for
you. The eval *runs* (scoring rows against your checks) happen in the same chat, using the prompts in
each module's Lab Guide. There's no code to write. A dashboard (LangSmith / Braintrust / Phoenix) is optional.

Two habits that make this work:
- **Own the judgement calls.** The trust metrics, the definition of "good", the severity ratings, the
  ship/hold call, these are yours. The assistant drafts; you decide.
- **Paste real numbers back.** After each eval run, paste the results in so the assistant writes the
  artifact from *your* data, not a guess.

---

## Setup (once)

> I'm taking Product School's AI Evals course. Open my forked `ai-evals` repo. Confirm the folder
> structure (`01-evaluation-strategy` … `06-culture`) and that each module folder has a `LAB.md`.

---

## M1, Evaluation strategy + first eval

> Walk me through `01-evaluation-strategy/LAB.md`. Run Lab 1 with me: compare Version A and Version B
> with a judge from a *different* model family. Then help me write my user promise, pick 3 trust metrics
> tied to it, and choose the two trade-offs between them. Write `strategy-canvas.md` as we go.

## M2, Failure audit + taxonomy

> Walk me through `02-failure-discovery/LAB.md`. In Lab 1, I'll flag two rows, send the judge prompt to a
> model and paste its reply back, then tell you which calls I disagree with and why. In Lab 2, help me pick
> my top three failures and set each priority with the matrix. Write `audit-log.md` and `failure-taxonomy.md`.

## M3, Eval suites

> Walk me through `03-eval-suites/LAB.md` using my #1 failure from M2. In Lab 1, push back if my checks
> are vague, run them on the 20 answers, and compare the results with my `audit-log.md`. I'll decide where
> the failure was caught. In Lab 2, help me write the five-part eval spec with a threshold my Lab 1 counts
> support, then draft the three team messages for me to edit. Write `eval-suite.md` and `eval-spec.md`.

## M4, Eval gates

> Walk me through `04-eval-gates/LAB.md`. Help me place each failure on severity × pipeline stage (≥1
> Hard/Soft/Advisory), set per-dimension floors + max-regression for the PR #218 replay, make the merge
> call, and write the release criteria. Keep CI policy per-dimension, never one blended number.

## M5, Scale

> Walk me through `05-scale/LAB.md`. Force at least 2 ❌ gaps in my coverage matrix, and hold me to the
> $200K cap with max 3 Level-3 slots in the budget grid. Write `lab-1-coverage-matrix.md` and
> `lab-2-budget-crisis.md` with a defensible fallback for every non-L3 item.

## M6, Culture (capstone)

> Walk me through `06-culture/LAB.md`. Help me write the Ship/Hold memo with the recommendation in the
> first sentence and real numbers from M2–M5, then assemble the final pitch deck from my repo. Be honest
> about any gate that isn't met.

---

## Handy follow-ups (any module)

- *"Show me what you changed and why."*
- *"That metric is too generic, tie it to my user promise."*
- *"Give me 2–3 options and a recommendation, then let me choose."*
- *"Now commit the file with a clear message."*
