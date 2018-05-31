---
categories:
- Software
date: "2010-05-19T12:38:57Z"
tags:
- registry
- Software
title: Enable Windows RDP by registry
url: /software/enable-windows-rdp-by-registry/
---

A short info how to enable the windows RDP (Remote Desktop) directly in the registry.

Open up the registry editor an go to this path:

{{< highlight registry >}}
HKLM\SYSTEM\CurrentControlSet\Control\Terminal Server
{{< /highlight >}}

There you will find fDenyTSConnection with the value 1. Change this to 0.

{{< highlight registry >}}
fDenyTSConnection   ->  0
{{< /highlight >}}
