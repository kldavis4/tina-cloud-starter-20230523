---
title: Legal Guidelines For The Use Of Location Data On The Web
slug: location-data-web-development-and-the-law
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5c94ad2e-abcf-4e91-a586-b5c58a494f3e/03-location-allow-preview-opt.png
date: 2016-03-10T17:39:09.000Z
author: heather-burns
summary: >-
  Location-based services are growing in popularity every day, and beacon-based services are tipped to be the advertising goldmine of 2016. You may already be using location data and beacons to enhance your users’ experience with your websites, apps and wearables. However, the use of location data is not without limits.
description: >-
  You may already be using location data and beacons to enhance your users’ experience with your websites, apps and wearables. However, the use of location data is not without limits.
categories:
  - Ethics
  - User Interaction
  - Security
  - Privacy
---

Developers must become aware of international privacy laws, as well as industry codes of self-regulation, that govern its usage. Following laws and codes, while also adhering to best practice principles through frameworks such as privacy by design (PbD), will ensure public trust in your app as well as in your services as a developer.

If you are creating a website, app or wearable that uses location data, building in responsible development and regulatory compliance from the very beginning is easy. This article will teach you how to build <strong>a healthy workflow for developing with location data</strong> by using best practice frameworks, providing users with privacy-friendly options, coding to development guidelines and working with an insightful regard for the law. By following this advice, you can create a responsible and legally compliant development process.

## What Is Location Data And Why Is It So Controversial?

A <em>location-based service</em> (LBS) is defined as a service where

*   the user is able to determine their location,
*   the information provided is spatially related to the user’s location,
*   the user is offered dynamic or two-way interaction with the location information or content.

These apps can tell you where your friends are checked in, help you locate your favorite coffee chain or even help you find the nearest wheelchair-accessible restroom. For example, Euan’s Guide, a travel resource for people with disabilities, allows users to note their current location. By providing information on wheelchair- and disability-friendly facilities in a user’s immediate area, the website has opened up a world of opportunities to people who were previously reluctant to travel far from home.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/02ef3d10-3976-4a39-8ed3-9b5cdd0ab2e4/01-euansguide-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/02ef3d10-3976-4a39-8ed3-9b5cdd0ab2e4/01-euansguide-preview-opt.png" alt="Euan’s Guide, a travel resource for people with disabilities, allows users to note their current location" /></a><figcaption>Euan’s Guide, a travel resource for people with disabilities, allows users to note their current location.</figcaption></figure>

When an LBS is mixed with other data sources — a pharmacy’s loyalty card records, for example — this is known as <a href="https://www.nytimes.com/2015/12/31/technology/personaltech/video-feature-the-mood-in-2016-sleek-and-to-the-point.html">beacon-based marketing</a>. These services can do things like offer you a discount on your favorite shampoo when you walk past a branch of the pharmacy.

While location-based services are a developer’s dream, they clearly have the potential to become a privacy nightmare. The law firm Taylor Wessig <a href="https://united-kingdom.taylorwessing.com/globaldatahub/article_intro_wearable_technology.html">uses the example</a> of Google Glasses combining location data with facial-recognition technology to “turn the public into paparazzi.” What’s worse, in countries with no overarching privacy legislation, little prevents users’ location data from being <a href="https://www.techrepublic.com/article/the-dark-side-of-wearables-how-theyre-secretly-jeopardizing-your-security-and-privacy/">transferred to data brokers</a> without their consent.

Developers cannot solve these complex and troubling issues on their own. However, there are many steps you can take to help users make better decisions about how to use your app, what data they can allow your app to collect and how they want their data to be used.

{{% feature-panel %}}

## Best Practices In Location-Based Data Projects

### Frameworks

The process of ensuring good location-data privacy starts before you begin to code. The best way to do this is through a workflow known as privacy by design (PbD). PbD is an approach to web development that takes privacy into account from the very beginning across all aspects of a project, rather than bolting it on at the end in “Settings.” The principles pertaining to location data within the <a href="https://www.ipc.on.ca/wp-content/uploads/Resources/pbd-ip-geo.pdf">framework</a> (PDF, 1 MB) are an excellent starting point. What’s more, the EU’s data-protection reform, which should come into effect in 2018, will include PbD requirements as part of the law — so, there’s no time like the present to begin integrating PbD in your workflow.

Another great resource is the Application Data Privacy project which offers best practice guides arranged by OS, platform, app store, operator, and IoT and home devices. We were also very impressed by the <a href="https://www.oaic.gov.au/agencies-and-organisations/guides/guide-for-mobile-app-developers">Australian government’s guide</a> on mobile privacy for app developers.

Whichever framework you choose, using one of them will give you a consistent work plan and set of checklists to follow throughout your location data projects.

### Contracts and Privacy Policies

The misuse of location data, whether intentional or not, can have serious legal consequences for both you and your client. To protect yourself, the use, processing and retention of location data should be addressed in your project contracts. You and your client should clarify how location data will be used, where it will be stored and what third parties will be granted access to it (more on that later). A robust contract would go further to confirm that no uses of location data will violate the laws of the user’s country. This may require your client to appoint a lawyer in countries where your app is targeted in order to clarify that your work will meet local, national and international data-protection and -privacy laws.

Your LBS and beacon-based marketing projects should include a privacy policy in the app, on the client’s website and on your own website as well. That privacy policy should detail what is done with location data, how that data is shared between the content provider, the mobile provider and any third parties such as ad networks, and how the user can revoke their consent to the use of their data. The privacy policy should be written in clear, plain language and include contact information for where users can raise any concerns they have. A sample privacy policy, along with many other useful resources, is available on the website of the <a href="https://www.mmaglobal.com/documents/mma-mobile-application-privacy-policy-framework">Mobile Manufacturing Association</a>.

### Third-Party Services

If your app will be using third-party services such as advertising or social media integration, clarify what use those third parties make of location data and whether your users’ location data will be combined with any other personal data by the third parties. If your website, app or wearable uses social log-in or sharing buttons, location data will very likely be passed to these social networks, and you may wish to remove these services from the areas of your project that use LBS.

Recently <a href="https://www.telegraph.co.uk/technology/apple/iphone/11941323/Hundreds-of-iPhone-apps-to-be-removed-from-Apple-App-Store-for-illegally-collecting-your-private-information.html">several hundred iOS apps were pulled from the App Store</a> after security researchers found that the apps were surreptitiously uploading users’ private data to a mobile ad provider in China. Critically, the developers of the affected apps were unaware of the violation and had no access to the siphoned data. All they had done was use the ad network in question to place ads in the apps. The information that the ad network was collecting could easily be paired with any location data used within the apps or even on the mobile devices themselves.

The Chinese experience shows that it is important to carefully examine what data your apps are passing to third parties, including location data, <strong>even if your client does not use any of that data themselves</strong>.

{{% ad-panel-leaderboard %}}

## Privacy-Friendly Options In Location Data

Once you have decided on a project framework and protected yourself contractually, there are many options you can use to make your location-based app more privacy-sensitive by design. Location data specialists <a href="https://manning-content.s3.amazonaws.com/download/b/a4de039-2cd5-4be1-8ba2-4c73af18be78/LAAsample_ch10.pdf">Richard Ferraro and Murat Aktihanoglu</a> (PDF, 1.17 MB) suggest five options.

### User Profiles

Allow an app’s users to control what permissions are requested, what data is collected and what data is shared. For example, while I use a step-counter app on my phone, I have deactivated location data in the app, so that the app only measures how much I walk, not where.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ffc30bdf-a5ad-4594-8d76-939ce99368a0/02-trainline-scotrail-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/17500c4c-6010-4f58-98ca-1f76d395fdf7/02-trainline-scotrail-preview-opt.png" alt="Another example of providing options for location data in user settings." /></a><figcaption>Another example of providing options for location data in user settings. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ffc30bdf-a5ad-4594-8d76-939ce99368a0/02-trainline-scotrail-opt.png">View large version</a>)</figcaption></figure>

Here is another example of providing options for location data in user settings: The app on the left allows me to turn location services on or off in the settings. The app on the right requires location data to be turned on by default. The latter app still demonstrates good privacy practice by informing me of its location-data requirements before I install the app, and it gives me the option to cancel the installation if I do not agree with it.

### Opt-In Screens

These are the familiar pop-up screens stating that the app “wants to use your current location.” These screens should be used in conjunction with app settings or user profiles.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5c94ad2e-abcf-4e91-a586-b5c58a494f3e/03-location-allow-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5c94ad2e-abcf-4e91-a586-b5c58a494f3e/03-location-allow-preview-opt.png" /></a><figcaption>A simple opt-in screen</figcaption></figure>

### Fuzzy Locations

This transmits an approximate location, such as a city, rather than a specific point in that city. This can be useful in situations where personal safety may be a consideration. One fascinating example of this is an <a href="https://www.manchestereveningnews.co.uk/news/reason-digitals-safety-nets-app-9811425">app for sex workers in Manchester</a>, England, which the workers use to alert each other to dangerous and violent customers.

### Terms of Service

Limit the time that a user’s location history is stored, and give them the option to delete any or all location records at any time.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7f8d3258-d93f-432f-83a3-00a2c2f29b79/04-twitter-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3608d75e-5198-42c7-a9aa-500ea970cdc9/04-twitter-preview-opt.png" alt="Twitter allows users to delete all geolocation data at any time." /></a><figcaption>Twitter allows users to delete all geolocation data at any time. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7f8d3258-d93f-432f-83a3-00a2c2f29b79/04-twitter-opt.png">View large version</a>)</figcaption></figure>

### Geofencing

You can block certain areas from being readable by an app’s location data, or give the user the option to block them. For example, in a check-in app, a user’s home and school locations should always be set to private by default.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b38b7893-56e3-4bee-a017-59da9e951070/05-geofence-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e9430ba7-1eb3-48ed-ae38-d17e3308805a/05-geofence-preview-opt.png" alt="While few users know what the word “geofencing” means, making users aware of it as an option is good privacy practice." /></a><figcaption>While few users know what the word “geofencing” means, making users aware of it as an option is good privacy practice. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b38b7893-56e3-4bee-a017-59da9e951070/05-geofence-opt.png">View large version</a>)</figcaption></figure>

## Guidelines For Developers

The developer guidelines for the three major app platforms demonstrate three very different approaches to privacy.

### iOS

Apple’s <a href="https://developer.apple.com/library/ios/documentation/UserExperience/Conceptual/LocationAwarenessPG/CoreLocation/CoreLocation.html#//apple_ref/doc/uid/TP40009497-CH2-SW16">developer guidelines for location-based apps</a> suggest that “with a few exceptions, avoid starting location services immediately at launch time or before such services might reasonably be used. Otherwise you might raise questions in the user’s head about how your app uses location data." Making the activation of location data conditional on other actions, rather than continuous from startup, is a simple way to give users control over their data. Additionally, Apple’s <a href="https://developer.apple.com/videos/play/wwdc2015-703/">2015 WWDC seminar on app privacy</a> specifically cites the use of location data as a legal risk to developers and suggests using randomly generated UUIDs as a safeguard.

### Android

As Evgeny Morozov explains in his book <em>To Save Everything, Click Here</em>:
<blockquote>“Google relies on GPS-enabled Android phones to generate live information about traffic conditions: once you start using its map and disclose your location, Google knows where you are and how fast you are moving.”</blockquote>

<a href="https://developers.google.com/maps/documentation/android-api/location?hl=en#location_permissions">Google’s developer guidelines for Android</a> require location-data permissions in apps. There are two options: coarse location, which uses mobile data beacons to identify a location within an area approximately the size of a city block, and fine location, which uses GPS to identify a location as precisely as possible.

Google also provides separate <a href="https://developer.android.com/training/articles/wear-permissions.html">location-data privacy guidelines for wearables</a>.

### Windows Phone

<a href="https://msdn.microsoft.com/en-us/library/windows/apps/hh768223.aspx">The Windows app developer guidelines</a> take a PbD approach by placing questions about the necessity and use of location-based data <em>first</em>, and only <em>then</em> offering the <a href="https://msdn.microsoft.com/en-us/library/system.device.location%28v=vs.110%29.aspx">requisite code resources.</a>

{{% ad-panel-leaderboard %}}

## What Does The Law Require You To Do?

### Europe

In Europe, location data is regulated by a 2002 law called the <a href="https://eur-lex.europa.eu/LexUriServ/LexUriServ.do?uri=CELEX:32002L0058:en:HTML">Directive on Privacy and Electronic Communications</a>. This law has been implemented in national legislation in all EU member states. It essentially states the following:

*   Location data should only be used when it is anonymized (i.e. it cannot be associated with any particular individual).
*   If it is not anonymized, the user must give their consent for their location data to be used and accessed. Additionally, the user must be able to withdraw their consent at any time. In practice, an app store’s terms and conditions often decree that downloading an app equates to consent to its use of location data, although privacy-friendly apps take that a step further by adding the option to disable location data within the app’s settings.
*   The service provider should inform the user what location data will be collected and processed, what it will be processed for and whether it will be transmitted to any third parties, including social media websites. Any transmission of data to a third party must also be anonymized.
*   Users should be able to temporarily stop the use of location data, even if they have previously given consent.
*   Location data should only be used for a specific reason, and only for the duration necessary for the purpose.

All processing and retention of location-based data is, of course, further governed by the <a href="https://eur-lex.europa.eu/LexUriServ/LexUriServ.do?uri=CELEX:31995L0046:en:HTML">EU Data Protection Directive</a> of 1995. This law is currently undergoing a major overhaul, and the revision is expected to come into effect in 2018, with tighter restrictions on data usage, as well as PbD requirements in all projects.

### United States

The two major laws governing the use of location data in the US are the <a href="https://it.ojp.gov/privacyliberty/authorities/statutes/1285">Electronic Communications Privacy Act of 1986</a> and the <a href="https://it.ojp.gov/PrivacyLiberty/authorities/statutes/1288">Communications Act of 1934</a> (you read that right: 1934). It is difficult to fathom what relevance these radio-era laws have to today’s problems of unauthorized use of location data in apps, and it may explain the lack of consideration for the appropriate use of location data in many popular platforms.

Industry self-regulation is a partial attempt to bridge the gap left by the lack of legislation. The Federal Trade Commission’s <a href="https://www.ftc.gov/sites/default/files/documents/reports/federal-trade-commission-staff-report-self-regulatory-principles-online-behavioral-advertising/p085400behavadreport.pdf">Behavioral Advertising Principles</a> (PDF, 411 KB) suggest that app developers should seek to obtain consent before using location data. This is, of course, a best practice and not a law.

As of this writing, there are <a href="https://www.gps.gov/policy/legislation/gps-act/">five separate draft bills</a> regarding the uses of location data across various sectors and situations. There is also a draft consumer rights bill, the <a href="https://cdt.org/blog/consumer-privacy-protection-act-is-data-breach-legislation-we-can-support/">Consumer Privacy Protection Act</a>, which would govern the use of location data. This law would override any <a href="https://cdt.org/insight/survey-of-state-location-privacy-legislation/">state-specific laws on location data</a>, and its progress is worth keeping an eye on.

While some form of regulation on location data is clearly coming soon in the US legal system, developers should not wait for legislation to implement best practices. Indeed, a lack of legislation should never be taken to mean a lack of concern. A <a href="https://www.pewinternet.org/2013/09/05/part-4-how-users-feel-about-the-sensitivity-of-certain-kinds-of-data/">2013 study of American Internet users</a> carried out by the Pew Research Centre found that over half of all respondents feel that having control over their location data is important. Responsible web development practice should meet those needs regardless of the lack of legal compulsion.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/363db2a1-2fdd-478a-9708-ea49aab1f803/06-pewdata-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/de8df017-c80c-4570-8392-4fe3b8557cbf/06-pewdata-preview-opt.png" alt="2013 study of American Internet users" /></a></figure>

2013 study of American Internet users. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/363db2a1-2fdd-478a-9708-ea49aab1f803/06-pewdata-opt.png">View large version</a>)

Public concern over control of location settings is indicated in the bars for “Place you are located when you use the internet.” Unlike in Europe, Americans have no national privacy law to meet these concerns, making privacy-sensitive development even more important for US audiences.

## Developing With Confidence

To summarize, you can achieve successful location-based projects by doing the following:

*   Adopt a best-practice framework in your workflow, such as the privacy-by-design principles.
*   Protect yourself legally by clarifying issues of data protection and privacy in your project contracts.
*   Investigate how third parties access and use location data and whether that data is being aggregated with any other personally identifiable data.
*   Use development guidelines to code responsibly and efficiently.
*   Develop your projects in a way that gives users the greatest possible control over the uses of their location data at any time.
*   Stay alert to changes in legislation affecting the uses of location data, such as the upcoming European data-protection reform.

### Further Reading

*   _Location-Aware Applications_, Richard Ferraro and Murat Aktihanoglu (Shelter Island: Manning Publications, 2011)
*   _The Net Delusion: The Dark Side of Internet Freedom_, Evgeny Morozov (London: Penguin, 2011)
*   _The People’s Platform: Taking Back Power and Culture in the Digital Age_, Astra Taylor (New York: Picador, 2014)

### <span class="rh">Related Reading</span> on SmashingMag:

*   [Entering The Wonderful World of Geo Location](https://www.smashingmagazine.com/2010/03/entering-the-wonderful-world-of-geo-location/)
*   [Maps In Modern Web Design: Showcase and Examples](https://www.smashingmagazine.com/2010/04/maps-in-modern-web-design/)
*   [Improve User Experience With Real-Time Features](https://www.smashingmagazine.com/2016/04/improve-user-experience-real-time-features/)
*   [Redesigning The Country Selector](https://www.smashingmagazine.com/2011/11/redesigning-the-country-selector/)

{{< signature "da, jb, ml, al" >}}
