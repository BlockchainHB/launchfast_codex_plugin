# LaunchFast Codex Plugin

LaunchFast for Codex is a Codex plugin marketplace repository for Amazon FBA research workflows. It exposes the `launchfast` plugin through the GitHub-installable marketplace layout that Codex expects, and the plugin itself connects Codex to the production LaunchFast MCP server with bundled skills for product research, PPC planning, supplier sourcing, and full opportunity reviews.

- Website: [launchfastlegacyx.com](https://launchfastlegacyx.com)
- Docs: [docs.launchfastlegacyx.com/mcp](https://docs.launchfastlegacyx.com/mcp)

## What’s Included

- `.agents/plugins/marketplace.json`
  Marketplace metadata so Codex can discover and install the plugin from this GitHub repository.
- `plugins/launchfast/.codex-plugin/plugin.json`
  The LaunchFast plugin manifest.
- `plugins/launchfast/.mcp.json`
  The MCP server definition pointing at the production LaunchFast endpoint.
- `plugins/launchfast/skills/`
  Bundled Codex-native workflows for Amazon seller research.
- `plugins/launchfast/assets/`
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

Authentication happens through LaunchFast using Codex's MCP OAuth flow against the remote LaunchFast MCP server. Codex manages the OAuth client flow and may open a localhost or `127.0.0.1` loopback callback such as `http://127.0.0.1:<ephemeral-port>/callback` during authorization.

Do not manually replace that callback URL with a LaunchFast domain URL. The loopback callback is expected for the local Codex client.

## Installation

Use the repository URL in Codex:

```text
https://github.com/BlockchainHB/launchfast_codex_plugin
```

Codex should detect the marketplace entry in `.agents/plugins/marketplace.json` and install the `launchfast` plugin from `plugins/launchfast`.

The marketplace entry uses install-time auth:

```json
{
  "policy": {
    "installation": "AVAILABLE",
    "authentication": "ON_INSTALL"
  }
}
```

## Repository Layout

```text
.
├── .agents/
│   └── plugins/
│       └── marketplace.json
└── plugins/
    └── launchfast/
        ├── .codex-plugin/
        │   └── plugin.json
        ├── .mcp.json
        ├── assets/
        └── skills/
```

## Notes

- This repository is a plugin marketplace repo, not the LaunchFast application codebase.
- The MCP implementation itself lives in the LaunchFast app and is consumed here as a remote production service.
- The plugin points directly at the remote LaunchFast MCP server at `https://launchfastlegacyx.com/api/mcp/server`; it does not use a local shell wrapper.
- Codex owns the OAuth redirect flow for this plugin. Loopback localhost or `127.0.0.1` callbacks are expected and should not be rewritten.
- Skill outputs default to local artifact paths under `./artifacts/launchfast/...` so the plugin can be used without modifying the repository itself.
