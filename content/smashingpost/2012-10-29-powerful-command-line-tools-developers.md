---
title: Powerful Command Line Tools For Developers
slug: powerful-command-line-tools-developers
image: null
date: 2012-10-29T13:27:16.000Z
author: ben-dowling
description: >-
  Good tools are invaluable in figuring out where problems lie, and can also help to prevent problems from occurring in the first place, or just help you to be more efficient in general.
categories:
  - Coding
  - Tools
---
Life as a Web developer can be hard when things start going wrong. The problem could be in any number of places. Is there a problem with the request you're sending, is the problem with the response, is there a problem with a request in a third party library you're using, is an external API failing?

Command line tools are particularly useful because they lend themselves well to automation and scripting, where they can be combined and reused in all sorts of different ways. Here we cover six particularly powerful and versatile tools which can help make your life a little bit easier.

Recommended reading: [Become A Command-Line Power User With Oh-My-ZSH And Z](https://www.smashingmagazine.com/2015/07/become-command-line-power-user-oh-my-zsh-z/)

{{% feature-panel %}}

<img loading="lazy" decoding="async" loading="lazy" decoding="async" class="122999" title="iterm2-split-panes-500" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1cd64827-46dd-4ba9-aee9-13ad205f2c85/terminal.jpg" alt="" width="500" height="351" /><br>
<em>(Image credit: kolnikcollection)</em>

## Curl

Curl is a network transfer tool that's very similar to Wget, the main difference being that by default Wget saves to a file, and curl outputs to the command line. This makes it really simple to see the contents of a website. Here, for example, we can get our current IP from the <a href="https://ifconfig.me">ifconfig.me</a> website:

<pre><code class="language-javascript">$ curl ifconfig.me
93.96.141.93</code></pre>

Curl's <code>-i</code> (show headers) and <code>-I</code> (show only headers) options make it a great tool for debugging HTTP responses and finding out exactly what a server is sending to you:

<pre><code class="language-javascript">$ curl -I news.ycombinator.com
HTTP/1.1 200 OK
Content-Type: text/html; charset=utf-8
Cache-Control: private
Connection: close</code></pre>

The <code>-L</code> option is handy, and makes <code>curl</code> automatically follow redirects. Curl has support for HTTP Basic authentication, cookies, manually setting headers and much, much more.</p>

## Ngrep

For serious network packet analysis there's <a href="https://www.wireshark.org/">Wireshark</a>, with its thousands of settings, filters and configuration options. There's also a command-line version, TShark. For simple tasks I find Wireshark can be overkill, so unless I need something more powerful, ngrep is my tool of choice. It allows you to do with network packets what grep does with files.

For Web traffic you almost always want the <code>-W</code> byline option, which preserves linebreaks, and <code>-q</code> is a useful argument which suppresses some additional output about non-matching packets. Here's an example that captures all packets that contain <code>GET</code> or <code>POST</code>:

<pre><code class="language-javascript">ngrep -q -W byline "^(GET|POST) .*"</code></pre>

You can also pass in additional packet filter options, such as limiting the matched packets to a certain host, IP or port. Here we filter all traffic going to or coming from Google, using port 80 and containing the term "search."

<pre><code class="language-javascript">ngrep -q -W byline "search" host www.google.com and port 80</code></pre>

## Netcat

Netcat, or <code>nc</code>, is a self-described networking Swiss Army knife. It's a very simple but also very powerful and versatile application that allows you to create arbitrary network connections. Here we see it being used as a port scanner:

<pre><code class="language-javascript">$ nc -z example.com 20-100
Connection to example.com 22 port [tcp/ssh] succeeded!
Connection to example.com 80 port [tcp/http] succeeded!</code></pre>

In addition to creating arbitrary connections, Netcat can also listen for incoming connections. Here we use this feature of <code>nc</code>, combined with <code>tar</code>, to very quickly and efficiently copy files between servers. On the server, run:

<pre><code class="language-javascript">$ nc -l 9090 | tar -xzf -</code></pre>

And on the client:

<pre><code class="language-javascript">$ tar -czf dir/ | nc server 9090</code></pre>

We can use Netcat to expose any application over the network. Here we expose a shell over port 8080:

<pre><code class="language-javascript">$ mkfifo backpipe
$ nc -l 8080  0&lt;backpipe | /bin/bash &gt; backpipe</code></pre>

We can now access the server from any client:

<pre><code class="language-javascript">$ nc example.com 8080
uname -a
Linux li228-162 2.6.39.1-linode34 ##1 SMP Tue Jun 21 10:29:24 EDT 2011 i686 GNU/Linux</code></pre>

While the last two examples are slightly contrived (in reality you'd be more likely to use tools such as rsync to copy files and SSH to remotely access a server), they do show the power and flexibility of Netcat, and hint at all of the different things you can achieve by combining Netcat with other applications.

Recommended reading: [Introduction To Linux Commands](https://www.smashingmagazine.com/2012/01/introduction-to-linux-commands/)

## Sshuttle

Sshuttle allows you to securely tunnel your traffic via any server you have SSH access to. It's extremely easy to set up and use, not requiring you to install any software on the server or change any local proxy settings.

By tunneling your traffic over SSH, you secure yourself against tools like <span class="removed_link" title="https://codebutler.com/firesheep/">Firesheep</span> and <a href="https://monkey.org/~dugsong/dsniff/">dsniff</a> when you're on unsecured public Wi-Fi or other untrusted networks. All network communication, including DNS requests, can be sent via your SSH server:

<pre><code class="language-javascript">$ sshuttle -r &lt;server&gt; --dns 0/0</code></pre>

If you provide the <code>--daemon</code> argument, sshuttle will run in the background as a daemon. Combined with some other options, you can make aliases to simply and quickly start and stop tunneling your traffic:

<pre><code class="language-javascript">alias tunnel='sshuttle --D --pidfile=/tmp/sshuttle.pid -r &lt;server&gt; --dns 0/0'
alias stoptunnel='[[ -f /tmp/sshuttle.pid ]] &amp;&amp; kill `cat /tmp/sshuttle.pid`'</code></pre>

You can also use sshuttle to get around the IP-based geolocation filters that are now used by many services, such as BBC's iPlayer, which requires you to be in the UK, and Turntable, which requires you to be in the US. To do this, you'll need access to a server in the target country. Amazon has a <a href="https://aws.amazon.com/free/">free tier</a> of EC2 Micro instances that are available in many countries, or you can find a cheap virtual private server (VPS) in almost any country in the world.

In this scenario, rather than tunneling all of our traffic, we might want to send only traffic for the service we are targeting. Unfortunately, sshuttle only accepts IP address arguments and not hostnames, so we need to make use of <code>dig</code> to first resolve the hostname:

<pre><code class="language-javascript">$ sshuttle -r &lt;server&gt; `dig +short &lt;hostname&gt;`</code></pre>

## Siege

Siege is a HTTP benchmarking tool. In addition to load-testing features, it has a handy <code>-g</code> option that is very similar to curl's <code>-iL</code>, except it also shows you the request headers. Here's an example with Google (I've removed some headers for brevity):

<pre><code class="language-javascript">$ siege -g www.google.com
GET / HTTP/1.1
Host: www.google.com
User-Agent: JoeDog/1.00 [en] (X11; I; Siege 2.70)
Connection: close

HTTP/1.1 302 Found
Location: https://www.google.co.uk/
Content-Type: text/html; charset=UTF-8
Server: gws
Content-Length: 221
Connection: close

GET / HTTP/1.1
Host: www.google.co.uk
User-Agent: JoeDog/1.00 [en] (X11; I; Siege 2.70)
Connection: close

HTTP/1.1 200 OK
Content-Type: text/html; charset=ISO-8859-1
X-XSS-Protection: 1; mode=block
Connection: close</code></pre>

What Siege is really great at is server load testing. Just like <a href="https://httpd.apache.org/docs/2.2/programs/ab.html">ab</a> (an Apache HTTP server benchmarking tool), you can send a number of concurrent requests to a site, and see how it handles the traffic. With the following command, we'll test Google with 20 concurrent connections for 30 seconds, and then get a nice report at the end:

<pre><code class="language-javascript">$ siege -c20 www.google.co.uk -b -t30s
...
Lifting the server siege...      done.
Transactions:                    1400 hits
Availability:                 100.00 %
Elapsed time:                  29.22 secs
Data transferred:              13.32 MB
Response time:                  0.41 secs
Transaction rate:              47.91 trans/sec
Throughput:                     0.46 MB/sec
Concurrency:                   19.53
Successful transactions:        1400
Failed transactions:               0
Longest transaction:            4.08
Shortest transaction:           0.08</code></pre>

One of the most useful features of Siege is that it can take a file of URLs as an input, and then hit those URLs rather than just a single page. This is great for load testing, because you can replay real traffic against your site and see how it performs, rather than just hitting the same URL again and again. Here's how you would use Siege to replay your Apache logs against another server to load test it:

<pre><code class="language-javascript">$ cut -d ' ' -f7 /var/log/apache2/access.log &gt; urls.txt
$ siege -c&lt;concurrency rate&gt; -b -f urls.txt</code></pre>

## Mitmproxy

Mitmproxy is an SSL-capable, man-in-the-middle HTTP proxy that allows you to inspect both HTTP and HTTPS traffic, and rewrite requests on the fly. The application has been behind quite a few iOS application privacy scandals, including Path's address book upload scandal. Its ability to rewrite requests on the fly has also been used to target iOS, including setting a <span class="removed_link" title="https://mitmproxy.org/doc/tutorials/gamecenter.html">fake high score in GameCenter</span>.

Far from only being useful to see what mobile applications are sending over the wire or for faking high scores, mitmproxy can help out with a whole range of Web development tasks. For example, instead of constantly hitting F5 or clearing your cache to make sure you're seeing the latest content, you can run

<pre><code class="language-javascript">$ mitmproxy --anticache</code></pre>

which will automatically strip all cache-control headers and make sure you always get fresh content. Unfortunately it doesn't automatically set up forwarding for you like sshuttle does, so after starting mitmproxy you still need to change your system-wide or browser-specific proxy settings.

Another extremely handy feature of mitmproxy is the ability to record and replay HTTP interactions. The official documentation gives an example of <span class="removed_link" title="https://mitmproxy.org/doc/tutorials/30second.html">a wireless network login</span>. The same technique can be used as a basic Web testing framework. For example, to confirm that your user signup flow works, you can start recording the session:

<pre><code class="language-javascript">$ mitmdump -w user-signup</code></pre>

Then go through the user signup process, which at this point should work as expected. Stop recording the session with <code>Ctrl</code> + <code>C</code>. At any point we can then replay what was recorded and check for the 200 status code:

<pre><code class="language-javascript">$ mitmdump -c user-signup | tail -n1 | grep 200 &amp;&amp; echo "OK" || echo "FAIL"</code></pre>

If the signup flow gets broken at any point, we'll see a <code>FAIL</code> message, rather than an <code>OK</code>. You could create a whole suite of these tests and run them regularly to make sure you get notified if you ever accidentally break anything on your site.

{{< signature "cp" >}}

