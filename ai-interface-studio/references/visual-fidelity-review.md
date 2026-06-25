# Visual Fidelity Review

Use this after the frontend preview is running. The reviewer must be independent from the implementation agent and must not edit frontend code.

## Required Inputs

- Approved design-system image
- Approved page mockups in reading order, including the vertical long-page mockup and scale contract for each `page-scroll` route
- `uiux-design.md`, including each page's visual-fidelity contract
- Running preview URL and route map
- Target desktop and requested mobile viewports

Missing reference images or an incomplete visual contract blocks review.

## Review Procedure

1. Open each approved mockup at readable resolution.
2. Set the browser to the matching viewport.
3. Capture a viewport screenshot for every single-viewport page and representative top, middle, and bottom scroll positions.
4. Capture a full-page screenshot for every `page-scroll` route.
5. For `page-scroll` routes, compare the vertical long-page mockup with the full-page browser screenshot using the recorded scale contract before judging local viewport frames.
6. Compare local viewport styling against the approved design-system image and visual-fidelity contract.
7. Compare reference and implementation side by side, region by region.
8. Record differences before judging pass or fail.
9. Re-run the full affected-page review after fixes; do not verify only the edited component.

## Comparison Order

Review in this order so local polish cannot hide structural drift:

1. Application shell: header, sidebar, navigation, content bounds, sticky regions
2. Page composition: section order, column ratios, major panels, whitespace distribution
3. Scroll continuity: top-to-bottom flow, section transitions, sticky behavior, and absence of visible seams
4. Components: type, count, placement, size, variants, controls, charts, tables, cards
5. Typography: family category, scale hierarchy, weight, line height, alignment
6. Visual tokens: palette, borders, radii, shadows, dividers, icon treatment
7. Density and rhythm: spacing, row height, card padding, content amount
8. Responsive transformation and scroll behavior
9. Content and state fidelity according to `uiux-design.md`

Do not use a raw pixel-difference score as the only judgment. Generated mockup text can vary, but composition and visual language must remain recognizably faithful.

## Severity

- **Blocker**: wrong page composition or theme, missing major region, incorrect navigation shell, unusable layout, implementation clearly resembles a different design, or a long page visibly restarts as separate pages while scrolling.
- **Major**: wrong column ratio, component type, placement, typography hierarchy, palette, spacing density, responsive behavior, repeated style pattern, visible scroll seam, broken section transition, or abrupt style change between long-page sections.
- **Minor**: local spacing, icon, border, shadow, or small typographic mismatch that does not alter the design language.

Acceptance requires zero open blocker and zero open major findings. Minor findings may remain only when documented as an allowed deviation or accepted by the user.

## Report Format

Write `gpt-images/uiux/<project-slug>/visual-review.md`:

```md
# Visual Review

- Reviewer mode: independent agent / sequential fallback
- Preview URL:
- Review date:
- Result: pass / fail

## Evidence

| Page ID | Reference | Browser Screenshot | Viewport | Result |
| --- | --- | --- | --- | --- |
| `PAGE-001` | `01-login.png` | `review/PAGE-001.png` | 1440x900 | Pass/Fail |
| `PAGE-003` | `03-settings-long.png` | `review/PAGE-003-full.png` | 1440xfull-page | Pass/Fail |

## Findings

| ID | Severity | Page / Region | Expected | Actual | Evidence | Required Correction | Status |
| --- | --- | --- | --- | --- | --- | --- | --- |
| `VIS-001` | Major | `PAGE-001` / header | ... | ... | ... | ... | Open |

## Accepted Deviations

| Page / Region | Deviation | Reason | Approved By |
| --- | --- | --- | --- |
| ... | ... | ... | ... |
```

## Rejection Rules

Reject the preview when any of these is true:

- The implementation agent did not inspect the original mockups.
- Screenshots use a different viewport without documenting why.
- A `page-scroll` reference was converted into a landscape overview, compressed board, or another aspect ratio not approved by the user.
- Major sections, controls, or visual hierarchy differ from the approved image.
- The implementation ignores `00-design-system.png` and uses a different visual system, even if the page structure is similar.
- A `page-scroll` route has missing sections, broken section transitions, visible stitching seams, restarted non-sticky headers, or style drift between adjacent scroll regions.
- Generic components replace distinctive approved components without an explicit decision.
- Only navigation and functional behavior were tested.
- Blocker or major findings remain open.
