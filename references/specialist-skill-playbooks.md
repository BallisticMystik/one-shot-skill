# Specialist Skill Playbooks

Use this reference when the local specialist skill is unavailable or when `one-shot` needs a portable summary of how to route specialist work. These are compressed execution rules derived from the local skills named by the operator.

## `solid`

Use for any code, refactor, debugging, architecture, review, or tests.

Mandatory rules:

- Prefer TDD: RED, GREEN, REFACTOR.
- Keep changes simple and directly tied to user value.
- Apply SOLID principles: single responsibility, open/closed, substitutability, interface segregation, dependency inversion.
- Use clear, searchable domain names.
- Avoid speculative abstractions; wait for real duplication.
- Validate with tests before claiming success.

## `tanstack-query-best-practices`

Use for React server-state/data fetching.

Rules:

- Query keys are arrays and include every variable dependency.
- Organize keys hierarchically or through query-key factories.
- Set `staleTime` and cache retention based on data volatility.
- Prefer targeted invalidation after mutations.
- Use optimistic updates only with rollback context.
- Handle loading, empty, error, and pending mutation states.
- Use `select` to transform query data without extra render churn.

## `websocket-engineer`

Use for realtime, WebSocket, SSE-adjacent, pub/sub, live updates, presence, rooms, and reconnection behavior.

Rules:

- Define connection lifecycle: connecting, connected, stale, reconnecting, disconnected.
- Authenticate before event access.
- Scope broadcasts by session/user/room; never broadcast sensitive data globally.
- Include heartbeat or stale detection.
- Implement reconnect/backoff and cleanup.
- Track metrics: connection count, latency, errors, dropped/stale events.
- For TimeMachineV9, preserve existing SSE/WebSocket conventions and backend source-of-truth rules.

## `mobile-ux-optimizer`

Use for responsive/mobile/touch/viewport work.

Rules:

- Build mobile-first and scale up.
- Use `100dvh`/`min-height: 100dvh`, not brittle `100vh`.
- Respect safe-area insets.
- Minimum touch targets: 44px/48px.
- Avoid horizontal scroll from asymmetric desktop layouts.
- Use bottom nav/drawers/hamburger patterns only when they improve task speed.
- Test text fit, tap spacing, loading/error states on narrow viewports.

## `high-end-visual-design`

Use for premium visual language, motion, and micro-interaction design. For TimeMachineV9 operational dashboards, temper agency-style expressiveness with operator clarity.

Rules:

- Avoid generic AI defaults: oversaturated purple/blue gradients, default Inter-only typography, generic equal-card grids, generic shadows.
- Use deliberate typography, color, spacing, and materiality.
- Use motion only through `transform` and `opacity`; avoid layout-triggering animation.
- Provide hover, active, focus, loading, empty, and error states.
- Avoid ornamental animation that obscures operational data.

## `design-taste-frontend`

Use for frontend architecture and anti-slop UI execution.

Rules:

- Verify dependencies before importing third-party libraries.
- Use existing React/Vite project conventions.
- Use CSS Grid for reliable layouts.
- Avoid `h-screen`; use `min-h-[100dvh]`.
- Use semantic HTML and accessible states.
- For dashboards, use dense, quiet hierarchy rather than marketing composition.
- Keep animations GPU-safe.

## `redesign-existing-projects`

Use for improving an existing UI without rewriting from scratch.

Rules:

- Scan framework/styling first.
- Diagnose weak typography, color, layout, states, content, iconography, and code quality.
- Apply targeted upgrades only.
- Preserve existing functionality and data flow.
- Replace generic cards, centered layouts, poor empty/error/loading states, and dead links.

## `code-modularization-evaluator`

Use after architecture-sensitive implementation or before module refactors.

Evaluate:

- Integration strength: intrusive, functional, model, contract.
- Distance: same file, module, subsystem, service, external system.
- Volatility: how often the coupled concepts change.
- Connascence: name, type, meaning, position, algorithm, execution, timing, value, identity.

Rule: high-strength coupling should stay close; low-strength coupling can be distant. Avoid both distributed monoliths and needless local abstractions.

## `architecture-blueprint-generator`

Use for architectural documentation, blueprinting, and consistency guides.

Output should cover:

- Detected stack and architecture pattern.
- Component boundaries and dependency directions.
- Data flow and cross-cutting concerns.
- Implementation patterns and extension points.
- Decision records when architecture choices are made.

## `senior-architect`

Use for major technical decisions, system design, scalability, dependency analysis, ADRs, and diagrams.

Expected output:

- Options considered.
- Tradeoffs and risks.
- Recommended decision.
- Boundaries and contracts.
- Mermaid/ASCII diagram when useful.
- Migration and verification plan.
