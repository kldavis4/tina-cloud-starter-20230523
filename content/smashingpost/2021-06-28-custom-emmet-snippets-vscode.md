---
title: 'Creating Custom Emmet Snippets In VS Code'
slug: custom-emmet-snippets-vscode
author: manuelmatuzovic
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b7ff6227-3a15-4237-8e58-aa783fc9c485/custom-emmet-snippets-vscode.jpg
date: 2021-06-28T10:30:00.000Z
summary: >-
   In this article, Manuel explains why Emmet is one of his favorite productivity tools for writing HTML and CSS, and how you can create custom Emmet snippets in Visual Studio Code to help you improve your front-end workflows even more.
description: >-
  In this article, Manuel explains why Emmet is one of his favorite productivity tools for writing HTML and CSS, and how you can create custom Emmet snippets in Visual Studio Code to help you improve your front-end workflows even more.
categories:
  - Tools
  - Coding
  - Techniques
---

Earlier this year, I shared the [HTML boilerplate](https://www.matuzo.at/blog/html-boilerplate/) I like to use when starting new web projects with line-by-line explanations on my blog. It’s a collection of mostly `<head>` tags and attributes I usually use on every website I build. Until recently, I would just copy and paste the boilerplate whenever I needed it, but I’ve decided to improve my workflow by adding it as a snippet to [VS Code](https://code.visualstudio.com/) &mdash; the editor of my choice.

{{< vimeo id="568343576" caption="Here’s a quick demo of the custom snippets I’ve created." >}}

## Snippets And Abbreviations In Visual Studio Code

VS Code comes built-in with custom [user snippets](https://code.visualstudio.com/docs/editor/userdefinedsnippets) and [HTML and CSS snippets and abbreviations](https://docs.emmet.io/cheat-sheet/) provided by [Emmet](https://emmet.io/).

For example, if you type `p>a{Sign Up}` in an HTML document and press <kbd>Enter</kbd> or <kbd>Tab</kbd>, Emmet will turn it into the following markup:

<pre><code class="language-markup">&lt;p&gt;&lt;a href=""&gt;Sign Up&lt;/a&gt;&lt;/p&gt;
</code></pre>

**Note**: *Visit the [Emmet docs](https://docs.emmet.io/) to learn how to use the [abbreviation syntax](https://docs.emmet.io/abbreviations/syntax/).*

If we need this specific abbreviation regularly, we can save it as a snippet to improve our workflow even more.

<pre><code class="language-html">{
  "html": {
    "snippets": {
      "signup": "p>a{Sign Up}"
    }
  }
}
</code></pre>

Now we can type `signup` and press <kbd>Enter</kbd> or <kbd>Tab</kbd> and we’ll get the same result. I’ll explain how to create snippets in the <a href="#custom-html-snippets">next section</a>.

Emmet comes with [a bunch of HTML snippets](https://github.com/emmetio/snippets/blob/master/html.json) by default. For example, `!` creates the basic structure of an HTML document.

<pre><code class="language-html">&lt;!DOCTYPE html&gt;
&lt;html lang="en"&gt;
&lt;head&gt;
  &lt;meta charset="UTF-8"&gt;
  &lt;meta http-equiv="X-UA-Compatible" content="IE=edge"&gt;
  &lt;meta name="viewport" content="width=device-width, initial-scale=1.0"&gt;
  &lt;title&gt;Document&lt;/title&gt;
&lt;/head&gt;
&lt;body&gt;
  
&lt;/body&gt;
&lt;/html&gt;
</code></pre>

That’s great, but if we want to adapt this snippet by removing or adding elements and attributes, we have to overwrite it and create our own snippet.

## Creating And Overwriting Snippets

If we want to create our own Emmet snippets or overwrite existing ones in VS Code, the following steps are necessary:

<ol>
  <li>Create a <em>snippets.json</em> file, add this basic JSON structure and save it somewhere on your hard disk.<br />

<pre><code class="language-json">{
  "html": {
    "snippets": {
    }
  },
  "css": {
    "snippets": {
    }
  }
}
</code></pre>
</li>
<li>Open the VS Code settings (Code&nbsp;&rarr; Preferences&nbsp;&rarr; Settings) and search for “Emmet Extensions Path”.<br />

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f2e5ec5b-964e-4e8e-89c9-9603549793db/1-custom-emmet-snippets-vscode.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f2e5ec5b-964e-4e8e-89c9-9603549793db/1-custom-emmet-snippets-vscode.png" width="800" height="" sizes="100vw" caption="" alt="" >}}
</li>
<li>Click “Add Item”, enter the path to the folder where you’ve saved the <em>snippets.json</em> file you’ve created earlier and press “OK”.<br />

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4ffcf7dc-c7b6-485a-9699-c08340ee41b3/2-custom-emmet-snippets-vscode.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4ffcf7dc-c7b6-485a-9699-c08340ee41b3/2-custom-emmet-snippets-vscode.png" width="800" height="" sizes="100vw" caption="" alt="" >}}
</li>
</ol>

That’s it. Now we’re ready to create snippets by adding properties to the `html` and `css` objects where the `key` is the name of the snippet and the `value` an abbreviation or a string.

## Some Of My Custom HTML Snippets

Before we dive deep into snippet creation and I show you how I created a snippet for my HTML boilerplate, let’s warm up first with some small, but useful snippets I’ve created, as well.

### Lazy Loading

Out of the box, there’s an `img` abbreviation, but there’s none for lazily loaded images. We can use the default abbreviation and just add the additional attributes and attribute values we need in square brackets.

<pre><code class="language-css">{
  "html": {
    "snippets": {
      "img:l": "img[width height loading='lazy']"
    }
  }
}
</code></pre>

`img:l` + <kbd>Enter</kbd>/<kbd>Tab</kbd> now creates the following markup:

<pre><code class="language-markup">&lt;img src="" alt="" width="" height="" loading="lazy"&gt;
</code></pre>

### Page

Most pages I create consist of `<header>`, `<main>` and `<footer>` landmarks and an `<h1>`. The custom `page` abbreviation lets me create that structure quickly.

<pre><code class="language-css">"snippets": {
  "page": "header>h1^main+footer{${0:&copy;}}"
}
</code></pre>

`page` + <kbd>Enter</kbd>/<kbd>Tab</kbd> creates the following markup:

<pre><code class="language-markup">&lt;header&gt;
  &lt;h1&gt;&lt;/h1&gt;
&lt;/header&gt;
&lt;main&gt;&lt;/main&gt;
&lt;footer&gt;&copy;&lt;/footer&gt;
</code></pre>

That abbreviation is quite long, so let’s break it down into smaller bits.

#### Breakdown

Create an `<header>` element and a child `<h1>`.

<pre><code class="language-markup">header>h1
</code></pre>

Move up, back to the level of the `<header>`, and create a `<footer>` that follows `<main>`.

<pre><code class="language-markup">^main+footer
</code></pre>

Set the final tab stop within the `<footer>` and set the default text to `&copy`.

<pre><code class="language-markup">{${0:&copy;}}
</code></pre>

### Navigation

The abbreviation `nav` just creates a `<nav>` start and end tag by default, but what I usually need is a `<nav>` with a nested `<ul>`, `<li>` elements and links ( `<a>`). If there are multiple `<nav>` elements on a page, they should also be labeled, for example by using `aria-label`.

<pre><code class="language-markup">"nav": "nav[aria-label='${1:Main}']>ul>(li>a[aria-current='page']{${2:Current Page}})+(li*3>a{${0:Another Page}})"
</code></pre>

That looks wild, so let’s break it down again.

#### Breakdown

We start with a `<nav>` element with an `aria-label` attribute and a nested `<ul>`. `${1:Main}` populates the attribute with the text “Main” and creates a tab stop at the attribute value by moving the cursor to it and highlighting it upon creation.

<pre><code class="language-markup">nav[aria-label='${1:Main}']>ul
</code></pre>

Then we create four list items with nested links. The first item is special because it marks the active page using `aria-current="page"`. We create another tab stop and populate the link with the text “Current Page”.

<pre><code class="language-markup">(li>a[aria-current='page']>{${2:Current Page}})
</code></pre>

Finally, we add three more list items with links and the link text “Another page”.

<pre><code class="language-markup">(li*3>a>{${0:Another Page}})
</code></pre>

Before our adaptations, we got this:

<pre><code class="language-markup"><-- Before: nav + TAB/Enter --&gt;  
&lt;nav&gt;&lt;/nav&gt;
</code></pre>

Now we get this:

<pre><code class="language-markup">&lt;-- After: nav + TAB/Enter --&gt;

&lt;nav aria-label="Main"&gt;
  &lt;ul&gt;
    &lt;li&gt;&lt;a href="" aria-current="page"&gt;Current Page&lt;/a&gt;&lt;/li&gt;
    &lt;li&gt;&lt;a href=""&gt;Another Page&lt;/a&gt;&lt;/li&gt;
    &lt;li&gt;&lt;a href=""&gt;Another Page&lt;/a&gt;&lt;/li&gt;
    &lt;li&gt;&lt;a href=""&gt;Another Page&lt;/a&gt;&lt;/li&gt;
  &lt;/ul&gt;
&lt;/nav&gt;
</code></pre>

{{% feature-panel %}}

### Style

The default `style` abbreviation only creates the `<style>` start and end tag, but usually when I use the `<style>` element I do it because I quickly want to test or debug something.

Let’s add some default rules to the `<style>` tag:

<pre><code class="language-markup">"style": "style>{\\* { box-sizing: border-box; \\}}+{\n${1:*}:focus \\{${2: outline: 2px solid red; }\\} }+{\n${0}}"
</code></pre>

#### Breakdown

Some characters (e.g. `$`, `*`, `{` or `}`) have to be escaped using  `\\`.

<pre><code class="language-markup">style>{\\* { box-sizing: border-box; \\}}
</code></pre>

`\n` creates a linebreak and `${1:*}` places the first tab stop at the selector `*`.

<pre><code class="language-markup">{\n${1:*}:focus \\{${2: outline: 2px solid red; }\\}}
</code></pre>

- **Before**: `<style><style>`
- **After**:  

<pre><code class="language-css">&lt;style&gt;
  &#42; { box-sizing: border-box; }  
  &#42;:focus { outline: 2px solid red; }
&lt;/style&gt;
</code></pre>

Alright, enough warming-up. Let’s create complex snippets. At first, I wanted to create a single snippet for my boilerplate, but I created three abbreviations that serve different needs.

<ol>
  <li><a href="#boilerplate-small">Small</a></li>
  <li><a href="#boilerplate-medium">Medium</a></li>
  <li><a href="#full-boilerplate">Full</a></li>
</ol>

{{% ad-panel-leaderboard %}}

### Boilerplate Small

This is a boilerplate for quick demos, it creates the following:

- Basic site structure,
-  `viewport` meta tag,
- Page title,
-  `<style>` element,
- A `<h1>`.

<div class="break-out">

 <pre><code class="language-markup">{
  "!": "{&lt;!DOCTYPE html&gt;}+html[lang=${1}${lang}]>(head&gt;meta:utf+meta:vp+{}+title{${2:New document}}+{}+style)+body>(h1&gt;{${3: New Document}})+{${0}}"
}
</code></pre>
</div>

#### Breakdown

A string with the doctype:

<pre><code class="language-markup">{&lt;!DOCTYPE html&gt;}
</code></pre>

The `<html>` element with a `lang` attribute. The value of the `lang` attribute is a variable you can change in the VS code settings (Code&nbsp;&rarr; Preferences&nbsp;&rarr; Settings).

<pre><code class="language-markup">html[lang=${1}${lang}]
</code></pre>

You can change the default natural language of the page by searching for “emmet variables” in VS Code settings and changing the `lang` variable. You can add your custom variables here, too.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6a4c4769-8d37-42c2-81f1-846e150e420f/3-custom-emmet-snippets-vscode.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6a4c4769-8d37-42c2-81f1-846e150e420f/3-custom-emmet-snippets-vscode.png" width="800" height="" sizes="100vw" caption="" alt="There are 2 default variables in VS Code, lang is set to en and charset to UTF-8." >}}

The `<head>` includes the `charset` meta tag, `viewport` meta tag, `<title>`, and `<style>` tag. `{}` creates a new line.

<pre><code class="language-markup">(head&gt;meta:utf+meta:vp+{}+title{${2:New document}}+{}+style)
</code></pre>

Let’s have a first quick look at what this gives us.

<pre><code class="language-html">&lt;!DOCTYPE html&gt;
&lt;html lang="en"&gt;
&lt;head&gt;
  &lt;meta http-equiv="Content-Type" content="text/html;charset=UTF-8"&gt;
  &lt;meta name="viewport" content="width=device-width, initial-scale=1.0"&gt;
  
  &lt;title&gt;New document&lt;/title&gt;
&lt;/head&gt;
&lt;/html&gt;
</code></pre>

Looks okay, but the `meta:utf` abbreviation creates the old way in HTML to define the `charset` and `meta:vp` creates two tab stops I don’t need because I never use a different setting for the `viewport`.

Let’s overwrite these snippets before we move on.

<pre><code class="language-css">{
  "meta:vp": "meta[name=viewport content='width=device-width, initial-scale=1']",
  "meta:utf": "meta[charset=${charset}]"
}
</code></pre>

Last but not least, the `<body>` element, an `<h1>` with default text, followed by the final tab stop.

<pre><code class="language-css">body>(h1>{${3: New Document}})+{${0}}
</code></pre>

The final boilerplate:

<pre><code class="language-html">&lt;!DOCTYPE html&gt;
&lt;html lang="en"&gt;
&lt;head&gt;
  &lt;meta charset="UTF-8"&gt;
  &lt;meta name="viewport" content="width=device-width, initial-scale=1"&gt;
  
  &lt;title&gt;New document&lt;/title&gt;
  
  &lt;style&gt;
    * { box-sizing: border-box; }
    
    *:focus { outline: 2px solid red; } 
    
    
  &lt;/style&gt;
&lt;/head&gt;
&lt;body&gt;
  &lt;h1&gt; New Document&lt;/h1&gt;
  
&lt;/body&gt;
&lt;/html&gt;
</code></pre>

For me, that’s the perfect minimal debugging setup.

### Boilerplate Medium

While I use the first boilerplate only for quick demos, the second boilerplate can be used for complex pages. The snippet creates the following:

- Basic site structure,
-  `viewport` meta tag,
- Page title,
-  `.no-js`/`.js` classes,
- External screen and print stylesheets,
- `description` and `theme-color` meta tag,
- Page structure.

<div class="break-out">

 <pre><code class="language-html">{
  "!!": "{&lt;!DOCTYPE html&gt;}+html[lang=${1}${lang}].no-js&gt;{&lt;!-- TODO: Check lang attribute --&gt; }+(head&gt;meta:utf+meta:vp+{}+title{${1:🛑 Change me}}+{}+(script[type=\"module\"]&gt;{document.documentElement.classList.replace('no-js', 'js');})+{}+link:css+link:print+{}+meta[name=\"description\"][content=\"${2:🛑 Change me (up to ~155 characters)}\"]+{&lt;!-- TODO: Change page description --&gt; }+meta[name=\"theme-color\"][content=\"${2:#FF00FF}\"])+body&gt;page"
}
</code></pre>
</div>

Yeaaah, I know, that looks like gibberish. Let’s dissect it.

#### Breakdown

The `doctype` and the root element are like in the first example, but with an additional `no-js` class and a comment that reminds me to change the `lang` attribute, if necessary.

<pre><code class="language-html">{&lt;!DOCTYPE html&gt;}+html[lang=${1}${lang}].no-js>{<!-- TODO: Check lang attribute --> }
</code></pre>

The [TODO Highlight](https://marketplace.visualstudio.com/items?itemName=wayou.vscode-todo-highlight) extension makes the comment really pop.

{{< rimg href="https://marketplace.visualstudio.com/items?itemName=wayou.vscode-todo-highlight" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/15080c47-7445-4120-adaf-6c261f3f1182/4-custom-emmet-snippets-vscode.png" width="800" height="" sizes="100vw" caption="" alt="The extension highlights certain keywords like TODO visually." >}}

The `<head>` includes the `charset` meta tag, `viewport` meta tag, `<title>`. `{}` creates a new line.

<pre><code class="language-javascript">(head>meta:utf+meta:vp+{}+title{${1:🛑 Change me}}+{}
</code></pre>

A script with a line of JavaScript. I’m [cutting the mustard](https://fettblog.eu/cutting-the-mustard-2018/) at the JS module support. If a browser supports JavaScript modules, it means that it’s a browser that supports modern JavaScript (e.g. modules, ES 6 syntax, fetch, and so on). I ship most JS only to these browsers, and I use the `js` class in CSS, if the styling of a component is different, when JavaScript is active.

<div class="break-out">

 <pre><code class="language-javascript">(script[type=\"module\"]>{document.documentElement.classList.replace('no-js', 'js');})+{}
</code></pre>
</div>

Two `<link>` elements; the first links to the main stylesheet and the second to a print stylesheet.

<pre><code class="language-html">link:css+link:print+{}
</code></pre>

The page description:

<pre><code class="language-html">meta[name=\"description\"\][content=\"${2:🛑 Change me (up to ~155 characters)}\"]+{<!-- TODO: Change page description --> }
</code></pre>

The `theme-color` meta tag:

<pre><code class="language-html">meta[name=\"theme-color\"\][content=\"${2:#FF00FF}\"])
</code></pre>

The body element and the basic page structure:

<pre><code class="language-html">body>page
</code></pre>

The final boilerplate looks like this:

<div class="break-out">

 <pre><code class="language-html">&lt;!DOCTYPE html&gt;
&lt;html lang="en" class="no-js"&gt;
&lt;!-- TODO: Check lang attribute --&gt; 
&lt;head&gt;
  &lt;meta charset="UTF-8"&gt;
  &lt;meta name="viewport" content="width=device-width, initial-scale=1.0"&gt;
  
  &lt;title&gt;🛑 Change me&lt;/title&gt;
  
  &lt;script type="module"&gt;
    document.documentElement.classList.replace('no-js', 'js');
  &lt;/script&gt;
  
  &lt;link rel="stylesheet" href="style.css"&gt;
  &lt;link rel="stylesheet" href="print.css" media="print"&gt;
  
  &lt;meta name="description" content="🛑 Change me (up to ~155 characters)"&gt;
  &lt;!-- TODO: Change page description --&gt; 
  &lt;meta name="theme-color" content="#FF00FF"&gt;
&lt;/head&gt;
&lt;body&gt;
  &lt;header&gt;
    &lt;h1&gt;&lt;/h1&gt;
  &lt;/header&gt;
  &lt;main&gt;&lt;/main&gt;
  &lt;footer&gt;&copy;&lt;/footer&gt;
&lt;/body&gt;
&lt;/html&gt;
</code></pre>
</div>

### Full Boilerplate

The full boilerplate is similar to the second boilerplate; the differences are additional `meta` tags and a `script` tag.

The snippet creates the following:

- Basic site structure,
-  `viewport` meta tag,
- Page title,
-  `js`/`no-js` classes,
- External screen and print stylesheets,
- `description` and open graph meta tags,
- `theme-color` meta tag,
- canonical `<link>` tag,
- Favicon tags,
- Page structure,
- <`script>` tag.

<div class="break-out">

 <pre><code class="language-html">{
  "!!!": "{&lt;!DOCTYPE html&gt;}+html[lang=${1}${lang}].no-js&gt;{&lt;!-- TODO: Check lang attribute --&gt; }+(head&gt;meta:utf+meta:vp+{}+title{${1:🛑 Change me}}+{}+(script[type=\"module\"]&gt;{document.documentElement.classList.replace('no-js', 'js');})+{}+link:css+link:print+{}+meta[property=\"og:title\"][content=\"${1:🛑 Change me}\"]+meta[name=\"description\"][content=\"${2:🛑 Change me (up to ~155 characters)}\"]+meta[property=\"og:description\"][content=\"${2:🛑 Change me (up to ~155 characters)}\"]+meta[property=\"og:image\"][content=\"${1:https://}\"]+meta[property=\"og:locale\"][content=\"${1:en_GB}\"]+meta[property=\"og:type\"][content=\"${1:website}\"]+meta[name=\"twitter:card\"][content=\"${1:summary_large_image}\"]+meta[property=\"og:url\"][content=\"${1:https://}\"]+{&lt;!-- TODO: Change social media stuff --&gt; }+{}+link[rel=\"canonical\"][href=\"${1:https://}\"]+{&lt;!-- TODO: Change canonical link --&gt; }+{}+link[rel=\"icon\"][href=\"${1:/favicon.ico}\"]+link[rel=\"icon\"][href=\"${1:/favicon.svg}\"][type=\"image/svg+xml\"]+link[rel=\"apple-touch-icon\"][href=\"${1:/apple-touch-icon.png}\"]+link[rel=\"manifest\"][href=\"${1:/my.webmanifest}\"]+{}+meta[name=\"theme-color\"][content=\"${2:#FF00FF}\"])+body&gt;page+{}+script:src[type=\"module\"]"
}
</code></pre>
</div>

This incredibly long snippet creates this:

<div class="break-out">

 <pre><code class="language-html">&lt;!DOCTYPE html&gt;
&lt;html lang="en" class="no-js"&gt;
&lt;!-- TODO: Check lang attribute --&gt; 
&lt;head&gt;
  &lt;meta charset="UTF-8"&gt;
  &lt;meta name="viewport" content="width=device-width, initial-scale=1.0"&gt;
  
  &lt;title&gt;🛑 Change me&lt;/title&gt;
  
  &lt;script type="module"&gt;
    document.documentElement.classList.replace('no-js', 'js');
  &lt;/script&gt;
  
  &lt;link rel="stylesheet" href="style.css"&gt;
  &lt;link rel="stylesheet" href="print.css" media="print"&gt;
  
  &lt;meta property="og:title" content="🛑 Change me"&gt;
  &lt;meta name="description" content="🛑 Change me (up to ~155 characters)"&gt;
  &lt;meta property="og:description" content="🛑 Change me (up to ~155 characters)"&gt;
  &lt;meta property="og:image" content="https://"&gt;
  &lt;meta property="og:locale" content="en_GB"&gt;
  &lt;meta property="og:type" content="website"&gt;
  &lt;meta name="twitter:card" content="summary_large_image"&gt;
  &lt;meta property="og:url" content="https://"&gt;
  &lt;!-- TODO: Change social media stuff --&gt; 
  
  &lt;link rel="canonical" href="https://"&gt;
  &lt;!-- TODO: Change canonical link --&gt; 
  
  &lt;link rel="icon" href="/favicon.ico"&gt;
  &lt;link rel="icon" href="/favicon.svg" type="image/svg+xml"&gt;
  &lt;link rel="apple-touch-icon" href="/apple-touch-icon.png"&gt;
  &lt;link rel="manifest" href="/my.webmanifest"&gt;
  
  &lt;meta name="theme-color" content="#FF00FF"&gt;
&lt;/head&gt;
&lt;body&gt;
  &lt;header&gt;
    &lt;h1&gt;&lt;/h1&gt;
  &lt;/header&gt;
  &lt;main&gt;&lt;/main&gt;
  &lt;footer&gt;&copy;&lt;/footer&gt;
  
  &lt;script src="" type="module"&gt;&lt;/script&gt;
&lt;/body&gt;
&lt;/html&gt;
</code></pre>
</div>

{{% ad-panel-leaderboard %}}

## Custom CSS Snippets

For the sake of completeness, here are some of the CSS snippets I’m using.

### Debugging

This snippet creates a 5px red outline with a custom offset.

<pre><code class="language-css">"debug": "outline: 5px solid red;\noutline-offset: -5px;"
</code></pre>

### Centering

A snippet that sets `display` to flex, and centers its child items.

<pre><code class="language-css">"center": "display: flex;\njustify-content: center;\nalign-items: center;"
</code></pre>

### Sticky

Sets the `position` property to `sticky`, with two tab stops at the `top` and `left` property.

<pre><code class="language-css">"sticky": "position: sticky;\ntop: ${1:0};\nleft: ${2:0};"
</code></pre>

{{< vimeo id="568320124" caption="A demonstration of all 3 CSS snippets applied to a <code>div</code> element." breakout="true" >}}

## User Snippets

At the beginning of this article, I mentioned that VS Code also provides custom snippets. The difference to Emmet snippets is that you can’t use abbreviations, but you can also define tab stops and make use of internal variables.

How to get the best out of user snippets could be a topic for another article, but here’s an example of a custom CSS snippet I’ve defined:

<div class="break-out">

 <pre><code class="language-css">"Visually hidden": {
"prefix": "vh",
"body": [
  ".u-vh {",
  "  position: absolute;\n  white-space: nowrap;\n  width: 1px;\n  height: 1px;\n  overflow: hidden;\n  border: 0;\n  padding: 0;\n  clip: rect(0 0 0 0);\n  clip-path: inset(50%);\n  margin: -1px;",
  "}"
],
"description": "A utility class for screen reader accessible hiding."
}
</code></pre>
</div>

This snippet doesn’t just create CSS rules, but a whole declaration block when we type `vh` and press <kbd>Enter</kbd> or <kbd>Tab</kbd>.

<pre><code class="language-css">.u-vh {
  position: absolute;
  white-space: nowrap;
  width: 1px;
  height: 1px;
  overflow: hidden;
  border: 0;
  padding: 0;
  clip: rect(0 0 0 0);
  clip-path: inset(50%);
  margin: -1px;
}
</code></pre>

## Final Words

It takes some time to create these snippets, but it’s worth the effort because you can customize Emmet to your personal preferences, automate repetitive tasks and save time in the long run. 

I’d love to see which snippets you use, so please share them with us in the comments. If you want to use my settings, you can find my [final snippets.json](https://gist.github.com/matuzo/188a81a567dc4780690c699c822ec387) on GitHub. 

### Resources

- Default [CSS Emmet snippets](https://github.com/emmetio/snippets/blob/master/css.json)
- Default [HTML Emmet snippets](https://github.com/emmetio/snippets/blob/master/html.json)
- Emmet [cheat sheet](https://docs.emmet.io/cheat-sheet/)
- [Emmet in VS Code docs](https://code.visualstudio.com/docs/editor/emmet)

{{< signature "vf, il" >}}
