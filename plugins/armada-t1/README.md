# Armada T1 — agent workflows for Canadian T1 tax files

Armada T1 is Blackspark's intake platform for Canadian personal (T1) tax
returns. This plugin teaches Claude how to **gather** a tax file on it: run a
taxpayer intake interview, read the slips and receipts a firm hands over,
write structured input records, attach each source document for provenance,
raise anything ambiguous as a task instead of guessing, and hand the file off
with its inputs complete, ready for the preparation stage of your workflow. Preparation, calculation, review and filing stay in the
firm's own tax software — this plugin builds the inputs.

## What the plugin contains

- **One skill, `gather`** (`skills/gather/SKILL.md`): instructions Claude
  follows during an intake. It is text only. There are no hooks, no commands,
  no agents, no scripts and no local servers in this plugin.
- **A reference to the Armada T1 MCP server.** On Claude the server comes from
  the `armada-t1-mcp` plugin, installed automatically as a dependency. On
  Codex, which has no plugin dependencies, the same server is declared in
  `mcp/armada-t1.json`.

## What it connects to and sends

The only network destination is Blackspark's own service:

- **`https://t1.blacksparkcorp.com/mcp/`** — the Armada T1 MCP server. Every
  tool call goes there and nowhere else.
- **`https://id.blacksparkcorp.com`** — Armada ID, Blackspark's sign-in
  service, reached once when you connect (OAuth 2.1 with PKCE and dynamic
  client registration). You sign in with your own Armada account; the plugin
  ships no credentials.

What Claude sends to the server is what you ask it to record: client
identity, the figures from slips and receipts, uploaded source documents, and
tasks and log entries about the file. Everything is stored in your firm's
Armada workspace under your firm's tenant, and the server enforces your
Armada role on every call. Nothing is sent to any third party by this plugin.

## Before you install

You need an Armada T1 account with the preparer, reviewer or admin role. Your
firm's Armada administrator grants it. Without one, the connection succeeds
and every tool call refuses — by design.

## Install

```sh
# Claude Code
/plugin marketplace add Blackspark/armada-agent-plugins
/plugin install armada-t1@armada        # pulls armada-t1-mcp in automatically

# Codex
codex plugin marketplace add https://github.com/Blackspark/armada-agent-plugins.git
codex plugin add armada-t1@armada
```

Then ask Claude to gather a tax file, or run `/armada-t1:gather` in Claude
Code. On first use you are sent to Armada ID to sign in.

## Tools, in plain terms

Reads (run without a per-call confirmation): list and search clients and tax
files, read and verify a section, list section states, tasks, notices, source
materials and the file log, look up countries, provinces, US states and
NAICS codes. Writes (always confirmed): create clients, files, section
instances, tasks, log entries and source materials; update or delete any of
them; set a section's applicability; move a file through its workflow stages; reconcile tasks and
notices; export to or import from Personal Taxprep. Deletes are permanent and
governed: a client with files cannot be deleted, and a file delete previews
first.

## Documentation, privacy and support

- Product: <https://www.blacksparkcorp.com>
- Privacy policy: <https://id.blacksparkcorp.com/privacy>
- Terms: <https://id.blacksparkcorp.com/terms>
- Documentation: <https://id.blacksparkcorp.com/help/armada-t1/claude>
- Support: <support@blacksparkcorp.com>

## Licence

See `LICENSE` in this folder. The skill is a reference implementation:
you may copy and adapt it for your own firm's use of Armada.
