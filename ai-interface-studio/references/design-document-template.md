# Design Document Template

Use this structure for `gpt-images/uiux/<project-slug>/uiux-design.md`. Keep it concise, design-complete, and precise enough to constrain an optional frontend preview.

## Contents

1. Product Brief
2. Roles And Permissions
3. Information Architecture
4. Visual Concept
5. Generated Images
6. Page Specifications
7. Component And Interaction Rules
8. Responsive And Mobile Notes
9. Frontend Implementation Strategy
10. Frontend Preview Specification
11. Development Handoff Contract
12. Image Prompts

```md
# [Project Name] UI/UX Design

## 1. Product Brief

- Product category:
- Business goal:
- Primary users:
- Core workflow:
- Success criteria:
- Constraints:

## 2. Roles And Permissions

| Role | Responsibilities | Key Permissions | UI Differences |
| --- | --- | --- | --- |
| ... | ... | ... | ... |

## 3. Information Architecture

- Navigation model:
- Page inventory:
- Page coverage summary:
- Cross-page patterns:
- Search/filter/sort patterns:

## 4. Visual Concept

- Concept name:
- Design thesis:
- Palette:
- Typography:
- Layout grid and spacing:
- Component language:
- Iconography:
- Motion and feedback:

## 5. Generated Images

| File | Page ID | Page | Reference Type | Viewport | Approval | Coverage |
| --- | --- | --- | --- | --- | --- | --- |
| [00-design-system.png](00-design-system.png) | N/A | Design system | N/A | 1440x900 | Approved | Global visual/component rules |
| [01-login.png](01-login.png) | `PAGE-001` | Login | Single | 1440x900 | Approved | Complete page |
| [03-settings-long.png](03-settings-long.png) | `PAGE-003` | Settings | Vertical long-page | 864x1821 | Approved | Complete scroll-page structure |

## 6. Page Specifications

### 6.1 [Page Name]

- Scroll model: single viewport / page scroll / internal scroll
- Coverage strategy: single viewport / vertical long-page / internal scroll
- Reference viewport:
- Reference browser CSS width:
- Image pixel dimensions:
- Scale contract:
- Images in reading order:
  1. `[file-name-long.png](file-name-long.png)`
- Full content order:
- Sticky elements:
- Internal scrolling regions:
- Purpose:
- Primary users:
- Entry points:
- Layout:
- Main components:
- Primary actions:
- Secondary actions:
- Data shown:
- Empty state:
- Loading state:
- Error state:
- Permission notes:
- Preview notes:

#### Page Coverage Plan

| Reference Type | Image | Scroll Position | Required Sections | Continuity Role |
| --- | --- | --- | --- | --- |
| Vertical long-page | `file-name-long.png` | Full scroll page | ... | Canonical implementation reference |

#### Visual Fidelity Contract

- Canonical reference images:
- Reference viewport:
- Coverage strategy and continuity rule:
  - `00-design-system.png` controls palette, typography hierarchy, shell language, component shapes, spacing rhythm, icon treatment, and density.
  - Vertical long-page mockup controls top-to-bottom composition, section order, section transitions, and page-level proportions.
  - Scale formula: `reference_css_width / image_pixel_width = scale`; `expected_css_page_height = image_pixel_height * scale`.
  - No landscape overview, same-size compressed overview, or separate AI-generated detail segment may override the long-page mockup or design system.
- Visual invariants that must remain recognizable:
- Allowed deviations:
- Responsive transformation:

| Region | Geometry / Proportion | Layout And Alignment | Typography | Palette / Surface | Components And Density |
| --- | --- | --- | --- | --- | --- |
| Application shell | ... | ... | ... | ... | ... |
| Primary content | ... | ... | ... | ... | ... |
| Secondary region | ... | ... | ... | ... | ... |

| Token Group | Approved Values / Rules | Reference Evidence |
| --- | --- | --- |
| Spacing and grid | ... | ... |
| Radii, borders, shadows | ... | ... |
| Type scale and weights | ... | ... |
| Color roles | ... | ... |

Freeze this contract before preview implementation. Record any later change as an explicit approved deviation.

## 7. Component And Interaction Rules

- Navigation:
- Forms:
- Tables:
- Filters:
- Charts:
- Cards:
- Modals/drawers:
- Status tags:
- Notifications:
- Validation:

## 8. Responsive And Mobile Notes

Document mobile and responsive behavior. Do not imply mobile images were generated unless the user explicitly requested them.

## 9. Frontend Implementation Strategy

Freeze this section and get user approval before preview code starts.

- Strategy status: proposed / approved / revised
- Approved by:
- Target repository:
- Framework and runtime:
- UI library:
- Styling system:
- Icon set:
- Charting and data visualization:
- Drawing / diagram technology:
- 3D / rendering technology:
- Motion / animation:
- Supporting image or media assets:
- Required custom components:
- Reference reconstruction mode: required
- Rejected alternatives:
- Known fidelity risks:

| Page / Region | Reference Visual | Implementation Method | Library / Asset | Fidelity Risk | Acceptance Note |
| --- | --- | --- | --- | --- | --- |
| `PAGE-001` / ... | `01-...png` | ... | ... | Low/Medium/High | ... |

### 9.1 Reference Reconstruction Map

Use this as the implementation checklist for screenshot-level reproduction. Default `Omission Allowed` to `No`; any `Yes` must be explicitly approved by the user.

| ID | Page / Region | Visible Element Or Effect | Reference Evidence | Required Implementation | Match Rule | Omission Allowed |
| --- | --- | --- | --- | --- | --- | --- |
| `RECON-001` | `PAGE-001` / ... | ... | `01-...png` | ... | same count / order / alignment / proportion / layer treatment | No |

Rules:

- Do not use the default stack until this strategy is approved.
- Do not replace distinctive UI, charts, drawings, 3D effects, maps, or material treatments with generic components unless the deviation is approved here.
- Do not begin frontend implementation until every implemented route has a reconstruction map.
- If the chosen stack cannot reproduce an approved region, return to the coordinator for a revised strategy before implementation.

## 10. Frontend Preview Specification

- Preview required: yes/no
- Preview scope:
- Routes and screens:
- Component breakdown:
- Mock data:
- Local interactions:
- Design tokens:
- Reference mockups and viewports:
- Long-page reference strategy:
- Visual fidelity target:
- Screenshot evidence location:
- Independent review required: yes/no
- Responsive targets:
- Accessibility notes:
- Explicitly out of scope: backend services, databases, production authentication, payments, external service integrations, deployment, and operations

## 11. Development Handoff Contract

### 11.1 Source Of Truth

- Requirements, exact copy, fields, permissions, states, behavior, and acceptance criteria: `uiux-design.md`
- Composition, visual hierarchy, palette, typography scale, spacing, component appearance, and density: approved mockups plus the visual-fidelity contract
- Technical reproduction choices for preview: approved frontend implementation strategy
- Required visible elements and effects for preview: reference reconstruction map
- Approved interaction and responsive behavior: accepted frontend preview
- Generated bitmap microcopy: direction only
- Conflicts: explicit coordinator decision required

### 11.2 Traceability Map

| Requirement / Flow ID | Page ID / Route | Interaction Or State | Preview Location | Acceptance IDs | Visual Review IDs |
| --- | --- | --- | --- | --- | --- |
| `REQ-001` / `FLOW-001` | `PAGE-001` / `/example` | `STATE-001` | `src/pages/...` | `AC-001` | `VIS-001` |

### 11.3 Route And Page Map

| Page ID | Page | Route / Entry | Scroll Model | Reference Mockups | Review Viewport | Roles | Upstream | Downstream | Preview Path |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| `PAGE-001` | ... | ... | ... | ... | ... | ... | ... | ... | ... |

### 11.4 Component Inventory

| Component ID | Component | Variants / States | Used By | Implementation Method | Token Dependencies | Reuse Notes |
| --- | --- | --- | --- | --- | --- | --- |
| `COMP-001` | ... | ... | ... | ... | ... | ... |

### 11.5 Interaction And State Matrix

| Flow / Page | Trigger | Preconditions | Loading | Success | Empty | Error | Disabled / Denied | Next Step |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| ... | ... | ... | ... | ... | ... | ... | ... | ... |

### 11.6 UI Data Contracts

| View Model | Field | Type | Required | Meaning | Example | Validation / Formatting | Visibility |
| --- | --- | --- | --- | --- | --- | --- | --- |
| ... | ... | ... | ... | ... | ... | ... | ... |

These are UI-facing contracts, not database schemas.

### 11.7 API Capability Requirements

| Capability ID | Consumer Page / Flow | Operation | Input | Expected Output | Error Cases | Permission | Data Notes |
| --- | --- | --- | --- | --- | --- | --- | --- |
| `CAP-001` | ... | ... | ... | ... | ... | ... | ... |

Describe required outcomes only. Do not invent endpoint URLs, database tables, service boundaries, or infrastructure.

### 11.8 Acceptance Criteria

| Acceptance ID | Requirement / Flow | Given | When | Then | Viewport / Role |
| --- | --- | --- | --- | --- | --- |
| `AC-001` | ... | ... | ... | ... | ... |

### 11.9 Visual Fidelity Evidence

| Page ID | Approved Reference | Browser Screenshot | Viewport | Open VIS Findings | Repair Owner | Result |
| --- | --- | --- | --- | --- | --- | --- |
| `PAGE-001` | `01-login.png` | `review/PAGE-001.png` | 1440x900 | None | N/A | Pass |
| `PAGE-003` | `03-settings-long.png` | `review/PAGE-003-full.png` | 1440xfull-page | None | N/A | Pass |

- Visual reviewer: independent agent / sequential fallback
- Review report: `[visual-review.md](visual-review.md)`
- Repair routing: coordinator routed findings only; code changes were made by Frontend Implementation Agent / Frontend Repair Agent / N/A
- Accepted deviations:

### 11.10 Preview-To-Production Guidance

- Reusable preview routes/components/tokens:
- Mock fixtures and adapters to replace:
- Production stack differences:
- Known gaps and assumptions:
- Explicitly out of scope:

## 12. Image Prompts

Store the final prompt used for each generated image. This makes regeneration and iteration possible.

For projects with more than 8 business-page frames, create a sibling `image-prompts.md` instead and link it here:

`Final prompts are stored in [image-prompts.md](image-prompts.md).`

### 00-design-system.png

```text
...
```
```

## Writing Standards

- Make the document the source of truth for exact labels, fields, states, and table content.
- Treat approved images as authoritative for visual composition while keeping generated image text directional only.
- Link images relatively so the folder can move as a unit.
- State assumptions plainly.
- Keep preview guidance practical; name components, mock data shapes, and local interactions when helpful.
- Do not let preview implementation start until the frontend implementation strategy is approved and recorded.
- Do not let preview implementation start until the reference reconstruction map is approved and recorded.
- Do not let the coordinator repair frontend code. If visual review fails, route `VIS-###` fixes to the Frontend Implementation Agent or a Frontend Repair Agent.
- Include enough state coverage for a convincing prototype: default, hover/focus where relevant, loading, empty, error, disabled, and permission-denied.
- Never invent backend architecture or present the frontend preview as a production-ready application.
- Preserve stable IDs across revisions and keep every critical requirement traceable to at least one page and acceptance criterion.
- Do not mark a long page complete until every section in its full content order is covered by at least one linked approved image.
- For long pages, require one vertical long-page canonical mockup only. Reject landscape overviews, same-size compressed overviews, and later AI-generated detail segments as competing visual sources. Use the scale contract, design-system image, and visual-fidelity contract to resolve bitmap ambiguity.
- Do not mark a visual-fidelity contract complete when it says only "follow the mockup"; record enough geometry, hierarchy, token, component, and density detail to constrain implementation.
- Do not mark a preview accepted without same-viewport evidence and zero open blocker or major `VIS-###` findings.
