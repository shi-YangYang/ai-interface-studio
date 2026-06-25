# Image Prompt Patterns

Use these patterns before generating mockup images. Keep prompts specific enough for strong design direction while preserving implementation realism.

## Contents

1. Global Prompt Requirements
2. Page Coverage Rules
3. Post-Generation Visual Handoff
4. Design-System Image Prompt
5. Single-Viewport Page Prompt
6. Full-Page Overview Prompt
7. Scrollable Page Segment Prompt
8. Mobile Page Prompt
9. Stronger Visual Concepts

## Global Prompt Requirements

Every image prompt should include:

- Project name and product category
- Page name and purpose
- Confirmed visual concept name
- Coverage mode: single viewport, page scroll, or internal scroll
- Desktop web viewport, usually 16:9 or 1440x900
- Real UI structure: navigation, content regions, forms, tables, cards, charts, controls, states
- Palette, typography, spacing, border, shadow, and icon direction
- Text constraint: key titles and labels only; exact copy belongs in `uiux-design.md`
- Avoid list: generic templates, illegible tiny text, random English filler, overlapping UI, stock illustrations, pure marketing hero layout
- For large batches, save prompts to `image-prompts.md` before generating images so the run can be resumed or audited.
- Match the user's language for visible labels. If the user works in Chinese, use concise Chinese labels and avoid random English filler.
- Use mobile viewport prompts only when the user explicitly requested a mobile page; otherwise keep mobile behavior in documentation.
- When the user provides sketches, screenshots, or visual references, preserve only the approved layout, hierarchy, palette, density, and interaction cues. Do not reproduce another product's branding or interface verbatim.

## Page Coverage Rules

- Plan full-page content before writing prompts. List every section in top-to-bottom reading order.
- Use one frame only when the full required page fits legibly in one viewport.
- For a vertically scrolling page, generate one same-size full-page overview image before detail segments. The overview keeps the same image size as other mockups, but scales down the entire long page inside the image to show complete top-to-bottom structure and continuity.
- The overview must look like one uninterrupted web page compressed into a readable map. It must not be a collage, storyboard, stacked screenshots, or multiple framed panels.
- Do not use the overview as the only implementation reference. After the overview, generate normal-scale detail frames for the top, middle, and bottom regions needed to inspect typography, components, spacing, forms, tables, charts, and states.
- Keep global navigation, page width, typography, spacing, and component styling consistent across all segments.
- Repeat only genuinely sticky UI. Do not restart the page title, breadcrumbs, or introductory content in every segment.
- Give adjacent segments a 15-25% shared overlap and a named continuity anchor, such as the end of a table, section heading, or partially continued content block.
- The overview controls top-to-bottom composition and transitions; detail segments control local component detail, spacing, typography, and density. Both must agree at segment boundaries.
- Do not use the compressed overview as a substitute for normal-scale detail frames. Do not stop after the top frame.
- Count the overview and all detail segments when estimating batch size and record every prompt in `image-prompts.md` for runs over 8 business-page frames.

## Post-Generation Visual Handoff

After generating each approved image, the visual design agent must inspect the actual saved bitmap at readable resolution. Do not derive the implementation contract from the prompt alone.

Record these observed properties in the page's visual-fidelity contract:

- Exact reference file and intended viewport
- Coverage strategy: single viewport, overview-plus-detail-segments, or internal scroll
- Application shell and major region proportions
- Section order, transitions, grid, alignment, and whitespace distribution
- Typography hierarchy and approximate scale relationships
- Palette roles, surfaces, borders, radii, shadows, and icon treatment
- Component type, placement, size, variants, and content density
- Sticky or scrolling behavior implied by the overview and sequential detail frames
- Exact overlap anchors between detail frames and any boundary risks
- Any ambiguity, inconsistency, or technically allowed deviation

If related mockups contradict each other, resolve or document the contradiction before frontend implementation. The implementation agent must not guess which image to follow.

## Design-System Image Prompt

Generate this first as `00-design-system.png`.

```text
Create a high-fidelity desktop UI design-system board for [PROJECT_NAME], a [PRODUCT_CATEGORY].
Visual concept: [CONCEPT_NAME].
Show the product's core visual system for implementation: color palette with semantic roles, typography scale, spacing rhythm, layout grid, icon style, buttons, inputs, selects, tabs, filters, table rows, cards, charts, status tags, modals, empty/loading/error states, and navigation patterns.
The board should feel like a practical design spec for a real web product, not a poster. Use a [DENSITY] enterprise SaaS layout with precise alignment, stable component sizes, and clear hierarchy.
Use key Chinese or English labels only where legible. Exact text and field definitions will be documented separately.
Avoid generic admin templates, decorative-only moodboards, distorted UI, overlapping labels, excessive gradients, one-color monotony, and watermark-like branding.
```

## Single-Viewport Page Prompt

Use this only when the complete required page fits legibly in one viewport, or when the product intentionally uses a fixed workspace with an internal scrolling region.

```text
Create a high-fidelity desktop web UI mockup for [PROJECT_NAME].
Page: [PAGE_NAME].
Purpose: [PAGE_PURPOSE].
Visual concept: [CONCEPT_NAME].
Viewport: 16:9 desktop web, around 1440x900.

UI structure:
- [NAVIGATION_STRUCTURE]
- [PRIMARY_CONTENT_REGION]
- [SECONDARY_PANELS_OR_ACTIONS]
- [REQUIRED_COMPONENTS]
- [IMPORTANT_STATES]

Design direction:
- Palette: [PALETTE]
- Typography: [TYPOGRAPHY]
- Layout density: [DENSITY]
- Component language: [COMPONENT_LANGUAGE]
- Interaction tone: [INTERACTION_TONE]

Use realistic product data shapes and meaningful labels, but keep small text minimal and avoid relying on generated microcopy. The page must look implementable in HTML/CSS/React, with consistent spacing, stable card sizes, aligned tables/forms, and no overlapping text.

Avoid generic Bootstrap/AdminLTE layouts, marketing landing-page composition, fake browser chrome dominating the image, illegible tiny text, distorted charts, one-note color palette, and decorative elements that do not serve the product workflow.
```

## Full-Page Overview Prompt

Use this first for every `page-scroll` page.

```text
Create one same-size full-page overview image for a vertically scrolling desktop web UI page for [PROJECT_NAME].
Page: [PAGE_NAME].
Purpose: [PAGE_PURPOSE].
Visual concept: [CONCEPT_NAME].
Canvas: same image size as the normal desktop mockups, around 1440x900 or 16:9. Compress the entire long page into this canvas so the viewer can see the complete page from top to bottom.
Coverage mode: full-page overview.

Full page content order:
1. [SECTION_1]
2. [SECTION_2]
3. [SECTION_3]
4. [SECTION_4]

UI structure:
- [GLOBAL_NAVIGATION_OR_SHELL]
- [TOP_SECTION]
- [MIDDLE_SECTIONS]
- [BOTTOM_SECTION]
- [STICKY_ELEMENTS_OR_NONE]

Design direction:
- Palette: [PALETTE]
- Typography: [TYPOGRAPHY]
- Layout density: [DENSITY]
- Component language: [COMPONENT_LANGUAGE]
- Interaction tone: [INTERACTION_TONE]

Keep a single consistent application shell, content width, grid, typography scale relationship, spacing rhythm, component styling, and visual density across the entire compressed page. Section transitions should feel like natural scroll continuation, not separate screenshots placed together.

Use readable major labels only. Small text is allowed to be schematic because this image is an overview map, not the detail reference. Exact text and field definitions will be documented separately.

Avoid montage layouts, stacked viewport cards, repeated non-sticky headers, restarted page titles in the middle, sudden palette or component changes, missing middle sections, browser chrome, and decorative filler that breaks the product workflow.
```

After generation, inspect the saved bitmap. Accept it only if the complete page structure is visible and continuous. Then generate normal-scale detail segments for implementation fidelity.

## Scrollable Page Segment Prompt

Generate all detail segments for the same page in top-to-bottom order. Reuse the approved design system, the full-page overview, and the preceding detail segment as continuity references.

```text
Create segment [SEGMENT_INDEX] of [SEGMENT_TOTAL] for a high-fidelity vertically scrolling desktop web page for [PROJECT_NAME].
Page: [PAGE_NAME].
Purpose: [PAGE_PURPOSE].
Visual concept: [CONCEPT_NAME].
Viewport: 16:9 desktop web, around 1440x900.
Scroll position: [TOP / MIDDLE / BOTTOM].

Full page content order:
1. [SECTION_1]
2. [SECTION_2]
3. [SECTION_3]
4. [SECTION_4]

This segment must show:
- [SEGMENT_SECTIONS]
- Overlap from previous segment: [PREVIOUS_ANCHOR_OR_NONE], approximately 15-25% of the frame when available
- Overlap into next segment: [NEXT_ANCHOR_OR_NONE], approximately 15-25% of the frame when available
- Sticky elements visible at this scroll position: [STICKY_ELEMENTS_OR_NONE]

Keep the same application shell, content width, grid, colors, typography, spacing, components, and realistic data language used by the overview and other detail segments of this page. This must look like the next viewport reached by scrolling the same page, not a separate page or a redesigned variation.

Do not repeat non-sticky page introductions, omit required sections, squeeze the complete long page into one frame, create montage panels, restart the page at segment boundaries, or add browser chrome that hides the product UI.
```

After generating all detail segments, verify that every item in the full page content order is represented by the overview and visible in at least one detail image. Adjacent detail overlaps must line up in shell, section transition, grid, spacing, typography, palette, component style, and content continuation.

## Mobile Page Prompt

Use this only when the user explicitly requests a mobile page.

```text
Create a high-fidelity mobile UI mockup for [PROJECT_NAME].
Page: [PAGE_NAME].
Purpose: [PAGE_PURPOSE].
Visual concept: [CONCEPT_NAME].
Viewport: mobile phone UI, around 390x844, shown as a clean phone screen mockup.
Coverage: [SINGLE VIEWPORT or SEGMENT_INDEX of SEGMENT_TOTAL].

UI structure:
- [COMPACT_HEADER]
- [PRIMARY_MOBILE_FLOW]
- [FORM_OR_TASK_COMPONENTS]
- [BOTTOM_ACTION_AREA]
- [IMPORTANT_STATES]

Design direction:
- Palette: [PALETTE]
- Typography: [TYPOGRAPHY]
- Layout density: mobile-optimized and uncluttered
- Component language: large tap targets, clear labels, stable controls
- Interaction tone: fast, reassuring, minimal friction

Use key labels only. The page must look implementable as mobile web or an embedded enterprise app entry, with no overlapping text.

Avoid generic mobile templates, playful consumer styling, tiny form text, fake browser chrome dominating the screen, and decorative illustrations that slow down the workflow.
```

Apply the same overview-plus-detail-segments rule to mobile pages that extend beyond one phone viewport.

## Stronger Visual Concepts

When the user's style request is vague, propose named concepts like:

- **Command Canvas**: precise workbench UI, neutral foundation, bright command accents, dense operational panels
- **Signal Grid**: data-driven grid, luminous status language, strong chart/table rhythm
- **Quiet Control Room**: restrained dark or light console, calm hierarchy, executive monitoring tone
- **Paperless Bureau**: document-heavy workflows, clear approvals, soft neutral surfaces, rigorous metadata
- **Aurora Glass**: premium glass layers, restrained glow, useful for high-tech internal systems only when not overused

Adapt concept names to the domain rather than reusing the same names every time.
