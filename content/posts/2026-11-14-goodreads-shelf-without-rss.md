---
title: Reading a Goodreads shelf without the RSS feeds
date: 2026-11-14T18:56:02
slug: goodreads-shelf-without-rss
summary: 'Goodreads discontinued its RSS feeds and the shelf pages now require a login. A public widget, a profile page and the GraphQL API behind the book pages still get you the whole shelf with full book details, without any login.'
tags: [development, automation, selfhosting, books]
languages: [en]
---

I was working on a small project that reads one of my Goodreads shelves a few times a day. It used the shelf's RSS feed, as it had for years. Until one morning, when every request came back with a `404`. Goodreads quietly [discontinued its RSS feeds](https://www.goodreads.com/blog/show/20-more-rss-feeds) in October 2026: "To keep your data secure, we retired this low-usage feature."

The official recommendation is the CSV export under _My Books → Import & Export_. That is fine for a one-off backup, but useless for anything that is supposed to run on its own. The public API has been gone since 2020. And the HTML version of a shelf (`/review/list/<user id>?shelf=to-read`) now redirects to the sign-in page.

So I looked at what Goodreads still serves without a login. It turns out to be quite a lot.

## What still works without logging in

| Endpoint | What you get |
|---|---|
| `/review/custom_widget/<user id>` | The shelf itself, via the embeddable blog widget: title, author, cover, review id. At most 100 books per request. |
| `/user/show/<user id>` | The public profile, including the exact number of books on each shelf. |
| `/book/show/<book id>` | The book page. It is built from a GraphQL API that you can query directly. |
| `/book/auto_complete?format=json&q=…` | The search suggestions, a small JSON list with book ids. |

The shelf and the profile have to be public, of course. Everything else is plain HTTP.

## The shelf widget

Goodreads still offers widgets that bloggers can embed to show their shelves. The "custom widget" is a small JavaScript file that writes the HTML of your shelf into the page, and it is happy to be requested on its own:

```shell
$ curl -s "https://www.goodreads.com/review/custom_widget/12345678?shelf=to-read&num_books=100&sort=date_added&order=d&widget_id=abc123"
  var widget_code = '  <div class=\"gr_custom_container_abc123\">\n [...]
            <a title=\"In the Shadow of Eight\" rel=\"nofollow\" href=\"https://www.goodreads.com/review/show/9087955320?utm_medium=api&amp;utm_source=custom_widget\"><img alt=\"In the Shadow of Eight\" border=\"0\" src=\"https://i.gr-assets.com/images/S/compressed.photo.goodreads.com/books/1781766398l/253943224._SY75_.jpg\" /><\/a>
[...]
            by <a rel=\"nofollow\" href=\"https://www.goodreads.com/author/show/70741857.Collin_Gosselin\">Collin Gosselin<\/a>
[...]
```

Take the string after `var widget_code = '`, undo the JavaScript escapes (`\"`, `\/`, `\n`, `\'`) and you have plain HTML. Every entry contains:

- **the review id** (`/review/show/9087955320`). It identifies the entry on the shelf and stays the same even when the book moves to another shelf, so it is the perfect key,
- **title and author**,
- **the cover**, and inside its file name **the book id** (`…/books/1781766398l/253943224._SY75_.jpg`). Remove the size suffix `._SY75_` and you get the full-size cover.

A few things I learned the hard way:

- **`num_books` is capped at 100**, and the `page` parameter is ignored.
- **`sort` and `order` work**, including `sort=random`. This becomes important in a minute.
- **The output is cached per `widget_id`.** Use a new one for every request, or you get the same result again.
- **Books without a cover** come with a `nophoto` placeholder and therefore without a book id. More on that below.
- **The grid widget** (`/review/grid_widget/…`) returns 200 books per request, which looks tempting. But it silently drops books without a cover, so you can never be sure you got all of them.

## Getting past 100 books

My shelf has over 600 books, and the widget only shows 100 at a time. But every sort order shows a *different* 100. So I collect them: the first and the last 100 for each sort key (`date_added`, `title`, `author`, `date_pub`, `avg_rating`, `num_pages`, `num_ratings`, `isbn`, each with `order=a` and `order=d`), and then `sort=random` until nothing is missing.

How do you know when nothing is missing? The public profile page shows the exact count per shelf:

```shell
$ curl -sL https://www.goodreads.com/user/show/12345678 | grep -A2 'shelf=to-read"'
            <a class="actionLinkLite userShowPageShelfListItem" href="/review/list/12345678?shelf=to-read">
              to-read
              (636)
```

For my 636 books, the sixteen fixed orders found 590. The random samples found the rest. That is about 40 requests in total, around 450 KB compressed, one minute with a pause of 1.5 seconds between requests.

Two things make this cheap and safe to run regularly:

1. **Only delete when the count matches.** I only remove books that were not found when the collected set is exactly as large as the profile count. A harvest that falls short (time limit, network issue) may add books, but never removes any.
2. **Check before you harvest.** Two requests are usually enough: the profile count and the 100 newest entries (`sort=date_added&order=d`). If the count is unchanged and all of the newest are known, nothing changed. If the count grew by exactly the number of unknown new entries, those are simply additions and can be inserted directly. Only removals need the full harvest.

## The GraphQL API behind the book pages

The widget does not give you a description, rating, page count or publication year. The book page has all of that, but it is expensive: about 640 KB per book. Goodreads does not compress it, no matter which `Accept-Encoding` you send. For 600 books that is roughly 400 MB.

The book pages are built with [Next.js](https://nextjs.org/), and the data comes from an [AWS AppSync](https://aws.amazon.com/appsync/) GraphQL API. Every page ships the API key in its embedded `__NEXT_DATA__` JSON. It is a public key, not a login: every anonymous visitor's browser uses it.

```shell
$ curl -s https://www.goodreads.com/book/show/68427 | grep -o '"apiKey":"[^"]*"'
"apiKey":"da2-…"
```

The endpoint is in the site's main JavaScript bundle (`/_next/static/chunks/pages/_app-….js`). With both, you can ask for exactly the fields you need. And with [aliases](https://graphql.org/learn/queries/#aliases), you can ask for several books in a single request:

```shell
$ curl -s --compressed https://<redacted>.appsync-api.us-east-1.amazonaws.com/graphql \
    -H "x-api-key: $KEY" -H "Content-Type: application/json" \
    -d '{"query":"query { b0: getBookByLegacyId(legacyId: 68427) { ...F } b1: getBookByLegacyId(legacyId: 19161852) { ...F } } fragment F on Book { title description imageUrl details { numPages publicationTime isbn13 } work { stats { averageRating } details { publicationTime } } }"}'
{
  "data": {
    "b0": {
      "title": "Elantris",
      "description": "Elantris was the capital of Arelon: gigantic, beautiful, literally rad…",
      "imageUrl": "https://m.media-amazon.com/images/S/compressed.photo.goodreads.com/books/1475740953i/68427.jpg",
      "details": { "numPages": 638, "publicationTime": 1148972400000.0, "isbn13": "9780765350374" },
      "work": { "stats": { "averageRating": 4.16 }, "details": { "publicationTime": 1114930800000.0 } }
    },
    "b1": {
      "title": "The Fifth Season",
      [...]
    }
  }
}
```

(I shortened the descriptions; you get the full text.)

The `legacyId` is the book id from the cover file name, and it has to be an `Int`. `details.publicationTime` belongs to this particular edition, while `work.details.publicationTime` is the original publication. Both are milliseconds since the epoch.

The difference is dramatic. With **25 books per request**, a book costs about **800 bytes instead of 640 KB**. My whole shelf of 636 books took 26 requests and about a minute.

Why 25 and not 100? I tried 50, and the request was blocked by AppSync's firewall (`403 WAFForbiddenException`). The limit seems to be the size of the *request body*: 50 lookups were 11.7 KB, and AWS WAF's standard rule set blocks bodies over 8 KB. A single request right afterwards went through, so it is not a ban, just a size limit. Use a fragment like the `...F` above, so each additional book only adds a few dozen bytes, and keep the body well below 8 KB.

## Some details that cost me time

- **Stale book ids.** When Goodreads merges editions, the cover file name in the widget can keep the *old* book id. GraphQL then answers that alias with `RESOURCE_NOT_FOUND` ("Book is invalid"), and the book page is a "soft 404": HTTP 200 with the title "Page not found". In that case I look the book up once by title and author through `/book/auto_complete?format=json&q=…` and continue with the current id. If that finds nothing either, the book really is gone.
- **Books without a cover** have no book id in the widget at all. The same autocomplete lookup solves that.
- **A 404 is final, everything else is not.** I never retry a missing book. A `429`, a `5xx`, a firewall `403` or a network error gets retried after a wait, using `Retry-After` if Goodreads sends one. Watch out: an AWS WAF challenge can come with status `202` and an `x-amzn-waf-action` header, so a `2xx` alone does not mean you got the content.
- **The key rotates.** If GraphQL answers `401`, read the key from a book page again. I store it and only fetch a page when needed.
- **Keep a fallback.** This API is undocumented and can change any day. If GraphQL stops working, my code falls back to parsing the `__NEXT_DATA__` of the book pages. That is slower, but it keeps working.

## Be nice

None of this is an official API. Everything above is what the Goodreads website itself does in every visitor's browser. But automated access is still a grey area under their terms, and they can change or block it whenever they like.

So: request only what you need, keep the requests spaced out, batch where you can, cache the results and don't fetch the same book twice. Back off when you get a `429` or a firewall response, and never try to get around a challenge. In my case that means a quick check of two requests four times a day, a full harvest of about 40 requests only when a book was removed, and the details for each new book fetched exactly once.

If you ran into the same 404 as I did, I hope this saves you a few evenings.