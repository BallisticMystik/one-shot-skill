# Definition Of Done

Use this before final response, checkpoint completion, or handoff.

## Done Checklist

- Acceptance criteria are satisfied or explicitly marked incomplete.
- Relevant tests/checks ran and exact results are known.
- No unsupported claims remain in the final answer.
- Docs, comments, and decision records match code behavior.
- Drift search ran for stale terms relevant to the task.
- Risk register is updated or no residual risks remain.
- Deferred items are filed when non-blocking gaps remain.
- UI work includes loading, empty, error, focus, responsive, and motion checks where applicable.
- Schema/API changes have matching consumers updated.
- Generated files are intentional.
- Unrelated dirty worktree files are identified but untouched.
- Checkpoint/progress artifacts are updated when governance requires it.
- Final report is written using `final-report-template.md`.

## Verification Evidence

Record commands like:

```text
command: <command>
result: <pass/fail summary>
notes: <important failures or skipped reason>
```

If a command cannot run, state why, whether it is sandbox/tooling related, and what risk remains.
