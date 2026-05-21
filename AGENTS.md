# ubunatic.com

Personal website for Uwe Jugel — hosted at ubunatic.com, self-hosted server, static HTML/CSS/JS (no build step).

## Structure

```
index.html               # Landing page
<pkg>/index.html         # Go package redirect page (one per package)
<subpage>/index.html     # Other subpage
go-pkg-template.html     # Template for new Go package redirects
AGENTS.md                # This file (CLAUDE.md is a symlink to it)
```

## Go package redirects

Each Go package hosted at `ubunatic.com/<pkg>` is a static HTML page that:

1. Tells `go get` where the real VCS repo is via `<meta name="go-import">`.
2. Redirects human visitors to the Codeberg repo via `<meta http-equiv="refresh">`.

**Primary VCS host:** Codeberg (`codeberg.org/ubunatic/<pkg>`)

To add a new package redirect: copy `go-pkg-template.html` into `<pkg>/index.html` and replace `<pkg>`.

## Subpages

`<subpage>/index.html` is the entry point for any self-contained section of the site: demos, games, portfolio pieces, or personal web services. Each lives under its own directory and is served as a clean URL (`ubunatic.com/<subpage>`).

Subpages may be:
- **Static** — plain HTML/CSS/JS, no build step, served directly.
- **Dynamic** — a backend service running on the server, proxied through the WAF at `ubunatic.com/<subpage>`. The `index.html` in that case can be a loading page or is served by the backend itself.

No fixed template — structure and content are up to the subpage. The only convention is that `<subpage>/index.html` must exist so the server can resolve the clean URL.

## Hosting & deployment

- **Hosting:** self-hosted, git-based deploy (push to `main` triggers auto-deploy)
- **Server:** handles `<dir>/index.html` for clean URLs automatically — no extra config needed

## Conventions

- No build step. All files are served as-is.
- Keep HTML minimal and self-contained — no frameworks, no bundlers.
- CSS lives inline or in a top-level `style.css` that pages link to.
- Do not add generated files, lock files, or node_modules.
