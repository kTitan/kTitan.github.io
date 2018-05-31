---
categories:
- Software
date: "2010-02-04T13:17:59Z"
tags:
- cell phone
- iphone
- itunes
- recover
- Software
title: iphone iTunes sync - recover your Library Persistent ID
url: /software/iphone-itunes-sync-recover-your-library-persistent-id/
---

Useful for example, if you...

-   have formatted your pc without backup of your iTunes folder
-   want to sync your iPhone to an second pc
-   don´t have jailbreak on your iPhone

Follow this easy steps and you will have your Library ID again, and that even if you don't have jailbreak on your phone!

<!--more-->

1. Connect your iPhone to your PC with USB and start iTunes

2. Your phone should not appear in your iTunes. Right-click your device and select "Backup" (yes this will work without deleting your phone contents)

3. After the backup is done, navigate in your explorer/finder to:

Windows:   %appdata%\apple computer\mobilesync\backup\<unique string>\

OS X:           $HOME/Library/Application Support/MobileSync/Backup/<unique string>/

-> Windows: simply copy+paste the above path into the explorer

-> OS X:       $HOME is your Home directory. Then click through the folders

-> Both:      "unique string" is random string that iTunes creates. there should only be one directory. If there are more, simply use that one with the latest date string

4. In the folder you will find an Info.plist, that contains the necessary data. But not in an easy readable format. Because of this you can use this tool, to decode it.

***I do not longer provide this tool, because nobody needs it anymore. If you still need it please drop me a line.***

That was already all you have to do. If you don't know what to do with the id, I will write another how-to later. But for this you can already find many resources via google.

One limit has this thing: The Option for encrypting your iTunes Backup must be turned off!

If it does NOT work:

-   Get somehow in contact with me

-   Send me (or upload it somewhere) the Info.plist file. I will of course delete it, after I found the failure
