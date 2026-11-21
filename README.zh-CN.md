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
| [`amo-deliver`](skills/amo-deliver/docs/SKILL.zh-CN.md) | 完成工作后的收尾：体验、按风险独立审查、修复定向复核与交付 |

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

这条主线由 Agent 按需选择技能，不要求用户逐个调用，也不是每个任务都必须走完所有步骤。“明确 → 直接实施”沿用已有执行授权；仅讨论方案不代表允许修改代码。独立实施任务进入首次交付收尾时，同样交接给 `amo-deliver`。简单任务合并阶段，不默认增加独立审查或全量测试；复杂任务按风险补齐必要验证。commit、push、合并、部署分别遵循授权和用户指定顺序，提前提交不代表用户已验收。仅要求 push 时复用有效验证，不重新启动整条链路。

界面验收时，Agent 会交接实际页面链接和入口路径、重点查看内容、可用时的当前截图，以及实际浏览器／服务状态。方案预览、样例数据及访问限制明确说明；没有界面变化的任务省略这份交接。

`amo-review` 可独立执行功能审查；交付中的独立审查由 `amo-deliver` 安排。收到需要核实的反馈时按需使用 `amo-check`，修复后仅重查受影响部分。`amo-draft` 可在任意阶段按需编写文档和文案。

交付中由 `amo-deliver` 复用有效审查覆盖，并按风险选择仍需完成的审查：

| 改动 | 路径 |
| :--- | :--- |
| 纯展示 | 实施 → 适用自检／页面验证 → 交付；只有明确要求时才独立审查。 |
| 局部逻辑修复 | 检查直接调用方 → 实施与针对性测试 → 一次直接独立审查 → 按需修复与定向复核 → 交付。 |
| 复杂或高风险改动 | 明确必要决策 → 分阶段实施／验证 → 深入独立审查 → 定向修复／复核 → 交付。 |

局部存储／API 修复可以采用轻量流程，同时保留关键失败路径检查。直接审查由一个独立会话应用 `amo-review`，本地 Claude `/code-review` 是可选执行方式，不是额外必经轮次。遵守明确指定的工具／审查者。协调会话用 `amo-check` 判断反馈，继承已有裁定并复用有效证据。边界清楚的局部修复可用针对性回归证据和实施者验证收尾；新的关键或复杂风险需要独立复核。不逐 commit 重审，也不在阶段切换时重写报告。简短提供修改说明、实际自测结果、实质缺口与已授权 Git 状态。

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
