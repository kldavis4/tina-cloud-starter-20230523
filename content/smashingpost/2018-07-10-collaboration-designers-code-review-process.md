---
title: 'Better Collaboration By Bringing Designers Into The Code Review Process'
slug: collaboration-designers-code-review-process
author: ida-aalen
image: >-
  //archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a9420f06-1331-4680-bcd8-a3983999f667/06-mocup-with-microcopy-800w.png
date: 2018-07-10T13:50:26+02:00
summary: >
  Involving other people early on &mdash; especially people from other disciplines &mdash; can feel scary. By taking inspiration from code reviews, we can improve collaboration both within our own fields as well as across disciplines, be it design, UX, content or development. 
description: >
  Involving other people early on &mdash; especially people from other disciplines &mdash; can feel scary. By taking inspiration from code reviews, we can improve collaboration both within our own fields as well as across disciplines, be it design, UX, content or development. 
categories:
  - Process
  - Business
  - Workflow
  - Teams
---
<p>Smooth collaboration between developers and designers is something everyone aspires to, but it’s <a href="https://www.smashingmagazine.com/2018/04/working-together-designers-developers/">notoriously difficult</a>. But with today’s advanced web, it's difficult &mdash; if not impossible &mdash; to build a truly great product without collaborating across disciplines. Because of the range of technologies required to build a product, the product can only truly succeed when all disciplines &mdash; developers <em>and</em> designers, content creators, and user experience strategists &mdash; are deeply involved from the early stages of the project. When this happens, all ends of what it takes to build a product come naturally together into a unified whole, and a thus great product.</p>

<p>Because of this, no one is really promoting <a href="https://en.wikipedia.org/wiki/Waterfall_model">waterfall processes</a> anymore. Nevertheless, involving other people early on, especially people from other disciplines, can feel scary. In the worst case scenario, it leads to “<a href="https://en.wikipedia.org/wiki/Design_by_committee">design by committee</a>.”</p>

<p>Moreover, both designers and content strategists often have backgrounds in fields in which a sole creative genius is still the ideal. Having someone else proof your work can feel like a threat to your creativity.</p>

<p>So how can you involve people early on so that you’re avoiding the waterfall, but also making sure that you’re not setting yourself up for design by committee? I found my answer when learning about code reviews.</p>

{{% feature-panel %}}

## The <em>Aha!</em> Moment

<p>In July 2017, I founded <a href="https://confrere.com">Confrere</a> together with two developers, and we quickly hired our first engineer (I’m not a developer myself, I’m more of a UX or content designer). Our collaboration was running surprisingly smoothly,  so much so that at our <a href="https://www.atlassian.com/team-playbook/plays/retrospective">retrospectives</a>, the recurring theme was that we all felt that we were “doing it right.”</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/50e9277c-279f-47c5-9565-53800ee25c30/00-the-team.jpeg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/50e9277c-279f-47c5-9565-53800ee25c30/00-the-team.jpeg" sizes="100vw" caption="Dag-Inge (CTO), myself (CPO) and Ingvild (Sr. Engineer). (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/50e9277c-279f-47c5-9565-53800ee25c30/00-the-team.jpeg'>Large preview</a>)" alt="Three people are smiling and sitting next to each other around a computer. From left to right, they are Dag-Inge (CTO), Ida (CPO) and Ingvild (Sr. Engineer)." >}}

<p>I sat down with my colleagues to try to pinpoint what exactly it was that we were “doing right” so that we could try to preserve that feeling even as our company grew and our team expanded. We came to the realization that we all appreciated that the whole team was involved early on and that we were being honest and clear in our feedback to each other. Our CTO Dag-Inge added: “It works because we’re doing it as peers. You’re not being berated and just getting a list of faults”.</p>

<p>The word “peer” is what gave me the aha moment. I realized that those of us working within UX, design, and content have a lot to learn from developers when it comes to collaboration.</p>

<p>Peer reviewing in the form of code reviews is essential to how software gets built. To me, code reviews offer inspiration for improving collaboration within our own fields, but also a model for collaborating across fields and disciplines.</p>

<p>If you’re already familiar with code reviews, feel free to skip the next section.</p>

## What Is A Code Review?

<p>A code review can be done in various ways. Today, the most typical form of code review happens in the way of so-called <a href="https://www.atlassian.com/git/tutorials/making-a-pull-request">pull requests</a> (using a technology called <a href="https://www.atlassian.com/git/tutorials/what-is-git">git</a>). As illustrated below, the pull requests let other people on the team know that a developer has completed code that they wish to merge with the main code base. It also allows the team to review the code: they give feedback on the code before it gets merged, in case it needs improvement.</p>

<p>Pull requests have clearly defined roles: there is an author and a reviewer(s).</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/354b8724-8a3f-4f0f-83fe-ff3c093360fe/01-code-review-01.jpeg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/354b8724-8a3f-4f0f-83fe-ff3c093360fe/01-code-review-01.jpeg" sizes="100vw" caption="Ingvild (the author) requests a review from Dag-Inge (the reviewer). (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/354b8724-8a3f-4f0f-83fe-ff3c093360fe/01-code-review-01.jpeg'>Large preview</a>)" alt="Ingvild and Dag-Inge is setting next to each other and smiling. An arrow indicated that Ingvild has sent code to Dag-Inge." >}}

<p>As an example, let’s say our senior engineer Ingvild has made a change to Confrere’s sign-up flow. Before it is merged into the main code base and gets shipped, she (the author) creates a pull request to request a review from our CTO Dag-Inge (the reviewer). He won’t make any changes to her code, only add his comments.</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b30af716-c158-44a1-93d3-3eb1101dd13d/02-code-review-02.jpeg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b30af716-c158-44a1-93d3-3eb1101dd13d/02-code-review-02.jpeg" sizes="100vw" caption="Dag-Inge comments on Ingvild’s code. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b30af716-c158-44a1-93d3-3eb1101dd13d/02-code-review-02.jpeg'>Large preview</a>)" alt="Ingvild and Dag-Inge is setting next to each other. An arrow indicates that Dag-Inge has sent comments on code back to Ingvild." >}}

<p>It’s up to Ingvild how she wants to act on the feedback she received in the review. She’ll update her pull request with the changes she sees fit.</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4311ee16-a41d-4dd6-bf32-0555f7c6262e/03-code-review-03.jpeg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4311ee16-a41d-4dd6-bf32-0555f7c6262e/03-code-review-03.jpeg" sizes="100vw" caption="Ingvild updates her code with the changes she sees fit in light of Dag-Inge’s comments. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4311ee16-a41d-4dd6-bf32-0555f7c6262e/03-code-review-03.jpeg'>Large preview</a>)" alt="Ingvild and Dag-Inge are sitting next to each other. An arrow indicates that Ingvild is sending back her code to Dag-Inge, having looked through the code he commented on." >}}

<p>When the reviewer(s) approve the pull request, Ingvild can then merge her changes with the main code base.</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9dd649db-9e2b-4d64-8388-2c4b862c053f/04-code-review-04.jpeg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9dd649db-9e2b-4d64-8388-2c4b862c053f/04-code-review-04.jpeg" sizes="100vw" caption="After Dag-Inge gives the thumbs up, Ingvild can push the fix to production. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9dd649db-9e2b-4d64-8388-2c4b862c053f/04-code-review-04.jpeg'>Large preview</a>)" alt="Ingvild and Dag-Inge are sitting next to each other. A thumbs-up is displayed on the code review Dag-Inge has sent to Ingvild. And arrow indicates she pushes this code to the main repository." >}}

## Why Bother Doing Code Review?

<p>If you’ve never done code review, the process above might sound bureaucratic. If you have doubts, here’s a <a href="https://www.atlassian.com/agile/software-development/code-reviews">ton</a> <a href="https://blog.fullstory.com/what-we-learned-from-google-code-reviews-arent-just-for-catching-bugs/">of</a> <a href="https://medium.com/@palantir/code-review-best-practices-19e02780015f">blog</a> <a href="https://mtlynch.io/human-code-reviews-1/">posts</a> and <a href="https://kev.inburke.com/docs/shull_defects.pdf">academic research</a> about the advantages of code review.</p>

<blockquote>Code reviews set the tone for the entire company that everything we do should be open to scrutiny from others, and that such scrutiny should be a welcome part of your workflow rather than viewed as threatening.<br /><br />&mdash; <a href="https://blog.fullstory.com/what-we-learned-from-google-code-reviews-arent-just-for-catching-bugs/">Bruce Johnson, co-founder of Full Story</a></blockquote>

<p>Code review reduces risk. Having someone proof your work, and also <em>knowing</em> someone will proof your work, helps weed out errors and heightens quality. In addition, it ensures consistency and helps every team member familiarize with more of the code base.</p>

<p>When done right, code review also builds a culture for collaboration and openness. Trying to understand and critique other people’s work is an excellent way to learn, and so is getting honest feedback on your work.</p>

<p>Always having at least two people look over the code also curtails ideas of “my” code and “your” code. It’s <em>our</em> code.</p>

<p>Considering these advantages, a review shouldn’t just be for code.</p>

{{% ad-panel-leaderboard %}}

## Review Principles For All Disciplines, Not Just Code

<p>With reviews, there is always one author and one or more reviewers. That means you can involve people early on without falling into design by committee.</p>

<p>First, I have to mention two important factors which will affect your team’s ability to do beneficial reviews. You don’t necessarily have to have mastered them, but as a minimum, you should aspire to the following:</p>

<ul>
<li>You and your colleagues <a href="https://www.smashingmagazine.com/2018/04/working-together-designers-developers/#respect">respect each other</a> and each other’s disciplines.</li>
<li>You’re sufficiently self-assured in your own role so that you feel like you can both give and receive criticism (this is also connected to the team’s <a href="https://www.nytimes.com/2016/02/28/magazine/what-google-learned-from-its-quest-to-build-the-perfect-team.html">psychological safety</a>).</li>
</ul>

<p>Even if we’re not reviewing code, there’s a lot to learn from existing <a href="https://medium.com/@palantir/code-review-best-practices-19e02780015f">best practices</a> for code reviews.</p>

<p>Within our team, we try to adhere to the following principles when doing reviews:</p>

1. Critique the work, not the author.
2. Be critical, but remain affable and curious.
3. Differentiate between a) Suggestions b) Requirements, c) Points that need discussion or clarification.
4. Move discussions from text to face-to-face. ([Video counts](https://www.smashingmagazine.com/2018/04/working-together-designers-developers/#creating-working-relationships))
5. Don’t forget to praise the good parts! What’s clever, creative, solid, original, funny, nice, and so on?

<p>These <a href="https://confrere.com/about/how-we-work/collaboration">principles</a> weren’t actually written down until <em>after</em> we discussed why our collaboration was working so well. We all felt we were allowed to and expected to ask questions and suggest improvements already, and that our motivations were always about building something great together, and not about criticising another person.</p>

<p>Because we were being clear about what kind of feedback we were giving, and also remembered to praise each other’s good work, doing reviews was a positive force rather than a demotivating one.</p>

## An Example

<p>To give you an idea of how our team uses review across disciplines and throughout a process, let’s look at how the different members of our team switched between the roles of author and reviewer when we created our sign-up flow.</p>

### Step 1: Requirements gathering

<p><strong>Author:</strong> Ida (UX)</p>

<p><strong>Reviewers:</strong> Svein (strategy), Dag-Inge (engineering), Ingvild (engineering).</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c4b47537-2a48-4d59-8b2f-64e0485a3c58/05-requirements-gathering.jpeg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c4b47537-2a48-4d59-8b2f-64e0485a3c58/05-requirements-gathering.jpeg" sizes="100vw" caption="The team gathered around the whiteboard. Svein (CEO) to the left, Ingvild (Sr. Eng), to the right. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c4b47537-2a48-4d59-8b2f-64e0485a3c58/05-requirements-gathering.jpeg'>Large preview</a>)" alt="A whiteboard is showing rough sketches of a sign-up form. A man (Svein) and a woman (Ingvild) are smiling and discussing." >}}

<p>Whiteboard sessions can be exhausting if there’s no structure to them. To maintain productivity and creativity, we use the author/reviewer structure, even for something as seemingly basic as brainstorming on a whiteboard. In this case, in which we were coming up with the requirements for our sign-up flow, I got to be the author, and the rest of the team gave their feedback and acted as reviewers. Because they also knew they’d be able to review what I came up with in step 2 (plenty more opportunity for adjustments, suggestions, and improvements), we worked swiftly and were able to agree upon the requirements in under 2 hours.</p>

### Step 2: Mockup with microcopy

<p><strong>Author:</strong> Ida (UX)</p>

<p><strong>Reviewers:</strong> Ingvild (engineering), Eivind (design), Svein (strategy).</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9ed5ed76-7ce6-4d5b-a2fb-6cc9309bb3c2/06-mocup-with-microcopy.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9ed5ed76-7ce6-4d5b-a2fb-6cc9309bb3c2/06-mocup-with-microcopy.png" sizes="100vw" caption="By mocking up in Google docs, it’s easy for people from all disciplines to provide feedback early on. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9ed5ed76-7ce6-4d5b-a2fb-6cc9309bb3c2/06-mocup-with-microcopy.png'>Large preview</a>)" alt="A screenshot of a Google Doc mocking up a sign-up form with comments from team members Ingvild and Ida." >}}

<p>As an author, I created a mockup of the sign-up flow with microcopy. Did the sign-up flow make sense, from both the user and engineering perspective? And how could we improve the flow from a design and frontend perspective? At this stage, it was essential to work in a format in which  it would be easy for all disciplines to give feedback (we opted for Google Docs, but it could also have been done with a tool like InvisionApp).</p>

### Step 3: Implementing the sign-up flow

<p><strong>Author:</strong> Ingvild (engineering)</p>

<p><strong>Reviewer:</strong> Ida (UX) and Dag-Inge (engineering).</p>

<p>We had agreed upon the flow, the input fields, and the microcopy, and so it was up to Ingvild to implement it. Thanks to <a href="https://surge.sh/">Surge</a>, we can automatically create preview URLs of the changes so that people who can’t read code are able to give feedback at this stage as well.</p>

### Step 4: User testing

<p><strong>Author:</strong> Ida (UX)</p>

<p><strong>Reviewer:</strong> The users.</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cdaaea55-cc0a-4930-80f7-af953d4b7316/07-user-testing.jpeg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cdaaea55-cc0a-4930-80f7-af953d4b7316/07-user-testing.jpeg" sizes="100vw" caption="Ida doing user testing on a small budget. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cdaaea55-cc0a-4930-80f7-af953d4b7316/07-user-testing.jpeg'>Large preview</a>)" alt="Two women (Ida and a user) sitting next to eachother in front of a laptop." >}}

<p>Yes, we consider user testing a form of review. We brought our newly built sign-up flow face-to-face with actual users. This step gave us a ton of insight, and the most significant changes in our sign-up flow came as a result.</p>

### Step 5: Design

<p><strong>Author:</strong> Eivind (design)</p>

<p><strong>Reviewers:</strong> Ingvild (engineering) and Ida (UX).</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f66371e6-9301-4f66-8d3f-4543e51c8db3/08-design.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f66371e6-9301-4f66-8d3f-4543e51c8db3/08-design.png" sizes="100vw" caption="The first version of the sign-up flow was based on existing design components. In this stage, Eivind developed some new components to help improve the design. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f66371e6-9301-4f66-8d3f-4543e51c8db3/08-design.png'>Large preview</a>)" alt="A screenshot from Slack. Eivind, the designer, has posted a screenshot, and Ida replies with enthusiasm." >}}

<p>When design suddenly shows up here in step 5, it might look a lot like a waterfall process. However, our designer Eivind had already been involved as a reviewer since step 2. He gave a bunch of useful feedback at that stage and was also able to start thinking about how we could improve the design of the sign-up flow beyond the existing modules in our design system. At this step, Eivind could also help solve some of the issues that we identified in the user testing.</p>

### Step 6: Implementation

<p><strong>Author:</strong> Ingvild (engineering)</p>

<p><strong>Reviewer:</strong> Eivind (design), Ida (UX) and Dag-Inge (engineering).</p>

<p>And then we’re back to implementing.</p>

#### Why review works

<p>In summary, there’s always just one author, thus avoiding design by committee. By involving a range of disciplines as reviewers early on, we avoid having a waterfall process.</p>

<p>People can flag their concerns early and also start thinking about how they can contribute later on. The clearly defined roles keep the process on track.</p>

## Regular Review Walkthroughs

<p>Taking inspiration from code walkthroughs, we also do regular review walkthroughs with different foci, guided by the following principles:</p>

<ul>
<li>The walkthrough is done <strong>together.</strong></li>
<li><strong>One person</strong> is in charge of reviewing and documenting.</li>
<li>The idea is to <strong>identify issues</strong>, not necessarily to solve them.</li>
<li>Choose a <strong>format</strong> that gives as much context as possible, so that it’s easy to act upon the findings later (e.g. InvisionApp for visual reviews, Google Docs for text, and so on).</li>
</ul>

<p>We’ve done review walkthroughs for things such as accessibility audits, reviewing feature requests, auditing the implementation of the design, and doing heuristic usability evaluations.</p>

<p>When we do our quarterly accessibility reviews, our accessibility consultant Joakim first goes through the interface and documents and prioritizes the issues he’s found in a shared Google Sheet. Joakim then walks us through the most important issues he’s identified.</p>

<p>Meeting face-to-face (or at least on video) to go through the issues helps create an environment for learning rather than a feeling of being supervised or micromanaged.</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ef4aac65-f779-4c7d-98dd-aeba501cba07/09-accessibility-review.jpeg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ef4aac65-f779-4c7d-98dd-aeba501cba07/09-accessibility-review.jpeg" sizes="100vw" caption="Accessibility review: Joakim (right) walks Ingvild and Dag-Inge through the accessibility issues he found in his audit. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ef4aac65-f779-4c7d-98dd-aeba501cba07/09-accessibility-review.jpeg'>Large preview</a>)" alt="Three people in a sofa gathered around a laptop. They’re discussing and smiling." >}}

<p>If you find yourself always being tied up with something that’s due for release, or fixing whatever is at the top of your inbox, reviews can help remedy that. If you set aside regular half days for reviewing work you’ve already done, you can identify issues before they become urgent. It can also help you refocus and make sure you’re priorities are keeping along the right lines. Your team should maybe not begin building that new feature before you’re confident that the existing features are living up to your standards.</p>

## User Testing Is A Form Of Review

<p>An important motivation for code reviews is to reduce risk. By doing it every single time you introduce a change or add something new to your product, and not just when you suspect something is maybe not up to par, you diminish the chance of shipping bugs or subpar features. I believe we should look at <a href="https://confrere.com/about/how-we-work/user-testing">user testing</a> from the same perspective.</p>

<p>You see, if you want to reduce the risk of shipping with major usability issues, user testing has to be part of your process. Just having your UX designers review the interface isn’t enough. <a href="https://www.measuringu.com/blog/effective-he.php">Several studies</a> have found that even usability experts fail in identifying every actual usability problems. On average, 1 in 3 issues identified by experts were false alarms &mdash; they weren’t issues for users in practice. But worse, 1 in 2 issues that users did in fact have, were overlooked by the experts.</p>

<p>Skipping user testing is just as big a risk as skipping code review.</p>

## Does Review Mean Death To Creativity?

<p>People working within design, user experience, and content often have educational backgrounds from art schools or maybe literature, in which the sole creator or creative artistic genius is hailed as the ideal. If you go back in history, this used to be the case for developers as well. Over time, this has changed by necessity as web development has grown more complex.</p>

<p>If you cling to the idea of creativity coming from somewhere deep within yourself, the idea of review might feel threatening or scary. Someone meddling in your half-finished work? Ouch. But if you think about creativity as something that can spring from many sources, including dialogue, collaboration, or any form of inspiration (whether from the outside or from someplace within you), then a review is only an asset and an opportunity.</p>

<p>As long as we’re building something for the web, there’s no way around collaborating with other people, be it within our own field or others. And a good idea will survive review.</p>

<p>Let’s create something great together.</p>

{{< signature "rb, ra, yk, il" >}}