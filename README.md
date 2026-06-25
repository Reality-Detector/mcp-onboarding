# Connect to Facticity.AI MCP (Hosted) — User Onboarding

This guide helps you connect any MCP-compatible client (Claude, ChatGPT, Cursor, …) to the
hosted Facticity.AI MCP server. No self-hosting required.

## TL;DR — Connection Info

- **MCP endpoint (use this in your client):** `https://apiv2.facticity.ai/mcp`
- Protected-resource metadata (OAuth discovery): `https://apiv2.facticity.ai/.well-known/oauth-protected-resource`
- Authorization-server metadata: `https://apiv2.facticity.ai/.well-known/oauth-authorization-server`
- Dynamic Client Registration (DCR): `https://apiv2.facticity.ai/register`
- Authorization endpoint: `https://apiv2.facticity.ai/oauth/authorize`
- Token endpoint: `https://apiv2.facticity.ai/oauth/token`
- Required scopes: `openid profile email`

> **The endpoint URL must end in `/mcp`.** Pointing a client at the bare
> `https://apiv2.facticity.ai` will fail to connect — discovery happens at the domain root,
> but MCP traffic goes to `/mcp`.

When your client first connects it will walk you through a one-time sign-in. After that it
refreshes access automatically in the background — you won't be asked to log in again for
about **30 days** (see [Authentication](#authentication)).

## What You Get

- **Fact-checking** — verdicts (True / False / Unverifiable) with supporting/counter evidence and sources
- **Claim extraction** — from text and video URLs (YouTube, TikTok, Instagram), with auto-transcription
- **Transcription** — text from supported media links
- **Source reliability** — bias and quality assessment for a URL
- **Prediction-market insights** — ArAIstotle's Polymarket market odds, edges, and resolution-risk signals
- **X/Twitter analysis** — Truth Terminal account/keyword truth-score analysis

## Connect With Common MCP Clients

### Claude (Custom Connector)

1) Settings → Connectors → **Add custom connector**.
2) Name it "Facticity.AI" and set the URL to `https://apiv2.facticity.ai/mcp`.
3) Leave OAuth Client ID/Secret **blank** — the server supports Dynamic Client Registration,
   so Claude registers itself automatically.
4) Click **Connect**. You'll be redirected to sign in, then returned to Claude — connected.

### ChatGPT (Custom Connector / MCP)

1) Add a custom connector / external MCP tool, name it "Facticity.AI".
2) Enter the URL: `https://apiv2.facticity.ai/mcp`
3) Complete the sign-in when prompted; approve access and you'll return to ChatGPT.

### Cursor or Other MCP-Enabled IDEs/Apps

1) Open the MCP connector settings.
2) Use the endpoint: `https://apiv2.facticity.ai/mcp`
3) Start the connection and follow the OAuth login flow in your browser.

Clients that support DCR register automatically at `https://apiv2.facticity.ai/register`.
Hosted-URL-only connectors autodiscover via `/.well-known/oauth-protected-resource`. If a
client asks for scopes, use `openid profile email`.

## Available Tools

**Fact-checking & media**
- `fact_check` — Assess a single claim; returns verdict, assessment, evidence, sources. (1 credit)
- `extract_claim` — Extract claims from text or a media URL; can transcribe audio/video.
- `transcribe_link` — Transcribe media at a URL (YouTube, TikTok, Instagram).
- `link_reliability_check` — Bias/quality for a URL using MediaBias data.

**Account & help**
- `get_credits` — View your remaining credits and account info. (free)
- `check_task_status` — Poll an async fact-check by its `task_id`. (free)
- `get_more_credits` — How to purchase / restore credits. (free)
- `how_to_use` — What Facticity.AI is and how to get started. (free)

**Prediction-market insights (ArAIstotle / Polymarket)**
- `araistotle_recent_insights` — Recent markets with market odds, ArAIstotle odds, edge, and risk. (1 credit)
- `araistotle_insight` — One market's full insight. (2 credits to serve a stored one; 10 to generate a new one)

**X/Twitter analysis (Truth Terminal)** — no credit charge
- `truth_terminal_search_suggestions` — Autocomplete for a partial query.
- `truth_terminal_search_by_username` — Truth-score analysis for an account (async → `task_id`).
- `truth_terminal_search_by_keywords` — Tweet analysis by keywords (async → `task_id`).
- `truth_terminal_task_status` — Poll a Truth Terminal async task by `task_id`.

Example call (conceptual):
```json
{ "name": "fact_check", "arguments": { "query": "The Eiffel Tower is 324 meters tall.", "mode": "sync" } }
```

## Authentication

- The first connection triggers a one-time OAuth login, delegated to Auth0. Scopes:
  `openid profile email` (your email identifies your account and credits).
- Your client then holds a short-lived **access token** plus a **refresh token**, and renews
  access **silently in the background**. You stay connected — no repeated login prompts —
  until the refresh token expires (about **30 days**) or you remove the connector.
- The server is **stateless**: there's no server-side session to lose, so deploys/restarts
  don't drop your connection.

First-time users automatically get a Facticity API key with a starter credit balance, so
fact-checking works immediately after you connect.

## Troubleshooting

- **"…returned an error when connecting" / can't connect after signing in:**
  Make sure the connector URL is exactly `https://apiv2.facticity.ai/mcp` (with `/mcp`).
- **It can't find auth metadata:**
  Confirm the client can reach `https://apiv2.facticity.ai/.well-known/oauth-protected-resource`.
- **Out of credits / billing error:**
  Run `get_credits` to check your balance, then `get_more_credits` for top-up instructions.
- **A tool says parameters are missing:**
  Check the required fields in your client's tool UI (e.g. `fact_check` needs `query`).

## Support

- Dashboard: `https://app.facticity.ai`
- API & credits: `https://app.facticity.ai/api`
- Email: `support@facticity.ai`

## Privacy & Security

- Login is delegated through OAuth (Auth0); only the minimum scopes (`openid profile email`)
  are requested.
- Access is granted via short-lived tokens with automatic, rotating refresh — no passwords
  are ever seen or stored by the MCP server.

## About Facticity.AI

Facticity.AI provides AI-powered fact-checking with transparent evidence, plus prediction-
market insights and social-media truth analysis. Connect your MCP client at
`https://apiv2.facticity.ai/mcp` and get started in minutes.
