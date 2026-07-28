# capability-isnt-free

> **STATUS: CONFIRMED on one fixture (k=25); replication pending.** The lead was *changed
> by the data* — see "What the data did to our hypothesis" below. We ran the test able to
> falsify our own claim, and it did.

> **Capability above the task is wasted spend. On mechanical work, a cheap model and a
> frontier model are *equally correct* — but the frontier model costs 3–15× more. Route
> each task to the cheapest tier that clears a deterministic gate; capability you don't
> need is a bill, not a benefit.**

## The result (routing table, k=25 per tier)

An explicit mechanical migration — 12 real call-sites to change, 8 trap sites to leave
alone — run at three tiers, scored by a deterministic oracle (no LLM judge):

| tier | clean-run rate | required / 12 | trap violations | est. cost | cost / *clean* run |
|------|:---:|:---:|:---:|:---:|:---:|
| **Haiku**  | 0.92 | 11.04 | 0.64 | 1× | **1.09** |
| **Sonnet** | 1.00 | 12.0 | 0.00 | 3× | 3.0 |
| **Opus**   | 1.00 | 12.0 | 0.00 | 15× | 15.0 |

Correctness is **statistically tied** (Opus − Haiku clean-rate +0.08, 95% CI [0, 0.20],
p=0.49; Haiku is ~100% through a gate + one cheap retry). Cost is **1× / 3× / 15×**. The
frontier tier buys a **14× bill for the same clean result.** Full method, CIs, and the
honest wrinkles: **[eval/routing-table.md](eval/routing-table.md)**.

## What the data did to our hypothesis (the integrity part)

This repo shipped first as a **pre-registration** of a stronger claim: that an
*over-capable model is measurably **worse*** at mechanical work (non-monotonic
capability). We built the test to expose that effect and ran it at k=25.

**It did not survive.** Opus was flawless — 12/12 migrations, zero trap sites touched,
and it over-reached *less* than the cheaper tiers, not more. So we **retract the
"over-capable is worse" framing.** What the same data cleanly supports is the routing
claim above: not *worse*, but *wasted* — equal correctness, wildly unequal cost.

The ~17/39 figure that motivated the original lead was a **monolith dropping nodes on a
68-edit migration** — a *scale/attention* effect that argues for orchestration, **not** a
model-tier effect (a single Opus call does these edits perfectly). It has been relocated
to the instrument's findings and is no longer this claim's evidence.

## The rule this earns

**Route by verified correctness, not token price — and not by capability either.** Pick
the cheapest tier that clears the deterministic gate on the task class; spend the
frontier premium only where a cheap tier *cannot* clear the gate. On mechanical work, it
can — so don't.

## Depends on

The whole rule rests on the gate being real. "Clears a deterministic gate" only means
something because an LLM judge is theater — the companion, powered result:
**[gate-on-the-fact](https://github.com/NovemberFalls/gate-on-the-fact)**.

## Roadmap

1. **Replicate** on a second independently-authored mechanical fixture (a config-key
   rename) at k=25 — kill the "one fixture" attack.
2. **Add the local tiers** (30B / 27B / gpt-oss on vLLM) — shared with
   [cheapest-hands](https://github.com/NovemberFalls/cheapest-hands); does a *local* model
   also clear the gate, making the cost gap ~∞?
3. **Metered cost + formal retry break-even** — replace the price-ratio estimate with
   per-token accounting (can only widen the gap at tied correctness).
4. Test the **scale/architecture** claim (monolith vs orchestrated on a large migration)
   separately — that is where the ~17/39 actually lives.

## Part of a program

One of three studies under **[deterministic-evals](https://github.com/NovemberFalls/deterministic-evals)**.
Measures **[swarmsmith](https://github.com/NovemberFalls/swarmsmith)** at pinned commit `59d9c2a`.
Charts: **[boord-its.com/skills](https://boord-its.com/skills)**.

## Built by

**November Falls.** MIT.
