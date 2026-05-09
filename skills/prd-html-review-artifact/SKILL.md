---
name: prd-html-review-artifact
description: Create a standalone HTML handoff artifact from completed PRD markdown workspaces. Use when Codex finishes a delivery-grade PRD workflow, needs to turn PRD source files into a human-readable handoff console, or when the user asks for HTML/readability/visual PRD output.
---

# PRD HTML Handoff Artifact

## Purpose

Turn completed PRD stage Markdown into a single-file HTML artifact for human handoff while keeping Markdown as the source of truth.

Use this after `prd-09-prd-compressor`, or when a user explicitly asks to make a PRD easier to read, share, present, or review.

Do not create HTML as a way to keep the pipeline moving past unresolved blockers. The default HTML artifact represents a completed PRD; finish the PRD first.

## Output Contract

For a PRD workspace, create or update:

```text
docs/prd-workspace/{feature-name}/
  design-language.md
  09-review.html
```

Keep existing stage files unchanged unless the user asks to revise the PRD content.

## Workflow

1. Read `08-delivery-prd.md` first.
2. Read `07-risk-review.md` and `06-data-acceptance.md` when risks, decisions, metrics, or acceptance details need stronger structure.
3. Reuse `design-language.md` when it already exists and the user has not asked to update visual direction.
4. If `design-language.md` does not exist, use `visual-taste-lab` when available to analyze the PRD content and create `design-language.md`.
5. If `visual-taste-lab` is unavailable, infer the design language from the PRD content yourself and continue.
6. Generate `09-review.html` as a standalone file with inline CSS and minimal inline JavaScript.
7. Verify desktop and mobile rendering with screenshots when Playwright or a browser tool is available.
8. Fix visible overflow, clipped text, incoherent spacing, and mobile horizontal scroll caused by layout rather than intentional table scrolling.

## Design Language Rules

Start from the artifact's job, not decoration.

If `design-language.md` already exists, treat it as the visual source of truth unless the user asks for a refresh.

When creating `design-language.md`, use `visual-taste-lab` if available. Do not ask the user to confirm style; style is a support decision, not a PRD blocker. Choose a direction based on the document:

- Rule-heavy PRDs should become dense engineering handoff documents.
- Strategy-heavy PRDs should become decision memos with clear rationale and trade-offs.
- Operations-heavy PRDs should become operational consoles focused on controls, exceptions, and responsibility.
- Experience-heavy PRDs should foreground functional behavior, flows, states, and acceptance evidence.

All directions must stay readable, table-friendly, and handoff-oriented. Do not use fake product screenshots, phone mockups, decorative gradients, marketing hero layouts, or visual-demo patterns unless the user explicitly asks.

## Required HTML Sections

Include these sections unless the PRD is too narrow for them:

```text
Overview / Delivery gate
Feature behavior
Sign-off defaults
Scope boundary
Flow
Core rules
Experience or page requirements
Metrics
Acceptance criteria
Risks and history checks
Source note
```

The first viewport should answer:

- What is this PRD about?
- Is it ready for handoff?
- How does the core feature work in plain product language?
- Which recommended defaults still need stakeholder sign-off?
- What is the biggest risk?

## Interaction Rules

Use interaction only when it improves handoff:

- Rule table filters are useful.
- Metric group filters are useful.
- Copy/export actions are useful only if they produce a real artifact.
- Do not add decorative animations.
- Do not add buttons that do not perform a real action.

## Content Rules

- Do not invent new PRD decisions, metrics, customers, screenshots, business claims, or implementation facts.
- Preserve recommended defaults, sign-off notes, risks, and non-blocking history checks.
- Include a visible `Feature behavior` or equivalent section near the top. Do not start the body with metrics, risks, or sign-off cards before explaining the core product behavior.
- Use concise labels and cards to expose uncertainty instead of hiding it in prose.
- Keep PRD source Markdown authoritative; HTML is a reading and handoff layer.

## Validation

When possible, run:

```powershell
npx playwright screenshot --viewport-size=1440,1100 "file:///ABS/PATH/09-review.html" "ABS/PATH/09-review-desktop.png"
npx playwright screenshot --viewport-size=390,1200 "file:///ABS/PATH/09-review.html" "ABS/PATH/09-review-mobile.png"
```

Then inspect screenshots. Fix:

- clipped titles;
- overlapping cards;
- unintended page-level horizontal overflow;
- text too small or too large for its container;
- visual emphasis that hides blockers or risks.

Intentional horizontal scrolling inside wide tables is acceptable.
