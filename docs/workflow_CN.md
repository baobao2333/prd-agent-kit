# 工作流说明

这套 PRD 工作流把“写 PRD”拆成多个阶段，让每个阶段都有清楚的职责，也方便单独评审和修改。

## 阶段列表

| 阶段 | Skill | 输出 |
|---|---|---|
| 00 | `prd-00-pipeline-orchestrator` | 协调整个流程 |
| 01 | `prd-01-idea-intake` | `00-intake.md` |
| 02 | `prd-02-business-boundary` | `01-boundary.md` |
| 03 | `prd-03-rule-modeler` | `02-rules.md` |
| 04 | `prd-04-flow-modeler` | `03-flows.md` |
| 05 | `prd-05-page-interaction` | `04-pages.md` |
| 06 | `prd-06-admin-config` | `05-admin-config.md` |
| 07 | `prd-07-data-acceptance` | `06-data-acceptance.md` |
| 08 | `prd-08-risk-debt-review` | `07-risk-review.md` |
| 09 | `prd-09-prd-compressor` | `08-review-ready-prd.md` |
| HTML | `prd-html-review-artifact` | `design-language.md`、`09-review.html` |

## 阶段门禁

如果还存在会影响方案成立的关键决策，流程应该暂停，不要假装已经评审完成。

非阻塞的不确定性可以标记为：`Fact`、`Assumption`、`Decision needed`、`Risk`、`Out of scope`、`Needs history check`、`Rule gap`。

如果流程、页面或验收阶段发现规则缺口，应该回到规则建模阶段补 `02-rules.md`，再继续往后走。

## 源文件和评审稿

Markdown 阶段文件是源文件。HTML 文件是给人阅读、分享和评审用的展示层。
