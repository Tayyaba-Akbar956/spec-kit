# VS Code Usage Guide

This guide explains how to run Specify commands when working in VS Code (or a compatible editor), and how to install the `specify` CLI for use alongside your AI assistant.

## CLI Commands vs. Slash Commands

| Command Type | Where to Run | Example |
|-------------|--------------|---------|
| CLI Commands | Terminal (Bash / PowerShell) | `specify init <PROJECT_NAME>` |
| Slash Commands | AI Assistant chat (e.g., GitHub Copilot Chat) | `/speckit.specify ...` |

- **CLI commands** have no leading slash and are typed in your terminal.
- **Slash commands** begin with `/speckit.` and are entered in an AI assistant or editor that supports slash commands (such as GitHub Copilot Chat in VS Code).

## Installing `specify`

### Persistent install (recommended)

Use `uv tool install` to add `specify` to your PATH permanently:

```bash
uv tool install --from git+https://github.com/github/spec-kit.git specify-cli
```

After this, `specify` is available in any terminal session:

```bash
specify --help
```

### One-time / ephemeral run

Use `uvx` to run `specify` without a permanent install:

```bash
uvx --from git+https://github.com/github/spec-kit.git specify init <PROJECT_NAME>
```

> **Note**: `uvx` is bundled with `uv`. Install `uv` from [https://docs.astral.sh/uv/](https://docs.astral.sh/uv/) — do **not** use `pip install uvx`.

## Running the CLI Directly from Source

If you have cloned the repository and want to run the CLI without installing it, use the module entrypoint from the repo root:

```bash
python -m src.specify_cli --help
python -m src.specify_cli init demo-project --ai copilot --script sh
```

## Using Slash Commands in Copilot Chat

1. Open the **GitHub Copilot Chat** panel in VS Code.
2. Type a slash command such as `/speckit.specify` followed by your prompt.
3. Ensure the `/speckit` prefix is present — removing it causes the text to be interpreted as a plain chat message rather than triggering the registered slash command.

Example:

```text
/speckit.specify Build a photo album organiser with drag-and-drop support.
```

## Troubleshooting

| Symptom | Fix |
|---------|-----|
| `specify: command not found` | Run `uv tool install --from git+... specify-cli` or use `uvx --from ...` |
| `uvx: command not found` | Install `uv` from [https://docs.astral.sh/uv/](https://docs.astral.sh/uv/) |
| Slash commands not appearing | Ensure GitHub Copilot Chat is active and project was initialized with `--ai copilot` |
| Wrong script type | Pass `--script sh` (Bash) or `--script ps` (PowerShell) to override auto-detection |

## Next Steps

- [Quick Start Guide](quickstart.md) — end-to-end walkthrough of the 4-step process
- [Installation Guide](installation.md) — detailed prerequisite and setup instructions
- [Local Development](local-development.md) — iterate on the CLI source locally
