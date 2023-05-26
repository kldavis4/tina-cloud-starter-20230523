---
title: A Comprehensive Guide To Firewalls
slug: introduction-to-firewalls
image: 'https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/38dfe8ea-7ee5-46ed-b227-036bd9cd984a/firewall-5001.png'
date: 2013-01-30T12:24:48.000Z
author: paul-tero
description: >-
  In the construction industry, a “firewall” is a specially-built wall designed
  to **stop a fire from spreading between sections** of a building. The term
  spread to other industries like car manufacturing, and in the late 1980s it
  made its way into computing.
categories:
  - Coding
  - Backend
  - Security
---
In the construction industry, a “firewall” is a specially-built wall designed to <strong>stop a fire from spreading between sections</strong> of a building. The term spread to other industries like car manufacturing, and in the late 1980s it made its way into computing. On one side of the wall is the seething electronic chaos of the Internet. On the other side is your powerful but vulnerable Web server.

These computer firewalls are actually more like fire doors because they have to let some stuff through. They <strong>monitor all the electronic traffic</strong> coming in and out of a network. They follow a strict set of rules to determine what is allowed and what is blocked.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [10 Ways To Beef Up Your Website’s Security](https://www.smashingmagazine.com/2010/06/10-ways-to-beef-up-your-websites-security/)
*   [Free SSL For Any WordPress Website](https://www.smashingmagazine.com/2016/06/free-ssl-for-any-wordpress-website/)
*   [The Current State Of Authentication: We Have A Password Problem](https://www.smashingmagazine.com/2016/06/the-current-state-of-authentication-we-have-a-password-problem/)
*   [Common Security Mistakes in Web Applications](https://www.smashingmagazine.com/2010/10/common-security-mistakes-in-web-applications/)

This article explains in more detail how they work, the different types of firewalls available, what they are good at and not so good at, and how to configure them to protect a typical Web server.

{{% feature-panel %}}

## Protocols And Ports

A computer is like a big housing complex. Every computer on the Internet has a numerical address, known as an IP address. At each address are two very large blocks of apartments. Each block contains 65,535 individual apartments. The vast majority of them are empty, but a few, especially the lower ones, have very communicative residents. All communication is by mail.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a827a6a7-8cb8-49c7-9f01-322477639cf2/flats1-300x250.jpg"><img title="A computer is like two big blocks of apartments." src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a827a6a7-8cb8-49c7-9f01-322477639cf2/flats1-300x250.jpg" alt="A computer is like two big blocks of apartments." width="546" height="485" /></a><br>
<em>A computer is like two big blocks of apartments. Ten points if you can identify these apartment buildings.</em>

The two blocks are called TCP and UDP. Residents of the TCP block only accept certified mail, and they are guaranteed to reply to you. Once you've started exchanging letters with someone in TCP, you can be sure they'll see the conversation through to the end. The UDP block is a bit shabbier. Its residents only reply if they can be bothered. They usually do, but there are no guarantees.

<strong>Each resident has a different job.</strong> For example, the family in apartment 80 of the TCP block handles website inquiries. You can write to them with a request like “send me the home page for <code>www.smashingmagazine.com</code>” and they will duly reply and send back the data.

The couple in UDP apartment 53 are responsible for <a href="https://en.wikipedia.org/wiki/Domain_Name_System">DNS</a>. They translate domain names into IP addresses. Sometimes letters get lost, but that's okay. The information they handle in UDP is not as critical. The sender can always ask again.

All addresses in the postal system therefore have three parts: computer <em>IP address</em>, block and apartment. So as an example: <code>80.72.139.101</code>, TCP, 80. In reality, the block is the <em>protocol</em>, and the apartment is the <em>port</em> number. TCP stands for <a href="https://en.wikipedia.org/wiki/Transmission_Control_Protocol">Transmission Control Protocol</a> and UDP is <a href="https://en.wikipedia.org/wiki/User_Datagram_Protocol">User Datagram Protocol</a>. Their main difference is that TCP creates and maintains a conversation (i.e. connection) between the two computers, whereas UDP does not. Therefore TCP is more reliable but slower.</p>

### Sender's Address

In the example above, the web-serving family at <code>80.72.139.101</code>, TCP, 80 are sitting around reading books, just waiting for letters. They never start their own conversations or connections. They are always on the receiving end.

But the sender also has an address. Whenever you browse for a Web page in your Web browser or on your smart phone, your computer assigns you an assistant in one of its apartments, generally one that is way up high in the building. A typical conversation between your Web browser and a Web server somewhere might look like this:

*   From `99.99.99.99`, TCP, 63454: “Dear `80.72.139.101`, TCP, 80, It has come to my attention that you handle enquiries relating to the website `www.smashingmagazine.com`. Can you please send me the `/books/` page? Yours truly, A Web Browser.”
*   From `80.72.139.101`, TCP 80: “Sure no problem. Here it is: `<!DOCTYPE html> <html>`…”
*   From `99.99.99.99`, TCP, 63454: “Thanks. That's all. Bye.”

Apartment numbers below 1024 are more secure than the higher numbers. They have CCTV, and they are reserved for privileged tasks like website and <a href="https://en.wikipedia.org/wiki/FTP">FTP</a> serving. The higher apartments are more ephemeral. People are moving in and out all the time. They are used for things like requesting Web pages and initiating FTP connections.</p>

### Danger

But not everyone is on the straight and narrow. Here is a sample conversation between a dodgy client living above a café and a trusting <a href="https://en.wikipedia.org/wiki/Secure_Shell">SSH</a> resident on a vulnerable server. SSH is a method for connecting to a remote computer and running commands on it. The SSH resident always lives in the TCP block, usually in apartment 22:

*   From `88.88.88.88`, TCP apartment 58123: “Dear SSH server, I want to establish a connection with you. I would like to login as the user called root.”
*   From `80.72.139.101`, TCP, 22: “Sure no problem, what's your password?”
*   From `88.88.88.88`: “smith”
*   From `80.72.139.101`: “That's incorrect. Try again.”
*   From `88.88.88.88`: “jones”
*   From `80.72.139.101`: “Still wrong. Try again.”
*   From `88.88.88.88`: “bloggs”
*   From `80.72.139.101`: “Great. Hi Mr. Root, long time, no see. What do you want to do today?”
*   From `88.88.88.88`: “I think I'll view the file `/etc/passwd`, the one with all the user names?”
*   From `80.72.139.101`: “Here's the information you requested… Anything else?”
*   From `88.88.88.88`: “Yes — show me all files containing the word 'credit card'”
*   From `80.72.139.101`: “Sorry. That took a while. But here you go:…”
*   From `88.88.88.88`: “Thanks, that's all, bye.”

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ddde6704-e66d-4baf-b980-b1709065d077/ssh-example2.png"><img title="The first part of the SSH conversation above: logging in as root, getting the password wrong twice, asking for a file." src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ddde6704-e66d-4baf-b980-b1709065d077/ssh-example2.png" alt="The first part of the SSH conversation above: logging in as root, getting the password wrong twice, asking for a file." width="546" height="411" /></a><br>
<em>The first part of the SSH conversation above: logging in as root, getting the password wrong twice, asking for a file.</em>

## Levels Of Protection

The server depicted above is vulnerable. Anybody can send a letter to <code>80.72.139.101</code>, TCP, 22. If they can guess the password correctly, then they have full access to the server and all its files. This section discusses four basic levels of protection which you can apply to a server to prevent this, and to only allow trusted people to communicate with your server.

Although SSH is just one of many services that can run on a server, it is a good one to start with because it offers the most control over the server. If a hacker breaks into your FTP or SMTP server, they can do damage, but not as much as with SSH.</p>

### Good Passwords

SSH does have its own built-in protection because it requires a user name and password. A first basic step in securing a server is to choose complicated hard-to-guess passwords.

Whenever the resident in apartment 22 receives a letter, he first asks for the correct password. If you can't get it right, then he won't help you. He's a trusting person though. You can usually have as many tries as you'd like. Every three tries, you might have to resend your initial opening letter, but he generally won't mind.</p>

### Refusing Connections

The SSH conversation above was partly faked. If you really try to SSH to <code>80.72.139.101</code> (the IP address of Smashing Magazine's Web server), you will get this:

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f95c07f8-c20e-4667-ad6f-f011949ada3d/ssh-denied1.png"><img title="SSH connection refused." src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f95c07f8-c20e-4667-ad6f-f011949ada3d/ssh-denied1.png" alt="SSH connection refused." width="546" height="173" /></a><br>
<em>SSH connection refused.</em>

This means that the resident in <code>80.72.139.101</code>, TCP, apartment 22, is receiving his mail, but is immediately sending it back. He has a piece of paper taped to the back of his door which lists all the people who he is allowed to correspond with. He checks the sender's address against the list. If you're not on it, he refuses to engage in any correspondence. But he does send a polite note back which says, “Sorry, connection refused.”

This kind of protection is provided by software like <a href="https://en.wikipedia.org/wiki/TCP_Wrapper">TCP Wrappers</a> on UNIX servers. The blocking is done at an application level using the files <code>/etc/hosts.deny</code> and <code>/etc/hosts.allow</code>.

With this type of blocking, it is still conceivable that a particularly cunning sender could convince the resident in apartment 22 to open a letter and read it. Also, it relies on the individual residents to take note of and obey the lists. Although the guy in apartment 22 in very conscientious, other residents may be less so.</p>

### Software Firewall

A software firewall is like a concierge who filters all the <strong>incoming</strong> mail before it is even distributed to the residents. He has a similar piece of paper on his desk. He checks the sender's address against the list. If your address isn't on the list, your letter goes straight in the bin. No follow-up or polite apology. Nothing. You wait around for a couple weeks and then give up. He also filters <strong>outgoing</strong> mail, consulting his list to see which residents are allowed to write to the outside world.

Technically it looks like this:

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/88ef1e5d-a71f-4312-953b-8d4faeb8d981/ssh-timed-out.png"><img title="SSH connection timed out either there is nobody home or there is a firewall in a the way." src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/88ef1e5d-a71f-4312-953b-8d4faeb8d981/ssh-timed-out.png" alt="SSH connection timed out either there is nobody home or there is a firewall in a the way." width="546" height="173" /></a><br>
<em>SSH connection timed out either there is nobody home or there is a firewall in a the way.</em>

This type of blocking is done at the operating system level. A software firewall makes sure the letter never even gets there. See this page for a nice explanation of the difference between TCP Wrappers and software firewalls.</p>

### Hardware Firewall

A hardware firewall is like having a well-trained security expert in your local post office. She has a similar list as the concierge, detailing who is allowed to send letters to whom. She might be protecting just your IP address, or she might be working for dozens of addresses at the same time, or maybe even the whole community. She scrutinizes every single bit of mail going into and out of your town. Anything she doesn't like, she chucks. As above, you'll just get a “connection timed out” message.

This is the ultimate in firewall security. The letters don't even make it to the front gate. No chance at all that he'll mistakenly pass on a letter to the resident in apartment 22.

Of course, you can implement all these levels of protection. And you can have multiple hardware firewalls. You could have one at your local post office, another at the bigger sorting office in the city and another that filters all mail coming into your county, state or country.

Note that in practice, a “hardware firewall” is just a computer which is wholly dedicated to being a firewall, and is physically separated from your Web server. The firewall itself is still a piece of software on that computer.</p>

### Stateless and Stateful Firewalls

The concierge and the security person filter incoming and outgoing mail. If they are new on the job, they are like <strong>stateless</strong> firewalls, i.e. <a href="https://en.wikipedia.org/wiki/Packet_filter#First_generation:_packet_filters">packet filters</a>. They treat all mail equally. When you send a letter to apartment 80, apartment 80 will send a letter back. That reply is checked against their lists. Your letter only gets through if mail from apartment 80 is allowed out.

After a while, they move up the pay scale and become <strong>stateful</strong> firewalls. They are trained to differentiate the outgoing mail between <strong>brand new</strong> outgoing letters and replies to previous letters. Consequently, their lists of rules can be a lot shorter. They can be told to deliver all letters that are part of an <strong>established</strong> correspondence, and throw away almost all new outgoing mail. So when you send a letter to apartment 80, the reply from apartment 80 is automatically allowed back through. But if on some lonely winter's evening, apartment 80 suddenly decides to start up its own letter writing campaign, it won't get through.

The next section looks at how the piece of paper with all the rules is formatted.</p>

## Firewall Rules

Whether you use a software or hardware firewall, you will hopefully get some sort of visual management tool. There are many firewalls available, each with its own way of doing things, but they generally stick to the same concepts. They mainly vary in their complexity. Some give you complete control but also require a lot of knowledge and effort. Others are simple but far less flexible.

This section introduces the terminology and shows two examples of firewall configuration interfaces.</p>

### Firewall Terminology

This is what the piece of paper on the concierge's desk might look like:

1.  Letters from any sender in any apartment to the TCP building, apartment 80 - deliver; replies to those letters from apartment 80 - deliver
2.  Letters from the address `99.99.99.99`, any apartment number, to the TCP building, apartment 22 - deliver; replies to those letters from apartment 22 - deliver
3.  Any other letters to or from the TCP building - throw away
4.  Any other letters to or from the UDP building - throw away

Whenever the concierge receives a new letter, he compares the sender's and recipient's addresses to each of these rules in order. When he finds a matching rule, he follows the instruction, which is to either deliver the letter or throw it away.

The overall effect is that anybody in the world can correspond with the Web server in apartment 80, but only the trustworthy people living at <code>99.99.99.99</code> can write to the SSH server in apartment 22. All other attempted communication is thrown away. This is how that would translate to a real software firewall like <a href="https://en.wikipedia.org/wiki/Iptables">IPTables</a>:

<table class="tablesaw break-out" data-tablesaw-mode="swipe" data-tablesaw-minimap>
<tbody>
<tr>
<td><strong>Rule</strong></td>
<td><strong>Protocol</strong></td>
<td><strong>Direction</strong></td>
<td><strong>Type</strong></td>
<td><strong>Remote IP
</strong></td>
<td><strong>Remote port</strong></td>
<td><strong>Server port</strong></td>
<td><strong>Action</strong></td>
</tr>
<tr>
<td>1a</td>
<td>TCP</td>
<td>incoming</td>
<td>any</td>
<td>any</td>
<td>any</td>
<td>80</td>
<td>Allow</td>
</tr>
<tr>
<td>1b</td>
<td>TCP</td>
<td>outgoing</td>
<td>established</td>
<td>any</td>
<td>any</td>
<td>80</td>
<td>Allow</td>
</tr>
<tr>
<td>2a</td>
<td>TCP</td>
<td>incoming</td>
<td>any</td>
<td><code>99.99.99.99</code></td>
<td>any</td>
<td>22</td>
<td>Allow</td>
</tr>
<tr>
<td>2b</td>
<td>TCP</td>
<td>outgoing</td>
<td>established</td>
<td><code>99.99.99.99</code></td>
<td>any</td>
<td>22</td>
<td>Allow</td>
</tr>
<tr>
<td>3</td>
<td>TCP</td>
<td>any</td>
<td>any</td>
<td>any</td>
<td>any</td>
<td>any</td>
<td>Deny</td>
</tr>
<tr>
<td>4</td>
<td>UDP</td>
<td>any</td>
<td>any</td>
<td>any</td>
<td>any</td>
<td>any</td>
<td>Deny</td>
</tr>
</tbody>
</table>

Most firewalls, however, will hide the gory details of new and established connections. They will assume that all replies to established connections are allowed through and only deal with the new connections. The table can then be much shorter:
<table class="tablesaw break-out" data-tablesaw-mode="swipe" data-tablesaw-minimap>
<tbody>
<tr>
<td><strong>Rule</strong></td>
<td><strong>Protocol</strong></td>
<td><strong>Direction</strong></td>
<td><strong>Remote IP
</strong></td>
<td><strong>Remote port</strong></td>
<td><strong>Server port</strong></td>
<td><strong>Action</strong></td>
</tr>
<tr>
<td>1</td>
<td>TCP</td>
<td>incoming</td>
<td>any</td>
<td>any</td>
<td>80</td>
<td>Allow</td>
</tr>
<tr>
<td>2</td>
<td>TCP</td>
<td>incoming</td>
<td><code>99.99.99.99</code></td>
<td>any</td>
<td>22</td>
<td>Allow</td>
</tr>
<tr>
<td>3</td>
<td>TCP</td>
<td>any</td>
<td>any</td>
<td>any</td>
<td>any</td>
<td>Deny</td>
</tr>
<tr>
<td>4</td>
<td>UDP</td>
<td>any</td>
<td>any</td>
<td>any</td>
<td>any</td>
<td>Deny</td>
</tr>
</tbody>
</table>

If these rules were applied to a hardware firewall, there would also be a <em>server IP address</em>, as hardware firewalls usually work on behalf of more than one server. In that case, the table could just have <em>source</em> and <em>destination</em> and no <em>direction</em>. like this:

<table class="tablesaw break-out" data-tablesaw-mode="swipe" data-tablesaw-minimap>
<tbody>
<tr>
<td><strong>Rule</strong></td>
<td><strong>Protocol</strong></td>
<td><strong>Source IP
</strong></td>
<td><strong>Source port</strong></td>
<td><strong>Destination IP</strong></td>
<td><strong>Destination port</strong></td>
<td><strong>Action</strong></td>
</tr>
<tr>
<td>1</td>
<td>TCP</td>
<td>any</td>
<td>any</td>
<td><code>80.72.139.101</code></td>
<td>80</td>
<td>Allow</td>
</tr>
<tr>
<td>2</td>
<td>TCP</td>
<td><code>99.99.99.99</code></td>
<td>any</td>
<td><code>80.72.139.101</code></td>
<td>22</td>
<td>Allow</td>
</tr>
<tr>
<td>3</td>
<td>TCP</td>
<td>any</td>
<td>any</td>
<td>any</td>
<td>any</td>
<td>Deny</td>
</tr>
<tr>
<td>4</td>
<td>UDP</td>
<td>any</td>
<td>any</td>
<td>any</td>
<td>any</td>
<td>Deny</td>
</tr>
</tbody>
</table>

To allow outgoing requests, the source and destination would be switched, with the server's IP address <code>80.72.139.101</code> appearing in the <em>source IP address</em> column. Also note that the remote and server protocol are always the same.</p>

### Firewall Example

Some firewall configurations provide tables and forms similar to the one above and you just have to fill in the blanks. The example below is the software firewall tool provided by Plesk 9.5.4. <a href="https://www.parallels.com/products/plesk/">Plesk</a> is a common server management application. To see the screen below, click “Modules” on the left, then “Firewall,” “Edit Firewall Configuration” and “Add Custom Rule.”

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e0188c85-c917-4a39-b47d-68269e0cfe5c/plesk1.png"><img title="Adding a new rule to the firewall in Plesk 9.5.4." src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e0188c85-c917-4a39-b47d-68269e0cfe5c/plesk1.png" alt="Adding a new rule to the firewall in Plesk 9.5.4." width="546" height="650" /></a><br>
<em>Adding a new rule to the firewall in Plesk 9.5.4.</em>

This has most of the fields shown in the table above: <em>direction</em>, action of <em>allow or deny</em>, <em>server port</em>, <em>protocol</em> and <em>remote/source IP address</em>. The mini-table above blocks both directions within the same rule (rules 3 and 4). In many configurations, these have to be done separately by setting up the rule and choosing a direction of incoming or outgoing.

In this interface, there is another choice for direction — forwarding. Port forwarding allows letters to be forwarded from one port to another. It is commonly used in household broadband routers, which allow several computers to share a single IP address by mapping ports.

For example, your laptop might have a local IP address of <code>192.168.1.10</code>. When you request a Web page (with your sender's address like <code>192.168.1.10</code>, TCP, 60000), your letter first goes to your broadband router, which puts your letter in a brand new envelope with a new sender's address (such as <code>78.78.78.78</code>, TCP, 12013) and forwards it to its destination (such as <code>80.72.139.101</code>, TCP, 80). When the router gets the reply, it remembers that apartment 12013 is just a forwarding address, so it puts it in a new envelope and forwards it to you (at <code>192.168.1.10</code>, TCP, 60000). A typical Web server would not need to do port forwarding and so the firewall would block all forwarding.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0b1d0899-b372-4a0b-af6c-ab7b7096fa81/iptables.jpg"><img title="The Plesk firewall is just a friendly interface for the UNIX firewall IPTables." src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0b1d0899-b372-4a0b-af6c-ab7b7096fa81/iptables.jpg" alt="The Plesk firewall is just a friendly interface for the UNIX firewall IPTables." width="546" height="564" /></a><br>
<em>The Plesk firewall is just a friendly interface for the UNIX firewall IPTables. The command <code>iptables -L</code> shows the current rules as above.</em>

### Another Firewall Example

The screenshot below is from the shared hardware firewall configuration tool provided by the host UK Fast. You have to pay extra for this service. In exchange, you can log into the UK Fast website and add, modify and remove rules:

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3775a45d-02c2-45f0-9448-9aa323245f02/ukfast1.png"><img title="A hardware firewall configuration interface for allowing incoming and outgoing traffic to TCP ports." src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3775a45d-02c2-45f0-9448-9aa323245f02/ukfast1.png" alt="A hardware firewall configuration interface for allowing incoming and outgoing traffic to TCP ports." width="546" height="499" /></a><br>
<em>A hardware firewall configuration interface for allowing incoming and outgoing traffic to TCP ports.</em>

This interface is very simple. It already knows your <em>server IP address</em> and it assumes that everything not listed is denied. The only thing you can do is add allowed ports.

The ports relate to the <em>server port</em> for incoming connections and the <em>remote port</em> for outgoing connections. As above, this only deals with new connections. Established requests are allowed through automatically. So the first incoming rule on the left states that anybody in the world can access port 80 on the server (the web-crazy family).

The first outgoing rule on the right allows the server to request port 80 on other servers. You may wonder why your Web server would ever need to do this. Surely it is not spending its free time browsing the Internet. But it is necessary for things like PayPal Instant Payment Notification, where your server sends a request to PayPal to double check that a payment has been received. Similarly, most of the other outgoing rules allow your server to send emails, check email accounts and do FTP.

There is no mention of the <em>remote IP address</em> on this screen. That is configured separately by clicking on “Admin Config” and is shown in the next subsection.</p>

### Subnets

The UK Fast hardware firewall has a separate screen for entering <em>remote IP addresses</em>. They have a preset list of restricted ports (such as 22 for SSH and 8443 for Plesk), and only the IP addresses shown are allowed to communicate with those ports. All other ports (like 80 for Web serving) are allowed to correspond with anybody. You lose some flexibility this way, but it makes it very easy to configure.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b47437ec-f6f3-4613-a98d-0571df8f952b/ukfast-ips.png"><img title="Entering a list of source IP addresses which are allowed to connect to restricted ports." src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b47437ec-f6f3-4613-a98d-0571df8f952b/ukfast-ips.png" alt="Entering a list of source IP addresses which are allowed to connect to restricted ports." width="546" height="439" /></a><br>
<em>Entering a list of source IP addresses which are allowed to connect to restricted ports.</em>

This screen also introduces <strong>subnets</strong>. Up till now, all the rules have dealt with single IP addresses like <code>99.99.99.99</code>, but you can also enter IP addresses in ranges.

IP addresses consist of four numbers between 0 and 255. (There are newer ones with six numbers but they are still relatively uncommon.) It would be nice to be able to enter ranges by putting things like 99.99.0-255.0-255. Unfortunately you can't. Instead you enter a starting address like 99.99.0.0 and a mask like <code>255.255.0.0</code>. Similarly the range <code>77.77.77.0-255</code> is entered as the address <code>77.77.77.0</code> and the subnet mask <code>255.255.255.0</code>.

You can enter smaller ranges such as <code>77.77.77.8-15</code>, which would be <code>77.77.77.8</code> with subnet mask <code>255.255.255.248</code>. It's confusing because it invokes binary, but there are lots of detailed subnet explanations available.</p>

### All the Fields

Here is a summary of the different fields discussed in this section:

*   Rule number: remember that rules are checked and applied in order
*   Protocol: either TCP or UDP
*   Direction: incoming, outgoing or forwarding
*   Remote IP address: such as `77.77.77.0`
*   Remote subnet mask: such as `255.255.255.0`
*   Remote port or port range
*   Server IP address
*   Server subnet mask
*   Server port or port range
*   Action: allow or deny

Sometimes the interface will have <em>source</em> and <em>destination</em> instead of <em>direction</em>, <em>remote</em> and <em>server</em>. In this case, they are the same for incoming mail, but reversed for outgoing. In other words, <em>remote</em> equals <em>source</em> for incoming but <em>remote</em> equals <em>destination</em> for outgoing.

The next section discusses the ports in more detail. The concierge's piece of paper is very limiting. A real Web server will look more like the hardware firewall example above.</p>

## Configuring A Firewall For A Web Server

The Web server family usually lives in apartment 80. Many other popular computer services have a preferred apartment too. This section lists and describes some of the <a href="https://en.wikipedia.org/wiki/List_of_TCP_and_UDP_port_numbers">most common ports</a> used by a standard Web and email server, and then provides recommendations on setting up your own firewall.</p>

### Ports

These are some of the well-known official ports you may come across. Some firewalls don't even show the port number, only the service which usually uses it.

<table class="tablesaw break-out" data-tablesaw-mode="swipe" data-tablesaw-minimap>
<tbody>
<tr>
<td><strong>Protocol</strong></td>
<td><strong>Port</strong></td>
<td><strong>Used by</strong></td>
<td><strong>Description</strong></td>
</tr>
<tr>
<td>TCP</td>
<td>20</td>
<td>FTP (active mode)</td>
<td><a href="https://www.mdjnet.dk/ftp.html">FTP</a> operates in active or passive mode, as requested by the person doing the FTPing. In both modes, commands are sent to the server on port 21. In <a href="https://slacksite.com/other/ftp.html#active">active mode</a>, the server initiates a new connection from port 20 to send data back. In <a href="https://slacksite.com/other/ftp.html#passive">passive mode</a>, there is an extra incoming connection to an unprivileged port (&gt;=1024). So for FTP to work, you either have to allow outgoing connections from port 20 (active) or incoming connections from port 21 to port&gt;=1024.</td>
</tr>
<tr>
<td>TCP</td>
<td>21</td>
<td>FTP</td>
<td>FTP is the File Transfer Protocol. Restrict it by IP address so that only trusted people can FTP to your server, or turn it off completely and only allow Secure FTP, which runs as part of SSH over port 22.</td>
</tr>
<tr>
<td>TCP</td>
<td>22</td>
<td>SSH</td>
<td>Secure Shell allows people to login and run commands on your server. This is very useful for server administration, but should be restricted by IP address.</td>
</tr>
<tr>
<td>TCP</td>
<td>23</td>
<td>Telnet</td>
<td>Telnet is an insecure version of SSH. It is usually completely denied.</td>
</tr>
<tr>
<td>TCP</td>
<td>25</td>
<td>SMTP</td>
<td>SMTP is the <a href="https://en.wikipedia.org/wiki/Simple_Mail_Transfer_Protocol">Simple Mail Transfer Protocol</a>. It handles two tasks. As a Mail Submission Agent it receives email for all the email accounts set up on your server. As a Mail Transfer Agent, it can also forward email to other servers. The submission tasks are now handled more often by port 587. And the transfer tasks are usually configured to require a password, and relaying (forwarding email for accounts not even listed on the server) is turned off completely to stop SPAM relaying. Either way it needs to be allowed.</td>
</tr>
<tr>
<td><a href="https://www.windowsnetworking.com/kbase/WindowsTips/WindowsServer2008/AdminTips/Admin/WhyDNSWorksOnBothTCPandUDP.html">UDP and TCP</a></td>
<td>53</td>
<td>DNS</td>
<td>DNS stands for Domain Name System. It translates domains names like <code>www.smashingmagazine.com</code> into IP addresses. DNS data is transferred between servers using TCP, and DNS queries are handled with UDP. Unless your server is acting as a DNS server, only outgoing UDP needs to be allowed. This allows your server to look up domain names. For instance, if you have a website which does PayPal Instant Notifications, then your Web server probably POSTs a request to <code>www.paypal.com</code>, but first it needs to translate that into an IP address, so it needs to initiate a request from UDP 53. Alternatively, you can put the translation into your <code>/etc/hosts</code> file (on UNIX) so that the DNS request is not required.</td>
</tr>
<tr>
<td>TCP</td>
<td>80</td>
<td>HTTP</td>
<td>This is your Web server. Allow it so people can browse your websites.</td>
</tr>
<tr>
<td>TCP</td>
<td>110</td>
<td>POP3</td>
<td>POP stands for Post Office Protocol. If your server hosts email accounts, this port allows people to check their email.</td>
</tr>
<tr>
<td>TCP</td>
<td>143</td>
<td>IMAP</td>
<td>IMAP is the Internet Message Access Protocol. It is a more sophisticated alternative to POP3, as it not only stores your incoming email but allows you to create folders too. The person who creates the email account is the one who decides whether it should be POP3 or IMAP.</td>
</tr>
<tr>
<td>TCP</td>
<td>443</td>
<td>HTTPS</td>
<td>This port is the default for a secure Web server, which requires an SSL certificate.</td>
</tr>
<tr>
<td>TCP</td>
<td>465</td>
<td><a href="https://en.wikipedia.org/wiki/SMTPS">SMTPS</a></td>
<td>This port was originally used for a secure version of SMTP. This is now done using the normal SMTP port 25.</td>
</tr>
<tr>
<td>TPP</td>
<td>587</td>
<td>SMTP</td>
<td>Port 587 is the official port for submitting email messages to a server.</td>
</tr>
<tr>
<td>TCP</td>
<td>3306</td>
<td>MySQL</td>
<td>Deny or restrict only to trusted IP addresses that connect directly to your MySQL databases from across the Internet.</td>
</tr>
<tr>
<td>TCP</td>
<td>8443</td>
<td>Plesk</td>
<td>Plesk is a server management tool. It runs as a mini-Web server, accessed via your Web browser. If you have a hardware firewall or a definitely permanently static IP address, you can restrict this by IP address. If you use Plesk's own software firewall, then restricting by IP address is dangerous in case your IP address ever changes, or your office burns down or you need to access it from somewhere else.</td>
</tr>
<tr>
<td>TCP</td>
<td>10000</td>
<td>Webmin</td>
<td>Webmin is another server management tool. The same caveats apply as with Plesk.</td>
</tr>
<tr>
<td>TCP</td>
<td>1024- 65535</td>
<td>Outgoing requests</td>
<td>One of the first scenarios in this article was a person using a Web browser. In this case, a high numbered port on the client (1024 or above) connects to the Web server's port 80. If your Web server looks up a Web page (as in PayPal IPN) it connects from one of its own high numbered ports. On many <a href="https://www.faqs.org/docs/securing/chap6sec70.html">UNIX computers</a>, the available range is set in the file <code>/proc/sys/net/ipv4/ip_local_port_range</code>. It is often from 1024-4099 or 32768-61000.</td>
</tr>
<tr>
<td>ICMP</td>
<td>n/a</td>
<td>Ping</td>
<td><a href="https://en.wikipedia.org/wiki/Internet_Control_Message_Protocol">Ping</a> is used to check if a computer is reachable over a network. It uses a different port-less protocol called Internet Control Message Protocol. Some firewalls will also give you control over this.</td>
</tr>
</tbody>
</table>

### Full Configuration

For a basic Web and email server with the Plesk management interface, you could configure your firewall to:

*   Allow incoming connections from anywhere to TCP ports 25 (SMTP), 80 (Web server), 110 (POP email accounts), 143 (IMAP email accounts), 443 (secure Web server), 587 (SMTP)
*   Restrict incoming connections to ports TCP 22 (SSH), 8443 (Plesk unless you use Plesk to configure the firewall)
*   Allow outgoing connections from any port on the server to the remote TCP ports 25 (SMTP), 80 (web), 443 (secure web), 587 (SMTP) and UDP 53 (DNS lookups)
*   Deny everything else

If you allow additional services, you will need to open up additional ports. This could include automatic backups, security scans or remote database access.</p>

### Checking With Telnet

All computers come with a Telnet client which allows you to connect to a Telnet server on port 23 and run commands. But the Telnet client can also connect to other ports, so it is a very useful way to check a firewall.

To use it, you'll need to open a Terminal or Command Prompt. On a Mac with OS X, go to <code>Applications</code> → <code>Utilities</code> and run Terminal. On a PC with Windows, go to <code>Start</code> → <code>All Programs</code> → <code>Accessories</code> and select “Command Prompt.” If you use Ubuntu Linux, it’s under <code>Applications</code> → <code>Accessories</code>, and in a similar location for other flavors of Linux.

Once you've got the Terminal open, try typing something like this followed by “Enter”:

<pre><code class="language-markup tmp-html">telnet www.smashingmagazine.com 21</code></pre>

First telnet will translate <code>www.smashingmagazine.com</code> into an IP address and then it will try to connect to its port 21. In this case the connection is refused, which means the FTP server isn't running at all or is being blocked at the application level. Here are a few more examples:

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/95604b16-7dfa-44e0-9cde-101625ae7cbb/telnet.png"><img title="Using telnet to probe www.smashingmagazine.com." src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/95604b16-7dfa-44e0-9cde-101625ae7cbb/telnet.png" alt="Using telnet to probe www.smashingmagazine.com." width="546" height="377" /></a><br>
<em>Using telnet to probe <code>www.smashingmagazine.com</code>.</em>

Ports 21 (FTP) and 25 (SMTP) refuse the connection. Port 23 (Telnet) doesn't even reply, which may mean that it's blocked by a firewall. Port 80 (Web server) connects successfully. I could then have issued an HTTP command like:

<pre><code class="language-markup tmp-html">GET / HTTP/1.1
Host: www.smashingmagazine.com</code></pre>

Followed by a blank line. That would have given me Smashing Magazine's home page. Instead I pressed Ctrl + ] to close the connection and then quit from Telnet.</p>

### Personal Firewalls

Firewalls are not just for servers. Many personal computers also have software firewalls, like the <a href="https://en.wikipedia.org/wiki/Windows_Firewall">Windows Firewall</a> on Windows Vista or the <a href="https://www.macwrite.com/critical-mass/mac-os-x-built-firewall-options">Mac Firewall</a> in Mac OS X. Underneath, these probably operate in the same way as server firewalls, but a lot of the details are hidden. They often just have an on/off switch which blocks all incoming traffic, with the ability add exceptions by application rather than by port. There are more sophisticated third-party products available which allow for port and IP address restrictions.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/856cf9cb-ed39-4a04-a136-00098dc07b7f/windows-firewall-settings.png"><img title="Configuration screen for Windows Firewall in Windows XP Service Pack 2." src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/856cf9cb-ed39-4a04-a136-00098dc07b7f/windows-firewall-settings.png" alt="Configuration screen for Windows Firewall in Windows XP Service Pack 2." width="434" height="515" /></a><br>
<em>Configuration screen for Windows Firewall in Windows XP Service Pack 2.</em>

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4b007ec2-3fc9-4b04-8592-3ca159f70fae/macfirewall.jpg"><img title="Configuration screen for Mac OS X firewall which is a graphical interface for the underlying UNIX software firewall called ipfirewall." src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4b007ec2-3fc9-4b04-8592-3ca159f70fae/macfirewall.jpg" alt="Configuration screen for Mac OS X firewall which is a graphical interface for the underlying UNIX software firewall called ipfirewall." width="546" height="428" /></a><br>
<em>Configuration screen for Mac OS X firewall which is a graphical interface for the underlying UNIX software firewall called ipfirewall.</em>

## Firewall Pitfalls

Firewalls are great for blocking traffic from unwanted sources. If you have access to a firewall, it is advisable to at least limit FTP and SSH to trusted IP addresses. In some senses though, they are very crude. They either allow or deny. They do not care about the contents of the letter.</p>

### Things That a Firewall Can't Block

Therefore, <strong>a firewall cannot block SPAM, viruses or hacks</strong>.

If your SMTP port 25 is open, then email can be sent to it. There might be 10,000 emails an hour discussing the finer points of Viagra, but they all look legitimate to a firewall. They might contain attached EXE files which will take over your computer once opened, but the firewall won't notice.

Similarly, all standard Web servers have port 80 or 443 open. The firewall cannot tell the difference between a valid request for your home page, or a piece of software canvassing Wordpress installations to look for weak spots, so it can post a Trojan Horse PHP file containing a mini-shell which will notify a hacker somewhere and allow your server to be used for denial of service attacks.

Finally, if a clever hacker somewhere figures out how to gain control over a server by issuing specially formatted requests to your IMAP port 143, the firewall won't lift a finger.

Therefore, even if you have a firewall, you still need to worry about SPAM and viruses in emails, and you still need to keep your server software and websites up-to-date with the latest security patches.</p>

### Locking Yourself Out

Software firewalls have an extra pitfall. It is entirely possible to lock yourself out of your own server. The example above showed a software firewall configured within Plesk, which usually runs on port 8443. If you mistakenly blocked port 8443 and saved the configuration, then you would not be able to login again and undo it. This could also happen if you restricted Plesk by IP address and then your IP address changed.

You would then have to login via SSH and manually figure out how to reverse the rule by editing IPtables. If you had also blocked SSH, your only recourse would be to call the hosting company. They might have to attach a physical keyboard and screen to your server in order to login and remove the rule.</p>

## Conclusion

This article has covered the basics of firewalls, and has hopefully given you a clear idea of how they operate. The analogy to a pair of massive apartment complexes is not perfect, but provides an insight into the world of ports.

In conclusion, if you have access to a firewall, you should use it. For software firewalls, you can safely restrict SSH and FTP by IP address and block any other services you are not using. For hardware firewalls, you can reliably restrict access to Plesk or your chosen server management tool.

.price_list { margin: 1em 0 2.5em 0; border-collapse: collapse;width: 100%;border: 1px solid rgba(0,0,0,0.1);border-radius: 8px !important;margin-top: 30px;}.price_list .desc { font-size: 12px; color: #555;}.price_list a { font-family: "Proxima Nova Bold", Arial, serif; }.price_list td {padding: 8px 5px;border: 1px solid rgba(0,0,0,0.05);}.price_list tr:nth-child(2n+1) { background-color: rgba(0,0,0,0.03); }.price_list thead td { color: #fff; font-size: 13px; text-transform: uppercase; background-color: #888;}.price_list td.new_price { color: #cc0000; font-weight: bold; width: 55px;}.price_list td.old_price { width: 55px; color: rgba(0,0,0,0.45); font-weight: bold;}

<em>Credits of image on start page: <a href="https://en.wikipedia.org/wiki/File:Firewall.png">Wikipedia</a>.</em>

{{< signature "cp" >}}

