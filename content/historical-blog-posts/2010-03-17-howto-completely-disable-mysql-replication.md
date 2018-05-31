---
categories:
- Software
date: "2010-03-17T09:01:29Z"
tags:
- mysql
- Software
title: Howto really completely disable mysql replication
url: /software/howto-completely-disable-mysql-replication/
---

There are many possibilities how-to setup a mysql replication. Here you will find a hopefully completely How-to really disable it. This is very useful for example if you want to make your slave a primary (standalone) server.

Connect to the mysql shell:

{{< highlight bash >}}mysql -uroot -p{{< /highlight >}}

<!--more-->

Commands:

{{< highlight mysql >}}
STOP SLAVE;
RESET SLAVE;
change master to master_host=", master_user=", master_password=";
{{< /highlight >}}

And now some changes to your my.cnf

{{< highlight bash >}}vi /etc/mysql/my.cnf{{< /highlight >}}

{{< highlight bash >}}
*   Comment out every line starting with "master-"
*   add this to your mysqld section

skip-slave-start
{{< /highlight >}}

Now only a restart of your mysqld should be done.

{{< highlight bash >}}/etc/init.d/mysqld restart{{< /highlight >}}
