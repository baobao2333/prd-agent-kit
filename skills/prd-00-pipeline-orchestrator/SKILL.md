---
name: prd-00-pipeline-orchestrator
description: Orchestrate a product idea into a reviewable PRD workspace by running the PRD skills with stage gates and feedback loops. Use when the user asks to run the full idea-to-PRD workflow, create a PRD from a rough idea, or coordinate multiple PRD drafting stages. Do not use for editing one isolated rule, one page, or one metric table.
---

# PRD Pipeline Orchestrator

## Purpose

Coordinate the full workflow from rough idea to business-usable PRD workspace. This skill does not write every detail itself. It decides which PRD sub-skills should be used, in what order, what artifact each stage must produce, and when a later stage must send work back for revision.

The core principle:

> AI expands possibilities; product management compresses them into executable consensus.

## Inputs

Accept any of the following:

- A rough product idea.
- A user feedback fragment.
- An operations request.
- A boss/strategy direction.
- A half-written PRD.
- A feature change proposal.

## Operating rules

1. Do not pretend the system context is known.
2. Do not ask a long questionnaire before producing value.
3. Start with a lightweight assumption map, then mark unknowns.
4. Keep each stage output small enough for the next stage to consume.
5. Preserve uncertainty labels: `Fact`, `Assumption`, `Decision needed`, `Risk`, `Out of scope`.
6. Never let a draft look more certain than the product manager is ready to sign off.
7. Write PRD content in Chinese by default unless the user asks for another language.
8. Ask at most 3 blocking questions per stage. Continue with explicit assumptions for non-blocking unknowns.
9. Each stage should create or update only its own stage artifact. Do not merge all details into the final PRD early.
10. If a later stage exposes a `Rule gap`, return to the relevant earlier artifact and update it before continuing.
11. If a stage has unresolved blocking `Decision needed` items, pause before treating the next artifact as `Review-ready`.
12. `prd-06-admin-config` may conclude that no admin or operations config is needed for this version. Do not invent admin requirements.

## Dialectical loop

Before moving from one stage to the next, run a short challenge pass:

1. State the current leading recommendation.
2. Name at least one credible alternative or "do nothing / defer" option.
3. List what evidence would make the recommendation wrong.
4. Check whether the next stage depends on an unresolved product, data, legal, cost, or architecture decision.
5. If the missing decision changes scope, rules, flow, acceptance, or operations, update the earlier artifact first instead of carrying the gap forward.

Do not force a single preferred decision when the inputs do not support one. Preserve competing options with trade-offs and owners until the user or stakeholder chooses.

## Stage gates

| Gate | If true | Action |
|---|---|---|
| Blocking `Decision needed` remains | The next artifact would imply a product choice | Stop and ask for the decision, or mark the workspace as `Needs product decision` if the user wants a review artifact |
| `Rule gap` appears in flow, page, data, or risk review | Existing rules cannot explain the behavior | Return to `prd-03-rule-modeler` and update `02-rules.md` |
| Acceptance criteria contain vague results such as "may", "significant", or "baseline" without a numeric or observable definition | QA cannot verify the case | Return to `prd-07-data-acceptance` before final compression |
| Admin config exists only because it is convenient, not necessary | Operations scope is expanding | Return to `prd-06-admin-config` and move it to hardcoded or later |
| Risk review status is `Needs product decision`, `Needs technical confirmation`, or `Not ready` | The final PRD cannot be called ready | Generate a decision-review PRD, not a review-ready PRD |

## Recommended stage order

Run these skills in order unless the user explicitly narrows the task:

1. `prd-01-idea-intake` — turn the rough idea into a problem brief.
2. `prd-02-business-boundary` — define scope, version boundary, and non-goals.
3. `prd-03-rule-modeler` — convert descriptions into rules, states, permissions, and conditions.
4. `prd-04-flow-modeler` — produce user flow, system judgment flow, and exception flow.
5. `prd-05-page-interaction` — describe pages, components, copy states, and interaction states.
6. `prd-06-admin-config` — identify necessary backend / operations controls only.
7. `prd-07-data-acceptance` — define metrics, event tracking, and acceptance tests.
8. `prd-08-risk-debt-review` — review historical debt, compatibility, abuse, cost, and responsibility risks.
9. `prd-09-prd-compressor` — compress all stage artifacts into either a review-ready PRD or a decision-review PRD, depending on unresolved gates.

## Output format

Create or update a working folder such as:

```text
docs/prd-workspace/{feature-name}/
  00-intake.md
  01-boundary.md
  02-rules.md
  03-flows.md
  04-pages.md
  05-admin-config.md
  06-data-acceptance.md
  07-risk-review.md
  08-review-ready-prd.md
```

If the user has not provided a feature name, generate a short kebab-case name from the idea.

## Definition of done

The workflow is complete when:

- The final PRD clearly states what this version does and does not do.
- Core rules are expressed as conditions, states, thresholds, and outcomes.
- Major exceptions are covered.
- Unknowns are not hidden.
- A developer can estimate the work without guessing product intent, or the document clearly says which decisions block estimation.
- A tester can write cases from the acceptance section, or the document clearly says which vague criteria block QA.
- The product manager can see what they must sign off on.

If these conditions are not met, the workflow may still produce a useful review artifact, but it must be labeled `Needs product decision`, `Needs technical confirmation`, or `Not ready` instead of `Review-ready`.
