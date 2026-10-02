# SEMINAR MASTER PLAN

**Working title:** *From Matrices to Microwaves: Designing and Measuring an RF Filter*
**Venue:** Undergraduate Maths Society, Constructor University
**Length:** ~50 min speaking + ~10 min questions
**Audience:** undergraduate mathematics students, mixed technical background, **most with little
or no RF engineering**

---

## S0 — Audience and thesis

### The audience, precisely

Mathematics undergraduates. They are **comfortable** with: complex numbers, matrices, matrix
multiplication, non-commutativity, inverses, linear algebra generally. They are **not** assumed to
know: transmission lines, impedance, decibels, S-parameters, filters, or what a VNA is.

**This is a gift, not a problem.** The mathematical core of the talk — cascaded 2×2 matrices,
order mattering, recovering one factor from a product — is material they already own. The talk's
job is to show them that *their* mathematics is the thing that makes a physical measurement
possible. That is a much better talk than a filter tutorial.

### Thesis

> A microwave circuit can be described by a matrix; connecting circuits means multiplying those
> matrices; and because multiplication can be undone, we can mathematically remove the parts of a
> measurement we did not want and recover the component we were actually trying to measure.

### The seminar question

> How can we mathematically describe a microwave circuit, combine several RF networks, and then
> recover the behaviour of one individual component from a real measurement?

### Rules that follow from the audience

1. **Narrative, not equations.** Every equation earns its place by answering a question the
   previous slide raised. Risk R-28.
2. **Three equations carry the talk**: Γ = (Z_L − Z₀)/(Z_L + Z₀); T_meas = T_L · T_DUT · T_R; and
   T_DUT = T_L⁻¹ · T_meas · T_R⁻¹. Everything else is support.
3. **No RF jargon without a plain-language gloss** the first time.
4. **Pictures over formulas** for the physics; formulas for the mathematics.
5. **Never present simulated data as measured.** Every plot is labelled with what produced it.
6. **Do not oversell the de-embedding equation.** It is the *principle*. Whether it is the exact
   production procedure depends on the method chosen at G8, and the talk says so.

---

## The three versions

The seminar must not fail because fabrication or VNA access slipped. Three complete versions
exist; the choice is made at the content-freeze date from what actually exists (decision D-011).

### SEMINAR A — full
Theory + ADS circuit + Momentum + PCB + VNA measurement + de-embedding.
**Requires:** G13. **The best version, and the least likely to be available in time.**

### SEMINAR B — measured, not de-embedded
Theory + ADS circuit + Momentum + PCB + VNA measurement; de-embedding **explained as principle,
with the honest account of why it was not completed.**
**Requires:** G11/G12.
**Note:** this is arguably a *better* talk than A for this audience. "Here is the beautiful
inversion, and here is why we could not justify applying it to our data" is intellectually honest
and more memorable than a clean result.

### SEMINAR C — simulation only, fixture demonstrated in simulation
Theory + verified ADS/Momentum results + a **clearly labelled simulated** fixture and de-embedding
demonstration.
**Requires:** G5, ideally G7. **Needs no hardware at all.**
**This is the default if nothing else is ready** — and it is a complete, honest talk.

### Non-negotiable across all three

> **NEVER invent experimental data.** In version C, every fixture/de-embedding plot is labelled
> **"simulated demonstration — no hardware measured"** on the slide itself, not only in the
> speaker notes. A label in the notes protects nobody; the audience sees the slide.

---

## Narrative arc

Twenty conceptual beats. Pacing will need **30–40 actual slides**; this is the structure, not the
deck. Detail in `slide_outline.md`.

| Act | Beats | Function | Needs |
|---|---|---|---|
| **I — The mystery** | 1–2 | Why does a wire stop being a wire? | nothing |
| **II — Waves** | 3–5 | Travelling waves, reflection, Γ | G1 |
| **III — Describing a box** | 6–8 | S-parameters as a measurement | G2 |
| **IV — The mathematics** | 9–11 | Matrices, cascading, **non-commutativity** | G2 |
| **V — Filters** | 12–14 | Response, geometry as circuit, design from theory | G3/G4 |
| **VI — Simulation** | 15–17 | Circuit model, layout, EM | G5/G7 |
| **VII — Reality** | 18–19 | The board, the VNA, the measurement | G11 |
| **VIII — The inversion** | 20–22 | Why measurement ≠ DUT; cascade; **de-embedding** | G8 (concept) |
| **IX — Honesty** | 23–24 | What we got, what we did not, limitations | G12/G13 |
| **X — Wider view** | 25 | Where else this mathematics appears | nothing |

**Acts I–V and VIII can be built now.** That is roughly 60 % of the talk, including both of its
strongest moments (non-commutativity, and the inversion). **This is why the seminar deadline is
survivable** — see `planning/milestones.md`.

---

## Development phases

| Phase | Deliverable | Needs | Status |
|---|---|---|---|
| **S0** | Audience + thesis fixed | nothing | ✅ **this document** |
| **S1** | Narrative architecture, beat by beat | nothing | ✅ `slide_outline.md` |
| **S2** | Theory slides + original diagrams | G2 | ⬜ |
| **S3** | Insert verified ADS circuit results | G5 | ⬜ |
| **S4** | Insert Momentum results | G7 | ⬜ |
| **S5** | Insert PCB photos + VNA results | G11 | ⬜ |
| **S6** | Insert de-embedding **only if defensible** | G13 | ⬜ |
| **S7** | Speaker notes | S2–S6 | ⬜ |
| **S8** | Timed rehearsal | S7 | ⬜ |
| **S9** | Cut and restructure on timing | S8 | ⬜ |
| **S10** | Q&A preparation | S9 | ⬜ |

> **Do not build a polished deck now.** S2 produces *diagrams and placeholders*. Polishing a deck
> whose results do not exist wastes the effort twice: once making it, once remaking it when the
> real plots arrive.

---

## Timing budget

| Act | Beats | Minutes |
|---|---|---|
| I — mystery | 1–2 | 4 |
| II — waves | 3–5 | 7 |
| III — describing a box | 6–8 | 6 |
| IV — **the mathematics** | 9–11 | **9** |
| V — filters | 12–14 | 6 |
| VI — simulation | 15–17 | 6 |
| VII — reality | 18–19 | 5 |
| VIII — **the inversion** | 20–22 | **8** |
| IX — honesty | 23–24 | 4 |
| X — wider view | 25 | 2 |
| | **total** | **57** |

**Over budget by ~7 minutes, deliberately.** First rehearsals always overrun; S9 exists to cut.

**Where to cut, in order:** Act VI (simulation detail — interesting to an engineer, less so to a
mathematician) → Act V (filter theory depth) → Act II (wave detail).
**Never cut Acts IV and VIII.** They are the talk. If the talk has to shrink to 30 minutes, it
becomes Acts I, IV, VIII and IX, and it still works.

---

## Q&A preparation (S10)

Questions a mathematics audience will actually ask — prepare honest answers:

- *"Is the matrix always invertible? What if it is singular?"* — **Expect this. They will spot it
  immediately.** It is the sharpest question available and the honest answer is the best part of
  the talk: near-singularity is exactly why naive inversion of noisy data is dangerous, and why
  gate G13 exists.
- *"How do you know your matrices are right?"* — calibration, verification standards, repeatability.
- *"What is the error bound?"* — repeatability spread from G11; be honest about what is not bounded.
- *"Why T-parameters and not S-parameters?"* — because S-matrices do not cascade by multiplication.
  Beat 9.
- *"Does the order of multiplication matter physically?"* — yes, and beat 11 showed it.
- *"Is this related to [transfer matrices in optics / scattering theory / Jones calculus]?"* —
  **yes, strongly.** Beat 25. Prepare this properly; it is where the talk lands for them.
- *"What went wrong?"* — have a real answer ready. Say the true thing.

> Prepare **"I don't know"** for at least two questions, and mean it. The audience is mathematically
> sharper than the speaker is in RF, and an honest boundary is more credible than a bluff — which
> is exactly the lesson a second-year student should want to demonstrate.
