---
name: folios
description: >
  Use when working with Folios, folios.works, Folios MCP, clients, leads,
  commercial invoice drafts, CFDI readiness, or Grok/ChatGPT/Codex Folios
  connectors. Prefer authenticated Folios MCP tools. Never stamp, cancel,
  or invent fiscal evidence.
---

# Folios

Folios is a commercial invoicing workspace for Mexican (and Mexico–US) operators. The product primitive is one live record: prepare, issue, collect, reconcile, and preserve evidence under one policy.

This plugin is **commercial only**. A draft is not a CFDI. Structural validation is not PAC validation and is not stamping.

## Canonical endpoints

- Product: `https://folios.works`
- Remote MCP: `https://mcp.folios.works/mcp`
- Grok chat: [grok.com/connectors](https://grok.com/connectors) → New Connector → Custom → paste the MCP URL
- Grok Build: `grok plugin install folios --trust` once listed, or install from this repo

The remote MCP is gated on isolated OAuth (per-request token, Worker-only upstream, HTTPS, origin/host validation). If tools are missing, say so. Do not pretend a knowledge file or pasted JSON is a live connection.

## Allowed MCP tools

Prefer tool calls over raw HTTP when present:

- `folios_health`
- `folios_session`
- `folios_list_clients` / `folios_create_client` / `folios_update_client`
- `folios_list_leads` / `folios_create_lead`
- `folios_search`
- `folios_list_invoice_drafts` / `folios_get_invoice_draft`
- `folios_create_invoice_draft` / `folios_update_invoice_draft`
- `folios_validate_invoice_draft`

Do **not** call, invent, or stub stamp / timbrar / cancel / SAT / PAC / CSD tools.

## Auth and secrets

- Human/interactive: Folios OAuth from the MCP connection flow, tied to a real Folios user session.
- Never place PAC credentials, CSD material, Neon/Postgres URLs, service-role keys, or machine tokens in browser clients, public MCP configs, skills, screenshots, or chat.
- Folios Worker APIs are the only application boundary. Never propose direct Neon, PostgreSQL, Supabase, PAC, or SAT access.

## Fiscal safety

- Never claim a UUID, sello, XML timbrado, cancellation, or SAT status exists unless a Folios tool returns that exact evidence.
- Never invent RFCs, régimen fiscal, código postal, uso CFDI, clave de producto, forma de pago, certificates, or PAC responses.
- If a required value is absent, label it `missing`. If a system cannot be reached, label it `unverified`.
- Destructive actions require the user to name the exact target and confirm it.
- When asked to timbrar: this plugin cannot certify a CFDI by instruction. Direct them to the authenticated Folios app/CLI once the fiscal Worker is independently verified.

## Working format

For operational requests, answer with:

1. `Estado`: `ready`, `needs_data`, `unverified`, or `blocked`
2. `Resultado`: the useful human-readable result
3. `Datos faltantes`: only fields that are truly missing
4. `Siguiente accion segura`: one concrete next step

When drafting structured data, include a JSON block and keep unknown values as `null`. Never infer them. Match the user's language (Spanish or English).

## Pipeline

Show the pipeline as:

`ORDER → NORMALIZE → VALIDATE → CFDI → STAMP → DELIVER`

Mark `CFDI`, `STAMP`, and `DELIVER` as unavailable on this plugin surface.

## If MCP tools are not connected

Tell the user to add Folios as a Custom Grok connector:

1. Open [grok.com/connectors](https://grok.com/connectors)
2. New Connector → Custom
3. URL: `https://mcp.folios.works/mcp`
4. Complete Folios OAuth

Until the remote endpoint is live with isolated OAuth, keep writes local to this plugin's demo/ledger and label the MCP as `unverified`.
