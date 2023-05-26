---
title: 'HTTPS Everywhere With Nginx, Varnish And Apache'
slug: https-everywhere-with-nginx-varnish-apache
image: 'https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ed801ed6-d237-429f-9b32-a423ed16463f/https.jpg'
date: 2015-09-17T22:22:04.000Z
author: rachel-andrew
summary: >-
  The web is moving toward using HTTPS encryption by default. This move has been encouraged by Google, which announced that <a href="https://googleonlinesecurity.blogspot.co.uk/2014/08/https-as-ranking-signal_6.html">HTTPS would be a ranking signal</a>. However, moving your website to HTTPS is good for <a href="https://medium.com/so-now-you-know/10-reasons-to-go-https-a2cba5734bb6">other reasons</a>, too. Rather than debate those reasons, this article assumes you have already decided to move to HTTPS. We’ll walk through how to move your website to HTTPS, taking advantage of Varnish Cache.
description: >-
  In this article, we’ll walk through how to move your website to HTTPS, taking advantage of Varnish Cache.
categories:
  - Coding
  - Development
  - Optimization
  - Caching
  - Varnish
  - Nginx
---

In previous articles on Smashing Magazine, I’ve explained how to use <a href="https://www.smashingmagazine.com/2013/12/speed-up-your-mobile-website-with-varnish/">Varnish to speed up your website</a>. For those of us who use Varnish and also want to move to HTTPS, there is a problem: <a href="https://www.varnish-cache.org/docs/trunk/phk/ssl_again.html">Varnish doesn’t support HTTPS</a>. If you make the move to SSL, configuring Apache to serve your website securely, then you lose the speed advantage of Varnish.

There is a relatively straightforward way to deal with this issue, and that is to stick something in between incoming SSL requests and Varnish, a layer that handles the secure connection and SSL certificates and then passes the request back to Varnish. For this task, we will use Nginx. You may know Nginx as a web server alternative to Apache, and it is. However, it can also be used as a proxy to handle and pass requests on to other services, which is what we are going to do here. In other words, we’re going to create a web server sandwich, with Varnish as the tasty cache-meat in the middle.

## Where We Are And Where We Want To Be

I’m assuming you are in a similar situation as me and have a server &mdash; whether virtual or dedicated hardware &mdash; with a number of websites running on it. Some of those websites you want to make fully HTTPS, and perhaps some will remain HTTP for the time being.

Your current configuration would have every request on port 80 handled by Varnish. Varnish then decides, based on the rules added to your Varnish Configuration Language (VCL), whether to deliver a cached copy of the page or hand the request back to Apache for a new page to be created. Once the page hits Apache, the web server might need to pull information from the database or do other processing before delivering it.

By the end of this tutorial, we want to be in the following position:

*   Nginx will run on port 443 and handle incoming HTTPS requests, handing them off to Varnish.
*   Varnish will run on port 80 and handle incoming HTTP requests, **including those from Nginx**, delivering directly from cache or handing to Apache
*   Apache will run on port 8080 and do what Apache does: deliver your website or application.

In this situation, Nginx becomes a proxy. It does no processing of your website, and it isn’t running PHP or connecting to your database. All it does is accept the HTTPS requests and pass them back to Varnish. Varnish then decides whether to hand back a cached copy or pass it back to Apache to get a fresh one, using the Varnish rules you already have.

{{% feature-panel %}}

## My Example Environment

I’m going to work in Vagrant, using Ubuntu Trusty. My starting point is as described above, with Apache installed on port 8080, and Varnish 4 installed on port 80.

If you would like to follow along, you can <a href="https://github.com/rachelandrew/smashing-ssl-tutorial">download my environment from GitHub</a>. Instructions on setting up are in the readme file.

I have two websites configured. If I visit those websites in a browser, Varnish will handle the request on port 80, either delivering the file from cache or passing it back to Apache.

At this point, it is useful to check which ports things are running on. SSH into Vagrant on the command line:

<pre><code class="language-bash">
&gt; vagrant ssh
</code></pre>

Then, run netstat:

<pre><code class="language-bash">
&gt; sudo netstat -taupen
</code></pre>

This will give you an output of ports, as well as information on which process is using them. You should find that Varnish is running on port 80 and Apache on 8080.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/edd037e7-2a56-445f-8b38-19b87726c6c6/01-netstat-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3d52a24e-d1f5-4aa6-8afe-f57b4b2f89ef/01-netstat-opt-small.png" alt="Netstat" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/edd037e7-2a56-445f-8b38-19b87726c6c6/01-netstat-opt.jpg">View large version</a>)</figcaption></figure>

You can also check that Varnish is running normally and serving pages from the cache by running the following:

<pre><code class="language-bash">
&gt; varnishstat
</code></pre>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/272c02df-193c-452f-8b9a-9c51432d5c36/02-varnishstat-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/29049238-b54b-477e-8789-b54c7986623e/02-varnishstat-opt-small.png" alt="varnishstat" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/272c02df-193c-452f-8b9a-9c51432d5c36/02-varnishstat-opt.jpg">View large version</a>)</figcaption></figure>

If you reload your page in the web browser, you should see cache hits and misses.

If you are using my VCL from GitHub, I’ve added to the Varnish configuration some code that will send a <code>HIT</code> or <code>MISS</code> header to the browser. This means you can look at the headers being sent. You should see <code>X-Cache: HIT</code> if the page came from Varnish and <code>X-Cache: MISS</code> if it was served by Apache.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/31c73016-3393-4b6a-9a03-98bfdce28a65/03-browser-hit-opt.png" alt="Viewing a HIT from Varnish in the headers" /><br>
<figcaption></figcaption></figure>

## Installing Nginx

We can now install Nginx. On an Ubuntu system, this is as straightforward as issuing the following command:

<pre><code class="language-bash">
&gt; sudo apt-get install nginx
</code></pre>

<a href="https://nginx.org/en/docs/install.html">Nginx’s documentation</a> has information on installing Nginx on a variety of systems, as well as packages for systems that do not include it in their package management. Remember that we are just using Nginx as a proxy, so you don’t need to worry about configuring PHP or MySQL support. Nginx won't start by default, and currently it is unable to start because Varnish is already using port 80. If you were doing this process on a live server, you would be safe to run this step without any impact on your running websites.

## Create Or Install An SSL Certificate

The next step is to set up our SSL certificate. Because we are working locally, we can create a “self-signed” certificate in order to test SSL connections.

To create a self-signed certificate for testing, first choose or create a directory to put it in. I've created an <code>nginx</code> directory in <code>/etc/ssl</code>. Then, run the command below to generate the key and certificate pair.

<pre><code class="language-bash">
&gt; sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /etc/ssl/nginx/smashing_ssl_one.tutorials.eoms.key -out /etc/ssl/nginx/smashing_ssl_one.tutorials.eoms.crt
</code></pre>

When you run this command you will be prompted for a series of questions. You can mostly put junk in these; however, when prompted for the “Common Name,” use the domain that you type in the URL bar to access your website on Vagrant. For me, this is <code>smashing_ssl_one.tutorials.eoms</code>.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6fe795af-d40e-4d0a-822c-08b894af38c3/04-self-signed-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/728b9aa4-b04e-4858-a39a-b1a6106f6888/04-self-signed-opt-small.png" alt="Creating a self-signed certificate" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6fe795af-d40e-4d0a-822c-08b894af38c3/04-self-signed-opt.png">View large version</a>)</figcaption></figure>

If you look now in the folder you created, you should see two files, one with a <code>.key</code> extension and one with a <code>.crt</code> extension.

On your live server, you would purchase a certificate from an issuing authority. You would then be given the key and certificate files and, rather than create them, you would place them on your server before following the next step.

## Configure The SSL Websites In Nginx

With your self-signed or purchased SSL certificates in place, you can set up your websites in Nginx.

First, remove the default configuration file from <code>/etc/nginx/sites-enabled</code>. You can delete the <code>default</code> file or move it elsewhere.

We only need to configure websites that will be served over SSL; any other websites will continue to be served directly from Varnish on port 80. In my case, I’m going to configure <code>smashing_ssl_one.tutorials.eoms</code>. Wherever you see that domain in the steps below, you can replace it with your own live or local domain, if you are not using my example.

In <code>/etc/nginx/sites-available/</code>, create a configuration file as <code>your_domain.com.conf</code>.

In that file, add the following:

<pre><code class="language-nginx">
server {
  listen *:443 ssl;
  server_name smashing_ssl_one.tutorials.eoms;

  ssl on;
  ssl_certificate /etc/ssl/nginx/smashing_ssl_one.tutorials.eoms.crt;
  ssl_certificate_key /etc/ssl/nginx/smashing_ssl_one.tutorials.eoms.key;

  location / {

    proxy_pass            https://127.0.0.1:80;
    proxy_read_timeout    90;
    proxy_connect_timeout 90;
    proxy_redirect        off;

    proxy_set_header      X-Real-IP $remote_addr;
    proxy_set_header      X-Forwarded-For $proxy_add_x_forwarded_for;
    proxy_set_header      X-Forwarded-Proto https;
    proxy_set_header      X-Forwarded-Port 443;
    proxy_set_header      Host $host;
  }
} 
</code></pre>

The first line tells the server we are listening on port 443. This is the default port for HTTPS connections, just as port 80 is for HTTP. We then give the server name.

We set SSL to be on and then add the certificate and key that we created or installed, using a full file system path.

Under location, we use <code>proxy_pass</code> to pass the request back to port 80, where Varnish is waiting for it. We then set some headers, which will be passed through.

After adding this file, symlink the file in <code>sites-available</code> to <code>sites-enabled</code>. If you ever want to switch off the website, you can just delete the symlink. The following command will create a symlink on the command line:

<pre><code class="language-bash">
&gt; ln -s /etc/nginx/sites-available/smashing_ssl_one.tutorials.eoms.conf /etc/nginx/sites-enabled/smashing_ssl_one.tutorials.eoms.conf
</code></pre>

Then, restart Nginx:

<pre><code class="language-bash">
&gt; sudo service nginx restart
</code></pre>

If you see the output <code>restarting nginx nginx</code>, followed by <code>[fail]</code>, the likely problem is some typo in your configuration. My usual problem are either separating the keys and values with a colon or forgetting the semicolon at the end of the line.

If Nginx fails to start, look at the log in <code>/var/log/nginx/error.log</code> because most problems are self-explanatory.

You will see <code>[OK]</code> if Nginx starts up successfully. Now, if you check to see what is running on which port, you should see that Nginx is now on port 443, Varnish still has port 80 and Apache 8080.

<pre><code class="language-bash">
&gt; sudo netstat -taupen
</code></pre>

The big test is to now visit the website using <code>https://</code>. If you are using a self-signed certificate, then you will have to step through the warning messages &mdash; your browser is warning you that the certificate is issued by an unknown authority.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/69bcf047-88b9-4ee5-a8bb-9347f3c5c9a4/05-exception-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a6a8a5d8-6348-4b34-80fc-8b2d66a58880/05-exception-opt-small.png" alt="Firefox warns me the connection is untrusted" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/69bcf047-88b9-4ee5-a8bb-9347f3c5c9a4/05-exception-opt.png">View large version</a>)</figcaption></figure>

If you see your page served securely with the padlock in the URL bar, then you are now serving HTTPS via Nginx. If you check the <code>HIT</code> or <code>MISS</code> headers or run <code>varnishstat</code> on the command line, you’ll be able to check that pages are being served from Varnish and not hitting Apache each time.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cbe82463-f793-42e6-ad90-60fffd277eab/06-secure-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5ae5a92b-f85f-4c9c-8d7f-ff46f16a3c46/06-secure-opt-small.png" alt="A secure site using a self-signed certificate" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cbe82463-f793-42e6-ad90-60fffd277eab/06-secure-opt.png">View large version</a>)</figcaption></figure>

## Redirecting To SSL Using Varnish

Based on my own experience of doing this, you might want to tweak a few things.

If your website was running on HTTP and you want to run it on HTTPS, then you will need to redirect all HTTP requests. You can do this using Varnish. Varnish is at at port 80, handling any non-SSL requests. What we want to do is ask Varnish to spot any request for our website and redirect it to HTTPS.

In your VCL file at <code>/etc/varnish/default.vcl</code>, add a subroutine as follows:

<pre><code class="language-nginx">
# handles redirecting from http to https
sub vcl_synth {
  if (resp.status == 750) {
    set resp.status = 301;
    set resp.http.Location = req.http.x-redir;
    return(deliver);
  }
}
</code></pre>

Then, in the <code>sub vcl_recv</code> block, add this:

<pre><code class="language-nginx">
if ( (req.http.host ~ "^(?i)smashing_ssl_one.tutorials.eoms") &amp;&amp; req.http.X-Forwarded-Proto !~ "(?i)https") {
  set req.http.x-redir = "https://" + req.http.host + req.url;
  return (synth(750, ""));
}
</code></pre>

You can view the <a href="https://gist.github.com/rachelandrew/6a2693d3cd6fb9268756">full VCL, with this code included</a>, on GitHub.

I am pattern-matching my domain and redirecting it to HTTPS with a 301 “moved permanently” code. So, now everything should be switched to SSL. Restart Varnish, and try to go to the HTTP version of the website and check that you are being redirected.

Another useful check is to use cURL on the command line. The following command will return only the headers of your request. You should see that you are getting a 301 when testing the HTTP URL.

<pre><code class="language-bash">
&gt; curl -I https://smashing_ssl_one.tutorials.eoms
</code></pre>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4926a323-5f35-4608-8402-5812b45c087e/07-headers-redirect-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/74f36e10-7adc-4037-8f70-c60d0477a022/07-headers-redirect-opt-small.png" alt="Redirect 301 headers with curl" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4926a323-5f35-4608-8402-5812b45c087e/07-headers-redirect-opt.png">View large version</a>)</figcaption></figure>

If you seem to be getting a lot of cache misses on your website, then it would be worth checking which cookies are being stripped by Varnish. Varnish doesn’t cache content with cookies because it assumes that this is personalized content. However, things like Google Analytics cookies should not make your content uncacheable. In my example VCL, I’m dealing with some common cookies, but look at <a href="https://ma.ttias.be/varnish-tip-see-cookies-stripped-vcl/">Mattias Geniar’s post</a> for a way to see which cookies are being sent to the back end so that you can deal with your unique examples.

{{% ad-panel-leaderboard %}}

## Grade An SSL

You’ve likely heard of the various compromises in OpenSSL. If you are going to all the trouble of running your websites on HTTPS, then make sure you aren’t vulnerable to any of these issues.

Once you have a live website using SSL, a great way to check is to use the <a href="https://www.ssllabs.com/ssltest/">SSL Server Test</a> from Qualys SSL Labs. Add your domain name and wait for the test to run. The test checks for many common issues in SSL configurations &mdash; your aim is to pass with an A.

When I first ran this on a server with a similar setup to our example Vagrant installation &mdash; Ubuntu Trusty, Nginx, Varnish and Apache &mdash; I got a B rating, due to the server being vulnerable to the Logjam attack. The fix for this is detailed in “<a href="https://weakdh.org/sysadmin.html">Weak Diffie-Hellman and the Logjam Attack</a>.”

Back on your server, <code>cd</code> to the directory that you used to put or create SSL certificates, and run the following:

<pre><code class="language-bash">
&gt; openssl dhparam -out dhparams.pem 2048
</code></pre>

This will create a file named <code>dhparams.pem</code>.

You can then add to your Nginx configuration the code detailed under “Nginx” on the “Weak Diffie-Hellman and the Logjam Attack” website.

<pre><code class="language-nginx">
server {
  listen *:443 ssl;
  server_name smashing_ssl_one.tutorials.eoms;

  ssl on;
  ssl_certificate /etc/ssl/nginx/smashing_ssl_one.tutorials.eoms.crt;
  ssl_certificate_key /etc/ssl/nginx/smashing_ssl_one.tutorials.eoms.key;
  ssl_dhparam /etc/ssl/nginx/dhparams.pem;
  ssl_protocols TLSv1 TLSv1.1 TLSv1.2;
  ssl_ciphers 'ECDHE-RSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-AES256-GCM-SHA384:DHE-RSA-AES128-GCM-SHA256:DHE-DSS-AES128-GCM-SHA256:kEDH+AESGCM:ECDHE-RSA-AES128-SHA256:ECDHE-ECDSA-AES128-SHA256:ECDHE-RSA-AES128-SHA:ECDHE-ECDSA-AES128-SHA:ECDHE-RSA-AES256-SHA384:ECDHE-ECDSA-AES256-SHA384:ECDHE-RSA-AES256-SHA:ECDHE-ECDSA-AES256-SHA:DHE-RSA-AES128-SHA256:DHE-RSA-AES128-SHA:DHE-DSS-AES128-SHA256:DHE-RSA-AES256-SHA256:DHE-DSS-AES256-SHA:DHE-RSA-AES256-SHA:AES128-GCM-SHA256:AES256-GCM-SHA384:AES128-SHA256:AES256-SHA256:AES128-SHA:AES256-SHA:AES:CAMELLIA:DES-CBC3-SHA:!aNULL:!eNULL:!EXPORT:!DES:!RC4:!MD5:!PSK:!aECDH:!EDH-DSS-DES-CBC3-SHA:!EDH-RSA-DES-CBC3-SHA:!KRB5-DES-CBC3-SHA';

  ssl_prefer_server_ciphers on;

  location / {

   proxy_pass            https://127.0.0.1:80;
   proxy_read_timeout    90;
   proxy_connect_timeout 90;
   proxy_redirect        off;

   proxy_set_header      X-Real-IP $remote_addr;
   proxy_set_header      X-Forwarded-For $proxy_add_x_forwarded_for;
   proxy_set_header      X-Forwarded-Proto https;
   proxy_set_header      X-Forwarded-Port 443;
   proxy_set_header      Host $host;

  }
} 
</code></pre>

Reload Nginx and retest your website. Once you have achieved a A rating, you can periodically check your website to make sure you still have that A.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/96be1096-4f44-4b3a-a3a7-17dcbc39949d/08-ssl-test-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a83e919d-6007-45b9-a9d0-b559b3e8e4db/08-ssl-test-opt-small.png" alt="Running SSL Test to check for any SSL issues" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/96be1096-4f44-4b3a-a3a7-17dcbc39949d/08-ssl-test-opt.png">View large version</a>)</figcaption></figure>

## Check For Mixed Content Warnings

Your website may well have resources being loaded from other domains that are not HTTPS &mdash; this will cause a warning on your website. In many cases, the third party will have an HTTPS endpoint that you can link to. However, I had to remove the Lanyrd badges from my own website because the JavaScript was hosted only on HTTP.

## Further Reading And Resources

I’ve added links to additional reading throughout this article. For your reference, here are those links, plus some extra resources I’ve found useful.

### HTTPS and SSL

*   “[10 Reasons to Use HTTPS](https://medium.com/so-now-you-know/10-reasons-to-go-https-a2cba5734bb6),” Guy Podjarny, Medium
*   “[The Big List of SEO Tips and Tricks for Using HTTPS on Your Website](https://moz.com/blog/seo-tips-https-ssl),” Cyrus Shepard, Moz Blog
*   “[Guide to Deploying Diffie-Hellman for TLS](https://weakdh.org/sysadmin.html)” A guide to protecting your server from the Logjam attack
*   [SSL Server Test](https://www.ssllabs.com/ssltest/index.html), Qualys SSL Labs
*   [StartSSL](https://www.startssl.com/) Free SSL certificates
*   [Let’s Encrypt](https://letsencrypt.org/) Offering free SSL certificates, this service will be available in September.

### Varnish

*   “[Varnish Tip: See Which Cookies Are Being Stripped in Your VCL](https://ma.ttias.be/varnish-tip-see-cookies-stripped-vcl/),” Mattias Geniar
*   “[Varnish and Website Performance](https://varnish-cache.org/docs/trunk/users-guide/performance.html),” Varnish Cache This section of the documentation will help you tune Varnish to your application.

If you know of any other helpful resources, or if you’ve followed these steps and found some extra piece of information, please add it to the comments. It will help out the next person doing it.

Under location, we use <code>proxy_pass</code> to pass the request back to port 80, where Varnish is waiting for it. We then set some headers, which will be passed through.

After adding this file, symlink the file in <code>sites-available</code> to <code>sites-enabled</code>. If you ever want to switch off the website, you can just delete the symlink. The following command will create a symlink on the command line:

<pre><code class="language-bash">
&gt; ln -s /etc/nginx/sites-available/smashing_ssl_one.tutorials.eoms.conf /etc/nginx/sites-enabled/smashing_ssl_one.tutorials.eoms.conf
</code></pre>

Then, restart Nginx:

<pre><code class="language-bash">
&gt; sudo service nginx restart
</code></pre>

If you see the output <code>restarting nginx nginx</code>, followed by <code>[fail]</code>, the likely problem is some typo in your configuration. My usual problem are either separating the keys and values with a colon or forgetting the semicolon at the end of the line.

If Nginx fails to start, look at the log in <code>/var/log/nginx/error.log</code> because most problems are self-explanatory.

You will see <code>[OK]</code> if Nginx starts up successfully. Now, if you check to see what is running on which port, you should see that Nginx is now on port 443, Varnish still has port 80 and Apache 8080.

<pre><code class="language-bash">
&gt; sudo netstat -taupen
</code></pre>

The big test is to now visit the website using <code>https://</code>. If you are using a self-signed certificate, then you will have to step through the warning messages &mdash; your browser is warning you that the certificate is issued by an unknown authority.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/69bcf047-88b9-4ee5-a8bb-9347f3c5c9a4/05-exception-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a6a8a5d8-6348-4b34-80fc-8b2d66a58880/05-exception-opt-small.png" alt="Firefox warns me the connection is untrusted" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/69bcf047-88b9-4ee5-a8bb-9347f3c5c9a4/05-exception-opt.png">View large version</a>)</figcaption></figure>

If you see your page served securely with the padlock in the URL bar, then you are now serving HTTPS via Nginx. If you check the <code>HIT</code> or <code>MISS</code> headers or run <code>varnishstat</code> on the command line, you’ll be able to check that pages are being served from Varnish and not hitting Apache each time.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cbe82463-f793-42e6-ad90-60fffd277eab/06-secure-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5ae5a92b-f85f-4c9c-8d7f-ff46f16a3c46/06-secure-opt-small.png" alt="A secure site using a self-signed certificate" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cbe82463-f793-42e6-ad90-60fffd277eab/06-secure-opt.png">View large version</a>)</figcaption></figure>

## Redirecting To SSL Using Varnish

Based on my own experience of doing this, you might want to tweak a few things.

If your website was running on HTTP and you want to run it on HTTPS, then you will need to redirect all HTTP requests. You can do this using Varnish. Varnish is at at port 80, handling any non-SSL requests. What we want to do is ask Varnish to spot any request for our website and redirect it to HTTPS.

In your VCL file at <code>/etc/varnish/default.vcl</code>, add a subroutine as follows:

<pre><code class="language-nginx">
# handles redirecting from http to https
sub vcl_synth {
  if (resp.status == 750) {
    set resp.status = 301;
    set resp.http.Location = req.http.x-redir;
    return(deliver);
  }
}
</code></pre>

Then, in the <code>sub vcl_recv</code> block, add this:

<pre><code class="language-nginx">
if ( (req.http.host ~ "^(?i)smashing_ssl_one.tutorials.eoms") &amp;&amp; req.http.X-Forwarded-Proto !~ "(?i)https") {
  set req.http.x-redir = "https://" + req.http.host + req.url;
  return (synth(750, ""));
}
</code></pre>

You can view the <a href="https://gist.github.com/rachelandrew/6a2693d3cd6fb9268756">full VCL, with this code included</a>, on GitHub.

I am pattern-matching my domain and redirecting it to HTTPS with a 301 “moved permanently” code. So, now everything should be switched to SSL. Restart Varnish, and try to go to the HTTP version of the website and check that you are being redirected.

Another useful check is to use cURL on the command line. The following command will return only the headers of your request. You should see that you are getting a 301 when testing the HTTP URL.

<pre><code class="language-bash">
&gt; curl -I https://smashing_ssl_one.tutorials.eoms
</code></pre>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4926a323-5f35-4608-8402-5812b45c087e/07-headers-redirect-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/74f36e10-7adc-4037-8f70-c60d0477a022/07-headers-redirect-opt-small.png" alt="Redirect 301 headers with curl" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4926a323-5f35-4608-8402-5812b45c087e/07-headers-redirect-opt.png">View large version</a>)</figcaption></figure>

If you seem to be getting a lot of cache misses on your website, then it would be worth checking which cookies are being stripped by Varnish. Varnish doesn’t cache content with cookies because it assumes that this is personalized content. However, things like Google Analytics cookies should not make your content uncacheable. In my example VCL, I’m dealing with some common cookies, but look at <a href="https://ma.ttias.be/varnish-tip-see-cookies-stripped-vcl/">Mattias Geniar’s post</a> for a way to see which cookies are being sent to the back end so that you can deal with your unique examples.

{{% ad-panel-leaderboard %}}

## Grade An SSL

You’ve likely heard of the various compromises in OpenSSL. If you are going to all the trouble of running your websites on HTTPS, then make sure you aren’t vulnerable to any of these issues.

Once you have a live website using SSL, a great way to check is to use the <a href="https://www.ssllabs.com/ssltest/">SSL Server Test</a> from Qualys SSL Labs. Add your domain name and wait for the test to run. The test checks for many common issues in SSL configurations &mdash; your aim is to pass with an A.

When I first ran this on a server with a similar setup to our example Vagrant installation &mdash; Ubuntu Trusty, Nginx, Varnish and Apache &mdash; I got a B rating, due to the server being vulnerable to the Logjam attack. The fix for this is detailed in “<a href="https://weakdh.org/sysadmin.html">Weak Diffie-Hellman and the Logjam Attack</a>.”

Back on your server, <code>cd</code> to the directory that you used to put or create SSL certificates, and run the following:

<pre><code class="language-bash">
&gt; openssl dhparam -out dhparams.pem 2048
</code></pre>

This will create a file named <code>dhparams.pem</code>.

You can then add to your Nginx configuration the code detailed under “Nginx” on the “Weak Diffie-Hellman and the Logjam Attack” website.

<pre><code class="language-nginx">
server {
  listen *:443 ssl;
  server_name smashing_ssl_one.tutorials.eoms;

  ssl on;
  ssl_certificate /etc/ssl/nginx/smashing_ssl_one.tutorials.eoms.crt;
  ssl_certificate_key /etc/ssl/nginx/smashing_ssl_one.tutorials.eoms.key;
  ssl_dhparam /etc/ssl/nginx/dhparams.pem;
  ssl_protocols TLSv1 TLSv1.1 TLSv1.2;
  ssl_ciphers 'ECDHE-RSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-AES256-GCM-SHA384:DHE-RSA-AES128-GCM-SHA256:DHE-DSS-AES128-GCM-SHA256:kEDH+AESGCM:ECDHE-RSA-AES128-SHA256:ECDHE-ECDSA-AES128-SHA256:ECDHE-RSA-AES128-SHA:ECDHE-ECDSA-AES128-SHA:ECDHE-RSA-AES256-SHA384:ECDHE-ECDSA-AES256-SHA384:ECDHE-RSA-AES256-SHA:ECDHE-ECDSA-AES256-SHA:DHE-RSA-AES128-SHA256:DHE-RSA-AES128-SHA:DHE-DSS-AES128-SHA256:DHE-RSA-AES256-SHA256:DHE-DSS-AES256-SHA:DHE-RSA-AES256-SHA:AES128-GCM-SHA256:AES256-GCM-SHA384:AES128-SHA256:AES256-SHA256:AES128-SHA:AES256-SHA:AES:CAMELLIA:DES-CBC3-SHA:!aNULL:!eNULL:!EXPORT:!DES:!RC4:!MD5:!PSK:!aECDH:!EDH-DSS-DES-CBC3-SHA:!EDH-RSA-DES-CBC3-SHA:!KRB5-DES-CBC3-SHA';

  ssl_prefer_server_ciphers on;

  location / {

   proxy_pass            https://127.0.0.1:80;
   proxy_read_timeout    90;
   proxy_connect_timeout 90;
   proxy_redirect        off;

   proxy_set_header      X-Real-IP $remote_addr;
   proxy_set_header      X-Forwarded-For $proxy_add_x_forwarded_for;
   proxy_set_header      X-Forwarded-Proto https;
   proxy_set_header      X-Forwarded-Port 443;
   proxy_set_header      Host $host;

  }
} 
</code></pre>

Reload Nginx and retest your website. Once you have achieved a A rating, you can periodically check your website to make sure you still have that A.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/96be1096-4f44-4b3a-a3a7-17dcbc39949d/08-ssl-test-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a83e919d-6007-45b9-a9d0-b559b3e8e4db/08-ssl-test-opt-small.png" alt="Running SSL Test to check for any SSL issues" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/96be1096-4f44-4b3a-a3a7-17dcbc39949d/08-ssl-test-opt.png">View large version</a>)</figcaption></figure>

## Check For Mixed Content Warnings

Your website may well have resources being loaded from other domains that are not HTTPS &mdash; this will cause a warning on your website. In many cases, the third party will have an HTTPS endpoint that you can link to. However, I had to remove the Lanyrd badges from my own website because the JavaScript was hosted only on HTTP.

## Further Reading And Resources

I’ve added links to additional reading throughout this article. For your reference, here are those links, plus some extra resources I’ve found useful.

### HTTPS and SSL

*   “[10 Reasons to Use HTTPS](https://medium.com/so-now-you-know/10-reasons-to-go-https-a2cba5734bb6),” Guy Podjarny, Medium
*   “[The Big List of SEO Tips and Tricks for Using HTTPS on Your Website](https://moz.com/blog/seo-tips-https-ssl),” Cyrus Shepard, Moz Blog
*   “[Guide to Deploying Diffie-Hellman for TLS](https://weakdh.org/sysadmin.html)” A guide to protecting your server from the Logjam attack
*   [SSL Server Test](https://www.ssllabs.com/ssltest/index.html), Qualys SSL Labs
*   [StartSSL](https://www.startssl.com/) Free SSL certificates
*   [Let’s Encrypt](https://letsencrypt.org/) Offering free SSL certificates, this service will be available in September.

### Varnish

*   “[Varnish Tip: See Which Cookies Are Being Stripped in Your VCL](https://ma.ttias.be/varnish-tip-see-cookies-stripped-vcl/),” Mattias Geniar

If you know of any other helpful resources, or if you’ve followed these steps and found some extra piece of information, please add it to the comments. It will help out the next person doing it.

### <span class="rh">Further Reading</span> on SmashingMag:

*   [HTTP/2: A Guide For Web Designers And Developers](https://www.smashingmagazine.com/2016/02/getting-ready-for-http2/)
*   [World Wide Web, Not Wealthy Western Web](https://www.smashingmagazine.com/2017/03/world-wide-web-not-wealthy-western-web-part-1/)
*   [Understanding REST And RPC For HTTP APIs](https://www.smashingmagazine.com/2016/09/understanding-rest-and-rpc-for-http-apis/)
*   [A Look At The Modern WordPress Server Stack](https://www.smashingmagazine.com/2016/05/modern-wordpress-server-stack/)

{{< signature "vf, ml, al, il" >}}
