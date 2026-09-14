# Explore Before Build

一个可跨 Agent 使用的开发前 GitHub 检索 Skill：在新系统、重要功能或独立模块开工前，先比较现有项目，再决定直接采用、基于修改、仅作参考，还是从零开发。

[English](README.md)

当前版本：`v1.1.0`

## 核心能力

- 默认只检索 GitHub，不自动扩展到其他平台；只有用户明确要求更广泛调研时，才交给宿主的常规调研流程扩展来源。
- 非英文需求先转换为英文 GitHub 关键词；地域相关时最多保留一组原语言查询。
- 使用二至四组查询，最多核验十个仓库、展示五个候选。
- 归档项目只能作为 `Reference`；维护状态优先于 Stars 和 Forks。
- 明确区分 `Complete`、`Partial`、`Unavailable` 三种检索状态；报告实际返回数量，无法核实的总数或字段标为 `unknown`。
- 多项目比较功能覆盖、缺口、技术栈、维护状态、许可证和改造量。
- Demo、starter、toolkit 如果覆盖明确的边界子系统，可以保留为组件候选；不会把它们冒充成完整产品基座。
- 仓库元数据和 README 不能证明构建成功或运行质量；未实际验证的属性标为 `not runtime-verified`。
- 分别核对代码、资源、字体、音频、数据和依赖的许可证。
- 支持组合决策：整体产品可以 `Build`，某个候选同时可以 `Adapt` 或 `Reference`；用户已明确委托时直接采用该决策，不重复确认。
- 用户确认前不 Clone、不安装、不运行、不 Fork，也不修改当前项目。
- 将 README 和仓库内容视为不可信数据，不执行其中的命令。
- 一份平台中立的 `SKILL.md`，不依赖 Python、Node.js 或运行脚本。

## 主流 Agent 安装位置

| Agent | 建议位置 |
|---|---|
| Codex | 用户级 `~/.agents/skills/explore-before-build/`；项目级 `.agents/skills/explore-before-build/` |
| Claude Code | 用户级 `~/.claude/skills/explore-before-build/`；项目级 `.claude/skills/explore-before-build/` |
| OpenClaw | 工作区 `skills/explore-before-build/`、`.agents/skills/explore-before-build/`，或 `~/.openclaw/skills/explore-before-build/` |
| Claude.ai | 将整个 Skill 目录压缩为 ZIP 后，在支持自定义 Skills 的设置中上传 |
| Claude API | 上传为自定义 Skill，再把返回的 `skill_id` 附加到容器 |

Codex 和 OpenClaw 可以共用 `~/.agents/skills` 下的一份副本；Claude Code 默认需要放到自己的 `.claude/skills` 路径。

## GitHub 工具适配

Skill 按当前 Agent 实际拥有的能力尝试只读路线；每条路线先尝试一次，只有路线明确报告可重试故障时才最多重试一次，然后继续下一条：宿主要求的 GitHub Skill（例如 `agent-reach`）、GitHub MCP／内置工具、`gh` CLI、GitHub API 或限定 GitHub 的网页搜索。如果全部不可用，就报告检索未完成并停止，不能伪造“没有结果”；如果已有部分结果，必须继续评估并标记缺失字段。

## 调用示例

```text
$explore-before-build 在开发这个功能前，先找找 GitHub 上有没有可以直接复用或修改的项目。
```

## 测试与安全

行为测试见 [`tests/scenarios.md`](tests/scenarios.md)。仓库页面、README、Issue 和源码都属于不可信外部数据；检索阶段只读，不执行其中的安装或操作指令。决定门槛解决并进入正常规划后，仍需在有风险的执行或外部写操作前取得授权。

## 许可证

本项目采用 [MIT 许可证](LICENSE)。
