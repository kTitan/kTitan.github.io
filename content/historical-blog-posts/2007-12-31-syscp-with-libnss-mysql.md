---
categories:
- Gentoo
- Linux
- Software
date: "2007-12-31T16:41:39Z"
tags:
- Gentoo
- Linux
- Software
- syscp
title: syscp with libnss-mysql
url: /linux/syscp-with-libnss-mysql/
---

After installing a new rootserver with syscp, I decided to also install libnss-mysql support on the system. The advantage is, that it is easy to see which file belongs to which user. I hate to only see the uids and gids 😉

Because I use gentoo on the server, I emerged libnss-mysql. If you use an other distribution, you have to install it with your package manager if it is available. I used version 1.5 of it.

Now it was a bit tricky to find the right config for syscp for it. After a long search and many tries now it works good. Here are my configs:

<!--more-->

/etc/libnss-mysql-root.cfg:

{{< highlight text >}}
> username syscp
> password SYSCPPASSWORD
{{< /highlight >}}

/etc/libnss-mysql.cfg

{{< highlight text >}}
> getpwnam SELECT username,'x',uid,gid,username,homedir,shell \
> FROM ftp_users \
> WHERE username='%1$s' \
> LIMIT 1
> getpwuid SELECT username,'x',uid,gid,username,homedir,shell \
> FROM ftp_users \
> WHERE uid='%1$u' \
> LIMIT 1
> getpwent SELECT username,'x',uid,gid,username,homedir,shell \
> FROM ftp_users
> getspnam SELECT username,password,'12345','0','99999','7',","," \
> FROM ftp_users \
> WHERE username='%1$s' \
> LIMIT 1
> getspent SELECT username,password,'12345','0','99999','7',","," \
> FROM ftp_users
> getgrnam SELECT groupname,",gid \
> FROM ftp_groups \
> WHERE groupname='%1$s' \
> LIMIT 1
> getgrgid SELECT groupname,",gid \
> FROM ftp_groups \
> WHERE gid='%1$u' \
> LIMIT 1
> getgrent SELECT groupname,",gid \
> FROM ftp_groups
> memsbygid SELECT username \
> FROM ftp_users \
> WHERE gid='%1$u'
> gidsbymem SELECT gid \
> FROM ftp_users \
> WHERE username='%1$s'
>
> host localhost
> database syscp
> username syscp
> password SYSCPPASSWORD
> #socket /var/lib/mysql/mysql.sock
> #port 3306
> timeout 3
> compress 0
{{< /highlight >}}

Now it would be good to also use this ;). So you have to change /etc/nsswitch.conf like this:

{{< highlight text >}}
> passwd: compat mysql
> shadow: compat mysql
> group: compat mysql
{{< /highlight >}}

If you use the nscd don't forget to restart it!

And that was it already 😉
