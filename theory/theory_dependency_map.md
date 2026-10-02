# THEORY DEPENDENCY MAP

*T1–T62, in dependency order, each with a test. This file is for the teacher (human or AI), not
for the student to read end to end.*

> **To the student:** do **not** read this file as a syllabus. It will look enormous and it is
> supposed to. Read `LEARNING_PATH_FOR_ME.md` instead — it tells you which block you are in and
> what to ignore. Come here only when a gate sends you.

> **To a Theory GPT or tutor:** teach **only** the concepts in the block the current gate requires.
> The project's biggest risk is premature theory (risk R-15) and its second biggest is unverified
> claims (R-22). Every concept below has a **test** phrased as "you understand this when you
> can…". Teaching is finished when the test passes — not when the explanation has been given.
> Cite Pozar (T1-01) or Hong & Lancaster (T1-02) for every load-bearing claim; see
> `research/claims_and_sources.md`.

---

## Block map and gate mapping

| Block | Concepts | Gate | Phase |
|---|---|---|---|
| A | T1–T7 — prerequisites | — | assumed from coursework |
| B | T8–T18 — transmission lines | **G1** | P1 |
| C | T19–T25 — RF networks and S-parameters | G2 | P2 |
| D | T26–T31 — matrix / network mathematics | G2 | P2 |
| E | T32–T41 — filters | G3, G4 | P3, P4 |
| F | T42–T47 — microstrip implementation | G6 | P6 |
| F+ | T48–T50 — planar EM concepts | G7 | P7 |
| G | T51–T54 — VNA and calibration | G10 | P10 |
| H | T55–T62 — de-embedding | G13 | P8 (concept), P12 (depth) |

**Dependency rule.** A block may not be taught before its prerequisites pass their tests. Block H
depends on D and G; attempting H without D is the mechanism behind risk R-21.

---

## BLOCK A — Prerequisites
*Assumed from second-year coursework. Verify quickly; do not teach unless a test fails.*

| ID | Concept | You understand this when you can… |
|---|---|---|
| T1 | Sinusoidal steady state | explain why a single frequency lets you replace differential equations with algebra |
| T2 | Phasors | convert between time-domain and phasor form, and say what information the phasor discards |
| T3 | Complex impedance | state what the real and imaginary parts physically do, and why a reactance stores rather than dissipates |
| T4 | Complex numbers as rotation/scaling | explain multiplication by e^(jθ) geometrically — **needed for the seminar; the maths audience will already have this** |
| T5 | Power and dB | convert between ratio and dB for power and for amplitude, and get the factor of 10 vs 20 right every time |
| T6 | Logarithmic frequency axes | read a Bode-style plot and estimate a slope per decade |
| T7 | Matrices and matrix multiplication | multiply 2×2 matrices confidently, and state when the product is defined |

---

## BLOCK B — Transmission lines ◀ **CURRENT**
*Gate G1, phase P1. Source: Pozar §2.1–2.3, §2.5–2.7.*

| ID | Concept | You understand this when you can… |
|---|---|---|
| T8 | Why distributed effects appear | explain, with one drawing, why a 10 cm wire is fine at 50 Hz and a problem at 3 GHz — **the seminar's opening** |
| T9 | Travelling waves on a line | write forward and backward waves and say what each physically is |
| T10 | Characteristic impedance Z₀ | state what Z₀ is, and explain why a multimeter cannot measure it |
| T11 | Propagation constant | separate α and β and say what each does to a wave |
| T12 | Wavelength and guided wavelength | compute λ₀ from f, and explain why λ_g in a substrate is shorter |
| T13 | Electrical length βl | explain why "short" and "long" are frequency-dependent words |
| T14 | Reflection coefficient Γ | derive Γ = (Z_L − Z₀)/(Z_L + Z₀) and compute it for any load |
| T15 | Open / short / matched terminations | predict Γ for all three and say what each does to the wave |
| T16 | Input impedance of a terminated line | explain that a line *transforms* impedance, and what is special about a quarter wave |
| T17 | S₁₁ as measured Γ, return loss | convert |Γ| to return loss in dB and interpret an S₁₁ plot without being told what it shows |
| T18 | Standing waves, VSWR *(light touch)* | explain where a standing wave comes from. **Do not go deep — Smith chart manipulation is not needed for this project.** |

**Block B exit test = gate G1.** Five items in `LEARNING_PATH_FOR_ME.md`.

---

## BLOCK C — RF networks and S-parameters
*Gate G2, phase P2. Source: Pozar §4.3.*

| ID | Concept | You understand this when you can… |
|---|---|---|
| T19 | Why S-parameters exist at RF | explain why voltage and current are awkward to measure at GHz and why waves are not |
| T20 | Incident and reflected wave variables | say what a and b are and why they are normalized |
| T21 | S₁₁ and S₂₂ | interpret both as reflections *looking into* a port with the other terminated |
| T22 | S₂₁ and S₁₂ | interpret both as transmission, and say what equality of the two implies (reciprocity) |
| T23 | Reference impedance | explain why an S-parameter is meaningless without one |
| T24 | Return loss and insertion loss | define both, **state the sign convention being used**, and read them off a plot |
| T25 | Two-port black box | explain what a 2×2 S-matrix does and does not capture |

---

## BLOCK D — Matrix and network mathematics
*Gate G2, phase P2. Source: Pozar §4.4. **The mathematical core of the project and the seminar.***

| ID | Concept | You understand this when you can… |
|---|---|---|
| T26 | Why S-parameters do not cascade by multiplication | explain why you cannot simply multiply two S-matrices to cascade two networks — **the motivating question for the whole block** |
| T27 | ABCD / chain matrices | write the ABCD matrix of a series impedance, a shunt admittance and a length of line, from memory |
| T28 | Cascading by multiplication | compute a two-network cascade and verify it against simulation |
| T29 | **Non-commutativity** | show A·B ≠ B·A with two real networks **and explain the physical meaning of the difference** — the seminar's best mathematical moment |
| T30 | Scattering transfer (T) parameters | explain how T differs from ABCD, why de-embedding uses T, **and state which convention you are using** |
| T31 | Conversions S ↔ ABCD ↔ T | convert in both directions, stating reference impedance and convention, and have it agree with ADS |

> **Risk R-21 lives here.** T-parameter definitions differ between sources. Pick one source, state
> it, and never mix. An error here is silent, survives plausibility checks, and would invalidate
> P12 without ever looking wrong.

---

## BLOCK E — Filters
*Gates G3 and G4, phases P3 and P4. Source: Pozar §8.3–8.4; Hong & Lancaster (chapters TBD).*

| ID | Concept | You understand this when you can… |
|---|---|---|
| T32 | Filter classes | sketch the ideal response of an LPF, HPF, BPF and BSF |
| T33 | Passband, stopband, transition band | mark all three on a real (non-ideal) response |
| T34 | Cut-off frequency | state the definition being used, and why "cut-off" needs a definition at all |
| T35 | Centre frequency and bandwidth | compute f₀ and bandwidth from band edges, and know whether f₀ is arithmetic or geometric mean in the convention used |
| T36 | Fractional bandwidth | compute it, and explain why it — not absolute bandwidth — predicts how hard the filter is to build |
| T37 | Filter order | explain what order buys, and what it costs in size, loss and tolerance sensitivity |
| T38 | Butterworth response | state its defining property and its trade-off |
| T39 | Chebyshev response | state its defining property, and what passband ripple buys |
| T40 | Normalized lowpass prototype | explain what normalization does and why element tables are universal |
| T41 | Frequency and impedance scaling, transformations | denormalize a prototype, and transform lowpass → bandpass |
| T41b | Resonators and coupling *(concept)* | explain what resonates and what couples in a coupled-resonator filter, and that coupling strength sets bandwidth |

---

## BLOCK F — Microstrip implementation
*Gate G6, phase P6. Source: Pozar §3.8; Hong & Lancaster (chapters TBD).*

| ID | Concept | You understand this when you can… |
|---|---|---|
| T42 | Microstrip geometry and the quasi-TEM picture | draw the cross-section and say where the field actually is |
| T43 | Effective permittivity ε_eff | explain why ε_eff lies between 1 and εr, and what that does to λ_g |
| T44 | Width → Z₀ | explain the direction of the relationship, and use LineCalc confidently |
| T45 | Quarter-wave and half-wave structures | compute physical lengths from f and ε_eff, and say what each structure does |
| T46 | Discontinuities | list what a step, bend, open end and T-junction each add, and say when each matters |
| T47 | Coupled lines and even/odd modes *(topology B/C only)* | explain why two coupled lines support two modes with different velocities, and how gap width controls coupling |
| T47b | Loss mechanisms | separate conductor loss from dielectric loss and say which dominates where |

---

## BLOCK F+ — Planar EM concepts
*Gate G7, phase P7. Source: ADS Momentum documentation (T2-05); Keysight 5992-1479.*

| ID | Concept | You understand this when you can… |
|---|---|---|
| T48 | What a method-of-moments surface solver does | explain that it solves for currents on conductor **surfaces**, and why that makes it 2.5-D rather than 3-D |
| T49 | Mesh, cells per wavelength, mesh frequency | explain why cell size is fixed while wavelength shrinks with frequency, and therefore why mesh frequency must be set to the top of the band |
| T50 | EM ports and reference planes | state where an EM simulation's result is referenced to, and what port calibration/de-embedding does — **this is de-embedding appearing inside the simulator, and it is the best bridge into block H** |

> **Explicitly flagged.** Do not carry over a CST-style volumetric adaptive-mesh convergence habit.
> See decision D-005 and claim M-04. Convergence here means stability of the S-parameters against
> the solver settings that control accuracy, plus agreement with a known answer.

---

## BLOCK G — VNA and calibration
*Gate G10, phase P10. Source: Keysight 5968-5329; instrument manual; Engen & Hoer if TRL.*

| ID | Concept | You understand this when you can… |
|---|---|---|
| T51 | What a VNA measures | explain that it measures ratios of waves, not voltages, and why that needs a reference |
| T52 | Reference planes | say exactly where the measurement plane is, and draw it on the physical setup |
| T53 | Systematic vs random error; what calibration removes | explain what calibration corrects and what it cannot (drift, repeatability, connector wear) |
| T54 | Calibration methods and Touchstone | describe the method actually being used, what standards it needs, and read a `.s2p` file by eye |

> Teach **the method being used**, not a survey of all of them. SOLT and TRL are both candidates
> and neither is assumed (decision D-006).

---

## BLOCK H — De-embedding
*Concept level at P8/G8; full depth only at P12/G13. Source: Keysight 5980-2784EN; Engen & Hoer;
IEEE Std 370-2020.*

| ID | Concept | You understand this when you can… |
|---|---|---|
| T55 | The fixture + DUT model | draw `fixture → DUT → fixture` and say what each block does to the measurement |
| T56 | Cascaded representation | write T_meas = T_L · T_DUT · T_R and explain why this needs T, not S (back to T26/T30) |
| T57 | Inverse networks | write T_DUT = T_L⁻¹ · T_meas · T_R⁻¹ and explain what "removing a network mathematically" means |
| T58 | Why order matters here | explain why the left and right inverses go on specific sides — **non-commutativity (T29) with real consequences** |
| T59 | Fixture characterization routes | describe at least three ways the fixture description could be obtained, with their assumptions |
| T60 | Validity assumptions | for the chosen method, list its assumptions and say how each would be checked |
| T61 | Numerical stability and noise | explain why inverting measured matrices amplifies noise, and name the checks that catch a non-physical result |
| T62 | When **not** to de-embed | state the conditions under which the honest answer is "do not proceed" — **this is a real engineering competence, not a cop-out** |

> **Teaching order matters.** T55–T58 are *conceptual* and teachable at P8, which is also when they
> are needed for the seminar. T59–T62 are *practical* and only needed at P12. Teaching T61 early
> is wasted; teaching it late is dangerous — it is the difference between R-18 and R-19.

---

## How to use this map

1. **Find the current gate** in `PROJECT_STATE.md`.
2. **Teach only that gate's block.** Ignore everything else.
3. **Test, don't assume.** The "you understand this when you can…" phrasing is the completion
   criterion. An explanation delivered is not a concept learned.
4. **Source every load-bearing claim.** Add it to `research/claims_and_sources.md`.
5. **If the student asks about a later block:** answer briefly, then point at
   `research/reading_queue.md` §3. Curiosity gets parked, not crushed.

### Concepts that carry double duty

These are needed by the project **and** are the seminar's best material. Invest extra in them:

- **T8** — why wires stop behaving like wires. The opening hook.
- **T14/T17** — reflection coefficient, and S₁₁ as its measurement.
- **T26** — why S-parameters do not cascade. The question the maths answers.
- **T29** — non-commutativity, with physical meaning. The single best slide in the talk.
- **T56–T58** — cascade and inversion. The intellectual climax.

A maths audience will find T29 and T57 more interesting than any filter result. Teach them well.
