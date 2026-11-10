<p align="center"><img src="assets/logo.png" width="96" height="96" alt="Kreatix"></p>

# Kreatix MCP server

Let your AI agent schedule posts to your Instagram, TikTok, YouTube, Facebook, X, LinkedIn and Pinterest pages, move or cancel them, and read your numbers.

[Kreatix](https://kreatix.cc) is a social media scheduler for people who run many pages: one video goes to every connected page at once, each with its own platform settings. This repository documents its hosted MCP server. There is nothing to install or run.

| | |
|---|---|
| Address | `https://api.kreatix.cc/mcp` |
| Transport | Streamable HTTP, stateless |
| Auth | Your Kreatix agent key, as `Authorization: Bearer kx_live_...` or inside the address: `https://api.kreatix.cc/mcp/kx_live_...` |
| MCP Registry | [`cc.kreatix/kreatix`](https://registry.modelcontextprotocol.io/v0/servers?search=cc.kreatix) |

## Get a key

1. Sign up at [kreatix.cc](https://kreatix.cc) and connect your pages.
2. Open Settings, then AI agent ([kreatix.cc/settings/agent](https://kreatix.cc/settings/agent)) and create a key. It is shown once.
3. Delete the key there at any time and it stops working at once.

Scheduling through an agent needs a paid plan or a running trial, the same as scheduling in the app. It costs nothing extra.

## Connect your agent

**Claude** (claude.ai and Claude Desktop): open Customize, Connectors, Add custom connector, and paste the address with your key:

```
https://api.kreatix.cc/mcp/YOUR_KEY
```

**ChatGPT**: open chatgpt.com/plugins, press + and choose Add custom MCP server, with No authentication. Paste the same address with your key.

**Grok**: open grok.com/connectors and choose New Connector, Custom. Paste the same address with your key.

**Claude Code**:

```bash
claude mcp add --transport http --scope user kreatix https://api.kreatix.cc/mcp --header "Authorization: Bearer YOUR_KEY"
```

**Cursor** (`~/.cursor/mcp.json`):

```json
{
  "mcpServers": {
    "kreatix": {
      "url": "https://api.kreatix.cc/mcp",
      "headers": { "Authorization": "Bearer YOUR_KEY" }
    }
  }
}
```

**VS Code** (`.vscode/mcp.json`):

```json
{
  "inputs": [
    { "type": "promptString", "id": "kreatix-key", "description": "Kreatix agent key", "password": true }
  ],
  "servers": {
    "kreatix": {
      "type": "http",
      "url": "https://api.kreatix.cc/mcp",
      "headers": { "Authorization": "Bearer ${input:kreatix-key}" }
    }
  }
}
```

**Codex** (`~/.codex/config.toml`):

```toml
[mcp_servers.kreatix]
url = "https://api.kreatix.cc/mcp"
http_headers = { "Authorization" = "Bearer YOUR_KEY" }
```

**Cline**: see [llms-install.md](llms-install.md).

Other apps that speak MCP over HTTP can use the same address, with the key in a Bearer header or inside the address.

## Tools

| Tool | What it does |
|---|---|
| `list_channels` | Your connected pages, with followers and groups. |
| `list_groups` | Your page groups: one request reaches a whole brand. |
| `schedule_post` | A video or text post on the pages you name, now or later. |
| `list_posts` | What is planned and what went out. |
| `reschedule_post` | Move a planned post to another time. |
| `cancel_post` | Cancel a planned post. |
| `get_stats` | Views, followers and follower change for a period. |

A video can be one already in your Kreatix library, or a public YouTube, TikTok, Instagram or Facebook link that Kreatix brings in first.

## Ask in plain words

- "Post this TikTok link to all my Instagram pages tomorrow at 18:00."
- "Which page got the most views this week?"
- "Move tonight's posts on my brand group to 21:00."

## What keeps your pages safe

- Kreatix tells the agent to confirm the pages, the caption and the time with you before it schedules.
- A key can post only so many times an hour, so an agent stuck in a loop cannot flood your pages.
- The agent has the seven tools above and nothing more. It cannot delete pages, read messages or change your account.

## Skill file

[`skills/kreatix/SKILL.md`](skills/kreatix/SKILL.md) is a skill for OpenClaw and other agents that read SKILL.md files. It calls the same server with curl.

## Links

- Setup page: [kreatix.cc/ai-agents](https://kreatix.cc/ai-agents/)
- Website: [kreatix.cc](https://kreatix.cc)
- Support: support@kreatix.cc
