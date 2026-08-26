# CaveViewer site preview

This repository is the public, static preview of the forthcoming CaveViewer
website. It is published separately from the production site at
<https://www.caveviewer.com/>, which this repository cannot change. It has no
server application, persistent storage, or database.

The preview is intentionally marked `noindex` while it is being reviewed. Its
Contact page keeps the approved FormSubmit action and honeypot; do not add
`_captcha=false`, which opts out of FormSubmit's default CAPTCHA. FormSubmit's
default CAPTCHA remains enabled. CaveViewer stores no contact data and runs no
contact backend or database.

## Publishing

GitHub Pages deploys only a prepared `_site/` artifact when `main` changes or
when the workflow is manually run from `main`. This path is an exported static
artifact: it contains the eight HTML pages plus `assets/` and `storage/`, not
the repository's tests, scripts, or Git metadata. The site has no custom
domain; its public URL is <https://caveviewer.github.io/caveviewer-preview/>.

This repository is the source of truth for the preview. Do not use it to
replace or alter the existing production Pages deployment.

## Contributing and checks

Contributors with write access can push changes directly to `main`, and those
changes can publish through the Pages workflow. Pull requests remain welcome,
but they are not required to publish the preview. The following checks continue
to run for pull requests and changes to `main`; they provide automated feedback
without blocking publication:

- `Static site contracts`
- `Browser site checks`

GitHub Actions use read-only default permissions. The repository allows only
the approved, full-SHA action revisions used by its workflows, and requires
full-SHA action pinning. Dependabot proposes bounded weekly updates for those
actions and the isolated browser-test dependency. When accepting an action
update, also add its reviewed full SHA to the repository's approved Actions
list before merging the Dependabot pull request.

The release chooser accepts only the official
`https://github.com/CaveViewer/CaveViewer` release repository, a three-part
numeric version, and the four expected version-matched package names. This
keeps the public preview from silently redirecting downloads to an unrelated
release source.

## Local review

From this repository's root:

```bash
python3 -m http.server 4173 --bind 127.0.0.1
```

Open <http://127.0.0.1:4173/>.

## Maintain the release chooser

`assets/data/release.json` is the maintained release source. After changing it,
run:

```bash
python3 scripts/sync_release.py
python3 scripts/sync_release.py --check
```

## Validate changes

With `pytest` available, run the static contracts from the repository root:

```bash
python3 -m pytest tests/unit/test_site.py -q
```

The browser checks live in `tests/browser/`. They reuse a local server or can
target the public site without submitting the Contact form:

```bash
cd tests/browser
npm ci
npx playwright install chromium
npm test
```

## Image delivery budget

Modern browsers select preferred WebP images through `picture`/`srcset` or CSS
`image-set`, while original PNG and JPEG assets remain fallbacks. The markup
supplies intrinsic dimensions to reserve layout space before images load.

| Route | Preferred modern candidates | Budget |
| --- | --- | ---: |
| Home | `ginnie1.webp`, `software-hero-cave-strokes-full.webp` | 1.30 MB |
| Why CaveViewer | Rendering, Map Library, Capture, and Streaming WebP images | 0.45 MB |
| Documentation | Import and Streaming preference WebP images | 0.12 MB |
| Team | Six responsive portrait WebP images | 0.80 MB |
| Sponsors | KISS Rebreathers and XDEEP logo WebP images | 0.05 MB |
| Projects | No local image assets; two privacy-enhanced YouTube embeds | — |
