# Instructor guide

Presenters: Drew Schillinger and Tyler Sztuka. Audience: KSU CS students.
Target duration: approximately 90 minutes. Speaker allocation remains open.

## Proposed timing

| Slides | Minutes | Purpose |
| --- | --- | --- |
| 1–4 | 0–8 | Introductions and one concrete user problem |
| 5–9 | 8–18 | Historical failure, OODA, and trust boundaries |
| 10–14 | 18–30 | Behavior contract and acceptance scenarios |
| 15–16 | 30–48 | One implementation slice; return to contract |
| 17–23 | 48–63 | DRY/SOLID/ACID/Big O/CoC in actual source |
| 24–28 | 63–78 | Challenge, staged defect, repair, audience discussion |
| 29–30 | 78–83 | Retain decision, evidence, and limits |
| 31–32 | 83–90 | Questions and take-home artifacts |

For linear presentation, cover 15–23 in order within the combined 33-minute
implementation/design window. Avoid repeatedly jumping forward and backward.

## Demonstration

Slide 25 is a local Vue fixture. It has four scenarios and a toggle between an
intentionally incomplete save-only claim and the repaired expected contract.
It does not contact Pensieve, authenticate users, alter membership, or establish
production correctness. Its source is components/HandoffCheck.vue:1.
Slide 26 provides the static explanation for the exported PDF.

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
