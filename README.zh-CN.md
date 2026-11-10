# amo-skill

[English](./README.md) | 中文

面向工程实践的 amo 技能集，按需支持方案推敲、实施验证与内容表达。

## Skills

| Skill | 职责 |
| :--- | :--- |
| [`amo-workflow`](skills/amo-workflow/docs/SKILL.zh-CN.md) | 协调完整功能交付、阶段证据、确认节点与进度恢复 |
| [`amo-feature`](skills/amo-feature/docs/SKILL.zh-CN.md) | 新功能方案设计 |
| [`amo-improve`](skills/amo-improve/docs/SKILL.zh-CN.md) | 主动调整已有功能 |
| [`amo-fix`](skills/amo-fix/docs/SKILL.zh-CN.md) | 分析异常根因与修复方案 |
| [`amo-refactor`](skills/amo-refactor/docs/SKILL.zh-CN.md) | 调整结构、职责与模块边界 |
| [`amo-research`](skills/amo-research/docs/SKILL.zh-CN.md) | 调研外部实现与可复用方案 |
| [`amo-best`](skills/amo-best/docs/SKILL.zh-CN.md) | 复核已有方案与取舍 |
| [`amo-detail`](skills/amo-detail/docs/SKILL.zh-CN.md) | 展开已讨论方案的具体实施方式与实施后变化 |
| [`amo-preview`](skills/amo-preview/docs/SKILL.zh-CN.md) | 跨产品场景制作带入口引导和连贯交互的界面方案预览 |
| [`amo-implement`](skills/amo-implement/docs/SKILL.zh-CN.md) | 按明确方案实施并验证，兼顾代码效率、精炼度、可读性和可维护性 |
| [`amo-review`](skills/amo-review/docs/SKILL.zh-CN.md) | 功能正确性与潜在 Bug 审查 |
| [`amo-check`](skills/amo-check/docs/SKILL.zh-CN.md) | 核实审查意见、当前处理必要性及不处理的影响 |
| [`amo-draft`](skills/amo-draft/docs/SKILL.zh-CN.md) | 编写聚焦目标的文档与文案 |
| [`amo-deliver`](skills/amo-deliver/docs/SKILL.zh-CN.md) | 完成工作后的收尾：本地体验、Orca／Claude Code 自动终审、意见轮次与收敛交付 |

## 使用链路

完整或分阶段功能交付及续做使用 `amo-workflow`，由它协调适用 skill，保留方案确认、可选的页面确认和最终用户验收。最终验收时接入 amo-deliver，无需用户再次调用。各 skill 仍可独立使用；直接说“功能做好了，帮我收尾”即可启动 amo-deliver。amo-deliver 通过 Orca orchestration 启动两个全新 Claude Code 会话，使用 open-code-review-delegate 审查并自动收回两份报告。

```text
amo-feature / amo-improve / amo-fix / amo-refactor（选一个）
→ amo-best（按需）
→ amo-detail（按需）
→ amo-implement
→ amo-review（功能审查）
→ amo-deliver（最终验收与交付收尾）

amo-research：按需辅助方案设计与复核
amo-preview：实施前引导用户找到改动、查看效果及体验操作
amo-check：按需核实已有意见并判断当前是否需要处理
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
