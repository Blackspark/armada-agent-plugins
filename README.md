# Blackspark Armada — agent plugins

The packages that plug **Armada** into an AI agent: an MCP connector and the
agent workflows that use it, installable into Claude Code, Claude Desktop,
claude.ai and Codex from this one repository.

| Plugin | What it is |
|---|---|
| [`armada-t1`](plugins/armada-t1) | Agent workflows for Canadian T1 tax files — the `gather` intake skill. Install this one. |
| [`armada-t1-mcp`](plugins/armada-t1-mcp) | The MCP connection to Armada T1. Installed automatically as a dependency of `armada-t1`. |

## Install

```sh
# Claude Code
/plugin marketplace add Blackspark/armada-agent-plugins
/plugin install armada-t1@armada

# Codex
codex plugin marketplace add https://github.com/Blackspark/armada-agent-plugins.git
codex plugin add armada-t1@armada
```

You need an Armada T1 account, granted by your firm's Armada administrator.
On first use you sign in at Armada ID with your own account; the plugins ship
no credentials. Each plugin's README describes exactly what it runs, sends and
connects to.

## Updates

This repository is generated from Blackspark's release pipeline — one commit
per Armada release. Claude Code and Codex pick up a new version with
`claude plugin update armada-t1@armada` / `codex plugin update armada-t1@armada`;
the Claude directory serves it automatically.

## Links

- Blackspark: <https://www.blacksparkcorp.com>
- Privacy policy: <https://www.blacksparkcorp.com/privacy-policy>
- Terms: <https://www.blacksparkcorp.com/terms-and-conditions>
- Support: <support@blacksparkcorp.com>
