# CLAUDE.md — JVtools Docs

**Auto-loaded into every Claude Code session in this repo.** This is the single documentation site for the **JVtools** family of Houdini digital assets (Jovan Maric's tools). One site, many products, each a top-level section. Read fully before editing.

> **⛔ THIS REPO IS DOCUMENTATION ONLY (Jovan, 2026-07-11).** A session started here edits the Retype docs and **nothing else** — **never** run hython, edit `.hdalc`/HDA files, or do any Houdini asset surgery from this session. That work lives in each product's own code repo (`RPLidar for Houdini`, `Reallusion Importer for Houdini`), whose CLAUDE.md owns the direct-asset-edit workflow. If a docs task seems to need an asset change (e.g. "add this logo to the HDA"), it means add it to the **docs** — product logos/screenshots are plain image copies under each product folder's `static/`.

> **🔴 NO UNRELEASED PRODUCT LIVES IN THIS REPO (Jovan, 2026-08-25).** A tool gets a docs section here **only once it is published on Gumroad** — not when it is being written, not when it is nearly done. **`visibility: hidden` is NOT sufficient and this is the trap:** it genuinely keeps a section out of the built site's nav and sitemap (verified by A/B), but **this repo is PUBLIC**, so the markdown is still plainly readable on github.com — name, pitch, feature list, roadmap and all. Hidden from the *site* is not hidden from the *world*. Pre-release sections live in the PRIVATE **`jvtools-internal/docs-staging/<slug>/`**, laid out exactly as they will be here so publishing is a copy rather than a rewrite; that folder's README carries the release checklist. ⚠ The same applies to **`versions/<slug>.json`** — the manifest names the product and its store URL, and nothing reads it until a build ships, so it stages too. ⚠ **And the leak is not only files: a COMMIT MESSAGE naming an unreleased product is just as public, and so is a note in this file about which products are staged.** Keep both generic here; the named list lives in the staging folder's README, in the private repo. 🔑 **This repo cannot simply be made private**: Pages serves the site from it and the shipped HDAs fetch the manifests unauthenticated over `raw.githubusercontent.com`. Public is a requirement of the product, which is exactly why what goes in it has to be curated.

> **🔒 FAMILY-INTERNAL KNOWLEDGE DOES NOT LIVE IN THIS REPO (2026-07-24).** This repo is **PUBLIC** — required by GitHub Pages and the HDAs' raw-manifest update check. The shared internal files (`JVTOOLS_HOUDINI_LESSONS.md`, `JVTOOLS_PRODUCT_STANDARDS.md`, `JVTOOLS_WORKING_RULES.md`) live in the **PRIVATE `jvtools-internal` repo** (`C:\Users\Jovan\Documents\GitHub\jvtools-internal`), auto-loaded into every session by an `@`-import in `~/.claude/CLAUDE.md` (user scope - a project-level import of a path outside the working directory is gated behind a one-time dialog and silently disabled if it is declined). **Never add internal engineering knowledge, product-repo lore, or anything trade-secret-adjacent here** — public docs pages, `versions/*.json` manifests, and this hub file only. (The two shared files briefly lived here 2026-07-24; they were moved out and this repo's history was scrubbed.)

## What this repo is

A **Retype** static documentation site. Each product (HDA) is a folder under the repo root; the root `index.md` is the landing page with product cards. Adding a new product = add a folder + a nav link, touching nothing else.

- **Tool:** Retype **Pro** (one-time license — no subscription). Config: `retype.yml`.
- **Local preview:** `retype start` (live-reload dev server). **Build:** `retype build` → static site in `.retype/` (git-ignored).
- **Deploy target (decided 2026-07-08):** GitHub Pages **project site** at **`https://tonehammer.github.io/jvtools-docs/`** (free github.io for now; migrate to a custom domain later — Pro license has 3 project slots). The Retype Pro **license key is registered to the domain `tonehammer.github.io`** and only builds projects whose retype.yml `url` matches — so `url:` is set to that exact base. Push to `main` → the workflow in `.github/workflows/retype-deploy.yml` builds and publishes → live. ⏳ Still TODO: create+push the GitHub repo, add the license key (repo secret for the Action), enable Pages.

## Structure & conventions

- **Root `index.md`** — landing page, `order: 10000`, product cards via `[!card title=... icon=... text=...](/product/README.md)`.
- **One folder per product** (e.g. `rplidar-in/`). Folder label/icon/order come from an **`index.yml`** inside it. The folder's default page is `README.md`.
- 🔧 **EVERY SECTION HAS A `reference/` SUBFOLDER, AND THE PARAMETER REFERENCE, TROUBLESHOOTING, CHANGELOG AND LICENCE LIVE IN IT — now and henceforth** (Jovan, 2026-08-26). Those four are lookup material; loose at the top level they bury the pages a new customer actually needs. Reallusion Importer was already built this way; Advanced Velocity, RPLidar In and COPout were moved to match on 2026-08-26. **`reference/index.yml` = `label: Reference` / `icon: book` / `order: 80` / `expanded: true`**, and inside it parameter reference 110, limitations 100, performance 90, troubleshooting 80, changelog 70, licence 60. Top level is then Getting started 100, Using 90, Reference 80 in every section.
  🔴 **The move changes URLs, and the links are not all in this repo** — after any such move, grep `(parameters.md)` / `(troubleshooting.md)` / `(changelog.md)` / `(license.md)` here until clean, then fix **jvtools-website**: the version badge href in `src/pages/products/[slug].astro` and every `notes:` in `src/data/changelog.mjs`.
- **Page frontmatter:** `icon:` + `order:`. **Higher `order` = higher in the sidebar** (verified). No order ⇒ alphabetical by title.
- **Icons:** emoji shortcodes (`:satellite:`, `:wrench:`) are safe and used throughout; Octicon names also work.
- **NO GitBook-style `description:` frontmatter** (it rendered as an unwanted subtitle — a rule carried from the product repos). Keep `icon:`/`order:` only.
- **Retype specifics:** don't guess component/config syntax from memory — Retype iterates. Verify against retype.com docs (WebFetch) before using an unfamiliar option, same discipline as never-guess-parm-names in the product repos.

## The product code repos (the map)

User-facing docs here must stay in sync with each HDA's **parameter tooltips / Help fields, which are the source of truth**. To sync, add the relevant code repo to the session (`claude --add-dir "<path>"` or `/add-dir`), read its parm builder for ground-truth names/labels/help, then update the docs. Never guess parm names.

| Product | Docs folder | Code repo on disk | Ground truth |
| --- | --- | --- | --- |
| RPLidar In | `rplidar-in/` | `C:\Users\Jovan\Documents\GitHub\RPLidar for Houdini` | `houdini/rplidar_sop.py` → `setup_hda_parms()` (parm names + `setHelp` tooltips) |
| Reallusion Importer for Houdini | `reallusion-importer/` | `C:\Users\Jovan\Documents\GitHub\Reallusion Importer for Houdini` | The HDA's per-parm **Help fields** (typed in Edit Parameter Interface) + `houdini/reallusion_importer_help.txt`. (GitBook retired 2026-08-07 — this Retype section is the only docs surface.) |

## Authoring reference

- **Icons:** page/folder/nav `icon:` must be a **bare Octicon name** (`icon: rocket`, `icon: broadcast`) — NOT an emoji shortcode (`:rocket:` silently renders nothing). Full list: retype.com/components/octicons. In-body icon component is `:icon-<name>:`.
- 🔴 **A PRODUCT'S ARTWORK IS REFERENCED IN THREE PLACES — changing `index.yml` alone changes nothing you can see.** Swapping Advanced Velocity's icon in `advanced-velocity/index.yml` left the site looking untouched, because the two references that actually render were somewhere else:
  1. `<product>/index.yml` → `icon:` — the folder entry.
  2. **`<product>/README.md` frontmatter `icon:`** — the section's landing page, which is what the sidebar entry shows. **This is the one that gets missed.**
  3. **`<product>/README.md` body `<img src="static/…">`** — the hero/cover image, referenced from nowhere else.
  🔧 **The rule: after replacing any shared asset, `grep` the OLD filename across `--include=*.md --include=*.yml` and only stop when it returns nothing.** Do not reason about which reference "should" be the one; there are three and they are independently authored. Same discipline as re-grepping every conditional after deleting a parm.
  ⚠ And do not diagnose a stale-looking site as a deploy lag before doing that grep — the Retype action publishes on every push to `main`, so a page that still looks old after a push is almost always a reference you did not change.
- **Colored callouts (FREE, not Pro):** `!!!<type>` … `!!!`. Types: `primary` (blue), `info` (light-blue), `success`/`tip` (green), `warning` (yellow), `danger` (red), `question` (purple), `secondary` (gray), `base/light/dark/ghost/contrast`. Optional title after the type. Collapsible: `!!-` (collapsed) / `!!+` (expanded), e.g. `!!-danger Title`. (Needed for the Reallusion Importer section.) 🔴 **The type must be ATTACHED: `!!!warning Title`, never `!!! warning Title`** — the spaced form silently falls back to the default info style and the type word leaks into the rendered title. Shipped broken once (2026-08-07, three callouts on timed-events); a screenshot is what caught it.
- **Cards** (landing pages): `[!card title="…" icon="…" text="…"](/path/README.md)`. The whole card is the only clickable link (→ its `(target)`). **Do NOT put purchase/Gumroad links in cards** — markdown links inside `text=`/`footer=` render as raw, unclickable text in this Retype version (Jovan, verified 2026-07-22).
- **Gumroad / purchase link (rule, Jovan 2026-07-22):** each product's Gumroad link goes as the **first element directly below the cover image** on its first page (README), not in the card. Format: `<p style="text-align:center; margin:0 0 1.5rem;"><a href="<gumroad-url>"><strong>Get it on Gumroad →</strong></a></p>`. URL source of truth = `versions/<product>.json` `url`. Skip it if that URL is a `PLACEHOLDER-*` (product not yet for sale).
- **Version on first page (rule, Jovan 2026-07-22):** show the current version **inline at the first mention of the product name** in the opening body paragraph, e.g. `Welcome! **Advanced Velocity** (v1.0) is a single Houdini SOP…`. **NOT in the H1** — the H1 also drives the sidebar label, so a version there clutters the nav. **Source of truth = the product's changelog page** — the top-most `## Version X.Y.Z` heading, now `reference/changelog.md` in every section. ⚠ **REVISED 2026-08-26: the `versions/<product>.json` `latest` field may no longer lag.** It still feeds the HDAs' in-app update check rather than the docs, but it carries the same full version, patch digit included — so a disagreement with the changelog is drift to fix, not a design.
- **Exclude from build:** the `exclude:` list in retype.yml (CLAUDE.md is already excluded — keeps the hub in-repo but off the site).

## 🔧 VERIFYING VISUALLY — build it and LOOK, never reason from the CSS (2026-08-06)

**Standing rule for any change with a visual result** (a card, a cover image, an icon, a layout tweak, a callout): render the built page and look at it before saying it is done. This is cheap — under a minute end to end — and it is the step that catches the whole class of "correct in the abstract, wrong on screen".

⚠ **Scope (Jovan, 2026-08-07): "visual result" means pixels and layout, not prose.** A text-only rewrite of an existing page needs a `retype build` (catches broken links/syntax), not a screenshot. Screenshot when a change touches nav/section structure, images or image paths, icons, cards, callout/Steps syntax, or anything Retype lays out — those break silently; paragraphs don't.

Why it is a rule and not a nicety: swapping the Advanced Velocity card image looked like a one-line edit, and three candidate images in a row *reasoned* fine and *rendered* wrong (a square crop lost 12% top and bottom; the 16:9 with a title lockup grazed it against the panel border). Reading the CSS told me the box existed; only the render told me what it did to the picture.

**The loop:**
1. `retype build .` from the repo root (~3s, 36 pages). Works locally with no license key despite `poweredByRetype: false` being Pro-only.
2. Serve it — `retype start` for live reload, or the **jvtools-docs-editor** (`C:\Users\Jovan\Documents\GitHub\jvtools-docs-editor\server.py`, port **8123**, base path **`/jvtools-docs/`**, rebuilds on save). ⚠ Serving `.retype/` directly at `/` 404s every asset — internal links are absolute under `/jvtools-docs/`.
3. Screenshot it headless with Edge, then **Read the PNG**:
   ```
   msedge --headless=new --disable-gpu --hide-scrollbars \
     --force-device-scale-factor=1 --window-size=1400,1300 \
     --virtual-time-budget=6000 \
     --screenshot="C:/full/win/path/out.png" "http://localhost:8123/jvtools-docs/"
   ```
   🔴 **The path must be a WINDOWS path** — a git-bash `/c/...` path silently renders Edge's "File not found" page and still reports "bytes written". `pwd -W` gives the right form. **Always open the PNG; never trust the exit message.**
4. **Check more than one viewport width.** Card and image boxes reflow at Retype's breakpoints, and a crop that survives at 1750 can clip at 1400. Two desktop widths plus one mobile (`--window-size=430,900 --force-device-scale-factor=2`) covers it.
5. For measuring rather than eyeballing (box sizes, `object-fit`, natural vs rendered dimensions), query the live DOM with the browser tools instead of guessing — that is how the geometry below was established.

📌 **Session state for the "jvtools business" chat — docs + marketing + Gumroad — lives in `jvtools-internal/BUSINESS_HANDOVER.md`.** Read it at the start of a session that covers any of those; it carries what is blocked, what is deployed and what is next.

📌 **The family-wide file for this work is `jvtools-internal/JVTOOLS_MARKETING_IMAGERY.md`**, imported just below (Jovan, 2026-08-06: the graphics work happens in THIS session, so it auto-loads here and nowhere else).
⚠ **Verify it actually loaded — `/context` should list it under Memory files.** A project-scope `@`-import whose path resolves OUTSIDE the working directory is an *external import*: gated behind a one-time approval dialog, and **silently dead forever if that is declined or never appears** — the exact failure that killed the shared-file imports in all four product repos. It resolves fine when the session's cwd is the GitHub root (jvtools-internal sits inside it); starting a session *in* jvtools-docs is the case that can trip the gate. If it is missing, just read the file by hand.

@C:/Users/Jovan/Documents/GitHub/jvtools-internal/JVTOOLS_MARKETING_IMAGERY.md It separates **documentation** covers (below: a browser crops them, so they have measured safe areas) from **Gumroad** covers (a fixed frame, no safe area, owned by the product repos' cover sessions). The card geometry here is the docs-specific detail; the shared technique and the store side live there.

### Card image geometry (measured on the live DOM, so nobody re-derives it)
- The card's image panel is **`object-fit: cover`** — it always crops, never letterboxes.
- The panel is `md:w-5/12` of the card width with its **height set by the description text**, not the image. So its aspect moves with BOTH the viewport width and the blurb length.
- 🔴 **IT CROPS IN TWO DIFFERENT DIRECTIONS, AND ONE MEASUREMENT ONLY EVER SHOWS YOU ONE OF THEM.** Measured on the RPLidar card, 2026-08-06:

  | viewport | panel | aspect | what is cropped |
  |---|---|---|---|
  | 1280 | 240x228 | 1.06:1 | full height, only the **middle 59% of the WIDTH** |
  | 1920 | 398x172 | 2.32:1 | full width, only the **middle 77% of the HEIGHT** |

  The blurb rewraps to fewer lines as the viewport widens, the panel gets shorter, and the crop flips axis. **The usable area is the INTERSECTION of the two**, not either one.
- **Mobile:** the panel stacks on top at `pb-9/16` — **exactly 16:9**.
- 🔧 **Therefore: supply 16:9, and keep everything that matters inside the middle 59% horizontally AND the middle 77% vertically.** On a 1600x900 that is x 328–1272, y 105–795. Corner-anchored logos and title lockups are the first casualties; a picture *composed* to the centre survives every breakpoint.
  ⚠ An earlier note here said "middle ~73%" with no vertical limit. That came from a single measurement at one viewport and was wrong in both respects — **measure at a narrow AND a wide viewport before trusting a safe area.**
- 🔧 **When a composition has to give somewhere, favour the WIDE case** (Jovan, 2026-08-06): these are Houdini users on desktop monitors, so the 1920-ish regime is the one most people see.
- The cover generator's `card` preset encodes both insets (`0.205` / `0.115`) and `--guides` draws the box on all four sides.
- Photographic cards ship as **JPG ~1600x900, q88 (~240 KB)**; a PNG of the same image is ~2.3 MB for no visible gain. **Flat vector art stays PNG** — JPG rings on hard edges and comes out larger anyway (RPLidar's card: 104 KB PNG).

## Retype features in use (added 2026-08-06 — read before adding more)

🔴 **A LOCAL BUILD RUNS WITHOUT PRO.** `RETYPE_KEY` is a CI secret and is not
in the shell environment, so `retype build` locally **silently skips every Pro
feature** — the only sign is one warning about the "Powered by Retype" logo.
A Pro feature therefore cannot be verified locally at all: it renders nothing,
which is indistinguishable from a broken config. **Verify Pro features on the
deployed site**, and do not conclude the YAML is wrong from a local build.

- **`data` + templating** — product versions live in ONE place (`retype.yml`
  `data:`) and pages say `{{ av.version }}`. A release bumps one line.
  ⚠ **Templating does NOT reach inside code spans or code blocks** (Retype
  emits them `v-pre`). Good news for code samples, which are safe by
  construction; bad news for anything like a filename in backticks — that
  still has to be written out or kept generic (`vX.Y`).
  🔑 The `data:` versions are the DOCS versions (changelog is their source of
  truth). `versions/<slug>.json` is a separate signal for the HDAs' update
  check. ⚠ Revised 2026-08-26: it used to lag on patches and no longer does —
  both carry the full version, so they should agree exactly.
- **Steps** (`>>> Title` … `>>>`) — used for the install instructions on
  Advanced Velocity and Reallusion Importer.
  🔴 **Consecutive `>>>` blocks do NOT auto-increment in Retype 4.6.0** — each
  becomes its own group and every step renders as "1", whatever the docs say
  about stacking. **Number them explicitly: `>>> 1. Title`, `>>> 2. Title`.**
  Only a screenshot catches this; the build is clean and the HTML looks
  plausible until you read the `step-number` attributes.
- **Social preview images** — Retype emits full Open Graph + Twitter tags. The
  per-page frontmatter **`image:`** sets `og:image` (verified); with no
  `image:` it falls back to the first image in the body, and the ROOT page had
  none at all, so sharing the docs link showed a blank card.
  🔴 **Retype hardcodes `og:image:width`/`height` to 1200x630 regardless of the
  real file**, so a social image of any other size ships wrong dimensions to
  every platform reading those tags. **Make them exactly 1200x630** — the
  cover generator (`Advanced Velocity/business-and-marketing/covers/`) has a
  `social` preset for this.
- **`lastUpdated`** — git-backed date footer, **Pro**. Needs full history at
  build time; the deploy workflow already checks out with `fetch-depth: 0`.
- **Embed** — `[!embed aspect="16:9"](url)`, needs the `/embed/` form of a
  YouTube URL, not `watch?v=`. Currently a commented-out placeholder on the
  Advanced Velocity landing page awaiting the trailer.
- **Analytics** — an `integrations:` block sits commented in `retype.yml`.
  Uncomment one and fill in the id. Plausible needs no cookie banner; Google
  Analytics is free but does in the EU.

## Retype Pro backlog (license unlocks these — implement when useful)

Already active: breadcrumbs, right-side Table of Contents, footer removed
(`poweredByRetype: false`), `lastUpdated` date.
- **Quick wins:** Next/Previous nav buttons; Branding base color (one accent color for the whole site).
- **As the family grows:** Stack navigation mode (stacked per-product sidebar); Nav badges/tags ("New"/"Beta"); Hub link (if a jvtools.com portal ever exists).
- **CI hardening:** Strict build mode — fail the build on broken links instead of shipping them. Turn on soon.
- **If needed:** Private/Protected pages (password-gate unreleased-product docs).

## Working rules

- **Minimal chat formatting**, get to the point (Jovan is technical).
- **The tooltip/Help field in the HDA is authoritative.** Docs are synced to it manually — change the parm, update the doc; there's no auto-binding.
- **Pushing (granted 2026-07-09):** this is a docs repo — Claude may commit + push **at will, without asking**. Still summarize what changed in the message. (A push to `main` triggers the Retype CI build → live site.)
- **Changelog altitude (Jovan, 2026-07-09):** public product changelog pages **compress small changes** — group minor fixes/tweaks under a single **"Bug fixes and improvements"** line; reserve individual bullets for headline features. (The product repos' internal CLAUDE.md trackers stay verbose; the public docs do not.)
- 🔧 **Changelog REGISTER (Jovan, 2026-08-25) — the altitude rule says which changes get a bullet; this says how long a bullet is. ONE LINE, and it stops there.** No explaining the mechanism (*"Character Creator writes such a map once and cross-references it…"*), no teaching how to use the feature (*"Left at its default it changes nothing, and it works in both FBX and USD modes"*), no reassuring caveats. Target ~12 words, ceiling ~20; if it needs a semicolon or an em-dash aside it is too long. ✅ *"Fixed an issue where shared texture objects would be imported as flat white."* **All five changelogs were swept to this register on 2026-08-25** (three docs pages, the Neonyte staging page, and the website's suite-wide `changelog.mjs`). The removed material belongs on the feature's docs page, which keeps the full §9 voice — a changelog is an inventory, a docs page is the argument. Full rule: STANDARDS §9.
- 🔧 **Who writes it (Jovan, 2026-08-25): OPUS/FABLE dictates, SONNET executes in plain English** — online docs and internal docs alike. The reasoning model settles the content and the claims; the executing model writes the prose and **invents nothing that was not dictated**. STANDARDS §9.
- **Retype v4.6.0 build is flaky:** an internal `DeploySitemapJob` concurrency race intermittently fails a build with no content problem — **just re-run it** (`gh run rerun <id> -R tonehammer/jvtools-docs`). The GitHub **Pages** deploy can also stall "queued/errored" — cancel the stuck run + re-dispatch (`gh run cancel <id>`; `gh workflow run retype-deploy.yml --ref master`). Cards: `image="/product/static/x.png"` sets a banner, `footer="[t](url)"` adds a secondary link, the whole card links to its `(target)` — no multi-link support. `versions/*.json` is excluded from the build (read by HDAs' update checks via GitHub raw).
- Typical flow: Jovan asks for a feature → in one session Claude edits the **product code** (its repo) *and* the **docs** (here) → pushes both → Retype rebuilds the site.
