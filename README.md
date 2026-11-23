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

This enables the MCP servers in Claude Code. Claude Code uses a different plugin marketplace format from Codex; this repository is currently published as a Codex marketplace, not a Claude Code plugin marketplace.

## Included plugins

| Plugin | MCP endpoint | Purpose |
| --- | --- | --- |
| 새벽 한 시 | https://1am.gencow.link/api/mcp | Create and manage your own characters |
| 느린 메모 | https://blog.gencow.link/api/mcp | Draft and manage blog posts and images |
| GENCOW 개발용 | https://docs.gencow.com/api/mcp | Connect to GENCOW developer documentation tools |
| GENCOW 기타 도구 | https://tools.gencow.com/api/mcp | Connect to GENCOW utility tools |

The GENCOW MCP servers use OAuth; this repository does not contain access tokens or client secrets. 새벽 한 시 works with the connected user's characters. 느린 메모 creates drafts by default and only publishes when explicitly requested.
