# Governance Writer

Use this after decisions are made and the plan is laid out, but before implementation. The goal is to write strong, app-specific execution governance so future agents know how to build the app without drifting, over-asking, or inventing semantics.

This is an add-on phase inside `one-shot`, not a generic CLAUDE.md rewrite. It should produce governance for the specific app, feature, sidechain, or execution lane being built.

## When To Use

Use when:

- Starting a new app or major feature.
- Creating a sidechain.
- A plan has multiple phases or agents.
- The product has safety, privacy, auth, payment, realtime, data, or UX correctness concerns.
- The user wants high autonomy after initial planning.

Skip when:

- The task is a tiny bug fix.
- Existing governance already covers the exact execution lane.
- The user explicitly asks for implementation only and no new process layer is needed.

## Inputs

Read:

- Preparation packet.
- Decision records.
- Risk register.
- Test strategy.
- Product/design brief or styleguide.
- Existing project governance files.
- Existing architecture/code patterns.

## Output Location

Choose the narrowest durable location:

- New app/project-wide rules: `AGENTS.md`, `CLAUDE.md`, or equivalent project instruction file.
- Sidechain-specific rules: planning directory `governance.md` or `CLAUDE.local.md` block when the repo already uses that pattern.
- Feature-specific rules: `docs/governance/<feature>.md` or sidechain `progress.md` locked-decision section.
- UI-specific rules: styleguide/design doc.

Stop for approval before modifying an existing global governance file unless the user already asked for it.

## Governance Sections

Write only sections that apply:

1. **Project Identity**
   - What is being built.
   - Primary users.
   - Critical workflows.
   - Non-goals.

2. **Tech Stack And Defaults**
   - Backend/runtime/framework.
   - Frontend/framework.
   - Styling/design system.
   - Data/storage.
   - Testing tools.
   - Dependency policy.

3. **Hard Invariants**
   - Rules that must never be violated.
   - Keep these concrete and enforceable.
   - Tie each invariant to code/docs/tests where possible.

4. **Architecture Boundaries**
   - Module ownership.
   - Allowed dependency directions.
   - API/data contracts.
   - Realtime/event boundaries.
   - Frontend/backend authority boundaries.

5. **Execution Workflow**
   - Planning artifacts.
   - TDD expectations.
   - Checkpoint cadence.
   - Progress update format.
   - Review requirements.

6. **Hard Stops**
   - Approval gates from `hard-stop-matrix.md`, narrowed to this app.
   - Include examples of what does and does not require approval.

7. **Quality Gates**
   - Tests/build/lint.
   - UI QA.
   - Security/privacy checks.
   - Documentation and drift checks.

8. **Design Governance**
   - Styleguide source of truth.
   - Color/typography/motion constraints.
   - Accessibility/responsive rules.
   - Product voice/content rules.

9. **Handoff And Done**
   - Definition of done.
   - Final report expectations.
   - Deferred item policy.

## Governance Quality Bar

Good governance is:

- Specific to this app.
- Enforceable by tests, review, or grep.
- Short enough to be read every session.
- Clear about authority and precedence.
- Conservative where user trust, data, money, auth, safety, or production stability is involved.
- Flexible where implementation details are low-risk.

Bad governance:

- Generic best-practice filler.
- Huge walls of advice no agent will follow.
- Rules without enforcement surfaces.
- Contradictions with existing code.
- Multiple semantic paths for the same behavior.
- Silent scope expansion.

## Governance Review Pass

After drafting governance, run this review before implementation:

- Does every hard invariant have a reason?
- Can an agent tell what files/docs/tests to check?
- Are approval gates clear enough to prevent over-asking and under-asking?
- Does it preserve project stack consistency?
- Does it leave enough autonomy for routine implementation?
- Does it avoid app-specific assumptions that are not in the plan?
- Does it conflict with existing governance?

If the governance changes global project behavior, present it for approval. If it only records already-approved sidechain/feature execution rules, proceed and note it in progress.

## Template

```markdown
# <App/Feature> Execution Governance

**Status:** proposed | approved | active
**Scope:** <app/feature/sidechain>
**Source decisions:** <links/files>

## Project Identity

## Tech Stack And Defaults

## Hard Invariants

1. ...

## Architecture Boundaries

## Execution Workflow

## Hard Stops

## Quality Gates

## Design Governance

## Done And Handoff
```
