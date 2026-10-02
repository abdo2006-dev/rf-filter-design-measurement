# BOOTSTRAP SELF-REVIEW

*Step 11 of the bootstrap: a deliberate pass looking for the specific failure modes this project
is most exposed to. Recorded rather than silently fixed, so a future session can see what was
checked and what remains open.*

**Date:** 2026-10-02

---

## 1. Contradictions — checked, 4 found and fixed

| # | Issue | Resolution |
|---|---|---|
| 1 | **Reference planes were named P0–P6, colliding with the phase names P0–P14.** "Plane P3" and "phase P3" would have been indistinguishable in prose — a real source of future confusion in exactly the document where precision matters most. | Reference planes renamed **RP0–RP6**, with a naming note in `measurement/measurement_plan.md`. |
| 2 | The master plan cited **absolute slide numbers** that did not match `slide_outline.md` and would drift every time the deck was re-ordered. | All 12 references changed to **act/beat + asset ID**, which are stable. |
| 3 | Theory map header said **T1–T56** while the map defines up to **T62**; `README.md` said T1–T52. Master plan cited **Block G as T48–T51** (actually T51–T54) and **Block H as T52+** (actually T55–T62). | All corrected and cross-checked against the map. |
| 4 | Source count stated as **22**; the bibliography contains **23**. | Corrected in `research_basis.md` and `planning/milestones.md`. |

**ID cross-reference audit:** every R-, D-, C-/M-/S-/F-, AS-, T-, G- and P- identifier referenced
anywhere is defined somewhere, and vice versa. All internal markdown links resolve.

## 2. Accidentally frozen provisional decisions — checked, none found

The highest-risk failure mode for this bootstrap. Every mention of a candidate parameter was
audited for whether the surrounding text could be read as a commitment:

| Parameter | Mentions | Verdict |
|---|---|---|
| 2.4 GHz | 6 files | Every one explicitly warns against adopting it. D-002 carries a dedicated warning; `alternatives.md` C-09 records "chose it because it is common" as a **rejected** reason. ✅ |
| FR-4 | 7 files | Never a design assumption. Appears as "not assumed" (D-008), as a hardware-constraint warning, and as UNVERIFIED claims S-01…S-03 explicitly kept to document their *rejection*. ✅ |
| Chebyshev | 10 files | Always as one of several response types, or as a "do not learn yet" item. D-004 OPEN. ✅ |
| Third order | 4 files | Always flagged as having no standing; FR-04 states order must be **derived** at G4. ✅ |
| SOLT / TRL | 6 files | Always listed as candidates. D-006 OPEN. `hardware_constraints.md` separates "methods the instrument supports" from "kits we physically have". ✅ |
| Parallel-coupled topology | matrix + plan | Leads the unweighted partial scoring, and the matrix says so explicitly — including that it leads only on criteria that are cheap to score, and that criterion 7 can eliminate it outright. ✅ |
| 50 Ω port impedance | FR-11 | Marked **PROVISIONAL**, not CONFIRMED, with the reasoning stated: if 50 Ω can be assumed without a decision entry, so can the centre frequency. ✅ |

**Only four things are CONFIRMED** (D-000 scope, D-001 G8 ordering, D-005 EM methodology, D-007
persistence). None is a filter design parameter.

## 3. Unsupported citations — checked, 3 open items (recorded, not hidden)

| # | Item | Status |
|---|---|---|
| 1 | **Claim C-09** (naive matrix inversion amplifies noise) has **no source**, and it backs a *required* seminar beat. | **OPEN.** Flagged in `claims_and_sources.md`, in `source_map.md` slide 38, and in the action list there. Must be sourced or restated as reasoning before the seminar. |
| 2 | **Hong & Lancaster chapter numbers are blank** throughout, because the book was not opened. | **OPEN by design** — deliberately left blank rather than guessed. Fill at P3; it is item 4 in the reading queue. |
| 3 | **No source opened in this session at all.** Every Tier-1/Tier-2 citation is bibliographic-metadata-only. | **Recorded in full** in `research/verification_log.md` with the blocked hosts named. No citation claims to have been read. |

Claims S-01…S-03 (generic FR-4 figures) are UNVERIFIED and explicitly barred from the report and
the seminar. Claims M-01…M-07 (Momentum) are PARTIALLY VERIFIED and must be confirmed in the
installed ADS documentation before G7 relies on them.

## 4. Missing dependencies — checked, 1 structural fix made

The first-draft outline deferred the de-embedding decision to the end of the project. That is a
**missing dependency**: the decision consumes fabricated copper, so it depends on *preceding* the
PCB, not following it. Fixed by creating phase P8 and gate G8 before layout (decision D-001).

Other dependency checks:
- G0 precedes G3 ✅ — the topology decision needs the minimum-gap fact.
- G2 precedes G8/P12 ✅ — de-embedding is block D applied carefully; attempting it without the
  matrix mathematics is risk R-21.
- G11 precedes G12 ✅ — a discrepancy cannot be claimed before repeatability bounds it.
- G5 precedes G6 precedes G7 ✅ — separate models, separate gates, so discrepancy stays attributable.
- Seminar S2 depends only on G2 ✅ — which needs no hardware, no licence and no money.

## 5. Excessive project scope — checked, bounded

| Control | Where |
|---|---|
| Hard stop line (no dimensions before G0 + G3) | `MASTER_PROJECT_PLAN.md` §0 |
| Explicit non-requirements | `planning/requirements.md` §4 |
| Out-of-scope list | `MASTER_PROJECT_PLAN.md` §4 |
| Idea sink | `planning/alternatives.md` §2, 8 deferred ideas |
| Curiosity sink | `research/reading_queue.md` §3 |
| Rejected-and-recorded list | `alternatives.md` §3, 10 entries |
| Research closed after one bounded pass | `research/research_basis.md` |
| Drift detector | reading queue growing faster than the project (R-15 trigger) |

**Named risk:** `alternatives.md` B-01 ("fabricate two boards on different substrates") is
identified as the single most likely creep vector, because it feels like "just one more board".

## 6. Seminar claims unsupported by engineering progress — checked, 0 presentable slides

`seminar/source_map.md` audits all 44 content slides: **0 are presentable today.** 18 need a
project result, ~14 need only a Tier-1 reading pass, 2 need a missing source, 1 needs a chapter
number. The table makes this visible rather than letting a plausible deck get built on unchecked
claims.

Version C's integrity rule is stated as non-negotiable: any simulated fixture/de-embedding
demonstration must be labelled *"simulated demonstration — no hardware measured"* **on the slide
itself**, not only in the speaker notes.

## 7. Known weaknesses of this bootstrap

Stated plainly, because the student has said he cannot yet independently judge every AI
recommendation:

1. **Nothing was read.** No PDF, no DOI, no textbook. The citations are honest about this but the
   first real reading pass is still ahead.
2. **The Momentum validation methodology (G7) is the weakest technical content here.** Its shape is
   sound — sweep the settings that control accuracy, declare the threshold in advance, benchmark
   against a known answer — but the specific numbers are PARTIALLY VERIFIED secondary material.
3. **The topology matrix cannot yet decide anything**, and its unweighted subtotals could mislead a
   hasty reader. The document warns about this in two places; the G3 procedure requires explicit
   weighting.
4. **This repository is an instance of risk R-22.** Treat its technical assertions as hypotheses to
   confirm, not findings. That is written into the risk register itself.
