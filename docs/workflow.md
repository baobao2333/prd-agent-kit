# Workflow

The PRD workflow is staged so each artifact has a clear job and can be corrected before the final delivery PRD is produced.

Every delivery PRD should include a prose feature behavior section. Tables define rules and evidence, but the reader should understand the core product behavior before reading the tables.

## Stages

| Stage | Skill | Output |
|---|---|---|
| 00 | `prd-00-pipeline-orchestrator` | Coordinates the full workflow |
| 01 | `prd-01-idea-intake` | `00-intake.md` |
| 02 | `prd-02-business-boundary` | `01-boundary.md` |
| 03 | `prd-03-rule-modeler` | `02-rules.md`, including a functional rule narrative |
| 04 | `prd-04-flow-modeler` | `03-flows.md` |
| 05 | `prd-05-page-interaction` | `04-pages.md` |
| 06 | `prd-06-admin-config` | `05-admin-config.md` |
| 07 | `prd-07-data-acceptance` | `06-data-acceptance.md` |
| 08 | `prd-08-risk-debt-review` | `07-risk-review.md` |
| 09 | `prd-09-prd-compressor` | `08-delivery-prd.md` |
| HTML | `prd-html-review-artifact` | `design-language.md`, `09-review.html` |

## Stage Gates

The workflow should resolve blocking gaps instead of merely recording them. The agent should loop back to the owning artifact, make a conservative recommendation when responsible, and re-run affected later stages. It should ask the user only when a missing choice cannot be safely decided by the agent.

If a flow, page, or acceptance stage exposes a rule gap, return to the rule model before final compression.

## Source Of Truth

Markdown stage files are the source of truth. The HTML artifact is a handoff and presentation layer.

When producing the HTML artifact, reuse an existing `design-language.md` unless the user asks for a refresh. If it does not exist, use `visual-taste-lab` to infer a design language from the PRD content and proceed without asking for style confirmation.
