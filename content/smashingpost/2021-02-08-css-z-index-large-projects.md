---
title: 'Managing CSS Z-Index In Large Projects'
slug: css-z-index-large-projects
author: steven-frieson
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fdfb1a51-46fd-4196-87b7-3ca6c98dd9e7/css-z-index-large-projects.jpg
date: 2021-02-08T12:00:13.000Z
summary: >-
  Wrangling z-index values is a difficult task for many developers. Here is an easy-to-implement mini-framework based on existing conventions that brings clarity and confidence to working with z-index.
description: >-
  Wrangling z-index values is a difficult task for many developers. Here is an easy-to-implement mini-framework based on existing conventions that brings clarity and confidence to working with z-index.
categories:
  - CSS
  - Techniques
  - Tools
---

There are several articles that explain z-index ([here’s a good one](https://philipwalton.com/articles/what-no-one-told-you-about-z-index/)), since it continues to trip up developers of all experience levels. I do not think that the number of articles is a sign that none of them do a good job at explaining it, but that there are a lot of developers out there and just because one developer read and understood the article doesn’t necessarily mean that everyone on their team read and understands it now. While taking the time to better understand how z-index (or any piece of technology) works will definitely set you up to work with it better, we can also take another approach: **make it easier to work with z-index**.

We use abstractions and conventions to hide away the tricky and error-prone parts, which in turn makes it easier for everyone who needs to do the same task. I had the opportunity to attempt to make z-index easier to work with for my team while working on a redesign of our company’s website. The system I designed allowed my team to implement the entire UI while never having to question what a certain z-index value was used for, what number to use when adding a new z-index declaration, or how to fix stacking bugs that crept into the system.

## Common Solution

The most common system I’ve seen for managing z-index values &mdash; other than no system &mdash; is setting several general-use values, each separated by an arbitrary number. This solution definitely tames z-index issues, but as I’ve worked on teams that use this system there still seems to be confusion about how to use it properly. Here is an example from [the Bootstrap documentation](https://getbootstrap.com/docs/5.0/layout/z-index/).

<pre><code class="language-scss">$zindex-dropdown:       1000;
$zindex-sticky:         1020;
$zindex-fixed:          1030;
$zindex-modal-backdrop: 1040;
$zindex-modal:          1050;
$zindex-popover:        1060;
$zindex-tooltip:        1070;
</code></pre>

Bootstrap defines z-index values in Sass variables like `$zindex-dropdown`, `$zindex-sticky`, and `$zindex-fixed`. Those names seem pretty straight forward, but when a developer goes to choose a value for a feature they’re working on, there could be confusion as to which value is most appropriate for their use. They end up asking, “Is what I’m implementing a ‘dropdown’ or a ‘popover’?” which can easily be debated and may not have a clear answer.

A second issue I see with this solution is that the actual values for the variables might seem confusing or lead to insecurity. This solution leaves space in between each value to give developers space to add their own values in between if necessary. Bootstrap defines seven values separated by increments of 10, starting at 1000 and ending at 1070.

Many questions could come to mind when reading this:

<blockquote>“Why start at 1000?<br /><br />“Is there anything less than 1000?”<br /><br />“Where is 1010? Is it a bug? Is something else using it?”<br /><br />“Why was 10 chosen? What if I need more than 9 values to go in between?”</blockquote>

Though I’ve never actually needed these “what if” questions answered, they can add insecurity and confusion to a system that already seems magical and misunderstood. Can we remove all of these concerns, allowing the developer to easily and accurately choose the z-index value they need?

{{% feature-panel %}}

## A New Solution

Since working on a redesign gave my team a fresh start, this was one common issue we wanted to see if we could avoid. To align with our general coding standards, my goals for managing z-index was to avoid [magic numbers](https://archive.org/details/cleancodehandboo00mart_843/page/n330/mode/2up) and to make it easier for every team member to confidently contribute. The second goal of making it easier for others is vague, so I focused on trying to solve these common issues:

- People often choose arbitrarily large z-index values;
- z-index bug fixes often result in a new z-index bug;
- The relationship between z-index values is difficult to trace.

Let’s look at solutions for each of these issues that I was able to apply, leaning on conventions and using existing technologies.

## Giving Z-Index Values Semantics

One reason people often choose arbitrarily large z-index values is because they don’t know the z-index value of the item above which they are trying to place a new item. Once they find an arbitrarily high value that works, they leave it instead of finding an optimal value. Later on, when someone finds this value they have no idea why it is what it is, and even the original author may have forgotten.

<pre><code class="language-css">z-index: 9999;</code></pre>

The solution for fixing “magic numbers” like this is by using a **named constant** instead. While naming the value alone does not give us much more value than the class name does, when we put our z-index constants together, their relationship starts to become explicit.

To remove the magic numbers, I first started defining all of our z-index values in a JavaScript file. I used a JavaScript file since our application was using a CSS-in-JS solution, though this and the ideas in this article can be implemented with styling preprocessors like Sass variables as well as in CSS using custom properties.

<pre><code class="language-javascript">export const backdrop = 0;
export const openButton = 1;
export const dropdown = 2;</code></pre>

With z-index constants, the CSS value has little more meaning, and the actual value is obscured away.

<pre><code class="language-javascript">css`
  z-index: ${backdrop};
`;</code></pre>

This also makes the original value easy to find, revealing the related constants, but there is a further improvement that can be made. We know by how z-index works that these values are related to each other, so we can **change our constants to make that more apparent**.

<pre><code class="language-javascript">export const backdrop = 0;
export const openButton = backdrop + 1;
export const dropdown = openButton + 1;</code></pre>

Using simple arithmetic, we can use the previous constants to make the next constant. Taking this idea one step further to further eliminate ambiguity, I added some utility constants to make these definitions read more like a sentence.

<pre><code class="language-javascript">const base = 0;
const above = 1;

export const backdrop = base;
export const openButton = above + backdrop;
export const dropdown = above + openButton;</code></pre>

Now when someone sees a line like `z-index: ${dropdown};` they can look find the dropdown’s definition and read, “The **dropdown** is **above** the **open button**.”

This makes future maintenance of the constants easier. Whenever you have a new value to add, you can be confident that you are adding it to the right place.

<pre><code class="language-javascript">export const backdrop = base;
export const openButton = above + backdrop;
export const dropdown = above + openButton;
export const closeButton = above + dropdown; // new</code></pre>

Deleting values is easy too, but you need to remember to update any other values that are dependent on it. Using JavaScript, the linter highlighted this for me.

Stacking bug tickets often show up that say something like, “the dropdown is overlapping with the button when it should be underneath.” When coming across these, the fix is as simple as **swapping the relationship pointers** in the definitions.

<pre><code class="language-javascript">export const backdrop = base;
export const dropdown = above + backdrop;
export const openButton = above + dropdown;
export const closeButton = above + dropdown; // ???</code></pre>

Now that we’ve swapped the z-index order, we notice another potential bug before we even check the browser. The close button might now conflict with the open button. You can now have the necessary conversations to resolve bugs _before_ anyone sees a problem in production.

One extra piece I found to be helpful in rare situations was a utility for placing items `below` others. To avoid mixing `above` and `below`, I made the rule that `below` should only be used for negative values.

<pre><code class="language-javascript">const base = 0;
const above = 1;
const below = -1;

export const backdrop = below + dropdown;
export const dropdown = below + button;
export const button = base;</code></pre>

{{% pull-quote %}}
 In this system, every z-index value is only as high as it needs to be, and since it’s dynamically chosen, you aren’t concerned with what the value actually is. 
{{% /pull-quote %}}

You can also delete and add values knowing with confidence how it will affect the other stacked elements.

Once our application ended up with a dozen or so z-index constants, though it started to become a little bit confusing having a long flat list.

{{% ad-panel-leaderboard %}}

### Organizing By Stacking Context

When thinking about stacking context and how the values of each stacking context are independent of others, it sounded like other front-end solutions for effective scoping. I drew similarities to other JavaScript modules, components, [atomic design](https://bradfrost.com/blog/post/atomic-web-design/), and [BEM](https://getbem.com/introduction/). They are all trying to solve similar problems of how we can independently scope concerns, keeping them from affecting other areas.

Taking inspiration from BEM, I made a **naming convention for our constants** to better organize the values and bring more order to the flat list of constants. The format I ended up using had a template like this: `z<Context><Element>`.

The `z` portion is a prefix denoting the fact that the value is meant to be used in z-index declarations, considering we had other constants defined in our JavaScript files like color variables.

The`<Context>` portion is replaced with the name stacking context the constant belongs to. This is similar to the “block” in BEM and in practice almost always shares the same name as the component being styled. The main exception is the root HTML stacking context that is used for page region stacking.

The final portion of the format, `<Element>` is for the name of the specific item to be positioned in the stacking context and is most similar to “element” in BEM.

Here is **a full example of what this naming convention could look like** when added to what we’ve talked about previously. For an interactive version, you can play around with the same example in a CodePen:

{{< codepen height="480" theme_id="light" slug_hash="xxEvepz" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [Managing CSS Z-Index in Large Projects Demo](https://codepen.io/smashingmag/pen/xxEvepz) by <a href="https://codepen.io/sfrieson">Steven Frieson</a>.{{< /codepen >}}

For other language versions, [check out this repository](https://github.com/sfrieson/managing-css-z-index-in-large-projects).

<pre><code class="language-javascript">// Utils
const base = 0;
const above = 1; // use this for all values above the base
const below = -1; // and this for all values below the base

// Page Layout
export const zLayoutNavigation = above + base;
export const zLayoutFooter = above + base;
export const zLayoutModal = above + zLayoutNavigation;
export const zLayoutPopUpAd = above + zLayoutModal;

// NavMenu
export const zNavMenuBackdrop = below + base;
export const zNavMenuPopover = above + base;
export const zNavMenuToggle = above + zNavMenuPopover;</code></pre>

Now that our constants are organized by their stacking context, we can quickly see which values are related and where a new value or fix should go.

### Taking It Further

That is essentially the specification of how this should work. Considering this solution was only **designed with one application in mind**, there are some further steps that could be taken to make it more mature and support more use cases. Some of these ideas are more specific to the language it’s being implemented in but most ideas carry over.

One area that could possibly be improved around what is being shipped to the browser. When I implemented this, the framework we were using did not give us much control over the build tools, so the JavaScript file of all the definitions was bundled with the application. This did not have a measurable performance impact on our application, but you may have noticed that all of the values could be computed at compile time. An implementation using Sass would end up not shipping any of the Sass variables to the client, but instead, insert the derived z-index value in the CSS. For **JS and CSS solutions**, build tools like Webpack and PostCSS, respectively, could help do the same.

The way the solution evolved as I worked on it, the z-index constants ended up all in one file. This ended up being a great way to see all of the z-index values across the application at once, making it easier to quickly glance for any possible stacking conflicts. They were also filed away with other **styling constants like colors and typography**, so it made sense to originally have them all defined together. As the file grew though, it started to be internally organized by stacking context as explained above. Since the stacking contexts often mapped to a component, it started feeling like each set of constants could be collocated with their component. This would bring all the normal benefits of collocation, being closer to the files they’re used in, causing less friction when needing to add, edit, and remove constants. We never refactored it, but that seems like a viable option to explore.

One additional piece has to do with ergonomics and developer experience. The constants are all exported as a flat list at the moment. The naming convention took inspiration from BEM, but Sass and JavaScript allow us to use other ways to **organize our data**. Sass maps or JavaScript Objects or Maps could have been used to organize the values hierarchically. If we had all the values in a `z` object, it could have led to shorter import statements. We could have gone further to have an object per stacking context as well leading to a usage style more like `z.layout.navigation`. Different tools like TypeScript could guard against making typos here, though this might be more effort than it’s worth.

## Our Results

The system as spelled out was successfully implemented and deployed to our production applications. Checking back in on the objectives, we definitely got rid of the magic numbers. As far as developer ease and confidence goes, my team was able to easily add new z-index values and **fix pre- and post-launch bugs without fear** that the changes would introduce new bugs. On multiple occasions, we fixed bugs before they were filed.

We also were able to avoid the issue of coming across a random `z-index: 9999;`. Though the application had sticky headers, floating action buttons, dropdowns, modals, pop up ads, and more in the stacking context, the highest value we had was 5. Even then, no one knew it since the values were all abstracted away from us in variables.

{{% pull-quote %}}
 Solving developer experience issues resulted in a z-index mini-framework, helping people make the correct decision with less effort and move more quickly.
{{% /pull-quote %}}

Something else we noticed was that sometimes we were assigning a z-index when we did not necessarily need one. Since stacking contexts can be created by several different properties, declarations like `position: sticky;` can act in a similar manner as setting `z-index: 1;`. In those cases, we continued to add a constant and declaration anyway. Keeping them allowed for better consistency in the system instead of allowing there to be special cases, which would degrade confidence about whether everything was working correctly or not. Keeping the constant list complete aided in understanding the system and set us up better for rearranging the values when necessary.

### What It Doesn’t Solve

Like any framework, there are parts that it doesn’t not do a good job at solving for you. Naming things is still hard, and this framework slightly exacerbates the problem by requiring that you name all of your z-index values. Even still, we found that the gained clarity overcame the chore of having to name them all.

This system also does not necessarily help you figure out which stacking context a bug is in. Coming across a z-index bug where you don’t know where the new stacking context is created or where the z-index value is set is not solved by this framework, but once you have found the issue, the path to making the correct fix is clear.

{{% ad-panel-leaderboard %}}

## Using It In Your App

The ideas shared here should be actionable in most applications depending on your styling solution and browser support. Migrating to use this system is not very risky since stacking contexts are already scoped individually; you can migrate one context as it already exists at a time. Changing to use these conventions forces you to describe more clearly what you already have in your app, shining a light on what might currently seem like a dark, scary corner.

If your z-index values are in a state where you are unsure about most or all of them, then the **best way to convert to this system** will probably be to start by creating a constant for each value in a single list in a single file. As the stacking contexts become more clear, you can start grouping them and renaming them (if necessary) to conform to the naming convention.

My team was not working with any external CSS libraries or frameworks that included z-index values, but that could possibly add some difficulty to adopting this system. Hopefully, the utilities are configurable enough to deal with most uses and to even incorporate the third-party values into the system.

Finally, all of the examples here have been written as a single file of z-index values, but you could **collocate these values with the component** to make an even stronger connection between the two. Using a file naming convention will make it easier to find all of the values throughout the application.

### Try It Out Yourself

If you are having trouble wrangling z-index values on your site and end up trying out these suggestions, **I would love to hear about your experience**. This mini-framework was developed over just a few months and has only been used in one production codebase, so there are certainly unexplored use cases and opinions that could be added or tweaked.

{{< signature "vf, yk, il" >}}
