# PAX Protocol

PAX means Phase Autonomous Execution. Use this when the operator engages a phase by name and wants the agent to execute the whole locked phase end-to-end without per-subtask approval interrupts.

This protocol is portable: it applies to any app or sidechain with a locked spec, not just financial/trading work.

## Trigger

PAX is engaged when the user says something like:

- `PAX <sidechain> P1`
- `engage Phase X`
- `run Phase X`
- `execute Phase X`
- `go` or `yes` in response to a phase-start proposal

Default scope is one phase. Multi-phase execution requires explicit range approval, such as `PAX P1-P3`.

## Behavior Contract

When PAX is engaged:

1. Locked spec is binding. Follow the plan, prompt chain, skills plan, and governance files. Do not silently expand scope.
2. Execute routine subtasks without per-subtask user approval.
3. Use TDD and required specialist skills/checks per the plan.
4. Update progress as work completes.
5. Run targeted tests per subtask and broader tests at phase boundary.
6. Run checkpoint ritual at phase close when required.
7. Surface a phase-close report before asking whether to continue.

## Hard-Pause Triggers

Always stop and ask before proceeding when:

- The locked spec contradicts another locked decision.
- Work leaks into another sidechain or execution lane.
- A new dependency/framework is needed.
- A schema/API/data contract change has unclear consumers.
- Security, privacy, auth, payment, signing, money movement, or destructive behavior changes.
- Production-visible external actions are needed: PR creation, push to shared branch when not already authorized, comments, Slack/email, deploys.
- Global governance/invariant files need semantic changes.
- Tests remain red after one focused retry.
- A destructive git operation is needed.
- The user-approved product/design direction would materially change.

## Soft-Pause Triggers

Proceed, but surface in the next update/report:

- New deferred item filed.
- Extra tests added because the plan missed a regression guard.
- Helper extraction or file split done to preserve maintainability.
- Minor clarification resolved from existing locked decisions.
- File rename/split done to preserve architecture.

## Construction Vs Execution

Construction phase can be autonomous after the user approves scoping:

- Editing sidechain planning docs.
- Drafting prompt chains.
- Updating progress tables.
- Writing proposed governance text.
- Creating decision records.

Execution phase follows PAX hard-pause gates:

- Source code changes.
- Schema changes.
- Threat/security docs that merge into authoritative governance.
- Global governance changes.
- External/production-visible actions.

Drafting an invariant or threat-model amendment is construction. Merging it into the authoritative repo document is execution and may require approval.

## Phase-Close Report

At phase close, report:

- Scope executed.
- Commits or changed files.
- Tests run and results.
- Checkpoint findings.
- Hard/soft pauses encountered.
- Deferred items filed.
- Residual risks.
- Next phase recommendation.

Do not ask for routine subtask approvals during PAX. The safety mechanism is the hard-pause trigger list plus checkpoint review.
