---
title: 'Copy Docs: Make Your Microcopy Full And Consistent, And Maintain It'
slug: copy-docs-microcopy
author: valeriia-panina
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dca1bf63-a585-487f-a4cd-8b884a009889/copy-docs-microcopy.png
date: 2020-11-26T10:30:00.000Z
summary: >-
  Copy docs is a framework that allows product designers and writers to manage their in-product copy in a smart way. In this article, Valeriia Panina shares her experience in how the copy docs technique turned out to be a game changer for her workflow.
description: >-
  Copy docs is a framework that allows product designers and writers to manage their in-product copy in a smart way. In this article, Valeriia Panina shares her experience in how the copy docs technique turned out to be a game changer for her workflow.
categories:
  - Design
  - Workflow
  - Tools
  - Microcopy
---

Remember all of the times you had to multiply your Figma or Sketch frames just so you can demonstrate single-word changes? Or having to mingle with the .json file in VS code whenever you needed to update that button text? What about irritating typos due to a lack of grammar checking plugins in most of the graphic editors? I’m afraid that calling copy docs (like any other framework) a silver bullet will be too much, but at least this technique can ease these struggles.

Let’s have a closer look.

## Some History And Credit

One of the early public [mentions of copy docs](https://medium.com/dropbox-design/how-to-improve-your-design-process-with-copy-docs-767f2d02377a) belongs to Andrea Drugay, a then UX writer at Dropbox. I encountered it during my certification in UX writing at the [UX Writing Hub](https://uxwritinghub.com/) Academy (*hi Yuval!*) in 2019. 

Since then, I’ve been largely using copy docs as a product designer and built on it to modify it to the needs of UX specialists at large, especially in small teams.

## What Is A Copy Doc?

It’s a document where you keep and update all your in-product texts, their instances, and describe their behavior.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/204c2ddc-e065-4b28-bf15-2d14401b1fa6/copy-docs-overview.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/204c2ddc-e065-4b28-bf15-2d14401b1fa6/copy-docs-overview.png" sizes="100vw" caption="Common structure: a frame name, a UI screenshot, and a table with two columns, the first being a namespace and the second its actual content plus annotations. NB: Here I’ll be demonstrating the copy doc technique on the Smashing Magazine website as if I worked on its UI from scratch in Figma; I did it in order to use an interface that looks familiar for you. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/204c2ddc-e065-4b28-bf15-2d14401b1fa6/copy-docs-overview.png'>Large preview</a>)" alt="A screenshot of a sample copy doc, demonstrating its elements" >}}

In this flow, Figma or Sketch is the ultimate source of UI elements while the copy doc is the ultimate source of in-product copy. It makes more sense: you use design tools for designing, and editing tools for working with content (including the handout process). All in all, it brings the work with in-product copy to the next level, both for the design specialist and the whole team.

## Reasons To Use Copy Docs

Right now you might feel a bit curious about using this technique but still skeptical. Right you are: there should be a very good reason to make your workflow more compound.

So let me give you some motive. 

### Copy Docs Can Go With Any Design Tool

It can be used along with any software you like. Figma, Sketch, XD &mdash; you name it.

### You Can Zero In On Content Solely

On one hand, a UX specialist’s focus is their dearest resource. On the other, the efficiency of the environment they are working in has a great impact on their ability. Copy docs level up both aspects. 

Switching environments helps to refresh one’s focus. And working with content in a content-native tool means fewer distractions.

For me, it is one of the most valuable benefits of copy docs. Especially when you are both a designer and a writer in your team.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fcc8df6d-2107-4c1d-8402-86fa7aa7d974/copy-docs-eye-path.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fcc8df6d-2107-4c1d-8402-86fa7aa7d974/copy-docs-eye-path.png" sizes="100vw" caption="Compare the path your eyes make when you want to progressively check your microcopy: when you are inside a mockup and inside a copy doc. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fcc8df6d-2107-4c1d-8402-86fa7aa7d974/copy-docs-eye-path.png'>Large preview</a>)" alt="A comparison of two trajectories of eye movement while working with in-product copy - in graphic and in content environments" >}}

Additionally, you will be more likely not to miss out on “hidden” states (error or success feedback, etc.) and can use various graphic means for annotations. And it becomes easier to describe complex logic like “If event X happens… then the button copy becomes Y…” &mdash; you literally change just the text, without mingling with the graphic.

Here you can object that working with copy outside an interface feels dubious. In reality, in 9 cases out of 10, you can clearly tell what length is reasonable. As for uncertain cases, you can always try a specific line in your interface when you really need it.

### Consistency Is Easy

While in IELTS the more synonyms you use the better, it is not the same in the UX field. For example, if you use the “Delete” term across your designs to mean an action of removing an item, but in a particular spot “Erase” for the same action pops in, it may confuse users: they might think that some other action is implied.

In a copy doc, you can quickly highlight all the instances of a word. It becomes handy when you want to check yourself. And if needed &mdash; say, you ran usability tests and discovered that in your very context “Erase” will do better, &mdash; you can do a bulk rename quickly and hand it out to developers or align your designs. Indeed, it is much better to fix a term in a doc and then just adapt your Figma or Sketch frames than to crawl over there hastily and peck at each element with the fear of skipping one. 

And it works in the opposite direction: sometimes you may want to split a term. For example, first, working with my own copy doc, I used the word “comment” to denote two different ideas: in the first case, I meant the native Google docs commenting tool, and in the second case I referred to my remarks in the body of the copy doc. Essentially they are different: the first one implies a ping-pong discussion with my team while the second one means my only informational notes to the developers on the item behavior. So now I am using “comments” and “annotations” correspondingly.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1d827360-a043-4552-9ea0-8e4e6d1a9089/copy-docs-consistency-terms.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1d827360-a043-4552-9ea0-8e4e6d1a9089/copy-docs-consistency-terms.png" sizes="100vw" caption="If we precisely distinguish terms, it keeps future discussions concise. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1d827360-a043-4552-9ea0-8e4e6d1a9089/copy-docs-consistency-terms.png'>Large preview</a>)" alt="The difference between two terms: a comment and an annotation" >}}

### Proofreaders Are Happy

The majority of language specialists usually work in Word-like formats. And here they can do an estimation based on word-count.

### Collaboration Is Nice And Deep

Since an editing soft provides a wonderful toolset catered for content-specific cooperation, now your team is taken to the next level of collaboration.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/63d17536-6c82-4ff2-86a8-aaca6b08b108/copy-docs-collaboration.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/63d17536-6c82-4ff2-86a8-aaca6b08b108/copy-docs-collaboration.png" sizes="100vw" caption="Mention people, get suggestions, assign tasks, count words, and many more. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/63d17536-6c82-4ff2-86a8-aaca6b08b108/copy-docs-collaboration.png'>Large preview</a>)" alt="Demo of Google doc native collaboration tools - assigned tasks and comments" >}}

And I already mentioned the benefits of the handout process. Now, in order to update the microcopy in live components, you actually hand out just the copy, organized and annotated.

### Files Are Light

With copy docs you avoid redundancy when you copy-paste frames with only textual changes &mdash; now you keep it in a separate dedicated document. Needless to say that it boosts performance.

### It means a “built-in” Grammarly for your designs

Haven’t you been dreaming of it every time you type a string of text in your Figma, Sketch, or XD mockups?

{{% feature-panel %}}

## How To Create A Copy Doc

These are the steps I follow when creating my copy docs.

### 1. Draft Your Interface

To start with copy docs, you need the skeleton of your interface. I prefer creating copy docs at the stage of mockups but you can start at the prototyping stage. However, if you follow a content-first approach, it is even possible to prototype with copy docs and then use them as a list of necessary elements while designing the UI. 

### 2. Create An Outline Of The Copy Doc

Create sections matching the names of your screens.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/eef40ffe-2c42-4eac-bd30-55178d922c92/copy-docs-backstage-outline.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/eef40ffe-2c42-4eac-bd30-55178d922c92/copy-docs-backstage-outline.png" sizes="100vw" caption="Apply styles and create a table of contents so you can navigate the document. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/eef40ffe-2c42-4eac-bd30-55178d922c92/copy-docs-backstage-outline.png'>Large preview</a>)" alt="A Google doc with headings per each UI section and a table of contents made of those headings" >}}

### 3. Paste Screenshots 

You should follow a “Heading + Screenshot + Table” pattern for every unit. 

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1953a921-dc40-43f0-bda5-f5dde2f2dd23/copy-docs-backstage-screenshots.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1953a921-dc40-43f0-bda5-f5dde2f2dd23/copy-docs-backstage-screenshots.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1953a921-dc40-43f0-bda5-f5dde2f2dd23/copy-docs-backstage-screenshots.png'>Large preview</a>)" alt="A sample screenshot pasted into a Google doc" >}}

### 4. Paste Tables

Ideally, you want to create an empty table with pre-set styles under each screenshot. For this, create a table for your first screen and fill it in. Then copy-paste the filled table under the second screenshot, clear, copy it again, and paste under the remaining screenshots multiple times. 

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dc786182-0265-4edf-a685-e455a2329ba2/copy-docs-backstage-tables.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dc786182-0265-4edf-a685-e455a2329ba2/copy-docs-backstage-tables.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dc786182-0265-4edf-a685-e455a2329ba2/copy-docs-backstage-tables.png'>Large preview</a>)" alt="A sample table created in a Google doc alongside the screenshot" >}}

### 5. Fill It In

All set for your _copy work_.

Work screen by screen. Start with namespaces. Then, fill in the very microcopy, avoiding common pitfalls that I share below.

### 6. Keep Your Copy Doc Up-to-Date

So, your copy doc is all set. Now you should pick up a habit of reflecting all the copy updates immediately. Anytime your copy doc is opened, it should show the most actual in-product copy. 

It may require some work but the good news is that you need not update the screenshots unless they undergo dramatic changes.

As for your Figma, Sketch, or XD files, it is strongly advised that you reflect changes in copy as well, but now it is your second priority &mdash; you work with the copy in a copy doc and then just align your design files later.

{{% ad-panel-leaderboard %}}

## Tips And Pitfalls

### Pay Attention to Taxonomy

The common namespace for a content item will look like:

<blockquote>Section / Subsection / Group / … / Item <br /><br />Table / Head / 1st column</blockquote>

Make sure you match names with your UI components’ names. 

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/617d8d49-3a39-4063-b5d6-c95bce85f5f2/copy-docs-consistency-ui-elements.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/617d8d49-3a39-4063-b5d6-c95bce85f5f2/copy-docs-consistency-ui-elements.png" sizes="100vw" caption="Say, if somebody wants to check in your copy doc Cards that they found in the design file, they should be Cards, not Boxes. etc. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/617d8d49-3a39-4063-b5d6-c95bce85f5f2/copy-docs-consistency-ui-elements.png'>Large preview</a>)" alt="A screenshot of a Components page in Figma, showing the name of an element and a screenshot of a copy doc with a corresponding element name that match" >}}

And, in their turn, the components should match the development framework. If you are not sure what name to pick up, consult with your developers. 

### Create The Legend

Being outside the design tool, you can use a variety of graphics to communicate ideas, not esthetics.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/43b25052-95c2-4794-bec4-c283a8cf6018/copy-docs-legend.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/43b25052-95c2-4794-bec4-c283a8cf6018/copy-docs-legend.png" sizes="100vw" caption="A legend functions like onboarding: it lets others navigate the document without extra explanations. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/43b25052-95c2-4794-bec4-c283a8cf6018/copy-docs-legend.png'>Large preview</a>)" alt="A starting page of a copy doc with all necessary marks and explanations that will be used throughout the doc" >}}

For example, use:

*   Highlights for variables
*   Brackets for annotations
*   Emoji or Unicode symbols for states

And be consistent &mdash; use the same highlighting method for every corresponding event. Remember about synonyms?

Also, remember about accessibility: it’s a good idea when different items differ with several parameters. 

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ac623e9a-93cd-495d-8bfd-5e0a96f0175c/copy-docs-annotations-accessibility.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ac623e9a-93cd-495d-8bfd-5e0a96f0175c/copy-docs-annotations-accessibility.png" sizes="100vw" caption="I never mark annotations with just a different color. Instead, I use both color and brackets. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ac623e9a-93cd-495d-8bfd-5e0a96f0175c/copy-docs-annotations-accessibility.png'>Large preview</a>)" alt="A part of a table with annotation and a variable that use different graphic language" >}}

### Avoid Redundancy And Conflicting Strings

Don’t reuse identical items.

For example, if you have a page with a common title and tabs, mention the title in the first unit, and later in other units don’t mention them again but reflect only changes on those pages.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0029ecd1-f0b9-4bc8-ae1a-2c8773eed10c/copy-docs-reuse.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0029ecd1-f0b9-4bc8-ae1a-2c8773eed10c/copy-docs-reuse.png" sizes="100vw" caption="Either do not include the second instance of the same item or leave a link to its initial record. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0029ecd1-f0b9-4bc8-ae1a-2c8773eed10c/copy-docs-reuse.png'>Large preview</a>)" alt="A part of a table with a repeated element and a link to its first instance" >}}

### Think Of States

Surely, the instances of your elements can vary, but below are the most common ones you need to think of. 

Feedback: messages, alerts, notifications, etc.

*   Info
*   Success
*   Warning
*   Error

Inputs and the like:

*   Placeholder
*   Typing
*   Filled
*   Null
*   Various errors

You get the idea. 

{{% ad-panel-leaderboard %}}

Literally use them as a checklist to provide exhaustive content for every change of your elements’ state.

As for their appearance, you can either create a separate row for each instance or group them in one cell, annotated. 

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b3248b65-12fd-4062-9a37-a08ed2ce0a31/copy-docs-rows-or-in-a-cell.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b3248b65-12fd-4062-9a37-a08ed2ce0a31/copy-docs-rows-or-in-a-cell.png" sizes="100vw" caption="You can start every item &mdash; be it an instance or a regular interface element &mdash; with a new row or combine them in one cell, adding annotations. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b3248b65-12fd-4062-9a37-a08ed2ce0a31/copy-docs-rows-or-in-a-cell.png'>Large preview</a>)" alt="Two ways of showing item - using a separate row for each item combining them in a cell" >}}

### Think Of Variables

Variables are those parts of copy that change with the context. Usually, it is date and time, users’ names, numbers, etc.

Probably, you already considered them at the stage of Information architecture or, partially, in Editorial policy. And now a copy doc is just the place to reflect what data is constant, and what data changes depending on the context, and how.

Highlight variables and choose their form. Follow the same counter-redundancy rule: state the variable’s form once, preferably at the beginning, and then refer to it across your doc. 

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d42e1e4d-8caa-4c84-a443-5f3bfa18584a/copy-docs-references.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d42e1e4d-8caa-4c84-a443-5f3bfa18584a/copy-docs-references.png" sizes="100vw" caption="I show the common date format at the beginning of the doc and after just refer to it as &#91;Date, default&#93;. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d42e1e4d-8caa-4c84-a443-5f3bfa18584a/copy-docs-references.png'>Large preview</a>)" alt="Three screenshots - how the date looks in the interface, how it is referred to throughout the copy doc, and how its basic form is stated in the legend " >}}

Do not forget to think of the minimum and maximum value of every variable &mdash; if you spot that it affects the UI in some way, you can leave a corresponding annotation.

## Afterword (And A Bonus)

This is pretty much it. The copy docs technique was a game changer for my workflow and I’d be happy if it boosts yours, too!

And please, let me know how you use it or, maybe, cater this framework to your needs. Screenshots, description of your experience, audio or video messages &mdash; anything will be great! I mean it. 

And I prepared a template for you. So, copy your [[Template] Copy doc](https://docs.google.com/document/d/1523iSM2IXjiibr6wGClD1-S2lOQsfh4bNiQmSTo9Yi4/edit?usp=sharing) &mdash; and stay safe!

{{< signature "ra, il" >}}
