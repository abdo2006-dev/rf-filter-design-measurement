# READING QUEUE

*The anti-distraction mechanism. Interesting things go here and are read when a gate needs them.*

**Rule.** Nothing is read because it is interesting. Everything is read because a gate needs it.
If something is genuinely interesting but no gate needs it, it goes in §3 and waits — possibly
forever, and that is a success, not a loss.

---

## 1. Read now (P0 → G1)

Minimal on purpose. The current block is transmission lines.

| # | What | Source | Why now | Done |
|---|---|---|---|---|
| 1 | Transmission line theory: wave equations, terminated lossless line | T1-01 Pozar §2.1–2.3 | Theory block B; prerequisite for the first ADS experiment | ☐ |
| 2 | Impedance transformation, quarter-wave behaviour | T1-01 Pozar §2.5–2.7 | EXP-003 | ☐ |
| 3 | Transmission-line chapter + its ADS workspaces | T2-04 Learning Kit | The ADS-side companion to items 1–2 | ☐ |
| 4 | **Hong & Lancaster contents page** — fill the chapter numbers into `annotated_bibliography.md` T1-02 | T1-02 | A load-bearing source currently has blank section pointers | ☐ |

**Estimated: 8–12 hours.** Do not add to this list.

## 2. Read when the gate arrives

| Gate | What to read | Source |
|---|---|---|
| G2 | The scattering matrix | T1-01 §4.3 |
| G2 | ABCD matrices + S↔ABCD conversion tables, **noting the convention** | T1-01 §4.4 |
| G2 | The S/T-parameter treatment used for de-embedding | T2-02 §review sections |
| G3 | Filter design by the insertion-loss method | T1-01 §8.3 |
| G3 | Filter transformations | T1-01 §8.4 |
| G3 | Basic filter concepts, lowpass prototype | T1-02 *(chapter TBD)* |
| G3 | Topology survey — skim all three candidates only | T1-02 *(chapters TBD)* + A3, A7, A10 |
| G4 | Prototype element tables, cross-check | T1-01 §8.3 + one independent table |
| G6 | Microstrip | T1-01 §3.8 |
| G6 | Microstrip lines, discontinuities, coupled lines | T1-02 *(chapters TBD)* |
| G6 | Microstrip examples, LineCalc | T2-04 |
| G7 | **Momentum mesh/convergence settings — in the installed version's help** | T2-05 |
| G7 | Planar EM workflow + the coupled-line BPF case study | T2-01 |
| G8 | **In-fixture measurement, fixture construction, building standards** | T2-03 |
| G8 | **De-embedding and embedding S-parameter networks — all of it** | T2-02 |
| G8 | De-embedding method families in microstrip | A5 |
| G8 | 2x-thru practice (secondary, standard is paywalled) | T4-04, T4-01 |
| G10 | The actual VNA's user guide, calibration section | instrument documentation |
| G10 | TRL original, **if** TRL is chosen | A9 |
| G12 | Reporting structure for measured-vs-simulated | A1, A2, A3 |
| G13 | 2x-thru implementation, if used | T4-01 scikit-rf |

## 3. Deferred — interesting, not needed

*Where curiosity goes to be safely parked. Revisit only after P13.*

- Hong & Lancaster's advanced chapters: HTS filters, micromachined filters, tunable/ferroelectric
  filters, UWB filters, RF MEMS. **Directly adjacent to the student's previous over-scoped
  projects. Actively avoid until the project is finished.**
- Coupled-resonator coupling-matrix synthesis in depth.
- Space-mapping and optimization-based filter design.
- Defected ground structures (appears in A10, A7 variants) — out of scope.
- Balanced/differential filters (A1) — out of scope.
- Multiline TRL and thru-free calibration variants.
- Substrate material characterization as a discipline.
- Momentum RF vs Microwave mode internals.
- Signal-integrity applications of IEEE 370 beyond fixture de-embedding.

## 4. Rejected

| Source | Why rejected |
|---|---|
| Generic web FR-4 permittivity figures | Unsourced and self-propagating. The real datasheet replaces them at G0. See claims S-01…S-03. |
| Additional 2.4 GHz filter papers | **Frequency is not a selection criterion.** Selecting on frequency was explicitly identified as a trap — it would make 2.4 GHz feel confirmed when it is not. |
| Further stepped-impedance LPF student papers | A8 and A10 already cover the topology. More of the same adds nothing. |
| Textbook PDFs found on file-sharing sites | Copyright. Use institutional access. |

---

## Adding to this queue

A new item needs three things: the gate that requires it, the specific question it answers, and
its tier. Without all three it goes in §3.

> **If the reading queue is growing faster than the project, the project is drifting.** That is the
> single clearest early warning this repository can give — it is risk R-15, and this file is the
> detector.
