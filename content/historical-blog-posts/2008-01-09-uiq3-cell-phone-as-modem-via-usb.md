---
categories:
- Gentoo
- Linux
date: "2008-01-09T13:21:18Z"
tags:
- cell phone
- Gentoo
- Handy
- Hardware
- Linux
- modem
- ppp
- uiq3
- usb
title: UIQ3 cell phone as modem via usb
url: /linux/uiq3-cell-phone-as-modem-via-usb/
---

I got my new Sony Ericsson P1i a few weeks ago. Because I hate it to use Windows I wanted to get it working as an usb modem under linux. In my case again under gentoo 😉 My cell phone provider in Germany is Eplus. So if you use this with an other provider you will have to change some values of course. The cell phone itself has SymbianOS on it. The version its called UIQ3. The instructions should work for all QUI3 phones, as far as I know. I used very much sites to get this together, so I beg your pardon that I forgot which that all was.

So first check if you have the need kernel options enabled:

<!--more-->

{{< highlight text >}}
> Device Drivers -->
> USB support -->
> USB Modem (CDC ACM) support
>
> Device Drivers -->
> Network device support -->
> PPP (point-to-point protocol) support
> PPP support for async serial ports
{{< /highlight >}}


If you compiled the things as modules make sure to load them. (and perhaps to autload them via /etc/modules.autoload.d/kernel-2.6)

{{< highlight text >}}
> modprobe modprobe cdc-acm ppp_async
{{< /highlight >}}


Of course we need also a ppp dialing program. I choose the normal commandline pppd, but I think this also can be done via some grapical ppp guis. But I did not tested it.

{{< highlight text >}}
> emerge ppp
{{< /highlight >}}

There are now only 3 files need to be created. If you use a gui this will perhaps be done via that...

/etc/ppp/peers/3g

{{< highlight text >}}
> lcp-echo-failure 0
> lcp-echo-interval 0
> nodetach
> connect "/usr/sbin/chat -f /etc/ppp/peers/3g-chat-connect"
> disconnect "/usr/sbin/chat -f /etc/ppp/peers/3g-chat-disconnect"
> /dev/ttyACM1
> 115200
> crtscts
> local
> noipdefault
> ipcp-accept-local
> defaultroute
> usepeerdns
> novj
> nobsdcomp
> novjccomp
> nopcomp
> noaccomp
> noauth
> user "eplus"
> password empty
> mtu 1500
> mru 1500
{{< /highlight >}}


/etc/ppp/peers/3g-chat-connect

{{< highlight text >}}
> TIMEOUT 5
> ECHO ON
> ABORT '\nBUSY\r'
> ABORT '\nERROR\r'
> ABORT '\nNO ANSWER\r'
> ABORT '\nNO CARRIER\r'
> ABORT '\nNO DIALTONE\r'
> ABORT '\nRINGING\r\n\r\nRINGING\r'
> " \rAT
> TIMEOUT 12
> SAY "Press CTRL-C to close the connection at any stage!"
> SAY "\ndefining PDP context...\n"
> OK ATH
> OK ATE1
> OK 'AT+CGDCONT=1,"IP","internet.eplus.de"'
> OK ATD*99#
> TIMEOUT 22
> SAY "\nwaiting for connect...\n"
> CONNECT ""
> SAY "\nConnected."
> SAY "\nIf the following ppp negotiations fail,\n"
> SAY "try restarting the phone.\n"
{{< /highlight >}}

/etc/ppp/peers/3g-chat-disconnect

{{< highlight text >}}
> ABORT "BUSY"
> ABORT "ERROR"
> ABORT "NO DIALTONE"
> SAY "\nSending break to the modem\n"
> "" "\K"
> "" "+++ATH"
> SAY "\nPDP context detached\n"
{{< /highlight >}}

That was it! now you can easyly connect

{{< highlight bash >}}
> pppd call 3g
{{< /highlight >}}
