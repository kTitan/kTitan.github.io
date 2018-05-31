---
categories:
- Software
date: "2010-01-26T10:47:29Z"
tags:
- php
- Software
title: 'Fix propel-gen error: Error reading project file build-propel.xml'
url: /software/fix-propel-gen-error-error-reading-project-file-build-propel-xml/
---

I had just installed propel-gen and phing with the pear method onto a new system. But after running the propel-gen I only get this error:

{{< highlight bash >}}

$ propel-gen $PWD

Buildfile: /usr/lib/php/data/propel_generator/pear-build.xml
[resolvepath] Resolved /devel/build/propel
propel-project-builder > projdircheckExists:
propel-project-builder > projdircheck:
propel-project-builder > configure:
[echo] Loading project-specific props from /devel/build/propel/build.properties
[property] Loading /devel/build/propel/build.properties
propel-project-builder > main:
[phing] Calling Buildfile '/devel/build/propel/build-propel.xml' with target 'main'
[phing] Error reading project file [wrapped: Unable to open /devel/build/propel/build-propel.xml for reading: ]
BUILD FINISHED

Total time: 0.1085 seconds
{{< /highlight >}}

My Installed software versions:

{{< highlight bash >}}
propel-gen -> 1.4.1
phing      -> 2.4
{{< /highlight >}}

And exactly this was the problem. It seems that the phing version 2.4 breaks some stuff. Because of this I have installed the old version, and now it works perfect.

{{< highlight bash >}}
$ pear uninstall -n phing/phing
$ pear install phing/phing-2.3.3
{{< /highlight >}}
