# research.pharns.com — "Pharns Genece — Notes from the Field"

Author hub + research notebook. MkDocs Material, deployed to GitHub Pages by `.github/workflows/deploy.yml` on push to `main`.

## What this site is (Pharns, 2026-10-14)
The personal, human, informal side: research notes, things I'm learning across cyber, and personal items like favorite quotes. It's also a **resource to help and teach people in cyber**: what I've learned, shared so others can learn it faster. The citable work lives elsewhere.

## Rules
- **Voice is Pharns's.** Aegis edits only on request.
- **LinkedIn pointer only when truly relevant** to ongoing work or citability. When that happens, first **promote the work to its proper home** (AAM-TR on aamcyber.com, a DOI) and point the post at that copy. Link back to the notebook entry as the origin when useful.
- **Notebook → formal report:** a note that grows substantial graduates to an AAM-TR on aamcyber.com. The notebook entry then links to it.
- **Personal items OK, OPSEC still binds:** no family/health/VA details, no location, no client data. Attribute every quote; verify quotes from others against a source before posting.
- **Publications link out to the canonical copy** (aamcyber.com / Zenodo DOI). Do not re-host papers here; this site is the author hub, not the archive.
- **No `citation_*` meta tags and no PDFs under `docs/notebook/`.** Scholar would index informal notes as articles.
- **Drafts live in the vault, OUTSIDE this repo, until they clear review.** The repo is public: a committed draft is readable on GitHub even if the site doesn't build it. The disclosure check happens BEFORE `git commit`, not before deploy.
- **The L4 hook only gates pushes Aegis makes.** A push Pharns makes himself is ungated, so run the registry check by hand first.
- **Every notebook post is a public disclosure.** Before pushing: check the Public Disclosure Registry (Tier 2 = "what it does" only), run `strategic-check` (L4 gate blocks the push otherwise). No patent serials, no mechanism detail on filed claims, no AAM Cyber client data.
- Public entity is AAM Cyber, never IPCo.

## Notebook is hidden (2026-10-14)
The nav entry and home-page section are commented out until 2+ posts clear the disclosure check. To unhide: restore the commented `nav` lines in `mkdocs.yml`, and append this to `docs/index.md`:

```markdown
## Notebook

Shorter notes on what I am researching and learning, across cyber. Not peer reviewed.

[Read the notebook →](notebook/index.md)
```

## Add a book
Under "Books I've read" in `docs/index.md`: title linked to its Google Books page (`https://books.google.com/books?id=<volume id>`; prefer a full-view edition when one exists), then a meta line `Author · year · Google Books`. Add the same line to `docs/llms.txt`.

## Add a notebook post
Create `docs/notebook/posts/YYYY-MM-DD-slug.md`:

```markdown
---
date: 2026-10-14
categories:
  - Detection Engineering
---

# Title

First paragraph (shown as the excerpt).

<!-- more -->

Rest of the post.
```

## One-time GitHub Pages setup (before the DNS record)
1. Repo `Pharns/research` → Settings → Pages → Source: **GitHub Actions**.
2. Custom domain: `research.pharns.com` → Save. (No CNAME file: GitHub ignores it for Actions deploys.)
3. Recommended: verify `pharns.com` under GitHub account Settings → Pages (blocks subdomain takeover).
4. THEN Cloudflare: CNAME `research` → `pharns.github.io`, **DNS only**.
5. Once the cert issues: tick **Enforce HTTPS**.

Deps: full dependency closure pinned to the exact versions tested locally (mkdocs 1.6.1, Material 9.7.6). Not hash-locked; a fresh local install fails to build `watchdog` on Python 3.14, so the lock was read from the tested venv. Actions are pinned to commit SHAs.

## Build locally
```bash
python3 -m venv .venv && .venv/bin/pip install -r requirements.txt
.venv/bin/mkdocs build --strict   # required before every push
.venv/bin/mkdocs serve            # http://127.0.0.1:8000
```
