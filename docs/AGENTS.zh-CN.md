> 中文翻译文档，仅供人阅读。真实 agent 执行规则以 ../AGENTS.md 为准。

# AGENTS.md

本文件定义本仓库中 skill 的维护方式，不定义任何具体 skill 的行为。

## 仓库定位

这是一个 agent skill 集合仓库，不是 CLI 或运行时项目。

目标：

- 触发条件清晰
- 结构简单
- 维护成本低
- 真实、非臆测的行为

## 目录约定

```text
skills/<skill-name>/SKILL.md
skills/<skill-name>/docs/SKILL.zh-CN.md
skills/<skill-name>/references/
README.md
README.zh-CN.md
marketplace.json
AGENTS.md
docs/AGENTS.zh-CN.md
```

规则：

1. 每个 skill 位于 `skills/<skill-name>/`。
2. 目录名使用 `kebab-case`。
3. 每个 skill 必须包含 `SKILL.md`。
4. `docs/SKILL.zh-CN.md` 是可选的忠实中文翻译，供人阅读，不是可执行的 skill 文件。
5. 仅在确实需要辅助材料时才添加 `references/`。

## Skill 设计

- 新 skill 至少覆盖：何时使用、何时不使用、工作流、核心规则、输出。
- 节名不必一致，但这些信息应易于找到。
- 一个 skill 解决一个明确问题，避免范围过大。
- `description` 应面向触发，不空泛。
- 主指令保持简短，细节按需移入 `references/`。
- 若执行依赖参考文件，`SKILL.md` 应显式说明先读它。
- 同一规则不在 `SKILL.md` 和 `references/` 中重复。
- 可执行的 skill 行为保存在 `SKILL.md`；`docs/SKILL.zh-CN.md` 下的中文文档供人阅读，应忠实翻译对应 `SKILL.md`，不成为第二正源。

## 措辞规范

1. 规则必须是强制性祈使指令；光一个模板代码块不构成指令。
2. 只有「不声明就会改变行为」的许可才写。
3. 每条约束只写一次；绝不重述另一条规则已隐含的内容。
4. 上下文已自明的省略。

## 输出骨架

1. Output 节必须声明标签块是强制的，不能只展示。
2. 骨架句式是跨 skill 契约：要改就所有 skill 一次改完。

## Skill 维护

1. 任务不明确要求时不改变 skill 行为。
2. 优先做结构清理，不为「看起来更完整」而扩充内容。
3. 不仅为追求模板一致而重写已有 skill。例外：共享契约措辞（输出标记、骨架句式）在全系列保持统一。
4. 保持触发条件和输出预期稳定。

## 版本号

1. 每次变更都 bump：措辞或修复提 patch 号，新规则或行为变化提 minor 号。
2. 三处版本保持同步：`SKILL.md`、`docs/SKILL.zh-CN.md`、`marketplace.json`。

## 仓库同步

发生以下情况时更新仓库级文档：

- 新增 skill
- 移除 skill
- 重命名 skill
- skill 的公开定位或 description 变化

需更新的文件：

- `README.md`
- `README.zh-CN.md`
- `marketplace.json`
- `AGENTS.md` 自身变更时同步 `docs/AGENTS.zh-CN.md`
