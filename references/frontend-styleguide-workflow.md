# Frontend Styleguide Workflow

Use this reference when a sidechain creates or changes a frontend surface.

## Styleguide First

Before implementation, create or update a styleguide artifact using `assets/styleguide-template.md`. Keep it close to the feature, for example:

- `docs/design/<feature>-styleguide.md`
- or sidechain planning output when the design is not yet committed.

## Required Decisions

Answer:

- Who is the primary user: operator, admin, trader, reviewer, or visitor?
- What task must be fastest?
- What data must be scannable at a glance?
- Which states exist: loading, stale, healthy, warning, blocked, error, empty?
- What mobile behavior is required?
- What interactions or animations clarify state instead of decorating it?
- Which existing components must be reused?
- What colors, typography, spacing, and density match the product domain?

## Design Defaults

For TimeMachineV9 operational tools:

- Prefer dense, quiet, work-focused layouts.
- Avoid marketing hero patterns for dashboards/tools.
- Use constrained panels, tables, tabs, segmented controls, icons, toggles, sliders, and clear state badges.
- Keep cards for repeated items or tool frames, not nested page sections.
- Use motion to clarify transitions, live updates, or causality. Avoid ornamental motion.
- Ensure text fits on mobile and desktop.

## Frontend Stack

- Vite + React.
- Use existing project CSS/component conventions first.
- Use TanStack Query for server state when applicable.
- Do not replicate backend safety logic in the frontend. Frontend may communicate status and disable controls for UX, but backend remains authoritative.

## Verification

Run relevant frontend tests/builds and inspect responsive behavior when feasible. For visual work, include screenshots or precise observations in the checkpoint when tooling allows.
