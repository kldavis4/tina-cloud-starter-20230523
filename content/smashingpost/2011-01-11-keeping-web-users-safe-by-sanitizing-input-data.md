---
title: Keeping Web Users Safe By Sanitizing Input Data
slug: keeping-web-users-safe-by-sanitizing-input-data
image: null
date: 2011-01-11T14:49:00.000Z
author: philip-tellis
description: >-
  In my [last
  article](https://www.smashingmagazine.com/2010/10/18/common-security-mistakes-in-web-applications/),
  I spoke about several common mistakes that show up in web applications. Of these, the one that causes the most trouble is insufficient input validation/sanitization. In this article, I'm joined by my colleague [Peter (evilops) Ellehauge](https://kilimanjaro.dk/blog/) in looking at input
  filtering in more depth while picking on a few real examples that we've seen around the web.
categories:
  - Coding
  - PHP
  - Security
---
In my <a href="https://www.smashingmagazine.com/2010/10/18/common-security-mistakes-in-web-applications/">last article</a>, I spoke about several common mistakes that show up in web applications.  Of these, the one that causes the most trouble is insufficient input validation/sanitization.  In this article, I'm joined by my colleague <a href="https://kilimanjaro.dk/blog/">Peter (evilops) Ellehauge</a> in looking at input filtering in more depth while picking on a few real examples that we've seen around the web.  As you'll see from the examples below, insufficient input validation can result in various kinds of code injection including <abbr title="Cross Site Scripting">XSS</abbr>, and in some cases can be used to phish user credentials or spread malware.

To start with, we'll take an example<sup>[<a href="#bm-cablegate">1</a>]</sup> from one of the most discussed websites today.  This example is from a site that hosts WikiLeaks material.  Note that the back end code presented is not the actual code, but what we think it might be based on how the exploit works.  The HTML was taken from their website.  We think it's fair to assume that it's written in PHP as the form's action is index.php.

<pre><code class="language-markup tmp-xml">&lt;form method='get' action='index.php'&gt;
&lt;input name="search" value="&lt;?php echo $_GET['search'];?&gt;" /&gt;
&lt;input type=submit name='getdata' value='Search' /&gt;&lt;/form&gt;</code></pre>

In this code, the query string parameter <em>search</em> is echoed back to the user without sanitization.  An attacker could email or IM unsuspecting users a crafted URL that escapes out of the <code>&lt;input&gt;</code> and does nasty things with JavaScript.  A simple way to test for this exploit without doing anything malicious is to use a URL like this:

<pre><code class="language-markup tmp-xml">https://servername/index.php?search="&gt;&lt;script&gt;alert(0)&lt;/script&gt;</code></pre>

{{% feature-panel %}}

This exploit works because PHP has no default <a href="https://www.php.net/manual/en/filter.configuration.php">input filtering</a>, and the developers haven't done any of their own filtering.  This exploit would work just as well in most other programming languages as most of them also lack default input filtering.  A safer way to write the above code is as follows:

<pre><code class="language-php">&lt;?php
$search = filter_input(INPUT_POST | INPUT_GET, 'search', FILTER_SANITIZE_SPECIAL_CHARS);
?&gt;
&lt;form method='get' action='index.php'&gt;
&lt;input name="search" value="&lt;?php echo $search;?&gt;” /&gt;
&lt;input type=submit name='getdata' value='Search' /&gt;&lt;/form&gt;</code></pre>

This is less convenient though and requires code for every input parameter used, so it is often a good choice to set <code>special_chars</code> as PHP's default filter, and then override when required.  We do this in PHP's ini file with the following directive:

<pre><code class="language-php">filter.default="special_chars"</code></pre>

We're not aware of similar default filters in other languages, but if you know of any, let us know in the comments.

It's important to note that simply adding this parameter to PHP's ini file does not automatically make your application secure.  This only takes care of the default case where an input parameter is echoed back in an HTML context.  However, a web page contains many different contexts and each of these contexts requires input to be validated in a different way.</p>

## Is input validation enough?

Recently we've stumbled upon the following code:

<pre><code class="language-php">&lt;?php
$name = "";
if ($_GET['name']) {
    $name = filter_input(INPUT_POST | INPUT_GET, 'name', FILTER_SANITIZE_SPECIAL_CHARS);
}
echo "&lt;a href=login?name=$name&gt;login&lt;/a&gt;";
?&gt;</code></pre>

The developer correctly applies input filtering, and this code was reviewed and made live.  However, something small seems to have slipped through.  The developer hasn't used quotes around the value of the <code>href</code> attribute, so the browser assumes that its value extends up to the first white-space character.  A crafted URL demonstrates the problem:

<pre><code class="language-markup tmp-xml">https://servername/login.php?name=foo+onmouseover=alert(/bar/)</code></pre>

All of the characters in name are safe and pass through the filter untouched, but the resulting HTML looks like this:

<pre><code class="language-markup tmp-xml">&lt;a href=login?name=foo onmouseover=alert(/bar/)&gt;login&lt;/a&gt;</code></pre>

The lack of quotes turns the attribute value into an <code>onmouseover</code> event handler.  When the unsuspecting user mouses over the link to click on login, the <code>onmouseover</code> handler triggers.  Quoting the value of the <code>href</code> attribute fixes the problem here.  This is a good enough reason to quote all attribute values even though they are optional according to the <a href="https://dev.w3.org/html5/spec/Overview.html#attributes-0">HTML spec</a>.

<pre><code class="language-php">&lt;?php
$name = "";
if ($_GET['name']) {
    $name = filter_input(INPUT_POST | INPUT_GET, 'name', FILTER_SANITIZE_SPECIAL_CHARS);
}
echo "&lt;a href="login?name=$name"&gt;login&lt;/a&gt;";
?&gt;</code></pre>

For this particular situation though, we also need to look at context.  The <code>href</code> attribute accepts a URL as its value, so the value passed to it needs to be urlencoded as well as quoted.

[![https://xkcd.com/327/](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fb2a3284-8578-4422-b859-fcba4d52e33f/sql.png)](https://xkcd.com/327/)  
_[Full image](https://xkcd.com/327/) (from xkcd)_

## Commonly overlooked sections

While many web developers correctly quote and validate input in page content, we find that some sections of the page are still overlooked, possibly because they aren't perceived to be a problem, or perhaps they've just been missed.  Here is an example from a dictionary web site:

<pre><code class="language-markup tmp-xml">&lt;title&gt;&lt;?php echo $word; ?&gt; - Definitions and more ...&lt;/title&gt;</code></pre>

Now by default, no browser executes code within the title tags, so the developer probably thought that it was safe to display data untreated in the title.  Carefully crafted input data can escape the title tags and inject script with something like this

<pre><code class="language-markup tmp-xml">https://servername/dictionary?word=&lt;/title&gt;&lt;script&gt;alert(/xss/)&lt;/script&gt;</code></pre>

Other commonly overlooked pages are error pages and error messages.  Does your 404 page echo on screen the incorrect URL that was typed in?  If it does, then it needs to treat that input first.  A banking website recently had code similar to the following<sup>[<a href="#bm-icici">2</a>]</sup> (they used ASP in this case):

<pre><code class="language-php">&lt;%
if Request.Querystring("errmsg") then
    Response.Write("&lt;em&gt;" &amp; Request.QueryString("errmsg") &amp; "&lt;/em&gt;")
end if
%&gt;</code></pre>

The <code>errmsg</code> parameter didn't come in from a form, but from a server-side redirect.  The developers assumed that since this URL came from the server it would be safe.

Ads/analytics sections at the bottom of a page are also frequently not handled correctly. Perhaps because boilerplate code is provided and it just works. As the following example from a travel site shows, you should not trust anyone and that includes boilerplate code:

<pre><code class="language-markup tmp-xml">&lt;script type="text/javascript"&gt;
google_afs_query = "&lt;?php echo $_GET['query'];?&gt;";
.
.
&lt;/script&gt;</code></pre>

This is vulnerable to the following attack string:

<pre><code class="language-markup tmp-xml">https://servername/?query=";alert(0)//</code></pre>

In this case input data needs to be validated for use in a JavaScript context since that's where the data is echoed out to.  What meta-characters would you scan for in this case?  Would you quote them or strip them?  The answer depends on context, and only you the developer or owner of the page know what the right context is.

## Different contexts

Now like we mentioned earlier, input may be used in different contexts, and it needs to be treated differently depending on the context that it will be used in.  Sometimes data will be used in multiple contexts and may require to be treated differently for each case.  Let's look at a few cases.</p>

### HTML Context

In an HTML context, data is written into an HTML page as part of the content, for example inside a <code>&lt;p&gt;</code> tag.  Examples include a search results page, a blog commenting system, dictionary.com's word of the day, etc.  In this context, all HTML meta characters need to be encoded or stripped.  That's primarily <code>&lt;</code> and <code>&gt;</code>, but using PHP's <code>FILTER_SANITIZE_SPECIAL_CHARS</code> is probably safer, and <code>FILTER_SANITIZE_STRIPPED</code> is probably the safest.  Make sure you know what character set your data is in before you try to encode it.

There may be cases when you want to allow some HTML tags, for example in a <abbr title="Content Management System">CMS</abbr> tool or a commenting system.  This is generally a bad idea because there are more ways to get it wrong than to get it right.  For example, let's say that your blogging system allows commenters to markup their comments with some simple tags like <code>&lt;q&gt;</code> and <code>&lt;em&gt;</code>.  Now a happy commenter comes along and adds the following code to his comment:

<pre><code class="language-markup tmp-xml">&lt;q onmouseover="alert('xss')"&gt;...&lt;/q&gt;</code></pre>

You've just been XSSed.  If you are going to allow a subset of tags, then strip all attributes from those tags.  A better idea is to use a CMS specific syntax like <a href="https://bbcode.org/">BBCode</a> that your back end can translate into safe tags.</p>

### Attribute Context

In attribute context, user data is included as the attribute value of an HTML tag.  Depending on the attribute in question, the context might be different.  For non-event handlers, all HTML meta characters need to be encoded.  <code>FILTER_SANITIZE_SPECIAL_CHARS</code> works here as well.  In addition, all attribute values should be quoted using single or double quotes or you'll be hit like the examples above.

For event handling attributes like <code>onmouseover</code>, <code>onclick</code>, <code>onfocus</code>, <code>onblur</code> or similar, you need to be more careful.  The best advice is to never ever put input data directly into an event handler.  Let's look at an example.

<pre><code class="language-php">&lt;?php
  $n = filter_input(INPUT_GET, 'n', FILTER_SANITIZE_SPECIAL_CHARS);
?&gt;
&lt;input type="text" value="" name="n" onfocus="do_something('&lt;?php echo $n; ?&gt;');"&gt;</code></pre>

Looks safe, doesn't it? What happens if an attacker tries to get out of the quoted region using a single quote, i.e., they use a URL like

<pre><code class="language-markup tmp-xml">https://servername/?n=foo');alert('xss</code></pre>

The input is sanitized and all single quotes are converted to <code>&#039;</code>.  Unfortunately, this isn't enough.  An event handler executes in two contexts one after the other.  The data in the page is first HTML decoded and the result is passed into a JavaScript context.  So, as far as the JavaScript handler is concerned, <code>'</code> and <code>&#039;</code> are exactly the same and this introduces an XSS hole.

The best thing to do is to <strong>never pass input data directly into an event handler</strong> &mdash; even if it has been treated.  It's better to store it as a the value of a hidden field and then let your handler pull the value out of that field.  Something like this would be safer:

<pre><code class="language-php">&lt;?php
  $n = filter_input(INPUT_GET, 'n', FILTER_SANITIZE_SPECIAL_CHARS);
?&gt;
&lt;input type="hidden" id="old_n" value="&lt;?php echo $n ?&gt;"&gt;
&lt;input type="text" value="" name="n" onfocus="do_something(document.getElementById('old_n').value);"&gt;</code></pre>

### URL Context

A special case of the attribute context is URL context.  The value of the <code>href</code> and <code>src</code> attributes of various elements are URLs and need to be treated as such.  Special characters included in a URL need to be <em>urlencoded</em> to be safe in this context.  Using an HTML specific filter is insufficient here as we've seen in the missing quotes example above.

Also take note of URLs in <code>meta</code> tags and in HTTP headers.  For example, code similar to the following was also recently seen online:

<pre><code class="language-php">&lt;?php
  if(preg_match('!^https?://(w+).mysite.com/!', $_GET['done']) {
      header("Location: " . $_GET['done']);
  }
?&gt;</code></pre>

On the face of it, it looks safe enough since we're checking that the <em>done</em> parameter matches our domain before we redirect, however we aren't validating the entire URL.  An attacker could easily slip in a newline character and then add more headers, for example, a second Location header, or an entire HTML document for that matter.  All it takes is a little <code>%0a</code> in the <em>done</em> parameter.

Notice that the match uses a <code>/</code> after <code>.com</code>.  This is necessary to protect against user@host style URLs or third party subdomains.  For example, a malicious user could create a subdomain called <code>www.mysite.com.evil.com</code> and trick your regex.  Alternately, they could use a URL like <code>https://www.mysite.com@www.evil.com/</code> and trick your regex.

If your URL contains only ASCII characters, then PHP's <a href="https://www.php.net/manual/en/filter.filters.validate.php">FILTER_VALIDATE_URL</a> filter can be used instead of funky regular expressions.

Remember: when writing out URLs, the <code>&amp;</code> character is special in HTML, so it needs to be written out as <code>&amp;amp;</code> (although most browsers will accept it if you don't), while the <code>;</code> character is special in an HTTP header, meaning that <code>&amp;amp;</code> will break the header.

When dealing with URLs, figure out which context the URL will be used in, encode it correctly and possibly check the domain.  When checking the domain, make sure you use a starts-with match, and include the trailing <code>/</code> to protect against user@host style URLs.</p>

### JavaScript Context

If input data needs to be written out in a JavaScript context, i.e., within &lt;script&gt; tags or in a file served as the <code>src</code> attribute of a &lt;script&gt; tag, the data should be JSON encoded. In PHP, the <code><a href="https://www.php.net/json_encode">json_encode</a></code> function can be used.  The <a href="https://json.org/">JSON homepage</a> has a list of JSON libraries for many other languages, all of which have a similar function.

Simply escaping quotes using <a href="https://www.php.net/manual/en/function.addslashes.php">addslashes</a> or something similar is insufficient, because within script tags quotes can also be represented by their HTML entity values.

One special case to think about in the JavaScript context is the use of web services that return <a href="https://json-p.org/">JSON-P</a> data.  You do this on your web page by including a script tag that points to a web service and specify a callback function to be called when the data is loaded.  For example, to load public photos from Flickr, you'd use something like this:

<pre><code class="language-markup tmp-xml">&lt;script src="https://api.flickr.com/services/feeds/photos_public.gne?format=json&amp;jsoncallback=myfunc"&gt;&lt;/script&gt;</code></pre>

Before you do that, you'd define <code>myfunc</code> in JavaScript.  However, what you're doing is giving the script from Flickr full access to your page's DOM.  As long as the script respects its contract with you (i.e., the API), you should be safe, but if whoever controlled that script were to suddenly turn evil, you've just opened your users up to attack.

In general, only point your scripts tags to URLs that you fully trust, both to not be evil and also to never be compromised themselves.  If you must include untrusted scripts, consider sandboxing them in an iframe or use <a href="https://en.wikipedia.org/wiki/Caja_%28programming_language%29">Caja</a> if you can.  If you do use an iframe, then consider that there may be certain conditions under which you need to use a double-iframe.  This is primarily done to prevent referrer leaking if your page's URL itself is secret, like a search results page or a <a href="https://en.wikipedia.org/wiki/Capability-based_security">capability</a> URL.</p>

### CSS Context

Internet Explorer is the only major browser around that allows script execution within CSS using the <code><a href="https://msdn.microsoft.com/en-us/library/ms537634%28VS.85%29.aspx">expression</a></code> syntax (deprecated and no longer supported in IE8 and later).  However, that's still reason enough to worry about it.  As an example, consider a website that allows users to customize the background of their profile pages, similar to MySpace or Twitter (note that neither website is vulnerable to this flaw).  Let's say that you accept a background color and/or image and assign that to the CSS <code>background</code> property.  If you don't correctly validate and sanitize the values passed in by the user, they could pass in a JavaScript expression instead of a real color.  This might result in CSS code like this:

<pre><code class="language-css">background: #28d expression("alert('xss')");</code></pre>

Making sure the background color the user specifies is a valid CSS color and nothing else will protect you from this kind of an attack.

With URLs, a different issue may come in to play.  Let's say that you allow the user to specify their own background image URL.  You validate this URL when the user specifies it &mdash; to make sure it doesn't return a 404 error. After this is done, the user could replace the URL with a script that returns a 401 HTTP status code.  This makes the browser throw up an authentication dialog, which might confuse the user into entering their username and password of your site.  An interesting attack that we haven't seen outside of the lab.

The fix is to download the specified image to your own server <em>and</em> run some kind of transformation on it, most commonly for size.  Even if your transformation does nothing, it can still remove <a href="https://www.microsoft.com/security/portal/Threat/Encyclopedia/Entry.aspx?Name=Exploit%3aWin32%2fMS04028!jpeg">malware that may be embedded in a JPEG</a>.</p>

### Other Contexts

There are other contexts that we don't look at in this article.  These commonly deal with the back end and include things like an SQL context or a Shell context or a back end web service context.  Another interesting attack that results from improper input validation is <a href="https://blog.mindedsecurity.com/2009/05/client-side-http-parameter-pollution.html">HTTP Parameter Pollution</a> or <em>HPP</em> for short.</p>

## Should you filter on input or output?

The comments of my last article brought up an interesting point regarding whether data should be filtered on input or output.  Since we have so many different contexts, it seems obvious that data should be filtered just before output depending on the context.  Filtering for the wrong context could still introduce vulnerabilities.  This is the ideal case where every programmer on your team knows what they are doing at all times and always programs with security in mind.  In practice, this doesn't always happen.  Even experienced programmers have been known to slip up once or twice, and it's those occasions that come back to bite you.

A simple guideline is to strip out all punctuation by default and let the web developer override this based on context.  This means that using untreated input will either be safe, or not work at all, which serves as a reminder to the developer that they need to think about context.  We encourage developers to validate data on input.  This involves checking data types, ranges, lengths and possibly the character set/encoding in use.  The purpose of validation is to make sure that we receive what we expect to receive.  Data should be further sanitized on output depending on context.  Sanitization involves transforming (possibly destructively) the data to be safe in the output context.  Remember that sometimes a single piece of data may be used in multiple contexts on the same page.

Both validation and sanitization are types of filters to be run on input data, and often both might be required.</p>

## In closing

No data that comes in from an untrusted source should be trusted.  This would include anything that you did not create yourself.  The data may come in as command line parameters, through a query string, through POST data, cookies, HTTP headers, a web service call, an uploaded file, or anything else.  If you did not create it, then it can't be trusted.  <strong>Validate all data to make sure it's what you expect</strong>, and then treat it to make sure it's safe in the context where it will be used.  Be aware of the different contexts within a web page and keep your users safe.</p>

## References

1.  [Cablegate security vulnerability](https://kilimanjaro.dk/blog/?p=228)
2.  [XSS on ICICIDirect](https://tech.bluesmoon.info/2011/01/fixing-xss-on-icicidirectcom.html)
3.  [Cross site scripting in CSS](https://stackoverflow.com/questions/3607894/cross-site-scripting-in-css-stylesheets)
4.  [PHP's input validation and sanitization filters](https://www.php.net/manual/en/filter.filters.php)
5.  [The Caja Project](https://code.google.com/p/google-caja/)
6.  [Capability based security](https://en.wikipedia.org/wiki/Capability-based_security)
7.  [HTTP Parameter Pollution](https://seclists.org/bugtraq/2010/Dec/56)
8.  [HTTP 4xx status codes](https://en.wikipedia.org/wiki/List_of_HTTP_status_codes#4xx_Client_Error)
9.  [JPEG exploit beats antivirus software](https://news.cnet.com/JPEG-exploit-could-beat-antivirus-software/2100-7349_3-5388633.html)

## Related Posts

You might be interested in the following related posts:

*   [Common Security Mistakes in Web Applications](https://www.smashingmagazine.com/2010/10/18/common-security-mistakes-in-web-applications/)
*   [Web Security: Are You Part Of The Problem?](https://www.smashingmagazine.com/2010/01/14/web-security-primer-are-you-part-of-the-problem/)
*   [10 Useful WordPress Security Tweaks](https://www.smashingmagazine.com/2010/07/01/10-useful-wordpress-security-tweaks/)

{{< signature "vf" >}}

