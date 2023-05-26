---
title: 'Best Practices With CSS Grid Layout'
slug: best-practices-grid-layout
author: rachel-andrew
image: >-
  //archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/df8d1430-5e25-47f3-a26c-e0b977c9e435/fr-min-auto.png
date: 2018-04-16T13:35:19+02:00
summary: >-
  In some ways, we are all still so new to CSS Grid Layout. A lot of folks keep asking about best practices that are available out there. Rachel Andrew ran a survey and shares the results as well as her thoughts in this article.
description: >-
  In some ways, we are all still so new to CSS Grid Layout. A lot of folks keep asking about best practices that are available out there. Rachel Andrew ran a survey and shares the results as well as her thoughts in this article.
categories:
  - CSS
  - CSS Grid
  - Layouts
  - Browsers
---
An increasingly common question &mdash; now that people are using CSS Grid Layout in production &mdash; seems to be “What are the best practices?” The short answer to this question is to use the layout method as defined in the specification. The particular parts of the spec you choose to use, and indeed how you combine Grid with other layout methods such as Flexbox, is down to what works for the patterns you are trying to build and how you and your team want to work.

Looking deeper, I think perhaps this request for “best practices” perhaps indicates a lack of confidence in using a layout method that is very different from what came before. Perhaps a concern that we are using Grid for things it wasn’t designed for, or not using Grid when we should be. Maybe it comes down to worries about supporting older browsers, or in how Grid fits into our development workflow.

In this article, I’m going to try and cover some of the things that either could be described as best practices, and some things that you probably don’t need to worry about.

## The Survey

To help inform this article, I wanted to find out how other people were using Grid Layout in production, what were the challenges they faced, what did they really enjoy about it? Were there common questions, problems or methods being used. To find out, I put together a quick survey, asking questions about how people were using Grid Layout, and in particular, what they most liked and what they found challenging.

In the article that follows, I’ll be referencing and directly quoting some of those responses. I’ll also be linking to lots of other resources, where you can find out more about the techniques described. As it turned out, there was far more than one article worth of interesting things to unpack in the survey responses. I’ll address some of the other things that came up in a future post.

{{% feature-panel %}}

## Accessibility

If there is any part of the Grid specification that you need to take care when using, it is when using anything that could cause content re-ordering:

<blockquote>“Authors must use order and the grid-placement properties only for visual, not logical, reordering of content. Style sheets that use these features to perform logical reordering are non-conforming.”<br /><br />&mdash; <a href="https://www.w3.org/TR/css-grid-1/#order-accessibility">Grid Specification: Re-ordering and Accessibility</a></blockquote>

This is not unique to Grid, however, the ability to rearrange content so easily in two dimensions makes it a bigger problem for Grid. However, if using any method that allows content re-ordering &mdash; be that Grid, Flexbox or even absolute positioning &mdash; you need to take care not to disconnect the visual experience from how the content is structured in the document. Screen readers (and people navigating around the document using a keyboard only) are going to be following the order of items in the source.

The places where you need to be particularly careful are when using `flex-direction` to reverse the order in Flexbox; the `order` property in Flexbox or Grid; any placement of Grid items using any method, if it moves items out of the logical order in the document; and using the dense packing mode of `grid-auto-flow`. 

For more information on this issue, see the following resources:

- [Grid Layout and Accessibility - MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Grid_Layout/CSS_Grid_Layout_and_Accessibility)
- [Flexbox and the keyboard navigation disconnect](https://tink.uk/flexbox-the-keyboard-navigation-disconnect/)

## Which Grid Layout Methods Should I Use?

<blockquote>”With so much choice in Grid, it was a challenge to stick to a consistent way of writing it (e.g. naming grid lines or not, defining grid-template-areas, fallbacks, media queries) so that it would be maintainable by the whole team.”<br /><br />&mdash; <a href="https://twitter.com/mbarker_84">Michelle Barker</a></blockquote>

When you first take a look at Grid, it might seem overwhelming with so many different ways of creating a layout. Ultimately, however, it all comes down to things being positioned from one line of the grid to another. You have choices based on the of layout you are trying to achieve, as well as what works well for your team and the site you are building. 

There is no right or wrong way. Below, I will pick up on some of the common themes of confusion. I've also already covered many other potential areas of confusion in a previous article “[Grid Gotchas and Stumbling Blocks](https://www.smashingmagazine.com/2017/09/css-grid-gotchas-stumbling-blocks/).”

### Should I Use An Implicit Or Explicit Grid?

The grid you define with `grid-template-columns` and `grid-template-rows` is known as the Explicit Grid. The Explicit Grid enables the naming of lines on the Grid and also gives you the ability to target the end line of the grid with `-1`. You’ll choose an Explicit Grid to do either of these things and in general when you have a layout all designed and know exactly where your grid lines should go and the size of the tracks.

I use the Implicit Grid most often for row tracks. I want to define the columns but then rows will just be auto-sized and grow to contain the content. You can control the Implicit Grid to some extent with `grid-auto-columns` and `grid-auto-rows`, however, you have less control than if you are defining everything. 

You need to decide whether you know exactly how much content you have and therefore the number of rows and columns &mdash; in which case you can create an Explicit Grid. If you do not know how much content you have, but simply want rows or columns created to hold whatever there is, you will use the Implicit Grid. 

Nevertheless, it's possible to combine the two. In the below CSS, I have defined three columns in the Explicit Grid and three rows, so the first three rows of content will be the following:

- A track of at least 200px in height, but expanding to take content taller,
- A track fixed at 400px in height,
- A track of at least 300px in height (but expands).

Any further content will go into a row created in the Implicit Grid, and I am using the `grid-auto-rows` property to make those tracks at least 300px tall, expanding to `auto`.

<pre><code class="language-css">.grid {  
  display: grid;  
  grid-template-columns: 1fr 3fr 1fr;  
  grid-template-rows: minmax(200px auto) 400px minmax(300px, auto);  
  grid-auto-rows: minmax(300px, auto);  
  grid-gap: 20px;  
}</code></pre>

### A Flexible Grid With A Flexible Number Of Columns

By using Repeat Notation, autofill, and minmax you can create a pattern of as many tracks as will fit into a container, thus removing the need for Media Queries to some extent. This technique can be found in [this video tutorial](https://gridbyexample.com/video/series-auto-fill-auto-fit/), and also demonstrated along with similar ideas in my recent article “[Using Media Queries For Responsive Design In 2018](https://www.smashingmagazine.com/2018/02/media-queries-responsive-design-2018/).”

Choose this technique when you are happy for content to drop below earlier content when there is less space, and are happy to allow a lot of flexibility in sizing. You have specifically asked for your columns to display with a minimum size, and to **auto fill**.

There were a few comments in the survey that made me wonder if people were choosing this method when they really wanted a grid with a fixed number of columns. If you are ending up with an unpredictable number of columns at certain breakpoints, you might be better to set the number of columns &mdash; and redefine it with media queries as needed &mdash; rather than using `auto-fill` or `auto-fit`.

### Which Method Of Track Sizing Should I Use?

I described track sizing in detail in my article “[How Big Is That Box? Understanding Sizing In Grid Layout](https://www.smashingmagazine.com/2018/01/understanding-sizing-css-layout/),” however, I often get questions as to which method of track sizing to use. Particularly, I get asked about the difference between percentage sizing and the `fr` unit.

If you simply use the `fr` unit as specced, then it differs from using a percentage because it distributes available space. If you place a larger item into a track then the way the `fr` until will work is to allow that track to take up more space and distribute what is left over.

<pre><code class="language-css">.grid {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
  grid-gap: 20px;
}
</code></pre>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/df8d1430-5e25-47f3-a26c-e0b977c9e435/fr-min-auto.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/df8d1430-5e25-47f3-a26c-e0b977c9e435/fr-min-auto.png" sizes="100vw" caption="The first column is wider as Grid has assigned it more space." alt="A three column layout, the first column is wider" >}}

To cause the `fr` unit to distribute **all** of the space in the grid container you need to give it a minimum size of `0` using `minmax()`.

<pre><code class="language-css">.grid {
    display: grid;
    grid-template-columns: minmax(0,1fr) minmax(0,1fr) minmax(0,1fr);
    grid-gap: 20px;
}</code></pre>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/02a0ded5-9fdc-47ed-850f-9abc4e324fe7/fr-min0.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/02a0ded5-9fdc-47ed-850f-9abc4e324fe7/fr-min0.png" sizes="100vw" caption="Forcing a 0 minimum may cause overflows" alt="three equal columns with the first overflowing" >}}

So you can choose to use `fr` in either of these scenarios: ones where you do want space distribution from a basis of auto (the default behavior), and those where you want equal distribution. I would typically use the `fr` unit as it then works out the sizing for you, and enables the use of fixed width tracks or gaps. The only time I use a percentage instead is when I am adding grid components to an existing layout that uses other layout methods too. If I want my grid components to line up with a float- or flex-based layout which is using percentages, using them in my grid layout means everything uses the same sizing method.

### Auto-Place Items Or Set Their Position?

You will often find that you only need to place one or two items in your layout, and the rest fall into place based on content order. In fact, this is a really good test that you haven’t disconnected the source and visual display. If things pretty much drop into position based on auto-placement, then they are probably in a good order.

Once I have decided where everything goes, however, I do tend to assign a position to everything. This means that I don’t end up with strange things happening if someone adds something to the document and grid auto-places it somewhere unexpected, thus throwing out the layout. If everything is placed, Grid will put that item into the next available empty grid cell. That might not be exactly where you want it, but sat down at the end of your layout is probably better than popping into the middle and pushing other things around.

### Which Positioning Method To Use?

When working with Grid Layout, ultimately everything comes down to placing items from one line to another. Everything else is essentially a helper for that.

Decide with your team if you want to name lines, use Grid Template Areas, or if you are going to use a combination of different types of layout. I find that I like to use Grid Template Areas for small components in particular. However, there is no right or wrong. Work out what is best for you.

## Grid In Combination With Other Layout Mechanisms

Remember that Grid Layout isn’t the one true layout method to rule them all, it’s designed for a certain type of layout &mdash; namely two-dimensional layout. Other layout methods still exist and you should consider each pattern and what suits it best.

I think this is actually quite hard for those of us used to hacking around with layout methods to make them do something they were not really designed for. It is a really good time to take a step back, look at the layout methods for the tasks they were designed for, and remember to use them for those tasks.

In particular, no matter how often I write about Grid versus Flexbox, I will be asked which one people *should* use. There are many patterns where either layout method makes perfect sense and it really is up to you. No-one is going to shout at you for selecting Flexbox over Grid, or Grid over Flexbox. 

In my own work, I tend to use Flexbox for components where I want the natural size of items to strongly control their layout, essentially pushing the other items around. I also often use Flexbox because I want alignment, given that the Box Alignment properties are only available to use in Flexbox and Grid. I might have a Flex container with one child item, in order that I can align that child.

A sign that perhaps Flexbox isn’t the layout method I should choose is when I start adding percentage widths to flex items and setting `flex-grow` to 0. The reason to add percentage widths to flex items is often because I’m trying to line them up in two dimensions (lining things up in two dimensions is exactly what Grid is for). However, try both, and see which seems to suit the content or design pattern best. You are unlikely to be causing any problems by doing so.

## Nesting Grid And Flex Items

This also comes up a lot, and there is absolutely no problem with making a Grid Item also a Grid Container, thus nesting one grid inside another. You can do the same with Flexbox, making a Flex Item and Flex Container. You can also make a Grid Item and Flex Container or a Flex Item a Grid Container &mdash; none of these things are a problem!

What we can’t currently do is nest one grid inside another and have the nested grid use the grid tracks defined on the overall parent. This would be very useful and is what the subgrid proposals in [Level 2 of the Grid Specification](https://drafts.csswg.org/css-grid-2/) hope to solve. A nested grid currently becomes a new grid so you would need to be careful with sizing to ensure it aligns with any parent tracks. 

## You Can Have Many Grids On One Page

A comment popped up a few times in the survey which surprised me, there seems to be an idea that a grid should be confined to the main layout, and that many grids on one page were perhaps not a good thing. **You can have as many grids as you like!** Use grid for big things and small things, if it makes sense laid out as a grid then use Grid.

## Fallbacks And Supporting Older Browsers

<blockquote>“Grid used in conjunction with @supports has enabled us to better control the number of layout variations we can expect to see. It has also worked really well with our progressive enhancement approach meaning we can reward those with modern browsers without preventing access to content to those not using the latest technology.”<br /><br />&mdash; <a href="https://twitter.com/joelambert">Joe Lambert</a> working on <a href="https://www.rareloop.com">rareloop.com</a></blockquote>

In the survey, many people mentioned older browsers, however, there was a reasonably equal split between those who felt that supporting older browsers was hard and those who felt it was easy due to Feature Queries and the fact that Grid overrides other layout methods. I’ve written at length about the mechanics of creating these fallbacks in “[Using CSS Grid: Supporting Browsers Without Grid](https://www.smashingmagazine.com/2017/11/css-grid-supporting-browsers-without-grid/).”

In general, modern browsers are far more interoperable than their earlier counterparts. We tend to see far fewer actual “browser bugs” and if you use HTML and CSS correctly, then you will generally find that what you see in one browser is the same as in another.

We do, of course, have situations in which one browser has not yet shipped support for a certain specification, or some parts of a specification. With Grid, we have been very fortunate in that browsers shipped Grid Layout in a very complete and interoperable way within a short time of each other. Therefore, our considerations for testing tend to be to need to test browsers with Grid and without Grid. You may also have chosen to use the `-ms` prefixed version in IE10 and IE11, which would then require testing as a third type of browser.

Browsers which support modern Grid Layout (not the IE version) also support Feature Queries. This means that you can test for Grid support before using it.

## Testing Browsers That Don’t Support Grid

When using fallbacks for browsers without support for Grid Layout (or using the `-ms` prefixed version for IE10 and 11), you will want to test how those browsers render Grid Layout. To do this, you need a way to view your site in an example browser.

I would not take the approach of breaking your Feature Query by checking for support of something nonsensical, or misspelling the value `grid`. This approach will only work if your stylesheet is incredibly simple, and you have put absolutely everything to do with your Grid Layout inside the Feature Queries. This is a very fragile and time-consuming way to work, especially if you are extensively using Grid. In addition, an older browser will not just lack support for Grid Layout, there will be other CSS properties unsupported too. If you are looking for “best practice” then setting yourself up so you are in a good position to test your work is high up there!

There are a couple of straightforward ways to set yourself up with a proper method of testing your fallbacks. The easiest method &mdash; if you have a reasonably fast internet connection and don’t mind paying a subscription fee &mdash; is to use a service such as BrowserStack. This is a service that enables viewing of websites (even those in development on your computer) on a whole host of real browsers. BrowserStack does offer [free accounts for open-source projects](https://www.browserstack.com/open-source). 

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8b054565-b4ed-4c06-a209-c14c3188ab75/ie-vms.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8b054565-b4ed-4c06-a209-c14c3188ab75/ie-vms.png" sizes="100vw" caption="You can download Virtual Machines for testing from Microsoft." alt="Screenshot of the download page" >}}

To test locally, my suggestion would be to use a Virtual Machine with your target browser installed. Microsoft offers free [Virtual Machine downloads](https://developer.microsoft.com/en-us/microsoft-edge/tools/vms/) with versions of IE back to IE8, and also Edge. You can also install onto the VM an older version of a browser with no Grid support at all. [For example by getting a copy of Firefox 51 or below](https://ftp.mozilla.org/pub/firefox/releases/). After installing your elderly Firefox, be sure to [turn off automatic updates as explained here](https://support.mozilla.org/en-US/kb/install-older-version-of-firefox) as otherwise it will quietly update itself!

You can then test your site in IE11 and in non-supporting Firefox on one VM (a far less fragile solution than misspelling values). Getting set up might take you an hour or so, but you’ll then be in a really good place to test your fallbacks.

## Unlearning Old Habits

<blockquote>“It was my first time to use Grid Layout, so there were a lot of concepts to learn and properties understand. Conceptually, I found the most difficult thing to unlearn all the stuff I had done for years, like clearing floats and packing everything in container divs.”<br /><br />&mdash; <a href="https://twitter.com/hdv">Hidde</a> working on <a href="https://hiddedevries.nl/en">hiddedevries.nl/en</a></blockquote>

Many of the people responding to the survey mentioned the need to unlearn old habits and how learning Layout would be easier for people completely new to CSS. I tend to agree. When teaching people in person complete beginners have little problem using Grid while experienced developers try hard to return grid to a one-dimensional layout method. I’ve seen attempts at “grid systems” using CSS Grid which add back in the row wrappers needed for a float or flex-based grid. 

**Don’t be afraid to try out new techniques**. If you have the ability to test in a few browsers and remain mindful of potential issues of accessibility, you really can’t go too far wrong. And, if you find a great way to create a certain pattern, let everyone else know about it. We are all new to using Grid in production, so there is certainly plenty to discover and share.

<blockquote>“Grid Layout is the most exciting CSS development since media queries. It's been so well thought through for real-world developer needs and is an absolute joy to use in production - for designers and developers alike.”<br /><br />&mdash; <a href="https://twitter.com/trysmudford">Trys Mudford</a> working on <a href="https://www.trysmudford.com">trysmudford.com</a></blockquote>

To wrap up, here is a very short list of current best practices! If you have discovered things that do or don’t work well in your own situation, add them to the comments.

1. Be very aware of the possibility of content re-ordering. Check that you have not disconnected the visual display from the document order. 
2. Test using real target browsers with a local or remote Virtual Machine.
3. Don’t forget that older layout methods are still valid and useful. Try different ways to achieve patterns. Don’t be hung up on having to use Grid.
4. Know that as an experienced front-end developer you are likely to have a whole set of preconceptions about how layout works. Try to look at these new methods anew rather than forcing them back into old patterns.
5. Keep trying things out. We’re all new to this. Test your work and share what you discover.

{{< signature "il" >}}

