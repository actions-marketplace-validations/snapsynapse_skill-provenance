# Project Context: Skill Provenance

## What this is

Skill Provenance is a metaskill (an Agent Skill about managing Agent Skills)
that adds portable version tracking, staleness detection, and SHA-256
integrity verification to Agent Skill bundles. It solves version confusion
when a skill bundle (`SKILL.md`, evals, scripts, docs) moves across local
folders, registries (ClawHub), platform uploads (Claude Settings UI), and
multi-agent sessions (Claude, Codex, Gemini CLI, OpenClaw agents).

Distributed as:
- A Claude Code plugin (`/plugin install skill-provenance@snapsynapse-skill-provenance`)
- A Codex plugin package manifest and a GitHub CLI-installable Agent Skill
- A standalone `.skill` file for the Claude Settings UI (and Perplexity Computer,
  renamed to `.zip`)
- A GitHub Action (`action.yml`) for CI-side bundle validation
- Source on ClawHub and GitHub

## Audience

Authors and teams who build, distribute, or run Agent Skills across multiple
surfaces (Chat, Code, Cowork, API) and non-Claude platforms, and need to
know a bundle they're editing or installing is the version they trust and
hasn't silently drifted. Secondary audience: agents themselves (Claude,
Codex, Gemini CLI, OpenClaw) reading `AGENTS.md`/`CLAUDE.md`/`GEMINI.md` for
how to work on this repo, and the bundled `skill-provenance/SKILL.md` for
how to apply the versioning protocol to *other* skill bundles they touch.

## Style / tone

Direct, technical, no marketing fluff. README uses comparison tables against
adjacent tools (`gh skill`, ClawHub, Claude Skills API, Skillman) rather than
vague claims. Docs favor concrete before/after examples over abstract
description (see the `SKILL_v4.md` → `SKILL.md`/`MANIFEST.yaml` snippet in
`README.md`). Security-conscious: `SECURITY.md` exists, CI includes an
`action-security-check.sh`, and recent changelog entries are hardening fixes
(fail-closed hash verification, safe input transport) rather than features.

## Key URLs

- Canonical site: https://skillprovenance.dev/
- Repo: https://github.com/snapsynapse/skill-provenance
- ClawHub listing: https://clawhub.ai/snapsynapse/skills/skill-provenance
- Assistant guide (pre-install verification): https://skillprovenance.dev/.well-known/assistant-guide.txt
- Releases: https://github.com/snapsynapse/skill-provenance/releases

## Current status (as of 2026-08-28 assessment)

- Stable public bundle release is 6.1.0. A local 6.2.0 adoption release adds
  a standalone verifier, portable bootstrap prompt, and refreshed ecosystem
  evidence. It is not committed, pushed, deployed, tagged, or published until
  each release step is explicitly authorized.
- The validator now fails closed on unsafe or ambiguous paths, duplicate
  entries, manifest-listed symlinks, and unsupported inventory syntax.
  Packaging reuses that validator policy at each derived-package boundary.
- Coverage is 41 core and 18 supplemental evals, 59 total, plus executable
  validator, action-input, packaging, and release-surface regression checks.
- The GitHub Marketplace validation action is publicly listed and the stable
  action reference is `snapsynapse/skill-provenance@v6.1.0`.
- GitHub Agent Skill publication dry-run passes, but discovery search does not
  yet return this repository. Publication remains an external authority gate.
- Current adoption work is portfolio dogfooding, verified-adopter evidence,
  GitHub Agent Skill publication, and targeted registry/toolmaker interop.
- Health verdict: healthy and actively maintained. See root `CLAUDE.md` for
  full agent-facing build, test, and release conventions.

## Documentation authority and taxonomy

| Scope | Authoritative source |
|---|---|
| Canonical bundle behavior and instructions | `skill-provenance/SKILL.md` and its routed references |
| Bundle identity, inventory, hashes, and validation attestations | `skill-provenance/MANIFEST.yaml` |
| Complete release history | Root `CHANGELOG.md` |
| Portable recent release history | `skill-provenance/CHANGELOG.md` |
| Current repository state and documentation routing | `PROJECT_CONTEXT.md` |
| Intended future work | `ROADMAP.md` |
| Agent-facing and executable trust boundaries | `AGENTIC_SURFACES.md` |
| Search policy and provider action ledger | `ops/search-indexing.md` and dated `ops/search/` evidence |
| Dated ecosystem observations | `docs/`; each note must preserve its source and measurement boundary |

Root documentation and `skill-provenance/references/` are maintained
references. `docs/` contains dated evidence notes, `ops/` contains operational
policy and evidence, and `handoffs/` is a temporary queue rather than history.
This file is the documentation index while those folders remain small. If a
folder grows beyond a few independently maintained documents, add a local
index before relying on bulk documentation audits.

Root reference documents do not require frontmatter. Bundle documentation
uses the per-file integer revision and hash recorded in `MANIFEST.yaml`;
`ops/search-indexing.md` keeps its existing title, purpose, status, updated,
owner, and open-task fields. Verify documentation claims with
`validate.sh`, `release-surface-check.sh`, and the offline search contract
before treating them as current. Migrate durable handoff content to the
authority above, then remove the temporary handoff rather than archiving it.
