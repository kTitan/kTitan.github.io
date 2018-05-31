---
categories:
- Linux
date: "2010-09-14T13:02:48Z"
tags:
- Linux
- Software
- xen
title: Fix pygrub booting of debian squeeze
url: /linux/fix-pygrub-booting-of-debian-squeeze/
---

Debian Squeeze is now using grub2 as the default bootmanager. Because of this pygrub has some difficulties to boot the domU after installing it. Here are the things i found out, if you have more remarks, drop me a comment please.

<!--more-->

First off all, because of the new grub2 you have to use at least **xen-tools** in the version **3.4.3**. The developers has first added the support to 4.x, but then they have made a back-port and released this officially in 3.4.3.

Ok now the new grub gets detected correctly by pygrub, but I still got an error message like this:

{{< highlight bash >}}
xen ~# xm create server02
Error code: Using class 'grub.GrubConf.Grub2ConfigFile' to parse  /boot/grub/grub.cfg
Error parameters: WARNING:root:Unknown directive load_video, Traceback  (most recent call last):, File "/usr/bin/pygrub", line 746, in ?,  raise RuntimeError, "Unable to find partition containing kernel",  RuntimeError: Unable to find partition containing kernel,
{{< /highlight >}}

The problem is an argument which is used in the grub.conf file. We have to change it a little bit. For this we have to mount the boot/root partition of the installed guest domU. If you don't know how you can do this, you can find the information [here](/linux/direct-mount-xvda-devices-or-multi-partition-isos/).

-   Open the grub.cfg file (boot/grub/grub.cfg) in your favorite editor.

-   Change msdos infos to a normal grub entry

{{< highlight bash >}}
hd0,msdos1 -> hd0,0
{{< /highlight >}}

-   Do this for all entries.

-   Keep in mind that debian perhaps update this file
