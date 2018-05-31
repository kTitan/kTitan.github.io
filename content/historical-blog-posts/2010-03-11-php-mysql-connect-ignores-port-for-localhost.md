---
categories:
- Software
date: "2010-03-11T19:45:18Z"
tags:
- mysql
- php
title: Php mysql connect ignores port for localhost
url: /software/php-mysql-connect-ignores-port-for-localhost/
---

I just tried to connect with php to an other mysql server which runs on my localhost on an other port then the standard 3306. I used this syntax:

{{< highlight php >}}mysql_connect('localhost:3307', 'mysql_user', 'mysql_password');{{< /highlight >}}

But the damn php always connected to the default mysql server with port 3306.

After a lot of google searches I found the solution.

<!--more-->

If you are using _localhost_ as your mysql server, php always use the port 3306. It simply ignores this value.

Easy workaround, is that you use 127.0.0.1 with the new port.

{{< highlight php >}}mysql_connect('127.0.0.1:3307', 'mysql_user', 'mysql_password');{{< /highlight >}}

Btw: If sql safe-mode is turned on the server parameter is ignored. Ask your Hoster to change it, or to turn it off.
