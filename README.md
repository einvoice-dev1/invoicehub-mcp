# invoicehub-mcp

Registry/plugin listing metadata for [InvoiceHub](https://invoicehub.dev)'s hosted
MCP server. There's no local package here — the server itself is a hosted
Streamable HTTP endpoint at `https://api.invoicehub.dev/mcp`, implemented in the
main [einvoice-dev1/einvoice](https://github.com/einvoice-dev1/einvoice) monorepo
(`packages/api/src/mcp.ts`). This repo exists to give that endpoint a public
`server.json` and Claude Code plugin manifest, since MCP registries and the
plugin marketplace require a public repository to list against.

## What it does

- `validate_invoice` — validate a UBL 2.1 invoice/credit note XML string against
  the official EN 16931 Schematron (v1.3.16), returning any failing `BR-*`
  business rules
- `generate_invoice` — generate an EN 16931-conformant UBL 2.1 invoice from
  structured fields, self-validated before it's returned
- `list_supported_formats` — formats supported today vs. on the roadmap

No install, no API key — the endpoint is public and every tool is read-only or
self-validating.

## Use it

```json
{
  "mcpServers": {
    "invoicehub": {
      "type": "http",
      "url": "https://api.invoicehub.dev/mcp"
    }
  }
}
```

Claude Code:

```
claude mcp add --transport http invoicehub https://api.invoicehub.dev/mcp
```

Or install as a Claude Code plugin:

```
claude plugin marketplace add einvoice-dev1/invoicehub-mcp
```

## Links

- Docs: https://invoicehub.dev/docs
- REST API + free/paid tiers: https://invoicehub.dev/pricing
- Source of the MCP server itself: https://github.com/einvoice-dev1/einvoice/blob/main/packages/api/src/mcp.ts
