# Sidechain Creation Walkthrough

Use this reference when creating or materially revising a TimeMachineV9 sidechain. It folds in the local `/sidechain` skill execution model: analyze, rate complexity, generate a JSON prompt chain, execute subtask-by-subtask with TDD, and update progress after each checkpoint.

The goal is to answer almost every question before implementation so the agent can proceed autonomously, stopping only for hard approvals or newly discovered edge cases.

## Preparation Packet

Create a preparation packet before execution. Include:

1. Objective: one concrete outcome, not a theme.
2. Scope: files, modules, docs, tests, and UI surfaces in scope.
3. Non-scope: explicit boundaries and deferred items.
4. Source of truth: governing files and exact precedence order.
5. Invariants touched: list each relevant invariant and whether it is read-only, amended, or implementation-enforced.
6. Current behavior: what must remain true.
7. Proposed behavior: what changes and why.
8. Acceptance criteria: observable pass/fail statements.
9. Test plan: unit, integration, E2E, manual, or doc-only checks.
10. Approval gates: hard stops expected during the work.
11. Rollback/recovery: what to do if tests or assumptions fail.
12. Progress/checkpoint plan: when status is updated and what review ritual applies.

## Required Sidechain Artifacts

Create or update these artifacts in the active planning directory unless governance says otherwise:

```text
opux/sidechain/<task-name>/
  analysis.md
  prompt-chain.json
  progress.md
  skills-plan.md              # when specialist invocation mapping is needed
  skill-invocation-templates.md # when CLAUDE.local.md requires mapped invocation templates
```

For TimeMachineV9, live sidechain working docs normally live in:

```text
D:/projects/TimeMachineV9-planning/opux/sidechain/<task-name>/
```

Do not commit live working docs unless the sidechain end-of-life ritual says to archive/distill them into repo history.

## Core Questions To Answer

Answer these before authorizing execution:

- What business/operator problem does this solve?
- What exact workflow will be different after completion?
- Which existing implementation path is canonical?
- Which old or alternate path must not be revived?
- Which state machines, persistence contracts, external APIs, or UI contracts are touched?
- What data shape changes are required?
- Does any migration need a rollback or compatibility plan?
- Does any signing, exchange, cap, or autonomous behavior change?
- What threat model section applies?
- What tests already cover this area?
- What tests are missing?
- What documentation could drift if code changes?
- What must be true for checkpoint acceptance?
- What would require stopping for user approval?

## Complexity Rating

Rate every subtask:

| Complexity | Use When | Instruction Layers |
|---:|---|---:|
| 1 | Single-file/simple logic/no coordination | 1 |
| 2 | 2-3 files, moderate state or API coordination | 2 |
| 3 | 4+ files, state machines, DB/API/UI integration, edge cases | 3 |

Instruction layers:

- `layer1`: goal and acceptance criteria.
- `layer2`: implementation approach, file locations, local patterns.
- `layer3`: edge cases, error handling, performance, recovery, and safety concerns.

## Analysis Template

`analysis.md` must cover:

- Task summary.
- Components, hooks, API queries/mutations, database integrations, UI integrations, services/business logic.
- Dependency graph.
- Risk assessment.
- TDD strategy and test execution order.
- Subtask summary with complexity, dependency, and agent/skill mapping.
- Verification checklist.

## Prompt Chain Contract

`prompt-chain.json` must use this structure:

```json
{
  "$schema": "sidechain-prompt-chain-v1",
  "taskId": "TASK-ID",
  "name": "Task Name",
  "description": "High-level task description",
  "complexity": 3,
  "tdd": true,
  "analysis": {
    "components": [],
    "hooks": [],
    "queries": [],
    "database": [],
    "ui": []
  },
  "subtasks": [
    {
      "id": "A1",
      "name": "Subtask Name",
      "complexity": 1,
      "agentType": "general-purpose",
      "instructions": {
        "layer1": "Primary goal and acceptance criteria"
      },
      "tdd": {
        "testFirst": "Description of test to write first",
        "testFile": "path/to/test.js",
        "testCommand": "bun test path/to/test.js",
        "implementation": "Brief implementation guidance"
      },
      "files": {
        "create": [],
        "modify": []
      },
      "dependencies": [],
      "outputs": []
    }
  ],
  "execution": {
    "order": ["A1"],
    "parallelizable": [],
    "checkpoints": [
      {
        "after": "A1",
        "verify": "Run tests, check types, update progress"
      }
    ]
  },
  "verification": {
    "finalTests": "bun run test",
    "typeCheck": "bun run lint",
    "acceptanceCriteria": []
  }
}
```

Use Bun commands for new sidechains by default. If the existing repo package scripts use npm, pnpm, or another runner, preserve the repo's current command style unless creating new Bun/Hono/Vite work from scratch.

## TDD Execution Contract

Every implementation subtask follows Red-Green-Refactor unless the task is explicitly docs-only:

1. RED: write the failing test described in the subtask.
2. Run the test and capture the expected failure.
3. GREEN: implement the minimum code to pass.
4. Run the test and capture the passing result.
5. REFACTOR: clean names, remove duplication, preserve behavior.
6. Run the subtask test again.
7. Update `progress.md` immediately with files touched, test output, skill outputs, and next step.

If TDD is not feasible, record why in `progress.md` and choose an alternate verification before coding.

## Progress Template

`progress.md` must track:

- Subtask table with TDD, implementation, and status.
- Execution log per subtask.
- Skill output captures in this format:

```text
### <SUBTASK-ID> — <skill> output
- Finding/decision:
- Recommendation:
- Action taken:
```

- Checkpoint results.
- Final verification.
- Errors encountered and resolution.
- Session summary and next resume point.

## Tech Stack Defaults

Use these defaults for new architecture unless current repo files override them:

- Backend: Bun runtime and Hono HTTP layer.
- Frontend: Vite + React.
- Language: plain JavaScript unless an existing package/module is already TypeScript.
- Styling: existing project system first; if creating a new UI surface, create or update a styleguide artifact before implementation.
- Data fetching: TanStack Query where the frontend consumes server state.
- Realtime: existing SSE/WebSocket conventions; do not invent a parallel channel.

## Execution Phases

1. Discovery: read governance, current implementation, tests, and docs.
2. Design lock: produce preparation packet and identify approvals.
3. Implementation: smallest coherent vertical slice.
4. Verification: run relevant tests and targeted drift searches.
5. Checkpoint: update progress and prepare review summary.
6. Handoff: list changed files, tests, open risks, and deferred items.

## Parallelization Rule

Parallelize only when write scopes are file-disjoint and the next local step is not blocked on the result. File-overlapping subtasks run sequentially. Any subagent/worker prompt must include:

- The owning sidechain subtask spec.
- Relevant governance file paths.
- The exact write scope.
- The instruction not to revert others' changes.
- Required test output before claiming completion.

## Autonomy Rule

Once the preparation packet is accepted or the user clearly asks to proceed, continue without asking for routine choices. Make conservative assumptions that preserve invariants and existing patterns. Stop only for hard-stop matrix items or new contradictions that could change the agreed behavior.
