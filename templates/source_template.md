# SOURCE TEMPLATE

Append to `research/annotated_bibliography.md`.

> **Metadata only.** The document itself is never committed. See the copyright rules in
> `research/source_hierarchy.md`.

---

```markdown
## <ID> <Short citation>

| Field | Value |
|---|---|
| Title | |
| Authors / organization | |
| Publication year | |
| Journal / publisher / document class | |
| Volume / issue / pages | |
| Edition | |
| DOI | |
| ISBN | |
| Publication number | <for vendor documents> |
| URL | <prefer the publisher's or vendor's own domain> |
| Source type | textbook / journal paper / conference paper / standard / application note / technical overview / documentation / video / blog / forum |
| **Tier** | 1 / 2 / 3 / 4 |
| **Role** | THEORY AUTHORITY / SOFTWARE PROCEDURE / MEASUREMENT AUTHORITY / ACADEMIC EXAMPLE / TEACHING RESOURCE / SEMINAR ASSET SOURCE / BACKGROUND ONLY |
| **Verification** | VERIFIED / PARTIALLY VERIFIED / UNVERIFIED — **and on what basis** |
| Access status | open access / paywalled / institutional / free registration / purchased / library |
| Reuse / licence status | <CC-BY, all rights reserved, unknown…> |
| Relevant sections | <chapter / section / page — be specific> |

**Useful for.**
<What claim or task this source can actually support, tied to a gate or phase.>

**Does NOT justify.**
<What it must not be used for. This field is the most valuable one in the record and
the one most often skipped. A source cited beyond its scope is how an unsupported
claim enters a project.>
```

---

## Rules

1. **Verification needs a basis, not just a word.** "VERIFIED" alone is unfalsifiable. Say *how* —
   publisher page, DOI resolution, document opened and read.
2. **Never write VERIFIED for a document you did not open.** This bootstrap opened none; see
   `research/verification_log.md`. Honesty here is what makes the rest of the repository usable.
3. **Role is not tier.** A vendor application note can be a strong MEASUREMENT AUTHORITY and a
   useless THEORY AUTHORITY.
4. **"Does NOT justify" is mandatory.** Writing it forces you to decide what the source actually
   covers, which is the step that prevents scope-creeping citations.
5. **Licence before any figure use.** Open access ≠ reusable figure.
6. **Every claim a source supports gets a row** in `research/claims_and_sources.md`.
