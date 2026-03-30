# Connect to Facticity.AI MCP (Hosted) — User Onboarding

This guide helps you connect any MCP-compatible client to the hosted Facticity.AI MCP server at `mcp.facticity.ai`. No self-hosting required.

## TL;DR — Connection Info

- MCP endpoint (POST): `https://mcp.facticity.ai/mcp`
- Protected resource metadata (OAuth discovery): `https://mcp.facticity.ai/.well-known/oauth-protected-resource`
- Dynamic Client Registration (DCR): `https://mcp.facticity.ai/register`
- Authorization endpoint: `https://mcp.facticity.ai/oauth/authorize`
- Token endpoint: `https://mcp.facticity.ai/oauth/token`
- Callback (handled by your MCP client): `{client-managed}`
- Required scopes: `openid profile email`

The server supports standard MCP flows. When your client first connects, it may be prompted to authenticate. Once authenticated, your live session will not re-prompt during the same MCP session.

## What You Get

- Fact-checking: verdicts with supporting/counter evidence and sources
- Claim extraction: from text and video URLs (YouTube, TikTok, Instagram)
- Transcription: get text from supported media links
- Source reliability: bias and quality assessment

## Connect With Common MCP Clients

### ChatGPT (External MCP Tool)

1) In ChatGPT, add an external MCP tool (name it “Facticity.AI” if you like).
2) When asked for a URL/endpoint, enter: `https://mcp.facticity.ai/mcp`
3) ChatGPT will follow the OAuth challenge:
   - You’ll be redirected to sign in.
   - Approve access. Upon completion you’ll return to ChatGPT.
4) You’re connected. In the same chat session, you won’t be asked to re-auth again.

Tips:
- If the connector supports “hosted URL only,” it will autodiscover via `/.well-known/oauth-protected-resource`.
- If it asks for scopes, provide: `openid profile email`.

### Cursor or Other MCP-Enabled IDEs/Apps

1) Open the MCP connector settings.
2) Use the endpoint: `https://mcp.facticity.ai/mcp`
3) Start the connection; follow the OAuth login flow in your browser.
4) Return to the client; the session will be live and ready.

If your client supports DCR, it can dynamically register at `https://mcp.facticity.ai/register`. Otherwise, it may use a static client configuration as documented by that client.

## Available Tools

- `fact_check` — Assess a single claim; returns verdict, assessment, evidence, and sources.
- `extract_claim` — Extract claims from text or supported media URLs; can transcribe audio/video.
- `transcribe_link` — Transcribe media at a URL (YouTube, TikTok, Instagram).
- `link_reliability_check` — Assess bias and quality for a URL using MediaBias data.
- `get_credits` — View your remaining credits and account info.
- `check_task_status` — Poll the status of long-running (async) jobs.
- `get_more_credits` — Guidance to purchase or restore credits.

Example call (conceptual):
```json
{ "name": "fact_check", "arguments": { "query": "The Eiffel Tower is 324 meters tall.", "mode": "sync" } }
```

## Prompts and Resources

- Prompts:
  - `fact_check_best_practices` — How to write precise, high-quality claims.
  - `onboarding` — Quick start suggestions.
- Resources:
  - `resource://facticity/homepage` — Dashboard, API links, and support.
  - `resource://facticity/api_docs` — Short API overview.

## Authentication Details

The first connection attempt triggers an OAuth login:
- Scopes: `openid profile email` (ensures your email is available, needed for account/credits)
- The server caches your verified auth for the duration of the MCP session (`mcp-session-id`). During that session, you won’t be asked to re-authenticate.

If you start a brand-new session (new `mcp-session-id`), the client may prompt you again to sign in.

## Troubleshooting

- I keep getting asked to log in again:
  - Ensure the client is preserving the same MCP session. Within one session, the server reuses verified auth.
- My client says it can’t find auth metadata:
  - Verify it is fetching: `https://mcp.facticity.ai/.well-known/oauth-protected-resource`
- I’m out of credits or see a billing/quota error:
  - Run the `get_credits` tool to confirm your balance.
  - Use `get_more_credits` for instructions to top up via the dashboard.
- A tool says parameters are missing:
  - Check tool input fields in your client’s tool UI; required parameters are documented by the server.

## Support

- Dashboard: `https://app.facticity.ai`
- API: `https://app.facticity.ai/api`
- Email: `support@facticity.ai`

## Privacy & Security

- Authentication is delegated through OAuth. Only the minimum scopes (`openid profile email`) are required.
- Sessions are cached per MCP session to reduce friction while maintaining security.

## About Facticity.AI

Facticity.AI provides AI-powered fact-checking with transparent evidence. It’s built to support professional workflows and everyday verification. Connect your MCP client and get started in minutes at `mcp.facticity.ai`.
