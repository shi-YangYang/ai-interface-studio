# Development Handoff Contract

Use this after the UI/UX package is approved and before final delivery. Write the handoff contract inside `uiux-design.md`; do not create a competing source-of-truth document.

## Source Of Truth

Record this order in the final document:

1. `uiux-design.md` for exact requirements, copy, fields, permissions, states, and acceptance criteria
2. Frontend preview for approved interaction and responsive behavior
3. Design-system image and page mockups for visual direction
4. Generated bitmap microcopy for direction only

When artifacts conflict, update the lower-priority artifact or explicitly document the exception.

## Stable Identifiers

Use concise stable IDs when the project has multiple pages or flows:

- `REQ-###` for requirements
- `FLOW-###` for user or business flows
- `PAGE-###` for pages and routes
- `COMP-###` for shared components
- `STATE-###` for important states
- `AC-###` for acceptance criteria

Preserve IDs across revisions. Mark removed items as deprecated instead of silently reusing their IDs.

## Required Handoff Maps

### Traceability Map

Map each requirement or flow to its page, interaction, preview location, and acceptance criteria. Every critical requirement must be traceable end to end.

### Route And Page Map

For each page, record its stable ID, route or entry point, scroll model, coverage segments, permitted roles, upstream entry, downstream destination, and preview implementation path when one exists.

### Component Inventory

List shared components with their IDs, variants, states, owning pages, design-token dependencies, and reuse guidance. Distinguish global components from page-specific compositions.

### Interaction And State Matrix

For each important action, record trigger, precondition, local response, loading state, success state, empty state, error state, disabled state, permission-denied state, and next destination.

### UI Data Contracts

Describe view-facing data shapes: field name, type, meaning, required/optional status, example value, formatting, validation, and visibility rules. State clearly that these are UI contracts, not database schemas.

### API Capability Requirements

Describe only the capabilities future engineering must provide: consumer page or flow, operation, input, expected output, error cases, permission requirement, and freshness or pagination needs. Do not invent endpoint URLs, database tables, service boundaries, or infrastructure.

### Acceptance Criteria

Write observable criteria with stable `AC-###` IDs. Cover content, interaction, state changes, responsive behavior, accessibility, and role-sensitive behavior. Prefer Given/When/Then when it makes the result clearer.

## Preview-To-Production Guidance

If the production stack matches the preview, identify reusable routes, components, tokens, UI models, and mock service adapters. Keep fixtures and mock operations outside visual components so future developers can replace them cleanly.

If the stack differs, treat the preview as an executable behavioral and visual reference. Reimplement from `uiux-design.md` instead of mechanically translating framework code.

Never describe the preview as production-ready. Backend architecture, persistence, real authentication, integrations, deployment, security hardening, and operations remain outside this skill.

## Final Checks

- Every confirmed page has a `PAGE-###` entry.
- Every `page-scroll` page has a complete ordered section list and coverage segments for its top, middle, and bottom content.
- Every critical flow reaches at least one acceptance criterion.
- Every preview route maps back to the design document.
- Mock data is distinguishable from production data requirements.
- API capability needs describe outcomes without prescribing backend architecture.
- Known gaps and assumptions are explicit.
