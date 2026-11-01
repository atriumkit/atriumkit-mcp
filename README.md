# AtriumKit MCP server

[AtriumKit](https://www.atriumkit.com) makes interactive product demos, step-by-step guides and
videos from one recording. Its hosted MCP server lets an AI assistant work on your demos for you:
"rewrite the tooltips for a CFO", "translate it into German and publish", "which step loses the
most viewers?".

This repository is documentation only. The server is hosted by AtriumKit, so there is nothing to
install or run.

| | |
| --- | --- |
| Server URL | `https://app.atriumkit.com/mcp` |
| Transport | Streamable HTTP |
| Auth | OAuth 2.1 (sign in and approve in the browser), or a personal access token sent as `Authorization: Bearer <token>` |
| Plans | Every AtriumKit plan |
| Clients | Claude (claude.ai, Desktop, mobile), Claude Code, ChatGPT, Cursor and other MCP clients |

Full setup guide with screenshots:
[Connect Claude, ChatGPT or Cursor to AtriumKit](https://www.atriumkit.com/help/ai-and-voice/connect-ai-assistants).

## Connect

### Claude

Works in claude.ai, Claude Desktop and the Claude mobile apps.

1. Open **Customize → Connectors** and choose **Add custom connector**. On Claude Team and
   Enterprise, an Owner adds it under **Organization settings → Connectors**, then each member clicks
   **Connect**.
2. Paste `https://app.atriumkit.com/mcp`. Leave the OAuth client fields empty.
3. Click **Add**, then **Connect**.
4. On the AtriumKit page that opens, sign in, pick the workspace and what Claude may do, then click
   **Allow access**.

### Claude Code

```sh
claude mcp add --transport http atriumkit https://app.atriumkit.com/mcp
```

Then run `/mcp` in Claude Code, pick `atriumkit` and choose **Authenticate**.

### ChatGPT

Custom MCP servers need developer mode, which is available on some ChatGPT plans.

1. In ChatGPT settings, open **Apps → Advanced settings** and turn on **Developer mode**.
2. Add a custom MCP server named AtriumKit, paste the server URL and choose OAuth. Leave the client ID
   and secret empty.
3. Sign in to AtriumKit, pick the workspace and what ChatGPT may do, then click **Allow access**.

### Cursor

Add this to `~/.cursor/mcp.json` (every project) or `.cursor/mcp.json` (one project). Cursor asks you
to sign in the first time it connects.

```json
{ "mcpServers": { "atriumkit": { "url": "https://app.atriumkit.com/mcp" } } }
```

### Other clients

Point any MCP client that supports Streamable HTTP at `https://app.atriumkit.com/mcp`. Clients that
support OAuth discover the authorization server from
`https://app.atriumkit.com/.well-known/oauth-protected-resource/mcp`. For a client or script that can
only send a fixed token, create a personal access token in AtriumKit under **Settings → AI assistants
& MCP → Access tokens** and send it as `Authorization: Bearer <token>`. Tokens work only on the MCP
server, never to sign in, and AtriumKit emails you when one is created.

## Permissions

You choose these when you connect an app or create a token. Your workspace role still applies: a
viewer's assistant can't edit, whatever was ticked.

| Scope | Name | What it allows | Role needed |
| --- | --- | --- | --- |
| `demos:read` | Read demos | See demos and collections: steps, copy, screens, share settings and links. Always included | Viewer |
| `demos:write` | Edit drafts | Change steps, copy, settings and translations, duplicate demos and add them to collections | Editor |
| `demos:publish` | Publish | Publish and unpublish demos | Editor |
| `analytics:read` | Read analytics | Views, completion rates, step funnels and traffic sources | Viewer |
| `leads:read` | Read leads | Names, emails and companies from lead forms. Only when you tick it | Viewer |

## What an assistant can do

List and read demos and screens; edit copy and steps; add choices; link navigation in clickable
demos; rewrite copy with AI; translate; generate voiceovers; publish and unpublish; read analytics
and leads; create personalized links; add demos to collections; read published guides; and search
the knowledge base.

Plan limits apply as in the app: translations, voiceovers, personalized links and the knowledge base
need Pro or Team, and AI rewrites and translations use the workspace's AI credits.

Every change an assistant makes shows in the demo's version history, marked like "Edits by Ana (via
Claude)", and can be restored. Assistants see screens the way viewers do: blurred areas, redacted
text and personal data on screenshots never go out.

## Limits

- Each connection or token works in one workspace. Connect again to use another.
- Up to 120 requests a minute per connection or token.
- Up to 25 active tokens per workspace.

## Disconnect

In AtriumKit, open **Settings → AI assistants & MCP** and click **Disconnect** next to an app or
**Revoke** next to a token. It stops working right away.

## Links

- Website: [atriumkit.com](https://www.atriumkit.com)
- MCP feature page: [atriumkit.com/product/mcp](https://www.atriumkit.com/product/mcp)
- Help center: [atriumkit.com/help](https://www.atriumkit.com/help)
- Support: [support@atriumkit.com](mailto:support@atriumkit.com)
- [Privacy](https://www.atriumkit.com/privacy) · [Terms](https://www.atriumkit.com/terms)

AtriumKit is made by Simplisik LLC.
