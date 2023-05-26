---
title: Website Maintenance Tips for Front-End Developers
slug: website-maintenance-tips-for-front-end-developers
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/88ed2d69-48db-4c98-bd0b-499c3b334e40/sketch.png
date: 2009-11-04T20:23:45.000Z
author: louis-lazaris
description: >-
  One of the biggest advantages of online media over print is the ability to
  change, update, and enhance online media at virtually anytime, with virtually
  no negative side effects. In fact, if a website or web application does not
  continually offer its users an ever-evolving and growing experience, that site
  or application would soon become insecure, unusable, and out of date.
categories:
  - Business
  - Design
  - Web Design
  - Bugs
  - Documentation
  - Security
  - Maintenance
---
One of the biggest advantages of online media over print is the ability to change, update, and enhance online media at virtually anytime, with virtually no negative side effects. In fact, if a website or web application does not continually offer its users an ever-evolving and growing experience, that site or application would soon become insecure, unusable, and out of date.

You may also want to check out the following Smashing Magazine articles:

*   [Effective Maintenance Pages: Examples and Best Practices](https://www.smashingmagazine.com/2009/06/effective-maintenance-pages-examples-and-best-practices/)
*   [A Comprehensive Website Planning Guide](https://www.smashingmagazine.com/2011/06/a-comprehensive-website-planning-guide/)
*   [404 Error Pages, One More Time](https://www.smashingmagazine.com/2009/01/404-error-pages-one-more-time/)

Have you beautified your code, validated your markup, and made your XHTML more semantic? Have you implemented basic SEO best practices, spell-checked content, and removed legacy code? Have you ensured JavaScript is unobtrusive, applied the principle of graceful degradation, and minimized the use of Flash? If you've done all those things (and possibly more), what comes next? Are there things you can do to <strong>improve your site's overall effectiveness</strong> beyond those?

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3c7ca125-ca2e-4bf4-aa7c-023e9f6d05fc/wrenches.jpg" alt="Wrenches" width="500" height="294" />

{{% feature-panel %}}

In this article, we will discuss ways that web designers and front-end coders can keep their websites relevant, timely, and accessible long after a site's launch. This guide goes beyond simple text and graphic updates, common "best practices" for CSS and XHTML, or other things you might see in a typical <a href="https://www.smashingmagazine.com/2009/06/29/45-incredibly-useful-web-design-checklists-and-questionnaires/">website checklist</a>. We'll expand on many of the basics, and provide some <strong>effective tips for website maintenance</strong> geared towards front-end designers and coders.</p>

## 1\. Keep Your Content Clean and Updated

After your website has accumulated dozens, maybe even hundreds of pages, <strong>content can become old and outdated</strong>. Website maintenance should include ongoing reviews of static content that may require updates or corrections. Of course, content that appears on blog or news pages would become outdated, but may not require changes. In those cases, the best solution may be to post new entries that update the information.

Of course, as a front-end developer for a company or agency, content maintenance would likely not be your responsibility, but if you're a one-man web agency or another type of freelancer, content maintenance would be a vital part of your routine.

<img title="Contract" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/15d42d69-b1aa-4830-8c40-5e3270902396/contract.jpg" alt="Contract" width="500" height="333" />

<strong>Policy Pages, Terms &amp; Conditions, Terms of Service</strong>
Legal issues could arise if policies and terms pages are not adequately updated to reflect the latest company standards and procedures. Reviewing these types of documents that appear on your website or in your web application should be a regular part of your maintenance routine.

<strong>Software Documentation</strong>
Documentation associated with a product or service may also become out of date with new releases or bug fixes. Where time allows, your maintenance routine may also include regular additions and modifications to documentation, whether they appear online or in downloadable format.

<strong>Contracts</strong>
The services your company provides may require agreement to services between both parties by means of a legal contract. Is this document up to date, reflecting the latest company policies and standards?

<strong>Keep Your Blog Clean</strong>
If you are engaging your readers to participate in discussions on your blog, make sure that your posts do not contain spam comments. For instance, at the very least, regularly go through popular posts to manually remove comments that lead to suspicious sites. It's also necessary to analyze tags that you've used. Some tags could be altered or modified to better reflect the topic, maybe because of a singular or plural rendering, or because of a misspelled word. You could also reconsider your tagging system and come up with a style guide that describes your process of tagging posts, which would improve future tagging and tag maintenance. You might also want to close comments on popular posts to avoid spam and link dropping.</p>

## 2\. Repairs, Fixes and Upgrades

The most common website maintenance tasks are those related to errors, bugs, broken links, and browser incompatibilities. There are server-side maintenance tasks that could be performed as well, but we won't be considering any of those in this article. Let's look at a few things a front-end developer could be responsible for in this particular area when performing website maintenance.</p>

### Checking Broken Links: Not Just URLs

Checking for broken links, both internal and external, is a fairly straightforward task, since there are a number of web-based and stand-alone tools that perform this task. But link checking can go beyond URLs; you can also check to ensure all images and external files are properly referenced. Here are some tools to assist with these tasks:

<a href="https://www.dead-links.com/">Dead Links</a> is a free web-based broken link checker that is very easy to use, and has an easy-to-read results page. Dead Links only checks links from anchor tags in your markup.

[![Dead Links](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/577df848-03e6-4999-9242-49b0a28dfab6/deadlinks.jpg "Dead Links")](https://www.dead-links.com/)

<a href="https://home.snafu.de/tilman/xenulink.html">Xenu's Link Sleuth</a> is a free stand-alone link-checker application with numerous features. It checks broken links, image paths, backgrounds, external CSS, external JavaScript, and more.

[![Xenu's Link Sleuth](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/584cabdb-04b8-4599-9243-4a46f473383f/sleuth.jpg "Xenu's Link Sleuth")](https://home.snafu.de/tilman/xenulink.html)

### Updating Your CMS & Plugins

If you're using a popular content management system, chances are very high that at some point you'll need to upgrade. This would be necessary for a variety of reasons — maybe the previous version has security problems, contains inefficient code, or just doesn't work properly any more.

WordPress is one of the most widely used blogging frameworks, and it is used prevalently as a multi-featured content management system. Since there are thousands of <a href="https://wordpress.org/extend/plugins/">WordPress plugins</a> available, there are also bound to be hundreds of plugins that are no longer supported. Older, unsupported plugins that have <strong>not been updated by the plugin author</strong> to be compatible with the most recent version of WordPress could make your website insecure.

[![WordPress Plugin Directory](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/70b26957-9b4d-472c-b3c5-d06001bb8f8f/wpplugins.jpg "WordPress Plugin Directory")](https://wordpress.org/extend/plugins/)

Fortunately, in recent versions of WordPress, <strong>updating your WP installation</strong> is as easy as a few clicks. Also, your dashboard will notify you when plugin upgrades are available. Your plugin page also gives you the option to view details on a particular plugin's recent changes. So, if your site is running on WordPress, updating your WordPress and related plugins should be high priority items in your website maintenance to-do list.

It's important to note that the upgraded version of your content management system won't necessarily support all tweaks and plugins that you have carefully installed and customized when the site was launched. So, as part of your maintenance routine, make sure you find newer versions of plugins or else replace them with reasonable alternatives before upgrading your CMS.</p>

## 3\. Browser Compatibility Testing

Ensuring all aspects of your website or web application are functioning properly in the most commonly-used browsers should be an ongoing part of your maintenance routine. While valid, semantic code will give you the best chance for cross-browser success, there is still the need to do manual and, if necessary, automated checks to <strong>ensure optimal compatibility</strong>.</p>

### Compatibility with Lesser-Used Browsers

Ensuring your site's compatibility with IE6/7/8 and Firefox 2/3 on a PC is commonplace in website maintenance. But don't forget to check some of the recent releases of lesser-used browsers like Opera, Chrome, and Safari. Firefox, Opera, and Safari should also be checked, if possible, on a Macintosh, because there is the potential for variations in rendering. I've personally seen CSS layout quirks that occur in Safari on a Mac, but do not appear in Safari on a PC.

![Browsers](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c2444b0e-6f08-4808-8b15-db69ffa64d3b/browsers.jpg "Browsers")

### Automated Application Testing

<a href="https://seleniumhq.org/">Selenium Web Application Testing System</a>
Selenium is a suite of tools specifically for testing web applications. The suite includes Selenium IDE (a Firefox plugin), Selenium Remote Control (which automates the process), and Selenium Grid (which allows concurrent tests on multiple platforms).

[![Selenium Web Application Testing System](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5dfcc0f2-5db1-4002-badc-ad6afc2c58d9/selenium.jpg "Selenium Web Application Testing System")](https://seleniumhq.org/)

### Online Compatibility Testing

<a href="https://browsershots.org/">Browsershots</a>
Browsershots is probably the most popular tool for viewing screenshots of your website in multiple browsers and on multiple platforms.

[![Browsershots](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/11e47e9f-b9d6-49a5-b4b0-aec8cd295447/browser-shots.gif "Browsershots")](https://browsershots.org/)

<a href="https://browserlab.adobe.com/">Adobe BrowserLab</a>
"Preview and test your web pages on leading browsers and operating systems — on demand. Adobe BrowserLab makes it easier and faster than ever before to see how your designs appear to your customers and audience. Get your results in real time, from virtually any computer connected to the web."

[![Adobe BrowserLab](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/20359586-85a6-4b51-8a79-c0546a56f289/browser-lab.jpg "Adobe BrowserLab")](https://browserlab.adobe.com/)

Further reading:

*   [How to Build the Best Browser Test Suite](https://www.sitepoint.com/blogs/2009/03/17/building-the-best-browser-test-suite/)
*   [10 Helpful Resources for Cross Browser Testing](https://designm.ag/resources/cross-browser-testing/)
*   [7 Fresh and Simple Ways to Test Cross-Browser Compatibility](https://freelancefolder.com/7-fresh-and-simple-ways-to-test-cross-browser-compatibility/)

## 4\. Beyond Validation and Web Standards

Typically, website maintenance might consist of continued validation of pages, usually after features are added or content is updated. Validation might include both <a href="https://validator.w3.org/">markup</a> and <a href="https://jigsaw.w3.org/css-validator/">styles</a>. There are things, however, that can be done beyond just simple validation of pages, since "valid" code does not necessarily equate to "good" code.</p>

### Cleaner, Leaner XHTML

Are there components in your markup that can be reduced in size? When you first coded the site, you may have suffered from a problem called "<strong>divitis</strong>". This basically means there are <code>&lt;div&gt;</code> tags in your code that could easily be removed because they don't serve a purpose. A perfect example is the <code>&lt;div&gt;</code> wrapped around a navigation section, like this:

<pre><code class="language-markup tmp-xml">&lt;div class="nav-holder"&gt;
  &lt;ul class="nav"&gt;
    &lt;li&gt;&lt;a href="home"&gt;Home&lt;/a&gt;&lt;/li&gt;
    &lt;li&gt;&lt;a href="about"&gt;About&lt;/a&gt;&lt;/li&gt;
    &lt;li&gt;&lt;a href="services"&gt;Services&lt;/a&gt;&lt;/li&gt;
    &lt;li&gt;&lt;a href="products"&gt;Products&lt;/a&gt;&lt;/li&gt;
    &lt;li&gt;&lt;a href="contact"&gt;Contact&lt;/a&gt;&lt;/li&gt;
  &lt;/ul&gt;
&lt;div&gt;</code></pre>

In the above code, in most cases, the <code>&lt;div&gt;</code> element is unnecessary. If a CSS enhancement is needed on the entire navigation section, this can be done on the <code>&lt;ul&gt;</code> element, since it too is a block-level element. Of course, there could be a reason that the outer <code>&lt;div&gt;</code> is needed, but the code would generally be just as flexible without that element.

What about <strong>too many attributes</strong>? This is not as bad as having too many <code>&lt;div&gt;</code> elements, but code can start to look cleaner and be easier to manage if you avoid habitually putting classes and IDs on virtually every element. Using inheritance principles in CSS, instead of direct targeting of each individual element can trim your code down to a more manageable level. It should be noted, however, that in some cases, while removing attributes could improve the performance of your markup, it could have negative effects on the performance of your CSS, albeit at <a href="https://meiert.com/en/blog/20090312/performance-of-css-selectors/">very small levels</a>.

Further reading:

*   [Divitis: what it is, and how to cure it.](https://csscreator.com/divitis)
*   [Cleaner HTML by Avoiding 'Attributitis'](https://www.impressivewebs.com/cleaner-html-by-avoiding-attributitis/)

### Improving the Quality of Your JavaScript

If you've created a lot of custom JavaScript, possibly in conjunction with a JavaScript library, your code might benefit from improvements. You can <strong>test the quality of your JavaScript code</strong> using Douglas Crockford's <a href="https://www.jslint.com/">JSLint</a>, which he calls "the code quality tool." I wouldn't classify JSLint as a "validator", because what is valid in JavaScript is not always what is best. In fact, many JavaScript techniques are now understood to cause major performance issues.

[![JSLint](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4750319b-161c-4ff7-8ba3-29cc31e80a92/jslint.jpg "JSLint")](https://www.jslint.com/)

So consider whether you can include quality testing of JavaScript code as part of your regular website maintenance routine.

Further reading:

*   Warning! JSLint Will Hurt Your Feelings

### Cleaning & Optimizing CSS

After years of development, CSS files can become bloated, hard to maintain, and unreadable. Along the way, you may have learned to produce stronger code, so any future additions would be acceptable, but what about going back to optimize and refactor older CSS code? Many CSS files, over time, will develop <strong>redundancies</strong> that hinder speed.

There are a number of <strong>tools available to help with this task</strong>, all of which should be used with care. Before doing any optimizing, be sure to have backups of all CSS files, because automated tools, if used improperly, can render your code unusable.

<a href="https://jigsaw.w3.org/css-validator/">W3C CSS Validation Service</a>
Before doing any CSS optimization, you should first check to ensure your CSS is valid. Errors in your CSS code could cause problems when doing any automated optimization or refactoring.

[![W3C CSS Validation Service](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7ea7db83-43b4-4aec-b495-77cc64c9cb07/css-validation.jpg "W3C CSS Validation Service")](https://jigsaw.w3.org/css-validator/)

<a href="https://www.cleancss.com/">Clean CSS</a>
This online CSS optimizer offers many different options and displays details of all changes made.

[![Clean CSS](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0a01b61b-b568-4c1f-8fb7-8233e26cb920/clean-css.jpg "Clean CSS")](https://www.cleancss.com/)

<a href="https://www.sitepoint.com/dustmeselectors/">Dust-Me Selectors</a> (thanks, <em>jeyaONE</em>)
This useful Firefox plugin will tell you which CSS selectors are no longer in use, so you can safely remove them.

[![Dust-Me Selectors](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9a3e81aa-cca0-460b-97af-7f05552138e7/dust-me.jpg)](https://www.sitepoint.com/dustmeselectors/)

You also have the option to do all optimization manually, to ensure no problems occur. Of course, many optimization techniques cannot be automated. One example is combining multiple CSS files to minimize HTTP requests. Also, you may decide to change class names and ID names to reflect more appropriate conventions. (e.g. using the class name "promo-box" would be more appropriate than "blue-box", since the color of the box could change).

Further reading:

*   [The Cascade, Specificity, and Inheritance](https://reference.sitepoint.com/css/inheritancecascade)
*   [7 Principles Of Clean And Optimized CSS Code](https://www.smashingmagazine.com/2008/08/18/7-principles-of-clean-and-optimized-css-code/)
*   The right way to name id and class attributes

## 5\. Improving Accessibility

If you've validated your markup and used best-practices coding techniques, then it's likely that your site's content is, generally speaking, accessible to users that are visiting your page using a screen reader or other assistive technology. But, since newly added content could affect the accessibility of your site, accessibility testing should be an ongoing process.</p>

### Tools to Test Website Accessibility

You can do ongoing checks for accessibility using a few tools, some examples of which are shown below.

<a href="https://wave.webaim.org/">WAVE - Web Accessibility Evaluation Tool</a>
"WAVE is a free web accessibility evaluation tool provided by WebAIM. It is used to aid humans in the web accessibility evaluation process. Rather than providing a complex technical report, WAVE shows the original web page with embedded icons and indicators that reveal the accessibility of that page."

[![WAVE - Web Accessibility Evaluation Tool](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bb5679ac-0827-43c1-a971-63e7a83d9e46/wave.jpg "WAVE - Web Accessibility Evaluation Tool")](https://wave.webaim.org/)

<a href="https://www.aprompt.ca/">A-Prompt - Web Accessibility Verifier</a>
"A-Prompt (Accessibility Prompt) is a software tool designed to help Web authors improve the usability of Web pages created in HTML format. A-Prompt first evaluates an HTML Web page to identify barriers to accessibility by people with disabilities. A-Prompt then provides the Web author with a fast and easy way to make the necessary repairs."

![A-Prompt - Web Accessibility Verifier](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/55f5be46-07ea-46be-8ab6-9276dceb0f21/a-prompt.jpg "A-Prompt - Web Accessibility Verifier")

Besides using the tools shown above, a simple way to perform ongoing accessibility tests on your web pages is to view them with <strong>styles and JavaScript disabled</strong>. This will give you a general idea of what content will be accessible through assistive technology.</p>

### Testing Mobile Access

If you haven't yet set up a mobile version of your website, there are a number of books and online resources that can assist you in this regard. If your mobile site is already up and running, you can continue to run tests on newly-added content and make adjustments as required. Below are a few helpful resources to assist you in making your site accessible to mobile devices.

<a href="https://mobilewebbook.com/">Mobile Web Design by Cameron Moll</a>
"Much has been written about mobile devices. Plenty has been written about developing websites for the so-called 'standards era' of the web. However, little has been written about the two colliding. This resource aims to fill that void."

[![Mobile Web Design Book](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/efb3c672-8f8b-4a65-ad1e-06472820ec43/mobile.jpg "Mobile Web Design Book")](https://mobilewebbook.com/)

<a href="https://www.instantfundas.com/2009/03/5-free-ways-to-create-mobile-version-of.html">5 free ways to create a mobile version of your website</a>
This article discusses a few free services that will assist in creating a mobile version of your website.

Further reading:

*   [Selecting Web Accessibility Evaluation Tools](https://www.w3.org/WAI/eval/selectingtools.html)
*   [456 Berea Street - Roger Johansson's web standards and accessibility blog](https://www.456bereastreet.com/)

## 6\. CSS3 & HTML5 Enhancements

Although it is true that not all currently-used browsers support CSS3 and HTML5, new techniques in those areas can still be applied to work in newer browsers that offer support. During site maintenance, you can assess what areas of your website could be enhanced using specific CSS3 and HTML5 techniques. Of course, you would ensure that any modifications in this area will <strong>degrade gracefully</strong> in browsers that don't support those new techniques. Progressive techniques, based upon CSS3 and HTML5, may help you finally get rid of the old code and all JS/(X)HTML/CSS-hacks that you had to use when the site was launched.

<a href="https://www.css3.info/">CSS3.info</a>
Everything you need to know about CSS3.

[![CSS3.info](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/92bf52a7-2b9d-405c-b8d7-8b3ffd6288f3/css3.jpg "CSS3.info")](https://www.css3.info/)

<a href="https://html5gallery.com/">HTML5 Gallery</a>
A showcase of sites using HTML5 markup.

[![HTML5 Gallery](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d52f7ed3-af50-4f62-bd36-b320fe6a7af0/html5.jpg "HTML5 Gallery")](https://html5gallery.com/)

<a href="https://articles.sitepoint.com/article/html-5-snapshot-2009">Yes, You Can Use HTML 5 Today!</a>
In this article on SitePoint, Bruce Lawson describes how HTML 5 techniques can be implemented in a cross-browser fashion using some JavaScript workarounds to support Internet Explorer.

<a href="https://www.webdesignerdepot.com/2009/08/5-css3-design-enhancements-that-you-can-use-today/">5 CSS3 Design Enhancements That You Can Use Today</a>
This article on Webdesigner Depot describes 5 CSS3 design techniques that can be used without harming the user experience.

Further reading:

*   [A Preview of HTML 5](https://www.alistapart.com/articles/previewofhtml5)
*   [HTML5 and The Future of the Web](https://www.smashingmagazine.com/2009/07/16/html5-and-the-future-of-the-web/)
*   [Push Your Web Design Into The Future With CSS3](https://www.smashingmagazine.com/2009/01/08/push-your-web-design-into-the-future-with-css3/)
*   [Take Your Design To The Next Level With CSS3](https://www.smashingmagazine.com/2009/06/15/take-your-design-to-the-next-level-with-css3/)

## 7\. Optimizing for Speed

A somewhat bizarre trend in recent modern web development is the seeming obsession with optimizing pages for speed — <strong>in spite of the continued rise in internet connection speeds</strong> worldwide. Although more people than ever before are on high-speed connections, more developers than ever before are concerned about the speed at which their pages load.

Analysis of a website's performance during website maintenance may instigate a desire to make changes that will improve the speed at which pages load. If you'd like to include website speed optimization techniques into your maintenance routine, the following resources could prove useful.</p>

### Books by Steve Souders

<a href="https://oreilly.com/catalog/9780596529307">High Performance Web Sites: Essential Knowledge for Front-End Engineers</a>
This book, by Steve Souders, is the ultimate guide to optimizing a website's load time, offering 14 specific techniques that can help you serve pages to your users quickly and efficiently.

[![High Performance Web Sites: Essential Knowledge for Front-End Engineers](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2e7e277b-aeb1-4976-aacc-8af8b8ffa338/hpw.jpg "High Performance Web Sites: Essential Knowledge for Front-End Engineers")](https://oreilly.com/catalog/9780596529307)

<a href="https://oreilly.com/catalog/9780596522308/">Even Faster Web Sites: Performance Best Practices for Web Developers</a>
This is Steve Souders' follow-up to <em>High Performance Websites</em>, providing a further 14 tips and techniques for improving website speed.

[![Even Faster Web Sites: Performance Best Practices for Web Developers](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/99ac9a98-5cc5-4670-ae5f-801e225409fd/efw.jpg "Even Faster Web Sites: Performance Best Practices for Web Developers")](https://oreilly.com/catalog/9780596522308/)

### Tools & Browser Plugins

<a href="https://www.cyberciti.biz/tips/website-load-speed-performace-testing-tools.html">6 Tools To Find Out Website Load Speed</a>
This article describes six different tools for testing the load speed of web pages, including Yahoo! YSlow, Google Page Speed, Internet Explorer's Pagetest, and more.

<a href="https://sixrevisions.com/tools/faster_web_page/">15 Tools to Help You Develop Faster Web Pages</a>
Jacob Gube of Six Revisions gives an overview of 15 different tools that can help you analyze and improve the speed of your website.</p>

## 8\. Adding Comments to New (and Old) Code

If you've validated your code, and cleaned up unnecessary sections as outlined earlier, could your code benefit from further optimization? If time allows, during website maintenance, including comments in your XHTML, CSS, and JavaScript could improve the speed at which you make site updates in the future.</p>

### Commenting Your Markup

In some cases, comments won't contribute a lot. For example, a <code>&lt;div&gt;</code> element with an ID of "sidebar" may not require a comment above it that says "This is the sidebar" — that's obvious from the well-named ID. But your code could be <strong>easier to read with comments</strong> added to the bottom of sections where there are a lot of nested <code>&lt;div&gt;</code> tags.

The lower portion of your HTML code might look like this:

<pre><code class="language-markup tmp-xml">&lt;/div&gt;

      &lt;/div&gt;

    &lt;/div&gt;

  &lt;/div&gt;  

  &lt;div id="footer"&gt;

  &lt;/div&gt;

&lt;/div&gt;

&lt;/body&gt;
&lt;/html&gt;</code></pre>

It might be difficult to make any major changes to this code without quickly being able to match the closing <code>&lt;div&gt;</code> tags to their opening tags. The same code would be easier for both front-end and back-end programmers with comments added, as shown below:

<pre><code class="language-markup tmp-xml">&lt;/div&gt;&lt;!-- /content-inner --&gt;

      &lt;/div&gt;&lt;!-- /content-inside --&gt;

    &lt;/div&gt;&lt;!-- /content-left --&gt;

  &lt;/div&gt;&lt;!-- /main content --&gt;  

  &lt;div id="footer"&gt;

  &lt;/div&gt;&lt;!-- /footer --&gt;

&lt;/div&gt;&lt;!-- /container --&gt;

&lt;/body&gt;
&lt;/html&gt;</code></pre>

### Commenting JavaScript

What about large sections of JavaScript that include nested loops that might be confusing long after you've written the code? It would be ideal to put comments in the code when writing it, but that's not always done.

You can <strong>review complicated sections of JavaScript code</strong> and add relevant comments that will help you, when doing updates, to identify code more efficiently. Doing this type of maintenance might also help remind you to comment your code during actual development time in the future.</p>

### Commenting & Organizing CSS

CSS code can also be analyzed to see if improvements can be made by commenting or other organizational changes. I personally like to include global styles near the top of my CSS files, while <strong>indenting sections of CSS</strong> to correspond with the indenting of the HTML tags that they match up with.

Below is an example of commented and indented CSS:

<pre><code class="language-css">/* FOOTER STYLES BEGIN HERE */

#footer {
  color: #A3A2A0;
  border-top: 1px solid #eee;
  min-width: 820px;
  height: 78px;
  font-size: .92em;
  line-height: 1.4;
  background-color: #fff;
}

   #footer p {
    float: left;
    width: 145px;
    margin-top: 5px;
   }

     #footer p span {
      width: auto;
      float: right;
      padding: 15px 25px 0 0;
     }

/* FOOTER STYLES END HERE */</code></pre>

Of course, when it comes to code improvements, what works best for your maintenance schedule and overall coding habits will be up to you. During site maintenance, your website may benefit from implementing some of these methods of commenting and organizing.</p>

## 9\. SEO Enhancements

As a front-end coder or designer for an agency or other company, you probably will not be responsible for SEO-related updates. If, however, this is a personal project or your own personal website, then you may need to do ongoing SEO maintenance.

Semantic, well-structured markup will automatically gain SEO benefits from the start — even without any specific search engine optimization techniques having been implemented. But, as time goes on, the <strong>integration of specific SEO methods</strong> may be required to boost your site in search rankings for particular search terms and phrases.

![SEO](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d1a8b8e2-d123-43e2-9cf8-aedca9de2548/seo.jpg "SEO")

So, specific SEO optimization practices — optimizing keyword phrases, improving title tags, adding meta descriptions, writing good page titles, and optimizing internal link structure — are other items that could be added to a website maintenance to-do list.

Further reading:

*   [Official Google Webmaster Central Blog](https://googlewebmastercentral.blogspot.com/)
*   [Axandra Search Engine Facts Newsletter](https://www.free-seo-news.com/index.php)

## 10\. Website Analytics & Conversions

Analysis of site traffic, bounce rates, traffic sources, and other web analytics-related statistics should be a regular part of a site's ongoing maintenance. Of course, in an agency or corporate environment this area would fall under marketing or SEO. For a personal project, however, unless you're outsourcing this type of work, you'll need to <strong>continually analyze your site statistics</strong> to see where improvements can be made.</p>

### Improving "Call To Action" Areas

If you experience lower conversion rates than you'd like, your site could benefit from an adjustment in <a href="https://www.smashingmagazine.com/2009/10/13/call-to-action-buttons-examples-and-best-practices/">call to action</a> buttons or similar components of your site. Wherever a user is located on your website, there should be a clear path to the services or products you offer. During site maintenance, changes could be made to ensure users are finding the most important parts of your website quickly and efficiently.

[![Google Analytics](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1ca6b6ca-761d-48ed-ad96-584527cc451d/yourwebjob-placement-high.jpg "Google Analytics")](https://www.smashingmagazine.com/2009/10/13/call-to-action-buttons-examples-and-best-practices/)

### Analytics Tools

A number of <strong>free analytics tools</strong> are available, the most popular of which is Google Analytics, which is very easy to install. Most likely you've installed it on your website, but are you doing the necessary ongoing analysis?

You can look at keywords that are helping users find your website, and add new content according to those keywords. I once wrote an article for my own website based purely on a key phrase that was regularly used to find my site through Google. Now, since I wrote an article that specifically deals with the content of that key phrase, that page is the <a href="https://www.impressivewebs.com/avoiding-problems-with-javascript-getelementbyid-method-in-internet-explorer-7/">most visited page on my site.</a>

<a href="https://www.google.com/analytics">Google Analytics</a>
Google Analytics is the premiere website statistics analysis tool.

[![Google Analytics](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d15a48f5-304d-4ba1-ac2e-b8b76fc285bd/ga.jpg "Google Analytics")](https://www.google.com/analytics)

<a href="https://mashable.com/2009/01/12/track-online-traffic/">Analytics Toolbox: 50+ More Ways to Track Website Traffic</a>
This article on Mashable.com offers a list of more than 50 tools for tracking and analyzing website statistics.

Further reading:

*   Your Website's Call-to-Action is Its Central Purpose
*   [Ten Ways to Improve Your Website Conversion Rate](https://www.addedbytes.com/online-marketing/ten-ways-to-improve-your-website-conversion-rate/)

## 11\. Incorporating User Feedback

A high-traffic, successful website should have clear methods for users to provide feedback. The most basic of these is the contact form or email address on the contact page. You could also collect feedback through social networking, polls, surveys, and blog post comments. Whatever means you're using to receive input on the functionality and usability of your site, your ongoing maintenance routine could incorporate many of the suggestions you receive.

![Feedback on Twitter](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d2b72407-7a16-49bd-88c8-c505c662577f/twitter-feedback.jpg "Feedback on Twitter")

Some suggestions for improvement could be simple bug and error fixes, or compatibility problems. These could be itemized and corrected in a relatively short time. Other suggestions received, however, could require significant layout changes or page restructuring, so would have to be factored into long-term maintenance.

Whatever the case may be, obtaining and acting on feedback from users will allow your website to grow and thrive, and will <strong>give evidence to your users that customer service is your priority</strong>.</p>

## Conclusion

Leaving a website untouched after its initial launch is, in many ways, like buying a car and never changing the oil or never filling up on gas — it might run fine for a while, but eventually it will slow down and come to a complete halt, providing no benefit to its owner or passengers. An ongoing routine of regular, <strong>scheduled analysis and maintenance</strong> using many of the techniques mentioned in this article could prove integral to the success and overall functioning of your website or web application.

