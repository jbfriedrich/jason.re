# Todo

Every open task for jason.re, and only here. Most important first. When an item is done,
delete it and put what's now true into its home (README, decisions).

## Open

- [ ] **Confirm the next deploy publishes under jason.re** (added 2026-11-15) — until the
  next push, the live build still uses `https://undertow.blog/` as its base URL (canonical
  links, Open Graph URLs, feed ids). The build host's domain setting was corrected on
  2026-11-15, so the next build fixes it. Done when
  `curl -s https://jason.re/index.xml | grep -m1 '<id>'` prints `https://jason.re/`.
- [ ] **Add a favicon** — every page links `/favicon.ico` (Wilde's `partials/head.html`),
  and neither this repo's `static/` nor the theme has one, so it 404s. Add
  `static/favicon.ico`. Done when `public/favicon.ico` exists after `hugo`.
- [ ] **Delete `static/CNAME`** — a GitHub Pages leftover; the site is not hosted on Pages,
  and the file is published as `/CNAME`.

## Waiting

- [ ] **Decide what undertow.blog links should do** — waits on the maintainer. Links
  shared between 2026-08-12 and 2026-11-14 point at undertow.blog, which now gets only the
  edge proxy's HTTP placeholder. Options: leave them broken, or have the edge proxy
  redirect undertow.blog to jason.re (needs a certificate for undertow.blog again).
- [ ] **Decide whether to consolidate the sites under one domain** — deferred by the
  maintainer to 2027. Nothing is planned until then.
