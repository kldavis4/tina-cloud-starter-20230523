---
title: 'Designing Better Links For The Web'
slug: designing-better-links-websites-emails-guideline
author: slava-shestopalov
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b157db62-e93c-4607-9c84-698fad4da3b3/designing-better-links-websites-emails-guideline.jpg
date: 2021-12-06T17:30:00.000Z
summary: >-
  There are so many websites out there that have not considered the overall usability of their visually impaired users. When it comes to designing better links and sending better emails, Slava Shestopalov has a few tips on how to improve your website’s experience while accessibility in mind.
description: >-
  There are so many websites out there that have not considered the overall usability of their visually impaired users. When it comes to designing better links and sending better emails, Slava Shestopalov has a few tips on how to improve your website’s experience while accessibility in mind.
categories:
  - Tools
  - Best Practices
  - Accessibility
  - UX
  - Design Patterns
---

Why are “click here” and “by this link” poor choices? And is it acceptable to use “read more”? All these phrases have become so common that many people don’t see any problems with them.

How many times have you encountered or composed the following on websites, in emails, or intranets?

<blockquote><ul><li><em>Fill in this <u>form</u> by the end of the day.</em></li>
<li><em>Check the equipment policy by the <u>link</u>.</em></li>
<li><em>You can find more information <u>here</u>, <u>here</u>, and <u>here</u>.</em></li></ul></blockquote>

In this article, I’ll explain popular wording and formatting mistakes and will show more accessible and informative alternatives. Let’s go!

- [Meaningful Links](#meaningful-links)
- [Exposing URLs](#exposing-urls)
- [Download Links](#download-links)
- [Links vs. Buttons](#links-vs-buttons)
- [Link-Rich Texts](#link-rich-texts)
- [Link Accessibility](#link-accessibility) 
  - [Distinction](#distinction)
  - [Color Contrast](#color-contrast)
  - [Focus State](#focus-state)
  - [Optimization For Screen Readers](#optimization-for-screen-readers)
  - [Duplicated Links](#duplicated-links)

## Meaningful Links

So what exactly is a hyperlink? It’s a combination of a web address (URL) and a clickable element (oftentimes a word or phrase, sometimes an image). While this is a vast topic, we’ll focus on text links, namely their usability and accessibility.

Thoughtfully composed links express respect to readers, whereas **jumbled-up ones cause confusion and suspicion**. When a link is presented as “here” or “this,” it’s harder to aim it with a cursor or finger. Also, it lacks transparency. What is hidden behind it: a page or file, an article or web form? One should re-read the whole sentence or paragraph to guess.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fd05c109-c7cc-4ca7-97b3-869ac54767c6/9-designing-better-links-websites-emails.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fd05c109-c7cc-4ca7-97b3-869ac54767c6/9-designing-better-links-websites-emails.png" width="800" height="463" sizes="100vw" caption="Links embedded into meaningful phrases are more comprehensible. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fd05c109-c7cc-4ca7-97b3-869ac54767c6/9-designing-better-links-websites-emails.png'>Large preview</a>)" alt="A comparison of four phrases with “naughty” links (on the left) and four phrases with “better” links (on the right). It is recommended to avoid using ‘here’ or ‘this’ and use parts of self-explanatory phrases as links." >}}

On the contrary, URLs attached to concise self-explanatory phrases inform people about the destination and are more convenient targets for clicking or tapping. Moreover, **a well-composed link makes sense out of context** and typically combines a topic (e.g. security, brand, marketing) and format (questionnaire, request form, guideline, policy, and so on).

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8bb4cc2f-e0ca-43ce-b151-08ed1b240af3/4-designing-better-links-websites-emails.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8bb4cc2f-e0ca-43ce-b151-08ed1b240af3/4-designing-better-links-websites-emails.png" width="800" height="463" sizes="100vw" caption="A well-composed link text usually makes sense out of context. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8bb4cc2f-e0ca-43ce-b151-08ed1b240af3/4-designing-better-links-websites-emails.png'>Large preview</a>)" alt="A comparison of four phrases on the left that are “in context” and fours phrases on the right that are “out of context”" >}}

## Exposing URLs

If a web address is short and doesn’t look like `M$c0P88%X4LHr&dxQ1A`, then exposing it right away will work quite well, too, especially if the audience is supposed to copy it and paste it somewhere else.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/53cc4336-df49-4515-a615-47678a87133e/16-designing-better-links-websites-emails.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/53cc4336-df49-4515-a615-47678a87133e/16-designing-better-links-websites-emails.png" width="800" height="463" sizes="100vw" caption="In many cases, there is nothing wrong with exposing short URLs; however, it won’t be the most elegant solution from a visual standpoint. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/53cc4336-df49-4515-a615-47678a87133e/16-designing-better-links-websites-emails.png'>Large preview</a>)" alt="A comparison of the links embedded into meaningful phrases (on the left, shown as ‘good’) and links exposing short URLs (right, shown as ‘also decent’)" >}}

And if you’ve got a long indecipherable chain of symbols, exposing it isn’t a great idea in most situations. In this case, consider embedding a URL into a succinct phrase or shortening the address in tools like [Bitly](https://bitly.com/) or [Cuttly](https://cutt.ly/).

However, **these tools aren’t silver bullets**: you do get a shorter link, but its meaningful parts will be replaced with random symbols, which are suspicious and not informative. Customizing shortened URLs is possible, but it’s typically a paid feature.

Compare the following examples:

- `bit.ly/30SjUa4y` (suspicious and unreadable);
- `bit.ly/smashing-books` (readable topic);
- `smash.ing/30SjUa4y` (recognizable domain);
- `smash.ing/books` (fully transparent).

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/545de747-e6d5-42a8-a497-ca13bf7ce02c/17-designing-better-links-websites-emails.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/545de747-e6d5-42a8-a497-ca13bf7ce02c/17-designing-better-links-websites-emails.png" width="800" height="463" sizes="100vw" caption="‘Long gibberish’ URLs occupy much space and are hard to memorize. However, they might become a non-fancy yet practical solution for copy-pasting. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/545de747-e6d5-42a8-a497-ca13bf7ce02c/17-designing-better-links-websites-emails.png'>Large preview</a>)" alt="A comparison of a ‘decent’ way to use shortened links (on the left) and a ‘naughty’ way that don’t look quite that good and use up too much space" >}}

## Download Links

A link that guides to some downloadable resource needs a slightly different treatment. Besides embedding it into a meaningful phrase, you should also **inform users** about the file format and size:

- The format gives clues to what you can do with this data (e.g. if the information is read-only or editable);
- The file size is crucial for people with costly internet, slow connection, or limited local storage.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5d172511-2554-46d3-9342-9669b42bb155/5-designing-better-links-websites-emails.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5d172511-2554-46d3-9342-9669b42bb155/5-designing-better-links-websites-emails.png" width="800" height="463" sizes="100vw" caption="A good practice for download links is to show the file format and size. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5d172511-2554-46d3-9342-9669b42bb155/5-designing-better-links-websites-emails.png'>Large preview</a>)" alt="A comparison of four “ ” ‘naughty’ phrases shown on the left and “ ” ‘better’ ones on the right that tell more about the file format and size" >}}

When you share a bunch of files (let’s say in different formats or versions), it’s not enough to design each link correctly. The whole series should be well-scannable and easy to use.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b92e8c41-e887-4790-ab73-cf5b50e55f61/3-designing-better-links-websites-emails.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b92e8c41-e887-4790-ab73-cf5b50e55f61/3-designing-better-links-websites-emails.png" width="800" height="463" sizes="100vw" caption="More with less: try to edit out repeated words and keep the list compact. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b92e8c41-e887-4790-ab73-cf5b50e55f61/3-designing-better-links-websites-emails.png'>Large preview</a>)" alt="A comparison of the links with many repeated words to the concise links which were edited out and are now ‘less wordy’" >}}

 {{% feature-panel %}}

## Links vs. Buttons

Not all links on a page or in an email are equally important. Authors often want their audience to click on the primary link, whereas other links can be skipped. If you’re going to draw people’s attention to the main action, think of presenting it as a button:

- “Subscribe to the newsletter”
- “Buy tickets”
- “Get the white paper”
- “Download the recording”

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f3a241ea-5007-4f28-a444-d08a94fa1fc1/15-designing-better-links-websites-emails.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f3a241ea-5007-4f28-a444-d08a94fa1fc1/15-designing-better-links-websites-emails.png" width="800" height="463" sizes="100vw" caption="The key link deserves to be a well-noticeable button. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f3a241ea-5007-4f28-a444-d08a94fa1fc1/15-designing-better-links-websites-emails.png'>Large preview</a>)" alt="A “naughty” example presented on the left of a subtle key link used within a random text. On the right, the same title and random text are presented but with a well-noticeable blue button that says “Buy Tickets”" >}}

If you cannot create a button because of technical or time constraints, go for a quick-and-dirty solution: put that link in a separate line, make it bold, add spacing above and below, and so on.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/92f577ec-ccb9-4767-911b-02b4fe70e89b/6-designing-better-links-websites-emails.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/92f577ec-ccb9-4767-911b-02b4fe70e89b/6-designing-better-links-websites-emails.png" width="800" height="463" sizes="100vw" caption="The main link can also be located on a separate line with spacing from the rest of the text. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/92f577ec-ccb9-4767-911b-02b4fe70e89b/6-designing-better-links-websites-emails.png'>Large preview</a>)" alt="An example with the button on the left, while the same title and random text are shown using a main link that is located on a separate line with spacing from the rest of the text" >}}

Of course, button text should follow corresponding patterns so that you don’t cross the line between motivating readers and manipulating them:

- **Be concise** (up to 4&ndash;5 words);
- Ideally, **start with a verb** (e.g. “get”, “buy”, “download”, “apply for”, and so on);
- **Call the action honestly** (i.e. avoid hushing up unpleasant steps like watching ads, registration or submitting personal data).

Compare *“Download the report,”* which assumes that downloading starts immediately after clicking, and *“Get the report,”* when a user downloads the file in exchange for their name and contact details.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6655e70f-5e34-4ebc-99f7-603c1014d381/14-designing-better-links-websites-emails.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6655e70f-5e34-4ebc-99f7-603c1014d381/14-designing-better-links-websites-emails.png" width="800" height="463" sizes="100vw" caption="Prominent buttons are suitable until they turn into aggressive banners or are overused. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6655e70f-5e34-4ebc-99f7-603c1014d381/14-designing-better-links-websites-emails.png'>Large preview</a>)" alt="A comparison of the link button with a long text (left) and another version shown using a concise button with a short text (right)" >}}

## Link-Rich Texts

Links enable the functioning of the Internet, however, vigorously pumping URLs into each sentence isn’t a good practice (of course, unless you contribute to a Wikipedia-like knowledge base that is cross-connected by nature).

Step zero is to make sure you really&mdash;*really*&mdash;need all the links. If you can edit something out, there won’t be a problem to solve. Otherwise, try to **group the links**: as a bulleted list, on the side of related paragraphs, or under a suitable title (e.g. “Recommended materials” or “Resources”).

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/aa6f8d74-74d0-4880-b32d-a68797f9725b/18-designing-better-links-websites-emails.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/aa6f8d74-74d0-4880-b32d-a68797f9725b/18-designing-better-links-websites-emails.png" width="800" height="463" sizes="100vw" caption="Link-crowded texts overwhelm the audience with too many options. Moreover, it’s challenging to formulate links when as part of a sentence. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/aa6f8d74-74d0-4880-b32d-a68797f9725b/18-designing-better-links-websites-emails.png'>Large preview</a>)" alt="An example of a link-crowded text shown on the left and another one with concise list of links on the right" >}}

Grouping the links helps a lot, but if the goal is to trigger action, the primary link should stand out. So, why not make it a button, then?

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/437aca96-5861-4bf4-b4db-42d64da6f4d0/11-designing-better-links-websites-emails.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/437aca96-5861-4bf4-b4db-42d64da6f4d0/11-designing-better-links-websites-emails.png" width="800" height="463" sizes="100vw" caption="The more eye-catching a link is, the more it encourages clicking/tapping on it. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/437aca96-5861-4bf4-b4db-42d64da6f4d0/11-designing-better-links-websites-emails.png'>Large preview</a>)" alt="The same example as above but now one of the phrases “Get free tickets” is presented as a blue button and is therefore attracting more attention" >}}

In the previous sections, we figured out how **descriptive links increase usability and accessibility**. At the same time, such links are longer, and consequently, can appear divided in a paragraph, when the first part of a link remains at the end of the previous line, and the second part jumps to the next line. It seems trivial compared to bigger flaws, but distorted links are a bit annoying in link-crowded texts.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d83fc39f-6eb7-48c3-b6ce-4dc0f5e2b289/13-designing-better-links-websites-emails.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d83fc39f-6eb7-48c3-b6ce-4dc0f5e2b289/13-designing-better-links-websites-emails.png" width="800" height="463" sizes="100vw" caption="Split links are a bit harder to perceive than the ones that fit into corresponding lines. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d83fc39f-6eb7-48c3-b6ce-4dc0f5e2b289/13-designing-better-links-websites-emails.png'>Large preview</a>)" alt="A comparison of the split links to the links which fit into corresponding lines of the text" >}}

If a paragraph width is fixed, compose text the way all links fit into lines, for example, try to start a paragraph with a link. However, **browsers and devices render content differently**, and links will still shift for some users. That’s why lists are a safer option for a set of links.

{{% ad-panel-leaderboard %}}

## Link Accessibility

Accessible links are not only the ones that look tidy and clear; they should also be properly working. [Web Content Accessibility Guidelines](https://www.w3.org/TR/WCAG21/) (WCAG), the world’s most famous digital accessibility standard, includes recommendations about hyperlinks, including some non-visual features.

### Distinction

One of the WCAG requirements is [not to rely on color only](https://www.w3.org/TR/WCAG20-TECHS/F73.html) when you want to distinguish a button or link from the rest of the text. Painting links in blue or another color doesn’t suffice since it still might not be visible for people with <a href="https://www.smashingmagazine.com/2017/10/nailing-accessibility-design/">color blindness</a>. The most typical method is underlining links; they can also appear in bold font.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/95d09d8b-3630-45c0-a57c-23dcfb0280f2/12-designing-better-links-websites-emails.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/95d09d8b-3630-45c0-a57c-23dcfb0280f2/12-designing-better-links-websites-emails.png" width="800" height="463" sizes="100vw" caption="Links should differ from the rest of the text by at least one more characteristic, except the color. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/95d09d8b-3630-45c0-a57c-23dcfb0280f2/12-designing-better-links-websites-emails.png'>Large preview</a>)" alt="A comparison of three ways of using links that are distinguishable with color: links shown in blue text (left), underlining links shown in blue text (middle) and links shown in bold blue font (right)" >}}

### Color Contrast

Links are essential interactive elements and have to comply with contrast recommendations. WCAG has two levels of contrast compliance:

1. **AA**: medium, used by many websites for a mass audience;
2. **AAA**: high, primarily applied on governmental sites and by communities of people with disabilities.

For example, the AA level requires maintaining a contrast between a link and background of at least `4.5:1` for normal font size and `3:1` for large text.

**Note**: *You can always check your colors with the help of the online [Contrast Checker](https://webaim.org/resources/contrastchecker/) or Figma’s [Contrast plugin](https://www.figma.com/community/plugin/733159460536249875).*

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d06a68e0-8150-45dd-bf6b-7a3221f1c45a/1-designing-better-links-websites-emails.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d06a68e0-8150-45dd-bf6b-7a3221f1c45a/1-designing-better-links-websites-emails.png" width="800" height="463" sizes="100vw" caption="Measuring contrast by the eye doesn’t always work. For example, green should be darker and more saturated than blue to pass the requirement. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d06a68e0-8150-45dd-bf6b-7a3221f1c45a/1-designing-better-links-websites-emails.png'>Large preview</a>)" alt="A comparion of links with different color contrast recommendations according to WCAG’s two levels of contrast compliance" >}}

### Focus State

Like all interactive components, links should have a [visible keyboard focus](https://www.w3.org/WAI/WCAG21/Understanding/focus-visible.html). All popular browsers have an embedded accessible focus by default (you might have seen this bold blue frame around input fields, dropdowns, buttons, and links in Google Chrome). Unfortunately, on some sites, focus gets manually removed or visually customized so that **a focused link can look even less noticeable** (e.g. faded out).

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7399a3ea-5a0d-4219-9c3b-f9f831418f75/10-designing-better-links-websites-emails.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7399a3ea-5a0d-4219-9c3b-f9f831418f75/10-designing-better-links-websites-emails.png" width="800" height="463" sizes="100vw" caption="If you don’t have inspiration for creating a custom focus state, at least keep the standard one. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7399a3ea-5a0d-4219-9c3b-f9f831418f75/10-designing-better-links-websites-emails.png'>Large preview</a>)" alt="Unfocused (left), standard focus (middle) and custom focus (right) examples shown using underlined and colored links (blue)" >}}

### Optimization For Screen Readers

Blind users don’t see the web &mdash; they listen to it by means of “screen readers,” assistive programs that transform a written text into fast robotic speech. They navigate with a keyboard and remember dozens of handy shortcuts to jump between headings, buttons, or links instead of obediently listening to the entire content on a page.

So, when you remove wordiness for sighted people (for example, in the lists of different language versions or formats), it’s important to **keep links clear for screen reader users**, too. Otherwise, blind visitors will hear the following:

<blockquote>“Ukrainian &mdash; link, English &mdash; link, German &mdash; link”</blockquote>

The self-explanatory should be heard instead:

<blockquote>“Download project plan template in Ukrainian &mdash; link, download project plan template in English &mdash; link…”</blockquote>

And probably the most annoying thing on a news website is to hear this:

<blockquote>“Read more &mdash; link, read more &mdash; link, read more &mdash; link”</blockquote>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2496e8f3-4199-4796-b932-a028cb3b8d59/2-designing-better-links-websites-emails.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2496e8f3-4199-4796-b932-a028cb3b8d59/2-designing-better-links-websites-emails.png" width="800" height="463" sizes="100vw" caption="There are two main ways to put a link on a news page: make each title a link or add auxiliary phrases like ‘Read more…’. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2496e8f3-4199-4796-b932-a028cb3b8d59/2-designing-better-links-websites-emails.png'>Large preview</a>)" alt="An example of using “Read more” links on the left compared to a version with titles being used as links on the right" >}}

Sighted people can guess that “Read more…” relates to the nearest title, and blind people need individualized *read-mores*. Fortunately, the HTML attribute `aria-label` comes in handy here; it enables attaching explanatory text for screen reader users.

It’s often a designer’s responsibility to compose accessibility-related text and collaborate with a developer around optimal implementation, so here is a simplified code example:

<div class="break-out">

<pre><code class="language-html">&lt;h4&gt;News&lt;/h4&gt;
&lt;p&gt;Eleks Design Team will participate in the Space Hackathon.
&lt;a href="aerospace-hackathon.html" aria-label="Read more about Eleks participation in the Space Hackathon"&gt;Read more...&lt;/a&gt;
&lt;/p&gt;
&lt;p&gt;Projector Tech and Creative Institute launches five courses on web accessibility this year.
&lt;a href="new-courses.html" aria-label="Read more about new courses on accessibility by Projector Institute"&gt;Read more...&lt;/a&gt;
&lt;/p&gt;</code></pre>
</div>

As you can see, each “Read more” has an extended explanation for screen readers. However, you won’t need to take care of article links with `aria-label` if each title is a link itself.

<div class="break-out">

<pre><code class="language-html">&lt;h4&gt;News&lt;/h4&gt;
&lt;h5&gt;&lt;a href="aerospace-hackathon.html"&gt;Eleks Design Team will participate in the Space Hackathon&lt;/a&gt;
&lt;/h5&gt;
&lt;h5&gt;&lt;a href="new-courses.html"&gt;Projector Tech and Creative Institute launches five courses on web accessibility this year&lt;/a&gt;
&lt;/h5&gt;</code></pre>
</div>

{{% ad-panel-leaderboard %}}

### Duplicated links

Multiple identical links are yet another widespread controversial practice. For example, on a web page, it means that the same web address is attached to an article title, hero image, and intro sentence. At first glance, nothing’s wrong: wherever you click &mdash; you get to the article. But for blind users, it means **repeating the same information thrice**, which extends the time they need to sift through content to what they are interested in.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2f37044e-dddb-472f-aae3-40489ab512b9/7-designing-better-links-websites-emails.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2f37044e-dddb-472f-aae3-40489ab512b9/7-designing-better-links-websites-emails.png" width="800" height="463" sizes="100vw" caption="It’s better to make the whole block a link rather than create multiple links that guide to the same destination. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2f37044e-dddb-472f-aae3-40489ab512b9/7-designing-better-links-websites-emails.png'>Large preview</a>)" alt="Left: An example of multiple identical links to the same link which covers the whole block. Right, the same link shown once." >}}

**An important note:** We are now talking about identical destinations, but a card can include different ones, for instance, a link to the article, author’s profile, and tags. In this case, minor links can appear “wrapped” in the main one.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/512f0cbd-b917-42df-a740-2ef395d45ce4/19-designing-better-links-websites-emails.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/512f0cbd-b917-42df-a740-2ef395d45ce4/19-designing-better-links-websites-emails.png" width="800" height="463" sizes="100vw" caption="The click area of the primary link ‘wraps’ the auxiliary ones (author’s profile and tags). (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/512f0cbd-b917-42df-a740-2ef395d45ce4/19-designing-better-links-websites-emails.png'>Large preview</a>)" alt="An example of a primary link (left) and secondary links which are ‘wrapped’ in the main one (right)" >}}

Now, emails. Let’s say we have an invitation to some online event, where a Zoom link repeats several times. In the event description, “what/when/where” section, and closing part. Not only will it create an impression of mess for sighted users, but also **visually impaired users** will be troubled with jumping between duplicated links.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/97558efb-6c91-49bd-ba10-881b0f2a99e7/8-designing-better-links-websites-emails.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/97558efb-6c91-49bd-ba10-881b0f2a99e7/8-designing-better-links-websites-emails.png" width="800" height="463" sizes="100vw" caption="One prominent link speaks louder than a bunch of scattered ones. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/97558efb-6c91-49bd-ba10-881b0f2a99e7/8-designing-better-links-websites-emails.png'>Large preview</a>)" alt="A “naughty” example presented on the left with duplicated links provided in a text compared to a “better” example shown on the right showing one prominent link presented as a blue button" >}}

### Recommended Reading

In this article, I wanted to suggest options instead of showing the topic in black and white. There are multiple shades of good design, and you can find yours on the overlap of best practices and your particular case. Meanwhile, some additional reading on this topic:

- “[Using `aria-label` For Link Purpose](https://www.w3.org/WAI/WCAG21/Techniques/aria/ARIA8.html),” Web Content Accessibility Guidelines (WCAG)
- “[How To Make ‘Read More’ Links Accessible](https://www.visionaustralia.org/services/digital-access/blog/how-to-make-read-more-links-accessible),” Vision Australia
- “[Writing Hyperlinks: Salient, Descriptive, Start With Keyword](https://www.nngroup.com/articles/writing-links/),” Marieke McCloskey, Nielsen Norman Group

{{< signature "vf, yk, il" >}}
