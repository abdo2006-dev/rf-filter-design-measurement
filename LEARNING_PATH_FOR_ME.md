# LEARNING_PATH_FOR_ME

*This file exists so I never have to look at the whole RF curriculum at once.*

**It tells me what to learn NOW and what I am allowed to ignore.**
Update it when a gate passes. Nothing else in the repository overrides it for study planning.

---

# ▶ YOU ARE HERE

## Transmission lines

Specifically: the idea that at GHz frequencies a piece of copper is no longer a node but a
*medium that waves travel along*.

## WHY

Everything in this project is a transmission line. The filter is made of transmission lines. The
cables are transmission lines. The connector is a transmission line discontinuity. The first ADS
experiment in P1 is a single transmission line with a load on the end, and I cannot interpret its
output without this block.

It is also the first 15 minutes of the seminar, which I have to be able to teach, not just use.

## LEARN NOW

- **Travelling waves on a line** — forward wave, backward wave, why a reflection exists at all.
- **Characteristic impedance Z₀** — what it is, what it is *not* (it is not a resistance you can
  measure with a multimeter).
- **Electrical length** — βl, and why "short" and "long" are frequency-dependent words.
- **Guided wavelength λ_g** vs free-space wavelength λ₀, and why the substrate changes it.
- **Reflection coefficient Γ = (Z_L − Z₀)/(Z_L + Z₀)** — and the three cases that build intuition:
  open, short, matched.
- **S₁₁ as a measured Γ**, and return loss in dB.
- **Input impedance of a terminated line**, at least qualitatively — the fact that a line
  *transforms* impedance, and that a quarter-wave line is special.

**Target:** about 6–10 focused hours. Pozar ch. 2 (§2.1–2.3, 2.5–2.7) is the main source; the
Keysight RF Design Software Learning Kit chapter on transmission lines is the ADS-side companion.

## DO NOT LEARN YET

Seriously — close the tab if you find yourself reading any of these:

- Chebyshev / Butterworth prototype synthesis, g-values, element tables
- Richards' transformation, Kuroda's identities
- Even- and odd-mode analysis of coupled lines
- Coupling coefficients, external Q, coupling matrices
- SOLT, TRL, LRM, 12-term error models
- De-embedding algorithms, T-parameter inversion, IEEE 370
- Momentum meshing, Green's functions, method of moments
- Smith chart manipulation beyond "this is what it is"
- Group delay, dispersion, higher-order modes, radiation

They are all in the plan. They all have a phase. None of them is now.

## HOW I KNOW I AM DONE WITH THIS BLOCK

I can do all five of these without notes:

1. Explain to a maths student, in under two minutes and with one drawing, why a 10 cm wire is
   fine at 50 Hz and is a problem at 3 GHz.
2. Compute Γ for a 50 Ω line terminated in 75 Ω, 0 Ω, ∞ Ω and 50 Ω, and say what each means
   physically.
3. Convert |Γ| = 0.1 to return loss in dB and back.
4. Say what λ_g is for a given substrate and frequency, and why it is shorter than λ₀.
5. Look at an S₁₁ plot and say whether the thing is well matched, without being told.

## AFTER THIS

**S-parameters and two-port networks** (theory block C, project phase P2).
Then — and only then — matrices and cascading (block D), which is where the seminar's
mathematical core lives.

---

# The road, compressed

So I can see that there *is* an end, without having to look at the details:

| Block | Topic | Gate it serves | Status |
|---|---|---|---|
| A | Prerequisites: phasors, complex impedance, dB | — | assumed from coursework, verify |
| **B** | **Transmission lines** | **G1** | **◀ YOU ARE HERE** |
| C | S-parameters, two-port networks | G2 | not yet |
| D | ABCD / T matrices, cascading, non-commutativity | G2 | not yet |
| E | Filter fundamentals, prototypes, response types | G3, G4 | not yet |
| F | Microstrip realization, coupled lines | G6 | not yet |
| G | VNA, reference planes, calibration | G10 | not yet |
| H | De-embedding | G13 | not yet, may never be needed |

Full concept-by-concept breakdown with tests: `theory/theory_dependency_map.md`.
Do not read it as a syllabus. Read it only when a gate tells you to.

---

# Rules I set for myself

1. **One block at a time.** If I am reading about something in "DO NOT LEARN YET", I have gone
   off the plan and the project gets slower, not faster.
2. **I must be able to teach it.** The seminar audience is maths students. If I cannot explain a
   concept with one drawing and no jargon, I do not understand it yet.
3. **Theory follows the gate, not my curiosity.** Curiosity is logged in
   `research/reading_queue.md` and read later.
4. **An AI explanation is a starting point, not an authority.** Anything load-bearing gets checked
   against Pozar or Hong & Lancaster and recorded in `research/claims_and_sources.md`.
5. **If I am stuck for more than 45 minutes, it goes to Artan**, in the next batched message —
   not as a separate interruption.
