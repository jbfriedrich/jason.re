# jason.re

The content and configuration of [jason.re](https://jason.re), a personal blog of posts,
notes, links and photos. It is a [Hugo](https://gohugo.io/) site using the
[Wilde](https://github.com/jbfriedrich/wilde) theme, which is a git submodule at
`themes/wilde` and carries [tinycss](https://github.com/jbfriedrich/tinycss) as its own
submodule.

## How it is published

- **Writing.** New entries arrive as commits from publicare (and its local twin,
  publicare-cli), which turns plain Markdown into typed Hugo content and pushes it here.
  Hand edits are ordinary commits.
- **Building.** Every push to `master` triggers a signed GitHub webhook. The self-hosted
  build host runs [blogdeploy](https://github.com/jbfriedrich/blogdeploy), which clones this
  repository with its submodules, builds it with Hugo and swaps the live site over
  atomically. A failed build leaves the previous version online.
- **Base URL.** blogdeploy sets Hugo's `--baseURL` from its own domain setting for the
  site, which overrides `baseURL` in `config.yaml`. Changing the domain means changing it
  there, not only here.

Pushing to `master` is publishing.

## Layout

| Path | Contents |
|---|---|
| `config.yaml` | Site config: permalinks, taxonomies, menus, feeds, theme params |
| `content/posts/` | Long-form posts, `<date>-<slug>.md`, or a folder with `index.md` when they have a feature image |
| `content/notes/` | Short posts |
| `content/links/` | Link posts, flat `<date>-<slug>.md` |
| `content/photos/<slug>/` | Galleries: `index.md` plus the images |
| `content/domains/_index.md` | Hides the `/domains/` list page; per-domain pages live at `/links/<domain>/` |
| `content/archive.md`, `feeds.md`, `impressum.md`, `privacy.md` | Standalone pages |
| `static/` | Copied as-is: `robots.txt`, `images/` (author photo, logo) |
| `themes/wilde/` | The theme (submodule) |

The content types, URLs and theme params are documented in the
[Wilde README](https://github.com/jbfriedrich/wilde#readme).

## Feeds

Atom only (`RSS` is disabled), full content, newest 40 entries:

| Feed | Contents |
|---|---|
| `/index.xml` | Everything |
| `/posts/index.xml`, `/notes/index.xml`, `/links/index.xml`, `/photos/index.xml` | One section each |

## Working locally

```sh
git clone --recursive https://github.com/jbfriedrich/jason.re.git
cd jason.re
hugo server -p 1314
```

Without `--recursive`, run `git submodule update --init --recursive` first; the build
fails if `themes/wilde/assets/tinycss/` is empty.

To update the theme: `git submodule update --remote themes/wilde`, check the result
locally, then commit the new submodule pointer.

## Documentation

- [docs/decisions.md](docs/decisions.md) — why the blog lives where it does.
- [docs/todo.md](docs/todo.md) — every open task.
- [AGENTS.md](AGENTS.md) — rules for agents working in this repo.

## Licence

<a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by-nc-sa/4.0/88x31.png" /></a><br />This work is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/">Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License</a>.
