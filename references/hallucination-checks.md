# Hallucination Checks

Use this reference before final answers, checkpoint claims, and architecture summaries.

## Evidence Rules

- Do not claim a test passed unless the command was run in this session or the user supplied exact output.
- Do not claim a file contains behavior without reading it.
- Do not infer current library/API behavior from memory when version-sensitive; inspect local dependencies or official docs.
- Do not quote governance status from memory; read the current governance files.
- Do not summarize generated documents as committed unless git status confirms it.

## Claim Audit

Before final response, scan your own answer for:

- "implemented", "verified", "green", "complete", "locked", "normative", "safe", "already"
- For each, identify the supporting file, command, or user-provided artifact.
- Remove or qualify unsupported claims.

## Cross-Source Checks

For safety-critical work, compare:

- Code implementation
- Tests
- Threat model
- Decision record
- `CLAUDE.md` invariant
- Progress/checkpoint notes

Any contradiction is either a correction task or a hard stop.
