# CLAUDE.md — JVtools Docs

**Auto-loaded into every Claude Code session in this repo.** This is the single documentation site for the **JVtools** family of Houdini digital assets (Jovan Maric's tools). One site, many products, each a top-level section. Read fully before editing.

## What this repo is

A **Retype** static documentation site. Each product (HDA) is a folder under the repo root; the root `index.md` is the landing page with product cards. Adding a new product = add a folder + a nav link, touching nothing else.

- **Tool:** Retype **Pro** (one-time license — no subscription). Config: `retype.yml`.
- **Local preview:** `retype start` (live-reload dev server). **Build:** `retype build` → static site in `.retype/` (git-ignored).
- **Deploy target (decided 2026-07-08):** GitHub Pages **project site** at **`https://tonehammer.github.io/jvtools-docs/`** (free github.io for now; migrate to a custom domain later — Pro license has 3 project slots). The Retype Pro **license key is registered to the domain `tonehammer.github.io`** and only builds projects whose retype.yml `url` matches — so `url:` is set to that exact base. Push to `main` → the workflow in `.github/workflows/retype-deploy.yml` builds and publishes → live. ⏳ Still TODO: create+push the GitHub repo, add the license key (repo secret for the Action), enable Pages.

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
| Reallusion Importer for Houdini | `reallusion-importer/` | `C:\Users\Jovan\Documents\GitHub\Reallusion Importer for Houdini` | The HDA's per-parm **Help fields** (typed in Edit Parameter Interface) + `houdini/reallusion_importer_help.txt`. ⚠ Docs are **dual-hosted**: this Retype section AND a still-**live GitBook** in the product repo's `docs/` (existing customers point there). Keep **both** in sync until the GitBook→Retype migration completes "down the line". |

## Authoring reference

- **Icons:** page/folder/nav `icon:` must be a **bare Octicon name** (`icon: rocket`, `icon: broadcast`) — NOT an emoji shortcode (`:rocket:` silently renders nothing). Full list: retype.com/components/octicons. In-body icon component is `:icon-<name>:`.
- **Colored callouts (FREE, not Pro):** `!!!<type>` … `!!!`. Types: `primary` (blue), `info` (light-blue), `success`/`tip` (green), `warning` (yellow), `danger` (red), `question` (purple), `secondary` (gray), `base/light/dark/ghost/contrast`. Optional title after the type. Collapsible: `!!-` (collapsed) / `!!+` (expanded), e.g. `!!-danger Title`. (Needed for the Reallusion Importer section.)
- **Cards** (landing pages): `[!card title="…" icon="…" text="…"](/path/README.md)`.
- **Exclude from build:** the `exclude:` list in retype.yml (CLAUDE.md is already excluded — keeps the hub in-repo but off the site).

## Retype Pro backlog (license unlocks these — implement when useful)

Already active: breadcrumbs, right-side Table of Contents, footer removed (`poweredByRetype: false`).
- **Quick wins:** Last-Updated label (git timestamps per page); Next/Previous nav buttons; Branding base color (one accent color for the whole site).
- **As the family grows:** Stack navigation mode (stacked per-product sidebar); Nav badges/tags ("New"/"Beta"); Hub link (if a jvtools.com portal ever exists).
- **CI hardening:** Strict build mode — fail the build on broken links instead of shipping them. Turn on soon.
- **If needed:** Private/Protected pages (password-gate unreleased-product docs).

## Working rules

- **Minimal chat formatting**, get to the point (Jovan is technical).
- **The tooltip/Help field in the HDA is authoritative.** Docs are synced to it manually — change the parm, update the doc; there's no auto-binding.
- **Pushing (granted 2026-07-09):** this is a docs repo — Claude may commit + push **at will, without asking**. Still summarize what changed in the message. (A push to `main` triggers the Retype CI build → live site.)
- Typical flow: Jovan asks for a feature → in one session Claude edits the **product code** (its repo) *and* the **docs** (here) → pushes both → Retype rebuilds the site.
