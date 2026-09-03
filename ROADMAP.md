# Roadmap

## Now

- Measure verified adoption of the public 6.2.0 standalone-verification
  release and GitHub Agent Skill discovery path.
- Reconcile the separately published ClawHub copy after its user-controlled
  license attestation and upload boundary are completed.
- Dogfood manifests across portfolio skills and add a verified-adopters loop.
- Use the dated skill-version drift evidence for targeted registry and
  toolmaker interop, keeping reported observations distinct from live metrics.

## Adoption evidence gate

After the 6.2.0 verifier is public, measure verified adopters, GitHub Agent
Skill discovery, registry interest, and interop responses before adding a new
service surface. Lack of evidence should defer expansion rather than create a
parallel monitoring or packaging system.

## Later

- **Multi-bundle workspace support**: Track multiple skill bundles in a
  monorepo with a single plugin instance.
- **Detached manifest signatures**: Add an optional interoperable trust layer
  without turning the zero-dependency integrity checker into a PKI client.
- **Registry and package-manager interop**: Preserve portable bundle identity
  while leaving install resolution and consumer lockfiles to their owners.

## Not Yet

- **MCP server**: Programmatic verify/audit endpoint for CI pipelines
  and external tooling.
- **PostToolUse hook for auto-hash**: Automatically recompute SHA-256
  in MANIFEST.yaml when SKILL.md is edited. Deferred until there is a safe
  design that avoids silent manifest churn and preserves stale-file intent.
