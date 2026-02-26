# Facticity.AI MCP Server - Quick Start Guide

Welcome! This guide will help you connect to the Facticity.AI MCP Server and start fact-checking claims, extracting information, and verifying sources.

## What is This?

The Facticity.AI MCP Server provides AI assistants with powerful fact-checking capabilities. Once connected, you can:

- ✅ **Fact-check claims** - Verify if statements are true or false
- ✅ **Extract claims** - Pull claims from text or videos (YouTube, TikTok, Instagram)
- ✅ **Transcribe videos** - Get transcripts from video URLs
- ✅ **Check source reliability** - Assess website credibility and bias
- ✅ **Monitor credits** - Track your API usage

## Step 1: Get Your API Key

1. Visit [https://app.facticity.ai/api](https://app.facticity.ai/api)
2. Sign up or log in to your account
3. Copy your API key from the dashboard

**Keep your API key secure** - don't share it publicly!

## Step 2: Connect to the Server

The server is hosted at: **`https://mcp.facticity.ai/mcp`**

Choose your MCP client below and follow the instructions:

---

## For Claude Desktop Users

1. **Find your config file:**
   - **Windows**: `%APPDATA%\Claude\claude_desktop_config.json`
   - **macOS**: `~/Library/Application Support/Claude/claude_desktop_config.json`
   - **Linux**: `~/.config/Claude/claude_desktop_config.json`

2. **Open the config file** and add this configuration:

```json
{
  "mcpServers": {
    "facticity-ai": {
      "url": "https://mcp.facticity.ai/mcp",
      "env": {
        "FACTICITY_API_KEY": "your_api_key_here"
      }
    }
  }
}
```

3. **Replace `your_api_key_here`** with your actual API key from Step 1

4. **Restart Claude Desktop** completely (quit and reopen)

5. **Verify connection**: Ask Claude "What fact-checking tools do you have?" or "Check my credits"

---

## For Cursor Users

1. **Open Cursor Settings**
   - Press `Ctrl+,` (Windows/Linux) or `Cmd+,` (Mac)
   - Or go to File → Preferences → Settings

2. **Search for "MCP"** or "Model Context Protocol"

3. **Add the server configuration:**

```json
{
  "mcpServers": {
    "facticity-ai": {
      "url": "https://mcp.facticity.ai/mcp",
      "env": {
        "FACTICITY_API_KEY": "your_api_key_here"
      }
    }
  }
}
```

4. **Replace `your_api_key_here`** with your actual API key

5. **Restart Cursor** completely

6. **Test it**: Ask Cursor to fact-check something or check your credits

---

## For Other MCP Clients

If you're using a different MCP client, use this configuration:

**Server URL:** `https://mcp.facticity.ai/mcp`

**Required Headers:**
- `Content-Type: application/json`
- `Accept: application/json, text/event-stream`

**Environment Variable:**
- `FACTICITY_API_KEY`: Your API key from Step 1

**Or send API key in header:**
- `X-Facticity-API-Key: your_api_key_here`

---

## Step 3: Start Using It!

Once connected, you can ask your AI assistant to:

### Fact-Check Claims
```
"Fact-check: Vaccines contain microchips"
"Verify: The Earth is flat"
"Is it true that coffee causes cancer?"
```

### Extract Claims from Content
```
"Extract claims from this text: [paste text]"
"Extract claims from this YouTube video: https://youtube.com/watch?v=..."
```

### Check Source Reliability
```
"Check the reliability of https://example.com/article"
"Is this source credible: https://news-site.com/story"
```

### Transcribe Videos
```
"Transcribe this video: https://youtube.com/watch?v=..."
"Get the transcript from: https://tiktok.com/@user/video/123"
```

### Check Your Credits
```
"How many credits do I have?"
"Check my API usage"
```

---

## Available Tools

Your AI assistant now has access to these tools:

| Tool | What It Does |
|------|-------------|
| `fact_check` | Verifies if a claim is true or false with evidence |
| `extract_claim` | Extracts claims from text or video URLs |
| `transcribe_link` | Transcribes audio/video from URLs |
| `link_reliability_check` | Assesses website credibility and bias |
| `get_credits` | Shows your remaining API credits |
| `check_task_status` | Checks status of async fact-check tasks |

---

## Troubleshooting

### "API key not configured" error

**Solution:** Make sure you've:
1. Added your API key to the config file
2. Used the exact key from your Facticity.AI dashboard
3. Restarted your MCP client completely

### "Failed to connect" error

**Solution:**
1. Check your internet connection
2. Verify the server URL is correct: `https://mcp.facticity.ai/mcp`
3. Try accessing the health endpoint: `https://mcp.facticity.ai/health` (should return `{"status":"ok"}`)

### Tools not appearing

**Solution:**
1. Make sure you've restarted your MCP client after adding the config
2. Check the config file syntax is valid JSON
3. Look for error messages in your client's logs

### Out of credits

**Solution:**
1. Check your credits: Ask "How many credits do I have?"
2. Visit [https://app.facticity.ai](https://app.facticity.ai) to manage your account
3. Upgrade your plan if needed

---

## API Credit Usage

Each operation costs credits:

- **Fact-Check**: 1 credit per request
- **Extract Claims**: 1 credit per 1 million characters
- **Transcribe Link**: 1 credit per transcription
- **Link Reliability Check**: 1 credit per check
- **Get Credits**: Free (no credits consumed)
- **Check Task Status**: Free (no credits consumed)

Monitor your usage regularly with the `get_credits` tool!

---

## Need Help?

- **Documentation**: [https://app.facticity.ai/api](https://app.facticity.ai/api)
- **Support**: Visit [https://app.facticity.ai](https://app.facticity.ai) for support
- **Server Status**: Check `https://mcp.facticity.ai/health`

---

## Security Notes

🔒 **Keep your API key secure:**
- Never share your API key publicly
- Don't commit it to version control
- Use environment variables or secure config files
- Rotate your key if it's ever exposed

---

**Happy fact-checking!** 🎉
