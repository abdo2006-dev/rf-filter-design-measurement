# MASTER PROJECT PLAN

**Project:** Design, EM Simulation, Fabrication, VNA Characterization and De-embedding of a
Microstrip RF Filter
**Owner:** Abdulrahman — B.Sc. Electrical and Computer Engineering (year 2), Constructor University
**Mentor:** Artan (PhD student, RF/microwave, same research group)
**Plan version:** 1.0 — 2026-10-02
**Status:** P0 in progress, blocked at G0

---

## 0. How to read this plan

The plan is **phases** (what we do) separated by **gates** (objective evidence that we may
proceed). Phases may be reordered or merged; **gates may not be skipped.**

Every phase has the same thirteen fields: Objective, Why it exists, Required theory,
Authoritative references, Engineering tasks, Expected outputs, Validation method, Evidence to
save, Questions for Artan, Risks, Exit criteria, Fallback route, Seminar material.

### The stop line

> **This plan authorizes no filter dimensions.** No centre frequency, line width, gap, coupling
> coefficient, resonator length or Gerber file may be produced until **G0 and G3 have both
> passed**. Anything earlier is guessing dressed as engineering.

### Changes from the first-draft 13-phase outline, and why

This version has **15 phases (P0–P14)** and **14 gates (G0–G13)**. Three deliberate changes:

1. **The fixture / de-embedding *strategy* decision moved from the end to before PCB layout
   (new P8, gate G8).** This is the single most important structural fix. Every realistic
   de-embedding method either needs extra copper on the panel (TRL standards, a 2x-thru, an
   open/short/line coupon) or needs a specific calibration kit. Once the board is fabricated,
   the de-embedding options are frozen by the copper that exists. Deciding this at P10+ — as the
   original outline did — guarantees the stretch goal is lost. Supported by Keysight 5968-5329
   (in-fixture standards must be designed and built) and IEEE Std 370-2020 (the 2x-thru is a
   *fabricated structure*, not a post-processing choice).

2. **"ADS circuit simulation" split into ideal-circuit (P5) and microstrip-realization (P6),
   with separate gates G5 and G6.** These are genuinely different models that fail in different
   ways, and the difference between them is one of the project's actual results. Collapsing them
   hides where discrepancy is introduced.

3. **Momentum validation (P7/G7) is defined as a *method to be established*, not imported.**
   Momentum is a 2.5-D method-of-moments solver. A CST-style volumetric adaptive-mesh convergence
   rule does not transfer to it. G7 requires a written, defensible planar-EM validation procedure
   before any Momentum number is believed. See P7.

---

## 1. Phase overview

| # | Phase | Gate at exit | Hardware needed | Can run in parallel with |
|---|---|---|---|---|
| P0 | Scope and hardware-constraint capture | G0 | none | — |
| P1 | ADS orientation + transmission-line experiments | G1 | ADS licence | S0, S1 (seminar) |
| P2 | S-parameters and two-port networks | G2 | ADS licence | S1, S2 |
| P3 | Filter fundamentals and topology selection | G3 | none | S2 |
| P4 | Analytical synthesis — lumped prototype | G4 | none | S2 |
| P5 | ADS ideal-circuit simulation | G5 | ADS licence | S3 |
| P6 | Microstrip realization (circuit-level) | G6 | ADS licence | S3 |
| P7 | Momentum planar EM model + EM validation method | G7 | Momentum licence | S4 |
| P8 | Measurement & de-embedding strategy, layout plan | **G8** | none | S4 |
| P9 | PCB design review and fabrication | G9 | fabricator | S4 |
| P10 | VNA familiarization and calibration | G10 | VNA + cal kit | S5 |
| P11 | Measurement and simulation-vs-measurement comparison | G11, G12 | VNA | S5 |
| P12 | Fixture characterization and de-embedding *(conditional)* | G13 | VNA | S6 |
| P13 | Final engineering documentation / portfolio | — | none | S7 |
| P14 | Seminar finalization | — | none | S8–S10 |

The seminar track (S0–S10) runs **in parallel** throughout and is specified in
`seminar/SEMINAR_MASTER_PLAN.md`. It is designed so that the talk can be delivered even if P9–P12
never complete.

---

## 2. Decision gates

A gate is a checklist of **objective evidence**. "It looks right" is not evidence. "The plot looks
good" is not evidence. If a gate's evidence cannot be produced, the gate has not passed, and the
honest action is to say so in `PROJECT_STATE.md` rather than proceed.

### G0 — Constraints known
*Opens P1 and, with G3, the whole design track.*

| Evidence | Form |
|---|---|
| Substrate laminate identified by manufacturer and product name | `design/hardware_constraints.md`, with datasheet εr, tanδ, thickness, copper weight, and the **frequency at which εr is quoted** |
| Fabrication route identified | fabricator name/route, lead time, cost, minimum trace, minimum gap, etch tolerance if published |
| VNA identified | model, frequency range, port connector type, number of ports |
| Calibration resources identified | which kits/ECal/standards physically exist and are accessible |
| Connector decided or shortlisted | type (SMA / end-launch / edge-mount), and whether a known-good launch footprint exists |
| ADS access confirmed | version, licence type, **whether Momentum is included** |

**Fails if** any of the six is still a guess. Partial pass is allowed only by explicitly marking
the unknown as a BLOCKED criterion in the topology matrix and re-opening it later.

### G1 — I can explain my first transmission-line simulation
| Evidence | Form |
|---|---|
| ADS workspace with a terminated transmission line, swept | committed under `ads/learning/` |
| Four written predictions made **before** running, then compared | `ads/learning/EXP-001_*.md` using `templates/experiment_template.md` |
| A written explanation of why S₁₁ behaves as it does for open / short / matched / mismatched loads | same file |
| Theory block B self-test (5 items) passed | `LEARNING_PATH_FOR_ME.md` checklist, dated |

**Fails if** the simulation ran but the prediction was written afterwards. The prediction-first
order is the point.

### G2 — I understand S₁₁/S₂₁ and cascaded two-port networks
| Evidence | Form |
|---|---|
| Hand-computed ABCD cascade of two simple networks, then the same cascade simulated in ADS, agreeing | `ads/learning/EXP-00x_*.md` with both numbers in a table |
| A worked demonstration that `A·B ≠ B·A` for two physically different cascaded networks, with the physical meaning of the difference stated | `theory/` note + seminar asset |
| Correct S ↔ ABCD ↔ T conversion written out with the convention and reference impedance stated explicitly | `design/calculations/` |
| Return loss and insertion loss defined, with sign convention stated | same |

**Fails if** the S↔T conversion is used without stating the convention. Conventions differ
between textbooks and this is a known source of silent error.

### G3 — Filter topology and specification reviewed and defensible
| Evidence | Form |
|---|---|
| All 14 criteria in the topology matrix scored, with no BLOCKED rows remaining | `design/topology_selection.md` |
| A written justification naming the two runner-up topologies and why they lost | same |
| Filter specification complete: response type, order, f₀ or f_c, bandwidth, ripple/flatness, required stopband attenuation at a stated frequency, port impedance, and the **frequency range over which the specification is claimed** | `design/filter_specification.md` |
| Specification checked for realizability against the known minimum gap and etch tolerance | `design/design_reviews/DR-001_*.md` |
| Mentor has seen the specification and the topology choice | dated note in `planning/decision_log.md` |

**Fails if** the specification was chosen to be achievable rather than derived from a requirement,
without saying so. If the specification is arbitrary (it legitimately may be, for a learning
project), the plan must *state* that it is arbitrary and state what bounded it.

### G4 — Lumped prototype verified against theory
| Evidence | Form |
|---|---|
| Normalized prototype element values derived **and** cross-checked against a published table | `design/calculations/` showing both, and the source of the table |
| Denormalized/transformed element values | same |
| Ideal-lumped ADS simulation meeting the specification | `ads/circuit/` |
| Independent check of the order: does the achieved stopband attenuation match the analytical prediction at the stated frequency? | written comparison, numbers not adjectives |

### G5 — Ideal-circuit model satisfies the specification and the mechanism is understood
| Evidence | Form |
|---|---|
| ADS circuit model (ideal lumped and/or ideal transmission-line) meeting every specification line | `ads/circuit/` + result-register entries |
| A sensitivity study: which single element most moves f₀, and which most moves bandwidth, with numbers | experiment record |
| A written answer to "where does the passband edge come from, physically?" | design review note |

**Fails if** the model meets the specification only after an optimizer run that is not understood.
**No optimization before the hand-designed baseline is simulated and recorded.**

### G6 — Microstrip-realized circuit model satisfies the specification
| Evidence | Form |
|---|---|
| Microstrip model using the real substrate definition, with all physical dimensions tabulated | `ads/microstrip/` |
| Documented, quantified differences from the ideal model (Δf₀, ΔIL, ΔBW, Δreturn loss) | result-register entries |
| Every dimension checked against minimum trace/gap **with margin stated** | `design/design_reviews/DR-002_*.md` |
| Discontinuities (steps, bends, open ends, T-junctions) either explicitly modelled or explicitly justified as negligible | same |
| A tolerance study: response under εr ±(datasheet tolerance) and etch ±(fab tolerance) | experiment record |

### G7 — Momentum model validated for this task
*This gate has no inherited rule. The procedure is established here and recorded before results
are believed.*

| Evidence | Form |
|---|---|
| A written planar-EM validation procedure, specific to a 2.5-D MoM solver | `ads/momentum/EM_VALIDATION_METHOD.md` |
| **Solver-settings sweep**, not a geometric mesh-refinement sweep: cells-per-wavelength varied (e.g. 20 / 30 / 40 / 50) with mesh frequency pinned at the highest simulated frequency, and the resulting Δf₀ and ΔS₂₁ tabulated | table in `results/tables/` |
| Edge-mesh on/off compared, with a stated expectation (edge mesh matters most where current crowds — coupled-line gaps) | same table |
| Adaptive frequency sampling cross-checked against a discrete frequency sweep over the critical band | same |
| **A known-answer benchmark**: a plain 50 Ω line of known length simulated in Momentum and compared against the analytic/closed-form microstrip model | `ads/momentum/` + written comparison |
| Port setup documented: port type, calibration/de-embedding setting, reference impedance, and what reference plane the result is at | `ads/momentum/` |
| Substrate stack-up documented: dielectric thickness, conductor thickness and conductivity, finite vs infinite ground, cover/box if any | same |
| A **numerical** convergence criterion fixed *before* the sweep (e.g. Δf₀ < 0.25 % and ΔS₂₁ < 0.1 dB between successive settings) and shown to be met | same table |

**Explicit caution recorded in this plan:** do not import a CST-style adaptive volumetric
mesh-convergence criterion. Momentum discretizes *surfaces* with a mesh set by cells-per-wavelength
at a chosen mesh frequency; refinement is not automatically monotonic, and excessive refinement can
*degrade* the result numerically. Convergence here means *stability of the reported S-parameters
against the solver settings that actually control accuracy*, plus agreement with a known answer.

### G8 — Measurement and de-embedding strategy decided, **before layout freeze**
*The gate that protects the stretch goal.*

| Evidence | Form |
|---|---|
| The measurement chain written out end to end, with every reference plane named | `measurement/measurement_plan.md` |
| Calibration method chosen from what physically exists, with the choice justified | same |
| De-embedding method chosen **or explicitly deferred/declined**, from a written inventory of candidates with their validity assumptions | `measurement/measurement_plan.md` §de-embedding candidates |
| Decision on whether test structures go on the same panel, and if so exactly which ones | `pcb/manufacturing_constraints/` + decision log |
| Panel budget: board area, number of coupons, extra connector count and cost | same |
| Mentor consulted (Artan Round 2) | dated note in decision log |

**Fails if** layout proceeds with "we'll work out de-embedding later." After fabrication that
sentence means "we will not de-embed."

### G9 — PCB passes design review
| Evidence | Form |
|---|---|
| Completed design-review checklist, signed and dated | `design/design_reviews/DR-003_*.md` |
| DRC clean against the fabricator's actual rules | export log |
| Gerber/ODB++ exports visually verified in an independent viewer | screenshot + note |
| Launch footprint matches the connector datasheet, dimension by dimension | review note |
| Every coupon from G8 present, labelled, and silkscreen-identifiable | review note |
| Board outline, panel, and connector clearance physically checkable | review note |

### G10 — VNA calibration and reference-plane procedure documented
| Evidence | Form |
|---|---|
| Instrument state saved and exported | `measurement/calibration/` |
| Calibration kit and method recorded, with standard definitions / kit ID | same |
| Post-calibration verification: a known standard measured and compared against its expected response | plot + numbers |
| An explicit statement of **where the reference plane is** after calibration | `measurement/measurement_plan.md` |
| Residual-error estimate or at minimum a documented verification result | same |

### G11 — Raw measurements preserved and repeatability checked
| Evidence | Form |
|---|---|
| Raw Touchstone files committed, never edited | `measurement/raw/` (append-only) |
| ≥3 reconnect/remeasure repeats of the same DUT | files + repeatability table |
| Quantified repeatability: spread in f₀, IL, return loss across repeats | `results/tables/` |
| Measurement log: date, instrument, settings, IF bandwidth, power, averaging, temperature if relevant, who measured | `measurement/measurement_plan.md` log section |

**Fails if** there is one measurement. One measurement has unknown uncertainty, so it cannot
support a discrepancy claim.

### G12 — Discrepancy quantitatively analyzed
| Evidence | Form |
|---|---|
| One table comparing theory / ideal circuit / microstrip circuit / Momentum / measured on the same metrics | `results/tables/` |
| Each discrepancy attributed to a named mechanism with supporting evidence, not a guess | `results/result_register.md` + written analysis |
| Discrepancies that cannot be attributed are **listed as unexplained** | same |
| Measurement uncertainty from G11 carried into every comparison | same |

### G13 — De-embedding go / no-go
*This gate is permitted to end the stretch goal.*

| Evidence | Form |
|---|---|
| Fixture characterization actually obtained by the method chosen at G8 | `measurement/` |
| Validity assumptions of the method checked against what was built, one by one | written check |
| A sanity test applied to the de-embedded result: passivity, reciprocity for a passive reciprocal DUT, no \|S₂₁\| > 1, physically plausible phase | written check |
| Noise/stability assessment: does the de-embedded result change unreasonably with small input perturbation? | written check |

**A legitimate outcome of G13 is: "Do not proceed with de-embedding."** If the available
standards, coupons or calibration do not support a defensible method, the correct engineering
result is to say so, explain what *would* have been needed, and present the comparison without
de-embedding. That is a finding, not a failure, and the seminar has a version (Seminar B) built
for it.

**Never** report a de-embedded result produced by inverting cascaded matrices on noisy data
without this gate's checks. Naive inversion amplifies noise and can produce non-physical results
that look plausible on a plot.

---

## 3. Phases in detail

---

### P0 — Scope and hardware-constraint capture

- **Objective.** Convert every unknown lab/manufacturing fact into a recorded, dated answer, so
  that design decisions become engineering decisions instead of guesses.
- **Why it exists.** Six of the fourteen topology-selection criteria depend on facts only the lab
  can supply. Choosing a topology before G0 means choosing it on aesthetics. This phase also
  prevents the failure mode of the student's two previous projects: unbounded scope.
- **Required theory.** None. This is deliberate — the project starts with a phase that needs no
  theory, so progress is possible immediately.
- **Authoritative references.** None required. `design/hardware_constraints.md` is the instrument.
- **Engineering tasks.**
  1. Send the Artan Round 1 message (`planning/questions_for_artan.md`).
  2. Fill `design/hardware_constraints.md` from his answers; mark anything still unknown BLOCKED.
  3. Obtain the actual substrate datasheet; record εr **and the frequency it is quoted at**, tanδ,
     thickness tolerance, copper weight.
  4. Obtain the fabricator's design rules; record minimum trace, minimum gap, etch tolerance.
  5. Confirm ADS version and whether Momentum is licensed.
  6. Score the 6 BLOCKED criteria in the topology matrix.
- **Expected outputs.** Completed `hardware_constraints.md`; decision-log entries; a fully scored
  topology matrix.
- **Validation method.** Every field traceable to a named source — a datasheet, a fabricator web
  page, or a dated statement from Artan. No field filled from memory or from an AI's assumption.
- **Evidence to save.** Datasheet *reference* (not the PDF — see copyright rules), fabricator rule
  page reference, dated notes of Artan's answers.
- **Questions for Artan.** Round 1, all of it.
- **Risks.** R-04 (substrate data unknown), R-11 (VNA availability), R-20 (mentor response time).
- **Exit criteria.** **G0.**
- **Fallback route.** If Artan is unavailable for >2 weeks: proceed with a *declared* hypothetical
  constraint set, clearly marked PROVISIONAL throughout, and treat the whole design track as a
  rehearsal to be redone on real constraints. Never let a hypothetical constraint silently become
  CONFIRMED.
- **Seminar material.** None directly — but this phase produces the honest "here is what an
  engineer must know before drawing anything" slide, which is a good early-talk beat.

---

### P1 — ADS orientation and transmission-line experiments

- **Objective.** Become able to build, simulate and *interpret* a simple transmission-line circuit
  in ADS, and to predict its behaviour before simulating.
- **Why it exists.** ADS competence is a stated career asset and a hard prerequisite for every
  later phase. Starting with a single transmission line means the first ADS failure is a software
  failure, not a software *and* physics failure.
- **Required theory.** Theory block B (T8–T18): travelling waves, Z₀, β, λ_g, electrical length,
  Γ, open/short/matched, input impedance of a terminated line.
- **Authoritative references.** Pozar ch. 2 (§2.1–2.3, 2.5–2.7); Keysight *RF Design Software
  Learning Kit* (transmission-line chapter and its ADS workspaces); Keysight ADS documentation for
  `TLIN`/`MLIN` and `S_Param` controller.
- **Engineering tasks.**
  1. Install/access ADS, create the project workspace, learn workspace/library/cell structure.
  2. EXP-001: ideal line (`TLIN`) with swept load — open, short, 50 Ω, 75 Ω. Predict first.
  3. EXP-002: sweep electrical length at fixed frequency; relate to λ_g.
  4. EXP-003: quarter-wave transformer between two unequal impedances; predict the match frequency.
  5. Learn to read and export S-parameter data; learn the data display.
- **Expected outputs.** 3 committed experiment records; 3 ADS workspaces; the first original
  seminar diagrams (wave on a line, reflection at a mismatch).
- **Validation method.** Prediction-before-simulation, recorded in that order. For EXP-001 the
  analytic Γ is computable by hand — the simulation must reproduce it to within numerical error.
- **Evidence to save.** Workspaces, exported S-parameter data, plots, the experiment records.
- **Questions for Artan.** Which ADS version/licence; is there a group ADS template or preferred
  substrate definition file; any group convention for workspace naming.
- **Risks.** R-01 (ADS learning curve), R-02 (ADS licence availability).
- **Exit criteria.** **G1.**
- **Fallback route.** If ADS access is delayed: do the identical experiments in an open tool
  (e.g. `scikit-rf`, QUCS-S) to keep the *theory* moving, and clearly label those results as
  non-ADS. Re-run in ADS when available — the ADS competence claim requires ADS.
- **Seminar material.** Seminar **Act I–II** (why wires stop behaving like wires; travelling waves; reflection, Γ)
  and original figures AS-01 to AS-04, plus AS-20 from EXP-001.

---

### P2 — S-parameters and two-port networks

- **Objective.** Be fluent with S₁₁/S₂₁/S₁₂/S₂₂, and be able to cascade networks correctly using
  ABCD/T matrices — by hand and in ADS, with matching answers.
- **Why it exists.** This is the project's mathematical core *and* the seminar's mathematical core.
  The de-embedding stretch goal is nothing but this block applied carefully. Doing it properly here
  is what makes P12 possible and what makes the seminar honest.
- **Required theory.** Blocks C and D (T19–T31): the four S-parameters, return/insertion loss,
  reference impedance, ABCD and T matrices, cascading, non-commutativity, S↔ABCD↔T conversions and
  their conventions.
- **Authoritative references.** Pozar §4.3 (S-parameters), §4.4 (ABCD matrices) and the
  conversion tables; Keysight 5980-2784 / AN 1364-1 for the S↔T treatment used in de-embedding.
- **Engineering tasks.**
  1. EXP-004: build two different two-ports (e.g. a series element and a length of line); compute
     the cascade ABCD by hand both ways round; simulate both orders in ADS; tabulate.
  2. Write the S↔ABCD↔T conversions out explicitly, stating reference impedance and the
     *definition of T* being used.
  3. EXP-005: cascade three networks and verify associativity but not commutativity.
  4. Build a small reusable calculation sheet (hand or script) for the conversions.
- **Expected outputs.** 2 experiment records; the conversion sheet in `design/calculations/`; the
  seminar's central "order matters" figure.
- **Validation method.** Hand calculation and ADS must agree to numerical precision. Any
  disagreement is a convention error and must be resolved, not averaged.
- **Evidence to save.** Hand calculations (scanned or typeset), ADS workspaces, the comparison
  table.
- **Questions for Artan.** Which T-parameter convention the group uses; whether he has a preferred
  reference for the conversions.
- **Risks.** R-21 (T/S convention confusion silently corrupting later de-embedding).
- **Exit criteria.** **G2.**
- **Fallback route.** None needed — this phase requires no hardware and no licence. It is the
  safest phase in the project and the best use of any waiting time.
- **Seminar material.** Seminar **Acts III–IV**: S-parameters as a measurement, the two-port black box, matrices,
  cascading as multiplication, non-commutativity. **The heart of the talk, and buildable here** —
  EXP-004 produces asset AS-22, the single most important plot in the deck.

---

### P3 — Filter fundamentals and topology selection

- **Objective.** Understand what a filter response *is*, and choose the topology on recorded
  criteria rather than preference.
- **Why it exists.** The topology choice determines the fabrication difficulty, the measurement
  difficulty, the de-embedding opportunity and the seminar's mathematical depth. It deserves a
  decision matrix, not an opinion.
- **Required theory.** Block E (T32–T41): LPF/HPF/BPF/BSF, passband, stopband, cut-off, f₀,
  bandwidth, fractional bandwidth, order, Butterworth vs Chebyshev trade-off, normalized
  prototypes, resonators, coupling.
- **Authoritative references.** Pozar ch. 8, especially §8.3 (insertion-loss method) and §8.4
  (filter transformations); Hong & Lancaster ch. 3 (basic design) and the topology chapters —
  ch. 5 for coupled-line/stepped-impedance structures and the hairpin treatment.
- **Engineering tasks.**
  1. Study the three candidate topologies at concept level — what resonates, what couples, what
     sets f₀ and bandwidth in each.
  2. Score all 14 criteria in `design/topology_selection.md` now that G0 has supplied the lab facts.
  3. Write the filter specification in `design/filter_specification.md` — and state whether each
     line is a *requirement* or an *arbitrary learning target*.
  4. Realizability pre-check: is the implied minimum gap manufacturable? This question kills more
     coupled-line designs than any other.
  5. Design review DR-001; mentor sign-off.
- **Expected outputs.** Scored matrix, written justification naming the losers, filter
  specification, DR-001.
- **Validation method.** Every score traceable to a reference, a datasheet, or a stated judgement
  with reasoning. The chosen topology must survive the realizability pre-check with margin.
- **Evidence to save.** Matrix, specification, review, decision-log entries.
- **Questions for Artan.** Does he prefer LPF or BPF for the educational goal? What centre-frequency
  region makes sense for the available VNA and substrate? Any topology he considers a trap for a
  first project?
- **Risks.** R-06 (minimum gap unmanufacturable), R-07 (etch tolerance), R-15 (scope creep via an
  over-ambitious specification).
- **Exit criteria.** **G3.**
- **Fallback route.** If the preferred topology fails realizability, fall to the next-ranked
  topology in the matrix — the matrix exists precisely so this is a lookup, not a new debate.
  A stepped-impedance LPF is the structural fallback of last resort: it has no critical gap.
- **Seminar material.** Seminar **Act V** (beats 20–21 in `slide_outline.md`): what a filter response is, and the
  order/selectivity/ripple trade-off. Assets AS-08, AS-09.

---

### P4 — Analytical synthesis: lumped prototype

- **Objective.** Derive the filter from theory to a set of element values, by hand, and verify them.
- **Why it exists.** This is the "theoretically designed" half of the core question. Without a
  hand-derived baseline there is nothing for the simulations and the measurement to be compared
  *against*, and the project degenerates into tuning.
- **Required theory.** Block E, deeper: insertion-loss method, normalized low-pass prototype,
  element tables, frequency and impedance scaling, bandpass transformation if applicable.
- **Authoritative references.** Pozar §8.3–8.4 (prototype values, transformations); Hong &
  Lancaster ch. 3 (lowpass prototype) and the relevant realization chapter.
- **Engineering tasks.**
  1. Derive the required order from the stopband requirement analytically; show the arithmetic.
  2. Obtain normalized prototype g-values; cross-check against a published table and cite it.
  3. Denormalize / transform to real element values.
  4. Predict, analytically, the insertion loss at two stopband frequencies — these become
     falsifiable predictions for P5.
- **Expected outputs.** `design/calculations/` with the full derivation; a prediction table.
- **Validation method.** Two independent routes to the element values (derivation + published
  table) must agree. The analytical stopband prediction must later be reproduced by the ideal
  circuit simulation.
- **Evidence to save.** Derivation, table citation, prediction table.
- **Questions for Artan.** Would he like to see the hand derivation before simulation (recommended
  — it is the cheapest possible review).
- **Risks.** R-03 (insufficient theory), R-22 (AI-supplied formula accepted without a textbook check).
- **Exit criteria.** **G4.**
- **Fallback route.** If the derivation stalls, reduce to a lower order or a simpler response type
  and record the reduction as a decision. A working third-order design beats a stalled fifth-order one.
- **Seminar material.** Seminar **Act V** (beat 22): the design comes out of mathematics — prototype, scaling,
  transformation. A strong beat for a maths audience.

---

### P5 — ADS ideal-circuit simulation

- **Objective.** Reproduce the hand design in ADS with ideal elements and confirm it meets the
  specification, understanding *why* it does.
- **Why it exists.** It isolates "is my maths right?" from "is my microstrip right?". A failure
  here is an analysis error; a failure at P6 is a realization error. Keeping them separate is what
  makes the final discrepancy analysis attributable.
- **Required theory.** Blocks C–E, already held.
- **Authoritative references.** Keysight *RF Design Software Learning Kit* (passive filters
  chapter); ADS documentation for the S-parameter simulation controller.
- **Engineering tasks.**
  1. Build the ideal-lumped schematic; simulate; compare against the P4 predictions.
  2. Build the ideal-transmission-line equivalent if the topology has one; compare.
  3. EXP: single-element sensitivity sweep — which element moves f₀ most, which moves BW most.
  4. Record the **unoptimized baseline** in the result register before touching any tuner.
- **Expected outputs.** `ads/circuit/` workspaces; result-register entries; sensitivity table.
- **Validation method.** Simulated stopband attenuation must match the P4 analytical prediction
  within a stated tolerance. If it does not, one of the two is wrong — find out which.
- **Evidence to save.** Workspaces, exported S-parameters, plots, experiment records.
- **Questions for Artan.** None blocking.
- **Risks.** R-16 (optimizing before understanding the baseline — explicitly forbidden until the
  baseline is committed).
- **Exit criteria.** **G5.**
- **Fallback route.** If ADS is unavailable, simulate in `scikit-rf` to keep moving, labelled as
  non-ADS, and re-run later.
- **Seminar material.** Seminar **Act VI** (beat 24), asset AS-23: the first simulated response with the hand
  prediction overlaid. "The maths predicted this line before the software drew it."

---

### P6 — Microstrip realization (circuit-level)

- **Objective.** Convert the ideal design into physical microstrip geometry using ADS microstrip
  models on the real substrate, and quantify what that conversion costs.
- **Why it exists.** This is where a design first meets physics: dispersion, discontinuities,
  finite conductor thickness, coupling that is not ideal. The ideal→microstrip delta is a project
  result in its own right.
- **Required theory.** Block F (T42–T47): effective permittivity, λ_g, quarter-/half-wave
  behaviour, coupled lines, even/odd modes (only if the chosen topology needs them), physical
  spacing vs coupling.
- **Authoritative references.** Hong & Lancaster ch. 4 (microstrip transmission lines and
  discontinuities) and the chosen topology's realization chapter; Pozar §3.8 (microstrip);
  Keysight LineCalc documentation and the *Learning Kit* microstrip examples.
- **Engineering tasks.**
  1. Define the substrate in ADS from the datasheet — including conductor thickness and
     conductivity, not just εr and h.
  2. Synthesize line widths/lengths/gaps with LineCalc; tabulate every dimension.
  3. Replace ideal elements with microstrip models; include steps, bends, open-end and T-junction
     models, or justify omitting each.
  4. Compare against the P5 ideal model; tabulate Δf₀, ΔIL, ΔBW, Δreturn loss.
  5. Tolerance study: εr ± datasheet tolerance, etch ± fab tolerance, h ± tolerance.
  6. Check every dimension against minimum trace/gap and record the margin.
  7. Design review DR-002.
- **Expected outputs.** `ads/microstrip/` workspaces; full dimension table; tolerance study;
  DR-002.
- **Validation method.** Every dimension manufacturable with stated margin. The ideal→microstrip
  differences must be *explainable* mechanism by mechanism, not merely observed.
- **Evidence to save.** Workspaces, dimension table, tolerance plots, review.
- **Questions for Artan.** Is the substrate definition realistic (conductor thickness,
  conductivity, surface finish)? Does he trust the datasheet εr at our frequency, or should the
  substrate be characterized first?
- **Risks.** R-04/R-05 (substrate data and tolerance), R-06 (minimum gap), R-07 (etch tolerance).
- **Exit criteria.** **G6.**
- **Fallback route.** If the required gap is unmanufacturable, return to the P3 matrix and take the
  next topology. This is the designed-in escape hatch and using it is not a setback.
- **Seminar material.** Seminar **Act VI** (beats 25–26), assets AS-24, AS-25, AS-10: geometry *is* the circuit; the
  layout; what the substrate does to wavelength.

---

### P7 — Momentum planar EM model and EM validation method

- **Objective.** Build a planar EM model of the actual layout, and — first — establish a defensible
  procedure for deciding when a Momentum result may be believed.
- **Why it exists.** The microstrip circuit models are analytic approximations composed
  piece-by-piece; they do not know about coupling between parts of the layout that are merely
  *near* each other, nor about the real current distribution. EM simulation is the bridge between
  "circuit model" and "copper". It is also where the project earns the phrase "EM simulation" on a CV.
- **Required theory.** Conceptual only: what a method-of-moments surface solver does, what a mesh
  is for, what a port and a reference plane mean in EM simulation. No Green's functions required.
- **Authoritative references.** Keysight **5992-1479**, *Planar Electromagnetic (EM) Simulation in
  ADS — Chapter 4*, which includes a coupled-line microstrip bandpass filter case study and the
  schematic→layout→EM workflow; ADS Momentum documentation on mesh density, mesh frequency, edge
  mesh and port calibration; Hong & Lancaster for the expected physics.
- **Engineering tasks.**
  1. **Write `ads/momentum/EM_VALIDATION_METHOD.md` before producing any result.** It must state
     the settings to be swept, the convergence metric, and the numerical threshold.
  2. Known-answer benchmark: simulate a plain 50 Ω line of known length; compare Momentum against
     the analytic microstrip model and against the expected phase per unit length.
  3. Generate layout from schematic; define substrate stack-up; define ports.
  4. Settings sweep: cells-per-wavelength at 20/30/40/50 with mesh frequency pinned at the top of
     the band; tabulate Δf₀ and ΔS₂₁ between successive settings.
  5. Edge mesh on/off; record the difference and whether it matches the expectation that it matters
     most at coupled-line gaps.
  6. Adaptive frequency sampling vs discrete sweep across the critical band.
  7. Document port calibration/de-embedding settings and state what reference plane the result is at.
  8. Compare Momentum against the P6 microstrip model; attribute the differences.
- **Expected outputs.** `ads/momentum/EM_VALIDATION_METHOD.md`; convergence table in
  `results/tables/`; EM S-parameters; current-distribution visualization (a genuinely good seminar
  asset); written circuit-vs-EM comparison.
- **Validation method.** The pre-declared numerical convergence criterion, **plus** the
  known-answer benchmark, **plus** physical plausibility. All three, not one.
- **Evidence to save.** Workspaces, convergence table, exported S-parameters, current plots, the
  method document.
- **Questions for Artan.** Is Momentum licensed? Does the group have a house convention for
  Momentum port setup and substrate definition? What convergence threshold does he consider
  adequate for a filter at this frequency?
- **Risks.** R-02/R-03 (licence and Momentum availability), R-23 (treating circuit and EM models as
  equivalent), R-24 (simulation time).
- **Exit criteria.** **G7.**
- **Fallback route.** If Momentum is unavailable: state that clearly, do **not** substitute a
  different solver and call it Momentum, and consider an open planar solver (openEMS, or
  `scikit-rf`-based comparison) labelled honestly. The project remains valid with P7 marked
  "not available"; the CV claim then says "circuit and microstrip simulation" and omits EM.
- **Seminar material.** Seminar **Act VI** (beats 27–28), assets AS-26, AS-27: what EM simulation adds; the current
  distribution; the three models overlaid on one axis.

---

### P8 — Measurement and de-embedding strategy, and layout plan

> **The most important phase in the plan, and the one the first outline got wrong.**

- **Objective.** Decide *before layout freeze* how the filter will be measured and whether/how the
  fixture will be de-embedded — and put whatever copper that decision requires on the panel.
- **Why it exists.** De-embedding is not a post-processing choice. Every realistic method needs
  something physical: TRL needs a thru, a reflect and one or more lines *in the same medium*;
  the IEEE-370 2x-thru method needs a fabricated 2x-thru coupon; a fixture-model approach needs a
  characterizable launch. After fabrication, the achievable methods are exactly those the copper
  supports. Deciding this at the end of the project is how the stretch goal gets silently lost.
- **Required theory.** Block G at concept level (reference planes, what calibration does, what it
  cannot do), plus block H at concept level (fixture + DUT model, inverse networks, validity
  assumptions). Full block H depth is not needed to *choose*; it is needed to *execute* at P12.
- **Authoritative references.** Keysight **5968-5329**, *In-Fixture Measurements Using Vector
  Network Analyzers* — fixture selection, error sources, and the construction/characterization of
  in-fixture calibration standards when no commercial fixture exists; Keysight **5980-2784 /
  AN 1364-1** — de-embedding and embedding via S/T-parameter networks; Engen & Hoer 1979 — the
  original TRL formulation; IEEE Std 370-2020 — fixture characterization practice and the 2x-thru
  structure.
- **Engineering tasks.**
  1. Write the measurement chain out: VNA port → cable → connector → launch → feed line → DUT →
     feed line → launch → connector → cable → VNA port. **Name every reference plane.**
  2. Build the **de-embedding candidate inventory** with validity assumptions for each (see
     `measurement/measurement_plan.md`): calibrate-to-coax + simulated fixture model negation;
     TRL with on-board microstrip standards; IEEE-370 style 2x-thru; port extension / electrical
     delay only; thru-only bisection; "none".
  3. Check each candidate against what physically exists (kit, connectors, panel area, budget) and
     against what the student can defensibly execute at this level.
  4. Choose one — **or explicitly defer/decline**, which is a permitted outcome.
  5. Decide the coupon set and lay out the panel budget: board area, coupon count, extra connectors
     needed, cost, lead time.
  6. Artan Round 2 (`planning/questions_for_artan.md`).
  7. Decision-log the outcome with reasoning.
- **Expected outputs.** `measurement/measurement_plan.md` complete through the strategy section;
  coupon decision in `pcb/manufacturing_constraints/`; decision-log entries; Round 2 answers.
- **Validation method.** Every chosen method's assumptions written out and checked against reality.
  A method whose assumptions cannot be checked is not chosen.
- **Evidence to save.** The plan, the inventory with assumptions, the decision, Artan's answers.
- **Questions for Artan.** All of Round 2 — test structures on the panel? which calibration
  strategy is realistic with the group's kit? dedicated coupons? SOLT-to-connector-plane then
  de-embed, or TRL, or something else? Do **not** prejudge his answer.
- **Risks.** R-12/R-13 (calibration kit and calibration error), R-17 (fixture characterization not
  possible), R-18 (de-embedding instability), and the structural risk this phase exists to kill:
  fabricating a board that forecloses de-embedding.
- **Exit criteria.** **G8.**
- **Fallback route.** If no defensible de-embedding method is available, record "de-embedding not
  supported by available resources" *now*, scope the project to P11, and switch the seminar to
  version B. Still place a thru coupon on the panel if panel area allows — it is cheap, it enables
  a sanity check on the launches, and it keeps the option open.
- **Seminar material.** Seminar **Act VIII** (beats 33–38), assets AS-12, AS-13, AS-14, AS-15: why measured data is not
  the DUT; the fixture–DUT–fixture picture; `T_meas = T_L · T_DUT · T_R`; and the **required**
  honest-caveat beat about what inversion costs.

---

### P9 — PCB design review and fabrication

- **Objective.** Produce a manufacturable board — filter plus the coupons decided at G8 — and get
  it made.
- **Why it exists.** Hardware is what separates this from a simulation exercise.
- **Required theory.** None new. Manufacturing literacy rather than theory.
- **Authoritative references.** Connector manufacturer's recommended launch footprint (the
  datasheet is authoritative here, not a forum post); fabricator's published design rules;
  Keysight 5968-5329 for fixture construction guidance.
- **Engineering tasks.**
  1. Lay out the filter and all coupons; label each with silkscreen.
  2. Implement the launch footprint exactly per the connector datasheet, including ground-via
     pattern and any pad relief.
  3. DRC against the fabricator's actual rule set.
  4. Export Gerbers/ODB++, drill, and a fabrication drawing; **verify the exports in an independent
     viewer**, not only in the CAD tool.
  5. Design review DR-003 against a written checklist; mentor sign-off.
  6. Order; record cost and lead time.
- **Expected outputs.** `pcb/exports/`; `pcb/fabrication_notes/`; DR-003; order record.
- **Validation method.** DRC clean; independent viewer check; footprint matched dimension-by-dimension
  to the datasheet; every G8 coupon present.
- **Evidence to save.** Exports, DRC log, viewer screenshots, the review, the order confirmation,
  and later photographs of the delivered board.
- **Questions for Artan.** Will he review the layout before it is ordered? Is there a known-good
  launch footprint in the group already — this is worth more than any amount of theory.
- **Risks.** R-08 (fabrication delay — the single biggest schedule risk), R-09 (launch quality),
  R-07 (etch tolerance).
- **Exit criteria.** **G9.**
- **Fallback route.** If the in-house route is slow, use a commercial prototype service. **Order
  early and order spares** — two or three boards cost little more than one and protect against a
  soldering accident on the only unit. If fabrication will clearly miss the seminar date, switch
  the seminar to version C and continue the hardware track afterwards.
- **Seminar material.** Seminar **Act VII** (beat 29), asset AS-30: the photograph of real copper. Audiences respond to
  the physical object more than to any plot.

---

### P10 — VNA familiarization and calibration

- **Objective.** Calibrate a two-port VNA correctly and know exactly where the reference plane is.
- **Why it exists.** An uncalibrated or wrongly calibrated measurement is not data. Everything in
  P11 and P12 rests on this phase.
- **Required theory.** Block G (T51–T54): reference planes, systematic vs random error,
  what calibration removes and what it cannot, the method actually being used, Touchstone format.
- **Authoritative references.** Keysight VNA fundamentals material and the specific instrument's
  user guide; Keysight 5968-5329 (in-fixture context); Engen & Hoer 1979 if TRL is used.
- **Engineering tasks.**
  1. Instrument familiarization: frequency range, IF bandwidth, power, averaging, and how each
     affects noise and sweep time.
  2. Calibrate using the method chosen at G8; save and export the instrument state.
  3. **Verify** the calibration: measure a known standard not used in the calibration and compare
     against its expected response.
  4. Write down where the reference plane now is, in one unambiguous sentence.
  5. Record the full instrument configuration in the measurement log.
- **Expected outputs.** `measurement/calibration/` with state files, kit identification,
  verification plot and numbers; the reference-plane statement.
- **Validation method.** The verification measurement. A calibration that is not verified is not
  known to be good.
- **Evidence to save.** State export, kit record, verification data and plot, photographs of the
  setup (also a seminar asset).
- **Questions for Artan.** Lab induction requirements; which kit; any instrument quirks; is there a
  group calibration procedure to follow.
- **Risks.** R-11 (VNA access), R-12 (kit availability), R-13 (calibration error), R-25 (connector
  wear and torque discipline — use a torque wrench if one exists).
- **Exit criteria.** **G10.**
- **Fallback route.** If the lab VNA is unavailable, seek access via the department or another
  group. If no VNA is reachable in time: seminar version C, and the project is reported honestly
  as simulation-complete and measurement-pending. **Never present a simulated curve as measured.**
- **Seminar material.** Seminar **Act VII** (beats 30–31), assets AS-31, AS-11: what a VNA actually does, and the
  calibration idea — "the instrument measures itself first".

---

### P11 — Measurement and simulation-vs-measurement comparison

- **Objective.** Measure the filter properly, preserve the data, quantify repeatability, and
  compare all five models honestly.
- **Why it exists.** This phase *is* the core question.
- **Required theory.** Blocks C, E, G, held.
- **Authoritative references.** The Tier-3 papers with measured-vs-simulated comparisons (see
  `research/annotated_bibliography.md`) as **examples of how to report**, not as recipes. Keysight
  5968-5329 for in-fixture error sources.
- **Engineering tasks.**
  1. Measure S₁₁, S₂₁, S₁₂, S₂₂ over a span wider than the band of interest.
  2. **Repeatability: at least three disconnect/reconnect/remeasure cycles.** Quantify the spread.
  3. Commit raw Touchstone to `measurement/raw/` and never touch it again.
  4. Process in `measurement/processed/` with scripts, not by hand-editing.
  5. Build the five-way comparison table: analytical prediction / ideal circuit / microstrip
     circuit / Momentum / measured.
  6. Attribute each discrepancy to a named mechanism — substrate εr error, etch tolerance, launch
     reflection, conductor loss, dielectric loss, connector repeatability, model omission — with
     evidence. List the unattributable ones as unexplained.
  7. If possible, close the loop: re-simulate with the *measured* substrate εr or etched dimensions
     and see whether the discrepancy reduces. This is the strongest result the project can produce.
- **Expected outputs.** Raw and processed data; repeatability table; the five-way comparison table;
  the discrepancy analysis; result-register entries.
- **Validation method.** Repeatability bounds every claim. Attribution must be supported — a
  mechanism is named only if there is evidence it is responsible.
- **Evidence to save.** Everything. This is the project's evidentiary core.
- **Questions for Artan.** Does he agree with the attribution? Is the observed discrepancy typical
  for this substrate and frequency in his experience?
- **Risks.** R-10 (repeatability), R-14 (overclaiming attribution), R-22 (AI-generated explanation
  accepted without evidence).
- **Exit criteria.** **G11** then **G12**.
- **Fallback route.** If the filter is far off specification, that is still a result — the project
  asks how closely theory reproduces measurement, and "not very, and here is exactly why" answers
  it. Do not hide a bad board; analyze it.
- **Seminar material.** Seminar **Act VII beat 32 and Act IX beats 40–41**, assets AS-32, AS-33, AS-34: measured vs
  simulated; the five-way table; the honest "what surprised me" beat.

---

### P12 — Fixture characterization and de-embedding *(conditional)*

- **Objective.** Characterize the fixture by the method chosen at G8 and extract the DUT response —
  **only if** the result survives G13's checks.
- **Why it exists.** It is the stretch question and the seminar's intellectual climax. It is
  optional by design.
- **Required theory.** Block H in full (T55–T62): fixture+DUT model, T-parameters, inverse networks,
  validity assumptions, numerical stability and noise amplification.
- **Authoritative references.** Keysight 5980-2784 / AN 1364-1 (primary); Keysight 5968-5329
  (standards construction); Engen & Hoer 1979 (TRL); IEEE Std 370-2020 (modern fixture practice,
  2x-thru); `scikit-rf` IEEE-P370 implementation as an open, inspectable processing route.
- **Engineering tasks.**
  1. Measure the coupons.
  2. Extract the fixture description by the chosen method.
  3. De-embed; use correct, convention-stated S↔T conversions.
  4. Sanity checks: passivity (no |S| > 1), reciprocity for a passive reciprocal DUT, physically
     plausible phase and group delay, continuity across frequency.
  5. Stability check: perturb the input slightly and confirm the output does not change
     unreasonably. Naive matrix inversion amplifies noise — this check is not optional.
  6. Compare the de-embedded DUT against the Momentum model — which is itself a de-embedded,
     port-calibrated result. This comparison is the cleanest one in the whole project.
- **Expected outputs.** `measurement/deembedded/`; the validity check; the comparison;
  result-register entries.
- **Validation method.** **G13 in full.** Every assumption checked individually.
- **Evidence to save.** Coupon data, extracted fixture, de-embedded result, every check, the
  processing scripts.
- **Questions for Artan.** Does he consider the extraction defensible? Has he seen this failure
  mode before?
- **Risks.** R-17 (characterization not possible), R-18 (instability), R-19 (reporting a
  non-physical result because it looked plausible).
- **Exit criteria.** **G13** — which may legitimately conclude **"do not proceed."**
- **Fallback route.** Decline de-embedding, document precisely what was missing and what would
  have been required, and present the principle with a clearly-labelled simulated demonstration
  (seminar version B). A well-argued "we could not justify this" is a better portfolio item than a
  confident wrong number.
- **Seminar material.** Seminar **Act VIII beat 39**, asset AS-35: the de-embedded result, or — equally good — the
  honest account of why it was not attempted.

---

### P13 — Final engineering documentation and portfolio

- **Objective.** Turn the repository into something a supervisor, recruiter or thesis committee can
  read in twenty minutes.
- **Why it exists.** Undocumented work is unusable work, and the portfolio value is a stated
  project goal.
- **Engineering tasks.** Write the engineering report (problem → theory → design → simulation →
  fabrication → measurement → analysis → limitations). Finalize the result register. Write the
  limitations section honestly. Draft the CV line **from what exists**, not from what was planned.
  Update `HANDOFF.md` to its final state.
- **Expected outputs.** Final report; finalized registers; an accurate CV/portfolio paragraph.
- **Validation method.** Every number in the report traceable to a result-register ID and a file.
  Every claim traceable to a source or a measurement.
- **Risks.** R-14 (overclaiming), R-26 (copyright/licensing error in figures), R-27 (accidentally
  publishing proprietary lab information — re-check before the repository is ever made public).
- **Seminar material.** The report is the script's backbone.

---

### P14 — Seminar finalization

- **Objective.** Deliver a ~50 minute talk with ~10 minutes of questions to an undergraduate
  mathematics audience, supported only by claims the project can actually back.
- **Why it exists.** It is a separate deliverable with its own deadline, and its own failure modes.
- **Engineering tasks.** Execute S7–S10 in `seminar/SEMINAR_MASTER_PLAN.md`: speaker notes, timed
  rehearsal, cut and restructure on timing, Q&A preparation. Select the version (A/B/C) based on
  what actually exists by the freeze date.
- **Validation method.** Every slide has a row in `seminar/source_map.md` with a verified source or
  a project result ID. Timed rehearsal within budget. No unlabelled simulated-as-measured data.
- **Risks.** R-15 (seminar deadline before hardware — mitigated by the three versions), R-26
  (figure licensing), R-28 (over-equation-ing a maths audience that does not know RF).

---

## 4. Scope discipline

Explicitly **out of scope**, and to be refused even if interesting:

- Tunable/varactor-loaded filters, active filters, amplifiers, PA work.
- Multi-band, UWB, defected-ground structures, metamaterial or metasurface loading.
- Any novelty claim or publication attempt.
- Optimizer-driven design before the hand-designed baseline is understood and committed.
- Substrate characterization as a project in its own right (a *bounded* εr extraction from the
  measured board at P11 is in scope; building a material-characterization setup is not).
- A second filter, "for comparison", before the first one is measured and documented.

The three previous projects' failure mode was unbounded scope. **If a new idea arrives, it goes to
`planning/alternatives.md`, not into the plan.**

## 5. Document maintenance rules

| When | Update |
|---|---|
| Every working session | `PROJECT_STATE.md` |
| Every gate pass | `PROJECT_STATE.md`, `HANDOFF.md`, `planning/milestones.md` |
| Every decision | `planning/decision_log.md` |
| Every experiment | a new file from `templates/experiment_template.md` |
| Every number worth quoting | `results/result_register.md` |
| Every new source | `research/annotated_bibliography.md` + `research/source_hierarchy.md` |
| Every load-bearing claim | `research/claims_and_sources.md` |
| Every gate pass | `LEARNING_PATH_FOR_ME.md` — move the "YOU ARE HERE" marker |
