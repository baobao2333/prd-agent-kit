# Customization

## Change One Stage

Edit the relevant `SKILL.md` file under `skills/`.

Examples:

- Change intake behavior: `skills/prd-01-idea-intake/SKILL.md`
- Change rule modeling strictness: `skills/prd-03-rule-modeler/SKILL.md`
- Change final PRD structure: `skills/prd-09-prd-compressor/SKILL.md`
- Change HTML handoff style: `skills/prd-html-review-artifact/SKILL.md`

## Change The Whole Workflow

Edit root `AGENTS.md` when you want to change:

- default language;
- output folder;
- stage order;
- stage gate rules;
- final response format.

## Keep The Workflow Stable

Prefer changing one stage at a time. If a stage starts inventing scope, tighten that stage's `SKILL.md` instead of adding broad global rules.

The most important principle is: stage files should make uncertainty visible, then resolve it through loops until the PRD is deliverable.
