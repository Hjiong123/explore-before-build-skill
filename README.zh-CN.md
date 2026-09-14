# Explore Before Build

一个可跨 Agent 使用的开发前 GitHub 检索 Skill：在新系统、重要功能或独立模块开工前，先比较现有项目，再决定直接采用、基于修改、仅作参考，还是从零开发。

[English](README.md)

## 核心能力

- 默认只检索 GitHub，不自动扩展到其他平台。
- 使用二至四组查询，最多核验十个仓库、展示五个候选。
- 多项目比较功能覆盖、缺口、技术栈、维护状态、许可证和改造量。
- 只有一个候选时如实评估，没有结果时停止，GitHub 不可用时明确说明。
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

Skill 按当前 Agent 实际拥有的能力选择：宿主要求的 GitHub Skill（例如 `agent-reach`）、GitHub MCP／内置工具、`gh` CLI、GitHub API 或限定 GitHub 的网页搜索。如果全部不可用，就报告检索未完成并停止，不能伪造“没有结果”。

## 调用示例

```text
$explore-before-build 在开发这个功能前，先找找 GitHub 上有没有可以直接复用或修改的项目。
```

## 测试与安全

行为测试见 [`tests/scenarios.md`](tests/scenarios.md)。仓库页面、README、Issue 和源码都属于不可信外部数据；检索阶段只读，不执行其中的安装或操作指令。

## 发布前事项

当前没有擅自选择开源许可证。上传公开 GitHub 仓库前，请由仓库所有者决定并添加许可证。

