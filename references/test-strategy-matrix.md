# Test Strategy Matrix

Use this to choose proof before coding.

| Change Type | Minimum Proof | Stronger Proof |
|---|---|---|
| Pure utility/function | Unit tests | Property/table tests |
| State machine/reducer | Transition table tests | Recovery/regression tests |
| API route | Route integration test | Contract test with consumers |
| Database/schema | Migration/schema test | Seed + read/write integration |
| Auth/permissions | Deny/allow tests | Role matrix tests |
| Payment/signing/external action | Reject-path + audit test | Sandbox/testnet integration |
| Realtime/SSE/WebSocket | Event delivery test | Reconnect/stale/drop tests |
| Frontend data hook | Query/mutation tests | Cache invalidation tests |
| UI component | Render state tests | Visual/screenshot/responsive checks |
| Performance-sensitive code | Benchmark or budget check | Profiling trace |
| Docs-only governance | Link/source consistency check | Drift grep + review |

## Required Negative Tests

For safety, auth, money, permissions, destructive actions, or user data:

- Test valid path.
- Test invalid/rejected path.
- Test audit/log/status does not claim success before real success.
- Test stale/missing data behavior.

## Command Selection

Prefer existing project scripts. For new apps, default to:

```text
bun test
bun run lint
bun run build
```

If the repo uses npm/pnpm/yarn, follow the repo.
