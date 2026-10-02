# HARDWARE CONSTRAINTS

*The gate-G0 instrument. Every field is BLOCKED until filled from a named source.*

> **Rule.** A field is filled only from a datasheet, a fabricator's published rules, an instrument
> manual, or a dated statement from Artan. **Never from memory, never from an AI's assumption,
> never from "typical values".** A guessed field here propagates into every dimension in the
> project.

**Last updated:** 2026-10-02 (created; nothing filled)
**Gate:** G0 — passes when every row below has a value and a source.

---

## 1. Substrate / laminate

| Field | Value | Source | Status |
|---|---|---|---|
| Manufacturer | — | — | **BLOCKED** |
| Product name / grade | — | — | **BLOCKED** |
| Dielectric constant εr | — | — | **BLOCKED** |
| **Frequency at which εr is quoted** | — | — | **BLOCKED** |
| εr tolerance | — | — | **BLOCKED** |
| Loss tangent tanδ | — | — | **BLOCKED** |
| Frequency at which tanδ is quoted | — | — | **BLOCKED** |
| Dielectric thickness h | — | — | **BLOCKED** |
| Thickness tolerance | — | — | **BLOCKED** |
| Copper weight / thickness t | — | — | **BLOCKED** |
| Copper conductivity (or assume annealed Cu) | — | — | **BLOCKED** |
| Surface finish | — | — | **BLOCKED** |
| Panel / sheet size available | — | — | **BLOCKED** |
| Number of copper layers | — | — | **BLOCKED** |

> **Why "frequency at which εr is quoted" has its own row.** Many laminate datasheets quote εr at
> 1 MHz. For a GHz filter that number is close to useless, and using it would silently shift f₀.
> This is the field most likely to be skipped and most likely to cause R-04.
>
> **FR-4 is not assumed** (decision D-008). If the laminate turns out to be FR-4, record its actual
> datasheet values — not the generic figures circulating online (claims S-01…S-03, all UNVERIFIED).

## 2. Fabrication

| Field | Value | Source | Status |
|---|---|---|---|
| Route (in-house / commercial / other) | — | — | **BLOCKED** |
| Process (photolithographic etch / milling / other) | — | — | **BLOCKED** |
| Lead time | — | — | **BLOCKED** |
| Cost per board | — | — | **BLOCKED** |
| Can spares be ordered? | — | — | **BLOCKED** |
| **Minimum trace width** | — | — | **BLOCKED** |
| **Minimum gap / clearance** | — | — | **BLOCKED** |
| Etch tolerance / bias | — | — | **BLOCKED** |
| Minimum drill / via size | — | — | **BLOCKED** |
| Maximum board size | — | — | **BLOCKED** |
| Solder mask available? | — | — | **BLOCKED** |
| Silkscreen available? | — | — | **BLOCKED** |

> **Minimum gap is the most design-determining number in the project.** It decides whether a
> coupled-line or hairpin filter is realizable at all (risk R-06). It is why G0 precedes the G3
> topology decision rather than following it.
>
> **Silkscreen matters more than it looks.** If the panel carries de-embedding coupons (gate G8),
> unlabelled coupons are easy to confuse under test, and a mislabelled coupon silently corrupts the
> de-embedding.

## 3. Measurement equipment

| Field | Value | Source | Status |
|---|---|---|---|
| VNA manufacturer / model *(record capability, not asset tags)* | — | — | **BLOCKED** |
| Number of ports | — | — | **BLOCKED** |
| **Frequency range** | — | — | **BLOCKED** |
| Port connector type | — | — | **BLOCKED** |
| Dynamic range | — | — | **BLOCKED** |
| Available cables | — | — | **BLOCKED** |
| Available adapters | — | — | **BLOCKED** |
| Torque wrench available? | — | — | **BLOCKED** |
| Access procedure / booking / induction | — | — | **BLOCKED** |

> **VNA frequency range bounds the filter's frequency** (requirement FR-12). The design frequency
> cannot be chosen before this row is filled — a filter whose stopband extends past the
> instrument's range cannot be characterized.

## 4. Calibration resources

| Field | Value | Source | Status |
|---|---|---|---|
| Calibration kit(s) physically available | — | — | **BLOCKED** |
| Kit connector type and gender | — | — | **BLOCKED** |
| Kit frequency range | — | — | **BLOCKED** |
| Standard definitions / coefficients available? | — | — | **BLOCKED** |
| Electronic calibration module available? | — | — | **BLOCKED** |
| Methods the instrument supports | — | — | **BLOCKED** |
| Verification standard available (not used in cal)? | — | — | **BLOCKED** |

> **"Which methods does the instrument support" is not the same question as "which kit do we
> physically have".** Both rows exist because the second one is what actually constrains us
> (risk R-12). Neither SOLT nor TRL is assumed (decision D-006).
>
> The verification-standard row serves gate G10: an unverified calibration cannot support a claim.

## 5. Connector and launch

| Field | Value | Source | Status |
|---|---|---|---|
| Connector type | — | — | **BLOCKED** |
| Mounting style (end-launch / edge / through-hole / vertical) | — | — | **BLOCKED** |
| Manufacturer and part number | — | — | **BLOCKED** |
| Rated frequency range | — | — | **BLOCKED** |
| Recommended launch footprint available? | — | — | **BLOCKED** |
| **Known-good footprint already used by the group?** | — | — | **BLOCKED** |
| Quantity available / cost each | — | — | **BLOCKED** |
| Suitable for the chosen substrate thickness? | — | — | **BLOCKED** |

> **The known-good-footprint row is worth more than any reading.** A footprint the group has
> already measured successfully removes risk R-09 almost entirely. Round 1 Q3 asks for it directly.
>
> Connector quantity matters at gate G8: every de-embedding coupon needs its own connectors, and
> that cost is usually what limits the coupon count rather than board area.

## 6. Software

| Field | Value | Source | Status |
|---|---|---|---|
| ADS version | — | — | **BLOCKED** |
| Licence type / contention | — | — | **BLOCKED** |
| **Momentum licensed?** | — | — | **BLOCKED** |
| Other EM tools available | — | — | **BLOCKED** |
| PCB CAD tool to be used | — | — | **BLOCKED** |
| Group ADS template / substrate definition exists? | — | — | **BLOCKED** |

> **Momentum availability determines whether phase P7 exists** (risk R-24). If it is not licensed,
> the project is still valid — but the portfolio claim changes from "planar EM simulation" to
> "circuit and microstrip simulation", and that must be reflected honestly at P13.

## 7. Time and schedule

| Field | Value | Source | Status |
|---|---|---|---|
| Hours per week realistically available | — | — | **BLOCKED** (student to decide honestly) |
| Seminar date | — | — | **BLOCKED** |
| Seminar content-freeze date | — | — | **BLOCKED** |
| Semester deadlines that compete | — | — | **BLOCKED** |
| Mentor availability pattern | — | — | **BLOCKED** |

> **Hours per week is a constraint, not an aspiration.** Risk R-15 (critical impact) is scope creep
> against coursework. An honest number here is what makes the phase estimates mean anything.

---

## Derived constraints

*Computed from the above once filled. Empty by design — these are the numbers that actually drive
the design, and every one of them is a product of fields that are currently blocked.*

| Derived quantity | Value | Depends on |
|---|---|---|
| Usable frequency range for the design | — | VNA range ∩ substrate usable range ∩ connector rating |
| 50 Ω line width on this substrate | — | εr, h, t |
| λ_g at the candidate frequency | — | ε_eff, f |
| Smallest realizable coupling gap, with margin | — | min gap + etch tolerance |
| Tightest achievable coupling coefficient | — | smallest gap, topology |
| Implied minimum fractional bandwidth | — | tightest coupling |
| Maximum board area | — | fabricator max size, panel size |
| Coupons that fit alongside the filter | — | board area, connector count, cost |

> **The chain that decides the project.** `minimum gap → tightest coupling → minimum fractional
> bandwidth → whether a narrowband coupled-line BPF is possible at all`. Four links, and the first
> one is a single number from the fabricator. That chain is the entire argument for why G0 comes
> before G3.

---

## Sign-off

| Item | Status |
|---|---|
| All §1–§7 rows filled with a named source | ☐ |
| Derived constraints computed | ☐ |
| Topology matrix BLOCKED rows now scoreable | ☐ |
| Entered in `planning/decision_log.md` with dates | ☐ |
| **Gate G0 passed** | ☐ |

**Nothing in `design/calculations/` may be produced before this sign-off is complete.**
