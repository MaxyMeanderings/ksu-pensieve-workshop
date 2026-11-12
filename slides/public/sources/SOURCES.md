# Works cited and evidence boundaries

Prepared 2026-11-09. Teaching proposals and synthetic scenarios are labeled in
the deck. References support specific claims, not blanket product correctness.

## Concepts

- OODA terminology, slide 6: https://csrc.nist.gov/glossary/term/ooda
- Claude Code guidance, slide 13: https://code.claude.com/docs/en/best-practices
  Teaching prompt is authored; it is not an execution transcript.
- DRY, slide 17: https://media.pragprog.com/titles/tpp20/dry.pdf
  Knowledge duplication is the concern; not every repeated text is the same rule.
- SOLID, slide 18: https://blog.cleancoder.com/uncle-bob/2020/10/18/Solid-Relevance.html
  Slide 18 shows the existing AWS vector interface; the recipient verifier remains proposed.
- ACID, slide 19: https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/transactions.html
  Database transaction guarantees do not create a distributed transaction over
  indexing, account setup, and the recipient's subsequent read.

## Implementation inspected

Pinned source revision: https://github.com/doctor-ew/pensieve/tree/c1b093bbb055e7de65f8c23125425aa506a8f068
See [captured excerpts](AWS-SOURCE-EXCERPTS.md) for original line numbers and hashes.

- Access boundary: src/aws-team-store.ts:35.
- Repository/vector interfaces: src/aws-team-store.ts:11,26; src/repositories.ts:1.
- Save staging and final publication: src/aws-team-store.ts:51–69.
- Exact selected read and provenance: src/aws-team-store.ts:74–76.
- Queued indexing and revision checks: src/aws-team-store.ts:99–114.
- Candidate retrieval and filtering: src/aws-team-store.ts:139.
- DynamoDB transaction adapter: src/aws-db.ts:23.
- Related test design: test/aws-storage.test.ts:24,27,28,49,52.

The deck makes no claim that these production tests were executed during slide
authoring. Source inspection is not verification of the deployed source revision.
The new recipient-verification receipt is a proposed feature, not an existing
production promise. components/HandoffCheck.vue is a synthetic local illustration.

## Big O scope

Slides 21–22 separate exact-record verification from semantic discovery. With
conventional constant-time Map/Set operations, the local candidate-validation
portion of src/aws-team-store.ts:139 scales with returned candidate count and
materialized record size. The hosted vector backend's search complexity, latency,
embedding latency, and I/O are not established by that loop. No benchmark is claimed.

The OpenClaw reviewer inspected the older railway-team-live SQLite path and
identified a full-scan cosine-ranking cost there. That is a separate implementation;
its N×D plus full-sort analysis is deliberately NOT presented as the AWS path.

## Historical case and visual reuse

- Historical incident: GSU Hack-Her-Thon/docs/PENSIEVE-SLIDE-HANDOFF.md:3.
  Wrong service, then separate recipient membership. The recorded repair is not
  proof that a second laptop was operated. Private account identifiers are omitted.
- GSU slides/slides.md:125: reusable teaching sequence, not historical transcript.
- GSU slides/ASSETS.md:6: code photograph provenance; portraits and fonts retained.
- KSU marks: supplied by Drew in this conversation; used unchanged.
- Presenter names and event context: confirmed by Drew; Tyler Sztuka and Drew Schillinger.

Slide footers use original source paths for traceability. The captured source
packet makes selected code available without a checkout; it is not a complete
copy of the Pensieve repository. No current hosting or access guarantee follows
from a source citation.

Pensieve product-purpose memory used for slide 3: pensive pool, memory
9fc071ede1c5428ae9191ffd4e1e35407813fe7bf27bd8750aea504ef8ba186a.
Historical design context, not current implementation proof.

## Original author review incorporated

Read-only source review completed 2026-11-09. Slides 17–23 now show concrete
authorization, injected vector dependency, conditional transaction, publication /
indexing failure gap, candidate bookkeeping, and test-discovery convention.
No new production tests or deployed-byte comparison were performed.
CoC here means Convention over Configuration: package.json:28.

## Definition expansion

Current deck: 37 slides. DRY definition on 17; individual SOLID definitions and
examples on 18–22; ACID definitions/example on 23–25; Big O and variables on
26–27; Convention over Configuration on 28. Earlier slide numbers above describe
the initial 32-slide edition.

- SOLID definitions: https://blog.cleancoder.com/uncle-bob/2020/10/18/Solid-Relevance.html
- Big O definition: https://xlinux.nist.gov/dads/HTML/bigOnotation.html
- N = pool memory count; K = returned candidate count; D = numbers per embedding;
  R = loaded memory rows. Numeric examples are illustrative, not benchmark data.
- Existing source supports the adapter/repository boundary and injection seam.
  The alternative adapter and query-only interface are explicitly proposed examples.

## Builder-reviewed architecture diagrams

Slides 8 and 25 describe code-defined topology at c1b093bbb055e7de65f8c23125425aa506a8f068,
not a fresh deployed-resource audit. Two configured Lambdas (API and worker);
the worker also handles invitation delivery. API recall embeds queries; worker
indexing embeds documents. Hourly reconciliation supplements stream processing.

- [Slide 8 Mermaid](AWS-TOPOLOGY.mmd): infra/aws-serverless/compute.tf:6,40,111;
  cloudfront.tf:42; src/aws-runtime.ts:22; src/cognito.ts:50;
  src/aws-team-store.ts:35; src/aws-vectors.ts:9,35; src/aws-share-store.ts:15.
- Slide 25 [save](SAVE-BOUNDARY.mmd), [index](INDEX-BOUNDARY.mmd),
  [recall](RECALL-BOUNDARY.mmd): src/aws-team-store.ts:51–71,101–113,139.
- Read the older proposed ARCHITECTURE.md and separate Invitation Lambda diagram
  as historical design, not current runtime evidence.

## Trust, works-cited, and repair-loop slides (added 2026-11-11)

Slides 31–36, 39, 42, 45–47, 49, 51, and 62 were ported from the GSU Hack-Her-Thon
archived deck. That file is no longer in the GSU working tree; it was last present at
commit 4e4e8ed2edcec7299fa403cccedeca65ba22487d as
slides/archive/deck-before-coach-walkthrough.md. Slide footers cite its line numbers
(for example "GSU archived deck:94"). Deck is now 63 slides; slide numbers 1–28 are unchanged.

| KSU slide | GSU archived deck line | Change |
| --- | --- | --- |
| 31 A green badge is a claim | 94 | Component ported; added "case 7" label |
| 32 A URL is a pointer | 261 | Ported unchanged |
| 33 Works cited: make each claim traceable | 277 | Ported unchanged |
| 34 Citation presence ≠ claim support | 293 | Ported unchanged |
| 35 Exercise · audit the claim | 310 | Ported unchanged |
| 36 Adversarial means skeptical | 327 | Ported unchanged |
| 39 Make the behavior observable | 360 | Quoted input rewritten for the verifier |
| 42 Repair the smallest thing | 446 | Ported unchanged |
| 45 Every response can violate more than one requirement | 378 | Ported unchanged; columns are the GSU coach's requirements |
| 46 A quote must belong to the case it cites | 412 | Ported unchanged |
| 47 Completed execution ≠ verified requirements | 429 | Ported unchanged |
| 49 Exercise · try to break it | 395 | Four inputs rewritten for the verifier |
| 51 Exercise · show one trace | 496 | Ported unchanged |
| 62 Works cited | 531 | New list built from this file's own references |

Real evidence behind slides 31, 32, 36, 45, 46, 47: the Nightshift retained run audit,
https://github.com/doctor-ew/nightshift-community/blob/0dcbcb9/docs/WORKSHOP-V2-AUDIT.md
(read 2026-11-11). It records an 8/8 grader result for a prompt-only coaching agent,
and its finding 1 is the unsourced competitor claims in case 7 (slide 31). Its finding 2 is a
reviewer citing case 8 evidence that the case 8 response does not contain (slide 46).
Slide 31's excerpt is an adapted teaching excerpt, not a verbatim transcript.

Synthetic material, not real data: handouts/SOURCE-PACKET.md (organizer counts and the
.test URL), the slide 39 and 49 inputs, and the slide 45 check marks. Handouts
CLAIM-LEDGER.md, SOURCE-PACKET.md, and EVIDENCE-REVIEW.md are copied from the GSU
slides/handouts/ directory. PROMPTS.md is adapted for the handoff verifier.

Works cited slide (62): the eight links were requested on 2026-11-11 and each returned
HTTP 200. That confirms the pages exist; the pages were not re-read for this slide.

## Nightshift build-harness slides (added 2026-11-11)

Slides 29, 30, 38, 43, 44, and 52 were adapted from the Nightshift talk deck, file
slides/shared-core.md in the local nightshift-community checkout (branch
nightshift/talks-memory-security). Footers say "adapted from Nightshift talk deck".
Nightshift is the presenter's own open-source harness, shown as one example.

| KSU slide | shared-core.md line | Cited files and links |
| --- | --- | --- |
| 29 The harness keeps the workflow | 5 | AGENTS.md; skills/nightshift/SKILL.md; routing.json; scripts/nightshift-pipeline.py |
| 30 Six stages retain their evidence | 47 | commands/nightshift-{product,adversarial,implement,review,drift,qa}.md |
| 38 Challenge the author's assumptions | 103 | routing.json; docs/133/IMPLEMENTATION.md |
| 43 We pointed it at itself | 219 | Issues 138 and 139; pull request 140 |
| 44 Review keeps the failed attempt | 478 | docs/138/REVIEW.md; docs/138/IMPLEMENTATION.md; screenshot |
| 52 Human checkpoints | 235 | AGENTS.md; commands/nightshift-implement.md |

Pinned links use commit 4f9f8e7 of https://github.com/doctor-ew/nightshift-community.
On 2026-11-11 the issue and pull request pages (138, 139, 140) and the pinned files
AGENTS.md, routing.json, commands/nightshift-adversarial.md,
commands/nightshift-implement.md, docs/133/IMPLEMENTATION.md, docs/138/REVIEW.md, and
docs/138/IMPLEMENTATION.md each returned HTTP 200. That confirms the pages exist; their
contents were not re-read for this deck. The other cited paths exist in the local checkout.

Slide 43 is a real, partially completed run (task 138): Review failed first, the repair
passed re-review, QA failed on a required human visual case, and the allowance was
exhausted before the controller's misrouted continuation could do substantive work.
The merge (pull request 140) followed an explicit operator instruction. Issue 139 records
the sequencing defect. The deck does not claim all six stages passed.
Slide 38 shows the routes recorded for one run (author Codex, reviewer Claude), not a
model ranking. Slide 44 uses public/assets/stage-review-actual.png, copied from the
Nightshift deck's public/assets/; it is an actual capture and shows a local file path
from the presenter's laptop.

## Nightshift 0.4.0 slides (added 2026-11-12)

Slides 53–58 cover Nightshift 0.4.0 (https://github.com/doctor-ew/nightshift-community,
tag v0.4.0). Slide 53 is adapted from docs/releases/0.4.0.md and docs/154/IMPLEMENTATION.md.
Slide 55 follows the option text in scripts/nightshift-factory.sh (--project, --provider,
--provider-policy, --model, --auth, --push). Slide 58 uses the plugin name nightshift
(.claude-plugin/plugin.json) and commands/nightshift-eng.md, with the session-local plugin
and namespaced-command behavior described at https://code.claude.com/docs/en/plugins/create.

Slides 54–57 are the presenter's own throwaway-repository run on 2026-11-12, with Claude Code
2.1.322, claude-only policy, subscription auth, and sonnet. The facts on them come from the
run's retained files: init output and git log (slide 54), the task state file and
proof-red.json (slide 56), and the implement-2 finding with id
IMPL-CLASSIFICATION-REVIEW-MISSING (slide 57). Those files are on the presenter laptop and not
published. The run did not complete; the cause of the missing review is not established.

On 2026-11-12 the five linked v0.4.0 pages and the Claude plugin documentation each returned
HTTP 200; their contents were not re-read in full. The shipped plugin.json at v0.4.0 declares
repository as an object, which Claude Code 2.1.322 rejects, and still reports version 0.3.0
while the VERSION file says 0.4.0. Slide 53's "default allowance is gone" refers to the
release notes' statement that new work has no default work, call or repair ceiling.
