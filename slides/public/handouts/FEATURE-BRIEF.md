# Verify this memory handoff

Proposed classroom feature, not a claim of an existing Pensieve capability.

Build a diagnostic verifier for one memory handoff. Given an expected service,
recipient, pool, memory ID, and content fingerprint, compare those expectations
with evidence from the recipient's own authenticated read.

Return a time-bound verified result only when the context and content match.
Distinguish unavailable, mismatch, and unresolved outcomes. A timeout is not
proof of denied access. Do not expose content or reveal an inaccessible pool.

Keep login, account merging, permission grants, memory copying, and indexing
outside the verifier. Use synthetic Alice/Bob fixtures while learning.

Acceptance cases:
1. Matching authenticated recipient with membership reads the selected record.
2. A nonmember receives no content and no successful verification.
3. A wrong signed-in account never reports recipient verification.
4. Wrong service, memory ID, or content never reports verification.
5. A failed request is unresolved, not silently passed.

Ask Claude to inspect the read boundary, propose a small spec and tests, and
identify assumptions before editing. Retain the requirement, source revision,
actual response, review decision, repair, and remaining limitation.

Source context: ../sources/AWS-SOURCE-EXCERPTS.md, src/aws-team-store.ts:35,74.
The acceptance cases above are authored teaching requirements.
