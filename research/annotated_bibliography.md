# ANNOTATED BIBLIOGRAPHY

*Metadata only. No document in this list is stored in this repository.*
*Read `verification_log.md` before relying on any entry.*

Each entry records what the source **is useful for** and — equally important — **what it does not
justify us assuming.**

---

# TIER 1 — STANDARD THEORY REFERENCES

## T1-01 Pozar, *Microwave Engineering*, 4th edition

| Field | Value |
|---|---|
| Author | David M. Pozar |
| Title | Microwave Engineering |
| Edition | 4th |
| Publisher | John Wiley & Sons |
| Year | 2011 (2012 printing cited in some records) |
| ISBN | 978-0-470-63155-3 (print); 978-1-118-21363-6 (e-text) |
| Pages | ~752 |
| Type | Textbook |
| Tier | 1 |
| Role | THEORY AUTHORITY |
| Verification | **VERIFIED** (bibliographic); chapter/page pointers **PARTIALLY VERIFIED** |
| Access | University library / purchase. **Not in this repository.** |
| Reuse | All rights reserved. Figures may not be reproduced. Redraw and cite. |

**Sections this project depends on** *(page numbers from a table-of-contents listing — confirm
against the physical copy at P1/P3)*:

- **Ch. 2** Transmission Line Theory — §2.1–2.3 (wave equations, terminated lossless line, Smith
  chart), §2.5–2.7. → theory block B, phase P1.
- **§3.8** Microstrip. → theory block F, phase P6.
- **§4.3** The Scattering Matrix. → block C, phase P2.
- **§4.4** The Transmission (ABCD) Matrix, with the S↔ABCD conversion tables. → block D, phase P2.
  **This is the mathematical core of both the project and the seminar.**
- **Ch. 8** Microwave Filters (p. 380): §8.1 Periodic Structures (381), §8.2 Image Parameter
  Method (388), **§8.3 Filter Design by the Insertion Loss Method (399)**, **§8.4 Filter
  Transformations (408)**. → block E, phases P3/P4.

**Useful for.** The derivation chain from Maxwell-level transmission-line behaviour to a designed
filter. The insertion-loss method in §8.3 is the method this project will use. The ABCD treatment
in §4.4 is what makes the de-embedding stretch goal intelligible.

**Does NOT justify.** Any statement about ADS. Any statement about our substrate, our fabricator
or our instrument. Pozar's worked examples use illustrative numbers — they are not our
specification. The book predates current measurement practice (e.g. IEEE 370), so it is not the
authority for modern fixture de-embedding.

---

## T1-02 Hong & Lancaster, *Microstrip Filters for RF/Microwave Applications*, 2nd edition

| Field | Value |
|---|---|
| Authors | Jia-Sheng Hong, M. J. Lancaster |
| Title | Microstrip Filters for RF/Microwave Applications |
| Edition | 2nd |
| Series | Wiley Series in Microwave and Optical Engineering |
| Publisher | John Wiley & Sons |
| Year | 2011 (January) |
| ISBN | 978-0-470-40877-3 (hardcover); 978-1-118-00212-4 (e-book) |
| Pages | ~656 |
| Type | Textbook / research monograph |
| Tier | 1 |
| Role | THEORY AUTHORITY |
| Verification | **VERIFIED** (bibliographic, incl. Heriot-Watt institutional record); chapter numbers **UNVERIFIED** |
| Access | University library / purchase. **Not in this repository.** |
| Reuse | All rights reserved. Redraw and cite. |

**Sections this project depends on.**

> **Deliberately left blank.** This session could not open the book and will not invent chapter
> numbers for a source this load-bearing. **Action at P3: open the physical copy, read the
> contents page, and fill in the chapter numbers for:**
>
> - [ ] basic filter concepts and the lowpass prototype → block E, P4
> - [ ] microstrip transmission lines, effective permittivity, discontinuities → block F, P6
> - [ ] coupled microstrip lines, even/odd modes → block F, P6 (needed only for topology B/C)
> - [ ] stepped-impedance realizations → topology A
> - [ ] parallel-coupled-line bandpass realizations → topology B
> - [ ] hairpin resonator realizations → topology C
> - [ ] coupled-resonator theory, coupling coefficients, external Q → block E/F

**Useful for.** The step this project actually lives or dies on: converting prototype element
values into physical microstrip geometry. This is the reference for all three candidate
topologies, so it serves the P3 decision even before the decision is made.

**Does NOT justify.** Copying any published dimension. The book is also a research monograph and
ranges far beyond this project (HTS, micromachined, UWB, tunable, MEMS) — **those chapters are
out of scope** and reading them is exactly the drift this project is designed to avoid.

---

# TIER 2 — OFFICIAL KEYSIGHT AND STANDARDS MATERIAL

## T2-01 Keysight 5992-1479 — *Planar Electromagnetic (EM) Simulation in ADS, Chapter 4*

| Field | Value |
|---|---|
| Organization | Keysight Technologies |
| Title | Planar Electromagnetic (EM) Simulation in ADS — Chapter 4 |
| Publication no. | 5992-1479 |
| Document class | Technical overview (ADS example-book chapter), **not** an application note |
| URL | `https://www.keysight.com/us/en/assets/7018-05192/technical-overviews/5992-1479.pdf` |
| Tier | 2 |
| Role | SOFTWARE PROCEDURE |
| Verification | **PARTIALLY VERIFIED** — number + title + official asset URL confirmed; PDF not opened |
| Access | Free download from Keysight. **Not stored here.** |
| Reuse | © Keysight. Link only; do not re-host. Screenshots of its figures need permission. |

**Useful for.** The schematic → layout → Momentum workflow, which is exactly phase P7. Search
evidence indicates it contains a **coupled-line microstrip bandpass filter case study** — if so it
is directly on-point for candidate topology B. *(Confirm on first read; the student's supplied
publication number was correct.)*

**Does NOT justify.** EM-convergence judgement. A worked example shows *a* set of settings that
produced *a* result; it is not a validation methodology. G7 requires our own
`EM_VALIDATION_METHOD.md` plus a known-answer benchmark. Also does not justify assuming Momentum
is licensed for us.

---

## T2-02 Keysight 5980-2784EN (AN 1364-1) — *De-Embedding and Embedding S-Parameter Networks Using a Vector Network Analyzer*

| Field | Value |
|---|---|
| Organization | Keysight Technologies (originally Agilent) |
| Title | De-Embedding and Embedding S-Parameter Networks **Using a Vector Network Analyzer** |
| Application note | AN 1364-1 |
| Publication no. | 5980-2784EN |
| URL | `https://www.keysight.com/us/en/assets/7018-06806/application-notes/5980-2784.pdf` |
| Tier | 2 |
| Role | MEASUREMENT AUTHORITY |
| Verification | **PARTIALLY VERIFIED** — number confirmed; **title corrected** vs. the student's version; PDF not opened |
| Access | Free from Keysight; also mirrored by third parties (prefer the official URL) |
| Reuse | © Keysight. Link only. |

**Useful for.** The project's primary de-embedding authority. Reported to cover S-parameter
matrices, signal-flow graphs, the standard one- and two-port error-correction process, de-embedding
via **scattering transfer (T) parameter** matrices, and the use of a negation component model in
ADS to de-embed a fixture directly in simulation. That last point matters: it is a route that
needs no extra coupons, which makes it a live candidate at G8.

**Does NOT justify.** That `T_DUT = T_L⁻¹ · T_meas · T_R⁻¹` is a safe production procedure on our
data. It is the correct *principle*; applying it requires a known fixture description and
noise-tolerant handling. It also does not justify skipping calibration — de-embedding is applied
*after* a valid calibration, not instead of one.

**Note.** This is the source for the seminar's central equation. Cite it as the measurement
authority and Pozar §4.4 as the mathematical authority.

---

## T2-03 Keysight 5968-5329 — *In-Fixture Measurements Using Vector Network Analyzers*

| Field | Value |
|---|---|
| Organization | Keysight Technologies (originally Hewlett-Packard / Agilent) |
| Title | In-Fixture Measurements Using Vector Network Analyzers |
| Publication no. | 5968-5329 |
| URL | `https://www.keysight.com/us/en/assets/7018-06814/application-notes/5968-5329.pdf` |
| Tier | 2 |
| Role | MEASUREMENT AUTHORITY |
| Verification | **PARTIALLY VERIFIED** — number and title confirmed exactly; PDF not opened |
| Access | Free from Keysight |
| Reuse | © Keysight. Link only. |

**Useful for.** Gate G8, more than any other source. Reported scope: why fixtures are needed,
fixture selection, measurement error and how to minimize it, basic fixture construction, and
**the construction and characterization of the required calibration standards when commercial
fixtures are not available** — which is precisely our situation. This is the document that tells us
what copper has to exist on the panel.

**Does NOT justify.** A specific coupon geometry for our board. It gives principles; our launch
footprint comes from the connector datasheet and our standards geometry from our substrate.

---

## T2-04 Keysight *RF Design Software Learning Kit*

| Field | Value |
|---|---|
| Organization | Keysight Technologies |
| Title | RF Design Software Learning Kit: Step-By-Step Examples on Using ADS Software for an Introductory RF/Microwave Course |
| ISBN (print) | 978-1-544219-08-0 |
| URL | `https://connectlp.keysight.com/EMORFDesignSoftwareLearningKit` (form-gated) |
| Contents | ~170 pp., 6 chapters, 3 design projects (design/fabrication/validation), 2 videos, with ADS workspaces |
| Tier | 2 |
| Role | TEACHING RESOURCE + SOFTWARE PROCEDURE |
| Verification | **PARTIALLY VERIFIED** |
| Access | Free behind a registration form |
| Reuse | © Keysight. **Check the licence before redistributing any workspace.** |

**Useful for.** The best match in existence for this student's exact position: an ADS beginner in
an introductory microwave course. Covers transmission-line theory through passive filters, with
ADS workspaces, and its three projects include fabrication and validation — the same arc as this
project. Primary companion for P1, P5 and P6.

**Does NOT justify.** Treating its example designs as our design, or committing its workspaces to
this repository without checking the licence (risk R-26). **Do not copy proprietary ADS example
files into the repository if redistribution is prohibited** — reference the kit instead.

---

## T2-05 ADS documentation — Momentum / Electromagnetic

| Field | Value |
|---|---|
| Organization | Keysight Technologies |
| Title | *Electromagnetic* (ADS product documentation; also the in-product Momentum help) |
| Tier | 2 |
| Role | SOFTWARE PROCEDURE |
| Verification | **UNVERIFIED** in this session — `edadownload.software.keysight.com` is egress-blocked |
| Access | Shipped with ADS; use the in-product help for the installed version |
| Reuse | © Keysight |

**Useful for.** The authority for Momentum mesh density (cells per wavelength), mesh frequency,
edge mesh, transmission-line mesh, adaptive frequency sampling and port calibration/de-embedding
settings — i.e. everything G7 depends on.

**Does NOT justify.** Anything until read in the *installed version's* help. Settings and defaults
change between ADS releases.

> **Action at P7:** use the in-product documentation for the actual installed ADS version, and cite
> it with that version number. Do not cite a web copy for a different release.

---

## T2-06 IEEE Std 370-2020

| Field | Value |
|---|---|
| Organization | IEEE |
| Title | IEEE Standard for Electrical Characterization of Printed Circuit Board and Related Interconnects at Frequencies up to 50 GHz |
| Designation | IEEE Std 370-2020 |
| Tier | 2 |
| Role | MEASUREMENT AUTHORITY |
| Verification | **PARTIALLY VERIFIED** — title and scope corroborated by several independent technical sources; IEEE's own page unreachable |
| Access | **Paywalled.** Check university access. **Metadata only — do not obtain a copy for this repository.** |
| Reuse | © IEEE. Cite by designation. |

**Useful for.** Current best practice for fixture characterization and de-embedding. Defines the
**2x-thru (FIX-FIX)** structure — two fixtures connected back to back — and describes both the
classical 2x-thru method (which assumes the left fixture, the right fixture and the 2x-thru
reference all have the same impedance) and an impedance-corrected variant. Directly informs the
G8 candidate inventory.

**Does NOT justify.** That we will use it. It targets interconnects to 50 GHz and assumes a signal-
integrity workflow; our project is a narrow-band filter at a far lower frequency with student
resources. It is a candidate to be evaluated at G8, not a default. Its central practical point is
the one that justifies moving G8 before layout: **the 2x-thru is copper that has to be fabricated.**

---

# TIER 3 — PEER-REVIEWED PAPERS

*Selected for what they show about the design→fabricate→measure process. Not selected by
frequency. No dimension is ever copied from any of them.*

## A1 — Parallel-coupled microstrip balanced bandpass filters

| Field | Value |
|---|---|
| Title | Parallel-Coupled Microstrip-Lines-Based Miniaturized Balanced Bandpass Filters with Flexible Differential-Fed I/O Ports |
| Journal | *Micromachines* (MDPI), vol. 16, art. 1238 |
| Year | 2025 |
| DOI | 10.3390/mi16111238 — **VERIFIED** |
| Tier / Role | 3 / ACADEMIC EXAMPLE |
| Access | Open access (MDPI, CC-BY); PMC mirror PMC12654537 |
| Reuse | CC-BY — figure reuse permitted **with attribution**; verify the specific licence line on the article |

**Useful for.** A current example of the parallel-coupled-line topology (candidate B) taken through
to measurement. Recent, open-access, and its figures are *potentially* reusable — one of very few
in this list where that is true.

**Does NOT justify.** Our topology choice. It is a *balanced/differential* filter with
miniaturization goals; our project is single-ended and makes no miniaturization claim. Its
substrate and frequency are not ours.

## A2 — Coupled lines loaded by open stubs

| Field | Value |
|---|---|
| Title | A microstrip bandpass filter using coupled lines loaded by open stubs |
| Authors | Kahkesh, Sheikhi *(author list PARTIALLY VERIFIED)* |
| Journal | *Scientific Reports*, vol. 14 |
| Year | 2024 |
| DOI | 10.1038/s41598-024-77818-4 — **VERIFIED** |
| Tier / Role | 3 / ACADEMIC EXAMPLE |
| Access | Open access (CC-BY) |
| Reuse | CC-BY — verify on the article page |

**Useful for.** The full chain done properly: theoretical analysis → simulation → measurement, with
all three compared. A good model for how P11 should be *reported*.

**Does NOT justify.** The open-stub loading technique for us — that is a modification beyond our
scope. Do not let it pull the project toward "improving" the filter.

## A3 — Parallel-coupled-line BPF with notch (UWB)

| Field | Value |
|---|---|
| Title | Parallel-Coupled-Line Bandpass Filter with Notch for Ultra-Wideband (UWB) Applications |
| Journal | *Applied Sciences* (MDPI), vol. 13, no. 11, art. 6834 |
| Year | 2023 |
| DOI | 10.3390/app13116834 — **VERIFIED** |
| Tier / Role | 3 / ACADEMIC EXAMPLE |
| Access | Open access (CC-BY) |
| Reuse | CC-BY — verify on the article page |

**Useful for.** Design → simulation → fabrication → measurement on the parallel-coupled topology,
reporting good measured/simulated agreement. Useful as a benchmark for what "good agreement" looks
like in print.

**Does NOT justify.** UWB or notch features — explicitly out of scope. Also, published claims of
"excellent agreement" are a reporting convention; they are not a target we must hit, and our
project's value includes honestly reporting *disagreement*.

## A4 — Chen, parallel coupled-line microstrip filter in broadband

| Field | Value |
|---|---|
| Title | Study of parallel coupled-line microstrip filter in broadband |
| Author | Chen (et al.) |
| Journal | *Microwave and Optical Technology Letters* (Wiley) |
| Year | 2006 |
| DOI | 10.1002/mop.21353 — **VERIFIED** |
| Tier / Role | 3 / ACADEMIC EXAMPLE |
| Access | Paywalled — use institutional access |
| Reuse | © Wiley. No figure reuse without permission. |

**Useful for.** A concrete simulated-vs-measured discrepancy on the candidate-B topology:
simulated bandwidth 67 % vs measured 64 %, insertion loss 1.27 dB *(figures from a secondary
summary — confirm on reading)*. A real example of the kind of gap our project is built to measure.

**Does NOT justify.** Broadband design. And its numbers must be confirmed from the paper before
being quoted anywhere, least of all in the seminar.

## A5 — De-embedding for planar microstrip sensors without evaluating error networks

| Field | Value |
|---|---|
| Title | De-embedding method for a sensing area characterization of planar microstrip sensors without evaluating error networks |
| Journal | *Scientific Reports*, vol. 14 |
| Year | 2024 |
| DOI | 10.1038/s41598-024-60640-3 — **VERIFIED** |
| Tier / Role | 3 / MEASUREMENT AUTHORITY (secondary) + ACADEMIC EXAMPLE |
| Access | Open access (CC-BY); PMC mirror PMC11066054 |
| Reuse | CC-BY — verify on the article page |

**Useful for.** A recent, open-access survey-in-passing of the in-microstrip de-embedding family —
TRL, LRL, TRM, LRM, TMRR, LRRM — and the point that standards implemented **directly in the
microstrip section** remove launcher, taper and feedline effects together. Directly feeds the G8
candidate inventory, and it is open access, so it can actually be read now.

**Does NOT justify.** Its specific method for us. It solves a sensor-characterization problem
with different constraints.

## A6 — Caballero et al., TRL for SIW with tapered microstrip transitions

| Field | Value |
|---|---|
| Title | Thru-reflect-line calibration for substrate integrated waveguide devices with tapered microstrip transitions |
| Authors | Caballero et al. |
| Journal | *Electronics Letters* (IET) |
| Year | 2013 |
| DOI | 10.1049/el.2012.3027 — **VERIFIED** |
| Tier / Role | 3 / MEASUREMENT AUTHORITY (secondary) |
| Access | Paywalled — institutional access |
| Reuse | © IET. No figure reuse without permission. |

**Useful for.** A worked precedent for applying TRL to move the reference plane past SMA connectors
and microstrip transitions, right up to the device. The clearest published illustration of the
*option* we are evaluating at G8.

**Does NOT justify.** TRL as our choice. SIW is not microstrip, and their standards were built for
their structure. TRL needs multiple fabricated line standards and brings its own band limitations.

## A7 — Ramdedović & Imeci, tight-coupled microstrip hairpin bandpass filter

| Field | Value |
|---|---|
| Title | Tight-coupled microstrip hairpin bandpass filter |
| Authors | Amel Ramdedović, Sehabeddin Taha Imeci |
| Journal | *Journal of Engineering Research* |
| Year | 2023–2025 *(unresolved — ScienceDirect PII suggests 2025, secondary records suggest 2023)* |
| DOI | 10.36909/jer.13255 — **UNVERIFIED** |
| Identifiers | ScienceDirect PII S2307187725001592; Kuwait Journals article 13255 |
| Tier / Role | 3 / ACADEMIC EXAMPLE |
| Access | Open access via Kuwait Journals |
| Reuse | Check the journal's licence before any figure reuse |

**Useful for.** The hairpin topology (candidate C) taken through design → simulation → fabrication
→ test, with reported measured/simulated correlation. The main published reference for candidate C
in this bibliography.

**Does NOT justify.** Hairpin as our choice — note in particular that its resonators are separated
by **~0.1 mm**, which on most low-cost fabrication processes is below the minimum gap. That single
detail is a strong argument for why the G0 minimum-gap fact must come before the P3 topology
decision. Verify the DOI and year before citing.

## A8 — Benjamin, Ainah & Enoma, stepped-impedance microstrip LPF using ADS

| Field | Value |
|---|---|
| Title | Stepped Impedance Microstrip Lowpass Filter Design using Advanced Design Systems |
| Authors | Ayibapreye Kelvin Benjamin, Priye Kenneth Ainah, Animiosevbuse Tosan Enoma |
| Journal | *International Journal of Scientific and Research Publications (IJSRP)*, vol. 11, no. 7 |
| Year | 2021 |
| DOI | 10.29322/IJSRP.11.07.2021.p11548 — **UNVERIFIED** |
| Tier / Role | 3 (nominally) / **ACADEMIC EXAMPLE — see warning** |
| Access | Open access |
| Reuse | Unclear — **do not reuse any figure** |

> ⚠ **AUTHORITY WARNING.** IJSRP is a low-barrier, author-pays venue with limited editorial
> reputation. Having a DOI is not a quality signal. **Treat this as a worked example of the
> ADS stepped-impedance workflow, nothing more.** Do not cite it for a theory claim, do not cite
> it in the seminar, and do not treat its results as validated. Every technical point it makes
> must be independently confirmed against Pozar §8.3/§8.4 or Hong & Lancaster.

**Useful for.** It is the closest published match to candidate topology A done in ADS on FR-4 with
a simulated-vs-measured comparison — i.e. a worked example of our own workflow. Useful for
orientation on *process*, and as a reminder that this exact project is a well-trodden student
exercise, which is a point in its favour: it is bounded and known to be completable.

**Does NOT justify.** Anything technical. Its dimensions, substrate assumptions and conclusions are
unvalidated. It is included *with* this warning precisely so a future session does not promote it
to an authority it has not earned. Prefer A10 or a Tier-1 source for the same topic.

## A9 — Engen & Hoer, Thru-Reflect-Line

| Field | Value |
|---|---|
| Title | Thru-Reflect-Line: An Improved Technique for Calibrating the Dual Six-Port Automatic Network Analyzer |
| Authors | Glenn F. Engen, Cletus A. Hoer |
| Journal | *IEEE Transactions on Microwave Theory and Techniques*, vol. 27, no. 12, pp. 987–993 |
| Year | 1979 |
| DOI | 10.1109/TMTT.1979.1129778 — **PARTIALLY VERIFIED** (high confidence; confirm before use) |
| Tier / Role | 3 / MEASUREMENT AUTHORITY |
| Access | Paywalled (IEEE) — institutional access |
| Reuse | © IEEE. No figure reuse without permission. |

**Useful for.** The original TRL formulation — the primary citation if TRL is chosen at G8. If the
seminar mentions TRL at all, this is the reference, not a vendor page. A 1979 paper that is still
the basis of current practice is also a good narrative beat for a maths audience.

**Does NOT justify.** That we can execute TRL. TRL needs fabricated standards in our medium, a
reflect of known-ish phase, and line standards whose length sets the usable band. Those are G8
decisions and G0 facts.

## A10 — Stepped-impedance microstrip LPF with DGS *(supplementary)*

| Field | Value |
|---|---|
| Title | Design of Stepped Impedance Microstrip Low Pass Filter with DGS |
| Journal | *Microwave and Optical Technology Letters* (Wiley) |
| DOI | 10.1002/mop.23843 — **UNVERIFIED** |
| Tier / Role | 3 / ACADEMIC EXAMPLE (supplementary) |
| Access | Paywalled |
| Reuse | © Wiley |

**Useful for.** A peer-reviewed stepped-impedance LPF fabricated photolithographically and measured
on a VNA — a better-quality alternative to A8 for the same topology, in a real journal.

**Does NOT justify.** Defected ground structures, which are out of scope. Ignore the DGS content
and read it only for the baseline stepped-impedance treatment and the measurement comparison.
Confirm the DOI before citing.

---

# TIER 4 — INFORMAL AND VENDOR SOURCES

*Software navigation and orientation only. Never cited for a technical claim in the report or the
seminar.*

| ID | Source | Role | Useful for | Does NOT justify |
|---|---|---|---|---|
| T4-01 | `scikit-rf` documentation, IEEE-P370 de-embedding example | TEACHING RESOURCE | An open, inspectable implementation of 2x-thru de-embedding. Valuable at P12 because the algorithm can actually be read, unlike a black box. Also a cross-check route for our own processing. | A method choice, or correctness of our data. It is a tool, not an authority. |
| T4-02 | Modelithics, *A Substrate-Scalable SMA Connector Model* (trade reprint) | BACKGROUND ONLY | Orientation on why an SMA launch is not an ideal connection and that scalable connector models exist. Useful framing for the stretch question. | Any connector model number for our board. Vendor material promoting a vendor product. |
| T4-03 | *Microwave Journal*, "Computational Electromagnetics Comparative Study of a 1 GHz Stepped-Impedance Filter" | BACKGROUND ONLY | Orientation on how different EM solvers disagree on the *same* stepped-impedance filter — a useful sanity expectation before P7. | Any convergence criterion. Trade press, not peer-reviewed. |
| T4-04 | MathWorks RF Toolbox documentation on IEEE 370 | BACKGROUND ONLY | A second plain-language description of the standard's methods while the standard itself is paywalled. | The standard's actual normative content. |
| T4-05 | ADS tutorial videos (various) | BACKGROUND ONLY | Finding menu items. Genuinely the fastest way to learn an unfamiliar GUI. | **Nothing.** Not cited anywhere. If a video teaches a physics point, find the Tier-1 source for it. |

---

# Gaps in this bibliography

Recorded honestly, to be filled when needed — not pre-emptively:

1. **No VNA/measurement textbook.** Tier 2 currently carries all measurement authority. If
   measurement theory becomes load-bearing at P10, a Tier-1 measurement text should be added with
   a recorded reason.
2. **No substrate datasheet.** Blocked on G0. It will become one of the most-cited sources in the
   project.
3. **No connector datasheet.** Blocked on G0. It is the authority for the launch footprint at P9.
4. **Hong & Lancaster chapter numbers missing** — see T1-02.
5. **No source for FR-4 εr tolerance.** Deliberate: generic FR-4 figures circulating on the web
   are unsourced, and once G0 names the real laminate the question is answered by its datasheet.
