# Installing the Kreatix MCP server

The Kreatix MCP server is hosted at `https://api.kreatix.cc/mcp` (streamable HTTP). Nothing has to be cloned, built or run.

1. Ask the user for their Kreatix agent key. They create it in Kreatix under Settings, then AI agent: https://kreatix.cc/settings/agent. It starts with `kx_live_`. Never guess or invent a key.
2. Add the server to the MCP settings file (for Cline, `cline_mcp_settings.json`), with the user's key in place of `YOUR_KEY`:

```json
{
  "mcpServers": {
    "kreatix": {
      "type": "streamableHttp",
      "url": "https://api.kreatix.cc/mcp",
      "headers": { "Authorization": "Bearer YOUR_KEY" },
      "disabled": false
    }
  }
}
```

3. Test it with the `list_channels` tool. It returns the user's connected pages.
   - A 401 means the key is missing or was deleted. Ask the user for a new key.
   - An empty list means no pages are connected yet. The user connects them at https://kreatix.cc.

Before `schedule_post`, `reschedule_post` or `cancel_post`, show the user the pages, the caption and the time, and wait for a yes. TikTok posts need `tiktok_privacy` and `tiktok_music_confirmed` from the user. There is no default, so ask.
