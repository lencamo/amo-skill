# amo-skill

English | [中文](./README.zh-CN.md)

Agent workflow skills for design, implementation, review, and documentation.

Repository: `https://github.com/lencamo/amo-skill`

Each skill lives in its own folder instead of a single markdown file. A skill can include bundled references and helper resources when needed.

## Install

This repository follows the standard `skills` layout and can be installed with the `skills` CLI for multiple agents. Common `-a <agent>` values include `codex`, `claude-code`, `cursor`, `opencode`, `gemini-cli`, `continue`, `windsurf`, and `trae`; for the full and current list, check the `skills` CLI docs or run `npx skills --help`.

List available skills:

```bash
npx skills add lencamo/amo-skill --list
```

Install all skills for Codex:

```bash
npx skills add lencamo/amo-skill -a codex -g -y
```

Install all skills for Claude Code:

```bash
npx skills add lencamo/amo-skill -a claude-code -g -y
```

Use the local repository during development:

```bash
git clone git@github.com:lencamo/amo-skill.git
cd amo-skill
npx skills add . -a codex -g -y
```

## License

This repository is released under the MIT License. See [LICENSE](./LICENSE) for the full text.

## Structure

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
        ├── agents
        ├── references
        ├── scripts
        └── templates
```

## References

- [vercel-labs/agent-skills](https://github.com/vercel-labs/agent-skills)
- [tw93/Waza](https://github.com/tw93/Waza)
- [Animated SVG Logo](https://antfu.me/posts/animated-svg-logo)
- [antislop-code](https://github.com/miqdadbadjuber/anti-slop/blob/main/skills/antislop-code/SKILL.md)
- [Claude Prompting Best Practices: Overeagerness](https://platform.claude.com/docs/en/build-with-claude/prompt-engineering/claude-prompting-best-practices#overeagerness)
