# KSU: Build with AI. Remember with evidence.

A 90-minute Claude event for Kennesaw State University CS students, presented by
Drew Schillinger and Tyler Sztuka. Shared memory, Pensieve, OODA, adversarial
review, and concrete DRY / SOLID / ACID / Big O / Convention over Configuration examples.

See [the deck guide](slides/README.md) for local presentation and [validation](slides/VALIDATION.md)
for checked behavior and remaining rehearsal work. The demo is synthetic, not a live Pensieve client.

## GitHub Pages

The workflow builds `slides/` with the repository's Pages base path, exports a PDF,
and deploys on pushes to `main`. Enable GitHub Actions as the Pages source in repository
settings. Speaker notes are excluded from the built site but remain in the source.

The published site includes handouts, cited source excerpts, and `ksu-pensieve.pdf`.
University and Claude marks remain owned by their respective owners; see [asset provenance](slides/ASSETS.md).
