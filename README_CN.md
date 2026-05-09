# PRD Agent Kit

PRD Agent Kit 是一套给 Codex 使用的 PRD 生成技能链和 agent 工作流。它的目标不是一次性写出一篇很长、很虚的 PRD，而是把 PRD 拆成一组可检查、可追踪、可修改的阶段产物。

英文说明见：[README.md](README.md)

## 适合什么场景

当你需要把下面这些输入整理成可评审 PRD 时，可以使用这套工具：

- 粗糙的产品想法；
- 用户反馈；
- 运营需求；
- 策略方向；
- 一篇太散、太长、太模糊的 AI 生成 PRD。

它会依次处理问题定义、业务边界、规则模型、流程、页面交互、后台配置、数据验收、风险债务、最终压缩，并生成一份 HTML 评审稿。

如果只是改一句页面文案、补一个指标表、调整一个孤立规则，不需要跑完整流程，直接调用对应阶段的 skill 就好。

## 仓库结构

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

`AGENTS.md` 是工作区级别的 agent 指令。`skills/` 里是完整 PRD 技能链。

## 快速安装

1. 克隆这个仓库。
2. 把 `skills/` 下面的每个 skill 文件夹复制到你的 Codex skills 目录。
3. 把 `AGENTS.md` 复制到你准备用来写 PRD 的项目工作区。

具体命令见：[docs/install_CN.md](docs/install_CN.md)

## 基本用法

在包含 `AGENTS.md` 的工作区里，对 Codex 说：

```text
把这个想法整理成可评审 PRD：

我们需要一个商家优惠券预算控制功能。运营可以设置活动预算上限，避免超发，并在上线前看到风险。
```

默认会生成：

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
  design-language.md
  09-review.html
```

## 工作流

完整流程由 `prd-00-pipeline-orchestrator` 协调，然后按阶段调用 `prd-01` 到 `prd-09`。最后用 `prd-html-review-artifact` 把 Markdown 产物转成单文件 HTML 评审稿。

阶段说明见：[docs/workflow_CN.md](docs/workflow_CN.md)

## 如何修改

想改某个阶段的行为，就改对应的 `skills/*/SKILL.md`。想改整体默认规则，比如输出语言、产物目录、阶段门禁，就改根目录的 `AGENTS.md`。

定制说明见：[docs/customization_CN.md](docs/customization_CN.md)

## License

MIT License。见 [LICENSE](LICENSE)。
