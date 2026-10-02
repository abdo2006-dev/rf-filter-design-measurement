# SEMINAR SOURCE MAP

*One row per slide or slide group. A slide with no row here does not get built.*

> **Purpose.** The student has never prepared an academic technical seminar. This table is designed
> to make it structurally hard to put an uncited or unsupported claim on a slide. A slide whose
> **Verified?** column reads "no" cannot be presented.

**Status:** `planned` / `drafted` / `built` / `verified` / `cut`

---

## Columns

| Column | Meaning |
|---|---|
| Slide | number from `slide_outline.md` |
| Question answered | the question this slide exists to answer |
| Claim | the assertion made — the thing that could be wrong |
| Equation | equation shown, if any |
| Source | bibliography ID + section, or a project result ID |
| Source type | THEORY AUTHORITY / SOFTWARE PROCEDURE / MEASUREMENT AUTHORITY / ACADEMIC EXAMPLE / TEACHING RESOURCE / OUR RESULT |
| Visual | what is shown |
| Origin | **original** / **adapted from** / **reproduced** |
| Licence | licence of any external material |
| Attribution | exact wording to appear on the slide |
| Verified? | is the source verification status good enough to present? |
| Project result required? | which gate must pass |
| Status | see above |

---

## Act I — The mystery

| Slide | Question | Claim | Eq. | Source | Type | Visual | Origin | Licence | Attribution | Verified? | Result needed | Status |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| 1 | — | — | — | — | — | title | original | — | — | n/a | no | planned |
| 2 | Why should I care? | A measurement can give the wrong answer for structural reasons | — | — | — | photo/sketch | original | — | — | n/a | no | planned |
| 3 | Why does a wire stop being a wire? | Distributed effects appear when the wavelength is comparable to the physical size | — | T1-01 Pozar ch. 2 | THEORY AUTHORITY | diagram | **original** | — | "After Pozar, *Microwave Engineering*, 4th ed., ch. 2" | **partial** — confirm on reading | no | planned |
| 4 | How big is the effect? | λ = c/f; ≈6000 km at 50 Hz, ≈10 cm at 3 GHz | λ = c/f | T1-01 ch. 2 | THEORY AUTHORITY | computed table | original | — | — | yes — arithmetic | no | planned |

## Act II — Waves

| Slide | Question | Claim | Eq. | Source | Type | Visual | Origin | Licence | Attribution | Verified? | Result needed | Status |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| 5 | What travels on a line? | Forward and backward travelling waves | — | T1-01 §2.1–2.2 | THEORY AUTHORITY | diagram/animation | **original** | — | "After Pozar §2.1–2.2" | partial | no | planned |
| 6 | Why is there a reflection? | Reflection arises at an impedance discontinuity | — | T1-01 §2.3 | THEORY AUTHORITY | analogy diagram | **original** | — | same | partial | no | planned |
| 7 | How much reflects? | Γ = (Z_L − Z₀)/(Z_L + Z₀) | **Eq. 1** | T1-01 §2.3 | THEORY AUTHORITY | equation + 3 cases | original | — | same | partial | no | planned |
| 8 | What do the cases mean? | open → Γ=+1, short → Γ=−1, matched → Γ=0 | — | T1-01 §2.3 | THEORY AUTHORITY | 3 small plots | **our own ADS** | — | "our simulation, EXP-001" | **no — needs G1** | **G1** | planned |
| 9 | How do I read these plots? | dB definition for power ratios | dB = 10 log₁₀ | T1-01 | THEORY AUTHORITY | mini-table | original | — | — | yes | no | planned |

## Act III — Describing a box

| Slide | Question | Claim | Eq. | Source | Type | Visual | Origin | Licence | Attribution | Verified? | Result needed | Status |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| 10 | How do we describe a component? | A two-port is fully described by four wave ratios | — | T1-01 §4.3 | THEORY AUTHORITY | diagram | **original** | — | "After Pozar §4.3" | partial | no | planned |
| 11 | What are the four? | S₁₁, S₂₁, S₁₂, S₂₂ definitions | S-matrix | T1-01 §4.3 | THEORY AUTHORITY | matrix + diagram | original | — | same | partial | no | planned |
| 12 | Why waves, not V and I? | V and I are impractical to measure at GHz; wave ratios are not | — | T1-01 §4.3; T2-03 | THEORY + MEASUREMENT AUTHORITY | diagram | original | — | same | partial | no | planned |
| 13 | What does one look like? | — | — | **our result** | OUR RESULT | S-param plot | ours | — | result ID | **no** | **G5** | planned |

## Act IV — The mathematics ★

| Slide | Question | Claim | Eq. | Source | Type | Visual | Origin | Licence | Attribution | Verified? | Result needed | Status |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| 14 | What if I connect two? | Cascading is the basic operation of RF design | — | T1-01 §4.4 | THEORY AUTHORITY | diagram | **original** | — | "After Pozar §4.4" | partial | no | planned |
| 15 | Can I multiply the S-matrices? | **No** — S-matrices do not cascade by multiplication (claim T26) | — | T1-01 §4.4 | THEORY AUTHORITY | the puzzle | original | — | same | partial | no | planned |
| 16 | What does work? | ABCD/transfer matrices re-cast the same physics so cascading becomes multiplication | ABCD | T1-01 §4.4 | THEORY AUTHORITY | matrix defs | original | — | same | partial | no | planned |
| 17 | So what is a cascade? | T_total = ∏ Tᵢ | **product** | T1-01 §4.4 | THEORY AUTHORITY | equation | original | — | same | partial | no | planned |
| **18** | **Does order matter?** | **A·B ≠ B·A, and the difference is physically measurable** | A·B ≠ B·A | T1-01 §4.4 + **our EXP-004** | THEORY AUTHORITY + OUR RESULT | two cascades, two plots | **ours** | — | "our simulation, EXP-004" | **no — needs G2** | **G2** | planned |
| 19 | Why does a mathematician care? | Non-commutativity has a physical consequence here | — | — | — | callback | original | — | — | n/a | no | planned |

## Act V — Filters

| Slide | Question | Claim | Eq. | Source | Type | Visual | Origin | Licence | Attribution | Verified? | Result needed | Status |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| 20 | What is a filter? | Passband/stopband; real responses are not ideal | — | T1-01 ch. 8 | THEORY AUTHORITY | diagram | **original** | — | "After Pozar ch. 8" | partial | no | planned |
| 21 | What is the trade-off? | Order ↔ selectivity ↔ ripple ↔ size; Butterworth vs Chebyshev (claim F-02) | — | T1-01 §8.3 | THEORY AUTHORITY | comparison plot | **original** | — | same | **partial — read §8.3 first** | no | planned |
| 22 | Where does the design come from? | Insertion-loss method: prototype → scale → transform (claim F-01) | — | T1-01 §8.3–8.4 | THEORY AUTHORITY | our derivation | ours | — | "our derivation, P4" | **no** | **G4** | planned |
| 23 | How does copper become a circuit? | Microstrip geometry realizes filter elements | — | T1-02 *(chapter TBD)* | THEORY AUTHORITY | diagram | **original** | — | "After Hong & Lancaster, 2nd ed." | **no — chapter unknown** | G3 | planned |

## Act VI — Simulation

| Slide | Question | Claim | Eq. | Source | Type | Visual | Origin | Licence | Attribution | Verified? | Result needed | Status |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| 24 | Did the maths work? | hand prediction vs simulated response | — | **our result** | OUR RESULT | overlay plot | ours | — | result IDs | **no** | **G5** | planned |
| 25 | What does it look like physically? | — | — | **our layout** | OUR RESULT | ADS layout | ours | — | ours | **no** | **G6** | planned |
| 26 | What does the substrate do? | ε_eff shortens λ_g (claim F-04) | λ_g = λ₀/√ε_eff | T1-01 §3.8 | THEORY AUTHORITY | diagram + numbers | **original** | — | "After Pozar §3.8" | partial | G6 | planned |
| 27 | Why simulate fields? | A circuit model cannot know about unintended coupling; MoM solves surface currents (claim M-06) | — | T2-01; T2-05 | SOFTWARE PROCEDURE | current plot | **ours** | — | ours | **no** | **G7** | planned |
| 28 | Do the models agree? | They disagree, and the disagreement is informative | — | **our results** | OUR RESULT | 3-way overlay | ours | — | result IDs | **no** | **G7** | planned |

## Act VII — Reality

| Slide | Question | Claim | Eq. | Source | Type | Visual | Origin | Licence | Attribution | Verified? | Result needed | Status |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| 29 | Is it real? | — | — | **our board** | OUR RESULT | photograph | **ours** | — | ours | **no** | **P9** | planned |
| 30 | How do you measure it? | A VNA measures ratios of waves | — | T2-03; instrument manual | MEASUREMENT AUTHORITY | photograph + diagram | **ours** | — | ours | **no** | **P10** | planned |
| 31 | What is calibration? | The instrument characterizes its own errors first; this sets the reference plane | — | T2-03 | MEASUREMENT AUTHORITY | diagram | **original** | — | "After Keysight 5968-5329" | partial | no | planned |
| 32 | Did it work? | measured vs simulated | — | **our result** | OUR RESULT | overlay | ours | — | result IDs | **no** | **G11** | planned |

## Act VIII — The inversion ★

| Slide | Question | Claim | Eq. | Source | Type | Visual | Origin | Licence | Attribution | Verified? | Result needed | Status |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| 33 | What did we measure? | Not the DUT — the DUT plus two fixtures (claim T55) | — | T2-02; T2-03 | MEASUREMENT AUTHORITY | diagram | **original** | — | "After Keysight 5980-2784EN" | partial | no | planned |
| 34 | How do we picture it? | fixture → DUT → fixture | — | T2-02 | MEASUREMENT AUTHORITY | diagram | **original** | — | same | partial | no | planned |
| 35 | What is it mathematically? | T_meas = T_L · T_DUT · T_R (claim C-01) | **Eq. 2** | T2-02; T1-01 §4.4 | MEASUREMENT + THEORY AUTHORITY | equation | original | — | both | partial | no | planned |
| 36 | Can we undo it? | T_DUT = T_L⁻¹ · T_meas · T_R⁻¹ | **Eq. 3** | T2-02 | MEASUREMENT AUTHORITY | equation + callback to 18 | original | — | same | partial | no | planned |
| 37 | How do you get T_L, T_R? | Several routes exist, each with assumptions (claims C-03…C-08) | — | T2-02; T2-03; A9; T2-06 | MEASUREMENT AUTHORITY | options diagram | **original** | — | all four | partial | G8 | planned |
| **38** | **What is the catch?** | **Inversion amplifies noise; near-singular matrices are dangerous; the simple equation is the principle, not necessarily the procedure** (claim C-09) | — | **C-09 is UNSOURCED** | — | diagram/illustration | **original** | — | **needs a proper source** | **no — see C-09** | no | planned |
| 39 | Did it work? | version-dependent | — | ours | OUR RESULT | overlay **or** honest explanation **or labelled simulation** | ours | — | result IDs | **no** | **G13** | planned |

## Acts IX–X

| Slide | Question | Claim | Eq. | Source | Type | Visual | Origin | Licence | Attribution | Verified? | Result needed | Status |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| 40 | What did we get? | five-way comparison | — | **our results** | OUR RESULT | table | ours | — | result IDs | **no** | **G12** | planned |
| 41 | What went wrong? | attributed mechanisms + explicit unexplained list | — | **our analysis** | OUR RESULT | table/plots | ours | — | result IDs | **no** | **G12** | planned |
| 42 | What does this not prove? | limitations and uncertainty | — | **our analysis** | OUR RESULT | text | ours | — | — | **no** | G12 | planned |
| 43 | Where else does this appear? | Transfer matrices recur across linear wave systems — optics, Jones calculus, scattering theory | — | **no source yet** | — | diagram | **original** | — | **needs sources if claims are specific** | **no** | no | planned |
| 44 | — | close, callback to slide 2 | — | — | — | — | original | — | — | n/a | no | planned |
| 45 | — | references | — | all | — | list | — | — | **full attributions** | — | no | planned |

---

## Audit

**Of 44 content slides:**

| | Count |
|---|---|
| Fully verified and presentable today | **0** |
| Blocked only on reading a Tier-1 source | ~14 |
| Blocked on a project result | 18 |
| Blocked on a missing source | **2 (slides 38, 43)** |
| Blocked on an unknown chapter number | 1 (slide 23) |

### Action list

1. **Slide 38's claim (C-09) is UNSOURCED.** It is also a **required** slide. Either find a proper
   source for noise amplification under matrix inversion, or restate it as explicit reasoning
   ("here is why this is dangerous") rather than a cited fact. **Do not present it as a citation
   it does not have.**
2. **Slide 43** needs real sources if it makes specific claims about optics or scattering theory.
   Keep it qualitative otherwise.
3. **Slide 23** needs the Hong & Lancaster chapter number (bibliography T1-02).
4. **Every "After Pozar §x" attribution** is currently PARTIALLY VERIFIED because the book has not
   been opened. Reading the sections is a P1/P3 task and upgrades roughly 14 rows at once.

> **Nothing here is presentable yet, and that is the correct state 0 % of the way through the
> project.** The table's job is to make that visible rather than letting a plausible-looking deck
> get built on unchecked claims.
