# parchmark-mcp

MCP server for managing ParchMark notes via Claude Code/Desktop.

## Installation

```bash
# Run directly
uvx --from git+https://github.com/TejGandham/parchmark-mcp parchmark-mcp

# Or install
pip install git+https://github.com/TejGandham/parchmark-mcp
```

## Configuration

### Environment Variables

| Variable | Description | Example |
|----------|-------------|---------|
| `PARCHMARK_URL` | API base URL | `https://parchmark.example.com/api` |
| `PARCHMARK_USERNAME` | Your username | `myuser` |
| `PARCHMARK_PASSWORD` | Your password | `mypassword` |

### Claude Code Setup

```bash
claude mcp add parchmark -s user \
  -e "PARCHMARK_URL=https://your-instance/api" \
  -e "PARCHMARK_USERNAME=your-user" \
  -e "PARCHMARK_PASSWORD=your-pass" \
  -- uvx --from git+https://github.com/TejGandham/parchmark-mcp parchmark-mcp
```

Or manually add to `.mcp.json`:

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

| Tool | Parameters | Description |
|------|------------|-------------|
| `list_notes` | None | List all notes (metadata only) |
| `get_note` | `note_id` | Get a specific note with full content |
| `create_note` | `content` | Create a new note from markdown |
| `update_note` | `note_id`, `content` | Update an existing note |
| `delete_note` | `note_id` | Delete a note |

## Architecture

```
parchmark-mcp/
├── src/parchmark_mcp/
│   ├── __init__.py      # Package version
│   ├── server.py        # FastMCP server & tools
│   ├── client.py        # ParchMark API client
│   └── models.py        # Pydantic models
├── tests/
│   ├── test_models.py   # Model tests
│   ├── test_client.py   # Client tests (mocked)
│   └── test_server.py   # Server tests (mocked)
└── pyproject.toml       # Package config
```

## Development

```bash
# Clone and install
git clone https://github.com/TejGandham/parchmark-mcp
cd parchmark-mcp
uv sync --all-extras

# Run tests
uv run pytest tests/ -v

# Lint & format
uv run ruff check src/ tests/
uv run ruff format src/ tests/

# Type check
uv run pyright src/ tests/
```

## Quality Gates

Pre-commit hooks enforce:
- `ruff` - Linting with autofix
- `ruff-format` - Code formatting
- `pyright --strict` - Type checking

## Tech Stack

- **FastMCP** - Python MCP framework
- **httpx** - Async HTTP client
- **Pydantic** - Data validation & models
- **pyright** - Static type checking (strict mode)
- **ruff** - Linting & formatting
- **pytest** - Testing with async support

## License

MIT
