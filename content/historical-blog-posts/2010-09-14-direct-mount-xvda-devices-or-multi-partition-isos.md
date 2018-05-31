---
categories:
- Linux
date: "2010-09-14T09:54:02Z"
tags:
- Linux
- Software
- xen
title: Direct mount xvda devices (or multi-partition isos)
url: /linux/direct-mount-xvda-devices-or-multi-partition-isos/
---

Sometimes you will get in the need to directly mount an xvda device which is often used, if you (for example) install a debian virtual system in xen. Then this block device consists out of several partitions, which can not directly be used. But of course you can access the data of it, without the need of booting the guest os (domU).

This is the same if you get an iso or any other type block devices which uses multiple partion slices.

<!--more-->

First we have to find out, at which position the slice (which we want to mount) start. For this we use the fdisk command which will give us all information we need. You do all this directly on the dom0, you dont have to boot the domU in any way!

{{< highlight bash >}}
xen ~ # fdisk -ul /dev/vg/server02
Disk /dev/vg/server02: 3221 MB, 3221225472 bytes
255 heads, 63 sectors/track, 391 cylinders, total 6291456 sectors
Units = sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disk identifier: 0x00090c14

 Device Boot      Start         End      Blocks   Id  System
/dev/vg/server02   *        2048     5894143     2946048   83  Linux
Partition 1 does not end on cylinder boundary.
/dev/vg/server02         5896190     6289407      196609    5  Extended
Partition 2 does not end on cylinder boundary.
/dev/vg/server02         5896192     6289407      196608   82  Linux swap / Solaris
{{< /highlight >}}

The important things are:

-   Sector size   ->  512

-   Start of the partition slice   ->  2048

Now fire up an calculator and multiply these number to get the correct offset:

512 * 2048 = **1048576**

With this value you can already **mount** the partition.

{{< highlight bash >}}
mount -o offset=1048576 /dev/vg/server02 /mnt/
{{< /highlight >}}

That was easy or what do you think?
