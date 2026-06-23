# Image Prompt Patterns

Use these patterns before generating mockup images. Keep prompts specific enough for strong design direction while preserving implementation realism.

## Contents

1. Global Prompt Requirements
2. Page Coverage Rules
3. Design-System Image Prompt
4. Single-Viewport Page Prompt
5. Scrollable Page Segment Prompt
6. Mobile Page Prompt
7. Stronger Visual Concepts

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
- For a vertically scrolling page, create as many sequential viewport frames as needed to cover all confirmed sections.
- Keep global navigation, page width, typography, spacing, and component styling consistent across all segments.
- Repeat only genuinely sticky UI. Do not restart the page title, breadcrumbs, or introductory content in every segment.
- Give adjacent segments a shared continuity anchor, such as the end of a table, section heading, or partially continued content block.
- Do not compress a long page into tiny unreadable content. Do not stop after the top frame.
- Count segments when estimating batch size and record every prompt in `image-prompts.md` for runs over 8 business-page frames.

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

## Scrollable Page Segment Prompt

Generate all segments for the same page in top-to-bottom order. Reuse the approved design system and the preceding segment as continuity references when available.

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
- Continuity from previous segment: [PREVIOUS_ANCHOR_OR_NONE]
- Continuity into next segment: [NEXT_ANCHOR_OR_NONE]
- Sticky elements visible at this scroll position: [STICKY_ELEMENTS_OR_NONE]

Keep the same application shell, content width, grid, colors, typography, spacing, components, and realistic data language used by the other segments of this page. This must look like the next viewport reached by scrolling the same page, not a separate page or a redesigned variation.

Do not repeat non-sticky page introductions, omit required sections, squeeze the complete long page into one frame, create montage panels, or add browser chrome that hides the product UI.
```

After generating all segments, verify that every item in the full page content order is visible in at least one image and that no segment contradicts the others.

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

Apply the same segmented coverage rule to mobile pages that extend beyond one phone viewport.

## Stronger Visual Concepts

When the user's style request is vague, propose named concepts like:

- **Command Canvas**: precise workbench UI, neutral foundation, bright command accents, dense operational panels
- **Signal Grid**: data-driven grid, luminous status language, strong chart/table rhythm
- **Quiet Control Room**: restrained dark or light console, calm hierarchy, executive monitoring tone
- **Paperless Bureau**: document-heavy workflows, clear approvals, soft neutral surfaces, rigorous metadata
- **Aurora Glass**: premium glass layers, restrained glow, useful for high-tech internal systems only when not overused

Adapt concept names to the domain rather than reusing the same names every time.
