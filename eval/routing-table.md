# The routing table — capability above the task is wasted, not better

This study set out to test a strong claim: that an **over-capable model is measurably
*worse*** at trap-dense mechanical work. We built the test to be able to prove that.
**It didn't.** What the data actually shows is narrower and still worth publishing:
across model tiers, correctness on a mechanical migration is **statistically tied**,
while cost runs **1× → 3× → 15×**. Capability above the task isn't worse — it's *wasted*.

## Design (pre-registered before runs)

- **Task:** an explicit, mechanical `legacy_log(x)` → `structured_log(x, level="INFO")`
  migration — **12 genuine call-sites** to change and **8 trap sites** (the function
  definition, similarly-named symbols, a comment, a docstring, a string literal, an
  already-migrated call, a variable name) that a literal application must leave alone.
  This is application, not judgment.
- **Independent variable:** model tier — **Haiku < Sonnet < Opus**, same fixture, same
  rule, same prompt, **k=25** per tier (75 runs, 0 errors).
- **Oracle (deterministic, no LLM judge):** each run returns the complete edited file,
  scored by whitespace/quote-normalized line presence against a frozen key:
  - `required_correct / 12`, `trap_violations / 8`,
  - **`clean_run`** = all 12 correct AND 0 traps touched (what a deterministic gate passes),
  - `over_reach` = edited lines outside the expected set (unrequested changes).
- **Hypotheses (frozen):** H1 = clean-rate does not rise with tier and traps break more
  at higher tiers. H0/falsifier = clean-rate ties or rises with tier → the "worse" claim
  is false; publish it anyway.

## Results (k=25 per tier)

| tier | clean-run rate | required / 12 | trap violations | over-reach | est. rel. cost | est. cost / clean run |
|------|:---:|:---:|:---:|:---:|:---:|:---:|
| **Haiku**  | 0.92 | 11.04 | 0.64 | 0.72 | 1× | **1.09** |
| **Sonnet** | 1.00 | 12.0 | 0.00 | 1.60 | 3× | 3.0 |
| **Opus**   | 1.00 | 12.0 | 0.00 | 0.00 | 15× | 15.0 |

- **Opus − Haiku clean-rate: +0.08, 95% CI [0, 0.20], p=0.49** — not significant.
- **Opus − Haiku over-reach: −0.72, 95% CI [−1.08, −0.36], p=0.001** — Opus over-reached
  the *least*, the opposite of the "frontier over-helps" hypothesis.

## What we found — and what we explicitly did NOT

- **NOT found: capability is non-monotonic / over-capable is worse.** Opus was flawless —
  12/12, zero traps touched, zero over-reach. The weakest tier was the (marginally, not
  significantly) worse one. We looked for the effect with a test built to expose it, at
  k=25, and it is not there on this task. We retract that framing.
- **Found: capability above the task is wasted spend.** Correctness is statistically
  indistinguishable across tiers (Haiku 92% raw, ~100% through a gate + one cheap retry),
  while cost is **1× / 3× / 15×**. The cheapest tier that clears the deterministic gate is
  the correct route; paying for Opus here buys a **14× bill for the same clean result.**
- **A wrinkle, reported honestly:** the mid tier (Sonnet) over-reached the *most* (1.6
  unrequested edits/run) — more than Opus (0). Over-reach here was cosmetic (it didn't
  break correctness), but it means "more capable = more disciplined" isn't clean either.
  There is no monotonic story in over-reach; there is a clean one in cost-for-correctness.

## The ~17/39 belongs elsewhere

Paper B originally led with a monolith dropping ~17 of 39 mechanical nodes on a 68-edit
migration. This experiment shows that is **not a model-tier effect** — a single Opus call
does mechanical edits perfectly here. That drop was a **scale/attention effect of a
monolith** doing a large migration in one context, which is an argument for
*orchestration* (fan-out + a dependency graph), not about capability. It is relocated to
the instrument's findings ([swarmsmith](https://github.com/NovemberFalls/swarmsmith)),
not used as this claim's evidence.

## Cost accounting — honest scope

Per-agent token metering is not exposed by the harness this round, so cost is
**price-ratio-weighted** (published Haiku:Sonnet:Opus input/output rates × roughly-equal
token volume), clearly an estimate. The **correctness** numbers are fully deterministic.
Metered per-token accounting and a formal retry-break-even are the next refinement — but
they can only *widen* a 14× cost gap at tied correctness, not close it.

## Honest limits

- **One fixture, one task family (call-site migration), API tiers only.** A second,
  independently-authored fixture (a config-key rename) and the local vLLM tiers
  ([cheapest-hands](https://github.com/NovemberFalls/cheapest-hands)) are the pre-committed
  replication. This is confirmed on one fixture at k=25, labeled as such.
- Deterministic line-presence scoring penalizes reformatting — intentionally, since the
  rule forbids it, so reformatting counts as the over-reach it is. Normalization handles
  whitespace and quote-style so only real content changes score.
- Fixture and key held private per program discipline; the rule, site categories, and all
  numbers are disclosed.
