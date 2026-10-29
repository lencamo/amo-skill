# AGENTS.md

English | [中文](./docs/AGENTS.zh-CN.md)

This file defines how skills in this repository should be maintained. It does not define the behavior of any specific skill.

## Repository Positioning

This is an agent skill collection repository, not a CLI or runtime project.

Goals:

- clear trigger conditions
- simple structure
- low maintenance cost
- real, non-speculative behavior

## Directory Conventions

```text
skills/<skill-name>/SKILL.md
skills/<skill-name>/docs/SKILL.zh-CN.md
skills/<skill-name>/references/
README.md
README.zh-CN.md
marketplace.json
AGENTS.md
docs/AGENTS.zh-CN.md
```

Rules:

1. Each skill lives in `skills/<skill-name>/`.
2. Directory names use `kebab-case`.
3. Each skill must include `SKILL.md`.
4. `docs/SKILL.zh-CN.md` is an optional faithful Chinese translation for human readers, not an executable skill file.
5. Add `references/` only when supporting material is actually needed.

## Skill Design

- A new skill should at minimum cover: when to use it, when not to use it, workflow, key rules, and output.
- Section names do not have to be identical, but these pieces of information should be easy to find.
- A skill should solve one clear problem and avoid becoming too broad.
- `description` should be trigger-oriented, not vague.
- Keep the main instructions short and move details into `references/` when appropriate.
- If execution depends on a reference file, `SKILL.md` should explicitly say to read it first.
- Do not duplicate the same rule in both `SKILL.md` and `references/`.
- Keep executable skill behavior in `SKILL.md`. Chinese docs under `docs/SKILL.zh-CN.md` are for readers and should faithfully translate the corresponding `SKILL.md` without becoming a second source of truth.

## Wording Rules

1. Rules are binding imperatives; a template block alone is not an instruction.
2. State a permission only when its absence changes behavior.
3. State each constraint once; never restate what another rule implies.
4. Omit what the context already implies.

## Output Skeleton

1. Output sections must declare their label block mandatory, not just show it.
2. The skeleton sentence is a cross-skill contract: change it in all skills at once.

## Skill Maintenance

1. Do not change skill behavior unless the task explicitly requires it.
2. Prefer structural cleanup over expanding content just to make it look more complete.
3. Do not rewrite existing skills only to force template consistency. Exception: shared contract wording (markers, skeleton sentence) stays uniform across skills.
4. Keep trigger conditions and output expectations stable.

## Versioning

1. Bump every change: patch for wording or fixes, minor for new rules or behavior.
2. Keep versions in sync across `SKILL.md`, `docs/SKILL.zh-CN.md`, and `marketplace.json`.

## Repository Sync

Update repository-level docs when any of the following happens:

- a skill is added
- a skill is removed
- a skill is renamed
- a skill's public positioning or description changes

Files to update:

- `README.md`
- `README.zh-CN.md`
- `marketplace.json`
- `docs/AGENTS.zh-CN.md` when `AGENTS.md` itself changes
