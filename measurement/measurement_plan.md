# MEASUREMENT PLAN

**Status: strategy UNDECIDED. This document must be completed before PCB layout begins (gate G8).**

> **Why this exists before the board.** Every realistic de-embedding method needs something
> physical that has to be fabricated — TRL standards, a 2x-thru coupon, a characterizable launch.
> After fabrication, the available methods are exactly those the copper supports. See decision
> D-001.

---

## 1. The measurement chain

Written out so every reference plane has a name. **Calibration moves the reference plane;
de-embedding moves it further.** Being vague about which plane a number refers to is the most
common error in fixtured measurement.

```
  [VNA port 1]
       │                          ← plane RP0: VNA test port (instrument's own reference)
    cable 1
       │                          ← plane RP1: end of cable / connector interface
   connector 1
       │                          ← plane RP2: coax-to-microstrip launch
   feed line 1
       │                          ← plane RP3: start of the DUT proper
  ┌────┴────┐
  │ FILTER  │                     ← the thing we actually want
  └────┬────┘
       │                          ← plane RP4: end of the DUT proper
   feed line 2
       │
   connector 2                    ← plane RP5
    cable 2
       │
  [VNA port 2]                    ← plane RP6
```

> **Naming note.** Reference planes are **RP0–RP6** to keep them distinct from the project's
> phase names (P0–P14). A sentence about "plane P3" would otherwise be ambiguous.

| | |
|---|---|
| **A standard coaxial calibration** puts the reference plane at | **RP1** (or RP0/RP1 depending on kit and cables) |
| **The thing we want** is the network between | **RP3 and RP4** |
| **Everything between RP1–RP3 and RP4–RP5 is the fixture** | ← this is what de-embedding would remove |
| **The Momentum model's result** is referenced at | whatever its port calibration setting defines — typically ≈RP3/RP4 |

> **That last line is the key insight of the whole project.** The EM simulation already gives a
> de-embedded answer, because EM port calibration *is* de-embedding inside the simulator (theory
> concept T50). So "measurement disagrees with Momentum" is partly an artefact of comparing results
> at **different reference planes** — which is precisely the stretch question, and the cleanest
> comparison available is de-embedded measurement vs Momentum.

| Field | Value | Status |
|---|---|---|
| Calibration method | — | **BLOCKED** (D-006, G8) |
| Reference plane after calibration | — | **BLOCKED** |
| De-embedding method | — | **BLOCKED** (D-006, G8) |
| Reference plane after de-embedding | — | **BLOCKED** |

---

## 2. De-embedding candidate inventory

**Do not prejudge.** Each candidate is listed with what it needs, what it assumes, and how it
fails. Selection happens at G8, after Artan Round 2, from what physically exists.

### Candidate 1 — Calibrate to the coaxial plane, then de-embed a simulated fixture model

| | |
|---|---|
| **Needs** | A working coax calibration; an EM model of the launch + feed line |
| **Copper needed on the panel** | **None** — this is its main attraction |
| **Assumes** | The EM model of the launch is accurate; the as-built launch matches the model; the solder joint is reproducible |
| **How it fails** | Silently. If the launch model is wrong, the "de-embedded" result is confidently wrong, and there is no internal check that catches it |
| **Authority** | Keysight 5980-2784EN (claim C-02 — ADS can de-embed a fixture via a negation model) |
| **Verdict** | Attractive and cheap. **Weakest on validation** — the thing it assumes is the thing hardest to verify, since the connector transition is exactly what EM models least reliably |

### Candidate 2 — TRL with on-board microstrip standards

| | |
|---|---|
| **Needs** | Thru, reflect and one or more line standards fabricated in microstrip on the same panel; VNA support for TRL; connectors for each standard |
| **Copper needed** | **Yes — several coupons**, each with its own connectors |
| **Assumes** | Standards are identical to the DUT's launches; the reflect is the same on both ports; line length sets a usable band (a line standard covers roughly an 8:1 frequency span before phase ambiguity) |
| **How it fails** | Band edges where the line approaches 0° or 180° of extra phase; non-identical launches; too few lines for the span |
| **Authority** | Engen & Hoer 1979 (A9); A6 Caballero 2013 as a planar precedent; A5 as a method survey (claims C-06, C-08) |
| **Verdict** | The **most rigorous** option, and the one that moves the reference plane into the microstrip medium where we actually want it. Costs the most panel area and connectors |

### Candidate 3 — IEEE-370-style 2x-thru de-embedding

| | |
|---|---|
| **Needs** | A fabricated 2x-thru (FIX-FIX) coupon: two fixtures connected back to back, each identical to the DUT's fixture |
| **Copper needed** | **Yes — one coupon**, plus connectors |
| **Assumes** | Left fixture, right fixture and the 2x-thru reference share the same impedance (claim C-05); fixture halves are symmetric and reciprocal |
| **How it fails** | Impedance mismatch between the coupon and the actual fixture halves; the standard's impedance-corrected variant exists precisely because this assumption often breaks |
| **Authority** | IEEE Std 370-2020 (T2-06, claim C-04); open implementation in `scikit-rf` (T4-01) |
| **Verdict** | **One coupon for a complete method** — the best copper-to-capability ratio. Open-source implementation means the algorithm can actually be read and checked, which matters a lot for a student who must be able to defend it. Note the standard targets interconnects to 50 GHz, which is not our regime |

### Candidate 4 — Port extension / electrical delay only

| | |
|---|---|
| **Needs** | Nothing beyond the calibration |
| **Copper needed** | None |
| **Assumes** | The fixture is a pure delay — i.e. matched and lossless |
| **How it fails** | It does not. It simply does not remove reflections or loss, only phase |
| **Verdict** | **Honest if labelled honestly.** But it does not answer the stretch question, because the interesting part of the fixture effect *is* the reflection. Useful as a baseline to show how much the crude correction misses |

### Candidate 5 — Thru-only bisection

| | |
|---|---|
| **Needs** | A thru coupon |
| **Copper needed** | One small coupon |
| **Assumes** | The thru is exactly two identical fixture halves; symmetry; a chosen bisection method |
| **How it fails** | Bisection is not unique without further assumptions; asymmetry corrupts it directly |
| **Verdict** | A cheap partial option. Mostly worth having because **a thru coupon is useful anyway** — it is the single best sanity check on launch quality, whatever method is chosen |

### Candidate 6 — No de-embedding

| | |
|---|---|
| **Needs** | Nothing |
| **Assumes** | Nothing |
| **Verdict** | **A legitimate, documented outcome** (gate G13). The measured result at the connector plane is still a real result; the fixture effects are then discussed qualitatively and, if an EM fixture model exists, *illustrated* in simulation without claiming an extracted DUT response. Seminar version B is built for this |

### Comparison

| | Copper | Connectors | Rigour | Checkability | Risk |
|---|---|---|---|---|---|
| 1 — simulated fixture model | none | none | medium | **low** | silent error |
| 2 — TRL | high | high | **high** | high | band limits, panel cost |
| 3 — 2x-thru | **low** | low | medium–high | **high** | impedance assumption |
| 4 — port extension | none | none | low | high | does not answer the question |
| 5 — thru bisection | low | low | low–medium | medium | asymmetry |
| 6 — none | none | none | n/a | n/a | none |

> **Pre-G8 observation, not a decision.** Candidates 3 and 5 have the best capability-per-coupon
> ratio, and **a thru coupon is worth fabricating under almost any outcome** — it costs little, it
> validates the launches independently of any de-embedding, and it keeps options 3 and 5 open.
> Recording this now so that if panel area is tight, the thru is the last coupon to be cut.
> **The actual choice is made at G8, with Artan, from what the lab has.**

---

## 3. Test structures on the panel

| Structure | Purpose | Include? | Status |
|---|---|---|---|
| The filter (DUT) | the measurement | yes | **CONFIRMED** |
| Thru line | launch validation; enables candidates 3/5 | — | **BLOCKED** (G8) |
| 2x-thru | candidate 3 | — | **BLOCKED** (G8) |
| TRL line standard(s) | candidate 2 | — | **BLOCKED** (G8) |
| TRL reflect (open or short) | candidate 2 | — | **BLOCKED** (G8) |
| Bare 50 Ω line of known length | ε_eff extraction; R-04 fallback; Momentum benchmark | — | **BLOCKED** (G8) — *cheap and useful under every scenario* |
| Resonator coupon for εr extraction | substrate validation | — | **BLOCKED** (G8) — probably out of scope |

**Panel budget** — fill at G8:

| | |
|---|---|
| Board area available | — |
| Area per coupon | — |
| Connectors available / cost each | — |
| **Limiting factor** | usually **connectors**, not area |

---

## 4. Measurement procedure *(fill at P10/P11)*

| Setting | Value | Status |
|---|---|---|
| Frequency span | — | BLOCKED — must exceed the band of interest on both sides |
| Number of points | — | BLOCKED |
| IF bandwidth | — | BLOCKED |
| Source power | — | BLOCKED |
| Averaging | — | BLOCKED |
| Parameters measured | S₁₁, S₂₁, S₁₂, S₂₂ | CONFIRMED — **all four**; S₁₂ and S₂₂ are what let reciprocity and symmetry be checked, and those checks are required at G13 |

**Procedure.**
1. Warm up the instrument.
2. Calibrate; save and export the state.
3. **Verify** with a standard not used in the calibration (gate G10).
4. Measure the DUT. Save raw Touchstone to `measurement/raw/`.
5. **Disconnect, reconnect, remeasure. At least three times** (gate G11).
6. Measure every coupon, same discipline.
7. Record everything in the log below.

### Measurement log

| Date | Instrument | Cal method | DUT/coupon | File | Operator | Notes |
|---|---|---|---|---|---|---|
| — | — | — | — | — | — | *no measurements exist* |

---

## 5. Data handling

| Directory | Contents | Rule |
|---|---|---|
| `raw/` | Touchstone exactly as the instrument wrote it | **APPEND-ONLY. NEVER EDIT. NEVER OVERWRITE.** |
| `processed/` | derived data | produced by committed **scripts**, never by hand-editing |
| `deembedded/` | de-embedded results | only if G13 passes |
| `calibration/` | instrument states, kit records, verification data | — |

**Naming:** `YYYY-MM-DD_<DUT-or-coupon>_<cal-method>_<repeat-number>.s2p`

> **The append-only rule is the one that matters most.** Raw measured data is the only thing in
> this project that cannot be regenerated. A simulation can be re-run; a board can be re-measured
> only while it still exists, still works, and the instrument is still available and still
> calibrated the same way. Treat `raw/` as write-once.

---

## 6. G8 sign-off

| Item | Status |
|---|---|
| Measurement chain written, every plane named | ☐ |
| Calibration method chosen from what exists | ☐ |
| De-embedding method chosen **or explicitly declined** | ☐ |
| Validity assumptions written for the chosen method | ☐ |
| Coupon set decided | ☐ |
| Panel budget computed | ☐ |
| Artan Round 2 answered | ☐ |
| Decision D-006 logged | ☐ |
| **Gate G8 passed** | ☐ |

**No PCB layout work begins until every box is ticked.**
