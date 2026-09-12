# 2hongo agent plugins

Plugin packages for [2hongo](https://www.2hongo.com), a Japanese learning app. One package, two hosts.

| Host                | Manifest                                    | Install                                         |
| ------------------- | ------------------------------------------- | ----------------------------------------------- |
| Claude Code, Cowork | `plugins/2hongo/.claude-plugin/plugin.json` | `/plugin marketplace add 2hongo/plugins`        |
| Codex               | `plugins/2hongo/.codex-plugin/plugin.json`  | add this repo as a marketplace, then `/plugins` |

Both hosts load the same skill from `plugins/2hongo/skills/2hongo-sensei/` and the same remote MCP
server at `https://www.2hongo.com/api/mcp`. The teaching skill needs no account; the dictionary tools
need a free 2hongo account, connected over OAuth on first use.

See [`plugins/2hongo/README.md`](./plugins/2hongo/README.md) for what the plugin does, example
prompts, and troubleshooting.

## Layout

```text
.claude-plugin/marketplace.json     Claude marketplace
.agents/plugins/marketplace.json    Codex marketplace
plugins/2hongo/                     the package both hosts install
```

## Contributing

This repository is **generated**. It is projected from 2hongo's application repository by a sync
script, so pull requests opened here are overwritten by the next sync. Please report issues through
[2hongo.com/en/contact](https://www.2hongo.com/en/contact).
