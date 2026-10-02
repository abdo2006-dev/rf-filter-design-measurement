# HANDOFF

*Read this file to resume the project from zero context. Update it after every major milestone
and at the end of every working session.*

**Handoff version:** 1.0
**Written:** 2026-10-02
**Written by:** Bootstrap session (architect / librarian / documentation manager role)

---

## Purpose

Design a microstrip RF filter from established filter theory, simulate it in Keysight ADS at
circuit, microstrip and planar-EM level, fabricate it as a PCB, measure it on a two-port VNA,
and quantitatively explain the differences between every stage. Optionally characterize and
de-embed the test fixture.

## Career / learning goal

The student is a second-year B.Sc. Electrical and Computer Engineering student at Constructor
University (Germany) targeting RF/microwave engineering, telecommunications and semiconductor
roles — RF hardware internships, research programmes such as Mitacs, a strong Bachelor thesis,
and possibly graduate study in RF/communications.

Two earlier projects (CST simulation of a varactor-tuned reflectarray; a literature review on
flexible intelligent metasurfaces) became too open-ended. **This project is deliberately
bounded.** Scope discipline is a requirement, not a preference.

The student is a **beginner in ADS** and does **not** yet have enough RF theory to independently
judge every technical recommendation an AI makes. Therefore: authoritative references matter,
validation matters, screenshots are not evidence, and every engineering decision needs recorded
reasoning.

## Broad confirmed scope

**CONFIRMED.** "Design, EM Simulation, Fabrication, VNA Characterization and De-embedding of a
Microstrip RF Filter."

Progression: theory → ADS orientation → filter synthesis → microstrip implementation → circuit
simulation → planar EM simulation → PCB fabrication → VNA measurement → simulation-vs-measurement
comparison → optional fixture de-embedding.

## Current exact implementation

**None.** No filter exists, on paper or otherwise.

The following are **PROVISIONAL candidates only** and must not be treated as chosen:

| Item | Candidates | Status |
|---|---|---|
| Topology | stepped-impedance LPF / parallel-coupled BPF / hairpin BPF | OPTION (matrix unscored) |
| Response | Butterworth / Chebyshev / other | OPTION |
| Order | — | OPTION |
| Centre frequency | — | BLOCKED on substrate + VNA range |
| Substrate | — | BLOCKED on Artan |
| Connector | — | BLOCKED on Artan |
| Calibration | SOLT / TRL / ECal / other | BLOCKED on available kit |
| De-embedding | fixture-model negation / TRL to microstrip plane / IEEE-370 2x-thru / none | BLOCKED on G8 |

A third-order parallel-coupled Chebyshev bandpass filter near ~2.4 GHz was discussed in
conversation. It is **not** the design. It is one unscored candidate. 2.4 GHz in particular must
not be adopted because it is familiar — see `planning/decision_log.md` D-002.

## Confirmed constraints

See `PROJECT_STATE.md` → "Confirmed constraints". Short version: ADS is the tool, the full
design→measure chain is the deliverable, the student is a beginner, the project must fit around
coursework, and no novelty is claimed.

## Current topology / specifications

Nothing specified. `design/filter_specification.md` is a populated **template with blanks**, not
a specification. `design/topology_selection.md` holds a 14-criterion matrix in which 8 criteria
are scored and 6 are marked BLOCKED pending G0.

## Completed phases

- **Bootstrap** (this session): research basis, repository, plan, gates, theory map, risks,
  topology matrix, seminar system, mentor questions.
- **P0** is *in progress* — it completes when gate G0 passes.

## Current evidence

- `research/` — curated source stack: 2 Tier-1 textbooks, 4 Tier-2 Keysight resources,
  1 measurement standard, 8 Tier-3 papers, each with verification status.
- `research/verification_log.md` — exactly what was and was not verifiable, and why.
- **No engineering evidence exists yet.** No `.ds`, no `.s2p`, no photograph, no plot.

## Known results

None.

## Known failures

- This session **could not create a GitHub repository.** The session's GitHub integration is
  bound to two unrelated pre-configured repositories and `POST /user/repos` returns
  403 "Resource not accessible by integration". Fallback used: local git repository + verified
  git bundle + zip archive. See `PERSISTENCE.md`.
- This session **could not open any PDF or DOI directly.** The container's egress policy denies
  `www.keysight.com`, `api.crossref.org`, `doi.org`, `arxiv.org`, `openlibrary.org`,
  `ieeexplore.ieee.org` and others (HTTP 403 on CONNECT). Only server-side web search was
  available. Every source is therefore classified honestly in
  `research/verification_log.md`; several are PARTIALLY VERIFIED rather than VERIFIED.
  **A future session with network access should re-verify them and upgrade the statuses.**

## Open questions

1. What substrate will actually be used, with what datasheet εr and tanδ, at what thickness?
2. What are the fabricator's minimum trace width, minimum gap and etch tolerance?
3. Which VNA, what frequency range, which calibration kits, which connector type?
4. Is ADS Momentum licensed and available?
5. Does the mentor prefer a low-pass or band-pass filter for the educational goal?
6. Should calibration/de-embedding test structures be placed on the same fabrication panel?
   (This must be answered **before** layout freeze, gate G8.)

## Artan decisions

**None recorded yet.** Artan is a PhD student in the research group; his Master's thesis was
*"GaN MMIC Load-Modulated Balanced Amplifier Design for Ka-Band Communication Systems"*. He
advised against jumping into advanced PA research and suggested starting with RF fundamentals
and a practical filter / transmission-line / measurement project — including the
`fixture → DUT → fixture` cascaded-matrix idea that became this project's stretch goal.

Record every answer he gives in `planning/decision_log.md`, and date it.

## Lab resources

**Unknown.** Do not assume any instrument, kit, substrate or fabrication service exists until
confirmed. See `design/hardware_constraints.md` — it is a form to be filled in, and every field
is currently BLOCKED.

## Important references

Full records in `research/annotated_bibliography.md`. The four that carry the most weight:

- Pozar, *Microwave Engineering*, 4th ed., Wiley 2011 — transmission lines, S-parameters,
  ABCD matrices, insertion-loss filter design.
- Hong & Lancaster, *Microstrip Filters for RF/Microwave Applications*, 2nd ed., Wiley 2011 —
  microstrip filter realization, coupled lines, hairpin, stepped impedance.
- Keysight app note **5980-2784** (AN 1364-1), *De-Embedding and Embedding S-Parameter Networks
  Using a Vector Network Analyzer* — the de-embedding authority.
- Keysight app note **5968-5329**, *In-Fixture Measurements Using Vector Network Analyzers* —
  fixture design and in-fixture calibration standards.

## Current files

52 markdown documents, ~5,560 lines. Directory map in `README.md`. Nothing binary, nothing
copyrighted, no data.

## Current phase

**P0 — Scope and hardware-constraint capture**, blocked at gate **G0**.

## Exactly what to do next

1. Send the Round 1 message in `planning/questions_for_artan.md` to Artan. Unedited if possible —
   it is deliberately short and grouped.
2. Record his answers in `design/hardware_constraints.md` and `planning/decision_log.md`.
3. Score the 6 BLOCKED criteria in `design/topology_selection.md`.
4. Only then open gate G0 and start P1.

**Do not** calculate line widths, gaps, coupling coefficients, resonator lengths or a centre
frequency before G0 and G3 pass. See `MASTER_PROJECT_PLAN.md` → "Stop line".
