---
title: 'How To Fix The Web: Obscure Back-End Techniques And Terminal Secrets'
slug: how-to-fix-the-web-obscure-back-end-techniques-and-terminal-secrets
image: null
date: 2013-07-23T11:35:39.000Z
author: paul-tero
description: >-
  Imagine that you wake up one morning, reach groggily for your laptop and fire
  it up. You’ve just finished developing a brand new website and last night you
  were proudly clicking through the product list. The browser window is still
  open, the Widget 3000 is still sparkling in its AJAXy newness.
categories:
  - Coding
  - Techniques
  - Backend
---
Imagine that you wake up one morning, reach groggily for your laptop and fire it up. You’ve just finished developing a brand new website and last night you were proudly clicking through the product list. The browser window is still open, the Widget 3000 is still sparkling in its AJAXy newness. You grin like a new parent and expectantly click on “More details”. And nothing happens. You click again, still nothing. You press <code>Refresh</code> and get that annoying swirling icon and then the page goes blank. Help! The Internet is gone!

This chapter starts with the worst case scenario and works inwards, <strong>exploring the infrastructure of the Internet and the make-up of a Web server</strong>, imparting lots of little tips and commands along the way, opening up a new perspective on how websites can stop working — and be fixed.</p>

## <span class="rh">Further Reading</span> on SmashingMag: [Link](https://www.smashingmagazine.com/2010/12/what-to-do-when-your-website-goes-down/#further-reading-on-smashingmag)

*   [<span class="headline">How to find out why your website stopped working</span>](https://www.smashingmagazine.com/2013/07/how-to-find-out-why-your-website-stopped-working/)
*   [9 Steps To A Happy Relationship With Your Hosting Provider](https://www.smashingmagazine.com/2009/03/9-steps-to-a-happy-relationship-with-your-hosting-provider/)
*   [Effective Maintenance Pages: Examples and Best Practices](https://www.smashingmagazine.com/2009/06/effective-maintenance-pages-examples-and-best-practices/)

## The End Of The World

It is unlikely that civilization has collapsed overnight, especially if you are light sleeper. You can verify this with a battery-powered radio. An apocalypse would certainly make the news and perhaps qualify for a full-blown government warning. All stations should be reporting it, assuming there are any left; it would be really, really bad news if not.

{{% feature-panel %}}

In the US, many broadcasters participate in the Emergency Alert System, which theoretically allows the President to address the nation within 10 minutes, though it might be <a href="https://www.computerworld.com/s/article/9236758/Emergency_Alert_System_devices_vulnerable_to_hacker_attacks_researchers_say">vulnerable to hackers</a>. France uses air raid sirens for its Signal National d’Alerte2 and Japan’s <a href="https://www.terradaily.com/reports/Japan_Launches_Alert_System_For_Tsunamis_And_Missiles_999.html">J-Alert uses loudspeakers</a>. All are part of the United Nation’s International Early Warning Program. This is important, especially now that the International Decade for Natural Disaster Reduction (the 1990s) is long over.

You should be able to ascertain pretty quickly if your website woes are related to this. If not, move on to the next section.</p>

## Infrastructure

The Internet depends on electricity. Your hosting company probably has an uninterruptible power supply (UPS) which will take over instantly in the event of power failure. It can provide <a href="https://powercontinuity.co.uk/help/faqs/ups-and-generators-how-long-can-they-run-for">power to your Web server</a> for a few minutes, long enough to have a diesel generator ready to take over. The major networking equipment connecting your Web server to the Internet is probably protected with UPSes and generators as well. And your laptop should survive for a few more hours if fully charged.

Your wireless router, however, will cease to function. It is the weakest link. You can get around it by checking the Internet via your smartphone, which should work as long as your nearest tower has backup power, and there is a route to the Internet through other working towers. It might be very slow though, especially if everyone in your neighborhood has also had the same idea. If your website is still gone, then the problem is a bit more personal.</p>

## Networking

Power outages aren’t the only things which upset broadband routers. They have many inventive ways of failing, as does all the other networking equipment between you and your website, and all the copper and fiber-optic cable in between.

To explore networking issues, you’ll need to run some commands. Much of this information is also available through various menus, but the command line gives you more data more quickly. On Mac OS X, go to Applications → Utilities and run Terminal. In Ubuntu Linux, the terminal is under Applications → Accessories. In Windows, go to Start → All Programs → Accessories and choose Command Prompt.</p>

### Your IP Address

Every computer connected to the Internet has a numerical IP (Internet Protocol) address. To find out yours, run the command ifconfig on Mac and Linux and <code>ipconfig /all</code> on Windows. The result will look something like this:

<pre><code class="language-javascript">$ ifconfig
eth0      Link encap:Ethernet  HWaddr 00:10:dc:75:d9:5b
          inet addr:192.168.0.11  Bcast:192.168.0.255  Mask:255.255.255.0
          inet6 addr: fe80::210:dcff:fe75:d95b/64 Scope:Link
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1...
</code></pre>

<pre><code class="language-javascript">lo        Link encap:Local Loopback
          inet addr:127.0.0.1  Mask:255.0.0.0
          inet6 addr: ::1/128 Scope:Host
          UP LOOPBACK RUNNING  MTU:16436  Metric:1...
</code></pre>

This says that the computer (Linux in this case) has two network interfaces. The <code>eth0</code> is the one which communicates with the Internet via a cable. If this computer had wireless there would also be an <code>eth1</code> or <code>wlan0</code> interface. The loopback interface lo is used as a shortcut for communicating with itself. Each interface has an IP address on the local network. The important line here is <code>inet addr:192.168.0.11</code>.

This gives the computer’s IP address. If you have a cable attached and wireless turned on, you may have two active interfaces and two IP addresses, but it’s usually just the one. Macs tend to call these interfaces <code>en0</code> and <code>en1</code>. Windows is more verbose and uses sexy names like “Ethernet adapter Local Area Connection”.</p>

### DHCP

<strong>How does your computer know its IP address?</strong> Especially on a home or wireless network, you do not need to enter this information yourself. When your computer first connects to your home network, it sends out a request to every other device on the network, something like: “Can someone please give me an IP address?”

Your broadband router should dutifully respond and assign your computer an IP address. As you probably know, routers are the devices that hold the Internet together. Unlike laptops and desktops, routers have more than one network interface, more than one cable (or wireless point) attached to them and so more than one IP address. In your home or office, the router is the little box which provides your connection to the Internet via your broadband service.

The method used to assign an IP address is Dynamic Host Configuration Protocol (DHCP). If there is no IP address when you run <code>ifconfig</code> or <code>ipconfig</code>, you can force your computer to retrieve new DHCP settings. On Windows, run <code>ipconfig /release</code> followed by <code>ipconfig /renew</code>. On a Mac, run <code>sudo ipconfig set en0 DHCP</code>, and on Linux use <code>sudo dhclient eth0</code>. On Mac and Linux, the actual command is prefaced by sudo which forces you to put in the root password for the computer. You must also specify which interface to renew, usually <code>eth0</code> on Linux and <code>en0</code> for Mac.

If this was successful, then voilà! You’re a tiny bit closer to being back on the Internet. If not, check your broadband router. It may be off, disconnected or broken, or it may just need resetting.</p>

### Default Gateway

You know your broadband router was alive at some point in the recent past because it gave you an IP address. But that could have been up to three days ago: is it still there now?

Every computer on the Internet also has a default gateway. This is basically the IP address of the piece of networking equipment at the other end of your network cable or wireless connection. <strong>It is your computer’s gateway to the Internet.</strong> Every time you request anything from the Internet, it goes via this gateway. To find our your default gateway, run <code>netstat -nr</code> on Mac and Linux, and <code>route print</code> (or <code>ipconfig</code> again) on Windows. You will get something a bit like:

<pre><code class="language-javascript">Destination     Gateway         Genmask         Flags Metric Ref    Use Iface
192.168.0.0     0.0.0.0         255.255.255.0   U     0      0        0 eth0
0.0.0.0         192.168.0.1     0.0.0.0         UG    100    0        0 eth0
</code></pre>

In the Destination column above, the 0.0.0.0 (or the word “default”) means anywhere and the G in the Flags column stands for “Gateway”. The default gateway of this computer is therefore 192.168.0.1. For people at home or in a small office this is probably the internal IP address of the broadband router.

You can use the ping command to see if it is up and available. Type <code>ping 192.168.0.1</code>.

<pre><code class="language-javascript">$ ping 192.168.0.1
PING 192.168.0.1 (192.168.0.1) 56(84) bytes of data.
64 bytes from 192.168.0.1: icmp_seq=1 ttl=64 time=1.31 ms
64 bytes from 192.168.0.1: icmp_seq=2 ttl=64 time=0.561 ms
64 bytes from 192.168.0.1: icmp_seq=3 ttl=64 time=12.6 ms
</code></pre>

The “64 bytes from 192.168.0.1” represents a successful reply. If you get a reply, then your broadband router is reachable. If not, then check it again. On Mac and Linux the replies will go on forever until you press Control + C. On Windows, it will quit after the fourth ping.</p>

### Beyond the Router

To go beyond your router, you will need the <code>traceroute</code> command on Mac and Linux, and <code>tracert</code> on Windows. This command traces a route through the Internet, reporting each networking device (router) it comes across. IP addresses are formed of four numbers from 0 to 255. Pick an IP address out of a hat and try it:

<pre><code class="language-javascript">$ traceroute -q 1 -n 1.2.3.4
traceroute to 1.2.3.4 (1.2.3.4), 30 hops max, 60 byte packets
 1  *
 2  80.3.65.217  9.163 ms
 3  213.105.159.157  11.158 ms
 4  213.105.159.190  11.215 ms
...
13  72.14.236.149  98.484 ms
14  209.85.252.47  104.071 ms
15  *
16  *...
</code></pre>

The <code>-q 1</code> option on Mac and Linux tells the command to try each router only once. The <code>-n</code> tells it not to bother looking up the human-readable name for each router, which makes the command much slower. This option is <code>-d</code> on Windows, so use <code>tracert -d 1.2.3.4</code>.

Each step above is known as a hop in networking jargon. The first hop is the broadband router. It is probably configured not to provide any information about itself, so <code>traceroute</code> just shows an asterisk. The second hop takes it outside the local network to the other side of the broadband router.

At each subsequent hop sits another router, probably with many network interfaces and many IP addresses. Each router has a routing table like the one above. Its table contains rules like: if the destination starts with 0 to 91, then send the packet down interface <code>eth1</code> (the Use <code>Iface</code> column); if it starts with 92 to 128, use <code>eth2</code>.

This example goes 14 hops before reaching a dead end, either because the IP address is blocked or not in use.

<strong>That is about as far as numbers alone can take us.</strong> Hopefully you’ve established that civilization is still going at least a couple networking hops beyond your front door. You’ve also learned how to use the useful networking commands <code>ifconfig</code>, <code>ping</code> and <code>traceroute</code>. To explore further, you’ll need DNS.</p>

## The Domain Name System

Smashing Magazine could have gone with https://80.72.139.101 as its main website address rather than https://www.smashingmagazine.com. It would have had two advantages: it would have used less space on business cards; and it would still have worked when DNS was down. However, Smashing’s marketing people may have objected, and their customer base would have been limited to people with extremely good memories.

The domain name system <strong>makes the Internet more human-friendly</strong> by translating between domain names like www.smashingmagazine.com and IP addresses like 80.72.139.101. DNS is a big hierarchical distributed database. You are probably aware that there is no single computer which knows all the translations and which everybody else consults. Rather, it is a huge network of computers each of which know a few translations, and know who else to ask if they don’t.</p>

### Your Local DNS Server

Every computer has a local DNS server. It is one of the crucial bits of information your broadband router provides via DHCP: your IP address; your default gateway’s IP address; and your local DNS server’s IP address.

When you type a website address into your browser, your computer first asks its local DNS server to translate it into an IP address. To find out your DNS server, run the command <code>cat /etc/resolv.conf</code> on Mac and Linux, or <code>ipconfig /all</code> on Windows. On Mac and Linux, the cat command displays a file, and the file <code>/etc/resolv.conf</code> contains your domain name servers. The file looks like:

<pre><code class="language-javascript">$ cat /etc/resolv.conf
nameserver 194.168.4.100
nameserver 194.168.8.100
</code></pre>

### Nslookup

To diagnose DNS problems, first check that your local DNS server is alive with <code>ping</code>. If it is, then you can use the <code>nslookup</code> command to see if it’s responding correctly. <code>nslookup</code> stands for name server lookup and is used like this:

<pre><code class="language-javascript">$ nslookup www.smashingmagazine.com
Server:		194.168.4.100
Address:	194.168.4.100#53
Non-authoritative answer:
Name:		www.smashingmagazine.com
Address:	80.72.139.101
</code></pre>

This command tells you the DNS server used (194.168.4.100) and the IP address you are looking for (80.72.139.101). If nslookup didn’t respond, then your Internet woes lie with your local DNS server. If you are at home or in a small office, your DNS server is probably provided by your broadband company.

They generally provide two or more of them, so it’s unlikely that they will all fail. If you happen to know the IP address of a different name server, you could query that instead (<code>nslookup www.smashingmagazine.com 194.168.8.100</code>), but it may well refuse to talk to a stranger. You’ll probably need to complain to your broadband company about the problem instead.</p>

### Free Advertising

Have you ever typed in a website address incorrectly and come up with a branded page from your broadband provider? Instead of admitting “I don’t know”, your local name server is sneakily replying with an alternative IP address of its choice, promoting the broadband company it is owned by. It’s nice to see that the marketing people are into DNS.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/44c9d27f-e97e-428e-9f93-19cf9b3760ca/virgin-redirect.png" alt="Virgin Redirect" /><br>
<em>Broadband company intercepting a non-existent website.</em>

### A Full Journey

Having confirmed that your local DNS server is working, you can tentatively try to establish human-friendly contact with the Internet using <code>traceroute</code> with a domain name instead of an IP address, and leaving out the <code>-n</code> option. This will report a readable name for each router.

<pre><code class="language-javascript">$ traceroute -q 1 www.smashingmagazine.com
traceroute to www.smashingmagazine.com (80.72.139.101), 30 hops max, 60 byte packets
 1  *
 2  brig-core-2b-ae6-725.network.virginmedia.net (80.3.65.177)  10.542 ms
 3  popl-bb-1b-ae14-0.network.virginmedia.net (213.105.159.157)  13.934 ms
 4  popl-bb-1c-ae1-0.network.virginmedia.net (213.105.159.190)  14.454 ms
 5  nrth-bb-1c-ae7-0.network.virginmedia.net (62.253.174.137)  15.982 ms
 6  nrth-tmr-1-ae1-0.network.virginmedia.net (213.105.159.30)  16.215 ms
 7  fran-ic-1-as0-0.network.virginmedia.net (62.253.185.81)  36.090 ms
 8  FFMGW4.arcor-ip.net (80.81.193.117)  39.064 ms
 9  92.79.213.133 (92.79.213.133)  47.404 ms
10  92.79.200.190 (92.79.200.190)  45.385 ms
11  kar-145-254-15-178.arcor-ip.net (145.254.15.178)  40.421 ms
12  145.253.159.106 (145.253.159.106)  46.436 ms
13  1-3-frr02.continum.net (80.72.130.170)  49.321 ms
14  1-6-frr04.continum.net (80.72.130.158)  47.194 ms
15  www.smashingmagazine.com (80.72.139.101)  48.081 ms
</code></pre>

This reveals much more about the journey packets of data take. The first few hops in any traceroute are probably owned by the local broadband company, Virgin Media in this case. If the traceroute stopped here, then it would be an issue for them resolve. You could phone them for more information.

Once the traceroute leaves your broadband provider, it enters a no man’s land of big inscrutable networking devices. In this case they are owned by Arcor, a subsidiary of Vodafone. If the traceroute fails here, it may represent a fairly major networking problem and there’s not much you can do.

Eventually, it will reach the hosting company for the website in question (Continum.net in this case). If it fails there, then the fault may lie with your hosting company. Or it may simply be that the traceroute is blocked by a firewall. Or that your website has moved.</p>

### Moving Websites

It’s unlikely that your website has moved to a different server without you knowing, especially as you were just working on it last night, but you can double-check this.

<strong>Every DNS server keeps a cache of every domain name it has been asked for.</strong> This saves clogging up the Internet with requests for things that rarely change. The downside is that if someone changes the IP address for a domain like www.smashingmagazine.com, it can take 24 to 48 hours for all the caches to clear so that everyone in the world knows the new IP address.

To ascertain that you have the latest information, you first need to find out the local name server for the domain name you are querying. To do this, give <code>nslookup</code> the option <code>-type=ns</code>, like this on Mac, Linux and Windows:

<pre><code class="language-javascript">$ nslookup -type=ns www.smashingmagazine.com
Server:		194.168.4.100
Address:	194.168.4.100#53
Authoritative answers can be found from:
smashingmagazine.com
	origin = a.regfish-ns.net
	mail addr = postmaster.regfish.com...
</code></pre>

The <code>origin</code> (or sometimes <code>primary name server</code>) is the local DNS server for www.smashingmagazine.com. You can use <code>nslookup</code> again to query this server directly:

<pre><code class="language-javascript">$ nslookup www.smashingmagazine.com a.regfish-ns.net
Server:        a.regfish-ns.net
Address:       79.140.49.11#53
Name:	       www.smashingmagazine.com
Address:       80.72.139.101
</code></pre>

Compare this to the <code>nslookup</code> on your local DNS server. It no longer says “non-authoritative”. This is now the authoritative reply. It’s the same IP address, so we know that www.smashingmagazine.com didn’t suddenly move last night.

On Mac and Linux, you can use the <code>dig command</code> to find out exactly how long your local DNS server has cached this translation for. It stands for domain information groper. Windows users will need to search for an online <code>dig</code> tool as Windows doesn’t natively support this command:

<pre><code class="language-javascript">$ dig www.smashingmagzine.com
...
;; ANSWER SECTION:
www.smashingmagzine.com. 246	IN	A	80.72.139.101...
</code></pre>

The 246 is the number of seconds before the local DNS server’s cache expires and it has to rediscover the IP address for www.smashingmagazine.com.</p>

### Your Broadband Router Revisited

Now that DNS is working, you can find out what the world thinks of you. You have already discovered your computer’s own IP address above. But that may not be the one that it uses on the Internet. If it starts with 192.168 or 10, then it is definitely not a public address. Those IP address ranges signify local IP addresses for use within your internal network only.

When your computer sends a request to the Internet, it first goes to your default gateway (your broadband router), which also has a local internal IP address such as 192.168.0.1. But your router has another public IP address as well. Your router wraps up your request and resends it from this public IP address instead.

Therefore, your broadband router’s public IP address is basically your public IP address. This is how the rest of the Internet sees you as you browse. This is the IP address that will show up in log files in any of the websites you visit. Consequently, anybody else using the same broadband router will have the same public IP address as you. Your router handles all of this using a process called network address translation, making sure requests and information go out and come back to the right local IP address.

You can find out your broadband router’s public IP address by visiting a website like whatismyipaddress.com. Alternatively, you can run the command <code>curl ipinfo.io/ip</code> on Mac or Linux, or <code>wget -O- -q ipinfo.io/ip</code> on Linux. Both <code>curl</code> and <code>wget</code> retrieve a Web page (https://ipinfo.io/ip) from the Internet. The <code>-O-</code> option (that’s a letter O, not zero) tells <code>wget</code> to output the result to the screen (signified by a single hyphen) rather than save it to a file, and <code>-q</code> tells it to do it quietly. <code>curl</code> automatically outputs to the screen. To use <code>curl</code> on Windows you have to download and install it first. All these methods go outside your local network and look back. There is no way to find out your router’s public IP address from the inside. The output is quite simple:

<pre><code class="language-javascript">$ curl ipinfo.io/ip
85.106.118.199
</code></pre>

### Where Are They?

Websites like whatismyipaddress.com and ipinfo.io do more than just tell you your public IP address. They also provide geolocation services. It is interesting to take the IP addresses from the <code>traceroute</code> above and copy and paste them in. Geolocation guesses at the physical location of the router, and can also tell you who owns the IP address. The address 62.253.185.81 above is in southern England but the next one crosses the Channel to 80.81.193.117 in Frankfurt, Germany. This type of geolocation relies on databases of IP address ownership.

In fact, there are websites which can map this all out for you, such as <a href="https://en.dnstools.ch/visual-traceroute.html">DNStools.ch</a> and <a href="https://www.yougetsignal.com/">YouGetSignal</a>. The starting points for these traceroutes will be the Web server hosting the tool, rather than your own computer. Below is an example from a website in Los Angeles to the BBC website in London.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f17edabe-b247-4267-b659-cce75cf20e1a/visual-traceroute-crop.png" alt="Visual Traceroute" /><br>
<em> Visual traceroute from Los Angeles to London covering 7,904 miles in 4.8 seconds.</em>

## Connecting To Your Server

So, civilization and its Internet are both up and running. What’s gone wrong?
Your website lives on a computer somewhere out there, probably in a big air-conditioned room full of other computers, with multiple fire doors and an awful lot of colorful cabling. This computer is colloquially known as a Web server.

Imagine for a moment that your Web server is the nation of France. If you want to send a large item of furniture to somewhere in France, it will be wrapped up tight on a container ship and sent off across the sea. It will arrive in one of France’s major ports, maybe Marseille or Bordeaux or Le Havre. It doesn’t really matter to you which port it goes through, but it does matter to the shipping company. Computers are similar, except they are a bit smaller and have 65,535 ports.

On computers, some ports are assigned specific functions. On a Web server, port 80 receives and replies to Web browsing requests. Ports 25 and 110 deal with email. A typical Web request could involve port 50133 on your computer (the sending port is often chosen randomly) sending a request to port 80 at 80.72.139.101, something like “Hey you, send me the Web page /index.html”.</p>

### Telnet and Netcat

The <code>telnet</code> command allows you to mimic a container ship and connect to a specific port on a server. Windows does not have <code>telnet</code> by default, but you can enable it on Windows 7 by going to Start → Control Panel → Programs → Turn Windows features on or off → Telnet Client.

Since we’re dealing with a website problem, and since the Web server is almost always on port 80, try telnetting to port 80:

<pre><code class="language-javascript">$ telnet www.smashingmagazine.com 80
Trying 80.72.139.101...
telnet: Unable to connect to remote host: Connection refused
</code></pre>

Mac and Linux support an alternative command: <code>netcat</code>. It is more specifically suited for networking tasks and supports additional features like proxies. This chapter will focus on <code>telnet</code>, however, as it also works on Windows. Add <code>-v</code> to <code>netcat</code> to make it verbosely tell you what it’s doing.

<pre><code class="language-javascript">$ netcat -v www.smashingmagazine.com 80
netcat: connect to www.smashingmagazine.com port 80 (tcp) failed: Connection refused
</code></pre>

Uh oh.

Except, not really. I faked the issue above. Smashing Magazine wasn’t really down. But I will use www.smashingmagazine.com as an example domain throughout this chapter. Suspend your disbelief and pretend that Smashing has moved into the Widget 3000 market and has sequentially fallen subject to just about every networking and website problem imaginable, and subsequently overcome them.</p>

### Control Panel

Whenever your Web server receives data on port 80, it sends it to a piece of software for processing. Confusingly, that software is also called a Web server. By far the most common type of Web server software is Apache. According to W3Techs in June 2013, <a href="https://w3techs.com/technologies/overview/web_server/all">it had a market share of 65.2%</a>. Microsoft’s Internet Information Server (IIS) is second with 15.7%, just in front of nginx at 14.3%.

Web server software shouldn’t ever stop working. But if it does you can, hopefully, just restart it again. The quickest way to do this is using a control panel provided by your server. Windows servers (<a href="https://w3techs.com/technologies/overview/operating_system/all">34.3% market share in June 2013</a>) are often managed by Remote Desktop or VNC which allow you to take control of the server’s screen, keyboard and mouse, and change settings directly on the server.

The rest of this chapter, however, will focus on Linux and UNIX servers (65.7%), which are usually managed via a Web interface such as Plesk, CPanel or Webmin. These management tools are really just websites, but running on a different port. Plesk, for example, usually runs on port 8443, CPanel on 2082 or 2083 and Webmin on 10000.

Dig deep into your email folders and look for the URL, username and password for your control panel. Log in and find the screen which allows you to restart your Web server software. In Plesk, look for “Services management” (in Server or Tools &amp; Settings) and press the Play button next to “Web Server (Apache)”.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bad0f9d4-1267-41bf-993f-1bb29b09134e/plesk.png" alt="Plesk" /><br>
<em> Restarting a Web server with Plesk.</em>

### SSH

If port 80 is down, there’s a good chance that the control panel won’t be available either. You will need to log in to the server and issue commands directly. For this there is Secure Shell (SSH). SSH is like the text-only version of Remote Desktop. It allows you to open a terminal window on the server. From a Linux or Mac desktop or laptop, use the command <code>ssh</code>. From a Windows computer, download and run PuTTY.

You’ll need the username and password for your server, contained in the same email as above. On a Linux server, <code>root</code> is the most powerful administrative user. For security reasons, the SSH user from your email will often be something less privileged like <code>admin</code>. When you run SSH, you have to provide the username as part of the command. It will ask you to accept a security fingerprint and enter a password:

<pre><code class="language-javascript">$ ssh root@www.smashingmagazine.com
The authenticity of host ‘www.smashingmagazine.com (80.72.139.101)’ can’t be established.
RSA key fingerprint is 00:5a:cf:51:83:46:0b:91:29:ef:2e:1d:c9:59:e9:ab.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added ‘www.smashingmagazine.com,80.72.139.101’ (RSA) to the list of known hosts.
root@www.smashingmagazine.com’s password: ...
</code></pre>

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/53213cf3-b418-4504-801f-616b28adeaa9/putty.png" alt="Putty" /><br>
<em>Using PuTTY for SSH from a Windows computer.</em>

If successful, you’ll end up with a welcome message and a terminal prompt:

<pre><code class="language-javascript">Linux dedivps-13236 2.6.10-091stab048.3 #1 SMP Fri Dec 7 17:06:14 GMT 2012 x86_64
Last login: Thu May  2 07:20:11 2013 from cpc1-brig18-2-0-cust123.3-3.cable.virginmedia.com
root@dedivps-13236:~#
</code></pre>

Note that this will only work on Linux or UNIX servers that have an SSH server which accepts connections, and the rare Windows servers that have opted to install it. For most other Windows servers, you’ll need Remote Desktop instead. If you can’t get at your server via a control panel or SSH, your options are very limited. There’s a slim chance that an overenthusiastic firewall is getting in the way, or that you’re experiencing a denial of service attack. Or else you’ll need to contact your hosting company and ask for help.</p>

### Firewalls

Firewalls are bits of hardware or software that filter incoming and outgoing data. These filters are applied according to the source and destination IP address and port. So, for example, a firewall should allow all requests going to the server’s port 80 or else nobody will be able to get to the website. But it may block all requests to port 8443 (Plesk), port 22 (SSH) or port 3389 (remote desktop) except from a few known and trusted IP addresses.

You can sort of tell if there’s a firewall in your way depending on how the connection fails. To test if SSH is being blocked, you can run the command <code>ssh</code> or use <code>telnet</code> as above to port 22:

<pre><code class="language-javascript">$ telnet www.smashingmagazine.com 22
Trying 80.72.139.101...
telnet: Unable to connect to remote host: Connection refused
</code></pre>

“Connection refused” means that your data reached the server but was probably refused entry for non-firewall reasons. For example, SSH may be turned off or running on a different port. The message “Connection timed out” or no message more strongly indicates a firewall block. If it does connect, press Control + ] to get to the <code>telnet&gt;</code> prompt and then type “quit” to quit.

So if you have a firewall (that email should tell you), you need to make sure that SSH is allowed and that your public IP address is in the list of trusted ones. Even if you know your IP address was in the list yesterday, it may have changed today, particularly if you have had broadband issues recently. The public IP addresses assigned to home routers can stay the same for months on end, and then suddenly change. How and why and when depends on your broadband company and your neighbors. The only way to avoid this is to pay extra for a static or fixed IP address.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/caff8fcb-d35f-4347-80f5-5b45e27b6ce1/firewall-trusted-ips.png" alt="Firewall" /><br>
<em> Many firewalls maintain a list of trusted IP addresses.</em>

### Denial Of Service

Imagine that the Widget 3000 suddenly goes viral. The Queen of England is filmed throwing one at the winner of X Factor and suddenly everybody in the world wants to own one. You might think “Fantastic!” But unless your server infrastructure is prepared to go from 100 visits an hour to 100 million, you probably won’t actually sell very many. All those visitors accessing your website at once will grind the network and your server to a halt. The first few thousand visitors may receive half a Web page, the rest will be staring at blank browsers.

And when you try to <code>telnet</code> to your server as above, it will also sit there waiting — no refusal but no entry either. This is roughly what happens in a distributed denial of service (DDoS) attack. All those hackers who have spent the last 15 years finding holes in Internet Explorer were not working in vain. They have managed to plant Trojan horses on millions of computers worldwide. When they issue the command, all those computers suddenly try to send data to and request data from your Web server, overwhelming it and making it unreachable.

Unless you are running a bank or a bomb factory, or have managed to make some clever and determined enemies, it is unlikely to happen to you. Let’s assume <code>telnet</code> has instead connected successfully.</p>

## Checking Your Server

Now you’re in business. You’ve got a terminal window open on your server waiting for your every command. From now on, all the commands are being issued on your Linux server, not your laptop.</p>

### Listening to Port 80

The first step is to figure out which software should have responded when you tried to <code>telnet</code> to port 80. For that, you can use the netstat command to display all the networking information about your server. Add <code>-tlpn</code> to the command to make it show only <u>T</u>CP connections that it is <u>l</u>istening for, along with the <u>n</u>umeric port and the <u>p</u>rogram they belong to.

<pre><code class="language-javascript">$ netstat -tlnp
Active Internet connections (only servers)
Proto Recv-Q Send-Q Local Address        Foreign Address      State       PID/Program name
tcp        0      0 127.0.0.1:53         0.0.0.0:*            LISTEN      4290/named
tcp        0      0 127.0.0.1:5432       0.0.0.0:*            LISTEN      3507/postmaster
tcp        0      0 0.0.0.0:3306         0.0.0.0:*            LISTEN      7117/mysqld...
</code></pre>

This shows only an abbreviated output. It normally shows all the ports which the server is listening to, and there can be between 10 and 100 of them. When running any command, you can whittle down its output using the <code>grep</code> command. <code>grep</code> filters the output and only shows lines containing a word or phrase you have specified. The vertical bar | makes a pipe, piping the output of one command (<code>netstat</code>) into the input of another (<code>grep</code>). Try this instead:

<pre><code class="language-javascript">netstat -tlpn | grep :80
tcp6       0      0 127.0.0.1:8005       :::*        LISTEN      22885/java
</code></pre>

This runs <code>netstat</code> and shows only results containing <code>:80</code>. This server has a <code>java</code> process listening to port 8005 but no Web server running.</p>

### Which Web Server

When a Linux server starts up it looks in the directory <code>/etc/init.d</code> and runs the scripts there to launch its software. On other UNIX flavors like BSD this might be <code>/etc/rc.d</code> or <code>/etc/rc.d/init.d</code>. This is similar to the Startup menu folder in Windows.

You can see what your server starts using the <code>ls</code> command which <u>l</u>i<u>s</u>ts the files in a directory. The -l shows a long format with permissions, owners, size and date created.

<pre><code class="language-javascript">$ ls -l /etc/init.d
total 368
-rwxr-xr-x 1 root root  7621 Sep 13  2012 apache2
-rwxr-xr-x 1 root root  3281 Oct  5  2012 bind9
-rwxr-xr-x 1 root root  2444 Jan  1  2011 bootlogd
-rwxr-xr-x 1 root root  5364 Nov  1  2011 courier-imap
-rwxr-xr-x 1 root root  3753 Dec 19  2010 cron...
</code></pre>

,p&gt;You are looking for a Web server software package such as <code>apache2</code>, <code>httpd</code> (the old name for Apache) or <code>nginx</code>. You can use <code>grep</code> again with the <code>-e</code> option which tells it to use a regular expression. In regular expressions, the vertical bar means “or” so this displays any files containing “apache” or “http” or “nginx”. The bar must be escaped with a back slash:

<pre><code class="language-javascript">$ ls -l /etc/init.d | grep -e “apache|http|nginx”
-rwxr-xr-x 1 root root  7621 Sep 13  2012 apache2
</code></pre>

### Restarting the Web Server Software

The files in /etc/init.d are called shell scripts. The commands you’ve been using on Mac and Linux up till now form part of a C-type language which also includes setting variables and running loops. As in JavaScript, the semicolon at the end of each line is optional, but if you use it, you can cram several commands onto a single line. Here is a simple <code>for</code> loop on the command line:

<pre><code class="language-javascript">$ for i in 1 2 3; do echo Line $i; done
Line 1
Line 2
Line 3
</code></pre>

To see a complex shell script, take a look at some of the startup scripts in <code>/etc/init.d</code>. Use the <code>less</code> command to view a file. Press space to view the next page or <code>q</code> to quit from <code>less</code>.

<pre><code class="language-javascript">$ less /etc/init.d/apache2
#!/bin/sh
set -e
SCRIPTNAME=”${0##*/}”...
</code></pre>

The reason we’re really here, though, is to restart the Web server software. If you logged into <code>ssh</code> as the administrative user <code>root</code>, you can run the restart command directly. In this case, you will have been typing your commands after a # instead of a $. If not, you’ll need to prefix it with the <code>sudo</code> command, which says <u>do</u> some command as the <u>s</u>uper <u>u</u>ser. You’ll need the root password to hand for sudo. To tell the Web server software to start, run:

<pre><code class="language-javascript">$ sudo /etc/init.d/apache2 start
Password:
Starting apache2...
</code></pre>

Hopefully this will fail with a useful error message. Hopefully, because then you will know why it crashed in the first place, and you can plug the error message into Google to find out how to fix it.

If it was unlucky enough to work, then your Web server is now running. All the scripts in /etc/init.d run as background processes, or daemons in UNIX parlance. This means that you can start them and they will stay running even after you exit from ssh, turn off you computer and go to the beach. This is unlike commands like <code>traceroute</code> and <code>ls</code> which do their thing and finish.

You can run <code>netstat</code> again to double-check the Web server is now running. Notice the d at the end of of <code>apached</code>. It stands for daemon.

<pre><code class="language-javascript">netstat -tlpn | grep :80
tcp        0      0 :::80            :::*             LISTEN      18201/apached
tcp6       0      0 127.0.0.1:8005   :::*             LISTEN      22885/java
</code></pre>

### Web Server Error Logs

If it failed to start and didn’t give a friendly error message, the next place to look is the error logs. These are usually in the <code>/var/log</code> directory named after the software. Run <code>ls /var/log</code> to double check. For example, Apache’s logs are in <code>/var/log/apache2</code>.

<pre><code class="language-javascript">$ ls -l /var/log/apache2/*log*
-rw-r----- 1 root adm  1944899 May  5 09:59 /var/log/nginx/access.log
-rw-r----- 1 root adm   538152 May  4 02:40 /var/log/nginx/access.log.2.gz
-rw-r----- 1 root adm    28647 May  5 08:18 /var/log/nginx/error.log
-rw-r----- 1 root adm     5701 May  4 02:35 /var/log/nginx/error.log.2.gz
</code></pre>

This shows that Apache has an access log and an error log. Both logs are zipped up around 02:30 each morning. The next command first <u>c</u>hanges into the <code>/var/log/apache2</code> <u>d</u>irectory with the <code>cd</code> command, and then uses <code>tail</code> to view the last few entries in a log file.

<pre><code class="language-javascript">$ cd /var/log/apache2; tail error.log
</code></pre>

To look at a gzipped log file, use the <code>zcat</code> command to output it and pipe through <code>tail</code>. The <code>-20</code> shows the last 20 lines.

<pre><code class="language-javascript">$ zcat error.log.2.gz | tail -20
</code></pre>

Or better yet, just look for errors using grep. Use <code>zcat</code> with the <code>-f</code> option to display both normal and zipped log files. Then pipe the output through <code>grep</code> to search for the word “error” case <u>i</u>nsensitively:

<pre><code class="language-javascript">$ zcat -f error.log* | grep -i error
</code></pre>

This command may produce a lot of output. If a Matrix fan happens to walk past your computer right now, they’ll be impressed to see all that raw data whizzing by. It won’t help you much, though, so pipe it through <code>less</code>:

<pre><code class="language-javascript">$ zcat -f error.log* | grep -i error | less
</code></pre>

<code>less</code> is powerful. You can press arrow keys or <code>j</code> to go down, <code>k</code> to go up, <code>/something</code> to search for “something” and <code>h</code> to see a helpful list of all the commands. If you can narrow down the moment of failure of your Web server to a few hours, you can use less to navigate to that part of the log file.</p>

### System Logs

There are several other useful log files in <code>/var/log</code> such as syslog (the system logger) and dmesg (bootup messages). They all use a similar date format so if you can narrow down the time when you suspect something went wrong, you can search them all at once. This command changes to the <code>/var/log</code> directory and then outputs all the files using <code>zcat -f</code>. The <code>[234]</code> in <code>grep</code> is borrowed from regular expressions, and matches the numbers 2 or 3 or 4. So this will display any error messages in any of the logs that took place on 5 May between 02:00 and 04:00 in the morning:

<pre><code class="language-javascript">$ cd /var/log; zcat -f * | grep “May  5 0[234]:” | less
</code></pre>

### Out of Space

If your Web server software still won’t start, and the error remains elusive, there are a couple common problems you can explicitly check for. Your server could have run out of hard drive space. Use the command <code>df</code> to show <u>d</u>isk <u>f</u>ile usage. The <code>-h</code> shows things in human-friendly form (with M for megabyte and G for gigabyte instead of really big numbers):

<pre><code class="language-javascript">$ df -h
Filesystem           1M-blocks      Used Available Use% Mounted on
/dev/simfs               20.4G      9.8G     10.6G  49% /
tmpfs                     1.6G         0      1.6G   0% /lib/init/rw
tmpfs                     1.6G         0      1.6G   0% /dev/shm
</code></pre>

If that was a problem, then a quick solution is to find and delete really big files. The find command is very powerful. The <code>-size</code> option tells it to look for files of at least the given size, and the <code>-printf</code> option tells it to print the size (<code>%12s</code>, where the 12 directs the print area to be 12 characters wide to help line things up), last modification time (<code>%t</code>), directory (<code>%h</code>), file name (<code>%f</code>) and then a new line (<code>n</code>). To view all files over 10 megabytes try:

<pre><code class="language-javascript">$ find / -size +10M -printf “%12s %t %h/%fn”
   445631888 Mon Mar 18 13:38:07.0380913017 2013 /var/www/some-huge-file.zip
</code></pre>

To delete the file and free up space quickly:

<pre><code class="language-javascript">$ rm /var/www/some-huge-file.zip
</code></pre>

### Out of Memory

To check your server’s RAM usage, run the <code>free</code> command, again with <code>-m</code> to show in megabytes:

<pre><code class="language-javascript">$ free -m
             total       used       free     shared    buffers     cached
Mem:          3067       2673        393          0          0        819
-/+ buffers/cache:       1853       1213
Swap:            0          0          0
</code></pre>

This server has 3GB of total memory and 393MB free. This is fine as Linux likes to use a lot of its memory. It’s the <code>buffers/cache</code> line which you should focus on. If this is nearly all used, then your system may be struggling to cope.

To find out what is hogging all the memory, use the top command. It shows a real-time display of system CPU and memory usage. Unfortunately this will also run very slowly if your server is under strain, but it may tell you what’s causing the problem.

<pre><code class="language-javascript">$ top
  PID USER      PR  NI  VIRT  RES  SHR S %CPU %MEM    TIME+  COMMAND
22885 tomcat6   20   0 2061m 159m 2644 S    1  5.2 780:41.85 java
    1 root      20   0  8360  568  536 S    0  0.0   0:52.30 init
    2 root      20   0     0    0    0 S    0  0.0   0:00.00 kthreadd/10086
    3 root      20   0     0    0    0 S    0  0.0   0:00.00 khelper/10086
14579 root      20   0 40900 3124 1668 S    0  0.1   1:30.27 nginx...
</code></pre>

If something is being a memory hog, you can kill it. However, be sure you know what it is first. You may crash the server completely, or lock yourself out, or stop an important database amalgamation which your efficiency-unaware colleague started three days ago. To kill a process, press k and type in the number from the process ID (PID) column. It will ask for confirmation and then try to kill the process. If you are not root, it may say “Operation not permitted”, in which case you’ll need to run <code>sudo top</code> instead.

The PID is used to identify a piece of software running on a computer. Each instance of an application, program or software has a unique PID. If the process refuses to go away, you can press <code>q</code> to leave <code>top</code> and try the <code>kill</code> command instead. Give it the more extreme <code>-9</code> option. <code>top</code> sends the friendly signal 15 (termination). Signal 9 goes straight for the kill.

<pre><code class="language-javascript">$ sudo kill -9 22885
</code></pre>

Run <code>top</code> again. If some other similar process has taken over the memory-eating honors, then you have only killed a child process. You will need to find out the parent which spawned the misbehaving child in the first place, because killing the parent will also stop all the children. The ps command can be used to display information about a specific process. Normally it does not show the parent process ID, so you need to add the <code>-o</code> option and specify that the output should show the parent process <code>ID ppid</code> and the full command that started it:

<pre><code class="language-javascript">$ ps -o ppid,command 14579
 PPID COMMAND
 6950 nginx: worker process
</code></pre>

This nginx process is not the main one.

<pre><code class="language-javascript">$ ps -o ppid,command 6950
 PPID COMMAND
    1 nginx: master process /usr/sbin/nginx
</code></pre>

A very low parent PID means that this process is the daddy. Killing process 6950 on this server will kill the main <code>nginx</code> process and all its children.

There is an easier way to do this. You can search for processes using <code>pgrep</code> and kill them with <code>pkill</code>. The <code>-l</code> tells <code>pgrep</code> to <u>l</u>ist the process name as well. For example:

<pre><code class="language-javascript">$ pgrep -l nginx
6950  nginx
14579 nginx...
</code></pre>

And then go in for the kill with <code>sudo pkill nginx</code>. A further way to search for processes is using <code>ps</code> with the <code>aux</code> option as in <code>ps aux | grep nginx</code>. Easier, but you wouldn’t have learned about the wonder of <code>top</code>.</p>

### Speaking HTTP

At this stage, your Web server software is hopefully up and running. If it did crash, you’ve restarted it, found out the reason and taken steps to prevent it from happening again.

You can now double-check your Web server is up and running by telnetting to port 80 from your laptop again. This time it should say “Connected” and then wait for your request. Web servers understand HTTP (hypertext transfer protocol). After a connection is established type <code>GET / HTTP/1.1</code> to tell the server you would like to <code>GET</code> (as opposed to <code>POST</code>) the home page / and that you speak version 1.1 of the protocol.

Press Enter and then type the <code>Host:</code> followed by the host name. This line is only necessary on servers which host more than one website. HTTP does not know that you telnetted to www.smashingmagazine.com. As far as it is concerned, you telnetted to 80.72.139.101 and it needs to know which of its many websites you are interested in. Press Enter twice to make the request. You should get back a long stream of text and HTML:

<pre><code class="language-javascript">$ telnet www.smashingmagazine.com 80
Trying 80.72.139.101...
Connected to www.smashingmagazine.com.
Escape character is ‘^]’.
GET / HTTP/1.1
Host: www.smashingmagazine.com

HTTP/1.1 200 OK
Date: Thu, 09 May 2013 13:25:52 GMT
Content-Type: text/html; charset=UTF-8
Transfer-Encoding: chunked
Connection: keep-alive
X-Powered-By: PHP/5.2.17
Content-Length: 25023
Content-Type: text/html

&lt;html&gt;
&lt;head&gt;&lt;...
</code></pre>

The lines above are mostly HTTP headers. The <code>HTTP/1.1 200 OK</code> says that the server also speaks version 1.1 of HTTP and gives the successful HTTP response code 200. Other common responses are 500 for Internal Server Error and 404 for File Not Found. It then continues with the HTML. If the Connection header specified “keep-alive” then telnet will wait for your next request and you’ll need to type <code>Control + ]</code> and then “quit” to exit. If the Connection header said “close” then it will finish by itself and say “Connection closed by foreign host” at the bottom.

<em>Paul Tero's chapter has been reviewed by <a href="https://twitter.com/coderholic">Ben Dowling</a> and <a href="https://twitter.com/chikuyonok">Sergey Chikuyonok</a>.</em>

<em>Front-page image credits: <a href="https://www.flickr.com/photos/brostad/5841286379">Bernt Rostad</a>.</em>

<em>(og) (il) (vf) (ea) (cm)</em>

