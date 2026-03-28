# CLAUDE.md — chatops-series

**Organization rules (mandatory): https://github.com/nlink-jp/.github/blob/main/CONVENTIONS.md**

## Non-negotiable rules

- **Tests are mandatory** — write them with the implementation. A feature is not complete without tests.
- **Design for testability** — pure functions, injected dependencies, no untestable globals.
- **Docs in sync** — update `README.md` and `README.ja.md` in the same commit as behaviour changes.
- **Small, typed commits** — `feat:`, `fix:`, `test:`, `chore:`, `docs:`, `refactor:`, `security:`

## This series

Pipe-friendly Slack tools for ChatOps automation and monitoring.

```
chatops-series/
├── md-to-slack/    github.com/nlink-jp/md-to-slack    (Go — Markdown → Slack Block Kit)
├── scat/           github.com/nlink-jp/scat            (Go — multi-destination content poster)
├── slack-router/   github.com/nlink-jp/slack-router    (Go — Slash Command daemon)
└── stail/          github.com/nlink-jp/stail           (Go — Slack tail -f)
```

## Release checklist

1. Update `CHANGELOG.md` → commit `chore: release vX.Y.Z` → tag → push
2. `gh release create` (no assets)
3. Build 5 platforms: `linux/amd64`, `linux/arm64`, `darwin/amd64`, `darwin/arm64`, `windows/amd64`
4. Zip each binary + `README.md` → upload one by one
5. Update umbrella submodule pointer in this repo
6. Update org profile: `nlink-jp/.github/profile/README.md`
