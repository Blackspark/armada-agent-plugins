# Armada T1 — the MCP connection

This plugin is the connection to Blackspark's **Armada T1** MCP server, the
intake platform for Canadian personal (T1) tax returns. It contains one file
that matters, `.mcp.json`, which points Claude at the server. It carries no
skill, no hooks, no commands, no scripts and no local servers.

You normally do not install this plugin yourself. The `armada-t1` plugin
depends on it and pulls it in automatically; install that one. Keeping the
connection separate lets the workflow plugin pin the tool surface it was
tested against, so a change to the tools cannot move underneath a workflow.

## What it connects to and sends

- **`https://t1.blacksparkcorp.com/mcp/`** — the Armada T1 MCP server, the
  only destination. Every tool call goes there.
- **`https://id.blacksparkcorp.com`** — Armada ID, Blackspark's sign-in
  service, reached once when you connect (OAuth 2.1 with PKCE and dynamic
  client registration). You sign in with your own Armada account; nothing in
  this plugin holds a credential.

The data sent is whatever the tools are asked to read or write: client
identity, tax-file inputs, uploaded source documents, tasks and log entries.
It is stored in your firm's Armada workspace, scoped to your firm's tenant,
and every call is checked against your Armada role. No third party receives
anything from this plugin.

## Before you connect

You need an Armada T1 account with the preparer, reviewer or admin role,
granted by your firm's Armada administrator. Without it the connection
succeeds and every tool call refuses.

## The tool surface

Forty-one tools over clients, tax files, sections, section instances, tasks,
notices, the file log, source materials, Taxprep export and import, and the
reference picklists (countries, provinces, US states, NAICS). Each tool is
annotated: reads run without a per-call confirmation, writes are confirmed,
and deletes are permanent and governed.

## Documentation, privacy and support

- Product: <https://www.blacksparkcorp.com>
- Privacy policy: <https://www.blacksparkcorp.com/privacy-policy>
- Terms: <https://www.blacksparkcorp.com/terms-and-conditions>
- Support: <support@blacksparkcorp.com>

## Licence

See `LICENSE` in this folder.
