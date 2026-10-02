# FILTER SPECIFICATION

**Status: NOT SPECIFIED. This is a form, not a specification.**

> **This document is empty on purpose.** Writing a filter specification now would mean inventing
> numbers, and the invented numbers would then propagate into every calculation in the project and
> be nearly impossible to dislodge. Gate **G3** fills it, after **G0** supplies the constraints and
> **D-003** chooses the topology.

**Gate:** G3 · **Blocked by:** G0, D-003, D-004 · **Filled at:** P3

---

## 1. Specification

| # | Parameter | Value | Requirement or arbitrary? | Source / rationale | Status |
|---|---|---|---|---|---|
| FR-01 | Filter class | — | — | — | **BLOCKED** |
| FR-02 | Topology | — | — | — | **BLOCKED** (D-003) |
| FR-03 | Response type | — | — | — | **BLOCKED** (D-004) |
| FR-04 | Order | — | — | — | **BLOCKED** — must be **derived** at G4, not chosen |
| FR-05 | Centre / cut-off frequency | — | — | — | **BLOCKED** (D-002) |
| FR-06 | Bandwidth / fractional bandwidth | — | — | — | **BLOCKED** |
| FR-07 | Passband ripple or flatness | — | — | — | **BLOCKED** |
| FR-08 | Max passband insertion loss | — | — | — | **BLOCKED** |
| FR-09 | Min passband return loss | — | — | — | **BLOCKED** |
| FR-10 | Stopband attenuation @ stated frequency | — | — | — | **BLOCKED** — drives FR-04 |
| FR-11 | Port impedance | 50 Ω | requirement | follows from the VNA and connector | **PROVISIONAL** |
| FR-12 | Frequency range the spec is claimed over | — | — | — | **BLOCKED** — bounded by VNA range |
| FR-13 | Max board size | — | — | — | **BLOCKED** |
| FR-14 | Min manufacturable feature | — | — | — | **BLOCKED** |

### The "requirement or arbitrary?" column

Every row must declare which it is. This project has **no external customer**, so most of the
specification will legitimately be *arbitrary learning targets* bounded by what is manufacturable
and measurable.

**That is fine — but it must be said.** A specification presented as a requirement when it was
actually chosen for convenience is the most common form of dishonesty in student engineering
reports, and it is detectable: an experienced reader asks "why 2.4 GHz?" and the answer has to be
better than "it is a common frequency."

Acceptable rationales for an arbitrary value:
- "Chosen so the stopband lies inside the VNA's range" — a real constraint.
- "Chosen so the required gap is ≥2× the fabricator's minimum" — a real constraint.
- "Chosen to keep the board under X mm" — a real constraint.

Not acceptable:
- "Common frequency." / "Typical value." / "Standard choice." — these are not reasons.

---

## 2. Realizability pre-check *(G3 requirement)*

| Check | Result | Status |
|---|---|---|
| Required minimum gap vs fabricator minimum, with margin | — | **BLOCKED** |
| Narrowest line width vs fabricator minimum, with margin | — | **BLOCKED** |
| Board size vs fabricator maximum | — | **BLOCKED** |
| Stopband extent vs VNA frequency range | — | **BLOCKED** |
| Passband insertion loss vs substrate tanδ | — | **BLOCKED** |
| Response under εr tolerance | — | **BLOCKED** |
| Response under etch tolerance | — | **BLOCKED** |

> **A specification that fails this pre-check is not a specification, it is a wish.** The whole
> point of running the check at G3 — before any dimension is calculated — is that it is free to
> change the specification then and expensive to change it after P6.

---

## 3. Analytical predictions *(filled at G4, used to falsify P5)*

The specification's purpose is to generate **falsifiable predictions**. These are written at G4,
before simulation, and are what P5 checks against.

| # | Prediction | Predicted value | Simulated (P5) | Microstrip (P6) | EM (P7) | Measured (P11) |
|---|---|---|---|---|---|---|
| PR-1 | Insertion loss at f₀ | — | — | — | — | — |
| PR-2 | Return loss at f₀ | — | — | — | — | — |
| PR-3 | Attenuation at stopband frequency 1 | — | — | — | — | — |
| PR-4 | Attenuation at stopband frequency 2 | — | — | — | — | — |
| PR-5 | 3 dB bandwidth | — | — | — | — | — |
| PR-6 | f₀ | — | — | — | — | — |

**This table is the project.** When it is full, the core engineering question is answered — the
row-by-row drift from column to column *is* the answer to "how closely can a theoretically
designed filter reproduce its intended response as we move from analysis to measurement?"

It also enforces honesty structurally: a blank cell is visible, and a cell cannot be filled from
expectation. Each filled cell cites a result-register ID.

---

## 4. Sign-off

| Item | Status |
|---|---|
| G0 passed | ☐ |
| Topology chosen (D-003), runners-up documented | ☐ |
| Every FR row filled, with requirement/arbitrary declared | ☐ |
| Realizability pre-check passed with margin | ☐ |
| Design review DR-001 complete | ☐ |
| Mentor has seen specification and topology | ☐ |
| **Gate G3 passed** | ☐ |
