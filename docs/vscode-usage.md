# VS Code Usage Guide

This guide explains how to set up and use Spec Kit with Visual Studio Code, including GitHub Copilot Chat slash commands and the `specify` CLI.

## Command Types

| Command Type | Where to Run | Example |
|-------------|--------------|---------|
| CLI Commands | Terminal (Bash, PowerShell) | `specify init <PROJECT_NAME>` |
| Slash Commands | GitHub Copilot Chat panel | `/speckit.specify ...` |

## Installing the `specify` CLI

### Option 1: Persistent install with `uv tool install` (recommended)

Install `specify-cli` as a persistent tool so the `specify` command is available globally in your shell:

```bash
uv tool install --from git+https://github.com/github/spec-kit.git specify-cli
```

Verify the install:

```bash
specify --help
```

### Option 2: One-time run with `uvx` (no install required)

Run `specify` directly without installing it permanently:

```bash
uvx --from git+https://github.com/github/spec-kit.git specify init <PROJECT_NAME>
```

This is the quickest way to bootstrap a new project without modifying your global tool environment.

> **Note**: `uvx` is included with [`uv`](https://docs.astral.sh/uv/getting-started/installation/). You do not need to install `uvx` separately — install `uv` and `uvx` is available automatically. Do **not** use `pip install uvx`.

## Running the CLI Module Directly (Development / Local Checkout)

If you have cloned the repository and want to run the CLI from source without installing:

```bash
# From the repo root
python -m src.specify_cli --help
python -m src.specify_cli init demo-project --ai claude --ignore-agent-tools --script sh
```

See [Local Development Guide](local-development.md) for the full local workflow.

## Using Slash Commands in GitHub Copilot Chat

1. Open the **GitHub Copilot Chat** panel in VS Code (`Ctrl+Alt+I` / `Cmd+Alt+I`).
2. Type a slash command with the `/speckit` prefix, for example:

   ```text
   /speckit.specify Describe what you want to build here.
   ```

3. Available slash commands:

   | Command | Purpose |
   |---------|---------|
   | `/speckit.specify` | Create a feature specification |
   | `/speckit.plan` | Generate a technical implementation plan |
   | `/speckit.tasks` | Break the plan into actionable tasks |
   | `/speckit.implement` | Generate implementation from tasks |

> **Important**: Always keep the `/speckit` prefix. Removing it will break slash command behaviour.

## Troubleshooting

- **`specify` not found after install**: Run `uv tool update-shell` (or restart your terminal) to ensure the `uv` tools directory is on your PATH.
- **`uvx` not found**: Install `uv` from <https://docs.astral.sh/uv/getting-started/installation/>; `uvx` is bundled with it.
- **Slash commands not appearing**: Ensure the GitHub Copilot extension is installed and you have initialised the project with `specify init`.
- **Wrong script type**: Pass `--script ps` (PowerShell) or `--script sh` (Bash) to override auto-detection.
