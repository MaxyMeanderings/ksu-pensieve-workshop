# Instructor guide

Presenters: Drew Schillinger and Tyler Sztuka. Audience: KSU CS students.
Target duration: approximately 90 minutes. Speaker allocation remains open.

## API-credit setup (slides 3–6)

Slides 3–6 are the API-credit onboarding from the GSU HackHers deck: claim the credits
by QR, the claim form, the Console balance, and `/login` with the Console account.
Run them first, about 5 minutes, before any hands-on work. The QR opens
https://platform.claude.com/offers/108423d8-32e1-498a-a482-d9d4ead9d28a. The claim
form screenshot on slide 4 is from an earlier offer page and shows that event's header.
Slide numbers in the table below predate this insert: add 4 to every number from 3 on.

## Proposed timing

The deck is 63 slides: the original 37, 14 trust, works-cited, and repair-loop
slides ported from the GSU archived deck, 6 build-harness slides adapted from the
Nightshift talk deck, and 6 slides on Nightshift 0.4.0 (what changes, a four-step walkthrough, and an optional plugin slide). Presenting all 63 does not fit in 90 minutes with the
exercises. Timing below is a proposal and has not been rehearsed.

| Slides | Purpose | Core or optional |
| --- | --- | --- |
| 1–4 | Introductions and one concrete user problem | Core |
| 5–9 | Historical failure, OODA, and trust boundaries | Core |
| 10–14 | Behavior contract and acceptance scenarios | Core |
| 15–16 | One implementation slice; return to contract | Core |
| 17–28 | DRY/SOLID/ACID/Big O/CoC in actual source | Core |
| 29–30 | Nightshift: the harness and its six stages | Core |
| 31–34 | Green badge is a claim; URL is a pointer; works cited; citation is not support | Core |
| 35 | Exercise: audit the claim (8 min) | Optional |
| 36–37 | Adversarial means skeptical; give the challenger the evidence | Core |
| 38 | Nightshift: challenge the author's assumptions | Optional |
| 39–42 | Observable behavior, staged defect fixture, repair loop | Core |
| 43 | Nightshift: we pointed it at itself (about 1 min) | Core |
| 44 | Nightshift: review keeps the failed attempt (screenshot) | Optional |
| 45–48 | False-pass lessons and the evidence trace | Core |
| 49 | Exercise: try to break it (12 min) | Optional |
| 50 | Your turn: reject one unsupported claim (2–3 min pair exercise) | Core |
| 51 | Exercise: show one trace (8 min) | Optional |
| 52 | Nightshift: human checkpoints | Core |
| 53 | Nightshift 0.4.0: what changes | Optional |
| 54–57 | Nightshift walkthrough: prepare, run, watch the stages, read the result | Optional |
| 58 | Nightshift inside Claude Code (needs the manifest fix) | Optional |
| 59–61 | Retain decision, next session, closing | Core |
| 62–63 | Works cited and take-home kit | Core (show briefly) |

Core is 52 slides (slides 53–58 are optional). At roughly 1.5 minutes per slide that is about 78 minutes. Add the
slide 50 pair exercise and seven minutes of questions and the total is about 88 minutes
with no slack. If a rehearsal runs long, cut the six Nightshift slides first (29, 30, 38,
43, 44, 52); the trust and repair arc stands without them. Add an optional exercise only
if the earlier sections run short; hand out the others with handouts/SOURCE-PACKET.md,
handouts/EVIDENCE-REVIEW.md, and handouts/CLAIM-LEDGER.md.

For linear presentation, cover 15–28 in order. Avoid repeatedly jumping forward and backward.

## Ported trust and works-cited slides

Slides 31–36, 39, 42, 45–47, 49, 51, and 62 come from the GSU archived deck (see
sources/SOURCES.md for the commit and line numbers). Slides 31–36, 42, 46, 47, 51, and 62
are close ports. Slides 39 and 49 were rewritten around the handoff verifier. Slide 45
keeps the original table because it shows a real audit finding; its columns are the
GSU coaching prompt's four requirements, not the verifier's. The reviewer error on slide 46
and the 8 / 8 result on slide 31 are real findings from the Nightshift retained audit.

## Nightshift build-harness slides

Slides 29, 30, 38, 43, 44, and 52 are adapted from the Nightshift talk deck
(nightshift-community, slides/shared-core.md). Nightshift is the author's own
open-source harness, shown as one example of the pattern. Slide 43 is a real, partially
completed run: it stopped at its work allowance and was merged after explicit operator
approval. Do not say all six stages passed or that it completed automatically. Slide 38
shows the routes recorded for one run, not a model ranking. Slide 44 is a screenshot of
the real Review panel and shows a local file path from the author's laptop.

Slides 53–58 cover Nightshift 0.4.0 (release notes at tag v0.4.0). Slides 54–57 walk
through one real run on a throwaway repository on 2026-11-12: prepare (init plus a brief),
run, watch the stages, read the result. That run did not complete: Product and Adversarial
passed, the controller sealed the spec and recorded the new tests failing, and
Implementation stopped because the independent classification review was not recorded. Say
so. The slides present it as the harness refusing to forge a missing check, and they state
that the cause is not established. Do not run the commands live unless rehearsed; $NS is a
placeholder for a Nightshift checkout. Slide 58 needs the plugin manifest fix (repository
as a string), which is uncommitted in the release worktree; skip the slide unless it is
released.

## Demonstration

Slide 40 is a local Vue fixture. It has four scenarios and a toggle between an
intentionally incomplete save-only claim and the repaired expected contract.
It does not contact Pensieve, authenticate users, alter membership, or establish
production correctness. Its source is components/HandoffCheck.vue:1.
Slide 41 provides the static explanation for the exported PDF.

An actual Claude Code build is optional and needs rehearsal in a separate demo
directory. Use public/handouts/FEATURE-BRIEF.md as input. Show the spec, a narrow
implementation against a synthetic authenticated-reader fixture, a failing case,
and the same case after repair. Do not edit deployed Pensieve during class.
If a live build is not ready, present the local fixture and inspected source;
label this as a walkthrough, not a recorded successful product build.

## Teaching emphasis

- Return to Observe → Orient → Decide → Act after each failure.
- Exact-ID verification and semantic discoverability are different questions.
- Do not collapse writer success into intended-recipient access.
- DRY is about knowledge; SOLID should change a concrete design decision.
- Explain the AWS transaction boundary, not the older SQLite implementation.
- Do not invent vector-service complexity, latency, or durability measurements.
- Never expose real tokens, account IDs, or private memory content on screen.

## Rehearsal still needed

- Confirm presenter split, preferred bios, and any live Claude build.
- Decide whether the audience discussion becomes hands-on work; the deck does
  not assume student API credits, paid accounts, or local tooling.
- Rehearse projector readability and a timed run with both presenters.
- Public deployment and student distribution are separate from local export.

Give each SOLID letter about two minutes: definition, Pensieve example, audience question.
The S boundary is existing code; O extension and I query-only refinement are proposed;
L illustrates a behavioral contract; D shows the existing injection seam.

Architecture walkthrough: allow about two minutes on slide 8 and three on
slide 25 within existing section timing. Ask which boundary to inspect if save
succeeds but recall fails. Distinguish code-defined topology from live audit.
