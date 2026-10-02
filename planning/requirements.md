# REQUIREMENTS

*What the project must deliver, separated from what the filter must do. The second list is almost
entirely empty, and that is the current state of the project.*

---

## 1. Project requirements (CONFIRMED)

These come from the student's situation, not from engineering, and they are the real constraints.

| ID | Requirement | Why | Verification |
|---|---|---|---|
| PR-01 | Must be completable alongside full-time coursework | Two previous projects failed on scope | Phase estimates fit the available hours; `alternatives.md` absorbs new ideas |
| PR-02 | Must have a definite end | Same | Definition of done, §3 |
| PR-03 | Must produce ADS competence, demonstrably | Stated career asset | Committed ADS workspaces at P1, P5, P6, P7 |
| PR-04 | Must reach physical hardware and real measurement | What separates this from a simulation exercise | Measured Touchstone files in `measurement/raw/` |
| PR-05 | Must be documented so a supervisor or recruiter can follow it in ~20 min | Portfolio goal | P13 report + registers |
| PR-06 | Must be recoverable by a new person or AI session from the repository alone | The student works with AI assistance across sessions | `HANDOFF.md` + `PROJECT_STATE.md` |
| PR-07 | Every engineering decision must have recorded reasoning | The student cannot yet independently judge every AI recommendation | `decision_log.md` |
| PR-08 | Every load-bearing claim must have a source | Same | `research/claims_and_sources.md` |
| PR-09 | No invented data, ever | Integrity, and the work is going on a CV | Status vocabulary; empty R-group in claims file |
| PR-10 | No copyright or licensing violation | Repository will be shown to others | `source_hierarchy.md` copyright rules |
| PR-11 | No proprietary lab information published | Mentor/group trust | Pre-publication review, risk R-27 |
| PR-12 | Must support a ~1 h seminar deliverable independent of hardware timing | Separate deadline, separate failure mode | Three seminar versions |
| PR-13 | Must make **no** novelty claim | Honesty; novelty is not the goal | Stated in README, research_basis, report |

## 2. Filter requirements

**Status: BLOCKED. Almost nothing here is known.**

This section is the project's actual front line. It is deliberately left as a form.

| ID | Requirement | Value | Status |
|---|---|---|---|
| FR-01 | Filter class (LPF / BPF / other) | — | **BLOCKED** — D-003, mentor Round 1 Q5 |
| FR-02 | Topology | — | **BLOCKED** — D-003, gate G3 |
| FR-03 | Response type | — | **BLOCKED** — D-004 |
| FR-04 | Order | — | **BLOCKED** — must be *derived* at G4, not chosen |
| FR-05 | Centre or cut-off frequency | — | **BLOCKED** — D-002. **Not 2.4 GHz by default.** |
| FR-06 | Bandwidth / fractional bandwidth | — | **BLOCKED** |
| FR-07 | Passband ripple or flatness | — | **BLOCKED** |
| FR-08 | Passband insertion loss budget | — | **BLOCKED** — depends on substrate tanδ |
| FR-09 | Passband return loss target | — | **BLOCKED** |
| FR-10 | Stopband attenuation at a stated frequency | — | **BLOCKED** — drives FR-04 |
| FR-11 | Port impedance | 50 Ω | **PROVISIONAL** — near-certain, but it follows from the VNA and connector, so it is confirmed at G0 like everything else |
| FR-12 | Frequency range over which the spec is claimed | — | **BLOCKED** — bounded by the VNA range |
| FR-13 | Maximum board size | — | **BLOCKED** — fabricator and connector constraints |
| FR-14 | Minimum manufacturable feature (trace / gap) | — | **BLOCKED** — G0. **The single most design-determining unknown.** |

> **FR-11 note.** Even 50 Ω is marked PROVISIONAL rather than CONFIRMED. It is almost certainly
> correct, but the discipline matters more than the certainty: if 50 Ω can be assumed without a
> decision-log entry, so can FR-05, and that is how 2.4 GHz would become "confirmed".

## 3. Definition of done

The project is **successful** when all of the following exist:

1. ☐ A defensible filter specification *(G3)*
2. ☐ A design synthesized from established theory *(G4)*
3. ☐ ADS simulation *(G5, G6)*
4. ☐ Physical microstrip implementation *(G6)*
5. ☐ Momentum planar EM simulation, **if available** *(G7)*
6. ☐ A manufacturable PCB *(G9)*
7. ☐ A fabricated board *(P9)*
8. ☐ Two-port VNA measurement *(P11)*
9. ☐ Raw S-parameter data preserved *(G11)*
10. ☐ Five-way comparison: theory / ideal circuit / microstrip / EM / measured *(G12)*
11. ☐ Major discrepancies explained *(G12)*

**Stretch, not required:** fixture characterization and de-embedding *(G13)*. A documented
"de-embedding not defensible with available resources" **counts as completing the stretch goal
properly**, not as failing it.

**Separate deliverable:** the seminar, in whichever of versions A/B/C the evidence supports.

## 4. Non-requirements

Stated so they cannot creep in:

- Publication, novelty, or state-of-the-art performance.
- Optimal, minimum-size, or high-performance filter design.
- A second filter for comparison.
- Substrate characterization as an end in itself.
- Automated/scripted design flows.
- Anything involving amplifiers, tuning elements, or active devices.
