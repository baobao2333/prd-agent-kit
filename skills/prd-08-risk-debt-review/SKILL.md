---
name: prd-08-risk-debt-review
description: Review a PRD draft for historical debt, compatibility issues, abuse risk, cost risk, operational risk, legal/finance/risk-control boundaries, and responsibility gaps. Use before final PRD compression or before engineering review. Do not use for rewriting the whole PRD.
---

# PRD Risk & Debt Review

## Purpose

Expose the risks that AI-written PRDs usually hide: historical debt, unclear ownership, old behavior, compatibility, abuse, cost, operations burden, and responsibility transfer.

## Inputs

- All previous PRD artifacts.
- Known system history, if available.
- Known legal, finance, risk-control, or operations constraints, if available.

## Review principles

1. Do not assume old systems are clean.
2. Do not assume existing data can support new logic.
3. Do not assume old clients behave correctly.
4. Do not move product decisions to engineering by using vague wording.
5. Do not hide business risk behind “optimize later”.
6. Every high-risk item must have an owner or an explicit decision gap.
7. Run a confidence loop before finalizing the review: ask whether the strategy is factually strong enough to defend. If not, find all known loopholes, suggest proper fixes, and repeat until no factual loopholes remain. If 100% confidence cannot be justified from the available facts, mark the PRD as `Not ready` or `Needs product decision` instead of pretending certainty.

## Process

1. Review scope creep.
2. Review undefined rules.
3. Review compatibility and historical data.
4. Review abuse and cost risk.
5. Review operations burden.
6. Review responsibility boundaries.
7. Review legal / finance / risk-control dependency if relevant.
8. Run the confidence loop: list loopholes, propose fixes, re-check the revised strategy, and preserve any remaining uncertainty.
9. Recommend delete, simplify, confirm, keep, or loop back to an earlier stage.

## Loop-back rules

- If the risk depends on product scope or version boundary, return to `prd-02-business-boundary`.
- If the risk depends on missing conditions, thresholds, states, permissions, or conflict handling, return to `prd-03-rule-modeler`.
- If the risk depends on unclear user/system behavior, return to `prd-04-flow-modeler`.
- If the risk depends on missing user-visible states or copy, return to `prd-05-page-interaction`.
- If the risk is caused by speculative controls or missing operations ownership, return to `prd-06-admin-config`.
- If the risk depends on vague metrics, alert triggers, logging, attribution, or QA evidence, return to `prd-07-data-acceptance`.
- Use `prd-09-prd-compressor` only when unresolved items are either non-blocking or are explicitly being packaged as a `Decision-review`, `Needs technical confirmation`, or `Not ready` artifact.

## Output format

```markdown
# 07 Risk & Debt Review: {Feature Name}

## 1. Review conclusion
| Status | Meaning |
|---|---|
| Ready with minor fixes / Needs product decision / Needs technical confirmation / Not ready |

## 2. Scope creep check
| Item | Problem | Recommendation |
|---|---|---|

## 3. Rule gaps
| Gap | Why it blocks execution | Owner |
|---|---|---|

## 4. Historical debt / compatibility risks
| Area | Risk | Impact | Who confirms | Recommended handling |
|---|---|---|---|---|

## 5. Abuse, cost, and operations risks
| Risk | Abuse / cost path | Impact | Mitigation | Must-have this version? |
|---|---|---|---|---|

## 6. Responsibility boundary risks
| Wording or decision | Why risky | Rewrite or decision needed |
|---|---|---|

## 7. Required decisions before review
| Decision | Options | Recommended default | Sign-off owner |
|---|---|---|---|

## 8. Handoff to next stage
| Condition | Recommended next skill | Reason |
|---|---|---|
| Ready with minor fixes | `prd-09-prd-compressor` | Compress into a review-ready PRD |
| Needs product decision | `prd-02-business-boundary` or `prd-09-prd-compressor` as `Decision-review` | Decide scope, goal, owner, or package decisions for review |
| Needs technical confirmation | Relevant earlier skill or `prd-09-prd-compressor` as `Needs technical confirmation` | Confirm architecture, data, logging, cost, or compatibility before estimation |
| Not ready | Relevant earlier skill | Do not compress into an execution PRD |
```

## Definition of done

The review is complete when the product manager can see what they would be signing and where they could get blamed later.
