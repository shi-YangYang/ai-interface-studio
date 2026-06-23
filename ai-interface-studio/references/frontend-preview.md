# Interactive Frontend Preview

Use this only after the UI/UX package is approved and the user requests a browser-ready preview. The preview is a design prototype, not a full-stack application.

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

- Treat `uiux-design.md` as the source of truth.
- Use generated mockups as visual direction, not as exact text extraction.
- Implement real HTML/CSS components rather than embedding the bitmap mockups as the UI.
- Build the first screen as the actual app surface, not a marketing landing page.
- Implement the complete confirmed content order for every `page-scroll` route, not only the first viewport represented by its top mockup.
- Implement the confirmed routes and interactions with mock data and local state.
- Make key actions visibly respond, but keep network operations stubbed.
- Include expected states where feasible: empty, loading, error, disabled, selected, and permission-limited.
- Keep dashboard and admin surfaces dense, scannable, and work-focused.
- Use stable dimensions for boards, toolbars, cards, tables, icon buttons, and counters so interactions do not resize the layout.
- Use lucide icons for common actions and tool buttons when available.
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
- Capture desktop and mobile screenshots.
- Capture a full-page browser screenshot for every `page-scroll` route, alongside normal viewport screenshots.
- Scroll through the top, middle, and bottom of long routes and verify all sections in the page coverage plan.
- Check that sticky headers, sidebars, and action bars do not hide content while scrolling.
- Exercise the confirmed navigation and interactions.
- Check for blank screens, overlapping text, broken assets, layout shifts, unreadable controls, dead controls, and console errors.
- Iterate until the preview matches the approved direction well enough for review.
