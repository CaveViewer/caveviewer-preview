# CaveViewer site preview

This repository is the public, static preview of the forthcoming CaveViewer
website. It is published separately from the production site at
<https://www.caveviewer.com/>, which this repository cannot change.

The preview is intentionally marked `noindex` while it is being reviewed. Its
Contact page keeps the approved FormSubmit action and honeypot; do not add
`_captcha=false`, which opts out of FormSubmit's default CAPTCHA.

## Publishing

GitHub Pages deploys this repository's root directory only when `main` changes
or when the workflow is manually run from `main`. It has no custom domain; the
expected public URL is <https://caveviewer.github.io/caveviewer-preview/>.

The source of truth remains `website-preview/` in
[`CaveViewer/CaveViewer`](https://github.com/CaveViewer/CaveViewer). Treat this
repository as a deliberate public snapshot: update the source repository,
review it, then export a new snapshot here. Do not use this repository to
replace or alter the existing production Pages deployment.

## Local review

From this repository's root:

```bash
python3 -m http.server 4173 --bind 127.0.0.1
```

Open <http://127.0.0.1:4173/>.
