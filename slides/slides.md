---
theme: default
title: Build with AI. Remember with evidence.
info: Kennesaw State University — shared memory and building Pensieve with Claude.
colorSchema: dark
aspectRatio: 16/9
canvasWidth: 1280
fonts:
  sans: Source Code Pro
  serif: Source Code Pro
  mono: Source Code Pro
  local: Source Code Pro
drawings:
  persist: false
transition: none
mdc: true
---

<div class="slide-number">KENNESAW STATE UNIVERSITY · 01</div>

# Build with AI.<br>Remember with evidence.

<div class="cover-mark"><img src="/assets/claude-logo.svg" alt="Claude" /></div><p class="hero-sub">Building shared memory with Pensieve.</p><p class="tagline">One feature. A visible OODA loop.<br>Engineering judgment you can defend.</p><p class="event-line">Kennesaw State University · Computer Science</p><img class="ksu-cover" src="/assets/ksu-owls.png" alt="Kennesaw State Owls" />

<div class="source">KSU Claude event · Drew Schillinger + Tyler Sztuka · <PublicLink path="sources/SOURCES.md">Sources</PublicLink></div>

<!--
Opening: ask who has had to explain the same project to a new AI session. Promise one complete engineering trace, not a full product build. No event date or API-credit promise has been assumed.
-->

---
class: content
---

<div class="slide-number">KENNESAW STATE UNIVERSITY · 02</div>

# Your guides

<div class="presenters"><div class="presenter"><img src="/assets/tyler.jpeg" alt="Tyler Sztuka" /><div><h3>Tyler Sztuka</h3><p class="role">Claude Community Ambassador<br>Atlanta</p><p>Building practical experiences with Claude.</p></div></div><div class="presenter"><img src="/assets/drew.jpg" alt="Drew Schillinger" /><div><h3>Drew Schillinger</h3><p class="role">Enterprise Architect<br>@doctorew</p><p>Connecting specifications, agentic workflows, and human judgment.</p></div></div></div>

<div class="source">Presenter confirmation: TALK-BRIEF.md · portrait provenance: ASSETS.md · <PublicLink path="sources/SOURCES.md">Sources</PublicLink></div>

<!--
Tyler confirmed by Drew. Roles adapted from GSU presenter material and this event brief. Confirm preferred bios and presenter split during rehearsal.
-->

---
class: content
---

<div class="slide-number">KENNESAW STATE UNIVERSITY · 03</div>

# What should survive<br>the next session?

<div class="three"><section><h3>The decision</h3><p>What did we choose—and why?</p></section><section><h3>The evidence</h3><p>What observation supports it?</p></section><section><h3>The limit</h3><p>What is still unknown?</p></section></div><p class="takeaway">A useful memory helps the next person reason.</p>

<div class="source">Authored framing · Pensieve purpose: source map · <PublicLink path="sources/SOURCES.md">Sources</PublicLink></div>

<!--
Invite one example from a group project. Distinguish a decision record from a raw chat transcript; never imply automatic access to all prior conversations.
-->

---
class: content
---

<div class="slide-number">KENNESAW STATE UNIVERSITY · 04</div>

# One feature.<br>The whole engineering loop.

<div class="build-strip">Requirement → implementation → challenge → repair → retained memory</div><div class="three"><section><h3>Build</h3><p>A recipient-verified handoff receipt.</p></section><section><h3>Inspect</h3><p>The code, assumptions, and boundaries.</p></section><section><h3>Explain</h3><p>Why the evidence supports the result.</p></section></div>

<div class="source">Authored teaching plan · agreed structure: TALK-BRIEF.md · <PublicLink path="sources/SOURCES.md">Sources</PublicLink></div>

<!--
90-minute plan: problem 8m, OODA/context 10m, contract 12m, implementation 18m, engineering lenses 15m, challenge 15m, memory 5m, Q&A 7m. Timing stays in notes, not as a rigid student-facing promise.
-->

---
class: content
---

<div class="slide-number">KENNESAW STATE UNIVERSITY · 05</div>

# “Saved” was true.<br>The handoff still failed.

<div class="three"><section><h3>First mismatch</h3><p>Writes reached an obsolete service.</p></section><section><h3>Second mismatch</h3><p>The signed-in recipient lacked pool access.</p></section><section><h3>Better check</h3><p>Read as the intended recipient on the intended service.</p></section></div>

<div class="source">Historical record: GSU docs/PENSIEVE-SLIDE-HANDOFF.md:3 · <PublicLink path="sources/SOURCES.md">Sources</PublicLink></div>

<!--
Actual historical incident, paraphrased. Do not display account identifiers, credentials, or copied private payloads. The record is not proof of a cross-laptop test. The new verifier is a proposed teaching feature.
-->

---
class: content
---

<div class="slide-number">KENNESAW STATE UNIVERSITY · 06</div>

# Observe. Orient.<br>Decide. Act.

<div class="ooda"><div><b>Observe</b><span>What happened?</span></div><div><b>Orient</b><span>What explains it?</span></div><div><b>Decide</b><span>What will we change?</span></div><div><b>Act</b><span>Run it. Inspect it.</span></div></div><p class="takeaway">Then observe again. A loop, not a ceremonial checklist.</p>

<div class="source"><a href="https://csrc.nist.gov/glossary/term/ooda">NIST: OODA</a> · software application is our teaching framework · <PublicLink path="sources/SOURCES.md">Sources</PublicLink></div>

<!--
Introduce OODA terms and keep returning to this loop. The software examples are an authored application, not a claim that Boyd prescribed these development steps.
-->

---
class: content
---

<div class="slide-number">KENNESAW STATE UNIVERSITY · 07</div>

# Observe the user’s result.

<div class="two"><section><h3>Weak evidence</h3><p>The save call returned successfully.</p></section><section><h3>Relevant evidence</h3><p>The intended recipient retrieved the expected record.</p></section></div><p class="takeaway">Whose identity? Which service? Which pool?</p>

<div class="source">Historical case: GSU docs/PENSIEVE-SLIDE-HANDOFF.md:3 · proposed verification contract · <PublicLink path="sources/SOURCES.md">Sources</PublicLink></div>

<!--
Ask the audience which observation they would collect first. A server receipt can establish persistence without establishing usability or authorized access.
-->

---
class: content
---

<div class="slide-number">KENNESAW STATE UNIVERSITY · 08</div>

# Orient before you repair.

<div class="flow"><span>Claude / client</span><i>→</i><span>Service</span><i>→</i><span>Identity + pool</span><i>→</i><span>Memory</span></div><div class="two"><section><h3>Competing explanations</h3><p>Wrong destination? Wrong account? Missing membership?</p></section><section><h3>Discriminating evidence</h3><p>Check the same record under the actual recipient’s session.</p></section></div>

<div class="source">AWS src/aws-team-store.ts:35,74 · source packet · <PublicLink path="sources/SOURCES.md">Sources</PublicLink></div>

<!--
Use the diagram as a simplified logical map, not an exhaustive deployment diagram. Explain that a pool name alone is insufficient and an identity is not a display name.
-->

---
class: content
---

<div class="slide-number">KENNESAW STATE UNIVERSITY · 09</div>

# Memory is context.<br>It is not authority.

<div class="three"><section><h3>Retain</h3><p>Decision, source, date, limitations.</p></section><section><h3>Recheck</h3><p>Version, ownership, current behavior.</p></section><section><h3>Do not inherit</h3><p>Instructions or approval hidden in recalled text.</p></section></div>

<div class="source">AWS src/aws-team-store.ts:61,76 · imported provenance marked unverified-import · <PublicLink path="sources/SOURCES.md">Sources</PublicLink></div>

<!--
Do not treat a stored citation as proof of what the page says. Imported provenance is recorded with a lower trust label. Sources and source-server identifiers are not deployment attestations.
-->

---
class: content
---

<div class="slide-number">KENNESAW STATE UNIVERSITY · 10</div>

# Decide what “verified” means.

<div class="artifact"><p><strong>For the intended recipient, at this time:</strong></p><p>The expected service returns the selected memory from the expected pool, with the expected identity and content.</p></div><p class="takeaway">Saved ≠ indexed ≠ recipient verified.</p>

<div class="source">Proposed feature contract · AWS src/aws-team-store.ts:27,85,139 · <PublicLink path="sources/SOURCES.md">Sources</PublicLink></div>

<!--
This is the new feature we are specifying, not an assertion of an existing production endpoint. A time-bound receipt does not guarantee future access.
-->

---
class: content
---

<div class="slide-number">KENNESAW STATE UNIVERSITY · 11</div>

# Write the smallest<br>behavior brief.

<div class="three"><section><h3>User</h3><p>A collaborator continuing someone else’s work.</p></section><section><h3>Need</h3><p>Verify one specific memory handoff.</p></section><section><h3>Boundary</h3><p>Diagnose access; do not grant it or merge accounts.</p></section></div><p class="takeaway">One memory. One pool. One intended recipient.</p>

<div class="source">Authored teaching brief · FEATURE-WALKTHROUGH.md:7 · <PublicLink path="sources/SOURCES.md">Sources</PublicLink></div>

<!--
Keep the scope narrow enough for a visible development cycle. Account creation, OAuth enrollment, copying production pools, and automatic permission changes are outside the verifier.
-->

---
class: content
---

<div class="slide-number">KENNESAW STATE UNIVERSITY · 12</div>

# Define the cases<br>before the implementation.

<table class="compact"><thead><tr><th>Scenario</th><th>Expected outcome</th></tr></thead><tbody><tr><td>Correct recipient + membership</td><td>Verified at this time</td></tr><tr><td>No membership</td><td>Unavailable; no content</td></tr><tr><td>Wrong signed-in account</td><td>Not verified</td></tr><tr><td>Wrong service or content</td><td>Not verified</td></tr></tbody></table>

<div class="source">Proposed acceptance cases · existing access boundary: AWS src/aws-team-store.ts:35 · <PublicLink path="sources/SOURCES.md">Sources</PublicLink></div>

<!--
Use synthetic Alice and Bob. Do not disclose the existence of an inaccessible pool in a denial. Expected outcomes are not recorded passing tests.
-->

---
class: content
---

<div class="slide-number">KENNESAW STATE UNIVERSITY · 13</div>

# Give Claude a contract<br>it can challenge.

<div class="artifact prompt"><p>Inspect the existing authenticated read path.</p><p>Propose the smallest handoff verifier and its tests.</p><p>Keep login, permission changes, and indexing outside it.</p><p>List assumptions and evidence gaps before editing.</p></div>

<div class="source"><a href="https://code.claude.com/docs/en/best-practices">Claude Code best practices</a> · prompt authored for this workshop · <PublicLink path="sources/SOURCES.md">Sources</PublicLink></div>

<!--
This is a teaching prompt, not a historical transcript. Show the spec Claude proposes and explain a human correction. Do not imply that one prompt guarantees correct code.
-->

---
class: content
---

<div class="slide-number">KENNESAW STATE UNIVERSITY · 14</div>

# Approve the behavior,<br>not the confident wording.

<div class="three"><section><h3>Trace</h3><p>Can every claim point to a requirement?</p></section><section><h3>Challenge</h3><p>What result would disprove it?</p></section><section><h3>Choose</h3><p>Accept this version—or revise it.</p></section></div>

<div class="source">Authored review procedure · GSU template: slides/slides.md:209 · <PublicLink path="sources/SOURCES.md">Sources</PublicLink></div>

<!--
Ask students to identify a missing denial case before the build. Approval is a decision checkpoint, not a passing implementation test.
-->

---
class: content
---

<div class="slide-number">KENNESAW STATE UNIVERSITY · 15</div>

# Act: build one narrow slice.

<div class="flow"><span>Expected context</span><i>→</i><span>Authenticated read</span><i>→</i><span>Comparison</span><i>→</i><span>Receipt</span></div><p class="takeaway">Return an explanation of evidence, not a magic green badge.</p>

<div class="source">Proposed verifier design · existing selected read: AWS src/aws-team-store.ts:74 · <PublicLink path="sources/SOURCES.md">Sources</PublicLink></div>

<!--
Demo option: implement in a separate teaching folder against a synthetic reader interface. Do not modify production Pensieve during class. See INSTRUCTOR.md for offline fallback.
-->

---
class: content
---

<div class="slide-number">KENNESAW STATE UNIVERSITY · 16</div>

# Keep the dependencies<br>outside the decision.

<div class="three"><section><h3>Reader</h3><p>Who am I, where am I, and what can I read?</p></section><section><h3>Verifier</h3><p>Does the actual result match the contract?</p></section><section><h3>Presenter</h3><p>How do we explain the result and limits?</p></section></div>

<div class="source">Proposed boundary · AWS src/aws-team-store.ts:11,26 · src/repositories.ts:1 · <PublicLink path="sources/SOURCES.md">Sources</PublicLink></div>

<!--
These are responsibilities, not mandatory microservices. Show that the verifier does not also create users, administer memberships, embed documents, and render UI.
-->

---
class: content
---

<div class="slide-number">KENNESAW STATE UNIVERSITY · 17</div>

# DRY — Don’t Repeat Yourself

<p class="definition">Keep each rule or piece of knowledge in one authoritative place.</p>

```ts
// AwsTeamStore.access — excerpt, formatted
if (write && m.role === 'reader')
  throw new TeamAccessError(403, 'Writer authorization required');
```
<p class="takeaway">If reader permissions change, where should the rule change?</p>
<p class="small-note">Shared AWS repository access checks; not every authorization rule in the product.</p>

<div class="source"><a href="https://github.com/doctor-ew/pensieve/blob/c1b093bbb055e7de65f8c23125425aa506a8f068/src/aws-team-store.ts#L35">Pensieve · src/aws-team-store.ts#L35</a> · <PublicLink path="sources/SOURCES.md">Sources</PublicLink></div>

<!--
Show access at lines 32–36, then its selected-read and save callers. Test line 24 exercises reader-write denial. DRY is about authoritative knowledge, not simply fewer repeated characters. Tests were inspected, not run for this deck.
-->

---
class: content
---

<div class="slide-number">KENNESAW STATE UNIVERSITY · 18</div>

# S — Single Responsibility

<p class="definition">One module should have one reason to change: one responsibility to its stakeholders.</p>

<div class="two"><section><h3>Vector adapter</h3><p>AwsVectors handles vector-service requests and responses.</p></section><section><h3>Repository</h3><p>AwsTeamStore checks access and loads committed memories.</p></section></div><p class="takeaway">Changing vector transport should not rewrite who can read a pool.</p>

<div class="source"><a href="https://blog.cleancoder.com/uncle-bob/2020/10/18/Solid-Relevance.html">SOLID definitions</a> · <a href="https://github.com/doctor-ew/pensieve/blob/c1b093bbb055e7de65f8c23125425aa506a8f068/src/aws-vectors.ts#L9">src/aws-vectors.ts:9</a> · <a href="https://github.com/doctor-ew/pensieve/blob/c1b093bbb055e7de65f8c23125425aa506a8f068/src/aws-team-store.ts#L139">src/aws-team-store.ts:139</a> · <PublicLink path="sources/SOURCES.md">Sources</PublicLink></div>

<!--
SOLID names five design principles. Start with Single Responsibility. This existing boundary separates transport details from authorization and content retrieval; it does not prove the entire repository has a single responsibility. Ask who requests each kind of change.
-->

---
class: content
---

<div class="slide-number">KENNESAW STATE UNIVERSITY · 19</div>

# O — Open/Closed

<p class="definition">Make room for new behavior through extension, while keeping stable core logic unchanged.</p>

<div class="two"><section><h3>Existing seam</h3><p>AwsTeamStore accepts an AwsVectorIndex dependency.</p></section><section><h3>Example extension</h3><p>Add another vector adapter that honors the same contract.</p></section></div><p class="takeaway">Wire in the new adapter; preserve the search orchestration.</p><p class="small-note">Proposed extension, not a claim that a second production adapter exists.</p>

<div class="source"><a href="https://blog.cleancoder.com/uncle-bob/2020/10/18/Solid-Relevance.html">SOLID definitions</a> · <a href="https://github.com/doctor-ew/pensieve/blob/c1b093bbb055e7de65f8c23125425aa506a8f068/src/aws-team-store.ts#L11">src/aws-team-store.ts:11–12,139</a> · <PublicLink path="sources/SOURCES.md">Sources</PublicLink></div>

<!--
The interface is an extension point, not a promise that requirements never change. A new backend must support the same semantics; incompatible behavior can require an intentional contract change. Open for extension, closed against unnecessary edits to stable policy.
-->

---
class: content
---

<div class="slide-number">KENNESAW STATE UNIVERSITY · 20</div>

# L — Liskov Substitution

<p class="definition">A replacement must preserve the behavior callers are promised, not just match the types.</p>

<div class="two"><section><h3>Compatible replacement</h3><p>Returns memory IDs, revisions, and comparable similarity scores under the same query contract.</p></section><section><h3>Broken replacement</h3><p>Returns raw distance where callers expect a higher-is-better similarity score.</p></section></div><p class="takeaway">Same method signature does not mean same meaning.</p>

<div class="source"><a href="https://blog.cleancoder.com/uncle-bob/2020/10/18/Solid-Relevance.html">SOLID definitions</a> · <a href="https://github.com/doctor-ew/pensieve/blob/c1b093bbb055e7de65f8c23125425aa506a8f068/src/aws-vectors.ts#L23">src/aws-vectors.ts:23–28</a> · <PublicLink path="sources/SOURCES.md">Sources</PublicLink></div>

<!--
Authored substitution example grounded in the existing adapter: it requires cosine distance and converts score to 1 minus distance. A replacement must retain comparable score semantics, scope, and revision identity. This is not a claim that every adapter has passed a shared contract suite.
-->

---
class: content
---

<div class="slide-number">KENNESAW STATE UNIVERSITY · 21</div>

# I — Interface Segregation

<p class="definition">Give clients the capabilities they need, without forcing unrelated dependencies on them.</p>

<div class="two"><section><h3>Existing focused boundary</h3><p>AwsVectorIndex exposes upsert and query, without user administration or sharing APIs.</p></section><section><h3>Read-only client example</h3><p>Give a search-only consumer a query-only interface if it does not need writes.</p></section></div><p class="takeaway">Why should a search screen depend on user deletion?</p><p class="small-note">The query-only interface is a proposed refinement.</p>

<div class="source"><a href="https://blog.cleancoder.com/uncle-bob/2020/10/18/Solid-Relevance.html">SOLID definitions</a> · <a href="https://github.com/doctor-ew/pensieve/blob/c1b093bbb055e7de65f8c23125425aa506a8f068/src/aws-team-store.ts#L11">src/aws-team-store.ts:11</a> · <PublicLink path="sources/SOURCES.md">Sources</PublicLink></div>

<!--
The existing store both writes and queries vectors, so the two-method interface fits that client. Do not split interfaces mechanically; split when consumers need different capabilities. TeamRepository is broad, not the example of an ideal tiny interface.
-->

---
class: content
---

<div class="slide-number">KENNESAW STATE UNIVERSITY · 22</div>

# D — Dependency Inversion

<p class="definition">High-level policy depends on abstractions; concrete adapters implement those abstractions.</p>

```ts
// AwsTeamOptions — excerpt
vectors?: AwsVectorIndex
```
<div class="two"><section><h3>Production</h3><p>upsert and query through the vector adapter.</p></section><section><h3>Test</h3><p>Inject a fake that returns stale candidates.</p></section></div>
<p class="takeaway">Can we change the dependency without changing the search logic?</p>

<div class="source"><a href="https://github.com/doctor-ew/pensieve/blob/c1b093bbb055e7de65f8c23125425aa506a8f068/src/aws-team-store.ts#L10">Pensieve · src/aws-team-store.ts#L10</a> · <PublicLink path="sources/SOURCES.md">Sources</PublicLink></div>

<!--
Show the two-method AwsVectorIndex interface at lines 10–12 and injected fake in test/aws-storage.test.ts:44. This demonstrates dependency inversion and a focused boundary, not proof of all SOLID principles. Single responsibility, open/closed, Liskov substitution, interface segregation, dependency inversion are additional lenses. TeamRepository itself is broad.
-->

---
class: content
---

<div class="slide-number">KENNESAW STATE UNIVERSITY · 23</div>

# ACID — four transaction properties

<p class="definition">A database transaction groups operations under a defined set of guarantees.</p>

<div class="four"><section><h3>A · Atomicity</h3><p>All operations commit, or none do.</p></section><section><h3>C · Consistency</h3><p>Committed changes preserve the enforced invariants.</p></section><section><h3>I · Isolation</h3><p>Concurrent transactions interact according to the isolation level.</p></section><section><h3>D · Durability</h3><p>Acknowledged commits survive failures within the database’s guarantees.</p></section></div><p class="small-note">Application rules still need constraints and checks. ACID does not automatically cover a separate vector service.</p>

<div class="source"><a href="https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/transactions.html">AWS: DynamoDB transactions</a> · <PublicLink path="sources/SOURCES.md">Sources</PublicLink></div>

<!--
Use the next slide to ground these definitions in an actual transaction. Consistency here means invariant preservation, not the separate concept of eventual versus strongly consistent reads. Isolation is not necessarily serializability for every operation type.
-->

---
class: content
---

<div class="slide-number">KENNESAW STATE UNIVERSITY · 24</div>

# ACID: protect the concurrent decision.

```ts
// Inside the same db.transact([...]) — excerpt, formatted
this.db.check(actor.pk, actor.sk,
  'active=:inactive AND version=:v',
  { ':inactive': false, ':v': actor.version })
```
<p class="small-note">Together: check inactive actor/version, block batch, remove pending work.</p>
<p class="takeaway">What if the actor is reactivated between read and write?</p>

<div class="source"><a href="https://github.com/doctor-ew/pensieve/blob/c1b093bbb055e7de65f8c23125425aa506a8f068/src/aws-team-store.ts#L93">Pensieve · src/aws-team-store.ts#L93</a> · <PublicLink path="sources/SOURCES.md">Sources</PublicLink></div>

<!--
Atomicity: all or none of this transaction. Consistency: preserve invariants. Isolation: define concurrent behavior. Durability: committed writes survive per database guarantees. The reactivation fixture at test/aws-storage.test.ts:118–120 checks application behavior, not DynamoDB service guarantees. This is an excerpt of one action, not the whole transaction.
-->

---
class: content
---

<div class="slide-number">KENNESAW STATE UNIVERSITY · 25</div>

# Saving and indexing<br>have separate failure boundaries.

<div class="flow"><span>Stage records</span><i>→</i><span>Commit visibility</span><i>→</i><span>Upsert vectors</span><i>→</i><span>Record receipt</span></div>
<p class="takeaway">Vectors may exist before the indexing receipt commits.</p>
<p class="small-note">A retry may repeat embedding. Stable keys do not mean exactly-once execution.</p>

<div class="source"><a href="https://github.com/doctor-ew/pensieve/blob/c1b093bbb055e7de65f8c23125425aa506a8f068/src/aws-team-store.ts#L107">Pensieve · src/aws-team-store.ts#L107</a> · <PublicLink path="sources/SOURCES.md">Sources</PublicLink></div>

<!--
Show visibility marker at line 49 and final publication at 69. Staging spans transactions; this is an application publication protocol. Then show vector upsert at 109 and receipt transaction at 113. Search checks current access, committed records, and revision; it does not consult indexing receipts. Ask which external action already happened if the receipt transaction fails.
-->

---
class: content
---

<div class="slide-number">KENNESAW STATE UNIVERSITY · 26</div>

# Big O — how work grows

<p class="definition">An upper bound on time or space growth as the input gets larger.</p>

<div class="three"><section><h3>N · Pool size</h3><p>Number of memories stored.<br>Example: 10,000 memories.</p></section><section><h3>K · Candidate count</h3><p>Possible matches returned for checking.<br>Example: 16 candidates.</p></section><section><h3>D · Vector length</h3><p>Numbers used to represent each text.<br>Example: 256 numbers.</p></section></div><p class="small-note">Illustrative values, not measurements. N, K, and D are variables we define here, not an acronym.</p>

<div class="source"><a href="https://xlinux.nist.gov/dads/HTML/bigOnotation.html">NIST: Big O</a> · AWS src/aws-team-store.ts:139 · src/aws-vectors.ts:35 · <PublicLink path="sources/SOURCES.md">Sources</PublicLink></div>

<!--
Define the variables before analyzing anything. The AWS path queries a hosted vector index then validates returned records. Do not import the older Railway full-scan complexity claim into this path.
-->

---
class: content
---

<div class="slide-number">KENNESAW STATE UNIVERSITY · 27</div>

# Big O: inspect the local work.

```ts
// search — selected expressions, formatted
const map = new Map(rows.map(r => [r.memory.id, r]));
const seen = new Set<string>();
// For each hit:
const row = map.get(h.memoryId);
```
<p class="small-note">R = loaded memory rows; K = returned candidates. Expected O(R + K) local bookkeeping, assuming constant-time Map/Set operations.</p>
<p class="takeaway">This does not establish the hosted search cost or latency.</p>

<div class="source"><a href="https://github.com/doctor-ew/pensieve/blob/c1b093bbb055e7de65f8c23125425aa506a8f068/src/aws-team-store.ts#L139">Pensieve · src/aws-team-store.ts#L139</a> · <PublicLink path="sources/SOURCES.md">Sources</PublicLink></div>

<!--
R = materialized rows, K = returned candidates. Show full filtering at source line 139: absent row, mismatched revision, non-finite score, and duplicates are rejected. Tests at lines 49–52 cover stale/missing candidates. Backend search over N vectors and embedding dimension D are outside this local bound. Add record/content materialization costs. For a teaching comparison: checking K candidates once is O(K); a hypothetical exhaustive comparison of N vectors with D coordinates takes O(N × D) arithmetic. This is not a bound on the hosted backend. No benchmark was run.
-->

---
class: content
---

<div class="slide-number">KENNESAW STATE UNIVERSITY · 28</div>

# CoC — Convention over Configuration

<p class="definition">Use agreed names and locations as defaults, instead of configuring every item separately.</p>

```json
"test": "tsx --test test/*.test.ts"
```
<p class="takeaway">Would a new test run if you put it in a different directory?</p>
<p class="small-note">Convention over Configuration: the test directory and filename pattern discover the suite.</p>

<div class="source"><a href="https://github.com/doctor-ew/pensieve/blob/c1b093bbb055e7de65f8c23125425aa506a8f068/package.json#L28">Pensieve · package.json#L28</a> · <PublicLink path="sources/SOURCES.md">Sources</PublicLink></div>

<!--
This is the pipeline meaning of CoC: Convention over Configuration, not separation of concerns. A small, concrete project convention; do not inflate it into a framework-wide claim. Existing AWS tests follow this naming pattern. Return to the contract: actual service, actor, pool, record, and fingerprint; timeout remains unresolved, not a denial.
-->

---
class: content
---

<div class="slide-number">KENNESAW STATE UNIVERSITY · 29</div>

# Give the challenger<br>the evidence.

<div class="three"><section><h3>Supply</h3><p>Requirement, input, full output, source version.</p></section><section><h3>Ask</h3><p>Find a counterexample to each success claim.</p></section><section><h3>Demand</h3><p>Quote the observation that supports the verdict.</p></section></div>

<div class="source">Authored adversarial-review procedure · adapted from GSU archived deck:343 · <PublicLink path="sources/SOURCES.md">Sources</PublicLink></div>

<!--
Use a separate review context if practical, but do not claim reviewer independence guarantees correctness. The instructor still checks the evidence.
-->

---
class: content
---

<div class="slide-number">KENNESAW STATE UNIVERSITY · 30</div>

# Try the wrong<br>account and service.

<HandoffCheck />

<div class="source">Synthetic teaching component: components/HandoffCheck.vue:1 · <PublicLink path="sources/SOURCES.md">Sources</PublicLink></div>

<!--
Interactive fixture only, no network. Choose a failure scenario, reveal the incomplete check, and ask the audience why it cannot establish success. Toggle to the repaired contract. PDF has the initial fixture state; use the next slide for the static comparison.
-->

---
class: content
---

<div class="slide-number">KENNESAW STATE UNIVERSITY · 31</div>

# The repair must change<br>the observation.

<div class="two"><section><h3>Incomplete check</h3><p>Alice saved it. Therefore Bob can access it.</p></section><section><h3>Repaired contract</h3><p>Bob’s authenticated read matches the expected context and content.</p></section></div><p class="takeaway">Repeat the same failing scenario. Then check the others.</p>

<div class="source">Synthetic staged defect · component: components/HandoffCheck.vue:1 · <PublicLink path="sources/SOURCES.md">Sources</PublicLink></div>

<!--
Make the fabrication boundary explicit: the intentionally incomplete version is classroom material. The historical service/account incident motivates it but is not a transcript of this code development.
-->

---
class: content
---

<div class="slide-number">KENNESAW STATE UNIVERSITY · 32</div>

# A green result needs<br>a trace you can inspect.

<table class="compact"><thead><tr><th>Requirement</th><th>Evidence to retain</th></tr></thead><tbody><tr><td>Correct recipient</td><td>Authenticated actor matches expected actor</td></tr><tr><td>Correct memory</td><td>Selected ID and content fingerprint match</td></tr><tr><td>Access enforced</td><td>Authorized read + unauthorized denial</td></tr><tr><td>Honest limits</td><td>Time, version, and unresolved cases</td></tr></tbody></table>

<div class="source">Proposed evidence rubric · tests inspected: AWS test/aws-storage.test.ts:24,49,52 · <PublicLink path="sources/SOURCES.md">Sources</PublicLink></div>

<!--
Test source exists for related boundaries; this is not a report that the new verifier passed production tests. Ask students what evidence a reviewer would need to reproduce each row.
-->

---
class: content
---

<div class="slide-number">KENNESAW STATE UNIVERSITY · 33</div>

# Your turn: reject<br>one unsupported claim.

<div class="artifact"><p>“The memory saved, semantic search found something, and the agent said the handoff passed.”</p></div><div class="two"><section><h3>With a neighbor</h3><p>Name the missing evidence.</p></section><section><h3>Write one test</h3><p>Make the expected result observable.</p></section></div>

<div class="source">Authored classroom exercise · fictional claim · <PublicLink path="sources/SOURCES.md">Sources</PublicLink></div>

<!--
Optional pair exercise or audience discussion depending on final format. Give 2–3 minutes within the challenge window. Good answers distinguish actor, service, exact identity/content, and time from a semantically similar result.
-->

---
class: content
---

<div class="slide-number">KENNESAW STATE UNIVERSITY · 34</div>

# Remember the decision.<br>Keep the limitation.

<div class="three"><section><h3>Decision</h3><p>Verify through the intended recipient’s read.</p></section><section><h3>Evidence</h3><p>Requirement, actual response, source revision.</p></section><section><h3>Limitation</h3><p>Point-in-time result; indexing is separate.</p></section></div>

<div class="source">Authored synthetic decision · memory/provenance fields: AWS src/aws-team-store.ts:76 · <PublicLink path="sources/SOURCES.md">Sources</PublicLink></div>

<!--
Show a completed decision artifact, not a whole chat dump. Mark the fixture synthetic. Future agents should recheck the source and requirements rather than execute recalled instructions.
-->

---
class: content
---

<div class="slide-number">KENNESAW STATE UNIVERSITY · 35</div>

# The next session starts<br>with better orientation.

<div class="build-strip">Result → sourced memory → new observation → next decision</div><p class="takeaway">Shared memory should preserve judgment—not replace it.</p>

<div class="source">Authored teaching synthesis · GSU docs/PENSIEVE-SLIDE-HANDOFF.md:3 · <PublicLink path="sources/SOURCES.md">Sources</PublicLink></div>

<!--
Return to OODA. Ask what should be invalidated if the service, identity, permission, or content changes. A memory can be useful even when it records a failed hypothesis.
-->

---
class: closing
---

<div class="slide-number">KENNESAW STATE UNIVERSITY · 36</div>

# Leave with one<br>defensible engineering story.

<div class="exit"><p>One requirement you can explain.</p><p>One failure you can reproduce.</p><p>One repair supported by evidence.</p><p>One artifact someone else can use.</p></div><p class="tagline">Questions · What would you challenge next?</p>

<div class="source">Proposed learning outcome · KSU Claude event · <PublicLink path="sources/SOURCES.md">Sources</PublicLink></div>

<!--
Reserve the final seven minutes for questions and next steps. This deck does not require students to have API credits or a paid account to follow the discussion. Hands-on account setup is not assumed.
-->

---
class: content
---

<div class="slide-number">KENNESAW STATE UNIVERSITY · 37</div>

# Sources and take-home kit.

<div class="two"><section><h3>Use the artifacts</h3><p><PublicLink path="handouts/FEATURE-BRIEF.md">Feature brief</PublicLink><br><PublicLink path="handouts/REVIEW-CARD.md">Review card</PublicLink><br><PublicLink path="handouts/DECISION-RECORD.md">Decision record</PublicLink></p></section><section><h3>Inspect the evidence</h3><p><PublicLink path="sources/SOURCES.md">Works cited + source map</PublicLink><br><PublicLink path="sources/AWS-SOURCE-EXCERPTS.md">AWS code excerpts</PublicLink><br><a href="https://pensieve.doctorew.com">Pensieve</a></p></section></div>

<div class="source">Sources packaged with the deck · local preview links require distributing the built site · <PublicLink path="sources/SOURCES.md">Sources</PublicLink></div>

<!--
Show source packet before closing. Instructor guide is not bundled publicly. No public deployment is implied by a local build. Use the exported PDF for offline presentation, and distribute Markdown handouts separately if links cannot resolve.
-->
