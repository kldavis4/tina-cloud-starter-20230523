---
title: Using HTML5 To Transform WordPress’ TwentyTen Theme
slug: using-html5-to-transform-wordpress-twentyten-theme
image: null
date: 2011-02-22T13:35:12.000Z
author: richard-shepherd
description: >-
  Last year, WordPress launched arguably its biggest update ever: WordPress 3.0\. Accompanying this release was the brand new default theme, TwentyTen, and the promise of a new default theme every year.
categories:
  - WordPress
  - Themes
  - Tutorials
  - Techniques (WP)
---
Somewhat surprisingly, TwentyTen declares the HTML5 doctype but doesn’t take advantage of many of the new elements and attributes that HTML5 brings.

Now, HTML5 does many things, but you can’t just add <code>&lt;!doctype html&gt;</code> to the top of a document and get excited that you’re <em>so</em> 2011. Mark-up, as they say, is meaning, and HTML5 brings a whole bunch of meaning to our documents.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Coding An HTML 5 Layout From Scratch](https://www.smashingmagazine.com/2009/08/designing-a-html-5-layout-from-scratch/)
*   [HTML 5 Cheat Sheet (PDF)](https://www.smashingmagazine.com/2009/07/html-5-cheat-sheet-pdf/)
*   [What To Consider When Choosing WordPress Themes](https://www.smashingmagazine.com/2014/12/what-to-consider-when-choosing-a-wordpress-theme/)
*   [Are You Getting Cheated When Buying A WordPress Theme?](https://www.smashingmagazine.com/2015/11/ripped-off-buying-wordpress-themes/)

{{% feature-panel %}}

In survey by Smashing Magazine, only 37% of voters said they use HTML5. This is depressing reading. Perhaps developers and designers are scared off by cross-browser incompatibility and the chore of learning new mark-up. The truth is that with a pinch of JavaScript, HTML5 can be used safely today across all browsers, back to IE6.

TwentyTen is a fine theme that already validates as HTML5; but in order to cater to users without JavaScript, it has to forgo a large chunk of HTML5 elements. The reason? Our old friend Internet Explorer doesn’t support most of them prior to version 9.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/70f958c2-d264-4932-9f51-ea6eec1bfa3f/twentytendefault.jpg"><img class="88016" title="TwentyTenDefault" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/70f958c2-d264-4932-9f51-ea6eec1bfa3f/twentytendefault.jpg" alt="Screenshot" width="550" height="400" /></a><br>
<em>The default TwentyTen WordPress Theme.</em>

For example, you’ve probably already heard of the <code>&lt;section&gt;</code> and <code>&lt;article&gt;</code> tags, both of which are champing at the bit to be embedded in a WordPress template. But to use these HTML5 elements in IE8 (and its predecessors), you need JavaScript in order to create them in the DOM. If you don’t have JavaScript, then the elements can’t be styled with CSS. Turn off JavaScript and you turn off the styling for these elements; invariably, this will break the formatting of your page.

I assume that WordPress decided to exclude these problematic tags so that its default theme would be supported by all browsers — not just those with JavaScript turned on.

While I understand this decision, I also think it’s a mistake. Three core technologies make the Web work: HTML, CSS and JavaScript. All desktop browsers support them (to some degree), so if any one of them off is disabled the user will have to expect a degraded experience. JavaScript is now fundamental to the user experience and while we should support users who turn off JavaScript, or have it turned off for them and have no chance to turn it on again as they don't have the right to do so, I question just <em>how far</em> we should support them.</p>

### Why Using JavaScript Makes Sense

Yahoo gives compelling evidence that less than 1.5% of its users turn off JavaScript. My own research into this, ably assisted by Greig Daines at eConversions, puts the figure below 0.5% (based on millions of visitors to a UK retail website).

Whilst it's true that JavaScript <em>should</em> be separated from a site's content, design and structure the reality is no longer black and white. I strongly believe that the benefits and opportunities HTML5 brings, together with related technologies such as CSS3 and media queries (both of which sometimes rely on JavaScript for cross-browser compatibility), is more than enough reason to use JavaScript to 'force' new elements to work in Internet Explorer. I am a passionate advocate for standards-based design that doesn't rely on JavaScript; HTML5 is the one structural exception.

Yes, we should respect a user's decision to deactivate JavaScript in their browser. However, I don't believe that this is a good enough reason for not using modern technologies, which would provide the vast majority of users with a richer user experience. After all, in the TwentyTen example, if the theme had HTML5 tags in it, everything would look fine in modern browsers (latest versions of Safari, Firefox, Opera, Chrome and IE9), with or without JavaScript.

If the browser is IE6 – IE8, and JavaScript is turned off, then users would see the content but it will not be styled correctly. If the content would not be displayed at all, we'd have a completely different discussion. If you are still not convinced, I will briefly discuss another option for those who <em>absolutely must</em> support users with JavaScript turned off.

To make TwentyTen play fair with IE, I suggest <a href="https://remysharp.com/2009/01/07/html5-enabling-script/">Remy Sharp’s HTML5 shim</a> or, if you want to sink your teeth into CSS3, <a href="https://www.modernizr.com/">Modernizr</a>. Modernizr not only adds support for HTML5 elements in IE but also tells you which CSS3 properties are supported by the user’s browser by adding special classes to the <code>&lt;html&gt;</code> element.

<img class="88243" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8fd65575-c9ca-470a-97ff-a297e0b1ed72/mordernizr.jpg" alt="Screenshot" width="550" height="355" /><br>
<em>Mordernizr.js</em>

So, let’s assume you’ve rightly banished non-JavaScript users with a polite message in a <code>&lt;noscript&gt;</code> tag. We can now start tinkering under the hood of TwentyTen to bring some more HTML5 to WordPress.</p>

## Upgrading To HTML5

TwentyTen gets a number of things spot on. First of all, it declares the right doctype and includes the abbreviated meta <code>charset</code> tag. It also uses other semantic goodness like Microformats and great accessibility features like WAI-ARIA. But we can go further.

<strong>Important notes:</strong>

*   I am referencing the HTML generated at [https://wp-themes.com/twentyten/](https://wp-themes.com/twentyten/), rather than the simple “Hello World” clean installation of WordPress 3.
*   For this article, I’ll be editing the files directly in the `/wp-content/themes/twentyten/` directory. I’ve provided all the updated HTML5 theme source files for you to download from [TwentyTen Five](https://www.twentytenfive.com/).
*   Line numbers may change over time, so when I reference one, I’ll usually say “on or around line…” The version of WordPress at the time of writing is 3.0.4.</p>

### Articles

One of the more confusing parts of the HTML5 spec is the <code>&lt;section&gt;</code> and <code>&lt;article&gt;</code> tags. Which came first, the chicken or the egg? The easiest way to remember is to refer to the specification. The <a href="https://dev.w3.org/html5/spec/Overview.html">HTML5 spec</a> may be dry at the best of times, but its <a href="https://dev.w3.org/html5/spec/Overview.html#the-article-element">explanation of articles</a> will always point you in the right direction:
<blockquote>The <code>article</code> element represents a self-contained composition in a document, page, application, or site and that is, in principle, independently distributable or reusable, e.g. in syndication.</blockquote>

If the piece of content in question can be, and most likely will be, syndicated by RSS, then there’s a good chance it’s an <code>&lt;article&gt;</code>. A blog post in WordPress fits the bill perfectly.

On the TwentyTen home page, we get the following HTML:

<pre><code class="language-markup tmp-html">&lt;div id="post-19"&gt;
…
&lt;/div&gt;</code></pre>

Semantically this means very little. But with the simple addition of an <code>article</code> tag, we’re able to transform it into mark-up with meaning.

<pre><code class="language-markup tmp-html">&lt;article id="post-19"&gt;
…
&lt;/article&gt;</code></pre>

Note that we retain the <code>id</code> to ensure that this <code>&lt;article&gt;</code> remains unique.

To make this change in the TwentyTen theme, open <em>loop.php</em>, which is in <code>/wp-content/themes/twentyten/</code>. On or around line 61, you should find the following code:

<pre><code class="language-php">&lt;div id="post-&lt;?php the_ID(); ?&gt;" &lt;?php post_class(); ?&gt;&gt;</code></pre>

We’ll need to change that <code>&lt;div&gt;</code> to an <code>&lt;article&gt;</code>, so that it reads:

<pre><code class="language-markup tmp-html">&lt;article id="post-&lt;?php the_ID(); ?&gt;" &lt;?php post_class(); ?&gt;&gt;</code></pre>

And then we close it again on or around line 97, so that…

<pre><code class="language-markup tmp-html">&lt;/div&gt;&lt;!-- #post-## --&gt;</code></pre>

… becomes:

<pre><code class="language-markup tmp-html">&lt;/article&gt;&lt;!-- #post-## --&gt;</code></pre>

There are also instances on lines 32, 101 and 124. Opening some of the other pages in the theme, for example <em>single.php</em>, and making the same change is worthwhile. Thus, line 22 in <em>single.php </em>would change from…

<pre><code class="language-php">&lt;div id="post-&lt;?php the_ID(); ?&gt;" &lt;?php post_class(); ?&gt;&gt;</code></pre>

… to:

<pre><code class="language-php">&lt;article id="post-&lt;?php the_ID(); ?&gt;" &lt;?php post_class(); ?&gt;&gt;</code></pre>

And line 55 would change from…

<pre><code class="language-php">&lt;/div&gt;&lt;!-- #post-## --&gt;</code></pre>

… to:

<pre><code class="language-php">&lt;/article&gt;&lt;!-- #post-## --&gt;</code></pre>

So far, so good. These are simple changes, but they already serve to overhaul the semantics of the website.</p>

### Time and Date

According to the HTML5 spec:
<blockquote>The <code>&lt;time&gt;</code> element either represents a time on a 24-hour clock, or a precise date on the proleptic Gregorian calendar, optionally with a time and a time-zone offset.</blockquote>

This means we can give the date and time of an article’s publication more context with HTML5’s <code>&lt;time&gt;</code> tag. Look at the code that WordPress generates:

<pre><code class="language-php">&lt;a href="https://wp-themes.com/?p=19" title="4:33 am"
rel="bookmark"&gt;&lt;span&gt;October 17, 2008&lt;/span&gt;&lt;/a&gt;</code></pre>

We can add meaning to our mark-up by transposing this to:

<pre><code class="language-php">&lt;a href="https://wp-themes.com/?p=19" title="4:33 am"
rel="bookmark"&gt;&lt;time datetime="2008-10-17T04:33Z"
pubdate&gt;October 17, 2008&lt;/time&gt;&lt;/a&gt;</code></pre>

This time is now machine-readable, and the browser can now interact with the date in many ways should we so wish. I’ve also added the boolean attribute <code>pubdate</code>, which designates this as the date on which the article or content was published.

Time in the <code>datetime</code> attribute is optional, but because WordPress includes it when you post an article, we can too. Implementing this in TwentyTen requires us to dig a little deeper. In <em>loop.php</em>, the following function on or around line 65 calls for the date to be included:

<pre><code class="language-php">&lt;?php twentyten_posted_on(); ?&gt;</code></pre>

To make our HTML5 changes, let’s head over to <code>/wp-content/themes/twentyten/</code> and open <em>functions.php</em>. On or around line 441, you’ll see this:

<pre><code class="language-php">function twentyten_posted_on() {
printf( __( '&lt;span&gt;Posted on&lt;/span&gt; %2$s &lt;span&gt;by&lt;/span&gt; %3$s', 'twentyten' ),
'meta-prep meta-prep-author',
sprintf( '&lt;a href="%1$s" title="%2$s" rel="bookmark"&gt;&lt;span&gt;%3$s&lt;/span&gt;&lt;/a&gt;',
get_permalink(),
esc_attr( get_the_time() ),
get_the_date()
),</code></pre>

If you don’t know what that means, don’t worry. We’re focusing on the <a href="https://php.net/manual/en/function.sprintf.php">sprintf</a> function, which basically takes a string and inserts the variables that are returned by the three functions listed: that is, <code>get_permanlink()</code>, <code>get_the_time()</code> and <code>get_the_date()</code> are inserted into <code>%1$s</code>, <code>%2$s</code> and <code>%3$s</code>, respectively.

We need to change how the date is formatted, so we’ll have to add a fourth function: <code>get_the_date('c')</code>. WordPress will then return the date in Coordinated Universal Time (UTC) format, which is exactly what the <code>&lt;time&gt;</code> element requires. Our finished code looks like this:

<pre><code class="language-php">printf( __( 'Posted on %2$s by %3$s', 'twentyten' ),
'meta-prep meta-prep-author',
sprintf( '&lt;a href="%1$s" rel="bookmark"&gt;&lt;time datetime="%2$s"
pubdate&gt;%3$s&lt;/time&gt;&lt;/a&gt;',
get_permalink(),
get_the_date('c'),
get_the_date()
),</code></pre>

I’ve included <code>get_the_date()</code> twice because we need two different formats: one for the <code>&lt;time&gt;</code> element and one that’s displayed to the user. I’ve also removed <code>title="[time published]"</code> because that information is already included in the <code>&lt;time&gt;</code> element.

For more details on WordPress’ date and time functions, check out:

*   [Function Reference/get the time](https://codex.wordpress.org/Function_Reference/get_the_time),
*   [Formatting Date and Time](https://codex.wordpress.org/Formatting_Date_and_Time).</p>

### Figures

A figure—for our purposes at least—is a piece of media that you upload in WordPress to embed in a post. The most obvious example would be an image, but it could be a video, too, of course. WordPress 3 is helpful enough to add captions to images when you first import the images, but it doesn’t display those captions using the new HTML5 <code>&lt;figure&gt;</code> and <code>&lt;figcaption&gt;</code> tags.

The <a href="https://dev.w3.org/html5/spec/Overview.html#the-figure-element">spec defines</a> <code>&lt;figure&gt;</code> as follows:
<blockquote>The <code>figure</code> element represents a unit of content, optionally with a caption, that is self-contained, that is typically referenced as a single unit from the main flow of the document, and that can be moved away from the main flow of the document without affecting the document’s meaning.</blockquote>

And it defines <code>&lt;figcaption&gt;</code> like so:
<blockquote>The <code>figcaption</code> element represents a caption or legend for the rest of the contents of the <code>figcaption</code> element’s parent <code>figure</code> element, if any.</blockquote>

Currently an image with a caption is rendered like this:

<pre><code class="language-markup tmp-html">&lt;div class="wp-caption" style="width: 445px;"&gt;&lt;img alt="Boat"
src="https://wpdotorg.files.wordpress.com/2008/11/boat.jpg"
title="Boat" width="435" height="288" /&gt;
&lt;p class="wp-caption-text"&gt;Boat&lt;/p&gt;
&lt;/div&gt;</code></pre>

<img class="88242" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/25ae1f14-56cf-412b-b782-1a4e8edbf55e/boat.jpg" alt="Screenshot" width="453" height="323" /><br>
<em>A WordPress image with a caption.</em>

Changing this HTML to include HTML5 elements requires us to first look at <em>media.php</em> in the <code>/wp-includes/</code> directory, where this code is generated. On or around line 739, you’ll find:

<pre><code class="language-php">return '&lt;div ' . $id . 'class="wp-caption ' . esc_attr($align) . '" style="width: ' . (10 + (int) $width) . 'px"&gt;'
. do_shortcode( $content ) . '&lt;p&gt;' . $caption . '&lt;/p&gt;&lt;/div&gt;';</code></pre>

To upgrade this to HTML5, we need to define a new function that outputs our <code>&lt;figure&gt;</code>-based HTML and assign this function to the same shortcode that calls <code>img_caption_shortcode()</code>. I’ve done this in <code>/wp-content/themes/twentyten/functions.php</code> by adding the following to the bottom of the file:

<pre><code class="language-php">add_shortcode('wp_caption', 'twentyten_img_caption_shortcode');
add_shortcode('caption', 'twentyten_img_caption_shortcode');

function twentyten_img_caption_shortcode($attr, $content = null) {

extract(shortcode_atts(array(
'id'    =&gt; ’,
'align'    =&gt; 'alignnone',
'width'    =&gt; ’,
'caption' =&gt; ’
), $attr));

if ( 1 &gt; (int) $width || empty($caption) )
return $content;

if ( $id ) $idtag = 'id="' . esc_attr($id) . '" ';

  return '&lt;figure ' . $idtag . 'aria-describedby="figcaption_' . $id . '" style="width: ' . (10 + (int) $width) . 'px"&gt;'
  . do_shortcode( $content ) . '&lt;figcaption id="figcaption_' . $id . '"&gt;' . $caption . '&lt;/figcaption&gt;&lt;/figure&gt;';
}</code></pre>

First, we point the shortcodes for <code>wp-caption</code> and <code>caption</code> to our new function <code>twentyten_img_caption_shortcode()</code>. Then, we simply copy the original function from <em>media.php</em>, and change the last few lines to include our <code>&lt;figure&gt;</code> element. This now renders our <em>boat.jpg</em> example from above like so:

<pre><code class="language-markup tmp-html">&lt;figure id="attachment_64" style="width: 445px;"&gt;
&lt;a href="https://localhost/wp-content/uploads/2010/07/boat.jpg"&gt;
&lt;img title="boat" src="https://localhost/wp-content/uploads/2010/07/boat.jpg"
alt="Screenshot" width="435" height="288" aria-describedby="figcaption_attachment_64"&gt;&lt;/a&gt;
&lt;figcaption id="figcaption_attachment_64"&gt;Boat&lt;/figcaption&gt;
&lt;/figure&gt;</code></pre>

### The Comments Form

One of the biggest improvements introduced in HTML5 is how form fields work and respond to user input. We can take advantage of these changes by using HTML5 form elements in the default WordPress comments form in three ways:

1.  We can set the text-input type to `email` and `url` for the relevant fields. This not only more accurately describes the input field, but also adds better keyboard functionality for the iPhone, for example.
2.  We can add the boolean attribute `required` to our required form fields. This goes beyond WAI-ARIA’s `aria-required='true'` because it invokes the browser’s own `required` behavior.
3.  We can add placeholder text to our form fields, a popular JavaScript method that is now handled in-browser. Placeholder text allows you to go into more detail about what information is required than a form label generally allows.

Before adding HTML, a typical comment input field might look like this:

<pre><code class="language-markup tmp-html">&lt;label for="email"&gt;Email&lt;/label&gt; &lt;span&gt;*&lt;/span&gt;
&lt;input id="email" name="email" type="text" value=""
size="30" aria-required='true' /&gt;</code></pre>

After our HTML5 changes, it would look like this:

<pre><code class="language-markup tmp-html">&lt;label for="email"&gt;Email&lt;/label&gt; &lt;span&gt;*&lt;/span&gt;
&lt;input id="email" name="email" type="email" value=""
size="30" aria-required='true'
placeholder="How can we reach you?" required /&gt;</code></pre>

To make these improvements in the code, we need to do two things. First, we need to change the HTML for the default fields (name, email address and website URL), and then we need to change it for the comment’s <code>&lt;textarea&gt;</code>. We can achieve both of these changes with additional filters and custom functions.

To change the HTML for the default form fields, we need to add the following filter to the bottom of <em>functions.php</em>:

<pre><code class="language-php">add_filter('comment_form_default_fields', 'twentytenfive_comments');</code></pre>

And then we have to create our custom function <code>twentytenfive_comments()</code> to change how these fields are displayed. We can do so by creating an array containing our new form fields and then returning it to this filter. Here’s the function:

<pre><code class="language-php">function twentytenfive_comments() {

$req = get_option('require_name_email');

$fields =  array(
'author' =&gt; '&lt;p&gt;' . '&lt;label for="author"&gt;' . __( 'Name' ) . '&lt;/label&gt; ' . ( $req ? '&lt;span&gt;*&lt;/span&gt;' : ’ ) .
'&lt;input id="author" name="author" type="text" value="' . esc_attr( $commenter['comment_author'] ) . '" size="30"' . $aria_req . ' placeholder = "What should we call you?"' . ( $req ? ' required' : ’ ) . '/&gt;&lt;/p&gt;',

'email'  =&gt; '&lt;p&gt;&lt;label for="email"&gt;' . __( 'Email' ) . '&lt;/label&gt; ' . ( $req ? '&lt;span&gt;*&lt;/span&gt;' : ’ ) .
'&lt;input id="email" name="email" type="email" value="' . esc_attr(  $commenter['comment_author_email'] ) . '" size="30"' . $aria_req . ' placeholder="How can we reach you?"' . ( $req ? ' required' : ’ ) . ' /&gt;&lt;/p&gt;',

'url'    =&gt; '&lt;p&gt;&lt;label for="url"&gt;' . __( 'Website' ) . '&lt;/label&gt;' .
'&lt;input id="url" name="url" type="url" value="' . esc_attr( $commenter['comment_author_url'] ) . '" size="30" placeholder="Have you got a website?" /&gt;&lt;/p&gt;'

);
return $fields;
}</code></pre>

You can see here that each element in the form has a name in the <code>array()</code>: author, email and url. We then type in our custom code, which contains the new HTML5 form attributes. We have added placeholder text to each of the elements and, where required, added the boolean <code>required</code> attribute (and we need to check if the admin has made these fields required using the <code>get_option()</code> function). We’ve also added the correct input type to the inputs for author, email address and website URL.

Finally, we need to add some HTML5 to the <code>&lt;textarea&gt;</code>, which is home to the user’s comments. We have to use another filter here, also in <em>functions.php</em>:

<pre><code class="language-php">add_filter('comment_form_field_comment', 'twentytenfive_commentfield');</code></pre>

We follow this with another custom function:

<pre><code class="language-php">function twentytenfive_commentfield() {

$commentArea = '&lt;p&gt;&lt;label for="comment"&gt;' . _x( 'Comment', 'noun' ) . '&lt;/label&gt;&lt;textarea id="comment" name="comment" cols="45" rows="8" aria-required="true" required placeholder="What's on your mind?"    &gt;&lt;/textarea&gt;&lt;/p&gt;';

return $commentArea;

}</code></pre>

This is more or less the same as the default <code>&lt;textarea&gt;</code>, except with <code>placeholder</code> and <code>required</code> attributes.

You can control exactly which fields appear in your form with these two filters, so feel free to add more if you want to collect more information.

Although relatively simple, these changes to the comment form provide additional (and useful!) features to users with latest-generation browsers. Look in Opera, Chrome (which doesn’t yet support <code>required</code>) or Firefox 4 to see the results.</p>

### Header, Navigation and Footer

We finally get around to inserting the new <code>&lt;header&gt;</code>, <code>&lt;nav&gt;</code> and <code>&lt;footer&gt;</code> elements. Currently, the code in <code>/wp-content/themes/twentyten/header.php</code> looks more or less like this:

<pre><code class="language-markup tmp-html">&lt;div id="header"&gt;
&lt;div id="masthead"&gt;
&lt;div id="branding" role="banner"&gt;
…
&lt;/div&gt;&lt;!-- #branding --&gt;

&lt;div id="access" role="navigation"&gt;
…
&lt;/div&gt;&lt;!-- #access --&gt;
&lt;/div&gt;&lt;!-- #masthead --&gt;
&lt;/div&gt;&lt;!-- #header --&gt;</code></pre>

It doesn’t take a genius to see that we can easily make this HTML5-ready by changing some of those divs to include <code>&lt;header&gt;</code> and <code>&lt;nav&gt;</code>.

<pre><code class="language-markup tmp-html">&lt;header id="header"&gt;
&lt;section id="masthead" &gt;
&lt;div id="branding" role="banner"&gt;
…
&lt;/div&gt;&lt;!-- #branding --&gt;

&lt;nav id="access" role="navigation"&gt;
…
&lt;/nav&gt;&lt;!-- #access --&gt;
&lt;/section&gt;&lt;!-- #masthead --&gt;
&lt;/header&gt;&lt;!-- #header --&gt;</code></pre>

You can see that we’ve left the WAI-ARIA role of <code>navigation</code> assigned to the <code>nav</code> element—simply to offer the broadest possible support to all browsers and screen readers.

I have replaced the <code>#masthead</code> div with a <code>&lt;section&gt;</code> because all of the elements in this area relate to one another and are likely to appear in a document outline. It seems you could delete this section altogether and just apply 30 pixels of <code>padding-top</code> to the header to maintain the layout. I’ve maintained the elements’ <code>id</code>s in case more than one of each are on the page—multiple headers, footers and navs (and more) are all welcome in HTML5.

While we’re editing the header, we can introduce the new <a href="https://dev.w3.org/html5/spec/Overview.html#the-hgroup-element">&lt;hgroup&gt;</a> element. This element enables us to include multiple headings in a section of our document, while they would be treated as just one heading in the document outline. Currently, the code on or around line 65 in <em>header.php</em> looks like this:

<pre><code class="language-php">&lt;?php $heading_tag = ( is_home() || is_front_page() ) ? 'h1' : 'div'; ?&gt;
&lt;&lt;?php echo $heading_tag; ?&gt; id="site-title"&gt;
&lt;span&gt;
&lt;a href="&lt;?php echo home_url( '/' ); ?&gt;" title="&lt;?php echo esc_attr( get_bloginfo( 'name', 'display' ) ); ?&gt;" rel="home"&gt;&lt;?php bloginfo( 'name' ); ?&gt;&lt;/a&gt;
&lt;/span&gt;
&lt;/&lt;?php echo $heading_tag; ?&gt;&gt;
&lt;div id="site-description"&gt;&lt;?php bloginfo( 'description' ); ?&gt;&lt;/div&gt;</code></pre>

We can edit this to include the <code>&lt;hgroup&gt;</code> tag, and also change <code>&lt;div id="site-description"&gt;</code> to an <code>&lt;h2&gt;</code> element:

<pre><code class="language-php">&lt;hgroup&gt;
&lt;?php $heading_tag = ( is_home() || is_front_page() ) ? 'h1' : 'div'; ?&gt;
&lt;&lt;?php echo $heading_tag; ?&gt; id="site-title"&gt;
&lt;span&gt;
&lt;a href="&lt;?php echo home_url( '/' ); ?&gt;" title="&lt;?php echo esc_attr( get_bloginfo( 'name', 'display' ) ); ?&gt;" rel="home"&gt;&lt;?php bloginfo( 'name' ); ?&gt;&lt;/a&gt;
&lt;/span&gt;
&lt;/&lt;?php echo $heading_tag; ?&gt;&gt;
&lt;h2 id="site-description"&gt;&lt;?php bloginfo( 'description' ); ?&gt;&lt;/h2&gt;
&lt;/hgroup&gt;</code></pre>

In <code>/wp-content/themes/twentyten/footer.php</code>, we have:

<pre><code class="language-php">&lt;div id="footer" role="contentinfo"&gt;
  &lt;div id="colophon"&gt;
  …
  &lt;div id="site-info"&gt;
    &lt;a href="&lt;?php echo home_url( '/' ) ?&gt;" title="&lt;?php echo esc_attr( get_bloginfo( 'name', 'display' ) ); ?&gt;" rel="home"&gt;
    &lt;?php bloginfo( 'name' ); ?&gt;
    &lt;/a&gt;
  &lt;/div&gt;&lt;!-- #site-info --&gt;

  &lt;div id="site-generator"&gt;
  …
  &lt;/div&gt;&lt;!-- #site-generator --&gt;

  &lt;/div&gt;&lt;!-- #colophon --&gt;
&lt;/div&gt;&lt;!-- #footer --&gt;</code></pre>

We can easily edit this to include a <code>&lt;footer&gt;</code> and another <code>&lt;section&gt;</code> element:

<pre><code class="language-php">&lt;footer role="contentinfo"&gt;
&lt;section id="colophon"&gt;
…
&lt;div id="site-info"&gt;
&lt;a href="&lt;?php echo home_url( '/' ) ?&gt;" title="&lt;?php echo esc_attr( get_bloginfo( 'name', 'display' ) ); ?&gt;" rel="home"&gt;
&lt;?php bloginfo( 'name' ); ?&gt;
&lt;/a&gt;
&lt;/div&gt;&lt;!-- #site-info --&gt;

&lt;div id="site-generator"&gt;
…
&lt;/div&gt;&lt;!-- #site-generator --&gt;

&lt;/section&gt;&lt;!-- #colophon --&gt;
&lt;/footer&gt;&lt;!-- #footer --&gt;</code></pre>

### JavaScript and CSS

As mentioned, we should include an HTML5 shim or <em>Modernizr.js</em> to make sure that all of our new elements render correctly in Internet Explorer prior to version 9. I added the following line to <em>header.php</em>:

<pre><code class="language-markup tmp-html">&lt;script src="&lt;?php bloginfo('stylesheet_directory'); ?&gt;/js/Modernizr-1.6.min.js"&gt;&lt;/script&gt;</code></pre>

A couple of things to note here. First, we no longer need <code>type="text/javascript"</code> because the browser will assume that a script is JavaScript unless it’s told different. Secondly, we have to use the WordPress <code>bloginfo()</code> function to point the source URL to our theme directory.

Although we are including Modernizr partly to make sure that IE can deal with the new HTML5 elements, I am serving it to all browsers because of the CSS3-checking functionality it provides.

In <em>style.css</em>, we need to make sure that our HTML5 elements have a <code>display: block</code> attribute, because some older browsers will treat them as inline elements. For our purposes, the following line at the top of the CSS file will do:

<pre><code class="language-css">header, nav, section, article, aside, figure, footer { display: block; }</code></pre>

While we’re talking about CSS, remember that we can now remove <code>type="text/css"</code> from our <code>&lt;link&gt;</code> tags. The simplified code looks like this:

<pre><code class="language-markup tmp-html">&lt;link rel="stylesheet" href="&lt;?php bloginfo( 'stylesheet_url' ); ?&gt;" /&gt;</code></pre>

That should be enough for now. Remember, though, that changing the structure of the page by replacing older HTML elements with new ones might require some additional CSS.

We should let the small minority of users know that we’ve stopped supporting browsers that have JavaScript turned off. A polite message just below the opening <code>&lt;body&gt;</code> tag in <em>header.php</em> should suffice:

<pre><code class="language-markup tmp-html">&lt;noscript&gt;&lt;strong&gt;JavaScript is required for this website to be displayed correctly. Please enable JavaScript before continuing...&lt;/strong&gt;&lt;/noscript&gt;</code></pre>

Add some very basic styling in <em>style.css</em> to make this message unmissable.

if ( 1 &gt; (int) $width || empty($caption) )
return $content;

if ( $id ) $idtag = 'id="' . esc_attr($id) . '" ';

  return '&lt;figure ' . $idtag . 'aria-describedby="figcaption_' . $id . '" style="width: ' . (10 + (int) $width) . 'px"&gt;'
  . do_shortcode( $content ) . '&lt;figcaption id="figcaption_' . $id . '"&gt;' . $caption . '&lt;/figcaption&gt;&lt;/figure&gt;';
}</code></pre>

First, we point the shortcodes for <code>wp-caption</code> and <code>caption</code> to our new function <code>twentyten_img_caption_shortcode()</code>. Then, we simply copy the original function from <em>media.php</em>, and change the last few lines to include our <code>&lt;figure&gt;</code> element. This now renders our <em>boat.jpg</em> example from above like so:

<pre><code class="language-markup tmp-html">&lt;figure id="attachment_64" style="width: 445px;"&gt;
&lt;a href="https://localhost/wp-content/uploads/2010/07/boat.jpg"&gt;
&lt;img title="boat" src="https://localhost/wp-content/uploads/2010/07/boat.jpg"
alt="Screenshot" width="435" height="288" aria-describedby="figcaption_attachment_64"&gt;&lt;/a&gt;
&lt;figcaption id="figcaption_attachment_64"&gt;Boat&lt;/figcaption&gt;
&lt;/figure&gt;</code></pre>

### The Comments Form

One of the biggest improvements introduced in HTML5 is how form fields work and respond to user input. We can take advantage of these changes by using HTML5 form elements in the default WordPress comments form in three ways:

1.  We can set the text-input type to `email` and `url` for the relevant fields. This not only more accurately describes the input field, but also adds better keyboard functionality for the iPhone, for example.
2.  We can add the boolean attribute `required` to our required form fields. This goes beyond WAI-ARIA’s `aria-required='true'` because it invokes the browser’s own `required` behavior.
3.  We can add placeholder text to our form fields, a popular JavaScript method that is now handled in-browser. Placeholder text allows you to go into more detail about what information is required than a form label generally allows.

Before adding HTML, a typical comment input field might look like this:

<pre><code class="language-markup tmp-html">&lt;label for="email"&gt;Email&lt;/label&gt; &lt;span&gt;*&lt;/span&gt;
&lt;input id="email" name="email" type="text" value=""
size="30" aria-required='true' /&gt;</code></pre>

After our HTML5 changes, it would look like this:

<pre><code class="language-markup tmp-html">&lt;label for="email"&gt;Email&lt;/label&gt; &lt;span&gt;*&lt;/span&gt;
&lt;input id="email" name="email" type="email" value=""
size="30" aria-required='true'
placeholder="How can we reach you?" required /&gt;</code></pre>

To make these improvements in the code, we need to do two things. First, we need to change the HTML for the default fields (name, email address and website URL), and then we need to change it for the comment’s <code>&lt;textarea&gt;</code>. We can achieve both of these changes with additional filters and custom functions.

To change the HTML for the default form fields, we need to add the following filter to the bottom of <em>functions.php</em>:

<pre><code class="language-php">add_filter('comment_form_default_fields', 'twentytenfive_comments');</code></pre>

And then we have to create our custom function <code>twentytenfive_comments()</code> to change how these fields are displayed. We can do so by creating an array containing our new form fields and then returning it to this filter. Here’s the function:

<pre><code class="language-php">function twentytenfive_comments() {

$req = get_option('require_name_email');

$fields =  array(
'author' =&gt; '&lt;p&gt;' . '&lt;label for="author"&gt;' . __( 'Name' ) . '&lt;/label&gt; ' . ( $req ? '&lt;span&gt;*&lt;/span&gt;' : ’ ) .
'&lt;input id="author" name="author" type="text" value="' . esc_attr( $commenter['comment_author'] ) . '" size="30"' . $aria_req . ' placeholder = "What should we call you?"' . ( $req ? ' required' : ’ ) . '/&gt;&lt;/p&gt;',

'email'  =&gt; '&lt;p&gt;&lt;label for="email"&gt;' . __( 'Email' ) . '&lt;/label&gt; ' . ( $req ? '&lt;span&gt;*&lt;/span&gt;' : ’ ) .
'&lt;input id="email" name="email" type="email" value="' . esc_attr(  $commenter['comment_author_email'] ) . '" size="30"' . $aria_req . ' placeholder="How can we reach you?"' . ( $req ? ' required' : ’ ) . ' /&gt;&lt;/p&gt;',

'url'    =&gt; '&lt;p&gt;&lt;label for="url"&gt;' . __( 'Website' ) . '&lt;/label&gt;' .
'&lt;input id="url" name="url" type="url" value="' . esc_attr( $commenter['comment_author_url'] ) . '" size="30" placeholder="Have you got a website?" /&gt;&lt;/p&gt;'

);
return $fields;
}</code></pre>

You can see here that each element in the form has a name in the <code>array()</code>: author, email and url. We then type in our custom code, which contains the new HTML5 form attributes. We have added placeholder text to each of the elements and, where required, added the boolean <code>required</code> attribute (and we need to check if the admin has made these fields required using the <code>get_option()</code> function). We’ve also added the correct input type to the inputs for author, email address and website URL.

Finally, we need to add some HTML5 to the <code>&lt;textarea&gt;</code>, which is home to the user’s comments. We have to use another filter here, also in <em>functions.php</em>:

<pre><code class="language-php">add_filter('comment_form_field_comment', 'twentytenfive_commentfield');</code></pre>

We follow this with another custom function:

<pre><code class="language-php">function twentytenfive_commentfield() {

$commentArea = '&lt;p&gt;&lt;label for="comment"&gt;' . _x( 'Comment', 'noun' ) . '&lt;/label&gt;&lt;textarea id="comment" name="comment" cols="45" rows="8" aria-required="true" required placeholder="What's on your mind?"    &gt;&lt;/textarea&gt;&lt;/p&gt;';

return $commentArea;

}</code></pre>

This is more or less the same as the default <code>&lt;textarea&gt;</code>, except with <code>placeholder</code> and <code>required</code> attributes.

You can control exactly which fields appear in your form with these two filters, so feel free to add more if you want to collect more information.

Although relatively simple, these changes to the comment form provide additional (and useful!) features to users with latest-generation browsers. Look in Opera, Chrome (which doesn’t yet support <code>required</code>) or Firefox 4 to see the results.</p>

### Header, Navigation and Footer

We finally get around to inserting the new <code>&lt;header&gt;</code>, <code>&lt;nav&gt;</code> and <code>&lt;footer&gt;</code> elements. Currently, the code in <code>/wp-content/themes/twentyten/header.php</code> looks more or less like this:

<pre><code class="language-markup tmp-html">&lt;div id="header"&gt;
&lt;div id="masthead"&gt;
&lt;div id="branding" role="banner"&gt;
…
&lt;/div&gt;&lt;!-- #branding --&gt;

&lt;div id="access" role="navigation"&gt;
…
&lt;/div&gt;&lt;!-- #access --&gt;
&lt;/div&gt;&lt;!-- #masthead --&gt;
&lt;/div&gt;&lt;!-- #header --&gt;</code></pre>

It doesn’t take a genius to see that we can easily make this HTML5-ready by changing some of those divs to include <code>&lt;header&gt;</code> and <code>&lt;nav&gt;</code>.

<pre><code class="language-markup tmp-html">&lt;header id="header"&gt;
&lt;section id="masthead" &gt;
&lt;div id="branding" role="banner"&gt;
…
&lt;/div&gt;&lt;!-- #branding --&gt;

&lt;nav id="access" role="navigation"&gt;
…
&lt;/nav&gt;&lt;!-- #access --&gt;
&lt;/section&gt;&lt;!-- #masthead --&gt;
&lt;/header&gt;&lt;!-- #header --&gt;</code></pre>

You can see that we’ve left the WAI-ARIA role of <code>navigation</code> assigned to the <code>nav</code> element—simply to offer the broadest possible support to all browsers and screen readers.

I have replaced the <code>#masthead</code> div with a <code>&lt;section&gt;</code> because all of the elements in this area relate to one another and are likely to appear in a document outline. It seems you could delete this section altogether and just apply 30 pixels of <code>padding-top</code> to the header to maintain the layout. I’ve maintained the elements’ <code>id</code>s in case more than one of each are on the page—multiple headers, footers and navs (and more) are all welcome in HTML5.

While we’re editing the header, we can introduce the new <a href="https://dev.w3.org/html5/spec/Overview.html#the-hgroup-element">&lt;hgroup&gt;</a> element. This element enables us to include multiple headings in a section of our document, while they would be treated as just one heading in the document outline. Currently, the code on or around line 65 in <em>header.php</em> looks like this:

<pre><code class="language-php">&lt;?php $heading_tag = ( is_home() || is_front_page() ) ? 'h1' : 'div'; ?&gt;
&lt;&lt;?php echo $heading_tag; ?&gt; id="site-title"&gt;
&lt;span&gt;
&lt;a href="&lt;?php echo home_url( '/' ); ?&gt;" title="&lt;?php echo esc_attr( get_bloginfo( 'name', 'display' ) ); ?&gt;" rel="home"&gt;&lt;?php bloginfo( 'name' ); ?&gt;&lt;/a&gt;
&lt;/span&gt;
&lt;/&lt;?php echo $heading_tag; ?&gt;&gt;
&lt;div id="site-description"&gt;&lt;?php bloginfo( 'description' ); ?&gt;&lt;/div&gt;</code></pre>

We can edit this to include the <code>&lt;hgroup&gt;</code> tag, and also change <code>&lt;div id="site-description"&gt;</code> to an <code>&lt;h2&gt;</code> element:

<pre><code class="language-php">&lt;hgroup&gt;
&lt;?php $heading_tag = ( is_home() || is_front_page() ) ? 'h1' : 'div'; ?&gt;
&lt;&lt;?php echo $heading_tag; ?&gt; id="site-title"&gt;
&lt;span&gt;
&lt;a href="&lt;?php echo home_url( '/' ); ?&gt;" title="&lt;?php echo esc_attr( get_bloginfo( 'name', 'display' ) ); ?&gt;" rel="home"&gt;&lt;?php bloginfo( 'name' ); ?&gt;&lt;/a&gt;
&lt;/span&gt;
&lt;/&lt;?php echo $heading_tag; ?&gt;&gt;
&lt;h2 id="site-description"&gt;&lt;?php bloginfo( 'description' ); ?&gt;&lt;/h2&gt;
&lt;/hgroup&gt;</code></pre>

In <code>/wp-content/themes/twentyten/footer.php</code>, we have:

<pre><code class="language-php">&lt;div id="footer" role="contentinfo"&gt;
  &lt;div id="colophon"&gt;
  …
  &lt;div id="site-info"&gt;
    &lt;a href="&lt;?php echo home_url( '/' ) ?&gt;" title="&lt;?php echo esc_attr( get_bloginfo( 'name', 'display' ) ); ?&gt;" rel="home"&gt;
    &lt;?php bloginfo( 'name' ); ?&gt;
    &lt;/a&gt;
  &lt;/div&gt;&lt;!-- #site-info --&gt;

  &lt;div id="site-generator"&gt;
  …
  &lt;/div&gt;&lt;!-- #site-generator --&gt;

  &lt;/div&gt;&lt;!-- #colophon --&gt;
&lt;/div&gt;&lt;!-- #footer --&gt;</code></pre>

We can easily edit this to include a <code>&lt;footer&gt;</code> and another <code>&lt;section&gt;</code> element:

<pre><code class="language-php">&lt;footer role="contentinfo"&gt;
&lt;section id="colophon"&gt;
…
&lt;div id="site-info"&gt;
&lt;a href="&lt;?php echo home_url( '/' ) ?&gt;" title="&lt;?php echo esc_attr( get_bloginfo( 'name', 'display' ) ); ?&gt;" rel="home"&gt;
&lt;?php bloginfo( 'name' ); ?&gt;
&lt;/a&gt;
&lt;/div&gt;&lt;!-- #site-info --&gt;

&lt;div id="site-generator"&gt;
…
&lt;/div&gt;&lt;!-- #site-generator --&gt;

&lt;/section&gt;&lt;!-- #colophon --&gt;
&lt;/footer&gt;&lt;!-- #footer --&gt;</code></pre>

### JavaScript and CSS

As mentioned, we should include an HTML5 shim or <em>Modernizr.js</em> to make sure that all of our new elements render correctly in Internet Explorer prior to version 9. I added the following line to <em>header.php</em>:

<pre><code class="language-markup tmp-html">&lt;script src="&lt;?php bloginfo('stylesheet_directory'); ?&gt;/js/Modernizr-1.6.min.js"&gt;&lt;/script&gt;</code></pre>

A couple of things to note here. First, we no longer need <code>type="text/javascript"</code> because the browser will assume that a script is JavaScript unless it’s told different. Secondly, we have to use the WordPress <code>bloginfo()</code> function to point the source URL to our theme directory.

Although we are including Modernizr partly to make sure that IE can deal with the new HTML5 elements, I am serving it to all browsers because of the CSS3-checking functionality it provides.

In <em>style.css</em>, we need to make sure that our HTML5 elements have a <code>display: block</code> attribute, because some older browsers will treat them as inline elements. For our purposes, the following line at the top of the CSS file will do:

<pre><code class="language-css">header, nav, section, article, aside, figure, footer { display: block; }</code></pre>

While we’re talking about CSS, remember that we can now remove <code>type="text/css"</code> from our <code>&lt;link&gt;</code> tags. The simplified code looks like this:

<pre><code class="language-markup tmp-html">&lt;link rel="stylesheet" href="&lt;?php bloginfo( 'stylesheet_url' ); ?&gt;" /&gt;</code></pre>

That should be enough for now. Remember, though, that changing the structure of the page by replacing older HTML elements with new ones might require some additional CSS.

We should let the small minority of users know that we’ve stopped supporting browsers that have JavaScript turned off. A polite message just below the opening <code>&lt;body&gt;</code> tag in <em>header.php</em> should suffice:

<pre><code class="language-markup tmp-html">&lt;noscript&gt;&lt;strong&gt;JavaScript is required for this website to be displayed correctly. Please enable JavaScript before continuing...&lt;/strong&gt;&lt;/noscript&gt;</code></pre>

Add some very basic styling in <em>style.css</em> to make this message unmissable.

<pre><code class="language-css">/* A message for users with JavaScript turned off */
noscript strong {
display: block;
font-size: 18px;
line-height:1.5em;
padding: 5px 0;
background-color: #ccc;
color: #a00;
text-align: center; }</code></pre>

## Still Not Convinced? A Cross-Browser Alternative

There is another option for those of you who absolutely <em>must</em> support users with JavaScript turned off, as suggested by <a href="https://icant.co.uk/">Christian Heilmann</a>. Simply wrap your HTML5 elements with divs which share the same ID name. For example:

<pre><code class="language-markup tmp-html">&lt;article id="post-123"&gt;
...
&lt;/article&gt;</code></pre>

becomes

<pre><code class="language-markup tmp-html">&lt;div class="article"&gt;
&lt;article id="post-123"&gt;
...
&lt;/article&gt;
&lt;/div&gt;</code></pre>

Then it's just a case of adding <code>.article</code> to your article CSS definition. It might look like this:

<pre><code class="language-markup tmp-html">.article,
article { display: block; background-color: #f7f7f7; }</code></pre>

It's worth noting that this adds another layer of markup to your code which isn't needed for most users. I'd only recommend it if non-JavaScript users are a significant proportion of your users and/or sales.</p>

## Final Thoughts

TwentyTen was a huge step forward for WordPress; and as a piece of HTML, it is a beacon of best practice. By including some simple JavaScript, we can now open up the theme to the world of HTML5—and the additional meaning and simpler semantic code that it offers.

While we’ve addressed a good number of new HTML5 elements in this article, it really is just a starting point and you can add many more yourself. For example, you could add headers and footers to individual posts, or you might like to add the new <code>&lt;aside&gt;</code> element. Let us know your ideas and how you get on with implementing them in the comments below!

### Download TwentyTen With HTML5

To complement this article, I have created a new version of TwentyTen, with the HTML5 elements we have discussed. Download this theme from <a href="https://www.twentytenfive.com">TwentyTen Five</a>.

<a href="https://www.twentytenfive.com"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ccef8d15-20e6-4f34-979c-4f61d419a195/twentyten-five.jpg" alt="TwentyTen With HTML5" width="500" height="393" /></a>

### Other Resources

You may be interested in the following articles and related resources:

*   [HTML5: A Vocabulary and associated APIs for HTML and XHTML](https://dev.w3.org/html5/spec/Overview.html) The HTML5 spec. An essential reference to bookmark.
*   [New Theme: Toolbox](https://en.blog.wordpress.com/2010/12/10/new-theme-toolbox/) WordPress announces the sandbox theme called Toolbox, built entirely in HTML5.
*   Toolbox Download the WordPress HTML5 theme Toolbox.
*   [Redesigning With HTML5 and WAI-ARIA](https://www.brucelawson.co.uk/2009/redesigning-with-html-5-wai-aria/) Bruce Lawson takes an early crack at introducing some HTML5 into WordPress.
*   [Coding an HTML5 Layout From Scratch](https://www.smashingmagazine.com/2009/08/04/designing-a-html-5-layout-from-scratch/) New to HTML5? This is a great place to start.

<em>(al) (vf) (ik)</em>

