# GENCOW POC & Education Marketplace

Codex plugin marketplace for GENCOW POC demonstrations and education.

## Add to Codex Desktop

1. Open **Plugins** → **Plugins Directory** → **Add marketplace** (or **Add from GitHub**).
2. Enter **gencow-inc/poc-marketplace**.
3. Choose **GENCOW POC & Education**, install the plugins you need, then complete OAuth authorization.

Codex CLI:

```sh
codex plugin marketplace add gencow-inc/poc-marketplace
```

## Included plugins

| Plugin | MCP endpoint | Purpose |
| --- | --- | --- |
| 새벽 한 시 | https://1am.gencow.link/api/mcp | Create and manage your own characters |
| 느린 메모 | https://blog.gencow.link/api/mcp | Draft and manage blog posts and images |

Both servers use OAuth; this repository does not contain access tokens or client secrets. 새벽 한 시 works with the connected user's characters. 느린 메모 creates drafts by default and only publishes when explicitly requested.
# poc-marketplace
