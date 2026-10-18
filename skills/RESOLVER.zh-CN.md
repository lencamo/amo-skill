# Amo 工作流路由

[English](./RESOLVER.md) | 中文

这个文件只服务于 `amo-*` 工作流路由。

README 是公开目录：列出所有 skill、安装命令和简短说明。
这个 resolver 是维护文档，用于处理多个 `amo-*` skill 都可能匹配同一个请求的场景。

运行时触发来源仍然是每个 `skills/amo-*/SKILL.md` frontmatter 里的 `description`。保持这个文件简短，只在 `amo-*` 触发边界变化时更新。

## 共享输出标记

所有 `amo-*` 工作流 skill 都需要在输出第一行以内联方式带上自己的 skill 标记：

| Skill | 标记 |
| :---- | :--- |
| `amo-feature` | `🧩 [amo-feature]` |
| `amo-improve` | `🧰 [amo-improve]` |
| `amo-fix` | `🛠️ [amo-fix]` |
| `amo-refactor` | `🧱 [amo-refactor]` |
| `amo-best` | `🏆 [amo-best]` |
| `amo-research` | `🔬 [amo-research]` |
| `amo-detail` | `🔎 [amo-detail]` |
| `amo-implement` | `🔨 [amo-implement]` |

标记必须和第一行内容放在同一行，不要单独成段。

## 主路由

| 用户意图 | 使用 |
| :------- | :--- |
| 构建当前不存在的新行为 | `amo-feature` |
| 有意改变、扩展、优化或重新设计已有行为 | `amo-improve` |
| 解释并修复错误、异常、不稳定、回归或失败的已有行为 | `amo-fix` |
| 调整结构、职责归属、耦合、状态/数据流、模块边界或组件边界 | `amo-refactor` |
| 挑战已有方案：“这是最佳方案吗？”“有没有更好方案？”“取舍/范围是否正确？” | `amo-best` |
| 调研竞品、社区实践或开源实现，寻找成熟、可复用的方案 | `amo-research` |
| 了解已有方案的整体链路、影响范围及前后端变化 | `amo-detail` |
| 实施已明确的方案并验证结果 | `amo-implement` |

## 维护规则

不要在这里重复每个 skill 的完整规则。这个文件只回答一个问题：

```text
面对这个用户请求，应该先使用哪个 amo 工作流 skill？
```
