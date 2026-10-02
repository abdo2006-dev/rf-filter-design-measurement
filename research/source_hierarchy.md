# SOURCE HIERARCHY

*What counts as authority for what. Read with `verification_log.md`.*

---

## The four tiers

### Tier 1 — Standard theory references
**Authority for:** physics, mathematics, derivations, design methodology.
**Not authority for:** which button to press, what our lab owns, current product behaviour.

Two books only, deliberately:

- **Pozar, *Microwave Engineering*, 4th ed.** — transmission lines, S-parameters, ABCD matrices,
  the insertion-loss filter design method, microstrip basics.
- **Hong & Lancaster, *Microstrip Filters for RF/Microwave Applications*, 2nd ed.** — the
  microstrip-specific realization: coupled lines, stepped impedance, hairpin, discontinuities.

A third Tier-1 book is added only if a real gap appears. The gap most likely to appear is
*measurement* theory. If it does, the candidate is a VNA/measurement text, and it must be added
with a recorded reason — not because more references look better.

### Tier 2 — Official vendor and standards material
**Authority for:** software procedure, instrument behaviour, measurement practice, de-embedding
method definitions.
**Not authority for:** physics (use Tier 1), or for what is best for *our* project.

Keysight application notes, technical overviews, ADS documentation, and IEEE standards. Note the
subdivision: a Keysight *application note* on de-embedding is a measurement authority; a Keysight
*technical overview* of an ADS workflow is a software-procedure authority. They are not
interchangeable.

### Tier 3 — Peer-reviewed papers
**Authority for:** evidence that something has been done, realistic magnitudes of
simulation-vs-measurement discrepancy, reporting structure, and precedent for a method.
**Not authority for:** our dimensions, our substrate, our specification.

Small and curated — ten entries, of which eight are core. Papers are selected for *what they
demonstrate about the process*, never because they happen to use a frequency we might use.

> **Hard rule:** no dimension, gap, width or coupling value is ever copied from a paper. A paper's
> geometry is valid only on that paper's substrate, with that paper's fabricator, at that paper's
> frequency. Copying it produces a design nobody can defend.

Journal quality is assessed, not assumed. Two entries in the bibliography carry explicit authority
warnings. "It has a DOI" is not a quality signal.

### Tier 4 — Informal sources
**Authority for:** where a menu item is in ADS. Nothing else.

Videos, blogs, vendor white papers, forum posts, trade press. Legitimately useful for software
navigation and for orientation. **Never cited as technical authority when a Tier 1–3 source exists
on the same point.** Never cited in the seminar for a physics claim.

The distinction that matters:

> "I learned where the Momentum mesh setting is from a YouTube video" — fine, and not worth citing.
>
> "A YouTube video is my authority for how Momentum convergence should be judged" — not acceptable.
> That claim needs the ADS documentation (Tier 2) and a known-answer benchmark (our own evidence).

---

## Source roles

Every entry in `annotated_bibliography.md` carries one role. The role says what the source may be
used *for*, independent of its tier.

| Role | Meaning |
|---|---|
| **THEORY AUTHORITY** | May support a physics or mathematics claim |
| **SOFTWARE PROCEDURE** | May support "this is how the tool is used/configured" |
| **MEASUREMENT AUTHORITY** | May support a calibration, reference-plane or de-embedding method claim |
| **ACADEMIC EXAMPLE** | May support "this has been done, and here is a realistic magnitude" |
| **TEACHING RESOURCE** | May support how to learn or explain something |
| **SEMINAR ASSET SOURCE** | A figure or data source for the talk, subject to licence check |
| **BACKGROUND ONLY** | Orientation. May not support any claim in the report or the seminar. |

A source may hold more than one role, but each *claim* cites the source under exactly one.

---

## Copyright and source management rules

**Non-negotiable, because this repository will be shown to other people.**

1. **No copyrighted textbooks or publisher PDFs in this repository.** Not in `research/`, not in
   `seminar/`, not "temporarily". `.gitignore` blocks `*.pdf` by default as a safety net, but the
   rule is the rule, not the gitignore.
2. **Metadata only.** Every source is stored as the record defined in `templates/source_template.md`:
   title, authors/organization, year, DOI, URL, source type, tier, role, project relevance,
   specific chapter/section/page, access status, reuse/licence status.
3. **Paywalled papers:** cite and link. Read them through the university's institutional access.
   Do not commit the PDF and do not use a pirated copy.
4. **IEEE standards are paywalled.** Cite IEEE Std 370-2020 by designation. Do not obtain or store
   a copy for this repository.
5. **Keysight application notes** are free to download but remain Keysight's copyright. Link to the
   official asset URL. Do not commit the file or re-host it.

### Figures and seminar assets

**Prefer our own, always.** Our drawings, our ADS schematics, our plots, our PCB renders, our
photographs, our measured data. This is both a copyright-safety rule and a quality rule — a
seminar built from our own figures is visibly a seminar about our own work.

If an external figure is genuinely needed:

1. Check the actual licence. **Open access does not mean unrestricted figure reuse.** A CC-BY paper
   permits reuse with attribution; many "free to read" papers do not permit reuse at all; a figure
   inside a CC-BY paper may itself be reproduced from a third party under a narrower licence.
2. Record the licence and the exact attribution wording in `seminar/asset_register.md` *before*
   the figure goes on a slide.
3. If the figure is redrawn rather than copied, label it **"adapted from [source]"** and still cite it.
4. **Never screenshot a copyrighted figure just because it is on the internet.** Textbook figures
   in particular are among the most tightly controlled material in the field.

Default behaviour when a published figure would be useful: **redraw a simplified version
ourselves, and cite the source for the idea.** Cleaner slide, correct attribution, no licence
problem, and it demonstrates understanding rather than retrieval.

### Proprietary and confidential information

Also non-negotiable. Out of this repository, permanently:

- Instrument serial numbers, asset tags, internal network paths, licence servers, licence keys.
- Unpublished results, data or figures belonging to the research group or to Artan.
- Anything shared in confidence, or anything whose publication status is unclear.
- Artan's unpublished thesis content beyond its public title.
- Named lab locations or access procedures.

Where a lab fact must be recorded for engineering reasons, record the *capability*, not the
identity: "a two-port VNA covering 300 kHz – 8.5 GHz" rather than an asset tag.

**Before this repository is ever made public, re-read it with this list in hand.** That is risk
R-27, and it is a listed gate item for P13.
