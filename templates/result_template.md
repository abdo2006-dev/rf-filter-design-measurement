# RESULT TEMPLATE

Append to `results/result_register.md`.

> A result is a **number with provenance**. A number without provenance is a rumour, and by P13
> there will be too many numbers to remember where any of them came from.

---

```markdown
### R-0NN

| Field | Value |
|---|---|
| **Result ID** | R-0NN |
| **Quantity** | <e.g. insertion loss at f0> |
| **Value** | |
| **Units** | |
| **Type** | analytical / simulated-ideal / simulated-microstrip / simulated-EM / measured / de-embedded |
| **Model / configuration** | <which exact model or hardware state> |
| **Source file** | <path + commit SHA> |
| **Extraction method** | <how the number was obtained from the data: marker, script, interpolation — and if a script, which one> |
| **Date** | |
| **Status** | provisional / final |
| **Uncertainty / limitations** | <for measurements: the repeatability spread from G11. For simulations: convergence/model limits. "None" is almost never the right answer.> |
| **Used in seminar?** | yes/no — slide # |
| **Used in CV/report?** | yes/no |
| **Notes** | |
```

---

## Rules

1. **Type is mandatory**, and the six types are not interchangeable. "The simulation says" is
   meaningless in this project — there are four different simulations (risk R-23).
2. **Source file plus commit SHA.** A path alone does not identify a version, and files change.
3. **Extraction method matters.** "f₀ = 2.41 GHz" read off a coarse sweep with a cursor is not the
   same number as one from an interpolated minimum. State which.
4. **Uncertainty is mandatory for every measured result.** It comes from the G11 repeatability
   study. **Never claim a discrepancy smaller than the repeatability spread** — that is risk R-10
   and it invalidates the attribution.
5. **Provisional until its gate passes.** A Momentum number is provisional until G7; a measured
   number until G11; a de-embedded number until G13.
6. **"Used in CV/report?" is a deliberate checkpoint.** Before a number reaches a CV, this row
   forces a look at its uncertainty and its status. Risk R-14.
