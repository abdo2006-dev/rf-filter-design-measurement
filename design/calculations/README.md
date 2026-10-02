# design/calculations/

**Empty, and must stay empty until gates G0 and G3 have both passed.**

This is the stop line from `MASTER_PROJECT_PLAN.md`. No centre frequency, line width, gap,
coupling coefficient, resonator length or element value may be computed before the constraints are
known and the topology is chosen. Calculating earlier produces numbers that feel settled, get
reused, and are wrong.

## What goes here, and when

| File | Phase | Gate |
|---|---|---|
| `s_abcd_t_conversions.md` — conversions with the convention and reference impedance **stated explicitly** | P2 | G2 |
| `order_derivation.md` — required order derived from the stopband requirement | P4 | G4 |
| `prototype_values.md` — normalized g-values, **plus an independent published table as a cross-check** | P4 | G4 |
| `denormalization.md` — frequency and impedance scaling, transformations | P4 | G4 |
| `microstrip_dimensions.md` — every physical dimension, tabulated, with its margin against the fabricator minimum | P6 | G6 |
| `tolerance_study.md` — response under εr, h and etch tolerances | P6 | G6 |

## Rules

1. **Show the arithmetic.** A number with no derivation cannot be checked, by Artan or by a future
   session.
2. **Two independent routes for anything load-bearing.** Derivation *and* a published table; or
   hand calculation *and* simulation. Gate G4 requires this.
3. **State the units and the convention.** Every time.
4. **Cite the source** for every formula, into `research/claims_and_sources.md`.
5. **Never use a dimension from a paper.** See the Tier-3 hard rule in
   `research/source_hierarchy.md`.
