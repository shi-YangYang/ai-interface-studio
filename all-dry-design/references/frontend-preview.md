# Frontend Preview Handoff

Use this only after the user confirms they want a quick frontend preview.

## Default Stack

Prefer the existing repository stack if there is one. If the target project is empty and the user does not specify a stack, use:

- React
- Vite
- Tailwind CSS
- lucide-react for icons

## Build Rules

- Treat `uiux-design.md` as the source of truth.
- Use generated mockups as visual direction, not as exact text extraction.
- Implement real HTML/CSS components rather than embedding the bitmap mockups as the UI.
- Build the first screen as the actual app surface, not a marketing landing page.
- Include expected states where feasible: empty, loading, error, disabled, selected, and permission-limited.
- Keep dashboard and admin surfaces dense, scannable, and work-focused.
- Use stable dimensions for boards, toolbars, cards, tables, icon buttons, and counters so interactions do not resize the layout.
- Use lucide icons for common actions and tool buttons when available.

## Verification

- Start the local dev server when needed.
- Open the app in a browser.
- Capture desktop and mobile screenshots.
- Check for blank screens, overlapping text, broken assets, layout shifts, unreadable controls, and console errors.
- Iterate until the preview matches the approved direction well enough for review.
