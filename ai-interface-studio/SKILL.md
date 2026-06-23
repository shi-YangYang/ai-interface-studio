---
name: ai-interface-studio
description: "AI-assisted product-idea-to-UI/UX-and-frontend-preview workflow for Codex. Use when the user invokes $ai-interface-studio or asks to turn a product idea, business requirement, admin system, SaaS console, internal tool, CRM/ERP/OA/data platform, or vague app concept into a confirmed product brief, strong visual concept, design-system image, complete single-viewport or scroll-page UI mockup coverage, UI/UX documentation, development handoff contract, and optionally a browser-ready interactive frontend preview. Use for AI-led product-manager interviews, page inventory and coverage confirmation, image-generation prompts, traceable design handoff, and lightweight frontend prototyping. Stop at frontend preview: use mock data and local state, and do not implement backend services, databases, production authentication, payments, cloud infrastructure, or deployment."
---

# AI Interface Studio Skill

AI Interface Studio Skill turns a product idea into a confirmed UI/UX package and, when requested, a browser-ready interactive frontend preview. It does not build production full-stack applications.

## Core Rules

- Act like a product manager first, then a UI/UX director, then a lightweight prototype builder only after the design is approved.
- Mirror the user's language. If the user writes in Chinese, keep interviews, confirmations, image labels, and `uiux-design.md` in Chinese unless the user asks otherwise.
- Accept product ideas as text, rough sketches, screenshots, or visual references. Extract useful layout, hierarchy, palette, and interaction cues without copying another product's brand or interface verbatim.
- Ask questions in rounds of 3-5. Do not interrogate the user with a long form.
- Do not generate final images until the user confirms the requirement brief, page inventory, and visual direction.
- If the user cannot answer a question, offer 2-3 concrete choices and allow "to be decided" only when the risk is called out.
- Default to desktop web viewport frames around 1440x900 or 16:9. Document mobile/responsive behavior, but do not generate mobile images unless the user explicitly asks.
- Treat a page and an image as different units. Classify every page as `single-viewport`, `page-scroll`, or `internal-scroll` before image generation.
- For `page-scroll` pages, generate sequential top, middle, and bottom viewport frames as needed. Do not deliver only the first screen, and do not shrink a long page into one unreadable image.
- Default soft limit: 8 business-page frames plus 1 design-system image. Count every scroll segment as a frame. If the estimated frame count is larger, warn that generation may be slow, offer to prioritize or split into batches, and proceed only after confirmation.
- Every project must have at least one explicit visual concept name, such as "Signal Grid", "Command Canvas", or a domain-specific name.
- Use image generation for bitmap mockups when available. Treat generated image text as directional; precise copy, fields, tables, and states belong in `uiux-design.md`.
- Keep progress visible during slow image batches: tell the user which artifact is being prepared, generated, saved, or reviewed.
- For large projects, avoid one huge response. Output or write artifacts in this order: confirmed file list, image prompts in chunks or `image-prompts.md`, generated images, then `uiux-design.md`.
- After images and `uiux-design.md` are approved, offer an interactive frontend preview. Do not build preview code by default unless the user already requested it.
- Keep the preview frontend-only: use mock data, local state, and stubbed actions. Do not add backend APIs, databases, production authentication, payment flows, external service integrations, cloud resources, deployment pipelines, or production operations.
- Describe the preview as a prototype, not a production-ready application.
- Keep `uiux-design.md` as the single source of truth. Put the development handoff contract inside it instead of creating a second authoritative specification.
- Use stable requirement, flow, page, component, state, and acceptance IDs for multi-page projects so downstream teams can trace decisions across artifacts.

## Workflow

1. **Intake**
   - Read `references/interview-checklist.md` before interviewing or when the user gives a vague brief.
   - Gather the minimum viable brief: project name, business goal, target users, roles/permissions, core flows, core pages, data objects, design preferences, references, delivery scope, and constraints.

2. **Confirmation**
   - Summarize the requirement brief.
   - Propose or normalize the page inventory.
   - Add a page coverage plan: scroll model, ordered content sections, frame count, and the sections covered by each frame.
   - Propose at least one named visual concept with color, typography, layout, density, component, and interaction direction.
   - State the total image count from the coverage plan. If it exceeds 8 business-page frames, state the expected slowness and batching options before asking for confirmation.
   - Wait for explicit confirmation before generating final images.

3. **Output Setup**
   - Create outputs in `gpt-images/uiux/<project-slug>/`.
   - Use these image names:
     - `00-design-system.png`
     - `01-login.png`
     - `02-dashboard.png`
     - Continue single-viewport pages with concise lowercase page slugs.
     - Name scroll segments sequentially, such as `03-settings-01-top.png`, `03-settings-02-content.png`, and `03-settings-03-bottom.png`.
   - Write the main document as `gpt-images/uiux/<project-slug>/uiux-design.md`.
   - For projects with more than 8 business-page frames, write prompts to `gpt-images/uiux/<project-slug>/image-prompts.md` and link it from `uiux-design.md` instead of stuffing every prompt into the main document.

4. **Image Generation**
   - Read `references/image-prompt-patterns.md` before generating image prompts.
   - Generate `00-design-system.png` first, then page mockups in inventory order.
   - Generate one frame for `single-viewport` pages. For `internal-scroll` workspaces, show the stable shell and document the internal scrolling region.
   - Generate every confirmed frame for `page-scroll` pages in top-to-bottom order, with stable global chrome and clear visual continuity between adjacent frames.
   - Review the coverage plan after generation. Every required page section must appear in at least one frame before the page is complete.
   - Mobile mockups are allowed only for pages the user explicitly requested as mobile; name them clearly, such as `01-mobile-repair-request.png`.
   - Keep UI density realistic for the product type; avoid generic admin templates, landing-page hero compositions, and decorative-only visuals.

5. **Design Document**
   - Read `references/design-document-template.md` before writing `uiux-design.md`.
   - Include PRD-level context, information architecture, page specs, interaction and state notes, visual system, component rules, frontend preview guidance, responsive notes, and the final image prompts.
   - Reference every generated image segment with relative Markdown links and preserve its top-to-bottom reading order.
   - For each page, document its scroll model, full content order, frame coverage, sticky elements, and internal scrolling regions.
   - Make the document the source of truth for exact copy, fields, states, permissions, and preview behavior; generated bitmap text is only visual direction.
   - Include a draft handoff contract that maps requirements, flows, pages, components, states, UI data, API capability needs, and acceptance criteria.

6. **Review And Iteration**
   - After delivery, summarize artifacts and call out assumptions or unresolved risks.
   - If the user requests changes, update the brief, regenerate only affected images, revise `uiux-design.md`, and update the preview only when one exists.

7. **Optional Interactive Frontend Preview**
   - If the user confirms they want a preview, read `references/frontend-preview.md`.
   - Build a browser-ready prototype that follows the approved design document and mockups.
   - Demonstrate the confirmed routes, navigation, filters, forms, dialogs, and important states with mock data and local interactions.
   - Keep fixtures and mock service adapters outside visual components so future developers can replace them without redesigning the UI.
   - Verify desktop and mobile layouts and the confirmed interactions in a browser.
   - For every `page-scroll` route, capture and review a browser full-page screenshot in addition to viewport screenshots.
   - Stop after the frontend preview. Do not continue into backend or production system development.

8. **Final Development Handoff**
   - Read `references/development-handoff.md` before final delivery.
   - Finalize the handoff contract inside `uiux-design.md`: source precedence, traceability, route and page map, component inventory, interaction and state matrix, UI data contracts, API capability requirements, acceptance criteria, and preview-to-production guidance.
   - Map every preview route back to a `PAGE-###` entry when a preview exists.
   - Describe backend needs only as capabilities required by the UI. Do not design backend architecture or claim the preview is production-ready.

## Quality Bar

- Strong design direction without sacrificing implementation realism.
- Clear hierarchy, compact but readable enterprise density, stable component sizing, and no overlapping text.
- Distinctive palette with more than one hue family; avoid one-note purple/blue, generic beige, and stock dark dashboard sameness.
- Real product surfaces over marketing pages: navigation, content, empty/error/loading states, data tables, forms, filters, details, and role-sensitive actions.
- Handoff-ready writing: enough detail for a faithful frontend preview without pretending generated bitmap text is exact UI copy.
- Preview fidelity over backend breadth: build the approved experience convincingly, but keep all data and business operations local or mocked.
- Traceable handoff: downstream product, frontend, backend, and QA teams can locate the approved requirement, UI surface, interaction state, data need, and acceptance criterion without guessing.
- Complete page coverage: long pages include all confirmed sections across sequential frames, with no missing middle or bottom content and no unreadable page compression.
