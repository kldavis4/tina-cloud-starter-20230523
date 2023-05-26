---
title: Sassy Z-Index Management For Complex Layouts
slug: sassy-z-index-management-for-complex-layouts
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0414f874-9b1e-4c42-b275-57eb0ed23ed7/02-behance-opt-500.jpg
date: 2014-06-12T21:52:25.000Z
author: jackiebalzer
description: >-
  Z-index is an inherently tricky thing, and maintaining z-index order in a
  complex layout is notoriously difficult. With different stacking orders and
  contexts, keeping track of them as their numbers increase can be hard — and once they
  start to spread across CSS files, forget about it! Because z-index can make or
  break a UI element’s visibility and usability, keeping your website’s UI in
  working order can be a delicate balance.
categories:
  - Coding
  - Frameworks
  - CSS
  - Sass
---
Because <a href="https://www.smashingmagazine.com/2009/09/15/the-z-index-css-property-a-comprehensive-look/">z-index is contextual</a>, once you start using it, it can be easy for other elements to start requiring it as well. Finding <code>z-index: 99999</code> rules scattered throughout a website is not uncommon, but <strong>the infamous</strong> <code>99999</code> <strong>was simply born of frustration</strong>. It is often misused as an easy way to force an element above everything else, but <code>z-index</code>es are not always so straightforward. It is also not entirely scalable: What if you need to add something on top of that?

## <span class="rh">Further Reading</span> on SmashingMag:

*   [The Z-Index CSS Property: A Comprehensive Look](https://www.smashingmagazine.com/2009/09/the-z-index-css-property-a-comprehensive-look/)
*   [Extending In Sass Without Creating A Mess](https://www.smashingmagazine.com/2015/05/extending-in-sass-without-mess/)
*   [What Everyone Should Know About The Process Behind App Design](https://www.smashingmagazine.com/2016/11/what-everyone-should-know-about-the-process-behind-app-design/)
*   [Stronger, Better, Faster Design with CSS3](https://www.smashingmagazine.com/2009/12/stronger-better-faster-design-with-css3/)

Another common strategy is to <a href="https://github.com/twbs/bootstrap/blob/master/less/variables.less#L250">increment z-index values</a> by double digits, so that you have room to insert other elements later, but that doesn’t solve the problem of keeping track of them all, and it doesn’t scale well when you want to add ones in between.

{{% feature-panel %}}

Every z-index instance raises a number of questions:

1.  Why does this element have this z-index value? What does it mean in the context of every other element?
2.  Where does it fit in the order and context of other z-index values? If I increase this one, which others are affected?
3.  If I add an element to the stacking order, which z-index values do I have to increase accordingly?

## Using Sass To Maintain Order

With Sass, controlling all of the factors above is easy using lists. Let’s use <a href="https://behance.net">Behance</a>’s home page as an example:

<figure><a class="at" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/73d7890e-92b1-40f5-85d0-c173482f984c/01-behance-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4a5ce781-efea-4b90-848b-a51115713ab5/01-behance-opt-500.jpg" alt="sass z-index" width="500" height="466" /></a><figcaption>Controlling all of the factors above is easy using lists. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/73d7890e-92b1-40f5-85d0-c173482f984c/01-behance-opt.jpg">View large version</a>)</figcaption><figure>We need to maintain the stacking order of the project covers, filter bar, location search modal, custom drop-down above the modal, and website navigation, in that order, from bottom to top. We can set up a Sass list, like so:

<pre><code class="language-css">
$elements: project-covers, sorting-bar, modals, navigation;
</code></pre>

This list represents the order in which we want our elements to appear, from lowest to highest, with each index, or position, in the array representing the z-index of that element. We can use the Sass <a href="https://sass-lang.com/documentation/Sass/Script/Functions.html#index-instance_method"><code>index</code> function</a> to assign a z-index value to each element.

For example:

<pre><code class="language-css">
.project-cover {
   z-index: index($elements, project-covers);
}
</code></pre>

This would print out:

<pre><code class="language-css">
.project-cover {
   z-index: 1;
}  
</code></pre>

This is because <code>project-cover</code> is the first element in the list, at index <code>1</code>, and the lowest element in our z-index stacking order. Let’s write the Sass for the rest of the items in our list:

<pre><code class="language-css">
.sorting-bar {
   z-index: index($elements, sorting-bar);
}
.modal {
   z-index: index($elements, modals);
}
.navigation {
   z-index: index($elements, navigation);
}  
</code></pre>

Now, our compiled CSS would look like this:

<pre><code class="language-css">
.project-cover {
   z-index: 1;
}
.sorting-bar {
   z-index: 2;
}
.modal {
   z-index: 3;
}
.navigation {
   z-index: 4;
}   
</code></pre>

Now you can apply the class to your elements accordingly. But what if we want to add an element to the existing stacking order? Suppose we wanted to add a tooltip that appears when the visitor hovers over a username, above the project covers but below everything else.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/68faab86-16b0-42d1-acbc-72c4c9c4c8ba/02-behance-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0414f874-9b1e-4c42-b275-57eb0ed23ed7/02-behance-opt-500.jpg" alt="With Sass, we just have to update our list with the new element." width="500" height="387" /></a><figcaption>With Sass, we just have to update our list with the new element. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/68faab86-16b0-42d1-acbc-72c4c9c4c8ba/02-behance-opt.jpg">View large version</a>)</figcaption><figure>With vanilla CSS, this change would mean having to update the z-index values of the sorting bar, modal and navigation. With Sass, we just have to update the list with our new element:

<pre><code class="language-css">
$elements: project-covers, user-tooltip, sorting-bar, modals, navigation;   
</code></pre>

Because the z-index values of the sorting bar, modals and navigation have changed in the list (they had values of <code>2</code>, <code>3</code> and <code>4</code> but now are <code>3</code>, <code>4</code> and <code>5</code>), our compiled CSS will automatically adjust their z-index values using their new positions. Let’s add this new line of Sass:

<pre><code class="language-css">
.user-tooltip {
   z-index: index($elements, user-tooltip);
}  
</code></pre>

This will make the compiled CSS look like this:

<pre><code class="language-css">
.user-tooltip {
   z-index: 2;
}
.sorting-bar {
   z-index: 3;
}
.modal {
   z-index: 4;
}
.navigation {
   z-index: 5;
}
</code></pre>

## Scaling The Solution Across Stacking Contexts

Suppose our layout is even more complex, with multiple stacking contexts and stacking orders. (Remember that in order for an element’s z-index value to have an effect, its <code>position</code> must not be <code>static</code>. This is what creates a new stacking context, giving any children of the element a stacking order specific to its parent.) In this case, one linear list might not be sufficient. Instead, we can create as many lists as we need, each of which would be considered one context.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/529bcd0b-1297-4855-b4e3-0744977a897a/03-behance-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3015e597-f92d-4c42-ab9f-1f90d15c7309/03-behance-opt-500.jpg" alt="You can create as many lists as you need, where each list is considered one context." width="500" height="393" /></a><figcaption>Create as many lists as you need, each of which would be considered one context. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/529bcd0b-1297-4855-b4e3-0744977a897a/03-behance-opt.jpg">View large version</a>)</figcaption><figure>

<pre><code class="language-css">
$elements: project-covers, user-tooltip, sorting-bar, modals, navigation;
$modal-elements: fields, form-controls, errors, autocomplete-dropdown;

.modal {
   z-index: index($elements, modals);

   .field {
      z-index: index($modal-elements, fields);
   }
   .form-controls {
      z-index: index($modal-elements, form-controls);
   }
   .error {
      z-index: index($modal-elements, errors);
   }
   .autocomplete-dropdown {
      z-index: index($modal-elements, autocomplete-dropdown);
   }

} /* .modal */

</code></pre>

This compiles to:

<pre><code class="language-css">
.modal {
   z-index: 4;
}
.modal .field {
   z-index: 1;
}
.modal .form-controls {
   z-index: 2;
}
.modal .error {
   z-index: 3;
}
.modal .autocomplete-dropdown {
   z-index: 4;
}   
</code></pre>

## Scaling The Solution Across A Website

The most important requirement of this technique is sticking to it. Any rogue hard-coded z-index values could compromise the integrity of those derived from your list. Because of this, you might find that you need to maintain the z-index order across several pages of a website. The simplest solution is to create a partial containing your site-wide lists, which you can then include anywhere you need it. (You might already have a partial that you include everywhere that stores variables for your website’s colors, font sizes, etc. — this is the same idea.)
### _zindex.scss

<pre><code class="language-css">
$elements: project-covers, user-tooltip, sorting-bar, modals, navigation;
$modal-elements: fields, form-controls, errors, autocomplete-dropdown;   
</code></pre>

### mypage.scss

<pre><code class="language-css">
@import '_zindex.scss'

.modal {
   z-index: index($elements, modals);
}   
</code></pre>

Combining or modifying global lists per individual page is also possible. You can import your partial and then use <a href="https://sass-lang.com/documentation/Sass/Script/Functions.html#list-functions">Sass’ list functions</a> (or <a href="https://hugogiraudel.com/2013/08/08/advanced-sass-list-functions/">other advanced ones</a>) to modify as needed. For example:

<pre><code class="language-css">
@import '_zindex.scss'

$modal-elements: append($modal-elements, close-button);
$elements: insert-nth($elements, sidebar-filters, 3);

.modal .close-button {
   z-index: index($modal-elements, close-button);
}
.sidebar-filter {
   z-index: index($elements, sidebar-filter);
}   
</code></pre>

This Sass would add a “Close” button to the end of the modal stacking order and insert birds into the main stacking order of the page it’s included on, all without affecting other pages that use the <code>_zindex.scss</code> partial.
## Error-Reporting

Always check for errors in your code to avoid mistakes. For example, if you tried to get the z-index value of an item not in your list, you might find an unexpected output:

<pre><code class="language-css">
.objects {
   z-index: index($elements, thing-not-in-my-list);
}
.objects {
   z-index: false;
}
</code></pre>

Because <code>false</code> isn’t a valid value for <code>z-index</code>, we don’t want it in our compiled code. We can stop this from happening by making a custom function that acts as a proxy to the call to <code>list</code> and that uses Sass’ <code>@warn</code> to tell us whether something has gone wrong.

<pre><code class="language-css">
@function z($list, $element) {

   $z-index: index($list, $element);

   @if $z-index {
      @return $z-index;
   }

   @warn 'There is no item "#{$element}" in this list; choose one of: #{$list}';
   @return null;
}   
</code></pre>

This function takes the same arguments as <code>index</code>, but before it returns the value, it checks that we are requesting something that exists in the list. If the value exists, then it returns the result of the <code>index</code> call, just like before. If the value does not exist, then two things happen:
<ol>
 	<li>A warning is printed telling you that the item you’re requesting is not in the list, and the values of the list are printed so that you can see what to choose from.</li>
 	<li>The value returned is <code>null</code>, which tells Sass not to print out the rule at all.</li>
</ol>
So, instead of the following invalid CSS…

<pre><code class="language-css">
.objects {
   z-index: false;
}   
</code></pre>

… the <code>z-index</code> would not get printed at all. As a bonus, if it was the only rule in your rule set, then Sass would not even print the selector, thereby minimizing unnecessary output.
## Conclusion

Keeping track of stacking contexts and orders in CSS is hard, but variables in preprocessors make it much easier. There are <a href="https://css-tricks.com/handling-z-index/">many ways</a> to handle it, but the approach we’ve looked at here is intended to be the most straightforward and require the least amount of maintenance, by using simple lists of items in the order they should appear. And because Sass lists and functions are so powerful, you have endless possibilities for expanding this technique to be as comprehensive as you need!
### Resources
<ul>
 	<li>“<a href="https://www.smashingmagazine.com/2009/09/15/the-z-index-css-property-a-comprehensive-look/">The Z-Index CSS Property: A Comprehensive Look</a>,” Louis Lazaris</li>
 	<li>“<a href="https://philipwalton.com/articles/what-no-one-told-you-about-z-index/">What No One Told You About Z-Index</a>,” Philip Walton</li>
 	<li>“<a href="https://css-tricks.com/handling-z-index/">Handling Z-Index</a>,” Chris Coyier</li>
 	<li>“<a href="https://developer.mozilla.org/en-US/docs/Web/Guide/CSS/Understanding_z_index/The_stacking_context">The Stacking Context</a>,” Paolo Lombardi</li>
 	<li>“<a href="https://sass-lang.com/documentation/Sass/Script/Functions.html#list-functions">Script Functions</a>,” Sass documentation</li>
 	<li>“<a href="https://hugogiraudel.com/2013/08/08/advanced-sass-list-functions/">Advanced Sass List Functions</a>,” Kitty Giraudel</li>
</ul>

{{< signature "al, ml, il" >}}

</figure></figure></figure></figure></figure></figure>

