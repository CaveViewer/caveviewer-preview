# CaveViewer Docs update

These files are based on `CaveViewer/caveviewer-preview` main at commit
`d71e7982dd6db95866cf58192762aa8f5ef4eec5`.

Copy the contents of this package over the repository root, preserving paths.
Then review and validate:

```bash
git diff --check
python3 -m pytest tests/unit/test_site.py -q
python3 -m http.server 4173 --bind 127.0.0.1
```

For browser validation, use a second terminal:

```bash
cd tests/browser
npm ci
npx playwright install chromium
npm test
```

The package adds the three-section Docs page and responsive preference images,
adds the Docs dropdown to every primary menu, updates the responsive header
breakpoint, adds Magic Mr_V's responsive Team portrait, includes the Docs route
in the GitHub Pages artifact, and updates unit and browser contracts.
