# design/design_reviews/

Reviews are **checklists with evidence**, not impressions. "It looks fine" is not a review.

| ID | Review | Gate | Status |
|---|---|---|---|
| DR-001 | Specification and topology review | G3 | ⬜ not started |
| DR-002 | Microstrip realization review | G6 | ⬜ not started |
| DR-003 | PCB / layout review before ordering | G9 | ⬜ not started |

## Structure of a review

```
Review ID:
Date:
Reviewed by:            (student self-review, and separately Artan where he is available)
Artefact under review:  (file paths and commit SHA — a review of an un-identified artefact is worthless)

Checklist:              each item PASS / FAIL / N-A, with evidence
Findings:               numbered, each with a severity
Actions:                numbered, each with an owner
Re-review needed?:      yes/no
Gate outcome:           PASSED / NOT PASSED
```

**Record the commit SHA.** A review refers to a specific state of the design. Without the SHA,
nobody can tell later what was actually reviewed — least of all a future session.

**A FAIL is a successful review.** Finding a problem at DR-002 costs an afternoon; finding the same
problem after fabrication costs the lead time plus the board.
