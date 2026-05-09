---
name: prd-07-data-acceptance
description: Define success metrics, event tracking needs, and QA acceptance criteria for a PRD. Use after rules, flows, pages, and admin needs are drafted. Do not use to invent unrelated dashboards or vanity metrics.
---

# PRD Data & Acceptance

## Purpose

Make the PRD measurable and testable. This skill defines what “done” means for product, engineering, QA, and operations.

## Inputs

- Business boundary.
- Rule model.
- Flow model.
- Page spec.
- Admin config spec, if any.

## Process

1. Define success metrics tied to the business goal.
2. Define guardrail metrics tied to cost, abuse, failure, or operations burden.
3. Define event tracking only where decisions need data.
4. Define acceptance scenarios for happy path, branch paths, and exceptions.
5. Mark metrics that require data pipeline confirmation.

## Metrics rules

- Do not list metrics for decoration.
- Every metric must answer a product or operations question.
- If a metric does not affect a decision, remove it.
- Define denominator and time window where relevant.
- Separate product outcome metrics from system health and risk metrics.
- Do not use vague alert triggers such as "significant decline", "above baseline", or "business limit" unless the baseline, threshold, owner, and observation window are defined.
- If the threshold is unknown, mark it as `Decision needed` or `Needs data confirmation` and explain whether it blocks launch, QA, or only later optimization.

## Acceptance rules

- Write cases from user-visible behavior and product rules.
- Include edge cases from the rule and flow models.
- Each case must have precondition, action, and expected result.
- Do not write implementation-specific test steps unless the user provided implementation constraints.
- Expected results must be directly observable through UI state, product state, logs, events, or admin state.
- Avoid soft outcomes such as "may show", "possibly", "improves", "works normally", or "does not affect users" unless they are converted into observable criteria.
- If a valid outcome is probabilistic because ranking, recommendation, or experimentation is involved, split the case into observable checkpoints such as candidate generated, candidate admitted to ranking, constraint rejected, exposure logged, or fallback used.
- If QA cannot execute a case without a missing rule or threshold, mark the case as `Blocked` and send the gap back to the rule, boundary, or data stage instead of hiding it in acceptance.

## Challenge pass

Before handing off to risk review:

1. Pick the most important success metric and name a scenario where it could improve while the product still gets worse.
2. Pick the most important guardrail and define what evidence would force rollback.
3. Check whether every P0 acceptance case has an observable expected result.
4. Check whether every alert trigger has a threshold, comparison baseline, owner, and time window.
5. If any P0 case is blocked, update `02-rules.md`, `03-flows.md`, or this artifact before continuing. If the blocker cannot be resolved from existing evidence with high confidence, stop and ask the user instead of handing off.

## Output format

```markdown
# 06 Data & Acceptance: {Feature Name}

## 1. Product success metrics
| Metric | Definition | Why needed | Decision it supports |
|---|---|---|---|

## 2. Guardrail metrics
| Metric | Definition | Risk monitored | Alert / review trigger |
|---|---|---|---|

## 3. Event tracking
| Event | Trigger timing | Key parameters | Success / failure distinction | Notes |
|---|---|---|---|---|

## 4. Acceptance criteria
| Case ID | Scenario | Precondition | Action | Expected result | Observable by | Priority | Status |
|---|---|---|---|---|---|---|---|

## 5. Data confirmation needed
| Item | Why uncertain | Who confirms |
|---|---|---|

## 6. Handoff to next stage
Recommended next skill: `prd-08-risk-debt-review`
```

## Definition of done

This stage is complete when QA can write test cases and the product manager can explain how launch success will be judged.

If QA cannot execute P0 cases because thresholds, logs, events, or product outcomes are missing, the stage is not complete. Mark the blocker and loop back; if the missing information is a stakeholder decision, ask the user instead of advancing.
