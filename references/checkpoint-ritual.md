# Checkpoint Ritual

Use this reference for phase close, progress review, checkpoint acceptance, or when context has compacted. It folds in the local `/checkpoint` skill: Record, Review, Reflect, Reduce, Present, Refactor, Resume.

## When To Run

Run a checkpoint when:

- A batch of sidechain subtasks completed.
- The working context was compacted.
- The user asks for status/review/pause.
- Plan-code drift is suspected.
- A new phase changes scope.
- A bug or rule violation suggests earlier planning missed something.

Skip for single small bug fixes or one-shot tasks under roughly 30 minutes unless governance requires it.

## Phase 1: Record

Reload facts before judgment.

Read:

- `task_plan.md`, `progress.md`, `findings.md` in the project planning folder when present.
- Active sidechain `progress.md` and `prompt-chain.json`.
- `CLAUDE.md` and `CLAUDE.local.md` if present.
- `git log --oneline -20`.
- `git status --short`.
- Relevant test/lint output.

Output: one factual "we are here" paragraph with timestamp appended to `progress.md`.

## Phase 2: Review

Investigate what the live build actually looks like.

Check:

- Line counts against governance targets.
- Test count and changed test coverage.
- `TODO`, `FIXME`, hardcoded constants, stale comments.
- Module wiring: imports, renders, route registration, dead imports.
- Dead code: symbols that lost callers.
- Data flow: correct scoping, source of truth, no duplicate semantic path.
- Deploy/runtime verification if backend or realtime behavior changed.

Output: raw findings with file paths and line numbers where possible.

## Phase 3: Reflect

Interpret findings and surface decisions.

Ask yourself:

- Does any finding violate `CLAUDE.md`, `CLAUDE.local.md`, or sidechain governance?
- Did code silently overturn a locked decision?
- Did ambiguity reappear where governance requires one path?
- What will bite the next batch?
- What did the plan assume existed but does not?

Ask the user only for decisions that require their input. Capture answers as locked decisions in the appropriate planning artifact.

Output: rule violations, user questions, and captured decisions.

## Phase 4: Reduce

Compress findings into an ordered action list:

1. Fix deviations from hard rules.
2. Purge legacy/dead/stale code.
3. Debug real bugs.
4. Reposition code/docs to match updated understanding.
5. Add new work only after the above.

Every action needs a reason rooted in Record/Review/Reflect.

## Phase 5: Present

Present only forward-looking new-work items as task cards for explicit user selection. Do not ask permission for required fix-deviation, purge, debug, or reposition items unless they trigger the hard-stop matrix.

Task card fields:

- Name.
- Scope.
- Effort estimate.
- Dependencies.
- Recommended order.
- Open sub-decisions.

Wait for the user's selection when new work is material or ordering/scope could change.

Skip Present only when no new-work items exist or all are trivial continuations. Record the skip explicitly in `progress.md`.

## Phase 6: Refactor

Splice the action list into the sidechain:

- Few independent items: prepend to current batch.
- Coherent block of 3+ related items: create a new sidechain block with `analysis.md`, `prompt-chain.json`, and `progress.md`, and reference it from parent progress as a prerequisite.
- Preserve TDD gates.
- Update parent plan/decision log if architecture changed.

Output: plan and sidechain agree with reality.

## Phase 7: Resume

Choose:

- Immediate: start the next refreshed sidechain item.
- Handoff: write a "next session starts here" note in `progress.md`.

If context is over 70% full or Refactor created a materially new direction, write a handoff note and clear/reload only between Refactor and Resume. Never clear before Reflect/Present.

## Checkpoint Inputs Summary

Minimum input set:

- Governance files.
- Active sidechain artifacts.
- Recent commits and worktree status.
- Test/lint/build outputs.

## Review Questions

- Does the checkpoint claim match actual code and docs?
- Are all acceptance criteria satisfied?
- Were required skills/gates used?
- Did any hard-stop trigger get bypassed?
- Did tests run, and are exact results recorded?
- Are docs, threat model, and decision records synchronized with code?
- Are unrelated dirty files clearly separated?
- Is there a deferred item for every known non-blocking gap?

## Output

Lead with findings:

```text
Checkpoint verdict: pass | needs correction | blocked
Findings:
- Severity: file/path:line — issue and required correction.
Required approvals:
- ...
Verified:
- command -> result
Residual risk:
- ...
```

Do not mark a phase complete if any required approval, safety gate, or verification is missing.

## Output Contract

Every checkpoint must produce:

1. Updated `progress.md` with timestamp, Record paragraph, rule violations, user questions/answers, and sidechain link.
2. Updated sidechain or explicit "no sidechain update needed" note.
3. Explicit Resume line: next action and whether context should clear/reload.

If any of these are missing, the checkpoint is incomplete.

## Reboot Test

A fresh session must be able to answer from planning files alone:

- What shipped since the last checkpoint?
- What must be fixed before new work?
- What open questions were closed?
- What is the next task?
- Did we violate a rule, and how was it handled?
