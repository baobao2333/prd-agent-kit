# 工作流说明

这套 PRD 工作流把“写 PRD”拆成多个阶段，让每个阶段都有清楚的职责，并在发现缺口时回到对应阶段修正，最终产出可交付 PRD。

每份交付级 PRD 都应该包含连续的功能行为描述。表格负责定义规则和证据，但读者应该先通过文字理解核心功能如何工作。

## 阶段列表

| 阶段 | Skill | 输出 |
|---|---|---|
| 00 | `prd-00-pipeline-orchestrator` | 协调整个流程 |
| 01 | `prd-01-idea-intake` | `00-intake.md` |
| 02 | `prd-02-business-boundary` | `01-boundary.md` |
| 03 | `prd-03-rule-modeler` | `02-rules.md`，包含功能规则叙述 |
| 04 | `prd-04-flow-modeler` | `03-flows.md` |
| 05 | `prd-05-page-interaction` | `04-pages.md` |
| 06 | `prd-06-admin-config` | `05-admin-config.md` |
| 07 | `prd-07-data-acceptance` | `06-data-acceptance.md` |
| 08 | `prd-08-risk-debt-review` | `07-risk-review.md` |
| 09 | `prd-09-prd-compressor` | `08-delivery-prd.md` |
| HTML | `prd-html-review-artifact` | `design-language.md`、`09-review.html` |

## 阶段门禁

如果还存在会影响方案成立的关键决策，流程不应该只记录问题后继续推进。agent 应该先回到对应阶段补齐，能做保守推荐就给出推荐默认值；只有无法替代业务方决策时才向用户提问。

非阻塞的不确定性可以标记为：`Fact`、`Assumption`、`Decision needed`、`Risk`、`Out of scope`、`Needs history check`、`Rule gap`。

如果流程、页面或验收阶段发现规则缺口，应该回到规则建模阶段补 `02-rules.md`，再继续往后走。

## 源文件和交付稿

Markdown 阶段文件是源文件。HTML 文件是给人阅读、分享和交付用的展示层。
