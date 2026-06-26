# Interactive Frontend Preview

Use this only after the UI/UX package is approved and the user requests a browser-ready preview. The preview is a design prototype, not a full-stack application.

The frontend implementation agent owns this stage. It must be separate from the coordinator and visual acceptance agent.

## Entry Gate

Do not write preview code until all of these exist:

- User-approved design-system image and page mockups
- Complete `uiux-design.md`
- A frozen visual-fidelity contract for every route in scope
- User-approved frontend implementation strategy, including framework, UI library, styling system, icon set, charting/drawing library, 3D/rendering library, animation approach, supporting asset plan, required custom components, and reference reconstruction map
- Exact reference viewport for every mockup, plus image dimensions and scale contract for every vertical long-page `page-scroll` route
- Coordinator-provided route and ownership scope

The implementation agent must open and inspect the original images before editing. A textual summary is not a substitute.
If the implementation strategy is missing, stop and return to the coordinator instead of choosing a convenient default stack.
If the reconstruction map is missing or does not list visible page regions and element groups, stop and return to the coordinator before coding.

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

Prefer the existing repository stack if there is one and it can reproduce the approved visuals. If the target project is empty and the user does not specify a stack, the coordinator should propose a default stack before implementation. A simple baseline is:

- React
- Vite
- Tailwind CSS
- lucide-react for icons

Extend or replace the baseline when the approved mockups require it. Choose the UI library to match the framework: for Vue projects, Element Plus is a common option; for React projects, Ant Design, MUI, Radix/shadcn, or another project-appropriate system may fit better. Use ECharts, D3, SVG, Canvas, Three.js, React Three Fiber, GSAP, Framer Motion, or generated supporting assets when the approved visuals contain charts, diagrams, 3D scenes, blueprint overlays, material effects, or animation that plain HTML/CSS cannot reproduce faithfully.

The implementation strategy should include a region-by-region visual technology map:

| Page / Region | Reference Visual | Implementation Method | Library / Asset | Fidelity Risk | Approval |
| --- | --- | --- | --- | --- | --- |
| `PAGE-001` / hero blueprint | `01-home-long.png` | CSS layout + SVG overlay + image asset | SVG, generated support asset | Medium | Approved |
| `PAGE-002` / KPI chart | `02-dashboard.png` | Real chart component | ECharts | Low | Approved |
| `PAGE-003` / 3D model | `03-scene.png` | Interactive 3D scene | Three.js | High | Approved |

The strategy should also include a reference reconstruction map. This map turns the approved image into implementation obligations:

| ID | Page / Region | Visible Element Or Effect | Reference Evidence | Required Implementation | Match Rule | Omission Allowed |
| --- | --- | --- | --- | --- | --- | --- |
| `RECON-001` | `PAGE-001` / header | logo, nav items, phone, primary CTA | `01-home-long.png` top bar | HTML/CSS + icon asset | same count, order, alignment, density | No |
| `RECON-002` | `PAGE-001` / hero | construction photo, blueprint overlay, measurement labels | `01-home-long.png` hero | image asset + SVG overlay | preserve composition and layer treatment | No |

## Build Rules

- Treat `uiux-design.md` as authoritative for requirements, exact copy, fields, states, permissions, and behavior.
- Treat `00-design-system.png` and its recorded visual tokens as authoritative for palette, typography hierarchy, shell language, component shapes, spacing rhythm, icon treatment, and density.
- Treat approved page mockups and their visual-fidelity contracts as authoritative for page composition, section order, major region proportions, visual hierarchy, and workflow structure.
- Treat the approved implementation strategy as authoritative for technical reproduction choices. Use the named libraries, custom components, and asset plan unless the coordinator approves a change.
- Treat the reconstruction map as an implementation checklist. Every `RECON-###` item must be present in the browser preview before review.
- Treat generated bitmap microcopy as directional only. Do not weaken the visual composition because small generated text is uncertain.
- Implement real HTML/CSS components rather than embedding the bitmap mockups as the UI.
- Implement in screenshot-reconstruction mode: first match the reference image's structure, proportions, visual layers, element count, and density; then add local interactions. Do not redesign the UI while making it functional.
- Build the first screen as the actual app surface, not a marketing landing page.
- Implement the shared application shell first and capture a matching-viewport screenshot before building all pages.
- Work in small page batches. Do not implement the complete preview in one unreviewed pass.
- Implement the complete confirmed content order for every `page-scroll` route, not only the first viewport represented by its top mockup.
- For `page-scroll` routes, use the single approved vertical long-page mockup as the top-to-bottom composition, proportion, and transition reference. Use the design-system image and visual-fidelity contract for local typography, spacing, component shape, data density, and styling.
- Implement according to the scale contract: reference image width maps to the browser CSS viewport width, and full-page screenshot height should match the reference image height after applying the same scale. Do not treat the long image as a landscape board or thumbnail.
- Do not implement a scrolling page as independent chunks that change spacing, shell, or component language at scroll boundaries. Do not invent missing sections that are not present in the long-page mockup or `uiux-design.md`.
- Implement the confirmed routes and interactions with mock data and local state.
- Make key actions visibly respond, but keep network operations stubbed.
- Include expected states where feasible: empty, loading, error, disabled, selected, and permission-limited.
- Keep dashboard and admin surfaces dense, scannable, and work-focused.
- Use stable dimensions for boards, toolbars, cards, tables, icon buttons, and counters so interactions do not resize the layout.
- Use lucide icons for common actions and tool buttons when available.
- Do not replace distinctive approved components with generic cards, tables, navigation, or dashboard patterns merely because they are easier to implement.
- Do not replace approved chart, drawing, 3D, map, or blueprint effects with flat placeholders unless the implementation strategy explicitly approves a static substitute. If a region cannot be reproduced with the approved stack, stop and ask the coordinator to revise the strategy.
- Do not omit visible UI element groups from the approved image. Missing mapped elements are visual defects, not implementation shortcuts.
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
- Capture a full-page browser screenshot for every `page-scroll` route, alongside normal viewport screenshots. Compare the full-page browser screenshot against the approved vertical long-page mockup using the recorded scale contract, then compare local styling against the design-system image and visual-fidelity contract.
- Verify every item in the visual technology map: required UI library components, custom components, charts, diagrams, 3D scenes, canvas/SVG drawings, animation, image treatments, and supporting assets must be present and visually aligned with the approved mockups.
- Verify every `RECON-###` item from the reconstruction map. Check that the visible element or effect exists, appears in the same region, keeps the same visual priority, and is not replaced by a generic approximation.
- Scroll through the top, middle, and bottom of long routes and verify all sections in the page coverage plan.
- Inspect scroll boundaries and verify that shell geometry, section transitions, spacing, typography, palette, and component styling do not visibly reset.
- Check that sticky headers, sidebars, and action bars do not hide content while scrolling.
- Exercise the confirmed navigation and interactions.
- Check for blank screens, overlapping text, broken assets, layout shifts, unreadable controls, dead controls, and console errors.
- Hand the running preview, route map, and screenshot paths to an independent visual acceptance agent.
- Read `visual-fidelity-review.md` for the comparison and rejection rules.
- Fix every blocker and major `VIS-###` finding only when acting as the Frontend Implementation Agent or an assigned Frontend Repair Agent. The coordinator must route findings and decisions, not patch code.
- After fixes, request a complete re-review of each affected page.
- Do not self-approve the preview or describe it as visually accepted before the independent report passes.
