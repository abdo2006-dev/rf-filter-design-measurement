# EXPERIMENT TEMPLATE

Copy to the relevant directory as `EXP-0NN_<short-name>.md`.

> **The rule this template exists to enforce: the prediction is written BEFORE the simulation or
> measurement is run.** An experiment record written afterwards is a report, not an experiment, and
> it teaches nothing — you cannot be surprised retrospectively. Gate G1 fails if the prediction was
> written after the result.
>
> **No random parameter sweeps.** Every parameter change needs a hypothesis, a predicted effect,
> and a metric to judge it by.

---

```markdown
# EXP-0NN — <title>

**Experiment ID:**
**Date:**
**Phase / Gate:**
**Status:** planned / running / complete / abandoned

## Engineering question
<The one question this answers. If there is more than one, split the experiment.>

## Hypothesis
<What you expect, and WHY — the mechanism, not just the outcome.>

## Prediction  ← WRITTEN BEFORE RUNNING
<Quantitative where possible. "S11 will dip near 2 GHz" is weak;
"S11 minimum within 5% of 2.0 GHz, below -15 dB" is a real prediction.>

| Quantity | Predicted value | Basis |
|---|---|---|
|  |  | <analytic calculation / textbook / previous result> |

## Model / hardware state
- Workspace / file:
- Commit SHA:
- Substrate definition:
- Instrument + calibration (if measurement):

## Independent variable
<The one thing being changed, and over what range.>

## Controlled variables
<Everything held fixed. Being explicit here is what makes the result attributable.>

## Method
<Enough that someone else could repeat it. Simulator settings, sweep setup, port
definitions; or instrument settings, IF bandwidth, power, averaging.>

## Observed outcome

| Quantity | Predicted | Observed | Difference |
|---|---|---|---|
|  |  |  |  |

## Files
- Workspace:
- Exported data:
- Plots:

## Interpretation
<Did the prediction hold? If not, WHY — was the prediction wrong, the model wrong,
or the execution wrong? These are three different conclusions with three different
follow-ups, and saying which is the actual learning.>

## Limitations
<What this does not show. Numerical precision, model assumptions, measurement
uncertainty, range not covered.>

## Decision
<What this changes. Link to a decision-log entry if it changes a project decision.>

## Next step
<One next action.>
```

---

## Index

| ID | Title | Phase | Gate | Status |
|---|---|---|---|---|
| EXP-001 | Terminated transmission line, swept load | P1 | G1 | ⬜ not started |
| EXP-002 | Electrical length sweep | P1 | G1 | ⬜ |
| EXP-003 | Quarter-wave transformer | P1 | G1 | ⬜ |
| EXP-004 | **Two-network cascade, both orders** | P2 | G2 | ⬜ — *also seminar asset AS-22* |
| EXP-005 | Three-network cascade: associativity | P2 | G2 | ⬜ |

*Further experiments are added as phases require them. Do not pre-plan experiments for phases that
are still blocked — their design depends on facts that do not exist yet.*
