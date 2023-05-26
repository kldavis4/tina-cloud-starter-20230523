---
title: 'Battling BEM CSS: 10 Common Problems And How To Avoid Them'
slug: battling-bem-extended-edition-common-problems-and-how-to-avoid-them
author: davidberner
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c5ff1e9d-e791-4004-ac3e-106377c999fc/bem-website-tools-opt.png
date: 2016-06-01T23:55:29.000Z
summary: >-
  This article aims to be useful for people who are already BEM enthusiasts and
  wish to use it more effectively or people who are curious to learn more about
  it.
description: >-
  Whether you’ve just discovered BEM or are an old hand (in web terms anyway!),
  you probably appreciate what a useful methodology it is. If you don’t know
  what BEM is, I suggest you read about it on the BEM website before continuing
  with this post, because I’ll be using terms that assume a basic understanding
  of this CSS methodology.
categories:
  - Coding
  - Frameworks
  - CSS
  - JavaScript
  - HTML5
---
Whether you’ve just discovered BEM or are an old hand (in web terms anyway!), you probably appreciate what a useful methodology it is. If you don’t know what BEM is, I suggest you read about it on the <a href="https://en.bem.info/">BEM website</a> before continuing with this post, because I’ll be using terms that assume a basic understanding of this CSS methodology.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c5ff1e9d-e791-4004-ac3e-106377c999fc/bem-website-tools-opt.png" width="500" height="305" alt="BEM CSS" title="Battling BEM CSS: 10 Common Problems And How To Avoid Them" /></figure>

This article aims to be useful for people who are already BEM enthusiasts and wish to use it more effectively or people who are curious to learn more about it.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [A New Front-End Methodology: BEM](https://www.smashingmagazine.com/2012/04/a-new-front-end-methodology-bem/)
*   [Scaling Down The BEM Methodology For Small Projects](https://www.smashingmagazine.com/2014/07/bem-methodology-for-small-projects/)
*   [<span class="headline">The Evolution Of The BEM Methodology</span>](https://www.smashingmagazine.com/2013/02/the-history-of-the-bem-methodology/)

{{% feature-panel %}}

Now, I’m under no illusion that this is a beautiful way to name things. It’s absolutely not. One of things that put me off of adopting it for such a long time was how eye-gougingly ugly the syntax is. The designer in me didn’t want my sexy markup cluttered with dirty double-underscores and foul double-hyphens.

The developer in me looked at it pragmatically. And, eventually, the logical, modular way of building a user interface outweighed the right-side of my brain that complained, “But it’s not pretty enough!”. I certainly don’t recommend picking a living-room centrepiece this way, but when you need a life jacket (as you do in a sea of CSS), I’ll take function over form any day. Anyway, enough rambling. Here are the 10 dilemmas I’ve battled with and some tips on how to deal with them.</p>

## 1\. “What To Do About ‘Grandchild’ Selectors (And Beyond)?”

To clarify, you would use a grandchild selector when you need to reference an element that is nested two levels deep. These bad boys are the bane of my life, and I’m sure their misuse is one of the reasons people have an immediate aversion to BEM. I’ll give you an example:

<div class="break-out">

<pre><code class="language-markup">&lt;div class="c-card"&gt;

    &lt;div class="c-card&#95;&#95;header"&gt;
        &lt;!-- Here comes the grandchild… --&gt;
        &lt;h2 class="c-card&#95;&#95;header&#95;&#95;title"&gt;Title text here&lt;/h2&gt;
    &lt;/div&gt;

    &lt;div class="c-card&#95;&#95;body"&gt;

        &lt;img class="c-card&#95;&#95;body&#95;&#95;img" src="some-img.png" alt="description"&gt;
        &lt;p class="c-card&#95;&#95;body&#95;&#95;text"&gt;Lorem ipsum dolor sit amet, consectetur&lt;/p&gt;
        &lt;p class="c-card&#95;&#95;body&#95;&#95;text"&gt;Adipiscing elit.
            &lt;a href="/somelink.html" class="c-card&#95;&#95;body&#95;&#95;text&#95;&#95;link"&gt;Pellentesque amet&lt;/a&gt;
        &lt;/p&gt;

    &lt;/div&gt;
&lt;/div&gt;
</code></pre></div>

As you might imagine, naming in this way can quickly get out of hand, and the more nested a component is, the more hideous and unreadable the class names become. I’ve used a short block name of <code>c-card</code> and the short element names of <code>body</code>, <code>text</code> and <code>link</code>, but you can imagine how out of control it gets when the initial block element is named something like <code>c-drop-down-menu</code>.

I believe the double-underscore pattern should appear only once in a selector name. BEM stands for <code>Block&#95;&#95;Element--Modifier</code>, <strong>not</strong> <code>Block&#95;&#95;Element&#95;&#95;Element--Modifier</code>. So, avoid multiple element level naming. If you’re getting to great-great-great-grandchild levels, then you’ll probably want to revisit your component structure anyway.

BEM naming isn’t strictly tied to the DOM, so it doesn’t matter how many levels deep a descendent element is nested. The naming convention is there to help you identify relationships with the top-level component block — in this case, <code>c-card</code>.

This is how I would treat the same card component:

<div class="break-out">

<pre><code class="language-markup">&lt;div class="c-card"&gt;
    &lt;div class="c-card&#95;&#95;header"&gt;
        &lt;h2 class="c-card&#95;&#95;title"&gt;Title text here&lt;/h2&gt;
    &lt;/div&gt;

    &lt;div class="c-card&#95;&#95;body"&gt;

        &lt;img class="c-card&#95;&#95;img" src="some-img.png" alt="description"&gt;
        &lt;p class="c-card&#95;&#95;text"&gt;Lorem ipsum dolor sit amet, consectetur&lt;/p&gt;
        &lt;p class="c-card&#95;&#95;text"&gt;Adipiscing elit.
            &lt;a href="/somelink.html" class="c-card&#95;&#95;link"&gt;Pellentesque amet&lt;/a&gt;
        &lt;/p&gt;

    &lt;/div&gt;
&lt;/div&gt;
</code></pre></div>

This means that all of the descendent elements will be affected only by the card block. So, we would be able to move the text and images into <code>c-card&#95;&#95;header</code> or even introduce a new <code>c-card&#95;&#95;footer</code> element without breaking the semantic structure.</p>

## 2\. “Should I Be Namespacing?”

By now, you’ve probably noticed the use of <code>c-</code> littered throughout my code samples. This stands for “component” and forms the basis of how I namespace my BEM classes. This idea stems from Harry Robert’s <a href="https://csswizardry.com/2015/03/more-transparent-ui-code-with-namespaces/">namespacing technique</a>, which improves code readability.

This is the system I have adopted, and many of the prefixes will appear throughout the code samples in this article:
<table class="tablesaw break-out">
<thead>
<tr>
<th>Type</th>
<th>Prefix</th>
<th>Examples</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>Component</td>
<td><code>c-</code></td>
<td><code>c-card</code>
<code>c-checklist</code></td>
<td>Form the backbone of an application and contain all of the cosmetics for a standalone component.</td>
</tr>
<tr>
<td>Layout module</td>
<td><code>l-</code></td>
<td><code>l-grid</code>
<code>l-container</code></td>
<td>These modules have no cosmetics and are purely used to position <code>c-</code> components and structure an application’s layout.</td>
</tr>
<tr>
<td>Helpers</td>
<td><code>h-</code></td>
<td><code>h-show</code>
<code>h-hide</code></td>
<td>These utility classes have a single function, often using <code>!important</code> to boost their specificity. (Commonly used for positioning or visibility.)</td>
</tr>
<tr>
<td>States</td>
<td><code>is-</code>
<code>has-</code></td>
<td><code>is-visible</code>
<code>has-loaded</code></td>
<td>Indicate different states that a <code>c-</code> component can have. More detail on this concept can be found inside problem 6 below, but</td>
</tr>
<tr>
<td>JavaScript hooks</td>
<td><code>js-</code></td>
<td><code>js-tab-switcher</code></td>
<td>These indicate that JavaScript behavior is attached to a component. No styles should be associated with them; they are purely used to enable easier manipulation with script.</td>
</tr>
</tbody>
</table>

I have found that using these namespaces has made my code infinitely more readable. Even if I don’t manage to sell you on BEM, this is definitely a key takeaway.

You could adopt many other namespaces, like <code>qa-</code> for quality-assurance testing, <code>ss-</code> for server-side hooks, etc. But the list above is a good starting point, and you can introduce others as you get comfortable with the technique.

You’ll see a good example of the utility of this style of namespacing in the next problem.</p>

## 3\. “What Should I Name Wrappers?”

Some components require a parent wrapper (or container) that dictates the layout of the children. In these cases, I always try to abstract the layout away into a layout module, such as <code>l-grid</code>, and insert each component as the contents of each <code>l-grid&#95;&#95;item</code>.

In our card example, if we wanted to lay out a list of four <code>c-card</code>s, I would use the following markup:

<div class="break-out">

<pre><code class="language-markup">&lt;ul class="l-grid"&gt;
    &lt;li class="l-grid&#95;&#95;item"&gt;
        &lt;div class="c-card"&gt;
            &lt;div class="c-card&#95;&#95;header"&gt;
                […]
            &lt;/div&gt;
            &lt;div class="c-card&#95;&#95;body"&gt;
                […]
            &lt;/div&gt;
        &lt;/div&gt;
    &lt;/li&gt;
    &lt;li class="l-grid&#95;&#95;item"&gt;
        &lt;div class="c-card"&gt;
            &lt;div class="c-card&#95;&#95;header"&gt;
                […]
            &lt;/div&gt;
            &lt;div class="c-card&#95;&#95;body"&gt;
                […]
            &lt;/div&gt;
        &lt;/div&gt;
    &lt;/li&gt;
    &lt;li class="l-grid&#95;&#95;item"&gt;
        &lt;div class="c-card"&gt;
            &lt;div class="c-card&#95;&#95;header"&gt;
                […]
            &lt;/div&gt;
            &lt;div class="c-card&#95;&#95;body"&gt;
                […]
            &lt;/div&gt;
        &lt;/div&gt;
    &lt;/li&gt;
    &lt;li class="l-grid&#95;&#95;item"&gt;
        &lt;div class="c-card"&gt;
            &lt;div class="c-card&#95;&#95;header"&gt;
                […]
            &lt;/div&gt;
            &lt;div class="c-card&#95;&#95;body"&gt;
                […]
            &lt;/div&gt;
        &lt;/div&gt;
    &lt;/li&gt;
&lt;/ul&gt;
</code></pre></div>

You should now have a solid idea of how layout modules and component namespaces should play together.

Don’t be afraid to use a little extra markup to save yourself a massive headache. No one is going to pat you on the back for shaving off a couple of <code>&lt;div&gt;</code> tags!

In some instances, this isn’t possible. If, for example, your grid isn’t going to give you the result you want or you simply want something semantic to name a parent element, what should you do? I tend to opt for the word <code>container</code> or <code>list</code>, depending on the scenario. Sticking with our cards example, I might use <code>&lt;div class="l-cards-container"&gt;[…]&lt;/div&gt;</code> or <code>&lt;ul class="l-cards-list"&gt;[…]&lt;/ul&gt;</code>, depending on the use case. The key is to be consistent with your naming convention.

## 4\. “Cross-Component… Components?”

Another issue commonly faced is a component whose styling or positioning is affected by its parent container. Various solutions to this problem are <a href="https://simurai.com/blog/2015/05/11/nesting-components">covered in detail by Simurai</a>. I’ll just fill you in on what I believe is the most scalable approach.

To summarize, let’s assume we want to add a <code>c-button</code> into the <code>card&#95;&#95;body</code> of our previous example. The button is already its own component and is marked up like this:

<pre><code class="language-markup">&lt;button class="c-button c-button--primary"&gt;Click me!&lt;/button&gt;
</code></pre>

If there are no styling differences in the regular button component, then there is no problem. We would just drop it in like so:

<div class="break-out">

<pre><code class="language-markup">&lt;div class="c-card"&gt;
    &lt;div class="c-card&#95;&#95;header"&gt;
        &lt;h2 class="c-card&#95;&#95;title"&gt;Title text here&lt;/h3&gt;
    &lt;/div&gt;

    &lt;div class="c-card&#95;&#95;body"&gt;

        &lt;img class="c-card&#95;&#95;img" src="some-img.png"&gt;
        &lt;p class="c-card&#95;&#95;text"&gt;Lorem ipsum dolor sit amet, consectetur&lt;/p&gt;
        &lt;p class="c-card&#95;&#95;text"&gt;Adipiscing elit. Pellentesque.&lt;/p&gt;

        &lt;!-- Our nested button component --&gt;
        &lt;button class="c-button c-button--primary"&gt;Click me!&lt;/button&gt;

    &lt;/div&gt;
&lt;/div&gt;
</code></pre></div>

However, what happens when there are a few subtle styling differences — for example, we want to make it a bit smaller, with fully rounded corners, but only when it’s a part of a <code>c-card</code> component?

Previously, I stated that I find a cross-component class to be the most robust solution:

<div class="break-out">

<pre><code class="language-markup">&lt;div class="c-card"&gt;
    &lt;div class="c-card&#95;&#95;header"&gt;
        &lt;h2 class="c-card&#95;&#95;title"&gt;Title text here&lt;/h3&gt;
    &lt;/div&gt;

    &lt;div class="c-card&#95;&#95;body"&gt;

        &lt;img class="c-card&#95;&#95;img" src="some-img.png"&gt;
        &lt;p class="c-card&#95;&#95;text"&gt;Lorem ipsum dolor sit amet, consectetur&lt;/p&gt;
        &lt;p class="c-card&#95;&#95;text"&gt;Adipiscing elit. Pellentesque.&lt;/p&gt;

        &lt;!-- My *old* cross-component approach --&gt;
        &lt;button class="c-button c-card&#95;&#95;c-button"&gt;Click me!&lt;/button&gt;

    &lt;/div&gt;
&lt;/div&gt;
</code></pre></div>

This is what is<a href="https://en.bem.info/forum/4/"> known on the BEM website</a> as a “mix.” I have, however, changed my stance on this approach, following some great comments from Esteban Lussich.

<p>In the example above, the <code>c-card&#95;&#95;c-button</code> class is trying to modify one or more existing properties of <code>c-button</code>, but it will depend on the source order (or even specificity) in order to successfully apply them. The <code>c-card&#95;&#95;c-button</code> class will work only if it is declared after the <code>c-button</code> block in the source code, which could quickly get out of hand as you build more of these cross-components. (Whacking on an <code>!important</code> is, of course, an option, but I certainly wouldn’t encourage it!)</p>

The cosmetics of a truly modular UI element should be totally agnostic of the element’s parent container — it should look the same regardless of where you drop it. Adding a class from another component for bespoke styling, as the “mix” approach does, violates the <a href="https://en.wikipedia.org/wiki/Open/closed_principle">open/closed</a> principle of component-driven design — i.e there should be no dependency on another module for aesthetics.

Your best bet is to use a modifier for these small cosmetic differences, because you may well find that you wish to reuse them elsewhere as your project grows.

<pre><code class="language-markup">&lt;button class="c-button c-button--rounded c-button--small"&gt;Click me!&lt;/button&gt;</code></pre>

Even if you never use those additional classes again, at least you won’t be tied to the parent container, specificity or source order to apply the modifications.

Of course, the other option is to go back to your designer and tell them that the button should be consistent with the rest of the buttons on the website and to avoid this issue altogether… but that’s one for another day.</p>

## 5\. “Modifier Or New Component?”

One of the biggest problems is deciding where a component ends and a new one begins. In the <code>c-card</code> example, you might later create another component named <code>c-panel</code> with very similar styling attributes but a few noticeable differences.

But what determines whether there should be two components, <code>c-panel</code> and <code>c-card</code>, or simply a modifier for <code>c-card</code> that applies the unique styles?

It’s very easy to over-modularize and make everything a component. I recommend starting with modifiers, but if you find that your specific component CSS file is getting difficult to manage, then it’s probably time to break out a few of those modifiers. A good indicator is when you find yourself having to reset all of the “block” CSS in order to style your new modifier — this, to me, suggests new component time.

The best way, if you work with other developers or designers, is to ask them for an opinion. Grab them for a couple of minutes and discuss it. I know this answer is a bit of a cop-out, but for a large application, it’s vital that you all understand what modules are available and agree on exactly what constitutes a component.</p>

## 6\. “How To Handle States?”

This is a common problem, particularly when you’re styling a component in an active or open state. Let’s say our cards have an active state; so, when clicked on, they stand out with a nice border styling treatment. How do you go about naming that class?

The way I see it, you have two options really: either a standalone state hook or a BEM-like naming modifier at the component level:

<pre><code class="language-markup">&lt;!-- standalone state hook --&gt;
&lt;div class="c-card is-active"&gt;
    […]
&lt;/div&gt;

&lt;!-- or BEM modifier --&gt;
&lt;div class="c-card c-card--is-active"&gt;
    […]
&lt;/div&gt;
</code></pre>

While I like the idea of keeping the BEM-like naming for consistency, the advantage of the standalone class is that it makes it easy to use JavaScript to apply generic state hooks to any component. When you have to apply specific modifier-based state classes with script, this becomes more problematic. It is, of course, entirely possible, but it means writing a lot more <a href="https://www.smashingmagazine.com/tag/javascript">JavaScript</a> for each possibility.

Sticking to a standard set of state hooks makes sense. Chris Pearce has <a href="https://github.com/chris-pearce/css-guidelines#state-hooks">compiled a good list</a>, so I recommend just pinching those.</p>

## 7\. “When Is It OK **Not** To Add A Class To An Element?”

I can understand people being overwhelmed by the sheer number of classes required to build a complex piece of UI, especially if they’re not used to assigning a class to every tag.

Typically, I will attach classes to anything that needs to be styled differently in the context of the component. I will often leave <code>p</code> tags classless, unless the component requires them to look unique in that context.

Granted, this could mean your markup will contain a lot of classes. Ultimately, though, your components will be able to live independently and be dropped anywhere without a risk of side effects.

Due to the global nature of CSS, putting a class on everything gives us control over exactly how our components render. The initial mental discomfort caused is well worth the benefits of a fully modular system.</p>

## 8\. “How To Nest Components?”

Suppose we want to display a checklist in our <code>c-card</code> component. Here is a demonstation of how <strong>not</strong> to mark this up:

<div class="break-out">

<pre><code class="language-markup">&lt;div class="c-card"&gt;
    &lt;div class="c-card&#95;&#95;header"&gt;
        &lt;h2 class="c-card&#95;&#95;title"&gt;Title text here&lt;/h3&gt;
    &lt;/div&gt;

    &lt;div class="c-card&#95;&#95;body"&gt;

        &lt;p&gt;I would like to buy:&lt;/p&gt;

        &lt;!-- Uh oh! A nested component --&gt;
        &lt;ul class="c-card&#95;&#95;checklist"&gt;
            &lt;li class="c-card&#95;&#95;checklist&#95;&#95;item"&gt;
                &lt;input id="option_1" type="checkbox" name="checkbox" class="c-card&#95;&#95;checklist&#95;&#95;input"&gt;
                &lt;label for="option_1" class="c-card&#95;&#95;checklist&#95;&#95;label"&gt;Apples&lt;/label&gt;
            &lt;/li&gt;
            &lt;li class="c-card&#95;&#95;checklist&#95;&#95;item"&gt;
                &lt;input id="option_2" type="checkbox" name="checkbox" class="c-card&#95;&#95;checklist&#95;&#95;input"&gt;
                &lt;label for="option_2" class="c-card&#95;&#95;checklist&#95;&#95;label"&gt;Pears&lt;/label&gt;
            &lt;/li&gt;
        &lt;/ul&gt;

    &lt;/div&gt;
    &lt;!-- .c-card&#95;&#95;body --&gt;
&lt;/div&gt;
&lt;!-- .c-card --&gt;
</code></pre></div>

We have a couple of problems here. One is the grandparent selector that we covered in section 1. The second is that all of the styles applied to <code>c-card&#95;&#95;checklist&#95;&#95;item</code> are scoped to this specific use case and won’t be reusable.

My preference here would be to break out the list itself into a layout module and the checklist items into their own components, enabling them to be used independently elsewhere. This brings our <code>l-</code> namespacing back into play as well:

<div class="break-out">

<pre><code class="language-markup">&lt;div class="c-card"&gt;
    &lt;div class="c-card&#95;&#95;header"&gt;
        &lt;h2 class="c-card&#95;&#95;title"&gt;Title text here&lt;/h3&gt;
    &lt;/div&gt;

    &lt;div class="c-card&#95;&#95;body"&gt;&lt;div class="c-card&#95;&#95;body"&gt;

        &lt;p&gt;I would like to buy:&lt;/p&gt;

        &lt;!-- Much nicer - a layout module --&gt;
        &lt;ul class="l-list"&gt;
            &lt;li class="l-list&#95;&#95;item"&gt;

                &lt;!-- A reusable nested component --&gt;
                &lt;div class="c-checkbox"&gt;
                    &lt;input id="option_1" type="checkbox" name="checkbox" class="c-checkbox&#95;&#95;input"&gt;
                    &lt;label for="option_1" class="c-checkbox&#95;&#95;label"&gt;Apples&lt;/label&gt;
                &lt;/div&gt;

            &lt;/li&gt;
            &lt;li class="l-list&#95;&#95;item"&gt;

                &lt;div class="c-checkbox"&gt;
                    &lt;input id="option_2" type="checkbox" name="checkbox" class="c-checkbox&#95;&#95;input"&gt;
                    &lt;label for="option_2" class="c-checkbox&#95;&#95;label"&gt;Pears&lt;/label&gt;
                &lt;/div&gt;

            &lt;/li&gt;
        &lt;/ul&gt;
        &lt;!-- .l-list --&gt;

    &lt;/div&gt;
    &lt;!-- .c-card&#95;&#95;body --&gt;
&lt;/div&gt;
&lt;!-- .c-card --&gt;
</code></pre></div>

This saves you from having to repeat the styles, and it means we can use both the <code>l-list</code> and <code>c-checkbox</code> in other areas of our application. It does mean a little more markup, but it’s a small price to pay for readability, encapsulation and reusability. You’ve probably noticed these are common themes!

## 9\. “Won’t Components End Up With A Million Classes?”

Some argue that having a lot of classes per element is not great, and <code>--modifiers</code> can certainly add up. Personally, I don’t find this to be problematic, because it means the code is more readable and I know exactly what it is supposed to be doing.

For context, this is an example of four classes being needed to style a button:

<pre><code class="language-markup">&lt;button class="c-button c-button--primary c-button--huge  is-active"&gt;Click me!&lt;/button&gt;
</code></pre>

I get that this syntax is not the prettiest to gaze upon, but it is explicit.

However, if this is giving you a major headache, you could look at the <a href="https://webuniverse.io/css-organization-naming-conventions-and-safe-extend-without-preprocessors/#To_extend_or_not_to_extend?">extension technique</a> that Sergey Zarouski came up with. Essentially, we would use <code>.className [class^="className"], [class*=" className"]</code> in the style sheet to emulate extension functionality in vanilla CSS. If this syntax looks familiar to you, that’s because it is very similar to the way <a href="https://icomoon.io/">Icomoon</a> handles its icon selectors.

With this technique, your output might look something like this:

<pre><code class="language-markup">&lt;button class="c-button--primary-huge  is-active"&gt;Click me!&lt;/button&gt;
</code></pre>

I don’t know whether the performance hit of using the <code>class^=</code> and <code>class*=</code> selectors is much greater than using individual classes at scale, but in theory this is a cool alternative. I’m fine with the multi-class option myself, but I thought this deserved a mention for those who prefer an alternative.</p>

## 10\. “Can We Change A Component’s Type Responsively?”

This was a problem posed to me by Arie Thulank and is one for which I struggled to come up with a 100% concrete solution.

An example of this might be a dropdown menu that converts to a set of tabs at a given breakpoint, or offscreen navigation that switches to a menu bar at a given breakpoint.

Essentially, one component would have two very different cosmetic treatments, dictated by a media query.

My inclination for these two particular examples is just to build a <code>c-navigation</code> component, because at both breakpoints this is essentially what it is doing. But it got me thinking, what about a list of images that converts to a carousel on bigger screens? This seems like an edge case to me, and as long as it is well documented and commented, I think it is perfectly reasonable to create a one-off standalone component for this type of UI, with explicit naming (like <code>c-image-list-to-carousel</code>).

Harry Roberts has written about <a href="https://csswizardry.com/2015/08/bemit-taking-the-bem-naming-convention-a-step-further/">responsive suffixes</a>, which is one way to handle this. His approach is intended more for changes in layout and print styles, rather than shifts of entire components, but I don’t see why the technique couldn’t be applied here. So, essentially you would author classes like this:

<pre><code class="language-markup">&lt;ul class="c-image-list@small-screen c-carousel@large-screen"&gt;
</code></pre>

These would then live in your media queries for the respective screen sizes. Pro tip: You have to escape the <code>@</code> sign in your CSS with a backslash, like so:

<pre><code class="language-css">.c-image-list\@small-screen {
    /* styles here */
}
</code></pre>

I haven’t had much cause to create these type of components, but this feels like a very developer-friendly way to do it, if you have to. The next person coming in should be able to easily understand your intention. I’m not advocating for names like <code>small-screen</code> and <code>large-screen</code> — they are used here purely for readability.</p>

## Summary

BEM has been an absolute lifesaver for me in my effort to create applications in a modular, component-driven way. I’ve been using it for nearly three years now, and the problems above are the few stumbling blocks I’ve hit along the way. I hope you’ve found this article useful, and if you’ve not given BEM a go yet, I highly encourage you to do so.

<strong>Note</strong>: <em>This is an enhanced version of my original article “<a href="https://medium.com/fed-or-dead/battling-bem-5-common-problems-and-how-to-avoid-them-5bbd23dee319#.xbw2qszc1">Battling BEM: 5 Common Problems and How to Avoid Them</a>,” which appeared on Medium. I’ve added five more common problems, (some of which were asked about in the comments of that article) and I have altered my views on one of the original problems.</em>

{{< signature "vf, al, il" >}}

