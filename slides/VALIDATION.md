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

## Nightshift 0.4.0 slides — 2026-11-12

- Added slides 53 (what 0.4.0 changes), 54 (run from the terminal) and 55 (run inside
  Claude Code). Deck is now 60 slides. Slides 1–52 keep their numbers; the old 53–57 are
  now 56–60. Section rail "Remember" now starts at 56.
- Passed: production build; slides 53–56 exported as PNG and viewed. No clipping or overlap.
- Passed: option names on slide 54 match scripts/nightshift-factory.sh in the release
  checkout; the five linked v0.4.0 pages and the plugin documentation returned HTTP 200.
- Not done: the commands were not executed. Slide 55 relies on the presenter's report that
  the namespaced command works; the shipped plugin.json still reports 0.3.0.
- Passed: full PDF export; page count read back with pdf-lib: 60.
- Not done: no timed rehearsal.

## Nightshift 0.4.0 command test — 2026-11-12

Throwaway repository and an isolated NIGHTSHIFT_HOME, both in the session scratchpad. No
remote, no push. Claude Code 2.1.322, claude-only policy, subscription auth, sonnet.

- Passed: `nightshift-factory.sh --help` lists every option used on slide 54.
- Found: in a new project the slide 54 command stops with MANIFEST_MISSING until
  `nightshift-factory.sh init claude "$PWD"` is run once. Init succeeded (mex graph
  indexing was reported unavailable, which did not block it). Slide 54 now shows the init step.
- Partly passed: with the project initialized, the command ran Product and Adversarial to
  a pass on sonnet and the claude provider, with paid API mode disabled. Implementation then
  failed twice and the run stopped blocked (exit 1); nothing was merged. The worker reported
  that the proof seal was blocked with classification_unreviewed, because the passed
  Adversarial receipt has no classification-review evidence. The Adversarial log also showed
  `child setpgid ... Operation not permitted`, so the test sandbox may have contributed.
  Cause not established. A completed end-to-end run was NOT demonstrated.
- Failed: slide 55. `claude plugin validate` reports `repository: Invalid input: expected
  string, received object` for .claude-plugin/plugin.json at v0.4.0, and Claude Code
  2.1.322 reports "Failed to load plugin", so `/nightshift:nightshift-eng` is not
  registered and `-p "/nightshift:nightshift-help"` was not available. In a scratch copy with
  `repository` set to the URL string, validation passed and 23 `nightshift:` commands
  registered, including `nightshift:nightshift-eng`. The plugin command itself was not run.
- Not changed: the Nightshift release checkout was not modified.

## Nightshift walkthrough and corrections — 2026-11-12

- Replaced slides 54–55 with a four-step walkthrough (54 prepare, 55 run, 56 watch the
  stages, 57 read the result) and a corrected optional slide 58 (inside Claude Code). Deck
  is now 63 slides; slides 1–53 keep their numbers, the old 56–60 are now 59–63, and the
  "Remember" rail section starts at 59.
- The walkthrough facts come from the throwaway run's retained files: product and
  adversarial passed (3m 27s, 2m 11s), the spec and failing tests were sealed in commits, 17
  assertions failed and none passed in RED, and implementation failed twice (1m 35s, 44s).
  Nothing was merged or pushed. Slide 57 says the cause was not established.
- Fixed in the Nightshift release worktree, uncommitted: .claude-plugin/plugin.json
  `repository` is now a URL string. `claude plugin validate` passes, `nightshift:nightshift-eng`
  registers from that path, and `/nightshift:nightshift-help` ran and returned the command
  map. The full `/nightshift:nightshift-eng` pipeline was not run. The v0.4.0 tag still has
  the old manifest until the change is committed and released.
- Passed: production build; full PDF export, 63 pages read back with pdf-lib; slides 54–58
  exported as PNG and each viewed, no clipping.
- Not done: no completed end-to-end Nightshift run and no timed rehearsal. The section above
  titled "command test" uses slide numbers from before this change.
