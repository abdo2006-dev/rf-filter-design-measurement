# PERSISTENCE

*How this project survives. Read this if the repository ever seems to have gone missing.*

---

## What happened in the bootstrap session (2026-10-02)

The session was asked to create a **private GitHub repository** named
`rf-filter-design-measurement` and push the bootstrap to it.

**It could not.** Two independent attempts:

| Method | Result |
|---|---|
| GitHub MCP `create_repository` | `403 Resource not accessible by integration` |
| `gh api -X POST /user/repos` | `403 This GitHub API path is not available: sessions are bound to their configured repositories.` |

The session's GitHub credential is scoped to two pre-existing, **unrelated** repositories
(`clip-distribution-mvp`, `bloxshop-theme-live`). Repository creation is not in scope, and
pushing this project into either of those repositories would have been wrong, so it was not done.

**Fallback executed instead:** local git repository, one clean bootstrap commit, a **verified**
git bundle, and a zip archive. All three are described below.

## What exists

| Artefact | Path | What it is |
|---|---|---|
| Working repository | `rf-filter-design-measurement/` | Full project, git-initialized, one commit, clean tree |
| Git bundle | `rf-filter-design-measurement.bundle` | Complete repository *including history*, single file, verified clonable |
| Zip archive | `rf-filter-design-measurement.zip` | Plain file copy including the `.git` directory |

**Prefer the bundle.** It preserves commit history and verifies its own integrity. The zip is a
convenience copy for anyone who does not want to touch git.

## Restore from the bundle

```bash
git clone rf-filter-design-measurement.bundle rf-filter-design-measurement
cd rf-filter-design-measurement
git log --oneline          # should show the bootstrap commit
git status                 # should be clean
```

A bundle clone leaves `origin` pointing at the bundle file. Repoint it at GitHub once the
repository exists:

```bash
git remote remove origin
```

…then follow the next section.

## Create the private GitHub repository manually

### Option A — GitHub CLI (fastest)

```bash
cd rf-filter-design-measurement

gh auth login                                  # once, if not already authenticated

gh repo create rf-filter-design-measurement \
  --private \
  --source=. \
  --remote=origin \
  --description "Design, EM simulation, fabrication, VNA characterization and de-embedding of a microstrip RF filter." \
  --push
```

Then verify:

```bash
gh repo view abdo2006-dev/rf-filter-design-measurement --json name,visibility,defaultBranchRef
git log --oneline -1
git status
```

`visibility` must read `PRIVATE`.

### Option B — web UI + plain git

1. Go to <https://github.com/new>.
2. **Repository name:** `rf-filter-design-measurement`
3. **Visibility:** **Private**
4. **Do not** add a README, `.gitignore` or licence — this repository already has them, and
   initializing would create a conflicting commit.
5. Create, then run:

```bash
cd rf-filter-design-measurement
git remote add origin https://github.com/abdo2006-dev/rf-filter-design-measurement.git
git branch -M main
git push -u origin main
```

### Verify the push really landed

```bash
git ls-remote --heads origin                    # remote main should exist
git rev-parse HEAD                              # local commit SHA
git rev-parse origin/main                       # must equal the line above
```

If those two SHAs match, the work is persisted off this machine. **Only then** is the bootstrap
genuinely safe.

## If the Claude session should be able to do this itself next time

Repository creation failed because this session's GitHub access is bound to pre-selected
repositories. To fix it for future sessions:

- Connect or reconnect the GitHub account at <https://claude.ai/connect-github>, and make sure the
  Claude GitHub App is installed for the account.
- Create `rf-filter-design-measurement` on GitHub **first** (Option A or B above), then start a new
  Claude session with that repository selected as a source. From then on the session can read,
  commit and push to it directly, and `PROJECT_STATE.md` / `HANDOFF.md` can be kept current
  automatically.

Separately, this session's **network egress policy** blocked every attempt to open a PDF or
resolve a DOI (`www.keysight.com`, `doi.org`, `api.crossref.org`, `arxiv.org`,
`ieeexplore.ieee.org`, `openlibrary.org` were all denied). If a future session should verify
sources properly, widen **Network access** in the environment settings — either a broader access
level or those specific hosts added to the allowed domains. Access levels are described at
<https://code.claude.com/docs/en/claude-code-on-the-web>.

## Standing rule

> The container this was built in is ephemeral. **The GitHub repository is the source of truth.**
> Until the push in this document has actually been verified, the bundle and the zip are the only
> copies, and they must be stored somewhere that is not a Claude container.

Back up after every working session. A project that exists in one place does not exist.
