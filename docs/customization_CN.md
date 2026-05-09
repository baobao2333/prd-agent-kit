# 定制说明

## 修改单个阶段

如果只想改某个阶段的行为，直接编辑 `skills/` 下对应的 `SKILL.md`。

例子：

- 修改想法收集：`skills/prd-01-idea-intake/SKILL.md`
- 修改规则建模严格度：`skills/prd-03-rule-modeler/SKILL.md`
- 修改最终 PRD 结构：`skills/prd-09-prd-compressor/SKILL.md`
- 修改 HTML 交付稿风格：`skills/prd-html-review-artifact/SKILL.md`

## 修改整体工作流

如果想改全局规则，编辑根目录 `AGENTS.md`。

适合放在 `AGENTS.md` 里的内容包括：

- 默认语言；
- 输出目录；
- 阶段顺序；
- 阶段门禁；
- 最终回复格式。

## 修改建议

优先一次只改一个阶段。比如发现规则模型太虚，就收紧 `prd-03-rule-modeler`，不要马上往所有 skill 里加一堆全局限制。

这套工作流最重要的原则是：让不确定性显性化，然后通过回环补齐到可交付，而不是把问题藏在一篇看起来很完整的 PRD 里。
