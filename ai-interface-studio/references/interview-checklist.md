# Interview Checklist

Use this checklist to run a product-manager-style interview. Ask only 3-5 questions per round and adapt to what the user already provided.

## Minimum Viable Brief

- Project name and one-sentence product category
- Business goal and success criteria
- Target users, user roles, and permission boundaries
- Core workflow from entry to completion
- Core pages or page types
- Page depth and scroll model: single viewport, page scroll, or an internally scrolling workspace
- Ordered content sections for any page that extends beyond one viewport
- Key data objects and their important fields
- Primary actions, approvals, notifications, and audit needs
- Visual preferences, reference images, brands to avoid, and tone
- Technical or organizational constraints
- Delivery scope: images and document only, or images, document, and an optional frontend preview
- Preview scope when requested: routes, key interactions, responsive targets, and states that must be demonstrable
- Preview fidelity target: reference viewports, pages that require close visual reproduction, and acceptable deviations
- Collaboration mode: coordinator-led multi-agent workflow when explicitly authorized, or disclosed sequential fallback
- Explicitly out of scope: backend services, databases, real authentication, production integrations, deployment, and operations

## Useful Question Patterns

Start broad:

1. What business problem should this product solve?
2. Who uses it daily, and who only reviews or approves?
3. What is the most important workflow the UI must make easier?

Fill product structure:

1. What are the main data objects users create, edit, approve, or search?
2. Which roles need different navigation, fields, or actions?
3. Which pages are required, and which can be inferred by Codex?
4. Which pages continue below the first viewport, and what sections must appear from top to bottom?
5. Which navigation, toolbars, or sidebars stay sticky while the page or an inner region scrolls?

Shape the design:

1. Should this feel operational, executive, creative, technical, financial, medical, industrial, or something else?
2. Do you have references or existing brand constraints?
3. Should the UI be high-density for repeated work or calmer for review and decision-making?

Shape the optional preview:

1. Is a browser-ready frontend preview required after the UI/UX design is approved?
2. Which routes and interactions must be clickable in the preview?
3. Which desktop and mobile viewport targets matter for review?
4. Should any page allow deliberate visual deviations from the approved mockup?

Confirm collaboration:

1. Explain that the standard preview workflow delegates product/UX, visual design, frontend implementation, and visual acceptance to separate agents.
2. Ask once for explicit multi-agent authorization when the user has not already requested delegation.
3. If subagents are unavailable, disclose the sequential fallback before work begins.
4. Do not begin the product interview until the coordination mode, role roster, and G1 status have been stated.

Shape the development handoff:

1. Will downstream frontend work reuse the preview stack or reimplement the design in another stack?
2. Which existing routes, design system, components, or API conventions must the handoff respect?
3. Which flows require explicit acceptance criteria for product, engineering, or QA review?

Resolve uncertainty:

1. Offer 2-3 plausible choices when the user is unsure.
2. Mark unresolved items as assumptions only after telling the user the risk.
3. Ask for confirmation once the brief and page inventory are coherent enough to design.

## Confirmation Format

Use this compact structure before image generation:

```md
## Requirement Confirmation

Project:
Business goal:
Primary users:
Roles and permissions:
Core workflow:
Key data objects:
Constraints:
Frontend preview scope:
Reference review viewports:
Multi-agent delegation: authorized / not authorized / unavailable
Downstream development target:
Out of scope:

## Page Inventory

1. Login
2. Dashboard
3. ...
9. Design system

## Page Coverage Plan

| Page | Scroll Model | Frames | Ordered Sections | Sticky / Internal Scroll Notes |
| --- | --- | ---: | --- | --- |
| Login | Single viewport | 1 | Authentication form | None |
| Settings | Page scroll | 3 | Header -> profile -> security -> notifications -> danger zone | Sticky section nav |

Total business-page frames:
Total images including design system:

## Visual Concept

Concept name:
Design thesis:
Palette:
Typography:
Layout and density:
Component language:
Interaction tone:

## Assumptions And Risks

- ...
```
