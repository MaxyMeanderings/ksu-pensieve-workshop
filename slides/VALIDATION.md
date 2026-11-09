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
  artifact deployment, and SPA 404 fallback.
- Sixteen project-base HTTP checks passed locally, including marks, portraits,
  fonts, handouts, sources, PDF, and 404 fallback document.
- Separate local Git repository prepared; private coordination/planning documents
  are excluded from the publication set. Public source visibility approved.

## Published verification — 2026-11-09

- Deployment of presentation revision `2936754` succeeded:
  https://github.com/doctor-ew/ksu-pensieve-workshop/actions/runs/42681344546
- Live presentation: https://doctor-ew.github.io/ksu-pensieve-workshop/
- All 16 live HTTP checks returned 200: index, fallback document, six images,
  two fonts, three handouts, two source documents, and the PDF. Entry-page
  JavaScript/CSS references also returned 200.
- Downloaded live PDF confirmed as 32 pages, titled
  “Build with AI. Remember with evidence.”
- These are deployment and HTTP checks; interactive browser behavior remains
  untested as described above.

## Definition and example revision — 2026-11-09

- Expanded to 37 slides: DRY definition; one definition/example per SOLID
  letter; four ACID properties; Big O definition and illustrative N/K/D values;
  explicit R meaning; Convention over Configuration definition.
- Updated navigation starts and instructor timing, retaining the 90-minute target.
- Node 24.13.1 production build and PDF export passed. All 12 pages in the
  affected 17–28 range rendered and visually inspected; no clipping observed.
- Existing-versus-proposed examples are labeled. No new product tests or
  complexity benchmarks were run. Browser interaction limitation remains.
