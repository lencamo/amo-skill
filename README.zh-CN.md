# amo-skill

[English](./README.md) | 中文

面向工程实践的 amo 技能集，按需支持方案推敲、实施验证与内容表达。

## Skills

| Skill | 职责 |
| :--- | :--- |
| [`amo-workflow`](skills/amo-workflow/docs/SKILL.zh-CN.md) | 协调轻量或分阶段交付、证据、确认节点与进度恢复 |
| [`amo-feature`](skills/amo-feature/docs/SKILL.zh-CN.md) | 新功能方案设计 |
| [`amo-improve`](skills/amo-improve/docs/SKILL.zh-CN.md) | 主动调整已有功能 |
| [`amo-fix`](skills/amo-fix/docs/SKILL.zh-CN.md) | 分析异常根因与修复方案 |
| [`amo-refactor`](skills/amo-refactor/docs/SKILL.zh-CN.md) | 调整结构、职责与模块边界 |
| [`amo-research`](skills/amo-research/docs/SKILL.zh-CN.md) | 调研外部实现与可复用方案 |
| [`amo-best`](skills/amo-best/docs/SKILL.zh-CN.md) | 复核已有方案与取舍 |
| [`amo-detail`](skills/amo-detail/docs/SKILL.zh-CN.md) | 展开已讨论方案的具体实施方式与实施后变化 |
| [`amo-preview`](skills/amo-preview/docs/SKILL.zh-CN.md) | 跨产品场景制作带入口引导和连贯交互的界面方案预览 |
| [`amo-implement`](skills/amo-implement/docs/SKILL.zh-CN.md) | 按明确方案实施并验证，兼顾代码效率、精炼度、可读性和可维护性 |
| [`amo-review`](skills/amo-review/docs/SKILL.zh-CN.md) | 按风险进行静态功能正确性与 Bug 审查 |
| [`amo-check`](skills/amo-check/docs/SKILL.zh-CN.md) | 核实审查意见、当前处理必要性及不处理的影响 |
| [`amo-draft`](skills/amo-draft/docs/SKILL.zh-CN.md) | 编写聚焦目标的文档与文案 |
| [`amo-deliver`](skills/amo-deliver/docs/SKILL.zh-CN.md) | 完成工作后的收尾：本地体验、Orca／Claude Code 自动终审、意见轮次与收敛交付 |

## 使用链路

功能交付或续做需要协调时，使用 `amo-workflow` 选择轻量或分阶段路径并安排适用技能。独立的小改、问答和审查可直接使用对应技能。

```text
你提出需求
    ↓
需求是否已经明确？
    ├─ 明确 → 直接实施
    │
    └─ 需要讨论 → 选择对应技能
                   ├─ 新功能：amo-feature
                   ├─ 调整已有功能：amo-improve
                   ├─ 修 Bug：amo-fix
                   └─ 重构：amo-refactor
                       ↓
                   形成具体方案
                       ↓
                   按需补充：
                   · 查外部做法：amo-research
                   · 判断方案好不好：amo-best
                   · 解释具体怎么做：amo-detail
                   · 看界面效果：静态图或 amo-preview
                       ↓
                   你确认方案
    ↓
amo-implement：修改代码、完成必要验证
    ↓
提供实际页面或运行结果，供你验收
    ↓
amo-deliver：按任务风险完成审查和收尾
    ↓
按你的授权 commit、push、合并或部署
```

这条主线由 Agent 按需选择技能，不要求用户逐个调用，也不是每个任务都必须走完所有步骤。“明确 → 直接实施”沿用已有执行授权；仅讨论方案不代表允许修改代码。简单任务合并阶段，不默认增加独立审查或全量测试；复杂任务按风险补齐必要验证。commit、push、合并、部署分别遵循授权和用户指定顺序，提前提交不代表用户已验收。仅要求 push 时复用有效验证，不重新启动整条链路。

`amo-review` 可独立执行功能审查；交付中的独立审查由 `amo-deliver` 安排。收到需要核实的反馈时按需使用 `amo-check`，修复后仅重查受影响部分。`amo-draft` 可在任意阶段按需编写文档和文案。

完整交付的独立审查由 amo-deliver 统一安排并使用本地 Claude /code-review，不额外执行第二轮 amo-review；阶段切换本身不要求再审一次。

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
