---
categories:
- Software
date: "2007-12-30T19:21:18Z"
tags:
- .htaccess
- permalink
- wordpress
title: WordPress 2.3 no working mod_rewrite
url: /software/wordpress-23-no-working-mod_rewrite/
---

I wanted just set up my new blog and use a permalink structure like this:

{{< highlight text >}}
/%category%/%postname%/
{{< /highlight >}}

The strange thing was that it want work. mod_rewrite is enabled from my hoster, other sites work with it without any problems. If I used a structure with the "index.php" in it, it worked without any problem. I googled a lot and read very much of the docu. Most of them only say, that the mod_rewrite, followsymlinks, and such things have to be enabled. But this is all how it should be! So where is the problem?

I don't really know it. All the docs says, that the new wordpress does not need an special .htaccess file for this kind of stuff. Or perhaps I always have over read it? I don't know. After a while I decided to put on a .htaccess which looks like this:

{{< highlight text >}}
<IfModule mod_rewrite.c>
RewriteEngine On
RewriteBase /
RewriteCond %{REQUEST_FILENAME} !-f
RewriteCond %{REQUEST_FILENAME} !-d
RewriteRule . /index.php [L]
</IfModule>
{{< /highlight >}}

After I did it, it WORKED. I hope I will not get any other problems with this little code, but till know I am happy with it. It simply works 😉
