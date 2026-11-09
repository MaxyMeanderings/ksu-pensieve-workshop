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
