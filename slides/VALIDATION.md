# KSU deck validation — 2026-11-09

## Passed

- Slidev 52.19.1 static build with notes excluded, under Node 24.13.1.
- PDF export with installed Google Chrome: ksu-pensieve.pdf, 32 pages.
- All 32 PDF pages rendered with Poppler and visually inspected in four contact
  sheets. No visible text clipping, content collisions, or missing images observed.
- Both user-supplied KSU marks render; the Owls wordmark is on the cover and the
  interlocking KSU mark appears in the section rail. Supplied white image backgrounds
  are retained because the source images were not edited.
- Tyler Sztuka and Drew Schillinger appear with the original GSU portraits.
- Code photograph, portraits, and Claude logo are byte-identical to GSU assets.
  No GSU university logo was copied.
- Ten referenced local assets/handout/source links exist and returned HTTP 200
  from the local Slidev server.
- Source contains 32 slide headings, each with a source footer and speaker notes.
- Synthetic demo is clearly labeled; slide 26 supplies a static PDF explanation.

## Limitations and warnings

- Browser plugin failed to start its required app-server executable. Interactive
  dropdown, toggle, navigation, keyboard behavior, and DOM overflow checks were
  not exercised through a browser. Rendering does not substitute for those checks.
- Export logged a caught FloatingVue/twoslash setup warning concerning Popper.
  Export completed; all pages rendered. This matches the warning retained in
  the GSU deck's slides/VALIDATION.md:14.
- Initial dependency install used Node 25.9.0 and reported an engine warning
  for postcss-nested. Build, export, and preview use Node 24.13.1, a supported
  version for that dependency. npm also reported an unrelated user-config warning.
- No new Pensieve application tests, authenticated recipient verification,
  cross-laptop test, or live Claude build was executed for this presentation.
- No public deployment or push performed. The local preview is not
  an audience-accessible hosting URL.
- Presenter split, timed rehearsal, and any live coding/student setup remain open.

## Outputs

- Source: slides.md; section rail: global-top.vue.
- Local fixture: components/HandoffCheck.vue.
- Static site: dist/ (speaker notes excluded).
- PDF: ksu-pensieve.pdf.
- Local authoring preview: http://localhost:3031/ while the server remains running.

## Pages preparation and author review

- Original Pensieve author review completed; code examples incorporated on slides
  17–23 with pinned revision citations. CoC is Convention over Configuration.
- Static build passed with `/ksu-pensieve-workshop/` base and speaker notes excluded.
- PublicLink.vue builds handout/source links using Vite BASE_URL.
- Revised 32-page PDF exported; pages 17–23 rendered and visually checked again.
  No clipping or collisions observed. Existing export warning remains.
- GitHub Pages workflow prepared with repository-derived base path, PDF export,
  artifact deployment, and SPA 404 fallback. Not yet run on GitHub.
- Sixteen project-base HTTP checks passed locally, including marks, portraits,
  fonts, handouts, sources, PDF, and 404 fallback document.
- Separate local Git repository prepared; private coordination/planning documents
  are excluded from the publication set. Source visibility decision is pending.
