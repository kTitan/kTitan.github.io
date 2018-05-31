---
categories:
- Software
date: "2010-07-31T18:58:46Z"
tags:
- cell phone
- iphone
- Software
title: iphone iTunes sync - fix repeatedly prompt for authorize
url: /software/iphone-itunes-sync-fix-repeatedly-prompt-for-authorize/
---

If you have the Problem that iTunes ask on every sync to authorize (activate) your computer again here is an easy way to fix this.

I had this problem today once again, and now I decide to post this solution again.

<!--more-->
-   Make sure that in your explorer the option is active, that you see hidden files and directories
-   Navigate to the folder C:\ProgramData\Apple Computer\iTunes
-   Inside this folder you will find another folder with the name "SC Info"
-   Delete it! Yes simply delete it.
-   After you open iTunes once again, it will configure some things and ask once more (the last time!) for the activation/authorizing

And that was all. Till now it has always fixed my problem. Hopefully it will also work for you.
