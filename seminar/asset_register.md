# SEMINAR ASSET REGISTER

*Every figure, plot, photograph and diagram that reaches a slide. No row, no slide.*

**Default: make it ourselves.** The strongest version of this talk is one where almost every visual
is the student's own work. That is a copyright-safety rule and a quality rule at once — a seminar
built from its own figures is visibly a seminar about its own project.

---

## Status

`needed` / `drafted` / `final` / `blocked`

## Origin

| Origin | Meaning | Licence work required |
|---|---|---|
| **original** | we made it from scratch | none |
| **adapted from** | we redrew it, informed by a source | cite the source; label "adapted from" |
| **reproduced** | the external figure itself | **full licence check and attribution before it reaches a slide** |

---

## A — Original diagrams (to draw)

The talk's backbone. **All of these can be drawn now** — they need no results, no hardware and no
licence check.

| ID | Asset | Slide | Tool | Status |
|---|---|---|---|---|
| AS-01 | Wire at 50 Hz vs 3 GHz | 3 | vector (Inkscape/draw.io) | needed |
| AS-02 | Forward and backward travelling waves | 5 | vector, ideally animated | needed |
| AS-03 | Reflection at an impedance discontinuity | 6 | vector | needed |
| AS-04 | Γ for open / short / matched | 7 | vector | needed |
| AS-05 | Two-port black box with four S-parameters | 10–11 | vector | needed |
| AS-06 | Two networks in cascade | 14 | vector | needed |
| AS-07 | **The two cascade orders, side by side** | **18** | vector | needed — *the key diagram* |
| AS-08 | Ideal vs real filter response | 20 | vector/plot | needed |
| AS-09 | Butterworth vs Chebyshev comparison | 21 | plot (own computation) | needed |
| AS-10 | Microstrip cross-section with field lines | 23, 26 | vector | needed |
| AS-11 | Calibration and reference planes | 31 | vector | needed |
| AS-12 | **fixture → DUT → fixture** | **34** | vector | needed — *the project's defining picture* |
| AS-13 | De-embedding: the inversion, illustrated | 36 | vector | needed |
| AS-14 | Why inversion is dangerous (noise amplification) | 38 | vector/plot | needed |
| AS-15 | Measurement chain with all reference planes RP0–RP6 | 33 | vector | needed |
| AS-16 | Transfer matrices across other fields | 43 | vector | needed |

> **AS-07 and AS-12 are the two most important visuals in the talk.** Spend real time on them.
> Both are drawable today.

## B — Our simulation results

| ID | Asset | Slide | Gate | Status |
|---|---|---|---|---|
| AS-20 | S₁₁ for open/short/matched, from ADS | 8 | G1 | blocked |
| AS-21 | First S-parameter plot | 13 | G5 | blocked |
| AS-22 | **Two cascade orders simulated** | 18 | G2 | blocked |
| AS-23 | Hand prediction vs simulation overlay | 24 | G5 | blocked |
| AS-24 | ADS schematic | 25 | G6 | blocked |
| AS-25 | Microstrip layout | 25 | G6 | blocked |
| AS-26 | Momentum current distribution | 27 | G7 | blocked |
| AS-27 | Ideal / microstrip / EM three-way overlay | 28 | G7 | blocked |

## C — Our hardware and measurements

| ID | Asset | Slide | Gate | Status |
|---|---|---|---|---|
| AS-30 | Photograph of the fabricated board | 29 | P9 | blocked |
| AS-31 | Photograph of the VNA setup | 30 | P10 | blocked |
| AS-32 | Measured vs simulated overlay | 32 | G11 | blocked |
| AS-33 | Five-way comparison table | 40 | G12 | blocked |
| AS-34 | Discrepancy attribution figure | 41 | G12 | blocked |
| AS-35 | De-embedded result **or** the honest alternative | 39 | G13 | blocked |

> **AS-31 note.** Photograph the *capability*, not the identity. Frame out asset tags, serial
> numbers, licence-server screens and anything identifying internal lab infrastructure. Risk R-27.

## D — External figures

**Currently: none, and that is the goal.**

| ID | Asset | Source | Origin | Licence | Attribution | Status |
|---|---|---|---|---|---|---|
| — | *(none)* | — | — | — | — | — |

### Before any external figure is added

All five, in order:

1. Identify the figure's **actual licence** — not the article's access status.
   **Open access ≠ free figure reuse.** A CC-BY article permits reuse with attribution; a
   "free to read" article often permits none; and a figure *inside* a CC-BY article may itself be
   reproduced from a third party under a narrower licence. Check the figure's own caption.
2. Record the licence text and the exact attribution wording **in this table, before building the
   slide**.
3. Prefer **adapting** (redraw, simplify, label "adapted from") over **reproducing**.
4. **Never screenshot a textbook figure.** Textbook figures are among the most tightly controlled
   material in the field, and Pozar and Hong & Lancaster are both all-rights-reserved.
5. If in doubt, **redraw it and cite the source for the idea.** This is the default, and it is
   almost always the better slide anyway.

**Candidates whose licence would permit reuse, if ever needed:** papers A1, A2, A3, A5 are
open-access MDPI/Nature titles, normally CC-BY. **Verify on the article page** — do not assume
from the publisher.

---

## Summary

| Category | Count | Buildable now |
|---|---|---|
| A — original diagrams | 16 | **16** |
| B — simulation results | 8 | 0 |
| C — hardware/measurement | 6 | 0 |
| D — external | 0 | n/a |
| **Total** | **30** | **16** |

> **Over half the talk's visuals can be made today**, including both of its most important
> diagrams, with no licence risk whatsoever. If the project ends up in seminar version C, the
> visual quality of the talk does not have to suffer — it just has to be honest about what is
> simulated.

## Technical conventions

Fix these once, at S2, and apply them everywhere — a consistent deck reads as more competent than
its content alone:

- Vector format (SVG/PDF) for every diagram. No bitmap line art.
- One font throughout, large enough for the back row.
- One colour convention for the models, used on **every** plot:
  *theory / ideal circuit / microstrip / EM / measured / de-embedded*.
- Every plot: axis labels, units, and a legend naming **which model produced it**.
- Every plot carries its result-register ID in the corner, so any number on screen is traceable.
- Colour choices must survive a projector and colour-blind viewers — do not distinguish two curves
  by red vs green alone.
