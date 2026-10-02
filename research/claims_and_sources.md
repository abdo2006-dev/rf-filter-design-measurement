# CLAIMS AND SOURCES

*Every load-bearing technical claim, and what backs it.*

**Rule.** A claim with no row here has no standing. It may not appear in the engineering report or
in the seminar. If an AI (including the one that wrote this file) asserts something load-bearing,
it gets a row, a source and a verification status — or it gets removed.

**Rule.** A claim whose source is UNVERIFIED may be used for internal planning but **not** in the
report or the seminar.

---

## Legend

- **Claim** — the assertion, stated so it could be checked or falsified.
- **Source** — bibliography ID + section pointer.
- **Status** — verification status of the *source* (from `verification_log.md`).
- **Used in** — where the claim currently appears.
- **Check at** — the gate or phase at which it must be confirmed by reading the source.

---

## C-group: project structure and methodology claims

| ID | Claim | Source | Status | Used in | Check at |
|---|---|---|---|---|---|
| C-01 | De-embedding can be expressed as removing known cascaded networks from a measured cascade, using scattering transfer (T) parameter matrices. | T2-02 (Keysight 5980-2784EN) | PARTIALLY VERIFIED | plan P8/P12, seminar slides 33–34 | P8 |
| C-02 | ADS can de-embed a fixture directly in simulation using a negation component model, without extra coupons. | T2-02 | PARTIALLY VERIFIED | G8 candidate inventory | P8 — **this is a candidate method; confirm it exists in our ADS version** |
| C-03 | When commercial fixtures are unavailable, the required calibration standards must themselves be constructed and characterized. | T2-03 (Keysight 5968-5329) | PARTIALLY VERIFIED | plan P8 rationale, G8 | P8 |
| C-04 | The IEEE-370 2x-thru (FIX-FIX) de-embedding method requires a *fabricated* 2x-thru structure. | T2-06 (IEEE Std 370-2020), corroborated by T4-01, T4-04 | PARTIALLY VERIFIED | **the justification for moving G8 before layout** | P8 |
| C-05 | The classical 2x-thru method assumes the left fixture, right fixture and 2x-thru reference share the same impedance. | T2-06, via T4-04 / T4-01 | PARTIALLY VERIFIED | G8 validity assumptions | P8 |
| C-06 | TRL calibration can place the reference plane in the microstrip medium, past the connector and any taper. | A6 (Caballero 2013), A9 (Engen & Hoer 1979), A5 | VERIFIED (A5, A6) / PARTIALLY VERIFIED (A9) | G8 candidate inventory, seminar slide 35 | P8 |
| C-07 | TRL was originally formulated by Engen & Hoer (1979) for the dual six-port ANA. | A9 | PARTIALLY VERIFIED | seminar, if TRL is mentioned | **confirm DOI before the seminar** |
| C-08 | Calibration standards realized directly in the microstrip section remove launcher, taper and feedline effects together. | A5 (Sci. Rep. 2024) | VERIFIED (source), claim PARTIALLY VERIFIED | G8 candidate inventory | P8 |
| C-09 | Naive inversion of cascaded matrices on noisy measured data can amplify noise and yield non-physical results. | general numerical-analysis principle; **no specific source yet** | **UNSOURCED** | plan P12, G13 | **P12 — find a proper source or restate as a reasoned caution, not a cited fact** |

## M-group: Momentum / planar EM claims

> **All M-group claims are currently too weak to use in the seminar.** They come from secondary
> descriptions of Keysight guidance, not from the documentation itself.

| ID | Claim | Source | Status | Used in | Check at |
|---|---|---|---|---|---|
| M-01 | Momentum's default mesh density is 20 cells per wavelength. | T2-05, via secondary summaries | PARTIALLY VERIFIED | G7 procedure | **P7 — confirm in installed ADS help** |
| M-02 | Roughly 20–30 cells per wavelength is typically needed for accurate results. | same | PARTIALLY VERIFIED | G7 procedure | P7 |
| M-03 | Too coarse a mesh prevents accurate current-distribution calculation and degrades S-parameter prediction. | same | PARTIALLY VERIFIED | G7 rationale | P7 |
| M-04 | Excessively fine meshing can introduce numerical error — refinement is not monotonically beneficial. | same | PARTIALLY VERIFIED | **G7 — the key reason a CST-style convergence rule does not transfer** | P7 |
| M-05 | Mesh frequency should be set to the highest simulated frequency, because cell size is fixed while wavelength shrinks with frequency. | same | PARTIALLY VERIFIED | G7 procedure | P7 — most common setup error |
| M-06 | Momentum is a 2.5-D method-of-moments surface solver, not a volumetric mesher. | general knowledge + T2-01 | PARTIALLY VERIFIED | G7 rationale, seminar slide 29 | P7 |
| M-07 | Keysight 5992-1479 contains a coupled-line microstrip bandpass filter case study. | T2-01, via search summary | PARTIALLY VERIFIED | P7 reference choice | **P7 — confirm on first read** |

## S-group: substrate and fabrication claims

| ID | Claim | Source | Status | Used in | Check at |
|---|---|---|---|---|---|
| S-01 | FR-4 εr varies ≈±10 % between manufacturing lots. | trade press / forums only | **UNVERIFIED** | risk R-04 narrative only | **replaced at G0 by the real datasheet. Never quote in the seminar.** |
| S-02 | FR-4 εr is frequency-dependent (≈4.7 at 100 MHz → ≈4.2 at 5 GHz). | trade press only | **UNVERIFIED** | risk R-04 narrative only | same |
| S-03 | FR-4 moisture absorption (≈0.10–0.15 %) further shifts εr. | trade press only | **UNVERIFIED** | risk R-04 narrative only | same |
| S-04 | Substrate εr tolerance shifts a filter's centre frequency measurably. | general theory (λ_g depends on ε_eff) — Pozar §3.8 | PARTIALLY VERIFIED | risk register, P6 tolerance study | P6 — **and then demonstrated by our own simulation, which is better than citing anyone** |

> **Note on S-01…S-03.** These are the kind of widely-repeated numbers that feel authoritative and
> are not. They are kept here *only* so a future session can see they were checked and rejected.
> At G0 the real laminate is named and its datasheet answers the question properly — and if the
> laminate turns out not to be FR-4, the whole group becomes irrelevant.

## F-group: filter theory claims

*Expected to be the largest group by P4. Currently near-empty by design: the theory has not been
read yet, and writing filter-theory claims before reading the chapter is exactly the behaviour
this file exists to prevent.*

| ID | Claim | Source | Status | Used in | Check at |
|---|---|---|---|---|---|
| F-01 | A filter can be designed from a specification via the insertion-loss method: normalized prototype → frequency/impedance scaling → transformation → physical realization. | T1-01 Pozar §8.3–8.4 | PARTIALLY VERIFIED (ToC-level) | plan P4, seminar slides 22–24 | **P3 — read §8.3–8.4** |
| F-02 | Chebyshev and Butterworth responses trade passband ripple against stopband roll-off at equal order. | T1-01 Pozar §8.3 | PARTIALLY VERIFIED | plan P3, seminar slide 20 | P3 |
| F-03 | Required filter order follows analytically from a stopband attenuation requirement at a stated frequency. | T1-01 Pozar §8.3 | PARTIALLY VERIFIED | plan P4, gate G4 | P4 |
| F-04 | Microstrip guided wavelength is shorter than free-space wavelength, set by effective permittivity. | T1-01 Pozar §3.8 | PARTIALLY VERIFIED | plan P6, seminar slide 28 | P6 |
| F-05 | In parallel-coupled-line filters the inter-resonator gap sets the coupling, so narrow bandwidth demands small gaps. | T1-02 Hong & Lancaster *(chapter TBD)* | **UNVERIFIED (chapter unknown)** | topology matrix, risk R-06 | **P3 — fill in the chapter, then confirm** |

## R-group: claims about our own results

**Empty, and must stay empty until results exist.**

No row may be added here from a prediction, an expectation, or a simulation that has not been run.
Each row, when it comes, cites a result-register ID and a committed file — not a plot the student
remembers seeing.

| ID | Claim | Source | Status |
|---|---|---|---|
| — | *(none)* | — | — |

---

## Audit log

| Date | Action |
|---|---|
| 2026-10-02 | File created. 25 claims recorded: 1 UNSOURCED (C-09), 3 UNVERIFIED (S-01…S-03), 1 UNVERIFIED-by-missing-chapter (F-05), rest PARTIALLY VERIFIED. **Zero claims currently qualify for use in the seminar without further reading.** |
