# PRD Agent Kit

PRD Agent Kit is a Codex skill and agent workflow for turning rough product ideas into complete, usable, delivery-grade PRDs.

It breaks PRD writing into small, auditable stages: idea intake, business boundary, rule modeling, flows, page interactions, admin configuration, data and acceptance, risk/debt resolution, final compression, and an HTML handoff artifact.

Chinese documentation: [README_CN.md](README_CN.md)

## What This Is For

Use this kit when you want an agent to:

- turn a rough idea, user feedback, operations request, or strategy direction into a PRD;
- avoid one huge vague AI-generated PRD;
- resolve assumptions, risks, rule gaps, and missing decisions through stage loops;
- produce Markdown source artifacts plus a human-readable HTML handoff artifact.

Do not use the full workflow for one small copy edit, one isolated metric table, or a narrow rule change. Use the relevant stage skill directly for those cases.

## Repository Layout

```text
prd-agent-kit/
  AGENTS.md
  skills/
    prd-00-pipeline-orchestrator/
    prd-01-idea-intake/
    prd-02-business-boundary/
    prd-03-rule-modeler/
    prd-04-flow-modeler/
    prd-05-page-interaction/
    prd-06-admin-config/
    prd-07-data-acceptance/
    prd-08-risk-debt-review/
    prd-09-prd-compressor/
    prd-html-review-artifact/
  docs/
  examples/
```

`AGENTS.md` is the workspace-level agent instruction. `skills/` contains the Codex skills used by the workflow.

## Quick Install

1. Clone this repository.
2. Copy every folder under `skills/` into your Codex skills directory.
3. Copy `AGENTS.md` into the workspace where you want to run PRD generation.

See [docs/install.md](docs/install.md) for exact commands.

## Basic Usage

In a workspace that contains this repo's `AGENTS.md`, ask Codex something like:

```text
Turn this idea into a delivery-grade PRD:

We need a merchant coupon budget control feature. Operators should be able to set campaign budget caps, stop over-issuance, and review risk before launch.
```

The agent will create staged artifacts under:

```text
docs/prd-workspace/{feature-name}/
```

Expected output shape:

```text
00-intake.md
01-boundary.md
02-rules.md
03-flows.md
04-pages.md
05-admin-config.md
06-data-acceptance.md
07-risk-review.md
08-delivery-prd.md
design-language.md
09-review.html
```

## Workflow

The full workflow is coordinated by `prd-00-pipeline-orchestrator`, then executed through the stage skills in order. The final `prd-html-review-artifact` skill turns the Markdown source into a standalone HTML handoff artifact.

See [docs/workflow.md](docs/workflow.md) for the stage-by-stage breakdown.

## Customization

You can edit any `SKILL.md` file to change the behavior of one stage. You can also edit `AGENTS.md` to change workspace-level defaults such as language, output folder, or stage gates.

See [docs/customization.md](docs/customization.md).

## License

MIT License. See [LICENSE](LICENSE).
