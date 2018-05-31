---
categories:
- Linux
- Software
date: "2011-02-04T20:14:22Z"
tags:
- Software
title: 'Quick Tip: Remove forced subtitle from mkv'
url: /linux/quick-tip-remove-forced-subtitle-from-mkv/
---

Do you have ever created an mkv (perhaps with the great tool makemkv) and after playing it, you discovered that the subtitle is set on by default?

<!--more-->

With the nice tool mkvpropedit you can simply change this. You can find this tool in the great [MKVToolnix](http://www.bunkus.org/videotools/mkvtoolnix/) package which is avaiable for linux, Mac OsX and even Windows.

{{< highlight bash >}}
mkvpropedit file.mkv --edit track:s1 --set flag-default=0
{{< /highlight >}}
