# Build with AI. Remember with evidence.

Kennesaw State University Claude event; approximately 90 minutes.
Presenters: Drew Schillinger and Tyler Sztuka.

The 32-slide deck follows a proposed recipient-verified memory handoff feature
through OODA, specification, implementation boundaries, adversarial review,
repair, and retained evidence. It includes speaker notes and a synthetic local
interactive fixture. The fixture is not a live Pensieve client.

## Present

Use Node 24.13.1. Install with `npm ci`, then run `npm run dev`.
Scripts are defined in package.json:6. Open the printed local URL; presenter
mode is available through Slidev's presentation controls.

Build with `npm run build`; export with `npm run export`.
Output: dist/ and ksu-pensieve.pdf (package.json:7).
If Chromium is unavailable, pass the installed Chrome executable through the
Slidev export executable-path option. See https://sli.dev/guide/exporting.

GitHub Pages deployment is configured in ../.github/workflows/pages.yml.
Public repository: https://github.com/doctor-ew/ksu-pensieve-workshop
Presentation: https://doctor-ew.github.io/ksu-pensieve-workshop/
For a project site, build with `npm run build -- --base /ksu-pensieve-workshop/`.
The instructor guide stays outside public/. Handouts and source excerpts are
bundled in public/ so their links work in the static build.

## Scope

- GSU code-photo background, font, portraits, and layout foundations reused.
- KSU marks supplied by Drew; no GSU logo or Hack-Her-Thon branding in the deck.
- The Claude logo is retained for the Claude event.
- No old API-credit promise, event date, or presenter split has been assumed.
- Definitions and inspected implementation have source footers; SOURCES.md
  distinguishes AWS source from the older Railway review.

See INSTRUCTOR.md for the proposed timing and rehearsal needs, ASSETS.md for
asset provenance, and VALIDATION.md for checks actually run.
