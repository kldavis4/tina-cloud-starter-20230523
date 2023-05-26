---
title: Five Useful CSS/jQuery Coding Techniques For More Dynamic Websites
slug: 5-coding-techniques-for-more-dynamic-websites
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2ffa6cb8-99db-4d98-8aea-a71f01964844/count.jpg
date: 2010-09-21T11:34:09.000Z
author: jon-raasch
description: >-
  Interactivity can transform a dull static website into a dynamic tool that not only delights users but conveys information more effectively. In this post, we'll walk through five different coding techniques that can be easily
  implemented on any website to provide a richer user experience. These
  techniques will allow you to better display difficult content, help users find information more effectively and provide meaningful UI cues without
  overwhelming the user: on-page text search, drag controls for oversized
  content, subtle hover effects, comment count bars and a full-page slider.
categories:
  - Coding
  - CSS
  - Techniques
  - jQuery
---
Interactivity can transform a dull static website into a dynamic tool that not only delights users but conveys information more effectively. In this post, we'll walk through five different coding techniques that can be easily implemented on any website to provide a richer user experience.

The techniques will allow you to better display difficult content, help users find information more effectively and provide meaningful UI cues without overwhelming the user.

1.  [On-page text search](#on-page-text-search)
2.  [Drag controls for oversized content](#drag-controls)
3.  [Subtle hover effects](#subtle-hover-effects)
4.  [Comment count bars](#comment-count-bars)
5.  [Full-page slider](#full-page-slider)

<a name="on-page-text-search"></a>

## 1\. On-Page Text Search

![On-page text search](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/27e6d0fd-c05c-44e3-bc9e-bf41c0ebb7d1/e-read-search-instant.gif "On-page text search")

{{% feature-panel %}}

Websites often have search boxes to allow users to find content from their archives. But what if you want to find content on the given page? Information Architects <del>has</del> had on-page text search that provides a great user experience. Let's recreate this using jQuery.</p>

### Mark-Up and Interaction

First let's build an input box for the search:

<pre><code class="language-markup tmp-html">&lt;input type="text" id="text-search" /&gt;</code></pre>

Next we'll need jQuery to attach a listener to track changes to the input box:

<pre><code class="language-javascript">$(function() {
    $('#text-search').bind('keyup change', function(ev) {
        // pull in the new value
        var searchTerm = $(this).val();
    )};
});</code></pre>

Here we bound our function to both the `keyup` and `change` events. This ensures that our operation fires regardless of whether the user types or pastes the text.

Now, let's turn to [Highlight](https://johannburkard.de/blog/programming/javascript/highlight-javascript-text-higlighting-jquery-plugin.html), a useful and lightweight jQuery plug-in that handles text highlighting. After including the plug-in source, let's add a `highlight()` call to our JavaScript:

<pre><code class="language-javascript">$(function() {
    $('#text-search').bind('keyup change', function(ev) {
        // pull in the new value
        var searchTerm = $(this).val();

        // disable highlighting if empty
        if ( searchTerm ) {
            // highlight the new term
            $('body').highlight( searchTerm );
        }
    });
});</code></pre>

In addition to highlighting the given text, we've also added a check to make sure the search term isn't empty (which causes an infinite loop).

This snippet highlights the search query throughout the page, but we can also limit the scope to a given `id`:

<pre><code class="language-javascript">$('#myId').highlight( searchTerm );</code></pre>

Or we can search only within a certain element:

<pre><code class="language-javascript">$('p').highlight( searchTerm );</code></pre>

This text highlighting by default is **case insensitive**. If you’d prefer case-sensitive highlighting, remove the `.toUpperCase()` on both lines 21 and 41 of the Highlight plug-in.</p>

### Styling the Highlighted Text

Now that the JavaScript is attached, we'll need to style our highlighted items. The Highlight plug-in wraps the highlighted terms in `<span class="highlight"></span>`, which we can style with CSS.

First, let's change the background color and then add rounded corners and a drop-shadow for all browsers except IE:

<pre><code class="language-css">.highlight {
    background-color: #fff34d;
    -moz-border-radius: 5px; /* FF1+ */
    -webkit-border-radius: 5px; /* Saf3-4 */
    border-radius: 5px; /* Opera 10.5, IE 9, Saf5, Chrome */
    -moz-box-shadow: 0 1px 4px rgba(0, 0, 0, 0.7); /* FF3.5+ */
    -webkit-box-shadow: 0 1px 4px rgba(0, 0, 0, 0.7); /* Saf3.0+, Chrome */
    box-shadow: 0 1px 4px rgba(0, 0, 0, 0.7); /* Opera 10.5+, IE 9.0 */
}</code></pre>

Although the highlighting is now visible, it still appears a bit tight around the text and could use some padding. But we'll have to be careful not to adjust the layout of text. These `span`s are inline elements, and if we simply add padding, the text will shift around on the page. So, let's include padding with a negative margin to compensate:

<pre><code class="language-css">.highlight {
    padding:1px 4px;
    margin:0 -4px;
}</code></pre>

### Finishing the Interaction

Last but not least, let's make sure to remove the highlighted text whenever the user edits text in the input box:

<pre><code class="language-javascript">$(function() {
    $('#text-search').bind('keyup change', function(ev) {
        // pull in the new value
        var searchTerm = $(this).val();

        // remove any old highlighted terms
        $('body').removeHighlight();

        // disable highlighting if empty
        if ( searchTerm ) {
            // highlight the new term
            $('body').highlight( searchTerm );
        }
    });
});</code></pre>

Here we added a call to remove any text highlighting, which is performed outside of the empty field check. This ensures that the highlight is also removed if the user clears the field.

Although `removeHighlight()` works well in most browsers, it will **crash IE6**. This is due to an [IE6 bug](https://stackoverflow.com/questions/2023255/node-normalize-crashes-in-ie6) with `node.normalize()`.

We can get the Highlight plug-in working in IE6 by rewriting this function. Simply replace lines 45-53 of `highlight.js` with the following:

<pre><code class="language-javascript">jQuery.fn.removeHighlight = function() {
 function newNormalize(node) {
    for (var i = 0, children = node.childNodes, nodeCount = children.length; i < nodeCount; i++) {
        var child = children[i];
        if (child.nodeType == 1) {
            newNormalize(child);
            continue;
        }
        if (child.nodeType != 3) { continue; }
        var next = child.nextSibling;
        if (next == null || next.nodeType != 3) { continue; }
        var combined_text = child.nodeValue + next.nodeValue;
        new_node = node.ownerDocument.createTextNode(combined_text);
        node.insertBefore(new_node, child);
        node.removeChild(child);
        node.removeChild(next);
        i--;
        nodeCount--;
    }
 }

 return this.find("span.highlight").each(function() {
    var thisParent = this.parentNode;
    thisParent.replaceChild(this.firstChild, this);
    newNormalize(thisParent);
 }).end();
};</code></pre>

This new function replaces the standard Javascript `normalize()` with a custom function that works in all browsers.

[Download the complete example.](https://gist.github.com/563055)

<a name="drag-controls"></a>

## 2\. Drag Controls For Oversized Content

[![Drag controls for oversized content](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bcc29c8b-50fb-4db5-8c94-b10b0c73c847/moscow.jpg "Drag controls for oversized content")](https://www.mospromstroy.com/)

When layout constraints bump up against the need for large images, finding a quality solution can be difficult. [Mospromstroy](https://www.mospromstroy.com/) uses a creative technique to handle this situation: a "drag and drop" control bar that allows users to pan through images.

We can accomplish something similar using jQuery UI's [draggable](https://jqueryui.com/demos/draggable/) behavior.</p>

### Mark-Up and CSS

First let's set up some mark-up for the content and controls:

<pre><code class="language-markup tmp-html">&lt;div id="full-sized-area"&gt;
    &lt;div id="full-sized-content"&gt;
    Your content here
    &lt;/div&gt;
&lt;/div&gt;

&lt;div id="drag-controls-area"&gt;
    &lt;div id="drag-controls"&gt;&lt;/div&gt;
&lt;/div&gt;</code></pre>

Next, let's apply some basic CSS:

<pre><code class="language-css">#full-sized-area {
    position: relative;
    overflow: hidden;
    width: 800px;
    height: 400px;
}

#full-sized-content {
    position: absolute;
    top: 0;
    left: 0;
}

#drag-controls-area {
    position: relative;
    width: 300px;
    height: 50px;
}

#drag-controls {
    position: absolute;
    top: 0;
    left: 0;
    height: 48px;
    border: 1px solid white;
}</code></pre>

Here we applied an `absolute` position to both the `#full-sized-content` and `#drag-controls`, and we also hid any overflow from the large image. Additionally, we applied some arbitrary dimensions to the content and drag controls wrappers; make sure to adjust these as needed.</p>

### Building Interactivity With jQuery

Now, let's use jQuery UI to build the interaction. Begin by [including jQuery UI](https://jqueryui.com/download) with the draggable module.

Before attaching the controls, let's resize the drag control box to the right dimensions:

<pre><code class="language-javascript">$(function() {
    var $fullArea = $('#full-sized-area');
    var $fullContent = $('#full-sized-content', $fullArea);

    // find what portion of the content is displayed
    var contentRatio = $fullArea.width() / $fullContent.width();

    // scale the controls box
    var $controlsArea = $('#drag-controls-area');
    var $controls = $('#drag-controls', $controlsArea);

    $controls.css('width', $controlsArea.width() * contentRatio);
});</code></pre>

Here, we've determined what portion of the content is visible in the content area and then scaled the width of the control box accordingly.

Next, let's attach the draggable behavior:

<pre><code class="language-javascript">$(function() {
    var $fullArea = $('#full-sized-area');
    var $fullContent = $('#full-sized-content', $fullArea);

    // find what portion of the content is displayed
    var contentRatio = $fullArea.width() / $fullContent.width();

    // scale the controls box
    var $controlsArea = $('#drag-controls-area');
    var $controls = $('#drag-controls', $controlsArea);

    $controls.css('width', $controlsArea.width() * contentRatio);

    // determine the scale difference between the controls and content
    var scaleRatio = $controlsArea.width() / $fullContent.width();

    // attach the draggable behavior
    $controls.draggable({
        axis : 'x', // confine dragging to the x-axis
        containment : 'parent',
        drag : function(ev, ui) {
            // move the full sized content
            $fullContent.css('left', -1 * ui.position.left / scaleRatio );
        }
    });
});</code></pre>

Here, we've attached a draggable event and set a couple options. First, we set `axis` to restrict dragging to the x-axis, and then we set `containment` to confine dragging to the parent element (i.e. the controls wrapper).

Finally, we set up a drag listener to move the full-sized content according to how far the user has dragged the control. For this, we negatively positioned the content to the left by the drag amount multiplied by the ratio of the controls to the content.</p>

### Custom Cursors

The draggable content is working, but we still have room for improvement.

First let's add some more styling to the control box to make it more interactive. jQuery UI's draggable attaches two class names that we can use for this: `ui-draggable` and `ui-draggable-dragging`.

<pre><code class="language-css">#drag-controls.ui-draggable {
    cursor: -moz-grab !important;
    cursor: -webkit-grab !important;
    cursor: e-resize;
}

#drag-controls.ui-draggable-dragging {
    cursor: -moz-grabbing !important;
    cursor: -webkit-grabbing !important;
    border-color: yellow;
}</code></pre>

In addition to applying a new border color to the active controls, this snippet also attaches a number of **cursor properties**, which use proprietary [UI cursors](https://www.gtalbot.org/DHTMLSection/Cursors.html) available in Firefox and Safari, with a back-up for IE.

Because of the implementation of the cursor property, we had to "bootstrap" this together using `!important`. This ensures that the proprietary cursors are used if available, while allowing the default cursor to overwrite them in IE. Unfortunately, Chrome does not currently support `-webkit-grab`, so we leave it out of this implementation. If you'd prefer to use the back-up `e-resize` cursor in both Chrome and Safari, just remove the `-webkit-grab` and `-webkit-grabbing` properties.</p>

### Parallax Effect

Let's make the sliding animation more three-dimensional by adding a two-layer [parallax effect](https://en.wikipedia.org/wiki/Parallax). To do so, we simply add a background to our full-sized content area and animate it at a slower rate.

Add the mark-up first:

<pre><code class="language-markup tmp-html">&lt;div id="full-sized-area"&gt;
    &lt;div id="full-sized-background"&gt;
    Your background here
    &lt;/div&gt;

    &lt;div id="full-sized-content"&gt;
    Your content here
    &lt;/div&gt;
&lt;/div&gt;

&lt;div id="drag-controls-area"&gt;
    &lt;div id="drag-controls"&gt;&lt;/div&gt;
&lt;/div&gt;</code></pre>

And then some basic styling:

<pre><code class="language-css">#full-sized-background {
    position: absolute;
    top: 0;
    left: 0;
}</code></pre>

Here, we use absolute positioning to lock the background in place. Note that we did not need to attach a [z-index](https://tjkdesign.com/articles/z-index/teach_yourself_how_elements_stack.asp), because we placed the background element before the content area in the mark-up.

Finally, let's add the background animation to our drag event:

<pre><code class="language-javascript">$fullBackground = $('#full-sized-background');

    $controls.draggable({
        axis : 'x', // confine dragging to the x-axis
        containment : 'parent',
        drag : function(ev, ui) {
            // move the full sized content
            var newContentPosition = -1 * ui.position.left / scaleRatio;
            $fullContent.css('left', newContentPosition);

            // move the background
            $fullBackground.css('left', newContentPosition * .4);
        }
    });</code></pre>

Here, we simply used the new position that we calculated for the main content and applied 40% of that change to the background. Adjust this value to change the speed of the parallax.

[Download the complete example.](https://gist.github.com/563087)

<a name="subtle-hover-effects"></a>

## 3\. Subtle Hover Effects

[![Subtle mouse effects on Veerle's blog](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a55974f2-94ed-4936-81de-124824182421/veerle.jpg "Subtle mouse effects on Veerle's blog")](https://veerle.duoh.com/)

[Veerle's blog](https://veerle.duoh.com/) uses subtle transitions to create a natural feel for mouse interactions. These can be easily accomplished using CSS3's `transition` property (and a jQuery back-up for unsupported browsers).

First, let's attach some CSS with the class `subtle` to all elements:

<pre><code class="language-css">.subtle {
    background-color: #78776C;
    color: #BBBBAD;
}

.subtle:hover, .subtle:focus {
    background-color: #F6F7ED;
    color: #51514A;
}</code></pre>

Here, we've styled these elements with a background and text color and included a hover state using the pseudo-class `:hover`. Additionally, we included the `:focus` pseudo-class for active input and text-area elements.

This CSS causes the style to change immediately on hover, but we can apply a smoother transition using CSS3:

<pre><code class="language-css">.subtle {
    -webkit-transition: background-color 500ms ease-in; /* Saf3.2+, Chrome */
    -moz-transition: background-color 500ms ease-in; /* FF3.7+ */
    -o-transition: background-color 500ms ease-in; /* Opera 10.5+ */
    transition: background-color 500ms ease-in; /* futureproofing */
    background-color: #78776C;
    color: #BBBBAD;
}

.subtle:hover, .subtle:focus {
    background-color: #F6F7ED;
    color: #51514A;
}</code></pre>

Here, we've attached a CSS3 transition that works in all modern browsers **except IE**. The `transition` property consists of three different values. The first is the CSS property to animate, and the second is the duration of the animation—in our case, `background-color` and 500 milliseconds, respectively. The third value allows us to specify an [easing function](https://james.padolsey.com/demos/jquery/easing/), such as `ease-in` or `linear`.</p>

### jQuery Back-Up

Our subtle transitions now work across a variety of browsers, but let's include support for all users by leveraging a [jQuery back-up technique](https://jonraasch.com/blog/graceful-degradation-with-css3#transition-backup).

First we'll need to detect whether the user's browser supports `transition`:

<pre><code class="language-javascript">// make sure to execute this on page load
$(function() {
    // determine if the browser supports transition
    var thisStyle = document.body.style,
    supportsTransition = thisStyle.WebkitTransition !== undefined ||
        thisStyle.MozTransition !== undefined ||
        thisStyle.OTransition !== undefined ||
        thisStyle.transition !== undefined;
});</code></pre>

Here, we check whether the body element can use any of the browser-specific transition properties that we defined above.

If the browser doesn't support `transition`, we can apply the animation using jQuery. However, jQuery's [animate()](https://api.jquery.com/animate/) function does not natively support **color-based animations**. To accommodate our `background-color` animation, we'll have to include a small chunk of [jQuery UI](https://jqueryui.com/): the effects core.

After including jQuery UI, we'll need to attach the animation to the **hover** and **focus** event listeners:

<pre><code class="language-javascript">// make sure to execute this on page load
$(function() {
    // determine if the browser supports transition
    var thisStyle = document.body.style,
    supportsTransition = thisStyle.WebkitTransition !== undefined ||
        thisStyle.MozTransition !== undefined ||
        thisStyle.OTransition !== undefined ||
        thisStyle.transition !== undefined;

    // assign jQuery transition if the browser doesn't support
    if ( ! supportsTransition ) {
        var defaultCSS = {
            backgroundColor: '#78776C'
        },
        hoverCSS = {
            backgroundColor: '#F6F7ED'
        };

        // loop through each button
        $('.subtle').each(function() {
            var $subtle = $(this);

            // bind an event listener for mouseover and focus
            $subtle.bind('mouseenter focus', function() {
                $subtle.animate(hoverCSS, 500, 'swing' );
            });

            // bind the reverse for mouseout and blur
            $subtle.bind('mouseleave blur', function(ev) {
                if ( ev.type == 'mouseleave' && ev.target == document.activeElement ) return false;

                $subtle.animate(defaultCSS, 500, 'swing' );
            });
        });
    }
});</code></pre>

Here, we recreated the transition using jQuery's `animate()`. Notice how we used values that are to the CSS3 transition—`500` specifies 500 milliseconds, and `swing` specifies an easing method that is close to `ease-in`.

While the mouse-over and focus event is fairly straightforward, notice the difference in the mouse-out and blur event. We added some code to end the function if the element is in focus. This retains the active state even if the user moves their mouse. jQuery's [is()](https://api.jquery.com/is/) method does not support the `:focus` pseudo-class, so we have to rely on DOM's `document.activeElement`.

[Download the complete example.](https://gist.github.com/563097)

<a name="comment-count-bars"></a>

## 4\. Comment Count Bars

[![Most commented posts bar representation](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/98b3fa3e-95ef-41af-bf84-e2d3959dc0a0/most-commented.gif "Most commented posts bar representation")](https://itexpertvoice.com/)

[IT Expert Voice](https://itexpertvoice.com/) uses a nice method for displaying the "Most commented" posts in its sidebar. Let's recreate this using WordPress and a bit of CSS and jQuery (non-WordPress users can skip the first section).</p>

### Pulling Posts With WordPress

Let's start by pulling in the top-five most-commented posts:

<pre><code class="language-php">&lt;?php $most_commented = new WP_Query('orderby=comment_count&amp;posts_per_page=5'); ?&gt;</code></pre>

Here, we used [WP_Query](https://codex.wordpress.org/Function_Reference/WP_Query) and a custom variable name so as not to disrupt any other post loops on the page.

Next, let's loop through the posts we've selected, outputting each as a list item:

<pre><code class="language-php">&lt;ul id="most-commented"&gt;

&lt;?php $most_commented = new WP_Query('orderby=comment_count&posts_per_page=5'); ?&gt;
	&lt;?php while ($most_commented-&gt;have_posts()) : $most_commented-&gt;the_post(); ?&gt;	

	&lt;li&gt;
	&lt;a href="&lt;?php the_permalink() ?&gt;" rel="bookmark" title="&lt;?php the_title_attribute(); ?&gt;"&gt;&lt;?php the_title(); ?&gt;&lt;/a&gt;

	&lt;span class="comment-bar"&gt;&lt;span class="comment-count"&gt;&lt;?php comments_number('0','1','%'); ?&gt;&lt;/span&gt;&lt;/span&gt;
	&lt;/li&gt;

&lt;?php endwhile; ?&gt;

&lt;/ul&gt;</code></pre>

Here, we used a `while()` loop to run through each post. First, we output a link to the post using [the_permalink()](https://codex.wordpress.org/Function_Reference/the_permalink) and [the_title()](https://codex.wordpress.org/Function_Reference/the_title), and then we output the comment count using [comments_number()](https://codex.wordpress.org/Function_Reference/comments_number) and some additional mark-up for styling.</p>

### Basic CSS Styling

Let's style the basic layout of the comments list using CSS:

<pre><code class="language-css">#most-commented li {
    list-style: none;
}

#most-commented a {
    display: block;
}</code></pre>

We've removed any list styling and defined the links as a block element so that they stay separate from our comment bar visualizations.

Let's set up some base styles for the comment bar and comment count:

<pre><code class="language-css">#most-commented .comment-bar {
    display: inline-block;
    position: relative;
    height: 30px;
    width: 0;
    margin: 5px 0;
    padding-left: 20px;
    background-color: #999;
}

#most-commented .comment-count {
    display: inline-block;
    position: absolute;
    right: -20px;
    top: -5px;
    width: 34px;
    height: 34px;
    border-width: 3px;
    border-style: solid;
    border-color: #FFF;
    -moz-border-radius: 20px;
    -webkit-border-radius: 20px;
    border-radius: 20px;
    text-align: center;
    line-height: 34px;
    background-color: #6CAC1F;
    font-size: 13px;
    font-weight: bold;
    color: #FFF;
}</code></pre>

Most of this styling is arbitrary, so feel free to attach a background image or otherwise tweak it to fit your theme. The main thing is to align the comment count to the right of the comment bar so that we can adjust the width of the bar at will.

Pay attention to the **total width** of the comment count, in our case `40px` (`34px` wide plus `3px` for the left and right borders). We're using **half** of that value to position the comment count: `20px` of negative positioning so that the count hangs on the right, and `20px` of left padding so that the comment bar reaches the center of the comment count.</p>

### Tying It All Together With jQuery

Finally, let's use jQuery to set the widths of the individual bars. We'll start by looping through the comments after the page loads:

<pre><code class="language-javascript">$(function() {
    $('#most-commented li').each(function(i) {
        var $this = $(this);
        var thisCount = ~~$this.find('.comment-count').text();
    });
});</code></pre>

We loop through all of the `<li>` elements, pulling out the **comment count** from the mark-up. Notice that we've used the [primitive data type](https://samuli.hakoniemi.net/10-small-things-you-may-not-know-about-javascript/) `~~` to convert the text to an integer. This is [significantly faster](https://web.archive.org/web/20150419121148/https://jsperf.com/integer-conversion) than alternatives such as `parseInt()`.

Let's set up some key variables in the first iteration of our loop:

<pre><code class="language-javascript">$(function() {
    // define global variables
    var maxWidth, maxCount;

    $('#most-commented li').each(function(i) {
        var $this = $(this);
        var thisCount = ~~$this.find('.comment-count').text();

        // set up some variables if the first iteration
        if ( i == 0 ) {
            maxWidth = $this.width() - 40;
            maxCount = thisCount;
        }
    });
});</code></pre>

Here, we started by defining variables outside of the `each()` loop. This allows us to use these values in every iteration.

Next, we subtracted 40 pixels from the width of the list item to define a maximum width for the comment bar. The 40 pixels compensate for the left-padding and negative position that we applied above.

We also set `maxCount` to the first value. Because we initially pulled the posts according to their number of comments, we can be sure that the first item will have the highest count.

Finally, let's calculate the width of each bar and animate the transition:

<pre><code class="language-javascript">$(function() {
    // define global variables
    var maxWidth, maxCount;

    $('#most-commented li').each(function(i) {
        var $this = $(this);
        var thisCount = ~~$this.find('.comment-count').text();

        // set up some variables if the first iteration
        if ( i == 0 ) {
            maxWidth = $this.width() - 40;
            maxCount = thisCount;
        }

        // calculate the width based on the count ratio
        var thisWidth = (thisCount / maxCount) * maxWidth;

        // apply the width to the bar
        $this.find('.comment-bar').animate({
            width : thisWidth
        }, 200, 'swing');
    });
});</code></pre>

If you'd rather style the elements without any animation, simply replace the `animate()` with a static `css()`.

[Download the complete example.](https://gist.github.com/563093)

<a name="full-page-slider"></a>

## 5\. Full-Page Slider

[![Full page slider on JaxVineyards.com](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b16bc15a-29dc-4c8e-8e05-3ba48942945d/wine-jax.jpg "Full page slider on JaxVineyards.com")](https://jaxvineyards.com/)

Sliding animation is an interactive way to show related content. But [JAX Vineyards](https://jaxvineyards.com/) takes the standard sliding gallery to the next level by animating across the entire page. Let's create a similar effect using jQuery.</p>

### Mark-Up and CSS

Start by adding the mark-up:

<pre><code class="language-markup tmp-html">&lt;div id="full-slider-wrapper"&gt;
    &lt;div id="full-slider"&gt;

        &lt;div class="slide-panel active"&gt;
        Panel 1 content here
        &lt;/div&gt;

        &lt;div class="slide-panel"&gt;
        Panel 2 content here
        &lt;/div&gt;

        &lt;div class="slide-panel"&gt;
        Panel 3 content here
        &lt;/div&gt;
    &lt;/div&gt;
&lt;/div&gt;</code></pre>

Because of the implementation of the cursor property, we had to "bootstrap" this together using `!important`. This ensures that the proprietary cursors are used if available, while allowing the default cursor to overwrite them in IE. Unfortunately, Chrome does not currently support `-webkit-grab`, so we leave it out of this implementation. If you'd prefer to use the back-up `e-resize` cursor in both Chrome and Safari, just remove the `-webkit-grab` and `-webkit-grabbing` properties.</p>

### Parallax Effect

Let's make the sliding animation more three-dimensional by adding a two-layer [parallax effect](https://en.wikipedia.org/wiki/Parallax). To do so, we simply add a background to our full-sized content area and animate it at a slower rate.

Add the mark-up first:

<pre><code class="language-markup tmp-html">&lt;div id="full-sized-area"&gt;
    &lt;div id="full-sized-background"&gt;
    Your background here
    &lt;/div&gt;

    &lt;div id="full-sized-content"&gt;
    Your content here
    &lt;/div&gt;
&lt;/div&gt;

&lt;div id="drag-controls-area"&gt;
    &lt;div id="drag-controls"&gt;&lt;/div&gt;
&lt;/div&gt;</code></pre>

And then some basic styling:

<pre><code class="language-css">#full-sized-background {
    position: absolute;
    top: 0;
    left: 0;
}</code></pre>

Here, we use absolute positioning to lock the background in place. Note that we did not need to attach a [z-index](https://tjkdesign.com/articles/z-index/teach_yourself_how_elements_stack.asp), because we placed the background element before the content area in the mark-up.

Finally, let's add the background animation to our drag event:

<pre><code class="language-javascript">$fullBackground = $('#full-sized-background');

    $controls.draggable({
        axis : 'x', // confine dragging to the x-axis
        containment : 'parent',
        drag : function(ev, ui) {
            // move the full sized content
            var newContentPosition = -1 * ui.position.left / scaleRatio;
            $fullContent.css('left', newContentPosition);

            // move the background
            $fullBackground.css('left', newContentPosition * .4);
        }
    });</code></pre>

Here, we simply used the new position that we calculated for the main content and applied 40% of that change to the background. Adjust this value to change the speed of the parallax.

[Download the complete example.](https://gist.github.com/563087)

<a name="subtle-hover-effects"></a>

## 3\. Subtle Hover Effects

[![Subtle mouse effects on Veerle's blog](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a55974f2-94ed-4936-81de-124824182421/veerle.jpg "Subtle mouse effects on Veerle's blog")](https://veerle.duoh.com/)

[Veerle's blog](https://veerle.duoh.com/) uses subtle transitions to create a natural feel for mouse interactions. These can be easily accomplished using CSS3's `transition` property (and a jQuery back-up for unsupported browsers).

First, let's attach some CSS with the class `subtle` to all elements:

<pre><code class="language-css">.subtle {
    background-color: #78776C;
    color: #BBBBAD;
}

.subtle:hover, .subtle:focus {
    background-color: #F6F7ED;
    color: #51514A;
}</code></pre>

Here, we've styled these elements with a background and text color and included a hover state using the pseudo-class `:hover`. Additionally, we included the `:focus` pseudo-class for active input and text-area elements.

This CSS causes the style to change immediately on hover, but we can apply a smoother transition using CSS3:

<pre><code class="language-css">.subtle {
    -webkit-transition: background-color 500ms ease-in; /* Saf3.2+, Chrome */
    -moz-transition: background-color 500ms ease-in; /* FF3.7+ */
    -o-transition: background-color 500ms ease-in; /* Opera 10.5+ */
    transition: background-color 500ms ease-in; /* futureproofing */
    background-color: #78776C;
    color: #BBBBAD;
}

.subtle:hover, .subtle:focus {
    background-color: #F6F7ED;
    color: #51514A;
}</code></pre>

Here, we've attached a CSS3 transition that works in all modern browsers **except IE**. The `transition` property consists of three different values. The first is the CSS property to animate, and the second is the duration of the animation—in our case, `background-color` and 500 milliseconds, respectively. The third value allows us to specify an [easing function](https://james.padolsey.com/demos/jquery/easing/), such as `ease-in` or `linear`.</p>

### jQuery Back-Up

Our subtle transitions now work across a variety of browsers, but let's include support for all users by leveraging a [jQuery back-up technique](https://jonraasch.com/blog/graceful-degradation-with-css3#transition-backup).

First we'll need to detect whether the user's browser supports `transition`:

<pre><code class="language-javascript">// make sure to execute this on page load
$(function() {
    // determine if the browser supports transition
    var thisStyle = document.body.style,
    supportsTransition = thisStyle.WebkitTransition !== undefined ||
        thisStyle.MozTransition !== undefined ||
        thisStyle.OTransition !== undefined ||
        thisStyle.transition !== undefined;
});</code></pre>

Here, we check whether the body element can use any of the browser-specific transition properties that we defined above.

If the browser doesn't support `transition`, we can apply the animation using jQuery. However, jQuery's [animate()](https://api.jquery.com/animate/) function does not natively support **color-based animations**. To accommodate our `background-color` animation, we'll have to include a small chunk of [jQuery UI](https://jqueryui.com/): the effects core.

After including jQuery UI, we'll need to attach the animation to the **hover** and **focus** event listeners:

<pre><code class="language-javascript">// make sure to execute this on page load
$(function() {
    // determine if the browser supports transition
    var thisStyle = document.body.style,
    supportsTransition = thisStyle.WebkitTransition !== undefined ||
        thisStyle.MozTransition !== undefined ||
        thisStyle.OTransition !== undefined ||
        thisStyle.transition !== undefined;

    // assign jQuery transition if the browser doesn't support
    if ( ! supportsTransition ) {
        var defaultCSS = {
            backgroundColor: '#78776C'
        },
        hoverCSS = {
            backgroundColor: '#F6F7ED'
        };

        // loop through each button
        $('.subtle').each(function() {
            var $subtle = $(this);

            // bind an event listener for mouseover and focus
            $subtle.bind('mouseenter focus', function() {
                $subtle.animate(hoverCSS, 500, 'swing' );
            });

            // bind the reverse for mouseout and blur
            $subtle.bind('mouseleave blur', function(ev) {
                if ( ev.type == 'mouseleave' && ev.target == document.activeElement ) return false;

                $subtle.animate(defaultCSS, 500, 'swing' );
            });
        });
    }
});</code></pre>

Here, we recreated the transition using jQuery's `animate()`. Notice how we used values that are to the CSS3 transition—`500` specifies 500 milliseconds, and `swing` specifies an easing method that is close to `ease-in`.

While the mouse-over and focus event is fairly straightforward, notice the difference in the mouse-out and blur event. We added some code to end the function if the element is in focus. This retains the active state even if the user moves their mouse. jQuery's [is()](https://api.jquery.com/is/) method does not support the `:focus` pseudo-class, so we have to rely on DOM's `document.activeElement`.

[Download the complete example.](https://gist.github.com/563097)

<a name="comment-count-bars"></a>

## 4\. Comment Count Bars

[![Most commented posts bar representation](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/98b3fa3e-95ef-41af-bf84-e2d3959dc0a0/most-commented.gif "Most commented posts bar representation")](https://itexpertvoice.com/)

[IT Expert Voice](https://itexpertvoice.com/) uses a nice method for displaying the "Most commented" posts in its sidebar. Let's recreate this using WordPress and a bit of CSS and jQuery (non-WordPress users can skip the first section).</p>

### Pulling Posts With WordPress

Let's start by pulling in the top-five most-commented posts:

<pre><code class="language-php">&lt;?php $most_commented = new WP_Query('orderby=comment_count&amp;posts_per_page=5'); ?&gt;</code></pre>

Here, we used [WP_Query](https://codex.wordpress.org/Function_Reference/WP_Query) and a custom variable name so as not to disrupt any other post loops on the page.

Next, let's loop through the posts we've selected, outputting each as a list item:

<pre><code class="language-php">&lt;ul id="most-commented"&gt;

&lt;?php $most_commented = new WP_Query('orderby=comment_count&posts_per_page=5'); ?&gt;
	&lt;?php while ($most_commented-&gt;have_posts()) : $most_commented-&gt;the_post(); ?&gt;	

	&lt;li&gt;
	&lt;a href="&lt;?php the_permalink() ?&gt;" rel="bookmark" title="&lt;?php the_title_attribute(); ?&gt;"&gt;&lt;?php the_title(); ?&gt;&lt;/a&gt;

	&lt;span class="comment-bar"&gt;&lt;span class="comment-count"&gt;&lt;?php comments_number('0','1','%'); ?&gt;&lt;/span&gt;&lt;/span&gt;
	&lt;/li&gt;

&lt;?php endwhile; ?&gt;

&lt;/ul&gt;</code></pre>

Here, we used a `while()` loop to run through each post. First, we output a link to the post using [the_permalink()](https://codex.wordpress.org/Function_Reference/the_permalink) and [the_title()](https://codex.wordpress.org/Function_Reference/the_title), and then we output the comment count using [comments_number()](https://codex.wordpress.org/Function_Reference/comments_number) and some additional mark-up for styling.</p>

### Basic CSS Styling

Let's style the basic layout of the comments list using CSS:

<pre><code class="language-css">#most-commented li {
    list-style: none;
}

#most-commented a {
    display: block;
}</code></pre>

We've removed any list styling and defined the links as a block element so that they stay separate from our comment bar visualizations.

Let's set up some base styles for the comment bar and comment count:

<pre><code class="language-css">#most-commented .comment-bar {
    display: inline-block;
    position: relative;
    height: 30px;
    width: 0;
    margin: 5px 0;
    padding-left: 20px;
    background-color: #999;
}

#most-commented .comment-count {
    display: inline-block;
    position: absolute;
    right: -20px;
    top: -5px;
    width: 34px;
    height: 34px;
    border-width: 3px;
    border-style: solid;
    border-color: #FFF;
    -moz-border-radius: 20px;
    -webkit-border-radius: 20px;
    border-radius: 20px;
    text-align: center;
    line-height: 34px;
    background-color: #6CAC1F;
    font-size: 13px;
    font-weight: bold;
    color: #FFF;
}</code></pre>

Most of this styling is arbitrary, so feel free to attach a background image or otherwise tweak it to fit your theme. The main thing is to align the comment count to the right of the comment bar so that we can adjust the width of the bar at will.

Pay attention to the **total width** of the comment count, in our case `40px` (`34px` wide plus `3px` for the left and right borders). We're using **half** of that value to position the comment count: `20px` of negative positioning so that the count hangs on the right, and `20px` of left padding so that the comment bar reaches the center of the comment count.</p>

### Tying It All Together With jQuery

Finally, let's use jQuery to set the widths of the individual bars. We'll start by looping through the comments after the page loads:

<pre><code class="language-javascript">$(function() {
    $('#most-commented li').each(function(i) {
        var $this = $(this);
        var thisCount = ~~$this.find('.comment-count').text();
    });
});</code></pre>

We loop through all of the `<li>` elements, pulling out the **comment count** from the mark-up. Notice that we've used the [primitive data type](https://samuli.hakoniemi.net/10-small-things-you-may-not-know-about-javascript/) `~~` to convert the text to an integer. This is [significantly faster](https://web.archive.org/web/20150419121148/https://jsperf.com/integer-conversion) than alternatives such as `parseInt()`.

Let's set up some key variables in the first iteration of our loop:

<pre><code class="language-javascript">$(function() {
    // define global variables
    var maxWidth, maxCount;

    $('#most-commented li').each(function(i) {
        var $this = $(this);
        var thisCount = ~~$this.find('.comment-count').text();

        // set up some variables if the first iteration
        if ( i == 0 ) {
            maxWidth = $this.width() - 40;
            maxCount = thisCount;
        }
    });
});</code></pre>

Here, we started by defining variables outside of the `each()` loop. This allows us to use these values in every iteration.

Next, we subtracted 40 pixels from the width of the list item to define a maximum width for the comment bar. The 40 pixels compensate for the left-padding and negative position that we applied above.

We also set `maxCount` to the first value. Because we initially pulled the posts according to their number of comments, we can be sure that the first item will have the highest count.

Finally, let's calculate the width of each bar and animate the transition:

<pre><code class="language-javascript">$(function() {
    // define global variables
    var maxWidth, maxCount;

    $('#most-commented li').each(function(i) {
        var $this = $(this);
        var thisCount = ~~$this.find('.comment-count').text();

        // set up some variables if the first iteration
        if ( i == 0 ) {
            maxWidth = $this.width() - 40;
            maxCount = thisCount;
        }

        // calculate the width based on the count ratio
        var thisWidth = (thisCount / maxCount) * maxWidth;

        // apply the width to the bar
        $this.find('.comment-bar').animate({
            width : thisWidth
        }, 200, 'swing');
    });
});</code></pre>

If you'd rather style the elements without any animation, simply replace the `animate()` with a static `css()`.

[Download the complete example.](https://gist.github.com/563093)

<a name="full-page-slider"></a>

## 5\. Full-Page Slider

[![Full page slider on JaxVineyards.com](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b16bc15a-29dc-4c8e-8e05-3ba48942945d/wine-jax.jpg "Full page slider on JaxVineyards.com")](https://jaxvineyards.com/)

Sliding animation is an interactive way to show related content. But [JAX Vineyards](https://jaxvineyards.com/) takes the standard sliding gallery to the next level by animating across the entire page. Let's create a similar effect using jQuery.</p>

### Mark-Up and CSS

Start by adding the mark-up:

<pre><code class="language-markup tmp-html">&lt;div id="full-slider-wrapper"&gt;
    &lt;div id="full-slider"&gt;

        &lt;div class="slide-panel active"&gt;
        Panel 1 content here
        &lt;/div&gt;

        &lt;div class="slide-panel"&gt;
        Panel 2 content here
        &lt;/div&gt;

        &lt;div class="slide-panel"&gt;
        Panel 3 content here
        &lt;/div&gt;
    &lt;/div&gt;
&lt;/div&gt;</code></pre>

We set up the basic mark-up and wrappers that we need for the animation. Make sure that the `full-slider-wrapper` is not contained in any element that is narrower than the browser window—we'll need the full width of the browser to pull off the effect.

Now, let's add some basic CSS to handle overflow and to position the panels:

<pre><code class="language-css">html {
    min-width: 800px;
}

#full-slider-wrapper {
    overflow: hidden;
}

#full-slider {
    position: relative;
    width: 800px;
    height: 600px;
    margin: 0 auto;
}

#full-slider .slide-panel {
    position: absolute;
    top: 0;
    left: 0;
    width: 800px;
    height: 600px;
    visibility: hidden;
}

#full-slider .slide-panel.active {
    visibility: visible;
}</code></pre>

We defined absolute positioning and set up some arbitrary dimensions for the panels and wrapper. Feel free to tweak these dimensions to your content.

We also attached `overflow: hidden` to our wrapper element, which will **prevent scroll bars** from appearing when we animate the panels. Because we hid the overflow, we also had to assign a `min-width` to the `html` document. This ensures that the content will get scroll bars if the browser window is too small.

Finally, we used the `active` class that we established in the mark-up to show the first panel.</p>

### jQuery Animation

Let's build the interaction using jQuery. We'll start by defining some variables and then create a function to handle the sliding animation in both directions:

<pre><code class="language-javascript">$(function() {
    var $slider = $('#full-slider');
    var $sliderPanels = $slider.children('.slide-panel');

    function slidePanel( newPanel, direction ) {
        // define the offset of the slider obj, vis a vis the document
        var offsetLeft = $slider.offset().left;

        // offset required to hide the content off to the left / right
        var hideLeft = -1 * ( offsetLeft + $slider.width() );
        var hideRight = $(window).width() - offsetLeft;

        // change the current / next positions based on the direction of the animation
        if ( direction == 'left' ) {
            currPos = hideLeft;
            nextPos = hideRight;
        }
        else {
            currPos = hideRight;
            nextPos = hideLeft;
        }

        // slide out the current panel, then remove the active class
        $slider.children('.slide-panel.active').animate({
            left: currPos
        }, 500, function() {
            $(this).removeClass('active');
        });

        // slide in the next panel after adding the active class
        $( $sliderPanels[newPanel] ).css('left', nextPos).addClass('active').animate({
            left: 0
        }, 500 );
    }
});</code></pre>

Here our `slidePanel()` function accepts two arguments: the index of the panel that we want to slide into view, and the direction of the slide (i.e. left or right).

Although this function looks complicated, the concepts are fairly simple. We determined the amount of offset necessary to hide the panels on the left and right sides. To calculate these values, we used jQuery's [offset()](https://api.jquery.com/offset/) and the slider and window widths. These offsets represent the `left` position values needed to hide the content on either side.

Next, we have a switch based on the direction of the animation, which uses the two values we defined previously.

<p>Finally, we trigger the animation using jQuery's <a href="https://api.jquery.com/animate/">animate()</a>. We slide the active panel out of view and then remove the <code>active</code> class once the animation completes. Then we set the new panel's left position off the screen, attach the active class to make it visible and slide it into place.

### Building the Controls

<p>Our function now handles the animation, but we still have to build controls to leverage it.</p>

<p>Append navigation elements to the slider object that we defined previously:</p>

<pre><code class="language-javascript">var $navWrap = $('&lt;div id="full-slider-nav"&gt;&lt;/div&gt;').appendTo( $slider );
    var $navLeft = $('&lt;div id="full-slider-nav-left"&gt;&lt;/div&gt;').appendTo( $navWrap );
    var $navRight = $('&lt;div id="full-slider-nav-right"&gt;&lt;/div&gt;').appendTo( $navWrap );</code></pre>

<p>We could have included this navigation in the initial mark-up, but we're appending it with JavaScript for two reasons: it ensures that the navigation won't appear until the JavaScript is loaded, and it keeps the navigation from being displayed on the off chance that JavaScript isn't enabled.</p>

<p>Let's style the navigation:</p>

<pre><code class="language-css">#full-slider-nav {
    position: absolute;
    top: 0;
    right: 0;
}

#full-slider-nav-left, #full-slider-nav-right {
    display: inline-block;
    height: 0;
    width: 0;
    margin-left: 15px;
    border: 20px solid transparent;
    cursor: pointer;
}

#full-slider-nav-left {
    border-right-color: #BBB;
}

#full-slider-nav-left:hover {
    border-right-color: #999;
}

#full-slider-nav-right {
    border-left-color: #BBB;
}

#full-slider-nav-right:hover {
    border-left-color: #999;
}</code></pre>

<p>Here we <code>absolute</code> position the navigation to the top right. We also use a <a href="https://www.dinnermint.org/css/creating-triangles-in-css/">CSS triangle trick</a> to quickly style the controls.</p>

<p>Let's attach our new slider navigation to the <code>slidePanel()</code> function that we defined previously:</p>

<pre><code class="language-javascript">var $navWrap = $('&lt;div id="full-slider-nav"&gt;&lt;/div&gt;').appendTo( $slider );
    var $navLeft = $('&lt;div id="full-slider-nav-left"&gt;&lt;/div&gt;').appendTo( $navWrap );
    var $navRight = $('&lt;div id="full-slider-nav-right"&gt;&lt;/div&gt;').appendTo( $navWrap );

    var currPanel = 0;

    $navLeft.click(function() {
        currPanel--;

        // check if the new panel value is too small
        if ( currPanel &lt; 0 ) currPanel = $sliderPanels.length - 1;

        slidePanel(currPanel, 'right');
    });

    $navRight.click(function() {
        currPanel++;

        // check if the new panel value is too big
        if ( currPanel &gt;= $sliderPanels.length ) currPanel = 0;

        slidePanel(currPanel, 'left');
    });</code></pre>

<p>This snippet assigns click events to the left and right navigation. In each, we change the value of <code>currPanel</code> according to the direction. If this new value falls outside of the available panels, we loop to the other end of our set. Finally, we trigger the <code>slidePanel()</code> function with the new panel and appropriate direction.</p>

<p>In our example, we built controls only for left and right navigation, but you could easily tweak this to have buttons for each panel. Simply pass the correct panel index to <code>slidePanel</code>.</p>

<p>Let's bring all the jQuery code together:</p>

<pre><code class="language-javascript">$(function() {
    function slidePanel( newPanel, direction ) {
        // define the offset of the slider obj, vis a vis the document
        var offsetLeft = $slider.offset().left;

        // offset required to hide the content off to the left / right
        var hideLeft = -1 * ( offsetLeft + $slider.width() );
        var hideRight = $(window).width() - offsetLeft;

        // change the current / next positions based on the direction of the animation
        if ( direction == 'left' ) {
            currPos = hideLeft;
            nextPos = hideRight;
        }
        else {
            currPos = hideRight;
            nextPos = hideLeft;
        }

        // slide out the current panel, then remove the active class
        $slider.children('.slide-panel.active').animate({
            left: currPos
        }, 500, function() {
            $(this).removeClass('active');
        });

        // slide in the next panel after adding the active class
        $( $sliderPanels[newPanel] ).css('left', nextPos).addClass('active').animate({
            left: 0
        }, 500 );
    }

    var $slider = $('#full-slider');
    var $sliderPanels = $slider.children('.slide-panel');

    var $navWrap = $('&lt;div id="full-slider-nav"&gt;&lt;/div&gt;').appendTo( $slider );
    var $navLeft = $('&lt;div id="full-slider-nav-left"&gt;&lt;/div&gt;').appendTo( $navWrap );
    var $navRight = $('&lt;div id="full-slider-nav-right"&gt;&lt;/div&gt;').appendTo( $navWrap );

    var currPanel = 0;

    $navLeft.click(function() {
        currPanel--;

        // check if the new panel value is too small
        if ( currPanel &lt; 0 ) currPanel = $sliderPanels.length - 1;

        slidePanel(currPanel, 'right');
    });

    $navRight.click(function() {
        currPanel++;

        // check if the new panel value is too big
        if ( currPanel &gt;= $sliderPanels.length ) currPanel = 0;

        slidePanel(currPanel, 'left');
    });
});</code></pre>

<p><a href="https://gist.github.com/563040">Download the complete example.</a></p>

## Final Thoughts

<p>In this post we walked through a variety of methods for adding dynamic functionality to your websites.  These techniques can be easily adapted to work with almost any site. The majority of these techniques rely on jQuery to provide interaction, but there are plenty of other approaches, both with and without jQuery.  Please post any alternate solutions in the comments below, or fork the example files on github.</p>

<p>Furthermore, these five methods represent only a small portion of interactive techniques.  Please post any links to other dynamic techniques and functionality in the comments below.</p>

## Related Posts
<p>You may be interested in the following related posts:</p>
<ul>
<li><a href="https://www.smashingmagazine.com/2008/08/11/5-useful-coding-solutions-for-designers-and-developers/">Useful Coding Solutions For Designers and Developers (part 1)</a></li>
<li><a href="https://www.smashingmagazine.com/2009/11/23/6-useful-coding-solutions-for-designers-and-developers/">Useful Coding Solutions For Designers and Developers (part 2)</a></li>
</ul>

{{< signature "al" >}}
[twcount]

