---
title: Building Pattern Libraries With Shadow DOM In Markdown
slug: pattern-libraries-in-markdown
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9c6a7204-2640-4361-86e1-b25880c924c5/markdown-shadowdom-preview-opt.png
date: 2017-07-11T18:42:04.000Z
author: heydon-pickering
description: >-
  Some people hate writing documentation, and others just hate writing. I happen
  to love writing; otherwise, you wouldn't be reading this. It helps that I love
  writing because, as a design consultant offering professional guidance,
  writing is a big part of what I do. But I hate, hate, hate word processors.

  When writing technical web documentation (read: [pattern
  libraries](https://www.smashingmagazine.com/taking-pattern-libraries-next-level/)),
  word processors are not just disobedient, but inappropriate. Ideally, I want a
  mode of writing that allows me to include the components I'm documenting
  inline, and this isn't possible unless the documentation itself is made of
  HTML, CSS and JavaScript. In this article, I'll be sharing a method for easily
  including code demos in Markdown, with the help of shortcodes and shadow DOM
  encapsulation.
categories:
  - Coding
  - Style Guides
  - Pattern Libraries
---
My typical workflow using a desktop word processor goes something like this:

1.  Select some text I want to copy to another part of the document.
2.  Note that the application has selected slightly more or less than I told it to.
3.  Try again.
4.  Give up and resolve to add the missing part (or remove the extra part) of my intended selection later.
5.  Copy and paste the selection.
6.  Note that the formatting of the pasted text is somehow different from the original.
7.  Try to find the styling preset that matches the original text.
8.  Try to apply the preset.
9.  Give up and apply the font family and size manually.
10.  Note that there is too much white space above the pasted text, and press "Backspace" to close the gap.
11.  Note that the text in question has elevated itself several lines at once, joined the heading text above it and adopted its styling.
12.  Ponder my mortality.

When writing technical web documentation (read: [pattern libraries](https://www.smashingmagazine.com/taking-pattern-libraries-next-level/)), word processors are not just disobedient, but inappropriate. Ideally, I want a mode of writing that allows me to include the components I'm documenting inline, and this isn't possible unless the documentation itself is made of HTML, CSS, and JavaScript. In this article, I'll be sharing a method for easily including code demos in Markdown, with the help of shortcodes and shadow DOM encapsulation.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9c6a7204-2640-4361-86e1-b25880c924c5/markdown-shadowdom-preview-opt.png" width="499" height="221" alt="An M, a down-arrow plus a dective hidden in the dark symbolizing Markdown and Shadown Dom" /></a></figure>

{{% feature-panel %}}

## CSS And Markdown

Say what you will about CSS, but it's certainly a more consistent and reliable typesetting tool than any WYSIWYG editor or word processor on the market. Why? Because there's no high-level black-box algorithm that tries to second-guess what styles you _really_ intended to go where. Instead, it's very explicit: You define [which elements take which styles in which circumstances](https://www.smashingmagazine.com/2016/11/css-inheritance-cascade-global-scope-new-old-worst-best-friends/), and it honors those rules.

The only trouble with CSS is that it requires you to write its counterpart, HTML. Even great lovers of HTML would likely concede that writing it manually is on the arduous side when you just want to produce prose content. This is where Markdown comes in. With its terse syntax and reduced feature set, it offers a mode of writing that is easy to learn but can still — once converted into HTML programmatically — harness CSS' powerful and predictable typesetting features. There's a reason why it has become the _de facto_ format for static website generators and modern blogging platforms such as Ghost.

Where more complex, bespoke markup is required, most Markdown parsers will accept raw HTML in the input. However, the more one relies on complex markup, the less accessible one's authoring system is to those who are less technical, or those short on time and patience. This is where shortcodes come in.</p>

## Shortcodes In Hugo

[Hugo](https://www.smashingmagazine.com/2015/11/static-website-generators-jekyll-middleman-roots-hugo-review/#hugo) is a static site generator written in Go — a multi-purpose, compiled language developed at Google. Due to concurrency (and, no doubt, other low-level language features I don't fully understand), Go makes Hugo a lightening-fast generator of static web content. This is one of the many reasons why Hugo has been chosen for the new version of Smashing Magazine.

Performance aside, it works in a similar fashion to the Ruby and [Node.js](https://www.smashingmagazine.com/2017/03/interactive-command-line-application-node-js/)-based generators with which you may already be familiar: Markdown plus meta data (YAML or TOML) processed via templates. Sara Soueidan has written an [excellent primer](https://www.sarasoueidan.com/blog/jekyll-ghpages-to-hugo-netlify/) on Hugo's core functionality.

For me, Hugo's killer feature is its [implementation of shortcodes](https://gohugo.io/extras/shortcodes/). Those coming from WordPress may already be familiar with the concept: a shortened syntax primarily used for including the complex embed codes of third-party services. For instance, WordPress includes a Vimeo shortcode that takes just the ID of the Vimeo video in question.

<pre><code class="language-html">
[vimeo 44633289]
</code></pre>

The brackets signify that their content should be processed as a shortcode and expanded into the full HTML embed markup when the content is parsed.

Making use of Go template functions, Hugo provides an extremely simple API for creating custom shortcodes. For example, I have created a simple Codepen shortcode to include among my Markdown content:

<pre><code class="language-html">
Some Markdown content before the shortcode. Aliquam sodales rhoncus dui, sed congue velit semper ut. Class aptent taciti sociosqu ad litora torquent.

{{&lt;codePen VpVNKW&gt;}}

Some Markdown content after the shortcode. Nulla vel magna sit amet dui lobortis commodo vitae vel nulla sit amet ante hendrerit tempus.
</code></pre>

Hugo automatically looks for a template named `codePen.html` in the `shortcodes` subfolder to parse the shortcode during compilation. My implementation looks like this:

<pre><code class="language-html">
{{ if .Site.Params.codePenUser }}
  &lt;iframe height='300' scrolling='no' title="code demonstration with codePen" src='//codepen.io/{{ .Site.Params.codepenUser | lower }}/embed/{{ .Get 0 }}/?height=265&amp;theme-id=dark&amp;default-tab=result,result&amp;embed-version=2' frameborder='no' allowtransparency='true' allowfullscreen='true' style='width: 100%;'&gt;
    &lt;div&gt;
      &lt;a href="//codepen.io/{{ .Site.Params.codePenUser | lower }}/pen/{{ .Get 0 }}"&gt;See the demo on codePen&lt;/a&gt;
    &lt;/div&gt;
  &lt;/iframe&gt;
{{ else }}
  &lt;p class="site-error"&gt;&lt;strong&gt;Site error:&lt;/strong&gt; The &lt;code&gt;codePenUser&lt;/code&gt; param has not been set in &lt;code&gt;config.toml&lt;/code&gt;&lt;/p&gt;
{{ end }}
</code></pre>

To get a better idea of how the Go template package works, you'll want to consult Hugo's "[Go Template Primer](https://gohugo.io/templates/go-templates/)." In the meantime, just note the following:

*   It's pretty fugly but powerful nonetheless.
*   The `{{ .Get 0 }}` part is for retrieving the first (and, in this case, only) argument supplied — the Codepen ID. Hugo also supports named arguments, which are supplied like HTML attributes.
*   The `.` syntax refers to the current context. So, `.Get 0` means "Get the first argument supplied for the current shortcode."

In any case, I think shortcodes are the best thing since shortbread, and Hugo's implementation for writing custom shortcodes is impressive. I should note from my research that it's possible to use [Jekyll includes](https://jekyllrb.com/docs/includes/) to similar effect, but I find them less flexible and powerful.</p>

## Code Demos Without Third Parties

I have a lot of time for Codepen (and the other code playgrounds that are available), but there are inherent issues with including such content in a pattern library:

*   It uses an API so cannot be easily or efficiently made to work offline.
*   It doesn't just represent the pattern or component; it is its own complex interface wrapped in its own branding. This creates unnecessary noise and distraction when the focus should be on the component.

For some time, I tried to embed component demos using my own iframes. I would point the iframe to a local file containing the demo as its own web page. By using iframes, I was able to encapsulate style and behavior without relying on a third party.

Unfortunately, iframes are rather unwieldy and difficult to resize dynamically. In terms of authoring complexity, it also entails maintaining separate files and having to link to them. I'd prefer to write my components in place, including just the code needed to make them work. I want to be able to write demos as I write their documentation.</p>

## The `demo` Shortcode

Fortunately, Hugo allows you to create shortcodes that include content between opening and closing shortcode tags. The content is available in the shortcode file using `{{ .Inner }}`. So, suppose I were to use a `demo` shortcode like this:

<pre><code class="language-html">
{{&lt;demo&gt;}}
    This is the content!
{{&lt;/demo&gt;}}
</code></pre>

"This is the content!" would be available as `{{ .Inner }}` in the `demo.html` template that parses it. This is a good starting point for supporting inline code demos, but I need to address encapsulation.</p>

### Style Encapsulation

When it comes to encapsulating styles, there are three things to worry about:

*   styles being inherited by the component from the parent page,
*   the parent page inheriting styles from the component,
*   styles being shared unintentionally between components.

One solution is to carefully manage CSS selectors so that there's no overlap between components and between components and the page. This would mean using esoteric selectors per component, and it is not something I would be interested in having to consider when I could be writing terse, readable code. One of the advantages of iframes is that styles are encapsulated by default, so I could write `button { background: blue }` and be confident it would only apply inside the iframe.

A less intensive way to prevent components from inheriting styles from the page is to use the `all` property with the `initial` value on an elected parent element. I can set this element in the `demo.html` file:

<pre><code class="language-html">
&lt;div class="demo"&gt;
    {{ .Inner }}
&lt;/div&gt;
</code></pre>

Then, I need to apply `all: initial` to instances of this element, which propagates to children of each instance.

<pre><code class="language-css">
.demo { all: initial }
</code></pre>

The behavior of <code>initial</code> is quite&hellip; idiosyncratic. In practice, all of the affected elements go back to adopting just their user agent styles (like <code>display: block</code> for <code>&lt;h2></code> elements). However, the element to which it is applied — <code>class="demo"</code> — needs to have certain user agent styles explicitly reinstated. In our case, this is just <code>display: block</code>, since <code>class="demo"</code> is a <code>&lt;div></code>.

<pre><code class="language-css">
.demo { 
  all: initial;
  display: block;
}
</code></pre>

**Note:** `all` is so far not supported in Microsoft Edge but is under consideration. Support is, otherwise, [reassuringly broad](https://caniuse.com/#feat=css-all). For our purposes, the `revert` value would be more robust and reliable but it is not yet supported anywhere.</p>

### Shadow DOM'ing The Shortcode

<p>Using <code>all: initial</code> does not make our inline components completely immune to outside influence (specificity still applies), but we can be confident that styles are unset because we are dealing with the reserved <code>demo</code> class name. Mostly just inherited styles from low-specificity selectors such as <code>html</code> and <code>body</code> will be eliminated.

<p>Nonetheless, this only deals with styles coming from the parent into components. To prevent styles written for components from affecting other parts of the page, we'll need to use <a href="https://glazkov.com/2011/01/14/what-the-heck-is-shadow-dom/">shadow DOM</a> to create an encapsulated subtree.</p>

<p>Imagine I want to document a styled <code>&lt;button&gt;</code> element. I'd like to be able to simply write something like the following, without fear that the <code>button</code> element selector will apply to <code>&lt;button&gt;</code> elements in the pattern library itself or in other components in the same library page.</p>

<pre><code class="language-html">
{{&lt;demo&gt;}}
&lt;button&gt;My button&lt;/button&gt;
&lt;style&gt;
button {
    background: blue;
    padding: 0.5rem 1rem;
    text-transform: uppercase;
}
&lt;/style&gt;
{{&lt;/demo&gt;}}
</code></pre>

<p>The trick is to take the <code>{{ .Inner }}</code> part of the shortcode template and include it as the <code>innerHTML</code> of a new <code>ShadowRoot</code>. I might implement this like so:</p>

<pre><code class="language-html">
{{ $uniq := .Inner | htmlEscape | base64Encode | truncate 15 "" }}
&lt;div class="demo" id="demo-{{ $uniq }}"&gt;&lt;/div&gt;
&lt;script&gt;
    (function() {
        var root = document.getElementById('demo-{{ $uniq }}');
        root.attachShadow({mode: 'open'});
        root.innerHTML = '{{ .Inner }}';
    })();
&lt;/script&gt;
</code></pre>

<ul>
<li><code>$uniq</code> is set as a variable to identify the component container. It pipes in some Go template functions to create a unique string… hopefully(!) &mdash; this isn't a bulletproof method; it's just for illustration.</li>

<li><code>root.attachShadow</code> makes the component container a shadow DOM host.</li>

<li>I populate the <code>innerHTML</code> of the <code>ShadowRoot</code> using <code>{{ .Inner }}</code>, which includes the now-encapsulated CSS.</li>
</ul>

### Permitting JavaScript Behavior

<p>I'd also like to include JavaScript behavior in my components. At first, I thought this would be easy; unfortunately, JavaScript inserted via <code>innerHTML</code> is not parsed or executed. This can be solved by importing from the content of a <code>&lt;template&gt;</code> element. I amended my implementation accordingly.</p>

<pre><code class="language-html">
{{ $uniq := .Inner | htmlEscape | base64Encode | truncate 15 "" }}
&lt;div class="demo" id="demo-{{ $uniq }}"&gt;&lt;/div&gt;
&lt;template id="template-{{ $uniq }}"&gt;
    {{ .Inner }}
&lt;/template&gt;
&lt;script&gt;
    (function() {
        var root = document.getElementById('demo-{{ $uniq }}');
        root.attachShadow({mode: 'open'});
        var template = document.getElementById('template-{{ $uniq }}');
        root.shadowRoot.appendChild(document.importNode(template.content, true));
    })();
&lt;/script&gt;
</code></pre>

<p>Now, I'm able to include an inline demo of, say, a working toggle button:</p>

<pre><code class="language-html">
{{&lt;demo&gt;}}
&lt;button&gt;My button&lt;/button&gt;
&lt;style&gt;
button {
    background: blue;
    padding: 0.5rem 1rem;
    text-transform: uppercase;
}

[aria-pressed="true"] {
    box-shadow: inset 0 0 5px #000;
}
&lt;/style&gt;
&lt;script&gt;
var toggle = document.querySelector('[aria-pressed]');

toggle.addEventListener('click', (e) =&gt; {
  let pressed = e.target.getAttribute('aria-pressed') === 'true';
  e.target.setAttribute('aria-pressed', !pressed);
});
&lt;/script&gt;
{{&lt;/demo&gt;}}
</code></pre>

<p><strong>Note:</strong> I have written in depth about <a href="https://inclusive-components.design/toggle-button/">toggle buttons and accessibility</a> for Inclusive Components.</p>

### JavaScript Encapsulation

<p>JavaScript is, to my surprise, <a href="https://robdodson.me/shadow-dom-javascript/">not encapsulated automatically</a> like CSS is in shadow DOM. That is, if there was another <code>[aria-pressed]</code> button in the parent page before this component's example, then <code>document.querySelector</code> would target that instead.</p>

<p>What I need is an equivalent to <code>document</code> for just the demo's subtree. This is definable, albeit quite verbosely:</p>

<pre><code class="language-javascript">
document.getElementById('demo-{{ $uniq }}').shadowRoot;
</code></pre>

<p>I didn't want to have to write this expression whenever I had to target elements inside demo containers. So, I came up with a hack whereby I assigned the expression to a local <code>demo</code> variable and prefixed scripts supplied via the shortcode with this assignment:</p>

<pre><code class="language-javascript">
if (script) {
  script.textContent = `(function() { var demo = document.getElementById(\'demo-{{ $uniq }}\').shadowRoot; ${script.textContent} })()`
}
root.shadowRoot.appendChild(document.importNode(template.content, true));
</code></pre>

<p>With this in place, <code>demo</code> becomes the equivalent of <code>document</code> for any component subtrees, and I can use <code>demo.querySelector</code> to easily target my toggle button.</p>

<pre><code class="language-html">
var toggle = demo.querySelector('[aria-pressed]');
</code></pre>

<p>Note that I have enclosed the demo's script contents in an immediately invoked function expression (IIFE), so that the <code>demo</code> variable &mdash; and all proceeding variables used for the component &mdash; are not in the global scope. This way, <code>demo</code> can be used in any shortcode's script but will only refer to the shortcode in hand.</p>

<p>Where ECMAScript6 is available, it's possible to achieve localization using "block scoping," with just braces enclosing <code>let</code> or <code>const</code> statements. However, all other definitions within the block would have to use <code>let</code> or <code>const</code> (eschewing <code>var</code>) as well.</p>

<pre><code class="language-javascript">
{
	let demo = document.getElementById(\'demo-{{ $uniq }}\').shadowRoot;
	// Author script injected here
}
</code></pre>

### Shadow DOM Support

<p>Of course, all of the above is only possible where shadow DOM version 1 is supported. Chrome, Safari, Opera and Android all look pretty good, but Firefox and Microsoft browsers are problematic. It is possible to feature-detect support and provide an error message where <code>attachShadow</code> is not available:</p>

<pre><code class="language-javascript">
if (document.head.attachShadow) {
  // Do shadow DOM stuff here
} else {
  root.innerHTML = 'Shadow DOM is needed to display encapsulated demos. The browser does not have an issue with the demo code itself';
}
</code></pre>

<p>Or you can include Shady DOM and the Shady CSS extension, which means a somewhat large dependency (60 KB+) and a different API. Rob Dodson was kind enough to provide me with a <a href="https://gist.github.com/robdodson/287030402bad4b496a0361314138f0f9">basic demo</a>, which I'm happy to share to help you get started.</p>

## Captions For Components

<p>With the basic inline demo functionality in place, quickly writing working demos inline with their documentation is mercifully straightforward. This affords us the luxury of being able to ask questions like, "What if I want to provide a caption to label the demo?" This is perfectly possible already since &mdash; as previously noted &mdash; Markdown supports raw HTML.</p>

<pre><code class="language-html">
&lt;figure role="group" aria-labelledby="caption-button"&gt;
    {{&lt;demo&gt;}}
    &lt;button&gt;My button&lt;/button&gt;
    &lt;style&gt;
    button {
        background: blue;
        padding: 0.5rem 1rem;
        text-transform: uppercase;
    }
    &lt;/style&gt;
    {{&lt;/demo&gt;}}
    &lt;figcaption id="caption-button"&gt;A standard button&lt;/figcaption&gt;
&lt;/figure&gt;
</code></pre>

<p>However, the only new part of this amended structure is the wording of the caption itself. Better to provide a simple interface for supplying it to the output, saving my future self &mdash; and anyone else using the shortcode &mdash; time and effort and reducing the risk of coding typos. This is possible by supplying a named parameter to the shortcode &mdash; in this case, simply named <code>caption</code>:</p>

<pre><code class="language-html">
{{&lt;demo caption="A standard button">}}
    ... demo contents here...
{{&lt;/demo&gt;}}
</code></pre>

<p>Named parameters are accessible in the template like <code>{{ .Get "caption" }}</code>, which is simple enough. I want the caption and, therefore, the surrounding <code>&lt;figure&gt;</code> and <code>&lt;figcaption&gt;</code> to be optional. Using <code>if</code> clauses, I can supply the relevant content only where the shortcode provides a caption argument:</p>

<pre><code class="language-html">
{{ if .Get "caption" }}
    &lt;figcaption&gt;{{ .Get "caption" }}&lt;/figcaption&gt;
{{ end }}
</code></pre>

<p>Here's how the full <code>demo.html</code> template now looks (admittedly, it's a bit of a mess, but it does the trick):</p>

<pre><code class="language-html">
{{ $uniq := .Inner | htmlEscape | base64Encode | truncate 15 "" }}
{{ if .Get "caption" }}
&lt;figure role="group" aria-labelledby="caption-{{ $uniq }}"&gt;
{{ end }}
    &lt;div class="demo" id="demo-{{ $uniq }}"&gt;&lt;/div&gt;
    {{ if .Get "caption" }}
        &lt;figcaption id="caption-{{ $uniq }}"&gt;{{ .Get "caption" }}&lt;/figcaption&gt;
    {{ end }}
{{ if .Get "caption" }}
&lt;/figure&gt;
{{ end }}
&lt;template id="template-{{ $uniq }}"&gt;
    {{ .Inner }}
&lt;/template&gt;
&lt;script&gt;
  (function() {
      var root = document.getElementById('demo-{{ $uniq }}');
      root.attachShadow({mode: 'open'});
      var template = document.getElementById('template-{{ $uniq }}');
      var script = template.content.querySelector('script');
      if (script) {
          script.textContent = `(function() { var demo = document.getElementById(\'demo-{{ $uniq }}\').shadowRoot; ${script.textContent} })()`
       }
       root.shadowRoot.appendChild(document.importNode(template.content, true));
  })();
&lt;/script&gt;</code></pre>

<p>One last note: Should I want to support markdown syntax in the caption value, I can pipe it through Hugo's <code>markdownify</code> function. This way, the author is able to supply markdown (and HTML) but is not forced to do either.</p>

<pre><code class="language-html">
{{ .Get "caption" | markdownify }}
</code></pre>

## Conclusion

<p>For its performance and its many excellent features, Hugo is currently a comfortable fit for me when it comes to static site generation. But the inclusion of shortcodes is what I find most compelling. In this case, I was able to create a simple interface for a documentation issue that I've been trying to solve for some time.</p>

<p>As in web components, a lot of markup complexity (sometimes exacerbated by adjusting for accessibility) can be hidden behind shortcodes. In this case, I'm referring to my inclusion of <code>role="group"</code> and the <code>aria-labelledby</code> relationship, which provides a better supported "group label" to the <code>&lt;figure&gt;</code> &mdash; not things that anyone relishes coding more than once, especially where unique attribute values need to be considered in each instance.</p>

<p>I believe shortcodes are to Markdown and content what web components are to HTML and functionality: a way to make authorship easier, more reliable and more consistent. I look forward to further evolution in this curious little field of the web.</p>

### Resources

<ul>
<li><a href="https://gohugo.io/overview/introduction/">Hugo documentation</a></li>

<li>"<a href="https://golang.org/pkg/text/template/">Package Template</a>," The Go Programming Language</li>

<li>"<a href="https://gohugo.io/extras/shortcodes">Shortcodes</a>," Hugo</li>

<li>"<a href="https://developer.mozilla.org/en/docs/Web/CSS/all">all</a>" (CSS shorthand property), Mozilla Developer Network</li>

<li>"<a href="https://developer.mozilla.org/en-US/docs/Web/CSS/initial">initial</a> (CSS keyword), Mozilla Developer Network</a></li>

<li>"<a href="https://developers.google.com/web/fundamentals/getting-started/primers/shadowdom">Shadow DOM v1: Self-Contained Web Components</a>," Eric Bidelman, Web Fundamentals, Google Developers</li>

<li>"<a href="https://www.webcomponents.org/community/articles/introduction-to-template-element">Introduction to Template Elements</a>," Eiji Kitamura, WebComponents.org</li>

<li>"<a href="https://jekyllrb.com/docs/includes/">Includes</a>," Jekyll</li>

{{< signature "vf, al, il" >}}

