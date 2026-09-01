# Folios — Grok plugin

Official Grok Build plugin for [Folios](https://folios.works).

Connects Grok to the Folios Worker for **clients, leads, and commercial invoice drafts**. Stamping, cancellation, PAC, and SAT tools are intentionally not included.

```text
MCP endpoint
https://mcp.folios.works/mcp
```

This repository does **not** claim that the remote MCP is already deployed. The URL is canonical. Connect it only after isolated OAuth is live: per-request user tokens, Worker-only upstream, HTTPS, origin/host validation, no process-global session.

## What it ships

| Path | Purpose |
| --- | --- |
| `.grok-plugin/plugin.json` | Plugin manifest |
| `.mcp.json` | Remote Folios MCP (HTTP) |
| `skills/folios/SKILL.md` | How Grok should use Folios |
| `skills/folios-safety/SKILL.md` | Fiscal safety (no stamping) |
| `commands/folios.md` | `/folios` slash command |
| `assets/logo.svg` | Brand mark |
| `marketplace-entry.json` | Payload for `xai-org/plugin-marketplace` |

## Install in Grok chat (today)

Grok chat does not self-list third-party tiles. Add Folios as a Custom connector:

1. Open [grok.com/connectors](https://grok.com/connectors)
2. **New Connector** → **Custom**
3. Name: `Folios`
4. URL: `https://mcp.folios.works/mcp`
5. Complete Folios OAuth

## Install in Grok Build

Until the official catalog lists `folios`:

```bash
grok plugin install https://github.com/FriskyDevelopments/folios-grok-plugin --trust
```

After the marketplace PR lands:

```bash
grok plugin install folios --trust
```

## Allowed tools

`folios_health`, `folios_session`, `folios_list_clients`, `folios_create_client`, `folios_update_client`, `folios_list_leads`, `folios_create_lead`, `folios_search`, `folios_list_invoice_drafts`, `folios_get_invoice_draft`, `folios_create_invoice_draft`, `folios_update_invoice_draft`, `folios_validate_invoice_draft`

Network endpoints this plugin calls: `https://mcp.folios.works/mcp` (OAuth to the Folios user session). No other hosts.

## Auth

- Human/interactive: Folios OAuth from the MCP connection flow.
- Never put PAC credentials, CSD material, Neon URLs, or machine tokens in this repo, in Grok, or in screenshots.

## Fiscal boundary

A commercial invoice draft is not a CFDI. Structural validation is not PAC validation. Do not claim UUID, sello, or XML timbrado unless a live Folios tool returns that evidence.

## Marketplace PR

See [MARKETPLACE.md](./MARKETPLACE.md). Pin `marketplace-entry.json` to a public commit SHA on this repo, then open a PR against [xai-org/plugin-marketplace](https://github.com/xai-org/plugin-marketplace).
