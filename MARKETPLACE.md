# Submit Folios to the Grok Build marketplace

Do this only after `https://mcp.folios.works/mcp` is publicly reachable with isolated OAuth. xAI CI fetches the pinned commit; a dead MCP is a review fail.

## Steps

1. Push this repo **public** under `FriskyDevelopments` (branded plugins from a personal hobby account get rejected).
2. Pin the default-branch HEAD:

   ```bash
   git ls-remote https://github.com/FriskyDevelopments/folios-grok-plugin.git HEAD
   ```

3. Fork [xai-org/plugin-marketplace](https://github.com/xai-org/plugin-marketplace).
4. Add the object in `marketplace-entry.json` to `.grok-plugin/marketplace.json`, replacing `PIN_AFTER_FIRST_PUBLIC_COMMIT` with the full 40-character lowercase SHA.
5. Regenerate and validate:

   ```bash
   python3 scripts/generate-plugin-index.py
   python3 scripts/validate-catalog.py
   ```

6. Open the PR. CI + code-owner review is required.

Keywords and domains stay brand-scoped (`folios`, `folios.works`, `cfdi`). Do not add generic terms (`invoice`, `api`, `database`).

This plugin does not run shell hooks, download binaries, or read `~/.ssh` / `.env`. The only network endpoint is `https://mcp.folios.works/mcp`.
