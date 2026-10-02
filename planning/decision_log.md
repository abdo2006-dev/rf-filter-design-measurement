# DECISION LOG

*The promotion mechanism. Nothing becomes CONFIRMED except by an entry here.*

**Rules.**
1. A decision needs: what was decided, **why**, what it rules out, what would reverse it, and a date.
2. A brainstorming suggestion is **not** a decision. Conversation does not confirm anything.
3. Reversal is normal. Mark the old entry SUPERSEDED, do not delete it — the reasoning is the value.
4. Decisions requiring Artan's input stay OPEN until he has actually answered, in writing, dated.

---

## Decisions taken

### D-000 — Project scope and deliverable chain
**Status:** CONFIRMED · **Date:** 2026-10-02 · **Decided by:** student, on mentor's advice

**Decision.** The project is "Design, EM Simulation, Fabrication, VNA Characterization and
De-embedding of a Microstrip RF Filter", progressing analytical design → circuit simulation →
microstrip simulation → planar EM simulation → PCB → two-port VNA measurement → comparison, with
fixture de-embedding as a stretch goal.

**Why.** Artan advised against jumping into advanced PA research and suggested starting from RF
fundamentals with a practical project spanning transmission lines, matching/filter networks,
microstrip, ADS, PCB, VNA, calibration and de-embedding. It is bounded, has a clear end, and
produces a defensible portfolio claim.

**Rules out.** Amplifier work, tunable/active filters, metasurface work, any novelty claim.

**Would reverse it.** Mentor redirection, or a hard blocker making hardware impossible (which would
reduce scope rather than change the project).

---

### D-001 — Fixture/de-embedding strategy decided before layout, not after
**Status:** CONFIRMED · **Date:** 2026-10-02 · **Decided by:** bootstrap session (architecture)

**Decision.** The measurement and de-embedding *strategy* decision becomes its own phase (P8) and
gate (G8), positioned **before** PCB layout — not at the end of the project.

**Why.** Every realistic de-embedding method needs something physical that must be fabricated:
TRL needs thru/reflect/line standards in the same medium (claim C-06), the IEEE-370 method needs a
fabricated 2x-thru coupon (claim C-04), and even a fixture-model approach needs a characterizable
launch. Keysight 5968-5329 exists largely to explain that these standards have to be built
(claim C-03). After fabrication, the available methods are exactly those the copper supports. A
plan that defers the decision to P10+ guarantees the stretch goal is lost.

**Rules out.** Starting layout before G8 passes.

**Would reverse it.** Nothing. This is the structural fix the first outline most needed.

---

### D-005 — Momentum validation methodology is to be established, not inherited
**Status:** CONFIRMED · **Date:** 2026-10-02 · **Decided by:** bootstrap session

**Decision.** G7 requires a written, planar-EM-specific validation procedure
(`ads/momentum/EM_VALIDATION_METHOD.md`) with a numerical convergence threshold declared **before**
the sweep, plus a known-answer benchmark. A CST-style volumetric adaptive-mesh convergence rule is
explicitly **not** imported.

**Why.** Momentum is a 2.5-D method-of-moments surface solver; it discretizes conductor surfaces
with a mesh controlled by cells-per-wavelength at a chosen mesh frequency. Refinement is not
automatically monotonic and over-refinement can degrade the result numerically (claim M-04). The
student's prior experience is CST, where the natural habit is adaptive mesh refinement until
convergence — a habit that does not transfer, and would produce false confidence.

**Rules out.** Reporting any Momentum result before the method document and the benchmark exist.

**Would reverse it.** Authoritative ADS documentation prescribing a different, better procedure —
in which case adopt it and supersede this entry. **Reading that documentation is itself a P7 task.**

---

### D-007 — Persistence: local repository plus bundle and zip
**Status:** CONFIRMED · **Date:** 2026-10-02 · **Decided by:** bootstrap session, forced by tooling

**Decision.** The bootstrap is persisted as a local git repository, a verified git bundle and a zip
archive, with manual GitHub instructions in `PERSISTENCE.md`. The repository was **not** created
automatically.

**Why.** Two attempts failed: the GitHub integration returned `403 Resource not accessible by
integration`, and `gh api POST /user/repos` returned `403 sessions are bound to their configured
repositories`. The session's credential is scoped to two unrelated repositories. Pushing this
project into either of them would have been wrong.

**Rules out.** Relying on the container. **The bundle must be stored off-container and the GitHub
repository created manually — see `PERSISTENCE.md`.**

**Would reverse it.** Creating the repository on GitHub first, then starting a session with it
selected as a source.

---

## Decisions OPEN — blocked on gate G0

These are the ones that matter, and **none of them is decided.** They are listed with their
candidates so that nobody mistakes a candidate for a choice.

### D-002 — Centre / cut-off frequency
**Status:** OPEN · **Blocked by:** G0 (substrate, VNA range), mentor input (Round 1 Q5)

**Candidates.** None ranked. A region "a few GHz" was discussed; **~2.4 GHz was discussed and must
not be adopted on familiarity.** The frequency must follow from the substrate's usable range, the
VNA's range, the manufacturable minimum feature at that frequency, and a sensible board size.

**Explicit warning.** 2.4 GHz is the number most likely to slip into CONFIRMED without a decision,
because it is familiar from Wi-Fi. If it is eventually chosen it must be chosen *for a reason
recorded here*, and the reason may not be "it is a common frequency."

### D-003 — Topology
**Status:** OPEN · **Blocked by:** G0, then G3

**Candidates.** (A) stepped-impedance LPF, (B) parallel-coupled BPF, (C) hairpin BPF. The matrix in
`design/topology_selection.md` has 8 of 14 criteria scored; **6 are BLOCKED on G0.** A third-order
parallel-coupled Chebyshev was discussed — it is one unscored candidate, not a plan.

### D-004 — Response type and order
**Status:** OPEN · **Blocked by:** D-003 and a written specification

**Candidates.** Butterworth / Chebyshev / others. Order undetermined — it must be *derived* from a
stopband requirement (gate G4), not chosen. Third order was mentioned in conversation; it has no
standing.

### D-006 — Calibration and de-embedding method
**Status:** OPEN · **Blocked by:** G0 (what kit exists), then G8

**Candidates** (inventory with validity assumptions lives in `measurement/measurement_plan.md`):
calibrate-to-coax + fixture-model negation; on-board TRL to the microstrip plane; IEEE-370-style
2x-thru; port extension only; **none**.

**Explicit warning.** Neither SOLT nor TRL is assumed. "None" is a legitimate, documented outcome.

### D-008 — Substrate
**Status:** BLOCKED · **Blocked by:** G0 · **Candidates:** unknown. **FR-4 is not assumed.**

### D-009 — Connector and launch
**Status:** BLOCKED · **Blocked by:** G0 · **Candidates:** unknown. SMA is plausible, not chosen.

### D-010 — Fabrication route
**Status:** BLOCKED · **Blocked by:** G0

### D-011 — Seminar version (A / B / C)
**Status:** OPEN · **Decide by:** the seminar content-freeze date, on what actually exists
**Default if undecided:** C, because it never requires hardware. See `seminar/SEMINAR_MASTER_PLAN.md`.

---

## Superseded

*(none yet)*

---

## Template

```
### D-0xx — <short title>
**Status:** CONFIRMED | PROVISIONAL | OPEN | BLOCKED | SUPERSEDED
**Date:** YYYY-MM-DD · **Decided by:** <who>
**Decision.** <what>
**Why.** <reasoning, with claim/source IDs where it rests on a reference>
**Rules out.** <what this closes off>
**Would reverse it.** <the evidence that would change this>
```

Full version in `templates/decision_template.md`.
