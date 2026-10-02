# ads/momentum/

Empty — no ADS work has been done.

Planar EM models (P7). EM_VALIDATION_METHOD.md must be written and committed BEFORE any Momentum result is believed — gate G7.

**Gate:** G7

## Committing ADS work

- Commit the **workspace design intent**: schematics, layouts, substrate definitions, exported
  S-parameter data, plots.
- Do **not** commit simulation caches, logs, mesh dumps or solver intermediates — `.gitignore`
  excludes them. They are large and regenerable.
- Do **not** commit Keysight example workspaces if their licence prohibits redistribution
  (risk R-26). Reference the source instead.
- Every workspace needs an experiment record from `templates/experiment_template.md`.

## EM_VALIDATION_METHOD.md — write this first

Gate G7 will not pass without it. It must state, **before any sweep is run**:

1. The solver settings to be swept (cells per wavelength, mesh frequency, edge mesh, adaptive
   frequency sampling) — **not** a geometric mesh-refinement sweep.
2. The **numerical** convergence criterion, fixed in advance — e.g. Δf₀ < 0.25 % and
   ΔS₂₁ < 0.1 dB between successive settings.
3. The known-answer benchmark: a plain 50 Ω line of known length, compared against the analytic
   microstrip model.
4. The port setup, reference impedance, and **what reference plane the result is at**.
5. The substrate stack-up, including conductor thickness and conductivity, and finite vs infinite
   ground.

> **Do not import a CST-style adaptive volumetric mesh-convergence rule.** Momentum is a 2.5-D
> method-of-moments surface solver; refinement is not automatically monotonic and over-refinement
> can degrade the result numerically. See decision D-005 and claims M-01…M-06 — **all of which are
> currently only PARTIALLY VERIFIED and must be confirmed in the installed ADS documentation.**
