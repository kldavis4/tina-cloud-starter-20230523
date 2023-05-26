---
title: >-
  Web Development Reading List #147: Security Guidelines, Accessible UI
  Components, And Content-First Design
slug: web-development-reading-list-147
image: 'https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/504b3208-d8ec-4f46-8127-cfa1978f762e/wdrl-147-opt.png'
date: 2016-07-29T20:54:00.000Z
author: anselm-hannemann
description: >-
  When working in a team, it’s important to stick to rules. A common challenge
  is to build all your projects with a similar or the same toolset and **coding
  guidelines**. Only yesterday I discussed how we could port over a project that
  outgrew its initial codebase over the years to a fresh, React.js-based source
  code.

  The decision for this wasn’t easy, since we had invested quite a lot of work
  and money into this project already, and a move to React would require quite
  some time, too. But since the switch makes sense from a technical perspective
  and the team is already using React for three other projects, we concluded
  that this would be a good step to do. It will enable more developers of the
  team to contribute to the project, to review code and to reduce the shift of
  technologies in the company. Occasionally, it’s time to re-evaluate your
  projects and move on.
categories:
  - Web Development Reading List
---
When working in a team, it’s important to stick to rules. A common challenge is to build all your projects with a similar or the same toolset and <strong>coding guidelines</strong>. Only yesterday I discussed how we could port over a project that outgrew its initial codebase over the years to a fresh, React.js-based source code.

The decision for this wasn’t easy, since we had invested quite a lot of work and money into this project already, and a move to React would require quite some time, too. But since the switch makes sense from a technical perspective and the team is already using React for three other projects, we concluded that this would be a good step to do. It will enable more developers of the team to contribute to the project, to review code and to reduce the shift of technologies in the company. Occasionally, it’s time to re-evaluate your projects and move on.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [It’s Time To Start Using CSS Custom Properties](https://www.smashingmagazine.com/2017/04/start-using-css-custom-properties/)
*   [Houdini: Maybe The Most Exciting Development In CSS](https://www.smashingmagazine.com/2016/03/houdini-maybe-the-most-exciting-development-in-css-youve-never-heard-of/)
*   [How To Scale React Applications](https://www.smashingmagazine.com/2016/09/how-to-scale-react-applications/)
*   [Truly Fluid Typography With vh And vw Units](https://www.smashingmagazine.com/2016/05/fluid-typography/)

## News

*   [Bootstrap 4 Alpha 3](https://blog.getbootstrap.com/2016/07/27/bootstrap-4-alpha-3/) has been released this week. It comes with an overhauled grid, updated form controls, a system font stack, and more.
*   Microsoft announced that their JavaScript engine [ChakraCore](https://github.com/Microsoft/ChakraCore) now supports Mac OS and Linux. This means, you can now test and run your Node.js applications not only in Google’s V8 engine. Christian Heilmann wrote up [why this is an important step](https://www.christianheilmann.com/2016/07/27/why-chakracore-matters/).

{{% feature-panel %}}

<figure><a href="https://github.com/Microsoft/ChakraCore"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ef0d0e4d-c65d-42be-89d4-a6b83911d17a/chakra-core-opt.png" alt="ChakraCore" width="500" height="232" /></a><figcaption>Good news for Mac and Linux users: <a href="https://github.com/Microsoft/ChakraCore">ChakraCore is finally supported</a>. (Image credit: <a href="https://www.christianheilmann.com/2016/07/27/why-chakracore-matters/">Christian Heilmann</a>)</figcaption></figure>

## Concept & Design

*   “[Web Design in 4 minutes](https://jgthms.com/web-design-in-4-minutes/)” is a very concise article on why content-first matters.</p>

## Tools & Workflows

*   If you work on small projects, an (S)FTP-client can still be very useful. But on the other hand, it means you need to manually copy files from your git workflow to the server. To solve this issue, the indie developer Jan Östlund built [GitFTP-Deploy](https://eastwest.se/apps/gitftpdeploy), a handy (S)FTP tool for a small fee that does automatic deployments based on your git workflow.
*   The privacy/tracking issue is bigger than we think. Have you ever monitored which apps connect to which service? You suddenly realize that an ad blocker/privacy add-on in your browser is only a drop in the bucket. Apps often connect to Google services, Google Analytics, sometimes to various ad networks, and very often to New Relic’s user tracking service. Fortunately, there’s a solution to nearly every problem: Add tracker hostnames to your `/etc/hosts` file. There’s even [a public sample hosts file that you can use](https://winhelp2002.mvps.org/hosts.txt) that includes most ad networks and trackers. Use it at your own risk though and be aware that some apps might not work anymore. But maybe your privacy is worth it?

## Security

*   FallibleInc’s “[A practical security guide for web developers](https://github.com/FallibleInc/security-guide-for-developers)” tries to help developers build more secure, less vulnerable solutions. While they claim that it’s by no means a comprehensive guide, it covers stuff based on the most common issues they’ve discovered in the past.
*   We know that HTTPS is not super-secure. That’s why lately a lot of bugs were fixed in the software implementations and a lot of techniques like HSTS and HPKP were added. But sometimes all of this won’t help. Recently, [an attack was discovered that can be carried out by operators](https://arstechnica.com/security/2016/07/new-attack-that-cripples-https-crypto-works-on-macs-windows-and-linux/) of just about any type of network, including public Wi-Fi networks, which arguably are the places where people need HTTPS the most. There are also hints that this type of attack is already in use by at least the NSA and therefore likely by a lot of other people, too. Please never trust TLS only for your own security but use a VPN for public networks.

<figure><a href="https://arstechnica.com/security/2016/07/new-attack-that-cripples-https-crypto-works-on-macs-windows-and-linux/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2271e05f-9629-4359-8bcf-bd1218f184cc/https-protection-opt.png" alt="HTTPS protection" width="500" height="411" /></a><figcaption>Even when the Wi-Fi can’t be trusted, people rely on HTTPS to secure their connection. A fallacy, as a <a href="https://arstechnica.com/security/2016/07/new-attack-that-cripples-https-crypto-works-on-macs-windows-and-linux/">recently-discovered attack</a> shows. (Image credit: <a href="https://arstechnica.com/security/2016/07/new-attack-that-cripples-https-crypto-works-on-macs-windows-and-linux/">Ars Technica</a>)</figcaption></figure>

## Privacy

*   I don’t want to be the scapegoat here, but Pokémon Go is very popular, and I read some interesting things about the privacy of the game. For example, not only Alphabet (aka Google) is one of the main investors, but there’s also a [financial relationship between the game-maker Niantic and the CIA angel investment company In-Q-Tel](https://medium.com/friction-burns/pokémon-spy-17087ae3653d). While there’s no evidence on what this could mean for the privacy of users, it definitely means that those companies are highly interested in the data that is provided by the gamers — understandable, as it’d be very hard to get geo information and pictures of private ground in a normal way. I’ve heard that several companies such as BMW already advised their employees that it’s forbidden to play the game at their factory sites and the German army published a similar order to their soldiers. ExpressVPN also published a short summary list with [nine privacy issues to consider when playing Pokémon Go](https://www.expressvpn.com/blog/pokemon-go-privacy-concerns/).</p>

## Web Performance

*   Erik Duindam writes about how a good architecture can save you a lot of money when building a product. He shares [how he built a Pokémon Go app with 500k users in just five days](https://medium.com/unboxd/how-i-built-an-app-with-500-000-users-in-5-days-on-a-100-server-77deeb238e83#.91iwcl397) and reduced the costs of it to a $100/month server infrastructure, compared to many MVP products that burn money by choosing bad technical designs.
*   Jake Archibald shares an interesting little fact about the benefits of using `rel=noopener`: [it’s faster](https://jakearchibald.com/2016/performance-benefits-of-rel-noopener/).</p>

## Accessibility

*   Addy Osmani explains how to build [accessible UI components for the web](https://medium.com/@addyosmani/accessible-ui-components-for-the-web-39e727101a67), taking into consideration visual, hearing, mobility and cognition as accessibility factors. A pretty great entry-level guide to better, accessible products.
*   Having a guideline for accessibility that developers can refer to makes sense for every project. Inspiration to create one comes from Vox who [published their accessibility guidelines publicly.](https://accessibility.voxmedia.com/)

## JavaScript

*   Pascal Precht shares how to [create custom form controls in Angular 2](https://blog.thoughtram.io/angular/2016/07/27/custom-form-controls-in-angular-2.html) in his usual easy-to-understand, high-quality style.
*   Krasimir Tsonev wrote an article about [React.js in design patterns](https://krasimirtsonev.com/blog/article/react-js-in-design-patterns) with some common code snippets that will come in handy in most React.js projects.</p>

## CSS/Sass

*   Chris Coyier wrote up solutions to [create full-width child containers](https://css-tricks.com/full-width-containers-limited-width-parents) of a limited-width parent, including [Sven Wolfermann’s simple and clever approach](https://css-tricks.com/full-width-containers-limited-width-parents/#article-header-id-6).</p>

## Work & Life

*   “Always improve, never stop, never pause, never appreciate” is something that developers, company leaders, and managers can easily apply to their work. Mathias Meyer points out [the importance of properly appreciating work that has been done](https://www.paperplanes.de/2015/9/28/always-improve-never-appreciate.html).
*   We have some evidence already that multitasking isn’t beneficial for productivity. Lydia Dishman now wrote up what changed when she moved to monotasking for a week. The reason why I found this article particularly interesting, is realizing [how much multitasking we do during a normal day without taking note of it](https://www.fastcompany.com/3062183/your-most-productive-self/what-happened-when-i-gave-up-multitasking-for-a-week).

<figure><a href="https://www.fastcompany.com/3062183/your-most-productive-self/what-happened-when-i-gave-up-multitasking-for-a-week"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/60989f62-dc96-493e-b17b-754da17c9a32/multitasking-opt.png" alt="Multitasking" width="500" height="352" /></a><figcaption>What happens when you give up multitasking for a week? <a href="https://www.fastcompany.com/3062183/your-most-productive-self/what-happened-when-i-gave-up-multitasking-for-a-week">Lydia Dishman found out</a>.</figcaption></figure>

## Going Beyond…

*   We still might not know if it’s our fault that [the climate is changing](https://www.flassbeck-economics.com/how-climate-change-is-rapidly-taking-the-planet-apart/). But what we now know is that [Greenland’s ice-shield lost twice as much ice in the past four years](https://www.washingtonpost.com/news/energy-environment/wp/2016/07/19/greenland-lost-a-trillion-tons-of-ice-in-just-four-years/) as in the 20 years before that. And this means much faster-rising sea levels, the loss of drinking water, and the loss of an important weather control on Earth (the Arctic has much influence on how storms and weather develop). In the end, it’s us who suffer from it, so we need to act and do our best to stop this trend.
*   Zack Bloom shares what [the alternative suggestions of languages were back when CSS was invented](https://eager.io/blog/the-languages-which-almost-were-css/) and why CSS succeeded.

<em>And with that, I’ll close for this week. If you like what I write each week, please <a href="https://wdrl.info/donate">support me with a donation</a> or share this resource with other people. You can learn more <a href="https://wdrl.info/costs/">about the costs of the project here</a>. It’s available via email, RSS and online.</em>

{{< signature "ah" >}}

