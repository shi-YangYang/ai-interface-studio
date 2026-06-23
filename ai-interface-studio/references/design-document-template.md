# Design Document Template

Use this structure for `gpt-images/uiux/<project-slug>/uiux-design.md`. Keep it concise, design-complete, and ready to guide an optional frontend preview.

## Contents

1. Product Brief
2. Roles And Permissions
3. Information Architecture
4. Visual Concept
5. Generated Images
6. Page Specifications
7. Component And Interaction Rules
8. Responsive And Mobile Notes
9. Frontend Preview Specification
10. Development Handoff Contract
11. Image Prompts

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

| File | Page ID | Page | Segment | Coverage |
| --- | --- | --- | --- | --- |
| [00-design-system.png](00-design-system.png) | N/A | Design system | N/A | Global visual/component rules |
| [01-login.png](01-login.png) | `PAGE-001` | Login | Single | Complete page |
| [03-settings-01-top.png](03-settings-01-top.png) | `PAGE-003` | Settings | 1/3 Top | Header, profile, account |

## 6. Page Specifications

### 6.1 [Page Name]

- Scroll model: single viewport / page scroll / internal scroll
- Images in reading order:
  1. `[file-name-01-top.png](file-name-01-top.png)`
  2. `[file-name-02-content.png](file-name-02-content.png)`
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

| Segment | Image | Scroll Position | Required Sections | Previous / Next Continuity Anchor |
| --- | --- | --- | --- | --- |
| 1/3 | `file-name-01-top.png` | Top | ... | None / ... |
| 2/3 | `file-name-02-content.png` | Middle | ... | ... / ... |
| 3/3 | `file-name-03-bottom.png` | Bottom | ... | ... / None |

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

## 9. Frontend Preview Specification

- Preview required: yes/no
- Preview scope:
- Routes and screens:
- Component breakdown:
- Mock data:
- Local interactions:
- Design tokens:
- Responsive targets:
- Accessibility notes:
- Explicitly out of scope: backend services, databases, production authentication, payments, external service integrations, deployment, and operations

## 10. Development Handoff Contract

### 10.1 Source Of Truth

1. `uiux-design.md`
2. Frontend preview
3. Design-system image and page mockups
4. Generated bitmap microcopy

### 10.2 Traceability Map

| Requirement / Flow ID | Page ID / Route | Interaction Or State | Preview Location | Acceptance IDs |
| --- | --- | --- | --- | --- |
| `REQ-001` / `FLOW-001` | `PAGE-001` / `/example` | `STATE-001` | `src/pages/...` | `AC-001` |

### 10.3 Route And Page Map

| Page ID | Page | Route / Entry | Scroll Model | Coverage Segments | Roles | Upstream | Downstream | Preview Path |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| `PAGE-001` | ... | ... | ... | ... | ... | ... | ... | ... |

### 10.4 Component Inventory

| Component ID | Component | Variants / States | Used By | Token Dependencies | Reuse Notes |
| --- | --- | --- | --- | --- | --- |
| `COMP-001` | ... | ... | ... | ... | ... |

### 10.5 Interaction And State Matrix

| Flow / Page | Trigger | Preconditions | Loading | Success | Empty | Error | Disabled / Denied | Next Step |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| ... | ... | ... | ... | ... | ... | ... | ... | ... |

### 10.6 UI Data Contracts

| View Model | Field | Type | Required | Meaning | Example | Validation / Formatting | Visibility |
| --- | --- | --- | --- | --- | --- | --- | --- |
| ... | ... | ... | ... | ... | ... | ... | ... |

These are UI-facing contracts, not database schemas.

### 10.7 API Capability Requirements

| Capability ID | Consumer Page / Flow | Operation | Input | Expected Output | Error Cases | Permission | Data Notes |
| --- | --- | --- | --- | --- | --- | --- | --- |
| `CAP-001` | ... | ... | ... | ... | ... | ... | ... |

Describe required outcomes only. Do not invent endpoint URLs, database tables, service boundaries, or infrastructure.

### 10.8 Acceptance Criteria

| Acceptance ID | Requirement / Flow | Given | When | Then | Viewport / Role |
| --- | --- | --- | --- | --- | --- |
| `AC-001` | ... | ... | ... | ... | ... |

### 10.9 Preview-To-Production Guidance

- Reusable preview routes/components/tokens:
- Mock fixtures and adapters to replace:
- Production stack differences:
- Known gaps and assumptions:
- Explicitly out of scope:

## 11. Image Prompts

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
- Treat generated image text as directional only; do not copy uncertain bitmap microcopy as final product copy.
- Link images relatively so the folder can move as a unit.
- State assumptions plainly.
- Keep preview guidance practical; name components, mock data shapes, and local interactions when helpful.
- Include enough state coverage for a convincing prototype: default, hover/focus where relevant, loading, empty, error, disabled, and permission-denied.
- Never invent backend architecture or present the frontend preview as a production-ready application.
- Preserve stable IDs across revisions and keep every critical requirement traceable to at least one page and acceptance criterion.
- Do not mark a long page complete until every section in its full content order is covered by at least one linked image segment.
