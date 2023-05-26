---
title: 'CommonMark: A Formal Specification For Markdown'
slug: commonmark-formal-specification-markdown
author: adebiyi-adedotun
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1585ffad-37a0-4e72-ad72-2ecd39e9dfee/commonmark-formal-specification-markdown.png
date: 2020-12-03T11:00:00.000Z
summary: >-
  Markdown is a powerful markup language that allows editing and formatting in plain text format that can then be parsed and rendered as HTML. It has a declarative syntax that is both powerful and easy to learn for technical and non-technical folks. However, due to the consequential ambiguities in its original specification, there have been a number of distinct [flavors (or custom versions)](https://github.com/commonmark/commonmark-spec/wiki/Markdown-Flavors) that aim to erase those ambiguities as well as extend the original syntax support. This has led to a steep divergence from what can be parsed and what is rendered. CommonMark aims to provide a standardized specification of Markdown that reflects its real-world usage.
description: >-
  Markdown has a declarative syntax that is both powerful and easy to learn for technical and non-technical folks. However, due to the consequential ambiguities in its original specification, there have been a number of distinct flavors (or custom versions). This has led to a steep divergence from what can be parsed and what is rendered. Find out how CommonMark provides a standardized specification of Markdown that reflects its real-world usage.
categories:
  - Tools
  - Coding
  - Techniques
---

CommonMark is a rationalized version of Markdown syntax with a spec whose goal is to remove the ambiguities and inconsistency surrounding the original Markdown specification. It offers a standardized specification that defines the common syntax of the language along with a suite of comprehensive tests to validate Markdown implementations against this specification.

GitHub uses Markdown as the markup language for its user content.

<blockquote>“CommonMark is an ambitious project to formally specify the Markdown syntax used by many websites on the internet in a way that reflects its real-world usage [...] It allows people to continue using Markdown the same way they always have while offering developers a comprehensive specification and reference implementations to interoperate and display Markdown in a consistent way between platforms.”<br /><br />&mdash; “<a href="https://github.blog/2017-03-14-a-formal-spec-for-github-markdown/">A Formal Spec For GitHub Flavored Markdown</a>,” The GitHub Blog</blockquote>

In 2012, GitHub proceeded to create its own flavor of Markdown &mdash; [GitHub Flavored Markdown](https://github.github.com/gfm/) (GFM) &mdash; to combat the lack of Markdown standardization, and extend the syntax to its needs. GFM was built on top of [Sundown](https://github.com/vmg/sundown), a parser specifically built by GitHub to solve some of the shortcomings of the existing Markdown parsers at the time. Five years after, in 2017, it announced the deprecation of Sundown in favor of CommonMark parsing and rendering library, [cmark](https://github.com/commonmark/cmark) in [A formal spec for GitHub Flavored Markdown](https://github.blog/2017-03-14-a-formal-spec-for-github-markdown/).

In the [Common Questions](https://code.visualstudio.com/Docs/languages/markdown#_common-questions) section of [Markdown and Visual Studio Code](https://code.visualstudio.com/Docs/languages/markdown), it is documented that Markdown in VSCode targets the CommonMark Markdown specification using the [markdown-it](https://github.com/markdown-it/markdown-it) library, which in itself follows the CommonMark specification.

CommonMark has been widely adopted and implemented (see the [List of CommonMark Implementations](https://github.com/commonmark/commonmark-spec/wiki/List-of-CommonMark-Implementations)) for use in different languages like C (e.g [cmark](https://github.com/commonmark/cmark)), C# (e.g [CommonMark.NET](https://github.com/Knagis/CommonMark.NET)), JavaScript (e.g [markdown-it](https://github.com/markdown-it/markdown-it)) etc. This is good news as developers and authors are gradually moving to a new frontier of been able to use Markdown with a consistent syntax, and a standardized specification.

## A Short Note On Markdown Parsers

Markdown parsers are at the heart of converting Markdown text into HTML, directly or indirectly. 

Parsers like [cmark](https://github.com/commonmark/cmark) and [commonmark.js](https://github.com/commonmark/commonmark.js) do not convert Markdown to HTML directly, instead, they convert it to an [Abstract Syntax Tree (AST)](https://en.wikipedia.org/wiki/Abstract_syntax_tree), and then render the AST as HTML, making the process more granular and subject to manipulation. In between parsing &mdash; to AST &mdash; and rendering &mdash; to HTML &mdash; for example, the Markdown text could be extended.

{{% feature-panel %}}

## CommonMark’s Markdown Syntax Support

[Projects or platforms](https://github.com/commonmark/commonmark-spec/wiki/List-of-CommonMark-Implementations) that already implement the CommonMark specification as the baseline of their specific flavor are often **superset** of the **strict subset** of the CommonMark Markdown specification. For the most part of it, CommonMark has mitigated a lot of ambiguities by building a spec that is built to be built on. GFM is a prime example, while it supports every CommonMark syntax, it also extends it to suits its usage.

CommonMark's syntax support can be limited at first, for example, it has no support for [this table syntax](https://github.github.com/gfm/#tables-extension-), but it is important to know that this is by design as [this comment](https://talk.commonmark.org/t/tables-in-pure-markdown/81/12) in [this thread](https://talk.commonmark.org/t/tables-in-pure-markdown/81) of conversation reveals: that the **supported syntax** is **strict** and said to be the **core** syntax of the language itself &mdash; the same specified by its creator, John Gruber in [Markdown: Syntax](https://daringfireball.net/projects/markdown/syntax).

At the time of writing, here are a number of supported syntax:

1. Paragraphs and Line Breaks,
2. Headers,
3. Emphasis and Strong Emphasis,
4. Horizontal Rules,
5. Lists,
6. Links,
7. Images,
8. Blockquotes,
9. Code,
10. Code Blocks.

*To follow along with the examples, it is advised that you use the [commonmark.js dingus](https://spec.commonmark.org/dingus/) editor to try out the syntax and get the rendered Preview, generated HTML, and AST.*

## Paragraphs And Line Breaks

In Markdown, paragraphs are continuous lines of text separated by at least a blank line.

The following rules define a paragraph:

1. Markdown paragraphs are rendered in HTML as the [Paragraph element, &lt;p&gt;](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/p).
2. Different paragraphs are separated with one or more blank lines between them.
3. For a line break, a paragraph should be post-fixed with two blank spaces (or its tab equivalent), or a backslash (`\`).

<table>
	<thead>
		<tr>
			<th data-tablesaw-priority="persist">Syntax</th>
			<th>Rendered HTML</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td>This is a line of text  </td>
			<td>&lt;p&gt;This is a line of text&lt;/p&gt;</td>
		</tr>
		<tr>
			<td>This is a line of text<br>And another line of text<br>And another but the<br>same paragraph</td>
			<td>&lt;p&gt;This is a line of text<br>And another line of text<br>And another but the<br>same paragraph&lt;/p&gt; </td>
		</tr>
		<tr>
			<td>This is a paragraph<br><br>And another paragraph<br><br>And another</td>
			<td>&lt;p&gt;This is a paragraph&lt;/p&gt;<br>&lt;p&gt;And another paragraph&lt;/p&gt;<br>&lt;p&gt;And another&lt;/p&gt;</td>
		</tr>
		<tr>
			<td>Two spaces after a line of text  <br>Or a post-fixed backslash\<br>Both means a line break</td>
			<td>&lt;p&gt;Two spaces after a line of text&lt;br /&gt;&lt;br&gt;Or a post-fixed backslash&lt;br /&gt;&lt;br&gt;Both means a line break&lt;/p&gt;</td>
		</tr>
	</tbody>
</table>

- [Interactive tutorial](https://commonmark.org/help/tutorial/03-paragraphs.html) to learn about paragraphs.
- [Dingus permalink](https://spec.commonmark.org/dingus/?text=This%20is%20a%20line%20of%20text%0A%0AThis%20is%20a%20line%20of%20text%0AAnd%20another%20line%20of%20text%0AAnd%20another%20but%20the%0Asame%20paragraph%0A%0AThis%20is%20a%20paragraph%0A%0AAnd%20another%20paragraph%0A%0AAnd%20another%0A%0ATwo%20spaces%20after%20a%20line%20of%20text%20%20%0AOr%20a%20post-fixed%20backslash%5C%0ABoth%20means%20a%20line%20break) check out the full example with the Preview and AST.
- Learn more about [paragraphs](https://github.github.com/gfm/#paragraphs).

## Headings

Headings in Markdown represents one of the HTML [Heading elements](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/Heading_Elements). There are two ways to define headings:

1. ATX heading.
2. Setext heading.

The following rules define [ATX](https://www.aaronsw.com/2002/atx/) headings:

1. Heading level 1 (`h1`), through to heading level 6, (`h6`) are supported.
2. Atx-style headings are prefixed with the hash (`#`) symbol.
3. There needs to be at least a blank space separating the text and the hash (`#`) symbol.
4. The count of hashes is equivalent to the cardinal number of the heading. One hash is `h1`, two hashes, `h2`, 6 hashes, `h6`.
5. It is also possible to append an arbitrary number of hash symbol(s) to headings, although this doesn't cause any effect (i.e. `# Heading 1 #`)


<table>
	<thead>
		<tr>
			<th data-tablesaw-priority="persist">Syntax</th>
			<th>Rendered HTML</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td># Heading 1</td>
			<td>&lt;h1&gt;Heading 1&lt;/h1&gt;</td>
		</tr>
		<tr>
			<td>## Heading 2</td>
			<td>&lt;h2&gt;Heading 2&lt;/h2&gt;</td>
		</tr>
		<tr>
			<td>### Heading 3</td>
			<td>&lt;h3&gt;Heading 3&lt;/h3&gt;</td>
		</tr>
		<tr>
			<td>#### Heading 4</td>
			<td>&lt;h4&gt;Heading 4&lt;/h4&gt;</td>
		</tr>
		<tr>
			<td>##### Heading 5</td>
			<td>&lt;h5&gt;Heading 5&lt;/h5&gt;</td>
		</tr>
		<tr>
			<td>###### Heading 6</td>
			<td>&lt;h6&gt;Heading 6&lt;/h6&gt;</td>
		</tr>
		<tr>
			<td>## Heading 2 ##</td>
			<td>&lt;h2&gt;Heading 2&lt;/h2&gt;</td>
		</tr>
	</tbody>
</table>

The following rules define [Setext](https://docutils.sourceforge.net/mirror/setext.html) headings:

1. Only Heading level 1 (h1), and heading level 2, (h2) are supported.
2. Setext-style definition is done with the equals (=) and dash symbols respectively.
3. With Setext, at least one equal or dash symbol is required.

<table>
	<thead>
		<tr>
			<th data-tablesaw-priority="persist">Syntax</th>
			<th>Rendered HTML</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td>Heading 1<br>=</td>
			<td>&lt;h1&gt;Heading 1&lt;/h1&gt;</td>
		</tr>
		<tr>
			<td>Heading 2<br>-</td>
			<td>&lt;h2&gt;Heading 2&lt;/h2&gt;</td>
		</tr>
	</tbody>
</table>

- [Interactive tutorial](https://commonmark.org/help/tutorial/04-headings.html) to learn about headings.
- [Dingus permalink](https://spec.commonmark.org/dingus/?text=%23%20Heading%201%0A%23%23%20Heading%202%0A%23%23%23%20Heading%203%0A%23%23%23%23%20Heading%204%0A%23%23%23%23%23%20Heading%205%0A%23%23%23%23%23%23%20Heading%206%0A%23%23%20Heading%202%20%23%23%0A%0AHeading%201%0A%3D%0AHeading%202%0A-%0AHeading%201%0A%3D%3D%3D%3D%3D%3D%3D%3D%3D%0AHeading%202%0A-----------%0A%0A) to check out the full example with the Preview and AST.
- Learn more about [ATX headings](https://github.github.com/gfm/#atx-headings).
- Learn more about [Setext headings](https://github.github.com/gfm/#setext-headings).

{{% ad-panel-leaderboard %}}

## Emphasis And Strong Emphasis

Emphasis in Markdown can either be italics or bold (strong emphasis).

The following rules define emphasis:

1. Ordinary and strong emphasis are rendered in HTML as the [Emphasis, &lt;em&gt;](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/em), and [Strong, &lt;strong&gt;](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/strong) element, respectively.
2. A text bounded by a single asterisk (`*`) or underscore (`_` ) will be an emphasis.
3. A text bounded by double asterisks or underscore will be a strong emphasis.
4. The bounding symbols (asterisks or underscore) must match.
5. There must be no space between the symbols and the enclosed text.

<table>
	<thead>
		<tr>
			<th data-tablesaw-priority="persist">Syntax</th>
			<th>Rendered HTML</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td><code>_Italic_</code></td>
			<td>&lt;em&gt;Italic&lt;/em&gt;</td>
		</tr>
		<tr>
			<td><code>*Italic*</code></td>
			<td>&lt;em&gt;Italic&lt;/em&gt;</td>
		</tr>
		<tr>
			<td><code>__Bold__</code></td>
			<td>&lt;strong&gt;Bold&lt;/strong&gt;</td>
		</tr>
		<tr>
			<td><code>**Bold**</code></td>
			<td>&lt;strong&gt;Bold&lt;/strong&gt;</td>
		</tr>
	</tbody>
</table>

- [Interactive tutorial](https://commonmark.org/help/tutorial/02-emphasis.html) to learn about emphasis.
- [Dingus permalink](https://spec.commonmark.org/dingus/?text=_empahsis_%0A*empahsis*%0A**strong%20emhasis**%0A__empahsis__) to check out the full example with the Preview and AST.
- Learn more about [Emphasis and strong emphasis](https://github.github.com/gfm/#emphasis-and-strong-emphasis).

## Horizontal Rule

A [Horizontal rule, &lt;hr/&gt;](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/hr) is created with three or more asterisks (`*`), hyphens (`-`), or underscores (`_`), on a new line. The symbols are separated by any number of spaces, or not at all.

<table>
	<thead>
		<tr>
			<th data-tablesaw-priority="persist">Syntax</th>
			<th>Rendered HTML</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td><code>***</code></td>
			<td>&lt;hr /&gt;</td>
		</tr>
		<tr>
			<td><code>* * *</code></td>
			<td>&lt;hr /&gt;</td>
		</tr>
		<tr>
			<td><code>---</code></td>
			<td>&lt;hr /&gt;</td>
		</tr>
		<tr>
			<td><code>- - -</code></td>
			<td>&lt;hr /&gt;</td>
		</tr>
		<tr>
			<td><code>___</code></td>
			<td>&lt;hr /&gt;</td>
		</tr>
		<tr>
			<td><code>_ _ _</code></td>
			<td>&lt;hr /&gt;</td>
		</tr>
	</tbody>
</table>

- [Dingus permalink](https://spec.commonmark.org/dingus/?text=***%0A*%20*%20*%0A---%0A-%20-%20-%0A___%0A_%20_%20_) to check out the full example with the Preview and AST.
- Learn more about [Thematic breaks](https://github.github.com/gfm/#thematic-breaks).

## Lists

Lists in Markdown are either a bullet (unordered) list or an ordered list.

The following rules define a list:

1. Bullet lists are rendered in HTML as the [Unordered list element, &lt;ul&gt;](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/ul).
2. Ordered lists are rendered in HTML as the [Ordered list element, &lt;ol&gt;](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/ol).
3. Bullet lists use asterisks, pluses, and hyphens as markers.
4. Ordered lists use numbers followed by periods or closing parenthesis.
5. The markers must be consistent (you must only use the marker you begin with for the rest of the list items definition).

<table>
	<thead>
		<tr>
			<th data-tablesaw-priority="persist">Syntax</th>
			<th>Rendered HTML</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td>* one<br>* two<br>* three</td>
			<td>&lt;ul&gt;<br />&lt;li&gt;one&lt;/li&gt;<br />&lt;li&gt;two&lt;/li&gt;<br />&lt;li&gt;three&lt;/li&gt;<br />&lt;/ul&gt;</td>
		</tr>
		<tr>
			<td>+ one<br>+ two<br>+ three</td>
			<td>&lt;ul&gt;<br />&lt;li&gt;one&lt;/li&gt;<br />&lt;li&gt;two&lt;/li&gt;<br />&lt;li&gt;three&lt;/li&gt;<br />&lt;/ul&gt;</td>
		</tr>
		<tr>
			<td>- one<br>- two<br>- three</td>
			<td>&lt;ul&gt;<br />&lt;li&gt;one&lt;/li&gt;<br />&lt;li&gt;two&lt;/li&gt;<br />&lt;li&gt;three&lt;/li&gt;<br />&lt;/ul&gt;</td>
		</tr>
		<tr>
			<td>- one<br>- two<br>+ three</td>
			<td>&lt;ul&gt;<br />&lt;li&gt;one&lt;/li&gt;<br />&lt;li&gt;two&lt;/li&gt;<br />&lt;/ul&gt;<br />&lt;ul&gt;<br />&lt;li&gt;three&lt;/li&gt;<br />&lt;/ul&gt;</td>
		</tr>
		<tr>
			<td>1. one<br>2. two<br>3. three</td>
			<td>&lt;ol&gt;<br />&lt;li&gt;one&lt;/li&gt;<br />&lt;li&gt;two&lt;/li&gt;<br />&lt;li&gt;three&lt;/li&gt;<br />&lt;/ol&gt;</td>
		</tr>
		<tr>
			<td>3. three<br>4. four<br>5. five</td>
			<td>&lt;ol start="3"&gt;<br />&lt;li&gt;three&lt;/li&gt;<br />&lt;li&gt;four&lt;/li&gt;<br />&lt;li&gt;five&lt;/li&gt;<br />&lt;/ol&gt;</td>
		</tr>
		<tr>
			<td>1. one<br>2. two<br>3. three</td>
			<td>&lt;ol&gt;<br />&lt;li&gt;one&lt;/li&gt;<br />&lt;li&gt;two&lt;/li&gt;<br />&lt;li&gt;three&lt;/li&gt;<br />&lt;/ol&gt;</td>
		</tr>
	</tbody>
</table>

- [Interactive tutorial](https://commonmark.org/help/tutorial/06-lists.html) to learn about lists.
- [Dingus permalink](https://spec.commonmark.org/dingus/?text=*%20one%0A*%20two%0A*%20three%0A---%0A%2B%20one%0A%2B%20two%0A%2B%20three%0A***%0A-%20one%0A-%20two%0A-%20three%0A---%0A-%20one%0A-%20two%0A%2B%20three%0A---%0A1.%20one%0A2.%20two%0A3.%20three%0A___%0A3.%20three%0A4.%20four%0A5.%20five%0A___%0A1.%20one%0A100.%20two%0A3.%20three) to check out the full example with the Preview and AST.
- Learn more about [Lists items](https://github.github.com/gfm/#list-items).

## Links

Links are supported with the **inline** and **reference** format.

The following rules define a link:

1. Links are rendered as the HTML [Anchor element, &lt;a&gt;](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/a).
2.  The inline format has the syntax: `[value](URL "optional-title")` with no space between the brackets.
3. The reference format has the syntax: `[value][id]` for the reference, and `[id]: href "optional-title"` for the hyperlink label, separated with at least a line.
4. The `id` is the **Definition Identifier** and may consist of letters, numbers, spaces, and punctuation.
5. Definition Identifiers are not case sensitive.
6. There is also support for Automatic Links, where the URL is bounded by the less than (<) and greater than (>) symbol, and displayed literally.

<div class="break-out">

<pre><code class="language-html">&lt;!--Markdown--&gt;
[Google](https://google.com “Google”)
&lt;!--Rendered HTML--&gt;
&lt;a href="https://google.com" title="Google"&gt;Google&lt;/a&gt;

&lt;!--Markdown--&gt;
[Google](https://google.com)
&lt;!--Rendered HTML--&gt;
&lt;a href="https://google.com"&gt;Google&lt;/a&gt;

&lt;!--Markdown--&gt;
[Comparing Styling Methods in Next.js](/2020/09/comparing-styling-methods-next-js)
&lt;!--Rendered HTML--&gt;
&lt;a href="/2020/09/comparing-styling-methods-next-js"&gt;Comparing Styling Methods In Next.js&lt;/a&gt;

&lt;!--Markdown--&gt;
[Google][id]
&lt;!--At least a line must be in-between--&gt;
[id]: https://google.com "Google"
&lt;!--Rendered HTML--&gt;
&lt;a href="https://google.com" title="Google"&gt;Google&lt;/a&gt;

&lt;!--Markdown--&gt;
&lt;https://google.com&gt;
&lt;!--Rendered HTML--&gt;
&lt;a href="https://google.com"&gt;google.com&lt;/a&gt;

&lt;!--Markdown--&gt;
&lt;mark@google.com&gt;
&lt;!--Rendered HTML--&gt;
&lt;a href="mailto:mark@google.com"&gt;mark@google.com&lt;/a&gt;
</code></pre>
</div>

- [Interactive tutorial](https://commonmark.org/help/tutorial/07-links.html) to learn about links.
- [Dingus permalink](https://spec.commonmark.org/dingus/?text=%5BGoogle%5D(https%3A%2F%2Fgoogle.com%20%22Google%22)%0A%0A---%0A%0A%5BGoogle%5D(https%3A%2F%2Fgoogle.com)%0A%0A---%0A%0A%5BComparing%20Styling%20Methods%20In%20Next.js%5D(%2F2020%2F09%2Fcomparing-styling-methods-next-js)%0A%0A---%0A%0A%5BGoogle%5D%5Bid%5D%0A%0A%5Bid%5D%3A%20https%3A%2F%2Fgoogle.com%20%22Google%22%0A%0A---%0A%0A%3Chttps%3A%2F%2Fgoogle.com%3E) to check out the full example with the Preview and AST.
- Learn more about [Links](https://github.github.com/gfm/#links).

## Images

Images in Markdown follows the **inline** and **reference** formats for Links.

The following rules define images:

1. Images are rendered as the HTML [image element, &lt;img&gt;](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/img).
2. The inline format has the syntax: `![alt text](image-url "optional-title")`.
3. The reference format has the syntax: `![alt text][id]` for the reference, and `[id]: image-url "optional-title"` for the image label. Both should be separated by at least a blank line.
4. The image title is optional, and the image-url can be relative.

<pre><code class="language-html">&lt;!--Markdown--&gt;
![alt text](image-url "optional-title")
&lt;!--Rendered HTML--&gt;
&lt;img src="image-url" alt="alt text" title="optional-title" /&gt;

&lt;!--Markdown--&gt;
![alt text][id]
&lt;!--At least a line must be in-between--&gt;
&lt;!--Markdown--&gt;
[id]: image-url "optional-title"
&lt;!--Rendered HTML--&gt;
&lt;img src="image-url" alt="alt text" title="optional-title" /&gt;</code></pre>

- [Interactive tutorial](https://commonmark.org/help/tutorial/08-images.html) to learn about images.
- [Dingus permalink](https://spec.commonmark.org/dingus/?text=!%5Balt%20text%5D(image-url%20%22optional-title%22)%0A%0A---%0A%0A!%5Balt%20text%5D%5Bid%5D%0A%0A%5Bid%5D%3A%20image-url%20%22optional-title%22) to check out the full example with the Preview and AST.
- Learn more about [Images](https://github.github.com/gfm/#images).

{{% ad-panel-leaderboard %}}

## Blockquotes

The HTML [Block Quotation element, &lt;blockquote&gt;](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/blockquote), can be created by prefixing a new line with the greater than symbol (`>`).

<pre><code class="language-html">&lt;!--Markdown--&gt;
&gt; This is a blockquote element
&gt; You can start every new line
&gt; with the greater than symbol.
&gt; That gives you greater control
&gt; over what will be rendered.

&lt;!--Rendered HTML--&gt;
&lt;blockquote&gt;
&lt;p&gt;This is a blockquote element
You can start every new line
with the greater than symbol.
That gives you greater control
over what will be rendered.&lt;/p&gt;
&lt;/blockquote&gt;</code></pre>

Blockquotes can be nested:

<pre><code class="language-html">&lt;!--Markdown--&gt;
&gt; Blockquote with a paragraph
&gt;&gt; And another paragraph
&gt;&gt;&gt; And another

&lt;!--Rendered HTML--&gt;
&lt;blockquote&gt;
&lt;p&gt;Blockquote with a paragraph&lt;/p&gt;
&lt;blockquote&gt;
&lt;p&gt;And another paragraph&lt;/p&gt;
&lt;blockquote&gt;
&lt;p&gt;And another&lt;/p&gt;
&lt;/blockquote&gt;
&lt;/blockquote&gt;
&lt;/blockquote&gt;</code></pre>

They can also contain other Markdown elements, like headers, code, list items, and so on.

<pre><code class="language-html">&lt;!--Markdown--&gt;
&gt; Blockquote with a paragraph
&gt; # Heading 1
&gt; Heading 2
&gt; -
&gt; 1. One
&gt; 2. Two

&lt;!--Rendered HTML--&gt;
&lt;blockquote&gt;
&lt;p&gt;Blockquote with a paragraph&lt;/p&gt;
&lt;h1&gt;Heading 1&lt;/h1&gt;
&lt;h2&gt;Heading 2&lt;/h2&gt;
&lt;ol&gt;
&lt;li&gt;One&lt;/li&gt;
&lt;li&gt;Two&lt;/li&gt;
&lt;/ol&gt;
&lt;/blockquote&gt;</code></pre>

- [Interactive tutorial](https://commonmark.org/help/tutorial/05-blockquotes.html) to learn about blockquotes.
- [Dingus permalink](https://spec.commonmark.org/dingus/?text=%3E%20This%20is%20a%20blockquote%20element%0A%3E%20You%20can%20start%20every%20new%20line%0A%3E%20with%20the%20greater%20than%20symbol.%0A%3E%20That%20gives%20you%20greater%20control%0A%3E%20over%20what%20will%20be%20rendered.%0A%0A---%0A%0A%3E%20Blockquote%20with%20a%20paragraph%0A%3E%3E%20And%20another%20paragraph%0A%3E%3E%3E%20And%20another%0A%0A---%0A%0A%3E%20Blockquote%20with%20a%20paragraph%0A%3E%20%23%20Heading%201%0A%3E%20Heading%202%0A%3E%20-%0A%3E%201.%20One%0A%3E%202.%20Two%0A) to check out the full example with the Preview and AST.
- Learn more about [Blockquotes](https://github.github.com/gfm/#block-quotes).

## Code

The HTML [Inline Code element, &lt;code&gt;](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/code), is also supported. To create one, delimit the text with back-ticks (&#96;), or double back-ticks if there needs to be a literal back-tick in the enclosing text.

<div class="break-out">

<pre><code class="language-javascript">&lt;!--Markdown--&gt;
`inline code snippet`
&lt;!--Rendered HTML--&gt;
&lt;code&gt;inline code snippet&lt;/code&gt;

&lt;!--Markdown--&gt;
`&lt;button type='button'&gt;Click Me&lt;/button&gt;`
&lt;!--Rendered HTML--&gt;
&lt;code&gt;&lt;button type='button'&gt;Click Me&lt;/button&gt;&lt;/code&gt;

&lt;!--Markdown--&gt;
`` There's an inline back-tick (`). ``
&lt;!--Rendered HTML--&gt;
&lt;code&gt;There's an inline back-tick (`).&lt;/code&gt;</code></pre>
</div>

- [Interactive tutorial](https://commonmark.org/help/tutorial/09-code.html) to learn about code.
- [Dingus permalink](https://spec.commonmark.org/dingus/?text=%60inline%20code%20snippet%60%0A%0A---%0A%0A%60%3Cbutton%20type%3D%27button%27%3EClick%20Me%3C%2Fbutton%3E%60%0A%0A---%0A%0A%60%60%20There%27s%20an%20inline%20back-tick%20(%60).%20%60%60) to check out the full example with the Preview and AST.
- Learn more about [Code spans](https://github.github.com/gfm/#code-spans).

## Code Blocks

<p>The HTML <a href="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/pre">Preformatted Text element, &lt;pre&gt;</a>, is also supported. This can be done with at least three and an equal number of bounding back-ticks (<code>`</code>), or tildes (<code>~</code>) &mdash; normally referred to as a code-fence, or a new line starting indentation of at least 4 spaces.</p>

<div class="break-out">

<pre><code class="language-javascript">&lt;!--Markdown--&gt;
```
const dedupe = (array) =&gt; [...new Set(array)];
```
&lt;!--Rendered HTML--&gt;
&lt;pre&gt;&lt;code&gt;const dedupe = (array) =&gt; [...new Set(array)];&lt;/code&gt;&lt;/pre&gt;

&lt;!--Markdown--&gt;
    const dedupe = (array) =&gt; [...new Set(array)];
&lt;!--Rendered HTML--&gt;
&lt;pre&gt;&lt;code&gt;const dedupe = (array) =&gt; [...new Set(array)];&lt;/code&gt;&lt;/pre&gt;</code></pre>
</div>

- [Interactive tutorial](https://commonmark.org/help/tutorial/09-code.html) to learn about code.
- [Dingus permalink](https://spec.commonmark.org/dingus/?text=%60%60%60%0Aconst%20dedupe%20%3D%20(array)%20%3D%3E%20%5B...new%20Set(array)%5D%3B%0A%60%60%60%0A%0A---%0A%0A%20%20%20%20const%20dedupe%20%3D%20(array)%20%3D%3E%20%5B...new%20Set(array)%5D%3B) to check out the full example with the Preview and AST.
- Learn more about [Fenced](https://github.github.com/gfm/#fenced-code-blocks) and [Indented](https://github.github.com/gfm/#indented-code-blocks) code blocks.

## Using Inline HTML

According to John Grubers original [spec note on inline HTML](https://daringfireball.net/projects/markdown/syntax#html), *any markup that is not covered by Markdown’s syntax, you simply use HTML itself,* with *The only restrictions are that block-level HTML elements — e.g. `<div>`, `<table>`, `<pre>`, `<p>`, etc. &mdash; must be separated from surrounding content by blank lines, and the start and end tags of the block should not be indented with tabs or spaces.*

However, unless you are probably one of the people behind CommonMark itself, or thereabout, you most likely will be writing Markdown with a flavor that is already extended to handle a large number of syntax not *currently* supported by CommonMark.

## Going Forward

CommonMark is a constant work in progress with its [spec last updated on April 6, 2019](https://spec.commonmark.org/). There are a number of popular [applications](https://github.com/commonmark/commonmark-spec/wiki/Applications-supporting-CommonMark) supporting it in the pool of [Markdown tools](https://www.markdownguide.org/tools/). With the awareness of CommonMark’s effort towards standardization, I think it is sufficient to conclude that in Markdown’s simplicity, is a lot of work going on behind the scenes and that it is a good thing for the CommonMark effort that the [formal specification of GitHub Flavored Markdown](https://github.github.com/gfm/) is based on the [specification](https://spec.commonmark.org/).

The move towards the CommonMark standardization effort does not prevent the creation of [flavors](https://github.com/commonmark/commonmark-spec/wiki/Markdown-Flavors) to extend its supported syntax, and as CommonMark gears up for release 1.0 with [issues that must be resolved](https://talk.commonmark.org/t/issues-we-must-resolve-before-1-0-release-6-remaining/1287), there are some interesting resources about the continuous effort that you can use for your perusal.

### Resources

- [Introducing Markdown by John Gruber](https://daringfireball.net/projects/markdown/)
- [CommonMark official website](https://commonmark.org/)
- [GitHub Flavored Markdown Spec](https://github.github.com/gfm/)
- [cmark official repo](https://github.com/commonmark/cmark)
- [GitHub's fork of cmark](https://github.com/github/cmark-gfm)
- [Markdown on Wikipedia](https://en.wikipedia.org/wiki/Markdown)
- [Markdown Guide](https://www.markdownguide.org/)

{{< signature "ks, ra, yk, il" >}}
