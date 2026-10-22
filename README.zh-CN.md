# amo-skill

[English](./README.md) | 中文

面向工程实践的 amo 技能集，按需支持方案推敲、实施验证与内容表达。

## Skills

| Skill | 职责 |
| :--- | :--- |
| [`amo-feature`](skills/amo-feature/docs/SKILL.zh-CN.md) | 新功能方案设计 |
| [`amo-improve`](skills/amo-improve/docs/SKILL.zh-CN.md) | 主动调整已有功能 |
| [`amo-fix`](skills/amo-fix/docs/SKILL.zh-CN.md) | 分析异常根因与修复方案 |
| [`amo-refactor`](skills/amo-refactor/docs/SKILL.zh-CN.md) | 调整结构、职责与模块边界 |
| [`amo-research`](skills/amo-research/docs/SKILL.zh-CN.md) | 调研外部实现与可复用方案 |
| [`amo-best`](skills/amo-best/docs/SKILL.zh-CN.md) | 复核已有方案与取舍 |
| [`amo-detail`](skills/amo-detail/docs/SKILL.zh-CN.md) | 展开已讨论方案的具体实施方式与实施后变化 |
| [`amo-implement`](skills/amo-implement/docs/SKILL.zh-CN.md) | 按明确方案实施并验证，兼顾代码效率、精炼度、可读性和可维护性 |
| [`amo-review`](skills/amo-review/docs/SKILL.zh-CN.md) | 功能正确性与潜在 Bug 审查 |
| [`amo-check`](skills/amo-check/docs/SKILL.zh-CN.md) | 审查代码风格、冗余、抽象与类型表达 |
| [`amo-draft`](skills/amo-draft/docs/SKILL.zh-CN.md) | 编写聚焦目标的文档与文案 |

## 使用链路

```text
amo-feature / amo-improve / amo-fix / amo-refactor（选一个）
→ amo-best（按需）
→ amo-detail（按需）
→ amo-implement
→ amo-review（功能审查）

amo-research：按需辅助方案设计与复核
amo-check：按需审查代码风格
amo-draft：任意阶段按需使用
```

路由规则见 [RESOLVER](skills/RESOLVER.zh-CN.md)。

## 许可证

[MIT](./LICENSE)

## 参考

- [vercel-labs/agent-skills](https://github.com/vercel-labs/agent-skills)
- [tw93/Waza](https://github.com/tw93/Waza)
- [antislop-code](https://github.com/miqdadbadjuber/anti-slop/blob/main/skills/antislop-code/SKILL.md)
- [Claude 提示词最佳实践：过度积极与过度设计](https://platform.claude.com/docs/en/build-with-claude/prompt-engineering/claude-prompting-best-practices#overeagerness)
- [Ponytail Review](https://github.com/DietrichGebert/ponytail/blob/main/skills/ponytail-review/SKILL.md)
- [Open Code Review Delegate](https://github.com/alibaba/open-code-review/blob/main/skills/open-code-review-delegate/SKILL.md)
