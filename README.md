# parchmark-mcp

MCP server for managing ParchMark notes via Claude Code/Desktop.

## Installation

```bash
uvx --from git+https://github.com/TejGandham/parchmark-mcp parchmark-mcp
```

## Configuration

Set environment variables:

- `PARCHMARK_URL` - API base URL (e.g., `https://parchmark.example.com/api`)
- `PARCHMARK_USERNAME` - Your username
- `PARCHMARK_PASSWORD` - Your password

### Claude Code (.mcp.json)

```json
{
  "mcpServers": {
    "parchmark": {
      "command": "uvx",
      "args": ["--from", "git+https://github.com/TejGandham/parchmark-mcp", "parchmark-mcp"],
      "env": {
        "PARCHMARK_URL": "https://parchmark.example.com/api",
        "PARCHMARK_USERNAME": "your-username",
        "PARCHMARK_PASSWORD": "your-password"
      }
    }
  }
}
```

## Tools

| Tool | Description |
|------|-------------|
| `list_notes` | List all notes (without content) |
| `get_note` | Get a specific note with full content |
| `create_note` | Create a new note from markdown |
| `update_note` | Update an existing note |
| `delete_note` | Delete a note |
