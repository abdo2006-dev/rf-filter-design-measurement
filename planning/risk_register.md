# RISK REGISTER

*Probability × Impact, with a **trigger** (the observable that says the risk is materializing) and
a **fallback** (what we do instead). A mitigation without a trigger is a wish.*

**Scales.** Probability: Low / Medium / High. Impact: Low / Medium / High / **Critical**
(Critical = the project cannot complete as scoped).

**Review:** at every gate.

---

## Summary

| ID | Risk | P | I | Owner |
|---|---|---|---|---|
| R-01 | ADS beginner learning curve | High | Medium | student |
| R-02 | ADS licence availability | Medium | High | Artan/lab |
| R-03 | Insufficient RF theory to judge recommendations | High | High | student |
| R-04 | Unknown / inaccurate substrate data | High | High | Artan/lab |
| R-05 | Substrate parameter tolerance | High | Medium | physics |
| R-06 | Minimum manufacturable gap too large for the chosen topology | Medium | High | fabricator |
| R-07 | Etch tolerance shifts the response | High | Medium | fabricator |
| R-08 | PCB fabrication delay | Medium | High | fabricator |
| R-09 | Poor SMA launch quality | Medium | Medium | student |
| R-10 | Poor measurement repeatability | Medium | High | student |
| R-11 | VNA availability | Medium | **Critical** | lab |
| R-12 | Calibration kit unavailable or incomplete | Medium | High | lab |
| R-13 | Calibration error | Medium | High | student |
| R-14 | Overclaiming in attribution or on the CV | Medium | High | student |
| R-15 | Scope creep / project consumes too much university time | **High** | **Critical** | student |
| R-16 | Optimizing before understanding the baseline | Medium | Medium | student |
| R-17 | Fixture characterization not possible | Medium | Low* | — |
| R-18 | De-embedding numerically unstable | Medium | Low* | — |
| R-19 | Reporting a non-physical de-embedded result | Low | High | student |
| R-20 | Mentor unavailable / slow response | Medium | High | — |
| R-21 | S/T-parameter convention error | Medium | High | student |
| R-22 | AI-generated unsupported claim accepted as fact | **High** | **High** | student |
| R-23 | Treating circuit and EM models as equivalent | Medium | Medium | student |
| R-24 | Momentum unavailable or simulation too slow | Medium | Medium | lab |
| R-25 | Connector wear / damage | Medium | Medium | student |
| R-26 | Copyright or figure-licensing mistake | Medium | High | student |
| R-27 | Proprietary lab information published | Low | **Critical** | student |
| R-28 | Seminar pitched wrongly for a maths audience | Medium | Medium | student |
| R-29 | Loss of work (ephemeral container, no backup) | Medium | **Critical** | student |

*\* Low impact because de-embedding is a stretch goal by design — a clean no-go is an acceptable
outcome. The *reporting* of a bad result (R-19) is what carries real impact.*

---

## Detail

### R-01 — ADS beginner learning curve
**P** High · **I** Medium
**Mitigation.** Start with one transmission line, not a filter (P1). Use the Keysight Learning Kit,
which targets exactly this position. Prediction-before-simulation so that software errors are
caught as physics mismatches.
**Trigger.** More than ~15 hours in P1 without a working swept simulation.
**Fallback.** Ask Artan for a 30-minute screen-share. One hour of a competent user beats twenty of
guessing — this is the highest-leverage help available in the whole project.

### R-02 — ADS licence availability
**P** Medium · **I** High
**Mitigation.** Confirm at G0 (Round 1 Q4), including Momentum. Learn licence checkout etiquette if
the licence is shared.
**Trigger.** Licence denied, or contention making work impractical.
**Fallback.** Do theory and `scikit-rf`/QUCS-S work labelled as non-ADS; batch ADS work into
sessions when the licence is free. **The ADS competence claim requires ADS**, so non-ADS results are
a holding pattern, not a substitute.

### R-03 — Insufficient RF theory to judge recommendations
**P** High · **I** High — *acknowledged by the student, which is why the controls exist*
**Mitigation.** Gates require *explanation*, not just output. Theory map gives a test per concept.
Every claim needs a source. Artan is the external reality check.
**Trigger.** Unable to explain a result at a gate; or accepting a formula without a textbook check.
**Fallback.** Stop. Go back one theory block. A gate failure is the system working.

### R-04 — Unknown / inaccurate substrate data
**P** High · **I** High
**Mitigation.** G0 requires the real datasheet, **including the frequency at which εr is quoted** —
a datasheet εr at 1 MHz is nearly useless at 3 GHz. Tolerance study at P6.
**Trigger.** No datasheet available; or measured f₀ offset from simulation beyond the tolerance
study's predicted range.
**Fallback.** Extract ε_eff from the measured board (a bounded extraction, not a characterization
project) and re-simulate. This *closes the loop* and is one of the best results the project could
produce — a risk that converts into a finding.

### R-05 — Substrate parameter tolerance
**P** High · **I** Medium
**Mitigation.** Tolerance study at P6 over εr, h and etch, before fabrication. Prefer a design with
tolerance margin over one that is nominally better.
**Trigger.** Tolerance study shows the specification is only met at nominal values.
**Fallback.** Relax the specification, reduce order, widen bandwidth, or choose a less
tolerance-sensitive topology. **Decide this before fabrication, not after.**

### R-06 — Minimum manufacturable gap too large for the chosen topology
**P** Medium · **I** High
**Mitigation.** G0 captures the minimum gap *before* G3 chooses the topology — this ordering exists
for this risk. Realizability pre-check is a G3 requirement. Note that published hairpin designs
with ~0.1 mm resonator spacing (paper A7) are below many low-cost processes' limits.
**Trigger.** Synthesis demands a gap below the fabricator's minimum, or within its tolerance.
**Fallback.** Next-ranked topology from the matrix. Stepped-impedance LPF is the structural
fallback of last resort — **it has no critical gap at all**, which is precisely why it is on the
candidate list.

### R-07 — Etch tolerance shifts the response
**P** High · **I** Medium
**Mitigation.** Include etch tolerance in the P6 study. Record the margin on every dimension.
**Trigger.** Measured response differs from simulation in the direction and magnitude predicted by
an etch bias.
**Fallback.** Report it as an attributed discrepancy — this is a *result*, not a defect. If a second
board is possible, apply an etch-bias correction and re-fabricate: a genuinely strong outcome.

### R-08 — PCB fabrication delay
**P** Medium · **I** High — *the largest schedule risk*
**Mitigation.** Capture lead time at G0. Order as early as G9 allows. **Order spares.**
**Trigger.** Lead time exceeds the margin before the seminar date.
**Fallback.** Commercial prototype service in parallel; switch the seminar to version C. The
seminar's three-version design exists for this risk.

### R-09 — Poor SMA launch quality
**P** Medium · **I** Medium
**Mitigation.** Use the connector datasheet's recommended footprint exactly; ask Artan for a
known-good footprint the group already trusts (Round 1 Q3) — worth more than any reading. Practise
soldering on a scrap coupon first.
**Trigger.** Poor or erratic return loss at the launch; visibly bad solder joint.
**Fallback.** Re-solder; use a spare board; include the launch in the de-embedding discussion. A
bad launch is itself evidence for the stretch question.

### R-10 — Poor measurement repeatability
**P** Medium · **I** High
**Mitigation.** G11 requires ≥3 reconnect cycles and a quantified spread. Torque wrench if one
exists. Fixed cable positions.
**Trigger.** Spread across repeats comparable to the simulation/measurement discrepancy being
claimed — at which point no attribution is defensible.
**Fallback.** More repeats, better connector discipline, and widen the stated uncertainty.
**Never claim a discrepancy smaller than the repeatability.**

### R-11 — VNA availability
**P** Medium · **I** **Critical**
**Mitigation.** Confirm at G0 (Round 1 Q3), including frequency range *before* the frequency is
chosen. Book time early. Complete lab induction early.
**Trigger.** No access within 4 weeks of the board arriving.
**Fallback.** Seek departmental or other-group access. If genuinely unavailable: report the project
honestly as simulation-complete and measurement-pending; seminar version C. **Never present a
simulated curve as measured** — this is an integrity line, not a preference.

### R-12 — Calibration kit unavailable or incomplete
**P** Medium · **I** High
**Mitigation.** G0 asks which kits physically exist, not which methods are theoretically possible.
G8 chooses the method from what exists.
**Trigger.** No kit for the connector type; or no kit definition data.
**Fallback.** Use whatever calibration is available and state its limitations; or an
electronic-calibration module if one exists; or document that de-embedding is unsupported (G13
no-go) and present the comparison at the available reference plane.

### R-13 — Calibration error
**P** Medium · **I** High
**Mitigation.** G10 requires a **verification** measurement of a standard not used in the
calibration. Save and export the instrument state.
**Trigger.** Verification standard does not match its expected response.
**Fallback.** Recalibrate; check standard definitions and kit ID; ask for the lab's procedure.
**An unverified calibration produces data that cannot support any claim.**

### R-14 — Overclaiming in attribution or on the CV
**P** Medium · **I** High
**Mitigation.** G12 requires evidence for every attribution and an explicit list of *unexplained*
discrepancies. The CV paragraph is written at P13 from what exists.
**Trigger.** A sentence in the report or on the CV that the repository cannot support with a file.
**Fallback.** Rewrite to what is true. "Designed, simulated and measured" is already a strong
second-year claim; it does not need inflating.

### R-15 — Scope creep
**P** **High** · **I** **Critical** — *the failure mode of both previous projects*
**Mitigation.** Hard stop line in the plan. Explicit non-requirements. `alternatives.md` as the
idea sink. `reading_queue.md` §3 as the curiosity sink. Gates prevent skipping forward.
**Trigger.** Any of: a new idea entering the plan rather than `alternatives.md`; the reading queue
growing faster than the project; a second filter being considered; coursework slipping.
**Fallback.** Freeze scope at the current gate. Finish the narrowest version that satisfies the
definition of done. **A finished small project beats an abandoned large one — that is the whole
lesson of the previous two projects.**

### R-16 — Optimizing before understanding the baseline
**P** Medium · **I** Medium
**Mitigation.** G5 forbids it explicitly: the unoptimized hand-designed baseline must be committed
to the result register before any tuner or optimizer is used.
**Trigger.** Reaching for the optimizer because the response is not right.
**Fallback.** Revert to the baseline, do the sensitivity study, understand the mechanism, and only
then optimize — if at all.

### R-17 — Fixture characterization not possible
**P** Medium · **I** Low *(by design)*
**Mitigation.** G8 decides early enough that the needed copper can be fabricated.
**Trigger.** G8 finds no candidate whose assumptions can be met.
**Fallback.** Record "de-embedding not supported by available resources", scope to P11, seminar
version B. **This is a permitted, documented outcome** (G13).

### R-18 — De-embedding numerically unstable
**P** Medium · **I** Low *(by design)*
**Mitigation.** G13 requires passivity, reciprocity, plausibility and a perturbation-stability
check before any de-embedded result is reported.
**Trigger.** Any failed check; |S₂₁| > 1; wild frequency-to-frequency variation.
**Fallback.** Report the instability itself as the finding — "the data did not support inversion,
and here is why" is a genuinely interesting result and an excellent seminar beat.

### R-19 — Reporting a non-physical de-embedded result
**P** Low · **I** High
**Mitigation.** G13's checks exist for exactly this. The danger is that a bad de-embedded curve can
look *more* plausible than the real one.
**Trigger.** A de-embedded result that is "better than expected" — treat improvement as suspicious,
not as success.
**Fallback.** Do not report it. Go back to the checks.

### R-20 — Mentor unavailable / slow
**P** Medium · **I** High
**Mitigation.** Batched, grouped, short questions (`questions_for_artan.md`). Round 1 front-loads
cheap factual questions so a partial answer still unblocks work.
**Trigger.** No answer in 2 weeks.
**Fallback.** Proceed with a *declared* hypothetical constraint set, labelled PROVISIONAL
throughout, treating the design track as a rehearsal. Alternatively find the facts directly — the
fabricator's rules and the VNA's manual are public. **Never let a hypothetical silently become
CONFIRMED.**

### R-21 — S/T-parameter convention error
**P** Medium · **I** High
**Mitigation.** G2 requires the convention and reference impedance to be stated explicitly
alongside every conversion, and a hand-vs-ADS cross-check. Ask Artan which convention the group
uses.
**Trigger.** Hand calculation and ADS disagree; or a de-embedded result is subtly wrong in a way
that looks like a transposition.
**Fallback.** Re-derive from one textbook's definitions only. **Do not mix sources for T-parameter
definitions** — this error is silent, survives plausibility checks, and would invalidate P12.

### R-22 — AI-generated unsupported claim accepted as fact
**P** **High** · **I** **High** — *explicitly raised by the student*
**Mitigation.** `claims_and_sources.md` with per-claim verification status. UNVERIFIED claims may
not enter the report or the seminar. `verification_log.md` states plainly that this bootstrap
opened no PDFs. Gates require explanation in the student's own words.
**Trigger.** A claim in the repository with no row in the claims file; or an inability to say where
a number came from.
**Fallback.** Delete the claim or source it. **Note: this bootstrap itself is an instance of this
risk.** Several of its claims are PARTIALLY VERIFIED or UNVERIFIED and are marked as such. Treat
this repository's technical assertions as hypotheses to confirm, not as findings.

### R-23 — Treating circuit and EM models as equivalent
**P** Medium · **I** Medium
**Mitigation.** Separate phases (P6, P7) and separate gates (G6, G7). The difference between them
is recorded as a result, not smoothed over.
**Trigger.** Reporting "the simulation" without saying which model.
**Fallback.** Always name the model. The five-way comparison table at G12 enforces this.

### R-24 — Momentum unavailable or too slow
**P** Medium · **I** Medium
**Mitigation.** G0 confirms the licence. Benchmark a small structure before the full layout.
**Trigger.** No Momentum licence; or a single sweep that does not finish in a usable time.
**Fallback.** Reduce the frequency sweep, use adaptive frequency sampling, simplify the geometry,
or declare P7 unavailable. **Then say "circuit and microstrip simulation" on the CV and omit EM.**
Do not substitute another solver and call it Momentum.

### R-25 — Connector wear / damage
**P** Medium · **I** Medium
**Mitigation.** Torque wrench if available; minimize connect cycles; inspect before mating; never
force a connection.
**Trigger.** Degrading repeatability over a session; visible damage.
**Fallback.** Replace the connector/cable; re-calibrate; note it in the measurement log. **Damaging
a lab calibration standard is a serious and expensive mistake** — ask before handling.

### R-26 — Copyright or figure-licensing mistake
**P** Medium · **I** High
**Mitigation.** `source_hierarchy.md` copyright rules; `.gitignore` blocks `*.pdf`;
`seminar/asset_register.md` requires a licence field before a figure reaches a slide; default
behaviour is redraw-and-cite.
**Trigger.** Any external figure without a completed asset-register row.
**Fallback.** Remove it and redraw. **Also applies to ADS example files** — do not commit
proprietary workspaces if redistribution is prohibited.

### R-27 — Proprietary lab information published
**P** Low · **I** **Critical** — *low probability, unrecoverable consequence*
**Mitigation.** Record capabilities, not identities. Explicit exclusion list in
`source_hierarchy.md`. Repository is **private**.
**Trigger.** Any serial number, licence key, internal path, unpublished group result, or anything
Artan shared in confidence appearing in a file.
**Fallback.** Remove it, **rewrite git history if it was ever pushed**, and tell Artan. A full
review against the exclusion list is a mandatory P13 task before the repository is shown to anyone
outside the project.

### R-28 — Seminar pitched wrongly for a maths audience
**P** Medium · **I** Medium
**Mitigation.** S0 defines the audience first. Narrative before equations. Timed rehearsal at S8
with cuts at S9. Target: every slide answers a question the previous slide raised.
**Trigger.** Rehearsal overruns; or a test listener cannot say what the talk was about.
**Fallback.** Cut RF detail, keep the mathematics — the audience is mathematicians, and the
matrices are the part they will actually enjoy. Non-commutativity and inverting a cascade are the
hooks, not filter synthesis.

### R-29 — Loss of work
**P** Medium · **I** **Critical**
**Mitigation.** `PERSISTENCE.md`. Git bundle + zip produced at bootstrap. GitHub repository to be
created manually.
**Trigger.** More than one working session's work existing in only one place.
**Fallback.** None. **This risk has no recovery, only prevention.** The bootstrap session could not
create the GitHub repository (D-007) — until that is done manually, the project is one lost file
from gone.
