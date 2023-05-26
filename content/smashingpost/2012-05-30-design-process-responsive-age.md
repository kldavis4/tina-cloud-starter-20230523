---
title: Design Process In The Responsive Age
slug: design-process-responsive-age
image: >-
  https://www.smashingmagazine.com/wordpress/2012/10/09/four-malware-infections-wordpress/attachment/events-14-101/attachment/groovy/attachment/change-process-feature-image500/
date: 2012-05-30T11:40:22.000Z
author: drew-clemens
description: >-
  You cannot plan for and design a _responsive_, _content-focused_,
  _mobile-first_ website the same way you’ve been creating websites for
  years—you just can’t. If your goal is to produce something that is not
  fixed-width and serves smaller devices just the styles they require, why would
  you use a dated process that contradicts those goals?
categories:
  - UX
  - Process
  - Wireframing
  - Responsive Design
---
You cannot plan for and design a responsive, content-focused, mobile-first website the same way you’ve been creating websites for years—you just can’t. If your goal is to produce something that is not fixed-width and serves smaller devices just the styles they require, why would you use a dated process that contradicts those goals?

I'd like to walk you through some problems caused by using old processes with responsive design. Let's look into an evolving design process we've been using with some <strong>promising new deliverables and tools</strong>. This should provide a starting point for you to freshen up your own process and bring it into the responsive age.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Responsive Web Design: What It Is And How To Use It](https://www.smashingmagazine.com/2011/01/guidelines-for-responsive-web-design/)
*   [Responsive Web Design Techniques, Tools and Design Strategies](https://www.smashingmagazine.com/2011/07/responsive-web-design-techniques-tools-and-design-strategies/)
*   [Sketching A New Mobile Web](https://www.smashingmagazine.com/2012/06/sketching-a-new-mobile-web/)

## The Problem

The issues caused when trying to force new results from an old process are significant yet, strangely enough, not immediately obvious. We’ve all <strong>just gotten used to them</strong>, like the annoying quirk we didn’t realize we had, until someone points it out. And from that point forward, it drives you crazy.

{{% feature-panel %}}

<img loading="lazy" decoding="async" loading="lazy" decoding="async" class="112248" title="Design Process In the Responsive Age" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4b65ed49-3664-47ea-8538-5d4286dd9645/change-process-feature-image500.jpeg" alt="Design Process In the Responsive Age" width="500" height="333" />

For example, when we create a desktop-sized, fixed-width site layout in Photoshop and hand it to a developer to interpret into HTML/CSS, we are asking the developer to make a lot of design decisions—possibly without even realizing it. Below is just a small sample:

*   How should the layout adjust for smaller-sized devices? (_It sure would be nice to have a hierarchy of important page elements based on their purpose, huh?)_
*   What is the hierarchy of the content? (_Gee, all that “Lorem Ipsum” doesn’t make it obvious?)_
*   How does the navigation respond to smaller screens? (_How do I handle ten links with five child pages each revealed on hover with a 320×480 touch device?!)_

This can cause major problems if the developer doesn’t feel confident in the visual arena. Even designers/developers who feel comfortable making those calls can get in hot water. In the end, the developer is often forced to make assumptions where plans were not made clear beforehand—sometimes days before feedback from designer or client becomes available. Sometimes it works, sometimes it doesn’t.</p>

### Work More or Work Efficiently?

It’s easy to resort to working more to resolve these new challenges. What comes naturally? Do a desktop and mobile-sized wireframe, then turn around and design a desktop and mobile-sized layout. This sort of solves the problem. You and your developer have more to work with, at least. However, what about all the device widths in-between—you’ll have to cover those as well, right?

At this point, you wake up and realize you're stuck in a familiar loop of ever-increasing deliverables and ever-shrinking profits. Using this old process to tackle new problems <strong>doesn’t really solve any of them</strong>, and it’s going to kill you from lack of sleep, make you poor from lack of profit, or both.

There are some good ideas floating around dealing with new processes. <a href="https://www.stuffandnonsense.co.uk/blog/about/time_to_stop_showing_clients_static_design_visuals/">Some smart folks</a> are of the very sensible opinion that the only answer is to design in the browser. However, other smart folks have admitted for the quiet rest of us that it's really, really hard to design freely in the browser—at least with current tools.

Of the emerging new process ideas, those that involve <a href="https://www.thismanslife.co.uk/projects/lab/responsivewireframes/">responsive HTML/CSS prototypes</a> look very promising. I'm planning to investigate these further. However, there are some definite challenges with this approach, not the least of which is the time it takes to create them when the <strong>site content is complex</strong>. Most of the examples I’ve seen are fairly generic, which doesn't translate well to real projects.

Currently, we are successfully using a different approach. It attempts to optimize content, design, and development time, finding a budget-friendly balance of appropriate direction from all disciplines—something that is effective, lean and uses quick, widely-accessible tools.</p>

## Solution: The Priority Guide

I used to call this my "mobile-sized content prototype wireframe thingy." For obvious reasons, however, I was encouraged to change the name by pretty much everyone I know. I liked the specificity of the name, but brevity won out. So, I settled on: <strong>Priority Guide</strong>.

Essentially, with the priority guide, we create a <strong>single deliverable</strong> that provides direction for content-focused design and mobile-first development in something resembling a wireframe.

<a title="Download PDF" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/210abab4-7555-4513-993d-0753b0c11b8f/dress-responsively-wireframe.pdf"><img loading="lazy" decoding="async" loading="lazy" decoding="async" class="112249" title="Dress Responsively Site Priority Guide" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0b562ecb-89af-4f6e-9756-c2d9fbf2ecda/rwd1.jpg" alt="Image of several screens from the Dress Responsively Site priority guide." width="500" height="444" /></a><br>
<a title="Download PDF" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/210abab4-7555-4513-993d-0753b0c11b8f/dress-responsively-wireframe.pdf">Download a PDF of the guide.</a>

By nature, a mobile-sized approach is narrow and forces more of a single column layout. The single column, in turn, causes a linear display of content and features. This linear display makes priority and hierarchy much more apparent than a desktop-sized wireframe, especially if you attempt to use a draft of real content instead of greek text—hence the <a href="https://www.smashingmagazine.com/2011/09/26/content-prototyping-in-responsive-web-design/">content prototype</a>.

At that point, armed with just this priority guide, the designer sets off to create something beautiful. The designer cranks up trusty ol' Photoshop and begins a new layout at a traditional desktop resolution—just like you may have done for the past ten years. For a good web designer (outfitted with his super-duper powers of visualization), it is a <strong>snap to make design decisions</strong> for a desktop resolution while looking at a mobile plan. That’s just how their minds work.

<a title="Download JPG" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b3a498b5-00be-47c5-bf1c-76be1b78d011/dress-responsively-home.jpg"><img loading="lazy" decoding="async" loading="lazy" decoding="async" class="112250" title="Dress Responsively Site Design" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5901c1ed-c388-409e-98fb-908e509f2711/change-process-site-design500.jpeg" alt="Homepage design for Dress Responsively site." width="500" height="444" /></a><br>
<a title="Download JPG" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b3a498b5-00be-47c5-bf1c-76be1b78d011/dress-responsively-home.jpg">Download a hi-res JPG of the final design.</a>

Once the design work is done, the handoff to the developer consists of the completed desktop-sized design and the original mobile-sized wireframe.</p>

### Don't Let the Simplicity Fool You

This approach may sound simple—which is part of the beauty of it—, but it also provides some <strong>real benefits</strong>:

*   The developer is provided a sort of bookended direction, both desktop and mobile. Two guides to follow, each offering unique information. Some interpretation still has to be made, which isn’t a bad thing, but there is far less guess work.
*   The designer is given a wireframe that provides hierarchy but does not dictate desktop-sized layout, where ample real estate allows for more creative room to breathe—designers need to be given their freedom, lest they shrivel up into sad, hollow, hipster-jean-wearing shells of themselves.
*   From the prototype and their linear approach, hierarchy can be understood fairly quickly, and the foundation for mobile-first markup and style is implied but flexible.
*   All of this is done in a two-deliverable process, like before, so it saves time and budget. Any method you get better results in the same amount of time (or less) is a good thing.</p>

### A Note About Context

Any conversation concerning mobile web draws questions of context. Is there a "mobile context"? If one does exist, do users actually have different expectations of a website's content while they are mobile? And, if users do have different expectations, how do we address them? Whew.

In short, those questions aren't what this article is about. These issues are <a href="https://mark-kirby.co.uk/2011/the-mobile-context/">being</a> <a href="https://www.lukew.com/ff/entry.asp?1333">discussed</a> <a href="https://www.useit.com/alertbox/mobile-vs-full-sites.html">in depth</a> <a href="https://www.netmagazine.com/opinions/nielsen-wrong-mobile">elsewhere</a>. I believe that questions of context can be answered very differently, depending on the project. I'll leave it to you and your team to apply due diligence in addressing context.

What I will suggest, however, is that you <strong>tread very carefully when making assumptions</strong> about your users and limiting content as a result. Though a mobile context may exist, you can't make those assumptions based on screen size alone. People surf the web on their phones from their couches, and they have all the time—and expectation—to access all of your site's content as they sit and watch TV. This is why we believe in a responsive web design approach that acts as a <a href="https://seesparkbox.com/foundry/safety_net">safety net</a> where little to no content is abridged from the experience of the user. This is the approach reflected in the above article—plan for all content in all contexts.

## Tools To Consider

### Style Tiles

Designer Samantha Warren just recently presented her concept of <a href="https://styletil.es/">Style Tiles</a> at SXSW. She was featured just days later <a href="https://www.alistapart.com/articles/style-tiles-and-how-they-work/">on A List Apart</a> discussing the same concept. We love it. It's one of those concepts that makes you slap your forehead, wondering why you didn't think of it sooner. It makes sense for web design in general, even more so in responsive design where client delieverables are much more tricky. We are already planning to integrate this into our workflow. We envision this deliverable being presented to a client during the wireframing process, so progress concerning style and layout can be made separately but concurrently.</p>

### Keynote for Wireframes

I’ve been loving Keynote for wireframes lately—it's even great for mobile-sized content prototype wireframe thingies. If you haven’t tried it, give it a shot. It’s quick, easy to learn, and easy to share. A really <span class="removed_link" title="https://edenspiekermann.com/en/blog/espi-at-work-the-power-of-keynote">interesting article</span> was written recently about designing in Keynote. I’m not sure I’m ready to go that far. However, it’s a fantastic wireframing and planning tool, and there are some great kits to get you started.</p>

## Conclusion

If you gain nothing more from this article, let me remind you what you already know: don’t be afraid to try new things. No process is a silver bullet—the same is true of tools and deliverables. If the ideas above don't fit your project, scrap them and try others. However, you must <strong>evolve your design process</strong> to account for the evolution of the web and users. If you hope to solve new problems, you're going to need a new approach.

You must also address the very human issue of <em>communication</em>. Earlier and more <strong>frequent collaboration</strong> among team members and the client must become the rule in your workflow, not the exception. Content, design, and development team members must review and collaborate regularly at every stage in the creation process until the site is live. We can’t 'throw it over the wall' anymore—at least, not if we want our sites to be excellent. There are simply too many moving parts now. Go forth and collaborate.

<em>(jc) (fi)</em>

