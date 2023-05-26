---
title: '&lt;article&gt; vs. &lt;section&gt;: How To Choose The Right One'
slug: article-section-elements-accessibility
author: olushuyi-olutimilehin
image: >-
  https://res.cloudinary.com/indysigner/image/upload/v1658760043/article-section-elements-accessibility_x3326s.jpg
date: 2022-07-25T14:30:00.000Z
summary: >-
  In this article, Olushuyi explores a mental model that helps you decide between the `<article>` and `<section>` elements when writing documents. You will explore how grouping content affects accessibility and how you can make it all count for users.
description: >-
  In this article, Olushuyi explores a mental model that helps you decide between the `<article>` and `<section>` elements when writing documents. You will explore how grouping content affects accessibility and how you can make it all count for users.
categories:
  - Accessibility
  - HTML
  - Semantics
---

“Do I use a `<section>` or an `<article>` element?” I have had to ask myself this question an unhealthy amount of times whenever I have to group content in a container element.

A [conversation I had on Twitter](https://twitter.com/ShuyiOlutimi/status/1455244970345082884?s=20&t=msdrhIBdSXGiEkc2pg0mOA) led me to research this question and ultimately to write on it. It was a conversation with [Grace Snow](https://www.gracesnowdesign.co.uk/) where I shared an approach to writing HTML that I love to use. I love to write out my HTML structure (boxes) first and with no content to ensure I am not thinking of styling while I write my HTML. She then spotted that I might be making problematic use of the `section` and `article` elements in my sincere attempt to be semantic.

It turns out that to choose between `section` and `article`, we need our content. In fact, to determine if our content is narrowed down enough to those two, we need our content.

We can build a mental model that ensures we make the best decision every time by taking our content into consideration.

Let’s take a deep dive in!

## Document Semantics

HTML passes two related but distinct information to user devices. The first is the visual presentation information, which tells the device how to display the document by default.

The second is known as semantic information or, simply, [semantics](https://html.spec.whatwg.org/multipage/dom.html#semantics-2). It conveys *“meanings”* in the document, i.e., each element’s purpose and the relationship between them. In this sense, the spec would say that an element [“represents”](https://html.spec.whatwg.org/#represents) something. So, when you see *“represents”* in the spec, what follows is the semantic information embedded in the element.

The `h1` element reveals the presence of these two sets of information. [The visual presentation information for the `h1` element](https://www.w3schools.com/cssref/css_default_values.asp), when encountered by browsers, is why it appears bold and with a larger font size than the rest of the document. [The semantic information that the `h1` represents](https://html.spec.whatwg.org/#the-h1,-h2,-h3,-h4,-h5,-and-h6-elements) is that it is the highest rank heading for its section.

Sighted users can gleam the semantic meaning from devices like the browser by observing the visuals. For headings, we can differentiate based on differences in font size and weight, or in the case of lists, the presence of bullet point markers or numbered markers. For users who do not rely on sight, the semantics are only accessible through options or devices that allow them to request that the semantic information be announced in other ways that may not be visual. These options and devices are generally called [assistive technology](https://w3c.github.io/aria/#dfn-assistive-technologies).

HTML prescribes some elements that convey implicit meaning to browsers which browsers can extract to the [accessibility API](https://www.smashingmagazine.com/2015/03/web-accessibility-with-accessibility-api/#accessibility-apis), making it available to assistive technologies that, in turn, interpret this meaning to users. This meaning gives users a wholesome sense of the webpage they are visiting, such as document structure and navigation assistance, or in this instant case, both document structure and navigation assistance. 

However, it is not only elements that directly wrap text content that carries semantic information. Elements meant for grouping other elements also carry some meaning; in some cases, it may be meaning we want to communicate.

## Does My Grouping Play A Semantic Role?

This first step in our mental model is to question if grouping the content as we are about to do is *necessary* for the document structure to make sense. Broken down, I would ask myself in this kind of manner:

- Is there any possibility the content of this block shares something in common that adds some sense to my document structure overall when it is read together?
- If I were to describe my document structure to a person without showing it to them, would I mention that there is that particular grouped area for them to appreciate the document structure?

If the answer to these questions is “no,” then you may have a situation where a [`<div>` could be appropriate](https://www.scottohara.me/blog/2022/01/20/divisive.html), as [Scott O’Hara](https://www.scottohara.me) notes. Reading Scott’s article could help you further examine the role your grouping plays and even formulate a better set of questions than mine. I do not intend to cover the `<div>` element in this article as Scott sufficiently covers it. I only intend to state that first, you must confirm that the grouping you are making is influenced by document structure. If it is, you can proceed to interrogate further to determine if it is an `<article>` or `<section>`.

To be clear, I do not mean that the grouping must *only* be influenced by document structure for you to start to consider `<article>` or `<section>`. It is enough that it is one of the possible reasons. For instance, it is possible for content in your grouping to share a distinct design or language and, at the same time, influence the document semantics.

{{% feature-panel %}}

## What Semantic Role Does My Grouping Play?

We have now decided that the grouped content serves some function in describing the document. The next step is to determine which of the semantic meaning already carried by the `article` or the `section` element most accurately describes what function your grouped content is intended to serve in the document structure.

### What The HTML Spec Say

Let us take a look at the primary source of authority on HTML and start to form our understanding of the `section` and `article` elements and their inherent semantic meaning.

[The HTML Living Standard says of the `article` element](https://html.spec.whatwg.org/#the-article-element):

<blockquote>The <a href="https://html.spec.whatwg.org/#the-article-element"><code>article</code></a> element <a href="https://html.spec.whatwg.org/#represents">represents</a> a complete, or self-contained, composition in a document, page, application, or site and that is, in principle, independently distributable or reusable, e.g., in syndication. This could be a forum post, a magazine or newspaper article, a blog entry, a user-submitted comment, an interactive widget or gadget, or any other independent content item.</blockquote>

As relates to the `section` element, [the HTML Living Standard defines it this way](https://html.spec.whatwg.org/#the-section-element):

<blockquote>The <a href="https://html.spec.whatwg.org/#the-section-element"><code>section</code></a> element <a href="https://html.spec.whatwg.org/#represents">represents</a> a generic section of a document or application. A section, in this context, is a thematic grouping of content, typically with a heading...<br /><br />Examples of sections would be chapters, the various tabbed pages in a tabbed dialog box, or the numbered sections of a thesis. A website’s home page could be split into sections for an introduction, news items, and contact information.</blockquote>

To help narrow it further, the specs offer [this clue on when to use the `section` element](https://html.spec.whatwg.org/multipage/sections.html#the-section-element):

<blockquote>...A general rule is that the <a href="https://html.spec.whatwg.org/multipage/sections.html#the-section-element"><code>section</code></a> element is appropriate only if the element’s contents would be listed explicitly in the document’s <a href="https://html.spec.whatwg.org/multipage/sections.html#outline">outline</a>.</blockquote>

The linked specs give quite elaborate examples. However, it is safe to say that the choice is seemingly heavily subjective. Authors must actively decide if the particular group they have come up with is “complete” and “independently distributable,” in which case the choice would be an `article` or if it is a “thematic grouping of content,” in which case the choice would be a `section`. Let’s consider some tasks.

If you were to build a blog like *Smashing Magazine*, which of these elements would you use to wrap the portion of the landing page that contains the list of all blog posts teasers? In that wrapped portion, what element would wrap each blog post teaser? If you click on one of the blog post teasers and land on the expanded post page, which elements would wrap up the blog article?

If you were to build Twitter, would you wrap each tweet fed into the users’ timeline in an `article` because they are “self-contained” and “in principle, independently distributable”? Or would you wrap them in a `section` because they are “a generic section of an application”? Or perhaps, in this case, a `div` is semantically appropriate? Still taking the Twitter example, is your timeline container a `section` of the whole Twitter application, or is your timeline an `article` within your Twitter application? Or perhaps everything is just *cake*, and nothing is real.

We will return to apply our mental model to these two scenarios.

### Understanding What The Specs Mean

I reckon the reason for the seeming confusion is the mental model we have. At least that was the case for me.

The `article` element was not so-named after a written article. I wrongly assumed that it was, and perhaps you might have too. I literally just learnt that an `article` element existed and assumed that blog articles are so important on the web that the WHATWG decided to make an element dedicated to wrapping blog posts like this one. It felt intuitive to me, but I was wrong. I guess that is why web standards exist. Intuitions are not always uniform.

It turns out that in the Oxford English Dictionary and other dictionaries, one of the definitions for the word article is “a particular item or separate thing.” This is the sense in which the specs use the `article` element. It is right there in the spec’s definition of the `article` element, but as I said, that is not how I generally use the word “article.” In fact, dictionaries give the first definition of an “article” as a written work. 

So, while the spec clearly says what sense it is used in, we still do not think of it that way.

To make it more adjust our thoughts, [Bruce Lawson gives the best anecdote to understand the article element](https://www.smashingmagazine.com/2020/01/html5-article-section/):

<blockquote>I gave my usual answer: think of <code>&lt;article&gt;</code> not just as a newspaper article or a blog post, but as an article of clothing &mdash; a discrete entity that can be reused in another context. So your trousers are an article, and you can wear them with a different outfit; your shirt is an article and can be worn with different trousers; your knee-length patent leather stiletto boots are an article (you wouldn’t wear just one of them, would you?).</blockquote>

It means what an `article` *represents* is content that can be taken out of the document and away from the immediate surrounding content, dropped somewhere else, say on another page, and still make total sense as it is grouped.

In the same way that you could use an article, such as a table lamp (an independent content group), to improve the aesthetics of your living room, and it would complement your sofa, tv console, curtains, and so on (immediate surrounding content). Yet, if you were to take your table lamp into your room, and it was simply placed at your bedside or your workstation, it would still be identifiable as a complete lamp.

The `section` element, on the other hand, *represents* “a thematic grouping of content,” meaning that a `section` is a part of a larger group without which it may not necessarily stand to make complete sense alone. It may stand alone, but in the theme of your content overall, it is less likely to be standalone. As the spec put it, “Examples of sections would be chapters, the various tabbed pages in a tabbed dialog box, or the numbered sections of a thesis. A website’s home page could be split into sections for an introduction, news items, and contact information.”

This is why a `section` would usually have a heading, providing a sort of call back to what part of the larger document the section relates to.

Let us go back to our lamp analogy. Our lamp itself makes sense as an item, but in reality, it has different parts that could technically be separated but really should not. I could take off the umbrella-shaped hood of my lamp, take the light bulb out, take off the base, and take off the upright stand. Together, they make up a lamp but, taken apart, not quite. If you are presented with the umbrella-shaped hood of a lamp, you are likely to think, “What is this from? Where is the rest of it?” If you are presented with the light bulb, you are likely to think, “Where does this go?”

{{% ad-panel-leaderboard %}}

## Let’s Group Some Content

### A Blog Website Landing Page

Firstly, let us take the example of a blog website. Our blog is the *Smashing Magazine*. Let us take a look at our landing page.

Here are the major areas on our landing page:

- Header with Site navigation,
- Main Area,
- Footer with Topic Navigation.

<pre><code class="language-html">&lt;header&gt;
	&lt;nav&gt;
		&lt;!-- 	Website navigation goes here --&gt;
	&lt;/nav&gt;
&lt;/header&gt;

&lt;main&gt;
	&lt;!-- 	We would group the content that should go here	 --&gt;
&lt;/main&gt;

&lt;footer&gt;
	&lt;nav&gt;
		&lt;!-- Topic navigation goes here	 --&gt;
	&lt;/nav&gt;
&lt;/footer&gt;</code></pre>

These are groups that already have elements to represent them. So, we are not deciding between `section` and `article` for these. 

In our Main Content, these are the identifiable groups:

- Selected Articles,
- Newsletter Subscription,
- Components and Guides,
- Latest Posts,
- Smashing products and offerings,
- Smashing conferences,
- External articles from community members.

What element should wrap these grouped content? Let us apply our mental model. For each of these content groups, we follow this mental model.

- Does grouping this content play a role that may help explain my document structure?
    - If it does not, then I can use a `div`.
    - If it does, play a role and proceed to consider if the role matches a `section` or an `article`.
- What role does it play in my document structure?
    - Is the content of this group thematically related such that it helps to understand the outline of my document? If it is, then it is possibly a `section`. 
    - Is the content of this group one that contains content that I can take out and redistribute to other pages while it does not totally tie to my document theme and outline? If it is, then it is possibly an `article`.

I encourage you to grab a piece of paper and make your grouping before proceeding to see mine. This way, we can compare how we think of each content group’s role on our page.

Now let’s build the skeletal grouping for our Smashing Magazine:

- **Selected Articles**  
Does it play a role in my document structure? Yes. What role? It is a part of the outline of content on my landing page. Verdict: `section`.
- **Newsletter Subscription**  
Does it play a role in my document structure? Hmm. Well, it is not exactly necessarily within the central theme of my landing page, so I am doubtful about this one. I’d just say “no.” Verdict: `div`. 
- **Components and Guides**  
Does it play a role in my document structure? Yes. What role? It is a part of the outline of content on my landing page. Verdict: `section`.
- **Latest Posts**  
Does it play a role in my document structure? Yes. What role? It is a part of the outline of content on my landing page. Verdict: `section`.
- **Smashing products and offerings**  
Does it play a role in my document structure? Yes. What role? It is a part of the outline of content on my landing page. Verdict: `section`.
- **Smashing conferences**  
Does it play a role in my document structure? Yes. What role? It is a part of the outline of content on my landing page. Verdict: `section`.
- **External articles from community members**  
Does it play a role in my document structure? Yes. What role? It is a part of the outline of content on my landing page. Verdict: `section`.

Here is what my *Smashing Magazine* landing page looks like now: 

<pre><code class="language-html">&lt;header&gt;
	&lt;nav&gt;
		&lt;!-- 	Website navigation	 --&gt;
	&lt;/nav&gt;
&lt;/header&gt;

&lt;main&gt;
	&lt;section&gt;
		&lt;!-- 	Selected articles	 --&gt;
	&lt;/section&gt;
	
	&lt;div&gt;
		&lt;!-- 	Newsletter subscription	 --&gt;
	&lt;/div&gt;
	
	&lt;section&gt;
		&lt;!--  Components and guides	--&gt;
	&lt;/section&gt;
	
	&lt;section&gt;
		&lt;!-- 	Latest posts --&gt;
	&lt;/section&gt;
	
	&lt;section&gt;
		&lt;!-- 	Smashing products and offerings --&gt;
	&lt;/section&gt;
	
	&lt;section&gt;
		&lt;!-- 	Smashing conferences	 --&gt;
	&lt;/section&gt;
	
	&lt;section&gt;
		&lt;!-- 	External articles from community members	 --&gt;
	&lt;/section&gt;
&lt;/main&gt;

&lt;footer&gt;
	&lt;nav&gt;
		&lt;!-- Topic navigation	 --&gt;
	&lt;/nav&gt;
&lt;/footer&gt;</code></pre>

We all might adjudge the role some items play differently. The “Newsletter Subscription” area, for instance. I would not outline “Newsletter Subscription” in my document outline, nor would I care to encounter it on a document outline for a page I visit. Yet again, if it were Substack, a platform for newsletters, I would definitely see how an area to subscribe to the newsletter would be a `section`. And while I have used a `div` here, it could as well have been an `aside`, but, of course, that is not why we are here today. The point is how we adjudge our content guides our decision.

I guess my point is your decision would be marginally better provided you interrogate and justify the role you want your content group to play in each case. You would have consciously put effort into making your web content understandable for users and other developers that would encounter your technical debt.

### An Article Post On A Blog Website

So, we have clicked on one blog article from the “Selected Articles” area and have expanded that article to its own page. This specific blog article you are reading, how is it grouped? Again, here is our base template:

<pre><code class="language-html">&lt;header&gt;
	&lt;nav&gt;
		&lt;!-- 	Website navigation	 --&gt;
	&lt;/nav&gt;
&lt;/header&gt;

&lt;main&gt;
	&lt;!-- This article is wrapped here --&gt;
&lt;/main&gt;

&lt;footer&gt;
	&lt;nav&gt;
		&lt;!-- Topic navigation	 --&gt;
	&lt;/nav&gt;
&lt;/footer&gt;</code></pre>

Do you wrap it in an `article`, do you wrap it in a `section`, or perhaps a `div`? 

Would you break this article itself into smaller grouped bits? Maybe a bunch of `section`s or a couple of `article`s? Are there redistributable parts of this article or parts that you would expose to the document outline?

I would refrain from saying what I arrived at, but I would love to know what you would use. Take a note of your answers as we shall revisit this later on.

### A Web Application: Twitter

So, we have one more exercise, a web application, specifically Twitter. 

- Is the timeline container a `section` of the whole Twitter application, or is your timeline an `article` within your Twitter application, or is it a `div`?
- Would you wrap each tweet fed into the users’ timeline in an `article` because they are “self-contained” and “in principle, independently distributable”? Or would you wrap them in a `section` because they are “a generic section of an application”? Or perhaps, in this case, a `div` is semantically appropriate?

If I apply the mental model, below is the way how I would do it:

My timeline is a part of my document outline, and yet, to an extent, it can be independently distributed. I could take my timeline out, and it would stand well alone. It seems like it could be viable for a `section` or an `article`. So, I question further, what do I really intend? Do I want it to function for redistribution or as a part of my application? If you use Twitter, you would agree that your timeline is more of an integral part of your homepage than it is redistributable. Here I would settle for a `section`.

For each tweet in my timeline, it would be an `article`. This is because each tweet is not thematically connected to the next tweet on my timeline such that I could say it can be a part of an outline. So, tweets are not `section`s. They are “self-contained” and “in principle, independently distributable.” You can even click a tweet to enter a new world with comments and quote tweets, and so much more.

Truly, and indeed, if you walk your way through the div-soup of the Twitter page, nested in, there is a nice pretty `section` just sitting there, as it should be. This `section` holds your timeline. And if you proceed deeper into the `section`, and further down a serving of `div`s, you can pick up an `article` holding each tweet. This is where I confess that I let out a tiny scream when I discovered that my thoughts matched what Twitter did.

This inspection of Twitter also shows how the presence of `div`s does not mean that semantic meaning has been sacrificed or lost.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/207b79a9-1836-460a-a070-367023e3e90d/twitter-timeline-is-a-section.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/207b79a9-1836-460a-a070-367023e3e90d/twitter-timeline-is-a-section.jpg" width="800" height="549" sizes="100vw" caption="Nestled in between all the <code>div</code>s, the Twitter timeline is really wrapped in a <code>section</code> element. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/207b79a9-1836-460a-a070-367023e3e90d/twitter-timeline-is-a-section.jpg'>Large preview</a>)" alt="A screenshot of Twitter timeline with the code below" >}}

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2efa8fe0-49c8-4a1e-8ce1-bbdbe8d465ec/each-tweet-is-an-article.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2efa8fe0-49c8-4a1e-8ce1-bbdbe8d465ec/each-tweet-is-an-article.jpg" width="800" height="552" sizes="100vw" caption="Nested further in the <code>section</code> that holds your timeline, each tweet is really wrapped in an <code>article</code> element. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2efa8fe0-49c8-4a1e-8ce1-bbdbe8d465ec/each-tweet-is-an-article.jpg'>Large preview</a>)" alt="A screenshot with one highlited tweet and the code below" >}}

### Nesting `section`s And `article`s And Other Groups

You can nest these elements within each other. You probably already figured that by now after looking at the Twitter example.

`div`s, `article`s, and `section`s can go into each other without necessarily breaking accessibility. If you apply the mental model, you can question each nesting you are about to make and group accordingly.

Take the example of this blog post. I did not answer how I would wrap it when I asked a few paragraphs ago. Here is what I could do:

I could wrap this whole article you are reading in an `article`. Then I would further nest the large chunks of this article into `section`s because I want each portion to be really divided up for easy understanding. So far, this is what this blog post you are reading could look like:

<div class="break-out">

<pre><code class="language-html">&lt;header&gt;
	&lt;nav&gt;
		&lt;!-- 	Website navigation	 --&gt;
	&lt;/nav&gt;
&lt;/header&gt;

&lt;main&gt;
	&lt;article&gt;
		&lt;h1&gt;Article versus section: Making your choice count in the larger context of accessibility&lt;/h1&gt;

		&lt;section&gt;
			&lt;h2&gt;Quick summary&lt;/h2&gt;
			&lt;!--  paragraphs go here	--&gt;
		&lt;/section&gt;

		&lt;section&gt;
			&lt;h2&gt;Introduction&lt;/h2&gt;
			&lt;!--  paragraphs go here	--&gt;
		&lt;/section&gt;

		&lt;section&gt;
			&lt;h2&gt;Document Semantics&lt;/h2&gt;
			&lt;!--  paragraphs go here	--&gt;
		&lt;/section&gt;

		&lt;section&gt;
			&lt;h2&gt;Does my grouping play a semantic role?&lt;/h2&gt;
			&lt;!--  paragraphs go here	--&gt;
		&lt;/section&gt;

		&lt;section&gt;
			&lt;h2&gt;What semantic role does my grouping play?&lt;/h2&gt;
			&lt;!--  paragraphs go here	--&gt;
			&lt;h3&gt;What the HTML specs say&lt;/h3&gt;
			&lt;!--  paragraphs go here	--&gt;
			&lt;h3&gt;Understanding what the specs mean&lt;/h3&gt;
			&lt;!--  paragraphs go here	--&gt;
		&lt;/section&gt;

		&lt;section&gt;
			&lt;h2&gt;Let's group some content&lt;/h2&gt;
			&lt;!--  paragraphs go here	--&gt;
			&lt;h3&gt;A bog website landing page&lt;/h3&gt;
			&lt;!--  paragraphs go here	--&gt;
			&lt;h3&gt;An article post on a blog website&lt;/h3&gt;
			&lt;!--  paragraphs go here	--&gt;
			&lt;h3&gt;A web application: Twitter&lt;/h3&gt;
			&lt;!--  paragraphs go here	--&gt;
		&lt;/section&gt;

		&lt;section&gt;
			&lt;h2&gt;Nesting sections AND articles&lt;/h2&gt;
			&lt;!--  paragraphs go here	--&gt;
		&lt;/section&gt;

		&lt;!-- 	Rest of article continues here	 --&gt;
	&lt;/article&gt;
&lt;/main&gt;

&lt;footer&gt;
	&lt;nav&gt;
		&lt;!-- Topic navigation	 --&gt;
	&lt;/nav&gt;
&lt;/footer&gt;
</code></pre>
</div>

Notice how I give my `section`s appropriate headings since I have decided to use `section`? Recollect that the spec says a `section` should typically have a heading. Also, recall that you make `section`s if you think they should feature in your document outline. As such, a heading would provide the text to feature in the outline.

If there is a need for it, your `section`s and `article`s could have other grouped content in them. For instance, you could have [a `header` to hold your section’s heading](https://html.spec.whatwg.org/#the-header-element) or [a `footer` to hold information about a section](https://html.spec.whatwg.org/#the-footer-element), such as links to related documents, etc. If you will, the “Further reading” area of this post could be wrapped in a `footer`.

As for `main`, you are restricted to using it only when it is [hierarchically correct](https://html.spec.whatwg.org/multipage/grouping-content.html#hierarchically-correct-main-element), i.e., if it is a direct child of `html`, `body`, `div` or `form`. In any case, you are [restricted from using more than one `main` element without the `hidden` attribute](https://html.spec.whatwg.org/multipage/grouping-content.html#the-main-element).

{{% ad-panel-leaderboard %}}

## How `section` And `article` Are Exposed

So far, we have looked at how to group content but only from the viewpoint of developers. How is how our grouping exposed to readers?

### `section` And `article` In Browsers

Browsers generate an *Accessibility Tree* which you can inspect with the developer tools. You can open the developer tools, activate the *Inspector*, and navigate to the *Accessibility* tab.

Firefox, Chrome, and Microsoft Edge similarly present the respective `role`s of the `article` and `section` elements on the Accessibility Tree. The `article` element has the `role` of “article” on the accessibility tree. The `section` element has the `role` of the “section.” This means that the browsers accurately recognise what our grouping of content *represents*.

However, while the browsers correctly understand what our grouping of content *represents,* users do not get any particular hints about this. So `article`s and `section`s are not perceivable or otherwise navigable by the keyboard on the browser. If the page is styled, then visual cues provided by your design could hint at the grouping of content. But there is no default underlining or outline on focus as you’d get with links.

**Note:** I should briefly note that we ([Manuel](https://twitter.com/mmatuzo) and I) got a little tripped up on browsers exposing the `section` element as having a role of “section” because, in aria accessibility definitions, the aria `role` of section is not the same as the HTML `section` element. [The aria role of “section”](https://www.w3.org/TR/wai-aria-1.2/#section) is an [abstract role and should not be used by authors/developers](https://www.w3.org/TR/wai-aria-1.2/#isAbstract). So please do not set a `role="section"` attribute in your HTML. Anyway, it would seem that the browsers may be using their own internal accessibility terms. This conclusion is especially supported by the fact that in Firefox, for instance, images have the role of “graphic,” but aria does not have any role known as a graphic. Perhaps someone more knowledgeable would definitely be able to explain what is happening. However, the expected behavior is correct.

### `section` And `article` In Screen Readers

Screen readers read the accessibility API and then handle the elements correctly. There are a couple of screen readers in use. Thankfully, [AccessibilityOZ documents how sectioning elements are handled by screen readers](https://www.accessibilityoz.com/2020/02/html5-sectioning-elements-and-screen-readers/), which still seems accurate at the time of writing this article. 

### `article` In Screen Readers

Where grouped content is wrapped in an `article`, different screen readers handle it differently.

In terms of being perceivable, AccessibilityOz documents that JAWS, Talkback on Android, and VoiceOver announce the entry into and exit from an “article” if it encounters it. NVDA and Narrator do not announce an `article`. 

I specifically was able to test on NVDA and Narrator as I use a Windows laptop, and the `article` was not announced. [Manuel](https://twitter.com/mmatuzo) was also kind enough to help test on VoiceOver and Talkback, and the `article` is announced if it is encountered as you traverse the page.

I snooped around and found that NVDA allows you to turn on the option to announce the presence of an `article`. It is just turned off by default. I am not certain how frequently non-developer users would customise that option.

Regarding navigation, users on Narrator cannot jump to an `article` as it is not perceivable. Users on NVDA that have activated the option to have `article`s announced cannot jump to an `article`. There is no shortcut for that. It is only announced if encountered while traversing the page. JAWS has a dedicated shortcut for moving through `article`s on a page by pressing the <kbd>O</kbd> key. VoiceOver users can jump across `article`s using the shortcut (VO + <kbd>Shift</kbd> + left/right arrow).

While some users would get the presence of an `article` announced, others would not. So, the experience is not uniform. I have also wondered if there is any practical use for announcing an `article`. I am not sure when I heard the announcement that I am “in the article” on a webpage, I would interpret it as “in an independent, redistributable and self-contained content.” It sounds more like I am in a “written body of work.” I do not have the capacity to test this anyway, so it really is just my own thought.

The question, then, is what direct benefits do users of my page get from grouping content semantically within an `article`? What does it translate to for my users after I have correctly wrapped my group in an `article`? If there is none, why should I not just use the `div` instead? Bruce Lawson’s article, “[Why You Should Choose HTML5 `article` Over `section`](https://www.smashingmagazine.com/2020/01/html5-article-section/)” adequately covers that. Reader for Apple’s WatchOS looks out for `article` elements to appropriately determine what to display on the iWatch. While this is not a use case particularly prescribed by the web standards, perhaps we might see a trend of device makers taking this approach. So if you are designing your page with WatchOS in mind, this would be an additional reason to use `article`, at least over a `div`.

But I still wondered if there are any additional reasons directly for the benefit of users. Why would I want to jump through all `article`s on a webpage? Why jump through independent items on a webpage without context in the manner that JAWS and Voiceover allow? So I did some digging, and here is what I found about [the prescribed functionality for article role by assistive technology](https://www.w3.org/TR/wai-aria-1.1/#article):

<blockquote>An article may be nested to form a discussion where assistive technologies could pay attention to article nesting to assist the user in following the discussion…<br /><br />…When nesting articles, the child articles represent content that is related to the content of the parent article. For instance, a weblog entry on a site that accepts user-submitted comments could represent the comments as articles nested within the article for the weblog entry.<br /><br />…When the user navigates to an element assigned the role of <code>article</code>, <a href="https://www.w3.org/TR/wai-aria-1.1/#dfn-assistive-technology">assistive technologies</a> that typically intercept standard keyboard events <strong>should</strong> switch to document browsing mode, as opposed to passing keyboard events through to the web application. Assistive technologies <strong>may</strong> provide a feature allowing the user to navigate the hierarchy of any nested <code>article</code> elements.</blockquote>

I was sadly unable to reproduce this behavior directly. Jumping through `article`s on VoiceOver with the shortcut merely announces “article, article, article.” It does not seem they implemented the feature to allow users to navigate the hierarchy of nested articles, or I could not get it to work.

However, it doesn’t hurt to build with nested `article`s if it is the appropriate thing to do. If screen reader makers implement this recommended behavior, your page is already prime and ready for it. Consider it some sort of future-proofing.

### `section` In Screen Readers

Where grouped content is wrapped in a `section`, screen readers treat it more consistently.

In terms of being perceivable, all screen readers do not announce entry into or exit from a `section`. This also means in terms of navigation, there is no way to navigate from one `section` to another.

### Extending `section` Into Navigable `region`

The imperceivable nature of `section` is only a default behavior. As such, we can customize our `section` and expose it to screen readers users using [WAI-ARIA (Web Accessibility Initiative &mdash; Accessible Rich Internet Applications)](https://developer.mozilla.org/en-US/docs/Learn/Accessibility/WAI-ARIA_basics#enter_wai-aria).

Here is a summary of what WAI-ARIA is and what it does [culled from the MDN Docs](https://developer.mozilla.org/en-US/docs/Learn/Accessibility/WAI-ARIA_basics#enter_wai-aria):

<blockquote><a href="https://www.w3.org/TR/wai-aria-1.1/">WAI-ARIA</a> (Web Accessibility Initiative &mdash; Accessible Rich Internet Applications) is a specification written by the W3C, defining a set of additional HTML attributes that can be applied to elements to provide additional semantics and improve accessibility wherever it is lacking...</blockquote> 

Implying that while you may already be writing semantic HTML, you can customise and provide even greater semantic meaning!

In this specific case, we are more concerned with the category of [landmark roles](https://www.w3.org/TR/wai-aria-1.1/#landmark_roles) provided by ARIA, which are roles that provide navigational context for the application or the document. To understand better, the [definition of landmark provided by WAI-ARIA](https://www.w3.org/TR/wai-aria-1.1/#dfn-landmark) reads:

<blockquote>A type of region on a page to which the user may want quick access. Content in such a region is different from that of other regions on the page and relevant to a specific user purpose, such as navigating, searching, perusing the primary content, etc.</blockquote>

With landmark `role`s, we can provide non-sighted users with a key experience that sighted (and fully non-disabled) users of our page would have: the ability to first [scan or skim through a page](https://www.nngroup.com/articles/f-shaped-pattern-reading-web-content/) and then decide where to focus their attention. 

For the specific case of `section` and the intended semantic, we intend to pass to users; namely that the content in it is thematically related or has a central idea, the particular `role` of `region` is our concern.

As a landmark role, [a `region` is intended by the w3c](https://www.w3.org/TR/wai-aria-1.1/#region) to be:

<blockquote>A perceivable <a href="https://www.w3.org/TR/wai-aria-1.1/#section"><code>section</code></a> containing content that is relevant to a specific, author-specified purpose and sufficiently important that users will likely want to be able to navigate to the section easily and to have it listed in a summary of the page.</blockquote>

We can make specific `section`s of our page into `region`s calculated to make it easier for screen reader users to jump to that part of the page. This could be especially useful on pages populated with a lot of content other than the primary reason users might be on the page.

To create a `region`, there are two things to do. Firstly, make your element a region by including the attribute-value pairing `role="region"` in your element’s opening tag. Secondly, you give your region an accessible name. However, where your grouping element is a `section`, you only have to do the second. This is because [if your `section` element has an accessible name, then it has an implicit role as a `region`](https://www.w3.org/TR/html-aria/#docconformance). As such, it is not recommended to set a role that matches the implied semantics for the element. So let’s set an accessible name.

An [accessible name](https://www.w3.org/TR/wai-aria-1.1/#dfn-accessible-name) is simply the name of a user interface element, especially as exposed by the accessibility API to assistive technologies.

[The specification for the `region` role](https://www.w3.org/TR/wai-aria-1.1/#region) requires that:

<blockquote>Authors <strong>must</strong> give each element with a region role a brief label that describes the purpose of the content in the region.</blockquote>

[An accessible name is **required** for the `region` role](https://www.w3.org/TR/wai-aria-practices-1.1/#naming_role_guidance). If there is no accessible name, then browsers and assistive technologies **must not** expose a region to users because users will be jumping to a region with no description or context, almost like what happens with an `article`.

There are multiple ways to provide a name depending on the element involved. However, we shall narrow it down to what is relevant for a `section` being used as a `region`.

The first and most preferred way to name your region is to [name via the `aria-labelledby` attribute](https://www.w3.org/TR/wai-aria-practices-1.1/#naming_with_aria-labelledby). To do this, you [reference a visible element on your page](https://www.w3.org/TR/wai-aria-practices-1.1/#naming_rule_visible_text) and direct the assistive technology to use the text content of that visible element as the name of the region. This visible element should preferably be a heading.

To do this, give the element whose content you are referencing an `id` attribute with a value of choice. Then give your `section` element an `aria-labelledby` attribute. Then set the value of the `aria-labelledby` attribute to the exact value as the `id` of the element whose content you are referencing. Take a look at this in action:

<div class="break-out">

<pre><code class="language-html">&lt;section aria-labelledby="posts"&gt;
&lt;!-- This area contains teasers for all blog posts on the website  --&gt;
	&lt;h2 id="posts"&gt;All blog posts&lt;/h2&gt;
	&lt;article&gt;
		&lt;header&gt;
			&lt;p&gt;Cosima Mielke wrote&lt;/p&gt;
				&lt;h2&gt;Expand Your Horizons (June 2022 Desktop Wallpapers Edition)&lt;/h2&gt;
		&lt;/header&gt;
		&lt;div&gt;
			&lt;p&gt;What could be a better way to welcome June than with some colorful inspiration? Well, we might have something for you: wallpapers created with love by artists and designers from across the globe.&lt;/p&gt;
			&lt;p&gt;&lt;a&gt;Continue reading ↬&lt;/a&gt;&lt;/p&gt;
		&lt;/div&gt;
&lt;/article&gt;
	&lt;!-- More blog post teasers here  --&gt;
&lt;/section&gt;</code></pre>
</div>

Take note that your `aria-labelledby` does not carry an `#`, unlike what obtains when linking to an `id` with an `href`. It is `aria-labelledby="posts"` not `aria-labelledby="#posts"`. Remember also that we do not set a `role=region` for a `section` element. It is already implied once you give an accessible name.

Using this code example, screen readers would have the region announced to them under the landmark navigation as such “all blog posts, region” or something similar.

The second way to give an accessible name is to use the `aria-label` attribute if there is no visible element with content that could accurately label your region. In this case, the value you give to the `aria-label` itself would be read as the name of the region.

<div class="break-out">

<pre><code class="language-html">&lt;section aria-label="all blog posts"&gt;
&lt;!-- This area contains teasers for all blog posts on the website  --&gt;
	&lt;article&gt;
		&lt;header&gt;
			&lt;p&gt;Cosima Mielke wrote&lt;/p&gt;
				&lt;h2&gt;Expand Your Horizons (June 2022 Desktop Wallpapers Edition)&lt;/h2&gt;
		&lt;/header&gt;
		&lt;div&gt;
			&lt;p&gt;What could be a better way to welcome June than with some colorful inspiration? Well, we might have something for you: wallpapers created with love by artists and designers from across the globe.&lt;/p&gt;
			&lt;p&gt;&lt;a&gt;Continue reading ↬&lt;/a&gt;&lt;/p&gt;
		&lt;/div&gt;
&lt;/article&gt;
	&lt;!-- More blog post teasers here  --&gt;
&lt;/section&gt;</code></pre>
</div>

In this code example, there is no heading for the region that we can reference. So this `region` would be announced as “all blog posts, region” by directly reading the value we supplied for the `aria-label` attribute. You will notice that the accessible name is written in lowercase. This is because [screenreaders could mistake words written in all caps to be acronyms](https://webaim.org/techniques/screenreader/#how) and then spell them out alphabet by alphabet instead of reading them as a single word. The sentence case is fine, but please avoid all caps. If you want to make emphasis, use the `em` tag.

To recap, `aria-labelledby` is a referential naming mechanism and is recommended because users, relying on assistive technology, get labels from existing content on the page, ensuring that the experience they are served is significantly the same as what other users get. On the other hand, `aria-label` is a direct naming mechanism. Using it means that users relying on assistive technology get labels from the author’s interpretation of what the element does. This is why it is recommended to use it only where no visible content on the page itself is appropriate. Active decision-making is required.

Finally, not every `section` has to be a region. Seriously, on learning this new power to create a `region`, it is tempting to look at all elements on your page and go, “you get a region, you get a region, everyone gets a region.” Please do not do this. Why? Scott O’Hara explains, “[Overpopulating a web page with landmarks will reduce their ability to help users find the most important parts of web pages](https://www.scottohara.me/blog/2021/07/16/section.html).” Remember, **regions should be attached to areas users want to reach easily**. Now let us look at real-life examples of these in play.

Smashing Magazine uses the `aria-label` technique for the “Quick Summary” part of this blog post. If you open your developer tool and Inspect the “Quick Summary”, this is what the markup looks like:

<div class="break-out">

<pre><code class="language-html">&lt;section aria-label="quick summary" class="article&#95;&#95;summary"&gt;
	&lt;span class="summary&#95;&#95;heading"&gt;Quick summary&nbsp;↬&lt;/span&gt;
	&lt;!-- 	Rest of summary continues here --&gt;
&lt;/section&gt;</code></pre>
</div>

Now screen reader users can jump to the “Quick Summary” region using shortcuts and get an overview of what the article is about without having to first interact with the whole article.

Let’s take another look at Twitter, a web application for using the `aria-labelledby` technique. Look at the developer tools, particularly the `section` holding your timeline. You will see an `aria-labelledby="accessible-list-9"` attribute in the `section`’s opening tag. It points to the `h1` element just below it, which has an `id="accessible-list-9"` and text content that says “Your Home Timeline.” Now users of screen readers can use the landmark navigation menu in their screen reader and navigate to “Your Home Timeline region.”

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9afb8a77-c54d-4043-bf09-f0da09576e9f/twitter-aria-labelledby-example.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9afb8a77-c54d-4043-bf09-f0da09576e9f/twitter-aria-labelledby-example.jpg" width="800" height="547" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9afb8a77-c54d-4043-bf09-f0da09576e9f/twitter-aria-labelledby-example.jpg'>Large preview</a>)" alt="A screenshot from Twitter with the code below showing aria-labelledby technique" >}}

Two questions may have crossed your mind. First, why is there a `role="region"` on the `section` element when the specs say that a `section` with an accessible name does not need to be assigned a region role expressly? Second, why can’t I see the `h1` element with “Your Home Timeline” in my browser if the `aria-labelledby` is supposed to reference a visible element? 

For the first question about declaring `role="region"` on the `section` element, the specs say it is not recommended to expressly set a role that is the same as the implied semantics. However, they do recognise that there might be browsers and devices that do correctly expose the implied semantics. As such, for an application like Twitter used by hundreds of millions of persons, it is reasonable to set the region role expressly to cover the bases as they cannot predict all the varying types of browsers and devices in use.

The second question is why the referenced element for the `aria-labelledby` is not on the page. This is a pattern/technique that people building pages with accessibility in mind employ every now and then. No rule has been broken here. An `h1` element is a visible element. What has been done here is to use CSS to remove the visual rendering of elements that are not considered necessary for sighted users but crucial for non-sighted users. For sighted users, the timeline is identifiable without a heading. However, the heading is also a reference point to name the region for screen reader users, so we need it in our HTML. By using a neat CSS technique, one can [take content off the screen but leave it visible to screen readers](https://webaim.org/techniques/css/invisiblecontent/).

Here’s another interesting thing I noticed when you make your `section` into a `region`. Remember our *Accessibility* tab using the *Inspector* in our developer tools? Well, the `section`’s role on the accessibility tree does not directly change to `region` in Firefox. What happens is that a `region` branch is created as a child of the `section`. In Firefox, the tree becomes `section` → `region`.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c40a4b1f-1a86-4749-8177-a49dc5ededb8/quick-summary-region-inspect-view-firefox.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c40a4b1f-1a86-4749-8177-a49dc5ededb8/quick-summary-region-inspect-view-firefox.jpg" width="800" height="517" sizes="100vw" caption="A screenshot of the Accessibility Tree shows that Firefox creates a new <code>region</code> branch as a child of the <code>section</code> when a <code>section</code> is assigned a role of <code>region</code>. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c40a4b1f-1a86-4749-8177-a49dc5ededb8/quick-summary-region-inspect-view-firefox.jpg'>Large preview</a>)" alt="A screenshot of the Accessibility Tree shows that Firefox creates a new region branch as a child of the section when a section is assigned a role of region" >}}

However, in Chrome and Microsoft Edge, the `section` itself changes to a `region` role.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/53d60a0d-87da-431f-85c3-1e19b971bf87/quick-summary-region-inspect-view-chrome.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/53d60a0d-87da-431f-85c3-1e19b971bf87/quick-summary-region-inspect-view-chrome.png" width="800" height="590" sizes="100vw" caption="A screenshot of the Accessibility Tree in Chrome shows that when a <code>section</code> made into a <code>region</code>, the <code>section</code> is removed from the accessibility tree and replaced with a <code>region</code>. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/53d60a0d-87da-431f-85c3-1e19b971bf87/quick-summary-region-inspect-view-chrome.png'>Large preview</a>)" alt="A screenshot of the Accessibility Tree in Chrome shows that when a section made into a region, the section is removed from the accessibility tree and replaced with a region" >}}

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2dfe27aa-7cbc-4871-b2da-c87062227ff0/quick-summary-region-inspect-view-edge.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2dfe27aa-7cbc-4871-b2da-c87062227ff0/quick-summary-region-inspect-view-edge.png" width="800" height="567" sizes="100vw" caption="A screenshot of the Accessibility Tree in Microsoft Edge shows that when a <code>section</code> is made into a <code>region</code>, the <code>section</code> is removed from the accessibility tree and replaced with a <code>region</code>. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2dfe27aa-7cbc-4871-b2da-c87062227ff0/quick-summary-region-inspect-view-edge.png'>Large preview</a>)" alt="A screenshot of the Accessibility Tree in Microsoft Edge shows that when a section is made into a region, the section is removed from the accessibility tree and replaced with a region" >}}

### Should I Bother?

Yes, you absolutely should. 

The truth is even if you are not designing for display on an iWatch or other smart gadgets, and even if you have no reason to create `region`s on your page, you should still use the correct element. 

Firstly, this article by [Mandy Michael](https://twitter.com/Mandy_Kerr) reveals that [browsers pay attention to your HTML structure to generate a Reader mode](https://medium.com/@mandy.michael/building-websites-for-safari-reader-mode-and-other-reading-apps-1562913c86c9) which strips the page of unnecessary information, images and background. Safari, Chrome, Firefox, Edge, and other reading apps specifically look out for [HTML sectioning content](https://html.spec.whatwg.org/#sectioning-content) to prioritise display for reading. The sectioning content includes `article` and `section` amongst others. Without carefully wrapping your content into appropriate elements, you risk it being ignored when a minimalist view is created.

Secondly, It helps you actively think about how you present your content. Content design is a crucial part of our page that we should be conscious about. It is the basis of our page. The words we use, the headings we use, and the length of our paragraphs all affect our users. How we group our content is also essential.

As designers and developers, we may feel that our main reason for grouping content is simply to style them. But if we start to care about the content, we may realise better ways to create our page. Grouping content does a lot more than preparing our content for visual styling. If we take care to write our HTML consciously, we can, to an extent, be certain that we have made our corner of the web a better place for all.

Writing this article and thinking about how I would have sectioned this page helped me create a coherent structure for my work. It helped me identify places where the content was out of place in terms of the surrounding context. With posts as long as this, thinking of how we group content becomes crucial. 

Even where content is extremely short, thinking about how we group content helps create better content. In a recent [knowledge-sharing webinar on Content Design and Accessibilit](https://docs.google.com/presentation/d/1GLOraVFcNaF_QeoV5unAFMgmX2ApLLIVM7P0OsA-IFg/edit?usp=sharing)y, [Amanda Diamond](https://www.linkedin.com/in/amanda-diamond-2bbabb33/?original_referer=https%3A%2F%2Fuk.linkedin.com%2Fin%2Famanda-diamond-2bbabb33&original) shared this slide showing how a very short content block can be broken up to make it easier for people to read. These two screenshots contain the exact same content, yet one is easier to digest. This would be a perfect place to use a `section` instead of just a `div`. Notice how each section carries an appropriate heading explaining each content block.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ceca208c-154e-42f4-b769-b62c67f0c125/content-design-screenshot.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ceca208c-154e-42f4-b769-b62c67f0c125/content-design-screenshot.png" width="800" height="452" sizes="100vw" caption="Two screenshots of a page giving the exact same information about ‘Being charged with a crime’. The first is split up into sections with headings making it easier to scan and scroll. The second contains the same information in just one paragraph. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ceca208c-154e-42f4-b769-b62c67f0c125/content-design-screenshot.png'>Large preview</a>)" alt="Two screenshots of a page giving the exact same information about ‘Being charged with a crime’. The first is split up into sections with headings making it easier to scan and scroll. The second contains the same information in just one paragraph" >}}

## Conclusion

We have looked at a mental model that forces us to interact with our content to determine how best to group it. We question:

- If the grouping plays a role in our document structure?
- If it does, what role does it play?

From our answers, we can choose the appropriate grouping element for our content. 

We have also looked at what happens when the browser builds an accessibility tree for our `section` or `article` elements and how to extend our `section` into a `region` to allow easy navigation.

Finally, I think we communicate with two sets of consumers of our content &mdash; the end-users who read our pages from an URL and others who have to interact with our markup. We may tend to think largely in terms of end-users when it comes to HTML. However, I believe writing HTML that is easy to understand and self-explanatory for whoever will work on it is sufficient reason to use the correct semantic element.

{{< signature "vf, yk, il" >}}
