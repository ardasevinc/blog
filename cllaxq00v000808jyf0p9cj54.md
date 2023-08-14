---
title: "BTRFS Maintance Guide: Do's and Don'ts"
seoDescription: "BTRFS freezing, scrub, balance, how to do btrfs maintance."
datePublished: Mon Aug 14 2023 13:52:57 GMT+0000 (Coordinated Universal Time)
cuid: cllaxq00v000808jyf0p9cj54
slug: btrfs-maintance-guide
tags: linux

---

BTRFS is a modern filesystem that supports features like COW (Copy-on-Write) and instant snapshots. It is more performant and space efficient than ext4 and others. It's on par with ZFS.

There are a couple things you should do and **not do** after setting a btrfs filesystem.

# Do

## Check filesystem usage with btdu

Btdu is a disk usage profiling tool for btrfs. As you might know, regular disk profling tools and du does not report disk space correctly with btrfs. By using btdu you can see which files and directories occupy the most space.

You can install it by grabbing the binaries from [its github page](https://github.com/CyberShadow/btdu/).

## Balance

```bash
sudo btrfs balance start -v -dusage=85 /
```

## Scrub

```bash
sudo btrfs scrub start /
```

# Don't

## Enable qgroups

It's all good until your filesystem freezes the entire kernel.

Source: Myself. I've used qgroups on two computers with timeshift snapshots enabled. They started freezing. When the freeze happens, all processes simultaneously hang. You can't even reach them by network (ssh).

# Final Words

This article is a living documentation, it will be continually updated as I keep using btrfs and having problems.

# Sources

For scrub and balance:

[https://discussion.fedoraproject.org/t/21695/3](https://discussion.fedoraproject.org/t/21695/3)

Qgroups:

My own anectodal experience and this [https://unix.stackexchange.com/a/529665](https://unix.stackexchange.com/a/529665)

Always check **arch wiki**

[https://wiki.archlinux.org/title/Btrfs](https://wiki.archlinux.org/title/Btrfs)