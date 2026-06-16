# Interview Checklist

Use this checklist to run a product-manager-style interview. Ask only 3-5 questions per round and adapt to what the user already provided.

## Minimum Viable Brief

- Project name and one-sentence product category
- Business goal and success criteria
- Target users, user roles, and permission boundaries
- Core workflow from entry to completion
- Core pages or page types
- Key data objects and their important fields
- Primary actions, approvals, notifications, and audit needs
- Visual preferences, reference images, brands to avoid, and tone
- Technical or organizational constraints
- Delivery scope: images only, document only, or optional frontend preview later

## Useful Question Patterns

Start broad:

1. What business problem should this product solve?
2. Who uses it daily, and who only reviews or approves?
3. What is the most important workflow the UI must make easier?

Fill product structure:

1. What are the main data objects users create, edit, approve, or search?
2. Which roles need different navigation, fields, or actions?
3. Which pages are required, and which can be inferred by Codex?

Shape the design:

1. Should this feel operational, executive, creative, technical, financial, medical, industrial, or something else?
2. Do you have references or existing brand constraints?
3. Should the UI be high-density for repeated work or calmer for review and decision-making?

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

## Page Inventory

1. Login
2. Dashboard
3. ...
9. Design system

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
