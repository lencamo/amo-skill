# amo-skill

[English](./README.md) | 中文

面向方案设计、实施、审查与文档编写的 amo 工作流 Skills 集合。

仓库地址：`https://github.com/lencamo/amo-skill`

## Skills

| Skill                                            | 目标                                      | 触发方式                                      |
| :----------------------------------------------- | :---------------------------------------- | :-------------------------------------------- |
| [`amo-feature`](skills/amo-feature/docs/SKILL.zh-CN.md)     | 新功能方案设计，并选择最佳标准            | “新增一个功能怎么做？”“这个需求怎么实现？”   |
| [`amo-improve`](skills/amo-improve/docs/SKILL.zh-CN.md)     | 已有功能改造，并选择最佳标准              | “现有功能要改成这样，怎么改最好？”           |
| [`amo-fix`](skills/amo-fix/docs/SKILL.zh-CN.md)             | Bug 根因分析，并选择修复标准              | “这个 bug 为什么出现？”“怎么修才对？”        |
| [`amo-refactor`](skills/amo-refactor/docs/SKILL.zh-CN.md)   | 按标准规划重构、模块边界、职责归属        | “这块是不是该重构？”“边界怎么拆？”           |
| [`amo-best`](skills/amo-best/docs/SKILL.zh-CN.md)           | 复核最佳标准，并对已有方案做压力测试      | “这是最佳方案吗？”“有没有更优方案？”         |
| [`amo-research`](skills/amo-research/docs/SKILL.zh-CN.md)   | 调研实现证据与可复用方案，辅助方案判断 | “竞品或开源项目是怎么实现这个功能的？”     |
| [`amo-detail`](skills/amo-detail/docs/SKILL.zh-CN.md)       | 呈现方案链路、影响范围和前后端变化        | “讲清楚这个方案的整体链路和前后端变化。”     |
| [`amo-implement`](skills/amo-implement/docs/SKILL.zh-CN.md) | 实施并验证方案，约束注释噪音、前端内容污染和范围蔓延 | “按这个方案实施并验证结果。”               |
| [`amo-review`](skills/amo-review/docs/SKILL.zh-CN.md)       | 审查已实现代码的风格、冗余和 TS 类型表达  | “帮我看看这段代码是否冗余、风格是否合理？”   |
| [`amo-draft`](skills/amo-draft/docs/SKILL.zh-CN.md)         | 编写目标聚焦的文档和文案，避免上下文污染  | “基于这些上下文写一份干净的页面文案/需求文档。” |

典型链路：

```text
amo-feature / amo-improve / amo-fix / amo-refactor
→ amo-best
→ amo-detail
→ amo-implement
→ amo-review
→ amo-draft
```

主方案类工作流 skill 会先选择最佳标准：目标态最佳、约束内最佳、演进式最佳或风险最低最佳。`amo-best` 只用于对已有方案做二次复核。`amo-review` 用于已实现代码的风格审查。`amo-draft` 用于目标聚焦的内容草稿。

`amo-research` 调研竞品、社区实践和开源实现，为 `amo-feature`、`amo-improve`、`amo-fix`、`amo-refactor` 和 `amo-best` 提供实现证据及复用建议。它可以独立使用，是可选步骤，不是设计的固定前置步骤。

`amo-detail` 呈现已有方案的整体链路、影响范围、前端变化、后端数据流向、存储及定时任务。方案可以由用户提供，也可以来自主方案类 skill，并按需经过 `amo-best` 复核。

`amo-implement` 实施并验证已明确的方案，保持注释有效、前端内容聚焦业务，并将改动控制在既定范围内。

`amo-*` 工作流的详细路由和歧义场景规则见 [`skills/RESOLVER.zh-CN.md`](skills/RESOLVER.zh-CN.md)。

每个 skill 都是一个独立目录，不只是单个 Markdown 文件。按需可以携带 `references/` 等辅助资源。

## 许可证

本仓库采用 MIT License。完整条款见 [LICENSE](./LICENSE)。

## 目录结构

```text
.
├── AGENTS.md
├── CLAUDE.md
├── LICENSE
├── marketplace.json
├── README.md
├── README.zh-CN.md
└── skills
    └── example-skill
        ├── SKILL.md
        ├── docs
        │   └── SKILL.zh-CN.md
        ├── agents
        ├── references
        ├── scripts
        └── templates
```

## 参考

- [vercel-labs/agent-skills](https://github.com/vercel-labs/agent-skills)
- [tw93/Waza](https://github.com/tw93/Waza)
- [antislop-code](https://github.com/miqdadbadjuber/anti-slop/blob/main/skills/antislop-code/SKILL.md)
- [Claude 提示词最佳实践：过度积极与过度设计](https://platform.claude.com/docs/en/build-with-claude/prompt-engineering/claude-prompting-best-practices#overeagerness)
