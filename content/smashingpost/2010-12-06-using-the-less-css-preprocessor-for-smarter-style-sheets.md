---
title: How To Use The LESS CSS Preprocessor For Smarter Style Sheets
slug: using-the-less-css-preprocessor-for-smarter-style-sheets
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bc379e97-3f17-49d5-a12e-fdbea59d232d/css-10.png
date: 2010-12-06T12:37:25.000Z
author: dmitry-fadeyev
description: >-
  As a Web designer you're undoubtedly familiar with CSS, the style sheet language used to format markup on Web pages. CSS itself is extremely simple,
  consisting of rule sets and declaration blocks—what to style, how to style it—and it does pretty much everything you want, right? Well, not quite. [Links checked March/06/2017]
categories:
  - Coding
  - CSS
  - Less
---
Enter the LESS CSS preprocessor. 

You see, while the simple design of CSS makes it very accessible to beginners, it also poses limitations on what you can do with it. These limitations, like the inability to set variables or to perform operations, mean that we inevitably end up repeating the same pieces of styling in different places. Not good for following best practices—in this case, sticking to DRY (don't repeat yourself) for less code and easier maintenance.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [An Introduction To LESS, And Comparison To Sass](https://www.smashingmagazine.com/2011/09/an-introduction-to-less-and-comparison-to-sass/)
*   [The “Other” Interface: Atomic Design With Sass](https://www.smashingmagazine.com/2013/08/other-interface-atomic-design-sass/)
*   [Smarter Grids With Sass And Susy](https://www.smashingmagazine.com/2015/07/smarter-grids-with-sass-and-susy/)
*   [Extending In Sass Without Creating A Mess](https://www.smashingmagazine.com/2015/05/extending-in-sass-without-mess/)

In simple terms, CSS preprocessing is a method of extending the feature set of CSS by first writing the style sheets in a new extended language, then compiling the code to vanilla CSS so that it can be read by Web browsers. Several CSS preprocessors are available today, most notably <a href="https://sass-lang.com/">Sass</a> and <a href="https://lesscss.org/">LESS</a>.

{{% feature-panel %}}

<a href="https://lesscss.org/index.html"><img loading="lazy" decoding="async"  class="alignnone" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f7aee31a-8604-4d53-a4ee-0423f4329018/less-css.jpg" alt="less css" width="550" height="415" /></a>

What's the difference? Sass was designed to both simplify and extend CSS, so things like curly braces were removed from the syntax. LESS was designed to be as close to CSS as possible, so the syntax is identical to your current CSS code. This means you can use it right away with your existing code. Recently, Sass also introduced a CSS-like syntax called SCSS (Sassy CSS) to make migrating easier.</p>

### If It Ain't Broke…?

By now you might be thinking, “So what? Why should I care about these things, and how exactly will they make my life as a Web designer easier?” I'll get to that in a moment, and I promise it will be worth your time. First, let me clarify the focus of this article.

In this tutorial, I'll be using LESS to demonstrate how CSS preprocessing can help you code CSS faster. But that doesn't mean you <em>must</em> use LESS. It's my tool of choice, but you may find that Sass fits your workflow better, so I suggest giving them both a shot. I'll talk a bit more about their differences at the end of the article.

I'll start off by explaining how LESS works and how to install it. After, I'll list a set of problems that large CSS files pose, one by one, and exactly how you can use LESS to solve them.

Let's go!

## Installing It

There are two parts to any CSS preprocessor: the language and the compiler. The language itself is what you'll be writing. LESS looks just like CSS, except for a bunch of extra features. The compiler is what turns that LESS code into standard CSS that a Web browser can read and process.

Many different compilers are actually available for LESS, each programmed in a different language. There's a <a href="https://lesscss.org/">Ruby Gem</a>, a <a href="https://leafo.net/lessphp/">PHP version</a>, a <a href="https://www.dotlesscss.org/">.NET version</a>, an <a href="https://incident57.com/less/">OS X app</a> and one written in <a href="https://github.com/cloudhead/less.js">JavaScript</a>. Some of these are platform-specific, like the OS X app. For this tutorial, I recommend the JavaScript version (less.js) because it's the easiest to get started with.

Using the JavaScript compiler is extremely easy. Simply include the script in your HTML code, and then it will process LESS live as the page loads. We can then include our LESS file just as we would a standard style sheet. Here's the code to put between the <code>&lt;head&gt;</code> tags of your mark-up:

<pre><code class="language-markup tmp-xml">&lt;link rel="stylesheet/less" href="/stylesheets/main.less" type="text/css" /&gt;
&lt;script src="https://lesscss.googlecode.com/files/less-1.0.30.min.js"&gt;&lt;/script&gt;</code></pre>

Note that I'm referencing the less.js script directly from the Google Code server. With this method, you don't even have to download the script to use it. The style sheet link goes above the script to ensure it gets loaded and is ready for the preprocessor. Also, make sure that the <code>href</code> value points to the location of your <code>.less</code> file.

That's it. We can now begin writing LESS code in our <code>.less</code> file. Let's go ahead and see how LESS makes working with CSS easier.</p>

## 1\. Cleaner Structure With Nesting

In CSS, we write out every rule set separately, which often leads to long selectors that repeat the same stuff over and over. Here's a typical example:

<pre><code class="language-css">#header {}
#header #nav {}
#header #nav ul {}
#header #nav ul li {}
#header #nav ul li a {}</code></pre>

LESS allows us to nest rule sets inside other rule sets, as a way to show hierarchy. Let's rewrite the above example with nesting:

<pre><code class="language-css"># header {
  #nav {
    ul {
      li {
        a {}
      }
    }
  }
}</code></pre>

I've omitted the content from the selectors for simplicity, but you can see how the structure of the code quickly changes. Now you don't have to repeat selectors over and over again; simply nest the relevant rule set inside another to indicate the hierarchy. It's also a great way to keep code organized because it groups related items together visually.

Also, if you want to give pseudo-classes this nesting structure, you can do so with the <code>&amp;</code> symbol. Pseudo-classes are things such as <code>:hover</code>, <code>:active</code> and <code>:visited</code>. Your code would look as follows:

<pre><code class="language-css">a {
  &amp;:hover {}
  &amp;:active {}
  &amp;:visited {}
}</code></pre>

## 2\. Variables For Faster Maintenance

We usually apply a palette of colors across an entire website. Any given color could be used for multiple items and so would be repeated throughout the CSS code. To change the color, you'd have to do a "Find and replace."

But that's not quite it. You could also isolate those values into separate rule sets; but with this method, the rule sets would keep growing as you add more colors across the website, leading to bloated selectors. Here's what I'm talking about:

<pre><code class="language-css">#header, #sidebar .heading, #sidebar h2, #footer h3, .aside h3 { color: red; }</code></pre>

To make a simple color change, we're faced with long selectors, all dedicated to that one color. It's not pretty. LESS allows us to specify variables in one place—such as for brand colors, border lengths, side margins and so on—and then reuse the variables elsewhere in the style sheet. The value of the variable remains stored in one place, though, so making a change is as simple as changing that one line. Variables start with an <code>@</code> and are written like this:

<pre><code class="language-css">@brand-color: #4455EE;

#header { background-color: @brand-color; }
#footer { color: @brand-color; }
h3 { color: @brand-color; }</code></pre>

In LESS, variables also have scope, so you could use variables with the same name in various places; when they're called, the compiler would check for the variable locally first (i.e. is there anything with that name where the declaration is currently nested?), and then move up the hierarchy until it finds it. For example, the following code:

<pre><code class="language-css">@great-color: #4455EE;

#header {
  @great-color: #EE3322;
  color: @great-color;
}</code></pre>

…compiles to:

<pre><code class="language-css">#header { color: #EE3322; }</code></pre>

## 3\. Reusing Whole Classes

Variables are great, but we often reuse more than single values. A good example is code that's different for every browser, like the CSS3 property <code>border-radius</code>. We have to write at least three declarations just to specify it:

<pre><code class="language-css">-webkit-border-radius: 5px;
-moz-border-radius: 5px;
border-radius: 5px;</code></pre>

If you use a lot of CSS3, then this sort of repeating code adds up quickly. LESS solves this by allowing us to reuse whole classes simply by referencing them in our rule sets. For example, let's create a new class for the above <code>border-radius</code> and reuse it in another rule set:

<pre><code class="language-css">.rounded-corners {
  -webkit-border-radius: 5px;
  -moz-border-radius: 5px;
  border-radius: 5px;
}
#login-box {
  .rounded-corners;
}</code></pre>

Now <code>#login-box</code> will inherit the properties of the <code>rounded-corners</code> class. But what if we want more control over the size of the corners? No problem. We can pass along variables to the "mixin" (these reusable classes are called mixins) to get a more specific outcome. First, we rewrite the original mixin to add the variable we want to manipulate:

<pre><code class="language-css">.rounded-corners(@radius: 5px) {
  -webkit-border-radius: @radius;
  -moz-border-radius: @radius;
  border-radius: @radius;
}</code></pre>

Now we've replaced the values for a variable, and we've specified the default value inside the parentheses. To give mixins multiple values, you'll just need to separate them with a comma. Now, if we want our <code>#login-box</code> to have a border radius of three pixels instead of five, we do this:

<pre><code class="language-css">#login-box {
  .rounded-corners(3px);
}</code></pre>

## 4\. Operations

Variables let us specify things such as common palettes of colors, but what about relative design elements, like text that's just a bit lighter than the background, or an inner border that's one pixel thicker than the outer border?

Rather than add more variables, we can perform operations on existing values with LESS. For example, we can make colors lighter or darker or add values to borders and margins. And when we change the value that these operations depend on, they update accordingly. Take the following:

<pre><code class="language-css">@base-margin: 25px;
#header { margin-top: @base-margin + 10px; }</code></pre>

This gives the <code>#header</code> element a top margin of 35 pixels. You can, of course, also multiply, divide and subtract, and perform operations on colors like <code>#888 / 4</code> and <code>#EEE + #111</code>.</p>

## 5\. Namespaces and Accessors

What if you want to group variables or mixins into separate bundles? You can do this by nesting them inside a rule set with an <code>id</code>, like <code>#defaults</code>. Mixins can also be grouped in this way:

<pre><code class="language-css">#defaults {
  @heading-color: #EE3322;
  .bordered { border: solid 1px #EEE; }
}</code></pre>

Then, to call a variable and a mixin from that particular group, we do this:

<pre><code class="language-css">h1 {
  color: #defaults[@heading-color];
  #defaults &gt; .bordered;
}</code></pre>

We can even access values of other properties in a given rule set directly, even if they're not variables. So, to give the sidebar heading the same color as your main <code>h1</code> heading, you'd write:

<pre><code class="language-css">h1 { color: red; }

.sidebar_heading { color: h1['color']; }</code></pre>

There's not much difference between variables and accessors, so use whichever you prefer. Accessors probably make more sense if you will be using the value only once. Variable names can add semantic meaning to the style sheet, so they make more sense when you look at them at a later date.
A couple more things to mention: You can use two slashes, <code>//</code>, for single-line comments. And you can import other LESS files, just as in CSS, with <code>@import</code>:

<pre><code class="language-css">@import 'typography';
@import 'layout';</code></pre>

## LESS CSS Conclusion

I hope by now you've got a pretty good idea why CSS preprocessors exist, and how they can make your work easier. The JavaScript version of the LESS compiler, less.js, is of course just one way to use LESS. It's probably the easiest to get started with, but it also has some downsides, the biggest one being that the compiling takes place live. This isn't a problem on modern browsers with fast JavaScript engines, but it might work slower on older browsers. Note that less.js actually caches the CSS once it's processed, so the CSS isn't regenerated for each user.

To use the generated CSS instead of LESS in your markup, you can compile your files using the various other compilers. If you're on OS X, I suggest trying out the <a href="https://incident57.com/less/">LESS App</a>, a desktop app that watches your LESS files for changes as you work and automatically compiles them into CSS files when you update them. The Ruby Gem has the same watcher functionality but is trickier to install if you're not familiar with Ruby (see the <a href="https://lesscss.org/">official website</a> for details on that). There are also <a href="https://leafo.net/lessphp/">PHP</a> and <a href="https://www.dotlesscss.org/">.NET</a> versions.

Finally, LESS isn't your only option for a CSS preprocessor. The other popular choice is <a href="https://sass-lang.com/">Sass</a>, but there are still more options to check out, such as <a href="https://xcss.antpaw.org/">xCSS</a>. The advantage of LESS is that it uses existing CSS syntax, so getting started is just a matter of renaming your <em>.css</em> file to <em>.less</em>. This might be a disadvantage if you dislike the CSS syntax and curly braces, in which case Sass would probably be a better choice. There is also the <a href="https://compass-style.org/">Compass</a> framework available for Sass, which is worth checking out if you go with Sass.

<em>(al) (sp)</em>

