# LaunchFast Codex Plugin

LaunchFast for Codex is a standalone plugin bundle for Amazon FBA research workflows. It connects Codex to the production LaunchFast MCP server and includes reusable skills for product research, PPC planning, supplier sourcing, and full opportunity reviews.

- Website: [launchfastlegacyx.com](https://launchfastlegacyx.com)
- Docs: [docs.launchfastlegacyx.com/mcp](https://docs.launchfastlegacyx.com/mcp)

## What’s Included

- `.codex-plugin/plugin.json`
  The Codex plugin manifest.
- `.mcp.json`
  The MCP server definition pointing at the production LaunchFast endpoint.
- `skills/`
  Bundled Codex-native workflows for Amazon seller research.
- `assets/`
  Plugin icon, logo, and screenshots.

## Bundled Skills

- `launchfast-product-research`
  Fast keyword-level opportunity scans.
- `product-research`
  Deeper FBA viability analysis using LegacyX criteria.
- `launchfast-ppc-research`
  Competitor ASIN keyword research and PPC export workflow.
- `launchfast-full-research-loop`
  End-to-end product, IP, supplier, and PPC reporting.
- `alibaba-supplier-outreach`
  Supplier shortlist, outreach drafting, reply review, and follow-up workflow.
- `batch-product-research`
  Multi-keyword comparison and artifact generation.
- `kunze-ad-setup`
  Broader phrase/broad PPC build with deterministic bulksheet output.
- `wilco-ad-setup`
  Exact-match, analytics-first PPC build with deterministic bulksheet output.

## MCP Endpoint

This plugin is intentionally wired to the production LaunchFast MCP server:

```json
{
  "mcpServers": {
    "launchfast": {
      "type": "http",
      "url": "https://launchfastlegacyx.com/api/mcp/server"
    }
  }
}
```

Authentication happens through LaunchFast. The production endpoint supports OAuth, and LaunchFast dashboard users can also manage MCP/API credentials through LaunchFast settings.

## Repository Layout

```text
.
├── .codex-plugin/
│   └── plugin.json
├── .mcp.json
├── assets/
└── skills/
```

## Notes

- This repository is the plugin distribution, not the LaunchFast application codebase.
- The MCP implementation itself lives in the LaunchFast app and is consumed here as a remote production service.
- Skill outputs default to local artifact paths under `./artifacts/launchfast/...` so the plugin can be used without modifying the repository itself.
