# Client setup

Prowl is a remote MCP server over HTTP. Any client that speaks MCP can connect; below
are the four shapes that cover most of them.

```
Endpoint  https://prowl.chat/mcp
Header    Authorization: Bearer prowl_<your_key>
```

Get a key from the dashboard at [https://prowl.chat](https://prowl.chat) first.

## Claude Code

```bash
claude mcp add --transport http prowl https://prowl.chat/mcp \
  --header "Authorization: Bearer prowl_YOUR_KEY"
```

Then `/mcp` in a session to confirm it connected.

## Cursor

`~/.cursor/mcp.json`, or `.cursor/mcp.json` in the project:

```json
{
  "mcpServers": {
    "prowl": {
      "url": "https://prowl.chat/mcp",
      "headers": { "Authorization": "Bearer prowl_YOUR_KEY" }
    }
  }
}
```

Reload the window. The tools appear under Settings → MCP.

## Codex

`~/.codex/config.toml`:

```toml
[mcp_servers.prowl]
url = "https://prowl.chat/mcp"

[mcp_servers.prowl.headers]
Authorization = "Bearer prowl_YOUR_KEY"
```

## Any other MCP client

Streamable HTTP transport, one header. If your client supports OAuth 2.1, point it at
the endpoint without a key and let it discover the authorization server — see
[authentication](../authentication.md).

## Keeping the key out of the config

The configs above are files people commit by accident. Two habits that prevent it:

- Put the key in an environment variable and reference it, if your client expands them.
- Otherwise keep the config git-ignored, and store the key in your OS keychain or a
  secret manager.

A key is a wallet. A leaked one spends your balance until you revoke it.

## Verifying it works

Ask your agent to list Prowl's tools. You should see **23**. Then
the cheapest real call there is:

```json
{ "tool": "prowl_get_stats" }
```

It returns your usage and spend, touches no provider, and proves the whole path —
transport, auth, and account — in one request. If it fails, [troubleshooting](troubleshooting.md).
