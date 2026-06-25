# Image Prompt Patterns

Use these patterns before generating mockup images. Keep prompts specific enough for strong design direction while preserving implementation realism.

## Contents

1. Global Prompt Requirements
2. Page Coverage Rules
3. Post-Generation Visual Handoff
4. Design-System Image Prompt
5. Single-Viewport Page Prompt
6. Vertical Long-Page Prompt
7. Prohibited Scroll Reference Regeneration
8. Mobile Page Prompt
9. Stronger Visual Concepts

## Global Prompt Requirements

Every image prompt should include:

- Project name and product category
- Page name and purpose
- Confirmed visual concept name
- Coverage mode: single viewport, page scroll, or internal scroll
- Desktop reference viewport. Use 1440 CSS px wide unless the user specifies another width.
- Real UI structure: navigation, content regions, forms, tables, cards, charts, controls, states
- Palette, typography, spacing, border, shadow, and icon direction
- Text constraint: key titles and labels only; exact copy belongs in `uiux-design.md`
- Avoid list: generic templates, illegible tiny text, random English filler, overlapping UI, stock illustrations, pure marketing hero layout
- For large batches, save prompts to `image-prompts.md` before generating images so the run can be resumed or audited.
- Match the user's language for visible labels. If the user works in Chinese, use concise Chinese labels and avoid random English filler.
- Use mobile viewport prompts only when the user explicitly requested a mobile page; otherwise keep mobile behavior in documentation.
- When the user provides sketches, screenshots, or visual references, preserve only the approved layout, hierarchy, palette, density, and interaction cues. Do not reproduce another product's branding or interface verbatim.
- After `00-design-system.png` is approved, page prompts must explicitly reuse its observed palette, typography hierarchy, shell geometry, component shapes, spacing rhythm, icon treatment, and density. Regenerate any page image that looks like a different design system.

## Page Coverage Rules

- Plan full-page content before writing prompts. List every section in top-to-bottom reading order.
- Use one frame only when the full required page fits legibly in one viewport.
- For a vertically scrolling page, generate one vertical long-page canonical mockup as the only AI-generated page reference for that page. The image should be taller than it is wide and should represent the full browser page from top to bottom at one consistent scale.
- Do not convert a scroll page into a landscape overview, design board, collage, storyboard, or stacked viewport panels. If the output is landscape for a `page-scroll` page, reject it and regenerate.
- Record a scale contract after generation: `reference_css_width / image_pixel_width = scale`; expected browser full-page screenshot height is `image_pixel_height * scale`.
- Do not generate new AI detail segments, close-ups, alternate local mockups, or horizontal overview boards after the long-page mockup. Those images become competing sources and often redesign the page.
- Use the design-system image and visual-fidelity contract for precise tokens and local implementation details that are hard to read in the generated bitmap.
- If local inspection is necessary, use deterministic zoom/crop views from the approved long-page mockup; do not treat those crops as new mockups or new design decisions.
- Count each long-page mockup as one business-page frame and record every prompt in `image-prompts.md` for runs over 8 business-page frames.

## Post-Generation Visual Handoff

After generating each approved image, the visual design agent must inspect the actual saved bitmap at readable resolution. Do not derive the implementation contract from the prompt alone.

Record these observed properties in the page's visual-fidelity contract:

- Exact reference file and intended viewport
- Coverage strategy: single viewport, vertical-long-page, or internal scroll
- Reference browser CSS width and image pixel dimensions
- Scale contract: `css_width / image_width = scale`; `expected_css_page_height = image_height * scale`
- Design-system inheritance: observed tokens, shell, components, and density reused from `00-design-system.png`
- Application shell and major region proportions
- Section order, transitions, grid, alignment, and whitespace distribution
- Typography hierarchy and approximate scale relationships
- Palette roles, surfaces, borders, radii, shadows, and icon treatment
- Component type, placement, size, variants, and content density
- Sticky or scrolling behavior implied by the long-page mockup
- Any bitmap ambiguity and the contract rule that resolves it
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

## Vertical Long-Page Prompt

Use this for every `page-scroll` page.

```text
Create one vertical long-page canonical mockup for a desktop web UI page for [PROJECT_NAME].
Page: [PAGE_NAME].
Purpose: [PAGE_PURPOSE].
Visual concept: [CONCEPT_NAME].
Reference browser viewport: [REFERENCE_WIDTH]px wide desktop web, usually 1440px.
Canvas: vertical long image, taller than wide, representing the complete scrollable page from top to bottom at one consistent scale. Preferred aspect ratio is roughly [WIDTH]:[HEIGHT] based on content length, usually between 1:1.8 and 1:4 for desktop website pages.
Coverage mode: vertical-long-page canonical mockup.

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

Keep a single consistent application shell, content width, grid, typography scale relationship, spacing rhythm, component styling, and visual density across the entire long page. Section transitions should feel like natural scroll continuation, not separate screenshots placed together.

Use readable major labels and realistic UI text density. Exact text and field definitions will be documented separately, but this image is the canonical implementation reference and must remain visually inspectable.

Avoid landscape overview boards, montage layouts, stacked viewport cards, repeated non-sticky headers, restarted page titles in the middle, sudden palette or component changes, missing middle sections, excessive browser chrome, and decorative filler that breaks the product workflow.
```

After generation, inspect the saved bitmap. Accept it only if it is vertical, complete, continuous, visually inspectable, and clearly inherits from `00-design-system.png`. Record pixel dimensions and scale mapping in `uiux-design.md`. Do not generate separate AI detail segments or a landscape overview for this page.

## Prohibited Scroll Reference Regeneration

Do not use image generation to create top, middle, bottom, detail, close-up, horizontal overview, or zoomed redesigns for a `page-scroll` page after its vertical long-page mockup is approved.

Allowed ways to inspect or implement local detail:

- Deterministically crop or zoom the approved long-page mockup without changing pixels.
- Describe inferred details in the visual-fidelity contract, using the approved design-system image as the token and component source.
- Ask the user to approve a revised long-page mockup if the current one is too ambiguous or the aspect ratio is wrong.

Forbidden:

- Regenerating a local segment from a prompt.
- Asking the model to "make the middle section clearer" as a separate page image.
- Letting a generated close-up or landscape overview override the long-page mockup or design system.

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

Apply the same vertical-long-page rule to mobile pages that extend beyond one phone viewport.

## Stronger Visual Concepts

When the user's style request is vague, propose named concepts like:

- **Command Canvas**: precise workbench UI, neutral foundation, bright command accents, dense operational panels
- **Signal Grid**: data-driven grid, luminous status language, strong chart/table rhythm
- **Quiet Control Room**: restrained dark or light console, calm hierarchy, executive monitoring tone
- **Paperless Bureau**: document-heavy workflows, clear approvals, soft neutral surfaces, rigorous metadata
- **Aurora Glass**: premium glass layers, restrained glow, useful for high-tech internal systems only when not overused

Adapt concept names to the domain rather than reusing the same names every time.
