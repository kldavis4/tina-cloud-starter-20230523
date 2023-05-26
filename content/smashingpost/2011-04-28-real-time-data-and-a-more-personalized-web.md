---
title: 'Real-Time Data And A More Personalized Web'
slug: real-time-data-and-a-more-personalized-web
image: https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9014bf13-33ad-4056-8073-7bacacb2be6b/chartbeat.png
date: 2011-04-28T10:50:18.000Z
author: sam-quayle
summary: >-
  Sam Quayle explores how the best in the Web industry are already adapting to personalization, instant data, and real-time communication. We are living a a new chapter in the evolution of the Web and “real-time data” and a more “personalized Web” mark two milestones. 
description: >-
  Sam Quayle explores how the best in the Web industry are already adapting to personalization, instant data, and real-time communication. We are living a a new chapter in the evolution of the Web and “real-time data” and a more “personalized Web” mark two milestones.
categories:
  - Design
  - Web Design
  - Personalization
---

As Web designers, we face a daily struggle to keep pace with advances in technology, new standards and new user expectations. We spend a large part of our working life dipping in and out of recent developments in an attempt to stay both relevant and competitive, and while this is what makes our industry so exciting to be a part of, it often becomes all too easy to get caught up in the finer details.

<a href="https://www.smashingmagazine.com/2011/01/guidelines-for-responsive-web-design/">Responsive Web design</a>, <a href="https://www.smashingmagazine.com/2010/09/23/html5-the-facts-and-the-myths/">improved semantics</a> and <a href="https://www.smashingmagazine.com/2011/03/02/the-font-face-rule-revisited-and-useful-tricks/">rich Web typography</a> have all seen their fair share of the limelight over the last year, but two developments in particular mark true milestones in the maturation of the Web: “real-time data” and a more “personalized Web.”

{{% feature-panel %}}

Since the arrival of the new Web, we’ve been enraptured by social media. We share links, we “follow,” we “poke,” we’ve become accustomed to it all. Through no fault of our own, we’ve become **lazy users**. The likes of Google, Twitter and Netflix cater to our every desire, serving up instant personalized searches, offering recommendations based on behavioral data and tapping into the preferences of our peers and others with similar tastes. Businesses are beginning to realize that loyal visitors can become volunteer sales forces, and these “anti-defection” measures show a real shift in power toward the user.

Web gurus and industry analysts are simultaneously arriving at the same conclusion: we are entering a new chapter in the evolution of the Web. Many would argue that the future of the Web will be influenced by the growth of the mobile market and location services, and their beliefs would be correct. Both of these, however, are pieces of the bigger picture: personalization, instant data and real-time communication. In this article, I’ll explore how the best in the industry are already adapting to these changes and how Web designers can design for an ever-shortening attention span.

Welcome to the new era.

## Real-Time Data

Serving up real-time data is an effective way to keep users interested and to persuade them to become return visitors. In large corporations, it shows transparency and accountability and can be a great way to facilitate trust and confidence in your brand.

The rise in browser support for the HTML5 canvas element provides the opportunity to display real-time data visualizations without the need for plug-ins&mdash;a technique admirably employed by Ben Sekulowicz-Barclay on his <a href="https://www.beseku.com/">portfolio website</a> (screenshot below). However, support for the element, and various other HTML5 features for that matter, is relatively limited, as full browser support is not yet here. While <code>canvas</code> can easily display relatively simple data visualizations and animations, it was never intended to replace the likes of Flash and Silverlight, which have more tutorials and learning resources and offer greater interactivity to the user.

When considering the implementation of a real-time data visualization, think of your users. For example, what browsers and devices do they use to view your website? What level of support for JavaScript and Flash are built into those browsers (see <a href="https://www.google.com/analytics">Google Analytics</a>). Also, factor in the complexity of your visualization and the user’s need for interactivity before making your decision.

<blockquote>

**Tip:**<br>
When trying to locate the canvas element on the page, you will need to “Inspect element” instead of viewing the page source. When you choose “Inspect element,” you will see that the document tree after the JavaScript has manipulated the DOM and the tree after the browser has applied its corrections.</blockquote>

<figure><a href="https://www.beseku.com/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d635dacc-0f36-4c4c-b760-b70ff73bb204/beseku.png" alt="Ben Sekulowicz-Barclay portfolio website" width="500" height="312" /><figcaption>Ben Sekulowicz-Barclay portfolio website.</figcaption></figure>

2010 saw the knives really come out for Flash, and while browser support for <code>canvas</code> is improving, Flash is still a significant force in real-time data delivery. <a href="https://yesiamprecious.com/">Yes I Am Precious</a> documented a charity bike ride across the US, during which the rider’s tweets, location, speed, temperature, humidity, grade and even cadence were all pulled together to form a great front-end experience. The implementation of an interactive history bar across the top of the website, which showed the status of the bike and the rider at various stages of the journey, let the user “roll back” and “replay” events. Consider this important feature when designing for real-time data; it gives context to the content. The emphasis, though, should always be on real time.

It is worth noting that using <code>canvas</code> or Flash for highly complex visualization or a lot of visualization can be taxing on the CPU and will be slower in browsers without hardware acceleration (which are still the majority).

<figure><a href="https://www.yesiamprecious.com/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8f2aef8b-ac29-41d9-b493-4855a2ad085e/yesiamprecious.png" alt="Yes I am Precious" width="500" height="370" /></a><figcaption>Yes I Am Precious: real-time data.</figcaption></figure>

Stefan Sagmeister’s newly redesigned website offers an interesting alternative: it uses JavaScript to show a real-time feed of his office, with floor-mounted vinyl stickers as the main navigational indicators.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/223c7c2d-6b6c-47c8-a408-153441fa2e85/sagmeister.png" alt="Stefan Sagmeister portfolio website" width="500" height="312" /><figcaption>Stefan Sagmeister portfolio website.</figcaption></figure>

<blockquote>

**Question**: What do Google Analytics and printed newspapers have in common?

**Answer**: They’re both yesterday’s news.</blockquote>

Real-time data is making waves in Web analytics. This new breed of analytics presents owners with instant actionable data and enables them to capitalize on opportunities and mitigate threats.

<a href="https://chartbeat.com/">Chartbeat</a> is one of the best examples of real-time analytics around. Its “bells and whistles” interface is backed up by an alert system that, via SMS, email or its very own iPhone app, informs the publisher of traffic spikes and downtime. The interface presents actionable data to the user, highlighted through the “F”-style layout. Color shades are consistent, headers are clear, and changes in data are designed to be easily recognizable. These are all excellent features to include when designing for real-time data.

<figure><a href="https://chartbeat.com/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9014bf13-33ad-4056-8073-7bacacb2be6b/chartbeat.png" alt="Chartbeat - real-time Web analytics" width="500" height="500" /></a><figcaption>Chartbeat: real-time Web analytics.</figcaption></figure>

Observing the way users interact with your website in real time is one thing, but acting on your findings is another. One option is to implement a Twitter widget like <a href="https://monitter.com">Monitter</a>, which doesn’t require a page refresh to update the feed. Monitter uses jQuery to deliver an asynchronous Twitter feed that you can easily implement on your website. It isn’t “real” real-time, but it’s pretty close, and with the surge in popularity of similar services, it won’t be long before truly real-time APIs and widgets are available. This use of a real-time Twitter widget allows publishers to communicate rapidly with their users and show what people are saying about their product or service.

<figure><a href="https://monitter.com/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f22a3c38-c9e3-4386-a392-baac6cbdd012/monitter1.png" alt="Monitter - real-time Twitter." width="500" height="339" /></a><figcaption>Monitter: real-time Twitter.</figcaption></figure>

For the last two years, <a href="https://collecta.com/">Collecta</a> has provided a real-time search engine, offering free embeddable APIs and publisher widgets. However, Collecta has recently stated that it is shuttering its main product and is now looking in a new direction in the real-time data market. When asked about their reasons for switching direction, CEO Gerry Campbell spoke about what he learned from their two years in business:

<blockquote>“First, there is a huge need for real-time information, Second, a destination site is not the correct vehicle for reaching people. Third, new behaviors, specifically with Facebook and mobile, are growing.”

&mdash; Gerry Campbell, *Collecta*</blockquote>

Interestingly, Collecta’s main competitor, OneRiot, has also recently changed directions, shelving its search engine and moving into online advertisements.

This highlights an important point for the API consumer: always have a back-up plan in case your API provider pulls the plug (as Collecta and OneRiot have done).

<figure><a href="https://collecta.com/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/67db6894-d386-4be9-b8e6-cae70abbdc98/collecta.png" alt="Collecta - real-time information." width="500" height="342" /></a><figcaption>Collecta: real-time information.</figcaption></figure>

Another proclaimed casualty of last year was the RSS feed, partly due to Twitter’s new-found purpose as a news distribution service. However, many believe that RSS is evolving to meet rising user expectations in the new Web climate. <a href="https://pubsubhubbub.appspot.com/">PubSubHubbub</a>, in addition to being quite a mouthful, is an instant publishing and subscription protocol that adds real-time capabilities to your RSS feed. <a href="https://wordpress.org/extend/plugins/pushpress/">PushPress</a> is a particularly useful plug-in that adds PubSubHubbub support to your WordPress RSS feed and allows your push subscribers to receive updates instantly.

One of the main advantages of PubSubHubbub is that it “pushes” new content to your users without the need for crawlers to “poll” (i.e. regularly visit to check for new content) your feed, thus saving CPU and bandwidth. While services such as <a href="https://pingomatic.com/">Ping-O-Matic</a> provide a similar service, subscribers still need visit the URL, which is where PubSubHubbub shines because it requires your server to do less work.

<figure><a href="https://wordpress.org/extend/plugins/pushpress/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e2e42987-0476-4d98-b59f-c69176653e49/pushpress.png" alt="PushPress - Add PubSubHubbub support to your WordPress website" width="500" height="409" /></a><figcaption>Add PubSubHubbub support to your WordPress website.</figcaption></figure>

It is important to recognize that the successful delivery of real-time data relies heavily on the integrity of the data. While vetting and backing up data are sound practices for any publisher (real time or not), serving up data in real time increases the importance of their adoption. The need to curate and filter data is also important when considering your website’s performance. When delivering real-time data, you want to keep client-side processing to a minimum and do whatever processing you can on your server. This way, you are only sending the user data that is useful to them, and you are optimizing the speed of your website.

On smaller shared servers, you will need to keep the volume of data small to adhere to bandwidth limits and ensure that your server isn’t spending too much time processing data in order to save CPU. If this limits your options, you could always upgrade your hosting package or use a third-party service such as <a href="https://kwwika.com/">Kwwika</a>, which will keep processing off your server.

{{% ad-panel-leaderboard %}}

## A More Personalized Web

<blockquote>“Every two days, we create as much information as we did up to 2003.”

&mdash; Eric Schmidt, then-CEO of Google</blockquote>

Although there are many positives to the rapid growth of user-generated content over the last few years, there are of course some corollary effects of the “content tiger.” Users are quickly becoming overwhelmed by the sheer volume of information being presented to them, with the increase in real-time data further weakening the “signal-to-noise” ratio. In an attempt to alleviate these problems and better organize the mass of information and data available, developers and content providers of the future will thrive by **making relevant information find the user**, as opposed to the user having to find the information relevant to them (bringing the mountain to Mohammad).

While catering to unique visitor segments and personalizing user experience is nothing new, its relevance has never been more important, and the technologies available to us have never been better. As the user becomes even more accustomed to these personalized touches, the bar of user expectation will once again rise, leaving behind sluggish publishers and retailers that are slow to adapt their online strategy.

Not only is this further shift towards a more personalized user experience becoming a necessity for our bombarded user, it also demonstrates, more interestingly, a measurable shift in consumer behavior. I presume that most of you will get your hair cut a few times this year. How many of you go to a particular salon or barber shop? How many of you even have a preferred hairdresser at that location? I know I do, and I return to this particular hairdresser month after month not for the complimentary light literature and cup of coffee, nor even for the quality of the haircut. I return because the service is personalized&mdash;a concept lost on some businesses.

Instead of looking after existing clientele, these businesses choose to put all their resources into pursuing new business. The method of targeting individual users based on their profile histories and the profiles of others has been fervently exploited by the e-commerce market. Savvy companies realize that **traditional marketing and advertising methods no longer exclusively drive consumer behavior**, and they are instead turning their attention to personalizing their services and investing in word of mouth. These companies are giving users both the inspiration and tools to talk about their products and share them across various social networks. Seth Godin coined a term for this process: <a href="https://sethgodin.typepad.com/seths_blog/2006/01/flipping_the_fu.html">flipping the funnel.</a>

<a href="https://www.netflix.com/">Netflix</a> was one of the first to implement a recommendations engine on its website. In addition to recommendations, there’s a “Friends” tab where the user can see what their friends are watching in order to compare interests. Recommendation engines use specific types of information filtering to present items (movies, products, etc.) that are likely to interest the user. When implementing such a mechanism, you must first understand the data, content and user’s intent. Recommended results should be visually defined and supplemented with a clear marketing message, and you should always be aware of data-shift issues. Although this type of technology may seem out of reach to small businesses and their developers, it is still possible on a smaller budget.

<a href="https://rads.stackoverflow.com/amzn/click/0596529325" rel="nofollow">Programming Collective Intelligence</a> is probably a good staring point for anyone looking to implement such functionality.

<figure><a href="https://www.netflix.com/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3a8f0a2a-f412-4286-876d-bd66398602dd/netflix.png" alt="Netflix - Watch TV Shows Online, Watch Movies Online" width="500" height="444" /></a><figcaption>Netflix was one of the first to implement a recommendations engine on its website.</figcaption></figure>

In June of last year, Facebook CEO Mark Zuckerberg commented at London's Barbican Centre on the potential of “products built around people” and spoke of the company’s “aggressive expansion” into the “personal Web.” Facebook's “Connect” APIs allow websites to connect with a Facebook user’s identity, profile information and even information about the user’s friends. These APIs provide an alternative to the sign-up process, social context, personalized content and other means of customer service communication.

Allowing users to share content across a variety of social platforms is an effective way to reach a large targeted audience. Social “sign-ins,” commenting, content sharing, widgets and APIs are all effective methods of optimization. Social optimization is beginning to rival search engine optimization in importance in the world of online marketing. A recent survey by <a href="https://pewresearch.org/pubs/1508/internet-cell-phone-users-news-social-experience">Pew</a> found that 75% of news consumed online was via links on social networking websites or in email.

<figure><a href="https://developers.facebook.com/docs/coreconcepts/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/16415a72-109c-4044-89e2-4228e992ea51/facebook-permission.jpg" alt="Facebook Connect" width="530" height="333" /></a><figcaption>Facebook Connect.</figcaption></figure>

The new <a href="https://www.bbc.co.uk">BBC</a> website is one of my favorite examples of a personalized user experience. The user can drag and drop various news widgets around the home page, remove them completely or customize the content that each widget serves. The website is optimized for social networks, but I feel that the sharing utilities could be slightly more user-friendly. Another step some companies have taken is to re-arrange content and navigation based on user profiles. While this can be convenient for the user, it can also put them off and have a negative effect on usability. For this type of personalization to work effectively, publishers should ensure that they build comprehensive customer profiles before creating rules to target user preferences.

<figure><a href="https://www.bbc.com/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d889db6b-bf0f-4f41-9991-85061a3fcfa6/bbc.png" alt="BBC home page" width="500" height="370" /></a><figcaption>BBC Home page.</figcaption></figure>

Reviews and comments are another way to engage and empower visitors. If your business delivers a good product or service, then they allow users to share their reviews over numerous social platforms. It’s the perfect breeding ground for customer evangelism.

<figure><a href="https://www.tripadvisor.com/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/62f495f8-c256-48e9-866f-c733e81dd00e/tripadvisor.png" alt="Trip advisor" width="500" height="339" /></a><figcaption>Trip advisor: reviews and comments as a way to engage and empower visitors.</figcaption></figure>

In addition to optimizing your website for mobile use or creating an app, personalize your service by targeting users according to their location. Recently, Google’s Marissa Mayer told <a href="https://www.mediabistro.com">Media Bistro</a> that Google’s focus at the local level is to use location to help searchers find what they’re looking for. Google’s interest in the local market led to an attempted acquisition of <a href="https://www.groupon.com">Groupon</a>, a discount provider that has been particularly successful in targeting users by location and socially optimizing its services.

<figure><a href="https://www.groupon.com/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6bf45110-9aa3-4c21-a9de-2876dc363b55/groupon.png" alt="Find Great Deals on Fun Things to Do" width="500" height="370" /></a><figcaption>Groupon website.</figcaption></figure>

## Summary

While this cataclysmic shift in the evolution of the Web and the role of the user is welcomed by most, others argue that focusing on providing a personalized Web experience creates an echo chamber of information, opinions and ideas. Is the outsider’s perspective getting lost? Are user expectations of “real time” becoming unrealistic? And could pandering to these expectations contribute to our own downfall? Regardless of the continuing importance of a static Web presence and the infancy of these new technologies, serving up the same stale content to everyone is, without question, no longer enough.

{{% ad-panel-leaderboard %}}

### Other Resources

**Real-Time Data:**

*   “[Real-Time Data Visualization Using Flex](https://ria.dzone.com/articles/flex-data-visualization)”
*   “[Real-Time Heat Map Example With JavaScript and HTML Canvas](https://www.patrick-wied.at/static/heatmap/)”
*   [jQuery-accessible charts](https://www.filamentgroup.com/lab/update_to_jquery_visualize_accessible_charts_with_html5_from_designing_with/)
*   [Chartbeat’s design process](https://www.web2expo.com/webexny2010/public/schedule/detail/15668)
*   “[Weekend Project: Add PubSubHubbub Syndication to Your Website or Blog](https://www.linux.com/learn/tutorials/382878:weekend-project-add-pubsubhubbub-syndication-to-your-site-or-blog)”
*   [Phil Leggetter](https://www.leggetter.co.uk/), real-time data evangelist

**A Personalized Web:**

*   “[HTML5 Apps: Positioning With Geolocation](https://mobile.tutsplus.com/tutorials/mobile-web-apps/html5-geolocation/)”
*    [Word of Mouth Marketing Association blog](https://womma.org/word/)
*   “Social + Algorithms = Personalized Web”
*   “[How to: Integrating Facebook in Your Website](https://www.1stwebdesigner.com/tutorials/facebook-integrate/)”
*   “[5 Predictions for APIs in 2011](https://gigaom.com/cloud/5-predictions-for-apis-in-2011/)”
*   “[Facebook eCommerce Success](https://info.gigya.com/WP.FBES.html)”

## Related Articles

You might want to read the following related articles as well:

*   [Designing For The Future Web](https://www.smashingmagazine.com/2011/03/29/designing-for-the-future-web/)
*   [Holistic Web Browsing: Trends Of The Future](https://www.smashingmagazine.com/2010/04/10/holistic-web-browsing-4-trends-of-the-future/)

### Further Reading

*   [Driving App Engagement With Personalization Techniques](https://www.smashingmagazine.com/2016/09/driving-app-engagement-with-personalization-techniques/)
*   [Privacy Guidelines For Designing Personalization](https://www.smashingmagazine.com/2016/03/privacy-for-personalization/)
*   [How Artificial Intelligence Is Changing Design](https://www.smashingmagazine.com/2017/01/algorithm-driven-design-how-artificial-intelligence-changing-design/)
*   [Conversational Interfaces: Where Are We Today? Where Are We Heading?](https://www.smashingmagazine.com/2016/07/conversational-interfaces-where-are-we-today-where-are-we-heading/)

{{< signature "al, mrn" >}}
