---
name: prd-03-rule-modeler
description: "Convert product descriptions into executable product rules: objects, states, permissions, conditions, thresholds, time windows, conflict handling, and user-visible outcomes. Use when PRD logic needs to become precise. Do not use for broad strategy, UI layout, backend implementation, or final writing polish."
---

# PRD Rule Modeler

## Purpose

Turn natural-language feature descriptions into rule language that engineering and QA can execute.

This skill is the heart of PRD quality. It removes vague phrases and replaces them with objects, states, conditions, actions, and exceptions.

## Inputs

- Business boundary document.
- Any known product rules.
- Any numerical thresholds or eligibility criteria.
- Any known roles, permissions, or timing constraints.

## Process

1. Identify rule objects.
2. Define states for each object.
3. Define state transitions.
4. Define permissions by role.
5. Define triggering conditions.
6. Define success and failure outcomes.
7. Define time boundaries.
8. Define repeat, reversal, deletion, expiration, and concurrency handling.
9. Write a functional rule narrative that explains the rule set in continuous prose.
10. Mark unknowns instead of filling them with fake certainty, then resolve any unknown that blocks engineering or QA before handoff.

## Rule writing rules

- Replace “support” with exact operation and result.
- Replace “eligible user” with eligibility conditions.
- Replace “high value” with threshold and time window.
- Replace “system determines” with inputs and output states.
- Replace “backend configurable” with actual config item, default value, and failure handling.
- Replace “optimized later” with explicit non-goal or follow-up trigger.
- If a threshold is not provided, choose a conservative initial default when product context supports it and mark the rationale.
- If no responsible default can be chosen, ask the user before handing off instead of passing the gap downstream.
- Do not let the output be only tables. Add a short prose narrative that connects objects, triggers, inputs, decisions, outputs, user-visible behavior, feedback, failure, and rollback.

## Output format

```markdown
# 02 Rule Model: {Feature Name}

## 1. Rule objects
| Object | Definition | Key fields / attributes | Notes |
|---|---|---|---|

## 2. States
| Object | State | Definition | Entry condition | Exit condition |
|---|---|---|---|---|

## 3. Permissions
| Role | Can view | Can operate | Cannot operate | Notes |
|---|---|---|---|---|

## 4. Core rules
| Rule ID | Rule | Trigger | Conditions | Result | User-facing response | Unknowns |
|---|---|---|---|---|---|---|

## 5. Time rules
| Rule | Start | End | Timezone / cycle | Boundary behavior |
|---|---|---|---|---|

## 6. Conflict and exception rules
| Case | System behavior | User-facing behavior | Needs confirmation? |
|---|---|---|---|
| Repeated operation |  |  |  |
| Concurrent operation |  |  |  |
| Expired resource |  |  |  |
| Deleted resource |  |  |  |
| Permission revoked |  |  |  |
| Old client version |  |  |  |

## 7. Functional rule narrative
{Continuous prose explaining how the feature works end to end using the rules above. Include trigger, inputs, system judgment, output, user-visible behavior, feedback, failure, and rollback.}

## 8. Handoff to next stage
Recommended next skill: `prd-04-flow-modeler`
```

## Definition of done

A rule model is complete when a developer no longer has to infer product decisions from prose, and a reader can understand the feature behavior before reading the tables in detail.
