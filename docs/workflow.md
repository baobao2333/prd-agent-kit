# Workflow

The PRD workflow is staged so each artifact has a clear job and can be reviewed independently.

## Stages

| Stage | Skill | Output |
|---|---|---|
| 00 | `prd-00-pipeline-orchestrator` | Coordinates the full workflow |
| 01 | `prd-01-idea-intake` | `00-intake.md` |
| 02 | `prd-02-business-boundary` | `01-boundary.md` |
| 03 | `prd-03-rule-modeler` | `02-rules.md` |
| 04 | `prd-04-flow-modeler` | `03-flows.md` |
| 05 | `prd-05-page-interaction` | `04-pages.md` |
| 06 | `prd-06-admin-config` | `05-admin-config.md` |
| 07 | `prd-07-data-acceptance` | `06-data-acceptance.md` |
| 08 | `prd-08-risk-debt-review` | `07-risk-review.md` |
| 09 | `prd-09-prd-compressor` | `08-review-ready-prd.md` |
| HTML | `prd-html-review-artifact` | `design-language.md`, `09-review.html` |

## Stage Gates

The workflow should pause when a blocking decision remains. Non-blocking uncertainty should be labeled as `Fact`, `Assumption`, `Decision needed`, `Risk`, `Out of scope`, `Needs history check`, or `Rule gap`.

If a flow, page, or acceptance stage exposes a rule gap, return to the rule model before final compression.

## Source Of Truth

Markdown stage files are the source of truth. The HTML artifact is a review and presentation layer.
