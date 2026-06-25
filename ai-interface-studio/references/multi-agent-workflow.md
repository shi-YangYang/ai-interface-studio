# Multi-Agent Workflow

Use this reference at project start. The coordinator owns the workflow but delegates specialized production and review work.

## Contents

1. Start Protocol
2. Roles
3. Stage Gates
4. Context Packets
5. Workflow State
6. Fallback

## Start Protocol

Before asking product questions, report:

- Coordination mode: awaiting authorization / multi-agent / sequential fallback
- Coordinator: current main agent
- Specialists: Product/UX, Visual Design, Frontend Implementation, Visual Acceptance
- Current gate: G1
- Gate status: in progress / passed / blocked

If the user has not explicitly authorized delegation, ask for that authorization first. When authorized and subagent tools exist, actually spawn separate agents at their stages. Never describe future persona changes by one Codex instance as a multi-agent workflow.

## Roles

### Coordinator

- Own user communication, confirmations, stage gates, artifact paths, and conflict resolution.
- Maintain `workflow-state.md` as a status ledger, not a design source of truth.
- Give each specialist only the approved files, image paths, target scope, and expected output needed for its stage.
- Do not generate final mockups, implement preview code, or perform the final visual acceptance.
- Do not substitute suggested human reviewers for the Visual Acceptance Agent.

### Product And UX Agent

- Own requirement synthesis, roles, flows, information architecture, page inventory, states, and acceptance intent.
- Write or update the relevant sections of `uiux-design.md`.
- Do not generate final visual mockups or frontend code.

### Visual Design Agent

- Own the design-system image, page mockups, image prompts, visual consistency, and the draft visual-fidelity contract.
- Inspect `00-design-system.png` before every page prompt, and regenerate page mockups that do not inherit its visual system.
- For scrolling pages, generate exactly one vertical long-page mockup, reject landscape overview outputs, and record the image-to-browser scale contract.
- Return original artifact paths and unresolved visual risks. Do not implement frontend code.

### Frontend Implementation Agent

- Own only `frontend-preview/<project-slug>/` and implementation notes requested by the coordinator.
- Read `uiux-design.md` and inspect every assigned original mockup before editing.
- Implement the shared shell first, then small page batches.
- Do not change approved mockups, weaken the visual contract, or self-approve the preview.

### Visual Acceptance Agent

- Remain independent from implementation.
- Inspect original mockups, the visual-fidelity contract, and browser screenshots at matching viewports.
- Record evidence-based `VIS-###` findings in `visual-review.md`.
- Do not edit frontend code. Accept only when no blocker or major visual findings remain.

## Stage Gates

| Gate | Required Evidence | Owner | Next Stage |
| --- | --- | --- | --- |
| G1 Brief confirmed | Requirement confirmation, page inventory, coverage plan | Coordinator + Product/UX | Visual design |
| G2 Visual direction approved | Design system and approved page mockups | Coordinator + Visual Design | Visual contract |
| G3 Visual contract frozen | Per-page visual-fidelity contract in `uiux-design.md` | Coordinator + Visual Design | Frontend implementation |
| G4 Preview ready for review | Running preview, route map, matching viewport screenshots | Frontend Implementation | Visual acceptance |
| G5 Visual acceptance passed | `visual-review.md`, no open blocker or major findings | Visual Acceptance | Final handoff |

Do not skip gates because earlier context feels clear. Evidence on disk, not conversational memory, opens the next gate.
Use the exact G1-G5 names in user-facing progress so the workflow cannot drift into an informal phase list.
Gate names describe their exit condition. Do not call `G1 Brief confirmed` passed while intake or user confirmation is still pending; report `G1 in progress` until the evidence exists.

## Context Packets

Every delegation message must include:

- Role and ownership boundary
- Current gate and exact task
- Approved artifact paths
- Required output paths
- Forbidden actions
- Completion criteria

Do not paste the entire conversation when approved artifacts already contain the needed decisions. Do not replace image paths with a prose summary.

## Workflow State

Use this compact format for `workflow-state.md`:

```md
# Workflow State

- Mode: multi-agent / sequential fallback
- Current gate: G1-G5
- Gate status: in progress / passed / blocked
- Approved by user:
- Active owner:
- Inputs:
- Expected outputs:
- Completed artifacts:
- Open decisions:
- Open VIS findings:
```

Only the coordinator edits this file. Product and visual decisions still belong in `uiux-design.md`.

## Fallback

When subagents are unavailable:

1. Tell the user that execution will use sequential role separation.
2. Finish and save each role's artifacts before changing roles.
3. Re-read the saved artifacts and original images at every gate.
4. State clearly that visual review was not independent.
5. Never claim multi-agent acceptance.
