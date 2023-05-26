---
title: 'How Frontend Developers Can Help To Bridge The Gap Between Designers And Developers'
slug: frontend-developers-designers
author: stefan-kaltenegger
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3fed9e01-bf79-482d-9edc-d2a25a370bf6/designers-developers-guide.png
date: 2019-05-14T12:30:59+02:00
summary: >-
  Developers are known to usually be the last ones who leave their fingerprints before a website or any sort of web product gets shipped. Obviously, a lot of responsibility is involved and the quality of their work can either make a project excel or go down the drain. This article gives suggestions about what frontend developers can do on their end to better bridge the gap between designers and developers.
description: >-
  In this article, Stefan Kaltenegger shares his personal experience and advice on what frontend developers can do on their end to better bridge the gap between designers and developers.
categories:
  - Workflow
  - Communication
---
Within the last nine years, almost every designer I used to work with expressed their frustration to me about them frequently having to spend days giving feedback to developers to correct spacings, font sizes, visual as well as layout aspects that had simply not been implemented correctly. This often lead to weakening the trust between designers and developers, and caused unmotivated designers along with a bad atmosphere among the two disciplines.

A lot of times developers still seem to have the bad reputation of being overly technical and ignorant when it comes to being considerate about details the design team came up with. According to an article by [Andy Budd](https://www.smashingmagazine.com/2016/08/developers-own-code-should-designers-own-experience/), “[...] a lot of developers are in the same position about design &mdash; they just don’t realize it.” In reality though (as [Paul Boag](https://www.smashingmagazine.com/2014/11/why-you-should-include-your-developer-in-the-design-process/) points out), “developers [need to] make design decisions all the time.”

In this article, I’ll provide practical points of advice for frontend developers to avoid frustration and increase productivity when working with their creative counterpart.

## Looking Through The Eyes Of A Designer

Let’s for one moment imagine you were a designer and spent the last weeks &mdash; if not months &mdash; to work out a design for a website. You and your teammates went through multiple internal revisions as well as client presentations, and put a solid effort into fine-tuning visual details such as white space, font styles, and sizes. (In a responsive era &mdash; for multiple screen sizes, of course.) The designs have been approved by the client and were handed off to the developers. You feel relieved and happy.

A few weeks later, you receive an email from your developer that says:

<blockquote>“Staging site is set up. Here’s the link. Can you please QA?”</blockquote>

In a thrill of anticipation, you open that staging link and after scrolling through some of the pages, you notice that the site looks a little off. Spacings are not even close to what your design suggested and you notice some kinks in the layout: wrong font faces and colors as well as incorrect interactions and hover states. Your excitement starts to slowly fade and turn into a feeling of frustration. You can’t help but ask yourself, “How could that have happened?”

{{% feature-panel %}}

## The Search For Reasons

Maybe there were just a lot of unfortunate misunderstandings in the communication between the designers and developers. Nevertheless, you continue asking yourself:

- What did the the handover of designs look like? Were there just some PDFs, Photoshop or Sketch files shared via e-mail with some comments, or was there an actual handover meeting in which various aspects such as a possible design system, typography, responsive behavior, interactions and animations were discussed?
- Did interactive or motion prototypes that help to visualize certain interactions exist?
- Was a list of important aspects with defined levels of priority created?
- How many conversations took place &mdash; with *both* designers and developers in the same room together?

Since **communication** and **handover** are two very important key points, let’s take a closer look at each.

## Communication Is Key

Designers and developers, please talk to each other. Talk *a lot*. The earlier on in the project and the more often, the better. If possible, review design work in progress together early in the project (and regularly) in order to constantly evaluate feasibility and get cross-disciplinary input. Designers and developers naturally both focus on different aspects of the same part and therefore **see things from different angles and perspectives**.

Checking in early on lets developers become familiarized with the project so they can start researching and planning ahead on technical terms and bring in their ideas on how to possibly optimize features. Having frequent check-ins also **brings the team together on a personal and social level**, and you learn how to approach each other to communicate effectively.

## The Handover From Design To Development

Unless an organization follows a truly agile workflow, an initial handover of design comps and assets (from the design team to the developers) will likely happen at some point in a project. This handover &mdash; if done thoroughly &mdash; can be a solid foundation of knowledge and agreements between both sides. Therefore, it is essential not to rush through it and plan some extra time.

Ask a lot of questions and talk through every requirement, page, component, feature, interaction, animation, *anything* &mdash; and take notes. **If things are unclear, ask for clarification**. For example, when working with external or contract-based teams, both designers and developers can sign off the notes taken as a document of mutual agreement for future reference.

<p class="c-pre-sidenote--left">Flat and static design comps are good for showing graphical and layout aspects of a website but obviously lack the proper representation of interactions and animations. Asking for prototypes or working demos of complex animations will create a clearer vision of what needs to be built for everyone involved.</p><p class="c-sidenote c-sidenote--right">Nowadays, there’s is a wide range of prototyping tools available that designers can utilize to mockup flows and interactions in different levels of fidelity. Javier Cuello explains <a href="https://www.smashingmagazine.com/2016/09/choosing-the-right-prototyping-tool/">how to choose the right prototyping tool for your project</a> in one of his comprehensive articles.</p>

Every project is unique, and so are its requirements. Due to these requirements, not all conceptualized features can always be built. Often the available time and resources to build something can be a limiting factor. Furthermore, **constraints can come from technical requirements** such as feasibility, accessibility, performance, usability and cross-browser support, economic requirements like budget and license fees or personal constraints like the skill level and availability of developers.

So, what if these constraints cause conflicts between designers and developers?

{{% ad-panel-leaderboard %}}

## Finding Compromises And Building Shared Knowledge

In order to successfully ship a project on time and meet all defined requirements, finding compromises between the two disciplines is mostly inevitable. Developers need to learn to speak to designers in non-technical terms when they explain reasons why things need changes or can’t be built in a specific situation.

Instead of just saying, “Sorry, we can’t build this,” developers should try to give an explanation that is understandable for designers and &mdash; in the best case &mdash; **prepare suggestions for an alternative solution** that works within the known constraints. Backing your point with statistics, research, or articles, can help to emphasize your argument. Also, if timing is an issue, maybe the implementation of some time-consuming parts can be moved to a later phase of the project?

<p class="c-pre-sidenote--left">Even though it is not always possible, having designers and developers sit next to each other can shorten feedback loops and make it easier to work out a compromised solution. Adapting and prototyping can be done directly through coding and optimizing with DevTools open.</p><p class="c-sidenote c-sidenote--right">Show your fellow designers how to use DevTools in a browser so that they can alter basic information and preview small changes in their browser (e.g. paddings, margins, font sizes, class names) on the fly.</p>

If the project and team structure allow it, building and prototyping in the browser as soon as possible can give everyone involved a better understanding of the responsive behavior and can **help eliminate bugs and errors in the early stage** of the project.

The longer designers and developers work together, the better designers will understand what is easier and what is more difficult for the developers to build. Over time, they can eventually refer to solutions that have worked for both sides in the past:

<blockquote>“We’ve used that solution to find a compromise in Project A. Can we use it for this project as well?”</blockquote>

This also helps developers get a better sense of what details the designers are very specific about and what visual aspects are important to them.

## Designers Expect The Frontend To Look (And Function) Like Their Design

### The Design File Vs. Browser Comparison

A helpful technique to prevent designers from frustration is to make a simple left-right comparison between the design file you got handed over and what your current state of development looks like. This might sound trivial, but as a developer, you have to take care of so many things that need to function under the hood that you might have missed some visual details. If you see some noticeable discrepancies, simply correct them.

Think of it this way: Every detail in your implementation that looks exactly as it was designed **saves both you and the designer valuable time and headaches**, and encourages trust. Not everyone might have the same level of attention to detail, but in order to train your eye to notice visual differences, a quick round of [Can’t Unsee](https://cantunsee.space/) might be a good help.

{{< rimg breakout="true" href="https://cantunsee.space/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e76d0c68-9949-4785-b915-72bc8eb798f0/cant-unsee-screenshot.png" sizes="100vw" caption="(Image credits: <a href='https://cantunsee.space/'>Can’t Unsee</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e76d0c68-9949-4785-b915-72bc8eb798f0/cant-unsee-screenshot.png'>Large preview</a>)" alt="“Can’t Unsee” is a game where you need to choose the most correct design out of two choices." >}}

This nostalgically reminds me of a game we used to play a long time ago called “Find it”. You had to find discrepancies by comparing two seemingly similar images in order to score points.

{{< rimg href="https://appsliced.co/app?n=mordillo-find-them&l=dev" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4cfd932b-968f-48ad-88c6-5afa32ad507d/game-find-it.jpeg" sizes="100vw" caption="(Image credits: <a href='https://appsliced.co/app?n=mordillo-find-them&l=dev'>Mordillo find them</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4cfd932b-968f-48ad-88c6-5afa32ad507d/game-find-it.jpeg'>Large preview</a>)" alt="In “Find it”, players have to find errors comparing two images" >}}

Still, you may be thinking:

<blockquote>“What if there simply is no noticeable system of font sizes and spacings in the design?”</blockquote>

Well, good point! Experience has shown me that it can help to start a conversation with the designer(s) by **asking for clarification** rather than radically starting to change things on your own and creating unwanted surprises for the designer(s) later.

{{% ad-panel-leaderboard %}}

## Learn Basic Typographic And Design Rules

As Oliver Reichenstein states in one of his articles, [95% of the information on the web is written language](https://ia.net/topics/the-web-is-all-about-typography-period). Therefore, typography plays a vital role not only in web design but also in development. Understanding basic terms and concepts of typography can help you communicate more effectively with designers, and will also make you more versatile as a developer. I recommend reading Oliver’s article as he elaborates the importance of typography on the web and explains terms such as *micro-* and *macro-typography*.

<p class="c-pre-sidenote--left">In the “<a href="https://www.smashingmagazine.com/2018/06/reference-guide-typography-mobile-web-design/">Reference Guide For Typography In Mobile Web Design</a>”, Suzanne Scacca thoroughly covers typography terminology such as typeface, font, size, weight, kerning, leading and tracking as well as the role of typography in modern web design.</p><p class="c-sidenote c-sidenote--right">If you would like to further expand your typographical horizon, Matthew Butterick’s book “<a href="https://practicaltypography.com/">Butterick’s Practical Typography</a>” might be worth reading. It also provides <a href="https://practicaltypography.com/summary-of-key-rules.html">a summary of key rules</a> of typography.</p>

One thing I found particularly useful in responsive web design is that one should aim for an average line length (characters per line) of **45 to 90 characters** since shorter lines are more comfortable to read than longer lines.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ca1a031d-6140-46a9-8e89-f4980e2d10ff/different-line-lengths.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ca1a031d-6140-46a9-8e89-f4980e2d10ff/different-line-lengths.png" sizes="100vw" caption="Comparing different line lengths (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ca1a031d-6140-46a9-8e89-f4980e2d10ff/different-line-lengths.png'>Large preview</a>)" alt="Comparing two text paragraphs with different line lengths" >}}

### Should Developers Design?

There has been a lot of discussion whether designers should learn to code, and you may be asking yourself the same question the other way around. I believe that one can hardly excel in both disciplines, and that’s totally fine.

Rachel Andrew nicely outlines in her article “[Working Together: How Designers And Developers Can Communicate To Create Better Projects](https://www.smashingmagazine.com/2018/04/working-together-designers-developers/)” that in order to **collaborate more effectively**, we all need to learn something of the language, skills, and priorities of our teammates so that we can create a shared language and overlapping areas of expertise.

One way to become more knowledgable in the field of design is an online course known as “[Design for Developers](https://frontendmasters.com/courses/design-for-developers/)” that is offered by [Sarah Drasner](https://www.smashingmagazine.com/author/sarahdrasner/) in which she talks about basic layout principles and color theory &mdash; two fundamental areas in web design.

<blockquote> “The more you learn outside of your own discipline, is actually better for you [...] as a developer.” <br /><br />&mdash; Sarah Drasner</blockquote>

### The Visual Center

By collaborating with designers, I learned the difference between the mathematical and visual center. When we want to draw the reader’s attention to a certain element, our eye’s natural focal point lies just slightly above the mathematical center of the page.

We can apply this concept, for example, to position modals or any kinds of overlays. This technique helps us to **naturally get the user’s attention** and makes the design appear more balanced:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/256fb9c2-8a2d-4b11-8ae6-406162cd37ac/mathematical-and-visual-center.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/256fb9c2-8a2d-4b11-8ae6-406162cd37ac/mathematical-and-visual-center.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/256fb9c2-8a2d-4b11-8ae6-406162cd37ac/mathematical-and-visual-center.png'>Large preview</a>)" alt="Comparing two page layouts where one shows a text aligned to the mathematical and the other a text aligned to the visual center" >}}

## We’re All In This Together

In fast-paced and not-so-agile agency environments with tight deadlines, developers are often asked to implement fully functional responsive frontends based on a mobile and desktop mockup. This inevitably forces the developer to take design decisions throughout the process. Questions such as, “At what width will we decrease the font size of headlines?” or “When should we switch our three-column layout to a single column?” may arise. 

Also, in the heat of the moment, it may happen that details like error states, notifications, loading states, modals or styles of 404 pages simply fall through the cracks. In such situations, **it’s easy to start finger-pointing and blaming** the people who should have thought about this earlier on. Ideally, developers shouldn’t ever be put in such a situation, but what if that’s the case?

When I listened to Ueno’s founder and CEO, Haraldur Thorleifsson, speak at a conference in San Francisco in 2018, he presented two of their core values:

<blockquote>“Nothing here is someone else’s problem.”</blockquote>

<blockquote>“We pick up the trash we didn’t put down.”</blockquote>

What if more developers proactively start mocking-up the above-mentioned missing parts as good as they can in the first place, and then refine together with the designer sitting next to them? Websites live in the browser, so why not utilize it to build and refine?

While winging missing or forgotten parts might not always be ideal, I’ve learned in my past experiences that it has always helped us to move forward faster and eliminate errors on the fly &mdash; as a *team*.

Of course, this does not mean that designers should be overruled in the process. It means that **developers should try to respectfully meet designers halfway** by showing initiative in problem-solving. Besides that, I as a developer was valued way more by the team simply for caring and taking on responsibility.

## Building Trust Between Designers And Developers

Having a trustful and positive relationship between the creative and tech team can strongly increase productivity and outcome of work. So what can we, as developers, do to increase trust between the two disciplines? Here are a few suggestions:

<ol>
<li><strong>Show an eye for details</strong>.<br />Building things exactly as they were designed will show the designers that you care and put a big smile on their faces.</li>
<li><strong>Communicate with respect</strong>.<br />We’re all human beings in a professional environment striving for the best possible outcome. Showing respect for each other’s discipline should be the basis for all communication.</li>
<li><strong>Check in early on and regularly</strong>.<br />Involving developers from the start can help to eliminate errors early on. Through frequent communication, team members can develop a shared language and better understanding of each other’s positions.</li>
<li><strong>Make yourself available</strong>.<br />Having at least an optional 30-minute window a day when designers can discuss ideas with developers can give designers a feeling of being supported. This also gives developers the opportunity to explain complex technical things in words that not-so-technical people can understand better.</li>
</ol>

## The Result: A Win-Win Situation

Having to spend less time in QA through effective communication and a proper handover of designs gives both the creative and dev team more time to focus on building actual things and less headaches. It ultimately creates a better atmosphere and builds trust between designers and developers. The voice of frontend developers that show interest and knowledge in some design-related fields will be heard more in design meetings.

Proactively contributing to finding **a compromise between designers and developers** and problem-solving as a developer can give you a broader sense of ownership and involvement with the whole project. Even in today’s booming creative industry, it’s not easy to find developers who &mdash; besides their technical skillset &mdash; care about and have an eye for visual details. This can be *your* opportunity to help bridge the gap in your team.

### Related Resources

- “[How To Choose The Right Prototyping Tool](https://www.smashingmagazine.com/2016/09/choosing-the-right-prototyping-tool/),” Javier Cuello
- “[A Reference Guide For Typography In Mobile Web Design](https://www.smashingmagazine.com/2018/06/reference-guide-typography-mobile-web-design/),” Suzanne Scacca
- “[Butterick’s Practical Typograhy](https://practicaltypography.com/),” Matthew Butterick
- “[Working Together: How Designers And Developers Can Communicate To Create Better Projects](https://www.smashingmagazine.com/2018/04/working-together-designers-developers/),” Rachel Andrew
- “[Design For Developers](https://frontendmasters.com/courses/design-for-developers/),” Sarah Drasner, Frontend Masters
- “[Web Design is 95% Typography](https://ia.net/topics/the-web-is-all-about-typography-period),” Oliver Reichenstein
- “[Can’t Unsee](https://cantunsee.space/),” *A browser quiz to train your sense of recognizing visual details.*

{{< signature "dm, yk, il">}}
