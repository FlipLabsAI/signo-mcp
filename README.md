# Signo MCP server

[![Signo MCP connector](https://glama.ai/mcp/connectors/fi.signo/signo/badges/score.svg)](https://glama.ai/mcp/connectors/fi.signo/signo) [![smithery badge](https://smithery.ai/badge/signo/Signo)](https://smithery.ai/servers/signo/Signo) [![M8ven Score](https://m8ven.ai/badge/mcp/fliplabsai-signo-mcp-0igvdy?v=f9f9d90c865994ab64a70c22279295a1)](https://m8ven.ai/mcp/fliplabsai-signo-mcp-0igvdy?s=readme)

[Signo](https://signo.fi) gives your AI assistant tools to set up agents that watch DeFi positions and alert you on Telegram. An agent can watch an Aave health factor, an LP range, a Pendle maturity or idle cash, and prepare the next step for you to sign.

The assistant only drafts. The wallet owner reviews every draft and signs it in Signo. The assistant never gets wallet keys or spending rights.

This repository is the public listing for Signo's hosted MCP server: its registry entry, setup snippets and example prompts. The server runs at `app.signo.fi`. There is nothing to install or build.

## Addresses

| Address | Sign-in | Tools |
| --- | --- | --- |
| `https://app.signo.fi/api/mcp` | None | 3 tools: read a public wallet report, draft an agent, draft an Execute permission |
| `https://app.signo.fi/api/mcp/account` | Your Signo account (OAuth, wallet sign-in) | The same 3, plus 6 to list, read, pause, resume, edit and remove your own agents |

Both speak MCP over Streamable HTTP. Official MCP Registry name: `fi.signo/signo`.

## Add it

Claude Code, no sign-in:

```bash
claude mcp add --transport http signo https://app.signo.fi/api/mcp
```

Cursor, in `.cursor/mcp.json`:

```json
{
  "mcpServers": {
    "signo": { "url": "https://app.signo.fi/api/mcp" }
  }
}
```

Claude (claude.ai, web or desktop), with your account:

1. Open Settings, then Connectors, and click Add custom connector.
2. Name it Signo and enter `https://app.signo.fi/api/mcp/account`.
3. Click Connect, sign in with your wallet on the Signo page, and click Allow.

ChatGPT (developer mode), with your account:

1. In Settings, open Apps & Connectors, then Advanced settings, and turn on Developer mode.
2. Create an app named Signo with `https://app.signo.fi/api/mcp/account` and OAuth.
3. Sign in with your wallet on the Signo page and click Allow.

More setup detail: [docs.signo.fi/for-assistants](https://docs.signo.fi/for-assistants/).

## Tools

No sign-in:

| Tool | What it does |
| --- | --- |
| `wallet_insights_report` | Reads a public report on any wallet, with the agents it suggests. Read-only. |
| `signo_draft_agent` | Drafts a Notify or Prepare agent from plain English. Returns a review link for the owner. |
| `signo_draft_permission` | Drafts an inactive Execute permission on X Layer or Arbitrum. The owner authorizes it onchain. Execute is in early access; a wallet without access gets a Prepare draft instead. |

With your Signo account, also:

| Tool | What it does |
| --- | --- |
| `signo_account_agents` | Lists the agents on your account. |
| `signo_account_agent` | Reads one agent's setup and its last check. |
| `signo_account_agent_history` | Reads its notifications and Execute runs. |
| `signo_account_agent_status` | Pauses or resumes it. |
| `signo_account_agent_update` | Edits supported fields on Notify and Prepare agents. |
| `signo_account_agent_remove` | Removes it and keeps its history. |

## How a draft becomes an agent

1. The assistant calls a draft tool and gets a private review link.
2. The wallet owner opens the link, connects the wallet and links Telegram.
3. The owner signs once. Only then does the agent run.

An Execute permission sets one action, one token, a limit per firing, a lifetime limit and an expiry. The [Signo Shield](https://github.com/FlipLabsAI/signo-shield) contract checks every firing against those limits. The owner can revoke it onchain at any time.

## Example prompts

See [examples/prompts.md](examples/prompts.md).

## Links

- Website: [signo.fi](https://signo.fi)
- Docs: [docs.signo.fi](https://docs.signo.fi)
- Privacy: [signo.fi/legal/privacy](https://signo.fi/legal/privacy)
- Terms: [signo.fi/legal/terms](https://signo.fi/legal/terms)

## License

The files in this repository are under the MIT License. See [LICENSE](LICENSE).
