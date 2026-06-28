# A Minimal Simulation Spec for CART

> This is a starting point for testing the [Correlation-Anchor Relativity Theory](PAPER.md) in code. It is deliberately small. The goal is not to reproduce our universe — it is to see whether *stable, law-like structure and self-consistent coordinate systems emerge on their own* from a system that was never told any laws.

## The core claim being tested

> A system can infer its own "laws" by continuously identifying the most stable correlations over time, without assuming them a priori.

If that's true, a lawless relational system left to evolve should spontaneously develop:

1. **Anchors** — correlations that stay stable while everything else churns.
2. **Effective coordinates** — a low-dimensional description that those anchors imply.
3. **Regime changes** — occasional reorganizations where one stable set of "laws" gives way to another.

## Minimal ingredients

| Component | Minimal choice |
|---|---|
| **Substrate** | `N` nodes, each holding a small state vector. |
| **Interactions** | Local update rules with *random, drifting* coupling strengths. No conserved quantities imposed. |
| **Observables** | Functions of node states (sums, products, pairwise differences). |
| **Correlation tracker** | Rolling mutual information (or correlation) between every observable pair. |
| **Stability functional `S`** | Inverse variance of each correlation over a sliding time window. |
| **Anchor set** | Top-k edges by `S` — the current "laws." |

## The loop

```
initialize N nodes with random states and random, slowly-drifting couplings
for each timestep t:
    1. update node states via local interactions
    2. measure all observables
    3. update rolling correlations C(O)
    4. score stability S(C) over the sliding window
    5. anchors[t] = top-k edges by S          # promote
    6. drop edges whose S has decayed          # demote
    7. log: which anchors persist, for how long, and when they reorganize
```

## What to measure

- **Anchor lifetime distribution.** Are some correlations dramatically more stable than the rest? (If everything is equally unstable, there are no "laws.")
- **Effective dimensionality.** Run PCA / manifold estimation on the anchored observables. Does a low, stable dimensionality emerge — and can the *same* dynamics be described by more than one coordinate set? (Tests Dimensional Relativity.)
- **Universality.** Swap the micro-dynamics (different interaction rules) but keep the structure. Do the *same* macro-anchors reappear? (Tests redundancy / reconstructability.)
- **Regime transitions.** Plot anchor membership over time. Look for phase-transition-like reorganizations where the stable set abruptly changes.

## Success / failure criteria

- ✅ **Supportive:** stable anchors emerge, imply a low-D coordinate system, survive changes of micro-dynamics, and occasionally reorganize.
- ❌ **Falsifying:** no correlation is meaningfully more stable than chance; "anchors" are just noise; no consistent coordinate description exists.

A negative result is genuinely interesting here — it would say that lawful structure does *not* come for free from correlation-stability alone, and that something more is required.

## Layer 2 — the space of laws (and walking it backward)

Layer 1 (above) produces **anchors** — candidate laws. The richer test treats those anchors as *objects in their own relational space* (see [`PAPER.md`](PAPER.md) §4).

**Forward (bottom-up):**
1. Take the anchors as **nodes**.
2. Draw edges between them: **derivation** (does fixing A let you predict B?), **co-stability** (correlate the anchors' stability time-series), **exclusion** (do A and B never co-occur as anchors?).
3. **Embed** that anchor-relationship graph (MDS / spectral / any knowledge-graph embedding).
4. Measure: emergent **clusters** (= regimes / effective theories), **cluster swaps** over time (= phase transitions / evolving laws), and whether **distance is non-unique** under different privileged relations (= Dimensional Relativity).

**Backward — the "cheat", and the more tractable test:**
Instead of hoping physics emerges from noise, **seed the space with known laws** as labeled anchors and *invert*: fit the generator (the "rules that make the rules") that reproduces their known relationships — e.g. *energy ↔ time-translation symmetry*, *Newtonian gravity as a limit of GR*.
- **Success criterion:** the recovered generator correctly predicts a **held-out** law's position and relationships (train/test split over known physics — and watch for leakage, the classic trap).
- **Payoff:** the emergent coordinate system — hence the effective **dimensionality** — is *read off the fitted generator* rather than assumed. That is the concrete meaning of "better dimensional awareness": the real degrees of freedom are discovered, not posited.

This backward pass is the cleaner experiment of the two — unlike the forward toy, it has a labeled answer key.

## Honest caveats

- "Mutual-information edges in a graph" is one operationalization of *anchor*; it may not be the right one. Part of the experiment is finding a stability functional that produces non-trivial anchors.
- Emergent low-dimensionality in a toy model would be suggestive, not proof that real spacetime works this way.
- This tests the *mechanism* (can laws/coordinates self-organize?), not the *claim about our universe* (do they?). Those are different bars.

## Contributing

If you build this — even a 200-line toy — open a PR or an issue with a link. Negative results welcome and explicitly wanted.
