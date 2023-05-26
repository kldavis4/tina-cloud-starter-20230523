---
title: Introduction To URL Rewriting
slug: introduction-to-url-rewriting
image: null
date: 2011-11-02T11:19:05.000Z
author: paul-tero
description: >-
  Many Web companies spend hours and hours **agonizing over the best domain names for their clients**. They try to find a domain name that is relevant and appropriate, sounds professional yet is distinctive, is easy to spell and remember and read over the phone, looks good on business cards and is available as a dot-com.
categories:
  - Coding
  - PHP
  - Techniques
  - URL
---
Or else they spend thousands of dollars to purchase the one they really want, which just happened to be registered by a forward-thinking and hard-to-find squatter in 1998.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Essential Guide To Regular Expressions: Tools and Tutorials](https://www.smashingmagazine.com/2009/06/essential-guide-to-regular-expressions-tools-tutorials-and-resources/)
*   [Technical SEO 2015: Wiring Websites for Organic Search](https://www.smashingmagazine.com/2015/11/technical-seo-2015-wiring-websites-organic-search/)
*   [Crucial Concepts Behind Advanced Regular Expressions](https://www.smashingmagazine.com/2009/05/introduction-to-advanced-regular-expressions/)
*   [<span class="headline">Obscure Back-End Techniques And Terminal Secrets</span>](https://www.smashingmagazine.com/2013/07/how-to-fix-the-web-obscure-back-end-techniques-and-terminal-secrets/)

They go through all that trouble with the domain name but neglect the rest of the URL, the element <em>after</em> the domain name. It, too, should be relevant, appropriate, professional, memorable, easy to spell and readable. And for the same reasons: to attract customers and improve in search ranking.

{{% feature-panel %}}

Fortunately, there is a technique called URL rewriting that can turn unsightly URLs into nice ones — with a lot less agony and expense than picking a good domain name. It enables you to fill out your URLs with friendly, readable keywords without affecting the underlying structure of your pages.

This article covers the following:

1.  What is URL rewriting?
2.  How can URL rewriting help your search rankings?
3.  Examples of URL rewriting, including regular expressions, flags and conditionals;
4.  URL rewriting in the wild, such as on Wikipedia, WordPress and shopping websites;
5.  Creating friendly URLs;
6.  Changing pages names and URLs;
7.  Checklist and troubleshooting.</p>

## What Is URL Rewriting?

If you were writing a letter to your bank, you would probably open your word processor and create a file named something like <code>lettertobank.doc</code>. The file might sit in your <code>Documents</code> directory, with a full path like <code>C:WindowsusersjulieDocumentslettertobank.doc</code>. One file path = one document.

Similarly, if you were creating a banking website, you might create a page named <code>page1.html</code>, upload it, and then point your browser to <code></code>. One URL = one resource. In this case, the resource is a physical Web page, but it could be a page or product drawn from a CMS.

URL rewriting changes all that. It allows you to completely separate the URL from the resource. With URL rewriting, you could have <code></code> taking the user to <code>…/page1.html</code> or to <code>…/about-us/</code> or to <code>…/about-this-website-and-me/</code> or to <code>…/youll-never-find-out-about-me-hahaha-Xy2834/</code>. Or to all of these. It’s a bit like shortcuts or symbolic links on your hard drive. One URL = one way to find a resource.

With URL rewriting, the URL and the resource that it leads to can be completely independent of each other. In practice, they’re usually not wholly independent: the URL usually contains some code or number or name that enables the CMS to look up the resource. But in theory, this is what URL rewriting provides: a complete separation.</p>

## How Does URL Rewriting Help?

Can you guess what this Web page sells?

B&amp;Q went to all the trouble and expense of acquiring <code>diy.com</code> and implementing a stock controlled e-commerce website, but left its URLs indecipherable. If you guessed “brown guttering,” you might want to considering playing the lottery.

Even when you search directly for this “miniflow gutter brown” on Google UK, B&amp;Q’s page comes up only seventh in the organic search results, below much smaller companies, such as a building supplier with a single outlet in Stirlingshire. B&amp;Q has 300+ branches and so is probably much bigger in budget, size and exposure, so why is it not doing as well for this search term? Perhaps because the other search results have URLs like <code>https://www.prof…co.uk/products/<strong>brown-miniflo-gutter</strong>-148/</code>; that is, the URL itself contains the words in the search term.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/40aec199-2235-4849-a6c4-7d6f93e9e876/miniflow-gutter-results2.png" alt="url rewriting" width="500" height="440" />

<em>Almost all of these results on Google have the search term in their URLs (highlighted in green). The one at the bottom does not.</em>

Looking at the URL from B&amp;Q, you would (probably correctly) assume that a file named <code>nav.jsp</code> within the directory <code>/diy/jsp/bq/</code> is used to display products when given their ID number, <code>11577676</code> in this case. That is the resource intimately tied to this URL.

So, how would B&amp;Q go about turning this into something more recognizable, like <code></code>, without restructuring its whole website? The answer is URL rewriting.

Another way to look at URL rewriting is like a thin layer that sits on top of a website, translating human- and search-engine-friendly URLs into actual URLs. Doing it is easy because it requires hardly any changes to the website’s underlying structure — no moving files around or renaming things.

URL rewriting basically tells the Web server that
<code>/products/miniflow-gutter-brown/11577676</code> should show the Web page at: <code>/diy/jsp/bq/nav.jsp?action=detail&amp;fh_secondid=11577676</code>,
without the customer or search engine knowing about it.

Many factors (or “signals”), of course, determine the search ranking for a particular term, over 200 of them according to Google. But friendly and readable URLs are <a href="https://searchengineland.com/21-essential-seo-tips-techniques-11580">consistently ranked as one of the most important</a> of those factors. They also help humans to quickly figure out what a page is about.

The next section describes how this is done.</p>

## How To Rewrite URLs

Whether you can implement URL rewriting on a website depends on the Web server. Apache usually comes with the URL rewriting module, <code>mod_rewrite</code>, already installed. The set-up is very common and is the basis for all of the examples in this article. <a href="https://www.isapirewrite.com/">ISAPI Rewrite</a> is a similar module for Windows IIS but requires payment (about $100 US) and installation.</p>

### The Simplest Case

The simplest case of URL rewriting is to rename a single static Web page, and this is far easier than the B&amp;Q example above. To use Apache’s URL rewriting function, you will need to create or edit the <em>.htaccess</em> file in your website’s document root (or, less commonly, in a subdirectory).

For instance, if you have a Web page about horses named <em>Xu8JuefAtua.htm</em>, you could add these lines to <em>.htaccess</em>:

<pre><code class="language-markup tmp-none">RewriteEngine On
RewriteRule   horses.htm   Xu8JuefAtua.htm</code></pre>

Now, if you visit <code></code>, you’ll actually be shown the Web page <code>Xu8JuefAtua.htm</code>. Furthermore, your browser will remain at <code>horses.htm</code>, so visitors and search engines will never know that you originally gave the page such a cryptic name.</p>

### Introducing Regular Expressions

In URL rewriting, you need only match the <strong>path</strong> of the URL, not including the domain name or the first slash. The rule above essentially tells Apache that if the path contains <code>horses.htm</code>, then show the Web page <code>Xu8JuefAtua.htm</code>. This is slightly problematic, because you could also visit <code><strong>reallyfast</strong>horses.htm<strong>l</strong></code>, and it would still work. So, what we really need is this:

<pre><code class="language-markup tmp-none">RewriteEngine On
RewriteRule   ^horses.htm$   Xu8JuefAtua.htm</code></pre>

The <code>^horses.htm$</code> is not just a search string, but a <a href="https://httpd.apache.org/docs/current/rewrite/intro.html#regex">regular expression</a>, in which special characters — such as <code>^ . + * ? ^ ( ) [ ] { }</code> and <code>$</code> — have extra significance. The <code>^</code> matches the beginning of the URL’s path, and the <code>$</code> matches the end. This says that the path must <strong>begin and end</strong> with <code>horses.htm</code>. So, only <code>horses.htm</code> will work, and not <code><strong>really</strong>fasthorses.htm</code> or <code>horses.htm<strong>l</strong></code>. This is important for search engines like Google, which can penalize what it views as <a href="https://www.google.com/support/webmasters/bin/answer.py?answer=66359&amp;&amp;hl=en">duplicate content</a> — identical pages that can be reached via multiple URLs.</p>

### Without File Endings

You can make this even better by ditching the file ending altogether, so that you can visit either <code></code> or <code></code>:

<pre><code class="language-markup tmp-none">RewriteEngine On
RewriteRule   ^horses/?$   Xu8JuefAtua.html  [NC]</code></pre>

The <code>?</code> indicates that the preceding character is optional. So, in this case, the URL would work with or without the slash at the end. These would not be considered duplicate URLs by a search engine, but would help prevent confusion if people (or link checkers) accidentally added a slash. The stuff in brackets at the end of the rule gives Apache some further pointers. <code>[NC]</code> is a flag that means that the rule is case insensitive, so <code></code> would also work.</p>

### Wikipedia Example

We can now look at a real-world example. Wikipedia appears to use URL rewriting, passing the title of the page to a PHP file. For instance…
<blockquote><code>https://en.wikipedia.org/wiki/Barack_obama</code>

&nbsp;</blockquote>

… is rewritten to:
<blockquote><code>https://en.wikipedia.org/w/index.php?title=Barack_obama</code></blockquote>

This could well be implemented with an <em>.htaccess</em> file, like so:

<pre><code class="language-markup tmp-none">RewriteEngine On
#Look for the word "wiki" followed by a slash, and then the article title
RewriteRule   ^wiki/(.+)$   w/index.php?title=$1   [L]</code></pre>

The previous rule had <code>/?</code>, which meant <strong>zero or one</strong> slashes. If it had said <code>/+</code>, it would have meant <strong>one or more</strong> slashes, so even <code></code> would have worked. In this rule, the dot (<code>.</code>) matches <strong>any character</strong>, so <code>.+</code> matches one or more of any character — that is, essentially anything. And the parentheses — <code>( )</code> — ask Apache to remember what the <code>.+</code> is. The rule above, then, tells Apache to look for <code>wiki/</code> followed by one or more of any character and to remember what it is. This is remembered and then rewritten as <code>$1</code>. So, when the rewriting is finished, <code>wiki/<strong>Barack_obama</strong></code> becomes <code>w/index.php?title=<strong>Barack_obama</strong></code>

Thus, the page <code>w/index.php</code> is called, passing <code>Barack_obama</code> as a parameter. The <code>w/index.php</code> is probably a PHP page that runs a database lookup — like <code>SELECT * FROM articles WHERE title='Barack obama'</code> — and then outputs the HTML.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ac912e5b-987e-44ee-a44f-fbe2e28b6e12/wikipedia-barack-short.png" alt="url rewriting" width="500" height="334" />

<em>You can also view Wikipedia entries directly, without the URL rewriting.</em>

### Comments and Flags

The example above also introduced comments. Anything after a <code>#</code> is ignored by Apache, so it’s a good idea to explain your rewriting rules so that future generations can understand them. The <code>[L]</code> flag means that if this rule matches, Apache can stop now. Otherwise, Apache would continue applying subsequent rules, which is a powerful feature but unnecessary for all but the most complex rule sets.</p>

### Implementing the B&Q Example

The recommendation for B&amp;Q above could be implemented with an <em>.htaccess</em> file, like so:

<pre><code class="language-markup tmp-none">RewriteEngine On
#Look for the word "products" followed by slash, product title, slash, id number
RewriteRule  ^products/.*/([0-9]+)$   diy/jsp/bq/nav.jsp?action=detail&amp;fh_secondid=$1 [NC,L]</code></pre>

Here, the <code>.*</code> matches <strong>zero or more of any character</strong>, so nothing or anything. And the <code>[0-9]</code> matches a single numerical digit, so <code>[0-9]+</code> matches <strong>one or more numbers</strong>.

The next section covers a couple of more complex conditional examples. You can also read the <a href="https://httpd.apache.org/docs/current/rewrite/intro.html">Apache rewriting guide</a> for much more information on all that URL rewriting has to offer.</p>

## Conditional Rewriting

URL rewriting can also include conditions and make use of environment variables. These two features make for an easy way to redirect requests from one domain alias to another. This is especially useful if a website changes its domain, from <code>mywebsite.co.uk</code> to <code>mywebsite.com</code> for example.</p>

### Domain Forwarding

Most domain registrars allow for domain forwarding, which redirects all requests from one domain to another domain, but which might send requests for <code>www.mywebsite.co.uk/horses</code> to the home page at <code>www.mywebsite.com</code> and not to <code>www.mywebsite.com/horses</code>. You can achieve this with URL rewriting instead:

<pre><code class="language-markup tmp-none">RewriteEngine On
RewriteCond   %{HTTP_HOST}   !^www.mywebsite.com$         [NC]
RewriteRule   (.*)           https://www.mywebsite.com/$1  [L,R=301]</code></pre>

The second line in this example is a <code>RewriteCond</code>, rather than a <code>RewriteRule</code>. It is used to compare an Apache environment variable on the left (such as the host name in this case) with a regular expression on the right. Only if this condition is true will the rule on the next line be considered.

In this case, <code>%{HTTP_HOST}</code> represents <code>www.mywebsite.co.uk</code>, the host (i.e. domain) that the browser is trying to visit. The <code>!</code> means “not.” This tells Apache, if the host does not begin and end with <code>www.mywebsite.com</code>, then remember and rewrite zero or more of any character to <code>www.mywebsite.com/$1</code>. This converts <code>www.mywebsite.co.uk/anything-at-all</code> to <code>www.mywebsite.com/anything-at-all</code>. And it will work for all other aliases as well, like <code>www.mywebsite.biz/anything-at-all</code> and <code>mywebsite.com/anything-at-all</code>.

The flag <code>[R=301]</code> is very important. It tells Apache to do a 301 (i.e. permanent) redirect. Apache will send the new URL back to the browser or search engine, and the browser or search engine will have to request it again. Unlike all of the examples above, the new URL will now appear in the browser’s location bar. And search engines will take note of the new URL and update their databases. <code>[R]</code> by itself is the same as <code>[R=302]</code> and signifies a temporary redirect.</p>

### File Existence and WordPress

Smashing Magazine runs on the popular blogging software WordPress. WordPress enables the author to choose their own URL, called a “slug.” Then, it automatically prepends the date, such as <code>https://www.smashingmagazine.com/2011/09/05/getting-started-with-the-paypal-api/</code>. In your pre-URL rewriting days, you might have assumed that Smashing Magazine’s Web server was actually serving up a file located at <code>…/2011/09/05/getting-started-with-the-paypal-api/index.html</code>. In fact, WordPress uses URL rewriting extensively.

<img style="border: 1px solid #CCC;" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6676c5d6-afac-402e-9b3d-c6dc78cbc260/wordpress-slug.png" alt="screenshot" width="500" height="107" />

<em>WordPress enables the author to choose their own URL for an article.</em>

WordPress’ <em>.htaccess</em> file looks like this:

<pre><code class="language-markup tmp-none">RewriteEngine On
RewriteBase /  
RewriteCond %{REQUEST_FILENAME} !-f
RewriteCond %{REQUEST_FILENAME} !-d
RewriteRule . /index.php [L]</code></pre>

The <code>-f</code> means “this is a file” and <code>-d</code> means “this is a directory.” This tells Apache, if the requested file name is <strong>not a file</strong>, and the requested file name is <strong>not a directory</strong>, then rewrite everything (i.e. any path containing any character) to the page <em>index.php</em>. If you are requesting an existing image or the log-in page <em>wp-login.php</em>, then the rule is not triggered. But if you request anything else, like <code>/2011/09/05/getting-started-with-the-paypal-api/</code>, then the file <em>index.php</em> jumps into action.

Internally, <em>index.php</em> (probably) looks at the environment variable <code>$_SERVER['REQUEST_URI']</code> and extracts the information that it needs to find out what it is looking for. This gives it even more flexibility than Apache’s rewrite rules and enables WordPress to mimic some very sophisticated URL rewriting rules. In fact, when administering a WordPress blog, you can go to Settings → Permalink on the left side, and choose the type of URL rewriting that you would like to mimic.

<img style="border: 1px solid #CCC;" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9db1d9b7-3be7-4bea-b639-6e73e301a00a/wordpress-permalink.png" alt="screenshot" width="500" height="219" />

<em>WordPress’ permalink settings, letting you choose the type of URL rewriting that you would like to mimic.</em>

### Rewriting Query Strings

If you are hired to recreate an existing website from scratch, you might use URL rewriting to redirect the 20 most popular URLs on the old website to the locations on the new website. This could involve redirecting things like <code>prod.php?id=20</code> to <code>products/great-product/2342</code>, which itself gets redirected to the actual product page.

Apache’s <code>RewriteRule</code> applies only to the path in the URL, not to parameters like <code>id=20</code>. To do this type of rewriting, you will need to refer to the Apache environment variable <code>%{QUERY_STRING}</code>. This can be accomplished like so:

<pre><code class="language-markup tmp-none">RewriteEngine On
RewriteCond   %{QUERY_STRING}           ^id=20$                   
RewriteRule   ^prod.php$             ^products/great-product/2342$      [L,R=301]
RewriteRule   ^products/(.*)/([0-9]+)$  ^productview.php?id=$1             [L]</code></pre>

In this example, the first <code>RewriteRule</code> triggers a permanent redirect from the old website’s URL to the new website’s URL. The second rule rewrites the new URL to the actual PHP page that displays the product.</p>

## Examples Of URL Rewriting On Shopping Websites

For complex content-managed websites, there is still the issue of how to map friendly URLs to underlying resources. The simple examples above did that mapping by hand, manually associating a URL like <code>horses.htm</code> with the file or resource <code>Xu8JuefAtua.htm</code>. Wikipedia looks up the resource based on the title, and WordPress applies some complex internal rule sets. But what if your data is more complex, with thousands of products in hundreds of categories? This section shows the approach that Amazon and many other shopping websites take.

If you’ve ever come across a URL like this on Amazon, <code>https://www.amazon.co.uk/High-Voltage-AC-DC/dp/B00008AJL3</code>, you might have assumed that Amazon’s website has a subdirectory named <code>/High-Voltage-AC-DC/dp/</code> that contains a file named <code>B00008AJL3</code>.

This is very unlikely. You could try changing the name of the top-level “directory” and you would still arrive on the same page, <code>https://www.amazon.co.uk/<strong>Test</strong>-Voltage-AC-DC/dp/B00008AJL3</code>.

The bit at the end is what really matters. Looking down the page, you’ll see that <code>B00008AJL3</code> is this AC/DC album’s ASIN (Amazon Standard Identification Number). If you change that, you’ll get a “Page not found” or an entirely different product: <code><strong>B003BEZ7HI</strong></code>.

The <code>/dp/</code> also matters. Changing this leads to a “Page not found.” So, the <code>B00008AJL3</code> probably tells Amazon what to display, and the <code>dp</code> tells the website how to display it. This is URL rewriting in action, with the original URL possibly ending up getting rewritten to something like:
<code>https://www.amazon.co.uk/<strong>d</strong>isplay<strong>p</strong>roduct.php?asin=<strong>B00008AJL3</strong></code>.</p>

### Features of an Amazon URL

This introduces some important features of Amazon’s URLs that can be applied to any website with a complex set of resources. It shows that the URL can be automatically generated and can include up to three parts:

1.  **The words** In this case, the words are based on the album and artist, and all non-alphanumeric characters are replaced. So, the slash in AC/DC becomes a hyphen. This is the bit that helps humans and search engines.
2.  **An ID number** Or something that tells the website what to look up, such as `B00008AJL3`.
3.  **An identifier** Or something that tells the website where to look for it and how to display it. If `dp` tells Amazon to look for a product, then somewhere along the line, it probably triggers a database statement such as `SELECT * FROM products WHERE id='B00008AJL3'`.</p>

### Other Shopping Examples

Many other shopping websites have URLs like this. In the list below, the ID number and (suspected) identifier are in bold:

*   `https://www.ebay.co.uk/**itm**/Ian-Rankin-Set-Darkness-Rebus-Novel-/**140604842997**`
*   `https://www.kelkoo.com/**c**-**138201**-lighting/brand/caravan`
*   `**5266430**_**3**`
*   `https://www.gumtree.com/**p**/for-sale/boys-bmx-bronx-blaze/**97669042**`
*   `**c**/Televisions/LCD-Plasma-LED-TVs/**1844**`

A significant benefit of this type of URL is that the actual words can be changed, as shown below. As long as the ID number stays the same, the URL will still work. So products can be renamed without breaking old links. More sophisticated websites (like Ciao above) will redirect the changed URL back to the real one and thus avoid creating the appearance of duplicate content (see below for more on this topic).

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/db681541-11c6-422e-9e08-43d10a0dfe3d/changed-url.png" alt="screenshot" width="500" />

<em>Websites that use URL rewriting are more flexible with their URLs — the words can change but the page will still be found.</em>

## Friendly URLs

Now you know how to map nice friendly URLs to their underlying Web pages, but how should you create those friendly URLs in the first place?

If we followed the current advice, we would separate words with hyphens <a href="https://www.mattcutts.com/blog/dashes-vs-underscores/">rather than underscores</a> and capitalize consistently. Lowercase might be preferable because most people search in lowercase. Punctuation such as dots and commas should also be turned into hyphens, otherwise they would get turned into things like <code>%2C</code>, which look ugly and might break the URL when copied and pasted. You might want to remove apostrophes and parentheses entirely for the same reason.

Whether to replace accented characters is debatable. URLs with accents (or any non-Roman characters) might look bad or break when rendered in a different character format. But replacing them with their non-accented equivalents might make the URLs harder for search engines to find (and even harder if replaced with hyphens). If your website is for a predominately French audience, then perhaps leave the French accents in. But substitute them if the French words are few and far between on a mainly English website.

This PHP function succinctly handles all of the above suggestions:

<pre><code class="language-markup tmp-none">function GenerateUrl ($s) {
  //Convert accented characters, and remove parentheses and apostrophes
  $from = explode (',', "ç,æ,œ,á,é,í,ó,ú,à,è,ì,ò,ù,ä,ë,ï,ö,ü,ÿ,â,ê,î,ô,û,å,e,i,ø,u,(,),[,],'");
  $to = explode (',', 'c,ae,oe,a,e,i,o,u,a,e,i,o,u,a,e,i,o,u,y,a,e,i,o,u,a,e,i,o,u,,,,,,');
  //Do the replacements, and convert all other non-alphanumeric characters to spaces
  $s = preg_replace ('~[^wd]+~', '-', str_replace ($from, $to, trim ($s)));
  //Remove a - at the beginning or end and make lowercase return strtolower (preg_replace ('/^-/', ’, preg_replace ('/-$/', ’, $s)));
}</code></pre>

This would generate URLs like this:

<pre><code class="language-markup tmp-none">echo GenerateUrl ("Pâtisserie (Always FRESH!)"); //returns "patisserie-always-fresh"</code></pre>

Or, if you wanted a link to a <code>$product</code> variable to be pulled from a database:

<pre><code class="language-markup tmp-none">$product = array ('title'=&gt;'Great product', 'id'=&gt;100);
echo '&lt;a href="' . GenerateUrl ($product['title']) . '/' . $product['id'] . '"&gt;';
echo $product['title'] . '&lt;/a&gt;';</code></pre>

## Changing Page Names

Search engines generally ignore <a href="https://www.google.com/support/webmasters/bin/answer.py?answer=66359&amp;&amp;hl=en">duplicate content</a> (i.e. multiple pages with the same information). But if they think they are being manipulated, search engines will actively penalize the website, so avoid this where possible. Google recommends using 301 redirects to send users from old pages to new ones.

When a URL-rewritten page is renamed, the old URL and new URL should both still work. Furthermore, to avoid any risk of duplication, the old URL should automatically redirect to the new one, as WordPress does.

Doing this in PHP is relatively easy. The following function looks at the current URL, and if it’s not the same as the desired URL, it redirects the user:

<pre><code class="language-markup tmp-none">function CheckUrl ($s) {
  // Get the current URL without the query string, with the initial slash
  $myurl = preg_replace ('/?.*$/', ’, $_SERVER['REQUEST_URI']);
  //If it is not the same as the desired URL, then redirect if ($myurl != "/$s") {Header ("Location: /$s", true, 301); exit;}
}</code></pre>

This would be used like so:

<pre><code class="language-markup tmp-none">$producturl = GenerateUrl ($product['title']) . '/' . $product['id'];
CheckUrl ($producturl); //redirects the user if they are at the wrong place</code></pre>

If you would like to use this function, be sure to test it in your environment first and with your rewrite rules, to make sure that it does not cause any infinite redirects. This is what that would look like:

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/69d8581a-69da-414b-8b9f-40d1e76b852b/redirect-loop1.png" alt="screenshot" width="500" />

<em>This is what happens when Google Chrome visits a page that redirects to itself.</em>

## Checklist And Troubleshooting

Use the following checklist to implement URL rewriting.</p>

### 1. Check That It’s Supported

Not all Web servers support URL rewriting. If you put up your <em>.htaccess</em> file on one that doesn’t, it will be ignored or will throw up a “500 Internal Server Error.”

### 2. Plan Your Approach

Figure out what will get mapped to what, and how the correct information will still get found. Perhaps you want to introduce new URLs, like <code>my-great-product/p/123</code>, to replace your current product URLs, like <code>product.php?id=123</code>, and to substitute <code>new-category/c/12</code> for <code>category.php?id=12</code>.</p>

### 3. Create Your Rewrite Rules

Create an <em>.htaccess</em> file for your new rules. You can initially do this in a <code>/testing/</code> subdirectory and using the <code>[R]</code> flag, so that you can see where things go:

<pre><code class="language-markup tmp-none">RewriteEngine On
RewriteRule   ^.+/p/([0-9]+)   product.php?id=$1    [NC,L,R]
RewriteRule   ^.+/c/([0-9]+)   category.php?id=$1    [NC,L,R]</code></pre>

Now, if you visit <code>www.mywebsite.com/testing/my-great-product/p/123</code>, you should be sent to <code>www.mywebsite.com/testing/product.php?id=123</code>. You’ll get a “Page not found” because <em>product.php</em> is not in your <code>/testing/</code> subdirectory, but at least you’ll know that your rules work. Once you’re satisfied, move the <em>.htaccess</em> file to your document root and remove the <code>[R]</code> flag. Now <code>www.mywebsite.com/my-great-product/p/123</code> should work.</p>

### 4. Check Your Pages

Test that your new URLs bring in all the correct images, CSS and JavaScript files. For example, the Web browser now believes that your Web page is named <code>123</code> in a directory named <code>my-great-product/p/</code>. If the HTML refers to a file named <code>images/logo.jpg</code>, then the Web browser would request the image from <code>www.mywebsite.com/my-great-product/p/images/logo.jpg</code> and would come up with a “File not found.”

You would need to also rewrite the image locations or make the references absolute (like <code>&lt;img src="<strong>/</strong>images/logo.jpg"/&gt;</code>) or put a base <code>href</code> at the top of the <code>&lt;head&gt;</code> of the page (<code>&lt;base href="/product.php"/&gt;</code>). But if you do that, you would need to fully specify any internal links that begin with <code>#</code> or <code>?</code> because they would now go to something like <code>product.php#details</code>.</p>

### 5. Change Your URLs

Now find all references to your old URLs, and replace them with your new URLs, using a function such as <code>GenerateUrl</code> to consistently create the new URLs. This is the only step that might require looking deep into the underlying code of your website.</p>

### 6. Automatically Redirect Your Old URLs

Now that the URL rewriting is in place, you probably want Google to forget about your old URLs and start using the new ones. That is, when a search result brings up <code>product.php?id=20</code>, you’d want the user to be <em>visibly</em> redirected to <code>my-great-product/p/123</code>, which would then be <em>internally</em> redirected back to <code>product.php?id=20</code>.

This is the reverse of what your URL rewriting already does. In fact, you could add another rule to <em>.htaccess</em> to achieve this, but if you get the rules in the wrong order, then the browser would go into a redirect loop.

Another approach is to do the first redirect in PHP, using something like the <code>CheckUrl</code> function above. This has the added advantage that if you rename the product, the old URL will immediately become invalid and redirect to the newest one.</p>

### 7. Update and Resubmit Your Site Map

Make sure to carry through your new URLs to your site map, your product feeds and everywhere else they appear.</p>

## Conclusion

URL rewriting is a relatively quick and easy way to improve your website’s appeal to customers and search engines. We’ve tried to explain some real examples of URL rewriting and to provide the technical details for implementing it on your own website. Please leave any comments or suggestions below.

{{< signature "al" >}}

