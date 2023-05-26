---
title: 'Improving The Accessibility Of Your Markdown'
slug: improving-accessibility-of-markdown
author: eric-bailey
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fa95c8d2-8322-4766-ac8d-891dabff0dd6/improving-accessibility-of-markdown.jpg
date: 2021-09-28T09:00:00.000Z
summary: >-
  You can find Markdown in many places on the Internet. This article covers different aspects of Markdown and how it interacts with other technology. At first, it may seem daunting since there is a lot of content to cover across a few different subject areas, but keep in mind that each tweak and update will have a direct impact on someone’s quality of life when using the web.
description: >-
  You can find Markdown in many places on the Internet. This article covers different aspects of Markdown and how it interacts with other technology.
categories:
  - Tools
  - Accessibility
  - Browsers
  - User Experience
---

Markdown is a small text to HTML conversion language. It was [created by John Gruber in 2004](https://daringfireball.net/projects/markdown/) with the goal of making writing formatted text in a [plain text editor](https://en.m.wikipedia.org/wiki/Text_editor#Plain_text_vs._rich_text) easier. You can find Markdown in many places on the internet, especially in locations where developers are present. Two notable examples are comments on GitHub and the source code for posts on Smashing Magazine!

## How Markdown Works

Markdown uses special arrangements of characters to format content. For example, you can create a link by wrapping a character, word, or phrase in square brackets. After the closing square bracket, you then include a URL wrapped in parenthesis to create a destination for the link.

So typing:

<pre><code class="language-markdown">[I am a link](https://www.smashingmagazine.com/)</code></pre>

Would create the following HTML markup:

<pre><code class="language-markdown">&lt;a href="https://www.smashingmagazine.com/"&gt;I am a link&lt;/a&gt;</code></pre>

You can also blend HTML with Markdown, and it will all boil down to HTML when compiled. The following example:

<pre><code class="language-markdown">I am a sentence that includes &lt;span class="class-name"&gt;HTML&lt;/span&gt; and __Markdown__ formatting.</code></pre>

Generates this as HTML markup:

<pre><code class="language-markdown">&lt;p&gt;I am a sentence that includes &lt;span class="class-name"&gt;HTML&lt;/span&gt; and &lt;strong&gt;Markdown&lt;/strong&gt; formatting.&lt;/p&gt;</code></pre>

## Markdown And Accessibility

Accessibility is a holistic concern, meaning that it affects every aspect of creating and maintaining digital experiences. Since Markdown is a digital tool, it also has accessibility considerations to be aware of.

- **The good news**:  
Markdown generates simple HTML markup, and simple HTML markup can be easily read by assistive technology. 
- **The less good news**:  
Markdown isn’t all-encompassing, nor is it prescriptive. In addition, there is more to accessibility than just assistive technology. 

When it comes to ensuring your Markdown content is accessible, there are two big-picture issues:

1. There are certain types of content Markdown does not support, and 
2. There isn’t a [Clippy-esque experience](https://en.m.wikipedia.org/wiki/Office_Assistant) to accompany you while you write, meaning that you won’t get a warning if you do something that will create inaccessible content.

Because of these two considerations, there are things we can do to ensure our Markdown content is as accessible as it can be.

{{% feature-panel %}}

## The Three Most Important Things You Can Do

It can be difficult to know where to start when it comes to making your content accessible. Here are three things you can do right now to make a large, significant impact.

### 1. Use Headings To Outline Your Content

Navigating by heading is by far [the most popular method](https://webaim.org/projects/screenreadersurvey9/#finding) many assistive technology users use to understand the content of the page or view they’re looking at.

Because of this, you want to use [Markdown’s heading formatting](https://www.markdownguide.org/basic-syntax/#headings) options (`#` , `##`, `###`, `####`, `#####`, and `######`) to create a logical heading structure:

<pre><code class="language-markdown">
# The title, a first-level heading

Content

## A second-level heading

Content

### A third-level heading

Content

## Another second-level heading

Content</code></pre>

This creates a hierarchical outline that is easy to scan:

<pre><code class="language-markdown">1. The title, a first-level heading
    a. A second-level heading
        i. A Third-level heading
    b. Another second-level heading</code></pre>

[Writing effective heading levels is a bit of an art](https://webdesign.tutsplus.com/articles/the-importance-of-heading-levels-for-assistive-technology--cms-31753), in that you want enough information to communicate the overall scope of the page, but not overwhelm someone by over-describing. For example, a recipe might only need a few `h2` elements to section the ingredients, instructions, and backstory, while an academic paper might need all six heading levels to fully communicate nuance.

Being able to quickly scan all the headings on a page or view and jump to a specific one is a technique that isn’t limited to just screen readers, either. I enjoy and benefit from extensions such as [headingsMap](https://github.com/dzc34/headingsMap) that let you take advantage of this feature.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7087aff1-d22a-44b1-ac2c-84b33e6e51b7/1-improving-accessibility-of-markdown.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7087aff1-d22a-44b1-ac2c-84b33e6e51b7/1-improving-accessibility-of-markdown.png" width="800" height="516" sizes="100vw" caption="Here is the heading outline for this post. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7087aff1-d22a-44b1-ac2c-84b33e6e51b7/1-improving-accessibility-of-markdown.png'>Large preview</a>)" alt="ALT: The HeadingsMap browser extension showing a nested tree of headings for this post. Screenshot." >}}

### 2. Write Meaningful Alternate Descriptions For Your Images

Alternate descriptions help folks who have low vision or are browsing with images turned off to understand the content of the image you’re using. 

In Markdown, an alternate description is placed in between the opening and closing brackets of the [image formatting code](https://www.markdownguide.org/basic-syntax/#images):

<pre><code class="language-markdown">![A sinister-looking shoebill staring at the camera.](https://live.staticflickr.com/3439/3259412053_92f822bee2_b.jpg)</code></pre>

An alternate description should clearly and concisely describe the content of the image and the context of why it was included. Also [don’t forget to add punctuation](https://thoughtbot.com/blog/add-punctuation-to-your-alt-text)!

Certain websites and web apps that use Markdown input will also try to add alternate description text for you. For example, GitHub will use the name of the file you upload for the `alt` attribute:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/35ef4840-c4de-4969-b15c-f4ba0b68c7d2/2-improving-accessibility-of-markdown.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/35ef4840-c4de-4969-b15c-f4ba0b68c7d2/2-improving-accessibility-of-markdown.png" width="800" height="327" sizes="100vw" caption="I don’t know what this image contains. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/35ef4840-c4de-4969-b15c-f4ba0b68c7d2/2-improving-accessibility-of-markdown.png'>Large preview</a>)" alt="Screenshot of a new GitHub issue. The title reads, “A sample GitHub issue with an uploaded image. The body is an image element with an alt attribute that reads, “ScreenCapture at Wed Aug 18 15:59:24 EDT 2021.”" >}}

Unfortunately, this does not provide enough context for a person who can’t see the image. In this scenario, you want to communicate why the image is important enough to be included. 

Examples of this you’ll commonly see on GitHub include:

- A visual bug, where something doesn’t look the way it’s supposed to,
- A new feature that is being proposed,
- An annotated screenshot providing feedback,
- Graphs and flowcharts that explain processes, and
- Reaction GIFs for communicating emotion.

[These images aren’t decorative](https://www.smashingmagazine.com/2021/06/img-alt-attribute-alternate-description-decorative/). Since GitHub is public by default, you don’t know who is accessing your repo, or their circumstances. Better to proactively include them.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8e558f2c-084c-49d9-a905-34cafd18d6c6/3-improving-accessibility-of-markdown.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8e558f2c-084c-49d9-a905-34cafd18d6c6/3-improving-accessibility-of-markdown.png" width="800" height="298" sizes="100vw" caption="Much better! (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8e558f2c-084c-49d9-a905-34cafd18d6c6/3-improving-accessibility-of-markdown.png'>Large preview</a>)" alt="Screenshot of a new GitHub issue. The title reads, “A sample GitHub issue with an uploaded image. The body is an image element with an alt attribute that reads, “A tooltip poking through an active slide drawer navigation menu.”" >}}

If you need help writing alternate descriptions, I’d enthusiastically recommend [the W3C’s alt Decision Tree](https://www.w3.org/WAI/tutorials/images/decision-tree/) and [Axess Lab’s Ultimate Guide to Alt Texts](https://axesslab.com/alt-texts/).

### 3. Use Plain Language

Simple, direct language helps everyone understand your content. This includes people:

- With [cognitive considerations](https://thenextweb.com/news/designing-for-cognitive-accessibility-where-to-begin), 
- Who don’t use English as their primary language, 
- Unfamiliar with the concepts you’re communicating,
- Who are stressed or multitasking and have limited attention spans, 
- And so on.

The easier it is for someone to read what you write, the easier it is for them to understand and internalize it. This helps with every form of written Markdown content, be it blog posts, Jira tickets, Notion notes, GitHub comments, Trello cards, and so on. 

Consider your sentence and word lengths. Also, consider who your intended audience is, and think about things like the jargon and idioms you use. 

If you need help simplifying your language, three tools I like to use are [Hemingway](https://hemingwayapp.com/), [Datayze’s Readability Analyzer](https://datayze.com/readability-analyzer), and the [xkcd Simple Writer](https://xkcd.com/simplewriter/). Another site worth checking out is [plainlanguage.gov](https://www.plainlanguage.gov/guidelines/words/use-simple-words-phrases/).

{{% ad-panel-leaderboard %}}

## Other Considerations

Want to go the extra mile? Great! Here are some things you can do:

### Images

In addition to providing alternate descriptions, there are a few other things you can do to make your Markdown-inserted images accessible.

#### Mark Up SVG Images Properly

SVG is a great format for graphs, icons, simple illustrations, and other kinds of imagery that uses simple shapes and crisp lines.

There are two ways to render SVG in Markdown. Both approaches have specific things you’ll need to be on the lookout for:

**1. Linking to an image with a `.svg` file extension**

**Note**: *The bug that I’m about to describe [has been fixed](https://www.scottohara.me/note/2021/09/03/img-svg-source.html), however, I’m still recommending the following advice for the next couple of years. This is due to Safari’s questionable tactic of tying browser updates to system updates, as well as hesitancy around updating software for some people who use assistive technology.*

If you’re linking to an SVG as an image, you’ll want to use HTML’s `img` element, and not Markdown’s image formatting code (`![]()`). 

The reason for this is that certain screen readers have bugs when they try to parse an `img` element that links to an SVG file. Instead of announcing it as expected as an image, it will [announce it as a group, or skip announcing the image entirely](https://www.scottohara.me/blog/2019/05/22/contextual-images-svgs-and-a11y.html#image-elements-with-svg-source-exception). To fix this, declare `role="img"` on the image element:

<pre><code class="language-markdown">&lt;img 
  role="img" 
  alt="A sylized sunflower."
  src="flower.svg" /&gt;</code></pre>

**2. Using Inline SVG Code**

There are a few reasons for declaring an image as inline SVG code instead of using an `img` element. The reason I most often encounter is to support dark mode.

Much like with using an img element, there are a couple of attributes you need to include to ensure assistive technology interprets it as an image, and not code. The two attribute declarations are `role="img"` and `aria-labelledby`:

<pre><code class="language-markdown">&lt;svg
  aria-labelledby="svg-title"
  fill="none"
  height="54"
  role="img"
  viewBox="0 0 90 54"
  width="90"
  xmlns="https://www.w3.org/2000/svg"&gt;
  &lt;title id="svg-title"&gt;A pelican.&lt;/title&gt;
  &lt;path class="icon-fill" d="M88.563 2.193H56.911a7.84 7.84 0 00-12.674 8.508h-.001l.01.023c.096.251.204.495.324.733l4.532 10.241-1.089 1.09-6.361-6.554a10.18 10.18 0 00-7.305-3.09H0l5.229 4.95h7.738l2.226 2.107H7.454l4.451 4.214h7.741l1.197 1.134c.355.334.713.66 1.081.973h-7.739a30.103 30.103 0 0023.019 7.076L16.891 53.91l22.724-5.263v2.454H37.08v2.81h13.518v-.076a2.734 2.734 0 00-2.734-2.734h-5.441v-3.104l2.642-.612a21.64 21.64 0 0014.91-30.555l-1.954-4.05 1.229-1.22 3.165 3.284a9.891 9.891 0 0013.036 1.066L90 5.061v-1.43c0-.794-.643-1.438-1.437-1.438zM53.859 6.591a1.147 1.147 0 110-2.294 1.147 1.147 0 010 2.294z"/&gt;&lt;/svg&gt;
</code></pre>

You’ll also want to ensure you use a `title` element (not to be confused with [the `title` attribute](https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes/title)) to describe the image, similar to an `img` element’s `alt` attribute. Unlike an `alt` attribute, you’ll also need to associate the `id` of the `title` element with its parent `svg` element by using `aria-labelledby`.

If you’d like to go deeper on accessibly marking up SVG, I recommend [Accessible SVGs](https://css-tricks.com/accessible-svgs/) by [Heather Migliorisi](https://twitter.com/_hmig), and [Accessible SVGs: Perfect Patterns For Screen Reader Users](https://www.smashingmagazine.com/2021/05/accessible-svg-patterns-comparison/) by [Carie Fisher](https://cariefisher.com/).

#### Load With Animated Images Paused

Animated GIFs are another common thing you’ll find with Markdown content &mdash; I find them more often than not being used by a developer to express their delight and frustration when discussing a technical topic.

The thing is, these animations can be distracting and adversely affect someone who is trying to read through your content. Cognitive considerations such as ADHD are especially affected here.

The good news is you can still include animated content! There are a few options:

1. Use [the `picture` element](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/picture), using filetypes such as `.mp4` and `.webm` that can load in a paused state, or
2. Use a solution that gives play/pause functionality to a `.gif`, such as [Steve Faulkner’s `details`/`summary` hack](https://codepen.io/stevef/pen/ExPdNMM?editors=1000), or the [freezeframe.js library](https://github.com/ctrl-freaks/freezeframe.js/).

This little detail can go a long way to helping people out without having to abandon a way for you to express yourself.

### Links

If you write content online, sooner or later you’re going to have to use links. Here are some things to be aware of:

#### Use Unique, Descriptive Link Names

Some forms of assistive technology can navigate through a list of links on a page or view the same way they can navigate through headings. Because of this, you want your links to hint at what someone can expect to find if they visit it.

<pre><code class="language-markdown">Learn more about [how to easily poach an egg](https://lifehacker.com/this-is-the-chillest-easiest-way-to-poach-an-egg-1825889759).</code></pre>

You’ll also want to avoid ambiguous phrases, especially if they repeat. Terms like “click here” and “learn more” are common culprits. These terms don’t make sense when separated from the context of their surrounding non-link content. In addition, using the term more than once can create experiences like this:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e7978b14-5c89-465d-b52c-78be080f5235/4-improving-accessibility-of-markdown.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e7978b14-5c89-465d-b52c-78be080f5235/4-improving-accessibility-of-markdown.png" width="800" height="497" sizes="100vw" caption="NVDA’s Elements List viewer showing all the links on a page. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e7978b14-5c89-465d-b52c-78be080f5235/4-improving-accessibility-of-markdown.png'>Large preview</a>)" alt="NVDA’s Elements List panel, set to showing links. The term “Click here” is shown 12 times. Screenshot." >}}

#### Avoid Opening Links In A New Tab Or Window

Certain variants of Markdown such as [Kramdown](https://kramdown.gettalong.org/) allow you to write code that can open links in a new tab or window:

<pre><code class="language-markdown">[link name](url){:target="&#95;blank"}</code></pre>

Doing this creates a [security risk](https://web.dev/external-anchors-use-rel-noopener/). In addition, this experience is so confusing and undesirable that it is [a Web Content Accessibility Guidelines (WCAG) success criterion](https://www.w3.org/WAI/WCAG21/Understanding/change-on-request.html). It is far better to let everyone using your website or web app [make the choice](https://inclusivedesignprinciples.org/#give-control) for themselves about whether or not they want to open a link in a new tab.

#### Use Skip Links With Discretion

[A skip link](https://webaim.org/techniques/skipnav/), or “skipnav" is a way to bypass large sections of content. You’ll commonly encounter them as a way to bypass the logo and main navigation on a webpage, allowing someone to quickly jump to the main content.

{{< vimeo id="604723866" breakout="true" >}}

[Skip links aren’t limited to just this use case](https://knowbility.org/blog/2019/skip-links#not-just-top-content)! Two other examples could be a table of contents and sorting/filtering controls on an e-commerce site.

Another great use for skip links is to allow someone to bypass embedded content that has multiple interactive elements:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f09b9b63-83ee-4549-a2cb-0c9b5f8a3df3/5-improving-accessibility-of-markdown.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f09b9b63-83ee-4549-a2cb-0c9b5f8a3df3/5-improving-accessibility-of-markdown.png" width="800" height="508" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f09b9b63-83ee-4549-a2cb-0c9b5f8a3df3/5-improving-accessibility-of-markdown.png'>Large preview</a>)" alt="An arrow demonstrating how someone can jump from a skip link over embedded content, and land on the skip link target placed immediately after the embedded content." >}}

This is also a great technique for allowing someone to bypass a “[keyboard trap](https://www.w3.org/WAI/WCAG21/Understanding/no-keyboard-trap.html),” something commonly found in embedded content. 

Keyboard traps are where someone who isn’t using a mouse or a touchpad cannot escape an interactive component due to how it is constructed. You’ll typically find these with embedded `iframe` widgets.

A good way to test for keyboard traps? [Use the <kbd>Tab</kbd> key](https://www.matuzo.at/blog/testing-with-tab/)!

Without a skip link, someone using assistive technology may have to resort to refreshing the page or view to escape the trap. This isn’t great and is especially troubling if [motor control concerns](https://webaim.org/articles/motor/motordisabilities) are thrown into the mix. I’m of the school of thought that most people will just close the tab if they run into this scenario, rather than try to wrestle with getting it to work.

In addition to his great post about testing with the <kbd>Tab</kbd> key, [Manuel Matuzović](https://twitter.com/mmatuzo) tells us about his use of skip links, as well as other improvements in [Improving the keyboard accessibility of Embedded CodePens](https://www.matuzo.at/blog/improving-the-keyboard-accessibility-of-codepen-embeds/).

#### Be Careful With Automatically Generated Heading Anchor Links

Some Markdown generators automatically add an anchor link to accompany each heading you write. This is so you can focus someone’s attention to the relevant section on a page or view when sharing content.

The issue is there might be some assistive technology issues with this, depending on how this anchor link is constructed. If the anchor link is only wrapped around a glyph such as #, ¶, or §, we run into two issues:

1. The link’s name does not make sense when removed from its surrounding context, and 
2. The link’s name is repeated.

This issue is discussed in more detail by [Amber Wilson](https://twitter.com/ambrwlsn90) in her post, [Are your Anchor Links Accessible?](https://amberwilson.co.uk/blog/are-your-anchor-links-accessible/) Her post also goes into detail about different solutions, as well as their potential drawbacks.

#### Indicate The Presence Of Downloads

Most of the times links take you to another page or view. Sometimes, however, the destination is [a download](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/a#attr-download). When this happens, the browser either: 

1. Opens an app associated with the request file type to display it, or 
2. Prompts you to save it to the Operating System’s [filesystem](https://en.m.wikipedia.org/wiki/File_system).

These two experiences can be jarring, especially if you can’t see the screen. A good way to prevent this less-than-ideal experience is to hint at the presence of the download in the link’s name. For example, here’s how you would do it in Markdown when linking to a PDF:

<pre><code class="language-markdown">Download our [2020 Annual Report (PDF)](https://mycorp.biz/downloads/2020/annual-report.pdf).</code></pre>

### Color

Color isn’t related to Markdown per se, but it does affect a lot of Markdown-generated content. The biggest color-related concerns are things you can usually modify if you are using a blogging service such as WordPress, Eleventy, Ghost, Jekyll, Gatsby, and so on. 

#### Use A Dark Mode Theme

[Providing a toggle for dark mode](https://piccalil.li/tutorial/create-a-user-controlled-dark-or-light-mode/) allows someone to choose an experience that helps them read. For some, it could be an aesthetic preference, for others it could be a way to avoid things like migraines, eye strain, and fatigue.

The important bit here is choice. Let someone who has dark mode turned on use light mode for your website, and vice-versa (and make sure the UI to do so is accessible).

The thing is, you can’t know what a person’s needs, desires, or circumstances are when they visit your website or web app, but you can provide them with the ability to do something about it.

Let’s also remember that Markdown exports simple, straightforward HTML, and that is easy to work within CSS. This goes a long way to making your dark mode theme easier to develop.

#### Use Syntax Highlighting With Good Color Contrast Support

Markdown can create blocks of code by wrapping content in triple backticks (<code>&#96;&#96;&#96;</code>). It can also create inline content wrapped in the `code` element by wrapping a character, word, or phrase in single backticks.

For both examples, many people add syntax highlighting libraries such as [PrismJS](https://prismjs.com/) to help people understand the code example they’re providing.

Certain themes use light-on-light or dark-on-dark values as an aesthetic choice. Unfortunately, this means the code may be difficult or impossible to see for some individuals. The trick here is to select a syntax highlighting theme that uses color values that are high enough contrast that people can actually see each and every glyph of the code. 

A way to determine if it is high enough contrast is to use [a tool such as WebAIM’s](https://webaim.org/resources/contrastchecker/) and manually check the color values provided by the theme. If you’re looking for a faster suggestion and don’t mind a little self-promotion, I maintain [a color contrast-friendly syntax highlighting theme](https://github.com/ericwbailey/a11y-syntax-highlighting).

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d45e310f-636f-4216-abbe-a23e08397870/6-improving-accessibility-of-markdown.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d45e310f-636f-4216-abbe-a23e08397870/6-improving-accessibility-of-markdown.png" width="800" height="443" sizes="100vw" caption="a11y-dark. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d45e310f-636f-4216-abbe-a23e08397870/6-improving-accessibility-of-markdown.png'>Large preview</a>)" alt="Screenshot of the a11y-dark theme, which uses red, green, teal, and gold colors on a dark gray background to highlight sample HTML and JavaScript code." >}}

### Content That Isn’t Supported By Markdown

Since you can use HTML in Markdown, there are certain kinds of content you’ll see more often than others in Markdown. Here are a few considerations for a couple of them.

#### Use The `title` Attribute To Describe `iframe` Content

[HTML’s `title` attribute](https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes/title) is commonly misused to create a tooltip effect. Unfortunately, [this causes a lot of headaches for assistive technology users](https://www.tpgi.com/using-the-html-title-attribute/), and its usage this way is considered an antipattern.

The one good use of a `title` attribute is to provide a concise, meaningful description of what the `iframe` contains. This description provides assistive technology users a clue about what to expect if they navigate into the `iframe` to check out its contents.

For Markdown, the most common form of `iframe` content will be embeds such as YouTube videos:

<pre><code class="language-markdown">&lt;iframe width="560" height="315" src="https://www.youtube.com/embed/SDdsD5AmKYA" title="YouTube: Accessibility is a Hydra | EJ Mason | CascadiaJS 2019." frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen&gt;&lt;/iframe&gt;</code></pre>

Much like your link text, you’ll also want to avoid generic and repetitive `title` content. YouTube’s embed code defaults to `YouTube video player`, which isn’t so great. We can do a little better and update that to `YouTube: Video title`. This will especially help if there’s more than one YouTube video embedded on the page or view.

As to why YouTube does it this way when it already knows the video title information is another problem entirely.

#### Provide Captions And Transcripts For Videos And Recorded Audio

Speaking of YouTube, another thing you’ll want to do is ensure your video and audio have captions and transcripts. 

##### Captions

Captions display a text version of video content in realtime as it is being spoken, allowing someone who biologically or circumstantially cannot hear audio to be able to understand the video’s content. Captions can also include sound effects, music, and other cues that are important to communicating meaning. 

[Most popular video hosting providers have features to support captioning](https://support.google.com/youtube/answer/2734796?hl=en), including displaying them in an embedded context. The important part here is to avoid [craptions](https://mashable.com/article/youtube-closed-captioning-nomorecraptions)—manually review automatically generated captions to ensure they make sense to a human being.

##### Transcripts

[Transcripts](https://www.w3.org/WAI/media/av/transcripts/) are caption’s sibling. They take all the spoken dialog, pertinent sound effects and music, and other important details and list them outside of the embedded video or audio. There are many benefits to doing this, including allowing someone to:

- Read through the video and audio content at their own pace;
- Modify the size and presentation of the content;
- Print the content out or convert it into a format that’s easier to digest;
- More easily discover the content via search engines;
- More easily translate the content.

{{% ad-panel-leaderboard %}}

## Reader Mode

Like other Markdown-adjacent concerns, Reader Mode can offer a lot of benefits from an accessibility perspective.

If you are unfamiliar, Reader Mode is a feature offered by many browsers that strips away everything other than the main content. Most reader modes also provide controls for adjusting the text size, font, line height, foreground and background color, column width, even having your device read the content out loud for you!

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/937f9f05-56ec-4ef9-ba1b-b16cba8f2019/7-improving-accessibility-of-markdown.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/937f9f05-56ec-4ef9-ba1b-b16cba8f2019/7-improving-accessibility-of-markdown.png" width="800" height="629" sizes="100vw" caption="Microsoft Edge’s Immersive Reader. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/937f9f05-56ec-4ef9-ba1b-b16cba8f2019/7-improving-accessibility-of-markdown.png'>Large preview</a>)" alt="Microsoft Edge’s Immersive Reader mode being applied to the Smashing Magazine post, A Complete Guide To Accessibility Tooling by Nic Chan. Screenshot." >}}

You can’t directly trigger Reader Mode by using Markdown. Longform Markdown content, however, is often rendered in templates that can be set to make them Reader Mode-friendly. 

[Mandy Michael](https://twitter.com/Mandy_Kerr) teaches us how to do this in her post, [Building websites for Safari Reader Mode and other reading apps](https://medium.com/@mandy.michael/building-websites-for-safari-reader-mode-and-other-reading-apps-1562913c86c9). A combination of semantic HTML, [sectioning elements](https://developer.mozilla.org/en-US/docs/Web/Guide/HTML/Content_categories#sectioning_content), and a dash of [structured microdata](https://schema.org/BlogPosting) are all it takes to unlock this great feature.

## You Don’t Have To Do Everything At Once

This is a long post that covers different aspects of Markdown and how it interacts with other technology. It can seem daunting, in that it is a lot of content to cover across a few different subject areas.

The thing about accessibility work is that every little bit helps. You don’t have to address every consideration I have in this post in one big, sweeping change. Instead, try picking one thing to focus on, and build from there. 

Know that each tweak and update will have a direct impact on someone’s quality of life when using the web, and that’s huge.

### Continue Reading on Smashing Magazine

- [CommonMark: A Formal Specification For Markdown](https://www.smashingmagazine.com/2020/12/commonmark-formal-specification-markdown/)
- [Building A Node.js Express API To Convert Markdown To HTML](https://www.smashingmagazine.com/2019/04/nodejs-express-api-markdown-html/)
- [Building Pattern Libraries With Shadow DOM In Markdown](https://www.smashingmagazine.com/2017/07/pattern-libraries-in-markdown/)

{{< signature "vf, yk, il" >}}
