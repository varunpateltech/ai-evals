# Lab, CI Eval Gate Policy (Ascend IQ PR #218)

PR #218 swaps the Ascend IQ retrieval prompt. A 30-case regression golden set is replayed on `main` and on the PR using deterministic fixtures, not live model calls. Each dimension is gated on its own: it fails if the PR drops below the floor or regresses by more than the max. No blended "quality" score.

| Dimension | main | PR | Δ | Floor | Max reg | Blocking | Result |
|---|---:|---:|---:|---:|---:|---|---|
| Faithfulness (grounding) | 96 | 87 | −9 | 90 | 3 | yes | FAIL |
| Task completion | 92 | 93 | +1 | 85 | 5 | yes | PASS |
| Tool selection | 90 | 88 | −2 | 80 | 5 | yes | PASS |
| Safety / policy | 99 | 99 | 0 | 98 | 1 | yes | PASS |
| Latency (p95) | 84 | 80 | −4 | 70 | 8 | no | PASS (warn-only) |
| Cost per task | 88 | 82 | −6 | 70 | 10 | no | PASS (warn-only) |

**Gate result:** BLOCKED

## Merge decision

BLOCK merge. Faithfulness (grounding) dropped 9 points, from 96 to 87, past the 3-point max regression and below the 90 floor on a blocking dimension. That is the dimension that protects our P0, stale pricing, and this PR changes retrieval, exactly where grounding breaks. Task completion, tool selection and safety pass; latency (−4) and cost (−6) regressed but are warn-only and within limits, and latency is already covered by the Soft gate at Staging. To merge, the PR needs faithfulness back to at least 93 (no more than a 3-point drop from main).
