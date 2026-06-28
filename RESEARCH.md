# CART in context: related work, novelty, and open problems

> **Why this file exists.** A "theory of everything" posted with no awareness of existing physics gets dismissed on sight. This document does the opposite: it shows that *every individual intuition behind CART already has a serious research lineage* — which is good news (the intuitions are in respectable company) — and then isolates what, if anything, is actually distinctive about the synthesis. It also lists the strongest objections honestly, because a thought experiment that hides its weak points isn't worth testing.
>
> **Bottom line up front:** CART is not new in its parts. It *is* an unusual combination of parts. The closest single thinker is **Lee Smolin** (evolving laws); the closest mechanism is **Wolfram / "it-from-qubit"** (dimension as emergent, not fundamental); the closest *method* for actually testing it is **Schmidt & Lipson**-style law-discovery from data. CART's one-line contribution is to put **evolving laws and emergent dimension under a single mechanism** — correlation-stability — and frame it as a *runnable inference loop*.

---

## 1. Where each CART claim already lives in the literature

| CART claim | Closest established work | One-line relationship |
|---|---|---|
| Laws **evolve** over time; they are not timeless | Lee Smolin, *Time Reborn*; cosmological natural selection | Smolin argues exactly this. CART's "laws drift" is Smolin's thesis, restated at the level of correlations. |
| Laws are **emergent / statistical**, not fundamental | Verlinde, entropic gravity; thermodynamic gravity (Jacobson) | Gravity-as-an-entropic-force is a worked example of "a law is a stable statistical tendency, not a primitive." |
| **Dimensions are emergent**, can be fractional, can vary | Wolfram Physics Project (hypergraph) | Wolfram: dimension "must emerge from the large-scale structure," can be non-integer, can vary with position/time. This is CART's Dimensional Relativity, already formalized. |
| **Geometry emerges from correlation** | "It from qubit" / holography / tensor networks | Spacetime geometry emerges from *patterns of entanglement* — and entanglement is a correlation. This is the strongest existing support for "dimensions from correlation structure." |
| Reality is **relational**; relations are primary, not the stage | Rovelli, Relational Quantum Mechanics; loop quantum gravity; causal sets | "Only relations have meaning; there is no background container." CART's relational substrate is this ontology. |
| A law = the **most compressed** stable description of observations | Minimum Description Length / Kolmogorov / Occam | "Best hypothesis = largest compression of the data." CART's "physics is a self-updating compression" is MDL applied to physics. |
| A system can **infer its own invariants** from raw data | Schmidt & Lipson (*Science*, 2009), Eureqa; AI Feynman; ML-discovered invariants | This is CART's *simulation*, already demonstrated for fixed laws. The open question CART adds: can it work when the laws themselves drift? |

---

## 2. The lineage, in a little more detail

### 2.1 Evolving laws — Lee Smolin
Smolin is the headline precedent. In *Time Reborn* (2013) and earlier in *The Life of the Cosmos* (1997), he argues that the laws of physics are **not** fixed and timeless but have **evolved**, via "cosmological natural selection" (universes reproduce through black holes, with slightly varied constants). CART shares Smolin's core move — *laws are products of a process, not eternal axioms* — but locates the variation in **correlation-stability over observation**, not in a multiverse of black-hole births.
- Smolin, *Time Reborn* — https://www.goodreads.com/book/show/15816556-time-reborn
- "The laws of the universe are changing" (IAI) — https://iai.tv/articles/lee-smolin-the-laws-of-the-universe-change-auid-2174

### 2.2 Laws as emergent statistics — Verlinde, Jacobson
Erik Verlinde (2011) derived Newton's gravity as an **entropic force** — gravity "is not a fundamental interaction but an emergent phenomenon arising from the statistical behavior of microscopic degrees of freedom." This is a concrete, worked instance of CART's Anchor Principle: a "law" as a stable statistical tendency. (Note the honest caveat: entropic gravity has been **challenged empirically**, e.g. dwarf-galaxy rotation, and is hard to distinguish from Newton/GR — a cautionary tale for CART too.)
- Entropic gravity (Wikipedia) — https://en.wikipedia.org/wiki/Entropic_gravity

### 2.3 Emergent dimension — Wolfram, and holography
The **Wolfram Physics Project** is the cleanest existing version of CART's Dimensional Relativity: space is "an emergent large-scale feature of the hypergraph," dimension "has no intrinsic value," can be **non-integer**, and can **vary with position and time** — with the universe possibly starting "essentially infinite-dimensional" and "cooling" to ~3D. Independently, the **"it-from-qubit"** program shows spacetime geometry emerging from **entanglement patterns** — correlation literally building dimension. CART's claim that dimensions are derived indices over correlation structure is, in these programs, a research reality rather than a speculation.
- The Structure of Space (Wolfram) — https://www.wolframphysics.org/technical-introduction/potential-relation-to-physics/the-structure-of-space/
- Emergent Holographic Spacetime from Quantum Information (PRL, 2025) — https://arxiv.org/abs/2506.06595

### 2.4 Relational ontology — Rovelli, causal sets
CART's "underlying relational structure" is the ontology of **Relational Quantum Mechanics** (Rovelli): state is always relative to another system; only relations carry meaning; in loop quantum gravity there is no background spacetime "container" — the relations reproduce its features. This is the philosophical backbone CART is leaning on.
- Relational QM (Stanford Encyclopedia) — https://plato.stanford.edu/entries/qm-relational/

### 2.5 Laws as compression — MDL / Kolmogorov
CART's "physics is a self-updating compression" is the **Minimum Description Length** principle (a formalization of Occam's razor): the best model is the one that most compresses the data; "any regularity useful for prediction is useful for compression, and vice versa." CART = MDL where the model is allowed to keep changing as the data stream evolves.
- MDL overview — http://www.modelselection.org/mdl/
- Tegmark et al., *Intelligence, physics and information* — https://arxiv.org/pdf/2001.03780

### 2.6 Inferring invariants from data — Schmidt & Lipson (the testable core)
This is the most important entry for anyone who wants to actually *run* CART. Schmidt & Lipson (*Science*, 2009) built a system (later **Eureqa**) that **distilled conservation laws, Hamiltonians and Lagrangians from raw motion data**, by searching for **invariants** rather than predictive models — "all laws of nature are essentially laws of conservation and symmetry." This is CART's simulation, *already working for fixed laws*. Two things CART must confront:
1. **The honest caveat (Hillar & Sommer, 2012):** the method implicitly *baked in* Hamilton's equations / Newton's 2nd law via how it structured its search. **Lesson for CART:** "we imposed no laws" is the hardest claim to actually honor — check what your correlation tracker quietly assumes.
2. **The new question CART adds:** Schmidt–Lipson assumed the invariant is *fixed*. CART's distinctive test is whether such a system can track an invariant that **drifts** — promoting/demoting anchors as the underlying balance changes.
- Distilling Free-Form Natural Laws (Science 2009) — https://pubmed.ncbi.nlm.nih.gov/19342586/
- Discovering invariants via machine learning (Phys. Rev. Research, 2021) — https://journals.aps.org/prresearch/abstract/10.1103/PhysRevResearch.3.L042035

---

## 3. So what (if anything) is actually new?

Honestly: **not the ingredients.** What's distinctive is the **specific synthesis**:

1. **One mechanism for two emergences.** Smolin gives evolving *laws*; Wolfram/holography give emergent *dimension*. CART proposes that **both** fall out of the *same* process — ranking correlations by stability — rather than treating them as separate stories.
2. **Drift as a first-class feature, not a bug.** Most law-discovery work (Schmidt–Lipson, AI Feynman) assumes a *fixed* target. CART's defining commitment is that the anchors are allowed — expected — to **reorganize over time**.
3. **A concrete, cheap, falsifiable toy.** "Anchors = top-k persistent mutual-information edges in a dynamic graph" is small enough to code in an afternoon, and it has a clean failure mode (no edge is more stable than chance ⇒ no laws emerge). See [`SIMULATION.md`](SIMULATION.md).

That's the honest pitch: **CART is a recombination, not a discovery.** Recombinations are still worth writing down — but the framing should invite "where does this sit relative to Smolin and Wolfram, and what does the toy actually show?", not "I have found the theory of everything."

---

## 4. Strongest objections (state them before a critic does)

1. **Unfalsifiable-as-stated.** Like entropic gravity, "laws are stable correlations" can be made to fit anything *post hoc*. It earns scientific status only if the toy makes a prediction that could fail. → That's the whole point of [`SIMULATION.md`](SIMULATION.md).
2. **"No laws imposed" is probably false.** Hillar–Sommer showed even careful systems smuggle in dynamics. CART's correlation tracker, sliding window, and stability functional are *themselves* assumptions. Be explicit about them.
3. **Correlation ≠ law.** Stable correlation can be spurious (common cause, selection effects). A real anchor needs more than persistence — arguably intervention/causation, not just observation.
4. **Emergent-dimension is already better developed elsewhere.** Wolfram and the holography program have far more machinery. CART should *cite and build on* them, not pretend to replace them.
5. **"Constants drift" is empirically constrained.** Searches for variation in fundamental constants (e.g. the fine-structure constant) mostly bound the drift to be very small. CART's "laws drift" must live within those bounds.

---

## 5. The single most useful next experiment

Grounded in §2.6: take a **Schmidt–Lipson / symbolic-regression invariant finder**, run it on a system whose conserved quantity is **slowly changed by the experimenter mid-stream**, and ask: *does the finder track the drifting invariant, and does it signal the handover as a regime change?* If yes, CART has a working demonstration of its one novel claim (drift-tracking). If no, that's a clean, publishable negative result about the limits of correlation-only law discovery.

---

## 6. References

- Smolin, L. *Time Reborn* (2013); *The Life of the Cosmos* (1997). https://iai.tv/articles/lee-smolin-the-laws-of-the-universe-change-auid-2174
- Verlinde, E. "On the Origin of Gravity and the Laws of Newton" (2011); Entropic gravity overview. https://en.wikipedia.org/wiki/Entropic_gravity
- Wolfram Physics Project — emergent dimension / structure of space. https://www.wolframphysics.org/technical-introduction/potential-relation-to-physics/the-structure-of-space/
- "It from qubit" / emergent holographic spacetime from quantum information (PRL, 2025). https://arxiv.org/abs/2506.06595
- Rovelli, C. Relational Quantum Mechanics (Stanford Encyclopedia of Philosophy). https://plato.stanford.edu/entries/qm-relational/
- Schmidt, M. & Lipson, H. "Distilling Free-Form Natural Laws from Experimental Data," *Science* 324 (2009). https://pubmed.ncbi.nlm.nih.gov/19342586/
- "Discovering invariants via machine learning," *Phys. Rev. Research* 3, L042035 (2021). https://journals.aps.org/prresearch/abstract/10.1103/PhysRevResearch.3.L042035
- Minimum Description Length principle. http://www.modelselection.org/mdl/
- Tegmark et al., "Intelligence, physics and information: the tradeoff between accuracy and simplicity." https://arxiv.org/pdf/2001.03780

*Compiled as a research pass for CART. Read the sources before citing them as support — several (entropic gravity, Schmidt–Lipson's hidden assumptions) are cautionary as much as confirmatory.*
