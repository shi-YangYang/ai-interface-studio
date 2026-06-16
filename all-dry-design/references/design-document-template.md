# Design Document Template

Use this structure for `gpt-images/uiux/<project-slug>/uiux-design.md`. Keep it concise but implementation-ready.

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

| File | Page | Purpose |
| --- | --- | --- |
| [00-design-system.png](00-design-system.png) | Design system | Global visual/component rules |
| [01-login.png](01-login.png) | Login | Authentication entry |

## 6. Page Specifications

### 6.1 [Page Name]

- Image: `[file-name.png](file-name.png)`
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
- Implementation notes:

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

## 9. Frontend Implementation Guidance

- Suggested stack:
- Routing:
- State model:
- Component breakdown:
- Design tokens:
- Accessibility notes:
- Browser verification notes:

## 10. Image Prompts

Store the final prompt used for each generated image. This makes regeneration and iteration possible.

For projects with more than 8 business pages, create a sibling `image-prompts.md` instead and link it here:

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
- Keep implementation guidance practical; name components and data structures when helpful.
- Include enough state coverage for frontend work: default, hover/focus where relevant, loading, empty, error, disabled, and permission-denied.
