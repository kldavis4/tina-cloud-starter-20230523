---
title: 'Accessibility Originates With UX: A BBC iPlayer Case Study'
slug: bbc-iplayer-accessibility-case-study
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a159cb94-0385-4cfb-86f5-a860a5e8fdab/111-iplayerhomepage-opt-small.png
date: 2015-02-23T23:17:27.000Z
author: henny-swan
summary: >-
  Design with choice in mind, and always give users control over the page. In this article, Henny Swan shares key principles that will ensure that your products are inclusive and usable for disabled people.
description: >-
  Design with choice in mind, and always give users control over the page. In this article, Henny Swan shares key principles that will ensure that your products are inclusive and usable for disabled people.
categories:
  - Coding
  - UX
  - Case Studies
  - Accessibility
---
<p>Not long after I started working at the BBC, I fielded a complaint from a screen reader user who was having trouble finding a favorite show via the <a href="https://www.bbc.co.uk/iplayer">BBC iPlayer’s home page</a>. The website had recently undergone an independent accessibility audit which indicated that, other than the odd minor issue here and there, it was reasonably accessible.</p>

<p>I called the customer to establish what exactly the problem was, and together we navigated the home page using a screen reader. It was at that point I realized that, while all of the traditional ingredients of an accessible page were in place &mdash; headings, <a href="https://www.w3.org/TR/wai-aria/roles#landmark_roles">WAI ARIA Landmarks</a>, text alternatives and so on &mdash; it wasn’t very usable for a screen reader user.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/654f18c0-9b19-4e4e-b734-fd4eae01b6b8/101-iplayerhomepage-opt.png"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4878b5be-b4d8-48a9-98c8-c9abae5934ec/101-iplayerhomepage-opt-small.png" alt="The old iPlayer homepage" /></a><figcaption>iPlayer’s old home page. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/654f18c0-9b19-4e4e-b734-fd4eae01b6b8/101-iplayerhomepage-opt.png">View large version</a>)</figcaption></figure>

The first issue was that the subnavigation was made up of only two links: “TV” and “Radio,” with links to other key areas such as “Categories,” “Channels” and “A to Z” buried further down the content order of the page, making them harder for the user to find.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b5f1809b-cfcd-4c3f-b37b-11a9f995a244/102-iplayerhomepage-opt.png"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5628be25-f027-4183-8783-d014b8ca82a9/102-iplayerhomepage-opt-small.png" alt="The old iPlayer homepage with Categories, Channels and A to Z highlighted" /></a><figcaption>iPlayer’s old home page showing “Categories,” “Channels” and “A to Z” far down the content order. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b5f1809b-cfcd-4c3f-b37b-11a9f995a244/102-iplayerhomepage-opt.png">View large version</a>)</figcaption></figure>

The second issue was how verbose the page was to the screen reader user. Instead of hearing a link to a program once, the program would be announced twice because the thumbnail image and the heading for the program were presented as two separate links.

{{% feature-panel %}}

This made the page longer to listen to and was confusing because links to the same destination were worded differently.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8de30452-ad44-484f-9e42-8c64341c63d8/103-iplayerhomepage-opt.png"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3d3a6dd8-ef3b-45ad-ae06-60f03f4aca89/103-iplayerhomepage-opt-small.png" alt="Duplicated links highlighted on the old iPlayer homepage" /></a><figcaption>iPlayer’s old home page showing duplicate links. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8de30452-ad44-484f-9e42-8c64341c63d8/103-iplayerhomepage-opt.png">View large version</a>)</figcaption></figure>

Finally, keyboard access on the page was illogical. In the “Categories” area, for example, a single click on a category would reveal four items in a panel next to it. To access the full list of items in that category, you had to click again on the same link to be taken to a listing page. This was a major hurdle for the user and the place where the customer I was talking to gave up using the application altogether.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a6bdfe2b-f031-4463-940b-fa687cc7ee2b/104-iplayerhomepage-opt.png"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f380cd88-c7c5-4799-8c51-02349e3308ea/104-iplayerhomepage-opt-small.png" alt="Categories, highlighted on the old iPlayer homepage" /></a><figcaption>iPlayer’s old home page showing the “Categories” links highlighted. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a6bdfe2b-f031-4463-940b-fa687cc7ee2b/104-iplayerhomepage-opt.png">View large version</a>)</figcaption></figure>

It was clear that, while the website had been built with accessibility in mind, it hadn’t been designed with accessibility in mind and this is where the issues originated.

## The Challenge

At the BBC, a number of internal standards and guidelines are in place that teams are required to follow when delivering accessible website and mobile applications. Key ones are:

*   [Accessibility Standards and Guidelines](https://www.bbc.co.uk/guidelines/futuremedia/accessibility/),
*   [Screen Reader Testing Guidelines](https://www.bbc.co.uk/guidelines/futuremedia/accessibility/screenreader.shtml),
*   [Mobile Accessibility Standards and Guidelines](https://www.bbc.co.uk/guidelines/futuremedia/accessibility/mobile_access.shtml).

There is also a strong culture of accessibility; the BBC is a <a href="https://www.bbc.co.uk/corporate2/insidethebbc/whoweare">publicly funded organization</a>, and accessibility is considered central to its remit and is a stronger driver than any legal requirement. So, how did this happen?

Part of the issue is that standards and guidelines tend to focus more on code than design, more on output than outcome, more on compliance than experience. As such, technically compliant pages could be built that are not the most usable for disabled users.

{{% ad-panel-leaderboard %}}

It may not seem immediately obvious, but visual design can have a massive impact on users who cannot see the page. I often find that mobile applications and websites that are problematic to make accessible are the ones where the visual design, by dictating structure, does not allow it.

This does not mean that standards and guidelines are redundant &mdash; far from it. But what we have found at the BBC is that standards need to sit within, and inform, an accessibility framework that runs through product management, user experience, development and quality assurance. As such, accessibility originates with UX. Most of the thinking and requirements should be considered up front so that poor accessibility isn’t designed in.

While redesigning the BBC iPlayer website, renewed focus was given to inclusive design, which, while adhering to the BBC’s standards and guidelines, is driven by four principles (more on that below). We then distilled our standards and guidelines to create a focused list of requirements for the UX to follow. We also started to train designers to annotate their own designs for accessibility.

## UX Principles

Our four main principles are the following:

*   Give users **choice**.
*   Put users in **control**.
*   Design with **familiarity** in mind.
*   Prioritize features that **add value**.

### Give Users Choice

Never assume that just because a user can access content one way that they want to access content in that one way. Because BBC’s iPlayer has “audio described” and “sign language” formats, it was never in any doubt that both of these should have their own dedicated listing pages, accessed via the “Categories” dropdown link. (Note that all on-demand content is subtitled, which is why there is no “Subtitled” category. Subtitles can be switched on in the media player.)

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fefc63d2-cfdc-47b6-9bfe-0fafd59f7514/105-iplayerhomepage-categories-opt.png"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/764f1efb-01af-4d88-821b-66686dd83e89/105-iplayerhomepage-categories-opt-small.png" alt="The Categories dowpdown with Audio Described and Signed sections" /></a><figcaption>The “Categories” dropdown with “Audio Described” and “Signed” sections. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fefc63d2-cfdc-47b6-9bfe-0fafd59f7514/105-iplayerhomepage-categories-opt.png">View large version</a>)</figcaption></figure>

User research and feedback indicated, however, that although people want dedicated categories, they also want to be able to search for and browse content in the same way that any other users would and to select their preferred format from there. I have stayed in touch over the years with the gentleman who complained about the old iPlayer page, and he’s said himself, “Don’t send us into disability silos!”

This means that from the outset the designs need to signpost “Audio Description” and “Signed” content via search results, A to Z, category and other listing pages. Not making any assumptions or not stereotyping users with disabilities is important &mdash; for instance, a person with a severe vision impairment might not always use audio descriptions; news, sports, music programs and live events often aren’t supported by audio description because commentators already provide enriched commentary.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c4b18e38-b637-44eb-aafa-89ab2506b933/106-iplayerlistings-opt.png"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1905dbce-b480-4e34-a82e-82efd75c938e/106-iplayerlistings-opt-small.png" alt="Alternative formats shown in listing pages" /></a><figcaption>List pages such as search, shown here, indicate what formats programs are available in. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c4b18e38-b637-44eb-aafa-89ab2506b933/106-iplayerlistings-opt.png">View large version</a>)</figcaption></figure>

On-demand pages also list alternative formats, allowing users to choose what they want. Looking ahead, the option to choose your format could also be included in the <a href="https://www.bbc.co.uk/blogs/internet/posts/Standard-Media-Player">Standard Media Player</a> &mdash; the BBC media player used for on-demand and live streaming video across all BBC products, including iPlayer.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b916e9ae-d878-4d1e-9bf3-2f2e16476953/107-iplayermediaplayer-opt.png"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/355e6f4f-2107-4da1-9514-33c7fa51aae3/107-iplayermediaplayer-opt-small.png" alt="Playback pages showing high definition and audio described formats" /></a><figcaption>Screenshot of the playback page showing HD and AD formats. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b916e9ae-d878-4d1e-9bf3-2f2e16476953/107-iplayermediaplayer-opt.png">View large version</a>)</figcaption></figure>

{{% ad-panel-leaderboard %}}

### Put Users in Control

Never taking control away from the user is essential. A key aspect of this in iPlayer, which is responsive, is not suppressing pinch zoom. Time and again in user testing, we have observed users zooming content, even on responsive websites, where text might be intentionally larger.

Due to an iOS bug that was rectified in iOS 6, the ability to pinch zoom was suppressed on many websites due to poor resizing when the orientation is changed from portrait to landscape. Now that this has been fixed, there is no reason to continue suppressing zoom.

Another aspect of control is autoplay. While iPlayer currently has autoplay for live content, this can be a problem because the sound of the video can make it difficult for a screen reader user to hear their reader’s output. However, we do know of screen reader users who request autoplay because it means they don’t have to navigate to the player, find the play button and activate play. The answer is to look at ways to give users control over playback by opting in or out of autoplay, such as by using a popup and saving preferences with cookies.

### Design With Familiarity in Mind

There needs to be a balance between the new and the familiar. Users understand how to interact with pages and apps that use familiar design patterns. This is especially important in native apps for iOS and Android, where standard UI components come with accessibility built in.

Equally important is the language used across the BBC’s native iPlayer apps and responsive website. Where the platform allows, consistent labels for headings, links and buttons &mdash; not just visually, but also via alternatives for screen reader users &mdash; ensure that the experience is familiar and recognizably “BBC iPlayer,” regardless of the platform.

Tied into this, the new designs reinforce a logical heading structure within the code, which in turn supports navigation for screen reader users. Key to this is ensuring that the pattern used for the heading structure is repeated across pages, so that users do not find main headings in different places depending on what page they are on. While structure is typically viewed as a responsibility of developers, it needs to be decided before designs are signed off in order to prevent poor structure getting coded in &mdash; more on that later.

### Prioritize Features That Add Value

Accessibility at the BBC is not just about meeting code, content and design requirements, but also about incorporating helpful features that add value for all users, including disabled users. A large proportion of feedback we get from our disabled users pertains to usability issues that could be experienced by anyone on some level but that seriously adversely affect disabled users. When we incorporate features to help users with specific disabilities, everyone gains access to a richer and easier experience.

One obstacle that comes up time and again is finding a favorite show. I’ve spoken with many screen reader users who say they save shortcuts to their favorite shows on their desktop but, due to changing URLs, often lose content. A simple way to address this that benefits all users is to ensure that there is a mechanism for saving favorites on the website. Adding in options to sort favorites and list them the way you want further improves this. It may sound unrelated to accessibility, but it was the single most requested feature received from disabled users. Simply accessing the favorites page to watch the latest episode of something, rather than having to search the website, makes all the difference.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/670855d0-272b-4eb8-b008-ab5d5affd289/108-iplayerfavourites-opt.png"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f7844f78-8df4-4985-9276-4a13044761e0/108-iplayerfavourites-opt-small.png" alt="Sorting favourites using A to Z and recent options" /></a><figcaption>The “Favourites” page, with options to sort by “A to Z” and “Recent”. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/670855d0-272b-4eb8-b008-ab5d5affd289/108-iplayerfavourites-opt.png">View large version</a>)</figcaption></figure>

Finding ways to allow people to get to the content they want more quickly has also influenced what is available within the media player itself. Once an episode has finished playing, exiting the media player and navigating back to the website to find the next episode is a massive overhead for some users. Adding a “More” button to the player itself &mdash; showing the next episode or programs similar to the current one &mdash; cuts down on the amount of effort it takes users to find new content.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5959ed1f-77ed-4c4f-bd51-56bece473500/109-iplayermediaplayerplugin-opt.png"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/64ae80db-f051-4820-b337-c77b5667f8b5/109-iplayermediaplayerplugin-opt-small.png" alt="The Standard Media Player plug in for related content" /></a><figcaption>The “You may also like” plugin shows related content and next episodes within the Standard Media Player. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5959ed1f-77ed-4c4f-bd51-56bece473500/109-iplayermediaplayerplugin-opt.png">View large version</a>)</figcaption></figure>

One key feature that has added value to BBC iPlayer’s native iOS and Android apps, as well as the website (when viewed in Chrome), is <a href="https://www.bbc.co.uk/blogs/internet/posts/Accessibility-on-BBC-iPlayer-on-Chromecast">support for Google Chromecast</a>. Being able to control what content you view on TV without having to use a remote or complex TV user interface is invaluable. Using one’s device of choice, whether it be iOS or Android, is much easier for a disabled user than using a remote control and a potentially inaccessible TV interface.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e6032b60-cd98-404e-bdd1-50ebf12a737b/110-iplayerchromecast-opt.jpg"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4f647716-62e2-4183-84e0-360ea3253f03/110-iplayerchromecast-opt-small.jpg" alt="Chromcast on BBC iPlayer" /></a><figcaption>BBC iPlayer and Chromecast. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e6032b60-cd98-404e-bdd1-50ebf12a737b/110-iplayerchromecast-opt.jpg">View large version</a>)</figcaption></figure>

## Guidelines

The principles above exist to create a mindset that helps product owners and UX practitioners alike when shaping and designing inclusive products. In addition to the four principles, a set of guidelines is used to design more accessible interfaces. The following are a subset taken from the “<a href="https://www.bbc.co.uk/guidelines/futuremedia/accessibility/mobile">BBC Mobile Accessibility Standards and Guidelines</a>”:

1.  **Color contrast**  
Ensure that text and backgrounds exceed the WCAG Double A 4.5:1 contrast minimum.
2.  **Color and meaning**  
Information conveyed with color must also be identifiable from context or markup.
3.  **Content order**  
Content order must be logical.
4.  **Structure**  
When supported by the platform, pages must provide a logical and hierarchical heading structure.
5.  **Containers and landmarks**  
When supported by the platform, page containers or landmarks should be used to describe page structure.
6.  **Duplicate links**  
Controls, objects and grouped interface elements must be represented as a single component.
7.  **Touch target size**  
Targets must be large enough to touch accurately (44 pixels).
8.  **Spacing**  
An inactive space must surround all active elements (unless they are large blocks exceeding 44 pixels).
9.  **Zoom**  
Where zoom is supported by the platform, it must not be suppressed.
10.  **Actionable elements**  
Links and other actionable elements must be clearly distinguishable.

## The New iPlayer

Keeping in mind this backdrop of principles and guidelines, along with the renewed focus on adding value and features that enhance the experience for disabled users, here are a few of the changes introduced in the BBC’s new iPlayer:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a98d4aaf-dab0-4ad3-ab74-966dca13f4be/111-iplayerhomepage-opt.png"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a159cb94-0385-4cfb-86f5-a860a5e8fdab/111-iplayerhomepage-opt-small.png" alt="The new BBC iPlayer homepage" /></a><figcaption>The BBC’s new iPlayer home page has better content order, search tools, structure and keyboard access. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a98d4aaf-dab0-4ad3-ab74-966dca13f4be/111-iplayerhomepage-opt.png">View large version</a>)</figcaption></figure>

At launch, the iPlayer’s navigation housed the BBC’s channels, a “TV Guide,” “Favourites” and “Categories.” These all sit at the start of the page, high up in the content order. While they are visually easy to see, they are also easily discoverable by screen reader users via a hidden heading and labeled navigation landmark:

<pre><code class="language-markup">&lt;div role="navigation"&gt;
&lt;h2&gt;iPlayer navigation&lt;/h2&gt;
</code></pre>

Where previously the “Categories” were unusable for the screen reader user I spoke with, they are now prominent in the page and fully keyboard navigable. Since launch, the addition of more channels has meant that the channel links have been rehoused in their own dropdown menu.

Search tools have also been added, enabling users to carry out predictive search, browse A to Z or view their most recently watched program. This is all keyboard accessible, it makes use of headings, and it has landmarks where appropriate.

The home page carousel is also fully keyboard accessible. Each program in the stream is presented as one link, with the reading order of text starting with the primary information first: channel attribution, program name, episode information, abstract and program duration.

Work has also been carried out to improve visible focus and bring both the iPlayer website and the Standard Media Player in line with the BBC header and footer. The pink underline used for the hover and focus states in the main BBC navigation is now used within the Standard Media Player to indicate when a button is selected &mdash; for example, when the subtitles are switched on. This replaces the use of color only to indicate a selected state, which was indistinguishable from the hover and focus states.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/46fc932c-bf4c-4533-b44d-8b7a7f5164bc/112-iplayernavigationfocusstate-opt.png"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d75c8f70-0e6f-4e66-9fbf-09448452c8f5/112-iplayernavigationfocusstate-opt-small.png" alt="BBC navigation hover and focus states" /></a><figcaption>The hover and focus pink underline used in the BBC header for iPlayer. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/46fc932c-bf4c-4533-b44d-8b7a7f5164bc/112-iplayernavigationfocusstate-opt.png">View large version</a>)</figcaption></figure>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/75f9a1db-9e40-4321-bf39-98290abfa507/113-iplayerhoverstates-opt.png"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8d6990a4-1412-446a-9983-3013f32a4a54/113-iplayerhoverstates-opt-small.png" alt="Hover and focus states used for the subtitle button on the Standard Media Player" /></a><figcaption>Active and inactive hover and focus states on the subtitle button in the Standard Media Player. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/75f9a1db-9e40-4321-bf39-98290abfa507/113-iplayerhoverstates-opt.png">View large version</a>)</figcaption></figure>

You can read more about what steps were taken to make <a href="https://www.bbc.co.uk/blogs/internet/posts/Making-the-new-iPlayer-accessible-for-all-users">iPlayer web-accessible</a> and to make the <a href="https://www.bbc.co.uk/blogs/internet/posts/Standard-Media-Player-accessibility">Standard Media Player accessible</a>, including creation of an <a href="https://www.bbc.co.uk/blogs/internet/posts/Creating-an-accessible-media-player-in-Flash">accessible media player in Flash</a>, on the BBC’s Internet Blog.

## Annotated UX

All of the thinking around inclusive design that comes from product owners, UX practitioners and designers needs to be captured and communicated to developers and engineers. At the BBC, we are moving to a model where designs need to be annotated for accessibility. This includes:

*   headings,
*   containers,
*   content order,
*   color contrast,
*   alternatives to color and meaning,
*   visible focus,
*   keyboard and input interactions.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/85043bf1-736f-461e-8cea-b1855bff774b/114-iplayercarousel-opt.png"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/099f0821-408e-488d-9b67-9fa52a887a54/114-iplayercarousel-opt-small.png" alt="Annotated UX for the iPlayer homepage showing headings, lists, labels and content order" /></a><figcaption>An example of an annotated UX showing headings and labels. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/85043bf1-736f-461e-8cea-b1855bff774b/114-iplayercarousel-opt.png">View large version</a>)</figcaption></figure>

The design above, showing an early version of the BBC One home page in iPlayer, outlines where the <code>&lt;h1&gt;</code> to <code>&lt;h6&gt;</code> headings should be. The UX practitioner doesn't need an in-depth knowledge of code, but rather an understanding of the hierarchy of data within a page. As such, an equally acceptable approach would be to indicate the “main heading,” “secondary heading,” “third-level heading” and so on. Developers can then take this and translate it into semantic markup.

Equally, indicating the logical order of content helps developers to code content in the right sequence (i.e. source order) &mdash; something that is essential to a screen reader or sighted keyboard user’s comprehension of the page.

Annotating the UX in this way is key to identifying designs that don’t allow for a logical page structure, content order or behavior. It is the first step to generating a style guide that documents focus states, colors and so on. Further down the line, these requirements can also be used to generate user acceptance criteria and automated quality assurance tests.

Even if you’re working in an agile way, where designs are iterative and not delivered in a complete form, annotation still works. As long as the basic framework of the page is well defined, the visual design can evolve from that.

## Summary

It’s very easy to get bogged down by accessible output and to forget that, ultimately, accessibility is about people. As such, keep the following in mind, whether you are working in product, UX, development or quality assurance:

*   Design with choice in mind.
*   Always give users control over the page.
*   Prioritize features that add value for disabled users.
*   Design with familiarity in mind.
*   Integrate accessibility into annotated UX and style guides.
*   Make no assumptions. Test ideas and concepts.

Fostering these key principles across the entire team will go a long way to ensuring that products are inclusive and usable for disabled people. Listening to users and actively including their feedback, along with adhering to organizational standards and guidelines, are essential.

### <span class="rh">Further Reading</span> on SmashingMag:

- [Color Contrast And Why You Should Rethink It](https://www.smashingmagazine.com/2014/10/color-contrast-tips-and-tools-for-accessibility/#further-reading-on-smashingmag)
- [Notes On Client-Rendered Accessibility](https://www.smashingmagazine.com/2015/05/client-rendered-accessibility/)
- [Accessibility APIs: A Key To Web Accessibility](https://www.smashingmagazine.com/2015/03/web-accessibility-with-accessibility-api/)
- [Making Accessibility Simpler, With Ally.js](https://www.smashingmagazine.com/2015/12/making-accessibility-simpler/)
- [The WAI Forward](https://www.smashingmagazine.com/2014/07/the-wai-forward/)

{{< signature "hp, il, al, ml" >}}