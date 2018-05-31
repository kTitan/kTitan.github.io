---
categories:
- Linux
date: "2010-01-14T09:53:47Z"
tags:
- Linux
- xen
title: Using independent clocks in xen domU (ntp)
url: /linux/using-independent-clocks-in-xen-domu-ntp/
---

Normally the xen domU´s are using the same clock as the dom0. But I had the problem, that there was a timeshift of 20 minutes on one of my hosts. I did not find out the reason for this, so I decided to simply setup ntp also on this.

To make this work you have to tell the kernel of the virtual machine to use its on clock. With this command you set the parameter online.

{{< highlight bash >}}
echo 1 > /proc/sys/xen/independent_wallclock
{{< /highlight >}}

To make this also boot safe, you will have to add a sysctl code to your */etc/sysctl.conf*

{{< highlight bash >}}
*   Set independent wall clock time
xen.independent_wallclock=1
{{< /highlight >}}

After that you can already use your own clock. For example you can now setup openntp on it, which will not work otherwise.
