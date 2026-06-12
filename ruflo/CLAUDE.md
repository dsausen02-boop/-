# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What This Repo Is

This is a **Claude Code plugin** (`.codex-plugin/plugin.json`) that wraps the `ruflo` npm package — a multi-agent orchestration layer built on top of Claude Flow. It is not a traditional application codebase; there is no build step, test suite, or source code to compile.

## MCP Server

The plugin registers a single MCP server (`ruflo`) via `.mcp.json`:

```json
npx -y ruflo@latest mcp start
```

This launches the Ruflo MCP server on demand using the latest published npm release. All orchestration tooling (swarms, memory, workflow) is provided by that package, not by files in this repo.

## Plugin Structure

| Path | Purpose |
|------|---------|
| `.codex-plugin/plugin.json` | Plugin manifest — name, version, MCP server ref, skills path, UI metadata |
| `.mcp.json` | MCP server definition consumed by Codex |
| `skills/<name>/SKILL.md` | Skill definitions (frontmatter + markdown instructions) |

## Adding or Editing Skills

Skills live under `skills/<skill-name>/SKILL.md` with YAML frontmatter:

```yaml
---
name: <slug>
description: <one-line description used for skill matching>
disable-model-invocation: false   # set true to suppress LLM calls inside the skill
---
```

The body is plain markdown — instruction prose shown to the model when the skill is invoked.

## Updating the Plugin Version

Version is tracked in `.codex-plugin/plugin.json` under `"version"`. Bump it manually when publishing a new release of the plugin.
