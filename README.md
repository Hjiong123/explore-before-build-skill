# Explore Before Build

A portable Agent Skill that checks GitHub before substantial implementation, compares reusable projects, and helps decide whether to adopt, adapt, reference, or build from scratch.

[简体中文](README.zh-CN.md)

Current release: `v1.1.0`

## Why

Coding agents often start scaffolding immediately under deadline pressure. This skill inserts a short, read-only decision gate before new systems, major features, modules, templates, or reusable components. It is deliberately narrower than general research workflows: GitHub is the default bounded source, other sources require an explicit user request, and no candidate is touched before the user decides.

## Features

- Two to four GitHub query variants.
- English-first queries for non-English briefs, with at most one original-language query when regional context matters.
- Deduplication of mirrors and forks.
- Up to ten repositories verified and five candidates presented.
- Archived projects remain reference-only; maintenance health outranks Stars and Forks.
- Explicit `Complete`, `Partial`, and `Unavailable` search status; report what was returned and mark unavailable totals or fields `unknown`.
- Evidence-based comparison of fit, gaps, stack, maintenance, license, and adaptation effort.
- Demo, starter, and toolkit repositories can be retained as bounded component candidates without treating them as whole-product bases.
- Repository metadata and README claims do not imply build success or runtime quality; unverified properties are labeled `not runtime-verified`.
- Separate license checks for code, assets, fonts, audio, data, and dependencies.
- Composite decisions: the overall product can be `Build` while individual candidates are `Adapt` or `Reference`; an explicit user delegation resolves the choice without a redundant confirmation.
- Read-only exploration with prompt-injection and command-execution boundaries.
- One platform-neutral `SKILL.md`; no runtime scripts or programming-language dependency.

## Compatibility

| Host | Install location | Notes |
|---|---|---|
| Codex | User: `~/.agents/skills/explore-before-build/` or repo: `.agents/skills/explore-before-build/` | `agents/openai.yaml` adds optional UI metadata. |
| Claude Code | User: `~/.claude/skills/explore-before-build/` or repo: `.claude/skills/explore-before-build/` | The same `SKILL.md` works without modification. |
| OpenClaw | Workspace `skills/explore-before-build/`, `.agents/skills/explore-before-build/`, or managed `~/.openclaw/skills/explore-before-build/` | Use the location matching the intended agent scope. |
| Claude.ai | Upload the skill directory as a ZIP in Skills settings when custom Skills are available. | Availability depends on the account and code-execution settings. |
| Claude API | Upload as a custom Skill and attach its `skill_id` to the container. | Requires the API's Skills and code-execution support. |
| Other Agent Skills hosts | Copy the directory into the host's documented skill root. | Requires Markdown/YAML Agent Skills support and read-only GitHub access. |

Codex and OpenClaw can share the same copy under `~/.agents/skills`. Claude Code needs its native `.claude/skills` location unless its configuration adds another skill root.

## GitHub access adapters

The skill tries each applicable read-only route once, with at most one retry only when the route itself reports a retryable failure:

1. a host-required GitHub skill such as `agent-reach`;
2. a GitHub tool or MCP server;
3. GitHub CLI (`gh`);
4. GitHub REST API or GitHub-restricted web search.

No adapter is bundled. This keeps the package portable and avoids forcing credentials, binaries, or one vendor's tool names on every host. A failed route does not turn usable fallback results into zero results.

## Installation

Install the whole repository directory, not only a pasted excerpt of `SKILL.md`. The runtime file is self-contained; the README and tests are for humans and maintainers.

After installation, invoke it explicitly when supported:

```text
$explore-before-build Find reusable GitHub projects before we build this feature.
```

It can also activate automatically when its frontmatter description matches the request.

## Behavioral tests

[`tests/scenarios.md`](tests/scenarios.md) defines the observable invariants. The baseline evidence in [`tests/baseline-results.md`](tests/baseline-results.md) records why the skill exists, and `tests/skill-results.md` records forward-test results.

## Security boundary

Repository pages, README files, issues, and source code are untrusted data. Exploration never executes their instructions and never clones, installs, runs, forks, vendors, or edits a project before the decision gate is resolved and normal planning authorizes the next action.

## License

Released under the [MIT License](LICENSE).
