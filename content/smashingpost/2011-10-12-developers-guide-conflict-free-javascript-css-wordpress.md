---
title: The Developer's Guide To Conflict-Free JavaScript And CSS In WordPress
slug: developers-guide-conflict-free-javascript-css-wordpress
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2bc464a9-98bf-40e7-a739-912651700e97/css-illus-wordpress.jpg
date: 2011-10-12T14:11:12.000Z
author: peter-wilson
description: >-
  Imagine you’re playing the latest hash-tag game on Twitter when you see this
  friendly tweet: "You might want to check your #WP site. It includes two copies
  of jQuery. Nothing’s broken, but loading time will be slower."

  [![sm-wp-css-js](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/35692e12-d1ac-47b5-850a-328ade8dd884/developers-guide-conflict-free-javascript-css-wordpress.jpg)](https://www.smashingmagazine.com/2011/10/12/developers-guide-conflict-free-javascript-css-wordpress/)

  You check your source code, and sure enough you see this:

  <pre class="brush: html"><script
  src="/wp-includes/js/jquery/jquery.js?ver=1.6.1"
  type="text/javascript"></script>

  <script src="/wp-content/plugins/some-plugin/jquery.js"></script>

  </pre>

  What went wrong? The first copy of jQuery is included the WordPress way, while
  some-plugin includes jQuery as you would on a static HTML page. A number of
  JavaScript frameworks are included in WordPress by default.
categories:
  - WordPress
  - Workflow
  - JavaScript
  - Maintenance
  - Techniques (WP)
---
Imagine you’re playing the latest hash-tag game on Twitter when you see this friendly tweet:
<blockquote>You might want to check your #WP site. It includes two copies of jQuery. Nothing’s broken, but loading time will be slower.</blockquote>

You check your source code, and sure enough you see this:

<pre><code class="language-markup tmp-html">&lt;script src="/wp-includes/js/jquery/jquery.js?ver=1.6.1" type="text/javascript"&gt;&lt;/script&gt;
&lt;script src="/wp-content/plugins/some-plugin/jquery.js"&gt;&lt;/script&gt;</code></pre>

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/05b5c510-3024-466e-8b49-3d86a3c47dfa/sm-wp-css-js.jpg" alt="sm-wp-css-js" width="550" height="329" />

### What Went Wrong?

The first copy of jQuery is included the WordPress way, while <code>some-plugin</code> includes jQuery as you would on a static HTML page.

{{% feature-panel %}}

A number of JavaScript frameworks are included in WordPress by default, including:

*   Scriptaculous,
*   jQuery (running in [noConflict mode](https://api.jquery.com/jQuery.noConflict/)),
*   the jQuery UI core and selected widgets,
*   Prototype.

A <a href="https://codex.wordpress.org/Function_Reference/wp_enqueue_script#Default_scripts_included_with_WordPress">complete list can be found in the Codex</a>. On the same page are instructions for using <a href="https://codex.wordpress.org/Function_Reference/wp_enqueue_script#jQuery_noConflict_wrappers">jQuery in noConflict mode</a>.</p>

### Avoiding the Problem

WordPress includes these libraries so that plugin and theme authors can avoid this problem by using the <code>wp_register_script</code> and <code>wp_enqueue_script</code> PHP functions to include JavaScript in the HTML.

Registering a file alone doesn’t do anything to the output of your HTML; it only adds the file to WordPress’s list of known scripts. As you’ll see in the next section, we register files early on in a theme or plugin where we can keep track of versioning information.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [How To Speed Up Your WordPress Website](https://www.smashingmagazine.com/2014/06/how-to-speed-up-your-wordpress-website/)
*   [How To Use AJAX In WordPress](https://www.smashingmagazine.com/2011/10/how-to-use-ajax-in-wordpress/)
*   [Useful JavaScript Libraries and jQuery Plugins](https://www.smashingmagazine.com/2012/09/useful-javascript-libraries-jquery-plugins-web-developers/)
*   [<span class="headline">A Beginner’s Guide To Creating A WordPress Website</span>](https://www.smashingmagazine.com/2016/02/beginners-guide-creating-wordpress-website/)

To output the file to the HTML, you need to enqueue the file. Once you’ve done this, WordPress will add the required script tag to the header or footer of the outputted page. More details are provided later in this article.

Registering a file requires more complex code than enqueueing the files; so, quickly parsing the file is harder when you’re reviewing your code. Enqueueing the file is far simpler, and you can easily parse how the HTML is being affected.

For these techniques to work, the theme’s <em>header.php</em> file must include the line <code>&lt;?php wp_head(); ?&gt;</code> just before the <code>&lt;/head&gt;</code> tag, and the <em>footer.php</em> file must include the line <code>&lt;?php wp_footer(); ?&gt;</code> just before the <code>&lt;/body&gt;</code> tag.</p>

## Registering JavaScript

Before registering your JavaScript, you’ll need to decide on a few additional items:

*   the file’s handle (i.e. the name by which WordPress will know the file);
*   other scripts that the file depends on (jQuery, for example);
*   the version number (optional);
*   where the file will appear in the HTML (the header or footer).

This article refers to building a theme, but the tips apply equally to building a plugin.</p>

### Examples

We’ll use two JavaScript files to illustrate the power of the functions:

The first is <em>base.js</em>, which is a toolkit of functions used in our example website.

<pre><code class="language-javascript">function makeRed(selector){
  var $ = jQuery; //enable $ alias within this scope
  $(function(){
    $(selector).css('color','red');
  });
}</code></pre>

The <em>base.js</em> file relies on jQuery, so jQuery can be considered a dependency.

This is the first version of the file, version 1.0.0, and there is no reason to run this file in the HTML header.

The second file, <em>custom.js</em>, is used to add the JavaScript goodness to our website.

<pre><code class="language-javascript">makeRed('*');</code></pre>

This <em>custom.js</em> file calls a function in <em>base.js</em>, so <em>base.js</em> is a dependency.

Like <em>base.js</em>, <em>custom.js</em> is version 1.0.0 and can be run in the HTML footer.

The <em>custom.js</em> file also indirectly relies on jQuery. But in this case, <em>base.js</em> could be edited to be self-contained or to rely on another framework. There is no need for jQuery to be listed as a dependency of <em>custom.js</em>.

It’s now simply a matter of registering your JavaScript using the function <code>wp_register_script</code>. This takes the following arguments:

*   `$handle` A string
*   `$source` A string
*   `$dependancies` An array (optional)
*   `$version` A string (optional)
*   `$in_footer` True/false (optional, default is false)

When registering scripts, it is best to use the <code>init</code> hook and to register them all at once.

To register the scripts in our example, add the following to the theme’s <em>functions.php</em> file:

<pre><code class="language-php">function mytheme_register_scripts() { 
  //base.js – dependent on jQuery 
  wp_register_script( 
    'theme-base', //handle 
    '/wp-content/themes/my-theme/base.js', //source 
    array('jquery'), //dependencies 
    '1.0.0', //version 
    true //run in footer 
  ); 

  //custom.js – dependent on base.js 
  wp_register_script( 
    'theme-custom', 
    '/wp-content/themes/my-theme/custom.js', 
    array('theme-base'), 
    '1.0.0', 
    true 
  ); 
} 
add_action('init', 'mytheme_register_scripts');</code></pre>

There is no need to register jQuery, because WordPress already has. Re-registering it could lead to problems.</p>

### You Have Achieved Nothing!

All of this registering JavaScript files the WordPress way has, so far, achieved nothing. Nothing will be outputted to your HTML files.

To get WordPress to output the relevant HTML, we need to enqueue our files. Unlike the relatively long-winded commands required to register the functions, this is a very simple process.</p>

## Outputting the JavaScript HTML

Adding the <code>&lt;script&gt;</code> tags to your HTML is done with the <code>wp_enqueue_script</code> function. Once a script is registered, it takes one argument, the file’s handle.

Adding JavaScript to the HTML is done in the <code>wp_print_scripts</code> hook with the following code:

<pre><code class="language-php">function mytheme_enqueue_scripts(){ 
  if (!is_admin()): 
    wp_enqueue_script('theme-custom'); //custom.js 
  endif; //!is_admin 
} 
add_action('wp_print_scripts', 'mytheme_enqueue_scripts');</code></pre>

Of our two registered JavaScript files (<em>base.js</em> and <em>custom.js</em>), only the second adds JavaScript functionality to the website. Without the second file, there is no need to add the first.

Having enqueued <em>custom.js</em> for output to the HTML, WordPress will figure out that it depends on <em>base.js</em> being present and that <em>base.js</em>, in turn, requires jQuery. The resulting HTML is:

<pre><code class="language-markup tmp-html">&lt;script src="/wp-includes/js/jquery/jquery.js?ver=1.6.1" type="text/javascript"&gt;&lt;/script&gt;
&lt;script src="/wp-content/themes/my-theme/base.js?ver=1.0.0" type="text/javascript"&gt;&lt;/script&gt;
&lt;script src="/wp-content/themes/my-theme/custom.js?ver=1.0.0" type="text/javascript"&gt;&lt;/script&gt;</code></pre>

## Registering Style Sheets

Both of the functions for adding JavaScript to our HTML have sister PHP functions for adding style sheets to the HTML: <code>wp_register_style</code> and <code>wp_enqueue_style</code>.

As with the JavaScript example, we’ll use a couple of CSS files throughout this article, employing the mobile-first methodology for responsive Web design.

The <em>mobile.css</em> file is the CSS for building the mobile version of the website. It has no dependencies.

The <em>desktop.css</em> file is the CSS that is loaded for desktop devices only. The desktop version builds on the mobile version, so <em>mobile.css</em> is a dependency.

Once you’ve decided on version numbers, dependencies and media types, it’s time to register your style sheets using the <code>wp_register_style</code> function. This function takes the following arguments:

*   `$handle` A string
*   `$source` A string
*   `$dependancies` An array (optional, default is none)
*   `$version` A string (optional, the default is the current WordPress version number)
*   `$media_type` A string (optional, the default is all)

Again, registering your style sheets using the <code>init</code> action is best.

To your theme’s <em>functions.php</em>, you would add this:

<pre><code class="language-php">function mytheme_register_styles(){ 
  //mobile.css for all devices 
  wp_register_style( 
    'theme-mobile', //handle 
    '/wp-content/themes/my-theme/mobile.css', //source 
    null, //no dependencies 
    '1.0.0' //version 
  ); 

  //desktop.css for big-screen browsers 
  wp_register_style( 
    'theme-desktop', 
    '/wp-content/themes/my-theme/desktop.css', 
    array('theme-mobile'), 
    '1.0.0', 
    'only screen and (min-width : 960px)' //media type 
  ); 

  /* *keep reading* */ 
} 
add_action('init', 'mytheme_register_styles');</code></pre>

We have used CSS3 media queries to prevent mobile browsers from parsing our desktop style sheet. But Internet Explorer versions 8 and below do not understand CSS3 media queries and so will not parse the desktop CSS either.

IE8 is only two years old, so we should support its users with conditional comments.</p>

### Conditional Comments

When registering CSS using the register and enqueue functions, conditional comments are a little more complex. WordPress uses the object <code>$wp_styles</code> to store registered style sheets.

To wrap your file in conditional comments, add extra information to this object.

For Internet Explorer 8 and below, excluding mobile IE, we need to register another copy of our desktop style sheet (using the media type <code>all</code>) and wrap it in conditional comments.

In the code sample above, <code>/* *keep reading* */</code> would be replaced with the following:

<pre><code class="language-php">global $wp_styles; 
wp_register_style( 
  'theme-desktop-ie', 
  '/wp-content/themes/my-theme/desktop.css', 
  array('theme-mobile'), 
  '1.0.0' 
); 

$wp_styles-&gt;add_data( 
  'theme-desktop-ie', //handle 
  'conditional',  //is a conditional comment 
  '!(IEMobile)&amp;(lte IE 8)' //the conditional comment 
);</code></pre>

Unfortunately, there is no equivalent for wrapping JavaScript files in conditional comments, presumably due to the concatenation of JavaScript in the admin section.

If you need to wrap a JavaScript file in conditional comments, you will need to add it to <em>header.php</em> or <em>footer.php</em> in the theme. Alternatively, you could use the <code>wp_head</code> or <code>wp_footer</code> hooks.</p>

## Outputting The Style Sheet HTML

Outputting the style sheet HTML is very similar to outputting the JavaScript HTML. We use the enqueue function and run it on the <code>wp_print_styles</code> hook.

In our example, we could get away with telling WordPress to queue only the style sheets that have the handles <code>theme-desktop</code> and <code>theme-desktop-ie</code>. WordPress would then output the <code>mobile</code>/<code>all</code> media version.

However, both style sheets apply styles to the website beyond a basic reset: <em>mobile.css</em> builds the website for mobile phones, and <em>desktop.css</em> builds on top of that. If it does something and I’ve registered it, then I should enqueue it. It helps to keep track of what’s going on.

Here is the code to output the CSS to the HTML:

<pre><code class="language-php">function mytheme_enqueue_styles(){ 
  if (!is_admin()): 
    wp_enqueue_style('theme-mobile'); //mobile.css 
    wp_enqueue_style('theme-desktop'); //desktop.css 
    wp_enqueue_style('theme-desktop-ie'); //desktop.css lte ie8 
  endif; //!is_admin 
} 
add_action('wp_print_styles', 'mytheme_enqueue_styles');</code></pre>

## What’s The Point?

You may be wondering what the point is of going through all of this extra effort when we could just output our JavaScript and style sheets in the theme’s <em>header.php</em> or using the <code>wp_head</code> hook.

In the case of CSS in a standalone theme, it’s a valid point. It’s extra work without much of a payoff.

But with JavaScript, it helps to prevent clashes between plugins and themes when each uses a different version of a JavaScript framework. It also makes page-loading times as fast as possible by avoiding file duplication.</p>

### WordPress Frameworks

This group of functions can be most helpful when using a framework for theming. In my agency, <a href="https://soupgiant.com/">Soupgiant</a>, we’ve built a framework to speed up our production of websites.

As with most agencies, we have internal conventions for naming JavaScript and CSS files.

When we create a bespoke WordPress theme for a client, we develop it as a <a href="https://codex.wordpress.org/Child_Themes">child theme</a> of our framework. In the framework itself, we register a number of JavaScript and CSS files in accordance with our naming convention.

In the child theme, we then simply enqueue files to output the HTML.

<pre><code class="language-php">function clienttheme_enqueue_css() { 
  if (!is_admin()): 
    wp_enqueue_style('theme-mobile'); 
    wp_enqueue_style('theme-desktop'); 
    wp_enqueue_style('theme-desktop-ie'); 
  endif; //!is_admin 
} 
add_action('wp_print_styles', 'clienttheme_enqueue_css'); 

function clienttheme_enqueue_js() { 
  if (!is_admin()): 
    wp_enqueue_script('theme-custom'); 
  endif; //!is_admin
} 
add_action('wp_print_scripts', 'clienttheme_enqueue_js');</code></pre>

Adding CSS and JavaScript to our themes the WordPress way enables us to keep track of exactly what’s going on at a glance.</p>

## A Slight Limitation

If you use a JavaScript framework in your theme or plugin, then you’re stuck with the version that ships with the current version of WordPress, which sometimes falls a version or two behind the latest official release of the framework. (Upgrading to a newer version of the framework is technically possible, but this could cause problems with other themes or plugins that expect the version that ships with WordPress, so I’ve omitted this information from this article.)

While this prevents you from using any new features of the framework that were added after the version included in WordPress, the advantage is that <em>all</em> theme and plugin authors know which version of the framework to expect.</p>

## A Single Point Of Registration

Register your styles and scripts in a single block of code, so that when you update a file, you will be able to go back and update the version number easily.

If you use different code in different parts of the website, you can wrap the logic around the enqueue scripts.

If, say, your archive pages use different JavaScript than the rest of the website, then you might register three files:

*   base JavaScript (registered as `theme-base`),
*   archive JavaScript (registered as `theme-archive`),
*   general JavaScript (registered as `theme-general`).

Again, the base JavaScript adds nothing to the website. Rather, it is a group of default functions that the other two files rely on. You could then enqueue the files using the following code:

<pre><code class="language-php">function mytheme_enqueue_js(){ 
  if (is_archive()) { 
    wp_enqueue_script('theme-archive'); 
  } 
  elseif (!is_admin()) { 
    wp_enqueue_script('theme-general');
  }
} 
add_action('wp_print_scripts', 'mytheme_enqueue_js');</code></pre>

## Using The Google AJAX CDN

While using JavaScript the WordPress way will save you the problem of common libraries conflicting with each other, you might prefer to serve these libraries from Google’s server rather than your own.

Using Jason Penny’s <a href="https://wordpress.org/extend/plugins/use-google-libraries/">Use Google Libraries</a> plugin is the easiest way to do this. The plugin automatically keeps jQuery in noConflict mode.</p>

## Putting It All Together

Once you’ve started registering and outputting your scripts and styles the WordPress way, you will find that managing these files becomes a series of logical steps:

1.  Registration to manage:
    *   version numbers,
    *   file dependencies,
    *   media types for CSS,
    *   code placement for JavaScript (header or footer);
2.  Enqueue/output files to HTML:
    *   logic targeting output to specific WordPress pages,
    *   WordPress automating dependencies.

Eliminating potential JavaScript conflicts from your WordPress theme or plugin frees you to get on with more important things, such as following up on sales leads or getting back to that hash-tag game that was so rudely interrupted.

{{< signature "al" >}}

