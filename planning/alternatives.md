# ALTERNATIVES

*The idea sink. New ideas come here instead of into the plan.*

**Why this file exists.** The student's two previous projects failed by growing. The mechanism was
not bad judgement — it was that each individual idea was *good*. The defence against good ideas is
not willpower, it is a place to put them.

**Rule.** Anything not required by the definition of done goes here. Nothing leaves this file
without a decision-log entry explaining what it replaces, and no idea is adopted mid-phase.

---

## 1. Live alternatives — real branches this project may take

These are genuine options the plan already accommodates.

| # | Alternative | When it becomes relevant | Trade-off |
|---|---|---|---|
| A-01 | Stepped-impedance LPF instead of a BPF | G3; fallback if R-06 fires | Simpler, no critical gap, far more robust to fabrication. Less coupled-line theory, so slightly less seminar depth — but a *working* filter beats a richer unbuildable one. |
| A-02 | Hairpin instead of parallel-coupled BPF | G3 | More compact; similar theory. Published designs use very small gaps (paper A7, ~0.1 mm), so it is probably *more* fabrication-sensitive, not less. |
| A-03 | Lower centre frequency than first discussed | G3, if minimum gap or board size binds | Larger features, easier fabrication, more forgiving. Bigger board. Often the right call for a first project. |
| A-04 | Lower filter order | G3/G4, if tolerance study fails | Less selectivity; much better tolerance behaviour and smaller board. |
| A-05 | Wider fractional bandwidth | G3, if gaps are too tight | Wider gaps, easier fabrication, less sensitive. Less impressive selectivity. **Usually the cheapest fix for an unmanufacturable coupled-line design.** |
| A-06 | De-embedding: fixture model from EM instead of on-board standards | G8 | Needs no extra coupons and no extra connectors. Relies on the EM model being right, which the project has not yet established. |
| A-07 | De-embedding: port extension / electrical delay only | G8 | Trivial to execute, honest if labelled as crude. Removes delay, not reflection — so it does not actually answer the stretch question. |
| A-08 | No de-embedding | G8/G13 | **A legitimate, documented outcome.** Costs the stretch goal, costs nothing else. |
| A-09 | Open-source EM solver if Momentum is unlicensed | G7, if R-24 fires | Keeps an EM step in the project. **Must be labelled honestly** — it is not Momentum, and the CV claim changes. |
| A-10 | Commercial PCB prototype service | G9, if R-08 fires | Predictable lead time and documented design rules. Cost, shipping, and less mentor involvement. |

## 2. Deferred — good ideas, wrong project

Parked. Revisit after P13, or as a Bachelor-thesis seed.

| # | Idea | Why it is attractive | Why not now |
|---|---|---|---|
| B-01 | Fabricate two filters on different substrates and compare | Directly addresses substrate effects; strong result | Doubles fabrication, measurement and analysis. **This is the single most likely scope-creep vector in the project** — it feels like "just one more board". |
| B-02 | Measured-εr extraction and re-simulation loop | Excellent closure of the core question | A *bounded* version is already in scope as the R-04 fallback at P11. Keep it bounded. Material characterization as a discipline is not this project. |
| B-03 | Compare two de-embedding methods against each other | Genuinely interesting; a real research question | Requires both methods' coupons, plus the theory depth to adjudicate. A Bachelor-thesis topic, not a second-year side quest. |
| B-04 | Tunable filter with varactors | Connects to the previous reflectarray work | Active components, bias networks, non-linearity. Exactly the open-endedness that sank project one. |
| B-05 | Compare ADS Momentum against CST | Student already knows CST | Two tool-chains, two meshing philosophies, two validation methodologies. Multiplies P7's hardest part. |
| B-06 | Build a proper test fixture rather than board-mounted connectors | Better measurement; closer to industry | Mechanical design and machining. Out of scope and off the critical path. |
| B-07 | Diplexer / filter bank / matching-network extension | Natural next step after one filter works | Only after M14. Realistically a different project. |
| B-08 | Write this up for a student conference | Portfolio value | **Only if the results justify it.** Decide at P13 from evidence, and note PR-13: no novelty claim. |

## 3. Rejected — recorded so they are not re-proposed

| # | Idea | Why rejected |
|---|---|---|
| C-01 | Start with a power amplifier | Artan explicitly advised against it. Needs the fundamentals this project builds. |
| C-02 | Metasurface / reflectarray continuation | The project this one exists to replace. |
| C-03 | Add defected ground structures | Appears in papers A7/A10. Out of scope, adds EM complexity, adds nothing to the core question. |
| C-04 | UWB or multi-band filter | Out of scope. Would invalidate the narrow comparison the project is built on. |
| C-05 | Optimizer-driven design from the start | Forbidden by G5. Produces a filter nobody understands, which defeats the entire purpose. |
| C-06 | Skip the circuit model and go straight to EM | Destroys attribution. The ideal→microstrip→EM deltas *are* the results. |
| C-07 | Skip fabrication, present simulation only | Hardware is the point. **Note:** seminar version C is a *contingency* for delay, not a plan. |
| C-08 | Claim novelty to strengthen the CV | Dishonest, and transparent to any RF engineer who reads it. PR-13. |
| C-09 | Choose 2.4 GHz because it is a common frequency | Familiarity is not a design reason. See D-002. |
| C-10 | Copy a published filter's dimensions | Produces a design that cannot be defended and teaches nothing. `source_hierarchy.md` Tier-3 hard rule. |

---

## Intake

When a new idea arrives:

1. **Write it here first.** Not in the plan, not in a chat, not in the next file you happen to edit.
2. Note what it would add, and what it would cost in weeks.
3. Ask: *does the definition of done require it?* If no → it stays in §2 until P13.
4. If it genuinely replaces something in scope, open a decision-log entry and say what it replaces.

> **The test.** "This would make the project better" is true of almost every idea in §2. That is
> why it is not the test. The test is: **"without this, is the project incomplete?"**
> For everything in §2, the answer is no.
