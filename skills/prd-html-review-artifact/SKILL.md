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
3. Create or update `design-language.md` before editing HTML.
4. Generate `09-review.html` as a standalone file with inline CSS and minimal inline JavaScript.
5. Verify desktop and mobile rendering with screenshots when Playwright or a browser tool is available.
6. Fix visible overflow, clipped text, incoherent spacing, and mobile horizontal scroll caused by layout rather than intentional table scrolling.

## Design Language Rules

Start from the artifact's job, not decoration.

For PRD handoff artifacts, prefer an institutional handoff console:

- Archetype: Evidence-Led Report + Dense Operational Dashboard.
- Mood: precise, calm, scannable, decision-first.
- Visual priority: delivery conclusion, sign-off defaults, scope, flow, rules, metrics, acceptance, risks.
- Layout: compact header, left or top navigation, decision cards, dense tables, functional diagrams.
- Color: neutral document base, one primary blue, one positive teal/green, red only for blocking decisions, amber only for controlled risk.
- Geometry: small radius, clear borders, minimal shadow.
- Imagery: no fake product screenshots, phone mockups, decorative gradients, or marketing hero unless the user explicitly asks.

If the user requests a different visual direction, state the direction and update `design-language.md` first.

## Required HTML Sections

Include these sections unless the PRD is too narrow for them:

```text
Overview / Delivery gate
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
