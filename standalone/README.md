# SummarizeVideo.ai MCP server for Kiro

Connect Kiro to the hosted SummarizeVideo.ai MCP server to read summaries and transcripts from your account. You can also request new summaries for public video URLs with a key that allows creation.

## Connect in Kiro IDE

1. Sign in to SummarizeVideo.ai and create a **Read only** key on the [Agent keys page](https://summarizevideo.ai/agent-keys). Use **Summarize and read** only when you want Kiro to start summaries.
2. Make the key available as `SUMMARIZEVIDEO_TOKEN` in the environment that starts Kiro. Use a shell or secret manager that keeps the value out of history. Approve expansion of that variable in Kiro if prompted. [Kiro environment variable settings](https://kiro.dev/docs/mcp/configuration/#environment-variables).
3. Open **Add to Kiro** and review the server URL and configuration before accepting. To set up just the current workspace, add the `summarizevideo` entry from [mcp.json](mcp.json) to `.kiro/settings/mcp.json` under `mcpServers`. Keep the variable reference in the file.

[![Add to Kiro](https://kiro.dev/images/add-to-kiro.svg)](https://kiro.dev/launch/mcp/add?name=summarizevideo&config=%7B%22url%22%3A%22https%3A%2F%2Fmcp.summarizevideo.ai%2Fmcp%22%2C%22headers%22%3A%7B%22Authorization%22%3A%22Bearer%20%24%7BSUMMARIZEVIDEO_TOKEN%7D%22%7D%2C%22disabled%22%3Afalse%2C%22autoApprove%22%3A%5B%5D%7D)

Kiro connects to `https://mcp.summarizevideo.ai/mcp` over Streamable HTTP and sends the scoped key as a Bearer token. Revoke the key on the Agent keys page when you stop using it.

## Tools and account limits

- `get_summary(requestID)` returns status and the Markdown summary when it is done. For an in-progress request, check again about every 30 seconds.
- `get_transcript(requestID, startCharacter?, maxCharacters?)` reads the source transcript when available. Pass `nextStartCharacter` back as `startCharacter` for the next page.
- `summarize_video(url, summaryLanguage?)` is available with **Summarize and read** access. It returns a request ID and may start processing. Resubmitting can restart failed work or advance a scheduled retry.

Summaries belong to the account that requested them. Reads leave the summary, allowance, and pass credits as they are. New work can download media, use the normal rolling 24-hour allowance or an existing Founding Pass credit, and send a completion email. Pass purchases happen on the website.

[Hosted MCP documentation and limits](https://summarizevideo.ai/mcp-server) · [Privacy](https://summarizevideo.ai/privacy) · [Support](mailto:hboon@motionobj.com)
