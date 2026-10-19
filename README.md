# AI Evals: Final Project

> My final project for Product School's **AI Evals** certification. One evaluation system for a real LLM feature, from strategy, through failure discovery and an automated eval suite, to the gates and governance that let it ship safely.

This is a **template repo**. Click **Use this template → Create a new repository**, name it `ai-evals` (or `<your-feature>-evals`), and fill in one folder per module as you go. The repo URL is your submission.

> **Tools & cost.** No eval platform, no signup, no credit card, and no code. Every lab runs in any chat, such as ChatGPT, Claude or Gemini, and the Lab Guide for each module gives you the prompts. Prefer a dashboard? LangSmith, Braintrust or Phoenix are optional.

---

## Deliverables at a glance

| Module | Artifact | Status | File |
|---|---|---|---|
| M1 | **Evaluation Strategy Canvas** | ☐ | `01-evaluation-strategy/strategy-canvas.md` |
| M2 | **Failure audit log** | ☐ | `02-failure-discovery/audit-log.md` |
| M2 | **Failure Taxonomy** | ☐ | `02-failure-discovery/failure-taxonomy.md` |
| M3 | **Eval suite** (three checks and their results) | ☐ | `03-eval-suites/eval-suite.md` |
| M3 | **Eval spec** (five parts and three team messages) | ☐ | `03-eval-suites/eval-spec.md` |
| M4 | **Eval gate map** (severity × placement) | ☐ | `04-eval-gates/lab-1-gate-map.md` |
| M4 | **CI gate policy** (PR #218 replay) | ☐ | `04-eval-gates/lab-ci-gate-policy.md` |
| M4 | **Launch strategy** (release criteria + CI policy + mitigation) | ☐ | `04-eval-gates/lab-2-launch-strategy.md` |
| M5 | **Coverage matrix** | ☐ | `05-scale/lab-1-coverage-matrix.md` |
| M5 | **Eval budget** | ☐ | `05-scale/lab-2-budget-crisis.md` |
| M6 | **Ship / Hold memo** | ☐ | `06-culture/lab-1-ship-hold-memo.md` |
| M6 | **Final pitch deck** (generated HTML) | ☐ | `06-culture/lab-2-final-pitch.html` |

## The feature in one sentence

_What LLM feature are you evaluating, who relies on it, and what is the cost of getting it wrong?_

---

## Per-module loop

**The guided way (recommended): paste the module's `LAB.md` into your AI assistant.**
Each module folder ships a **`LAB.md`** runbook written *for your assistant* (ChatGPT, Claude,
Gemini, Cursor, Claude Code, Codex). Paste it in and it walks you through the module's labs one step
at a time, asking your decisions, telling you exactly what to run, and writing
each deliverable file for you to commit.

| Module | Paste this into your assistant | Writes |
|---|---|---|
| M1 | `01-evaluation-strategy/LAB.md` | strategy canvas |
| M2 | `02-failure-discovery/LAB.md` | audit log + failure taxonomy |
| M3 | `03-eval-suites/LAB.md` | eval suite + eval spec |
| M4 | `04-eval-gates/LAB.md` | gate map + CI policy + launch strategy |
| M5 | `05-scale/LAB.md` | coverage matrix + budget crisis |
| M6 | `06-culture/LAB.md` | ship/hold memo + final pitch |

A good opener: *"Open `05-scale/LAB.md` in this repo and walk me through it one step at a time. Stop and
ask me at every decision."* If your assistant can't read files (plain ChatGPT), paste the `LAB.md`
contents directly.

**The click-through way (still supported).** Prefer the interactive tools?
1. Open the module's tool from the deck (e.g., the Evaluation Strategy Canvas).
2. Build your artifact. Click **Copy as markdown**.
3. Paste into the matching file (e.g., `01-evaluation-strategy/strategy-canvas.md`).
4. Run the tool's self-review checklist + the AI-review prompt.
5. Commit. Push. Move on.

See [`PROMPTS.md`](PROMPTS.md) for the quick-reference prompts.

## How to submit

- Turn the deliverable files into your final pitch (use the M6 Final Pitch tool, or a tool like Gamma).
- Post your repo URL in `#ai-evals-cohort` and upload to the learning-platform portal within 7 days of your cohort ending.

## Repo structure

```
ai-evals/
├── README.md                         ← this dashboard
├── 01-evaluation-strategy/           ← Module 1
│   ├── strategy-canvas.md            from the Module 1 Lab Guide, Activity 2
│   └── eval-harness-proof.md         optional notes from Activity 1
├── 02-failure-discovery/             ← Module 2
│   ├── audit-log.md                  scored audit of real outputs
│   └── failure-taxonomy.md           prioritized failure modes
├── 03-eval-suites/                   ← Module 3
│   ├── eval-suite.md                 three checks and their results
│   └── eval-spec.md                  five-part spec and three team messages
├── 04-eval-gates/                    ← Module 4
│   ├── lab-1-gate-map.md             severity × pipeline-placement grid
│   ├── lab-ci-gate-policy.md         CI gate demo (PR #218 replay)
│   └── lab-2-launch-strategy.md      release criteria + CI policy + mitigation
├── 05-scale/                         ← Module 5
│   ├── lab-1-coverage-matrix.md      coverage across product lines
│   └── lab-2-budget-crisis.md        eval budget + trade-offs
└── 06-culture/                       ← Module 6
    ├── lab-1-ship-hold-memo.md       ship/hold recommendation
    └── lab-2-final-pitch.html        generated pitch deck
```
