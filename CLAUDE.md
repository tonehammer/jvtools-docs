# CLAUDE.md — JVtools Docs

**Auto-loaded into every Claude Code session in this repo.** This is the single documentation site for the **JVtools** family of Houdini digital assets (Jovan Maric's tools). One site, many products, each a top-level section. Read fully before editing.

## What this repo is

A **Retype** static documentation site. Each product (HDA) is a folder under the repo root; the root `index.md` is the landing page with product cards. Adding a new product = add a folder + a nav link, touching nothing else.

- **Tool:** Retype **Pro** (one-time license — no subscription). Config: `retype.yml`.
- **Local preview:** `retype start` (live-reload dev server). **Build:** `retype build` → static site in `.retype/` (git-ignored).
- **Deploy:** push to GitHub → auto-build → live (GitHub Pages via Retype's GitHub Action, or Cloudflare Pages watching the repo). Set up once; after that **push = live**, like GitBook's git sync. ⏳ Deploy wiring is TODO — pending Jovan's Retype Pro key + a chosen domain (`url:` in retype.yml is a placeholder).

## Structure & conventions

- **Root `index.md`** — landing page, `order: 10000`, product cards via `[!card title=... icon=... text=...](/product/README.md)`.
- **One folder per product** (e.g. `rplidar-in/`). Folder label/icon/order come from an **`index.yml`** inside it. The folder's default page is `README.md`.
- **Page frontmatter:** `icon:` + `order:`. **Higher `order` = higher in the sidebar** (verified). No order ⇒ alphabetical by title.
- **Icons:** emoji shortcodes (`:satellite:`, `:wrench:`) are safe and used throughout; Octicon names also work.
- **NO GitBook-style `description:` frontmatter** (it rendered as an unwanted subtitle — a rule carried from the product repos). Keep `icon:`/`order:` only.
- **Retype specifics:** don't guess component/config syntax from memory — Retype iterates. Verify against retype.com docs (WebFetch) before using an unfamiliar option, same discipline as never-guess-parm-names in the product repos.

## The product code repos (the map)

User-facing docs here must stay in sync with each HDA's **parameter tooltips / Help fields, which are the source of truth**. To sync, add the relevant code repo to the session (`claude --add-dir "<path>"` or `/add-dir`), read its parm builder for ground-truth names/labels/help, then update the docs. Never guess parm names.

| Product | Docs folder | Code repo on disk | Ground truth |
| --- | --- | --- | --- |
| RPLidar In | `rplidar-in/` | `C:\Users\Jovan\Documents\GitHub\RPLidar for Houdini` | `houdini/rplidar_sop.py` → `setup_hda_parms()` (parm names + `setHelp` tooltips) |
| Reallusion Importer for Houdini | *(add folder)* | *(path TBD — fill in)* | *(TBD)* |

## Working rules

- **Minimal chat formatting**, get to the point (Jovan is technical).
- **The tooltip/Help field in the HDA is authoritative.** Docs are synced to it manually — change the parm, update the doc; there's no auto-binding.
- **Pushing:** this is a docs repo (not module code), so summarize changes and get Jovan's go-ahead before pushing, unless he says otherwise. (Mirrors the product-repo push tiers.)
- Typical flow: Jovan asks for a feature → in one session Claude edits the **product code** (its repo) *and* the **docs** (here) → pushes both → Retype rebuilds the site.
