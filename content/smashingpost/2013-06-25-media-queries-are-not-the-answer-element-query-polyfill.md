---
title: 'Media Queries Are Not The Answer: Element Query Polyfill'
slug: media-queries-are-not-the-answer-element-query-polyfill
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d045208c-0c47-4932-8ef9-2457381b155d/various-mobile-devices-illu.jpg
date: 2013-06-25T07:24:57.000Z
author: tyson-matanich
description: >-
  Responsive Web design has transformed how websites are designed and built. It
  has inspired us to think beyond device classifications and to use media
  queries to adapt a layout to the browser’s viewport size. This, however,
  deviates from the hierarchical structure of CSS and characterizes elements
  relative to the viewport, instead of to their container.
categories:
  - Coding
  - CSS
  - Responsive Design
---
Responsive Web design has transformed how websites are designed and built. It has inspired us to think beyond device classifications and to use media queries to adapt a layout to the browser’s viewport size. This, however, deviates from the hierarchical structure of CSS and characterizes elements relative to the viewport, instead of to their container.

Extensive use of media queries might be the answer for today, but it is <strong>not a viable long-term solution</strong>. Media queries do not allow for reusable modules that adapt based on their containers’ size.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Picturefill 2.0: Responsive Images And The Perfect Polyfill](https://www.smashingmagazine.com/2014/05/picturefill-2-0-responsive-images-and-the-perfect-polyfill/)
*   [How I Ended Up With Element Queries](https://www.smashingmagazine.com/2016/07/how-i-ended-up-with-element-queries-and-how-you-can-use-them-today/)
*   [<span class="headline">The Flexbox Reading List: Techniques And Tools</span>](https://www.smashingmagazine.com/2016/02/the-flexbox-reading-list/)

## What Is Responsive Web Design?

Responsive Web design is not limited to a set of technologies; rather, it is a different approach to designing and building websites. I, like many, took <a href="https://alistapart.com/article/responsive-web-design">Ethan’s words</a> about responsive Web design too literally and overlooked the essence of what was being said:
<blockquote>"Fluid grids, flexible images, and media queries are the three technical ingredients for responsive web design, but it also requires a different way of thinking."</blockquote>

{{% feature-panel %}}

We have accomplished great things while embracing the stated “technical ingredients” for responsive Web design, but we have much room for growth when it comes to a “different way of thinking.” Thinking differently should affect not only how we design and build our websites, but also how we design and build the tools and technologies that our websites are founded on.</p>

## Modular Design

When I learned about how media queries could be used in responsive Web design, I was excited by the possibilities. However, it was not long before I learned of the limitations. Media queries are great for adapting layouts to various screen sizes, but terrible for creating <a href="https://daverupert.com/2013/04/responsive-deliverables/">modular designs</a>. Modular CSS is already hard enough, and media queries provide very little to no help. <strong>Truly modular layouts need to respond to the sizes of containers</strong>, not just to the viewport’s size. Media queries, however, are based on the viewport, rather than an element’s container. There is some hope for standard CSS on the horizon, in the form of a <a href="https://www.w3.org/TR/css3-cascade/#all">W3C working draft</a>, by allowing the cascade inheritance to be broken and resetting an element to its defaults. But what about media queries?

## The @media Hack

Web developers are masters at taking something created for one purpose and using it to accomplish other things. The Web’s history is littered with examples of this, and media queries are no exception. Kudos to Ian Storm Taylor for writing down his thoughts in the article “<a href="https://ianstormtaylor.com/media-queries-are-a-hack/">Media Queries Are a Hack</a>.” Hacks are necessary on the Web to provide desired functionality until proper support is achieved, as well as to provide support to older browsers. The <a href="https://www.w3.org/TR/css3-mediaqueries/">W3C states</a>, “By using media queries, presentations can be tailored to a specific range of output devices <strong>without changing the content itself</strong>.” The key word here is “can,” but just because you <em>can</em> do something, doesn’t mean you <em>should</em>… But do we have any other choice?

## The Element Query

Introducing the element query. An element query is similar to a media query in that, if a condition is met, some CSS will be applied. Element query conditions (such as <code>min-width</code>, <code>max-width</code>, <code>min-height</code> and <code>max-height</code>) are based on elements, instead of the browser. Unfortunately, CSS doesn’t yet support element queries, but that shouldn’t stop us from dreaming, hacking and pushing for new standards.</p>

### Conceptual Example

Consider the following example, in which the navigation menu should become visible when it reaches a minimum width of 500 pixels (representing one of many potential syntaxes):

<pre><code class="language-css">nav (min-width: 500px) {
    display: block;
}
</code></pre>

Compare this to a media query in which the navigation menu’s visibility depends on the viewport’s width and needs to account for the padding and other declarations of parent elements:

<pre><code class="language-css">@media all and (min-width: 520px) {
    nav {
        display: block;
    }
}
</code></pre>

Now imagine having to build a modular component that needs to be placed in containers of various sizes on a single page. One current approach is to provide different theme classes (like <code>.module--large</code>) to trigger CSS in media queries. This, however, adds a lot of complications and requires a module to know how its parent will react to various viewport widths.</p>

### Issues: Invalid and Looping Conditions

There are several cases in which the CSS of an element query would invalidate the element query itself or create recursion. Hopefully, the browser would be able to detect these conditions and respond appropriately.

Consider the following examples.

Once an element reaches 500 pixels wide, it’s resized to 200 pixels, at which point the rule would no longer apply:

<pre><code class="language-css">.element (min-width: 500px) {
    width: 200px;
}
</code></pre>

Once an element’s width reaches 31.250 ems, its font size would be decreased, which changes the definition of the em unit:

<pre><code class="language-css">.element (min-width: 31.250em) {
    font-size: 0.75em;
}
</code></pre>

Once a container’s width reaches 450 pixels, the size of its child changes to 400 pixels, which would shrink the size of the container:

<pre><code class="language-css">.container { float: left; }
.child { width: 500px; }
.container (min-width: 450px) &gt; .child {
    width: 400px;
}
</code></pre>

There are many other such examples, but you get the point: Element queries are not as simple as we had hoped.</p>

## Element Query Polyfill

Element queries seem pretty awesome, but they also have some real issues. To help sort these out, I’ve written a proof-of-concept polyfill. The polyfill has enabled me to understand how a browser might react to various conditions. As I got further along, I realized that the polyfill could hold real value in the Web community’s debate on element queries, and that some developers could even start using element queries today.

The elementQuery polyfill script is available <a href="https://github.com/tysonmatanich">on GitHub</a> for you to use, fork and contribute to.</p>

### Selector Syntax

The syntax used in the previous examples caused limitations, so I updated the polyfill to support an attribute selector syntax. The <a href="https://css-tricks.com/attribute-selectors/#rel-space"><code>~=</code> attribute selector</a> checks whether the value is contained in a space-delimited list (supported in modern browsers above Internet Explorer 6).

The following examples show CSS rules using the syntax required for the elementQuery polyfill.

This rule queries itself for a single condition:

<pre><code class="language-css">header[min-width~="500px"] {
    background-color: #eee;
}
</code></pre>

This rule queries itself for multiple conditions:

<pre><code class="language-css">header[min-width~="500px"][max-width~="800px"] {
    background-color: #eee;
}
</code></pre>

This rule queries a parent for a condition:

<pre><code class="language-css">header[min-width~="31.250em"] nav {
    clear: both;
}
</code></pre>

### How It Works

Unfortunately, the elementQuery polyfill requires JavaScript and the <a href="https://sizzlejs.com/">Sizzle</a> selector engine (which is embedded in jQuery). When the document object model (DOM) is ready, elementQuery scans the <code>document.styleSheets</code> collection for any CSS rules that use elementQuery. When it finds a match, it extracts the following information:

*   **Selector**.  Such as `header`, `ul > li.class`
*   **Query type** `min-width`, `max-width`, `min-height`, `max-height`
*   **Query value**.  Such as `500px`, `31.250em`

elementQuery then uses this information to add or remove attributes from elements that match the given selector and query condition.</p>

### Expanded Support

Most browsers, but not Internet Explorer, don’t provide access to the contents of cross-domain style sheets, which causes issues when CSS files are served from a content delivery network. Additionally, parsing style sheets takes time (not much, though). So, I created two branches for elementQuery: <a href="https://github.com/tysonmatanich/elementQuery">master</a> and <a href="https://github.com/tysonmatanich/elementQuery/tree/prod">prod</a>. The master branch includes the code for extracting the necessary elementQuery information (selector, query type, query value), and it also provides a <code>selectors()</code> function to export the information. The prod branch requires the information to be declared in JavaScript, which avoids the cross-domain file issue and the time required to parse the style sheets.

Here is an example of how to export elementQuery information using the master branch:

<pre><code class="language-javascript">console.log(JSON.stringify(elementQuery.selectors()));
</code></pre>

And here is an example of how to import elementQuery information using the prod branch:

<pre><code class="language-javascript">elementQuery({"header":{"min-width":["500px","31.250em"],"max-width":["800px"]}});
</code></pre>

### Working Examples

I’ve put together a few working examples on CodePen (using the master branch) that you can experiment with or fork. I would love to see what other examples people create (which will probably be much cooler than mine). Just be sure to tag them with <a href="https://codepen.io/tag/elementquery">#elementquery</a> so that others can benefit.

*   [Grid](https://codepen.io/tysonmatanich/pen/johpn): nested elements
*   [Menu](https://codepen.io/tysonmatanich/pen/wramd): width-based elementQuery
*   [Blockquote](https://codepen.io/tysonmatanich/pen/jIBpJ): height-based elementQuery

## Be Creative

I didn’t write this just to get you to jump on the element query bandwagon, but rather to encourage people to think about how we can solve the problems that are limiting our medium. Let’s keep the discussion going and make the Web a better place. So, go wild and make cool stuff!

*   View [elementQuery](https://github.com/tysonmatanich/elementQuery) on GitHub.</p>

### Further Reading

*   “[Em values in JavaScript](https://www.matanich.com/2013/06/24/em-values-javascript/),” Tyson Matanich
*   “[Working Around a Lack of Element Queries](https://filamentgroup.com/lab/element_query_workarounds/),” Filament Group
*   “[Element Queries](https://www.xanthir.com/b4PR0),” Tab Atkins Jr.

<em>(Source of image on front page: <a href="https://www.smashingmagazine.com/2012/10/24/beyond-common-media-query-breakpoints/">Looking Beyond Common Media Query Breakpoints</a>)</em>

{{< signature "al" >}}

