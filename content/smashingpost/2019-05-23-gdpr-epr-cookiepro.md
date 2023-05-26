---
title: 'What’s Happening With GDPR And ePR? Where Does CookiePro Fit In?'
slug: gdpr-epr-cookiepro
author: suzanne-scacca
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d2944227-a58f-4783-814e-292451d56cba/cookie-scan.jpg
date: 2019-05-23T10:00:59+02:00
summary: >-
  Now that we have a year of GDPR under our belts, and the ePR is coming soon, there’s no better time than now to review your websites. Do you know what kinds of cookies collect information from your site? And have you provided visitors with information about an option to accept those cookies? If your site is currently not in compliance, or you’re not sure if it is, read this post and start using CookiePro’s cookie consent tool to get your sites moving in the right direction.
description: >-
  Do you know what kinds of cookies collect information from your site? If your site is currently not in compliance, start using CookiePro’s cookie consent tool to get your sites moving in the right direction.
categories:
  - Ethics
disable_ads: true
disable_panels: true
---

<p>(This is a sponsored article.) Is privacy an issue on the web? According to <a href="https://www.nbcnews.com/id/42239031/ns/business-consumer_news/t/whos-watching-you-online-ftc-pushes-do-not-track-plan/#.XMc3lBNKjBI">this ConsumerMan piece from NBC News</a> a few years back, it is:</p>

<blockquote>The Internet has become a serious threat to our privacy.<br />&mdash; Jeff Chester of the Center for Digital Democracy</blockquote>

<blockquote>Your online profile is being sold on the web. It's kind of crazy and it's not harmless.<br />&mdash; Sharon Goott Nissim of the Electronic Privacy Information Center</blockquote>

<blockquote>There are no limits to what types of information can be collected, how long it can be retained, with whom it can be shared or how it can be used.<br />&mdash; Susan Grant of the Consumer Federation of America</blockquote>

<p>While there’s been talk of introducing a “Do Not Track” program into U.S. legislation, the EU is the first one to actually take steps to make the Internet a safer place for consumers.</p>

<p>On May 25, 2018, the <a href="https://www.gdpreu.org/">General Data Protection Regulation</a> (GDPR) was enacted. Soon to follow will be the <a href="https://ec.europa.eu/digital-single-market/en/proposal-eprivacy-regulation">ePrivacy Regulation</a> (ePR).</p>

<p>With these initiatives holding businesses accountable for the information they track and use online, web developers have to add another thing to their list of requirements when building a website:</p>

<p><strong>The protection of user privacy.</strong></p>

<p>In this post, we’re going to look at:</p>

<ul>
  <li>Where we currently stand with GDPR,</li>
  <li>What changes we’ve seen on the web as a result,</li>
  <li>What’s coming down the line with ePR,</li>
  <li>And take a look CookiePro <a href="https://bit.ly/smcookieconsent">Cookie Consent</a> tool that helps web developers make their websites compliant <em>now</em>.</li>
</ul>

## GDPR: Where Are We Now?

<p>With the one-year anniversary of GDPR upon us, now is a great time to talk about what the updated legislation has done for online privacy.</p>

### GDPR Recap

<p>It’s not like the EU didn’t have privacy directives in place before. As <a href="https://www.smashingmagazine.com/2018/02/gdpr-for-web-developers/">Heather Burns explained</a> in a Smashing Magazine article last year:</p>

<blockquote>All of the existing principles from the original Directive stay with us under GDPR. What GDPR adds is new definitions and requirements to reflect changes in technology which simply did not exist in the dialup era. It also tightens up requirements for transparency, disclosure and, process: lessons learned from 23 years of experience.</blockquote>

<p>One other key change that comes with moving from the previous privacy directive to this privacy <em>regulation</em> is that it’s now consistently implemented across all EU states. This makes it easier for businesses to implement digital privacy policies and for governing bodies to enforce them since there’s no longer any question of what one country has done with the implementation of the law. It’s the same for all.</p>

<p>What’s more, there are clearer guidelines for web developers that are responsible for implementing a privacy solution and notice on their clients’ websites.</p>

### Has GDPR Led to Any Changes in How Websites Handle Data?

<p>It seems as though many companies are struggling to get compliant with GDPR, based on <a href="https://www.talend.com/about-us/press-releases/the-majority-of-businesses-are-failing-to-comply-with-gdpr-according-to-new-talend-research/">a test done by Talend</a> in the summer of 2018. They sent data requests to over a hundred companies to see which ones would provide the requested information, per the new GDPR guidelines.</p>

<p>Here is what they found:</p>

<ul>
  <li>Only 35% of EU-based companies complied with the requests while 50% outside of the EU did.</li>
  <li>Only 24% of retail companies responded (which is alarming considering the kind of data they collect from consumers).</li>
  <li>Finance companies seemed to be the most compliant; still, only 50% responded.</li>
  <li>65% of companies took over 10 days to respond, with the average response time being 21 days.</li>
</ul>

<p>What Talend suggests, then, is that digital services (e.g. SaaS, mobile apps, e-commerce) are more likely to fall in line with GDPR compliance. It’s the other companies &mdash; those that didn’t start as digital companies or who have older legacy systems &mdash; that are struggling to get onboard.</p>

<p>Regardless of what actions have been taken by businesses, they know they must do it.</p>

<p>A 2018 report published by <a href="https://iapp.org/media/pdf/resource_center/Ponemon_race-to-gdpr.pdf">McDermott Will & Emery and Ponemon Institute</a> showed that, despite businesses’ inability to be compliant, they were scared of what would happen if they were found not to be:</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/17d21a0c-b6a6-4ce6-a981-0585835e79d7/gdpr-compliance-concerns.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/17d21a0c-b6a6-4ce6-a981-0585835e79d7/gdpr-compliance-concerns.jpg" sizes="100vw" caption="Data on what businesses believed to be the greatest costs of failing to comply with GDPR. (Source: <a href='https://iapp.org/media/pdf/resource_center/Ponemon_race-to-gdpr.pdf'>McDermott Will & Emery and Ponemon Institute</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/17d21a0c-b6a6-4ce6-a981-0585835e79d7/gdpr-compliance-concerns.jpg'>Large preview</a>)" alt="GDPR report - failure to comply costs" >}}

<p>Those that said they feared financial repercussions were right to do so. The <a href="https://www.gdpreu.org/compliance/fines-and-penalties/">GDPR assesses fines</a> based on how severe the infringement is:</p>

<ul>
  <li>Lower level offenses result in fines of up to €10 million or 2% of the the revenue made in the prior fiscal year.</li>
  <li>Upper level offenses result in fines of up to €20 million or 4%.</li>
</ul>

<p>Some high-profile cases of fines have already popped up in the news, too.</p>

<p><a href="https://www.cnil.fr/en/cnils-restricted-committee-imposes-financial-penalty-50-million-euros-against-google-llc">Google</a> received a €50 million penalty for committing a number of violations.</p>

<p>Mainly, the issue taken with Google is that it buries its privacy policies and consent so deep that most consumers never find it. What’s more, a lot of their privacy policies are ambiguous or unclear, which leads users to “Accept” without really understanding what they’re accepting.</p>

<p><a href="https://ico.org.uk/about-the-ico/news-and-events/news-and-blogs/2018/10/facebook-issued-with-maximum-500-000-fine/">Facebook</a> is another company we shouldn’t be too surprised to see in GDPR’s crosshairs.</p>

<p>Their penalty was only for £500,000. That’s because the fine was assessed for grievances issued between 2007 and 2014 &mdash; before GDPR went into place. It’ll be interesting to see if Facebook changes its privacy policies in light of the much larger sum of money they’ll owe when another inevitable breach occurs.</p>

{{% pull-quote %}}
It’s not just the monetary fine businesses should be nervous about when failing to comply with GDPR.
{{% /pull-quote %}}

<p>Stephen Eckersley of the UK Information Commissioner's Office said that, after the GDPR went into effect, <a href="https://www.theregister.co.uk/2019/03/14/more_than_200000_gdpr_cases_in_the_first_year_55m_in_fines/">the amount of data breach reports increased exponentially</a>.</p>

<p>In June of 2018, there were 1,700 reports of companies in violation of GDPR. Now, the average is roughly 400 a month. Even so, Eckersley estimates that there will be double the amount of reports in 2019 than there were in previous years (36,000 vs. 18,000).</p>

<p>So, not only are the governing bodies willing to penalize businesses for failure to comply. It seems that consumers are fed up enough (and empowered!) to report more of these violations now.</p>

## Let’s Talk About ePR For A Second

<p>The ePrivacy Regulation has not yet become law, but it’s expected to soon enough. That’s because both GDPR and ePR were drafted to work together to update the old Data Protection Directive.</p> 

<p>ePR is an update to Article 7 in the <a href="https://eur-lex.europa.eu/legal-content/EN/TXT/?uri=CELEX:12012P/TXT">EU Charter of Human Rights</a>. GDPR is an update to Article 8.</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/239ca5f1-4e3e-43bc-a414-953bd4c5177a/eu-charter-of-human-rights.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/239ca5f1-4e3e-43bc-a414-953bd4c5177a/eu-charter-of-human-rights.jpg" sizes="100vw" caption="The Freedoms laid out by the EU Charter of Human Rights. (Source: <a href='https://eur-lex.europa.eu/legal-content/EN/TXT/?uri=CELEX:12012P/TXT'>EU Charter of Human Rights</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/239ca5f1-4e3e-43bc-a414-953bd4c5177a/eu-charter-of-human-rights.jpg'>Large preview</a>)" alt="EU Charter of Human Rights" >}}

<p>Although they’re separately defined, it’s best to think of ePR as an enhancement of GDPR. So, not only do businesses have to take care with <strong>data</strong> collected from individuals, the ePR says that they have to be careful with protecting the <strong>identity</strong> of individuals, too.</p> 

<p>As such, when the ePR rolls out, all digital communications between business and consumer will be protected. That includes:</p>

<ul>
  <li>Skype chats</li>
  <li>Facebook messages</li>
  <li>VoiP calls</li>
  <li>Email marketing</li>
  <li>Push notifications</li>
  <li>And more.</li>
</ul>

<p>If a consumer has not expressly given permission for a business to contact them, the ePR will prohibit them from doing so. In fact, the ePR will take it a step further and give more control to consumers when it comes to cookies management.</p>

<p>Rather than display a pop-up consent notice that asks “Is it okay if we use cookies to store your data?”, consumers will decide what happens through their browser settings.</p>

<p>However, <strong>we’re not at that point yet</strong>, which means it’s your job to get that notice up on your website and to make sure you’re being responsible with how their data is collected, stored and used.</p>

## What Web Developers Need To Do To Protect Visitor Privacy

<p>Do a search for "How to Avoid Being Tracked Online":</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5c61d3a6-3984-4f87-9731-2d0175d879a4/how-to-avoid-being-tracked-online.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5c61d3a6-3984-4f87-9731-2d0175d879a4/how-to-avoid-being-tracked-online.jpg" sizes="100vw" caption="Search for “How to Avoid Being Tracked Online” on Google. (Source: <a href='https://www.google.com/'>Google</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5c61d3a6-3984-4f87-9731-2d0175d879a4/how-to-avoid-being-tracked-online.jpg'>Large preview</a>)" alt="A sample Google search" >}}

<p>There are <em>over 57 million pages</em> that appear in Google’s search results. Do similar keyword searches and you’ll also find endless pages and forum submissions where consumers express serious concerns over the information gathered about them online, wanting to know how to “stop cookies”.</p>

<p><strong>Clearly, this is a matter that keeps consumers up at night.</strong></p>

<p>The GDPR should be your motivation to go above and beyond in putting their minds at ease.</p>

<p>While you probably won’t have a hand in the actual data management or usage of data within the business, you can at least help your clients get their websites in order. And, if you already did this when GDPR initially was enacted, now would be a good time to revisit what you did and make sure their websites are still in compliance.</p>

<p>Just make sure that your client is safely handling visitor data and protecting their privacy before providing any sort of privacy consent statement. Those statements and their acceptance of them are worthless if the business isn’t actually fulfilling its promise.</p>

<p>Once that part of the compliance piece is in place, here’s what you need to do about cookies:</p>

### 1. Understand How Cookies Work

<p>Websites allow businesses to gather lots of data from visitors. Contact forms collect info on leads. eCommerce gateways accept methods of payment. And then there are <a href="https://cookiepedia.co.uk/all-about-cookies">cookies</a>:</p>

<blockquote>Cookies are pieces of data, normally stored in text files, that websites place on visitors' computers to store a range of information, usually specific to that visitor &mdash; or rather the device they are using to view the site &mdash; like the browser or mobile phone.</blockquote>

<p>There are some that collect bare-bones details that are necessary to provide visitors with the best experience. Like preserving a logged-in session as visitors move from page to page. Or not displaying a pop-up after a visitor dismissed it on a recent visit.</p> 

<p>There are other cookies, usually from third-party tracking services, that pry deeper. These are the ones that track and later target visitors for the purposes of marketing and advertising.</p>

<p>Regardless of where the cookies come from or what purpose they serve, the fact of the matter is, consumers are being tracked. And, until recently, websites didn’t have to inform them when that took place or how much of their data was stored.</p>

### 2. Don’t Use Cookies That Are Irrelevant

<p>There’s no getting around the usage of cookies. Without them, you wouldn’t have access to analytics that tell you who’s visiting your website, where they come from and what they’re doing while they’re there. You also wouldn’t be able to serve up personalized content or notifications to keep their experience with the site feeling fresh.</p>

<p>That said, do <em>you</em> even know what kinds of cookies your website uses right now?</p>

<p>Before you go implementing your own cookie consent notice for visitors, make sure you understand what exactly it is you’re collecting from them.</p>

<p>Go to the <a href="https://bit.ly/smcookiepro">CookiePro website</a> and run a free scan on your client’s site:</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/57e04404-c08e-4524-93da-b80ae85db861/cookiepro-website-privacy-scan.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/57e04404-c08e-4524-93da-b80ae85db861/cookiepro-website-privacy-scan.jpg" sizes="100vw" caption="CookiePro offers a free website privacy scan. (Source: <a href='https://www.cookiepro.com/'>CookiePro</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/57e04404-c08e-4524-93da-b80ae85db861/cookiepro-website-privacy-scan.jpg'>Large preview</a>)" alt="CookiePro website privacy scan" >}}

<p>After you enter your URL and start the scan, you’ll be asked to provide just a few details about yourself and the company. The scan will start and you’ll receive a notice that says you’ll receive your free report within 24 hours.</p>

<p>Just to give you an idea of what you might see, here are the report results I received:</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d2944227-a58f-4783-814e-292451d56cba/cookie-scan.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d2944227-a58f-4783-814e-292451d56cba/cookie-scan.jpg" sizes="100vw" caption="CookiePro runs a scan on all data collection elements and trackers. (Source: <a href='https://www.cookiepro.com/cookie-consent/'>Cookie Consent</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d2944227-a58f-4783-814e-292451d56cba/cookie-scan.jpg'>Large preview</a>)" alt="CookiePro scan" >}}

<p>As you can see, CookiePro does more than just tell me how many or which cookies my website has. It also includes forms that are gathering data from visitors as well as tags.</p>

<p>Be sure to review your report carefully. If you’re tracking data that’s completely unnecessary and unjustified for a website of this nature to get ahold of, that needs to change ASAP. Why put your clients’ business at risk and compromise visitor trust if you’re gathering data that has no reason to be in their hands?</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/15e88751-9aaa-4584-b008-2caaf85aeaf0/cookiepro-results.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/15e88751-9aaa-4584-b008-2caaf85aeaf0/cookiepro-results.jpg" sizes="100vw" caption="CookiePro’s cookies report tells you what purpose they serve and where they come from. (Source: <a href='https://www.cookiepro.com/cookie-consent/'>Cookie Consent</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/15e88751-9aaa-4584-b008-2caaf85aeaf0/cookiepro-results.jpg'>Large preview</a>)" alt="CookiePro scan results" >}}

<p><em>Note:</em> if you sign up for an account with CookiePro, you can run your own cookie audit from within the tool (which is part of the next step).</p>

### 3. Provide Transparency About Cookie Usage

<p>GDPR isn’t trying to discourage businesses from using cookies on their websites or other marketing channels. What it’s doing, instead, is encouraging them to be transparent about what’s happening with data and then be responsible with it once they have it.</p>

<p>So, once you know what sort of cookies you’re using and data you’re handling, it’s time to inform your visitors about this cookie usage.</p>

<p>Keep in mind that this shouldn’t just be served to EU-based visitors. While those are the only ones protected under the regulation, what could it hurt to let everyone know that their data and identity are protected when they’re on your website? The rest of the world will (hopefully) follow, so why not be proactive and get consent from everyone now?</p>

<p>To provide transparency, a simple entry notice is all you need to display to visitors.</p>

<p>For example, here is one from <a href="https://www.debenhams.com/">Debenhams</a>:</p> 

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/16aabdf6-a202-49df-9099-5e7aa1e96b54/debenhams-cookies.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/16aabdf6-a202-49df-9099-5e7aa1e96b54/debenhams-cookies.jpg" sizes="100vw" caption="This is an example of a cookies notice found on the Debenhams website. (Source: <a href='https://www.debenhams.com/'>Debenhams</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/16aabdf6-a202-49df-9099-5e7aa1e96b54/debenhams-cookies.jpg'>Large preview</a>)" alt="Debenhams cookies notice" >}}

<p>As you can see, it’s not as simple as asking visitors to “Accept” or “Reject” cookies. They’re also given the option to manage them.</p>

<p>To add your own cookies entry banner and advanced options, use CookiePro’s <a href="https://www.cookiepro.com/cookie-consent/">Cookie Consent</a> tool.</p>

<p>Signup is easy &mdash; if you start with the free plan, it takes just a few seconds to sign up. Within an hour, you’ll receive your login credentials to get started.</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/272efcf8-88ad-4f99-ae41-aee341dc9986/cookiepro-dashboard.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/272efcf8-88ad-4f99-ae41-aee341dc9986/cookiepro-dashboard.jpg" sizes="100vw" caption="A peek inside the CookiePro Cookie Consent Dashboard. (Source: <a href='https://www.cookiepro.com/cookie-consent/'>Cookie Consent</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/272efcf8-88ad-4f99-ae41-aee341dc9986/cookiepro-dashboard.jpg'>Large preview</a>)" alt="Cookie Consent dashboard" >}}

<p>Before you can create your cookie consent banner, though, you must add your website to the tool and run a scan on it. (You may have already completed that in the prior step).</p>

<p>When the scan is complete, you can start creating your cookie banner:</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6dd90242-12ad-4a74-88db-7e42cd5cdfb9/create-cookie-banner.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6dd90242-12ad-4a74-88db-7e42cd5cdfb9/create-cookie-banner.jpg" sizes="100vw" caption="Creating a cookie banner within the Cookie Consent tool. (Source: <a href='https://www.cookiepro.com/cookie-consent/'>Cookie Consent</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6dd90242-12ad-4a74-88db-7e42cd5cdfb9/create-cookie-banner.jpg'>Large preview</a>)" alt="Create banner with Cookie Consent" >}}

<p>By publishing a cookie consent banner to your website, you’re taking the first big step to ensuring that visitors know that their data and identity is being protected.</p>

### 4. Make Your Cookie Consent Form Stand Out

<p>Don’t stop at simply adding a cookie banner to your website. <a href="https://www.smashingmagazine.com/2019/04/privacy-ux-better-cookie-consent-experiences/">As Vitaly Friedman explained</a>:</p>

<blockquote>In our research, the vast majority of users willingly provide consent without reading the cookie notice at all. The reason is obvious and understandable: many customers expect that a website ‘probably wouldn’t work or the content wouldn’t be accessible otherwise.’ Of course, that’s not necessarily true, but users can’t know for sure unless they try it out. In reality, though, nobody wants to play ping-pong with the cookie consent prompt and so they click the consent away by choosing the most obvious option: ‘OK.’</blockquote>

<p>While ePR will eventually rid of us of this issue, you can do something about it now &mdash; and that’s to design your cookie consent form to stand out.</p>

<p><strong>A word of caution</strong>: be careful with using <a href="https://www.smashingmagazine.com/2018/04/mobile-pop-up-ads/">pop-ups on a mobile website</a>. Although consent forms are one of the exceptions to Google’s penalty against entry pop-ups, you still don’t want to compromise the visitor experience all for the sake of being GDPR compliant.</p>

<p>As such, you might be better off using a cookie banner at the top or bottom of the site and then designing it really stand out.</p>

<p>What’s nice about CookiePro is that you can customize everything, so it really is yours to do with as you like. For example, here is one I designed:</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/535a445d-5706-4e98-9f46-e1c988a2f9ce/cookie-consent-preview.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/535a445d-5706-4e98-9f46-e1c988a2f9ce/cookie-consent-preview.jpg" sizes="100vw" caption="A preview of a cookie consent banner built with Cookie Consent. (Source: <a href='https://www.cookiepro.com/cookie-consent/'>Cookie Consent</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/535a445d-5706-4e98-9f46-e1c988a2f9ce/cookie-consent-preview.jpg'>Large preview</a>)" alt="Cookie Consent preview" >}}

<p>You can change:</p>

<ul>
  <li>Text color</li>
  <li>Button color</li>
  <li>Background color.</li>
</ul>

<p>You can write your own copy for each element:</p>

<ul>
  <li>Header</li>
  <li>Message</li>
  <li>Cookie policy note</li>
  <li>Cookie policy settings</li>
  <li>Accept button.</li>
</ul>

<p>And you get to decide how the banner will function if or when visitors engage with it.</p>

### 5. Educate Visitors on Cookies

<p>In addition to giving your cookie consent banner a unique look, use it as a tool to educate visitors on what cookies are and why you’re even using them. That’s what the Cookie Settings area is for.</p>

<p>With Cookie Consent, you can inform visitors about the different types of cookies that are used on the website. They then have the choice to toggle different ones on or off based on their comfort level.</p>

<p>That’s what’s so nice about CookiePro taking care of the cookie scan for you. That way, you know what kinds of cookies you actually have in place. All you have to do, then, is go to your Cookie List and choose which descriptions you want to display to visitors:</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f4e77a29-6259-4917-813e-d6e9da3edc97/cookie-list.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f4e77a29-6259-4917-813e-d6e9da3edc97/cookie-list.jpg" sizes="100vw" caption="CookiePro lets you educate visitors about cookies used on the site. (Source: <a href='https://www.cookiepro.com/cookie-consent/'>Cookie Consent</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f4e77a29-6259-4917-813e-d6e9da3edc97/cookie-list.jpg'>Large preview</a>)" alt="Cookie List feature in CookiePro" >}}

<p>Just make sure you explain the importance of the most basic of cookies (“strictly necessary” and “performance) and why you recommend they leave them on. The rest you can provide explanations for in the hopes that their response will be, “Okay, yeah, I’d definitely like a personalized experience on this site.” If not, the choice is theirs to toggle off/on which kinds of cookies they want to be shown. And the Cookie Consent tool can help.</p>

<p>In other words, a cookie consent bar is not some superficial attempt to get consent. You’re trying to help them understand what cookies do and give them the power to influence their on-site experience.</p>

## Wrapping Up

<p>There’s a lot we have to be thankful for with the Internet. It closes geographic gaps. It presents new opportunities for doing business. It enables consumers to buy pretty much anything they want with just a few clicks.</p>

<p>But as the Internet matures, the ways in which we build and use websites become more complex. And not just complex, but risky too.</p>

<p>GDPR and ePR have been a long time coming. As websites gather more data on consumers that can then be used by third parties or to follow them to other websites, web developers need to take a more active role in abiding by the new regulations while also putting visitors’ minds at ease. Starting with a cookie consent banner.</p>

{{< signature "ms, yk, il" >}}
