---
name: prd-09-prd-compressor
description: Compress resolved PRD stage artifacts into a concise delivery-grade PRD for engineering, design, QA, and operations. Use only after stage gates are resolved. Do not use to invent new requirements.
---

# PRD Compressor

## Purpose

Turn resolved stage artifacts into a final PRD document that is short enough to review and precise enough to execute.

This skill must compress, not expand.

## Invocation gate

Run this skill only when all of these are true:

1. Blocking product, data, technical, legal, cost, rule, and acceptance gates are resolved.
2. Remaining sign-off notes have recommended defaults and do not block engineering estimation or QA case writing.
3. The risk review does not require a loop-back to an earlier artifact.

If blockers remain, do not write `08-delivery-prd.md`. Return to the owning earlier skill, resolve the gap, and re-run affected later stages. Ask the user only when the missing decision cannot be responsibly made by the agent.

## Inputs

- Intake brief.
- Business boundary.
- Rule model.
- Flow model.
- Page interaction spec.
- Admin config spec.
- Data and acceptance spec.
- Risk and debt review.

## Compression rules

1. Preserve decisions; remove brainstorming.
2. Preserve rules; remove slogans.
3. Preserve boundaries; remove speculative future features.
4. Preserve non-blocking assumptions and sign-off notes; do not fake certainty.
5. Move non-blocking details to appendix or later version.
6. Convert vague wording into explicit product language.
7. If a section is not actionable by engineering, design, QA, operations, or PM, delete or rewrite it.
8. Do not convert unresolved `Decision needed`, `Rule gap`, or `Needs history check` items into final decisions. Resolve them before this skill runs, or keep only non-blocking sign-off notes with recommended defaults.
9. If a blocking decision remains, stop and loop back instead of compressing.
10. Always include a prose feature description before goals, scope, metrics, or risk tables. This section is the product behavior spine of the PRD; do not replace it with tables.

## Feature description rules

The final PRD must include a continuous natural-language description of the feature behavior. It should answer, in prose:

1. What the feature is and where it lives in the product.
2. Who or what triggers it.
3. What inputs the system reads.
4. What judgment, rule, or transformation the system performs.
5. What output is produced.
6. What the user sees or can do.
7. How feedback, failure, expiration, rollback, and edge cases behave.

Keep this section concrete and execution-oriented. It should be readable by product, design, engineering, QA, and operations without needing to decode the rule tables first.

## Dialectical compression

For every major recommendation, preserve the strongest credible alternative in rationale when useful, but the final PRD must have one executable default path.

Before finalizing, run this challenge pass:

1. Which recommendation could be wrong?
2. Which team would be forced to decide later if this stays vague?
3. Which metric or acceptance case is not directly observable?
4. Which admin or operations item exists only because it is convenient?
5. Which earlier artifact must be updated if this gap changes behavior?

If any answer exposes a blocking gap, stop instead of compressing. Return to the earlier artifact that owns the gap, or ask the user if the choice is truly business-owned.

## Forbidden phrases unless immediately defined

- “提升用户体验”
- “增强互动感”
- “后台灵活配置”
- “系统智能判断”
- “根据用户行为推荐”
- “后续优化”
- “异常情况按默认处理”
- “具体由研发实现”
- “运营手动处理即可”

## Output format

```markdown
# PRD: {Feature Name}

## 0. Review conclusion
| Item | Conclusion |
|---|---|
| Delivery status | Ready for handoff |
| Version goal |  |
| This version does |  |
| This version does not do |  |
| Recommended defaults requiring sign-off |  |
| Biggest risk |  |
| Engineering estimate readiness | Ready |
| QA case readiness | Ready |

## 1. Background and problem
{Short, concrete problem statement}

## 2. Feature description
{Continuous prose describing the core feature behavior: trigger, inputs, system judgment, output, user-visible behavior, feedback, failure, and rollback.}

## 3. Goals and non-goals
### Goals
| Goal | Success meaning |
|---|---|

### Non-goals
| Non-goal | Reason |
|---|---|

## 4. Scope
| Scope item | Included? | Notes |
|---|---:|---|

## 5. Roles and permissions
| Role | View | Operate | Restrictions |
|---|---|---|---|

## 6. Core rules
| Rule ID | Trigger | Condition | Result | User-facing behavior |
|---|---|---|---|---|

## 7. Flow summary
### User flow
{Mermaid or concise numbered flow}

### System judgment flow
{Mermaid or concise numbered flow}

### Key exceptions
| Exception | Handling |
|---|---|

## 8. Page and interaction requirements
| Page / component | Required content | Actions | States |
|---|---|---|---|

## 9. Admin and operations requirements
| Requirement | Must-have? | Notes |
|---|---:|---|

## 10. Data and acceptance
### Metrics
| Metric | Definition | Why needed |
|---|---|---|

### Acceptance criteria
| Case | Precondition | Action | Expected result |
|---|---|---|---|

## 11. Risks and decisions
| Type | Item | Owner | Recommendation / status |
|---|---|---|---|

## Appendix: deferred items
| Item | Reason deferred | Revisit trigger |
|---|---|---|
```

## Definition of done

The final PRD is done when:

- The delivery status is ready for handoff.
- Engineering can estimate without guessing intent.
- Design knows what information and states must be represented.
- QA can write test cases.
- Operations knows what it can and cannot control.
- PM can see every remaining sign-off item.
- The document no longer sounds like AI generated expansion.

If these conditions fail, this skill should not be the next step.
