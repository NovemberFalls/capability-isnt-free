# capability-isnt-free

> **STATUS: PRE-REGISTERED, DATA PENDING.** The hypothesis and the full measurement
> protocol are frozen below *before* the powered runs. This repo publishes the result
> whichever way it lands — including a clean retraction if the effect fails to replicate.

> **Capability is not monotonic. Handed mechanical work, an *over-capable* model is
> measurably *worse* — and a second review pass does not buy the correctness back. So
> capability isn't free: you pay for it in errors, not just dollars. Route each task to
> the cheapest hands that clear a deterministic gate — and decide *which* hands by
> verified accounting, never by token price.**

## The claim, and why it's falsifiable

Most routing advice is a price list: cheap model for easy work, expensive for hard,
pick by cost. The **motivating observation** — from a *single* run, not yet in the
powered dataset — is that it breaks in **both** directions: a frontier monolith
mis-handled a large share (~17 of 39) of the mechanical find-and-replace nodes on a
trap-dense migration that a cheaper, properly-briefed orchestrated configuration got
right; and the naive inverse ("it's mechanical, route it cheap") fails wherever the
brain hasn't lowered the task to application. **That is one fixture, one run** — its
exact tally is being consolidated from the raw stream (see Roadmap), and replicating it
is precisely what the protocol below pre-registers. It is not published as a lead.

The claim is deliberately killable by two measured numbers:

1. **Retry break-even, per task class.** If (cheap-hands failure-rate × retry-cost)
   exceeds frontier-first cost, routing cheap is *false* for that class.
2. **The interpretation→application floor.** "Any decent model can do it" holds only
   where the spec lowered the task to application. Where it can't, cheap hands fail.
   That boundary is the honest limit, quantified — not hidden.

## Why "data pending" is a feature, not a hedge

The motivating result currently rests on **one fixture, one run**. Promoting it to a
published lead would be exactly the sin this program exists to reject. So the claim
ships here as a **pre-registration**: the matrix, the k, the oracle, and the break-even
formula are frozen below, and the result is appended when the runs complete. A
hypothesis committed before its data is stronger evidence than one reverse-engineered
from it.

## The pre-registered protocol (frozen)

**The crossed routing table** — node class × model lane, each cell run to power.

|            | haiku | sonnet | opus |
|------------|:-----:|:------:|:----:|
| **MUNDANE** (mechanical / diffable) | cell | cell | cell |
| **non-MUNDANE** (generative / judgment) | cell | cell | cell |

Each cell reports four numbers: **success @ tier**, **cheapest tier clearing the bar**,
**Δcost vs frontier-first**, **retry break-even** (the falsifier).

- **Replication (load-bearing):** the MUNDANE-worse effect must appear as a comparable
  *rate* on **two independently-authored** trap-dense fixtures — the existing migration
  plus a second (an API-signature migration with its own hidden oracle). One fixture
  cannot carry the lead.
- **Control:** the non-MUNDANE row must show the *opposite* ordering (capability helps),
  or the word "non-monotonic" is unearned.
- **Counterexample (required):** ≥1 cell where naive token accounting says "route cheap"
  but verified break-even says "don't." This is what makes *verified* accounting a real
  distinction, not a slogan.
- **Power:** pilot at k=3–5 to confirm effect direction (kill-early on the null), then
  k=25 on decisive cells. Bootstrap CIs; Mann–Whitney; a pre-registered dethronement
  trigger carried from the program's prior rounds.
- **Reproducibility of shape:** re-run the matrix on one alternate lineup — the exact
  table decays each model generation; the *procedure* is the citable artifact.

## Supporting evidence already in hand (cited, pinned)

The adjacent, *already-measured* results that make this claim plausible live in the
instrument's white paper, cited at a pinned commit so they can't drift under this claim:

- **Effort is mostly a tax, and the worker floor** — a stronger orchestrator at low/high
  effort held correctness while max effort mostly bought cost; worker lanes hold far
  below their labels on well-specified briefs. [swarmsmith FINDINGS.md §4.3–4.4 @ 59d9c2a](https://github.com/NovemberFalls/swarmsmith/blob/59d9c2a68ff0fb9c63df5b88533acdb37bfde989/FINDINGS.md).
- **The apply-tier — why a deterministic diff removes the worker model from mechanical
  work entirely** — [§4.7](https://github.com/NovemberFalls/swarmsmith/blob/59d9c2a68ff0fb9c63df5b88533acdb37bfde989/FINDINGS.md).

> **Note on the ~17/39 motivating figure:** it is a real single run from the reframe
> work, not yet reconciled into FINDINGS.md. Consolidating its provenance (raw stream →
> FINDINGS) and then replicating it at k is the first roadmap item — the number is
> treated as a hypothesis to test, never as an established result.

## Roadmap

1. **Consolidate the ~17/39 provenance** — recover the exact tally from the raw run
   stream and reconcile it into swarmsmith FINDINGS.md, so the motivating figure is
   citable before it is tested.
2. Build the second MUNDANE fixture (an API-signature migration) with a hidden oracle
   and a pre-registered trap map.
3. Pilot the routing table at k=3–5 (kill-early on the null), then k=25 on decisive cells.
4. Run the counterexample cell and the alt-lineup shape-reproduction.
5. Append results here — whichever way they land.

## Depends on

The verification half of this claim — "route by *verified* accounting" — is only
meaningful because the gate is deterministic. That's the companion study:
**[gate-on-the-fact](https://github.com/NovemberFalls/gate-on-the-fact)**.

## Part of a program

One of three studies under **[deterministic-evals](https://github.com/NovemberFalls/deterministic-evals)**.
Measures **[swarmsmith](https://github.com/NovemberFalls/swarmsmith)** at pinned commit `59d9c2a`.
Charts: **[boord-its.com/skills](https://boord-its.com/skills)**.

## Built by

**November Falls.** MIT.
