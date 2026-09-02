---
title: S3 is now a file system
date: 2026-09-02T15:27:42
link: https://www.lastweekinaws.com/blog/s3-is-not-a-filesystem-but-now-theres-one-in-front-of-it/
domains: [lastweekinaws.com]
url: /links/lastweekinaws.com/20260902152742/
tags: [aws, s3]
---

Corey Quinn on the design of the new „S3 filesystem“:

> They didn’t just bolt a POSIX layer on top of S3 and call it a day. That’s been tried, badly. That’s what s3fs-fuse was. That’s what goofys was. That’s what Amazon’s own Mountpoint for Amazon S3 (motto: “you know it’s good because we put it on GitHub”) was. Every single one of those was the engineering equivalent of duct-taping a saddle onto a fish and calling it a horse.
> 
> Andy Warfield’s team went a different direction: instead of forcing files and objects to behave identically (which makes everyone miserable, as anyone who’s tried will confirm over drinks), they built a system where each works the way it’s supposed to, with automatic syncing between them. Your authoritative data stays in your S3 bucket. The filesystem maintains a view of your objects and translates filesystem operations into efficient S3 requests. Writes go through the filesystem and sync back to S3.
> 
> S3 still isn’t a filesystem. But your S3 data can now be used with a filesystem. That distinction matters, because the pricing tells a very specific story: what they built is less “S3 learned to be a filesystem” and more “EFS, but backstopped by S3.”
