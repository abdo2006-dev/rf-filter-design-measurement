# rf-filter-design-measurement

**Design, EM Simulation, Fabrication, VNA Characterization and De-embedding of a Microstrip RF Filter**

Undergraduate RF/microwave engineering project — Abdulrahman, B.Sc. Electrical and Computer
Engineering (year 2), Constructor University, Germany.

---

## What this repository is

This is the **persistent source of truth** for the project. It holds the plan, the research
basis, the theory roadmap, the design record, the measurement record, and the seminar system.
It is a *documentation and traceability* repository first; simulation and measurement artefacts
are added as they are produced.

It is not a code project. There is nothing to build or run.

## Project status

> **Phase 0 — Scope and hardware-constraint capture.**
> No filter has been designed. No dimensions have been calculated. No measurement exists.

Read these two files first, in this order:

1. **[PROJECT_STATE.md](PROJECT_STATE.md)** — two-minute status snapshot.
2. **[HANDOFF.md](HANDOFF.md)** — everything a new person or new AI session needs to resume.

Then, depending on who you are:

| You are | Read |
|---|---|
| The student (me) | [LEARNING_PATH_FOR_ME.md](LEARNING_PATH_FOR_ME.md) |
| A supervisor / mentor | [MASTER_PROJECT_PLAN.md](MASTER_PROJECT_PLAN.md), [planning/questions_for_artan.md](planning/questions_for_artan.md) |
| A future AI session | [HANDOFF.md](HANDOFF.md), then [planning/decision_log.md](planning/decision_log.md) |
| A recruiter / reviewer | [MASTER_PROJECT_PLAN.md](MASTER_PROJECT_PLAN.md), [results/result_register.md](results/result_register.md) |

## Core engineering question

> How closely can a theoretically designed RF microstrip filter reproduce its intended response
> as we move from analytical design to circuit simulation, planar EM simulation, fabrication,
> and VNA measurement?

**Stretch question**

> How much of the discrepancy between the measured response and the expected filter response is
> caused by connectors / launches / fixtures, and how does de-embedding change the extracted DUT
> response?

This is an engineering-learning and portfolio project. It makes **no novelty claim**.

## Repository map

```
README.md                     this file
MASTER_PROJECT_PLAN.md        phase-by-phase plan (P0-P14) and decision gates (G0-G13)
PROJECT_STATE.md              short live status
HANDOFF.md                    session-recovery document
LEARNING_PATH_FOR_ME.md       what to study NOW, what to ignore
PERSISTENCE.md                how this repo is backed up / how to push it to GitHub

planning/      requirements, milestones, decision log, risks, alternatives, mentor questions,
               bootstrap self-review
research/      source hierarchy, annotated bibliography, claim-to-source map, verification log
theory/        theory dependency map (T1-T62) with "you understand this when you can..." tests
design/        hardware constraints, filter specification, topology selection, calculations
ads/           ADS learning exercises, circuit model, microstrip model, Momentum model
pcb/           manufacturing constraints, fabrication notes, exports
measurement/   measurement plan, calibration records, raw / processed / de-embedded data
results/       result register, tables, figures
seminar/       seminar master plan, slide outline, source map, asset register, speaker notes
templates/     experiment / decision / result / source templates
```

## Status vocabulary

Every statement in this repository carries one of these:

| Status | Meaning |
|---|---|
| **CONFIRMED** | Evidence-backed or finalized. Needs a reference, a measurement, or an explicit decision. |
| **PROVISIONAL** | Current working choice, expected to be revisited. |
| **OPTION** | A possible branch not currently chosen. |
| **BLOCKED** | Cannot proceed until missing information arrives. |
| **SUPERSEDED** | Historically relevant, no longer current. |

A brainstorming suggestion never becomes CONFIRMED on its own. Promotion to CONFIRMED requires
an entry in [planning/decision_log.md](planning/decision_log.md).

## Hard rules for this repository

1. **No invented data.** No measured value exists until hardware is measured. No simulated value
   exists until a simulation is run and its file is committed.
2. **No copyrighted textbooks, publisher PDFs, or paywalled papers in this repository.** Metadata
   only. See [research/source_hierarchy.md](research/source_hierarchy.md).
3. **Raw measurement data is append-only.** Never overwrite a file in `measurement/raw/`.
4. **No proprietary lab information.** Equipment serial numbers, internal network paths, licence
   keys, unpublished group results and anything a supervisor gave in confidence stay out.
5. **Every load-bearing technical claim has a source** in
   [research/claims_and_sources.md](research/claims_and_sources.md).
6. **Provisional stays provisional.** Nothing about frequency, substrate, order, topology,
   response type, calibration method or de-embedding method is settled yet.

## Licence

Project documentation: © 2026 Abdulrahman. All rights reserved for now; no licence granted.
Cited third-party works remain the property of their respective rights holders and are
referenced by metadata only.
