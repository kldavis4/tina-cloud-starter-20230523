---
title: 'Introducing Mavo: Create Web Apps Entirely By Writing HTML!'
slug: introducing-mavo
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d92988e0-c8f9-468f-982c-42a20ce74602/zenpencils-programming-comic-500w-opt.png
date: 2017-05-16T21:20:25.000Z
author: lea-verou
description: >-
  Have you ever wanted to make a website that non-technical folks can edit right
  in the browser? Or have you ever wanted to make a website that presents an
  editable collection of items (e.g. your portfolio)? Or simply upload images to
  a website you made, right from the browser?

  Well, what if I told you, that you can do these things (and more!), **just
  with HTML and CSS**? **No programming code to write, no servers to manage.**
  You can make any element editable and saveable just by adding one HTML
  attribute to it. In fact, you can store your data locally in the browser, on
  Github, on Dropbox, or any other service just by changing an HTML attribute.
categories:
  - Coding
  - Tools
  - HTML
---
*   Make a website that non-technical folks (clients? family members?) can edit right in the browser
*   Make a website that presents an editable collection of items (your portfolio?)
*   Upload images to a website you made, right from the browser
*   Make an app to track and/or share an aspect of your life
*   Make a website that lets other people suggest edits to your data
*   Make an app that calculates something and presents the results in a custom way.

You can put your hand down now, it will get tired up there.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9ab5f0e2-6703-4c8e-bbaa-c16717fb22fa/comic.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/333d49b1-65fb-43bd-be35-a3d0b23ff953/comic-opt.gif" /></a><figcaption>Image adapted from <a href="https://zenpencils.com/comic/98-alan-watts-what-if-money-was-no-object/">this excellent Zen Pencils comic</a>, used with permission. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9ab5f0e2-6703-4c8e-bbaa-c16717fb22fa/comic.gif">Large preview</a>)</figcaption></figure>

What if I told you, that you can do these things (and more!), **just with HTML and CSS**? **No programming code to write, no servers to manage.** You can make any element editable and saveable just by adding one HTML attribute to it. In fact, you can store your data locally in the browser, on Github, on Dropbox, or any other service just by changing an HTML attribute.

{{% feature-panel %}}

You can also turn any HTML element into a collection, with customizable controls for adding items, deleting items, and rearranging items via drag and drop. And your website visitors could suggest edits to your data that create Github pull requests behind the scenes, straight from your website.

What if I told you can dynamically display the results of calculations on this data anywhere in your UI with a syntax that is engineered to be easy to read and write, even by non-programmers? And that you can create dynamic, interactive websites with the same processes and hosting providers you use for static websites?

These are only some of the things you can do with [Mavo](https://mavo.io), the project I’ve been working on for the past two years at [MIT CSAIL](https://csail.mit.edu/) and am excited to release today. **Mavo is a language that extends HTML to describe applications that manage, store, and transform data.** All you need to do to use Mavo in any HTML page is to [include its two files](https://mavo.io/docs/primer/#using-mavo). Yup, that’s it.

But how does it all work? Let's look at a few examples.</p>

## Editable Homepage

Assume we have a run-of-the-mill static homepage, with the following HTML inside `<body>`:

<pre><code class="language-html">
&lt;main&gt;
&lt;h1&gt;
	&lt;img src="images/photo.jpg" alt=""&gt;
	&lt;span&gt;Grumpy Cat&lt;/span&gt;
&lt;/h1&gt;
&lt;p&gt;
	&lt;strong&gt;Tardar Sauce&lt;/strong&gt; (born April 4, 2012), commonly known as &lt;strong&gt;Grumpy Cat&lt;/strong&gt;, is a cat, Internet and media personality and actress...
&lt;/p&gt;

&lt;div class="links"&gt;
	&lt;a class="twitter" href="https://twitter.com/RealGrumpyCat" target="_blank" title="Twitter"&gt;?&lt;/a&gt;
	&lt;a class="facebook" href="https://www.facebook.com/TheOfficialGrumpyCat" target="_blank" title="Facebook"&gt;f&lt;/a&gt;
	&lt;a class="wikipedia" href="https://en.wikipedia.org/wiki/Grumpy_Cat" target="_blank" title="Wikipedia"&gt;W&lt;/a&gt;
&lt;/div&gt;
&lt;/main&gt;
</code></pre>

_Photos and text taken from [Grumpy Cat’s Wikipedia page](https://en.wikipedia.org/wiki/Grumpy_Cat)._

Which, when styled looks like this:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2b692031-994a-4ba9-ae1d-cb9fea783fef/02-introducing-mavo-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ecdb6b2f-73dd-4379-9f97-409e3c0d6782/02-introducing-mavo-780w-opt.png" /></a><figcaption><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2b692031-994a-4ba9-ae1d-cb9fea783fef/02-introducing-mavo-preview-opt.png">Large preview</a></figcaption></figure>

By adding a few Mavo attributes, we can make it editable, and save its data to the cloud via Github (Github is only one of the supported services):

<pre><code class="language-html">
&lt;main mv-app="homepage" mv-storage="https://github.com/mavoweb/data/homepage" mv-plugins="tinymce"&gt;
&lt;h1&gt;
	&lt;img property="image" src="images/photo.jpg" alt=""&gt;
	&lt;span property="name"&gt;Grumpy Cat&lt;/span&gt;
&lt;/h1&gt;

&lt;p property="description" class="tinymce"&gt;
	&lt;strong&gt;Tardar Sauce&lt;/strong&gt; (born April 4, 2012), commonly known as &lt;strong&gt;Grumpy Cat&lt;/strong&gt;, is a cat, Internet and media personality and actress...
&lt;/p&gt;

&lt;div class="links"&gt;
	&lt;a property class="twitter" href="https://twitter.com/RealGrumpyCat" target="_blank" title="Twitter"&gt;?&lt;/a&gt;
	&lt;a property class="facebook" href="https://www.facebook.com/TheOfficialGrumpyCat" target="_blank" title="Facebook"&gt;f&lt;/a&gt;
	&lt;a property class="wikipedia" href="https://en.wikipedia.org/wiki/Grumpy_Cat" target="_blank" title="Wikipedia"&gt;W&lt;/a&gt;
&lt;/div&gt;
&lt;/main&gt;
</code></pre>

You can see the result in the video below or play with the live demo [here](https://mavo.io/demos/homepage).</p>

{{< vimeo id="217637310" >}}

But how did it work? What did we just do with all these attributes? Here is a breakdown:

*   `[mv-app="homepage"](https://mavo.io/docs/primer/#mv-app)` gives our app a name and tells Mavo to be active on this portion of the page.
*   `[property](https://mavo.io/docs/primer/#property)` attributes name important elements. By default, these elements will become editable and will be saved. The editing UI is generated based on the type of element, e.g. note that `img` is edited very differently from `<a>` or `span`. Of course, any generated UI is fully customizable.
*   The `[mv-storage](https://mavo.io/docs/primer/#mv-storage)` attribute tells Mavo where to store the data. Here its value is a (fuzzy) Github URL, so any data and uploads are stored on Github.
*   `mv-plugins="tinymce"` loads the [Mavo TinyMCE plugin](https://plugins.mavo.io/plugin/tinymce) for rich text editing, and `class="tinymce"` tells Mavo to edit this element via TinyMCE. Mavo is designed for extensibility, so developers that _do_ know JavaScript can write [Plugins](https://plugins.mavo.io) that extend Mavo’s functionality or even completely change how it works. Using these plugins is as easy as adding an `mv-plugins` attribute to any element in your page.

Besides editability and persistence, one of Mavo’s cool features when used in conjunction with Github is that you can let visitors log in to send **"edit suggestions"** to your data, entirely via the same graphical interface you use for editing said data. These "edit suggestions" create pull requests behind the scenes that you can easily approve or reject.</p>

## To-Do List

At this point, we have demonstrated how Mavo can help get rid of CMSes for very simple websites. However, it can do a lot more. Let’s look at a very different example, a to-do app!

As before, we start with a static HTML mockup:

<pre><code class="language-html">
&lt;main&gt;
	&lt;header&gt;
		&lt;h1&gt;My tasks&lt;/h1&gt;
		&lt;p&gt;&lt;strong&gt;0&lt;/strong&gt; done out of &lt;strong&gt;1&lt;/strong&gt; total&lt;/p&gt;
	&lt;/header&gt;

	&lt;ul&gt;
		&lt;li&gt;
			&lt;label&gt;
				&lt;input type="checkbox" /&gt;
				Do stuff
			&lt;/label&gt;
		&lt;/li&gt;
	&lt;/ul&gt;
&lt;/main&gt;
</code></pre>

Which looks like this after some styling:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/02483687-0e56-4e36-a363-1744a6931a0a/01-introducing-mavo-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f4afe61b-6fe9-4444-8191-7a93393ba1c9/01-introducing-mavo-780w-opt.png" /></a><figcaption><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/02483687-0e56-4e36-a363-1744a6931a0a/01-introducing-mavo-preview-opt.png">Large preview</a></figcaption></figure>

Can we use Mavo to turn this into a fully functional to-do list? You probably suspect what the answer is by now: Indeed we can! These are the changes we would need to make to our markup:

<pre><code class="language-html">
&lt;main mv-app="todo" mv-storage="local" mv-mode="edit"&gt;
	&lt;header&gt;
		&lt;h1&gt;My tasks&lt;/h1&gt;
		&lt;p&gt;&lt;strong&gt;[count(done)]&lt;/strong&gt; done out of &lt;strong&gt;[count(task)]&lt;/strong&gt; total&lt;/p&gt;
	&lt;/header&gt;

	&lt;ul&gt;
		&lt;li property="task" mv-multiple&gt;
			&lt;label&gt;
				&lt;input property="done" type="checkbox" /&gt;
				&lt;span property="taskTitle"&gt;Do stuff&lt;/span&gt;
			&lt;/label&gt;
		&lt;/li&gt;
	&lt;/ul&gt;
&lt;/main&gt;
</code></pre>

You can see the result in the video below or play with the live demo [here](https://mavo.io/demos/todo).</p>

{{< vimeo id="217638664" >}}

So, what did we do here?

*   `mv-storage="local"` tells Mavo to store the data locally in the browser.
*   You already know about `property` from the previous example. Note that it can also be used to group other properties.
*   `[mv-multiple](https://mavo.io/docs/primer/#mv-multiple)` is the Mavo feature that seems to excite people the most. It converts the element it’s on to an editable collection of items, full with controls to add and delete items, reorder items via drag and drop, and even keyboard shortcuts for all these!
*   `mv-mode="edit"` tells Mavo that everything should be editable immediately, and does not need a separate read mode.
*   `[count(done)]` and `[count(task)]` are [expressions](https://mavo.io/docs/primer/#expressions), similar to those you may have used in spreadsheets. Expressions are written in MavoScript, an expression language designed to be readable, forgiving, and easy to use even by non-programmers. Experienced developers can also use JavaScript in Mavo Expressions.

Mavo does not treat HTML as merely a shortcut to JavaScript, but as the primary language for creating web applications. We have done [actual user studies](https://dl.acm.org/citation.cfm?id=2984551) to prove that Mavo can be successfully used even by people with no programming experience, the [results](https://dl.acm.org/citation.cfm?id=2984551) of which are published at ACM UIST 2016, one of the top academic venues for Human-Computer Interaction research. Our vision is that JavaScript, server backends, and databases should become the "Assembly of the Web", mainly needed for specialized or high performance tasks. For everything else, HTML and CSS should suffice.</p>

<figure><a href="https://mavo.io"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f7b96458-6558-4965-a4a4-98ecf6aac8ec/mavo-logo-500w-opt.png" width="500" height="148" alt="Mavo Logo" /></a></figure>

Want to know more? Go over to [mavo.io](https://mavo.io), look at the [Demos](https://mavo.io/demos) and read the [Docs](https://mavo.io/docs/primer) to understand more about the language.

Is Mavo perfect yet? Far from it. As with every project of this magnitude, there is much more work to be done than what has already been done, in every front. But it's at a state where it can be useful, and demonstrate our vision for the future of Web development. We hope that others share that vision too, and (why not?) want to help us get there.

{{< signature "vf, yk, il" >}}

