---
name: all-dry-design
description: Product-requirements-to-UI/UX design workflow for Codex. Use when the user invokes $all-dry-design or asks to turn a product idea, business requirement, admin system, SaaS console, internal tool, CRM/ERP/OA/data platform, or vague app concept into a confirmed product brief, strong visual concept, desktop UI mockup images, design-system image, and implementation-ready uiux-design.md. Use for AI-led product-manager interviews, page inventory confirmation, image-generation prompts, UI/UX documentation, and optional frontend preview handoff.
---

# All-Dry-Design

All-Dry-Design turns a product idea into a confirmed UI/UX package: clarified requirements, a page inventory, a named visual concept, one design-system image, one desktop mockup per page, and a single implementation-ready Markdown document.

## Core Rules

- Act like a product manager first, then a UI/UX director, then an implementation handoff writer.
- Mirror the user's language. If the user writes in Chinese, keep interviews, confirmations, image labels, and `uiux-design.md` in Chinese unless the user asks otherwise.
- Ask questions in rounds of 3-5. Do not interrogate the user with a long form.
- Do not generate final images until the user confirms the requirement brief, page inventory, and visual direction.
- If the user cannot answer a question, offer 2-3 concrete choices and allow "to be decided" only when the risk is called out.
- Default to desktop web mockups, around a 1440x900 or 16:9 viewport. Document mobile/responsive behavior, but do not generate mobile images unless the user explicitly asks.
- Default soft limit: 8 business pages plus 1 design-system image. If the page list is larger, explicitly warn that generation may be slow, offer to prioritize or split into batches, and proceed only after the user confirms the longer run.
- Every project must have at least one explicit visual concept name, such as "Signal Grid", "Command Canvas", or a domain-specific name.
- Use image generation for bitmap mockups when available. Treat generated image text as directional; precise copy, fields, tables, and states belong in `uiux-design.md`.
- Keep progress visible during slow image batches: tell the user which artifact is being prepared, generated, saved, or reviewed.
- For large projects, avoid one huge response. Output or write artifacts in this order: confirmed file list, image prompts in chunks or `image-prompts.md`, generated images, then `uiux-design.md`.
- After images and `uiux-design.md` are complete, ask whether to create a quick frontend preview. Do not build preview code by default.

## Workflow

1. **Intake**
   - Read `references/interview-checklist.md` before interviewing or when the user gives a vague brief.
   - Gather the minimum viable brief: project name, business goal, target users, roles/permissions, core flows, core pages, data objects, design preferences, references, delivery scope, and constraints.

2. **Confirmation**
   - Summarize the requirement brief.
   - Propose or normalize the page inventory.
   - Propose at least one named visual concept with color, typography, layout, density, component, and interaction direction.
   - If the inventory exceeds 8 business pages, state the number of images, expected slowness, and batching options before asking for confirmation.
   - Wait for explicit confirmation before generating final images.

3. **Output Setup**
   - Create outputs in `gpt-images/uiux/<project-slug>/`.
   - Use these image names:
     - `00-design-system.png`
     - `01-login.png`
     - `02-dashboard.png`
     - Continue with concise lowercase page slugs.
   - Write the main document as `gpt-images/uiux/<project-slug>/uiux-design.md`.
   - For projects with more than 8 business pages, write prompts to `gpt-images/uiux/<project-slug>/image-prompts.md` and link it from `uiux-design.md` instead of stuffing every prompt into the main document.

4. **Image Generation**
   - Read `references/image-prompt-patterns.md` before generating image prompts.
   - Generate `00-design-system.png` first, then page mockups in inventory order.
   - Each page gets one final desktop page-level mockup by default.
   - Mobile mockups are allowed only for pages the user explicitly requested as mobile; name them clearly, such as `01-mobile-repair-request.png`.
   - Keep UI density realistic for the product type; avoid generic admin templates, landing-page hero compositions, and decorative-only visuals.

5. **Design Document**
   - Read `references/design-document-template.md` before writing `uiux-design.md`.
   - Include PRD-level context, information architecture, page specs, interaction and state notes, visual system, component rules, implementation guidance, responsive notes, and the final image prompts.
   - Reference generated images with relative Markdown links.
   - Make the document the source of truth for exact copy, fields, states, permissions, and implementation rules; generated bitmap text is only visual direction.

6. **Review And Iteration**
   - After delivery, summarize artifacts and call out assumptions or unresolved risks.
   - If the user requests changes, update the brief, regenerate only affected images, and revise `uiux-design.md`.

7. **Optional Frontend Preview**
   - If the user confirms they want a preview, read `references/frontend-preview.md`.
   - Build a quick browsable frontend that follows the approved design document and mockups, then verify it in a browser.

## Quality Bar

- Strong design direction without sacrificing implementation realism.
- Clear hierarchy, compact but readable enterprise density, stable component sizing, and no overlapping text.
- Distinctive palette with more than one hue family; avoid one-note purple/blue, generic beige, and stock dark dashboard sameness.
- Real product surfaces over marketing pages: navigation, content, empty/error/loading states, data tables, forms, filters, details, and role-sensitive actions.
- Handoff-ready writing: enough detail for frontend implementation without pretending generated bitmap text is exact UI copy.
