---
title: 'Everything You Need To Know About CSS Margins'
slug: margins-in-css
author: rachel-andrew
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1906ccea-2ce1-4e56-84af-07c646285040/css-margins-sharing-card.png
date: 2019-07-15T12:30:59+02:00
summary: >-
  Margins in CSS seem simple enough at first glance. Applied to an element it forms a space around the element, pushing other elements away. However, there is more to a margin than you might think.
description: >-
  Margins in CSS seem simple enough at first glance. Applied to an element it forms a space around the element, pushing other elements away. However, there is more to a margin than you might think.
categories:
  - CSS
  - Browsers
  - Guides
---

One of the first things most of us learned when we learned CSS, was details of the various parts of a box in CSS, described as The CSS Box Model. One of the elements in the Box Model is the margin, a transparent area around a box, which will push other elements away from the box contents. The `margin-top`, `margin-right`, `margin-bottom` and `margin-left` properties were described right back in CSS1, along with the shorthand `margin` for setting all four properties at once.

A margin seems to be a fairly uncomplicated thing, however, in this article, we will take a look at some of the things which trip people up with regard to using margins. In particular, we will be looking at how margins interact with each other, and how margin collapsing actually works.

## The CSS Box Model

As with all articles about parts of the CSS Box Model, we should define what we mean by that, and how the model has been clarified through versions of CSS. The _Box Model_ refers to how the various parts of a box &mdash; the content, padding, border, and margin &mdash; are laid out and interact with each other. In CSS1, [the Box Model was detailed with the ASCII art diagram](https://www.w3.org/TR/CSS1/#formatting-model) shown in the image below.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/685c8ac3-58d9-48c6-adab-159568483386/css1-box-model.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/685c8ac3-58d9-48c6-adab-159568483386/css1-box-model.png" sizes="100vw" caption="Depiction of the CSS Box Model in CSS1" alt="ascii art drawing of the box model" >}}

The four margin properties for each side of the box and the `margin` shorthand were all defined in CSS1.

The CSS2.1 specification has an illustration to demonstrate the Box Model and also defines terms we still use to describe the various boxes. The specification describes the `content box`, `padding box`, `border box`, and `margin box`, each being defined by the edges of the content, padding, border, and margin respectively.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/146404a4-5c8c-45fb-8d73-8813c768a064/css2-box-model.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/146404a4-5c8c-45fb-8d73-8813c768a064/css2-box-model.png" sizes="100vw" caption="Depection of the CSS Box Model in CSS2" alt="diagram of the CSS Box Model" >}}

There is now a [Level 3 Box Model specification](https://www.w3.org/TR/css-box-3/) as a Working Draft. This specification refers back to CSS2 for the definitions of the Box Model and [margins](https://www.w3.org/TR/css-box-3/#margins), therefore it is the CSS2 definition we will be using for the majority of this article.

{{% feature-panel %}}

## Margin Collapsing

The CSS1 specification, as it defined margins, also defined that vertical margins _collapse_. This collapsing behavior has been the source of margin-related frustration ever since. Margin collapsing makes sense if you consider that in those early days, CSS was being used as a documenting formatting language. Margin collapsing means that when a heading with a bottom margin, is followed by a paragraph with a top margin, you do not get a huge gap between those items.

When margins collapse, they will combine so that the space between the two elements becomes the larger of the two margins. The smaller margin essentially ending up inside the larger one.

Margins collapse in the following situations:

<ul>
	<li><a href="#adjacent-siblings">Adjacent siblings</a></li>
	<li><a href="#completely-empty-boxes">Completely empty boxes</a></li>
	<li><a href="#parent-first-last-child-element">Parent and first or last child element</a></li>
</ul>

Let’s take a look at each of these scenarios in turn, before looking at the things which prevent margins from collapsing in these scenarios.

### Adjacent Siblings

My initial description of margin collapsing is a demonstration of how the margins between adjacent siblings collapse. Other than in the situations mentioned below, if you have two elements displaying one after the other in normal flow, the bottom margin of the first element will collapse with the top margin of the following element.

In the CodePen example below, there are three `div` elements. The first has a top and bottom margin of 50 pixels. The second has a top and bottom margin of 20px. The third has a top and bottom margin of 3em. The margin between the first two elements is 50 pixels, as the smaller top margin is combined with the larger bottom margin. The margin between the second two elements in 3em, as 3em is larger than the 20 pixels on the bottom of the second element.

{{< codepen height="480" theme_id="light" slug_hash="OevMPo" default_tab="result" breakout="true" user="rachelandrew" editable="true" data-editable="true" >}}See the Pen [Margins: adjacent siblings](https://codepen.io/rachelandrew/pen/OevMPo) by <a href="https://codepen.io/rachelandrew">Rachel Andrew</a>.{{< /codepen >}}

### Completely Empty Boxes

If a box is empty, then its top and bottom margin may collapse with each other. In the following CodePen example, the element with a class of empty has a top and bottom margin of 50 pixels, however, the space between the first and third items is not 100 pixels, but 50. This is due to the two margins collapsing. Adding anything to that box (even padding) will cause the top and bottom margins to be used and not collapse.

{{< codepen height="480" theme_id="light" slug_hash="JQLGMr" default_tab="result" breakout="true" user="rachelandrew" editable="true" data-editable="true" >}}See the Pen [Margins: empty boxes](https://codepen.io/rachelandrew/pen/JQLGMr) by <a href="https://codepen.io/rachelandrew">Rachel Andrew</a>.{{< /codepen >}}

### Parent And First Or Last Child Element

This is the margin collapsing scenario which catches people out most often, as it does not seem particularly intuitive. In the following CodePen, I have a `div` with a class of wrapper, and I have given that `div` an `outline` in red so that you can see where it is. The three child elements all have a margin of 50 pixels. However, the first and last items are flush with the edges of the wrapper; there is not a 50-pixel margin between the element and the wrapper.

{{< codepen height="480" theme_id="light" slug_hash="BgrKGp" default_tab="result" breakout="true" user="rachelandrew" editable="true" data-editable="true" >}}See the Pen [Margins: margin on first and last child](https://codepen.io/rachelandrew/pen/BgrKGp) by <a href="https://codepen.io/rachelandrew">Rachel Andrew</a>.{{< /codepen >}}

This is because the margin on the child collapses with any margin on the parent thus ending up on the outside of the parent. You can see this if you inspect the first child using DevTools. The highlighted yellow area is the margin.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4bcc95c4-cc61-4682-a38f-c4e7bb4279f3/devtools-margin.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4bcc95c4-cc61-4682-a38f-c4e7bb4279f3/devtools-margin.png" sizes="100vw" caption="DepvTools can help you see where your margin ends up" alt="The item with a yellow highlighted margin showing outside the parent">}}

## Only Block Margins Collapse

The last example also highlights something about margin collapsing. In CSS2, only vertical margins are specified to collapse &mdash; that is the top and bottom margins on an element if you are in a horizontal writing mode. So the left and right margins above are not collapsing and ending up outside the wrapper.

**Note**: *It is worth remembering that margins only collapse in the block direction, such as between paragraphs.*

{{% ad-panel-leaderboard %}}

## Things Which Prevent Margin Collapsing

Margins never collapse if an item has absolute positioning, or is floated. However, assuming you have run into one of the places where margins collapse outlined above, how can you stop those margins collapsing?

The first thing that stops collapsing is situations where there is something between the elements in question.

For example, a box completely empty of content will not collapse it’s top and bottom margin if it has a border, or padding applied. In the example below I have added 1px of padding to the box. There is now a 50-pixel margin above and below the box.

{{< codepen height="480" theme_id="light" slug_hash="gNeMpg" default_tab="result" breakout="true" user="rachelandrew" editable="true" data-editable="true" >}}See the Pen [Margins: empty boxes with padding do not collapse](https://codepen.io/rachelandrew/pen/gNeMpg) by <a href="https://codepen.io/rachelandrew">Rachel Andrew</a>.{{< /codepen >}}

This has logic behind it, if the box is completely empty with no border or padding, it is essentially invisible. It might be an empty paragraph element thrown into the markup by your CMS. If your CMS was adding redundant paragraph elements, you probably wouldn’t want them to cause large gaps between the other paragraphs due to their margins being honored. Add anything to the box, and you will get those gaps.

Similar behavior can be seen with margins on first or last children which collapse through the parent. If we add a border to the parent, the margins on the children stay inside.

{{< codepen height="480" theme_id="light" slug_hash="vqRKKX" default_tab="result" breakout="true" user="rachelandrew" editable="true" data-editable="true" >}}See the Pen [Margins: margin on first and last child doesn’t collapse if the parent has a border](https://codepen.io/rachelandrew/pen/vqRKKX) by <a href="https://codepen.io/rachelandrew">Rachel Andrew</a>.{{< /codepen >}}

Once again, there is some logic to the behavior. If you have wrapping elements for semantic purposes that do not display visually, you probably don’t want them to introduce big gaps in the display. This made a lot of sense when the web was mostly text. It is less useful as behavior when we are using elements to lay out a design.

### Creating a Block Formatting Context

A new Block Formatting Context (BFC) will also prevent margin collapsing through the containing element. If we look again at the example of the first and last child, ending up with their margins outside of the wrapper, and give the wrapper `display: flow-root`, thus creating a new BFC, the margins stay inside.

{{< codepen height="480" theme_id="light" slug_hash="VJXjEp" default_tab="result" breakout="true" user="rachelandrew" editable="true" data-editable="true" >}}See the Pen [Margins: a new Block Formatting Context contains margins](https://codepen.io/rachelandrew/pen/VJXjEp) by <a href="https://codepen.io/rachelandrew">Rachel Andrew</a>.{{< /codepen >}}

To find out more about `display: flow-root`, read my article "[Understanding CSS Layout And The Block Formatting Context](https://www.smashingmagazine.com//2017/12/understanding-css-layout-block-formatting-context/)". Changing the value of the `overflow` property to `auto` will have the same effect, as this also creates a new BFC, although it may also create scrollbars that you didn’t want in some scenarios.

{{% ad-panel-leaderboard %}}

### Flex And Grid Containers

Flex and Grid containers establish Flex and Grid _formatting contexts_ for their children, so they have different behavior to block layout. One of those differences is that margins do not collapse:

<blockquote>“A flex container establishes a new flex formatting context for its contents. This is the same as establishing a block formatting context, except that flex layout is used instead of block layout. For example, floats do not intrude into the flex container, and the flex container’s margins do not collapse with the margins of its contents.”<br /><br />&mdash; <a href="https://www.w3.org/TR/css-flexbox-1/#flex-containers">Flexbox Level 1</a></blockquote>

If we take the example above and make the wrapper into a flex container, displaying the items with `flex-direction: column`, you can see that the margins are now contained by the wrapper. Additionally, margins between adjacent flex items do not collapse with each other, so we end up with 100 pixels between flex items, the total of the 50 pixels on the top and bottom of the items.

{{< codepen height="480" theme_id="light" slug_hash="mZxreL" default_tab="result" breakout="true" user="rachelandrew" editable="true" data-editable="true" >}}See the Pen [Margins: margins on flex items do not collapse](https://codepen.io/rachelandrew/pen/mZxreL) by <a href="https://codepen.io/rachelandrew">Rachel Andrew</a>.{{< /codepen >}}

## Margin Strategies For Your Site

Due to margin collapsing, it is a good idea to come up with a consistent way of dealing with margins in your site. The simplest thing to do is to only define margins on the top _or_ bottom of elements. In that way, you should not run into margin collapsing issues too often as the side with a margin will always be adjacent to a side without a margin.

**Note**: *[Harry Roberts has an excellent post](https://csswizardry.com/2012/06/single-direction-margin-declarations/) detailing the reasons why setting margins only in one direction is a good idea, and not just due to solving collapsing margin issues.*

This solution doesn’t solve the issues you might run into with margins on children collapsing through their parent. That particular issue tends to be less common, and knowing _why_ it is happening can help you come up with a solution. An ideal solution to that is to give components which require it `display: flow-root`, as a fallback for older browsers you could use `overflow` to create a BFC, turn the parent into a flex container, or even introduce a single pixel of padding. Don’t forget that you can use feature queries to detect support for `display: flow-root` so only old browsers get a less optimal fix.

Most of the time, I find that knowing why margins collapse (or didn’t) is the key thing. You can then figure out on a case-by-case basis how to deal with it. Whatever you choose, make sure to share that information with your team. Quite often margin collapsing is a bit mysterious, so the reason for doing things to counter it may be non-obvious! A comment in your code goes a long way to help &mdash; you could even link to this article and help to share the margin collapsing knowledge.

I thought that I would round up this article with a few other margin-related pieces of information.

## Percentage Margins

When you use a percentage in CSS, it has to be a percentage of something. Margins (and padding) set using percentages will always be a percentage of the inline size (width in a horizontal writing mode) of the parent. This means that you will have equal-sized padding all the way around the element when using percentages.

In the CodePen example below, I have a wrapper which is 200 pixels wide, inside is a box which has a 10% margin, the margin is 20 pixels on all sides, that being 10% of 200.

{{< codepen height="480" theme_id="light" slug_hash="orqzrP" default_tab="result" breakout="true" user="rachelandrew" editable="true" data-editable="true" >}}See the Pen [Margins: percentage margins](https://codepen.io/rachelandrew/pen/orqzrP) by <a href="https://codepen.io/rachelandrew">Rachel Andrew</a>.{{< /codepen >}}

## Margins In A Flow-Relative World

We have been talking about vertical margins throughout this article, however, modern CSS tends to think about things in a flow relative rather than a physical way. Therefore, when we talk about vertical margins, we really are talking about margins in the block dimension. Those margins will be top and bottom if we are in a horizontal writing mode, but would be right and left in a vertical writing mode written left to right.

Once working with logical, flow relative directions it becomes easier to talk about block start and block end, rather than top and bottom. To make this easier, CSS has introduced the Logical Properties and Values specification. This maps flow relative properties onto the physical ones.

For margins, this gives us the following mappings (if we are working in English or any other horizontal writing mode with a left-to-right text direction).

- `margin-top` = `margin-block-start`
- `margin-right` = `margin-inline-end`
- `margin-bottom` = `margin-block-end`
- `margin-left` = `margin-inline-start`

We also have two new shorthands which allow for the setting of both blocks at once or both inline.

- `margin-block`
- `margin-inline`

In the next CodePen example, I have used these flow relative keywords and then changed the writing mode of the box, you can see how the margins follow the text direction rather than being tied to physical top, right, bottom, and left.

{{< codepen height="480" theme_id="light" slug_hash="BgrQRj" default_tab="result" breakout="true" user="rachelandrew" editable="true" data-editable="true" >}}See the Pen [Margins: flow relative margins](https://codepen.io/rachelandrew/pen/BgrQRj) by <a href="https://codepen.io/rachelandrew">Rachel Andrew</a>.{{< /codepen >}}

You can read more about logical properties and values on [MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Logical_Properties) or in my article "[Understanding Logical Properties And Values](https://www.smashingmagazine.com/2018/03/understanding-logical-properties-values/)" here on Smashing Magazine.

## To Wrap-Up

You now know most of what there is to know about margins! In short:

- Margin collapsing is a thing. Understanding why it happens and when it doesn’t will help you solve any problems it may cause.
- Setting margins in one direction only solves many margin related headaches.
- As with anything in CSS, share with your team the decisions you make, and comment your code.
- Thinking about block and inline dimensions rather than the physical top, right, bottom and left will help you as the web moves towards being writing mode agnostic.

{{< signature "il" >}}
