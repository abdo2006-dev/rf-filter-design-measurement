# RESEARCH BASIS

*What the project's technical foundation actually rests on, and how bounded the research pass was.*

---

## The bounded research pass

**Conducted:** 2026-10-02, one session.
**Budget:** deliberately small. 13 targeted searches. The instruction was "a curated source stack,
not 100 papers," and that instruction is itself a project control — the student's two previous
projects failed through unbounded research.

**Outcome: 23 sources.** 2 textbooks, 6 vendor/standards documents, 10 papers, 5 informal.

**What was deliberately not done.** No systematic literature review. No citation-graph expansion.
No attempt at comprehensive coverage of microstrip filter literature — there are thousands of such
papers and reading more of them would not improve this project by one decibel. The Tier-3 set
exists to show *that the process works and what magnitude of discrepancy is normal*, not to survey
a field.

**Research is now closed** until a gate needs something specific. New sources enter via
`reading_queue.md`, with a stated gate that requires them. "Interesting" is not a reason.

---

## What the foundation rests on, by question

| The project needs to know… | Authority | Confidence |
|---|---|---|
| How a transmission line behaves | Pozar ch. 2 | High — settled textbook physics |
| What S-parameters are and how to cascade networks | Pozar §4.3–4.4 | High |
| How to design a filter from a requirement | Pozar §8.3–8.4 (insertion-loss method) | High |
| How to turn element values into microstrip geometry | Hong & Lancaster | High — **but chapter pointers not yet confirmed** |
| How to use ADS for this | Keysight *RF Design Software Learning Kit* (T2-04) | Medium — not yet opened |
| How to run and judge a planar EM simulation | ADS Momentum documentation (T2-05) + our own benchmark | **Low until P7** — this is the weakest link, see below |
| How to measure in a fixture | Keysight 5968-5329 | Medium — not yet opened |
| How to de-embed | Keysight 5980-2784EN, Engen & Hoer, IEEE 370 | Medium — all three identified, none opened |
| What discrepancy is realistic | Tier-3 papers A1–A4, A7, A10 | Medium — examples, not authority |
| What our substrate, fabricator, VNA and connector are | **nothing** | **BLOCKED — this is gate G0** |

## The weakest links, named

Stating these explicitly because the student has said he cannot yet independently judge every
technical recommendation. These are the places where this bootstrap is *least* able to protect him:

1. **Momentum validation (G7).** No authoritative document on planar-EM convergence was opened in
   this session. What exists in `MASTER_PROJECT_PLAN.md` for G7 is a *methodology* assembled from
   secondary descriptions of Keysight's guidance plus first-principles reasoning about what a 2.5-D
   MoM solver actually discretizes. The methodology is sound in shape — sweep the settings that
   control accuracy, declare a numerical threshold in advance, and benchmark against a known
   answer — but **the specific numbers (20/30/40/50 cells per wavelength) must be confirmed in the
   installed ADS documentation before being treated as guidance.**

2. **Nothing was read.** Every Tier-1 and Tier-2 source in this repository is cited from
   bibliographic metadata only, because the container could not open a single PDF. See
   `verification_log.md`. The citations are honest about this, but it means **the first real
   reading pass is still ahead**, and it belongs at the start of P1 and P3.

3. **No substrate data.** Every microstrip calculation in the project depends on εr, tanδ and
   thickness, and none of those are known. This is why G0 exists and why no dimension may be
   computed before it.

4. **The topology decision is 6/14 blocked.** It is not possible to choose responsibly yet, and
   the matrix says so rather than pretending otherwise.

## What this project does *not* claim

- No novelty. The design will be a textbook topology designed by a textbook method.
- No state of the art. The Tier-3 papers are more advanced than this project and that is fine.
- No contribution to filter theory, measurement theory, or de-embedding methodology.

The contribution is **to the student's competence**, and the evidence is the traceability: a
documented chain from a requirement to a measured number, with every discrepancy accounted for.
That is what an RF employer or a thesis supervisor is actually looking for from a second-year
student, and it is a far better thing to have than an over-reaching claim.

## How a source becomes load-bearing

1. It enters `annotated_bibliography.md` with full metadata and a verification status.
2. The claim it supports is written into `claims_and_sources.md` with a specific section pointer.
3. If it supports a *seminar* claim, it also gets a row in `seminar/source_map.md`.
4. If the verification status is UNVERIFIED, the claim **may not appear in the report or the
   seminar** until it is upgraded.

That last rule is the main defence against the failure mode the student named: an AI-supplied
claim quietly becoming a fact. A claim with no row in `claims_and_sources.md` has no standing in
this project.
