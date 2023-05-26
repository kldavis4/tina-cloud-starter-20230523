---
title: A Brief Overview On Responsive Navigation Patterns
slug: overview-responsive-navigation-patterns
image: 'https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6de228da-c1d0-497e-beda-8e3c01dcbe2e/intel-500w-opt.png'
date: 2017-04-19T20:08:37.000Z
author: chris-poteet
summary: >-
  To say that responsive web design has changed our industry would be an understatement at best. We used to ask our clients which resolutions and devices they wanted us to support, but we now know the answer is “as many as possible.” To answer a challenge like this and to handle our increasingly complex world, our industry has exploded with new thinking, patterns and approaches.
description: >-
  To say that responsive web design has changed our industry would be an understatement at best. We used to ask our clients which resolutions and devices they wanted us to support, but we now know the answer is “as many as possible.” To answer a challenge like this and to handle our increasingly complex world, our industry has exploded with new thinking, patterns and approaches.
categories:
  - Mobile
  - Navigation
  - Responsive Design
---
In this article, I want to look specifically at the issue of responsive navigation. We will first talk about information architecture, then the purpose of navigation, and finally we will look at three responsive navigation patterns that have served well over time.</p>

## The Information Architecture Challenge

The first things that are affected in a mobile-first world, or at least should be, are content and information architecture strategies. If our applications are primarily about facilitating tasks and sharing of information, then we must focus there first.

The industry went through a trend of megamenus and increasingly complex navigation structures, but responsive web design has forced us to rethink this complexity. How much does our navigation need to hold in order to be effective? Does an application really need several different types of navigation, or can it work fine with just one? You will find that most responsive navigation patterns have forced us to simplify and concentrate, and that is a benefit of a [mobile-first approach](https://www.lukew.com/ff/entry.asp?933).</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8389b874-b960-4eba-ac59-7cecc226810b/intel-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7198c21b-454b-4d36-ab38-4fd8477649cf/intel-preview-opt.png" width="780" height="448" alt="An image of the responsive navigation used on Intel's website." /></a><figcaption>Intel’s navigation is complex, and that complexity is exacerbated on small viewports. Notice that the navigation has tabs, a listing of links and subcategories in a small space. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8389b874-b960-4eba-ac59-7cecc226810b/intel-large-opt.png">View large version</a>)
</figcaption></figure>

The truth is that if your information architecture isn’t optimized, then it doesn’t matter how slick your responsive navigation solution is. This was true long before we were debating the merits of media queries, but now the challenge is even greater. We must ensure that our navigation structures, when they are revealed on our websites, are clear and minimize any [cognitive friction](https://www.interaction-design.org/literature/article/my-head-hurts-cognitive-friction-in-the-age-of-mobile).

### <span class="rh">Further Reading</span> on SmashingMag:

*   [Responsive Navigation On Complex Websites](https://www.smashingmagazine.com/2013/09/responsive-navigation-on-complex-websites/)
*   [Navigation For Mega-Sites](https://www.smashingmagazine.com/2013/03/navigation-mega-sites/)
*   [<span class="headline">Implementing Off-Canvas Navigation For A Responsive Website</span>](https://www.smashingmagazine.com/2013/01/off-canvas-navigation-for-responsive-website/)
*   [Responsive Menus: Enhancing Navigation On Mobile Websites](https://www.smashingmagazine.com/2012/06/responsive-menus-enhancing-navigation-on-mobile-websites/)

{{% feature-panel %}}

Here are a couple of questions to ask as you create your navigation:

*   Is it painfully clear what each of your labels means, and is the value proposition (sometimes called “[information scent](https://www.nngroup.com/articles/information-scent/)”) clear to your visitors?
*   How can you reduce the complexity in your navigation as much as possible? If your navigation structure is seven levels deep, not many are going to be up for that challenge.
*   How can you ensure that the navigation doesn’t get lost throughout your resolution adaptations?
*   Have you tested it thoroughly to ensure that the navigation aligns with the user’s goals in visiting the website?

## The Purpose Of Navigation

Let’s take a quick moment to reflect on the purpose of navigation. This might seem elementary, but I’ve seen too many applications whose designers have forgotten these important principles. The best article I’ve read on this comes from one [written over a decade ago by Derek Powazek](https://alistapart.com/article/whereami) (which shows that the heart of the matter remains the same). He writes:

<blockquote>
<p>Navigation also has three parts, which are used to communicate to the user about their past, present, and future. Any good global navigation scheme should, at a glance, answer the top three questions every user has at the back of their mind on any page:</p>

<ul>
<li>Where am I? (Present)</li>
<li>Where can I go? (Future)</li>
<li>Where have I been? (Past)</li>
</ul>
</blockquote>

We must revisit these principles because I see that most responsive navigation solutions handle these very inconsistently. Most solutions handle the question “Where can I go?” pretty well, but most websites don’t even bother to show in their responsive solutions where the user is currently or where they’ve been. As you adapt some of the patterns we’ll look at, be sure to mold them to satisfy these important criteria.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/64715b54-6e46-4bd2-bb35-c91291e4fba1/ncsbn-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8a62410f-c977-41a3-a7ca-6706ac94fe40/ncsbn-preview-opt.png" width="780" height="587" alt="An image of the responsive navigation used on NCSBN website." /></a><figcaption>NCSBN’s website is one of the few that marks in its responsive navigation where you are in the website’s structure. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/64715b54-6e46-4bd2-bb35-c91291e4fba1/ncsbn-large-opt.png">View large version</a>)
</figcaption></figure>

Stephanie Lin has just posted an article entitled “[The Rules for Modern Navigation](https://www.uxbooth.com/articles/the-rules-for-modern-navigation/),” which makes a good complement to this article. She covers important interaction design components to consider in your navigation.</p>

## Preferable Patterns Of Responsive Navigation

Remember that we have a lot of options today for responsive navigation, but here is my take on the best patterns. Brad Frost has done us all a service and cataloged most, if not all, of these patterns on his website [This Is Responsive](https://bradfrost.github.io/this-is-responsive/patterns.html#navigation). He has also written two posts about these patterns: “[Navigation Patterns](https://bradfrost.com/blog/web/responsive-nav-patterns/)” and “[Complex Navigation Patterns for Responsive Design](https://bradfrost.com/blog/web/complex-navigation-patterns-for-responsive-design/).”

## 1\. The “Do Very Little” Pattern

This pattern is well illustrated on the [UX London 2017's website](https://2017.uxlondon.com/). Here is what it looks in small viewports.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0a1b2ee7-9dc1-4006-9078-6d62045f91a3/ux-london-2017-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0a1b2ee7-9dc1-4006-9078-6d62045f91a3/ux-london-2017-opt.png" width="660" height="218" alt="An image of the responsive navigation used on UX Longdon 2017." /></a><figcaption>UX London 2017 uses a pattern that maximizes its navigation’s visibility and utility.</figcaption></figure>

### Why It Works

I love this pattern because it fundamentally makes navigation a priority, and it doesn’t hide the navigation behind any [progressive disclosure](https://vanseodesign.com/web-design/progressive-discolosure/). Most responsive navigation patterns involve progressive disclosure, and while disclosure is a good option, it should only be pursued when a better option doesn’t exist. I agree with [Nielsen Norman Group on this issue](https://www.nngroup.com/articles/killing-global-navigation-one-trend-avoid/): If you can show navigation, show it. No one visiting this website has to wonder where the navigation is. A bonus is that this has no client-side dependencies, so you can keep your dependencies low and reduce failure points.

However, this is a hard sell for a lot of responsive applications. First of all, it doesn’t handle complex navigation well. If you need more than one level in your application shown at one time, then this pattern is not for you. Also, it could take up a lot of important vertical space in the application, so be sure that you can implement it like the UX London site and keep the allotted space in check.</p>

{{% ad-panel-leaderboard %}}

## 2\. The Multi-Level Toggle

Most applications can get away with two levels of navigation, and I have found this is the sweet spot for many of my implementations. In small viewports, this pattern enables users to toggle the subsections easily and see the contents within. One modern example of this is the [White House’s website](https://whitehouse.gov).</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fd1fd715-7011-43d0-ad88-f91f6aa032c9/whitehouse-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fd1fd715-7011-43d0-ad88-f91f6aa032c9/whitehouse-preview-opt.png" width="738" height="" alt="An image of the responsive navigation solution used for WhiteHouse.gov." /></a><figcaption>The White House’s website provides toggles to show subcontent.</figcaption></figure>

### Why It Works

It may not be the flashiest solution, but I have found it to be very stable. This pattern works well for the majority of navigation I need to support, and it effectively handles simple two-level navigation structures (which I’m hesitant to go beyond in most circumstances). Also, we must always build these solutions [progressively](https://alistapart.com/article/understandingprogressiveenhancement), so that they work even when the code supporting them fails.

I used to use [FlexNav](https://jasonweaver.name/lab/flexiblenavigation/) to achieve this effect, but the project has been abandoned by its owner. A promising alternative is [SmartMenus](https://www.smartmenus.org), but I have not used it yet. If you are interested in a pure CSS version of this, check out [CSS Script’s code example](https://www.cssscript.com/multi-level-toggle-responsive-navigation-menu-using-pure-css/).

## 3\. The Simple Toggle

This is another good option and is really a variant of the previous pattern. In this case, we have no need for multiple levels, but the navigation items are still too numerous to allow for the “do very little” pattern. An example of this is found on [Starbucks](https://www.starbucks.com/)’ website.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8d5c4192-ffb4-47f9-be68-6aa65a8dad1d/starbucks-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f8d73111-6580-4fab-968f-93bd4e497f6a/starbucks-preview-opt.png" width="780" height="376" alt="An image of the responsive navigation solution used for Starbucks." /></a><figcaption>Starbucks provides a simple toggle. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8d5c4192-ffb4-47f9-be68-6aa65a8dad1d/starbucks-large-opt.png">View large version</a>)
</figcaption></figure>

### Why It Works

With some clear iconography and colors, this option can really work well because it is very simple to implement and use. Variations of this pattern push content down or overlap it, and I feel both are acceptable. If you want a good script for this, check out [Responsive Nav](https://responsive-nav.com/).

Remember that you do not necessarily have to support multiple levels in your responsive solution. For example, the [World Wildlife Fund](https://www.worldwildlife.org/)’s navigation at higher viewport resolutions has a dropdown, but at the lowest viewport it simply toggles and the top-level links go to landing pages, where the remaining navigation items are shown. You could also provide alternate ways to navigate, including breadcrumbs, which can be a helpful addition at any viewport size.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f1fb9f23-478f-4d0c-88bd-8a7beb901cbb/wwf-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5814e02d-0873-47e0-b86b-cca7f76815ca/wwf-preview-opt.png" width="780" height="504" alt="An image of the responsive navigation solution used for World Wildlife Fund." /></a><figcaption>World Wildlife Fund presents top-level links and shows subitems on the landing pages. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f1fb9f23-478f-4d0c-88bd-8a7beb901cbb/wwf-large-opt.png">View large version</a>)
</figcaption></figure>

## Honorable Mentions

As mentioned, there are many approaches you could choose from today to handle your project’s needs. Even though I like the three above the best, here are two other possibilities.</p>

{{% ad-panel-leaderboard %}}

### Off-Canvas

This is probably the most popular, but some implementations are better than others. It can be done well, and if you want a script, I have used [MMenu](https://mmenu.frebsite.nl/) with great results.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0c05ffa6-4c01-499c-a4c4-56ade738c130/zurb-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ff173c5b-4961-43ab-bf4f-93ae1ffb83a3/zurb-preview-opt.png" width="780" height="256" alt="Zurb's Foundation has popularized the off-canvas pattern." /></a><figcaption>Responsive frameworks like Zurb’s Foundation have popularized the off-canvas pattern. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0c05ffa6-4c01-499c-a4c4-56ade738c130/zurb-large-opt.png">View large version</a>)
</figcaption></figure>

### Priority Plus

This has picked up steam in the last year or so, and it can also be good in some situations. I have used it on websites that have really long horizontal navigation, to avoid having to hide the menu items too early as the viewport shrinks. The only big problem with this solution is that it forces you to make assumptions about what is most important, so be careful. I have used the [PriorityNav.js](https://gijsroge.github.io/priority-nav.js/) script for this, and it has worked well.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9556450b-6112-43af-ae0a-22f7c8278a83/wonderfulmachine-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/93b25ef6-6b2f-4aad-bc7b-da67aa97b6bf/wonderfulmachine-preview-opt.png" width="780" height="137" alt="Wonderful Machine uses the Priority Plus pattern to good effect." /></a><figcaption>Wonderful Machine uses the Priority Plus pattern to good effect. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9556450b-6112-43af-ae0a-22f7c8278a83/wonderfulmachine-large-opt.png">View large version</a>)
</figcaption></figure>

## The Dreaded Hamburger Icon

There is simply no way I can talk about responsive navigation and not mention the debate around the hamburger icon (there are also other variants of [responsive "mystery meat" navigation indicators](https://twitter.com/lukew/status/591296890030915585)). The real issue here is: Does the icon convey enough meaning on its own, or does it need a textual indicator? The debate is essentially about the universality and recognizability of the hamburger icon. For me, very few icons have a universally clear meaning without some kind of text to support them, and the hamburger icon is just another example of why it’s best not to rely on the icon alone. Ask yourself, Is it worth confusing a visitor by not including it, or should I just include it to increase the likelihood that it will be understood? I lean towards including a textual indicator. Remember to always evaluate the context of your application to answer questions like these.

Here are some articles that talk about the issue if you want to learn more:

*   “[Obvious Always Wins](https://www.lukew.com/ff/entry.asp?1945),” Luke Wroblewski
*   “[Icons as Part of a Great User Experience](https://www.smashingmagazine.com/2016/10/icons-as-part-of-a-great-user-experience/),” Nick Babich, Smashing Magazine
*   “[Hamburger Menus and Hidden Navigation Hurt UX Metrics](https://www.nngroup.com/articles/hamburger-menus/),” Kara Pernice and Raluca Budiu, Nielsen Norman Group
*   “[Testing the Hamburger Icon for More Revenue](https://conversionxl.com/testing-hamburger-icon-revenue/),” Peep Laja, CXL

## Conclusion

The great news is that there are more options than ever for handling navigation in your responsive application. As long as you stick to clear information architecture design, testing and proven patterns, you will ensure that visitors will be able to use your website easily now and into the future. The next step is to start experimenting with these and other patterns to see what works best for your particular application. Behavior and needs change over time, so continually re-evaluate how you use these approaches. Another article on Smashing Magazine, “[Responsive Navigation on Complex Websites](https://www.smashingmagazine.com/2013/09/responsive-navigation-on-complex-websites/),” provides case studies and code for you to go further.

_My thanks to [Ben Callahan](https://twitter.com/bencallahan) and [Jacqui Olkin](https://twitter.com/OlkinComm) for their feedback on drafts of this article._

{{< signature "da, vf, yk, al, il" >}}

