---
layout: post
title:  "Adventures with ZFS "
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

