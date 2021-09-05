---
title: INWX DynDNS Service
date: 2019-08-04T22:27:48
feature_image: https://images.unsplash.com/photo-1544197150-b99a580bb7a8
tags:
  - networking
  - internet
  - en
---

I have not used [dynamic DNS](https://en.wikipedia.org/wiki/Dynamic_DNS) in a very, very long time. I think the last time was back at the end of the 90's or the beginning 00's. Most (if not all) of the services I used at the time do not exist anymore. I happily noticed that my DNS and domain provider offers a [DynDNS service](https://www.inwx.de/en/offer/dyndns). My new [EdgeRouter 4](https://www.ui.com/edgemax/edgerouter-4/) has a built-in DynDNS client, supporting multiple protocols. 

```
$ ssh jfriedrich@192.168.1.1                        
Welcome to EdgeOS

By logging in, accessing, or using the Ubiquiti product, you
acknowledge that you have read and understood the Ubiquiti
License Agreement (available in the Web UI at, by default,
http://192.168.1.1) and agree to be bound by its terms.

jfriedrich@192.168.1.1's password:
Linux er4 4.9.79-UBNT #1 SMP Wed Jun 5 15:53:11 UTC 2019 mips64
jfriedrich@er4:~$ configure
jfriedrich@er4# set service dns dynamic interface eth0 service dyndns host-name dyndnshostname.domain.tld
jfriedrich@er4# set service dns dynamic interface eth0 service dyndns login MyUserName
set service dns dynamic interface eth0 service dyndns password P4ssw0rd
jfriedrich@er4# set service dns dynamic interface eth0 service dyndns protocol dyndns2
jfriedrich@er4# set service dns dynamic interface eth0 service dyndns server dyndns.inwx.com
jfriedrich@er4# commit
jfriedrich@er4# save
Saving configuration to '/config/config.boot'...
Done
jfriedrich@er4# exit
exit
```

Easy Peasy Lemon Squeezy!
