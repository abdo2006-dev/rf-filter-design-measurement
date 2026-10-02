# SLIDE OUTLINE

**~40 slides across 25 narrative beats.** Conceptual structure, not a locked deck.
Every slide needs a row in `source_map.md` before it is built.

**Legend:** 🟢 buildable now · 🟡 needs a gate · 🔴 needs hardware · ⚪ version-dependent

---

## ACT I — The mystery (4 min)

| # | Slide | Content | Status |
|---|---|---|---|
| 1 | Title | *From Matrices to Microwaves* · name, affiliation, date | 🟢 |
| 2 | The question | "Here is a small piece of copper. I measured it and got the wrong answer. This talk is about how mathematics tells me the right one." | 🟢 |
| 3 | A wire is not a wire | Same 10 cm wire at 50 Hz and at 3 GHz. **Original diagram.** The hook. | 🟢 |
| 4 | Why | λ at 50 Hz ≈ 6000 km; at 3 GHz ≈ 10 cm. The wire is now a *medium*. | 🟢 |

**Beat:** make them curious before explaining anything.

## ACT II — Waves (7 min)

| # | Slide | Content | Status |
|---|---|---|---|
| 5 | Two waves | Forward and backward travelling waves. **Original diagram**, ideally animated. | 🟢 |
| 6 | Why a reflection happens | Impedance mismatch, by analogy (wave hitting a change of medium) | 🟢 |
| 7 | **Γ = (Z_L − Z₀)/(Z_L + Z₀)** | **Equation 1 of 3.** Then the three cases: open → +1, short → −1, matched → 0 | 🟢 |
| 8 | What that means physically | Three small plots/diagrams for the three cases | 🟢 |
| 9 | Decibels, briefly | Only enough to read the later plots. 30 seconds, no more. | 🟢 |

## ACT III — Describing a box (6 min)

| # | Slide | Content | Status |
|---|---|---|---|
| 10 | The black box | Two ports, four things that can happen. **Original diagram.** | 🟢 |
| 11 | The four S-parameters | S₁₁, S₂₁, S₁₂, S₂₂ as reflection and transmission, each way | 🟢 |
| 12 | S-parameters are measurable | Unlike voltage and current at GHz. This is *why* they exist. | 🟢 |
| 13 | A real S-parameter plot | From our own simulation once G5 exists; a sketch until then | 🟡 G5 |

## ACT IV — The mathematics ★ (9 min)

> **The heart of the talk.** This act is the reason a maths society invited an engineer.

| # | Slide | Content | Status |
|---|---|---|---|
| 14 | Connecting two boxes | Physical picture: two networks in cascade. **Original diagram.** | 🟢 |
| 15 | **The problem** | You cannot just multiply the two S-matrices. Pose it as a puzzle and let it sit. | 🟢 |
| 16 | The fix: a different matrix | ABCD / transfer matrices. Same physics, different bookkeeping — chosen *so that* cascading becomes multiplication. | 🟢 |
| 17 | **Cascade = product** | T_total = T₁ · T₂ · T₃ … **The payoff slide.** | 🟢 |
| 18 | ★ **Order matters** | A·B ≠ B·A with two *physically real* networks, and what the difference physically is. **The single best slide in the talk.** | 🟡 G2 |
| 19 | Why they will like this | Non-commutativity is not an abstraction here — swapping two components changes a measurable number | 🟢 |

## ACT V — Filters (6 min)

| # | Slide | Content | Status |
|---|---|---|---|
| 20 | What a filter does | Ideal vs real response. **Original diagram.** | 🟢 |
| 21 | The trade-off | Order vs selectivity vs ripple vs size. Butterworth vs Chebyshev in one picture. | 🟢 |
| 22 | Design *from mathematics* | Normalized prototype → scale → transform. "The design came out of a table and some algebra, before any software." | 🟡 G4 |
| 23 | Geometry becomes a circuit | How copper shapes become Ls, Cs and resonators. **Original diagram.** | 🟡 G3 |

## ACT VI — Simulation (6 min)

| # | Slide | Content | Status |
|---|---|---|---|
| 24 | ★ Prediction vs simulation | Our hand-calculated prediction overlaid on the first simulated response. **"The maths drew this line before the software did."** | 🟡 G5 |
| 25 | The layout | Schematic → physical microstrip geometry | 🟡 G6 |
| 26 | What the substrate does | ε_eff shortens the wavelength; the board is *electrically* bigger than it looks | 🟡 G6 |
| 27 | Electromagnetic simulation | What a field solver adds that a circuit model cannot know. Current distribution picture. | 🟡 G7 |
| 28 | Three models, one axis | Ideal / microstrip / EM overlaid. They disagree — and *that is the point*. | 🟡 G7 |

## ACT VII — Reality (5 min)

| # | Slide | Content | Status |
|---|---|---|---|
| 29 | Real copper | Photograph of the fabricated board | 🔴 P9 |
| 30 | The instrument | What a VNA does: measures wave *ratios*. Photograph of the setup. | 🔴 P10 |
| 31 | Calibration | The instrument measures itself first. Reference planes. **Original diagram.** | 🟢 |
| 32 | ★ The measurement | Measured vs simulated, overlaid. **The moment of truth.** | 🔴 G11 |

## ACT VIII — The inversion ★ (8 min)

> **The intellectual climax.** Buildable now, except the final result slide.

| # | Slide | Content | Status |
|---|---|---|---|
| 33 | What did we actually measure? | Not the filter — the filter *plus two connectors, two launches, two feed lines* | 🟢 |
| 34 | fixture → DUT → fixture | **Original diagram.** The picture the whole project rests on. | 🟢 |
| 35 | **T_meas = T_L · T_DUT · T_R** | **Equation 2 of 3.** The measurement *is* a matrix product. | 🟢 |
| 36 | **T_DUT = T_L⁻¹ · T_meas · T_R⁻¹** | **Equation 3 of 3.** Undo the multiplication. Note the sides — **non-commutativity again, now with consequences** (callback to slide 18). | 🟢 |
| 37 | But how do you know T_L and T_R? | The real engineering problem. Fabricate standards, or model the fixture. Mention TRL and the 2x-thru briefly. | 🟡 G8 |
| 38 | ⚠ The honest caveat | **Required slide.** Inverting measured matrices amplifies noise. Near-singular matrices. The simple equation is the *principle*; the real procedure needs care and validity checks. | 🟢 |
| 39 | ★ The de-embedded result | **Version A:** de-embedded vs Momentum. **Version B:** why we could not justify it. **Version C:** clearly labelled simulated demonstration. | ⚪ G13 |

## ACT IX — Honesty (4 min)

| # | Slide | Content | Status |
|---|---|---|---|
| 40 | What we got | The five-way comparison table | 🔴 G12 |
| 41 | What went wrong, and why | Named mechanisms, with evidence. **And an explicit list of what we could not explain.** | 🔴 G12 |
| 42 | Limitations | Measurement uncertainty, model assumptions, what this does not prove | ⚪ |

## ACT X — Wider view (2 min)

| # | Slide | Content | Status |
|---|---|---|---|
| 43 | Where else this appears | Transfer matrices in optics, Jones calculus, scattering theory, cascaded linear systems generally. **Land the talk in their world.** | 🟢 |
| 44 | Close | Back to slide 2's question, now answered | 🟢 |
| 45 | References | Full attributions, per `source_map.md` | 🟢 |

---

## Build status

| | Slides | Count |
|---|---|---|
| 🟢 Buildable now | 1–12, 14–17, 19–21, 31, 33–36, 38, 43–45 | **26** |
| 🟡 Needs a simulation gate | 13, 18, 22–28, 37 | **11** |
| 🔴 Needs hardware | 29, 30, 32, 40, 41 | **5** |
| ⚪ Version-dependent | 39, 42 | **2** |

> **26 of 44 content slides can be built before any result exists** — including every slide in
> Acts I, II, III, most of IV, and almost all of VIII. **The two strongest moments of the talk
> (slides 18 and 33–38) need no hardware.**
>
> Slide 18 needs only gate G2, which needs no hardware, no licence and no money.
> **If only one thing gets built early, build slide 18.**

## Required slides

Cannot be cut under any version:

- **Slide 38** — the honest caveat about inversion. Without it the talk overclaims.
- **Slide 42** — limitations.
- **Slide 39's label** — in version C it must read *"simulated demonstration — no hardware
  measured"* **on the slide**, not in the notes.
- **Slide 45** — references.
