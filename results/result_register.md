# RESULT REGISTER

**EMPTY. No results exist.**

> No simulation has been run. No measurement has been taken. No hardware exists.
> **Nothing may be added to this table from a prediction or an expectation** — only from a
> committed file produced by a run that actually happened.

**Rules in full:** `templates/result_template.md`.

---

## Register

| ID | Quantity | Value | Units | Type | Model/config | Source file | Extraction | Date | Status | Uncertainty | Seminar? | CV/report? |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| — | *(none)* | — | — | — | — | — | — | — | — | — | — | — |

---

## The five-way comparison

This is the table the whole project exists to fill. It is the answer to the core engineering
question, and its shape *is* the answer: how far each column drifts from the one before it.

| Metric | Analytical | Ideal circuit | Microstrip circuit | Momentum EM | Measured | De-embedded |
|---|---|---|---|---|---|---|
| f₀ or f_c | — | — | — | — | — | — |
| Insertion loss at f₀ | — | — | — | — | — | — |
| Return loss at f₀ | — | — | — | — | — | — |
| 3 dB bandwidth | — | — | — | — | — | — |
| Attenuation @ stopband f₁ | — | — | — | — | — | — |
| Attenuation @ stopband f₂ | — | — | — | — | — | — |

Each cell cites a result ID. Each column names the gate that validated it:
analytical → G4 · ideal circuit → G5 · microstrip → G6 · Momentum → G7 · measured → G11 ·
de-embedded → G13.

**The de-embedded column may legitimately stay empty** (G13 no-go). An empty column with a
recorded reason is a result.

## Repeatability

Filled at G11, from ≥3 disconnect/reconnect cycles. **Every measured uncertainty in the register
comes from here.**

| Metric | Run 1 | Run 2 | Run 3 | Spread | Std dev |
|---|---|---|---|---|---|
| f₀ | — | — | — | — | — |
| IL at f₀ | — | — | — | — | — |
| RL at f₀ | — | — | — | — | — |
| 3 dB BW | — | — | — | — | — |

> **The spread column sets the floor on every claim in the project.** A 0.3 dB difference between
> simulation and measurement means nothing if remeasuring the same board gives 0.5 dB of scatter.
> This is risk R-10, and it is why G11 precedes G12.

## Discrepancy attribution

Filled at G12. A mechanism is named **only** with evidence.

| Discrepancy | Magnitude | Attributed mechanism | Evidence | Confidence |
|---|---|---|---|---|
| — | — | — | — | — |

### Unexplained

**This section is mandatory and may not be left empty by wishful thinking.** Some discrepancy
always resists attribution, and listing it honestly is worth more than a confident wrong
explanation — it is also what an experienced reader looks for first.

| Discrepancy | Magnitude | What was ruled out | What would be needed to explain it |
|---|---|---|---|
| — | — | — | — |
