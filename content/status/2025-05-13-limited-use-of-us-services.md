---
title: Limited use of US services
date: 2025-05-13T20:31:24
type: status
tags: [tech, usa, en]
---

Due to recent events, I decided to start limiting the use of US services for my IT needs. I am hosting with [Hetzner](https://www.hetzner.com/de/) forever, either using their Cloud offerings or a dedicated Root server. My email is hosted with [Fastmail](https://www.fastmail.com/), which is an Australian company. So it is not hosted in the US, but it still feels not optimal as they have a presence in the US as well. Fastmail's contenders in Germany are not that great though. [Mailbox.org](https://mailbox.org)'s webmail interface is horrible compared to Fastmail, and it seems there are some latency issues as well when using IMAP.

My [landing page](https://friedrich.uk) and my [blog](https://jason.re) are based on Hugo, which is a static site generator. So my hosting needs are not that complicated or elaborate. The content for both sites is stored on GitHub and the sites are automatically rebuild and redeployed on Cloudflare Pages if there is a change in the repository.

I liked Cloudflare's service because it was easy to maintain and fast – and GitHub had a lot of outages at the time. Things at GitHub have stabilized for some time now, and I do not like the fact that I have to use Cloudflare's nameservers for my domain. Since I have all my code hosted on GitHub anyway, I decided to ditch Cloudflare Pages and go back to GitHub Pages for now. The ultimate goal is to move all my code to a self-hosted Gitlab instance, but I am not ready for that just yet.

To be continued, I guess…
