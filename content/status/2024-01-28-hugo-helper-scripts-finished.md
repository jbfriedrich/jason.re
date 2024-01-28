---
title: Hugo helper scripts finished
date: 2024-01-28T03:48:03
type: status
tags: [blogging, en]
---

The Python n00b in me is very happy right now. It took me ages, but version 1.0 of my two scripts that will help me blogging comfortably with Hugo are finally ready. They are not perfect, nor "finished" – and probably a bit rough around the edges. But I think it is a good first version – especially as I am not a developer at all.

These scripts now allow me to publish posts and status messages to my blog either directly via Telegram chat, or via Markdown files in a certain Webdav directory (abiding by a very simple format). Non-Markdown files get uploaded to S3 while the Markdown files get committed to my blog repository over at Github (including auto-generated Frontmatter).

I need to clean up the working directory and then publish it to repository.
