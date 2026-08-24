# CaveViewer Preview agent guide

This repository is a public, static preview of the forthcoming CaveViewer
website. It has no server application, contact backend, persistent storage, or
database. Preserve that boundary and do not use this repository to alter the
production site.

## Read first

- [README.md](README.md) for the publishing boundary, release chooser, local
  review, and validation commands.
- [Development documentation](docs/development/README.md) for the canonical
  planning, test, and workflow references.
- [Work definition](docs/development/work-definition.md) before starting
  substantial or multi-step work.

## Code standards

- Keep the site static and its published artifact limited to the five public
  HTML routes plus `assets/` and `storage/`. Do not introduce a backend,
  database, analytics service, or unnecessary framework/build dependency.
- Follow the existing HTML, CSS, and JavaScript conventions. Prefer semantic
  landmarks, native controls, shared styles, progressive enhancement, and
  small focused changes over parallel patterns.
- Preserve accessibility as a product requirement: keyboard operation, visible
  focus and current-navigation cues, a usable skip link, logical heading
  structure, sufficient readable sizing, and content that remains available
  without JavaScript or with reduced motion.
- Make layouts resilient rather than viewport-specific. Check narrow screens,
  large text or 200% zoom, and short viewports; do not clip, overlap, or make
  essential content unreachable.
- Keep visual assets local. Retain responsive WebP delivery with appropriate
  fallbacks and intrinsic dimensions when changing images, and respect the
  documented page image budgets.
- Treat `assets/data/release.json` as the release chooser's source of truth.
  Regenerate it with `scripts/sync_release.py`; do not loosen its trusted
  repository, version, or package-name constraints.
- Preserve the Contact form's approved FormSubmit action, honeypot, and default
  CAPTCHA behavior. Never automate a real submission.

## Required review

Every agent must complete the following before handoff:

1. **Documentation review.** Update the root README for changes to local setup,
   publishing, release data, or repository boundaries. Update the development
   index when a canonical document, test, or workflow changes. Review
   user-facing copy, headings, links, alternatives for images, and assertions
   so they accurately describe a website preview rather than the desktop app.
2. **Code-standards review.** Check that changed HTML, CSS, JavaScript, assets,
   and workflows follow the rules above and introduce no unused files, broken
   local references, unsafe external dependency, or regression of the static
   deployment boundary.
3. **User-experience, usability, and QA review.** Exercise the changed journey
   with keyboard navigation and at desktop and mobile widths. Where relevant,
   verify zoom or large text, reduced motion, JavaScript-disabled content,
   responsive image behavior, download choices, and contact-page reachability.
   Add or update focused static or browser coverage for changed behavior.

## Validation

Run the proportionate checks from the repository root before handoff:

```bash
python3 -m pytest tests/unit/test_site.py -q
git diff --check
```

When the release manifest changes, run both:

```bash
python3 scripts/sync_release.py
python3 scripts/sync_release.py --check
```

For HTML, CSS, JavaScript, assets, navigation, or interaction changes, run the
browser suite against a local static server:

```bash
python3 -m http.server 4173 --bind 127.0.0.1
```

In another terminal:

```bash
cd tests/browser
npm ci
npx playwright install chromium
npm test
```

Report the commands run, the result, and any deliberate verification not
automated by the suite. Do not change unrelated user files or generated test
artifacts while completing a task.
