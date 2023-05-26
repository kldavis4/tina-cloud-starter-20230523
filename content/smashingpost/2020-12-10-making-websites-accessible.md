---
title: 'Making Websites Easier To Talk To'
slug: making-websites-accessible
author: frederick-o-brien
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ba976a66-64a0-47f8-b36c-f76f07b7442a/making-websites-accessible.png
date: 2020-12-10T12:00:00.000Z
summary: >-
  Modern websites aren’t inseparable from screens any more. Between phone assistants, home speakers, and screen readers, more and more people are using the web without even looking at it. Websites need to evolve in kind.
description: >-
  Modern websites aren’t inseparable from screens any more. Between phone assistants, home speakers, and screen readers, more and more people are using the web without even looking at it. Websites need to evolve in kind.
categories:
  - Design
  - Accessibility
  - UX
  - Chatbots
---

A website without a screen doesn’t sound right does it. Like a book without pages, or a car without a steering wheel. Yet there are audiobooks, hand-free vehicles. And increasingly websites are being used without even being looked at &mdash; at least by humans. 

Phone assistants and home speakers are a growing part of the Internet ecosystem. In the article, I will try to break down what that means for websites going forward, what designers can do about it, and why this might finally be a leap forward to accessibility. [More than two thirds of the web is inaccessible to those with visual impairments](https://devops.com/new-research-shows-how-the-internet-is-unavailable-to-blind-users/), after all. It’s time to make websites easy to talk to.

## Invasion Of The Home Speakers

[Global smart speaker sales topped 147 million in 2019](https://marketingland.com/more-than-200-million-smart-speakers-have-been-sold-why-arent-they-a-marketing-channel-276012) and pandemic or no pandemic the trend is going up. Talking is faster than typing, after all. From Google Home to Alexa to smartphone assistants, cars, and even fridges, more and more people are [using programmes to search the web on their behalf](https://voicebot.ai/2019/10/11/over-20-of-uk-households-have-smart-speakers-while-germany-passes-10-and-ireland-approaches-that-milestone/).

{{< rimg  href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/adebadb6-e9fb-4751-a8b9-42f253d3ce6c/1-making-websites-accessible.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/adebadb6-e9fb-4751-a8b9-42f253d3ce6c/1-making-websites-accessible.png" sizes="100vw" caption="User testing for the next generation of Google home speakers. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/adebadb6-e9fb-4751-a8b9-42f253d3ce6c/1-making-websites-accessible.png'>Large preview</a>)" alt="Screenshot from the film adaptation of George Orwell’s ‘1984’." >}}

Putting aside the rather ominous Big Brother Inc undertones of this trend, it’s safe to say hundreds of millions of people are already exploring the web each day without actually looking at it. Screens are no longer essential to browsing the web and sites ought to adapt to this new reality. Those that don’t are cutting themselves off from hundreds of millions of people. 

{{% pull-quote %}}
Developers, designers and writers alike should be prepared for the possibility that their work will not be seen or clicked at all — it will be heard and spoken to.
{{% /pull-quote %}}

## Designing Invisibility

There are two main prongs to the topic of website talkiness &mdash; tech and language. Let’s start with tech, which runs the gauntlet all the way from basic content structure to semantic markup and beyond. I’m as keen on good writing as anyone, but it’s not the place to start. You could have website copy worthy of a Daniel Day-Lewis performance, but if it isn’t arranged and marked up properly it won’t be worth much to anyone.

### Age Old Foundations

The idea of websites being understood without being seen is not a new one. Screen readers have been around for decades, [with two-thirds of users choosing speech as their output, with the final third choosing braille](https://webaim.org/projects/screenreadersurvey7/).

The focus of this article goes further than this, but making websites screen reader friendly provides a rock solid foundation for the fancier stuff below. I won’t linger on this too long as others have written extensively on the topic (links below) but below are things you should always be thinking about:

- Clear navigation in-page and across the site.
- Align DOM structure with visual design.
- Alt text, no longer than 16 words or so, if an image does not need alt text (if it’s a background for example) have empty alt text, not *no* alt text.
- Descriptive hyperlinks.
- ‘Skip to content links’.

Visual thinking actually blinds us to many design failings. Users can and often do put the pieces together themselves, but that doesn’t do much for machine-readable websites. Making websites easy to talk to starts with making them text-to-speech (TTS) friendly. It’s good practice and it massively improves accessibility. Win win. 

#### Further Reading On TTS Design And Accessibility 

- [Text to Speech](https://www.w3.org/WAI/perspective-videos/speech/) by W3C
- [Front End North Pt 2: Léonie Watson blew my mind](https://supercooldesign.co.uk/blog/front-end-north-leonie-watson-blew-my-mind)
- [Text-To-Speech With AWS (Part 1)](https://www.smashingmagazine.com/2019/08/text-to-speech-aws/)
- [Text-To-Speech And Back Again With AWS (Part 2)](https://www.smashingmagazine.com/2019/10/text-to-speech-aws-part-2/)
- [Notes On Client-Rendered Accessibility](https://www.smashingmagazine.com/2015/05/client-rendered-accessibility/)
- [Labelling Controls](https://www.w3.org/WAI/tutorials/forms/labels/) by the W3C
- [Using the aria-label attribute](https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/ARIA_Techniques/Using_the_aria-label_attribute) by Mozilla
- [I Used The Web For A Day Using A Screen Reader](https://www.smashingmagazine.com/2018/12/voiceover-screen-reader-web-apps/)
- [From The Experts: Global Digital Accessibility Developments During COVID-19](https://www.smashingmagazine.com/2020/11/global-digital-accessibility-developments-during-covid/)

### Fancier Stuff

As well as laying a strong foundation, designing for screen readers and accessibility is good for its own sake. That’s reason enough to mention it first. However, it doesn’t quite provide for the uptick of ‘hands-free’ browsing I spoke about at the start of this piece. Voice user interfaces, or VUIs. For that we have to dig into semantic markup.

Making websites easy to talk to means labelling content at a much more granular level. When people ask their home assistant for the latest news, or a recipe, or whether that restaurant is open on Tuesday night, they don’t want to navigate a website using their voice. They want the information. Now. For that to happen information on websites needs to be clearly labelled.

I’ve rather [tumbled down the Semantic Web rabbit hole](https://www.smashingmagazine.com/2020/10/developing-semantic-web/) this year, and I don’t intend to repeat myself here. The web can and should aspire to be machine readable, and that includes talkiness.

{{% feature-panel %}} 

Semantic markup already exists for this. One is called ‘speakable’, a Schema.org property currently in beta which highlights the parts of a web page which are [‘especially appropriate for text-to-speech conversion.’](https://schema.org/speakable)

For example, I and two friends review an album a week as a hobby. We recently redesigned the website with semantic markup integrated. Below is a portion of a page’s structured data showing speakable in action:

<div class="break-out">

<pre><code class="language-javascript">{
  "@context": "https://schema.org",
  "@type": "Review",
  "reviewBody": "It's breathless, explosive music, the kind of stuff that compels listeners to pick up an instrument or start a band. Origin of Symmetry listens like a spectacular jam — with all the unpolished, patchy, brazen energy that entails — and all in all it's pretty rad, man.",
  "datePublished": "2015-05-23",
  "author": [
	{
  	"@type": "Person",
  	"name": "André Dack"
	},
	{
  	"@type": "Person",
  	"name": "Frederick O'Brien"
	},
	{
  	"@type": "Person",
  	"name": "Andrew Bridge"
	}
  ],
  "itemReviewed": {
	"@type": "MusicAlbum",
	"name": "Origin of Symmetry",
	"@id": "https://musicbrainz.org/release-group/ef03fe86-b54c-3667-8768-029833e7e1cd",
	"image": "https://alpha.audioxide.com/api/images/album-artwork/origin-of-symmetry-muse-medium-square.jpg",
	"albumReleaseType": "https://schema.org/AlbumRelease",
	"byArtist": {
  	"@type": "MusicGroup",
  	"name": "Muse",
  	"@id": "https://musicbrainz.org/artist/9c9f1380-2516-4fc9-a3e6-f9f61941d090"
	}
  },
  "reviewRating": {
	"@type": "Rating",
	"ratingValue": 26,
	"worstRating": 0,
	"bestRating": 30
  },
  "speakable": {
	"@type": "SpeakableSpecification",
	"cssSelector": [
  	".review-header__album",
  	".review-header__artist",
  	".review-sidebar__summary"
	]
  }
}</code></pre>
</div>

So, if someone asks their home speaker assistant what *Audioxide* thought of *Origin of Symmetry* by Muse, speakable should direct it to the album name, the artist, and the bite-sized summary of the review. Convenient and to the point. (And spares people the ordeal of listening to our full summaries.) Nothing’s there that wasn’t there before; it’s just labelled properly. You’ll notice as well that choosing a CSS class is enough. Easy. 

This kind of functionality lends itself better to certain types of sites than others, but possibilities are vast. Recipes, news stories, ticket availability, contact information, grocery shopping… all these things and more can be made better if only we get into the habit of making websites easier to talk to, every page packed with clearly structured and labelled information ready and waiting to answer queries when they come their way.

Beyond that the big brains at places like Google and Mozilla are hard at work on dedicated [web speech APIs](https://wicg.github.io/speech-api/), allowing for more sophisticated user interactions with things like forms and controls. It’s early days for tech like this but absolutely something to keep an eye on.

The rise of home speakers means old and new worlds are colliding. Providing for one provides for the other. Let’s not forget websites are supposed to have been designed for screen readers for decades.

#### Further Reading

- [Web apps that talk &mdash; Introduction to the Speech Synthesis API](https://developers.google.com/web/updates/2014/01/Web-apps-that-talk-Introduction-to-the-Speech-Synthesis-API)
- [Web Speech Concepts and Usage](https://developer.mozilla.org/en-US/docs/Web/API/Web_Speech_API) by Mozilla
- [What are Voice User Interfaces?](https://www.interaction-design.org/literature/topics/voice-user-interfaces) By the Interaction Design Foundation

{{% ad-panel-leaderboard %}}

## Writing For Speaking

You’ve taken steps to make your website better understood by screen readers, search engines, and all that good stuff. Congratulations. Now we get to the fuzzier topics of tone and personality.

Designing a website to speak is different to designing it to be read. The nature of user interactions is different. A major point to keep in mind is that where voice queries are concerned websites are almost always responsive &mdash; answering questions, giving recipes, confirming orders.

[An Open NYT study found](https://open.nytimes.com/how-might-the-new-york-times-sound-on-smart-speakers-3b59a6a78ae3) that for household users ‘interacting with their smart speakers sometimes results in frustrating, or even funny, exchanges, but that feels like a better experience than being tethered to a phone that pushes out notifications.’

In other words, you can’t and shouldn’t force the issue. The look-at-me ethos of pop ups and ads and endless engagement has no place here. Your task is having a good site that gives information on command as clearly and succinctly as possible. A virtual butler, if you will.

What this means in linguistic terms is:

- Succinct sentences,
- Plain, simple language,
- Front-loaded information (think [inverted pyramid](https://en.m.wikipedia.org/wiki/Inverted_pyramid_(journalism))),
- Phrasing answers as complete sentences.

Say what you write out loud, have free text-to-speech systems like [TTSReacher](https://ttsreader.com/) say it back to you. Words can sound very different out loud than they do written down, and visa versa. [I have my reservations about readability algorithms](https://www.smashingmagazine.com/2020/05/readability-algorithms-tools-targets/), but they’re useful tools for gauging clarity.

#### Further Reading

- [‘Readability Testing for Voice Content’](https://alistapart.com/article/usability-testing-for-voice-content/) on *A List Apart*
- [*The Elements of Style*](https://www.jlakes.org/ch/web/The-elements-of-style.pdf) by William Strunk Jr.

{{% ad-panel-leaderboard %}}

## HAL, Without The Bad Bits

Talking with websites is part of a broader shift towards channel-agnostic web experiences. The nature of websites is changing. From desktop to mobile, and from mobile to smart home systems, they are becoming more fluid. We all know about ‘mobile-first’ indexing. How long until it’s ‘voice-first’? 

Moving away from rigid constraints is daunting, but it is liberating too. We look at websites, we listen to them, we talk to them. Each one is like a little HAL, with as much or little personality and/or murderous intent as we see fit to design into it.

Here are steps we can take to make websites easier to talk to, whether building from scratch or updating old projects:

- Navigate your site using screen readers.
- Try vocal queries via phone/home assistants.
- Use semantic markup.
- Implement speakable markup.

Designing websites for screenless situations improves their accessibility, but it also sharpens their personality, their purpose, and their usefulness. As [Preston So writes for *A List Apart*](https://alistapart.com/article/usability-testing-for-voice-content/), ‘it’s an effective way to analyze and stress-test just how channel-agnostic your content truly is.’

Making your websites easy to talk to prepares them for the channel-agnostic web, which is fast becoming a reality. Rather than text and visuals on a screen, sites must be abstract and flexible, ready to interact with an ever growing range of devices. 

{{< signature "ra, yk, il" >}}

