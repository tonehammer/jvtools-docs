# CLAUDE.md — JVtools Docs

**Auto-loaded into every Claude Code session in this repo.** This is the single documentation site for the **JVtools** family of Houdini digital assets (Jovan Maric's tools). One site, many products, each a top-level section. Read fully before editing.

> **⛔ THIS REPO IS DOCUMENTATION ONLY (Jovan, 2026-07-11).** A session started here edits the Retype docs and **nothing else** — **never** run hython, edit `.hdalc`/HDA files, or do any Houdini asset surgery from this session. That work lives in each product's own code repo (`RPLidar for Houdini`, `Reallusion Importer for Houdini`), whose CLAUDE.md owns the direct-asset-edit workflow. If a docs task seems to need an asset change (e.g. "add this logo to the HDA"), it means add it to the **docs** — product logos/screenshots are plain image copies under each product folder's `static/`.

> **🔴 NO UNRELEASED PRODUCT LIVES IN THIS REPO (Jovan, 2026-08-25).** A tool gets a docs section here **only once it is published on Gumroad** — not when it is being written, not when it is nearly done. **`visibility: hidden` is NOT sufficient and this is the trap:** it genuinely keeps a section out of the built site's nav and sitemap (verified by A/B), but **this repo is PUBLIC**, so the markdown is still plainly readable on github.com — name, pitch, feature list, roadmap and all. Hidden from the *site* is not hidden from the *world*. Pre-release sections live in the PRIVATE **`jvtools-internal/docs-staging/<slug>/`**, laid out exactly as they will be here so publishing is a copy rather than a rewrite; that folder's README carries the release checklist. ⚠ The same applies to **`versions/<slug>.json`** — the manifest names the product and its store URL, and nothing reads it until a build ships, so it stages too. ⚠ **And the leak is not only files: a COMMIT MESSAGE naming an unreleased product is just as public, and so is a note in this file about which products are staged.** Keep both generic here; the named list lives in the staging folder's README, in the private repo. 🔑 **This repo cannot simply be made private**: Pages serves the site from it and the shipped HDAs fetch the manifests unauthenticated over `raw.githubusercontent.com`. Public is a requirement of the product, which is exactly why what goes in it has to be curated.

> **🔒 FAMILY-INTERNAL KNOWLEDGE DOES NOT LIVE IN THIS REPO (2026-07-24).** This repo is **PUBLIC** — required by GitHub Pages and the HDAs' raw-manifest update check. The shared internal files (`JVTOOLS_HOUDINI_LESSONS.md`, `JVTOOLS_PRODUCT_STANDARDS.md`, `JVTOOLS_WORKING_RULES.md`) live in the **PRIVATE `jvtools-internal` repo** (`C:\Users\Jovan\Documents\GitHub\jvtools-internal`), auto-loaded into every session by an `@`-import in `~/.claude/CLAUDE.md` (user scope - a project-level import of a path outside the working directory is gated behind a one-time dialog and silently disabled if it is declined). **Never add internal engineering knowledge, product-repo lore, or anything trade-secret-adjacent here** — public docs pages, `versions/*.json` manifests, and this hub file only. (The two shared files briefly lived here 2026-07-24; they were moved out and this repo's history was scrubbed.)

## What this repo is

A **Retype** static documentation site. Each product (HDA) is a folder under the repo root; the root `index.md` is the landing page with product cards. Adding a new product = add a folder + a nav link, touching nothing else.

- **Tool:** Retype **Pro** (one-time license — no subscription). Config: `retype.yml`.
- **Local preview:** `retype start` (live-reload dev server). **Build:** `retype build` → static site in `.retype/` (git-ignored).
- **Deploy target (since 2026-08-28):** the canonical home is **`https://jvtools.dev/docs/`** — the Retype Pro key is re-licensed to `jvtools.dev` and `retype.yml`'s `url:` matches it exactly (a key/`url:` mismatch FAILS the build outright). Push to `main` → `.github/workflows/retype-deploy.yml` builds and publishes to the `retype` branch → GitHub Pages serves it at `tonehammer.github.io/jvtools-docs/` AND `jvtools-website`'s postbuild step pulls the same branch into `jvtools.dev/docs`. ⛔ *The original 2026-07-08 plan block that stood here ("github.io for now, key registered to tonehammer.github.io, ⏳ still TODO: create the repo / add the key / enable Pages") was months stale — all long done, then superseded by the move.*

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

| Product | Docs folder | Code repo on disk |
| --- | --- | --- |
| Reallusion Importer for Houdini | `reallusion-importer/` | `C:\Users\Jovan\Documents\GitHub\Reallusion Importer for Houdini` |
| Advanced Velocity | `advanced-velocity/` | `C:\Users\Jovan\Documents\GitHub\Advanced Velocity` |
| RPLidar In | `rplidar-in/` | `C:\Users\Jovan\Documents\GitHub\RPLidar for Houdini` |
| COPout | `copout/` | `C:\Users\Jovan\Documents\GitHub\COPout` |
| Deoverlap Polylines | `deoverlap-polylines/` | `C:\Users\Jovan\Documents\GitHub\Deoverlap Polylines` |
| FLIP DOP Controller | `flip-dop-controller/` | `C:\Users\Jovan\Documents\GitHub\FLIP DOP Controller` |

Ground truth in every case is the HDA's per-parm **Help fields** (plus the embedded node help page, `houdini/help/<slug>.txt` where the repo carries one). *(Table expanded 2026-08-30 — it had listed 2 of 6 products since July.)*

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
- **Version on first page (rule, Jovan 2026-07-22):** show the current version **inline at the first mention of the product name** in the opening body paragraph, e.g. `Welcome! **Advanced Velocity** (v1.0) is a single Houdini SOP…`. **NOT in the H1** — the H1 also drives the sidebar label, so a version there clutters the nav. **Source of truth = the product's changelog page** — the top-most `## Version X.Y.Z` heading, now `reference/changelog.md` in every section. **Show the FULL version, patch digit included** (`1.2.3`, not `1.2`) — Jovan, 2026-08-26: everything a human reads carries the exact shipped version. ⚠ The `versions/<product>.json` **`latest`** field is a different thing: it is the in-app update check's NOTIFY gate and deliberately holds at the minor through a patch, so it will legitimately read `1.2` while the changelog says `1.2.3`. That is not drift. The manifest's optional **`shipped`** key carries the displayable version for consumers that need it (the website badge).
- **Exclude from build:** the `exclude:` list in retype.yml (CLAUDE.md is already excluded — keeps the hub in-repo but off the site).

## 🔧 VERIFYING VISUALLY — build it and LOOK, never reason from the CSS (2026-08-06)

**Standing rule for any change with a visual result** (a card, a cover image, an icon, a layout tweak, a callout): render the built page and look at it before saying it is done. This is cheap — under a minute end to end — and it is the step that catches the whole class of "correct in the abstract, wrong on screen".

⚠ **Scope (Jovan, 2026-08-07): "visual result" means pixels and layout, not prose.** A text-only rewrite of an existing page needs a `retype build` (catches broken links/syntax), not a screenshot. Screenshot when a change touches nav/section structure, images or image paths, icons, cards, callout/Steps syntax, or anything Retype lays out — those break silently; paragraphs don't.

Why it is a rule and not a nicety: swapping the Advanced Velocity card image looked like a one-line edit, and three candidate images in a row *reasoned* fine and *rendered* wrong (a square crop lost 12% top and bottom; the 16:9 with a title lockup grazed it against the panel border). Reading the CSS told me the box existed; only the render told me what it did to the picture.

**The loop:**
1. `retype build .` from the repo root (~3s, 36 pages). Works locally with no license key despite `poweredByRetype: false` being Pro-only.
2. Serve it — `retype start` for live reload, or the **jvtools-docs-editor** (`C:\Users\Jovan\Documents\GitHub\jvtools-docs-editor\server.py`, port **8123**, base path **`/jvtools-docs/`**, rebuilds on save). ⚠ Serve it under the same base path the editor uses; a bare `/` can 404. 🔑 **CORRECTED 2026-08-28: this is NOT because links are absolute — they are DOCUMENT-RELATIVE, both page links and assets** (`href="../../../resources/css/retype.css"`, `src="../../static/x.png"`). Measured off the built HTML. **Only `canonical`, `og:url` and the sitemap carry the absolute `url:` value.** That is what makes one build portable across hosts, and it is the whole reason the docs could move to jvtools.dev/docs while `tonehammer.github.io/jvtools-docs/` keeps serving the same artifact correctly for every shipped HDA's baked Docs button.
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
  🔴 **AND IT DOES NOT MERELY FAIL TO SUBSTITUTE — IT FAILS THE PRO BUILD, WITH
  AN ERROR THAT NAMES NOTHING.** Measured 2026-08-27: `` `JV-Thing-v{{ dp.version }}.hdalc` ``
  on one page took the CI build down with `ERROR: capacity ('-2') must be a
  non-negative value` and `1 page failed`, and the log does not say which page.
  🔑 **A LOCAL BUILD CANNOT REPRODUCE IT** — locally the same commit was 48
  pages, 0 errors, because the per-page link/template resolution that trips it
  is Pro-gated (the giveaway is that CI printed 10 warnings and the local run
  printed 1). ✅ **Diagnose it by grepping for what is NOVEL rather than
  bisecting by push:** `grep -rn "{{" --include=*.md` showed every attested use
  was plain prose in a README, and exactly one was inside backticks. That was
  it. Write the version out literally on any page that needs it in a filename.
  🔴 **CORRECTED 2026-08-28 — THE SAME `capacity` ERROR IS ALSO THE FLAKY BUILD,
  AND THE ENTRY ABOVE WILL SEND YOU HUNTING A CONTENT BUG THAT IS NOT THERE.**
  A commit adding three docs sections went red with **4** of these errors and
  `4 pages failed`. Two novel constructs were found by exactly the grep-for-novel
  method above and removed; the next build came back **worse — 6 errors** from a
  change that only deleted things. **Re-running that identical commit built 48
  pages with 0 errors.** So the count is non-deterministic and the whole detour
  was wasted. ✅ **RE-RUN THE BUILD FIRST — `gh run rerun <id>` — and only start
  reading your diff if it fails the SAME WAY TWICE.** 🔑 The tell that it is the
  race and not your content is the error count MOVING between runs of the same
  or near-identical tree; a real content bug fails identically every time. Note
  the 2026-08-27 case was diagnosed on a single red run, so it may itself have
  been the flake — the `{{ }}`-in-backticks rule stands on the templating
  behaviour, which is independently true, not on that one build.
  🔑 The `data:` versions are the DOCS versions (changelog is their source of
  truth). `versions/<slug>.json` is a separate signal for the HDAs' update
  check, and its `latest` deliberately lags on patches so nothing notifies — do
  not sync them blindly. ⚠ The DOCS versions always show the full `1.2.3`
  (Jovan, 2026-08-26); the manifest's optional `shipped` key carries that same
  number for anything reading the manifest to display.
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
  cover generator (`jvtools-internal/tools/covers/`) has a
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
- 🔴 **THE SITE MOVED TO `jvtools.dev/docs` ON 2026-08-28, AND `tonehammer.github.io/jvtools-docs/` MUST KEEP *PUBLISHING*.** All shipped products bake that URL into the Docs button callback and keep it until each product's next release (measured by reading every `.hdalc`). ⛔ **CORRECTED 2026-08-30 (business audit): "keeps serving" holds for the ARTIFACT only — since `url:` moved, Retype's JS renders "Website Configuration Error" over every github.io page in a real browser** (the raw HTML is complete, so every 200/content check passes; only a rendered load shows it). The baked Docs buttons therefore land on that error until each product's next release re-bakes `DOCS_URL` to `jvtools.dev/docs/<slug>/` (Jovan's call, 2026-08-30 — STANDARDS §8; board chore `utilities-website-button`). Verify docs liveness with a BROWSER load per host, never a fetch. Both are served from the same artifact: the docs repo publishes to the `retype` branch as always, and **jvtools-website pulls that branch into `dist/docs` in a `postbuild` step** (`scripts/fetch-docs.mjs`) so Cloudflare Pages serves the new home natively — no Worker, no proxy. It works because Retype writes page links **and assets document-relative**; only `canonical`/`og:url`/sitemap take `url:`, which is exactly what should point at the new home.
  🔴 **THE TRAP THAT TOOK THE DOCS DOWN: RETYPE WRITES A `CNAME` FILE FROM THE HOST IN `url:`.** Setting `url: https://jvtools.dev/docs/` put `CNAME=jvtools.dev` in the published branch, GitHub then **adopted jvtools.dev as this repo's Pages custom domain**, and Pages began 301ing `tonehammer.github.io/jvtools-docs/*` to `jvtools.dev/*` **with the `/docs` prefix dropped** — 404 on every page, i.e. every customer's Docs button, within one deploy. ✅ **The workflow now deletes that file between build and publish** (`rm -f "${{ steps.build.outputs.retype-output-path }}/CNAME"`, with the build step given `id: build`). ⚠ Two follow-on gotchas: the publish action **overwrites but does not delete**, so a CNAME already in the branch survives a fixed build; and the custom domain is a **repo SETTING**, not just a file — clear it with `gh api -X PUT repos/tonehammer/jvtools-docs/pages -f cname=` (which also drops the file). Verify with `gh api repos/tonehammer/jvtools-docs/pages -q .cname` reading `null`.
  🔴 **AND A KEY/`url:` MISMATCH FAILS THE BUILD OUTRIGHT — it does NOT silently drop Pro.** `ERROR: The specified key is not valid for the "url" config host: "..."`. So the key and `url:` must move together, and once the secret is swapped **there is no reverting `url:` alone** — the revert cannot build, which is how a bad deploy becomes fix-forward-only. Plan the order accordingly: swap the secret (triggers no build), then push the `url:` change.
- 🔴 **PUSHING THIS REPO PUBLISHES TO github.io ONLY. `jvtools.dev/docs` IS A BUILD-TIME SNAPSHOT AND DOES NOT MOVE UNTIL THE *WEBSITE* REBUILDS — SO EVERY DOCS PUSH IS TWO PUSHES, IN TWO REPOS.** `jvtools-website/scripts/fetch-docs.mjs` runs as `postbuild` and pulls a codeload tarball of this repo's `retype` branch into `dist/docs`. The chain is: push `master` -> the Retype action builds -> it commits to `retype` -> **github.io serves it immediately** -> *and only the next jvtools-website deploy carries it to jvtools.dev*. Nothing in either repo triggers the other.
  🔑 **THE SIGNATURE, AND WHY IT IS ALWAYS MISREAD AS A CACHE: the same page serves DIFFERENT content on the two origins while the docs deploy is green.** Measured twice — `Version 1.3` vs `Version 1.2` (2026-08-30, AV 1.3) and `card.png` vs `card.jpg` (2026-08-31, the FLIP DOP docs card). **Waiting does nothing**, hard-refreshing does nothing, and re-running the docs action does nothing, because the docs side was never wrong. ✅ **Diagnose it in one command before touching anything** — the two origins disagreeing IS the diagnosis:
  ```
  curl -s https://tonehammer.github.io/jvtools-docs/ | grep -o '<the thing you changed>'
  curl -s https://jvtools.dev/docs/            | grep -o '<the thing you changed>'
  ```
  ✅ **The fix is an empty commit to jvtools-website** — no site source changes, the postbuild does the work: `git commit --allow-empty -F msg.txt && git push`, message *"Redeploy to pull the latest docs snapshot"* plus what it is pulling (precedents `d9a6e4d`, `f4f6002`). Cloudflare Pages rebuilds in well under a minute; poll `jvtools.dev/docs` for the changed string rather than assuming.
  ⚠ **ORDER MATTERS: push docs, wait for the Retype action to finish and update the `retype` branch, THEN redeploy the website.** A website build that races the docs action pulls the *previous* snapshot and looks like the redeploy did not work.
  ⚠ **THIS IS NOT A RELEASE-ONLY STEP.** It was first written down as one (`JVTOOLS_RELEASE.md` Phase 2 step 4) and was promptly rediscovered on 2026-08-31 by a plain card-image swap that was nothing to do with a release. **Any push to this repo whose result is meant to be visible to a customer needs the website redeploy**, because `jvtools.dev` is the origin the shipped `DOCS_URL` points at from each product's next release onward.
- **Retype v4.6.0 build is flaky:** an internal concurrency race intermittently fails a build with no content problem — **just re-run it** (`gh run rerun <id> -R tonehammer/jvtools-docs`). 🔑 **Its real mechanism, caught in a 2026-08-28 stack trace: `Retype.App.IO.AbstractOutputTracker` mutates a plain `Dictionary` from the parallel `DeployFileJob` phase** (`InvalidOperationException: Operations that change non-concurrent collections must have exclusive access`). That is the same corruption that surfaces as the nonsense `capacity ('-2')` errors, so those two faces are ONE bug — see the templating entry above, and §11 of `JVTOOLS_HOUDINI_LESSONS.md` for the general law (**a failure count that MOVES between runs of the same tree is a race; re-run before reading your diff**). The GitHub **Pages** deploy can also stall "queued/errored" — cancel the stuck run + re-dispatch (`gh run cancel <id>`; `gh workflow run retype-deploy.yml --ref master`). Cards: `image="/product/static/x.png"` sets a banner, `footer="[t](url)"` adds a secondary link, the whole card links to its `(target)` — no multi-link support. `versions/*.json` is excluded from the build (read by HDAs' update checks via GitHub raw).
- ⛔ *The old "typical flow" line here ("in one session Claude edits the product code and the docs, pushes both") described the pre-split workflow and is dead* (WORKING_RULES §5/§6, 2026-08-25): a product session never pushes this repo. Docs move at a release (`JVTOOLS_RELEASE.md` Phase 2) or in a business-chat docs session; they sync FROM the parm Help fields.
