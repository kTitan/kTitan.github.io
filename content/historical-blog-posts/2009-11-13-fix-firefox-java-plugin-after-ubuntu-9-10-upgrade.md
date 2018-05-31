---
categories:
- Linux
date: "2009-11-13T10:31:32Z"
tags:
- firefox
- java
- Linux
- ubuntu
title: Fix Firefox Java Plugin after Ubuntu 9.10 Upgrade
url: /linux/fix-firefox-java-plugin-after-ubuntu-9-10-upgrade/
---

I had the problem, that my java plugin for Firefox was no longer working after I had upgraded my Ubuntu from 9.04 to 9.10 (karmic). In the old version it was necessary to add some lines to the sources.list. In the new version of ubuntu this is no longer necessary to install java.

After I had found this out, I thought the solution could be easy: Simply reinstall it!

So first the uninstall:

<!--more-->

{{< highlight bash >}}
$ sudo apt-get remove  sun-java6-jre sun-java6-plugin
[sudo] password for user:
Reading package lists... Done
Building dependency tree
Reading state information... Done
The following packages were automatically installed and are no longer required:

java-common

Use 'apt-get autoremove' to remove them.
The following packages will be REMOVED:
sun-java6-bin sun-java6-fonts sun-java6-jre sun-java6-plugin
0 upgraded, 0 newly installed, 4 to remove and 0 not upgraded.
After this operation, 101MB disk space will be freed.

Do you want to continue [Y/n]?

(Reading database ... 132896 files and directories currently installed.)  
Removing sun-java6-plugin ...
Removing sun-java6-fonts ...
Updating fontconfig cache for /usr/share/fonts/truetype/ttf-lucida
No CIDSupplement specified for Batang-Bold, defaulting to 0.
No CIDSupplement specified for ZenHei, defaulting to 0.
No CIDSupplement specified for UMingCN, defaulting to 0.
No CIDSupplement specified for ZenHei-CNS, defaulting to 0.
No CIDSupplement specified for Dotum-Regular, defaulting to 0.
No CIDSupplement specified for Batang-Regular, defaulting to 0.
No CIDSupplement specified for Dotum-Bold, defaulting to 0.
Removing sun-java6-bin ...
Removing sun-java6-jre ...
Processing triggers for desktop-file-utils ...
Processing triggers for shared-mime-info ...
{{< /highlight >}}

And after that you can already install it again

{{< highlight bash >}}
$ sudo apt-get install  sun-java6-jre sun-java6-plugin sun-java6-fonts
Reading package lists... Done
Building dependency tree
Reading state information... Done
The following extra packages will be installed:
sun-java6-bin

The following NEW packages will be installed:
sun-java6-bin sun-java6-fonts sun-java6-jre sun-java6-plugin

0 upgraded, 4 newly installed, 0 to remove and 0 not upgraded.
Need to get 0B/35.5MB of archives.
After this operation, 101MB of additional disk space will be used.

Do you want to continue [Y/n]?

Preconfiguring packages ...  
Selecting previously deselected package sun-java6-jre.
(Reading database ... 131983 files and directories currently installed.)
Unpacking sun-java6-jre (from .../sun-java6-jre_6-15-1_all.deb) ...
sun-dlj-v1-1 license has already been accepted
Selecting previously deselected package sun-java6-bin.
Unpacking sun-java6-bin (from .../sun-java6-bin_6-15-1_i386.deb) ...
sun-dlj-v1-1 license has already been accepted
Selecting previously deselected package sun-java6-fonts.
Unpacking sun-java6-fonts (from .../sun-java6-fonts_6-15-1_all.deb) ...
Selecting previously deselected package sun-java6-plugin.
Unpacking sun-java6-plugin (from .../sun-java6-plugin_6-15-1_i386.deb) ...
Processing triggers for shared-mime-info ...
Processing triggers for desktop-file-utils ...
Setting up sun-java6-bin (6-15-1) ...
update-alternatives: using /usr/lib/jvm/java-6-sun/jre/bin/ControlPanel to provide /usr/bin/ControlPanel (ControlPanel) in auto mode.
update-alternatives: using /usr/lib/jvm/java-6-sun/jre/bin/java to provide /usr/bin/java (java) in auto mode.
update-alternatives: using /usr/lib/jvm/java-6-sun/jre/bin/java_vm to provide /usr/bin/java_vm (java_vm) in auto mode.
update-alternatives: using /usr/lib/jvm/java-6-sun/jre/bin/javaws to provide /usr/bin/javaws (javaws) in auto mode.
update-alternatives: using /usr/lib/jvm/java-6-sun/jre/bin/jcontrol to provide /usr/bin/jcontrol (jcontrol) in auto mode.
update-alternatives: using /usr/lib/jvm/java-6-sun/jre/bin/keytool to provide /usr/bin/keytool (keytool) in auto mode.
update-alternatives: using /usr/lib/jvm/java-6-sun/jre/bin/pack200 to provide /usr/bin/pack200 (pack200) in auto mode.
update-alternatives: using /usr/lib/jvm/java-6-sun/jre/bin/policytool to provide /usr/bin/policytool (policytool) in auto mode.
update-alternatives: using /usr/lib/jvm/java-6-sun/jre/bin/rmid to provide /usr/bin/rmid (rmid) in auto mode.
update-alternatives: using /usr/lib/jvm/java-6-sun/jre/bin/rmiregistry to provide /usr/bin/rmiregistry (rmiregistry) in auto mode.
update-alternatives: using /usr/lib/jvm/java-6-sun/jre/bin/unpack200 to provide /usr/bin/unpack200 (unpack200) in auto mode.
update-alternatives: using /usr/lib/jvm/java-6-sun/jre/bin/orbd to provide /usr/bin/orbd (orbd) in auto mode.
update-alternatives: using /usr/lib/jvm/java-6-sun/jre/bin/servertool to provide /usr/bin/servertool (servertool) in auto mode.
update-alternatives: using /usr/lib/jvm/java-6-sun/jre/bin/tnameserv to provide /usr/bin/tnameserv (tnameserv) in auto mode.
update-alternatives: using /usr/lib/jvm/java-6-sun/jre/lib/jexec to provide /usr/bin/jexec (jexec) in auto mode.
Setting up sun-java6-jre (6-15-1) ...
Setting up sun-java6-fonts (6-15-1) ...
Updating fontconfig cache for /usr/share/fonts/truetype/ttf-lucida
No CIDSupplement specified for Batang-Bold, defaulting to 0.
No CIDSupplement specified for ZenHei, defaulting to 0.
No CIDSupplement specified for UMingCN, defaulting to 0.
No CIDSupplement specified for ZenHei-CNS, defaulting to 0.
No CIDSupplement specified for Dotum-Regular, defaulting to 0.
No CIDSupplement specified for Batang-Regular, defaulting to 0.
No CIDSupplement specified for Dotum-Bold, defaulting to 0.
Setting up sun-java6-plugin (6-15-1) ...
{{< /highlight >}}

And after that it is working perfectly. 🙂
