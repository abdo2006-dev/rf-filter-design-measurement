# VERIFICATION LOG

*What was actually checked, how, and what could not be checked. Read this before trusting any
citation in this repository.*

**Verification pass:** 2026-10-02, bootstrap session
**Method available:** server-side web search only

---

## 1. What this session could and could not do

The task explicitly required this session **not** to inherit the previous session's
"UNVERIFIED" statuses, and to try again independently. It did try again. Here is the result.

### Blocked

Every attempt to open a primary document directly failed. The container's network egress policy
denies the hosts needed:

| Host | Needed for | Result |
|---|---|---|
| `www.keysight.com` | the four Keysight application notes | `403` on CONNECT (policy denial) |
| `doi.org` | resolving every DOI | `403` |
| `api.crossref.org` | authoritative bibliographic metadata | `403` |
| `arxiv.org` | preprints | `403` |
| `ieeexplore.ieee.org` | IEEE papers and IEEE Std 370 | `403` |
| `openlibrary.org` | book metadata / ISBN confirmation | `403` |
| `edadownload.software.keysight.com` | ADS manuals | `403` |
| `www.rogerscorp.com` | substrate datasheets | `403` |

Both available fetch paths were tried (the agent's own fetch tool and `curl` through the
configured proxy). Both are denied by the same policy. This is not a transient failure and was
not worked around.

**Consequence: no PDF was opened in this session, and no claim in this repository should be read
as "I read the document."** Where a chapter or section is cited, it is a *pointer to check*, not
a verified quotation.

### Available

Server-side web search worked. It returns result titles and URLs from a search index. That is
genuine third-party evidence that a document with a given title exists at a given official URL —
which is enough to confirm *identity* (title, publication number, publisher, year, DOI string) —
but it is not enough to confirm *content*.

---

## 2. Verification vocabulary used in this repository

| Status | Means |
|---|---|
| **VERIFIED** | Identity confirmed from the publisher's or standards body's own domain, corroborated by at least one independent source. Bibliographic facts only. |
| **PARTIALLY VERIFIED** | Identity strongly corroborated, but either the document was not opened, or one field (a DOI string, an author list, a page number) rests on a single secondary source. |
| **UNVERIFIED** | Plausible but resting on a single unconfirmed secondary mention. Must be checked before use. |

**No source in this repository is marked VERIFIED on the basis of its content.** Content
verification requires opening the document, which requires either network access or a library.

---

## 3. Results of this pass

### Tier 1 — textbooks

| Source | Field | Status | Basis |
|---|---|---|---|
| Pozar, *Microwave Engineering*, 4th ed. | title, author, edition, publisher (Wiley), year 2011/2012, print ISBN 978-0-470-63155-3, eText ISBN 978-1-118-21363-6 | **VERIFIED** | Wiley product page + multiple independent booksellers agree |
| Pozar | ch. 8 "Microwave Filters" at p. 380; §8.1 p. 381, §8.2 p. 388, §8.3 p. 399, §8.4 p. 408 | **PARTIALLY VERIFIED** | table-of-contents listing via search; book not opened. **Check against the physical copy.** |
| Hong & Lancaster, *Microstrip Filters for RF/Microwave Applications*, 2nd ed. | title, authors, edition, publisher (Wiley), year 2011, hardcover ISBN 978-0-470-40877-3, e-book ISBN 978-1-118-00212-4 | **VERIFIED** | Wiley product page + Heriot-Watt institutional research portal + independent booksellers agree |
| Hong & Lancaster | specific chapter numbers for microstrip lines / coupled-line / hairpin / stepped-impedance realizations | **UNVERIFIED** | not confirmed. This repository deliberately cites these as "the relevant realization chapter" rather than inventing a number. **Fill in from the physical copy's contents page at P3.** |

### Tier 2 — Keysight

The three publication numbers supplied by the student were **not** taken on trust. Each was
searched independently, and each resolves to a live asset URL on Keysight's own domain with a
matching title.

| Claimed | Found | Status |
|---|---|---|
| "Planar Electromagnetic (EM) Simulation in ADS – Chapter 4", pub. 5992-1479 | `keysight.com/us/en/assets/7018-05192/technical-overviews/5992-1479.pdf`, title matches, classified by Keysight as a *technical overview* | **PARTIALLY VERIFIED** — number and title correct; PDF not opened |
| "De-Embedding and Embedding S-Parameter Networks", AN 1364-1 / 5980-2784 | `keysight.com/us/en/assets/7018-06806/application-notes/5980-2784.pdf`. Full current title is longer: *"De-Embedding and Embedding S-Parameter Networks **Using a Vector Network Analyzer**"*. Current designation appears as **5980-2784EN**. | **PARTIALLY VERIFIED** — number correct, **title corrected** (see note below) |
| "In-Fixture Measurements Using Vector Network Analyzers", pub. 5968-5329 | `keysight.com/us/en/assets/7018-06814/application-notes/5968-5329.pdf`, title matches exactly | **PARTIALLY VERIFIED** — number and title correct |
| "RF Design Software Learning Kit" | exists as a Keysight landing page (`connectlp.keysight.com/EMORFDesignSoftwareLearningKit`) and as a print book, ISBN 978-1-544219-08-0. Described as ~170 pages, 6 chapters, 3 design projects, 2 videos, with accompanying ADS workspaces. Gated behind a form. | **PARTIALLY VERIFIED** |

**Corrections to record (the student's numbers were right, two details were not):**

1. The de-embedding note's full title includes **"Using a Vector Network Analyzer"**. Cite it that
   way. The historical "AN 1364-1" designation is still widely used in citations, and the
   literature number is now written **5980-2784EN**.
2. 5992-1479 is a **technical overview / example-book chapter**, not an application note. It is
   chapter 4 of a Keysight ADS example-book series. Classify it as SOFTWARE PROCEDURE, not as a
   peer-reviewed or theory authority.

Note also that search-result summaries indicated 5992-1479 contains a **coupled-line microstrip
bandpass filter case study**. If true, that is directly on-point for this project's candidate
topology B. **Treat as PARTIALLY VERIFIED and confirm on first read.**

### Tier 2b — measurement standard

| Source | Status | Basis |
|---|---|---|
| IEEE Std 370-2020, *IEEE Standard for Electrical Characterization of Printed Circuit Board and Related Interconnects at Frequencies up to 50 GHz* | **PARTIALLY VERIFIED** | title and scope corroborated across multiple independent technical sources (MathWorks documentation, scikit-rf documentation, Signal Integrity Journal, Altium resources). IEEE's own page not reachable. Standard itself is paywalled — **metadata only, do not attempt to obtain a copy for this repository.** |

The 2x-thru (FIX-FIX) de-embedding structure and the "impedance-corrected" variant are attributed
to this standard by several independent sources. Important for gate G8: **the 2x-thru is a
fabricated coupon, not a post-processing option.**

### Tier 3 — papers

DOI strings were only accepted as VERIFIED where the DOI itself appeared in a result URL. DOIs
that appeared only inside a generated summary are marked UNVERIFIED and must be checked.

| # | Paper (short) | DOI | DOI status | Basis |
|---|---|---|---|---|
| A1 | Parallel-coupled microstrip balanced BPF, *Micromachines* 16 (2025) | 10.3390/mi16111238 | **VERIFIED** | appeared as a `doi.org` result URL; mirrored on PubMed Central |
| A2 | Coupled lines loaded by open stubs, *Scientific Reports* 14 (2024) | 10.1038/s41598-024-77818-4 | **VERIFIED** | nature.com article URL; Nature article IDs are the DOI suffix |
| A3 | Parallel-coupled-line BPF with notch (UWB), *Applied Sciences* 13(11):6834 (2023) | 10.3390/app13116834 | **VERIFIED** | mdpi.com/2076-3417/13/11/6834; MDPI DOI construction is deterministic |
| A4 | Chen, parallel coupled-line microstrip filter in broadband, *MOTL* (2006) | 10.1002/mop.21353 | **VERIFIED** | Wiley `onlinelibrary.wiley.com/doi/abs/...` URL |
| A5 | De-embedding for planar microstrip sensors, *Scientific Reports* 14 (2024) | 10.1038/s41598-024-60640-3 | **VERIFIED** | nature.com article URL + PMC mirror |
| A6 | Caballero et al., TRL for SIW with tapered microstrip transitions, *Electronics Letters* (2013) | 10.1049/el.2012.3027 | **VERIFIED** | IET `ietresearch.onlinelibrary.wiley.com/doi/full/...` URL |
| A7 | Ramdedović & Imeci, tight-coupled microstrip hairpin BPF, *Journal of Engineering Research* | 10.36909/jer.13255 | **UNVERIFIED** | title and two hosting URLs confirmed (ScienceDirect PII S2307187725001592; Kuwait Journals). DOI from summary only. |
| A8 | Benjamin, Ainah & Enoma, stepped-impedance microstrip LPF using ADS, *IJSRP* 11(7) (2021) | 10.29322/IJSRP.11.07.2021.p11548 | **UNVERIFIED** | ijsrp.org PDF URL confirmed (`ijsrp-p11548.pdf`); DOI from summary only. **See authority warning in the bibliography.** |
| A9 | Engen & Hoer, Thru-Reflect-Line, *IEEE Trans. MTT* 27 (1979) 987–993 | 10.1109/TMTT.1979.1129778 | **PARTIALLY VERIFIED** | title, authors, journal, volume and pages corroborated; Semantic Scholar record found; DOI string from summary. High confidence — this is a canonical paper — but **confirm the DOI before citing it in the seminar.** |
| A10 | Stepped-impedance microstrip LPF with DGS, *MOTL* | 10.1002/mop.23843 | **UNVERIFIED** | summary mention only. Low priority. |

### Technical facts gathered and their status

| Fact | Status | Note |
|---|---|---|
| Momentum default mesh density is **20 cells per wavelength**; 20–30 CpW typically needed for accurate results; too high a value can introduce numerical error | **PARTIALLY VERIFIED** | consistent across Keysight-derived documentation quoted in several independent places; **confirm in the ADS Momentum documentation itself** |
| Mesh frequency should be set to the **highest frequency simulated**, because cell size is fixed while wavelength shrinks | **PARTIALLY VERIFIED** | same basis. This is the single most commonly made Momentum setup error. |
| FR-4 εr varies roughly ±10 % between manufacturing lots and is frequency-dependent (≈4.7 at 100 MHz falling to ≈4.2 at 5 GHz); moisture absorption shifts it further | **UNVERIFIED** | trade-press and forum sources only. Directionally important for risk R-04/R-05, but **do not quote these numbers in the seminar without a datasheet or a textbook.** |
| IEEE-370 2x-thru de-embedding is implemented in the open-source `scikit-rf` package | **PARTIALLY VERIFIED** | scikit-rf documentation page found. Useful as an inspectable processing route at P12. |

---

## 4. What a future session must re-verify

Priority order:

1. **Open the four Keysight PDFs** and confirm: 5992-1479 contains a coupled-line BPF case study;
   5980-2784EN's de-embedding procedure and its stated assumptions; 5968-5329's guidance on
   constructing in-fixture standards.
2. **Confirm the Hong & Lancaster chapter numbers** from the physical copy and fill them into
   `annotated_bibliography.md`. The repository deliberately leaves them blank rather than guessing.
3. **Confirm the four UNVERIFIED/PARTIALLY VERIFIED DOIs** (A7, A8, A9, A10).
4. **Replace the FR-4 tolerance figures** with numbers from the actual substrate datasheet once
   G0 supplies it — at which point they stop being generic FR-4 claims anyway.
5. **Confirm the Momentum mesh guidance** in the shipped ADS documentation before writing
   `ads/momentum/EM_VALIDATION_METHOD.md`.

To make that possible, the environment's **Network access** setting needs widening — either a
broader access level or the specific hosts in §1 added to the allowed domains.
