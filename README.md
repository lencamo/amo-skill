# amo-skill

English | [中文](./README.zh-CN.md)

Agent workflow skills for design, implementation, review, and documentation.

Repository: `https://github.com/lencamo/amo-skill`

## Workflow Skills

| Skill                                                    | Goal                                                       | Trigger                                                                      |
| :------------------------------------------------------- | :--------------------------------------------------------- | :--------------------------------------------------------------------------- |
| [`amo-feature`](skills/amo-feature/SKILL.md)             | Design a new feature and choose the right best-standard     | "How should we implement this new feature?"                                  |
| [`amo-improve`](skills/amo-improve/SKILL.md)             | Plan existing-feature changes with the right best-standard  | "How should we improve or change this existing behavior?"                    |
| [`amo-fix`](skills/amo-fix/SKILL.md)                     | Diagnose a bug and choose the right fix standard            | "Why is this bug happening, and what is the right fix?"                      |
| [`amo-refactor`](skills/amo-refactor/SKILL.md)           | Plan refactors and architecture boundaries by standard      | "Should this be refactored, and where should the boundary be?"              |
| [`amo-best`](skills/amo-best/SKILL.md)                   | Re-check the chosen best-standard and pressure-test a plan  | "Is this the best solution, or is there a better approach?"                 |

Workflow routing rules live in [`skills/RESOLVER.md`](skills/RESOLVER.md).

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

Install selected skills for a specific agent:

```bash
npx skills add lencamo/amo-skill -a codex -g -y -s amo-feature
npx skills add lencamo/amo-skill -a codex -g -y -s amo-improve
npx skills add lencamo/amo-skill -a codex -g -y -s amo-fix
npx skills add lencamo/amo-skill -a codex -g -y -s amo-refactor
npx skills add lencamo/amo-skill -a codex -g -y -s amo-best
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
