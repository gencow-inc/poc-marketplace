# GENCOW POC & Education Marketplace

Codex plugin marketplace for GENCOW POC demonstrations and education. The repository also includes project-scoped MCP configuration for Claude Code.

## Add to Codex Desktop

1. Open **Plugins** → **Plugins Directory** → **Add marketplace** (or **Add from GitHub**).
2. Enter **gencow-inc/poc-marketplace**.
3. Choose **GENCOW POC & Education**, install the plugins you need, then complete OAuth authorization when prompted.

Codex CLI:

```sh
codex plugin marketplace add gencow-inc/poc-marketplace
```

## Use with Claude Code

Claude Code can connect to these remote MCP servers. The root `.mcp.json` configures the two GENCOW servers for this repository.

1. Clone this repository and open Claude Code from its directory:

```sh
git clone https://github.com/gencow-inc/poc-marketplace.git
cd poc-marketplace
claude
```

2. Trust the repository if Claude Code asks, then approve the listed project MCP servers. Complete OAuth authorization if prompted.

Add and install the Claude Code plugin marketplace:

```text
/plugin marketplace add gencow-inc/poc-marketplace
/plugin install one-am@gencow-poc-education
```

Replace `one-am` with `slow-memo`, `gencow-developer`, or `gencow-tools` to install another plugin. Each plugin connects to its corresponding remote MCP server; Claude Code will prompt you to authorize OAuth when the server requests it.

## Included plugins

| Plugin | MCP endpoint | Purpose |
| --- | --- | --- |
| 새벽 한 시 | https://1am.gencow.link/api/mcp | Create and manage your own characters |
| 느린 메모 | https://blog.gencow.link/api/mcp | Draft and manage blog posts and images |
| GENCOW 개발용 | https://docs.gencow.com/api/mcp | Connect to GENCOW developer documentation tools |
| GENCOW 기타 도구 | https://tools.gencow.com/api/mcp | Connect to GENCOW utility tools |

The GENCOW MCP servers use OAuth; this repository does not contain access tokens or client secrets. 새벽 한 시 works with the connected user's characters. 느린 메모 creates drafts by default and only publishes when explicitly requested.

## Plugin icons

Each plugin keeps its icon in `plugins/<name>/assets/`. Both `logo` (listing) and `composerIcon` (composer) in `.codex-plugin/plugin.json` → `interface` reference that local file. Asset paths resolve from the plugin root.

- **새벽 한 시** uses the app's original 512 × 512 PNG from https://1am.gencow.link/icons/icon-512.png.
- **느린 메모** uses a note and leaf icon.
- **GENCOW 개발용** uses a code window icon.
- **GENCOW 기타 도구** uses a toolbox icon.

The three SVG icons are included in this repository. To replace an icon, update its asset and keep both manifest paths in sync. Icon changes require refreshing the marketplace and updating the installed plugin in Codex.

## MCP discovery and authentication

These plugins use the Codex compatibility layout: `.codex-plugin/plugin.json` explicitly references `./.mcp.json`. Each `.mcp.json` declares its HTTP server URL; Codex discovers OAuth from the server's protected-resource metadata and `401` challenge. The marketplace requests authentication on installation with `policy.authentication: "ON_INSTALL"`.

This layout was checked with Codex `0.167.0-alpha.4.1`. In that client, the previous portable `plugin.json` / `mcp.json` packages returned an empty `mcpServers` list, so installation succeeded without discovering a server or starting OAuth. Do not add a root `plugin.json` alongside the compatibility manifest without checking MCP discovery: it takes precedence in this client.

After updating the source, refresh the marketplace and reinstall/update existing plugins to replace their cached package. Verify that the plugin details show its MCP server, then complete the account connection. Installation alone does not prove authentication succeeded.

For OAuth to start, unauthenticated MCP requests must reach the server and return `401` with a `WWW-Authenticate: Bearer resource_metadata="..."` challenge, and discovery endpoints must be accessible. A Cloudflare `403` prevents this discovery; inspect the site's security events and configure access for legitimate MCP clients rather than changing plugin authentication to anonymous.
