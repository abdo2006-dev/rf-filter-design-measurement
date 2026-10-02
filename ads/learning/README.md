# ads/learning/

Empty — no ADS work has been done.

ADS learning exercises (P1, P2). One subdirectory per experiment, named EXP-0NN_<name>, holding the workspace plus the experiment record.

**Gate:** G1, G2

## Committing ADS work

- Commit the **workspace design intent**: schematics, layouts, substrate definitions, exported
  S-parameter data, plots.
- Do **not** commit simulation caches, logs, mesh dumps or solver intermediates — `.gitignore`
  excludes them. They are large and regenerable.
- Do **not** commit Keysight example workspaces if their licence prohibits redistribution
  (risk R-26). Reference the source instead.
- Every workspace needs an experiment record from `templates/experiment_template.md`.
