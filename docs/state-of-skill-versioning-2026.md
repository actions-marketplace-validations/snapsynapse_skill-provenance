# State of Skill Versioning 2026

Status: Evidence note, updated 2026-08-28

## Finding

An external registry-diff observer reported on 2026-08-27 that version labels
did not move for 169 of 1,193 observed Agent Skill instruction-text changes,
or 14.2 percent. The changes affected 660 distinct skills.

The same observer reported a control population of 25,122 MCP registry
entries: 100 percent carried a version and 99.9 percent were semver-shaped.
Their interpretation was that version reliability differs by distribution
surface. A version pin can be a useful proxy for MCP packages while remaining
an unreliable integrity handle for Agent Skills.

## Relevance to Skill Provenance

This observation supports the repository's existing separation of concerns:

- `bundle_version` is a human-readable release label.
- Per-resource SHA-256 digests determine whether the bytes match recorded
  state and can fail verification.
- `validated_against` records are environment-specific attestations that age.
  They inform re-validation decisions but do not override byte integrity.

The reported 14.2 percent is evidence for making digests load-bearing rather
than evidence that semver should be removed. Semver remains useful for release
communication, while digests answer the narrower factual question of whether
the artifact changed.

## Measurement boundary

The 14.2 percent figure is a dated third-party observation, not a live metric
maintained by this repository. Cite it with its date and source. Do not present
it as independently reproduced here.

The linked public endpoint is rolling. Its current aggregate and exposed event
sample do not provide the frozen numerator and denominator needed to reproduce
the 2026-08-27 calculation directly. The endpoint also cannot observe behavior
changes caused by a loader, harness, model, or policy when artifact bytes do
not change. That unobservable runtime drift is why `validated_against` remains
a separate, informational record.

## Sources

- Nikolife2016, registry-diff observation and methodology note:
  https://github.com/agentskills/agentskills/issues/46#issuecomment-5441281208
- Skill Provenance working implementation offered as prior art:
  https://github.com/agentskills/agentskills/issues/46#issuecomment-4862075282
- Integrity and environment-attestation separation:
  https://github.com/agentskills/agentskills/issues/46#issuecomment-4994929787
- Rolling public drift endpoint cited by the observer:
  https://pulsefeed.dev/mcp/drift.json?days=30

## Publication rule

Refresh time-sensitive counts before reusing them in a new report. Keep dated
observations distinct from current measurements, and keep private outreach or
pursuit notes outside the public repository.
