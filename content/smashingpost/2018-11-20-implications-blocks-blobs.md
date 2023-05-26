---
title: 'Implications Of Thinking In Blocks Instead Of Blobs'
slug: implications-blocks-blobs
author: leonardolosoviz
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9f873f29-ed5f-4430-ae6f-99d1fecc2686/layout-components-800w.jpg
date: 2018-11-20T13:00:59+01:00
summary: >-
  What does Gutenberg bring to the future of WordPress? In this article, Leonardo Losoviz shares a number of implications of building sites through a component-based architecture (as the concept) and through Gutenberg (as the implementation), including what new functionalities it can deliver and how much better it can integrate with current website development trends.
description: >-
  What does Gutenberg bring to the future of WordPress? In this article, Leonardo Losoviz shares a number of implications of building sites through a component-based architecture (as the concept) and through Gutenberg (as the implementation), including what new functionalities it can deliver and how much better it can integrate with current website development trends.
categories:
  - WordPress
  - Plugins
  - HTML
---
Gutenberg is a JavaScript-based editor (more specifically, it is a React-based editor), which will soon transform the experience of creating content for WordPress and (on an upcoming stage when Gutenberg is transformed into a site builder) the experience of creating WordPress sites. 

Gutenberg, the site builder, will demand a different way of thinking how to lay the foundations of a website. In what we can already call the "old" model, WordPress sites are created by giving structure through templates (`header.php`, `index.php`, `sidebar.php`, `footer.php`), and fetching the content on the page from a single blob of HTML code. In the new model, the page has [(React) components](https://reactjs.org/docs/components-and-props.html) placed all over the page, each of them controlling their own logic, loading their own data, and self-rendering. 

To appreciate the upcoming change visually, WordPress is moving from this:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/366c70f4-04d8-4adc-a84a-f560a2e20a0d/layout-templates.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/366c70f4-04d8-4adc-a84a-f560a2e20a0d/layout-templates.jpg" sizes="100vw" caption="Currently pages are built through PHP templates. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/366c70f4-04d8-4adc-a84a-f560a2e20a0d/layout-templates.jpg'>Large preview</a>)" alt="The page contains templates with HTML code" >}}

...to this:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/695ebc02-fb0a-4950-a5eb-2183810ca36d/layout-components.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/695ebc02-fb0a-4950-a5eb-2183810ca36d/layout-components.jpg" sizes="100vw" caption="In the near future, pages will be built by placing self-rendering components in them. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/695ebc02-fb0a-4950-a5eb-2183810ca36d/layout-components.jpg'>Large preview</a>)" alt="The page contains autonomous components" >}}

I believe that switching from blobs of HTML code to components for building sites is nothing short of a paradigm shift. Gutenberg’s impact is much more than a switch from PHP to JavaScript: there are things that could be done in the past which will possibly not make sense anymore. Likewise, a new world of possibilities opens up, such as rich and powerful user interactions. Web developers will not go from creating their sites in one language to creating their sites in another language because the site will not be the same anymore; it will be a completely different site that will be built. 

<p><strong>Recommended reading</strong>: <em><a href="https://www.smashingmagazine.com/2018/08/complete-anatomy-gutenberg-wordpress-editor/">The Complete Anatomy Of The Gutenberg WordPress Editor</a></em></p>

{{% feature-panel %}}

Gutenberg has not been fully embraced by the WordPress community yet, for many reasons. For one, the new architecture is based on a plethora of tools and technologies (React, NPM, Webpack, Redux, and so on) which is much more difficult to learn and master than the old PHP-based one. And while it may be worth learning a new stack that delivers new functionalities, not every mom&pop site needs these new, shiny features.

After all, it is no coincidence that 30% of all sites across the globe are WordPress sites: most of these are really simple sites such as blogs, not dynamic social networks like Facebook. For another, WordPress inclusivity means that anyone could build a simple website &mdash; even people without coding experience, such as designers, content marketers, and bloggers.

But the complexity of the new architecture [will leave many people out](https://wptavern.com/wordpress-accessibility-team-lead-resigns-cites-political-complications-related-to-gutenberg#comment-263881) (I don’t even want to think about debugging my site in minified JavaScript code). And for another, once Gutenberg goes live, Facebook-backed React will be added to as many as 30% of all websites in the world &mdash; overnight. Many folks are uncomfortable with giving so much power to any sort of JavaScript library, while many others are mistrustful of Facebook. To alleviate this concern, Gutenberg abstracts React to also enable coding in other frameworks or libraries; however, in practice, React will undoubtedly be the predominant JavaScript library.

And yet, the prospect of being offered a new world of possibilities is sweet indeed. In my case, I am excited. However, my excitement is not about the technology (React) or about the implementation (Gutenberg), but about the concept, which is to create sites using components as the building unit. In the future, the implementation may switch to another platform, such as Vue, but the concept will remain.

Foreseeing what new features we will be able to implement is not always easy. It takes time to adapt to a new paradigm, and we tend to use new tools the old way until it dawns upon us how to use the new tools to accomplish new objectives. Even PDF files (which are a representation of print, the predominant technology before the web was born) are still a common sight on the web, neglecting the advantages that the web has over print.

<blockquote>“Imitating paper on a computer screen is like tearing the wings off a 747 and using it as a bus on the highway.”</br><br />&mdash; Ted Nelson</blockquote>

In this article, I will analyze several implications of building sites through a component-based architecture (as the concept) and through Gutenberg (as the implementation), including what new functionalities it can deliver, how much better it can integrate with current website development trends, and what it means to the future of WordPress.

{{% ad-panel-leaderboard %}}

## Extended Versatility And Availability Of Content

A very important side effect of treating all content as blocks is that it allows to target chunks of HTML individually and use them for different outputs. Whereas content inserted in the HTML blob is accessible only through the webpage, as chunks it can be accessed through an API, and its metadata is readily available. Take media elements &mdash; such as videos, audio or images. As a standalone block, the video can be played in an app, the audio can be played as a podcast, and the images can be attached to the email when sending a digest &mdash; all of this without having to parse the HTML code.

Likewise, content from blocks can be adapted for different mediums: from the tiniest screen to the biggest ones, touchscreen or desktop, commanded by voice or by touch, 2D/AR/VR, or who knows what the future might bring. For instance, an audio block allows the audio to be played on an Apple Watch, commanded by voice through the In-car system or an AWS Echo, or as a floating item in our virtual world when using a VR headset. Blocks can also make it easier to set-up a single source of truth for content to be published in different outputs, such as a responsive website, AMP, mobile app, email, or any other, as was done by NPR through their [Create Once, Publish Everywhere (COPE)](https://www.programmableweb.com/news/cope-create-once-publish-everywhere/2009/10/13) approach.

**Note**: *For more info on these topics, I suggest watching Karen McGrane’s [Content in a Zombie Apocalypse](https://karenmcgrane.com/talks/content-in-a-zombie-apocalypse/) talk.*

Blocks can improve the user experience too. If browsing the site through 3G, blocks can self-render in a slow-connection mode to display low-quality images and skip loading videos. Or it can enhance the layout, such as offering to show an image gallery with one click at any point of the webpage, and not just at the place where it was embedded in the article.

These experiences can be attained by separating content from form, which implies that the presentation and the meaning of the content are decoupled, and only the meaning is saved on the database, making presentation data secondary and saving it on another place. Semantic HTML is an expression of this concept: we should always use `<em>` which implies meaning, instead of `<i>` which is a form of presentation (to make the character be displayed in italics), because then this content will be available to other mediums, such as voice (Alexa can’t read in italics, but she can add emphasis to the sentence). 

Obtaining a thorough separation of content from form is very difficult since presentation code will often be added inside the block, through HTML markup (adding class "pull-right" already implies presentation). However, architecting the site using blocks already helps attain some level of separation at the layout level. In addition, blocks created to do just one thing, and do it very well, can make use of proper semantic HTML, have a good separation of concerns in its own architecture concerning HTML, JS, and CSS (so that porting them to other platforms may require only a minimum effort,) and be accessible, at least at the component-level.

**Note**: *A general rule of thumb: The more inclusive a component is, the more prepared it is for mediums yet to be invented.*

{{% ad-panel-leaderboard %}}

Unfortunately, Gutenberg was not designed with this purpose in mind, so blocks contain plenty of HTML markup for presentation too. For instance, an image block from an external image has, as its meaning, only the URL for the image, the alt description, and the caption (and possibly also the width and height); after creating an image block, the following chunk of code was saved in the DB (class `aligncenter` is for presentation, and the markup `<div class="wp-block-image" />` would be completely redundant if storing only meaning):

<div class="break-out">

<pre><code class="language-markup">&lt;!-- wp:image {"align":"center"} --&gt;
    &lt;div class="wp-block-image"&gt;
    &lt;figure class="aligncenter"&gt;
    &lt;img src="https://cldup.com/cXyG__fTLN.jpg" alt="Beautiful landscape"/&gt;
    &lt;figcaption&gt;If your theme supports it, you’ll see the "wide" button on
    the image toolbar. Give it a try.&lt;/figcaption&gt;
    &lt;/figure&gt;
    &lt;/div&gt;
&lt;!-- /wp:image --&gt;
</code></pre></div>

In addition, blocks are saved inside the post’s content (which is a big HTML blob) instead of [each having an entry of its own in the database](https://twitter.com/JJJ/status/940953146817380352). Reusable blocks (also called global blocks) do have their own entry though, which makes me fear that developers may convert standard blocks to reusable blocks just for a quick hack to access them straight in the DB. 

Similarly, I am worried that, if not properly designed, blocks can even cause havoc in our sites. For instance, unaware developers may ignore [the rule of least power](https://adactio.com/journal/14327), using JavaScript not just for functionality but also for [CSS](https://www.heydonworks.com/article/css-a-new-kind-of-JavaScript) and markup. In addition, Gutenberg’s server-side rendering (SSR) functionality is not isomorphic (i.e. it does not allow a single codebase to produce the output for both client and server-side code), hence dynamic blocks must implement the function to generate the HTML code also as PHP as to offer progressive enhancement (without which [the site is unaccessible while being initially loaded](https://twitter.com/jaffathecake/status/207096228339658752)). 

In summary, blocks are a step in the right direction towards making WordPress content available on any format and for any medium, but they are not a definitive solution, so much work still needs to be done.

## Performance

Performance matters. Faster sites lead to happier users, which [leads to better conversion rates](https://alistapart.com/article/improving-ux-through-front-end-performance). The team at Etsy, for instance, shelves new features, as cool as they may be, if these make their site loading time go over a critical threshold (I recommend watching Allison McKnight’s talk on [Building Performance for the Long Term](https://vimeo.com/254947097) and [slides](https://speakerdeck.com/aemcknig/building-performance-for-the-long-term)), while the team at Twitter [re-architected their site](https://blog.twitter.com/engineering/en_us/a/2012/improving-performance-on-twittercom.html) several years ago to support server-side rendering in order to show content as soon as possible, and continually implements [plenty of small changes](https://medium.com/@paularmstrong/twitter-lite-and-high-performance-react-progressive-web-apps-at-scale-d28a00e780a3) that add up to deliver a fast user experience.

JavaScript being so attractive to developers, they [experience no constraint on their use of it](https://infrequently.org/2018/09/the-developer-experience-bait-and-switch/), which is a real problem: [JavaScript is very expensive concerning performance](https://medium.com/@addyosmani/the-cost-of-JavaScript-in-2018-7d8950fbb5d4), and it should be used very carefully.

As it stands now, Gutenberg is far from optimal: whereas creating a post with the old editor (for which we need to install the [Classic Editor](https://wordpress.org/plugins/classic-editor/)) requires loading around 1.4 MB of JavaScript, Gutenberg loads around 3.5 MB of JavaScript, **just for its basic experience** (that is, without installing any additional block):

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1365bd0e-3633-420a-880d-5c19bd9ff771/gutenberg-scripts-load.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1365bd0e-3633-420a-880d-5c19bd9ff771/gutenberg-scripts-load.jpg" sizes="100vw" caption="Loading scripts for Gutenberg. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1365bd0e-3633-420a-880d-5c19bd9ff771/gutenberg-scripts-load.jpg'>Large preview</a>)" alt="At least 3.5 MB of scripts are required for loading Gutenberg" >}}

That means that, as it stands now, 3.5 MB is the baseline, and loading size will only increase from there as the site admin installs more blocks. As was seen in a [recent article on Smashing Magazine](https://www.smashingmagazine.com/2018/10/gutenberg-testimonials-sliderblock/), creating a testimonials block required 150KB of minified JavaScript. How many blocks will a standard site require? How many MB of JavaScript will the average site need to download?

The implications are several: for one, a heavy site is out of reach to the [next billion users](https://www.smashingmagazine.com/2017/03/world-wide-web-not-wealthy-western-web-part-1/), who have access mainly on slow connections, and who buy data plans which represent a significant chunk of their wage. For them, every MB of data makes a difference: sending Whatsapp messages is affordable, downloading several MBs of scripts just to load one site is not.

It is true that the user of the website will not need to interact with Gutenberg, since Gutenberg is simply for building the site, not for using it: Gutenberg is a back-end editor, not a front-end editor (and [it may never be](https://wpshout.com/changes-everything-gutenberg-good-now/) &mdash; at least as part of WordPress core). However, content creators will be penalized, and they are already a sizable target. In addition (as I argued earlier), users may end up being penalized too through dynamic blocks, which may create their markup through client-side JavaScript instead of server-side PHP.

There is also the issue of bloat from duplicated functionality added by 3rd party plugins. In the old days, a WordPress site may have loaded several versions of jQuery, which was relatively [easy](https://frankchimero.com/writing/everything-easy-is-hard-again/) to fix. Nowadays, there is a huge array of open source libraries to choose from for implementing a needed functionality (drag and drop, calendars, multi-select components, carousels, etc.,) so more likely than not a site with dozens of 3rd party blocks will have the same functionality implemented by different libraries, creating unnecessary bloat. In addition, there is a bit of bloat added to Gutenberg itself: because blocks are registered in the frontend, unregistering an already-registered block [is done by loading an additional script](https://jasonbahl.com/2018/05/29/whitelisting-blacklisting-blocks/). In my opinion, this is one of the biggest challenges for the Gutenberg contributors: to put in place a streamlined process that allows anyone (not just developers experienced with Webpack) to remove undesired libraries and package only the minimal set of resources needed for the application. 

Finally, I mention again that Gutenberg supports server-side rendering, but because it may not be easy to maintain, developers may be tempted to not rely on it. In this case, there is the cost of additional roundtrips needed to get the data from the REST endpoints, just to render the layout, during which time the user will be waiting. 

In my opinion, performance will be one of the major challenges for Gutenberg, the one that could make or break in terms of widespread adoption, and there is still plenty of work that should be done, mainly targeting the next stage when Gutenberg becomes a site builder.

## Web Standards

As mentioned earlier, Gutenberg abstracts React to provide a [framework-agnostic approach to building blocks](https://wptavern.com/wordpress-explores-a-JavaScript-framework-agnostic-approach-to-building-gutenberg-blocks) which, if implemented properly, can avoid WordPress being locked to React. The WordPress community is cautious when merging any JavaScript framework into WordPress core, in great part because Backbone.js, not long after being added to WordPress core, saw a sharp decline in popularity, and other than powering the Media Manager not many features were accomplished with it. Even if React is the [most popular JavaScript library right now](https://2018.stateofjs.com/front-end-frameworks/overview), there is no reason to believe that this will always be the case (as jQuery’s unraveling [can attest](https://githubengineering.com/removing-jquery-from-github-frontend/)), and WordPress must be prepared for when that day finally arrives (which, given the fast pace of technology, may happen sooner than expected).

The best way to avoid being locked to any library is through web standards and, more specifically in this case, the implementation of blocks through [web components](https://www.sitepen.com/blog/2018/07/06/web-components-in-2018/). Web components are strongly encapsulated components which operate with the browser APIs, so they don’t require any JavaScript library to work with. However, they can be implemented through any client-side JavaScript framework.

Even though [React doesn’t provide a seamless integration](https://custom-elements-everywhere.com/) with web components yet, it eventually (or rather hopefully) will. As it is [explained in React’s documentation](https://reactjs.org/docs/web-components.html), web components and React components can work alongside:

<blockquote>“React and Web Components are built to solve different problems. Web Components provide strong encapsulation for reusable components, while React provides a declarative library that keeps the DOM in sync with your data. The two goals are complementary. As a developer, you are free to use React in your Web Components, or to use Web Components in React, or both.”</blockquote>

As of today, prospects of this situation taking place are not looking very promising: I haven’t been able to find any tutorial for building blocks with web components. I believe the community should focus some effort towards this cause, encouraging developers to start building blocks using web components, and the sooner the better, since Gutenberg forces us to learn new technologies anyway, right now. It is an opportunity to establish a strong foundation with web standards, from the very beginning.

## Interoperability Between Sites, Homogenization Of Sites 

A block is a smaller entity than a theme or a plugin, so eventually blocks will be [accessible on their own](https://wptavern.com/gutenberg-block-library-provides-a-searchable-index-of-individual-blocks), and acquired through [newly created block markets](https://wptavern.com/gutenberg-cloud-a-cross-platform-community-library-for-custom-gutenberg-blocks). Most likely there will initially be a Cambrian explosion of blocks as many players in the ecosystem rush to be the first to market their solutions, leading on the medium and long-term towards consolidation of the most successful ones. 

Once the dust has settled, a few blocks will stand out and become the winners, obtaining most of the market on their specific categories. If/when that happens will be a cause of both concern and jubilation: concern about a new wave of [homogenization of the web](https://www.smashingmagazine.com/2018/06/bringing-personality-back-to-the-web/) taking place (as it happened with Bootstrap), as sites using the same components may end up with the same look and feel, an jubilation about an increased interoperability between sites from relying on the same components and the same APIs, which can open the gates to new opportunities.

I am particularly excited about expanding interoperability between sites. It is an area that could, in the long term, undo kingdoms such as Facebook's: instead of relying on a monopolistic gateway for sharing information, sites with different communities can easily share data among themselves, directly. This is not a new concept: the [IndieWeb](https://indieweb.org/) movement has long been working towards enabling anyone to own their own data on their own servers, by having websites talk to each other through microformats. For instance, their [Webmention](https://indieweb.org/Webmention) web standard allows two sites to have a conversation, in which each comment and response is stored in both of them, and [Micro.blog](https://micro.blog) offers a Twitter-of-sorts but based on the open web, in which the posts on the user’s timeline are gathered from RSS and JSON feeds from subscribed sites. These endeavors are wonderful, but still very small in impact, since there is some level of tech-savviness required to be part of them. Gutenberg’s component-based architecture can potentially produce a much broader impact: Popular blocks can enable scores of WordPress sites to talk to each other, eventually allowing up to 30% of all sites on the web to be part of a decentralized, loosely-coupled network.

This area will need plenty of work though, before being viable. I do not think the default REST endpoints are the best communication interface since they were not conceived for this purpose (the folks from micro.blog have proposed a better solution through their [JSON interface](https://jsonfeed.org/), which is based on the RSS specification). In addition, REST is itself being made obsolete by GraphQL, so I wouldn’t place high hopes on it for the long term. I am also involved in finding a better way, for which I am currently working on a [different type of API](https://getpop.org/en/blog/describing-the-foundations-of-the-new-pop/), which can retrieve all the required data in only one request, and supports extensibility through a component-based architecture.

I also expect integration with cloud services to be more prominent, since providers can release their own blocks to interact with their own services. Because a component is a standalone unit, just by drag-and-dropping the block into the page already does all the work from the user’s perspective, making it very easy to build powerful websites with little or no knowledge. For instance, an image storage provider like [Cloudinary](https://cloudinary.com/) could release a block that automatically crops the image according to the viewport of the device, or requests the image as WebP if supported, or other use cases. 

In summary, consolidation of the block market may bring homogenization of the way in how it looks and feels, which would be a regrettable event and should be avoided, and powerful capabilities concerning interoperability and data-sharing between sites and integration with cloud services.

## Integration With Pattern Libraries

A pattern library is a collection of user interface design elements, each of them often composed by snippets of HTML, JS, and CSS. A block is an autonomous component, often made up of bits of HTML, JS, and CSS. So blocks are evidently well-suited to be documented/built with pattern libraries. Having blocks ship their pattern libraries would be a great deal since it could enable teams not to start implementing the site’s pattern library only at the site level, but as an aggregation and refinement of the mini-pattern libraries from all the required blocks.

I believe something similar to the streamlining process for producing bloatless JavaScript packages that I mentioned earlier happens in this case, but concerning UI/UX/Documentation. It would be both a challenge and an opportunity for Gutenberg contributors to put in place a process that makes it easy for block developers to create pattern libraries for their blocks which, when aggregated all together, can result in a coherent pattern library for the site. Well implemented, such feature could drive down the costs of building sites from a documentation/maintenance perspective.

## What Will Become Of WordPress?

Gutenberg will certainly make websites more attractive, even though at the cost of a required level of expertise that not everyone will be able to handle. In the longer term, this may lead to higher quality, lower quantity. Coming from the WordPress maxim of "Democratizing Publishing," this may become a problem.

I am enthusiastic about Gutenberg, but more as the concept of a component-based architecture, than the React-based implementation. In general terms, I do agree with what Matt Mullenweg said during [WordCamp Europe 2018](https://wordpress.tv/2018/07/04/matt-mullenweg-a-summertime-update-keynote-and-qa/) to justify Gutenberg:

<blockquote>“The foundation of WordPress that is now served us well for fifteen years will not last for the next fifteen.”</blockquote>

However, I also believe that the WordPress of fifteen years into the future may end up being completely different than the one we know today. I wonder if WordPress will end up primarily being the client-based editor, and not much more: the initiative to [integrate Gutenberg into Drupal](https://drupalgutenberg.org/), with the aim of making Gutenberg become the editor of the open web, will officialize WordPress as a headless CMS operating through REST endpoints. This is a good development by itself, but it will make WordPress the back-end dispensable: if any other back-end platform provides better features, there is no reason to stick to the WordPress back-end anymore. After all, client-side Gutenberg will be able to work with any of them, while the simplicity of creating a site with WordPress will be lost, leveling the playing field with all other platforms.

In particular, I would not be surprised if developers feel that maintaining two codebases (one in JavaScript and one in PHP) for rendering dynamic blocks is too taxing, and decide to shift towards platforms which support [isomorphic server-side rendering](https://medium.com/@phoebe.greig/headache-free-isomorphic-app-tutorial-react-js-react-router-node-js-ssr-with-state-and-es6-797a8d8e493a). If this scenario actually happens, would Matt decide to shift the WordPress backend to Node.js?

It is mainly because of this issue that I dare to say that the WordPress from 15 years from now may be a very different entity than what it is nowadays. Who knows what will happen?

## Conclusion

By making components the new unit for building sites, the introduction of Gutenberg will be transformational to WordPress. And as with any paradigm shift, there will be winners and losers. Different stakeholders will consider Gutenberg a positive or negative development depending on their own situation: while the quality of a website will go up, the price of building such a site from hiring developers who can handle its complexity will also go up, making it less affordable and less popular.

These are exciting times, but also pivotal times. From now on, WordPress may slowly start being a different entity from what we are used to, and we may eventually need to think about what WordPress is, and what it represents, all over again.

{{< signature "rb, ra, yk, il" >}}
