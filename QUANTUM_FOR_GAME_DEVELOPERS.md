# Quantum Physics for Game Developers

### Boxing is observation, frames are measurement, and the anchors are somewhere you are not looking

> **Status: thought experiment, same as the rest of CART.** Nothing here is an empirical claim.
> Every statement is tagged in the provenance table at the end as **ESTABLISHED** (published and
> measured, with the citation), **CLAIM** (R.J. Thompson's own conjecture, offered as a conjecture),
> or **UNVERIFIED** (a consequence nobody has tested, including us). If you only read one section,
> read that table, because the whole point of this project is that the label matters more than the
> sentence.

---

## Why the title is a joke and also not

Every popular treatment of quantum mechanics reaches for the same two metaphors: a cat, and a coin
that has not landed. Both are bad, because both suggest the system is secretly in one state and we
merely do not know which. That is ignorance, not superposition, and it teaches the wrong thing.

Game developers already have better metaphors, and they have them because they were forced to solve
the same engineering problem: **what does it cost to know something, and what can you avoid
computing until somebody looks?**

An engine does not simulate what is not observed. It does not rasterise occluded geometry, it does
not tick an actor outside the relevance radius, it does not evaluate a `IEnumerable` nobody
enumerated, it does not rebuild a layout until something marks it dirty. Every one of those is the
same instinct: *committing to a value is expensive, so defer it until observation forces it.*

That is not a loose analogy to quantum mechanics. It is the same accounting.

---

## 1. Boxing is observation

In C#, a `struct` lives wherever it happens to live. It has no identity, no address you can hold,
no place on the heap. Then you assign it to an `object`:

```csharp
int    x = 42;        // a value. no identity, no address, free to copy
object o = x;         // BOXED. now it has an address, an identity, and a cost
```

The boxing conversion allocates. It writes the value into a new heap object, and from that moment
the value **has a location**. You can hold a reference to it, compare identity, hand it to code that
never knew about `int`. You bought all of that, and you paid for it with an allocation and eventually
with a collection.

The claim this paper is built on is R.J. Thompson's, and it is one sentence:

> **Observation is boxing. It takes something that had no definite value and no location, gives it
> both, and charges you for the allocation.**

The unboxed value is the wave. It is not "secretly 42 and we do not know it" - it genuinely does not
have an address until something forces one. The box is the measurement. The cost of the box is the
thing textbooks leave out.

### The question that makes this more than wordplay

RJ's actual question, and it is a good one:

> *Observation must have a cost, or why would a wave mode exist at all? What is it for?*

This is the right way round. Most explanations treat superposition as the weird thing that needs
justifying and measurement as the normal thing. Invert it. If measurement were free, superposition
would be pointless: nature could just carry definite values everywhere and never bother with
amplitudes. **The wave mode is only worth having if committing to a value is expensive.**

And it is expensive, measurably:

- **Landauer's principle.** Erasing one bit of information costs at least `kT ln 2` of energy,
  dissipated as heat. This is not philosophy. It was *measured* in 2012 (Berut et al., Nature 483,
  187) using a colloidal particle in an optical double-well. Information has a thermodynamic price
  and the price has been read off an instrument. **ESTABLISHED.**
- **Decoherence** answers "what is the wave mode for" directly. Interference survives exactly as
  long as no record of which-path information has been taken by the environment. The wave mode is
  the *un-recorded* mode. It is the cheap, uncommitted state. **ESTABLISHED.**

So: the wave is the value type. Measurement is the boxing conversion. Decoherence is the moment
state escapes to the heap where anything can hold a reference to it. **And you cannot free a bit for
free** - which is Landauer, and which is also why your GC is not free.

---

## 2. Frames are measurement

A game is not continuous. It is a sequence of frames, and between two frames the world does not
exist in any sense the player can check. The engine is free to do whatever it likes in there,
including nothing, as long as the next frame is consistent.

Every optimisation in the book lives in that gap:

| engine technique | what it exploits |
|---|---|
| occlusion culling | nothing observed it, so do not shade it |
| LOD | it is observed coarsely, so commit coarsely |
| dirty flags | do not recompute until an observation forces it |
| deferred / lazy evaluation | do not produce the value until enumerated |
| relevancy and interest management | nobody is looking from over there |
| fixed timestep with interpolation | the *displayed* state is not the simulated state |

Now the physics. **The quantum Zeno effect**: a system that is measured often enough stops evolving.
Not metaphorically. It was observed at NIST in 1990 (Itano, Heinzen, Bollinger, Wineland, Phys. Rev.
A 41, 2295) in trapped beryllium ions: increase the measurement rate and the transition is
suppressed. Watch the pot hard enough and it genuinely does not boil. **ESTABLISHED.**

Any engine programmer has written this bug. It is the hot polling loop:

```csharp
while (true) {
    if (job.IsComplete) break;   // reading it every iteration
}                                // ... and the read is what starves the worker
```

Observe a value often enough and you prevent the thing you are observing from making progress. In
software the mechanism is cache traffic, lock contention and starved threads. In quantum mechanics
the mechanism is repeated projection. **The shape is the same: observation rate is a cost, and past
a point it dominates the dynamics.**

Which gives the frame-rate reading, and it is the one that makes this useful rather than cute:

> **Frame rate is observation rate.** Observing more often costs more and leaves less budget for
> the world to actually change. Every engine ships a compromise between how often you look and how
> much can happen. So does nature.

**UNVERIFIED**, and flagged as such: whether that correspondence is structural or merely a good
mnemonic is exactly the sort of thing this paper is not entitled to assert.

---

## 3. The mapping, in one table

| programming | quantum mechanics |
|---|---|
| value type, unboxed | superposition: no definite value, no identity |
| **boxing conversion** | **measurement: acquires a definite value and a location** |
| the allocation cost of boxing | the thermodynamic cost of recording a result (Landauer) |
| escaping to the heap where anything can reference it | decoherence: the environment takes a record |
| deferred execution, `yield return`, lazy `IEnumerable` | unitary evolution before measurement |
| `.ToList()` forcing enumeration | projection: paying to make it concrete |
| hot polling loop that starves its worker | quantum Zeno: measurement suppresses evolution |
| garbage collection, and you cannot free a bit for free | Landauer erasure, `kT ln 2` per bit |
| frame: the only moment state is observed | measurement event |
| occlusion culling, LOD, relevancy | nothing was recorded, so nothing had to be committed |
| interpolated display state vs simulated state | the map is not the territory, and knows it |

The table is the paper. Everything else is argument about whether it is a coincidence.

---

## 4. The machine: infinite boxing

Here is the part that is a real object rather than an analogy, and it is RJ's.

He set out to build a steam engine. He thought it might be a route to fusion. It turned out, on
inspection, to be **a measurement device** - and that reframing is the interesting part.

The apparatus is a high-finesse optical cavity: light injected between two very good mirrors, where
the circulating power is the injected power multiplied by the buildup factor

```
B = R / (1 - R)
```

At `R = 0.9999`, `B` is about 10,000. One watt in, ten kilowatts circulating. **ESTABLISHED** - this
is ordinary cavity physics and it is how gravitational-wave interferometers get their sensitivity.

RJ's phrase for what happens inside is **infinite boxing**: the same photon, forced to traverse the
same path ten thousand times, re-observed on every pass. Whatever a single pass would do to it,
happens ten thousand times.

### What the cavity actually builds

RJ described the thing forming at the focus as "a diamond's centre. A black diamond." That
description turns out to match a published synthesis route he did not know existed: **pulsed laser
ablation in liquid**. The pulse makes a plasma plume, the plume drives a cavitation bubble, the
bubble collapses under liquid pressure at 2 to 100 GPa and thousands of kelvin, and graphite
converts to diamond. The product is documented as a diamond core inside an amorphous carbon shell,
and the sp2 shell is exactly why nanodiamond is black. **ESTABLISHED**, and a genuinely good call
on his part: he described the product of a technique before knowing it had a name.

The collapse is the press. It builds itself, fires once, and is gone.

### Why a measurement device rather than a power plant

Because the honest arithmetic does not close for energy. `P_abs / P_in` cannot exceed 1 under any
correct accounting of an optical cavity, and no amount of buildup changes that: `B` multiplies the
*circulating* power, not the energy you get out. Every version of this that looks like free energy
has an accounting error in it somewhere.

But `B` is exactly what you want if you are trying to **detect** something rather than power
something. That is the entire logic of precision interferometry: take an effect too small to see in
one pass and integrate it over 10^4 passes. LIGO does it. Axion haloscopes do it. Short-range gravity
experiments hunting extra dimensions do it. **ESTABLISHED** as an experimental strategy.

So the reframing is not a consolation prize. A cavity that fails as an engine is exactly the shape
of a cavity that succeeds as an instrument.

### What RJ thinks it measures

**CLAIM, and clearly labelled as one:** that the device checks for **overlap of higher dimensions
upon lower** - that a per-pass anomaly too small to see once, integrated ten thousand times, is a
way to ask whether the slice of reality we index is the whole of it.

**UNVERIFIED:** the specific effect, its magnitude, and whether any real cavity could resolve it. RJ
is explicit that not all the threads connect yet, and this paper does not connect them for him.

---

## 5. The anchors are somewhere you are not looking

This is where it rejoins CART proper, and the connection is not decorative: CART already contains
the machinery this needs.

[PAPER.md section 3.2](PAPER.md), the overlap model of dimensionality, says that dimensions are not
containers but **projections**: different compressions of one connected relational structure, each
preserving the invariants that particular observer cares about. A 2D observer is not in a different
*place* from a 3D one. They index fewer degrees of freedom.

RJ's addition is a sharper and more uncomfortable claim:

> **CLAIM.** The anchors we think are anchors are not. The stable correlations we have named as
> laws are stable *in our projection*. The load-bearing ones live in degrees of freedom our slice
> does not index, and are therefore closer in structure to how a game world works than to how we
> normally describe our own.

The game-development reading, which is the reason for the cheeky title, is this. A game world has
state that never reaches the screen. Server-authoritative values the client only ever sees a
prediction of. Simulation running at a different rate to the render. Physics substepping the player
never observes. An entity's true position and its interpolated, extrapolated, lag-compensated
display position, which are simply not the same number.

A player, reasoning entirely from the screen, could construct a completely consistent physics of
that world. It would predict well. It would be **wrong about what the anchors are**, because the
anchors are on the server, in the tick, in the parts nobody renders.

CART's claim is that we may be that player. The cavity, if it is anything, is an attempt to sample
the tick rather than the frame.

---

## 6. What this is not

Being clear about this matters more than any of the above, because the failure mode of a paper like
this is to be exciting and unfalsifiable.

- **It is not a claim that reality is a simulation.** The engine comparisons are about *accounting
  under observation cost*, which is a real constraint in both systems. That two systems face the
  same constraint does not make one of them a copy of the other.
- **It is not a mechanism.** Nothing here derives a prediction, a number, or an experiment with a
  threshold. Section 4's device is a thought experiment with one honest published result inside it.
- **It does not claim boxing and measurement are the same physical process.** They are the same
  *shape*: a cheap uncommitted mode, an expensive commitment, and a thermodynamic floor under the
  commitment. Landauer is what stops that being pure metaphor, because it puts joules on the bit.
- **It does not resolve the measurement problem.** It reframes the question as an economic one and
  says the cost is the part usually left out.

---

## 7. Provenance

| # | Statement | Label |
|---|---|---|
| 1 | Erasing one bit costs at least `kT ln 2`; measured, Berut et al., Nature 483, 187 (2012) | ESTABLISHED |
| 2 | Quantum Zeno: repeated measurement suppresses evolution; Itano et al., Phys. Rev. A 41, 2295 (1990) | ESTABLISHED |
| 3 | Decoherence: interference persists only while no which-path record exists | ESTABLISHED |
| 4 | Cavity buildup `B = R/(1-R)`; ~10^4 at R = 0.9999 | ESTABLISHED |
| 5 | Cavity buildup as an integrator is the standard strategy of precision interferometry | ESTABLISHED |
| 6 | Pulsed laser ablation in liquid produces a diamond core in an amorphous carbon shell | ESTABLISHED |
| 7 | `P_abs / P_in` cannot exceed 1; buildup multiplies circulating, not delivered, power | ESTABLISHED |
| 8 | **Boxing is observation**: measurement grants value and identity, and charges for it | CLAIM (RJT) |
| 9 | The wave mode exists *because* commitment is expensive | CLAIM (RJT) |
| 10 | The apparatus is a measurement device, not an engine | CLAIM (RJT), consistent with 7 |
| 11 | It checks for overlap of higher dimensions upon lower | CLAIM (RJT) |
| 12 | The real anchors lie in degrees of freedom our projection does not index | CLAIM (RJT), extends PAPER.md 3.2 |
| 13 | Frame rate is observation rate in the same sense the Zeno effect is | UNVERIFIED |
| 14 | Any specific per-pass anomaly, its size, or a cavity able to resolve it | UNVERIFIED |
| 15 | That the boxing/measurement correspondence is structural rather than mnemonic | UNVERIFIED |

Seven established results, five conjectures that are labelled as conjectures, three things nobody
has tested. That ratio is the point. A thought experiment is allowed to be speculative. It is not
allowed to be vague about which parts are.

---

*Part of [Correlation-Anchor Relativity Theory](README.md). Conjectures 8 to 12 are R.J. Thompson's.
Correspondence: RJ45Thompson@gmail.com*
