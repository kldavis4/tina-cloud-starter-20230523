---
title: Smart Transitions In User Experience Design
slug: smart-transitions-in-user-experience-design
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/589d1978-01c5-4d90-a034-7f765d30a740/illu-transitions.jpg
date: 2013-10-23T08:51:12.000Z
author: adrian-zumbrunnen
summary: >-
  Some websites outperform others, whether in their content, usability, design, features, and so on. Details of interaction design and animation make a fundamental difference on modern websites. We’ll share some lessons drawn from various models and analyze why these simple patterns work so well.
description: >-
  Some websites outperform others, whether in their content, usability, design, features, and so on. We’ll share some lessons drawn from various models and analyze why these simple patterns work so well.
categories:
  - Usability
  - Interaction Design
  - Graphic Design
---

When we design digital products, we often use design applications such as Photoshop and Sketch. Most people who have been in the business for a few years obviously know that design is more than just about visual presentation. Still, many continue to create static designs. <a href="https://www.nytimes.com/2003/11/30/magazine/30IPOD.html?pagewanted=all">Steve Jobs said this</a> about design:
<blockquote>"It’s not just what it looks like and feels like. <strong>Design is how it works.</strong>"</blockquote>

Our experience and impression of a product are shaped by a combination of factors, with interaction playing a fundamental role. No longer can we think of user interfaces as static designs and add the magic of interaction later on. Instead, we need to embrace the interactive nature of the Web from the very beginning and think of it as natural constituent.</p>

Let’s look at some examples in which smart interaction, defined by subtle animation, gently improves the user experience.</p>

## Animated Scrolling

The blessing and the curse of the Web are hyperlinks. When you click on a link, it could take you anywhere, from a product page to the website of the creepy old puppet store down the street. The result is a <strong>loss of context</strong>.

One of the great things about the user experience of books is the linearity. Every chapter in a book builds on the last. You must read chapter one in a primer on economics to understand chapter two. When you skip a chapter, you are aware that you might miss something and, thus, lack some knowledge about the subsequent content. On the Web, and especially on long websites, this often happens subconsciously. By adding a scrolling animation, we can fix that:

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/297a82bb-5508-4993-9590-3f414d3a6b74/scrollinganimated.gif" alt="Scrolling animation" width="250" height="290" />

Compare that to this:

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a24a7b76-06ac-4d49-8d8b-ef4cb7320caf/scrollingnoanimation.gif" alt="Scrolling without animation" width="250" height="290" />

Compare the default behavior of “name” anchor links with the animated behavior. Skipping content is not an unconscious action anymore; it’s a decision. In fact, *Hope Lies at 24 Frames Per Second* has a menu button for its mobile view that sends you to the top of the page, without any animation. It took me more than a minute to figure out what actually happened.

<strong>Takeaway:</strong> Abrupt changes in an interface are hard for users to process. Don’t leave them in the dark; always show what’s happening.</p>

{{% feature-panel %}}

## Stateful Toggle

As we saw in the last example, transitions help users understand the pace and flow of an interface. Nothing feels more unnatural than a sudden change, because <strong>sudden changes just don’t exist in the real world</strong>. Let’s look at another example: toggle menus. Users associate the “plus” symbol with the action of adding content or expanding an element. By rotating it by 45°, the plus becomes a cross, an interface element widely understood to mean “close”:

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/38662f60-bde4-4e13-aacf-453dddf8e2c4/stateful-toggle.gif" alt="Toggle menu" width="250" height="290" />

This simple transition completely changes the meaning of the icon. Such a small detail means the difference between having to guess what will happen next and knowing what the icon means in either state. That toggle is pretty user-friendly, if you ask me. Also, note that the plus sign always rotates in the same direction as the content, reinforcing the flow of information.

<strong>Takeaway:</strong> Make your website element understandable in each state.</p>

## Collapsed Forms And Comments

The comment forms on many blogs and news websites are not the happiest-looking elements. Why? Well, most of them are not exactly friendly, right? When you are ready to post a comment, you just want to start typing the comment itself and nothing else. Instead, a typical form asks you all kinds of other stuff first. It’s annoying.

To motivate people to comment more, we can collapse the form and <strong>show only the most crucial element: the comment field</strong>. When the user clicks on the field, you can expand the form accordingly. A real-world example of this progressive disclosure can be found on the New York Times’ beta website:

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c522529b-2fb2-4131-bfa9-762f20d1ded8/ny-times.gif" alt="Progressive disclosure on the New York Times’ beta website" />

You could take this even further by setting the cursor’s focus to the comment field when the form expands. This approach has a problem, though: A key principle of interaction design is that <strong>an action should always happen close to where the interaction occurs</strong> (near the locus of attention). We could go one step further, then, and animate the comment field to orient the user:

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8948a57a-9ecb-444a-9b1e-1108e6fdf113/expandingcomments.gif" alt="Animated comment field" width="250" height="290" />

You could even pin the comment field to the top, expand it accordingly and display additional fields below it.

As you can see, this reduces clutter and makes the comment form more inviting. But what about collapsing all of the previous comments, too?

By collapsing the comments, we get the scroll bar to represent the length of the article itself, instead of the entire page. A common practice is to automatically load comments when the user reaches the bottom of a page. We should avoid forcing the user to click unless there is a really good reason to.

<strong>Takeaway:</strong> Progressively disclose in order to reduce UI components to their essence. Reveal features as the user needs them.</p>

{{% ad-panel-leaderboard %}}

## Pull To Refresh

One of the most exciting interactions to emerge shortly after the introduction of the iPhone was “pull to refresh,” pioneered by Loren Brichter. It allows the user to update scrollable reverse-chronological content. You can see this concept in action in Twitter’s app. Once you’ve scrolled to the top of the stream of tweets, scroll a little further to refresh the stream.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2239129f-b02b-4a23-b633-7757206c65e1/twitter.gif" alt="Pull to refresh on Twitter" />

Why does this work so well? Before pull to refresh existed, users had to hit the refresh button in their browser to load more content. By connecting the user’s desire of finding more content with the action of refreshing, the need for an explicit action became obsolete.

<strong>Takeaway:</strong> By connecting intent with action, the experience becomes more seamless.

## Sticky Labels

Sticky labels are another subtle yet useful combination of a user-interface component and a meaningful transition. Check out <a href="https://edenspiekermann.com/projects">Edenspiekermann’s use of this technique</a> in its portfolio.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/098a03b8-eb74-4d00-8b1f-b0173f6996e1/sticky-label.gif" alt="Edenspiekerman’s use of sticky labels" width="250" height="290" />

The project label scrolls along with the content, thus providing context for the images on the right, until the next project appears. This behavior is similar to that of the address book in iOS and is especially helpful for providing context in long sections. The transition offers both improved orientation and smooth context-based descriptions.

<strong>Takeaway:</strong> Use sticky labels for long sections in which descriptions or titles add valuable information to content that doesn’t fit in the viewport.</p>

## Affordance Transition

The concept of affordance derives from cognitive psychology and refers to particular characteristics of an object that guide the viewer.

In the context of user-interface design, the <a href="https://ec.europa.eu/regional_policy/archive/country/commu/docevent/26112008/5_doulgerof_glossary.pdf">usability glossary</a> (PDF) of the EU’s website defines it as follows:
<blockquote>"An affordance is a desirable property of a user interface — software which naturally leads people to take the correct steps to accomplish their goals."</blockquote>

Ridges are often used to enhance affordance. Ridges around a button suggest that the button can be manipulated. This UX technique was widely popularized by the camera app in iOS.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7f3e615e-6849-4a79-b1e7-2b261e2c5fbe/ios-lockscreen-final-opt.jpg"><img loading="lazy" decoding="async" class="119698" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/225d8df5-5a4e-4716-ac9d-b58a918f721c/ios-lockscreen-500-final.jpg" alt="iOS_Lockscreen-500-final" width="500" height="750" /></a>

iOS 6’s lock screen featured ripples around the camera icon, suggesting draggability. Apple removed it in iOS 7, apparently because users got accustomed to it, making the icon look more like a standalone button now. What happens is still the same, though: When you drag the button, the lock screen bounces up, revealing the camera underneath. This is a great technique to point users to features in an interface.

<strong>Takeaway:</strong> Give elements a high affordance to point users to features in an interface.</p>

## Context-Based Hiding

Google Chrome on iOS has had context-based hiding since it launched. This is what it looks like:

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7e9837a4-68f0-46b9-baab-a585daa84cd8/cbh.gif" alt="Context-based hiding" width="250" height="290" />

The basic idea is that the browser chrome and navigation controls hide automatically once the user scrolls down. As soon as the user scrolls up again, the controls reappear. This approach both enhances the contextual experience (focusing on the content itself) and increases screen space. The latter is, of course, particularly important on mobile devices.

The underlying assumption is that <strong>users will flow with the content that they’re consuming</strong>. As soon as they stop the flow, a change of context is likely required; thus, the navigation controls reappear. While this technique saves screen space, check whether the assumption holds up in your use case.

iOS takes this a step further. When you reach the bottom of a page, the controls expand again. It’s a good example of dynamically incorporating the needs of the user in an interface.

<strong>Takeaway:</strong> Use context-based hiding to enhance the user’s focus and save screen space.</p>

{{% ad-panel-leaderboard %}}

## Focus Transition

About a week ago, Nikita Vasilyev, a Toronto-based UI designer, came up with a pretty neat idea. He developed a script that animates focused elements. While still experimental, the concept is pretty interesting. Have a look at his video below. (And please put your earphones on — the music is epic.)

When navigating by keyboard, the user is often not clear on where the focus has moved to upon pressing the Tab key. Animation points them to the right spot on the page. The transition is subtle but has a big impact on orienting the user.

<strong>Takeaway:</strong> Orient the user, regardless of how they navigate.</p>

## Conclusion

These are only a few examples, among many others out there. The point is not to show the latest and fanciest interaction techniques, but rather to highlight how small interaction details can significantly improve the user experience.

If we are to design better digital products, then <strong>we need to challenge our current beliefs</strong> and see how interaction patterns can potentially ease the user’s life. I’m not saying we should reinvent the wheel, but it would be pretty naive to stop exploring. So, get out of your comfort zone. Keep exploring and testing.

If you like this article, you can follow me on Twitter, or join me for a bar of Swiss chocolate in Switzerland.

Which transition patterns have you found especially useful in your projects?

### Further Reading

*   [Meaningful Transitions: Motion Graphics in the User Interface](https://www.ui-transitions.com)
*   “[Mission Transition](https://www.smashingmagazine.com/2012/02/28/mission-transition/),” Mark Cossey, Smashing Magazine
*   “[12 Basic Principles of Animation](https://en.wikipedia.org/wiki/12_basic_principles_of_animation),” by Disney animators Ollie Johnston and Frank Thomas
*   [Improving User Flow Through Page Transitions](https://www.smashingmagazine.com/2016/07/improving-user-flow-through-page-transitions/)
*   [Why Transitions Are Important](https://www.smashingmagazine.com/2012/02/mission-transition/)
*   [Using Motion For User Experience On Apps And Websites](https://www.smashingmagazine.com/2015/01/using-motion-for-ux-on-apps-and-websites/)

{{< signature "al, il, ea" >}}
