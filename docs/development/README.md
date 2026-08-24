# Development documentation

- [Site overview and local review](../../README.md): the preview's static-site
  boundary, local server, Pages publication, release chooser, and validation
  commands.
- [Work definition](work-definition.md): the template and maintenance rules for
  planning independently verifiable repository work.
- [Agent guide](../../AGENTS.md): required documentation review, site standards,
  and usability-focused quality assurance for automated contributors.
- [Static site contracts](../../tests/unit/test_site.py): route, publication,
  release-manifest, accessibility, and image-delivery invariants.
- [Browser site checks](../../tests/browser/specs/website-preview.spec.mjs):
  keyboard, responsive, zoom, reduced-motion, no-JavaScript, and visual-flow
  checks.
- [Continuous integration](../../.github/workflows/site-checks.yml): static and
  browser checks run for pull requests and `main` without blocking publication.
- [Pages publication](../../.github/workflows/pages.yml): the exported static
  artifact and deployment workflow.

The focused documents and executable contracts linked here are canonical for
their subjects. The root project README keeps operational details that are most
useful when reviewing or maintaining the preview locally.
