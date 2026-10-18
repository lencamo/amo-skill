# amo-skill

[English](./README.md) | 中文

面向方案设计、实施、审查与文档编写的 amo 工作流 Skills 集合。

仓库地址：`https://github.com/lencamo/amo-skill`

## 工作流类 Skills

| Skill                                            | 目标                                      | 触发方式                                      |
| :----------------------------------------------- | :---------------------------------------- | :-------------------------------------------- |
| [`amo-feature`](skills/amo-feature/docs/SKILL.zh-CN.md)     | 新功能方案设计，并选择最佳标准            | “新增一个功能怎么做？”“这个需求怎么实现？”   |

工作流路由规则见 [`skills/RESOLVER.zh-CN.md`](skills/RESOLVER.zh-CN.md)。

每个 skill 都是一个独立目录，不只是单个 Markdown 文件。按需可以携带 `references/` 等辅助资源。

## 安装

本仓库遵循标准 `skills` 目录结构，可通过 `skills` CLI 安装到多个 agent。`-a <agent>` 的常见取值包括 `codex`、`claude-code`、`cursor`、`opencode`、`gemini-cli`、`continue`、`windsurf`、`trae` 等；完整支持列表请以当前 `skills` CLI 文档或 `npx skills --help` 为准。

查看可安装列表：

```bash
npx skills add lencamo/amo-skill --list
```

为 Codex 安装全部 skills：

```bash
npx skills add lencamo/amo-skill -a codex -g -y
```

为 Claude Code 安装全部 skills：

```bash
npx skills add lencamo/amo-skill -a claude-code -g -y
```

按需为指定 agent 安装指定 skill：

```bash
npx skills add lencamo/amo-skill -a codex -g -y -s amo-feature
```

本地开发时使用当前仓库：

```bash
git clone git@github.com:lencamo/amo-skill.git
cd amo-skill
npx skills add . -a codex -g -y
```

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
- [Animated SVG Logo](https://antfu.me/posts/animated-svg-logo)
- [antislop-code](https://github.com/miqdadbadjuber/anti-slop/blob/main/skills/antislop-code/SKILL.md)
- [Claude 提示词最佳实践：过度积极与过度设计](https://platform.claude.com/docs/en/build-with-claude/prompt-engineering/claude-prompting-best-practices#overeagerness)
