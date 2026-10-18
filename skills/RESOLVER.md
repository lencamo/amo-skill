# Amo Workflow Resolver

English | [中文](./RESOLVER.zh-CN.md)

This file exists only for `amo-*` workflow routing.

README is the public catalogue: it lists all skills, install commands, and short descriptions.
This resolver is the maintenance guide for cases where several `amo-*` skills could match the same request.

Runtime trigger source remains each `skills/amo-*/SKILL.md` frontmatter `description`. Keep this file short and update it only when an `amo-*` trigger boundary changes.

## Shared Output Marker

All `amo-*` workflow skills prefix the first output line inline with their skill marker:

| Skill | Marker |
| :---- | :----- |
| `amo-feature` | `🧩 [amo-feature]` |
| `amo-improve` | `🧰 [amo-improve]` |
| `amo-fix` | `🛠️ [amo-fix]` |
| `amo-refactor` | `🧱 [amo-refactor]` |

Keep the marker inline with the first line, not as a standalone paragraph.

## Primary Routing

| User intent | Use |
| :---------- | :-- |
| Build behavior that does not exist yet | `amo-feature` |
| Intentionally change, extend, improve, or redesign existing behavior | `amo-improve` |
| Explain and fix broken, wrong, flaky, regressed, or failing existing behavior | `amo-fix` |
| Change structure, ownership, coupling, state/data flow, module boundaries, or component boundaries | `amo-refactor` |

## Maintenance Rule

Do not duplicate each skill's full rules here. This file should answer only one question:

```text
For this user request, which amo workflow skill should be used first?
```
