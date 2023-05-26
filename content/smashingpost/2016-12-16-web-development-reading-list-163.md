---
title: 'Web Development Reading List #163: The End-Of-Year Wrap-Up'
slug: web-development-reading-list-163
image: 'https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/309f9434-6b90-487f-bee3-66a6f6b8ff54/wdrl-163-opt.png'
date: 2016-12-16T22:27:36.000Z
author: anselm-hannemann
description: >-
  Only one week left until Christmas, and people already start freaking out
  again. No gifts purchased yet, work isn’t finished either, and suddenly some
  budget has to be spent until the end of the year. All of this **puts us under
  pressure**. To avoid the stress, I’ve seen a lot of people take a vacation
  from now until the end of the year — probably a good idea.

  And while it’s nice to see so many web advent calendars, I feel like **I’ve
  never written a longer reading list** than this one. So save this edition if
  you don’t have much time currently and read it during some calm moments later
  this year or early next year. Most articles are still worth reading in a few
  weeks.
categories:
  - Web Development Reading List
---
Only one week left until Christmas, and people already start freaking out again. No gifts purchased yet, work isn’t finished either, and suddenly some budget has to be spent until the end of the year. All of this <strong>puts us under pressure</strong>. To avoid the stress, I’ve seen a lot of people take a vacation from now until the end of the year — probably a good idea.

And while it’s nice to see so many web advent calendars, I feel like <strong>I’ve never written a longer reading list</strong> than this one. So save this edition if you don’t have much time currently and read it during some calm moments later this year or early next year. Most articles are still worth reading in a few weeks.</p>

### <span class="rh">Further Reading</span> on SmashingMag:

*   [The WAI Forward](https://www.smashingmagazine.com/2014/07/the-wai-forward/)
*   [You, Me And The Emoji: Character Sets, Encoding And Emoji](https://www.smashingmagazine.com/2016/11/character-sets-encoding-emoji/)
*   [GPU Animation: Doing It Right](https://www.smashingmagazine.com/2016/12/gpu-animation-doing-it-right/)
*   [A Beginner’s Guide To Progressive Web Apps](https://www.smashingmagazine.com/2016/08/a-beginners-guide-to-progressive-web-apps/)

## News

*   [Opera 42 (built upon Chromium 55) is out](https://dev.opera.com/blog/opera-42/) and comes with a built-in currency converter, support for Pointer Events, JavaScript async/await, and CSS `hyphens`. `document.write()` on the other hand, will [no longer load](https://developers.google.com/web/updates/2016/08/removing-document-write) over 2G connections.
*   The EU Parliament is now drafting a directive that [will force private sector companies to accommodate disabled people when offering their goods](https://qa-financial.com/testing/companies/eu-ready-set-laws-accessibility-testing/) and services. This means financial firms will need to comply with WCAG and other accessibility standards soon.
*   Firefox has introduced Telemetry a while ago to its browser and now shares [some details on what devices and hardware Firefox users use](https://metrics.mozilla.com/firefox-hardware-report/). In September 2016, for example, 10% still used Windows XP while only 7% used macOS and 77% of the users still have Flash installed. The most common screen resolutions are `1366x768px` and `1920x1080px`. There are many more really interesting statistics in there, and we’ll have to see how this develops over the next few years. But for us web developers, this also highlights that we shouldn’t assume that people use QuadCore CPU, 8GB RAM machines but have “lower-end” devices instead. So be aware of this before you create fancy CPU/memory-consuming web applications that a user will not have fun with.
*   [Samsung Internet browser 5.0 has been released](https://medium.com/samsung-internet-dev/announcing-samsung-internet-5-0-1ac2bfc14b78#.xl2j1qb4x). It has some interesting new technologies built in, such as content provider extensions, 360˚ video, a QR code reader, and a video assistant.

{{% feature-panel %}}

<figure><a href="https://metrics.mozilla.com/firefox-hardware-report/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/be1ae6b8-9644-46ec-b653-fb559d08aedd/firefox-hardware-report-opt.png" alt="Firefox Hardware Report" width="650" height="422" /><br>
</a><figcaption>The <a href="https://metrics.mozilla.com/firefox-hardware-report/">Firefox Hardware Report</a> gives insights into the hardware Firefox users are using. (Image credit: <a href="https://metrics.mozilla.com/firefox-hardware-report/">Firefox Hardware Report</a>)</figcaption></figure>

## Security

*   Mathias Karlsson shows how easy it is to [enable a `postMessage` XSS on your site by integrating a sharing button](https://labs.detectify.com/2016/12/15/postmessage-xss-on-a-million-sites/).</p>

## Privacy

*   A lot of us are using Disqus’ commenting system on their websites. It’s an easy way to add comments to your static website, but now Disqus announced that they need to lay off about 20% of their employees. But not only that, they will also [change their strategy towards data collection and advertising](https://techcrunch.com/2016/12/13/disqus-lays-off-11-as-it-plans-a-deeper-focus-on-data/). Specifically, they elaborate on displaying ads in comments, and there are speculations that they will try to sell (anonymized) user data to advertisers to help them tailor their ads more precisely to users. Maybe time to reconsider if you really want to use the service.
*   The Freedom of Press Foundation has [asked camera manufacturers to provide encryption methods](https://www.wired.com/2016/12/200-filmmakers-ask-nikon-canon-sell-encrypted-cameras/) for the stored data on the memory cards to help journalists in critical circumstances prevent leaks of their captured images.
*   According to a leaked draft, the new EPrivacy law of the European Union will [allow companies to do behavioral advertising based on user metadata](https://arstechnica.co.uk/tech-policy/2016/12/web-users-metadata-tracked-targeted-ads-leaked-draft-eu-law-reveals/).</p>

## Web Performance

*   Sergey Chikuyonok dives deep into the technical details of browsers and hardware to explain [how to get GPU animation right](https://www.smashingmagazine.com/2016/12/gpu-animation-doing-it-right/) and why it makes a big difference if we render animations on the CPU or on the GPU.
*   Steve Souders explains why [setting `async` on a script can cause various issues and how `defer` is different from that](https://calendar.perfplanet.com/2016/prefer-defer-over-async/). His conclusion: `defer` should be your default choice over `async`.</p>

## Accessibility

*   Covering unit tests and functional tests, [The Intern](https://theintern.github.io/) is a nice testing tool for JavaScript. But you can also [use The Intern for accessibility testing](https://www.sitepen.com/blog/2016/12/13/accessibility-testing-with-intern/), as Jason Cheatham explains in a recent article.
*   Chats are common these days, but how many of the web chats out there are accessible? Theodor Vararu shares [patterns for accessible web chats](https://accessibility.blog.gov.uk/2016/12/09/patterns-for-accessible-webchats/).

<figure><a href="https://www.sitepen.com/blog/2016/12/13/accessibility-testing-with-intern/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/47fbe407-5c37-46a4-adb0-2d1894544550/intern-accessibility-opt.png" alt="Intern Accessibility" width="650" height="363" /></a><figcaption>Jason Cheatham explains how you can <a href="https://www.sitepen.com/blog/2016/12/13/accessibility-testing-with-intern/">use the JavaScript testing tool The Intern for accessibility testing</a>. (Image credit: )</figcaption></figure>

## JavaScript

*   Todd Motto wrote a tutorial on how to [build a live calculator for a Tesla with Angular 2 reactive forms](https://toddmotto.com/building-tesla-range-calculator-angular-2-reactive-forms).
*   `[...'?‍?‍?'] // ["?", "‍", "?", "‍", "?"]` or `‘?‍?‍?’.length // 8` — do you wonder why that works? Stefan Judis found out and shares the technical details on [why the Emoji family works so well with JavaScript operations](https://www.contentful.com/blog/2016/12/06/unicode-javascript-and-the-emoji-family/) and how you even can dynamically generate the skin color of an [emoji](https://www.smashingmagazine.com/2016/11/character-sets-encoding-emoji/ "You, Me And The Emoji: Character Sets, Encoding And Emoji") with color codes and the unicode.
*   If you need to deal with different currency formats, it’s likely that some third-party library is in place. A [powerful tool that can handle most conversions really well is `toLocaleString`](https://remysharp.com/2016/12/13/format-numjsor-es6).
*   Paul Kinlan introduces the Web Share API, a solution that allows websites to [invoke the native sharing capabilities of the host platform](https://medium.com/dev-channel/introducing-the-web-share-api-40c69d93fe2a).
*   Max Stoibers explains how to use [stylelint](https://stylelint.io/) to [lint your CSS when writing them in JavaScript](https://mxstbr.blog/2016/12/linting-styles-in-js-with-stylelint/).

<figure><a href="https://www.contentful.com/blog/2016/12/06/unicode-javascript-and-the-emoji-family/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f320a3f0-03bd-40aa-8b76-683065cdc63b/emoji-prototype-opt.png" alt="Emoji.prototype.length — a tale of characters in Unicode" width="650" height="359" /></a><figcaption>We use emoji every day. But why do they work so well with JavaScript operations? Stefan Judis sheds some light into the dark. (Image credit: <a href="https://www.contentful.com/blog/2016/12/06/unicode-javascript-and-the-emoji-family/">Marko Skenderović</a>)</figcaption></figure>

## CSS/Sass

*   Harry Roberts shares why you shouldn’t write `background: black;` but be explicit with `background-color: black;`. The [shorthand syntax often unsets other properties that we never intended to modify](https://csswizardry.com/2016/12/css-shorthand-syntax-considered-an-anti-pattern/) and, thus, can cause unwanted side-effects.
*   Remy Sharp explains how to properly [build a close icon when using system fonts](https://remysharp.com/2016/12/10/in-the-detail-close-button). `x` is just wrong, so use `×` instead.</p>

## Work & Life

*   Cal Newport wrote about the concept of _Deep Work_ and [why it’s probably more efficient if you schedule your deep work in advance](https://calnewport.com/blog/2016/12/07/from-deep-tallies-to-deep-schedules-a-recent-change-to-my-deep-work-habits/) rather than just logging it on-the-go.
*   Working long hours doesn’t mean someone has a good “work ethic”. Instead, it just means working too much. Jason Fried on [what “work ethic” really is about](https://m.signalvnoise.com/work-ethic-e34bd63d2489).</p>

## Going Beyond…

*   Carole Cadwalladr discusses [the struggles of services like Google and Facebook between freedom of the press and promoting fake news](https://www.theguardian.com/commentisfree/2016/dec/11/google-frames-shapes-and-distorts-how-we-see-world). An interesting insight into how search results are influenced.
*   Sarah Jones on tech moguls that claim that they want to remake the world and why [they behaved as if they owe us no explanation for their decisions](https://newrepublic.com/article/139147/year-silicon-valley-went-morally-bankrupt) this year. A moral analysis of the startup culture.

<em>And with that, I’ll close for this week. If you like what I write each week, please <a href="https://wdrl.info/donate">support me with a donation</a> or share this resource with other people. You can learn more <a href="https://wdrl.info/costs/">about the costs of the project here</a>. It’s available via email, RSS and online.</em>

{{< signature "ah" >}}

