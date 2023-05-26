---
title: The Importance Of Manual Accessibility Testing
slug: importance-manual-accessibility-testing
author: eric-bailey
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ed4a4393-77a9-4703-9172-e9927b20334c/nutrition-cards-and-styled-form-controls-800w.png
date: 2018-09-12T13:30:55+02:00
summary: >-
  Automated accessibility tests are a great resource to have, but they can’t automatically make your site accessible. Use them as one step of a larger testing process.
description: >-
  Automated accessibility tests are a great resource to have, but they can’t automatically make your site accessible. Use them as one step of a larger testing process.
categories:
  - Accessibility
  - UX
  - Testing
---
Earlier this year, a man [drove his car into a lake](https://nymag.com/selectall/2018/01/waze-app-directs-driver-to-drive-car-into-lake-champlain.html) after following directions from a smartphone app that helps drivers navigate by issuing turn-by-turn directions. Unfortunately, the app’s programming did not include instructions to avoid roads that turn into boat launches.

From the perspective of the app, it did exactly what it was programmed to do, i.e. to find the most optimal route from point A to point B given the information made available to it. From the perspective of the man, it failed him by not taking the real world into account.

The same principle applies for accessibility testing.

<div class="c-felix-the-cat">
<h4 class="h3">Designing For Accessibility And Inclusion</h4>
<p>The more inclusive you are to the needs of your users, the more accessible your design is. Let’s take a closer look at the different lenses of accessibility through which you can refine your designs. <a href="https://www.smashingmagazine.com/2018/04/designing-accessibility-inclusion/" class="btn btn--medium btn--blue">Read a related article&nbsp;&rarr;</a></p>
</div>

## Automated Accessibility Testing

I am going to assume that you’re reading this article because you’re interested in learning how to test your websites and web apps to ensure they’re accessible. If you want to learn more about why accessibility is necessary, [the topic has been covered extensively](https://www.w3.org/WAI/fundamentals/accessibility-intro/) elsewhere.

Automated accessibility testing is a process where you use a series of scripts to test for the presence, or lack of certain conditions in code. These conditions are dictated by the [ Web Content Accessibility Guidelines (WCAG)](https://www.w3.org/TR/WCAG21/), a standard by the W3C that outlines how to make digital experiences accessible.

{{% feature-panel %}}

For example, an automated accessibility test might check to see if the `tabindex` attribute is present and if [its value is greater than](https://developer.paciellogroup.com/blog/2014/08/using-the-tabindex-attribute/) [`0`](https://developer.paciellogroup.com/blog/2014/08/using-the-tabindex-attribute/). The pseudocode would be something like:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8dc9a519-567b-49a5-823c-1d452f200e77/tabindex-flowchart.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8dc9a519-567b-49a5-823c-1d452f200e77/tabindex-flowchart.png" sizes="100vw" caption="" alt="A flowchart that asks if the tabindex value is present. If yes, it asks if the tabindex value is greater than 0. If it is greater than zero, it fails. If not, it passes. If no tabindex value is present, it also passes." >}}

Failures can then be collected and used to generate reports that disclose the number, and severity of accessibility issues. Certain automated accessibility products can also integrate as a [Continuous Integration](https://en.m.wikipedia.org/wiki/Continuous_integration) or [Continuous Deployment](https://en.m.wikipedia.org/wiki/Continuous_delivery) (CI/CD) tool, presenting just-in-time warnings to developers when they attempt to add code to a central repository.

These automated programs are incredible resources. Modern websites and web apps are complicated things that involve hundreds of states, thousands of lines of code, and complicated multi-screen interactions. It’d be absurd to expect a human (or a team of humans) to mind all the code controlling every possible permutation of the site, to say nothing of things like [regressions](https://en.m.wikipedia.org/wiki/Software_regression), [software rot](https://en.m.wikipedia.org/wiki/Software_rot), and [A/B tests](https://en.m.wikipedia.org/wiki/A/B_testing).

Automation really shines here. It can repeatedly and tirelessly pour over these details with perfect memory, at a rate far faster than any human is capable of.

## However...

Automated accessibility tests aren’t a turnkey solution, nor are they a silver bullet. There are some limitations to keep in mind when using them.

### Thinking To Think Of Things

One of both the best and worst aspects of the web is that there are many different ways to implement a solution to a problem. While this flexibility has kept the web robust and adaptable and ensured it outlived other competing technologies, it also means that you’ll sometimes see code that is, um, creatively implemented.

The test suite is only as good as what its author thought to check for. A naïve developer might only write tests for [the happy path](https://en.m.wikipedia.org/wiki/Happy_path), where everyone writes semantic HTML, fault-tolerant JavaScript, and well-scoped CSS. However, this is the real world. We need to acknowledge that things like tight deadlines, unfamiliarity with the programming language, [atypical user input](https://github.com/minimaxir/big-list-of-naughty-strings), and sketchy 3rd party scripts exist.

For example, [the automated accessibility testing site Tenon.io](https://tenon.io/) wisely includes a rule that checks to see if a form element has both a `label` element and an [`aria-label`](https://www.w3.org/TR/wai-aria/#aria-label) associated with it, and if the text strings for both declarations differ. If they do, it will flag it as an issue, as the visible label [may be different](https://www.w3.org/WAI/intro/usable) than what someone would hear if they were navigating using a screen reader.

If you’re not using a testing service that includes this rule, it won’t be reported. The code will still “pass”, but it’s passing by omission, not because it’s actually accessible.

### State

Some automated accessibility tests cannot parse the various states of interactive content. Critical parts of the user interface are effectively invisible to automation unless the test is run when the content is in an active, selected, or disabled state.

By interactive content, I mean things that the user has yet to take action on, or aren’t present when the page loads. Unopened modals, collapsed accordions, hidden tab content and carousel slides are all examples.

It takes sophisticated software to automatically test the various states of every component within a single screen, let alone across an entire web app or website. While it is possible to augment testing software with automated accessibility checks, it is very resource-intensive, usually requiring a dedicated team of engineers to set up and maintain.

### “Valid” Markup

[Accessible Rich Internet Applications (ARIA)](https://www.w3.org/WAI/standards-guidelines/aria/) is a set of attributes that extend HTML to allow it to describe interaction in a way that can be better understood by assistive technologies. For example, [the `aria-expanded` attribute](https://www.w3.org/TR/wai-aria/#aria-expanded) can be toggled by JavaScript to programmatically communicate if a component is in an expanded (`true`) or collapsed (`false`) state. This is superior to toggling a CSS class like `.is-expanded`, where [the update in state is only communicated visually](https://css-tricks.com/user-facing-state/).

Just having the presence of ARIA does not guarantee that it will automatically make something accessible. Unfortunately, and in spite of [its first rule of use](https://www.w3.org/TR/using-aria/#firstrule), ARIA is commonly misunderstood, and [consequently abused](https://twitter.com/vavroom/status/1014891718058151937). A lot of off-the-shelf code has this problem, perpetuating the issue.

For example, certain ARIA attributes and values [can only be applied to certain elements](https://www.w3.org/TR/html-aria/#docconformance). If incorrectly applied, assistive technology will ignore or misreport the declaration. Certain roles, known as [Abstract Roles](https://www.w3.org/TR/wai-aria-1.1/#abstract_roles), only exist to set up [the overall taxonomy](https://www.w3.org/TR/wai-aria-1.1/#state_prop_taxonomy) and should <strong>never</strong> be placed in markup.

<pre><code class="language-html">&lt;button role="command"&gt;Save&lt;/button&gt;

&lt;!-- Never do this --&gt;
</code></pre>

To further complicate the issue, [support for ARIA is varied across browsers](https://www.powermapper.com/tests/screen-readers/aria/). While an attribute may be used appropriately, the browser may not communicate the declared role, property, or state to assistive technology.

There is also the scenario where ARIA can be applied to an element and be valid from a technical standpoint, yet be unusable from an assistive technology perspective. For example:

<pre><code class="language-html">&lt;h1 aria-hidden="true"&gt;
  Tired of unevenly cooked asparagus? Try this tip from the world's oldest cookbook.
&lt;/h1&gt;
</code></pre>
<p><em>This one <a href="https://mtstandard.com/lifestyles/food-and-cooking/tired-of-unevenly-cooked-asparagus-try-this-tip-from-the/article_bb6ff21c-29ef-5774-a4eb-6b58599253b4.html">Weird Trick</a>.</em></p>

The  `aria-hidden` declaration will [remove the presence of content from assistive technology](https://developer.paciellogroup.com/blog/2012/05/html5-accessibility-chops-hidden-and-aria-hidden/), yet allow it to be still rendered visibly on the page. It’s a problematic pattern.

Headings &mdash; especially first-level headings &mdash; are vital in [communicating the purpose of a page](https://www.w3.org/WAI/tutorials/page-structure/headings/). If a person is using assistive technology to navigate, the `aria-hidden` declaration applied to the `h1` element will make it difficult for them to quickly determine the page’s purpose. It will force them to navigate around the rest of the page to gain context, an annoying and labor-intensive process.

Some automated accessibility tests may scan the code and not report an error since the syntax itself is valid. The automation has no way of knowing the greater context of the declaration’s use.

This isn’t to say you should completely avoid using ARIA! When [authored with care and deliberation](https://css-tricks.com/aria-spackle-not-rebar/), ARIA can fix the gaps in accessibility that sometimes plague complicated interactions; it provides some much-needed context to the people who rely on assistive technology.

{{% ad-panel-leaderboard %}}

## Much-Needed Context

As the soggy car demonstrates, computers are awful at understanding the overall situation of the outside world. It’s up to us humans to be the ultimate arbiters in determining if what the computer spits out is useful or not.

### Debunking

Before we discuss how to provide appropriate context, there are a few common misunderstandings about accessibility work that need to be addressed:

First, not all screen reader users are blind. In addition to all the points Adrian Roselli [outlines in his post](https://adrianroselli.com/2017/02/not-all-screen-reader-users-are-blind.html), some food for thought: [the use of voice assistants is on the rise](https://www.pewresearch.org/fact-tank/2017/12/12/nearly-half-of-americans-use-digital-voice-assistants-mostly-on-their-smartphones/). When’s the last time you spoke to Siri or Alexa?

Second, accessibility is more than just screen readers. The rules outlined in the [Web Content Accessibility Guidelines](https://www.w3.org/WAI/standards-guidelines/wcag/) ensure that the largest number of people can read and operate technology, regardless of ability or circumstance.

For example, the rule that stipulates [a website or web app needs to be able to work regardless of device orientation](https://www.w3.org/WAI/WCAG21/Understanding/orientation.html) benefits everyone. Some people may need to mount their device in a fixed location in a specific orientation, such as in landscape mode on the arm of a wheelchair. Others might want to lie in bed and watch a movie, or better investigate a product photo ([pinch and pull zooming](https://www.w3.org/TR/UNDERSTANDING-WCAG20/visual-audio-contrast-scale.html) will also be helpful to have here).

Third, disabilities [can be conditional](https://uxmag.com/articles/we-re-just-temporarily-abled) and can be brought about by your environment. It can be a short-term thing, like rain on your glasses, sleep deprivation, or an allergies-induced migraine. It can also be longer-term, such as a debilitating illness, broken limb, or a depressive episode. Multiple, compounding conditions can (and do) affect individuals.

That all being said, many accessibility fixes that help screen readers work properly also benefit other assistive technologies.

### Get Your Feet Wet

Knowing where to begin can be overwhelming. Consider [Zoë Bijl](https://twitter.com/ZoeBijl/status/520946983700541441)’s great advice:

<blockquote>“Before you release a website, tab through it. If you cannot see where you are on the page after each tab; you&#39;re not finished yet. <a href="https://twitter.com/hashtag/a11y?src=hash&amp;ref_src=twsrc%5Etfw">#a11y</a></blockquote>

[Tab through](https://www.smashingmagazine.com/2018/07/web-with-just-a-keyboard/) a few of the main [user flows](https://uxdesign.cc/the-biggest-wtf-in-design-right-now-87139f367d66) on your website or web app to determine if all interactive components’ [focus states are visually apparent](https://css-tricks.com/focusing-on-focus-styles/), and if they can be activated via keyboard input. If there’s something you can click or tap on that isn’t getting highlighted when receiving keyboard focus, take note of it. Also pay attention to the order interactive components are highlighted when focused &mdash; it should match the reading order of the site.

An obvious focus state and logical tab order go a great way to helping make your site accessible. These two features benefit [a wide variety of assistive technology](https://webaim.org/articles/motor/assistive), including, [but not limited to](https://www.youtube.com/watch?v=ImlKOA1MhlI), screen readers.

If you need a baseline to compare your testing to, Dave Rupert has an excellent project called [A11Y Nutrition Cards](https://davatron5000.github.io/a11y-nutrition-cards/), which outlines expected behavior for common interactive components. In addition, Scott O'Hara maintains a project called [a11y Styled Form Controls](https://scottaohara.github.io/a11y_styled_form_controls/). This project provides examples of components such as switches, checkboxes, and radio buttons that have well-tested and documented support for assistive technology. A clever reader might use one of these resources to help them try out the other!

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/43da18aa-bbd8-46f3-a83d-cc0ffbd37914/nutrition-cards-and-styled-form-controls.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/43da18aa-bbd8-46f3-a83d-cc0ffbd37914/nutrition-cards-and-styled-form-controls.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/43da18aa-bbd8-46f3-a83d-cc0ffbd37914/nutrition-cards-and-styled-form-controls.png'>Large preview</a>)" alt="A screenshot of homepage for the a11y Styled Form Controls website placed over a screenshot of the Nutrition Cards for Accessible Components website." >}}

### The Fourth Myth

With that out of the way, I’m going to share a fourth myth with you: not every assistive technology user is a power user. Like with any other piece of software, there’s a learning curve involved.

In her post about [Aaptiv’s redesign](https://medium.com/aaptiv-engineering/lessons-in-ios-voiceover-accessibility-834c5ed9a374), Lisa Zhu discovers that their initial accessibility fix wasn’t intuitive. While their first implementation was “technically” correct, it didn’t line up with how people who rely on VoiceOver actually use their devices. A second solution simplified the interaction to better align with their expectations.

Don’t assume that just because something hypothetically functions that it’s actually usable. Trust your gut: if it feels especially awkward, cumbersome, or tedious to operate for you, chances are it’ll be for others.

### Dive Right In

While not every accessibility issue is a screen reader issue, you should still get in the habit of testing your site with one. Not an emulator, simulator, or some other proxy solution.

If you find yourself struggling to operate a complicated interactive component using [basic screen reader commands](https://developer.paciellogroup.com/blog/2015/01/basic-screen-reader-commands-for-accessibility-testing/), it’s probably a sign that the component needs to be simplified. Chances are that the simplification will help non-assistive technology users as well. Good design benefits everyone!

The same goes for navigation. If it’s difficult to move around the website or web app, it’s probably a sign that you need to update your [heading structure](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/Heading_Elements#Accessibility_concerns) and [landmark roles](https://www.scottohara.me/blog/2018/03/03/landmarks.html). Both of these features are used by assistive technology to quickly and efficiently navigate.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e86e65a5-74d6-4f89-98a5-11cb21ec3f12/sidebar-markup.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e86e65a5-74d6-4f89-98a5-11cb21ec3f12/sidebar-markup.png" sizes="100vw" caption="Both of these are sidebars, but only one of them is semantically described as such. A computer doesn't know what a sidebar is, so it's up to you to tell it." alt="Two code examples for a sidebar. One uses a div element, while the others uses an aside element. Both have the class of sidebar applied to them, with a subheading of Recent Posts." >}}

Another good thing to review is the text content used to describe your links. Hopping from link to link is another common assistive technology navigation technique; some screen readers can even generate a list of all link content on the page:

<blockquote>“Think before you link! Your &quot;helpful&quot; click here links look like this to a screen reader user. ALT = JAWS links list”<br /><figure><a href="https://twitter.com/NeilMilliken/status/1004590832559841280?ref_src=twsrc%5Etfw"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4d8f2774-e31a-4cb0-8d83-218294973918/27-links-nils-milliken-tweet.jpg" width="329" height="442" alt="Tweet by Neil Milliken" /></a></figure><br /><br />&mdash; <a href="https://twitter.com/NeilMilliken/status/1004590832559841280?ref_src=twsrc%5Etfw">Neil Milliken</a></blockquote>

When navigating using an ordered list devoid of the surrounding non-link content, avoiding ambiguous terms like “click here” or “more info” can go a long way to ensuring a person can understand the overall meaning of the page. As a bonus, it’ll help alleviate cognitive concerns for everyone, as you are more accurately explaining [what a user should expect after activating a link](https://medium.com/@heyoka/dont-use-click-here-f32f445d1021).

{{% ad-panel-leaderboard %}}

## How To Test

Each screen reader has a different approach to how it announces content. This is intentional. It’s a balancing act between the product’s features, the operating system it is installed on, the form factor it is available in, and the types of input it can receive.

[The Browser Wars](https://en.m.wikipedia.org/wiki/Browser_wars) taught us the folly of developing for only one browser. Similarly, we should not cater to a single screen reader. It is important to note that many people rely exclusively on a specific screen reader and browser combination &mdash; by circumstance, preference, or necessity’making this all the more important. However, there is a caveat: each screen reader works better when used with a specific browser, typically the one that allows it access to the greatest amount of [accessibility API](https://www.smashingmagazine.com/2015/03/web-accessibility-with-accessibility-api/) information.

<strong>All of these screen readers can be used for free</strong>, provided you have the hardware. You can also virtualize that hardware, either [for free](https://developer.microsoft.com/en-us/windows/downloads/virtual-machines) or [on the cheap](https://www.24a11y.com/2017/build-cloud-hosted-accessibility-testing-windows-computer-using-amazon-workspaces/).

### Automate

Automated accessibility tests should be your first line of defense. They will help you catch a great deal of nitpicky, easily-preventable errors before they get committed. Repeated errors may also signal problems in template logic, where one upstream tweak can fix multiple pages. Identifying and resolving these issues allows you to spend your valuable manual testing time much more wisely.

It may also be helpful to log accessibility issues in a place where people can collaborate, such as Google Sheets. Quantifying the frequency and severity of errors can lead to good things like updated documentation, opportunities for lunch and learn education, and other healthy changes to organizational workflow.

Much like manual testing with a variety of screen readers, it is recommended that you [use a combination of automated tools](https://medium.com/pulsar/which-accessibility-testing-tool-should-you-use-e5990e6ef0a) to prevent gaps.

### Windows

The two most popular screen readers on Windows are JAWS and NVDA.

#### JAWS

[JAWS (Job Access With Speech)](https://www.freedomscientific.com/Products/Blindness/JAWS) is the most popular and [feature-rich](https://doccenter.freedomscientific.com/doccenter/doccenter/rs25c51746a0cc/2014-09-24_enhancedconvenientocrandsemi-autoformsmode/02_ConvenientOCR.htm) screen reader on the market. It works best with Firefox and Chrome, with concessions for supporting Internet Explorer. Although it is pay software, it can be operated in full in demo mode for 40 minutes at a time (this should be more than sufficient to perform basic testing).

#### NVDA

[NVDA (NonVisual Desktop Access)](https://www.nvaccess.org/) is free, although [a donation](https://www.nvaccess.org/support-us/#donation-support) is strongly encouraged. It is a feature-rich alternative to JAWS. It works best with Firefox.

#### Narrator

Windows comes bundled with a built-in screen reader called [Narrator](https://support.microsoft.com/en-us/help/22798/windows-10-narrator-get-started). It works well with Edge, but has difficulty interfacing with other browsers.

### Apple

#### macOS

[VoiceOver](https://help.apple.com/voiceover/info/guide/10.13/) is a powerful screen reader that comes bundled with macOS. Use it in conjunction with Safari, first making sure that [full keyboard access](https://a11yproject.com/posts/safari-keyboard-navigation/) is enabled.

#### iOS

VoiceOver is also [included in iOS](https://help.apple.com/iphone/10/#/iph3e2e415f), and is the most popular mobile screen reader. Much like its desktop counterpart, it works best with Safari. An interesting note here is that according to the 2017 WebAIM screen reader survey, a not-insignificant amount of respondents [augment their phone with external hardware keyboards](https://webaim.org/projects/screenreadersurvey7/#mobilekeyboard).

### Android

Google recently folded [TalkBack](https://support.google.com/accessibility/android/answer/6283677?hl=en&ref_topic=3529932), their mobile screen reader, into a larger collection of accessibility services called the [Android Accessibility Suite](https://play.google.com/store/apps/details?id=com.google.android.marvin.talkback&hl=en_US). It works best with Mobile Chrome. While many Android apps are notoriously inaccessible, it is still worth testing on this platform. Android’s [growing presence in emerging markets](https://qz.com/986042/google-goog-designed-android-go-to-win-over-the-next-billion-smartphone-users-in-the-developing-world/), as well as increasing internet use amongst [elderly](https://www.pewinternet.org/2017/05/17/tech-adoption-climbs-among-older-adults/) and [lower-income](https://www.pewresearch.org/fact-tank/2017/03/22/digital-divide-persists-even-as-lower-income-americans-make-gains-in-tech-adoption/) demographics, should give pause for consideration.

<table class="tablesaw break-out" data-tablesaw-mode="swipe" data-tablesaw-minimap>
  <caption>Popular screen readers</caption>
  <thead>
    <tr>
      <th scope="col">Screen Reader</th>
      <th scope="col">Platform</th>
      <th scope="col">Preferred Browser(s)</th>
      <th scope="col">Manual</th>
      <th scope="col">Launch</th>
      <th scope="col">Quit</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td scope="row"><a href="https://www.freedomscientific.com/Products/Blindness/JAWS">JAWS</a></td>
      <td>Windows</td>
      <td>Chrome, Firefox</td>
      <td><a href="https://www.freedomscientific.com/products/blindness/jawsdocumentation">JAWS 2018 Documentation</a></td>
      <td>Launch JAWS as you would any other Windows application</td>
      <td><kbd>Insert</kbd> + <kbd>F4</kbd></td>
    </tr>
    <tr>
      <td scope="row"><a href="https://www.nvaccess.org/">NVDA</a></td>
      <td>Windows</td>
      <td>Firefox</td>
      <td><a href="https://www.nvaccess.org/files/nvda/documentation/userGuide.html">NVDA 2018.2.1 User Guide</a></td>
      <td><kbd>Ctrl</kbd> + <kbd>Alt</kbd> + <kbd>N</kbd></td>
      <td><kbd>Insert</kbd> + <kbd>Q</kbd></td>
    </tr>
    <tr>
      <td scope="row"><a href="https://support.microsoft.com/en-us/help/22798/windows-10-narrator-get-started">Narrator</a></td>
      <td>Windows</td>
      <td>Edge</td>
      <td><a href="https://support.microsoft.com/en-us/help/22798/windows-10-narrator-get-started">Get started with Narrator</a></td>
      <td><kbd>Windows key</kbd> + <kbd>Control</kbd> + <kbd>Enter</kbd></td>
      <td><kbd>Windows key</kbd> + <kbd>Control</kbd> + <kbd>Enter</kbd></td>
    </tr>
    <tr>
      <td scope="row"><a href="https://www.apple.com/accessibility/mac/vision/">VoiceOver</a></td>
      <td>macOS</td>
      <td>Safari</td>
      <td><a href="https://help.apple.com/iphone/11/#/iph3e2e415f">VoiceOver Getting Started Guide</a></td>
      <td><kbd>Command</kbd> + <kbd>F5</kbd> or tap <a href="https://support.apple.com/en-us/HT207054">the Touch ID button</a> 3 times</td>
      <td><kbd>Command</kbd> + <kbd>F5</kbd> or tap <a href="https://support.apple.com/en-us/HT207054">the Touch ID button</a> 3 times</td>
    </tr>
    <tr>
      <td scope="row"><a href="https://www.apple.com/accessibility/iphone/vision/">Mobile VoiceOver</a></td>
      <td>iOS</td>
      <td>Mobile Safari</td>
      <td><a href="https://help.apple.com/iphone/11/#/iph3e2e415f">VoiceOver overview - iPhone User Guide</a></td>
      <td>Tell Siri to, “Turn on VoiceOver.” or <a href="https://help.apple.com/iphone/11/#/iph3e2e2329">activate in Settings</a></td>
      <td>Tell Siri to, “Turn off VoiceOver.” or <a href="https://help.apple.com/iphone/11/#/iph3e2e2329">deactivate in Settings</a></td>
    </tr>
    <tr>
      <td scope="row"><a href="https://play.google.com/store/apps/details?id=com.google.android.marvin.talkback">Android Accessibility Suite</a></td>
      <td>Android</td>
      <td>Mobile Chrome</td>
      <td><a href="https://support.google.com/accessibility/android/answer/6283677?hl=en&ref_topic=3529932">Get started on Android with TalkBack</a></td>
      <td>Press both volume keys for 3 seconds</td>
      <td>Press both volume keys for 3 seconds</td>
    </tr>
  </tbody>
</table>

### Call The Professionals

If you do not require the use of assistive technology on a frequent basis then [you do not fully understand](https://yetanotherlefty.wordpress.com/2017/05/01/what-non-disabled-people-get-wrong-about-accessibility/) how the people who do interact with the web.

Much like traditional user testing, being too close to the thing you created may cloud your judgment. [Empathy exercises](https://medium.com/@acuity_design/empathy-exercises-dont-work-b984dacc8fd6) are a good way to become aware of the problem space, but you should not use yourself as a litmus test for whether the entire experience is truly accessible. <strong>You are not the expert</strong>.

If your product serves a huge population of users, if its core base of users trends towards having a higher probability of disability conditions (specialized product, elderly populations, foreign language speakers, etc.), and/or if it is [required to be compliant by law](https://axesslab.com/web-accessibility-directive/), I would strongly encourage allocating a portion of your budget for testing by people with disabilities.

<blockquote>“At what point does your organisation stop supporting a browser in terms of % usage? 18% of the global pop. have an <a href="https://twitter.com/hashtag/Accessibility?src=hash&amp;ref_src=twsrc%5Etfw">#Accessibility</a> requirement, 2% people have a colour vision deficient. But you consider 2% IE usage support more important? Support everyone be inclusive.”<br /><br />&mdash; <a href="https://twitter.com/MarkAWilcock/status/1000791354975440896?ref_src=twsrc%5Etfw">Mark Wilcock</a></blockquote>

This isn’t to say you should completely delegate the responsibility to these testers. Much as how automated accessibility testing can detect smaller issues to remove, a first round of basic manual testing helps professional testers focus their efforts on the complicated interactions you need an expert’s opinion on. In addition to optimizing the value of their time, it helps to get you more comfortable triaging. It is also a professional courtesy, plain and simple.

There are a few companies that perform manual testing by people with disabilities:

- [Accessible360](https://accessible360.com/)
- [Perkins School For The Blind](https://www.perkins.org/solutions/assessments-training)
- [AccessWorks](https://access-works.com/) (by Knowbility)
- [Fable Tech Labs](https://www.makeitfable.com/)

## Designed Experiences

We also need to acknowledge the other large barrier to accessible sites that can’t be automated away: poor user experience.

User experience can make or break a product. Your code can compile perfectly, your time to first paint can be lightning quick, and your Webpack setup can be beyond reproach. All this is irrelevant if [the end result is unusable](https://ethanmarcotte.com/wrote/accessibility-is-not-a-feature/). User experience encompasses all users, including those who navigate with the aid of assistive technology.

If a person cannot operate your website or web app, they’ll abandon it and not think twice. If they are forced to use your site to get a service unavailable by other means, there’s [a growing precedent for taking legal action](https://www.lflegal.com/2017/06/winn-dixie/) (and rightly so).

As a discipline, user experience can be roughly divided into two parts: how something <strong>looks</strong> and how it <strong>behaves</strong> They’re intrinsically interlinked concepts &mdash; work on either may affect both. While accessible design is a topic unto itself, there are some big-picture things we can keep in mind when approaching accessible user experiences from a testing perspective:

### How It Looks

The WCAG does a great job covering a lot of [the basics of good design](https://uxdesign.cc/designing-for-accessibility-is-not-that-hard-c04cc4779d94). Color contrast, font size, user-facing state: a lot of these things can be targeted by automation. What you should pay attention to is all the atomic, difficult to quantify bits that compound to create your designs. Things like the [words you choose](https://www.nngroup.com/articles/writing-for-lower-literacy-users/), the fonts you use to display them, the spacing between things, [affordances for interaction](https://en.m.wikipedia.org/wiki/Affordance), the way you handle your breakpoints, etc.

<blockquote>“A good font should tell you:<br />the difference between m and rn<br />the difference between I and l<br />the difference between O and 0.”<br /><br />&mdash; <a href="https://twitter.com/stommepoes/status/506707772181061633?ref_src=twsrc%5Etfw">mallory, alice &amp; bob</a></blockquote>

It’s one of those “[an ounce of prevention is worth a pound of cure](https://www.deque.com/blog/design-code-thinking-accessibility-ground/)” situations. Smart, accessible defaults can save countless time and money down the line. Lean and mean startups all the way up to multinational conglomerates value efficient use of resources, and this is one of those places where you can really capitalize on that. Put your basic design patterns &mdash; say collected in something like a mood board or living style guide &mdash; in front of people early and often to see if your designed intent is clear.

### How It Behaves

An enticing color palette and collection of thoughtfully-curated stock photography only go so far. Eventually, you’re going to have to synthesize all your design decisions to create something that addresses a need.

Behavior can be as small as a [microinteraction](https://microinteractions.com/what-is-a-microinteraction/), or as large as finding a product and purchasing it. What’s important here is to make sure that all the barriers to a person trying to accomplish the task at hand are removed.

If you’re using personas, don’t create a separate persona for a user with a disability. Instead, [blend accessibility considerations](https://webdesign.tutsplus.com/articles/making-the-web-accessible-for-everyone-with-inclusive-design-and-diverse-personas--cms-27505) into your existing ones. As a persona is an abstracted representation of the types of users you want to cater to, you want to make sure the kinds of conditions they may be experiencing are included. Disability conditions aren’t limited to just physical impairments, either. Things like a metered data plan, non-native language, or [anxiety](https://developer.paciellogroup.com/blog/2018/08/a-web-of-anxiety-accessibility-for-people-with-anxiety-and-panic-disorders-part-1/) are all worth integrating.

<blockquote>“When looking at your site&#39;s analytics, remember that if you don&#39;t see many users on lower end phones or from more remote areas, it&#39;s not because they aren&#39;t a target for your product or service. It is because your mobile experience sucks.<br />As a developer, it&#39;s your job to fix it.”<br /><br />&mdash; <a href="https://twitter.com/estellevw/status/1027305654501826560?ref_src=twsrc%5Etfw">Estelle Weyl</a></blockquote>

User testing, ideally simulating conditions as close to what a person would be doing in the real world (including their individual device preferences and presence of assistive technology), is also key. Verifying that people are actually able to make the logical leaps necessary to operate your interface addresses a lot of [cognitive concerns](https://webaim.org/articles/cognitive/), a difficult-to-quantify yet vital thing to accommodate.

## We Shape Our Tools, Our Tools Shape Us

Our tool use corresponds to the kind of work we do: Carpenters drive nails with hammers, chefs cook using skillets, surgeons cut with scalpels. It’s a self-reinforcing phenomenon, and it tends to lead to over-categorization.

Sometimes this over-categorization gets in the way of us remembering to consider the real world. A surgeon might have a carpentry hobby; a chef might be a retired veterinarian. It’s important to understand that [accessibility is everyone’s responsibility](https://abookapart.com/products/accessibility-for-everyone), and there are many paths to making our websites and web apps the best they can be for everyone. To [paraphrase Mikey Ilagan](https://twitter.com/mikeyil/status/979180468556980224), accessibility is a holistic practice, essential to some but useful to all.

Used with discretion, ARIA is a very good tool to have at our disposal. We shouldn’t shy away from using it, provided we understand the <strong>how</strong> and <strong>why</strong> behind why they work.

The same goes for automated accessibility tests, as well as GPS apps. They’re great tools to have, just get to know the terrain a little bit first.

## Resources

### Automated Accessibility Tools

- [aXe](https://www.deque.com/axe/) (Chrome and Firefox, powers [Chrome DevTools' Lighthouse](https://developers.google.com/web/tools/lighthouse/))
- [SiteImprove Accessibility Checker](https://siteimprove.com/en-us/company/press/2017/siteimprove-launches-free-google-chrome-accessibility-checker/) (Chrome)
- [Tenon](https://tenon.io/) (Browser)
- [WAVE Web Accessibility Evaluation Tool](https://wave.webaim.org/extension/) (Chrome and Firefox)

### Professional Services

- [Deque](https://www.deque.com/)
- [Knowbility](https://knowbility.org/)
- [Level Access](https://www.levelaccess.com/)
- [The Paciello Group](https://www.paciellogroup.com/)
- [Tenon](https://tenon.io/)
- [WebAIM](https://webaim.org/)

### References

- [The A11Y Project](https://a11yproject.com/)
- [ADG* - Accessibility Developer Guide](https://www.accessibility-developer-guide.com/)
- [Inclusive Design Principles](https://inclusivedesignprinciples.org/)
- “[Accessibility for Teams](https://accessibility.digital.gov/),” Digital.gov
- “[Involving Users in Evaluating Web Accessibility](https://www.w3.org/WAI/test-evaluate/involving-users/),” Web Accessibility Initiative (WAI)
- “[WAI-ARIA Overview](https://www.w3.org/WAI/standards-guidelines/aria/),” Web Accessibility Initiative (WAI)
- “[Using ARIA](https://www.w3.org/TR/aria-in-html/),” W3C Working Draft

### Quick Tests

- “[5 Accessibility Tests You Can Do In 5 minutes](https://openinclusion.com/blog/5-accessibility-tests/),” Open Inclusion
- “[The 6 Simplest Web Accessibility Tests Anyone Can Do](https://www.karlgroves.com/2013/09/05/the-6-simplest-web-accessibility-tests-anyone-can-do/),” Karl Groves
- “[Basic Screen Reader Commands For Accessibility Testing](https://developer.paciellogroup.com/blog/2015/01/basic-screen-reader-commands-for-accessibility-testing/),” The Paciello Group
- “[Easy Checks - A First Review Of Web Accessibility](https://www.w3.org/WAI/test-evaluate/preliminary/),” Web Accessibility Initiative (WAI)
- “[Handling Common Accessibility Problems](https://developer.mozilla.org/en-US/docs/Learn/Tools_and_testing/Cross_browser_testing/Accessibility),” MDN Web Docs

### Further Reading

- “[7 Things Every Designer Needs To Know About Accessibility](https://medium.com/salesforce-ux/7-things-every-designer-needs-to-know-about-accessibility-64f105f0881b),” Jesse Hausler, Medium
- “[Accessibility In User-Centered Design: Usability Testing](https://www.uiaccess.com/accessucd/ut.html),” Shawn Lawton Henry, uiAccess
- “[Accessibility Testing On A $7 Budget](https://medium.com/@claudioluisvera/testing-for-accessibility-on-a-7-budget-4cb05a787b4f),” Claudio Luís Vera, Medium
- “[Designing For Accessibility And Inclusion](https://www.smashingmagazine.com/2018/04/designing-accessibility-inclusion/),” Steven Lambert, Smashing Magazine
- “[Efficiency In Accessibility Testing Or, Why Usability Testing Should Be Last](https://www.karlgroves.com/2012/04/27/efficiency-in-accessibility-testing-or-why-usability-testing-should-be-last/),” Karl Groves
- “[Firefox Accessibility Inspector](https://developer.mozilla.org/en-US/docs/Tools/Accessibility_inspector),” MDN Web Docs
- “[Get Started With Accessibility: A Primer Based On Experience](https://www.susanjeanrobertson.com/writing/get-started-with-accessibility/),” Susan Jean Robertson
- “[Getting Comfortable With WCAG](https://seesparkbox.com/foundry/getting_comfortable_with_wcag),” Sparkbox
- “[I Used The Web For A Day With Just A Keyboard](https://www.smashingmagazine.com/2018/07/web-with-just-a-keyboard/),” Chris Ashton, Smashing Magazine
- “[Practical Examples Of Accessibility Improvements](https://axesslab.com/practical-accessibility-improvements/),” Axess Lab
- “[Testing For Accessibility](https://www.gov.uk/service-manual/technology/testing-for-accessibility),” Service Manual, GOV.UK
- “[Stop Designing For Only 85% Of Users: Nailing Accessibility In Design](https://www.smashingmagazine.com/2017/10/nailing-accessibility-design/),” Tom Graham &amp; André Gonçalves, Smashing Magazine
- “[Structural Semantics: The Importance Of HTML5 Sectioning Elements](https://www.smashingmagazine.com/2013/01/the-importance-of-sections/),” Heydon Pickering, Smashing Magazine
- “[The WAI Forward](https://www.smashingmagazine.com/2014/07/the-wai-forward/),” Heydon Pickering, Smashing Magazine
- “[The Web Is Made Of Edge Cases](https://codepen.io/tigt/post/the-web-is-made-of-edge-cases),” Taylor Hunt, CodePen
- “[What We Found When We Tested Tools On The World’s Least-Accessible Webpage](https://accessibility.blog.gov.uk/2017/02/24/what-we-found-when-we-tested-tools-on-the-worlds-least-accessible-webpage/),” Mehmet Duran, GOV.UK

{{< signature "rb, ra, yk, il" >}}