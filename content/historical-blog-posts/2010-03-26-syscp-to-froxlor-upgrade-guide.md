---
categories:
- Software
date: "2010-03-26T14:38:11Z"
tags:
- froxlor
- Linux
- Software
- syscp
title: Syscp to Froxlor Upgrade Guide
url: /software/syscp-to-froxlor-upgrade-guide/
---

In this Howto I will do an upgrade from syscp 1.4.2.1 to the fork froxlor in the current revision of 0.9.3. I hope to cover all fall sticks. But overall the upgrade is very painless and easy. Thanks a lot to guys of froxlor!

I do this as always on a gentoo host. Its your choice to use the good ebuild to install froxlor or to download it by hand. Here I will cover the manual steps.

First start with the basic stuff (download, uncompress, ...)

<!--more-->

{{< highlight bash >}}
cd /tmp
wget -q http://files.froxlor.org/releases/froxlor-0.9.3.tar.gz
wget -q http://files.froxlor.org/releases/froxlor-0.9.3.tar.gz.md5
md5sum -c froxlor-0.9.3.tar.gz.md5
tar xfz froxlor-0.9.3.tar.gz -C /var/www
{{< /highlight >}}

Now froxlor is installed to /var/www/froxlor and we only have to correct the permission. I asume that you have an syscp user already created in the syscp installation. Because of this the ownership can differ (also if you use mod_fcgid), so please look in your syscp installation. I try to copy the ownership with this command. If it fails do it by yourself.

{{< highlight bash >}}
chown $(ls -al /var/www/syscp/index.php | awk '{print $3":"$4}') /var/www/froxlor
{{< /highlight >}}

The good thing is that we only have to copy the user data file over, because it has not changed.

{{< highlight bash >}}
cp -p /var/www/syscp/lib/userdata.inc.php /var/www/froxlor/lib/
{{< /highlight >}}

Now it would a good time to disable the syscp cronjobs and do a backup the database. (The databasename will not be changed by upgrading to froxlor)

{{< highlight bash >}}
rm /etc/cron.d/syscp
mysqldump -opt -p syscp > /tmp/mysqldump_syscp.sql
{{< /highlight >}}

Because of the new docroot we have to change the pathes in the vhost. I use apache and my vhost file is called 95_syscp-admin.conf

{{< highlight bash >}}
sed -i 's|/var/www/syscp|/var/www/froxlor|g' /etc/apache2/vhosts.d/95_syscp-admin.conf
/etc/init.d/apache2 reload
{{< /highlight >}}

Now you have to connect to your syscp/froxlor vhost, where you already should greeted with the nice froxlor logo. Please log in and let it do the needed database upgrades (done automatically). After that you can continue here.

Froxlor also changes the name of generated include file for bind. If you use it, you have to do this:

{{< highlight bash >}}
sed -i 's|syscp_bind.conf|froxlor_bind.conf|g' /etc/bind/named.conf
rm /etc/bind/syscp_bind.conf
{{< /highlight >}}

You will find the same thing for awstats. You will see a failure immediatly if forget to do this, at the first run of cron.

{{< highlight bash >}}
mv /etc/awstats/awstats.model.conf.syscp /etc/awstats/awstats.model.conf.froxlor
{{< /highlight >}}

Now we should move the aps things from syscp to froxlor.

{{< highlight bash >}}
mv /var/www/syscp/packages/* /var/www/froxlor/packages/
mv /var/www/syscp/temp/* /var/www/froxlor/temp/
{{< /highlight >}}

I find it saver to do the first froxlor cron run by myself, to check for generated failures.

{{< highlight bash >}}
/usr/lib/php5/bin/php -q /var/www/froxlor/scripts/froxlor_master_cronjob.php
{{< /highlight >}}

If everything was ok, you can now add the froxlor cron. The dos2unix line should not be needed anymore, because Dessa fixed the bug in the 0.9.4 release.

{{< highlight bash >}}
cp /var/www/froxlor/templates/misc/configfiles/gentoo/cron/etc_cron.d_froxlor /etc/cron.d/froxlor
dos2unix /etc/cron.d/froxlor
chmod +x /etc/cron.d/froxlor
{{< /highlight >}}

And that was it! Have fun with your new froxlor installation. If you have comments or more snares, please give me a info.

IMHO: I find it very good that the old syscp developers has started this fork, and has fixed many many many bugs already 🙂

**_Changelog of this guide_**

{{< highlight text >}}
0001 - added dos2unix for froxlor cron job (bug in froxlor v0.9.3)
0002 - fixed some pathes, which was mentioned by Dessa
0003 - added aps info
{{< /highlight >}}
