# MILESTONES

*Gate-anchored, not date-anchored. Dates are set once G0 reveals the lead times that actually
drive the schedule.*

---

## Status board

| # | Milestone | Gate | Status | Date |
|---|---|---|---|---|
| M0 | Project bootstrapped: plan, research basis, repository | — | ✅ **done** | 2026-10-02 |
| M1 | Hardware constraints known | G0 | ⬜ **blocked** — Artan Round 1 | — |
| M2 | First transmission-line simulation understood | G1 | ⬜ | — |
| M3 | S-parameters and cascaded two-ports understood | G2 | ⬜ | — |
| M4 | Topology chosen, specification defensible | G3 | ⬜ | — |
| M5 | Lumped prototype derived and verified | G4 | ⬜ | — |
| M6 | Ideal circuit model meets specification | G5 | ⬜ | — |
| M7 | Microstrip model meets specification, manufacturable | G6 | ⬜ | — |
| M8 | Momentum model validated | G7 | ⬜ | — |
| M9 | **Measurement + de-embedding strategy frozen** | **G8** | ⬜ | — |
| M10 | PCB passes design review, ordered | G9 | ⬜ | — |
| M11 | Board in hand | — | ⬜ | — |
| M12 | VNA calibrated and verified | G10 | ⬜ | — |
| M13 | Measurements taken, repeatability quantified | G11 | ⬜ | — |
| M14 | Five-way comparison complete, discrepancies attributed | G12 | ⬜ | — |
| M15 | De-embedding go/no-go decided | G13 | ⬜ | — |
| M16 | Engineering report complete | — | ⬜ | — |
| M17 | Seminar delivered | — | ⬜ | — |

## Seminar track (parallel)

| # | Milestone | Needs | Status |
|---|---|---|---|
| SM1 | Audience + thesis fixed (S0) | nothing | ⬜ |
| SM2 | Narrative architecture (S1) | nothing | ⬜ |
| SM3 | Theory slides + original diagrams (S2) | G2 | ⬜ |
| SM4 | Circuit results inserted (S3) | G5 | ⬜ |
| SM5 | Momentum results inserted (S4) | G7 | ⬜ |
| SM6 | Hardware + measurement inserted (S5) | G11 | ⬜ |
| SM7 | De-embedding inserted, if defensible (S6) | G13 | ⬜ |
| SM8 | Speaker notes (S7) | — | ⬜ |
| SM9 | Timed rehearsal (S8) | — | ⬜ |
| SM10 | Cut and restructure (S9) | — | ⬜ |
| SM11 | Q&A preparation (S10) | — | ⬜ |

**Key fact about the seminar schedule:** SM1–SM4 and SM8–SM11 need **no hardware at all**. Roughly
two thirds of the talk can be finished before the board exists. That is deliberate, and it is what
makes the seminar deadline survivable.

## The critical path

```
Artan Round 1  →  G0  →  G3  →  G6  →  G8  →  G9  →  [FABRICATION LEAD TIME]  →  G10 → G11 → G12
     ↑                                                          ↑
  blocking now                                      the schedule-dominating unknown
```

Two observations:

1. **The project is currently blocked on one message.** Everything downstream waits on Artan
   Round 1. Sending it is the highest-value action available, and it costs nothing.
2. **Fabrication lead time dominates the schedule**, and it is unknown until G0 answers it. That is
   why lead time is a G0 evidence item and not an afterthought.

The de-embedding branch (G13) is explicitly **off** the critical path. The project completes
without it.

## Scheduling rules

1. **No dates until G0.** A schedule built on an unknown lead time is fiction.
2. **Fabrication is ordered as early as G9 permits** — it is the only step whose duration cannot be
   compressed by working harder.
3. **The seminar content freeze is a real date.** When it arrives, version A/B/C is chosen on what
   exists (D-011), and the hardware track continues afterwards regardless.
4. **No gate is skipped to meet a date.** If a date cannot be met, the deliverable shrinks — the
   evidence standard does not.
5. **Coursework wins.** This is risk R-15 with critical impact. If the project starts costing
   coursework, it freezes at the current gate.

## Log

| Date | Event |
|---|---|
| 2026-10-02 | M0 complete. Bootstrap: 15 phases, 14 gates, 29 risks, theory map, topology matrix (8/14 scored), seminar system, 23 sources. Repository created locally; GitHub creation blocked (D-007). Next action: Artan Round 1. |
