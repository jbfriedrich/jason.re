# AGENTS.md — working in the jason.re repo

The content and config of the jason.re blog. Read the [README](README.md) first. Reasons
are in [docs/decisions.md](docs/decisions.md); **[docs/todo.md](docs/todo.md) holds every
open task** — add new ones there and delete them when done.

## Rules

- **A push to `master` publishes the live site.** Never push without the maintainer's
  go-ahead. Commit only when asked; no `Co-Authored-By` or other AI attribution.
- **Content is the author's.** publicare writes most entries; don't rewrite posts, notes or
  links unless asked. Its front matter conventions (`title:` only when the author wrote one,
  `url:` on links, `domains:`) are load-bearing for the theme.
- **Theme changes belong in Wilde**, not in `layouts/` here. This repo has no layout
  overrides; keep it that way. Update the theme by bumping the `themes/wilde` submodule.
- **Never modify photo files.** Display problems are fixed in Wilde's templates.
- **The production base URL comes from blogdeploy**, not `config.yaml` (see the README).
- **Public repo: name private repos, don't link them.** This repository is public. Its
  docs may mention a private repository (publicare, publicare-cli, the infrastructure
  repository, outofscope.blog) or a document in one by name, but never link to it — the
  link is a 404 for everyone else — and never copy infrastructure details out of it: no
  host or VM names, addresses, ports, user names, home paths or secret-manager item names.
