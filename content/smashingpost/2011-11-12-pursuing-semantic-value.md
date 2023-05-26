---
title: Pursuing Semantic Value
slug: pursuing-semantic-value
image: 'https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/21fab4e4-9ae6-4111-b4dc-b0def16805b1/semantic-grid1.jpg'
date: 2011-11-12T13:35:44.000Z
author: jeremy-keith
description: >-
  Divya Manian, one of the super-smart web warriors behind _HTML5 Boilerplate_, has published an article called [Our Pointless Pursuit Of Semantic Value](https://www.smashingmagazine.com/2011/11/11/our-pointless-pursuit-of-semantic-value/).
categories:
  - Coding
  - HTML5
  - HTML
  - Semantics
---
**Disclaimer**: This post by Jeremy Keith is [one](https://adactio.com/journal/4999/) [of](https://dbushell.com/2011/11/11/in-favour-of-semantics/) the [many](https://www.stuffandnonsense.co.uk/blog/about/our_pointless_pursuit_of_semantic_value) reactions to our [recent article](https://www.smashingmagazine.com/2011/11/11/our-pointless-pursuit-of-semantic-value/) on the pursuit of semantic value by Divya Manian. Both articles are published in the _Opinion column_ section in which we provide active members of the community with the opportunity to share their thoughts and ideas publicly.

I’m afraid I have to agree with [Patrick’s comment](https://www.smashingmagazine.com/2011/11/11/our-pointless-pursuit-of-semantic-value/) when he says that the abrasive title, the confrontational tone and strawman arguments at the start of the article make it hard to get to the real message.

But if you can get past the blustery tone and get to the kernel of the article, it’s a fairly straightforward message: don’t get too hung up on semantics to the detriment of other important facets of web development. Divya clarifies this in [a comment](https://www.smashingmagazine.com/2011/11/11/our-pointless-pursuit-of-semantic-value/):

<blockquote>
  <p>Amen, this is the message the article gets to. Not semantics are useless but its not worth worrying over minute detail on.</p>
</blockquote>

{{% feature-panel %}}

The specific example of `div`s and sectioning content is troublesome though. There **is** a difference between a `div` and a `section` or `article` (or `aside` or `nav`). I don’t just mean the semantic difference (a `div` conveys no meaning about the contained content whereas a `section` element is specifically for enclosing _thematically-related_ content). There are also practical differences.

A `section` element will have an effect on the generated outline for a document (a `div` will not). The new outline algorithm in HTML5 will make life a lot easier for future assistive technology and searchbots (as other people mentioned in the comments) but it already has practical effects today in some browsers in their default styling.

Download the HTML document I’ve thrown up at [https://gist.github.com/1360458](https://gist.github.com/1360458) and open it in the latest version of Safari, Chrome or Firefox. You’ll notice that the same element (`h1`) will have different styling depending on whether it is within a `div` or within a `section` element (thanks to `-moz-any` and `-webkit-any` CSS declarations in the browser’s default stylesheets).

So that’s one illustration of the practical difference between `div` and `section`.

Now with that said, I somewhat concur with the conclusion of “when in doubt, just use a div”. I see far too many documents where every `div` has been swapped out for a `section` or an `article` or a `nav` or an `aside`. But my reason for coming to that conclusion is the polar opposite of Divya’s reasoning. Whereas Divya is saying there is effectively no difference between using a `div` and using sectioning content, the opposite is the case: it makes a big difference to the document’s outline. So if you use a `section` or `article` or `aside` or `nav` without realising the consequences, the results could be much worse than if you had simply used a `div`.

I also agree that there’s a balance to be struck in the native semantics of HTML. In many ways its power comes from the fact that it is a limited—but universally understood by browsers—set of semantics. If we had an element for every possible type of content, the language would be useless. Personally, I’m not convinced that we need a `section` element _and_ an `article` element: the semantics of those two elements are so close as to be practically identical.

And that’s the reason why right now is _exactly_ the time for web developers to be thinking about semantics. The specification is still being put together and our collective voice matters. If we want to have well-considered semantic elements in the language, we need to take the time to consider the effects of every new element that could potentially be used to structure our content.

So I will continue to stop and think when it comes to choosing elements and class names just as much as I would sweat the details of visual design or the punctation in my copy or the coding style of my JavaScript.

{{< signature "vf" >}}

