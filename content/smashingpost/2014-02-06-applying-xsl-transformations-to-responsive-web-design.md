---
title: How To Apply Transformations To Responsive Web Design
slug: applying-xsl-transformations-to-responsive-web-design
image: null
date: 2014-02-06T10:06:28.000Z
author: ishan-anand
description: >-
  To most Web developers, it sounds controversial until you hear the punchline:
  Last summer, the developers in charge of Google’s Chrome browser floated a
  [proposal](https://groups.google.com/a/chromium.org/forum/#!topic/blink-dev/zIg2KC7PyH0)
  that went virtually unnoticed by the technology press, which was to remove
  support for an established W3C standard that every other browser vendor still
  supports.
categories:
  - Mobile
  - Opinion Column
  - Apps
  - Content
  - Responsive Design
  - CSS3
---
To most Web developers, it sounds controversial until you hear the punchline: Last summer, the developers in charge of Google’s Chrome browser floated a <a href="https://groups.google.com/a/chromium.org/forum/#!topic/blink-dev/zIg2KC7PyH0">proposal</a> that went virtually unnoticed by the technology press, which was to remove support for an established W3C standard that every other browser vendor still supports. The standard in question? Extensible Stylesheet Language Transformations, otherwise known as XSLT.

In reaction to this news, most Web developers would likely shrug and say “So what?” That’s unfortunate.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Responsive Web Design: What It Is And How To Use It](https://www.smashingmagazine.com/2011/01/guidelines-for-responsive-web-design/)
*   [Responsible Considerations For Responsive Web Design](https://www.smashingmagazine.com/2013/03/responsible-web-design/)
*   [Design Process In The Responsive Age](https://www.smashingmagazine.com/2012/05/design-process-responsive-age/)

Transformations are a simple yet <strong>powerful technique for separating content and presentation</strong> in Web applications. Yet, outside of enterprise and data-processing circles, transformations have failed to gain popularity through XSLT. As a result, Web developers are liable to think that transformations “don’t apply to me,” even though they work with HTML, a structured format ripe for transformation. Thankfully, new transformation frameworks are on the horizon, including work by the inventor of Sass, that hold the promise of a revival.

{{% feature-panel %}}

In this article, we will reintroduce transformations and explore their applications to mobile and responsive design. We will not only teach the old dog new tricks, but show that transformations are relevant to everyone who deals with HTML.</p>

## Separating Content And Presentation

A transformation is simply a system that transforms its input into an output according to a set of predefined rules.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0fa2eaeb-d57f-4f80-94dc-5c36bb791280/transforms-1-transform-large-opt.jpg"><img title="The data flow of a transform" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d0192709-304d-4838-8eb4-483bb41acf40/transforms-1-transform-opt.jpg" alt="The data flow of a transform" width="500" height="130" /></a><br>
<em>The data flow of a transformation. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0fa2eaeb-d57f-4f80-94dc-5c36bb791280/transforms-1-transform-large-opt.jpg">Large view</a>)</em>

The key thing about transformations isn’t the action they perform but the capability they enable. Transformations create an <strong>abstraction that decouples content and functionality from presentation.</strong> This separation is a design goal of many frameworks, but transformations facilitate it in powerful and unique ways.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f8c781f1-abe9-403d-8dc8-f43da2a9bd2a/transforms-2-separation-of-concerns-large-opt.jpg"><img title="The transformation data flow recast as a separation of concerns" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6f845f28-8e8e-4e9c-86a2-e256d3f18322/transforms-2-separation-of-concerns-opt.jpg" alt="The transformation data flow recast as a separation of concerns" width="500" height="150" /></a><br>
<em>The transformation data flow recast as a separation of concerns. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f8c781f1-abe9-403d-8dc8-f43da2a9bd2a/transforms-2-separation-of-concerns-large-opt.jpg">Large view</a>)</em>

A powerful example of this decoupling occurs in <a href="https://github.com/cgrand/enlive">Enlive</a>, a transformation and templating system written in Clojure. Most templating engines use a customized markup language to mix HTML with programming constructs such as loops and variables. Take PHP, for example:

<pre><code class="language-php">&lt;ul&gt;
  &lt;?php foreach ($task_list as $task) { ?&gt; 
    &lt;li&gt; &lt;?php echo $task ?&gt; &lt;/li&gt;
  &lt;?php } ?&gt; 
&lt;/ul&gt;
</code></pre>

By contrast, Enlive templates use the same plain old HTML that you would get from your designer or PSD slicer. For example, a simple <code>hello-world.html</code> Enlive template might look like this:

<pre><code class="language-markup">
&lt;html&gt;
	&lt;body&gt;
		&lt;h1 id="output"&gt;Lorem Ipsum&lt;/h1&gt;
	&lt;/body&gt;
&lt;/html&gt; 
</code></pre>

Instead of embedding logic in the markup, Clojure code that is associated with the HTML transforms it into output:

<pre><code class="language-clojure">
  (deftemplate helloworld 
    "hello-world.html" 
    [] 
    [:h1#output] 
    (content "Hello World!"))
</code></pre>

Completely understanding the code above is not important, but you’ll probably recognize the <code>h1#output</code> argument as a CSS selector. In this example, a template named <code>helloworld</code> is being defined, in which the <code>h1#output</code> element’s content is replaced by “Hello World!” When executed, this template would output the following:

<pre><code class="language-markup">
&lt;html&gt;
	&lt;body&gt;
		&lt;h1 id="output"&gt;Hello World&lt;/h1&gt;
	&lt;/body&gt;
&lt;/html&gt;
</code></pre>

For more on Enlive, I recommend David Nolen’s <a href="https://github.com/swannodette/enlive-tutorial">excellent tutorial</a>. But the key point is that content and presentation have been decoupled. Website changes, A/B tests and even a redesign could be as easy as getting new HTML from your designer and dropping it in. In addition, the designer doesn’t need to know anything about the templating language and may use HTML classes and IDs, concepts that they already know.

While you don’t need to build a website in this way, the situation is analogous to building a Web page without a style sheet. True, you could design a page purely with inline styles (that is, using only the <code>style</code> attribute), and novice developers often code this way out of expediency. But experienced developers know that <strong>a style sheet improves workflow and productivity at scale</strong>.

Similarly, by separating content and presentation, you will unlock more productivity and agility for your team. In effect, transformations truly separate the front end from the back end and create a new workspace for the visual design team to operate independently of the rest of the system. In an industry where even simple things like the <a href="https://blog.hubspot.com/blog/tabid/6307/bid/20566/The-Button-Color-A-B-Test-Red-Beats-Green.aspx">color of a button can affect conversion rates</a>, enabling your visual design team to iterate more quickly and continually could deliver tremendous value to the bottom line.</p>

## Responsive Retrofitting

Transformations are not just useful in a templating system. This decoupling of content and presentation can also be applied to an existing website, enabling developers to apply a new presentation regardless of how the original website was built. This combination of <strong>separating content and presentation and its applicability to existing websites</strong> is what makes transformations so powerful and useful to a broader audience than currently use them. I’ll illustrate this by responsively retrofitting an existing website using a transformation technology that’s in every browser today (at least for now), XSLT.

<a href="https://en.wikipedia.org/wiki/XSLT">XSLT</a> was introduced in the late 1990s as a language for transforming XML and XHTML documents. During the ascendency of XML, XSLT was seen as a solution for separating content and presentation in Web applications built on XML data formats. The W3C recommended XSLT as a standard, and almost every major browser incorporated support for some form of the language.

Now that Google’s Chrome and Blink team has <a href="https://groups.google.com/a/chromium.org/forum/#!topic/blink-dev/zIg2KC7PyH0%5B51-75-false%5D">proposed</a> dropping support for XSLT, some might be concerned about using it long term. However, at the time of writing, XSLT is supported in all major browsers, including Chrome and the latest versions of the iPhone and Android browsers. In addition, XSLT may be used both server- and client-side. Server-side implementation works regardless of browser support, and open-source and commercial XSLT engines are available. Finally, JavaScript implementations of XSLT, such as <a href="https://www.saxonica.com/ce/index.xml">Saxon-CE</a>, could also fill the gap client-side if Google does indeed decide to drop support for XSLT.

Responsive retrofitting is the process of grafting responsive Web design techniques onto an existing website that was not built to be responsive. Although a lot of resources and tutorials on building a responsive website from scratch are out there, retrofitting has curiously received far less attention, despite its enormous value. A lot more old websites exist than new ones, and significant capital and effort have been invested in them.

A long responsive rebuild might not meet the budget or time-to-market requirements for many of these websites. Transformations provide <strong>an effective way to make a website responsive without the expense of rebuilding it</strong>.

The natural first step would be to retrofit the website purely in CSS. <a href="https://github.com/sparkbox/Responsive-Retrofitting">Ben Callahan’s bookmarklet</a> for example, inserts a custom CSS file to make a given website more responsive. However, adding CSS gets you only so far. Eventually, the layout, nesting and order of elements in the original HTML will restrict your design options. <a href="https://www.xmlbook.info/9-XSL-XSLT.phtml">John Shirrel describes this</a> as an inherent flaw of CSS:
<blockquote>"You have discovered the weakness of using CSS… CSS does not allow you to transform your document. Elements must remain in the order they appear… There is no real decision-making power in CSS."</blockquote>

Fundamentally, this process breaks down because CSS and HTML do not purely separate presentation and content. Whenever you’ve found yourself needing to wrap an element in an extra <code>div</code> or <code>span</code> to make the design work, you’ve encountered that breakdown. This is where transformations come in, restoring the abstraction (surprisingly) by enabling us to manipulate the document.

To demonstrate the technique, I’ve created an <a href="https://s3-us-west-1.amazonaws.com/smashing/hacker-news-xhtml-xslt-stylesheet.xml">sample retrofit</a> of Hacker News’ home page, by making the top navigation responsive, using ZURB’s <a href="https://foundation.zurb.com/">Foundation</a> framework. Naturally, additional design changes beyond these would be required, but it should serve to illustrate the process. Why Hacker News? First, using code from a real website helps to demonstrate the power of the technique. Secondly, the HTML on this website is Goldilocks-sized: not so small that it’s a toy, but not so big as to make our example complicated.

<img title="Hacker News' HTML, with Foundation's responsive top bar added by transformations" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d0f8ef2a-4c5a-4f82-8315-72f098a8492a/transforms-3-hackernews-500-opt.png" alt="Hacker News' HTML, with Foundation's responsive top bar added by transformations" width="270" height="480" /><br>
<em>Hacker News’ HTML, with Foundation’s responsive top bar added by transformations.</em>

The most relevant file in this retrofit is the XSL style sheet <code>transformer.xsl</code>, which you can <a href="https://s3-us-west-1.amazonaws.com/smashing/transformer.xsl">download directly</a>. In the paragraphs below, we’ll highlight some key points about the code in <code>transformer.xsl</code>. While a full explanation of XSLT is beyond the scope of this article, a quick crash course should make these explanations more understandable:

*   **Syntax**.  The XSLT programming language is written in a form of XML. For example, an `if` statement in XSLT would be `<xsl:if></xsl:if>` element.
*   **Parameters**.  Parameters to statements like `<xsl:if>` are specified in the attributes and child nodes of the element.
*   **Matching elements**.  A common parameter is the `match` attribute, which selects a collection of nodes. For example, the template specified by the `<xsl:template match="body/center">` rule would be applied when the XSLT engine encounters the `<center>` element that is the child of the `<body>`.
*   **Embedding HTML**.  Finally, you can embed bare HTML in a style sheet.

The first thing we need to do is tell the browser to use the rules in <code>transformer.xsl</code>. To do this, we change the document’s <code>Content-Type</code> to <code>text/xml</code> (alternatively, in some browsers, you can simply change the file’s extension from <code>.html</code> to <code>.xml</code>) and add an <code>&lt;?xml-stylesheet&gt;</code> tag like the following to the top of the document:

<pre><code class="language-markup">
&lt;?xml-stylesheet type="text/xsl" href="transformer.xsl"?&gt;
</code></pre>

When the browser encounters this tag, it will transform the document according the XSLT rules specified in the style sheet before rendering it. This will execute the transformation in the browser (i.e. client-side). But <strong>transformations can also be performed server-side</strong>. Doing transformations server-side could result in better performance, but we’re doing transformations client-side to make our example accessible to anyone with a browser. For those interested in using this technique client-side, <a href="https://stackoverflow.com/questions/434976/how-do-i-profile-and-optimize-an-xslt">optimization techniques and tools</a> are available for writing performant XSLT.

Another issue is how XSLT handles unspecified elements. By default, XSLT strips out any elements not specified in the transformation rules. This is a design decision that makes sense for XML documents, which typically represent data. However, when transforming a fully formed Web page, you will usually want to change only a relatively small part of the document, and specifying every single element we need to be preserved would be laborious. Thankfully, we can add a construct called the <a href="https://en.wikipedia.org/wiki/Identity_transform">identity transform</a> to the <code>transformer.xsl</code> style sheet:

<pre><code class="language-markup">
&lt;!-- XSLT identity transform allows most of the input to pass through to the output. --&gt;
&lt;xsl:template match="@* | node()"&gt;
  &lt;xsl:copy&gt;
    &lt;xsl:apply-templates select="@* | node()"/&gt;
  &lt;/xsl:copy&gt;
&lt;/xsl:template&gt;
</code></pre>

The code above might appear cryptic, but in essence it tells the XSLT engine to copy (i.e. <code>&lt;xsl:copy&gt;</code>) every element node and attribute in the input to the output. Adding this to our style sheet will effectively change the default behavior from stripping out elements to passing them through.

The next step is to add Foundation to the document. For example, the following code would add Foundation’s CSS (<code>foundation.css</code>) and its dependencies (<code>normalize.css</code> and Modernizr) to the top of the <code>&lt;head&gt;</code>:

<pre><code class="language-markup">
&lt;!-- Install and initialize Foundation --&gt;
&lt;!-- Note the match attribute targeting the document's head element --&gt;
&lt;xsl:template match="head"&gt;
  &lt;link rel="stylesheet" href="normalize.css" /&gt;
  &lt;link rel="stylesheet" href="foundation.css" /&gt;    
  &lt;script src="custom.modernizr.js"&gt;&lt;/script&gt;
  &lt;xsl:apply-templates select="@* | *"/&gt;
&lt;/xsl:template&gt;
</code></pre>

Likewise, to add Foundation to the bottom of the <code>&lt;body&gt;</code> element, you would write this:

<pre><code class="language-markup">
&lt;xsl:template match="body"&gt;
  &lt;xsl:apply-templates select="@* | *"/&gt;
  &lt;script src="zepto.js"&gt;&lt;/script&gt;
  &lt;script src="foundation.min.js"&gt;&lt;/script&gt;
  &lt;script&gt;$(document).foundation();&lt;/script&gt;
&lt;/xsl:template&gt;
</code></pre>

The chief difference between the two code samples above are the <code>match</code> attribute values (<code>head</code> versus <code>body</code>, indicating the element being targeted) and the placement of the <code>&lt;xsl:apply-templates&gt;</code> tag (which controls whether our new content will appear before or after the existing content).

Finally, to add the responsive header, we inline new HTML that matches the structure of Foundation’s top bar, and we use the <code>for-each</code> and <code>copy-of</code> commands to populate it with the relevant links from the existing header.

<pre><code class="language-markup">
&lt;!-- Add our Foundation top bar --&gt;
   &lt;xsl:template match="body/center"&gt;
     &lt;nav class="top-bar"&gt;

	&lt;!-- Boilerplate removed for clarity --&gt;

        &lt;section class="top-bar-section"&gt;
          &lt;ul class="right"&gt;

            &lt;!-- Pull the menu links from the old header into our new Foundation header --&gt;
            &lt;xsl:for-each select="//span[@class='pagetop']/a"&gt;
              &lt;li&gt;&lt;xsl:copy-of select="." /&gt;&lt;/li&gt;
            &lt;/xsl:for-each&gt;

          &lt;/ul&gt;
        &lt;/section&gt;
     &lt;/nav&gt;
     &lt;xsl:apply-templates select="@* | *"/&gt;
   &lt;/xsl:template&gt;
</code></pre>

There are <strong>some caveats to this approach the reader should be aware of</strong>. First, in this retrofitting example the transformations were performed by the browser but executing the transformations server-side has a couple of advantages. Server-side transformation reduces the burden on mobile devices, which have less processing, power, and memory capabilities than the server.

The server is also the appropriate place to segment your content to avoid sending unnecessary data over the network and to improve performance. Lastly, you can update the server transformation engine and keep it consistent, instead of dealing with potentially different quirks and levels of XSLT support among browsers. (For example, while XSLT 1.0 is supported in most browsers, XSLT 2.0 is not supported in any, although Saxon-CE is one attempt to add it via JavaScript.)

Second, XSLT’s roots in functional programming make it inaccessible to the average Web developer. It isn’t simply a matter of learning a new syntax. <strong>The recursive processing model of XSLT requires a new way of thinking</strong> that is unfamiliar to developers of imperative languages, especially developers from a design background who do not have formal training in computer science.

Finally, a larger challenge is that this technique works only for Web pages that are in XHTML (a flavor of HTML that is XML-compliant), because XSLT can transform only XML, not HTML. According to W3Techs, <a href="https://w3techs.com/technologies/details/ml-xhtml/all/all">55% of websites are in XHTML</a>. While this is a majority, it still leaves out a large number of websites. In fact, for this retrofitting example, I worked around this limitation by running Hacker News’ HTML code through an <a href="https://www.it.uc3m.es/jaf/html2xhtml/">HTML to XHTML converter</a>.

In the next section, we'll explore how the Tritium transformation language was built to address these issues.

## Responsive Delivery

In the example above, we’ve used transformations in the browser to create a responsive experience for an existing website, but conceptually the two approaches overlap. Because responsive Web design is itself about <strong>changing presentation across multiple screen sizes</strong>, transformations can help in that process as well. Instead of simply pairing different CSS styles to the same fixed HTML as in typical responsive design, we can leverage transformations to change the HTML across devices.

As we explored earlier, the ability to manipulate the HTML (which is missing from CSS alone) not only creates flexibility but actually improves the separation between presentation and content. As a result, maintainability becomes easier because the content is more semantic and less tied to layout. In essence, think of this as moving the breakpoints in responsive design to the transformation layer.

At <a href="https://www.moovweb.com/?utm_source=d_smashingmag&amp;utm_medium=d_article&amp;utm_campaign=d_smashingmag">Moovweb</a>, we’ve leveraged these insights about transformations to implement a technique called responsive delivery, which draws inspiration from responsive Web design, RESS and adaptive design. With responsive delivery, transformations are used to adapt an existing website to different touch points, such as smartphones and tablets.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/64dcd9ab-73fa-4b49-bf2d-23549ae3085a/transforms-5-responsive-delivery-large-opt.jpg"><img title="The data flow in this responsive delivery configuration transforms desktop HTML for mobile and tablet end points." src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dba07dd0-0176-413b-ad82-1bb8fc59b49f/transforms-5-responsive-delivery-opt.jpg" alt="TThe data flow in this responsive delivery configuration transforms desktop HTML for mobile and tablet end points." width="500" height="200" /></a><br>
<em>The data flow in this responsive delivery configuration transforms desktop HTML for mobile and tablet end points. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/64dcd9ab-73fa-4b49-bf2d-23549ae3085a/transforms-5-responsive-delivery-large-opt.jpg">Large view</a>)</em>

Because the transformed website inherits directly from the desktop, responsive delivery provides the unified content and functionality across touch points that you get with responsive Web design, while the majority of the processing is done server-side. And because <strong>transformations can be used to manipulate the HTML</strong>, we get the benefits that we saw earlier: independent and precise control over the look and feel for each touch point, thanks to an abstraction that separates content from layout.

In some sense, we can think of responsive delivery as part of a larger trend of <a href="https://www.slideshare.net/yiibu/adaptation-why-responsive-design-actually-begins-on-the-server/">weaving adaptive design techniques</a> into responsive design and moving more processing to the server, as in <a href="https://www.lukew.com/ff/entry.asp?1392">RESS</a>.

Also worth noting is that responsive delivery can power desktop websites. In the ideal scenario, the back end would produce semantic but unstyled HTML (affectionately called “wireframe HTML”), and the responsive delivery layer would transform the output for all user touch points.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d2c835a4-70de-4125-9ae7-df65405bba30/transforms-6-wireframe-responsive-delivery-large-opt.jpg"><img title="The data flow in this responsive delivery configuration uses wireframe HTML as the source data for transformations that output to mobile, tablet, app, and desktop end points." src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1442164a-710b-4ba1-b490-359f209b3602/transforms-6-wireframe-responsive-delivery-opt.jpg" alt="The data flow in this responsive delivery configuration uses wireframe HTML as the source data for transformations that output to mobile, tablet, app and desktop end points." width="500" height="255" /></a><br>
<em>The data flow in this responsive delivery configuration uses wireframe HTML as the source data for transformations that output to mobile, tablet, app and desktop end points. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d2c835a4-70de-4125-9ae7-df65405bba30/transforms-6-wireframe-responsive-delivery-large-opt.jpg">Large view</a>)</em>

Especially in large organizations, this makes for a powerful decoupling of teams. Back-end engineers can focus purely on functionality (i.e. producing the “wireframe HTML”), and front-end designers can focus on the experience (i.e. transforming the wireframe HTML into a styled Web page). Because the channel between both teams is simply HTML, both teams understand it, and passing through implementation details that are inherited by the front end (such as styles and JavaScript) becomes easy.

<strong>Consider a simple autocomplete widget.</strong> With a responsive delivery approach, the back-end engineer would write the server code to support an autocomplete API and embed the corresponding JavaScript that powers the widget in the wireframe HTML. The designer could then style the widget using CSS and transformations and, if necessary, add JavaScript beyond the stub provided by the back-end engineer. The key point is that HTML is used as a flexible carrier of both content and functionality, as opposed to XML or JSON, which represent only data.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/09150076-32f6-49dc-827e-264d990c1646/transforms-7-wireframe-example-large-opt.jpg"><img title="Shown here are the wireframe HTML and the transformed mobile and desktop output used to power Remix Moovweb." src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dd748467-9235-4ecc-9c80-cf95d6d4a67f/transforms-7-wireframe-example-opt.jpg" alt="Shown here are the wireframe HTML and the transformed mobile and desktop output used to power Remix Moovweb." width="500" height="255" /></a><br>
<em>Shown here are the wireframe HTML and the transformed mobile and desktop output used to power Remix Moovweb. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/09150076-32f6-49dc-827e-264d990c1646/transforms-7-wireframe-example-large-opt.jpg">Large view</a>)</em>

One way of applying this approach is to use a software-as-a-service platform to process transformations in the cloud. This is the service that we built at Moovweb to power mobile websites and apps for Macy’s and 1-800-Flowers, among others, using our own open-source transformation language, called Tritium. Tritium was designed by Hampton Catlin, inventor of the CSS preprocessor <a href="https://sass-lang.com/">Sass</a>. He used his experience to create a transformation language that’s accessible to Web designers and developers. Some features that we felt would be important to the language are the following:

*   **Familiar syntax**.  The syntax should be similar to CSS and jQuery so that it’s more familiar and readable than XSLT’s XML syntax.
*   **Imperative style**.  We wanted to use an imperative programming style, instead of the function and recursive processing model of XSLT.
*   **Input transparency**.  The input is passed directly to the output, so there is no need for a construct like the identity transformation (as is the case with XSLT). Stated differently, the identity transformation is an empty document.
*   **HTML-compatible**.  Tritium was designed to process regular HTML, so it can be used on any website, not just XHTML websites (as with XSLT).

For a simple “Hello world” example, the following Tritium script will select all of the HTML table elements with an ID of <code>foo</code> and change their <code>width</code> attributes to <code>100%</code>:

<pre><code class="language-markup">
# Select all HTML nodes that are table elements with ID of foo.

# The $$() function takes a regular CSS selector
$$("table#foo") {
        # change the width attributes to "100%""
        attribute("width", "100%")
}
</code></pre>

The Tritium language has its own <a href="https://tritium.io">official website</a>, and Moovweb has scheduled to open-source the language in 2014. Developers interested in contributing are encouraged to check out the public <a href="https://github.com/moovweb/tritium">GitHub repository</a> for the core Tritium parser library.

To compare an example, the analogous Tritium code for adding Foundation to an HTML document, as we did earlier with XSLT, would be this:

<pre><code class="language-markup">
  # Install Foundation in the document
  $$("head") {
    inject_top('&lt;link rel="stylesheet" href="normalize.css" /&gt;
                &lt;link rel="stylesheet" href="foundation.css" /&gt;
                &lt;script src="custom.modernizr.js"&gt;&lt;/script&gt;')
  }
  $$("body") {
    inject_bottom('&lt;script src="zepto.js"&gt;&lt;/script&gt;
                   &lt;script src="foundation.min.js"&gt;&lt;/script&gt;
                   &lt;script&gt;$(document).foundation();&lt;/script&gt;')
  }   
</code></pre>

Recall that, in the case of XSLT, the relative placement of new content in the document relies on the judicious placement of the <code>&lt;xsl:apply-templates&gt;</code> tag. However, in the Tritium code just above, the straightforwardly named functions <code>inject_top</code> and <code>inject_bottom</code> are used to insert the boilerplate HTML that installs Foundation.

In practice, the Moovweb SDK offers a <a href="https://developer.moovweb.com/training/advanced/foundation">Foundation scaffold</a> that installs the Foundation boilerplate for you. The scaffold also offers convenience functions to use other components in the Foundation framework. For example, we would use the following functions to create the responsive top bar for Hacker News:

<pre><code class="language-markup">foundation.tbar() {
  foundation.tbar_title("Hacker News", "", "menu-icon")
  foundation.tbar_section("right") {
    move_here("//span[@class='pagetop']//a"){
      wrap("li")
    }
  }
}
</code></pre>

As in the XSLT example, the XPath selector <code>"//span[@class='pagetop']//a"</code> is used to select the links for the menu, but the <code>foundation.tbar*()</code> convenience functions make it easier and spare us from having to know the details of the top bar’s HTML format.

As a final example, a full project implementing the responsive retrofit of Hacker News with Tritium is <a href="https://github.com/moovweb-demos/responsive-retrofit-example">available on GitHub</a> for you to run and play with using the Moovweb SDK. Unlike the XSLT version, which uses HTML downloaded from Hacker News (due to the need to run it through an XHTML converter), you can run this project with the live version of the website.</p>

## Transform Your Thinking

Closures once sat obscurely in functional languages until languages such as JavaScript and Ruby brought them into the mainstream. Likewise, transformations have been buried in frameworks that are alien to the average developer, and the popularity of the transformation approach has been married to the fate of XSLT.

This is unfortunate because transformations are more about a new way of thinking than about any particular technology. They <strong>enable a powerful separation of content and logic from presentation</strong>, and the usefulness of this separation is important in a number of ways. As we move into the post-PC era, transformations provide one part of the answer to serving websites across a wide array of form factors.

Furthermore, the separation enabled by transformations enhances productivity and accelerates the iteration cycle for visual design teams. Meanwhile, for developers who rearrange DOM objects via JavaScript or jQuery, transformations are a new lens on their current workflow, and they open up new doors to optimizing tasks, such as server-side transformation.

In an industry that has no shortage of new ideas, sometimes the most useful thing is to connect new concepts with old ones to make them more digestible. That is what this article has tried to do with transformations. Hopefully, we’ve demonstrated the power of thinking in transformations, showing its relevance to anyone who works with HTML.

{{< signature "al, ea" >}}

