# 安装说明

## 前置条件

- 你已经在本机使用 Codex，并支持本地 skills。
- 你有一个准备用来生成 PRD 的工作区。

## 安装 Skills

把本仓库 `skills/` 下面的所有文件夹复制到你的 Codex skills 目录。

PowerShell 示例：

```powershell
$repo = "F:\prd-agent-kit"
$codexSkills = "$env:USERPROFILE\.codex\skills"
Copy-Item "$repo\skills\*" $codexSkills -Recurse -Force
```

Bash 示例：

```bash
repo="$HOME/prd-agent-kit"
codex_skills="$HOME/.codex/skills"
cp -R "$repo"/skills/* "$codex_skills"/
```

## 安装工作区 Agent

把根目录的 `AGENTS.md` 复制到你准备用来写 PRD 的工作区。

PowerShell 示例：

```powershell
Copy-Item "F:\prd-agent-kit\AGENTS.md" "F:\your-prd-workspace\AGENTS.md" -Force
```

之后在这个工作区里正常和 Codex 对话，就可以触发完整 PRD 工作流。

## 验证安装

在目标工作区里问 Codex：

```text
使用 PRD Generation Agent，把这个想法整理成 PRD：商家优惠券预算控制。
```

正常情况下会生成：

```text
docs/prd-workspace/{feature-name}/
```
