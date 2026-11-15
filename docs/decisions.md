# Decisions

Why jason.re is built and hosted the way the [README](../README.md) describes. Newest last.

## Wilde theme with the `stream` preset (2026-07-02)
The blog moved from the Hemingway theme to Wilde, a theme shared at the time with
outofscope.blog, and from free-form content to the four types publicare writes: posts,
notes, links and photos. jason.re uses the `stream` preset — the homepage is a compact,
dated list of everything — because it mixes many short notes with fewer long posts, and
rows show more of that at once than cards.

## Built on the self-hosted build host, not GitHub Pages (2026-07-17)
blogdeploy on the self-hosted build host replaced the GitHub Pages workflow; the workflow
was deleted the same day. A build there keeps a persistent Hugo image cache, which cuts a
rebuild from about a minute to seconds, and leaves hosting under the maintainer's control.
Pages was kept as a fallback for a while and is no longer used.

## Technical writing came back from outofscope.blog (2026-08-12)
On 2026-07-06 the technical notes moved to a separate blog, outofscope.blog, to keep
jason.re personal. Deciding which blog a piece belonged on cost more than writing it — the
topics overlap constantly — and the split was undone: all of outofscope.blog's posts, notes
and links were copied back here. outofscope.blog is retired; its repository is kept as an
archive and the site is not served.

## jason.re, not undertow.blog, is the blog's domain (2026-11-15)
From 2026-08-24 the blog was published as undertow.blog, a domain without the author's
name, chosen so the writing would not come up in a search for the name (see the
2026-08-08 domain-strategy note in the webdesign workspace). In use it felt too
impersonal, and on 2026-11-14 the site moved back to jason.re. undertow.blog is not used;
its DNS still points at the edge proxy, which serves only a placeholder for it. Whether
to bring all of the author's sites
under one domain is open until 2027 ([todo](todo.md)).
