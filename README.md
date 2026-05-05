# One Shot

`one-shot` is a portable execution-governance skill for AI coding agents. It is designed for situations where you want the agent to do the hard thinking up front, lock the plan, write app-specific governance, then execute with high autonomy while stopping only at meaningful approval gates.

The skill works for any application build, not just financial or trading systems. It is especially useful for multi-phase app development, sidechain-style planning, major refactors, frontend product work, realtime systems, security-sensitive changes, and any project where plan drift or shallow execution would be expensive.

## What It Does

`one-shot` turns a vague or ambitious request into a disciplined execution lane:

1. Discover the project and governance context.
2. Ask and answer the core product, architecture, risk, test, and UX questions.
3. Create a readiness packet before coding.
4. Capture decisions and risks.
5. Write app-specific governance for the execution lane.
6. Execute autonomously once the plan is ready.
7. Stop only for hard approvals or unexpected fringe cases.
8. Run checkpoint and anti-drift reviews.
9. Produce a polished final handoff.

It is not a replacement for specialist skills. It is an orchestrator that decides when to use specialist guidance and how to keep the work coherent.

## When To Use

Use `one-shot` when you want an agent to:

- Build a new app or major feature.
- Create a sidechain or multi-phase implementation plan.
- Execute a locked plan with autonomy.
- Prepare governance before implementation.
- Refactor or clean up code without drifting from product intent.
- Review checkpoint status and compress findings into next actions.
- Add or revise frontend UI with a styleguide and QA checklist.
- Work across backend, frontend, data, realtime, and UX boundaries.
- Avoid hallucinated claims and unsupported “done” summaries.

Skip it for tiny one-file fixes where a normal edit/test/final loop is enough.

## Default Stack Assumptions

For new app work, `one-shot` assumes:

- Backend: Bun + Hono
- Frontend: Vite + React
- Language: plain JavaScript unless the repo already uses TypeScript
- UI: existing project conventions first, then a feature-specific styleguide

If an existing repo uses another stack, the skill instructs the agent to follow the repo instead of forcing these defaults.

## Install

Copy this repository into a skills directory supported by your agent.

Example Codex-style layout:

```text
~/.codex/skills/one-shot/
  SKILL.md
  agents/openai.yaml
  assets/
  references/
```

Example Claude-style layout:

```text
~/.claude/skills/one-shot/
  SKILL.md
  agents/openai.yaml
  assets/
  references/
```

You can also keep it repo-local:

```text
<project>/.agents/skills/one-shot/
```

Repo-local installation is useful when the governance model should travel with a project.

## Invocation

Typical prompts:

```text
Use one-shot to plan and execute this feature.
```

```text
Use one-shot to create a sidechain for the new dashboard workflow.
```

```text
PAX Phase 1 with one-shot once the plan is ready.
```

```text
Use one-shot to review this checkpoint and tell me what needs correction.
```

```text
Use one-shot to create app-specific governance after we lock these decisions.
```

The skill also supports explicit PAX-style phase execution when a phase spec is already locked.

## Core Workflow

### 1. Discovery

The agent reads available project instructions and planning artifacts, such as:

- `CLAUDE.md`
- `CLAUDE.local.md`
- `AGENTS.md`
- `.cursorrules`
- `task_plan.md`
- `analysis.md`
- `spec.md`
- `findings.md`
- `progress.md`
- existing source code and tests

For projects without these files, the agent builds a minimal governance context from package files, source layout, user request, and existing patterns.

### 2. Definition Of Ready

Before coding, the agent must prove the work is ready:

- Objective is concrete.
- Scope and non-scope are explicit.
- Acceptance criteria are testable.
- Current behavior and proposed behavior are known.
- Risks and hard stops are listed.
- Test strategy is chosen.
- UI work has a styleguide path when applicable.
- Open questions are either answered or explicitly approved as assumptions.

See `references/definition-of-ready.md`.

### 3. Decision And Risk Capture

The skill includes templates for:

- decision records
- risk registers
- test strategy selection
- hard-stop approvals

These keep future agents from reviving rejected paths or silently changing assumptions.

### 4. Governance Writer

After decisions are made and the plan is laid out, `one-shot` can write app-specific governance for that execution lane.

Examples:

- project-wide `AGENTS.md`
- feature-specific `docs/governance/<feature>.md`
- sidechain `governance.md`
- design governance inside a styleguide

The governance writer is meant to be specific, enforceable, and short enough to be read every session.

See `references/governance-writer.md`.

### 5. Sidechain Planning

For complex work, `one-shot` folds in a sidechain-style process:

- analyze components, hooks, APIs, database, UI, services
- rate each subtask complexity 1-3
- create `prompt-chain.json`
- require TDD per implementation subtask
- update `progress.md` as work lands
- checkpoint at phase boundaries

See `references/sidechain-creation-walkthrough.md`.

### 6. PAX Phase Autonomous Execution

PAX means Phase Autonomous Execution.

When a phase is locked and the user says something like `PAX P1` or `engage Phase 1`, the agent executes the whole phase without per-subtask approvals. It still stops for hard-pause triggers such as:

- spec contradiction
- security/privacy/payment/auth changes
- destructive git operations
- tests still red after one focused retry
- dependency additions
- global governance changes
- material product/design direction changes

See `references/pax-protocol.md`.

### 7. Checkpoint Ritual

At natural boundaries, the agent runs the checkpoint ritual:

1. Record
2. Review
3. Reflect
4. Reduce
5. Present
6. Refactor
7. Resume

This catches drift, stale docs, missing tests, dead code, and silent decision changes.

See `references/checkpoint-ritual.md`.

### 8. Definition Of Done

Before handoff, the agent checks:

- acceptance criteria
- tests/builds/lints
- docs and decisions
- drift search
- UI QA
- risks and deferred items
- unrelated dirty worktree files
- final report quality

See `references/definition-of-done.md`.

## Reference Map

| File | Purpose |
|---|---|
| `SKILL.md` | Top-level routing and operating model |
| `references/definition-of-ready.md` | Pre-implementation readiness gate |
| `references/definition-of-done.md` | Completion gate |
| `references/sidechain-creation-walkthrough.md` | Sidechain analysis, complexity, prompt-chain, TDD |
| `references/source-sidechain-skill.md` | Markdown export of the original `/sidechain` skill source |
| `references/checkpoint-ritual.md` | Seven-phase checkpoint process |
| `references/pax-protocol.md` | Phase-autonomous execution rules |
| `references/governance-writer.md` | App-specific governance generation |
| `references/hard-stop-matrix.md` | Approval gates |
| `references/anti-drift-review.md` | Drift search and correction rules |
| `references/hallucination-checks.md` | Claim verification rules |
| `references/decision-record-template.md` | Decision record format |
| `references/risk-register-template.md` | Risk register format |
| `references/test-strategy-matrix.md` | Choosing the right tests |
| `references/ui-qa-checklist.md` | Frontend QA checks |
| `references/frontend-styleguide-workflow.md` | UI styleguide workflow |
| `references/specialist-skill-playbooks.md` | Portable summaries of specialist skills |
| `references/subagent-prompt-template.md` | Delegation prompt template |
| `references/final-report-template.md` | Final handoff formats |
| `assets/styleguide-template.md` | Reusable styleguide template |

## Specialist Skill Routing

`one-shot` can call or emulate specialist skills, including:

- `solid`
- `senior-architect`
- `architecture-blueprint-generator`
- `code-modularization-evaluator`
- `tanstack-query-best-practices`
- `websocket-engineer`
- `mobile-ux-optimizer`
- `design-taste-frontend`
- `high-end-visual-design`
- `redesign-existing-projects`
- `pax-protocol`

If the actual specialist skill is not installed, `one-shot` uses `references/specialist-skill-playbooks.md` as a fallback.

## Hard Stops

The agent must stop and ask for approval when the work would cross meaningful boundaries, including:

- new dependency or framework
- destructive git operation
- production-visible external action
- security/privacy/auth/payment changes
- schema or API contract ambiguity
- global governance changes
- material UX/product direction changes
- locked-plan contradiction
- tests still red after one focused retry

The goal is not to ask more questions. The goal is to ask only the questions that actually matter.

## Frontend Product Quality

For UI work, `one-shot` requires:

- styleguide decisions before implementation
- color swatches
- typography scale
- responsive rules
- animation and motion constraints
- loading, empty, error, stale, disabled, and success states
- mobile QA
- accessibility and focus checks

This makes the result feel like a considered product, not just working components.

## Updating The Skill

After editing the skill, validate it:

```bash
python <path-to-skill-creator>/scripts/quick_validate.py <path-to-one-shot>
```

For this repository, the expected structure is:

```text
SKILL.md
agents/openai.yaml
assets/styleguide-template.md
references/*.md
```

Do not add unrelated documentation files unless they directly support the skill.

## Design Philosophy

`one-shot` is built around a simple operating principle:

> Answer almost everything before execution, then let the agent run with autonomy until a real approval gate appears.

It is intentionally rigorous because shallow planning creates expensive drift. The skill aims to make thorough execution repeatable across any app build.
