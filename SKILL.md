---
name: one-shot
description: "Enforce one-shot product execution for any app: deep preparation, plan locking, autonomous implementation, checkpoint review, anti-drift cleanup, hallucination checks, frontend styleguides, and polished handoff. Use when an agent should answer core questions up front, lock decisions, then execute with autonomy except for hard-stop approvals."
---

# One Shot

Use this skill as a product-execution governance orchestrator. It does not replace specialist skills; it decides which governance phase is active, which reference to load, which existing local skills to invoke when available, and where hard-stop approval is required.

Default stack assumptions for new app work: Bun + Hono backend, Vite + React frontend, plain JavaScript unless the repo already says otherwise. Prefer existing project patterns over introducing new frameworks.

## Operating Model

1. Read the active governance layer before planning: project instructions such as `CLAUDE.md`, `CLAUDE.local.md`, `AGENTS.md`, `.cursorrules`, current sidechain `progress.md`, and any local `task_plan.md`, `analysis.md`, `spec.md`, or `findings.md` relevant to the request.
2. Classify the work as one of: sidechain creation, sidechain execution, checkpoint/review, code cleanup, frontend/design, safety/threat-model, or planning-only.
3. Load only the relevant reference files:
   - Sidechain creation or major planning: `references/sidechain-creation-walkthrough.md`
   - Original sidechain skill source: `references/source-sidechain-skill.md`
   - Readiness gate: `references/definition-of-ready.md`
   - Approval gates: `references/hard-stop-matrix.md`
   - Phase autonomous execution: `references/pax-protocol.md`
   - Checkpoint or review: `references/checkpoint-ritual.md`
   - Drift cleanup or review: `references/anti-drift-review.md`
   - Claims verification: `references/hallucination-checks.md`
   - Decision capture: `references/decision-record-template.md`
   - App-specific governance writing: `references/governance-writer.md`
   - Risk planning: `references/risk-register-template.md`
   - Test planning: `references/test-strategy-matrix.md`
   - Specialist skill execution details: `references/specialist-skill-playbooks.md`
   - UI/frontend work: `references/frontend-styleguide-workflow.md` and `assets/styleguide-template.md`
   - UI QA: `references/ui-qa-checklist.md`
   - Subagent/delegation: `references/subagent-prompt-template.md`
   - Completion gate: `references/definition-of-done.md`
   - Handoff: `references/final-report-template.md`
4. Build a preparation packet before implementation. The packet should answer the core questions, resolve ambiguities, define success criteria, and pass `references/definition-of-ready.md`. Do not start coding while core questions remain open unless the user explicitly approves proceeding with a named assumption.
5. After decisions are made and the plan is laid out, use `references/governance-writer.md` to create app-specific execution governance. Review it for enforceability before implementation.
6. Execute with high autonomy after preparation/governance is accepted or clearly implied: make scoped changes, run relevant tests, update progress/checkpoints, and report only hard stops or unexpected fringe cases.
7. Never weaken repo invariants, product contracts, safety rules, or user-approved design direction to complete a task. If a request conflicts with locked governance, stop and surface the conflict with file/line evidence.

## Specialist Skill Routing

Invoke matching local skills when available. If a named skill is unavailable, follow the corresponding reference here as fallback.

- Phase autonomous execution: `pax-protocol` when available, otherwise `references/pax-protocol.md`
- Architecture decisions: `senior-architect`
- Clean implementation/refactor: `solid`
- Modularization review: `code-modularization-evaluator`
- Backend data/pipeline/state persistence: `senior-data-engineer`
- WebSocket/realtime: `websocket-engineer`
- Risk/caps/trading safety: `risk-management`
- Hyperliquid signing/exchange semantics: `hyperliquid`
- React server-state/data fetching: `tanstack-query-best-practices`
- Frontend quality: `design-taste-frontend`, `high-end-visual-design`, `mobile-responsiveness`, `redesign-existing-projects`

Do not assume Claude and Codex have identical skill paths. Refer to skills by capability/name and degrade gracefully to `references/specialist-skill-playbooks.md`.

## Core Preparation Questions

Before sidechain creation or substantial execution, answer these explicitly:

- What is the user-visible or operator-visible outcome?
- Which governance files are authoritative for this task?
- Which invariants can be touched, and which are out of bounds?
- What files/modules are in scope, and which are explicitly out of scope?
- What current behavior is being preserved?
- What new behavior is being introduced?
- What are the acceptance criteria?
- What tests or checks prove the work?
- What docs/checkpoints must be updated?
- What approval gates may be encountered?
- What failure modes would cause a hard stop?
- For frontend work: what styleguide, interaction, responsive, and animation rules will govern the UI?

Use `references/sidechain-creation-walkthrough.md` for the full planning checklist and `references/definition-of-ready.md` before implementation.

## Hard-Stop Rule

Stop for approval at major decision points listed in `references/hard-stop-matrix.md`. In all other cases, continue autonomously using conservative repo-aligned assumptions and record the assumption in the progress/checkpoint output.

Hard stops include sidechain activation, locked-plan changes, safety/security/privacy changes, production data or money movement, destructive git operations, dependency additions, schema-contract ambiguity, checkpoint acceptance, and design direction changes that would materially alter the user-approved product.

## Output Discipline

For planning, produce a concise preparation packet with decisions, assumptions, gates, and verification plan.

For implementation, produce a final summary with changed files, tests run, residual risks, and any checkpoint/progress updates. Mention unrelated dirty worktree files only when they affect the task.

For checkpoint review, lead with pass/fail findings and required corrections before summaries.

Before final response, run `references/definition-of-done.md` and shape the handoff with `references/final-report-template.md`.
