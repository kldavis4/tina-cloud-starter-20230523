---
title: 'Design Systems Are About Relationships'
slug: design-systems-relationships
author: ryan-debeasi
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b3b2088f-3f11-4f53-a436-8eeb2e30766b/design-systems-relationships.png
date: 2019-10-07T12:30:59+02:00
summary: >-
  Design systems can improve usability, but they can also limit creativity or fall out of sync with actual products. In this article, we’ll explore how designers and developers can create more robust design systems by building a culture of collaboration.
description: >-
  Design systems can improve usability, but they can also limit creativity or fall out of sync with actual products. In this article, we’ll explore how designers and developers can create more robust design systems by building a culture of collaboration.
categories:
  - Design Systems
  - Workflow
  - Design
---
Design systems can be incredibly helpful. They provide reusable elements and guidelines for building a consistent “look and feel” across products. As a result, users can take what they learned from one product and [apply it to another](https://uxdesign.cc/design-principle-consistency-6b0cf7e7339f). Similarly, teams can roll out well-tested patterns for navigation or reviews, making products [more trustworthy](https://www.nngroup.com/articles/trustworthy-design/). Effective design systems [solve boring problems](https://bigmedium.com/ideas/boring-design-systems.html) in a repeatable way so that developers and designers can focus on solving novel problems. 

Yet when someone uses the term “design system” in a meeting, I’m never quite sure what reaction to expect. I’ve seen curiosity and excitement about trying a new way of working, but I’ve also seen frustration and concern at the idea of a system limiting designers’ creativity.  Some designers argue that design systems [sap creativity](https://blog.prototypr.io/design-system-weaknesses-81a562232d98), or that they are [solutions in search of a problem](https://www.webdesignerdepot.com/2019/04/why-dont-we-just-use-material-design/). Design systems can [fragment over time](https://24ways.org/2017/why-design-systems-fail/), causing teams to stop using them.

Design systems aren’t going away, though. Just 15% of organizations lacked a design system in 2018, [according to one survey](https://uxtools.co/survey-2018/#design-system). That’s down from 28% the previous year. Some teams use large, general-purpose design systems such as Google’s Material Design, while others use smaller, more bespoke systems such as REI’s [Cedar](https://rei.github.io/rei-cedar-docs/) and Mozilla’s [Protocol](https://protocol.mozilla.org/).

Design systems should empower teams, not limit them. For that to happen, we need to start thinking more holistically. **A design system isn’t just code, or designs, or documentation.** It’s all of these things, plus relationships between the people who make the system and the people who use it. It includes not just CSS files and Sketch documents, but also trust, communication, and shared ownership. As it turns out, there’s a whole field of study dedicated to exploring systems like these.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/18574855-b47e-428b-9c29-3a26ba5c84be/design-systems-relationships-cedar.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/18574855-b47e-428b-9c29-3a26ba5c84be/design-systems-relationships-cedar.png" sizes="100vw" caption="In REI’s Cedar Design System, icons are tailored to the company’s outdoor gear business. The snowflake icon indicates ski and snowboard services, and the ruler icon indicates a size chart. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/18574855-b47e-428b-9c29-3a26ba5c84be/design-systems-relationships-cedar.png'>Large preview</a>)" alt="Grid of icons including stars, a shopping cart, and a snowflake" >}}

{{% feature-panel %}}

## The Big Picture

A 1960 paper titled “Socio-technical systems” [explored](https://academic.oup.com/iwc/article/23/1/4/693091#12178445) the interactions among technology, humans, and the larger environment in which they exist. [Enid Mumford explained](https://onlinelibrary.wiley.com/doi/abs/10.1111/j.1365-2575.2006.00221.x) that researchers began by investigating how to build better relationships between managers and employees, but by the 1980s, they were focused on making work more efficient and cost-effective. In 2011, Gordon Baxter and Ian Sommerville [wrote](https://academic.oup.com/iwc/article/23/1/4/693091#12178445) that this research helped inspire user-centered design, and that there’s a lot of work left to do.

Baxter and Sommerville argued that today, there is still a tension between “humanistic” research, which focuses on employees’ quality of life, and “managerial” research, which focuses on their productivity. They also [explained](https://academic.oup.com/iwc/article/23/1/4/693091#https://academic.oup.com/iwc/article/23/1/4/693091#12178469) that it’s important to consider both technology and human interactions: “system performance relies on the joint optimization of the technical and social subsystems.”

I’d argue that design systems are socio-technical systems. They involve interactions between the people who create the system, the people who create products using the system, and the end users who interact with these products. They also evoke the same tension between efficiency and humanism that Baxter and Sommerville saw.

Design systems aren’t composed just of images and code; they involve conversations among designers, developers, product managers, CEOs, and random people on GitHub. These interactions occur in various contexts &mdash; a company, an open-source community, a home &mdash; and they happen across cultures and organizational boundaries. Building a team can mean bringing together people from disciplines such as [animation](https://www.carbondesignsystem.com/guidelines/motion/), [sound design](https://www.smashingmagazine.com/2012/09/guidelines-for-designing-with-audio/), [data visualization](https://ux.mailchimp.com/patterns/stats), [haptics](https://material.io/design/platform-guidance/android-haptics.html), and [copywriting](https://design-system.futurelearn.com/core-styles/microcopy). Creating a successful design system requires equal parts of technical expertise and soft skills.

And yet, peruse design or engineering news aggregators and you’re likely to see a distinct focus on that “technical subsystem” &mdash; code and tools, rather than people and conversations. Which creative tool is the best at keeping track of design tokens? What JavaScript technologies should be used for building reusable components &mdash; React, web components, or something else? Which build tool is best?

The answer to these questions is, of course, “it depends!” Who will design, build, and use the system? What are their needs? What constraints are they operating under? What tools and technologies are they comfortable with? What do they want to learn?

To answer these sorts of questions, Baxter and Sommerville recommend two types of activities:

- **Sensitisation and awareness activities**  
Learning about the varied people who will create and participate in the system, and sharing that information far and wide.
- **Constructive engagement**  
Communicating across roles, building prototypes, and considering both the technical and social parts of the system.

{{% ad-panel-leaderboard %}}

## Digging In

In early 2019, I was part of a team &mdash; let’s call them “team blue” &mdash; that was building a design system for a large organization. I facilitated informal chats with this team and “team green”, which was using the design system to build a web application. Every couple of weeks, we got all the developers and designers together around a table and talked about what we were building and what problems we were trying to solve. These chats were our “sensitization and awareness activities.”

We didn’t have permission to make our design system public, so we did the next best thing: we treated it like a small open-source project within the organization. We put the code in a repository that both teams could access and asked for contributions. Team blue was responsible for reviewing and approving these contributions, but anyone on either team could contribute. Team blue was also building an application of their own, so in a sense, they were both users and custodians of the design system.

These interactions helped the teams build better products, but just as importantly, they established _trust_ between the teams. Team blue learned that folks were using the system thoughtfully and building clever new ideas on top of it. Team green learned that the system really was tailored to their needs, so they could work with it instead of against it. Baxter and Sommerville might call this work “constructive engagement.”

We found that both teams were under pressure to learn new technologies and deliver a complete product quickly. In other words, they were already operating under a pretty considerable [cognitive load](https://alistapart.com/article/psychology-of-design/). As a result, the two teams agreed to focus on making the system easy to use. That meant sidestepping the whole [web components debate](https://dev.to/richharris/why-i-don-t-use-web-components-2cia), focusing mostly on CSS, and ensuring that our documentation was clear and friendly.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9a743383-e6d9-4147-bcbb-3266530435b8/design-systems-relationships-fluent.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9a743383-e6d9-4147-bcbb-3266530435b8/design-systems-relationships-fluent.png" sizes="100vw" caption="Microsoft’s Fluent Design System targets four very different platforms. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9a743383-e6d9-4147-bcbb-3266530435b8/design-systems-relationships-fluent.png'>Large preview</a>)" alt="Screenshot of links to Windows, Web, iOS, and Android documentation" >}}

## Putting It All Together

Organizations of all sizes create reusable design elements to help teams build more consistent, elegant applications. Different organizations’ needs and dynamics are expressed in their design systems. Here are just a few examples:

- Google’s Material Design has several implementations in different frameworks and languages. It’s used by a variety of people inside and outside of Google, so it has comprehensive documentation and a variety of toolkits for design apps.
- Microsoft’s [Fluent Design System](https://www.microsoft.com/design/fluent/#/) targets four very different platforms. Like Material, it includes toolkits for UX designers and comprehensive documentation.
- Mozilla’s [Protocol](https://protocol.mozilla.org/) is implemented in Sass and vanilla JavaScript.  It has a strong focus on internationalization. Alex Gibson [says that this system helps Mozilla](https://alxgbsn.co.uk/2019/04/15/my-sixth-year-working-at-mozilla/) “create on-brand web pages at a faster pace with less repetitive manual work.”
- REI’s [Cedar](https://rei.github.io/rei-cedar-docs/) is built with Vue.js components and can’t be used with other JavaScript frameworks. Cedar is used primarily by REI’s internal developers and is closely tied to the company’s brand. The design system’s code is open source, but [its fonts are not](https://rei.github.io/rei-cedar-docs/about/cedar-design-system/).
- Salesforce’s Lightning Design System is a [JavaScript-agnostic CSS framework](https://lightningdesignsystem.com/faq/). It can optionally be used alongside the Lightning Component Framework, which [includes two JavaScript implementations](https://developer.salesforce.com/blogs/2018/12/introducing-lightning-web-components.html): one using web components and another using Salesforce’s proprietary Aura framework.
- Red Hat’s PatternFly was created to provide a consistent user experience [across the company’s cloud platform products](https://opensource.com/business/15/6/go-beyond-bootstrap-patternfly), so it has a relatively high information density and includes a variety of data visualization components. The PatternFly team recently [switched from Angular to React](https://blog.patternfly.org/patternfly/js-framework-for-patternfly-4/) after some [experimentation with web components](https://developers.redhat.com/blog/2016/08/09/are-web-components-in-the-future-for-patternfly-2/). PatternFly also includes a JavaScript-agnostic implementation using HTML and CSS. (Full disclosure: I’m a former Red Hatter.)
- IBM's[ Carbon Design System](https://www.carbondesignsystem.com/getting-started/developers/vanilla) offers implementations in React, Vue, Angular, and vanilla JavaScript as well as a [design toolkit](https://github.com/carbon-design-system/carbon-design-kit) for Sketch. The Carbon team is [experimenting with web components](https://github.com/carbon-design-system/carbon-custom-elements). (Hat tip to Jonathan Speek for [tracking down](https://dev.to/jonathanspeek/comment/c60m) that repository.)

Systems like these are consistent and reliable because people from different teams and roles worked together to build them. These systems solve real problems. They’re not the result of developers trying to impose their will upon designers or vice-versa.

Josh Mateo and Brendon Manwaring [explain that](https://spotify.design/articles/2018-12-04/the-paradox-of-design-systems/) Spotify’s designers “see their role as core contributors and co-authors of **a shared** system &mdash; one that they have ownership of.” Mina Markham [describes herself](https://styleguides.io/podcast/mina-markham/) as “the translator between engineering and design” on the Pantsuit design system. Jina Anne [digs into](https://www.designbetter.co/design-systems-handbook/designing-design-system) the team dynamics and user research behind design systems: “Spoiler alert! You’re going to need more than just designers.”

{{% ad-panel-leaderboard %}}

## Let’s Build Some Stuff!

Now that we’ve gone through research and some examples, let’s talk about how to build a new design system. Start by talking to people. Figure out who will be using and contributing to your design system. These people will probably span a variety of disciplines &mdash; design, development, product management, business, and the like. Learn about people’s needs and goals, and ask them to share what they’re working on. Consider planning an informal meeting with snacks, coffee, or tea to create a welcoming atmosphere. Establish regular communication with these folks. That might mean joining a shared chat room or scheduling regular meetings. Keep the tone casual and friendly, and focus on listening.

As you talk about what you’re working on, look for common problems and goals. You might find that teams need to display large amounts of data, so they’re investigating tools for displaying tables and generating reports. Prioritize solutions for these problems.

Look also for repeated patterns and variations on similar themes. You might find that buttons and login forms look a bit different across teams. What’s the significance of these variations? What variations are intentional &mdash; for example, a primary button versus a secondary button &mdash; and what variations have happened by accident? Your design system can name and catalog the intentional patterns and variations, and it can eliminate the “accidental” variations.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/374b6a5b-7096-4758-aac1-b242fc0a1dc1/design-systems-relationships-carbon.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/374b6a5b-7096-4758-aac1-b242fc0a1dc1/design-systems-relationships-carbon.png" sizes="100vw" caption="IBM’s Carbon Design System lists all the variations of its components. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/374b6a5b-7096-4758-aac1-b242fc0a1dc1/design-systems-relationships-carbon.png'>Large preview</a>)" alt="Screenshot of five different button styles" >}}

The goal here is to establish a rapid feedback loop with people who are using the design system. Faster feedback and smaller iterations can help avoid going too far in the wrong direction and having to dramatically change course. P.J. Onori [calls these sudden, large changes “thrash.”](https://blog.prototypr.io/the-most-important-lessons-ive-learned-about-creating-design-systems-have-little-to-do-with-design-4ceee2717298) He says that some thrash is good &mdash; it’s a sign that you’re learning and responding to change &mdash; but that too much can be disruptive. “You shouldn’t fear thrash,” he says, “but you need to know when it’s useful and how to help mitigate its downsides. One of the best [ways] to mitigate the downsides of thrash is to start small — with _everything_.”

Consider starting small by setting up a few basic elements:

- A version control system to store your code. GitHub, GitLab, and Bitbucket are all great options here. Make sure that everyone who uses the system can access the code and propose changes. If possible, consider making the code open source to reach the widest possible audience.
- CSS code to implement the system. Use [Sass variables](https://sass-lang.com/documentation/variables) or [CSS custom properties](https://developer.mozilla.org/en-US/docs/Web/CSS/Using_CSS_custom_properties) to store “design tokens” &mdash; common values such as widths and colors. 
- A package.json file that defines how applications can build and install the design system.
- HTML documentation that demonstrates how to use the design system, ideally using the system’s own CSS.

The [node-sass documentation](https://bulma.io/documentation/customize/with-node-sass/) for the CSS framework Bulma describes these steps in a bit more detail. You can skip installing and importing Bulma if you’d like to start from scratch, or you can include it if you’d like to start off with some of the basics in place.

You might have noticed that I didn’t mention anything about JavaScript here. You might want to add this element eventually, but you don’t need it to get started. It’s easy to go down a rabbit hole researching the best and newest JavaScript tools, and getting lost in this research can make it harder to get started. For example, “[5 Reasons Web Components Are Perfect For Design Systems](https://ionicframework.com/blog/5-reasons-web-components-are-perfect-for-design-systems/)” and “[Why I Don’t Use Web Components](https://dev.to/richharris/why-i-don-t-use-web-components-2cia)” both make valid points, but only you can decide what tools are right for your system. Starting with just CSS and HTML lets you gather real-world feedback that will help you make this decision when the time comes.

As you release new versions of the system, update your system’s version number to indicate what has changed. Use [semantic versioning](https://semver.org/) to indicate what’s changed with a number like “1.4.0.” Increment the last number for bug fixes, the middle number for new features, and the first number for big, disruptive changes. Keep communicating with the folks who use the design system, invite feedback and contributions, and make small improvements as you go. This collaborative, iterative way of working can help minimize “thrash” and establish a sense of shared ownership.

Finally, consider [publishing your design system as a package on npm](https://www.freecodecamp.org/news/how-to-make-a-beautiful-tiny-npm-package-and-publish-it-2881d4307f78/) so that developers can use it by running the command `npm install your-design-system`. By default, npm packages are public, but you can also [publish a private package](https://docs.npmjs.com/creating-and-publishing-private-packages), publish the package to a [private registry](https://levelup.gitconnected.com/deploying-private-npm-packages-to-nexus-a16722cc8166), or ask developers to install the package [directly from a version control system](https://remarkablemark.org/blog/2016/09/19/npm-install-from-github/). Using a package repository will make it easier to discover and install updates, but installing directly from version control can be an easy short-term solution to help teams get started.

If you’re interested in learning more about the engineering side of things, Katie Sylor-Miller’s [Building Your Design System](https://www.designbetter.co/design-systems-handbook/building-design-system) provides a fantastic deep dive. (Full disclosure: I’ve worked with Katie.)

## Wrapping Up

Design systems are made up of code, designs, and documentation as well as relationships, communication, and mutual trust. In other words, they’re socio-technical systems. To build a design system, don’t start by writing code and choosing tools; start by talking to the people who will use the system. Learn about their needs and constraints, and help them solve problems. When making technical, design, or strategy decisions, consider these people’s needs over the theoretically “best” way to do things. Start small, iterate, and communicate as you go. Keep your system as simple as possible to minimize thrash, and invite feedback and contributions to establish a sense of shared ownership. 

By giving equal weight to engineering and interpersonal considerations, we can get the benefits of design systems while avoiding the pitfalls. We can work in a way that’s efficient _and_ humane; we don’t have to choose one over the other. We can empower teams rather than limiting them. Empowered teams ultimately help us better serve our users &mdash; which, after all, is why we’re here in the first place.

### <span class="rh">Further Reading</span> on SmashingMag:

<ul>
<li><a title="Read 'Tips For Managing Design Systems'" href="https://www.smashingmagazine.com/2019/05/tips-managing-design-systems/" rel="bookmark">Tips For Managing Design Systems</a></li>
<li><a title="Read 'Including Animation In Your Design System'" href="https://www.smashingmagazine.com/2019/02/animation-design-system/" rel="bookmark">Including Animation In Your Design System</a></li>
<li><a title="Read 'Beyond Tools: How Building A Design System Can Improve How You Work'" href="https://www.smashingmagazine.com/2018/03/building-design-systems-to-improve-work/" rel="bookmark">Beyond Tools: How Building A Design System Can Improve How You Work</a></li>
<li><a title="Read 'Building A Large-Scale Design System For The U.S. Government (Case Study)'" href="https://www.smashingmagazine.com/2017/10/large-scale-design-system-us-government/" rel="bookmark">Building A Large-Scale Design System For The U.S. Government (Case Study)</a></li>
</ul>

{{< signature "ah, il" >}}
