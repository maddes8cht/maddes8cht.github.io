---
layout: post
title:  "Adventures with ZFS "
Excerpt: I have a ZFS pool that was originally equipped with 4 disks of 3 TB each. After I had replaced these successively with 4 TB disks, I had expected to be able to use the increased capacity - the existing documentation on ZFS suggests exactly that.
---

I have a ZFS pool that was originally equipped with 4 disks of 3 TB each.
After I had replaced these successively with 4 TB disks, I had expected to be able to use the increased capacity - the existing documentation on ZFS suggests exactly that.

But unfortunately it did not work for me.
I get the following output from the command line:

```
zpool status
  pool: ZFS-Pool
 state: ONLINE
  scan: scrub repaired 0 in 0 days 13:12:33 with 0 errors on Tue Jul 19 05:37:43                                     2022
config:

        NAME        STATE     READ WRITE CKSUM
        ZFS-Pool    ONLINE       0     0     0
          raidz1-0  ONLINE       0     0     0
            ada1    ONLINE       0     0     0
            ada0    ONLINE       0     0     0
            ada3    ONLINE       0     0     0
            ada2    ONLINE       0     0     0
```

```
zfs list
NAME       USED  AVAIL  REFER  MOUNTPOINT
ZFS-Pool  5.67T  1.98T  5.54T  /mnt/ZFS-Pool

```

```
zpool list -v
NAME         SIZE  ALLOC   FREE  CKPOINT  EXPANDSZ   FRAG    CAP  DEDUP  HEALTH  ALTROOT
ZFS-Pool    10.9T  7.81T  3.07T        -     3.62T    25%    71%  1.00x  ONLINE  -
  raidz1    10.9T  7.81T  3.07T        -     3.62T    25%  71.8%
    ada1        -      -      -        -         -      -      -
    ada0        -      -      -        -         -      -      -
    ada3        -      -      -        -         -      -      -
    ada2        -      -      -        -         -      -      -

```
There is a discrepancy in the capacity that exists in the filesystem and what the ZPool could actually hold.
It took me a long time to get a closer look at the meaning of the column 'EXPANDSZ': This is the size to which the existing device can be expanded.

The usage is
```
zpool online [-e] <pool> <device> ...
```

so for my pool

```
zpool online -e ZFS-Pool ada0
zpool online -e ZFS-Pool ada1
zpool online -e ZFS-Pool ada2
zpool online -e ZFS-Pool ada3
```
for all disks. And lo and behold, now it worked:

```
 zfs list
NAME       USED  AVAIL  REFER  MOUNTPOINT
ZFS-Pool  5.68T  4.52T  5.55T  /mnt/ZFS-Pool
```

```
zpool list -v
NAME         SIZE  ALLOC   FREE  CKPOINT  EXPANDSZ   FRAG    CAP  DEDUP  HEALTH  ALTROOT
ZFS-Pool    14.5T  7.81T  6.69T        -         -    19%    53%  1.00x  ONLINE  -
  raidz1    14.5T  7.81T  6.69T        -         -    19%  53.9%
    ada1        -      -      -        -         -      -      -
    ada0        -      -      -        -         -      -      -
    ada3        -      -      -        -         -      -      -
    ada2        -      -      -        -         -      -      -

```
