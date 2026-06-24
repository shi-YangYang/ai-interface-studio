# Interactive Frontend Preview

Use this only after the UI/UX package is approved and the user requests a browser-ready preview. The preview is a design prototype, not a full-stack application.

The frontend implementation agent owns this stage. It must be separate from the coordinator and visual acceptance agent.

## Entry Gate

Do not write preview code until all of these exist:

- User-approved design-system image and page mockups
- Complete `uiux-design.md`
- A frozen visual-fidelity contract for every route in scope
- Exact reference viewport for every mockup
- Coordinator-provided route and ownership scope

The implementation agent must open and inspect the original images before editing. A textual summary is not a substitute.

## Scope Boundary

Build only the frontend experience needed to review the approved product direction.

Allowed:

- Routes and navigation between approved screens
- Responsive desktop and mobile layouts
- Forms, filters, tables, tabs, dialogs, drawers, charts, and status changes
- Mock data, fixtures, local component state, and browser storage when helpful
- Stubbed submit, upload, search, approval, and notification interactions
- Loading, empty, error, disabled, selected, and permission-limited demonstration states

Do not build:

- Backend servers or API endpoints
- Databases, migrations, or persistent data models
- Real authentication, authorization providers, or account systems
- Payments, email delivery, messaging infrastructure, or external service integrations
- Cloud resources, deployment pipelines, monitoring, or production operations
- Production security claims or production-ready business logic

## Default Stack

Prefer the existing repository stack if there is one. If the target project is empty and the user does not specify a stack, create the preview in `frontend-preview/<project-slug>/` with:

- React
- Vite
- Tailwind CSS
- lucide-react for icons

## Build Rules

- Treat `uiux-design.md` as authoritative for requirements, exact copy, fields, states, permissions, and behavior.
- Treat approved mockups and their visual-fidelity contracts as authoritative for shell geometry, page composition, visual hierarchy, palette, typography scale, spacing, component appearance, and density.
- Treat generated bitmap microcopy as directional only. Do not weaken the visual composition because small generated text is uncertain.
- Implement real HTML/CSS components rather than embedding the bitmap mockups as the UI.
- Build the first screen as the actual app surface, not a marketing landing page.
- Implement the shared application shell first and capture a matching-viewport screenshot before building all pages.
- Work in small page batches. Do not implement the complete preview in one unreviewed pass.
- Implement the complete confirmed content order for every `page-scroll` route, not only the first viewport represented by its top mockup.
- Implement the confirmed routes and interactions with mock data and local state.
- Make key actions visibly respond, but keep network operations stubbed.
- Include expected states where feasible: empty, loading, error, disabled, selected, and permission-limited.
- Keep dashboard and admin surfaces dense, scannable, and work-focused.
- Use stable dimensions for boards, toolbars, cards, tables, icon buttons, and counters so interactions do not resize the layout.
- Use lucide icons for common actions and tool buttons when available.
- Do not replace distinctive approved components with generic cards, tables, navigation, or dashboard patterns merely because they are easier to implement.
- Record any technically necessary deviation and wait for coordinator approval before treating it as accepted.
- Do not add backend dependencies or present placeholder integrations as real.

## Handoff-Friendly Structure

When the existing project does not already define an equivalent structure, separate concerns like this:

```text
src/
├── components/       shared visual components
├── pages/            route-level page compositions
├── routes/           navigation and route definitions
├── data/fixtures/    mock records and scenarios
├── services/mock/    stubbed operations used by the UI
├── types/            UI-facing data contracts
└── styles/tokens/    colors, typography, spacing, and component tokens
```

- Map route-level pages to the `PAGE-###` IDs in `uiux-design.md`.
- Keep fixtures out of visual components.
- Put mock operations behind replaceable adapters instead of calling imaginary endpoints.
- Reuse the same UI data field names documented in the handoff contract.
- Record the preview path for every implemented route in the final traceability map.

## Verification

- Start the local dev server when needed.
- Open the app in a browser.
- Capture screenshots at the exact viewport of each reference image. Capture additional mobile screenshots only for confirmed mobile targets.
- Capture a full-page browser screenshot for every `page-scroll` route, alongside normal viewport screenshots.
- Scroll through the top, middle, and bottom of long routes and verify all sections in the page coverage plan.
- Check that sticky headers, sidebars, and action bars do not hide content while scrolling.
- Exercise the confirmed navigation and interactions.
- Check for blank screens, overlapping text, broken assets, layout shifts, unreadable controls, dead controls, and console errors.
- Hand the running preview, route map, and screenshot paths to an independent visual acceptance agent.
- Read `visual-fidelity-review.md` for the comparison and rejection rules.
- Fix every blocker and major `VIS-###` finding, then request a complete re-review of each affected page.
- Do not self-approve the preview or describe it as visually accepted before the independent report passes.
