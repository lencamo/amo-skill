# amo-skill

English | [中文](./README.zh-CN.md)

Amo skills for engineering work: planning, implementation, verification, and writing, used as needed.

## Skills

| Skill | Responsibility |
| :--- | :--- |
| [`amo-workflow`](skills/amo-workflow/SKILL.md) | Coordinate lightweight or staged delivery, evidence, approvals, and resumable progress |
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
| [`amo-deliver`](skills/amo-deliver/SKILL.md) | Close out finished work: experience, risk-based independent review, focused repair rechecks, and delivery |

## Workflow

When feature delivery or continuation needs coordination, use `amo-workflow` to choose a lightweight or staged path and coordinate the applicable skills. Standalone edits, questions, and reviews can use the relevant skill directly.

```text
You describe the requirement
    ↓
Is the requirement already clear?
    ├─ Yes → Implement directly
    │
    └─ Needs discussion → Choose the relevant skill
                          ├─ New feature: amo-feature
                          ├─ Change existing behavior: amo-improve
                          ├─ Fix a bug: amo-fix
                          └─ Refactor: amo-refactor
                              ↓
                          Form a concrete proposal
                              ↓
                          Add support as needed:
                          · Research external approaches: amo-research
                          · Reassess the proposal: amo-best
                          · Explain implementation details: amo-detail
                          · Preview the UI: static image or amo-preview
                              ↓
                          You approve the proposal
    ↓
amo-implement: change the code and perform necessary verification
    ↓
Provide the running page or results for your acceptance
    ↓
amo-deliver: arrange review and closeout proportionate to risk
    ↓
Commit, push, merge, or deploy within your authorization
```

The agent selects skills as needed; users do not need to invoke each one, and not every task traverses every step. “Clear → Implement directly” reuses existing execution authorization; discussing a proposal alone does not authorize code changes. Standalone implementation also hands off to `amo-deliver` when the same task reaches its first delivery closeout. Simple tasks combine stages without defaulting to independent review or a full test suite; complex tasks receive the verification their risks require. Commit, push, merge, and deployment follow their respective authorization and the user's specified order; an earlier commit does not count as user acceptance. A push-only request reuses valid verification without restarting the entire flow.

For UI acceptance, the agent hands over the actual page link and entry path, what to inspect, a current screenshot when available, and the actual browser/service state. Prototype or sample data and access limitations remain explicit; tasks without UI changes omit this handoff.

`amo-review` can perform standalone functional review; `amo-deliver` coordinates independent review during delivery. Use `amo-check` for feedback that needs verification, then recheck only the scope affected by repairs. Use `amo-draft` for documentation and copy at any stage as needed.

During delivery, `amo-deliver` reuses valid review coverage and selects the remaining review by risk:

| Change | Path |
| :--- | :--- |
| Pure presentation | Implement → applicable self-check/page verification → deliver; independent review only when requested or required. |
| Bounded logic repair | Inspect direct callers → implement and focused tests → one direct independent review → repair and targeted recheck as needed → deliver. |
| Complex or high-risk change | Resolve necessary decisions → staged implementation/verification → in-depth independent review → focused repair/recheck → deliver. |

A bounded storage/API repair can use a lightweight process while retaining critical failure-path checks. Direct review uses one independent session applying `amo-review`; the local Claude `/code-review` is an optional executor, not an extra mandatory pass. Honor explicit tool/reviewer requirements. The coordinator evaluates feedback using `amo-check`, retains settled decisions, and reuses valid evidence. A clear bounded repair may close with focused regression evidence and implementer verification; new critical or complex risks need independent recheck. Do not re-review each commit or rewrite reports at stage transitions. Report changes and actual self-test results briefly, with material gaps and authorized Git status.

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
