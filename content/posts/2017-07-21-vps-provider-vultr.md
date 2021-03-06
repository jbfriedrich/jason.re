---
title: VPS Provider VULTR
date: 2017-07-21T09:36:16.000Z
feature_image: https://images.unsplash.com/photo-1518432031352-d6fc5c10da5a?ixlib=rb-0.3.5&q=80&fm=jpg&crop=entropy&cs=tinysrgb&w=1080&fit=max&ixid=eyJhcHBfaWQiOjExNzczfQ&s=2ac2a0ba9c4b41180fa2038665684948
tags:
  - hosting
  - tech
  - en
---

For the reasons of diversity and high availability I was looking for an alternative to [DigitalOcean](https://digitalocean.com). Not that I was dissatisfied with their service, but it is always good to try new services and to spread your services between several providers.

People on the IRC channel and posts on social media mentioned [VULTR](http://www.vultr.com/?ref=7149844). Their service is similar to DigitalOcean’s. They offer quick deployment of Virtual Private Servers (VPS) in 15 locations worldwide, hosted on SSD-only storage (with optional block storage). You can either choose out of a variety of operating systems or upload an ISO and install a custom OS yourself.

{{< img src="https://rmbr.eu/file/dstore/17/7/Screen-Shot-2017-07-21-at-09.06.17_sojwtj-1024x540.png" >}}

Other than DigitalOcean, they also provide dedicated VPS instances in the United States and Japan. Also their price scheme slightly differs. Their $5 instances provide 1GB virtual memory, 1 vCPU, 25 GB SSD storage and 1TB bandwidth — twice as much memory and 5 GB more storage than the matching Droplet at DigitalOcean. They also offer an even smaller instance for $2.50 per month, which includes 512 MB virtual memory, 1 vCPU, 20 GB SSD storage and 500 GB bandwidth. Enough for personal usage in my opinion.

I already deployed a few test instances and will keep a small 512 MB instance, mainly used as miscellaneous test and development VPS.
