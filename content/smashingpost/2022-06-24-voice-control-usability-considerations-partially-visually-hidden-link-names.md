---
title: 'Voice Control Usability Considerations For Partially Visually Hidden Link Names'
slug: voice-control-usability-considerations-partially-visually-hidden-link-names
author: eric-bailey
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/54545ed9-3238-4807-b56c-3c2b18e576c7/voice-control-usability-considerations-partially-visually-hidden-link-names-sharing-card.jpg
date: 2022-06-24T09:00:00.000Z
summary: >-
  Overcorrecting for one form of disability may unintentionally negatively impact the experience for other forms of disability. For example, partially visually hidden link names may work great for people who use screen readers, but this approach can be problematic for people who rely on voice control software. Because of this, your designs need to be flexible and adaptable, as well as accommodate the many different ways people can interact with them.
description: >-
  Partially visually hidden link names may be good for people who use screen readers, but they can be problematic for those who rely on voice control software. Here’s a suggestion on how to solve this.
categories:
  - Accessibility
  - Usability
  - User Experience
  - Voice
---
Digital accessibility tends to be taught through the lens of how your experience works (or fails to work) with a screen reader. It makes sense to think that, if [it works for a screen reader](https://alistapart.com/article/semantics-to-screen-readers/), it will also work for a lot of other kinds of assistive technology.

However, this approach also indirectly reinforces the narrative that blindness is the majority experience. Within this narrative, there is also some subtlety in the fact that [not everyone who uses a screen reader is blind](https://adrianroselli.com/2017/02/not-all-screen-reader-users-are-blind.html). 

[The majority disability experience is actually depression](https://www.who.int/news-room/fact-sheets/detail/depression), which is a complicated disability with highly variable symptoms. One of the most notable symptoms of depression is that it negatively impacts your cognition, which affects your ability to understand things.

The other salient bit is that the majority experience is not default. The point I’m getting at is that overcorrecting for one form of disability may unintentionally negatively impact the experience for other forms of disability &mdash; voice control software being one example.

## Unique Link Names

Making each link’s accessible name unique is an important thing to do. It helps clarify where each link goes to someone who is navigating via a specialized screen reader browsing mode. For example, all major screen readers have the ability to list all the links on the current page or view, with the links being removed from their surrounding text content and context.

Eleven links called “learn more” don’t make a lot of sense when separated from their surrounding context. It’s far better to tell the reader what they’ll be learning about:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4601bced-d2e3-463d-8f4a-f01e1179e692/1-voice-control-usability-considerations-partially-visually-hidden-link-names.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4601bced-d2e3-463d-8f4a-f01e1179e692/1-voice-control-usability-considerations-partially-visually-hidden-link-names.png" width="800" height="625" sizes="100vw" caption="Screenshots of NVDA’s Elements List panel. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4601bced-d2e3-463d-8f4a-f01e1179e692/1-voice-control-usability-considerations-partially-visually-hidden-link-names.png'>Large preview</a>)" alt="Two screenshots of NVDA’s Elements List panel. The first one lists the phrase “learn more” 11 times. The second one provides more detail about what you’ll learn more about, with 11 examples of clickbait-style article headlines about movies." >}}

## Visually Hidden Text

If you use CSS libraries such as [Bootstrap](https://getbootstrap.com/docs/4.1/getting-started/accessibility/#visually-hidden-content) or [Tailwind](https://tailwindcss.com/docs/screen-readers), you may be familiar with a specialized class that a screen reader can read, but is not displayed visually. These classes help provide additional context, such as supplying [additional heading elements to help with way-finding](https://webaim.org/projects/screenreadersurvey9/#heading).

<pre><code class="language-javascript">&lt;h2 class="sr-only"&gt;
  Footer
&lt;/h2&gt;
</code></pre>

## Partially Visually Hidden Text

Another thing visually hidden classes are commonly used for is to hide the portion of an interactive control that makes its name unique. A common pattern for this is a call-to-action (CTA) link in a card component:

{{< codepen height="300" theme_id="light" slug_hash="gOvJOav" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [Hidden link names](https://codepen.io/smashingmag/pen/gOvJOav) by <a href="https://codepen.io/ericwbailey">Eric Bailey</a>.{{< /codepen >}}  


The typical reason the visually hidden text is inserted in the first place is that the designer of the card component decided that the truncated look of the CTA link looked “cleaner.” This aesthetic decision is made because of a historical lack of accessibility concerns in design education. 

A common variant of this pattern is using ARIA in place of a visually hidden class:

<pre><code class="language-javascript">&lt;!-- Never do this --&gt;
&lt;a aria-label="Learn more about these 10 overlooked vampire movies" class="card-cta" href="/path/to/article"&gt;Learn more&lt;/a&gt;
</code></pre>

In this case, the `aria-label` declaration provides the unique, accessible name. Many developers are quick to use it, even though [ARIA is something you should only use when there are no other alternatives](https://www.w3.org/TR/using-aria/#firstrule). Misuse of `aria-label`:

- May violate [Web Content Accessibility Guidelines (WCAG) Success Criterion 2.5.3 Label in Name](https://w3c.github.io/wcag/guidelines/22/#label-in-name), 
- [May not be translated](https://adrianroselli.com/2019/11/aria-label-does-not-translate.html), and 
- Makes the accessible name impossible to see, making it impossible to know how to activate the control.  
  
## Problems With Partially Visually Hidden Text

Partially visually hidden text &mdash; while helpful for people who use screen readers &mdash; can negatively impact others. Truncated CTA links can be problematic for people who:

- Are browsing using screen magnification or an increased default font size, where the CTA link might not have the context of the surrounding card content;
- Have cognitive and digital literacy concerns, where the phrase is not descriptive enough to indicate specifically where someone will navigate to;
- Aren’t fluent in the language used and may have difficulty constructing the larger context the rest of the card’s content provides;
- Use voice control software, where obscuring the full, accessible name of the link keeps them from easily activating it.

Voice Control on macOS and iOS both don’t support being able to directly say “Click learn more,” since they are listening for the full, accessible name of the link. **This includes the visually hidden portion**. 

Since part of each link is visually hidden, there is no way to know each link’s actual accessible name, unless you’re augmenting your browsing experience with a screen reader, or with a developer tooling to inspect the underlying code.

{{< youtube id="dG9kdwLLlMk" caption="Partially visually hidden link names using macOS and iOS Voice Control" >}}

## More About Voice Control Software

The reason I am focusing on voice control software is because it presents a potential objective access barrier. Sadly, concerns around subjective barriers are commonly dismissed by people not immediately impacted by them.

If you are unfamiliar, voice control is one of the many ways you can use a device that doesn’t rely on a mouse, keyboard, or physical touch. As its name implies, you use your voice to issue commands, and specialized software will translate that into things like navigating, entering, and editing content.  

{{% feature-panel %}}

### The Landscape  

Every major operating system provides some degree of voice control:

- Windows uses [Voice Recognition](https://support.microsoft.com/en-us/windows/use-voice-recognition-in-windows-83ff75bd-63eb-0b6c-18d4-6fae94050571),
- macOS and iOS use [Voice Control](https://support.apple.com/en-us/HT210539), and
- Android uses [Voice Access](https://support.google.com/accessibility/android/answer/6151848?hl=en).

Voice assistants are another form of voice control software. Examples of this are Apple’s [Siri](https://www.apple.com/siri/), Microsoft’s [Cortana](https://www.microsoft.com/en-us/cortana), and Amazon’s [Alexa](https://www.amazon.com/b?node=21576558011). These voice assistants are interesting in sense that they can accomplish some, but not all, of the things that more full-featured voice control software can.

There are also third-party applications that provide specialized voice control functionality. Two notable examples are: 

1. [Dragon](https://www.nuance.com/dragon.html), which offers long-form voice dictation and web browsing.
2. [Talon Voice](https://talonvoice.com/), which offers powerful customization and scripting.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/10715f4a-3f5d-41d5-81e9-0102f7bd8314/2-v2-voice-control-usability-considerations-partially-visually-hidden-link-names.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/10715f4a-3f5d-41d5-81e9-0102f7bd8314/2-v2-voice-control-usability-considerations-partially-visually-hidden-link-names.jpg" width="800" height="1004" sizes="100vw" caption=" Voice control software. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/10715f4a-3f5d-41d5-81e9-0102f7bd8314/2-v2-voice-control-usability-considerations-partially-visually-hidden-link-names.jpg'>Large preview</a>)" alt="A grid with three columns and rows. The three logos for the first row are Voice Access by Google, Voice Control by Apple, and Voice Recognition by Apple. The logos for the second row are Alexa by Amazon, Cortana by Microsoft, and Siri by Apple. The logos for the third row are Dragon by Nuance and Talon by aegis." >}}

### Who Uses It?  

There are more people who use voice control than you’d think. If you’ve ever asked Siri to set a timer, congratulations! You’re a voice control user!

That being said, software like Voice Control, Dragon, and Talon are designed for more long-form, specialized use. [People who use these applications](https://tetralogical.com/blog/2021/11/15/browsing-with-speech-recognition/) may temporarily or permanently, and circumstantially or biologically be:

- Fully or partially paralyzed;
- Unable to use their hands;
- Unable to make fine motor movements;
- Unable to make repetitive movements over a long duration;
- Operating with lowered cognition.

Disability is also not a binary state, so it is entirely possible (and relatively common) that multiple disability conditions may be present at any given time.  

{{% ad-panel-leaderboard %}}

## Workarounds

Some voice control software has the functionality to work around this issue, the same way screen readers do. Dragon, for example, uses heuristics to identify links that contain the term “learn more.” It then lists a number for each link with that term, which you can then say “choose number” to activate.

{{< youtube id="Rfzxy8GZ524" caption="Partially visually hidden link names using Windows and Dragon Home" >}}

Most other voice control software allows you to [display numbers that map to all the interactive controls currently on the screen](https://thoughtbot.com/blog/an-introduction-to-macos-voice-control#navigating). If that doesn’t work, they can also display a grid and let you zoom into an area of the screen for precise selection and manipulation.

## The Question And The Choice

The larger question is why do we force people to do all this extra work? Partially visually hidden link text isn’t necessarily a hard WCAG failure, but it is also not a good user experience.

For macOS and iOS, you can only activate partially visually hidden link text if you know the other commands to work around the issue. That means it is a question of digital literacy: how familiar you are with this specialized software, as well as technology in general.

For voice control software that offers heuristics, the question is why do we force a disabled audience to expend more effort per link than an abled one? Remember that this interaction can happen multiple times per session, as well as nearly every time someone browses the web. It’s [a draining, exhausting experience](https://makeitfable.com/article/ive-had-enough-when-access-friction-becomes-an-access-barrier/).

When you learn about this, you need to make a choice: 

1. Do you keep honoring a misplaced sense of minimal aesthetics and keep the partially visually hidden text?
2. Or do you remove a burden for those affected by it and show the full link name to everyone?

One vital aspect of user experience is making things work for anyone, regardless of circumstance, device, or ability. Or, as [Billy Gregory](https://twitter.com/thebillygregory) puts it:

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">When UX doesn&#39;t consider ALL users, shouldn&#39;t it be known as &quot;SOME User Experience&quot; or... SUX? <a href="https://twitter.com/hashtag/a11y?src=hash&amp;ref_src=twsrc%5Etfw">#a11y</a></p>&mdash; Billy Gregory (@thebillygregory) <a href="https://twitter.com/thebillygregory/status/552466012713783297?ref_src=twsrc%5Etfw">January 6, 2015</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

## What About Truncated Text That Uses An Ellipses?

To quote [Karen McGrane](https://twitter.com/karenmcgrane), “Truncation is not a content strategy.” 

In addition to [embarrassing issues that can crop up by truncating text that is longer than its container](https://css-tricks.com/embracing-asymmetrical-design/), an interactive control that has part of its name obscured by ellipses can be hard or impossible to activate without using showing numbers/grid functionality. 

## What About My Unlabeled Icon Button?

Another example of this is a button that doesn’t have the benefit of any visible text. The more obscure the icon and abstract and minimal visual treatment it uses, the harder it can be to understand.

{{< youtube id="jMu39E4GRuc" caption="Using buttons without visible text labels with voice control" >}}

You might think this is a contrived example, but remember that tech and language literacy, jargon, and an aesthetic treatment can all conspire to prevent someone from knowing what an icon represents.

Again, voice control software offers workarounds for this. However, I repeat the question asked earlier: Why do we force people to use them?

## What About My Pixel-perfect Design?

Accessibility is a multidisciplinary, holistic concern. And so is Design. 

When you update your partially visually hidden link text, you may get link names that extend to more than one line. If the link is placed inside a card component, and there are multiple card components arranged in a grid, there is the chance that cards will have varying heights. And you know what? That’s totally okay. 

A CTA link extending to multiple lines is one example of the sorts of things you should already be considering. How your components can handle things like: 

- Varying lengths of content; 
- Grid placement and negative space with variable content height;
- Different configurations (What if a badge is added? What if the description is removed?);
- Translation and localization;
- Failure states (What if the hero image doesn’t load?).

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5f6b1202-b73a-45b5-b3ec-c8c28f4829c2/3-voice-control-usability-considerations-partially-visually-hidden-link-names.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5f6b1202-b73a-45b5-b3ec-c8c28f4829c2/3-voice-control-usability-considerations-partially-visually-hidden-link-names.jpg" width="800" height="474" sizes="100vw" caption=" (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5f6b1202-b73a-45b5-b3ec-c8c28f4829c2/3-voice-control-usability-considerations-partially-visually-hidden-link-names.jpg'>Large preview</a>)" alt="A wireframe card component showing 6 variations. There are varying lengths of content for the headline, description, and call to action links. Things like the hero photo and badges are also added and removed." >}}

If you need to update your existing work to accommodate these kinds of real-world considerations, you’ll probably have to collaborate with content writers, developers, and project managers. [Design thrives in this kind of collaborative environment](https://uxdesign.cc/design-is-about-facilitation-not-creation-c268e76ce1fd), where you can identify and work with the limits of the systems you work inside of.

Sometimes you’ll be able to tweak what you already have. Sometimes you’ll have to create net-new content. Sometimes you’ll even have to throw it all out and go back to the drawing board. These efforts all speak to the value of a [Shift Left methodology](https://applitools.com/blog/shifting-accessibility-testing-to-the-left/), where these kinds of considerations are named and dealt with early in the conception phase.

## How Do We Make Sure Our Experiences Are Easy To Use By Voice Control Software?

For interactive controls such as links and buttons, you’ll want to:

- Show the full text of the control’s name,
- Use a unique, accessible name for each control on the current page or view, 
- Avoid overriding accessible names with `aria-label`, and
- Avoid using just a cryptic or abstract icon &mdash; especially if the control’s functionality is exotic.

These steps will go a long way towards making using voice control software easier and more pleasant.  

{{% ad-panel-leaderboard %}}  

## It’s Not Really About Voice Control Software

The three overarching themes that I hope you’re picking up on:

1. Testing with a range of assistive technology is important to understanding actual support,
2. Agency can be granted by letting go of control, and 
3. Design decisions carry a tremendous amount of power.

Your designs need to be flexible and adaptable, as well as be able to accommodate the many different ways people can interact with them. This includes voice control, as well as numerous other forms of assistive technology.

### Further Reading On Smashing Magazine

- “[Everything You Want To Know About Creating Voice User Interfaces](https://www.smashingmagazine.com/2022/02/voice-user-interfaces-guide/),” Nick Babich & Gleb Kuznetsov 
- “[Equivalent Experiences: What Are They?](https://www.smashingmagazine.com/2020/05/equivalent-experiences-part1/),” Eric Bailey
- “[Making A Strong Case For Accessibility](https://www.smashingmagazine.com/2021/07/strong-case-for-accessibility/),” Todd Libby
- “[The Guide To Windows High Contrast Mode](https://www.smashingmagazine.com/2022/06/guide-windows-high-contrast-mode/),” Cristian Díaz
  
  {{< signature "nl" >}}