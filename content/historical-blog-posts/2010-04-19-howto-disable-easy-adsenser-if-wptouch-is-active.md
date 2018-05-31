---
categories:
- Software
date: "2010-04-19T09:35:55Z"
tags:
- php
- Software
- wordpress
title: Howto disable easy-adsenser if wptouch is active
url: /software/howto-disable-easy-adsenser-if-wptouch-is-active/
---

WpTouch is a great plugin, if you want to optimize your wordpress blog for mobile content. It also comes with an integrated adsense option for the mobile content.

This is of course much better then the normal google ads.

But now comes the problem: In my blogs i often use easy-adsenser as the adsense mangement software. But if this is active, and you also activate the adsense option in WpTouch you will see ALL ads in the mobile view (the one from WpTouch and the one(s) from easy-adsenser). This can also be perhaps against the terms of google, depending how you setup easy-adsenser.

I looked a bit around in the code and found an easy we how to solve this problem.

<!--more-->

All you have to do is editing this file:

wp-content/plugins/easy-adsenser/easy-adsenser.php

Then search for the function *ezAdSense_content* (around line 440). In the beginning of this function it is checked if the ads should be inserted or not. Here I added the check if WpTouch view is active or not. This is the new line:

{{< highlight php >}}
if (function_exists('bnc_wptouch_is_mobile') && bnc_wptouch_is_mobile()) return $content ;  
{{< /highlight >}}

After the modification it should look like this:

{{< highlight php >}}
if ($ezAdOptions['kill_tag'] && is_tag()) return $content ;
if ($ezAdOptions['kill_archive'] && is_archive()) return $content ;
if (!$ezAdOptions['allow_feeds'] && is_feed()) return $content ;
if (function_exists('bnc_wptouch_is_mobile') && bnc_wptouch_is_mobile()) return $content ;

$mc = $ezAdOptions['mc'] ;
$this->mced = false ;
{{< /highlight >}}

Perhaps clear now your cache, but that was already all. Check it!

Attached you will find a diff file for that. **But remember:** If you update you easy-adsenser plugin you have to do that again!

[disable_easy-adsenser_on_wptouch_mobileview.diff](/files/disable_easy-adsenser_on_wptouch_mobileview.diff)
