---
date: 2022-02-20T20:05:31
type: status
tags:
  - macos
  - hardware
  - software
---

Very interesting thread by Hector Martin, where he goes into more detail about the performance of Apple's NVMe drivers, explains how they work and what challenges he is facing under [Asahi Linux](https://asahilinux.org/).

From the looks of it, under macOS, you can either have fast write speeds or data integrity when it comes to NVMe storage:

> As it turns out, macOS cheats. On Linux, fsync() will both flush writes to the drive, and ask it to flush its write cache to stable storage.
> 
> So, effectively, Apple's drive is faster than all the others without cache flushes, but it is more than 3 times slower than a lowly SATA SSD at flushing its cache. Even if all you wrote is a couple of sectors. You pay a huge flush penalty if you do *any* writes.
>
> [...]
> 
> macOS doesn't even seem to try to proactively issue syncs; you can write a file on macOS, fsync() it, wait 5 seconds, issue a hard reboot (e.g. via USB-PD command), and the data is gone. That's pretty bad.
>
> [...]
> 
> Not flushing means we cannot guarantee ordering of writes, which means you could end up with actual data corruption in e.g. a database, not just data loss. There's no good way around this other than doing full flushes.
>
> [...]

It is a very [long thread](https://twitter.com/marcan42/status/1494213855387734019), but its worth the read.

{{< tweet 1494213855387734019 >}}
