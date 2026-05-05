# Definition Of Ready

Use this before implementation. If any required item is missing, keep planning or ask for approval to proceed with a named assumption.

## Ready Checklist

- Objective is concrete and user-visible, operator-visible, or developer-visible.
- Scope and non-scope are explicit.
- Source-of-truth files are identified.
- Current behavior to preserve is documented.
- New behavior is documented.
- Acceptance criteria are testable.
- A test strategy is selected from `test-strategy-matrix.md`.
- Hard-stop gates are listed.
- Key risks are captured in a risk register or explicitly waived.
- Dependencies and tech stack are consistent with the existing app.
- Data/schema/API contracts are known, or the unknowns are hard-stopped.
- UI work has a styleguide or an explicit reason it does not need one.
- Rollback/recovery path is known for migrations, external integrations, and risky changes.
- The agent knows what files/modules are likely in scope.
- The user has approved any material product, architecture, dependency, or safety decision.

## Preparation Packet Format

```text
Objective:
Scope:
Non-scope:
Source of truth:
Current behavior:
Proposed behavior:
Acceptance criteria:
Test strategy:
Design/styleguide:
Risks:
Hard stops:
Autonomous assumptions:
First implementation step:
```

## Readiness Verdict

Use one:

- `ready`: proceed autonomously.
- `ready-with-assumptions`: proceed and record assumptions.
- `not-ready`: ask only the minimum blocking questions.
- `hard-stop`: use `hard-stop-matrix.md`.
