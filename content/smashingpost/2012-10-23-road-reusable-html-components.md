---
title: The Road To Reusable HTML Components
slug: road-reusable-html-components
image: null
date: 2012-10-23T11:46:44.000Z
author: niels-matthijs
description: >-
  A few weeks ago, I dug up an old article that I wrote for Smashing Magazine,
  “[When One Word Is More Meaningful Than a
  Thousand](https://www.smashingmagazine.com/2010/07/14/when-one-word-is-more-meaningful-than-a-thousand).”
  While I stand firmly behind all of the HTML development principles I listed
  back then, the article lacked one important thing: hands-on examples.
categories:
  - Coding
  - HTML
  - Semantics
---
A few weeks ago, I dug up an old article that I wrote for Smashing Magazine, “<a href="https://www.smashingmagazine.com/2010/07/14/when-one-word-is-more-meaningful-than-a-thousand">When One Word Is More Meaningful Than a Thousand</a>.” While I stand firmly behind all of the HTML development principles I listed back then, the article lacked one important thing: hands-on examples.

Sure enough, the theory behind component-based HTML is interesting in its own right, but without a few illustrative examples, it’s all very dry and abstract. Not that HTML enthusiasts should shy away from that (on the contrary, I would say), but there’s nothing like a good example to clear up some of the finer points of a concept.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [An Introduction To Object Oriented CSS (OOCSS)](https://www.smashingmagazine.com/2011/12/an-introduction-to-object-oriented-css-oocss/)
*   [<span class="headline">Client-Side Templating</span>](https://www.smashingmagazine.com/2012/12/client-side-templating/)
*   [Semantic CSS With Intelligent Selectors](https://www.smashingmagazine.com/2013/08/semantic-css-with-intelligent-selectors/)

So, that’s what I’ve set out to do in this article. In the previous one, I sampled a couple of common content types (such as products, stories and videos) across different websites. Now I’ll stick to four different views of a single content type: the story (or news article). It’s a pretty simple and straightforward content type that most people know and have developed at some point in their career. For some real-world inspiration, I’ll refer to the Boston Globe website (a front-end favorite of mine).

{{% feature-panel %}}

One important disclaimer before we get started. This article isn’t so much about the resulting HTML as it is about the methodology of writing HTML. Your opinion on the class names, structures and source order that I suggest along the way may differ, but that’s not what the article is really about (although I’m not saying it wouldn’t yield some interesting discussion).</p>

## The Difference Between This And Other Popular Component-Based Methodologies

Component-based HTML development isn’t exactly new. A couple of months ago, Smashing Magazine has run articles on <a href="https://www.smashingmagazine.com/2012/04/16/a-new-front-end-methodology-bem/">BEM</a>, <a href="https://www.smashingmagazine.com/2011/12/12/an-introduction-to-object-oriented-css-oocss/">OOCSS</a> and <a href="https://www.smashingmagazine.com/2012/04/20/decoupling-html-from-css/">SMACSS</a>. While I don’t have enough information to judge BEM, the other two methodologies are clearly opposed to what I am going to propose here.

Methodologies such as OOCSS and SMACCS were born out of frustration with CSS, but these methodologies try to ease CSS development by altering the HTML code. I think this is definitely not the way to go (and if you check the original presentation by Nicole Sullivan, you’ll find that she proposes an early version of mixins as a better alternative). Writing HTML is about so much more than making sure the CSS has the hooks it needs for you to implement the design; so, coming at it from a CSS angle can only diminish the overall quality of the HTML you write. The problem is not limited to providing the right hooks for CSS and JavaScript; the true challenge is to make sure that every element across a website is identifiable. If you can accomplish that, then you’ve got CSS, JavaScript and whatever other script technology you’re using covered without having to worry about the project’s specifics.

The methodology I will demonstrate below was conceived with reusability and robustness in mind. It is largely independent of project-specific requirements and remains as close as possible to the purity that HTML development deserves, resulting in individual HTML snippets that are as versatile as they are reusable.</p>

## Step 1: Gather All Views And Instances Of A Single Component

Let’s take this one step at a time. First of all, we need to state the requirements of our content type. To do that, we would normally run through all of the wireframes of a project, listing and grouping all of the different instances and views of each content type. To keep our example as clear and simple as possible, though, I’ve hand-picked four representative views that I’ve encountered on the <a href="https://bostonglobe.com/">Boston Globe</a> website.

<img loading="lazy" decoding="async" class="120790" title="Boston News" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/39c47875-8de2-411a-b45e-10c9577e5640/boston-news.jpeg" alt="Boston News" width="500" height="711" />

I peeked quickly behind the curtains and found the following hooks in the HTML code:

1.  Shortlist view: `.in-section ul li`
2.  Thumb view: `.feat-thumb`
3.  Summary view: `div.story`
4.  Detail view: `div.article` (or no root at all)

To be honest, I find this quite messy. If for some reason you wanted to single out all stories on your page or website (whether for CSS, JavaScript, analytics or another reason), you would have to work around quite a few ambiguities. Surely, we can do a better job.</p>

## Step 2: Define The Root

<pre><code class="language-markup tmp-html">&lt;article class="story"&gt;
   …
&lt;/article&gt;</code></pre>

There! That wasn’t too difficult now, was it? We picked the <code>article</code> element and hooked a single class name to it, which we’ll use as a base indicator for all stories. This way, we make sure that we can target all story instances using a single fixed identifier. As you can see from the Boston Globe examples, though, each view requires unique styling. Relying solely on the context of our story instances is far from flexible, so let’s introduce a specifying class for each view:

1.  Shortlist view: `.story.shortlist`
2.  Thumb view: `.story.thumb`
3.  Summary view: `.story.summary`
4.  Detail view: `.story.detail`

The reason for adding specifying classes to the root element itself (rather than, for example, to a list surrounding it) is flexibility. If tomorrow you are asked to build a composite list that holds both summary and shortlist views of the story component, you want to be able to do that without breaking a sweat.</p>

## Step 3: Defining The Logical Units Inside

With that out of the way, it’s time to look at what’s inside each story component. Rather than writing the HTML for each separate view, we’ll start by going through all of the different views, listing all of the elements (i.e. logical units) that we find inside. For each element, we’ll define the HTML. Mind that these logical units could probably reappear in a different context and that they are usually components by themselves, so chances are high that you’ve already written HTML snippets for them elsewhere in your project.</p>

### Heading

There’s always a heading. The heading summarizes all of the content that follows, so it’s one of the most essential parts of your content type (apart from the content itself, of course). All of the views listed above contain a heading, but even if you come across a view that doesn’t visually display a heading, put it in the HTML code anyway and hide it with CSS if necessary. This way, you will always “enter” your content type knowing what it’s going to be about. As for the actual code, that’s pretty straightforward:

<pre><code class="language-markup tmp-html">&lt;h1&gt;news heading&lt;/h1&gt;</code></pre>

### Thumbnail

The second thing we see is a thumbnail image. Thumbnail images aren’t quite a part of the actual content, although in some cases a thumbnail is little more than a (browser-)resized version of the first image within the story content. It doesn’t have to be, though, because a thumbnail functions mainly as a visual cue that attracts the visitor’s attention to the story. In some cases, it isn’t even featured at all in the story itself, so let’s consider it a standalone item.

Again, the code is pretty simple. We’ve just added a wrapper around the <code>img</code> element so that we can easily add a caption if needed.

<pre><code class="language-markup tmp-html">&lt;div class="image thumb"&gt;&lt;img src="…" alt="…" /&gt;&lt;/div&gt;</code></pre>

### Meta Data

Most content types feature meta data. Meta data isn’t truly a part of the content itself, but it tells you something extra about the content embedded within the content type. In the views above, we find several types of meta data: author, publication date, section indicator and a “first published in [resource]” line.

Coming up with the markup for meta data is a little trickier. If you follow the HTML5 specficiation to the letter, then you are supposed to use a definition list. Meta data is nothing more than a list of label-value pairs, which is exactly what the specification’s authors had in mind when they expanded the semantic range of the HTML5 definition list. But because the markup for definition lists is still missing a wrapper for list items, it’s not very robust, and in many cases styling it proves to be a real hassle (if not impossible). You could invalidate your code by wrapping a div around each <code>dd</code>-<code>dt</code> pair (so that you still enjoy the semantic benefits of the element), but I usually prefer to keep my code valid, sacrificing some tag semantics in the process.

<pre><code class="language-markup tmp-html">&lt;div class="meta"&gt;
    &lt;div class="author"&gt;
        &lt;span class="dt"&gt;label:&lt;/span&gt;&lt;span class="dd"&gt;value&lt;/span&gt;
    &lt;/div&gt;
    &lt;div class="publishDate"&gt;
        &lt;span class="dt"&gt;label:&lt;/span&gt;&lt;span class="dd"&gt;value&lt;/span&gt;
    &lt;/div&gt;
    &lt;div class="section"&gt;
        &lt;span class="dt"&gt;label:&lt;/span&gt;&lt;span class="dd"&gt;value&lt;/span&gt;
    &lt;/div&gt;
    &lt;div class="publishedIn"&gt;
        &lt;span class="dt"&gt;label:&lt;/span&gt;&lt;span class="dd"&gt;value&lt;/span&gt;
    &lt;/div&gt;
&lt;/div&gt;</code></pre>

### Abstract

An abstract is a short summary of or introduction to your content type. In some cases, but not always, it is identical to the actual introductory text. If the abstract is identical to the introductory text, then you could consider it a part of the actual content; if it’s tailored copy, then it should be marked up separately.

As for the HTML, you could use a paragraph tag with a class attached to it, but then you’d limit abstracts to a single paragraph. Looking at the Boston Globe example, it’s fine, but if we want our code to be portable across projects, then keeping our options open is probably best. This results in the following HTML code:

<pre><code class="language-markup tmp-html">&lt;div class="abstract"&gt;
    &lt;p&gt; … &lt;/p&gt;
&lt;/div&gt;</code></pre>

### Action Links

In the detail view of the story, we see a list of actions related to the story itself. Typically, lists such as these include print and mail actions and, of course, the token social sharing options. Instead on relying on source order or numbered classes, we’ll give each link a unique class so that we can play around with it if needed.

<pre><code class="language-markup tmp-html">&lt;div class="actions"&gt;
   &lt;ul&gt;
      &lt;li class="recommend"&gt;…&lt;/li&gt;
      …
      &lt;li class="print"&gt;…&lt;/li&gt;
   &lt;/ul&gt;
&lt;/div&gt;</code></pre>

You’ll notice that the action list is placed above the content, making it a likely candidate to be put inside a <code>header</code> element. While I’ll stick to that as a concession to the design, the links actually belong in the <code>footer</code> element of your content type. These are actions that become relevant once you know the context. You wouldn’t (or at least shouldn’t) share an article based merely on the title; knowing the content is crucial to deciding on your action. Adventurous CSS’ers could leave room in the header and then position the list from within the footer, but that would make the CSS implementation more fragile.</p>

### Actual Content

Finally, we get to the crux of the matter, the story itself. What’s actually inside a story often depends on the freedom you’ve given to your content editors. Either you’ve given them a fixed set of templates to work with, or you’ve just dropped a WYSIWYG editor into the CMS and hoped for the best. One thing you need to do, though, is contain the content section, if only as a warning that what follows may be user content.

<pre><code class="language-markup tmp-html">&lt;div class="content"&gt;
    …
&lt;/div&gt;</code></pre>

### Related Stories

Finally, we find a shortlist of related stories. The most important thing to recognize here is that example one is exactly the same view as the list of related stories that we’re trying to make, so there’s really no reason to differentiate the HTML code between the two instances.

<pre><code class="language-markup tmp-html">&lt;section class="storyList"&gt;
    &lt;div class="main"&gt;
      &lt;article class="story"&gt; … &lt;/article&gt;
    &lt;/div&gt;
&lt;/section&gt;</code></pre>

## Step 4: Defining Structural Containers

The elements listed above have not only a logical sequence of elements, but also a logical hierarchical structure. Some elements precede the content itself and should be placed separate from the main content. Some elements are afterthoughts or additional information and should be placed after the actual content. To do this, we set up a typical <code>header</code>-<code>main</code>-<code>footer</code> structure.

<pre><code class="language-markup tmp-html">&lt;article class="story"&gt;
   &lt;header&gt; … &lt;/header&gt;
   &lt;div class="main"&gt; … &lt;/div&gt;
   &lt;footer&gt; … &lt;/footer&gt;
&lt;article&gt;</code></pre>

The main wrapper might not look absolutely necessary at first glance, but because it is a logical unit, it deserves a container of its own.</p>

## Step 5: Throw Everything Together

Now that all of the HTML snippets are ready, it is time to throw everything together, creating one master component.

<pre><code class="language-markup tmp-html">&lt;article class="story"&gt;
   &lt;header&gt;
      &lt;h1&gt;story heading&lt;/h1&gt;
      &lt;div class="image thumb"&gt;&lt;img src="…" alt="…" /&gt;&lt;/div&gt;
      &lt;div class="meta"&gt;
         &lt;div class="author"&gt;
            &lt;span class="dt"&gt;label:&lt;/span&gt;&lt;span class="dd"&gt;value&lt;/span&gt;
         &lt;/div&gt;
         &lt;div class="publishDate"&gt;
            &lt;span class="dt"&gt;label:&lt;/span&gt;&lt;span class="dd"&gt;value&lt;/span&gt;
         &lt;/div&gt;
         &lt;div class="section"&gt;
            &lt;span class="dt"&gt;label:&lt;/span&gt;&lt;span class="dd"&gt;value&lt;/span&gt;
         &lt;/div&gt;
         &lt;div class="publishedIn"&gt;
            &lt;span class="dt"&gt;label:&lt;/span&gt;&lt;span class="dd"&gt;value&lt;/span&gt;
         &lt;/div&gt;
      &lt;/div&gt;
      &lt;div class="abstract"&gt;
         &lt;p&gt; … &lt;/p&gt;
      &lt;/div&gt;
      &lt;div class="actions"&gt;
         &lt;ul&gt;
            &lt;li class="recommend"&gt;…&lt;/li&gt;
            …
            &lt;li class="print"&gt;…&lt;/li&gt;
         &lt;/ul&gt;
      &lt;/div&gt;
   &lt;/header&gt;
   &lt;div class="main"&gt;
      &lt;div class="content"&gt; … &lt;/div&gt;
      &lt;aside&gt;
         &lt;section class="storyList"&gt;
            &lt;div class="main"&gt;
               &lt;article class="story"&gt;…&lt;/article&gt;
            &lt;/div&gt;
         &lt;/section&gt;
      &lt;/aside&gt;
   &lt;/div&gt;
   &lt;footer&gt; (used for read more links, links to comment section, etc.) &lt;/footer&gt;
&lt;article&gt;</code></pre>

## Step 6: Adding Microdata

Even though the HTML code is now flexible and descriptive enough for other scripts to extract or pinpoint whatever structure they need, our component still misses a common vocabulary. Sure enough, we’ve added a <code>.story</code> class to the root element, but what about using <code>.news</code>, <code>.article</code> or <code>.newsItem</code>? They’re still not very semantic. Well, HTML5 provides us with microdata, a part of the HTML5 specification, which allows us to add a global vocabulary to our HTML code. You can make your own vocabulary if you wish, but if you check a website such as <a href="https://schema.org/">Schema.org</a> you’ll see that plenty are already available for the most common objects. As a bonus, search engines such as Google, Yahoo and Bing support microdata already.

The <code>itemscope</code> property should be placed in the root element, together with the <code>itemtype</code> (which specifies a URL for the vocabulary — in this case, the Schema.org website). After that, it’s just a matter of running through the available vocabulary properties and adding them to your code using <code>itemprop</code>. This will give us the following HTML component:

<pre><code class="language-markup tmp-html">&lt;article class="story" itemscope="itemscope" itemtype="https://schema.org/NewsArticle"&gt;
   &lt;meta content="en" itemprop="inLanguage" /&gt;
   &lt;header&gt;
      &lt;h1 itemprop="headline"&gt;story heading&lt;/h1&gt;
      &lt;div class="image thumb"&gt;&lt;img src="…" alt="…" itemprop="image"/&gt;&lt;/div&gt;
      &lt;div class="meta"&gt;
         &lt;div class="author"&gt;
            &lt;span class="dt"&gt;label:&lt;/span&gt;&lt;span class="dd" itemprop="author"&gt;value&lt;/span&gt;
         &lt;/div&gt;
         &lt;div class="publishDate"&gt;
            &lt;span class="dt"&gt;label:&lt;/span&gt;&lt;span class="dd" itemprop="datePublished"&gt;value&lt;/span&gt;
         &lt;/div&gt;
         &lt;div class="section"&gt;
            &lt;span class="dt"&gt;label:&lt;/span&gt;&lt;span class="dd" itemprop="articleSection"&gt;value&lt;/span&gt;
         &lt;/div&gt;
         &lt;div class="publishedIn"&gt;
            &lt;span class="dt"&gt;label:&lt;/span&gt;&lt;span class="dd"&gt;value&lt;/span&gt;
         &lt;/div&gt;
      &lt;/div&gt;
      &lt;div class="abstract" itemprop="description"&gt;
         &lt;p&gt; … &lt;/p&gt;
      &lt;/div&gt;
      &lt;div class="actions"&gt;
         &lt;ul&gt;
            &lt;li class="recommend"&gt;…&lt;/li&gt;
            …
            &lt;li class="print"&gt;…&lt;/li&gt;
         &lt;/ul&gt;
      &lt;/div&gt;
   &lt;/header&gt;
   &lt;div class="main"&gt;
      &lt;div class="content" itemprop="articleBody"&gt; … &lt;/div&gt;
      &lt;aside&gt;
         &lt;section class="storyList"&gt;
            &lt;div class="main"&gt;
               &lt;article class="story" itemscope="itemscope" itemtype="https://schema.org/NewsArticle"&gt;…&lt;/article&gt;
            &lt;/div&gt;
         &lt;/section&gt;
      &lt;/aside&gt;
   &lt;/div&gt;
   &lt;footer&gt; (used for read more links, links to comment section, etc.) &lt;/footer&gt;
&lt;article&gt;</code></pre>

## Step 7: And Finally…

Now that we have our master component, all that’s left to do is check each view and remove the elements from the master component that are not needed. If this results in any leftover (<code>= empty</code>) structural wrappers, we’ll remove them, too. This will give us the following snippets:

### Shortlist View

<pre><code class="language-markup tmp-html">&lt;article class="story shortlist" itemscope="itemscope" itemtype="https://schema.org/NewsArticle"&gt;
   &lt;meta content="en" itemprop="inLanguage" /&gt;
   &lt;header&gt;
      &lt;h1 itemprop="headline"&gt;story heading&lt;/h1&gt;
   &lt;/header&gt;
&lt;article&gt;</code></pre>

### Thumb view

<pre><code class="language-markup tmp-html">&lt;article class="story thumb" itemscope="itemscope" itemtype="https://schema.org/NewsArticle"&gt;
   &lt;meta content="en" itemprop="inLanguage" /&gt;
   &lt;header&gt;
      &lt;h1 itemprop="headline"&gt;story heading&lt;/h1&gt;
      &lt;div class="image thumb"&gt;&lt;img src="…" alt="…" itemprop="image"/&gt;&lt;/div&gt;
      &lt;div class="meta"&gt;
         &lt;div class="section"&gt;
            &lt;span class="dt"&gt;label:&lt;/span&gt;&lt;span class="dd" itemprop="articleSection"&gt;value&lt;/span&gt;
         &lt;/div&gt;
      &lt;/div&gt;
   &lt;/header&gt;
&lt;article&gt;</code></pre>

### Summary view

<pre><code class="language-markup tmp-html">&lt;article class="story summary" itemscope="itemscope" itemtype="https://schema.org/NewsArticle"&gt;
   &lt;meta content="en" itemprop="inLanguage" /&gt;
   &lt;header&gt;
      &lt;h1 itemprop="headline"&gt;story heading&lt;/h1&gt;
      &lt;div class="image thumb"&gt;&lt;img src="…" alt="…" itemprop="image"/&gt;&lt;/div&gt;
      &lt;div class="meta"&gt;
         &lt;div class="author"&gt;
            &lt;span class="dt"&gt;label:&lt;/span&gt;&lt;span class="dd" itemprop="author"&gt;value&lt;/span&gt;
         &lt;/div&gt;
      &lt;/div&gt;
      &lt;div class="abstract" itemprop="description"&gt;
         &lt;p&gt; … &lt;/p&gt;
      &lt;/div&gt;
   &lt;/header&gt;
   &lt;div class="main"&gt;
      &lt;aside&gt;
         &lt;section class="storyList"&gt;
            &lt;div class="main"&gt;
               &lt;article class="story" itemscope="itemscope" itemtype="https://schema.org/NewsArticle"&gt;…&lt;/article&gt;
            &lt;/div&gt;
         &lt;/section&gt;
      &lt;/aside&gt;
   &lt;/div&gt;
&lt;article&gt;</code></pre>

### Detail view

<pre><code class="language-markup tmp-html">&lt;article class="story detail" itemscope="itemscope" itemtype="https://schema.org/NewsArticle"&gt;
   &lt;meta content="en" itemprop="inLanguage" /&gt;
   &lt;header&gt;
      &lt;h1 itemprop="headline"&gt;story heading&lt;/h1&gt;
      &lt;div class="meta"&gt;
         &lt;div class="author"&gt;
            &lt;span class="dt"&gt;label:&lt;/span&gt;&lt;span class="dd" itemprop="author"&gt;value&lt;/span&gt;
         &lt;/div&gt;
         &lt;div class="publishDate"&gt;
            &lt;span class="dt"&gt;label:&lt;/span&gt;&lt;span class="dd" itemprop="datePublished"&gt;value&lt;/span&gt;
         &lt;/div&gt;
         &lt;div class="section"&gt;
            &lt;span class="dt"&gt;label:&lt;/span&gt;&lt;span class="dd" itemprop="articleSection"&gt;value&lt;/span&gt;
         &lt;/div&gt;
         &lt;div class="publishedIn"&gt;
            &lt;span class="dt"&gt;label:&lt;/span&gt;&lt;span class="dd"&gt;value&lt;/span&gt;
         &lt;/div&gt;
      &lt;/div&gt;
      &lt;div class="actions"&gt;
         &lt;ul&gt;
            &lt;li class="recommend"&gt;…&lt;/li&gt;
            …
            &lt;li class="print"&gt;…&lt;/li&gt;
         &lt;/ul&gt;
      &lt;/div&gt;
   &lt;/header&gt;
   &lt;div class="main"&gt;
      &lt;div class="content" itemprop="articleBody"&gt;…&lt;/div&gt;
   &lt;/div&gt;
&lt;article&gt;</code></pre>

## Reusable HTML Components Make Sense

If you look closely at the core principles of HTML, you will see that HTML leaves little room for variation. The HTML code we write is supposed to describe our content as clearly as possible, independent of the styling; so, there is really no reason to make different structural versions of a single component that appears in different contexts, pages or even projects. A news article is a news article, and while the inner particles may vary, the core structure, tag selection and naming conventions need not be tampered with. Of course, there is still room to accommodate the author’s personality, including minor personal preferences, certain ideologies and overall experience, but one author should ideally stick to a single structure for a single component.

Component-based HTML also has important practical advantages. Of course, the news article above is just one simple example, but you could do the same for all of the components that you use across projects. This might seem like a lot of work at first, but you’ll need to do it only once; after that, you can spend the time that you’ve saved on the dumb monkey work of fine-tuning your library. When I write the HTML for a new website these days, about 80 to 85% of the components are out of the box; the remaining 15 to 20% consist of small changes for project-specific requirements and new components (which might get added to my core library later on). This speeds up HTML development dramatically.

It’s also a tremendous advantage for people who prefer to design in the browser. One of the biggest drawbacks of designing in the browser is that the HTML is usually the least of your worries. You might intend to clean it up later, but if you’re honest with yourself, then you know that the probability that you’ll take the time to perfect an aspect of your work that’s mostly invisible to the client anyway is quite low. <strong>By using your own library of components, you won’t need to worry about the HTML anymore.</strong> If you need a certain component, you can just pluck it out of the box, knowing that you’re getting quality HTML from the start, and leaving you to focus on the design and CSS.

The most important advantage of component-based HTML is the quality of service you will be providing to your clients. Rather than delivering project-specific (i.e. styled) templates, you can offer them a solid HTML and component framework. This way, you give clients the option to deploy these components across multiple websites. Again, this will greatly speed up HTML development (and back-end implementation) in future projects — projects that can now start as soon as the wireframes are finished, rather than once the graphical designs are done. You could even go so far as to wireframe using your HTML components (with a white-label CSS attached to them). The possibilities seem endless. At the same time, this methodology will introduce an unprecedented level of consistency and predictability in code across all of the client’s websites, two things that are often lacking these days.</p>

## The Future Of HTML

The way I see it, reusable, component-based HTML is definitely the way forward, and it’s about time we take this next step in HTML development. Just start from the components that you’ve already built, make yourself a snippet library, and go from there. Of course, some level of customization will always be needed, but I’m confident that the HTML snippet above can handle 90% of all story content types that you’ll find on the Web. The meta data may differ a little sometimes, and certain visualizations might require you to change the source order, but the basics are there to create whatever you need in less than five minutes. This is about applying the DRY principle (“don’t repeat yourself”) not just within a single project, but across multiple websites and even multiple clients.

In the end, methodologies such as OOCSS and SMACSS will only work against this ideal, because they are rooted in visual styling that prohobits the proper reuse of components across different websites. Not only that, but they will slow down the development cycle because the design becomes just another dependency. For now, this means you’ll have to rely on CSS preprocessors if you want maintainable CSS, but in the long run, we’ll benefit greatly from adapting the methodology described above. I’m interested in hearing your thoughts on this.

<em><a href="https://www.flickr.com/photos/opensourceway/4749432099/">Image source</a> of picture on front page.</em>

{{< signature "al" >}}

