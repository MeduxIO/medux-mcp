# Medux MCP Server

Connect AI assistants to [Medux](https://medux.io) for AI media generation and editing: video, image, speech, voice cloning, avatars, and PDF/audio/video tools.

- Endpoint (streamable HTTP): `https://medux.io/api/mcp/v1`
- Authentication: `Authorization: Bearer sk-medux-...`
- Tools: 60+ (generation, editing, conversion, task query)

## 1. Get an API key

Create an API key (starts with `sk-medux-`) in your Medux account at <https://medux.io>.
Keep it secret; do not commit it to a repository.

## 2. GitHub Copilot / VS Code

Requires VS Code with GitHub Copilot signed in, and Copilot Chat in **Agent** mode.

1. Run **MCP: Open User Configuration** from the Command Palette (⇧⌘P / Ctrl+Shift+P).
2. Add the server:

   ```json
   {
     "servers": {
       "medux": {
         "type": "http",
         "url": "https://medux.io/api/mcp/v1",
         "headers": { "Authorization": "Bearer ${input:medux-api-key}" }
       }
     },
     "inputs": [
       { "type": "promptString", "id": "medux-api-key", "description": "Medux API key", "password": true }
     ]
   }
   ```

3. In the MCP Servers list, open the gear next to `medux` and choose **Start Server** (or **Restart Server**).
4. In Copilot Chat (Agent mode) open the tools picker and confirm the `medux` tools are listed.
5. Try a harmless request first, for example: "Use medux to list what you can do".

### If the key prompt never appears

In some setups VS Code does not show the `${input:...}` prompt, and tool calls end with `Canceled` or `401`.
Replace the header value with your key directly in your **user-level** `mcp.json` (never in a repository):

```json
"headers": { "Authorization": "Bearer sk-medux-xxxxxxxx" }
```

Then restart the server.

### Troubleshooting

| Symptom | Likely cause |
| --- | --- |
| `401` / unauthorized | Missing `Bearer ` prefix, wrong or revoked key |
| `Canceled: Canceled` on every call | The key prompt was not answered; use the direct-header form above |
| `404` with `NOT_FOUND` | The request reached Medux; the task or resource id does not exist |
| Server not listed | Check **MCP: Open User Configuration** saved correctly; view logs via the gear → **Show Output** |

## Registry

Published to the [MCP Registry](https://registry.modelcontextprotocol.io) as `io.github.MeduxIO/medux`
through `.github/workflows/publish-mcp.yml` (GitHub OIDC).
To release a new version: bump `version` in `server.json`, then run the workflow or push a `v*` tag.

## License

MIT
