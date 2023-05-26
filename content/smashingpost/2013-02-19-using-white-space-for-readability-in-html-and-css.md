---
title: Using White Space For Readability In HTML And CSS
slug: using-white-space-for-readability-in-html-and-css
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/91b546a5-f8db-4d78-8d5d-484cbf1baa73/labyrinth-comic-1.jpg
date: 2013-02-19T13:32:15.000Z
author: louis-lazaris
description: >-
  Right up front, I’ll offer some simple advice: In production, your code should
  be as performance-friendly as possible. This means, Gzip’ing, concatenating
  and minifying as many assets as possible, thus serving the smallest possible
  files and the least number of files.

  I don’t think anyone would argue that these suggestions aren’t best practices
  (even if we don’t implement them in every project). Now that we’ve got that
  out of the way, how can we use white space in development code to ensure that
  our files are as readable and maintainable as possible?
categories:
  - Coding
  - CSS
  - HTML
  - Readability
---
Right up front, I’ll offer some simple advice: In production, your code should be <strong>as performance-friendly as possible</strong>. This means, Gzip’ing, concatenating and minifying as many assets as possible, thus serving the smallest possible files and the least number of files. I don’t think anyone would argue that these suggestions aren’t best practices (even if we don’t implement them in every project).</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cdad17d7-5f0d-4ca6-8307-37c323fee905/labyrinth-comic.jpg" alt="White Space Readability" title="Using White Space For Readability In HTML And CSS" width="500" height="375" /><br>
<figcaption>Well-written, readable code doesn't create mind games and labyrinths when other developers read it. (Image: <a href="https://www.flickr.com/photos/tocaboca/5630744267/in/photostream/">Toca Boca</a>)</figcaption></figure>

Now that we’ve got that out of the way, how can we use white space in development code to ensure that our files are as readable and maintainable as possible? Well, we could consider a number of options, starting with some basics.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Principles Of Minimalist Web Design, With Examples](https://www.smashingmagazine.com/2010/05/principles-of-minimalist-web-design-with-examples/)
*   [16 Pixels: For Body Copy. Anything Less Is A Costly Mistake](https://www.smashingmagazine.com/2011/10/16-pixels-body-copy-anything-less-costly-mistake/)
*   [The Perfect Paragraph](https://www.smashingmagazine.com/2011/11/the-perfect-paragraph/)
*   [Space Yourself](https://www.smashingmagazine.com/2015/10/space-yourself/)

{{% feature-panel %}}

## Basic HTML Indentation

I think most if not all of us add basic indentation in our HTML:

<pre><code class="language-markup">&lt;header&gt;

   &lt;hgroup&gt;
      &lt;h1&gt;Section title&lt;/h1&gt;
      &lt;h2&gt;Tagline&lt;/h2&gt;
   &lt;/hgroup&gt;

   &lt;nav&gt;
      &lt;ul&gt;
      &lt;li&gt;&lt;a href="/"&gt;Home&lt;/a&gt;&lt;/li&gt;
      &lt;li&gt;&lt;a href="/about/"&gt;About&lt;/a&gt;&lt;/li&gt;
      &lt;li&gt;&lt;a href="/services/"&gt;Services&lt;/a&gt;&lt;/li&gt;
      &lt;li&gt;&lt;a href="/contact/"&gt;Contact&lt;/a&gt;&lt;/li&gt;
      &lt;/ul&gt;
   &lt;/nav&gt;

&lt;/header&gt;

&lt;div class="main"&gt;
   &lt;p&gt;Content goes here.&lt;/p&gt;
&lt;/div&gt;</code></pre>

The principle here is that <strong>whenever something is nested, you indent</strong>, so that it’s clear where everything is in the markup’s hierarchy. With simple HTML nesting, the content in the <code>&lt;head&gt;</code> section is often neglected, but keeping the nesting consistent here, too, is good practice.

For example, the following sample code is fairly readable, even with no nesting:

<pre><code class="language-markup">&lt;!DOCTYPE html&gt;
&lt;html&gt;
&lt;head&gt;
&lt;title&gt;Foo&lt;/title&gt;
&lt;/head&gt;
&lt;body&gt;
&lt;!-- content… --&gt;
&lt;/body&gt;
&lt;/html&gt;</code></pre>

However, with much more content in the <code>&lt;head&gt;</code> section, nesting could make it easier to <strong>scan the contents</strong>:

<pre><code class="language-markup">&lt;!doctype html&gt;
&lt;html class="no-js" lang="en"&gt;
   &lt;head&gt;
      &lt;meta charset="utf-8"&gt;
      &lt;meta content="IE=edge,chrome=1" http-equiv="X-UA-Compatible"&gt;
      &lt;title&gt;HTML5 Please - Use the new and shiny responsibly&lt;/title&gt;
      &lt;meta name="description" content="Look up HTML5, CSS3, etc features, know if they are ready for use, and if so find out how you should use them - with polyfills, fallbacks or as they are."&gt;
      &lt;meta content="width=device-width, initial-scale=1.0" name="viewport"&gt;

      &lt;link rel="shortcut icon" href="favicon.ico" /&gt;
      &lt;link rel="apple-touch-icon-precomposed" sizes="114x114" href="apple-touch-icon-114x114-precomposed.png"&gt;
      &lt;link rel="apple-touch-icon-precomposed" sizes="72x72" href="apple-touch-icon-72x72-precomposed.png"&gt;
      &lt;link rel="apple-touch-icon-precomposed" href="apple-touch-icon-precomposed.png"&gt;

      &lt;link href="https://fonts.googleapis.com/css?family=Francois+One|Open+Sans:400italic,400,800" rel="stylesheet"&gt;
      &lt;link href="css/style.css" rel="stylesheet"&gt;
      &lt;script src="js/libs/modernizr-2.0.min.js"&gt;&lt;/script&gt;
      &lt;script&gt;if (location.host == 'h5bp.github.com') location.href = '//html5please.us/'&lt;/script&gt;

   &lt;/head&gt;
   &lt;body id="gfs"&gt;
      &lt;!-- content… --&gt;
   &lt;/body&gt;
&lt;/html&gt;</code></pre>

This last chunk of code is taken from the <a href="https://html5please.com/">HTML5 Please</a> website. As you can see, when the content in the <code>&lt;head&gt;</code> section starts to get larger, <strong>indenting makes things a bit easier to digest</strong> at a glance. Notice that the <code>&lt;head&gt;</code> and <code>&lt;body&gt;</code> elements are indented, because they are both immediate children of the <code>&lt;html&gt;</code> element.

Of course, some developers might have a slightly different method of indenting in certain areas, but the idea is basically the same; the intention is to make the code easier to read in a development environment.</p>

## Basic CSS Indentation

In addition to indenting HTML, many developers (me included) will do matching indentation in any corresponding CSS. The following code would match the HTML shown in the first example above:

<pre><code class="language-css">header {
   color: blue;
}

   hgroup {
      color: green;
   }

      hgroup h1 {
         line-height: 1.5;
      }

      hgroup h2 {
         font-size: 15px;
      }

   nav {
      background: purple;
   }

      nav ul {
         float: left;
      }

         nav ul li {
            font-size: 20px;
         }

            nav ul li a, nav ul li a:visited {
               text-decoration: none;
            }

.main {
   border: solid 1px #ccc;
}</code></pre>

To some, <strong>this seems a bit obsessive</strong>. But I prefer it because it helps me to scan the CSS and find matching hierarchies without having to read each selector. Of course, this type of hierarchy in your CSS should be used sparingly if you’re implementing modular CSS principles that encourage class-based modules and limited use of the descendant selector (for example, <code>ul li</code>).

Certainly, some of the code above is kind of awful; I wouldn’t recommend tying your heading and list styles to a specific context like that. But for the purpose of understanding this concept of indenting CSS, look at it as a theoretical example.

The point is that you have the option to indent CSS to match the HTML’s structure, thus making it easier to scan and easier to make sense of relative to the markup.

Of course, as is the case with a few things mentioned in this post, some of this doesn’t apply when you’re using a CSS preprocessor. For example, the nested selectors option for Sass would make this last tip quite different in such an environment.

## Readable CSS3

Let’s take our abuse of white space even further. Many new CSS3 features allow for either comma-separated or space-separated value sets. Two simple examples are <a href="https://css3clickchart.com/?prop=multiple-backgrounds">multiple backgrounds</a> and <a href="https://cssvalues.com/#transform%20">transforms</a>. Let’s see how we can make these easier to read:

<pre><code class="language-css">.example {
   background: url(images/example.png) center center no-repeat,
               url(images/example-2.png) top left repeat,
               url(images/example-3.png) top right no-repeat;
}

.example-2 {
   transform: scale(.8)
              skew(20deg, 30deg)
              translateZ(0);
}</code></pre>

<strong>Notice what we’ve done here?</strong> Instead of keeping the entire value on a single line (which can get lengthy in some cases — especially when gradients and vendor prefixes are involved), we’ve put each value set on a new line, aligned with the one above it.

Thus, each of the three backgrounds is on its own line, and each transform function is on its own line, left-aligned with the first of each example.

Generally, this might go against the idea of having a single property per line (assuming, of course, that you’re not doing single-line rule sets). But when compared to the alternative of potentially really long lines, this is a good option, and it makes these rule sets very easy to read.</p>

### Dealing With Vendor Prefixes

As mentioned, if you’re <a href="https://net.tutsplus.com/tutorials/html-css-techniques/sass-vs-less-vs-stylus-a-preprocessor-shootout/">preprocessing your CSS</a> or using <a href="https://leaverou.github.com/prefixfree/">-prefix-free</a>, then this advice doesn’t apply. But you could manipulate white space to make your vendor prefixes easier to read at a glance:

<pre><code class="language-css">.example {
   -webkit-transform: scale(.8);
      -moz-transform: scale(.8);
        -o-transform: scale(.8);
           transform: scale(.8);
}</code></pre>

Here we’ve lined up the colons so that the values align, making it easy to scan all values to ensure they’re the same. I can’t tell you how many times I’ve adjusted only the WebKit value in a rule set like this and forgotten to do the rest. Of course, this illustrates <strong>the importance of preprocessing</strong>, but if you’re not doing that yet, then this use of white space is a good option to consider.

Additionally, many text editors offer a feature called “block edit” or multiline editing. This is available <a href="https://www.sublimetext.com/docs/selection">in Sublime Text</a>, <a href="https://vim.wikia.com/wiki/Inserting_text_in_multiple_lines">Vim</a>, <a href="https://www.panic.com/blog/2012/07/top-20-secrets-of-coda-2/#tip15">Coda</a> and probably most others. Using this feature is that much easier when the values you’re changing are aligned vertically.</p>

## Readable File References

The gist of this next suggestion comes from a <a href="https://twitter.com/fat/status/278010543711875073">tweet by Twitter Bootstrap cofounder Jacob Thornton</a>. The idea here is that if a list of file references is contained in your document, you can make them easier to read by doing something like the following:

<pre><code class="language-markup">
&lt;link rel="apple-touch-icon-precomposed" sizes="144x144" href="assets/ico/apple-touch-icon-144-precomposed.png"&gt;
&lt;link rel="apple-touch-icon-precomposed" sizes="114x114" href="assets/ico/apple-touch-icon-114-precomposed.png"&gt;
  &lt;link rel="apple-touch-icon-precomposed" sizes="72x72" href="assets/ico/apple-touch-icon-72-precomposed.png"&gt;
                &lt;link rel="apple-touch-icon-precomposed" href="assets/ico/apple-touch-icon-57-precomposed.png"&gt;
                               &lt;link rel="shortcut icon" href="assets/ico/favicon.png"&gt;</code></pre>

The example above is taken <a href="https://github.com/twitter/bootstrap/blob/master/docs/javascript.html">directly from Bootstrap</a>. Here, all <code>href</code> attributes of the <code>&lt;link&gt;</code> elements are aligned. This makes it easier to refer to or adjust a <code>&lt;link&gt;</code> tag because the update will usually be to the value of the <code>href</code> attribute.

Of course, this somewhat violates the rules of indenting HTML. <strong>So, alternatively, you could opt for this:</strong>

<pre><code class="language-markup tmp-html">&lt;link rel="apple-touch-icon-precomposed" sizes="144x144" href="assets/ico/apple-touch-icon-144-precomposed.png"&gt;
&lt;link rel="apple-touch-icon-precomposed" sizes="114x114" href="assets/ico/apple-touch-icon-114-precomposed.png"&gt;
&lt;link rel="apple-touch-icon-precomposed" sizes="72x72"   href="assets/ico/apple-touch-icon-72-precomposed.png"&gt;
&lt;link rel="apple-touch-icon-precomposed"                 href="assets/ico/apple-touch-icon-57-precomposed.png"&gt;
&lt;link rel="shortcut icon"                                href="assets/ico/favicon.png"&gt;</code></pre>

This latter example seems cleaner and has the bonus of aligning the other attributes, although that’s not as necessary in my opinion.

But wait. What if you don’t care that the <code>href</code> attribute is listed last (which seems to be the custom and is unnecessary for validation)? <strong>Then you could do this instead</strong>:

<pre><code class="language-markup tmp-html">&lt;link href="assets/ico/apple-touch-icon-144-precomposed.png" rel="apple-touch-icon-precomposed" sizes="144x144"&gt;
&lt;link href="assets/ico/apple-touch-icon-114-precomposed.png" rel="apple-touch-icon-precomposed" sizes="114x114"&gt;
&lt;link href="assets/ico/apple-touch-icon-72-precomposed.png" rel="apple-touch-icon-precomposed" sizes="72x72"&gt;
&lt;link href="assets/ico/apple-touch-icon-57-precomposed.png" rel="apple-touch-icon-precomposed"&gt;
&lt;link href="assets/ico/favicon.png" rel="shortcut icon"&gt;</code></pre>

<strong>No white space tricks needed here</strong>, because the <code>href</code> attributes align just fine. But if you’re bothered by the lack of alignment of the other attributes, or if you just can’t stand the thought of the <code>href</code> attribute being listed first, then you’ll have to opt for one of the preceding solutions.</p>

### Readable Conditional Classes

The concept behind the alignment of attributes is nothing new. HTML5 Boilerplate has been doing this sort of thing for some time now with its IE conditional classes. Here’s what that chunk of code looks like in the latest version:

<pre><code class="language-markup">&lt;!--[if lt IE 7]&gt;      &lt;html class="no-js lt-ie9 lt-ie8 lt-ie7"&gt; &lt;![endif]--&gt;
&lt;!--[if IE 7]&gt;         &lt;html class="no-js lt-ie9 lt-ie8"&gt; &lt;![endif]--&gt;
&lt;!--[if IE 8]&gt;         &lt;html class="no-js lt-ie9"&gt; &lt;![endif]--&gt;
&lt;!--[if gt IE 8]&gt;&lt;!--&gt; &lt;html class="no-js"&gt; &lt;!--&lt;![endif]--&gt;</code></pre>

In this case, the class attribute on the opening <code>&lt;html&gt;</code> tag in each conditional (and, incidentally, the tag itself) is being aligned, because this is the part of the code that’s most relevant to readability and maintenance, and the part of the code that would suffer most in readability if this alignment were not present.</p>

## Readable Comma-Separated Selectors

Sticking with Boilerplate, let’s go back to CSS. Here’s something used in that project’s main style sheet:

<pre><code class="language-css">html,
button,
input,
select,
textarea {
   color: #222;
}</code></pre>

Here, instead of keeping all of the comma-separated selectors on a single line — which would be more difficult to scan — each selector is put on a new line. This can be helpful when the selectors are somewhat lengthy, as in this next example, also taken from Boilerplate:

<pre><code class="language-css">.visuallyhidden.focusable:active,
.visuallyhidden.focusable:focus {
   clip: auto;
   height: auto;
   margin: 0;
   overflow: visible;
   position: static;
   width: auto;
}</code></pre>

Similar to the idea behind aligning HTML attributes discussed above, this vertical alignment makes the code a breeze to scan through when compared to scanning a single seemingly never-ending line of comma-separated selectors.</p>

## Can Your Text Editor Help With Any Of This?

As a long-time developer who has grown accustomed to coding by hand, my knowledge of the features of different text editors is fairly limited.

Some text editors or IDEs might do some of this automatically. Also, plugin developers can use some of these patterns to create plugins or extensions that do this sort of thing automatically or at the click of a button.

If you have any suggestions of built-in tools or extensions to text editors that can assist with this, I’m sure Smashing Magazine’s readers would be glad to hear about them.</p>

## Conclusion

We’re all encouraged to do whatever we can to make code in a development environment as easy to read and maintain as possible. I hope these suggestions will improve your code in this way.

And knowing that this use of white space won’t bloat our files is comforting — after all, this is not for production code. So, do whatever you feel is necessary to make your HTML and CSS easier to deal with, and be sure to minify those assets when deploying to production.

Finally, if you have any suggestions on using white space in HTML or CSS, we’d be glad to hear them.

{{< signature "al" >}}

