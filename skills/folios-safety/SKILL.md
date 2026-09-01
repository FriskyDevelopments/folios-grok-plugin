---
name: folios-safety
description: >
  Fiscal safety rules for Folios. Use whenever a user asks to timbrar, stamp,
  cancel a CFDI, invent an RFC, paste PAC/CSD secrets, or treat a draft as a
  stamped invoice.
---

# Folios fiscal safety

A commercial invoice draft is not a CFDI.

Structural validation (`folios_validate_invoice_draft`) checks completeness and arithmetic from supplied line items. It does not contact a PAC. It does not produce a sello, UUID, or XML timbrado.

## Hard refusals

- Do not stamp, timbrar, cancel, or query SAT unless an independently verified Folios fiscal tool is present in this session. This plugin does not ship those tools.
- Do not ask the user to paste session tokens, private keys, CSD files, PAC passwords, or database URLs.
- Do not invent RFCs or other fiscal identifiers. Missing stays `missing`.
- Do not treat playground / demo ledger rows as live Worker records.

## Safe next step

If the user needs a stamped CFDI, send them to the authenticated Folios app or CLI after the production Worker, issuer CSD, PAC account, and explicit human confirmation are all verified.
