# amo-skill

English | [中文](./README.zh-CN.md)

Amo skills for engineering work: planning, implementation, verification, and writing, used as needed.

## Skills

| Skill | Responsibility |
| :--- | :--- |
| [`amo-feature`](skills/amo-feature/SKILL.md) | Design new features |
| [`amo-improve`](skills/amo-improve/SKILL.md) | Plan intentional changes to existing behavior |
| [`amo-fix`](skills/amo-fix/SKILL.md) | Diagnose bugs and plan fixes |
| [`amo-refactor`](skills/amo-refactor/SKILL.md) | Reshape structure, ownership, and module boundaries |
| [`amo-research`](skills/amo-research/SKILL.md) | Research external implementations and reusable approaches |
| [`amo-best`](skills/amo-best/SKILL.md) | Reassess existing proposals and tradeoffs |
| [`amo-detail`](skills/amo-detail/SKILL.md) | Explain how a discussed proposal will be implemented and how behavior will change |
| [`amo-implement`](skills/amo-implement/SKILL.md) | Implement defined proposals and verify results |
| [`amo-review`](skills/amo-review/SKILL.md) | Functional correctness and bug review |
| [`amo-check`](skills/amo-check/SKILL.md) | Review code style, redundancy, abstractions, and type clarity |
| [`amo-draft`](skills/amo-draft/SKILL.md) | Write focused documentation and copy |

## Workflow

```text
amo-feature / amo-improve / amo-fix / amo-refactor (choose one)
→ amo-best (optional)
→ amo-detail (optional)
→ amo-implement
→ amo-review (functional review)

amo-research: support design and proposal review as needed
amo-check: review code style as needed
amo-draft: use at any stage as needed
```

See [RESOLVER](skills/RESOLVER.md) for routing rules.

## License

[MIT](./LICENSE)

## References

- [vercel-labs/agent-skills](https://github.com/vercel-labs/agent-skills)
- [tw93/Waza](https://github.com/tw93/Waza)
- [antislop-code](https://github.com/miqdadbadjuber/anti-slop/blob/main/skills/antislop-code/SKILL.md)
- [Claude Prompting Best Practices: Overeagerness](https://platform.claude.com/docs/en/build-with-claude/prompt-engineering/claude-prompting-best-practices#overeagerness)
- [Ponytail Review](https://github.com/DietrichGebert/ponytail/blob/main/skills/ponytail-review/SKILL.md)
- [Open Code Review Delegate](https://github.com/alibaba/open-code-review/blob/main/skills/open-code-review-delegate/SKILL.md)
