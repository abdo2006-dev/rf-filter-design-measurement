# rf-filter-design-measurement

**Design, EM simulation, fabrication, VNA characterization and de-embedding of a microstrip RF filter**

An undergraduate RF/microwave engineering project by Abdulrahman, B.Sc. Electrical and Computer
Engineering (year 2), Constructor University, Germany. Mentored by a PhD student in the university's
RF/microwave research group.

---

## Goal

Design a microstrip RF filter from first principles, simulate it at three levels of fidelity in
Keysight ADS, fabricate it as a printed circuit board, measure it on a vector network analyzer
(VNA), and explain every difference between the predicted and the measured response.

**The core question**

> How closely can a theoretically designed RF microstrip filter reproduce its intended response as
> we move from analytical design to circuit simulation, planar EM simulation, fabrication, and VNA
> measurement?

**The stretch question**

> How much of the gap between the measured response and the expected response is caused by the
> connectors, launches and fixtures, and how does de-embedding change the extracted device response?

**What "done" means.** The project is complete when it has: a defensible filter specification; a design
derived from established theory; ADS circuit and microstrip simulations; a manufacturable and fabricated
board; a two-port VNA measurement with the raw data preserved; a five-way comparison (theory, ideal
circuit, microstrip circuit, planar EM, measured) with each major discrepancy explained or listed as
unexplained. De-embedding is a stretch goal. A documented finding that de-embedding is not defensible
with the available equipment counts as completing that goal properly.

**What this project is not.** It makes **no novelty claim**. It is a learning and portfolio project
that is meant to be followed by a supervisor or a recruiter in about 20 minutes. It sets no filter
dimensions until the gates described below have passed.

---

## Current status

> **Phase 0 — scope and hardware-constraint capture. Blocked at gate G0.**
>
> No filter has been designed. No dimensions have been calculated. No measurement exists.

The project is waiting on five hardware facts from the mentor: the substrate (εr, loss tangent,
thickness), the fabricator's minimum trace width and gap, the VNA and its frequency range, the
available calibration kits, and the connector type. Each of these is recorded as **BLOCKED** in
[design/hardware_constraints.md](design/hardware_constraints.md) until it is answered. Nothing is
assumed to fill a blank.

| Milestone | Gate | Status |
|---|---|---|
| Project bootstrapped: plan, research basis, repository | — | done |
| Hardware constraints known | G0 | **blocked**, waiting on mentor |
| Filter topology chosen, specification defensible | G3 | not started |
| Ideal circuit meets specification | G5 | not started |
| Microstrip circuit meets specification and is manufacturable | G6 | not started |
| Measurement and de-embedding strategy frozen before layout | G8 | not started |
| PCB passes design review and is ordered | G9 | not started |
| VNA calibrated and verified | G10 | not started |
| Measurements taken, repeatability quantified | G11 | not started |
| Five-way comparison complete, discrepancies attributed | G12 | not started |

Full list: [planning/milestones.md](planning/milestones.md). No calendar dates are set. They will be set
once G0 reveals the fabrication lead time, because a schedule built on an unknown lead time would be
guesswork.

Read these two files first, in this order:

1. **[PROJECT_STATE.md](PROJECT_STATE.md)** — two-minute status snapshot.
2. **[HANDOFF.md](HANDOFF.md)** — everything a new reader or a new AI session needs to resume.

---

## How I will build it

The project runs in five stages. Each stage ends at a **decision gate**: objective evidence that the
next stage may start. Gates may be reordered in time, but they are never skipped. The full plan with
all 15 phases, their inputs, validation methods and fallback routes is in
[MASTER_PROJECT_PLAN.md](MASTER_PROJECT_PLAN.md).

### Stage 1 — Foundations (phases P1–P2, gates G1–G2)

Get fluent in the tools and the theory before designing anything.

- Learn Keysight ADS: transmission lines, first simulations, schematic and data-display workflow.
- Learn two-port networks: S-parameters, reference impedance, ABCD and T matrices, cascading, and
  conversions between them.
- Every concept is checked by doing it twice: by hand, and in ADS, with matching answers.

**Exit:** I can explain what S₁₁ and S₂₁ mean on a real simulation, and I can cascade two networks
by hand and get the same answer ADS gives.

### Stage 2 — Design (phases P3–P4, gates G3–G4)

Choose the filter from the constraints, not from habit.

- Score candidate topologies (low-pass or band-pass, stepped-impedance, coupled-line, hairpin, and
  others) against the measured constraints in a decision matrix.
- Write the filter specification. Every number in it is either a requirement with a source or a
  declared arbitrary choice with a reason. Nothing is copied from an example.
- Derive the lumped-element prototype analytically, with the order **derived** from the specification,
  not chosen. Verify the prototype's response against the specification before going further.

**Exit:** a specification and a topology that a supervisor can challenge, and a lumped prototype
whose response matches the specification.

### Stage 3 — Simulation ladder (phases P5–P7, gates G5–G7)

Simulate the same filter at three levels of fidelity. Each level must meet the specification before the
next one starts. The differences between levels are part of the results, so they are kept separate
rather than collapsed.

| Level | Tool | What it adds |
|---|---|---|
| Ideal circuit | ADS schematic simulation | Lumped or ideal transmission-line behaviour; tests the synthesis |
| Microstrip circuit | ADS transmission-line models on the real substrate | Real line widths, lengths and losses |
| Planar EM | ADS Momentum, **if licensed** | Full electromagnetic model of the layout |

For the planar EM level I will write down how the simulation is validated before I believe any of its
numbers. Momentum is a 2.5-D method-of-moments solver, so a convergence rule for a volumetric
solver does not carry over to it.

**Exit:** all three models meet the specification, and the EM validation procedure is written down.

### Stage 4 — Fabrication (phases P8–P9, gates G8–G9)

This is the step that is hardest to undo, so the measurement strategy is settled first.

- Decide how the board will be measured, and whether the fixtures and calibration structures it needs
  are part of the design. **G8 freezes this decision before layout begins.** Any of these must go
  on the same panel as the filter, and once the board is fabricated they cannot be added:
  - a TRL (thru-reflect-line) calibration set on the board;
  - a 2x-thru coupon for IEEE 370-style de-embedding;
  - a port-extension or electrical-delay check, reported as the crude method it is.
- Lay out the board to the fabricator's minimum-gap and minimum-width limits, with the measurement
  structures included.
- Pass a written design review (DR-001), then order the PCB.

**Exit:** a manufacturable layout, a frozen measurement strategy, and an order placed.

### Stage 5 — Measurement and analysis (phases P10–P12, gates G10–G13)

- Learn the VNA. Calibrate with the available kit, then measure a known verification standard that was
  not used in the calibration and compare it with its expected response. An unverified calibration
  supports no claim.
- Measure the board and store the raw Touchstone files. Raw data is **append-only**: it is never
  overwritten, and every processed result links back to it.
- Repeat the measurement, and quantify the repeatability. Every comparison carries that uncertainty.
- Build the five-way comparison table. For each discrepancy, name a mechanism only when there is
  evidence for it: substrate εr error, etch tolerance, launch reflection, conductor loss, dielectric
  loss, connector repeatability, or a model omission. Anything that cannot be attributed is listed as
  unexplained.
- Close the loop where possible: re-simulate with the measured substrate or etched dimensions, and
  see whether the discrepancy shrinks.
- **Conditional (P12):** characterize the fixture and attempt de-embedding, **only if** the method
  chosen at G8 is defensible at G13. If it is not, the project says so and reports the measured result
  with the fixture included.

**Exit:** a measured response with uncertainty, a five-way comparison, and a discrepancy analysis in
which every explanation has evidence.

### A separate track: the seminar

A ~50-minute talk, with questions, for an undergraduate mathematics audience. It is built in parallel
and does not depend on the hardware. Most of it, including the theory, the speaker notes and the Q&A
preparation, can be finished before the board exists. The plan is in
[seminar/SEMINAR_MASTER_PLAN.md](seminar/SEMINAR_MASTER_PLAN.md). Which of three versions (A, B, C) is
delivered depends on what the evidence supports at the content freeze.

---

## Tools and what is still unconfirmed

| Item | Status |
|---|---|
| Keysight ADS, as the design environment | **Confirmed**, as the mentor's recommendation |
| ADS Momentum (planar EM) | **Unconfirmed**. If it is not licensed, the planar-EM level is dropped and the report says so |
| VNA, frequency range and calibration kits | **Blocked**, waiting on the mentor |
| Substrate (εr, tanδ, thickness, copper weight) | **Blocked**, waiting on the mentor |
| Fabricator, minimum trace width and gap, lead time | **Blocked**, waiting on the mentor |
| Connector type and launch footprint | **Blocked**, waiting on the mentor |
| Filter class, topology, centre frequency, order | **Blocked**, decided at G3 from the constraints above |

The full list of open decisions is in [planning/decision_log.md](planning/decision_log.md), and the
requirements that are still blocked are in [planning/requirements.md](planning/requirements.md).

---

## Evidence standard

- **No invented data.** No measured value exists until hardware is measured. No simulated value exists
  until a simulation is run and its file is committed.
- **Simulated is never presented as measured.** Each result is labelled with where it came from.
- **Every decision is recorded** with its reasoning in the decision log, dated, including the
  decisions an AI assistant proposed.
- **Every load-bearing technical claim has a source** in
  [research/claims_and_sources.md](research/claims_and_sources.md).
- **Gates are not skipped to meet a date.** If a date cannot be met, the deliverable shrinks. The
  evidence standard does not.
- **Coursework comes first.** If the project starts to cost coursework, it freezes at its current gate.

---

## Core references

- D. M. Pozar, *Microwave Engineering*, 4th ed., Wiley, 2011 — transmission lines, S-parameters,
  ABCD matrices, filter design by insertion loss.
- J.-S. Hong and M. J. Lancaster, *Microstrip Filters for RF/Microwave Applications*, 2nd ed., Wiley,
  2011 — microstrip realization: coupled lines, hairpin and stepped-impedance filters.
- IEEE Std 370-2020 — fixture de-embedding practice.

Metadata only is kept here. Full records and verification status are in
[research/annotated_bibliography.md](research/annotated_bibliography.md) and
[research/verification_log.md](research/verification_log.md).

---

## Repository map

```
README.md                     this file
MASTER_PROJECT_PLAN.md        phase-by-phase plan (P0-P14) and decision gates (G0-G13)
PROJECT_STATE.md              short live status
HANDOFF.md                    session-recovery document
LEARNING_PATH_FOR_ME.md       what to study now, and what to ignore
PERSISTENCE.md                how this repository is backed up and pushed to GitHub

planning/      requirements, milestones, decision log, risks, alternatives, mentor questions
research/      source hierarchy, annotated bibliography, claim-to-source map, verification log
theory/        theory dependency map, with a "you understand this when you can..." test per topic
design/        hardware constraints, filter specification, topology selection, calculations
ads/           ADS learning exercises, circuit model, microstrip model, Momentum model
pcb/           manufacturing constraints, fabrication notes, exports
measurement/   measurement plan, calibration records, raw / processed / de-embedded data
results/       result register, tables, figures
seminar/       seminar master plan, slide outline, source map, asset register, speaker notes
templates/     experiment, decision, result and source templates
```

## Status vocabulary

Every statement in this repository carries one of these labels:

| Status | Meaning |
|---|---|
| **CONFIRMED** | Evidence-backed or finalized. Needs a reference, a measurement, or an explicit decision. |
| **PROVISIONAL** | Current working choice, expected to be revisited. |
| **OPTION** | A possible branch not currently chosen. |
| **BLOCKED** | Cannot proceed until missing information arrives. |
| **SUPERSEDED** | Historically relevant, no longer current. |

A brainstorming suggestion never becomes CONFIRMED on its own. Promotion to CONFIRMED requires an
entry in [planning/decision_log.md](planning/decision_log.md).

## Hard rules for this repository

1. **No invented data.** No measured value exists until hardware is measured. No simulated value exists
   until a simulation is run and its file is committed.
2. **No copyrighted textbooks, publisher PDFs, or paywalled papers in this repository.** Metadata only.
   See [research/source_hierarchy.md](research/source_hierarchy.md).
3. **Raw measurement data is append-only.** Never overwrite a file in `measurement/raw/`.
4. **No proprietary lab information.** Equipment serial numbers, internal network paths, licence keys,
   unpublished group results and anything a supervisor gave in confidence stay out.
5. **Every load-bearing technical claim has a source** in
   [research/claims_and_sources.md](research/claims_and_sources.md).
6. **Provisional stays provisional.** Nothing about frequency, substrate, order, topology, response
   type, calibration method or de-embedding method is settled yet.

## Licence

Project documentation: © 2026 Abdulrahman. All rights reserved; no licence is granted for reuse.
The repository is public so it can be read and reviewed. Cited third-party works remain the property of
their respective rights holders and are referenced by metadata only.
