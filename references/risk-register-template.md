# Risk Register Template

Use this for any non-trivial app build, external integration, data migration, realtime system, auth/payment/safety behavior, or frontend workflow with meaningful user impact.

```markdown
| Risk | Severity | Likelihood | Detection | Mitigation | Owner | Status |
|---|---|---|---|---|---|---|
| | low/med/high | low/med/high | test/log/manual | | | open/mitigated/deferred |
```

## Common Risk Categories

- Product ambiguity: user outcome is unclear.
- Data correctness: stale, partial, duplicated, or mismatched data.
- Security/privacy: auth, permissions, secrets, PII, payment, signing, admin power.
- Reliability: crash recovery, retry, idempotency, offline, reconnect.
- Migration: schema drift, incompatible data shape, rollback gaps.
- UX: hidden failure states, inaccessible controls, mobile breakage.
- Performance: expensive renders, slow endpoints, excessive network chatter.
- Observability: no logs/metrics for failure modes.
- Maintainability: duplicate paths, weak boundaries, unclear ownership.

## Rule

Every high severity risk needs either a mitigation, a test, a hard-stop approval, or a documented deferral.
