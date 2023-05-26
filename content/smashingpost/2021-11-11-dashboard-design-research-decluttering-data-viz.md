---
title: 'From Good To Great In Dashboard Design: Research, Decluttering And Data Viz'
slug: dashboard-design-research-decluttering-data-viz
author: adam-fard
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/835f0cba-e214-437a-a025-e69ba7691997/dashboard-design-research-decluttering-data-viz.jpg
date: 2021-11-11T14:00:00.000Z
summary: >-
  Dribbbleshots just might be the hotbed of questionable dashboards. Striking visuals, little context, and no research: all recipes for mediocrity. Mediocrity won’t do. We’ll pursue greatness. And in that pursuit, we’ll cover research, decluttering, and data visualization. 
description: >-
  Dribbbleshots just might be the hotbed of questionable dashboards. Striking visuals, little context, and no research: all recipes for mediocrity. Mediocrity won’t do. We’ll pursue greatness. And in that pursuit, we’ll cover research, decluttering, and data visualization.
categories:
  - Design Patterns
  - Data Visualization
  - UX
  - Techniques
---

Even if it’s a blessing in disguise, discarding elements of your work is no fun. Tossing out suboptimal parts of our design can be a daunting task, especially after you’ve invested hours of work into it. But make no mistake, this is a bias most designers are prone to. We can get too attached to things we’ve created, despite them not providing any real value to our users. Here lies the difference between *okay* and *great* dashboard design. The former is fairly easy to achieve. The latter isn’t.

I’ve compiled a few things that I’ve learned throughout my career with regard to dashboard design. In this article, we’ll talk about research, decluttering, and data visualization, as well as how these things can make your dashboard design better.

## Definition

A dashboard is a part of an application that displays global information about the app’s usage or any other external data. They come in different kinds, from relatively simplistic one-layered dashboards like this one:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a846211d-35b3-44b0-97b0-1dc98854332b/image-1-one-layered-dashboard.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a846211d-35b3-44b0-97b0-1dc98854332b/image-1-one-layered-dashboard.png" width="800" height="303" sizes="100vw" caption="A simple one-layered dashboard (Image source: <a href='https://dribbble.com/shots/14058657-Organic-Project-Management-Dashboard'>Dribbble</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a846211d-35b3-44b0-97b0-1dc98854332b/image-1-one-layered-dashboard.png'>Large preview</a>)" alt="A simple one-layered dashboard" >}}

While others are more complex and multilayered ones like the one below:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a0918f69-3d8b-4b02-a153-792ff50b7541/image-2-a-more-complex-dashboard.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a0918f69-3d8b-4b02-a153-792ff50b7541/image-2-a-more-complex-dashboard.png" width="800" height="304" sizes="100vw" caption="A complex multi-layered dashboard (Image source: <a href='https://dribbble.com/shots/10495812-Dark-mode-for-YogaPlanner'>Dribbble</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a0918f69-3d8b-4b02-a153-792ff50b7541/image-2-a-more-complex-dashboard.png'>Large preview</a>)" alt="A complex multi-layered dashboard" >}}

The recommendations we will provide in this article apply to a wide range of dashboards, regardless of their complexity.

Before diving into our arguments, first, let’s sort out what I mean by “mediocre” and “great”. These terms imply a value system that isn’t exactly conventional, so I owe you an explanation.

## Mediocre vs Great Dashboard Design

The difference between “mediocre” and “great”, I believe, lies in the process. There’s also a continuum involved between these two categories. In the context of this article, the axes of this continuum are as follows:

- Sourcing inspiration (copying),
- Research (referred to in the next section as “homework”),
- Design Validation (substantiating design decisions with data),
- Data Visualization,
- Color Palette.

<table class="tablesaw break-out">
	<thead>
		<tr>
			<th></th>
      <th>Mediocre</th>
			<th>Great</th>
		</tr>
	</thead>
	<tbody>
		<tr>
      <td><strong>Sourcing inspiration</strong></td>
			<td>✅</td>
      <td>✅</td>
		</tr>
    <tr>
			<td><strong>Research</strong></td>
			<td>Limited and fragmented</td>
      <td>Consistent and purposeful</td>
		</tr>
    <tr>
			<td><strong>Design Validation</strong></td>
			<td>Limited to internal stakeholders</td>
      <td>Inclusive of both internal and end-users</td>
		</tr>
    <tr>
			<td><strong>Data Visualization</strong></td>
			<td>Heavily focused on aesthetics and trends</td>
      <td>Data viz solutions are consistent with its purpose; a good balance between efficiency and complexity;</td>
		</tr>
    <tr>
			<td><strong>Color palette</strong></td>
			<td>Arbitrary / trend-based</td>
      <td>Utilizable of color connotations, and alignment with brand values</td>
		</tr>
	</tbody>
</table>

*(Throughout this article, all references to mediocrity are based on these distinctions)*

Now that we’ve sorted out the definitions, let’s quickly give an overview of my arguments. In this article, I suggest that, as opposed to mediocre dashboards, great ones require:

- Research,
- A healthy dose of cluttering & decluttering,
- A thought-through color palette.

First, let’s break down research, or “homework” as I like to call it. How do you even do “homework” as a designer? Is it ok to copy someone else’s work as long as you don’t make it obvious? Or do you start from scratch every time? &mdash; Let’s think this through.

{{% feature-panel %}}

## Doing Your Own Homework VS Copying Your Peers

Sure, there’s always the option of copying and tweaking what your competitors already offer. Or, if there are no close equivalents, you can just “Frankenstein” the elements together from similar dashboards. This indeed sounds easier than “reinventing the wheel”. “*Good artists copy, great artists steal,*” as Picasso’s quote goes &mdash; but, unfortunately, this approach is likely to doom your design to mediocrity. Let me elaborate.

A quick disclaimer: if what you’re looking for is to learn, then by all means copy great designs and try to learn from them. However, if you’re working on commercial / “real” projects, then copying alone doesn’t do.

First of all, theoretically speaking, you could strike gold by copying great dashboards. There’s a catch, however. What is the likelihood that your source of inspiration is well-researched, practical, and most importantly *applicable to your particular situation*? Are the dashboards you’ve found worth stealing? Who knows. If you ask me, however, I wouldn’t bet on it. This ties in well with the ideas Austin Kleon outlined in his book *Steal like an artist*. 

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e8649c90-1a4d-44b8-ae3b-c913091364f3/image-3-is-it-worth-stealing.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e8649c90-1a4d-44b8-ae3b-c913091364f3/image-3-is-it-worth-stealing.png" width="800" height="510" sizes="100vw" caption="(Image source: <a href='https://www.amazon.com/Steal-Like-Artist-Things-Creative/dp/0761169253'>Amazon</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e8649c90-1a4d-44b8-ae3b-c913091364f3/image-3-is-it-worth-stealing.png'>Large preview</a>)" alt="A diagram: is it worth stealing? If yes, then steal it and move on. If not, don’t steal it and move on." >}}

Secondly, when you’re sourcing inspiration, all you see is the end product: a colorful nice-looking dashboard. Rarely can you find inspiration accompanied by a thorough analysis of the process, research, and decision-making involved. This leads to something akin to a cargo cult, i.e. replicating the patterns you see without understanding why. 

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3d3f7ed5-688a-4b44-809d-b9228f05825b/image-4-dashboard-cargo-cult.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3d3f7ed5-688a-4b44-809d-b9228f05825b/image-4-dashboard-cargo-cult.png" width="800" height="436" sizes="100vw" caption="Don’t join the ranks of Dashboard cargo cultists. 😄 (Dashboard credit: Source: <a href='https://dribbble.com/shots/10711741-Free-UI-Kit-for-Figma-Online-Courses-Dashboard'>Dribbble</a>, <a href='https://bigalmanack.com/dont-be-a-cargo-cult/'>BigAlmanac</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3d3f7ed5-688a-4b44-809d-b9228f05825b/image-4-dashboard-cargo-cult.png'>Large preview</a>)" alt="A plane out of straw positioned on the landscape of a dashboard as a background" >}}

Finally, another unfortunate side effect of merely copying is that it’s not consistent. You can’t play the odds and win every time. That’s not to say that a “proper” [design process](https://adamfard.com/ux-design-process) is foolproof. I believe that following the principles I outline in this article will make your designs consistently better, so you can “strike gold” with a higher degree of reliability and replicability.

{{% pull-quote %}}
 Simply put, following a proper process and having a command of design principles, as opposed to mindlessly copying, gives you a better chance of coming up with usable designs with fewer iterations and useability testing sessions.
{{% /pull-quote %}}

So how do you strike a balance between “copying” and “doing your own homework”? Here’s what I think. On top of “stealing” (ahem.. looking for inspiration), also **talk to your users**.

I 👏 can’t 👏 stress 👏 this 👏enough.

I bet we’re all (myself included) tired of hearing this mantra. “Talking to users” is like exercising or eating healthy &mdash; everyone knows they should do more of it, but few actually do it.

<blockquote>“People ignore design that ignores people”.<br /><br />&mdash; <a href="https://frankchimero.com/">Frank Chimero</a></blockquote>

Is there a worse way to ignore users than excluding them from the conversation altogether?

Alright, talking to users is important. That much is clear. What isn’t self-explanatory though is how exactly this communication should take place &mdash; let’s go over a couple of activities to examine a couple of ways.

### User interviews:

Here are a few questions worth looking into when designing a dashboard. 

- What information do users need the most?
- What is the purpose of this dashboard?
- What do users consult this dashboard for?
- How do they go about looking for this information currently?

[In this piece](https://www.toptal.com/designers/data-visualization/dashboard-design-best-practices), Stelian Suboti, a UI & UX designer with more than 7 years of experience, the author claims that:

{{% pull-quote %}}
 Truly valuable insight can come out of a short user research phase with just five users — and it will save an enormous amount of time down the line.
{{% /pull-quote %}}

Doing research (user interviews in this case) is the first step of the design thinking process (empathy), as well as the UX process in general. 

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e48d7b20-fe13-427e-8e91-4cbdd9d29ebd/image-5-usability-testing.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e48d7b20-fe13-427e-8e91-4cbdd9d29ebd/image-5-usability-testing.png" width="800" height="557" sizes="100vw" caption="(Image source: <a href='https://adamfard.com/projects/saas-b2b-platform'>Adam Fard Studio</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e48d7b20-fe13-427e-8e91-4cbdd9d29ebd/image-5-usability-testing.png'>Large preview</a>)" alt="research of the user interview" >}}

### Card-Sorting

<blockquote>“Card sorting by its very nature, is a method you would use when you want to discover categories, groups, or interrelationships. Use this method when you want to know how users respond to visual cues and you want to capture the similarities and differences.”<br /><br />&mdash; <a href="https://think.design/user-design-research/card-sorting/">Think Design</a></blockquote>

As we’ve just learned, card sorting helps us understand how users group and categorize information. In practical terms, card sorting looks something like this 👇  

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/04b68278-5886-4e2e-8880-55d5c56963ba/18-dashboard-design-research-decluttering-data-viz.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/04b68278-5886-4e2e-8880-55d5c56963ba/18-dashboard-design-research-decluttering-data-viz.png" width="800" height="515" sizes="100vw" caption="(Image source: <a href='https://medium.com/@shouldibuythisforyou/heuristics-e2f0982b435a'>Medium</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/04b68278-5886-4e2e-8880-55d5c56963ba/18-dashboard-design-research-decluttering-data-viz.png'>Large preview</a>)" alt="card-sorting with different color stickers" >}}

You generally want to split your dashboard into “atoms”, bits of information of the smallest size, so that the participants can establish the relationships among these elements. This is how you could build the information hierarchy within the dashboard that’s consistent with users’ mental models. 

### Usability Testing

[Usability testing](https://adamfard.com/blog/usability-testing) is arguably the most important and insightful research activity you can conduct with regard to dashboard design. Playing by ear and skipping this step altogether just might be the biggest cardinal sin of UX design.

Here’s what Nielsen Norman Group, the world’s leading product design authority, [has to say](https://www.nngroup.com/articles/usability-testing-101/) about usability testing: 

<blockquote>“Even the best UX designers can’t design a perfect &mdash; or even good enough &mdash; user experience without <a href="https://www.nngroup.com/articles/parallel-and-iterative-design/">iterative design</a> driven by observations of real users and of their interactions with the design.”</blockquote>

In practical terms, you would want to conduct usability testing sessions after card sorting and user interviews. The latter two activities blended with your own assumptions should result in early dashboard versions. These rough ideas will then need to be tested and iterated on from sketches, and low-fi wireframes all the way to a high-fidelity prototype.

Now that we discussed the research methods, we can safely move on to my second argument, which is all about decluttering. How do you know if your dashboard is cluttered? Does the “less is more” principle work every time? &mdash; These are the topics we’re tackling next.

## To Declutter Or Not To Declutter

In a conventional sense, decluttering is nearly synonymous with simplifying. Moreover, the practice of “keep it simple stupid” (KISS) has become somewhat of a design truism. The simpler the better, right? I wish it was that simple (no pun intended). 

A cluttered design, by definition, overwhelms its users. That’s not to say that an app can’t have a learning curve. Adobe products are probably a textbook definition of what “overwhelming a first-time user” means. 

Let’s take a look at the following dashboard:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/39a2f2a8-1da7-4ecb-a963-37be2ecb978e/10-dashboard-design-research-decluttering-data-viz.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/39a2f2a8-1da7-4ecb-a963-37be2ecb978e/10-dashboard-design-research-decluttering-data-viz.png" width="800" height="516" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/39a2f2a8-1da7-4ecb-a963-37be2ecb978e/10-dashboard-design-research-decluttering-data-viz.png'>Large preview</a>)" alt="An ostensibly complex dashboard with financial information" >}}

This is an excellent example of what might be considered “cluttered”. A closer look at the dashboard will tell you that it has to do with stock (index) price movement, trading volume, economic events, etc. If you think that this looks intimidating &mdash; you’re right. For an average user, it probably is. I’d wager, though, that the people qualified to use this kind of software actually benefit from this complexity &mdash; it allows them to work efficiently. Obscuring much of the information presented in this dashboard will only result in unnecessary clicks and excessive friction.

Now let’s try to take a look at something seemingly decluttered and “clean”. By the way, this particular dashboard, designed by [Bhojendra Rauniyar](https://www.uplabs.com/bhojendra), won in the minimal dashboard challenge by UpLabs. Congrats to Bhojendra!

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1f8f2fa3-e0a3-4582-9737-f0a304b22455/26-dashboard-design-research-decluttering-data-viz.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1f8f2fa3-e0a3-4582-9737-f0a304b22455/26-dashboard-design-research-decluttering-data-viz.png" width="800" height="600" sizes="100vw" caption="(Image source: <a href='https://www.uplabs.com/challenges/minimal-dashboard-challenge/results'>UpLabs</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1f8f2fa3-e0a3-4582-9737-f0a304b22455/26-dashboard-design-research-decluttering-data-viz.png'>Large preview</a>)" alt="An ostensibly simple but poorly usable dashboard" >}}

Before I start critiquing the dashboard above, here’s a disclaimer. First of all, this is a dribbble shot, so we can’t be certain whether it’s an isolated piece of design or a part of a product. Secondly, I don’t have access to the designer to ask for his rationale behind certain design decisions. Thirdly, I do not know whether this design has been tested and the full context of its usage. As such, all I have left is to speculate and assume. I hope, for educational purposes, that will do.

Let’s start with the chart. It compares client ratings with earnings. I’m left to wonder though what values define these two categories? The values have to be the same since both curves are on the same graph. So do we measure earnings in average rating or rating in dollars? Additionally, there are no labels for the scale, so I can’t even be sure of the units of measurement. What would probably be more useful is having separate graphs for key metrics with clear labels, i.e. to introduce “extra complexity”.

Additionally, the stats alone are not very valuable. Is earning “5k” in “1.8k” hours a good result? How does that compare to my peers? What are my dynamics?

That’s not to say that the dashboard I mentioned first is perfect and the second one is bad. You could argue that both of these require further work. My point is that decluttering for the sake of decluttering is a poor design maxim. 

Cluttered apps are unnecessarily overwhelming and hard to navigate. How do you know if an app is all of the above? Presto! That’s right, you talk to the users and have usability testing sessions with them. Other than usability testings, there are a few other practices that will help ensure that your interface is not cluttered:

- Clear information hierarchy;
- The use of modals or panels;
- On-hover interactions;
- Two to three colors;
- White space, plenty of it.

Now that we went through research and cluttering, we can move on to data visualization. Data visualization is irreplaceable for many reasons. It allows you to:

- See patterns,
- Compare data,
- Articulate the information visually,
- Track data dynamics.

Does this ring a bell? Exactly &mdash; this is pretty much everything that a dashboard should do. It’s no coincidence that almost all dashboards feature graphs and charts. Therefore, being competent at data visualization directly translates into being a competent dashboard designer. Let’s zoom in on that.

{{% ad-panel-leaderboard %}}

## Step Up Your Data Visualization Game

There are multiple types of charts available, thus we need to choose wisely. The sunburst chart does look awesome, but is it as clear and transparent as the pie chart? Perhaps. That really does depend on your users. Types of charts aside, there are also colors, their semantics and so many other things that add to the complexity of data visualization in dashboard design. 

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/92f9d4a7-02cb-4f94-be65-cca9d7b75605/image-9-types-of-charts.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/92f9d4a7-02cb-4f94-be65-cca9d7b75605/image-9-types-of-charts.png" width="800" height="497" sizes="100vw" caption="(Image source: <a href='https://theunspokenpitch.com/charts/'>The Unspoken Pitch</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/92f9d4a7-02cb-4f94-be65-cca9d7b75605/image-9-types-of-charts.png'>Large preview</a>)" alt="An infographic with 30 different kinds of charts" >}}

In this section, I will do my best to outline some of the data visualization best practices and their application in dashboard design. Let’s start with colors. 

This section is largely based on the research of [Claus O. Wilke](https://clauswilke.com/), Professor in Molecular Evolution at The University of Texas at Austin, and the author of *Fundamentals of Data Visualization*.

### Color In Dashboard Design

Let’s address the issue with numbers first. How many colors should you use in UI design and dashboard design in particular? &mdash; Frankly, there’s no magic number of colors that works no matter what. However, if I were to recommend you a number, it would be 5. That doesn’t include shades if the intensity of the color represents a value or semantic colors if you need them (e.g. red for error messages or green for success messages). 

Why 5? Well, there’s a 6:3:1 “golden” rule of visual design. These numbers represent the proportion among three brand colors: main, secondary, and accent. However, you should remember that on top of these three colors, you’re likely going to need some variation of white and black for text and its background.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/866b7b67-1262-4d5d-850c-10ca99fce0c4/20-dashboard-design-research-decluttering-data-viz.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/866b7b67-1262-4d5d-850c-10ca99fce0c4/20-dashboard-design-research-decluttering-data-viz.png" width="800" height="378" sizes="100vw" caption="(Image credit: <a href='https://www.qed42.com/insights/coe/design/understanding-colors-ui-design'>QED42</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/866b7b67-1262-4d5d-850c-10ca99fce0c4/20-dashboard-design-research-decluttering-data-viz.png'>Large preview</a>)" alt="An example of three color palettes" >}}

Another thing to use colors for is to distinguish among different entities. Here are a few common color palettes.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ef47a0c3-e8aa-4475-91a3-461106d4e492/16-dashboard-design-research-decluttering-data-viz.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ef47a0c3-e8aa-4475-91a3-461106d4e492/16-dashboard-design-research-decluttering-data-viz.png" width="800" height="336" sizes="100vw" caption="(Image source: <a href='https://www.oreilly.com/library/view/fundamentals-of-data/9781492031079/ch04.html'>Oreiily</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ef47a0c3-e8aa-4475-91a3-461106d4e492/16-dashboard-design-research-decluttering-data-viz.png'>Large preview</a>)" alt="An example of three monochromatic pallets" >}}

Use monochromatic color palettes if showing information within a single category. That way you can introduce another dimension to your chart that’s easy to read. For example, the more intense the colors, the higher the value and vice versa.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b6477891-29e7-4be2-ac35-57fbfc5d32e4/2-dashboard-design-research-decluttering-data-viz.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b6477891-29e7-4be2-ac35-57fbfc5d32e4/2-dashboard-design-research-decluttering-data-viz.png" width="800" height="350" sizes="100vw" caption="(Image source: <a href='https://clauswilke.com/dataviz/color-basics.html'>Claus Wilke</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b6477891-29e7-4be2-ac35-57fbfc5d32e4/2-dashboard-design-research-decluttering-data-viz.png'>Large preview</a>)" alt="An example of three monochromatic pallets" >}}

Here’s an example:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ad00201d-4bce-49e2-9b76-0e7692cf58bd/23-dashboard-design-research-decluttering-data-viz.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ad00201d-4bce-49e2-9b76-0e7692cf58bd/23-dashboard-design-research-decluttering-data-viz.png" width="800" height="545" sizes="100vw" caption="(Image source: <a href='https://wilkelab.org/practicalgg/reference/texas_income.html'>Wilke Lab</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ad00201d-4bce-49e2-9b76-0e7692cf58bd/23-dashboard-design-research-decluttering-data-viz.png'>Large preview</a>)" alt="A map of Texas indicating the county income" >}}

What you can also do is pick two colors to represent the opposite ends of a spectrum. That way you can easily tell apart values that belong to different extremes. Here’s an example:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3057ebfc-5285-400b-adfa-e1b10cbf4ae3/image-13-map-of-the-us.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3057ebfc-5285-400b-adfa-e1b10cbf4ae3/image-13-map-of-the-us.png" width="800" height="515" sizes="100vw" caption="(Image source: <a href='https://www.dallasnews.com/business/2018/06/21/when-will-latinos-outnumber-whites-in-texas-experts-have-a-new-prediction/'>Dallas News</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3057ebfc-5285-400b-adfa-e1b10cbf4ae3/image-13-map-of-the-us.png'>Large preview</a>)" alt="The map of the United States indicating the change in average age" >}}

Here are a few color palettes for this approach you can choose:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/23451848-6f12-4ead-8fae-ca3fd4349a55/image-14-diverging-color-schemes.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/23451848-6f12-4ead-8fae-ca3fd4349a55/image-14-diverging-color-schemes.png" width="500" height="250" sizes="100vw" caption="(Image source: <a href='https://betterfigures.org/2015/06/23/picking-a-colour-scale-for-scientific-graphics/'>Better Figures</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/23451848-6f12-4ead-8fae-ca3fd4349a55/image-14-diverging-color-schemes.png'>Large preview</a>)" alt="An example of diverging color pallets" >}}

### Beware Of Colors Semantics

Now that we went through the approaches you can take with using colors, it should also be noted that colors elicit subconscious reactions. These reactions are often referred to as “color semantics”.

When comparing 2 groups, using colors like red and green (because of the semantics associated with these colors) might lead to misrepresentation. Red, for instance, is often associated with danger, failure, and poor performance.

Take a look at the graphs below, which illustrate the math performance of two classes. We might automatically assume that students on the graph on the left in Class A are performing poorly, due to the fact that the values are represented with red. Red, especially in combination with green, often elicits such an interpretation.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5f0c0dbe-e0cf-4b89-8f25-d3f404bf0492/image-15-semantics.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5f0c0dbe-e0cf-4b89-8f25-d3f404bf0492/image-15-semantics.png" width="800" height="482" sizes="100vw" caption="(Image source: <a href='https://adamfard.com/projects/edtech-saas-design'>Adam Fard Studio</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5f0c0dbe-e0cf-4b89-8f25-d3f404bf0492/image-15-semantics.png'>Large preview</a>)" alt="Two scatter plot charts are compared side by side. The only difference between the charts is the colors used. The left chart uses blue and green which bear no connotation, while the one on the right uses red and green that imply a connotation." >}}

However, there are cases where this semantic difference can be used to our advantage like in the example below, i.e. using red to display performance that’s below average, and green for above. Also, note that it’s more natural for people to instinctively associate values on top as greater than those below. The graph below illustrates the last point.  

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/76741025-e3f0-429b-84c7-b57ebcbb84ad/image-16-semantics.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/76741025-e3f0-429b-84c7-b57ebcbb84ad/image-16-semantics.png" width="800" height="485" sizes="100vw" caption="(Image source: <a href='https://adamfard.com/projects/edtech-saas-design'>Adam Fard Studio</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/76741025-e3f0-429b-84c7-b57ebcbb84ad/image-16-semantics.png'>Large preview</a>)" alt="An example of two bar charts. The first chart doesn’t utilize the color semantics, while the other one does." >}}

As you can see, green represents students who perform above average, while red is reserved for those who underperform. Semantic color cues make this chart a lot more readable than it would otherwise be with another color scheme.

{{% ad-panel-leaderboard %}}

### On Which Charts To Use

Data visualization can induce a fair amount of friction when done incorrectly. Make sure to choose the most suitable type of chart to deliver the right kind of data. Below, you’ll find a more or less comprehensive list of charts you can use to represent the information featured in your dashboard, depending on the roles they fulfill.

**NB:** *Most charts serve more than one purpose. For instance, a pie chart is used to compare values, show composition, and data distribution. As such, I will mention these charts multiple times depending on the use case. However, I will only give a brief explanation for each chart once.*

#### Compare

- **Pie**  
Typically used to represent fractions of a whole. Pie charts work great whenever you need to compare a relatively low number of segments that are comparable in terms of their size. Conversely, having too many segments or tiny segments makes the chart too hard to read. A major con of pie charts is their inability to show changes over time.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9b08e220-e727-4a8f-b0f9-e50711798fa6/image-17-piechart-example.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9b08e220-e727-4a8f-b0f9-e50711798fa6/image-17-piechart-example.png" width="799" height="449" sizes="100vw" caption="(Image source: <a href='https://exceljet.net/chart-type/pie-chart'>exceljet.net</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9b08e220-e727-4a8f-b0f9-e50711798fa6/image-17-piechart-example.png'>Large preview</a>)" alt="An example of a pie chart" >}}

- **Stacked Bar**  
Especially useful when comparing categories. Just like the pie charts, the more complex they get (more series & categories), the harder they are to read. An advantage that stacked bar charts have over pie charts is the ability to see changes over time. Another thing to look out for is that when you have series that vary in their value, it gets harder to compare them visually. For example, take a look at the example below, it’s not obvious whether the orange series for “Eyebrow pencil” is larger or smaller than that of “Foundation”.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3125451a-b8a8-42c6-b937-9f8ca5f855f4/image-18-stacked-bar.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3125451a-b8a8-42c6-b937-9f8ca5f855f4/image-18-stacked-bar.png" width="800" height="600" sizes="100vw" caption="(Image source: <a href='https://www.anychart.com/ru/products/anychart/gallery/Bar_Charts/'>anychart.com</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3125451a-b8a8-42c6-b937-9f8ca5f855f4/image-18-stacked-bar.png'>Large preview</a>)" alt="An example of a stacked bar chart" >}}

- **Mekko**  
Perfect for visualizing the differences of certain categories within multiple dimensions. Just like the rest of the charts we’ve gone over so far, they’re easy to read but get increasingly harder to grasp once the categories and dimensions start to pile up. Additionally, you should avoid using Mekko charts if the differences among elements are too drastic.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8df8b988-de1d-4b29-9cc7-954c081ecd98/image-19-mekko-chart.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8df8b988-de1d-4b29-9cc7-954c081ecd98/image-19-mekko-chart.png" width="681" height="454" sizes="100vw" caption="(Image source: <a href='https://www.empowersuite.com/en/blog/marimekko-chart-powerpoint'>empowersuite.com</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8df8b988-de1d-4b29-9cc7-954c081ecd98/image-19-mekko-chart.png'>Large preview</a>)" alt="An example of a Mekko chart" >}}

- **Stacked Column**  
A great way to show comparisons between categories. You might have noticed that this chart type bears a strong resemblance to a stacked bar chart. Though there are differences in naming, you should know that horizontal bars usually go from highest to lowest value (or vice versa), while vertical ones imply another order rationale.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/38d4f80a-afab-4f75-b73f-4b60bda6fbfb/image-20-stacked-bar.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/38d4f80a-afab-4f75-b73f-4b60bda6fbfb/image-20-stacked-bar.png" width="800" height="504" sizes="100vw" caption="(Image source: <a href='https://www.amcharts.com/demos/100-stacked-column-chart/'>amcharts</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/38d4f80a-afab-4f75-b73f-4b60bda6fbfb/image-20-stacked-bar.png'>Large preview</a>)" alt="An example of a Stacked Bar chart" >}}

- **Area**  
A really common way of representing quantitative data. Often used to show the increase or decrease of various data series over time. The major con of this type of visualization is that it’s hard to connect a specific point of the graph to a value on both axes. And, as always, the more information you cram in, the less readable it becomes. Finally, if the graphs overlap, then one area will go over another and vice versa. Therefore, area charts are good for helping see the big picture without too much regard for being extremely precise.  
You might also notice a similarity between area and line charts. The former should be used when there’s an emphasis on a part-to-whole relationship.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/54deac20-0e74-4b63-9e99-e6e2d0a1220b/image-21-area-chart.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/54deac20-0e74-4b63-9e99-e6e2d0a1220b/image-21-area-chart.png" width="800" height="482" sizes="100vw" caption="(Image source: <a href='https://www.storytellingwithdata.com/blog/2020/4/9/what-is-an-area-graph'>storytellingwithdata.com</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/54deac20-0e74-4b63-9e99-e6e2d0a1220b/image-21-area-chart.png'>Large preview</a>)" alt="An example of an Area Chart" >}}

- **Waterfall**  
This kind of chart is often used in the financial industry to display the movement of value and its incremental path towards an endpoint. These charts, not being all too common, might not be the most intuitive to read, so they should better be reserved for professionals who deal with waterfall charts often.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1e860a8f-aadb-40c8-b97b-48b6ed1ee3fe/image-22-waterfall.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1e860a8f-aadb-40c8-b97b-48b6ed1ee3fe/image-22-waterfall.png" width="800" height="419" sizes="100vw" caption="(Image source: <a href='https://www.fusioncharts.com/dev/chart-guide/standard-charts/waterfall-chart'>Fusioncharts</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1e860a8f-aadb-40c8-b97b-48b6ed1ee3fe/image-22-waterfall.png'>Large preview</a>)" alt="An example of a Waterfall Chart" >}}

- **Line**  
A good choice when you’re looking to present a series of values. These values (also called markers) are typically connected by straight line segments. The line chart mimics the disadvantages of the area chart, except for the color overlapping problem.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bc2ce2da-354d-4b9e-a6cc-3ad9b20018d0/image-23-line-chart.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bc2ce2da-354d-4b9e-a6cc-3ad9b20018d0/image-23-line-chart.png" width="600" height="315" sizes="100vw" caption="(Image source: <a href='https://www.excel-easy.com/examples/line-chart.html'>Excel easy</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bc2ce2da-354d-4b9e-a6cc-3ad9b20018d0/image-23-line-chart.png'>Large preview</a>)" alt="An example of a Line Chart" >}}

**Showcase the composition:**

- Pie,
- Stacked Bar,
- Mekko,
- Stacked Column,
- Waterfall.

**Distribution of Data:**

- **Scatter Plot**  
A great way to emphasize the relationships between one or multiple numeric variables and/or their distribution across two axes. The major problem with using scatter plots for UX purposes, it’s that this type of chart is considerably harder to read than all of the other ones we’ve discussed so far. As such, scatter plots should be reserved for experienced users only.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4245128b-06f6-4b21-9725-7c3488983be3/image-24-scatter-plot.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4245128b-06f6-4b21-9725-7c3488983be3/image-24-scatter-plot.png" width="800" height="500" sizes="100vw" caption="(Image source: <a href='https://www.data-to-viz.com/graph/scatter.html'>data-to-viz.com</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4245128b-06f6-4b21-9725-7c3488983be3/image-24-scatter-plot.png'>Large preview</a>)" alt="An example of a Scatter Plot" >}}

- **Mekko**
- **Column**
- **Bubble**  
Commonly used to present financial data. Bubble charts are similar to scatter plots, however, they provide a more in-depth understanding of the data, since they have 3 axes. 

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c031f0a5-dabd-4f19-b419-83687814287d/image-25-bubble.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c031f0a5-dabd-4f19-b419-83687814287d/image-25-bubble.png" width="800" height="468" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c031f0a5-dabd-4f19-b419-83687814287d/image-25-bubble.png'>Large preview</a>)" alt="An example of a Bubble Chart" >}}

**Correlation and relationship between values:**

- Scatter Plot,
- Bubble,
- Line.

If we were to summarize the charts above in a matrix, it would look something like this.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/34049c21-7972-4c93-bca9-1eefc3065797/image-26-types-of-chart-usage.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/34049c21-7972-4c93-bca9-1eefc3065797/image-26-types-of-chart-usage.png" width="800" height="415" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/34049c21-7972-4c93-bca9-1eefc3065797/image-26-types-of-chart-usage.png'>Large preview</a>)" alt="An infographic with the types of charts. For the sake of comparison, you can use pie, mekko, area, waterfall, line, bar, and column charts. To compare, you can use pie, mekko, waterfall, bar, column charts. To show distribution pie, mekko, waterfall, scatter plot, bar, column, bubble. To show relationship, scatter plot, line, bubble. To show change, you can use area, waterfall, line, and column." >}}

It is only fitting that we summarized the types of charts and their usage as an infographic. 😄

Be advised though, that I’ve indicated what these charts are **generally** used for. Theoretically, if you wanted to, you could do a bubble chart, where each bubble is a pie chart. Voila, your bubble chart can now also show the composition of each bubble. Of course, it’s easier said than done, because usually, bubbles vary in their size drastically. Anyhow, you get the idea: the matrix is a general guideline, but you can get more creative with charts if you want to at your own discretion.

### Balancing Between The Complexity And Efficiency

So here’s a thing. As you might have noticed, lots of charts can be used for similar purposes. That doesn’t mean, however, that these charts are equally good for a certain task.

Generally, once you narrow down your choice to a few charts that seem to work best, you then want to make sure that they’re the least complex they could be. Below, I’ve outlined some of the charts we’ve mentioned by the degree of their complexity and efficiency.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/84eb4f9a-d22d-4512-bf06-4158e20c6299/image-27-complexity-vs-efficiency.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/84eb4f9a-d22d-4512-bf06-4158e20c6299/image-27-complexity-vs-efficiency.png" width="800" height="450" sizes="100vw" caption="This ‘chart for charts’ (very meta, I know) should be taken with a grain of salt. The efficiency axis implies that you're using the chart properly. The complexity axis is a representation of my experience. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/84eb4f9a-d22d-4512-bf06-4158e20c6299/image-27-complexity-vs-efficiency.png'>Large preview</a>)" alt="An infographic outlining the efficiency and complexity of the charts is mentioned in this article. The more efficient and less complex a chart is, the more effective it is." >}}

In a nutshell, you want to maximize efficiency and minimize complexity. This is the top-left quadrant. These charts are easy enough to be understood by middle school students. You should stick to those for the “consumer” persona, i.e. an average Joe. The more you move toward the right, the more reasons you should have to believe your users would be comfortable with reading them.

## What’s Next?

In case you’d like to continue learning about dashboards and the aspects of their design, here are some resources my team and I have found helpful (to an increasing degree of complexity):

### Articles

- [Data-heavy applications: How to design perfect charts](https://uxplanet.org/data-heavy-applications-how-to-design-perfect-charts-c0c893fef6de)
- [Top 16 Types of Chart in Data Visualization](https://towardsdatascience.com/top-16-types-of-chart-in-data-visualization-196a76b54b62)
- [Dashboard Design: best practices and examples](https://www.justinmind.com/blog/dashboard-design-best-practices-ux-ui/)
- [How to design and build a great dashboard](https://www.geckoboard.com/best-practice/dashboard-design/)
- [Dashboard UI Design: 14 Best Practices for Stakeholders](https://adamfard.com/blog/dashboard-ui)

### Books

- [Refactoring UI](https://www.refactoringui.com/book)
- [Beautiful Visualization: Looking at Data through the Eyes of Experts (Theory in Practice)](https://www.amazon.com/Beautiful-Visualization-Looking-through-Practice/dp/1449379869#customerReviews)
- [Functional Art, The: An introduction to information graphics and visualization (Voices That Matter)](https://www.amazon.com/Functional-Art-introduction-information-visualization/dp/0321834739)

### Scientific papers

- [Visualization Criticism - The Missing Link Between Information Visualization and Art](https://ieeexplore.ieee.org/document/4272046)
- [Principles of Effective Data Visualization](https://www.sciencedirect.com/science/article/pii/S2666389920301896)

{{< signature "ah, vf, il, yk" >}}
