---
title: 'Weaving Web Accessibility With Usability'
slug: weaving-web-accessibility-usability
author: uri-paz
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ec1e0356-61ee-4ea9-9461-acc5e626d5e8/web-accessibility-usability.png
date: 2020-11-30T13:00:00.000Z
summary: >-
  In this article, Uri Paz explains how a site complying with accessibility guidelines may still present usability issues when testing with real users. Find out how weaving accessibility best practices with usability testing, can help as many people as possible to fully use your site.
description: >-
  In this article, Uri Paz explains how a site complying with accessibility guidelines may still present usability issues when testing with real users. Find out how weaving accessibility best practices with usability testing, can help as many people as possible to fully use your site.
categories:
  - Usability
  - Accessibility
  - UX
---

By formally adopting web accessibility standards, you can provide access to people with visual impairments without involving them in the product development lifecycle, but does that mean the end product is usable? In this article, I’ll briefly discuss visual impairments, as well as the connection between web accessibility standards and usability principles. I’ll also share my key takeaways from a usability test I conducted with visually impaired and blind participants.

## What Is Visual Impairment?

The term _visual impairment_ refers to people who can see but have a decrease in visual acuity or visual field. Visual impairment affects the ability to perform daily activities, such as reading, walking, driving, and social activities &mdash; all of which become difficult (and sometimes even impossible). There is a range of visual impairments which vary from mild to severe vision loss in one or both eyes.

Here are a few examples:

- **Central Scotoma**  
Loss of vision in the central visual field.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1d111987-9d08-48ad-916f-9ade9ae4fa19/central-scotoma.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1d111987-9d08-48ad-916f-9ade9ae4fa19/central-scotoma.png" sizes="100vw" caption="<a href='https://chrome.google.com/webstore/detail/funkify-%E2%80%93-disability-simu/ojcijjdchelkddboickefhnbdpeajdjg?hl=en'>Funkify Disability Simulator</a> with “Peripheral Pierre” activated. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1d111987-9d08-48ad-916f-9ade9ae4fa19/central-scotoma.png'>Large preview</a>)" alt="Screenshot of an online stationery store with a large, black circle in the center, and the rest of the screen a bit blurred to show the impact of Central scotoma" >}}

- **Tunnel Vision**  
Loss of vision in the peripheral visual field.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/00aad7fd-f47e-4765-a411-bd323b779fde/tunnel-vision.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/00aad7fd-f47e-4765-a411-bd323b779fde/tunnel-vision.png" sizes="100vw" caption="<a href='https://chrome.google.com/webstore/detail/funkify-%E2%80%93-disability-simu/ojcijjdchelkddboickefhnbdpeajdjg?hl=en'>Funkify Disability Simulator</a> with “Tunnel Toby” activated. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/00aad7fd-f47e-4765-a411-bd323b779fde/tunnel-vision.png'>Large preview</a>)" alt="Screenshot of an online stationery store with only a small part of the site visible, to show the impact of tunnel vision" >}}

- **Hemianopia**  
Loss of vision in half the visual field.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c800f3dc-c75c-4ebf-9b88-660a1358f152/hemianopia.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c800f3dc-c75c-4ebf-9b88-660a1358f152/hemianopia.png" sizes="100vw" caption="<a href='https://chrome.google.com/webstore/detail/nocoffee/jjeeggmbnhckmgdhmgdckeigabjfbddl'>NoCoffee Vision Simulator</a> with ”Side (hemianopia)” activated. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c800f3dc-c75c-4ebf-9b88-660a1358f152/hemianopia.png'>Large preview</a>)" alt="Screenshot of an online stationery store with only half the screen visible, to show the impact of Hemianopia" >}}

- **Blindness**  
This term is only used for complete or near-complete loss of vision.

{{% feature-panel %}}

## Warp &amp; Weft

Weaving is a method of textile production in which the longitudinal **warp** and transverse **weft** come together to make a fabric. As in weaving, the creation of a user experience for people with visual impairments is based on the interweaving of two components: accessibility and usability.  

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/006ee7e2-df49-404a-bc5a-700efc8de2cb/weave-diagram.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/006ee7e2-df49-404a-bc5a-700efc8de2cb/weave-diagram.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/006ee7e2-df49-404a-bc5a-700efc8de2cb/weave-diagram.png'>Large preview</a>)" alt="A diagram showing the structure of warp (vertical) and weft (horizontal) yarns in a weave" >}}

### Warp — Accessibility

Web accessibility means that websites, web applications, and technologies are designed and developed so that people with disabilities can use them. More specifically, people can: perceive, understand, navigate, and interact with and contribute to the web.

There is a range of disabilities that can impact how people access the web, including auditory, cognitive, neurological, physical, speech, and visual.

<blockquote>“The power of the web is in its universality. Access by everyone regardless of disability is an essential aspect”.<br /><br />&mdash; Tim Berners-Lee, inventor of the World Wide Web</blockquote>

In order to ensure the universality of the web and provide access to everyone, as Berners-Lee noted, there’s a wide range of web accessibility standards (which come with a myriad of acronyms).

Let’s focus on these three key components:

*   [Web Content Accessibility Guidelines (WCAG)](https://www.w3.org/WAI/standards-guidelines/wcag/)  
Define how content (such as texts, images, forms) should be created so that it will be accessible through the use of sound, mouse-free navigation, compatibility with assistive technologies, and more.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/47ca7f16-924d-4050-ad79-0200344f8737/wcag-documentation.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/47ca7f16-924d-4050-ad79-0200344f8737/wcag-documentation.png" sizes="100vw" caption="<a href='https://www.w3.org/TR/WCAG21/'>WCAG 2.1</a> has 13 guidelines that are organized under 4 principles: perceivable, operable, understandable, and robust. For each guideline, there are testable success criteria which are at three levels: A, AA and AAA. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/47ca7f16-924d-4050-ad79-0200344f8737/wcag-documentation.png'>Large preview</a>)" alt="Screenshot of the web content accessibility guidelines 2.1 documentation with the main sections highlighted, including the principle, guideline and success criterion" >}}

*   [Authoring Tool Accessibility Guidelines (ATAG)](https://www.w3.org/WAI/standards-guidelines/atag/)  
Define how content editing tools (such as HTML editors or CMSs) should be created so that people with disabilities can author content that is compatible with WCAG.
*   [User Agent Accessibility Guidelines (UAAG)](https://www.w3.org/WAI/standards-guidelines/uaag/)  
Define how user agents (such as browsers, browser extensions, and media players) should be created in order to be accessible.

Compliance with web accessibility guidelines is technical and requires a high level of expertise. While you can use these guidelines to create a more accessible product, does that mean the product is also easy to use?

While I tested visually impaired and blind participants on a product that was accessible according to the guidelines, I encountered the following cases:

*   Visually impaired participants were unable to read a large-size font because it’s weight was too thin. 
*   Blind participants were unable to book a reservation at a restaurant because the navigation between dates was too hard to understand.
*   Visually impaired participants were unable to find their checkout because it opened elsewhere on the screen that was out of their visual field.

In other words, formal adoption of the web accessibility guidelines can certainly lead to compliance, but not necessarily usability. This is also recognized in [W3C documentation](https://www.w3.org/WAI/fundamentals/accessibility-usability-inclusion/) where there is an explicit reference to the fact that usability must always be taken into account:

<blockquote>“Yet when designers, developers, and project managers approach accessibility as a checklist to meet these standards, the focus is only on the technical aspects of accessibility. As a result, the human interaction aspect is often lost, and accessibility is not achieved.”</blockquote>

I particularly like Bruce Lawson’s pictorial description in the introduction of the book _Web Accessibility: Web Standards and Regulatory Compliance_:

<blockquote>“I wouldn’t want you to think that making your sites accessible is just a matter of following a recipe; to make nourishing accessibility pudding, add one part CSS, one part valid code, a pinch of semantic markup, and a cupful of WCAG guidelines. It would be nice if I could guarantee that slavishly following such a recipe would make everything lovely… but the annoying fact is that people are people, and insist on having different needs and abilities.”</blockquote>

Compliance with accessibility standards is a necessary goal (and often required by law), but it can’t exist in a vacuum.

### Weft — Usability

Usability is a measure of how much a specified user in a particular environment can use a user-interface to achieve a defined goal.

Usability is not an exact science that consists of formulas or black and white answers. Over the years, various usability models have been proposed for measuring the usability of software systems. One of the models was created by Jacob Nielsen, who proposed in his 1993 book _Usability Engineering_ that usability is not a single, one-dimensional property of a user interface, but consists of five core attributes:

1. **Learnability**  
How easy is it for the users to accomplish basic tasks during the first time they encounter the design?
2. **Efficiency**  
How fast can users perform tasks and be productive after learning the design?
3. **Memorability**  
How fast can returned-users reestablish proficiency, after a period of not using the design, without having to relearn everything?
4. **Errors**  
How many errors do users make, how serious are these errors, and how easily can they recover from the errors?
5. **Satisfaction**  
How subjectively are users satisfied with the use of the design?

To ensure a product is usable, it’s essential that these five cornerstones are dominant in the design and development process.

{{% ad-panel-leaderboard %}}

## What I Learned From Conducting A Usability Test With Visually Impaired And Blind Participants

A usability test is a structured interview where participants that match a target audience perform a series of tasks. While the participants are working, they verbally describe their reactions to interactions with the product. This allows the observers to understand not only what the participants are doing in the interface, but why they’re doing so. 

When I conducted my first usability test with visually impaired and blind participants on a product that is in compliance with the accessibility standards, I wasn’t able to find too much information about conducting these types of sessions. So, I thought to share some highlights from the process. These are divided into three parts:

<ol>
	<li><a href="#before">Before The Session</a></li>
	<li><a href="#during">During The Session</a></li>
	<li><a href="#after">After The Session</a></li>
</ol>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c8367717-2b93-4cda-a617-df2b274c4733/usability-participant.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c8367717-2b93-4cda-a617-df2b274c4733/usability-participant.png" sizes="100vw" caption="We had 5 sessions: 2 with visually impaired participants, and 3 with blind participants. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c8367717-2b93-4cda-a617-df2b274c4733/usability-participant.png'>Large preview</a>)" alt="A visually impaired participant examines a magnified user-interface while a moderator watches from the side" >}}

### 1. Before The Session

#### Defining The Test Goal

This is a starting point for a usability test. The test goal should be clear, specific, achievable, and relevant. The way we defined the goal is by collaborating with a multidisciplinary team: Designers, Product Managers, Developers, Content Writers, and QAs &mdash; each role brings a different perspective and expertise.

#### Creating Tasks

Since visually impaired and blind participants can take a longer time to complete tasks due to the way they navigate the site, we prioritized the tasks based on what’s most important to us, but this doesn’t mean that complex tasks need to be compromised.

#### Setting A Schedule:

Setting up our schedule for usability sessions required us to consider a range of issues, especially considering the complexity of our product and the physical limitations of the participants. This included:

*   Time to accompany the participant when entering and exiting the lab (we assigned a staff member to accompany each of the participants).
*   Time to configure and arrange assistive technology settings for each of the participants, depending on their abilities and if they brought their own equipment.
*   A time that the participants can comfortably navigate the interface.
*   Time to debrief with the staff after each session.

We set one hour for each session and 45 minutes between sessions which was stressful  and forced us to rush (it is better to take an hour between sessions).

#### Recruiting Participants

The selection of participants whose background and abilities represent the target audience is a crucial component in the testing process. In our case, we were looking for visually impaired and blind candidates who have experience purchasing products online.

Sources for finding participants can vary, such as information and technology learning centers for people with visual impairments in hospitals, colleges, and universities.

In our case, my wife, an ophthalmologist by profession, referred me to the operator of the *Information Center for the Visually Impaired and Blind* at the hospital where she works. To my delight, I encountered someone who was happy to help and referred me to a group of relevant candidates.

In order to prepare the candidates, we discussed the following:

*   The nature of the test, including that  there will be people watching them and a recording of the session.
*   Their online shopping experience. Do they primarily purchase on a computer or mobile? What is their favorite browser? What assistive technologies do they use? Additionally, in instances when the test is done in a non-English speaking country, ask them about the level of language proficiency when the interface is in English.
*   That each participant will receive an incentive (it’s important to make sure the incentive is also accessible).
*   If the candidates could bring their equipment with them.

Overall the responsiveness was high, and most candidates expressed a desire to attend.

#### Setting Up The Test Position

The candidates who confirmed their participation had different ways of interacting with the web. Some consume information by customizing settings for fonts, colors contrast, screen magnification, or listening to a screen reader, while some needed a combination of a few things.

Since most participants were not interested in bringing equipment with them (mainly due to difficulties carrying it or having a desktop computer), we had to take care of it ourselves. Once we found a staff member who understood how to configure the assistive technology, it didn’t take long to set up or adjust between sessions.

We set up various browsers and assistive technologies, including  NVDA, JAWS, and ZoomText.

Additionally, the camera and microphone should be adjusted to the needs of visually impaired participants, who need to get closer to the screen and view it at different angles. 

It’s necessary to check before starting that the lab is physically accessible as well. For example, that there are no stairs at the entrance, there’s an accessible toilet, access to public transportation, and a place for a guide dog to sit.

#### Sending A Non-Disclosure Agreement (NDA)

Like any other instance where you want to get informed consent, you can send the NDA online using an accessible PDF. 

#### Conducting A Dry Run Session

A week before the usability session, we conducted a dry run with a visually impaired participant in order to avoid unexpected difficulties. For example, we saw that the screen sharing tool we were using conflicted with one of the assistive technologies. Additionally, the dry run helped us get a better feeling for the schedule. For example, the introduction of the moderator was too long, so we weren’t able to check some of the planned tasks. Also, it helped us to refine the test plan in instances where certain tasks weren’t clear, more difficult than expected, or too easy. Just as importantly, the dry run allowed the moderators to train with a “real” participant, and mentally prepare themselves for this type of usability test.

{{% ad-panel-leaderboard %}}

### 2. During The Session

#### Moderator

The moderator is an important key to make this type of usability test go smoothly. Jared M. Spool once wrote:

<blockquote>“The best usability test moderators have a lot in common with an orchestra conductor. They keep the participant comfortable and stress-free. The moderator tries to make the participant forget they are in a foreign environment with a bunch of strangers who intensely watch everything that he/she does. They keep the information flowing to the design team, especially the tough news. And they do all this with organized flair and patience, ensuring every aspect of the user’s experience is explored.”<br /><br />&mdash; <a href="https://articles.uie.com/moderating_multiple_personalities/">Moderating With Multiple Personalities: 3 Roles For Facilitating Usability Tests</a></blockquote>

In a test with visually impaired and blind participants, the orchestra conductor should behave even more sensitively. For example, during sessions where a screen reader was used—which affects the concentration of the observers—it is important to ask participants to speak loud and clear, so we can understand their process and how they comprehend tasks.

#### Observers

We invited relevant people from different departments so they would be directly exposed to participants and have a better chance to absorb the key information. After all, getting a report on the results doesn’t provide the same benefits as seeing the participants’ experience firsthand.

During the test, it’s important to pay attention and listen to the participant–even though the screen reader is distracting.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4d18a84a-d7f9-4e7c-9e87-4a5f8e729de3/usability-observers.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4d18a84a-d7f9-4e7c-9e87-4a5f8e729de3/usability-observers.jpg" sizes="100vw" caption="The beauty of accessibility is that it spans a wide range of roles. Here you can see a product designer, front-end developer, and analyst observing one of the sessions. In total, we had 12 observers. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4d18a84a-d7f9-4e7c-9e87-4a5f8e729de3/usability-observers.jpg'>Large preview</a>)" alt="Three people remotely observing the usability session from a conference room" >}}

### 3. After The Session

#### Writing A Report

After the sessions, we wrote a report with our insights from the test:

Some of the insights were related to bugs that we had to fix. For example, blind participants didn’t always find a particular button in the NVDA’s Elements List dialog, or sometimes they didn’t receive confirmation in the screen reader after clicking on the "Like" button.

Some of the insights were related to the content. For example, some blind participants didn’t notice they were filling out the wrong form or wanted to scan an entire page quickly, but the strings in the aria-labels were too long.

Some of the insights were related to visuals. For example, visually impaired participants who use magnifying software didn’t understand how to proceed when the next action appeared in a different area of ​​the screen. Other times they didn’t notice the modal “close” icon &mdash; although its color was high contrast. 

In the end, we found 65 issues that impact multiple departments in the company.

Additionally, our report included happy moments from the sessions. For example, some participants noted that using an icon next to a link helps them because they don’t have to read the text. Others liked the contrast of the placeholder text, and some mentioned that the image-zoom worked very well.

## “Nothing About Us Without Us”

On July 26, 2020, the world marked the 30th anniversary of the signing of the American Disability Act (ADA). This opened doors that were closed too long for people with disabilities, such as participating in basic daily activities like traveling by bus, going to school, attending movies, visiting museums, and more.

All the events marking this historic signature were canceled or moved online due to the spread of the coronavirus.

One of the online events was the [Virtual Crip Camp](https://cripcamp.com/officialvirtualexperience/?utm_content=131676188&utm_medium=social&utm_source=facebook&hss_channel=fbp-114193500436&fbclid=IwAR1SiZIr-_ilBVZj_c4E4nrjSOw5zU0s9KRUsBcPDmS66FTnL6nk9R2FTpo), featuring trailblazing speakers from the disability community. In the invitation to this event, there is a green bus with the slogan “<em>Nothing About Us Without Us</em>”:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b08b5924-1f35-401f-86d6-eecaf321aa28/virtual-crip-camp-invitation.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b08b5924-1f35-401f-86d6-eecaf321aa28/virtual-crip-camp-invitation.png" sizes="100vw" caption="The Invitation for the Virtual Crip Camp (Of course, it’s related to the rousing <a href='https://www.netflix.com/il-en/title/81001496'>Netflix’s documentation</a>.)  (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b08b5924-1f35-401f-86d6-eecaf321aa28/virtual-crip-camp-invitation.png'>Large preview</a>)" alt="A light green bus with the phrase “Nothing About Us Without Us” along the side underlined in red. Red-colored peace symbols are located on the back and front of the bus. A crutch and various black hands raised in fists and love fingers reach out of the windows. A wheelchair ramp is visible with the side door wide open. The text reads “Crip Camp: The Official Virtual Experience” in bold black letters" >}}

_“Nothing About Us Without Us”_ conveys the idea that a decision should be made with the direct participation of those most affected. The slogan came into use by activists with disabilities during the 1990s and is a connecting point between various disability rights movements around the world. The widespread use of the slogan (and in social networks using the hashtag [#NothingAboutUsWithoutUs](https://twitter.com/search?q=%23NothingAboutUsWithoutUs&src=typed_query)), reflects the desire of people with disabilities to take part in shaping the decisions that affect their personal lives.

The same DNA is common with the _User-Centered Design_ approach, whose philosophy is that the product should fit the user—and not make the user adapt to the product. Under the _User-Centered Design_ approach, there is a collaboration with users through a variety of techniques applied at different points in the product development lifecycle. Usability testing is one of those techniques.

The real magic of the usability test is not the reporting of data after the test, but the change in the perspective of team members who watch the participant in real-time and absorb what those participants say, think, do and, feel. As a result, they’ll develop empathy and better understand, reflect, and share the needs and motivations of another person.

In the case of participants with disabilities, this empathy is essential for many reasons — it harnesses the observers, creates motivation for change, and raises awareness about the experience for people with disabilities.

While automated tools that offer to make websites accessible can, at best, show us how well our site meets WCAG’s guidelines, they don’t clearly reflect how usable the website is for people with disabilities. In regard to a mechanistic approach to accessibility, my colleague Neil Osman, an accessibility engineer at Wix who is visually impaired, often uses the following expression:

<blockquote>"You can put lipstick on a pig, but it’s still a pig."</blockquote>

Making a usable product is not just the ability to rely on a list of accessibility standards. In order to create solutions for people with disabilities, we need to be exposed to them firsthand.

**Disclaimer**: *The information provided here does not, and is not intended to, constitute legal advice; instead, all information, content, and materials are for general informational purposes only. The information contained herein may not constitute the most up-to-date legal or other information.*

<hr />

*Credits: Jeremy Hoover, Udi Gindi, Bat-El Sebbag, Nir Horesh, Neil Osman, Alon Fridman Waisbard, Shira Fogel and Zivan Krisher contributed to this article.*

{{< signature "ra, il" >}}
