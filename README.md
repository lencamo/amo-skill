# amo-skill

English | [中文](./README.zh-CN.md)

Amo skills for engineering work: planning, implementation, verification, and writing, used as needed.

## Skills

| Skill | Responsibility |
| :--- | :--- |
| [`amo-workflow`](skills/amo-workflow/SKILL.md) | Coordinate complete feature delivery, stage evidence, approvals, and resumable progress |
| [`amo-feature`](skills/amo-feature/SKILL.md) | Design new features |
| [`amo-improve`](skills/amo-improve/SKILL.md) | Plan intentional changes to existing behavior |
| [`amo-fix`](skills/amo-fix/SKILL.md) | Diagnose bugs and plan fixes |
| [`amo-refactor`](skills/amo-refactor/SKILL.md) | Reshape structure, ownership, and module boundaries |
| [`amo-research`](skills/amo-research/SKILL.md) | Research external implementations and reusable approaches |
| [`amo-best`](skills/amo-best/SKILL.md) | Reassess existing proposals and tradeoffs |
| [`amo-detail`](skills/amo-detail/SKILL.md) | Explain how a discussed proposal will be implemented and how behavior will change |
| [`amo-preview`](skills/amo-preview/SKILL.md) | Preview UI changes with entry guidance and connected interactions across product types |
| [`amo-implement`](skills/amo-implement/SKILL.md) | Implement defined proposals and verify results, balancing code efficiency, concision, readability, and maintainability |
| [`amo-review`](skills/amo-review/SKILL.md) | Risk-proportionate static correctness and bug review |
| [`amo-check`](skills/amo-check/SKILL.md) | Verify review feedback, current need for action, and consequences if unchanged |
| [`amo-draft`](skills/amo-draft/SKILL.md) | Write focused documentation and copy |
| [`amo-deliver`](skills/amo-deliver/SKILL.md) | Close out finished work: local experience, automated Orca/Claude Code final reviews, feedback rounds, and converged delivery |

## Workflow

Use `amo-workflow` for complete or staged feature delivery and continuation. It coordinates the applicable skills with plan approval, an optional UI checkpoint, and final user acceptance. It enters amo-deliver at final acceptance without a separate user invocation. Individual skills remain available independently; ask to wrap up a finished feature to start amo-deliver directly. amo-review provides risk-proportionate review standards and performs standalone reviews. During delivery, amo-deliver records justified low-risk exemptions, reuses valid independent reviews, or starts one fresh Claude Code session through Orca to run the built-in local /code-review command with an explicitly selected effort and scope. Review is static by default; implementation owns necessary tests and builds. Repair rechecks cover changed behavior and affected contracts.

```text
amo-feature / amo-improve / amo-fix / amo-refactor (choose one)
→ amo-best (optional)
→ amo-detail (optional)
→ amo-implement
→ amo-review (functional review as needed)
→ amo-deliver (final acceptance and closeout)

amo-research: support design and proposal review as needed
amo-preview: guide users from familiar entrances to proposed UI changes and local interactions
amo-check: verify existing feedback and whether action is necessary now as needed
amo-draft: use at any stage as needed
```

During complete delivery, amo-deliver coordinates the independent review through the local Claude /code-review command; do not also execute amo-review as a second pass. A stage transition alone does not require another review.

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
