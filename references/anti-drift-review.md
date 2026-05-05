# Anti-Drift Review

Use this reference during review, cleanup, and after implementation.

## Drift Classes

Check for:

- Code/doc drift: documentation describes behavior that implementation does not have.
- Governance drift: `CLAUDE.md`, `CLAUDE.local.md`, decision records, and progress disagree.
- Terminology drift: stale words like "candidate", "in flight", "temporary", "legacy", or "TODO" after promotion.
- Test drift: tests assert old semantics or fail to cover the promoted invariant.
- Architecture drift: two semantic paths exist for one behavior.
- Safety drift: frontend or docs imply enforcement that only exists client-side.
- Audit drift: logs/trades/checkpoints claim success before exchange-valid proof.

## Search Patterns

Use targeted search terms such as:

```text
candidate
in flight
TODO
legacy
temporary
FIXME
not yet
sequential
fallback
skip guard
submitted_ok
dispatchSource
threat-model
```

Tune terms to the sidechain domain.

## Correction Rules

- Fix stale wording when the implementation is already clear and tests pass.
- Add tests when a promoted invariant has enforcement but no regression coverage.
- Stop for approval if the correction changes semantics, not just wording.
- File deferred items for real but non-blocking gaps.
