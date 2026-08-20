<!-- Upstream template: portfolio-search-indexing-audit bundle v5; repository contract v4 -->
---
title: "Search indexing"
purpose: "Property-specific index policy, validation commands, deployment gate, and console follow-up."
status: active
updated: 2026-08-20
owner: "Sam"
open_tasks: []
---
# Search indexing

Canonical origin: `https://skillprovenance.dev/`

Console property ID: `sc-domain:skillprovenance.dev`

Property mode: `website`

Generated output: `.`

If deployment assembles a separate staging directory, this path must name that exact deployable artifact, not its source directory.

## Index policy

| Surface | Policy | Reason |
|---|---|---|
| `/` | Index and include in sitemap | Canonical product and installation page |
| `/404.html` and unknown routes | `noindex` and omit from sitemap | Error handling, not a content destination |
| `/robots.txt`, `/sitemap.xml`, `/llms.txt` | Crawlable and omitted from the page sitemap | Search and agent discovery surfaces |
| `/.well-known/assistant-guide.txt` and sidecar | Crawlable and omitted from the page sitemap | Bounded agent verification surfaces |
| GitHub, ClawHub, and other external copies | Omit from this sitemap | Distribution copies are not site canonical pages |

## Validation lanes

- Offline: `node scripts/check-search.mjs`
- Production after deployment: `node scripts/check-production-search.mjs`
- Machine-readable output: add `--json`
- Local HTTP test: add `--base=http://127.0.0.1:8765/` after starting the static server on port 8765

Exit code `0` is pass, `1` is a site defect, and `2` is configuration or infrastructure failure.

For a creator-profile or external-platform property, replace the website validation lanes with the reports and controls the property actually exposes. Do not invent repository, production, sitemap, or indexing work.

## Deployment and console sequence

1. Run the normal build and offline search contract.
2. If deployment copies or transforms output, stage the exact deployable artifact with the same builder used by release automation.
3. Ensure repository-wide checks include newly scaffolded files, including checks based on `git ls-files`.
4. Deploy through the repository's normal release path.
5. Wait for the deployment to complete.
6. Run the production search contract.
7. Confirm the deployed sitemap URL set matches the repository sitemap.
8. Refresh a materially changed stale sitemap at most once, using its full canonical URL for a domain property.
9. Inspect or request indexing for canonical HTML pages.
10. Start issue-group validation only when matching production behavior is live.
11. Record console state under `ops/search/<provider>/YYYY-MM-DD/`.

## Expected noise

- `http://skillprovenance.dev/`, `https://www.skillprovenance.dev/`, and `http://www.skillprovenance.dev/` intentionally redirect to `https://skillprovenance.dev/`.
- `/404.html` and synthetic unknown paths intentionally return the custom noindex error page.
- Machine-readable discovery files are intentionally not listed as canonical HTML pages in the sitemap.
- Provider crawl and indexing reports may lag accepted sitemap submissions and deployed changes.

## Current baseline

- Repository, generated output, and production matched before the 2026-08-20 console action.
- Production canonical, robots, sitemap, JSON-LD, assistant files, redirects, and hosted 404 behavior passed the property gate.
- Google Search Console reported `Success`, last read 2026-08-20, with one discovered page.
- The homepage was individually reported indexed. Provider recrawl latency remains expected after later deployments.

## Console action ledger

Read this table before opening the console. Add only observed actions and confirmations. An accepted request remains pending until a later report proves completion.

| Provider and property | Action and target | Accepted at | Confirmation | Result class | Repeat policy | Next review |
|---|---|---|---|---|---|---|
| Google Search Console, `sc-domain:skillprovenance.dev` | Resubmit `https://skillprovenance.dev/sitemap.xml` | 2026-08-20 | Sitemap detail showed `Success`, last read 2026-08-20, one discovered page | Accepted submission, not proof of future recrawl or indexing | Do not repeat until a later deployed material revision is absent from provider state or GSC names a failure | After the next authorized production deployment and normal provider lag |

Keep rejected attempts and unknown outcomes distinct from accepted actions. Do not repeat an accepted action merely because the provider report remains stale.
