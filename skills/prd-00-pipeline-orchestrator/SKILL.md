---
name: prd-00-pipeline-orchestrator
description: Orchestrate a product idea into a complete, delivery-grade PRD workspace by running the PRD skills with stage gates and automatic feedback loops. Use when the user asks to run the full idea-to-PRD workflow, create a PRD from a rough idea, or coordinate multiple PRD drafting stages. Do not use for editing one isolated rule, one page, or one metric table.
---

# PRD Pipeline Orchestrator

## Purpose

Coordinate the full workflow from rough idea to business-usable, delivery-grade PRD workspace. This skill does not write every detail itself. It decides which PRD sub-skills should be used, in what order, what artifact each stage must produce, and when a later stage must send work back for revision. Its goal is to finish the PRD, not to produce a list of reasons why the PRD is unfinished.

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
6. Never let a draft hide uncertainty, but also do not leave solvable gaps unresolved.
7. Write PRD content in Chinese by default unless the user asks for another language.
8. Ask at most 3 blocking questions per stage. Continue with explicit assumptions for non-blocking unknowns.
9. Each stage should create or update only its own stage artifact. Do not merge all details into the final PRD early.
10. If a later stage exposes a `Rule gap`, return to the relevant earlier artifact and update it before continuing.
11. If a stage has unresolved blocking `Decision needed` items, resolve them through the delivery loop before continuing.
12. `prd-06-admin-config` may conclude that no admin or operations config is needed for this version. Do not invent admin requirements.

## Delivery loop

When a blocker appears, do not merely record it and continue. Use this loop:

1. Locate the owning artifact: boundary, rules, flow, page, admin, data, or risk.
2. Inspect existing artifacts and any available project context.
3. Choose a conservative default when confidence is high enough for a product owner to review. Record the rationale and rejected alternative.
4. Update the owning earlier artifact.
5. Re-run every later stage affected by that change.
6. Continue only when the downstream artifact is executable by its audience.

Ask the user at most 3 questions only when the missing information is a true business choice that cannot be safely decided by the agent, such as a pricing policy, legal commitment, brand-risk tolerance, budget cap, or stakeholder-specific launch trade-off.

Do not substitute a summary for completion. The normal workflow exists to finish the PRD.

## Dialectical loop

Before moving from one stage to the next, run a short challenge pass:

1. State the current leading recommendation.
2. Name at least one credible alternative or "do nothing / defer" option.
3. List what evidence would make the recommendation wrong.
4. Check whether the next stage depends on an unresolved product, data, legal, cost, or architecture decision.
5. If the missing decision changes scope, rules, flow, acceptance, or operations, run the delivery loop before moving on.

Do not force a careless decision, but do make a recommended default when the available evidence supports one. Preserve competing options in rationale, not as unresolved final PRD branches.

## Stage gates

| Gate | If true | Action |
|---|---|---|
| Blocking `Decision needed` remains | The next artifact would imply a product choice | Run the delivery loop; ask the user only if the choice is truly business-owned |
| `Rule gap` appears in flow, page, data, or risk review | Existing rules cannot explain the behavior | Return to `prd-03-rule-modeler` and update `02-rules.md` |
| Acceptance criteria contain vague results such as "may", "significant", or "baseline" without a numeric or observable definition | QA cannot verify the case | Return to `prd-07-data-acceptance` before final compression |
| Admin config exists only because it is convenient, not necessary | Operations scope is expanding | Return to `prd-06-admin-config` and move it to hardcoded or later |
| Risk review requires loop-back or user decision | The final PRD cannot be delivered | Loop back to the owning artifact, resolve the issue, and re-run risk review |

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
9. `prd-09-prd-compressor` — compress all stage artifacts after gates are resolved.

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
  08-delivery-prd.md
```

If the user has not provided a feature name, generate a short kebab-case name from the idea.

## Definition of done

The workflow is complete when:

- The final PRD clearly states what this version does and does not do.
- Core rules are expressed as conditions, states, thresholds, and outcomes.
- Major exceptions are covered.
- Unknowns are either resolved, converted into explicit recommended defaults, or limited to sign-off notes that do not block execution.
- A developer can estimate the work without guessing product intent.
- A tester can write cases from the acceptance section.
- The product manager can see what they must sign off on.

If these conditions are not met, the normal workflow is not complete. Loop back, supplement the missing information, and continue. Ask the user only when the missing choice cannot be responsibly made by the agent.
