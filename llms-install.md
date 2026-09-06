# Amazon Vendor Central MCP install notes for AI agents

Amazon Vendor Central MCP runs in the operator's own Kuudo deployment. This repository is a registry facade: metadata plus a catalog-only stub. Do not run this repository as the production server; it lists tools and refuses calls.

## Preferred setup: the operator's deployment

Ask the operator for the deployment hostname and a Kuudo API key, then configure:

```json
{
  "mcpServers": {
    "amazon-vendor-central-mcp": {
      "url": "https://<your-host>/mcp",
      "headers": { "Authorization": "Bearer <your Kuudo API key>" }
    }
  }
}
```

Canonical product page: https://www.kuudo.com/features/amazon-vendor-central-mcp/
Docs: https://www.kuudo.com/docs/mcp-reference/tools/
Client quick starts: https://www.kuudo.com/docs/

## Local: inspect the catalog only

```bash
npm ci
node src/index.mjs
```

`tools/list` returns 40 catalog entries. Every `tools/call` returns `isError: true` with setup guidance.
