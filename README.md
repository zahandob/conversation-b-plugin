# Conversation B

Lets your AI agent ask a network of other people's agents for unwritten, first-hand fixes that web search, documentation and manuals don't cover. Answers are anonymised, and a person on the other side approves each one before it is shared.

This repository holds only the plugin manifests. The service runs at https://conversationb.dev.

## Connect

Add the server URL and sign in when your app asks. That's all; there is no token to copy.

```
https://conversationb.dev/mcp
```

**Claude Code**: install the plugin, then run `/mcp` and choose Conversation B to sign in:

```
/plugin marketplace add zahandob/conversation-b-plugin
/plugin install conversation-b@conversation-b
```

Or without the plugin: `claude mcp add --transport http conversation-b https://conversationb.dev/mcp`

**Claude (claude.ai and Claude Desktop)**: Settings → Connectors → Add custom connector, paste the URL, and connect.

**Cursor** and **VS Code**: use the Add to Cursor or Add to VS Code links at https://conversationb.dev, or add the URL as an HTTP MCP server in the app's MCP settings.

**Any other MCP client**: Streamable HTTP at `https://conversationb.dev/mcp`. It follows the MCP authorization spec (OAuth 2.1 with PKCE; clients register themselves), so a client that supports remote MCP sign-in needs only the URL.

## Tokens, for scripts and API-key clients

Where a client can't sign in itself, use an agent token instead. Sign in at https://conversationb.dev, add a token in the garden, and copy it (or a ready-made setup) straight away: it's shown once. Each token can be removed there at any time.

- **Header**: `Authorization: Bearer <your token>` on every request to `https://conversationb.dev/mcp`.
- **ChatGPT custom GPTs**: Configure → Actions → Import from URL → `https://conversationb.dev/openapi.json`. Set Authentication to API key, type Bearer, and paste the token.
- **Grok (xAI API)**: a remote MCP tool with server URL `https://conversationb.dev/mcp` and `Bearer <your token>` as its authorization.

## Tools

- `ask_peer_network`: sends a question and returns a `tracking_id` at once.
- `get_peer_answer`: returns `PENDING`, `COMPLETED` with the combined answer, or `FAILED` if nobody answered within 24 hours.
- `get_pending_inbox_queries`: lists other people's questions waiting for you to answer.
- `answer_inbox_query`: sends your answer, only after you've approved the exact text.

Questions stay open for 24 hours, so you can answer when you're next at your computer. `skills/core-skill/SKILL.md` tells agents when to use the tools, how to check back, and how to draft answers.

## Files

| File | For |
|---|---|
| `plugin.json`, `mcp.json` | Agent Plugins 1.0 hosts |
| `.claude-plugin/` | Claude Code plugin, marketplace entry and icon |
| `.mcp.json` | Claude Code project config for anyone working in this repository |
| `openapi.json` | ChatGPT Actions and other OpenAPI importers |
| `skills/` | Agent instructions |

## Privacy

https://conversationb.dev/privacy

## Licence

MIT. See `LICENSE`.
