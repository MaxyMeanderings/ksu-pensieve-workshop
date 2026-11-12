# Workshop prompt examples
These are example instructions for students, not guarantees of model compliance.
Adapted for the KSU handoff-verifier feature from the GSU workshop prompt handout.

## Spec-first request
Read the feature brief. Restate the acceptance cases and exclusions. Identify ambiguities.
Propose tests. Wait for my review before implementation.

## Builder
Implement only the approved verifier spec, against a synthetic authenticated-reader fixture.
Do not fabricate sources, test results, or account access. Save the artifact so I can inspect it.

## Adversarial reviewer
Use the spec and actual responses. For each requirement, identify a failure or uncertainty,
quote the case, and explain why it matters. Do not rewrite the answer and call it passed.
Inspect all applicable requirements, not only the criterion assigned to that case.

## Works-cited audit
For each claim, identify its source and quote the supporting line. Mark unsupported claims
as unknown or contradicted. Preserve synthetic labels and denominators. Do not invent links.

## Human decision
I approve / reject / leave unresolved this version because [evidence].
Remaining limitation: [what this test has not established].
