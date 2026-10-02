# PROJECT_STATE

*Short by design. If this file takes more than two minutes to read, it is too long.*

**Last updated:** 2026-10-02
**Updated by:** Bootstrap session (project architect / research librarian role)

---

## Current phase

**P0 — Scope and hardware-constraint capture.**

## Current objective

Get the five blocking hardware facts from Artan (substrate, fabrication limits, VNA,
calibration kit, connector) so the topology decision matrix can be scored and a filter
specification can be written.

## Confirmed constraints

- **CONFIRMED** Software: Keysight ADS is the design environment. (Mentor's recommendation;
  my own learning goal.)
- **CONFIRMED** Deliverable chain: analytical design → circuit sim → microstrip sim →
  planar EM sim → PCB → two-port VNA measurement → comparison.
- **CONFIRMED** Student skill level: ADS beginner; RF theory at second-year level.
- **CONFIRMED** The project must be completable alongside full-time coursework.
- **CONFIRMED** No novelty claim is required or attempted.

*Nothing else is confirmed. In particular: no frequency, no substrate, no order, no response
type, no topology, no calibration method, no de-embedding method.*

## Confirmed design decisions

**None.** See `planning/decision_log.md` — D-001 to D-006 are all open.

## Completed

- Bounded research pass (Tier 1 / Tier 2 / Tier 3 source stack assembled and classified).
- Repository bootstrap: plan, gates, theory map, risk register, topology matrix, seminar system.

## Evidence available

- Source stack with verification status: `research/verification_log.md`.
- No simulation results. No measurement results. No hardware.

## Current results

**None.** No number in this repository is a project result yet.

## Open problems

1. Topology cannot be chosen — 6 of 14 decision criteria depend on unknown lab facts.
2. Momentum availability unknown, which affects whether P7 exists at all.
3. De-embedding method cannot be chosen before the calibration kit and coupon options are known,
   and that decision must be made **before** PCB layout freeze (gate G8).

## Blocked by

**G0.** Five hardware facts, all from Artan or the lab:
substrate laminate + datasheet, fabrication source + minimum trace/gap, VNA model + frequency
range, available calibration kit(s), RF connector type + known-good launch footprint.

## Waiting on Artan

Round 1 message is drafted and ready to send: `planning/questions_for_artan.md`.

## Next action

**Send the Artan Round 1 message.** Nothing downstream of G0 should start before it is answered.

While waiting, the only sanctioned parallel work is theory block **B (transmission lines)** in
`theory/theory_dependency_map.md` and ADS installation/orientation (P1 prep). Do not start
filter synthesis.
