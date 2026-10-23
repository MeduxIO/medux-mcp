# Medux MCP Server

Connect AI assistants to [Medux](https://medux.io) for AI media generation and editing: video, image, speech, voice cloning, avatars, and PDF/audio/video tools.

MCP endpoint (streamable HTTP): `https://medux.io/api/mcp/v1`

Authentication: `Authorization: Bearer sk-medux-...` (create an API key in your Medux account).

## GitHub Copilot / VS Code

Add to `.vscode/mcp.json`:

```json
{
  "inputs": [
    { "type": "promptString", "id": "medux-api-key", "description": "Medux API key", "password": true }
  ],
  "servers": {
    "medux": {
      "type": "http",
      "url": "https://medux.io/api/mcp/v1",
      "headers": { "Authorization": "Bearer ${input:medux-api-key}" }
    }
  }
}
```

Or search `@mcp medux` in the VS Code Extensions view.

## Registry

Published to the MCP Registry as `io.github.MeduxIO/medux` via `.github/workflows/publish-mcp.yml`
(bump `version` in `server.json`, then run the workflow or push a `v*` tag).

## License
MIT
