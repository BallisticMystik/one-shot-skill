# Subagent Prompt Template

Use when delegating work to another agent. Keep tasks bounded and file-disjoint when parallel.

```text
You are working in <repo/path>.

Read first:
- <governance files>
- <sidechain analysis/spec/progress files>
- <specific code files>

Task:
<one concrete subtask>

Write scope:
- You may edit:
  - <file/module>
- Do not edit:
  - <files/modules>

Constraints:
- Do not revert or overwrite changes by others.
- Follow existing project patterns.
- Preserve <invariants/contracts>.
- Use TDD where applicable: write failing test, implement, rerun.
- Stop and report if you hit <hard-stop triggers>.

Expected output:
- Files changed.
- Tests run and exact result.
- Any assumptions.
- Any risks/deferred items.
```

## Delegation Rules

- Do not delegate the immediate blocking task if local work depends on it.
- Do not assign overlapping write scopes to parallel agents.
- Do not ask agents to make broad exploratory changes.
- Prefer concrete implementation tasks over vague "review everything" prompts.
- Integrate returned changes with a local review before final handoff.
