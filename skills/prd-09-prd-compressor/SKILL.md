---
name: prd-09-prd-compressor
description: Compress all PRD stage artifacts into a concise final review document for engineering, design, QA, and operations. It may be review-ready, decision-review, or not-ready depending on unresolved gates. Use at the end of the PRD workflow or when an AI-generated PRD is too long, vague, or mixed. Do not use to invent new requirements.
---

# PRD Compressor

## Purpose

Turn stage artifacts into a final PRD document that is short enough to review and honest about whether it is precise enough to execute.

This skill must compress, not expand.

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
4. Preserve unknowns; do not fake certainty.
5. Move non-blocking details to appendix or later version.
6. Convert vague wording into explicit product language.
7. If a section is not actionable by engineering, design, QA, operations, or PM, delete or rewrite it.
8. Do not convert unresolved `Decision needed`, `Rule gap`, or `Needs history check` items into final decisions.
9. If blocking decisions remain, mark the PRD as not review-ready and list the exact owner or confirmation needed.

## Readiness gate

Set one explicit status before writing the final document:

| Status | Use when | Required behavior |
|---|---|---|
| `Review-ready` | No blocking product, data, technical, legal, cost, rule, or acceptance gaps remain | Compress into an execution-ready PRD |
| `Decision-review` | The document is useful for stakeholder review, but at least one decision blocks estimation or QA | Lead with the blocking decisions and do not imply development can start |
| `Needs technical confirmation` | Product direction is stable, but architecture, data, logging, cost, compatibility, or integration facts are unconfirmed | Lead with confirmation questions and owners |
| `Not ready` | Scope, rules, success criteria, or responsibility boundaries are unstable | Do not compress into an execution PRD; summarize what must be resolved first |

The filename may remain `08-review-ready-prd.md` for compatibility, but the document title and conclusion must use the actual status. Never let the filename override the readiness status.

## Dialectical compression

For every major recommendation, preserve the strongest credible alternative when the source artifacts contain unresolved choices. Do not collapse options into one preferred path unless a stage artifact records the decision.

Before finalizing, run this challenge pass:

1. Which recommendation could be wrong?
2. Which team would be forced to decide later if this stays vague?
3. Which metric or acceptance case is not directly observable?
4. Which admin or operations item exists only because it is convenient?
5. Which earlier artifact must be updated if this gap changes behavior?

If any answer exposes a blocking gap, mark it in `## 10. Risks and decisions` and set the readiness status accordingly.

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
| Readiness status | Review-ready / Decision-review / Needs technical confirmation / Not ready |
| Version goal |  |
| This version does |  |
| This version does not do |  |
| Biggest decision needed |  |
| Biggest risk |  |
| Can engineering estimate? | Yes / No, blocked by ... |
| Can QA write executable cases? | Yes / No, blocked by ... |

## 1. Background and problem
{Short, concrete problem statement}

## 2. Goals and non-goals
### Goals
| Goal | Success meaning |
|---|---|

### Non-goals
| Non-goal | Reason |
|---|---|

## 3. Scope
| Scope item | Included? | Notes |
|---|---:|---|

## 4. Roles and permissions
| Role | View | Operate | Restrictions |
|---|---|---|---|

## 5. Core rules
| Rule ID | Trigger | Condition | Result | User-facing behavior |
|---|---|---|---|---|

## 6. Flow summary
### User flow
{Mermaid or concise numbered flow}

### System judgment flow
{Mermaid or concise numbered flow}

### Key exceptions
| Exception | Handling |
|---|---|

## 7. Page and interaction requirements
| Page / component | Required content | Actions | States |
|---|---|---|---|

## 8. Admin and operations requirements
| Requirement | Must-have? | Notes |
|---|---:|---|

## 9. Data and acceptance
### Metrics
| Metric | Definition | Why needed |
|---|---|---|

### Acceptance criteria
| Case | Precondition | Action | Expected result |
|---|---|---|---|

## 10. Risks and decisions
| Type | Item | Owner | Status |
|---|---|---|---|

## Appendix: deferred items
| Item | Reason deferred | Revisit trigger |
|---|---|---|
```

## Definition of done

The final PRD is done when:

- The readiness status is explicit and consistent with unresolved decisions.
- Engineering can estimate without guessing intent, or blockers are clearly labeled as blocking estimation.
- Design knows what information and states must be represented.
- QA can write test cases, or vague acceptance criteria are clearly labeled as blocking QA.
- Operations knows what it can and cannot control.
- PM can see every remaining sign-off item.
- The document no longer sounds like AI generated expansion.
