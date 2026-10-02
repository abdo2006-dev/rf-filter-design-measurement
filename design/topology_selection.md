# TOPOLOGY SELECTION

**Status: UNDECIDED. 8 of 14 criteria scored, 6 BLOCKED on gate G0.**

*The matrix is deliberately incomplete. Scoring a criterion that depends on an unknown lab fact
would be inventing data, which is prohibited.*

---

## Candidates

| ID | Topology | One-line description |
|---|---|---|
| **A** | Stepped-impedance low-pass filter | Alternating high- and low-impedance line sections approximating series Ls and shunt Cs |
| **B** | Parallel-coupled-line bandpass filter | Cascaded half-wave resonators coupled side-by-side through gaps |
| **C** | Hairpin bandpass filter | Folded half-wave resonators — a compacted relative of B |

All three were discussed in conversation. **None is chosen.** A third-order parallel-coupled
Chebyshev was mentioned as "attractive"; that is a conversational remark, not a decision
(see `planning/decision_log.md` D-003).

---

## Scoring

**Scale:** 1 = poor / 5 = excellent, *from this project's point of view* — not in general.
**BLOCKED** = depends on a G0 fact. Not scored, not guessed.

| # | Criterion | A: Stepped-Z LPF | B: Coupled BPF | C: Hairpin BPF | Notes |
|---|---|---|---|---|---|
| 1 | Theory richness | 3 | **5** | **5** | A needs prototype + stepped-impedance approximation. B and C add coupled lines, even/odd modes and coupling coefficients — considerably more theory, which is a *benefit* for a learning project. |
| 2 | Beginner difficulty *(5 = easiest)* | **5** | 3 | 2 | A is the standard first filter. B is a standard second one. C adds folding, bend discontinuities and tighter coupling. |
| 3 | ADS educational resources | 4 | **5** | 3 | A is covered by paper A8 (low authority) and general ADS material. B appears in the Keysight Learning Kit and — per claim M-07 — as a case study in 5992-1479. C has the least official material. |
| 4 | Momentum educational value | 3 | **5** | **5** | A's behaviour is well captured by circuit models, so EM adds less. B and C involve real coupling where EM genuinely diverges from circuit models — a better demonstration of *why* EM simulation exists. |
| 5 | PCB size | BLOCKED | BLOCKED | BLOCKED | Needs εr, h and f₀. C is more compact than B by construction, but "how much" is unanswerable without the substrate. |
| 6 | Fabrication sensitivity | BLOCKED | BLOCKED | BLOCKED | Needs etch tolerance. Direction is known (A least sensitive, C most), magnitude is not. |
| 7 | Required minimum gap | BLOCKED | BLOCKED | BLOCKED | **The decisive criterion.** A needs *no* critical gap. B and C do. Unscoreable until the fabricator's minimum gap is known (risk R-06). |
| 8 | Sensitivity to substrate tolerance | BLOCKED | BLOCKED | BLOCKED | Needs the εr tolerance figure. Narrowband designs are more sensitive, so this couples to the specification, which does not exist yet. |
| 9 | Ease of SMA launch | BLOCKED | BLOCKED | BLOCKED | Needs the connector type and footprint. All three terminate in a 50 Ω line, so differences are probably small — but "probably" is not a score. |
| 10 | Measurement clarity | 4 | **5** | **5** | A bandpass response is more striking on a VNA and has more features to compare (f₀, bandwidth, skirts, both edges). A low-pass gives a corner and a roll-off. |
| 11 | Usefulness for the de-embedding study | 3 | **4** | **4** | Fixture effects are more visible against a sharper, more structured response, and matter more where return loss is part of the specification. |
| 12 | Seminar mathematical depth | 3 | **5** | 4 | B gives coupled resonators, coupling matrices and two-mode behaviour — the richest material for a maths audience. C is similar but harder to draw clearly on a slide. |
| 13 | Relevance to future RF work | 3 | **5** | 4 | Coupled-resonator filters and coupling-matrix methods are directly adjacent to the mentor's field (PAs need matching and filtering networks) and to RF front-end work generally. |
| 14 | Time risk *(5 = lowest risk)* | **5** | 3 | 2 | Partially scoreable: A has fewer failure modes and a known-good fallback path. **Fabrication lead time is BLOCKED**, so this score covers design/simulation effort only. |

### Scored subtotals *(8 of 14 criteria — provisional and not a ranking)*

| | A | B | C |
|---|---|---|---|
| Sum of scored criteria | **30** | **37** | **30** |
| Criteria scored | 8 | 8 | 8 |
| Criteria BLOCKED | 6 | 6 | 6 |

> ⚠ **Do not read this as a result.** The six blocked criteria include **#7 (minimum gap)**, which
> is capable of eliminating B and C outright. A topology that cannot be fabricated scores zero
> regardless of its other merits. The subtotals are shown only to make the blocked rows' importance
> visible — B leads on the criteria that *do not matter yet*.

---

## What the blocked criteria could do

Honest conditional reasoning, recorded now so the G3 decision is quick rather than re-argued:

| If G0 reveals… | Then |
|---|---|
| Minimum gap is coarse (e.g. ≳0.2 mm) relative to what the specification needs | B and C become difficult or impossible → **A** |
| Minimum gap is fine and etch tolerance tight | B becomes the leading candidate |
| Board size is tightly constrained | C's compactness matters; otherwise it is a cost without a benefit |
| εr tolerance is loose | narrowband designs become unreliable → widen bandwidth (alternative A-05) or move to **A** |
| VNA range is limited | constrains f₀, which feeds back into the achievable gap and board size |
| Momentum is unavailable | criterion #4 collapses and B/C lose part of their advantage |
| Artan prefers a low-pass educationally | **A**, and the matrix is a sanity check rather than the decider |

> **Note on criterion 7 and paper A7.** The published hairpin filter in the bibliography uses
> resonator spacing of about **0.1 mm**. That is below the minimum gap of many low-cost fabrication
> processes. It is a concrete illustration that candidate C's feasibility is a fabrication question
> first and a design question second.

---

## Decision procedure at G3

1. Fill the six BLOCKED rows from `hardware_constraints.md`. **No guessing.**
2. Apply the **elimination filter first**: any topology whose required minimum gap is not
   manufacturable with margin is removed, whatever it scores. Feasibility is not a weighted
   criterion — it is a gate.
3. Re-total the survivors.
4. **Weight the criteria.** The current totals are unweighted, which implicitly treats "PCB size"
   as equal in importance to "required minimum gap". It is not. Assign weights explicitly at G3 and
   record them — unweighted sums are a convenient display, not a decision method.
5. If two survivors are within ~10 %, the tie-break is **time risk** (criterion 14), because
   risk R-15 is the project's critical risk.
6. Write the justification: what won, and **why each runner-up lost**.
7. Mentor sign-off. Decision-log entry D-003.

## What this matrix must not become

- A justification written after the choice is made. If the matrix is filled in to support a
  pre-existing preference, it is worse than no matrix.
- A reason to pick B because it scores highest on unweighted partial data. It currently leads only
  on criteria that are cheap to score.
- A reason to pick the most impressive-sounding topology. **A fabricated, measured,
  fully-understood stepped-impedance LPF is worth far more — to the project, the seminar and the
  CV — than an unbuildable coupled-line filter.**
