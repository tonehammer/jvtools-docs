# store-covers

Gumroad cover and thumbnail art, parked here **only so the Gumroad API can
fetch it** — `POST /v2/products/:id/covers` takes a public URL and refuses a
file upload, and `raw.githubusercontent.com` serves anything in a public repo
whether or not the site build includes it.

🔴 **This folder is in `retype.yml`'s `exclude:` list and must stay there.**
Store covers are marketing artefacts that argue why you want the product; the
documentation reader has already got it. `JVTOOLS_MARKETING_IMAGERY.md` forbids
publishing them onto the docs site, and the docs card / social image are a
different picture by design (a plain product lockup, no title, no accent).

Same trick as `versions/*.json`: excluded from the build, still fetchable raw.
