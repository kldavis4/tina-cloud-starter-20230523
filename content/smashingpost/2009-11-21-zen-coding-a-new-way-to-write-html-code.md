---
title: 'Zen Coding: A Speedy Way To Write HTML/CSS Code'
slug: zen-coding-a-new-way-to-write-html-code
image: null
date: 2009-11-21T18:58:00.000Z
author: sergey-chikuyonok
description: >-
  In this post we present a new speedy way of writing HTML code using CSS-like
  selector syntax — a handy set of tools for high-speed HTML and CSS coding. It
  was developed by our author Sergey Chikuyonok and released for Smashing
  Magazine and its readers.
categories:
  - Coding
  - Tools
  - CSS
  - HTML
---
<em>In this post we present a new speedy way of writing HTML code using CSS-like selector syntax — a handy set of tools for high-speed HTML and CSS coding. It was developed by our author Sergey Chikuyonok and released for Smashing Magazine and its readers.</em>

How much time do you spend writing HTML code: all of those tags, attributes, quotes, braces, etc. You have it easier if your editor of choice has code-completion capabilities, but you still do a lot of typing. 

You may want to take a look at the following related posts:

*   [<span class="headline">Goodbye, Zen Coding. Hello, Emmet!</span>](https://www.smashingmagazine.com/2013/03/goodbye-zen-coding-hello-emmet/)
*   [Challenging CSS Best Practices](https://www.smashingmagazine.com/2013/10/challenging-css-best-practices-atomic-approach/)
*   [Responsive Design Frameworks: Just Because You Can, Should You?](https://www.smashingmagazine.com/2014/02/responsive-design-frameworks-just-because-you-can-should-you/)

We had the same problem in JavaScript world when we wanted to access a specific element on a Web page. We had to write a lot of code, which became really hard to support and reuse. And then JavaScript frameworks came along, which introduced CSS selector engines. Now, you can use simple CSS expressions to access DOM elements, which is pretty cool.

{{% feature-panel %}}

But what if you could use CSS selectors not just to style and access elements, but to <em>generate code</em>? For example, what if you could write this...

<pre><code class="language-markup tmp-xml">div#content&gt;h1+p</code></pre>

...and see this as the output?

<pre><code class="language-markup tmp-xml">&lt;div id="content"&gt;
&lt;h1&gt;&lt;/h1&gt;
&lt;p&gt;&lt;/p&gt;
&lt;/div&gt;</code></pre>

Today, we'll introduce you to <a href="https://code.google.com/p/zen-coding/">Zen Coding</a>, a set of tools for high-speed HTML and CSS coding. Originally <a href="https://pepelsbey.net/2009/04/zen-coding-concept/">proposed by Vadim Makeev</a> (article in Russian) back in April 2009, it has been developed by yours truly (i.e. me) for the last few months and has finally reached a mature state. Zen Coding consists of two core components: an abbreviation expander (abbreviations are CSS-like selectors) and context-independent HTML-pair tag matcher. Watch this demo video to see what they can do for you.

If you'd like to skip the detailed instructions and usage guide, please take a look at the demo and download your plugin right away:

### Demo

*   [Demo](https://code.google.com/archive/p/zen-coding/) (use _Ctrl + ,_ to expand an abbreviation, requires JavaScript)

### Downloads (Full Support)

*   [Aptana](https://code.google.com/p/zen-coding/downloads/detail?name=Zen.Coding-Aptana.v0.5.zip) (cross-platform);
*   Coda, via [TEA for Coda](https://github.com/sergeche/tea-for-coda/downloads) (Mac);
*   Espresso, via [TEA for Espresso](https://github.com/sergeche/tea-for-espresso/downloads) (Mac);

### Downloads (Partial Support, "Expand Abbreviation" Only)

*   [TextMate](https://code.google.com/p/zen-coding/downloads/detail?name=Zen%20Coding%20for%20TextMate%20v0.3.1.zip) (Mac, and can be used with E-text editor for Windows);
*   [TopStyle](https://code.google.com/p/zen-coding/downloads/detail?name=TopStyle.Zen.Coding.1.0.zip);
*   [Sublime Text](https://code.google.com/p/zen-coding/downloads/detail?name=Sublime.Zen.Coding.1.1.3.zip);
*   [GEdit](https://www.kryogenix.org/days/2009/09/21/zen-coding-for-gedit);
*   [editArea online editor](https://code.google.com/archive/p/zen-coding/);

Now, let's see how these tools work.</p>

## Expand Abbreviation

The Expand Abbreviation function transforms CSS-like selectors into XHTML code. The term "abbreviation" might be a little confusing. Why not just call it a "CSS selector"? Well, the first reason is semantic: "selector" means to <em>select</em> something, but here we're actually <em>generating</em> something, <strong>writing a shorter representation of longer code</strong>. Secondly, it supports only a small subset of real CSS selector syntax, in addition to introducing some new operators.

Here is a list of supported properties and operators:

*   E Element name (`div`, `p`);
*   E#id Element with identifier (`div#content`, `p#intro`, `span#error`);
*   E.class Element with classes (`div.header`, `p.error.critial`). You can combine classes and IDs, too: `div#content.column.width`;
*   E>N Child element (`div>p`, `div#footer>p>span`);
*   E+N Sibling element (`h1+p`, `div#header+div#content+div#footer`);
*   E*N Element multiplication (`ul#nav>li*5>a`);
*   E$*N Item numbering (`ul#nav>li.item-$*5`);

As you can see, you already know how to use Zen Coding: just write a simple CSS-like selector (oh, "abbreviation"—sorry), like so...

<pre><code class="language-markup tmp-xml">div#header&gt;img.logo+ul#nav&gt;li*4&gt;a</code></pre>

...and then call the Expand Abbreviation action.

There are two custom operators: element multiplication and item numbering. If you want to generate, for example, five <code>&lt;li&gt;</code> elements, you would simply write <code>li*5</code>. It would repeat all descendant elements as well. If you wanted four <code>&lt;li&gt;</code> elements, with an <code>&lt;a&gt;</code> in each, you would simply write <code>li*4&gt;a</code>, which would generate the following output:

<pre><code class="language-markup tmp-xml">&lt;li&gt;&lt;a href=""&gt;&lt;/a&gt;&lt;/li&gt;
&lt;li&gt;&lt;a href=""&gt;&lt;/a&gt;&lt;/li&gt;
&lt;li&gt;&lt;a href=""&gt;&lt;/a&gt;&lt;/li&gt;
&lt;li&gt;&lt;a href=""&gt;&lt;/a&gt;&lt;/li&gt;</code></pre>

The last one–item numbering is used when you want to mark a repeated element with its index. Suppose you want to generate three <code>&lt;div&gt;</code> elements with <code>item1</code>, <code>item2</code> and <code>item3</code> classes. You would write this abbreviation, <code>div.item$*3</code>:

<pre><code class="language-markup tmp-xml">&lt;div class="item1"&gt;&lt;/div&gt;
&lt;div class="item2"&gt;&lt;/div&gt;
&lt;div class="item3"&gt;&lt;/div&gt;</code></pre>

Just add a dollar sign wherever in the class or ID property that you want the index to appear, and as many an you want. So, this...

<pre><code class="language-markup tmp-xml">div#i$-test.class$$$*5</code></pre>

would be transformed into:

<pre><code class="language-markup tmp-xml">&lt;div id="i1-test" class="class111"&gt;&lt;/div&gt;
&lt;div id="i2-test" class="class222"&gt;&lt;/div&gt;
&lt;div id="i3-test" class="class333"&gt;&lt;/div&gt;
&lt;div id="i4-test" class="class444"&gt;&lt;/div&gt;
&lt;div id="i5-test" class="class555"&gt;&lt;/div&gt;</code></pre>

You'll see that when you write the <code>a</code> abbreviation, the output is <code>&lt;a href=""&gt;&lt;/a&gt;</code>. Or, if you write <code>img</code>, the output is <code>&lt;img src="" alt="" /&gt;</code>.

How does Zen Coding know when it should add default attributes to the generated tag or skip the closing tag? A special file, called <em>zen_settings.js</em> describes the outputted elements. It's a simple JSON file that describes the abbreviations for each language (yes, you can define abbreviations for different syntaxes, such as HTML, XSL, CSS, etc.). The common language abbreviations definition looks like this:

<pre><code class="language-javascript">'html': {
'snippets': {
'cc:ie6': '&lt;!--[if lte IE 6]&gt;nt${child}|n&lt;![endif]--&gt;',
...
}, 

'abbreviations': {
'a': '&lt;a href=""&gt;&lt;/a&gt;',
'img': '&lt;img src="" alt="" /&gt;',
...
}
}</code></pre>

### Element Types

Zen Coding has two major element types: <strong>"snippets" and "abbreviations."</strong> Snippets are arbitrary code fragments, while abbreviations are tag definitions. With snippets, you can write anything you want, and it will be outputted as is; but you have to manually format it (using <code>n</code> and <code>t</code> for new lines and indentation) and put the <code>${child}</code> variable where you want to output the child elements, like so: <code>cc:ie6&gt;style</code>. If you don't include the <code>${child}</code> variable, the child elements are outputted <em>after</em> the snippet.

With abbreviations, you have to write tag definitions, and the syntax is very important. Normally, you have to write a simple tag with all default attributes in it, like so: <code>&lt;a href=""&gt;&lt;/a&gt;</code>. When Zen Coding is loaded, it parses a tag definition into a special object that describes the tag's name, attributes (including their order) and whether the tag is empty. So, if you wrote <code>&lt;img src="" alt="" /&gt;</code>, you would be telling Zen Coding that this tag must be empty, and the "Expand Abbreviation" action would apply special rules to it before outputting.

For both snippets and abbreviations, you can ad a pipe character (|), which tells Zen Coding where it should place the cursor when the abbreviation is expanded. By default, Zen Coding puts the cursor between quotes in empty attributes and between the opening and closing tag.</p>

### Example

So, here's what happens when you write an abbreviation and call the "Expand Abbreviation" action. First, it splits a whole abbreviation into separate elements: so, <code>div&gt;a</code> would be split into <code>div</code> and <code>a</code> elements, with their relationship preserved. Then, for each element, the parser looks for a definition inside the snippets and then inside the abbreviations. If it doesn't find one, it uses the element's name as the name for the new tag, applying ID and class attributes to it. For example, if you write <code>mytag#example</code>, and the parser cannot find the <code>mytag</code> definition among the snippets or abbreviation, it will output <code>&lt;mytag id="example"&gt;&lt;mytag&gt;</code>.

We have made a lot of <a href="https://code.google.com/p/zen-coding/wiki/ZenCSSPropertiesEn">default CSS</a> and <a href="https://code.google.com/p/zen-coding/wiki/ZenHTMLElementsEn">HTML abbreviations and snippets</a>. You may find that learning them increases your productivity with Zen Coding.</p>

## HTML Pair Matcher

Another very common task for the HTML coder is to find the tag pair of an element (also known as "balancing"). Let's say you want to select the entire <code>&lt;div id="content"&gt;</code> tag and move it elsewhere or just delete it. Or perhaps you're looking at a closing tag and want to known which opening tag it belongs to.

Unfortunately, many modern development tools lack support for this feature. So, I decided to write my own tag matcher as part of Zen Coding. It is still in beta and has some issues, but it works quite well and is fast. Instead of scanning the full document (as regular HTML pair matchers do), it finds the relevant tag from the cursor's current position. This makes it very fast and <em>context-independent</em>: it works even with this <strong>JavaScript code snippet</strong>:

<pre><code class="language-javascript">var table = '&lt;table&gt;';
for (var i = 0; i &lt; 3; i++) {
table += '&lt;tr&gt;';
for (var j = 0; j &lt; 5; j++) {
table += '&lt;td&gt;' + j + '&lt;/td&gt;';
}
table += '&lt;/tr&gt;';
}
table += '&lt;/table&gt;';</code></pre>

## Wrapping With Abbreviation

This is a really cool feature that combines the power of the abbreviation expander with the pair tag matcher. How many times have you found that you have to <strong>add a wrapping element to fix a browser bug</strong>? Or perhaps you have had to add decoration, such as a background image or border, to a block's content? You have to write the opening tag, temporarily break your code, find the appropriate spot and then close the tag. Here's where "Wrap with Abbreviation" helps.

This function is pretty simple: it asks you to enter the abbreviation, then it performs the regular "Expand Abbreviation" action and puts your desired text <em>inside the last element</em> of your abbreviation. If you haven't selected any text, it fires up the pair matcher and use the result. It also makes sense of where your cursor is: inside the tag's content or within the opening and closing tag. Depending on where it is, it wraps the tag's content or the tag itself.

Abbreviation wrapping introduces a special abbreviation syntax for wrapping individual lines. Simply skip the number after the multiplication operator, like so: <code>ul#nav&gt;li*&gt;a</code>. When Zen Coding finds an element with an undefined multiplication number, it uses it as a <em>repeating element</em>: it is outputted as many times as there are lines in your selection, putting the content of each line inside the <em>deepest child</em> of the repeating element.

If you'll wrap this abbreviation <code>div#header&gt;ul#navigation&gt;li.item$*&gt;a&gt;span</code> around this text...

<pre><code class="language-markup tmp-none">About Us
Products
News
Blog
Contact Up</code></pre>

You'll get the following result:

<pre><code class="language-markup tmp-xml">&lt;div id="header"&gt;
&lt;ul id="navigation"&gt;
&lt;li class="item1"&gt;&lt;a href=""&gt;&lt;span&gt;About Us&lt;/span&gt;&lt;/a&gt;&lt;/li&gt;
&lt;li class="item2"&gt;&lt;a href=""&gt;&lt;span&gt;Products&lt;/span&gt;&lt;/a&gt;&lt;/li&gt;
&lt;li class="item3"&gt;&lt;a href=""&gt;&lt;span&gt;News&lt;/span&gt;&lt;/a&gt;&lt;/li&gt;
&lt;li class="item4"&gt;&lt;a href=""&gt;&lt;span&gt;Blog&lt;/span&gt;&lt;/a&gt;&lt;/li&gt;
&lt;li class="item5"&gt;&lt;a href=""&gt;&lt;span&gt;Contact Up&lt;/span&gt;&lt;/a&gt;&lt;/li&gt;
&lt;/ul&gt;
&lt;/div&gt;</code></pre>

You can see that Zen Coding is quite a powerful text-processing tool.
<div id="zen-coding-info"><br>
## Key Bindings
<ul>
 	<li><code>Ctrl+,</code>
Expand Abbreviation</li>
 	<li><code>Ctrl+M</code>
Match Pair</li>
 	<li><code>Ctrl+H</code>
Wrap with Abbreviation</li>
 	<li><code>Shift+Ctrl+M</code>
Merge Lines</li>
 	<li><code>Ctrl+Shift+?</code>
Previous Edit Point</li>
 	<li><code>Ctrl+Shift+?</code>
Next Edit Point</li>
 	<li><code>Ctrl+Shift+?</code>
Go to Matching Pair</li>
</ul>
</div>

## Online Demo

You've learned a lot about how Zen Coding works and how it can make your coding easier. Why not try it yourself now, right here? Because Zen Coding is written in pure JavaScript and ported to Python, it can even work inside the browser, which makes it a prime candidate for including in a CMS.

*   [Demo](https://code.google.com/archive/p/zen-coding/) (use _Ctrl + ,_ to expand an abbreviation, requires JavaScript)

## Supported Editors

Zen Coding doesn't depend on any particular editor. It's a stand-alone component that works with text only: it takes text, does something to it and then returns new text (or indexes, for tag matching). Zen Coding is written in JavaScript and Python, so it can run on virtually any platform out of the box. On Windows, you can run the JavaScript version of Windows Scripting Host. And modern Macs and Linux distributions are bundled with Python.

To make your editor support Zen Coding, you need to write a special plug-in that can transfer data between your editor and Zen Coding. The problem is that an editor may not have full Zen Coding support because of its plug-in system. For example, <a href="https://macromates.com/">TextMate</a> easily supports the "Expand Abbreviation" action by replacing the current line with the script output, but it can't handle pair-tag matching because there's no standard way to ask TextMate to select something.</p>

### Full Support

*   [Aptana](https://code.google.com/p/zen-coding/downloads/detail?name=Zen.Coding-Aptana.v0.5.zip) (cross-platform);
*   Coda, via [TEA for Coda](https://github.com/sergeche/tea-for-coda/downloads) (Mac);
*   Espresso, via [TEA for Espresso](https://github.com/sergeche/tea-for-espresso/downloads) (Mac);

### Partial Support ("Expand Abbreviation" Only)

*   [TextMate](https://code.google.com/p/zen-coding/downloads/detail?name=Zen%20Coding%20for%20TextMate%20v0.3.1.zip) (Mac, and can be used with E-text editor for Windows);
*   [TopStyle](https://code.google.com/p/zen-coding/downloads/detail?name=TopStyle.Zen.Coding.1.0.zip);
*   [Sublime Text](https://code.google.com/p/zen-coding/downloads/detail?name=Sublime.Zen.Coding.1.1.3.zip);
*   [GEdit](https://www.kryogenix.org/days/2009/09/21/zen-coding-for-gedit);
*   [editArea online editor](https://code.google.com/archive/p/zen-coding/);

Aptana is my primary development environment, and it uses a JavaScript version of Zen Coding. It also contains many more tools that I use for routine work. Every new version of Zen Coding will be available for Aptana first, then ported to Python and made available to other editors.

The Coda and Espresso plug-ins are powered by the excellent <a href="https://onecrayon.com/tea/">Text Editor Actions</a> (TEA) platform, developed by <a href="https://beckism.com/">Ian Beck</a>. The original source code is <a href="https://github.com/onecrayon">available at GitHub</a>, but I made <a href="https://github.com/sergeche/">my own fork</a> to integrate Zen Coding's features.</p>

## Conclusion

Many people who have tried Zen Coding have said that it has changed their way of creating Web pages. There's still a lot of work to do, many editors to support and much documentation to write. Feel free to browse the <a href="https://code.google.com/p/zen-coding/w/list">existing documentation</a> and source code to find answers to your questions. Hope you enjoy Zen Coding!

{{< signature "al" >}}

