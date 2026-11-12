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

## Builder-reviewed architecture revision — 2026-11-09

- Replaced slides 8 and 25; deck remains 37 slides. Architecture is explicitly
  code-defined, not a fresh audit of deployed AWS resources.
- Original builder supplied topology and corrections; diagram omits ingress,
  reconciliation, S3 snapshots and SES from its nodes for readability and states
  them in the caption/notes. Worker is shared, not a separate invitation Lambda.
- Slide 25 separates save, indexing and recall; notes explain receipt timing
  and the application publication marker. Four .mmd sources are downloadable.
- Local PDF export passed. Both changed slides rendered and inspected; topology
  labels enlarged after the first export. No clipping observed in final output.

## Trust and works-cited port — 2026-11-11

- Added 14 slides ported or adapted from the GSU archived deck; deck is now 51 slides.
  Slides 1–28 keep their numbers. Section rail has a new "Trust + works cited"
  section (starts 29), "Challenge + repair" starts 34, "Remember" starts 47.
- Added components/EvidenceCheck.vue and four handouts (claim ledger, source packet,
  evidence review, prompt examples). Take-home slide 51 links all of them.
- Passed: `npm ci`, production build with the `/ksu-pensieve-workshop/` base, and
  full PDF export with installed Google Chrome, on Node 26.13.0 (the project asks
  for 24.13.1). The existing FloatingVue/Popper export warning appeared again.
- Passed: slides 29–46, 50, and 51 exported as PNG and visually inspected for the
  ported layouts. Slides 29, 31, 32, 33, 36, 39, 40, 44, 50, and 51 were each viewed;
  the rest use the same layouts. Slide 33's list markers overlapped the box border,
  which was fixed in style.css and rechecked on slides 33 and 46's shared layout (33 viewed).
- Passed: all seven handouts and six source files are present in dist/.
- Passed: the eight Works cited URLs each returned HTTP 200 on 2026-11-11.
- Not done: PDF page count was not read back, slides 30, 34, 35, 38, 41–43, 45–49
  were not individually viewed after the port, and the interactive EvidenceCheck
  reveal button and section-rail clicks were not exercised in a browser.
- Not done: no timed rehearsal. The 51-slide deck does not fit in 90 minutes
  with every optional exercise; INSTRUCTOR.md marks the core path.

## Nightshift build-harness slides — 2026-11-11

- Added 6 slides adapted from the Nightshift talk deck: 29 The harness keeps the workflow,
  30 Six stages retain their evidence, 38 Challenge the author's assumptions, 43 We pointed
  it at itself, 44 Review keeps the failed attempt, 52 Human checkpoints. Deck is now 57
  slides. Slides 1–28 keep their numbers. Slide numbers in the section above predate this
  insertion; every slide from the old 29 onward moved down by 2 to 6.
- Section rail now starts "Trust + works cited" at 29, "Challenge + repair" at 36, and
  "Remember" at 53. The rail highlight was confirmed on slides 29, 30, 38, 43, 44, and 52.
- Added style.css rules for the stage grid and walkthrough screenshot, and copied
  public/assets/stage-review-actual.png from the Nightshift deck.
- Passed: production build with the `/ksu-pensieve-workshop/` base; full PDF export;
  PDF page count read back with pdf-lib: 57. The FloatingVue/Popper export warning
  appeared again.
- Passed: slides 29, 30, 38, 43, 44, and 52 exported as PNG and each viewed. No clipping
  or overlap observed. Slide 44's screenshot shows a local file path from the
  presenter's laptop.
- Passed: stage-review-actual.png and all seven handouts are present in dist/.
- Passed: Nightshift issue and pull request pages (138, 139, 140) and seven pinned files
  returned HTTP 200 on 2026-11-11.
- Not done: the other 51 slides were not re-viewed after renumbering, and the
  EvidenceCheck button and section-rail clicks were not exercised in a browser.
- Not done: no timed rehearsal. Core path is now 52 slides, about 78 minutes plus
  exercise and questions (see INSTRUCTOR.md); the deployed site still shows the old deck
  until this is pushed to main.
