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
| `amo-best` | `🏆 [amo-best]` |
| `amo-research` | `🔬 [amo-research]` |
| `amo-detail` | `🔎 [amo-detail]` |
| `amo-implement` | `🔨 [amo-implement]` |
| `amo-review` | `🧹 [amo-review]` |

Keep the marker inline with the first line, not as a standalone paragraph.

## Primary Routing

| User intent | Use |
| :---------- | :-- |
| Build behavior that does not exist yet | `amo-feature` |
| Intentionally change, extend, improve, or redesign existing behavior | `amo-improve` |
| Explain and fix broken, wrong, flaky, regressed, or failing existing behavior | `amo-fix` |
| Change structure, ownership, coupling, state/data flow, module boundaries, or component boundaries | `amo-refactor` |
| Challenge an existing proposal: "is this best?", "better way?", "tradeoff right?", "scope right?" | `amo-best` |
| Research competitor products, community practices, or open-source implementations for mature, reusable approaches | `amo-research` |
| Understand an existing proposal's overall flow, impact, and frontend/backend changes | `amo-detail` |
| Implement an already defined proposal and verify the result | `amo-implement` |
| Review implemented code for redundancy, unnecessary abstractions, TypeScript type noise, or composable usage clarity | `amo-review` |

## Maintenance Rule

Do not duplicate each skill's full rules here. This file should answer only one question:

```text
For this user request, which amo workflow skill should be used first?
```
