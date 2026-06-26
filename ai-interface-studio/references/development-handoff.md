# Development Handoff Contract

Use this after the UI/UX package is approved and before final delivery. Write the handoff contract inside `uiux-design.md`; do not create a competing source-of-truth document.

## Source Of Truth

Use domain-specific precedence instead of one total ordering:

- User-approved decisions and documented exceptions override earlier artifacts.
- `uiux-design.md` governs requirements, exact copy, fields, permissions, states, behavior, and acceptance criteria.
- Approved design-system image governs palette, typography scale, spacing rhythm, shell language, component appearance, and density. Approved page mockups plus the visual-fidelity contract govern page composition, hierarchy, section order, and workflow structure.
- The approved frontend implementation strategy governs preview framework, UI library, styling system, charting/drawing/3D libraries, supporting assets, and custom component choices.
- The reference reconstruction map governs which visible elements and effects must appear in the preview.
- The accepted frontend preview demonstrates behavior and responsive implementation after visual review.
- Generated bitmap microcopy remains directional only.

When behavioral and visual sources conflict, the coordinator must record a decision. The implementation agent must not silently choose the easier interpretation.
When visual review returns code defects, the coordinator records the decision and delegates the fix. The coordinator must not patch preview code or assets.

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

For each page, record its stable ID, route or entry point, scroll model, coverage strategy, reference mockups, permitted roles, upstream entry, downstream destination, and preview implementation path when one exists.

### Component Inventory

List shared components with their IDs, variants, states, owning pages, implementation method, design-token dependencies, and reuse guidance. Distinguish global components from page-specific compositions.

### Interaction And State Matrix

For each important action, record trigger, precondition, local response, loading state, success state, empty state, error state, disabled state, permission-denied state, and next destination.

### UI Data Contracts

Describe view-facing data shapes: field name, type, meaning, required/optional status, example value, formatting, validation, and visibility rules. State clearly that these are UI contracts, not database schemas.

### API Capability Requirements

Describe only the capabilities future engineering must provide: consumer page or flow, operation, input, expected output, error cases, permission requirement, and freshness or pagination needs. Do not invent endpoint URLs, database tables, service boundaries, or infrastructure.

### Acceptance Criteria

Write observable criteria with stable `AC-###` IDs. Cover content, interaction, state changes, responsive behavior, accessibility, and role-sensitive behavior. Prefer Given/When/Then when it makes the result clearer.

### Visual Fidelity Evidence

For every implemented `PAGE-###`, link the approved mockup, exact viewport, browser screenshot, full-page screenshot when the page scrolls, relevant `VIS-###` findings, and final pass status. Keep `visual-review.md` as review evidence, not a competing design specification.

## Preview-To-Production Guidance

If the production stack matches the preview, identify reusable routes, components, tokens, UI models, and mock service adapters. Keep fixtures and mock operations outside visual components so future developers can replace them cleanly.

If the stack differs, treat the preview as an executable behavioral and visual reference. Reimplement from `uiux-design.md` instead of mechanically translating framework code.

Never describe the preview as production-ready. Backend architecture, persistence, real authentication, integrations, deployment, security hardening, and operations remain outside this skill.

## Final Checks

- Every confirmed page has a `PAGE-###` entry.
- Every `page-scroll` page has a complete ordered section list, exactly one approved vertical long-page mockup, and a recorded image-to-browser scale contract.
- Every critical flow reaches at least one acceptance criterion.
- Every preview route maps back to the design document.
- Every implemented page has a frozen visual-fidelity contract.
- Every implemented page is covered by an approved frontend implementation strategy, visual technology map, and reference reconstruction map.
- Every implemented page has same-viewport reference and browser screenshot evidence; every implemented `page-scroll` route also has full-page screenshot evidence.
- Any blocker or major repair was performed by the Frontend Implementation Agent or an assigned Frontend Repair Agent, not by the coordinator.
- The final visual review was performed by an agent that did not implement the preview, or the sequential fallback limitation is disclosed.
- No blocker or major `VIS-###` finding remains open.
- Mock data is distinguishable from production data requirements.
- API capability needs describe outcomes without prescribing backend architecture.
- Known gaps and assumptions are explicit.
