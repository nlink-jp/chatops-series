# chatops-series

A collection of CLI tools for ChatOps workflows, maintained under the [nlink-jp](https://github.com/nlink-jp) organisation.

Each tool is a standalone project with its own repository, release cycle, and documentation.
This umbrella repository tracks them together as git submodules and hosts shared conventions.

## Tools

| Tool | Description |
|------|-------------|
| [swrite](https://github.com/nlink-jp/swrite) | Slack writer — post messages and files to Slack channels and DMs from pipelines |
| [stail](https://github.com/nlink-jp/stail) | Slack tail — stream channel messages in real time (`tail -f`) or export history to JSON |
| [scat](https://github.com/nlink-jp/scat) | General-purpose content poster — send text, files, and Block Kit messages to Slack from stdin or files |
| [slack-router](https://github.com/nlink-jp/slack-router) | Slack Slash Command daemon — routes commands to local shell scripts via Socket Mode |
| [md-to-slack](https://github.com/nlink-jp/md-to-slack) | Markdown → Slack Block Kit JSON filter — pipe into `swrite` to post formatted messages |
| [slack-mcp-extender](https://github.com/nlink-jp/slack-mcp-extender) | Transparent proxy for the official Slack MCP — adds ext_ file upload/download tools under the user's own identity |

## Design Philosophy

- **Pipe-friendly**: `swrite`, `stail`, and `scat` are composable with standard Unix tools — stdout is data, stderr is diagnostics.
- **Decoupled**: `slack-router` separates routing from response — the daemon ACKs the command, your script handles the reply.
- **Secure by default**: tokens via environment variables or config files; `slack-router` passes parameters via stdin JSON (not argv).
- **Server-ready**: `swrite`, `stail`, and `scat` support `*_MODE=server` for container and CI deployments.

## Build

All Go tools use a unified `Makefile` with consistent targets:

```sh
make build      # Build for the current platform → dist/<binary>
make build-all  # Cross-compile for all platforms → dist/<binary>-<goos>-<goarch>[.exe]
make package    # Build and create .zip archives → dist/<binary>-<version>-<goos>-<goarch>.zip
make test       # Run the test suite
make clean      # Remove dist/
```

Target platforms: `linux/amd64`, `linux/arm64`, `darwin/amd64`, `darwin/arm64`, `windows/amd64`.

> **Note for `slack-router`**: daemon tool — Windows is not a supported target platform.

## Shared Conventions

See [CONVENTIONS.md](https://github.com/nlink-jp/.github/blob/main/CONVENTIONS.md) for coding, documentation, and release standards that apply across all tools in this series.
