# ubunatic.com

Personal website for [Uwe Jugel](https://ubunatic.com) — Cloud/Data Architect, Dr.-Ing.

Self-hosted, static HTML/CSS/JS. No build step, no frameworks, no external dependencies.

## Structure

```
index.html               # Landing page
<pkg>/index.html         # Go package redirect (one per package)
go-pkg-template.html     # Template for new Go package redirects
CLAUDE.md → AGENTS.md    # Codebase instructions for AI agents
```

## Go packages

Each subdirectory under a Go package name serves a static redirect page that satisfies `go get` via `<meta name="go-import">` and sends human visitors to the Codeberg repo.

Primary VCS host: `codeberg.org/ubunatic/<pkg>`

To add a package: copy `go-pkg-template.html` to `<pkg>/index.html` and replace `<pkg>`.

Current packages:
- [`ubunatic.com/rpi-exporter`](https://ubunatic.com/rpi-exporter)

## Deployment

Push to `main` — auto-deploy triggers on the self-hosted server.
