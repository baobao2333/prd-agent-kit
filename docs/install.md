# Installation

## Prerequisites

- Codex with local skills support.
- A workspace where you want to generate PRDs.
- The companion `visual-taste-lab` skill installed in Codex. The PRD kit uses it to generate adaptive `design-language.md` files for HTML handoff artifacts.

## Install Skills

Copy all folders under this repository's `skills/` directory into your Codex skills directory.

PowerShell example:

```powershell
$repo = "F:\prd-agent-kit"
$codexSkills = "$env:USERPROFILE\.codex\skills"
Copy-Item "$repo\skills\*" $codexSkills -Recurse -Force
```

Bash example:

```bash
repo="$HOME/prd-agent-kit"
codex_skills="$HOME/.codex/skills"
cp -R "$repo"/skills/* "$codex_skills"/
```

## Install Companion Skill

Install `visual-taste-lab` in the same Codex skills directory before running the full workflow. If you keep that skill as a local folder, copy it like this:

```powershell
$codexSkills = "$env:USERPROFILE\.codex\skills"
Copy-Item "PATH\TO\visual-taste-lab" "$codexSkills\visual-taste-lab" -Recurse -Force
```

The PRD workflow uses this companion skill only for the HTML handoff design-language pass.

## Install The Workspace Agent

Copy `AGENTS.md` into the workspace where PRD work should happen.

PowerShell example:

```powershell
Copy-Item "F:\prd-agent-kit\AGENTS.md" "F:\your-prd-workspace\AGENTS.md" -Force
```

The workspace should then be able to run the full PRD workflow through normal Codex prompts.

## Verify Installation

Ask Codex in the target workspace:

```text
Use the PRD Generation Agent to turn this idea into a PRD: merchant coupon budget control.
```

The expected output folder is:

```text
docs/prd-workspace/{feature-name}/
```
