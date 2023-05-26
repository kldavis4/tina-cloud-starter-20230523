---
title: 'World Wide Web, Not Wealthy Western Web (Part 2)'
slug: world-wide-web-not-wealthy-western-web-part-2
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/15e400b6-3274-4e6e-864a-d75fdae43b80/mobile-phones-world-graphy-opt.png
date: 2017-03-13T19:07:19.000Z
author: bruce-lawson
description: >-
  In [part
  1](https://www.smashingmagazine.com/2017/03/world-wide-web-not-wealthy-western-web-part-1/)
  of this article, we looked at where in the world the new entrants to the World
  Wide Web are, and some of the new technologies the standards community has
  worked on to address some of the challenges that the next 4 billion people are
  facing when accessing the web. In short, we've tried to make some supply-side
  improvements to web standards so that websites can be made to better serve
  the whole world, not just the wealthy West.
categories:
  - Browsers
  - Web Design
  - Responsive Design
  - User Research
---
But there are other challenges to surmount, such as ways to get over creaky infrastructure in developing markets (which can be done with stopgap technological solutions, such as proxy browsers), and we'll also look at some of the reasons why some of the offline billions remain offline, and what can be done to address this.</p>

## Proxy Browsers

A common problem people encounter in emerging economies relates to networks. Networks are getting better, but they're not there yet. In 2016, <a href="https://www.ericsson.com/thinkingahead/consumerlab/consumer-insights/experience-shapes-mobile-customer-loyalty">Ericsson reported</a>:

<blockquote>While cellular networks have improved… smartphone users are still facing issues as frequently as they did in 2013. Globally, 26 percent of smartphone users say they face video streaming issues daily, increasing to over one third in markets like Brazil, India and Indonesia.</blockquote>

{{% feature-panel %}}

This is an excellent statement of the problem. Infrastructure is expensive to upgrade, especially in countries like Indonesia, which is made up of thousands of islands, and India, which is huge and has vast mountain ranges. And as soon as infrastructure is upgraded, more people come online and want to consume video rather than boring old text, and so much more bandwidth is required, and the newly upgraded network crawls again.

In places where bandwidth is seriously constrained (in congested Asian megacities, not just rural areas; I'm in the heart of an Indian city with an international airport, and power cuts and Internet outages occur daily), a lot of people opt to use proxy browsers. Proxy browsers do a lot of the heavy lifting of rendering web pages on their servers and sending compressed versions down to the user, resulting in often significant reductions in data consumption. This is obviously a very appealing proposition for consumers in territories where bandwidth is expensive. Because the data transferred is smaller, websites render faster, too.</p>

<a href="https://data.wurfl.io/MOVR/pdf/2016_q1/MOVR_2016_q1.pdf">Scientia Mobile reported</a> in 2016 that, for global market share of proxy browsers, Opera Mini is at 42%, Opera Turbo is at 9%, Chrome is at 39% and UCWeb is at 6%, and there is also Puffin, Silk and others. Opera reports more than 250 million active monthly users of Opera Mini.

Websites compressed by proxy browsers and sent as binary blobs also have a better chance of getting through congested networks. In 2013, Avendus reported (in "India's Mobile Internet: The Revolution Has Begun," no longer online):

<blockquote>In India, only 96k of the 736k cell towers are 3G enabled… only 35k of those towers have a fiber-optic connection to the backbone.</blockquote>

(If you're a real networking anorak, you'll find the report <a href="https://docs.google.com/presentation/d/1fZ7ftsJJ4adiPov4y_8AtV_zjqAmEASaSxRBHBwkiOw/edit#slide=id.g73cf3c208_0_158">2G Network Issues Observed While in India</a> to be even more fun than a game of Werewolf at a Star Wars convention.)

### Limitations of Proxy Browsers

So, if proxy browsers are so great, why doesn't everyone use them? The answer is that such compression comes at a cost; websites can look very different in a proxy browser, and JavaScript can often behave unexpectedly.

In a proxy browser, everything happens on the server, everything needs user interaction, and everything needs a round-trip to the server. Opera Mini on Android and iOS has two modes; one uses proprietary compression techniques and the device's standard web view, and thus JavaScript isn't affected. In Opera Mini's extreme mode, all of the rendering is done on Opera's server farms, on which JavaScript is allowed to run for 5 seconds and then is throttled. (Disclosure: I was Deputy CTO of Opera until November 2016 and can talk authoritatively about its technology. However, I have no relationship with the company now.)

Therefore, to make websites work in Opera Mini's extreme mode, treat JavaScript as an enhancement, and ensure that your core functionality works without it. Of course, it will probably be clunkier without scripts, but if your website works and your competitors' don't work for Opera Mini's quarter of a billion users, you'll get the business.

Mini's extreme mode has design constraints, too: it doesn't do CSS rounded corners or gradients, because it can't rely upon every client device to draw those things successfully; so, to render it on the server, it would need to convert them into bitmaps, which would bloat the page. But that's OK; CSS is for design, and people in highly bandwidth-constrained situations are happy to get the words.

Similarly, Mini's extreme mode doesn't do CSS or SVG animations, only showing the first frame. The reason for this is that animations consume CPU cycles, and CPU cycles consume battery. Yes, your animations are lovely, but if you are sitting on a bus in Lagos in a traffic jam and need to phone your sister to ask her to pick up your children from school, you need that battery life more than you need pretty animations.

Neither does Mini's extreme mode download web fonts, which can be huge files that are primarily for aesthetics. On many very small monochrome screens, the system fonts tend to be designed for those screens and work better. If you want icons, use SVG rather than icon fonts because, well, that's what SVG is for.</p>

## Revolutionary New Development Technique

The best way to ensure that your website or web app (is there a real difference?) will work for people on proxy browsers, conventional browsers with very slow connections and everyone else is to adopt a revolutionary new development methodology.

Airbnb tried it with its new app and <a href="https://nerds.airbnb.com/weve-launched-our-first-nodejs-app-to-product/">wrote excitedly</a>:

<blockquote>… we've launched our first Holy Grail app… It looks exactly the same as the app it replaced, however initial pageload feels drastically quicker…</blockquote>

What voodoo magic did they employ?

<blockquote>… we serve up real HTML instead of waiting for the client to download JavaScript before rendering. Plus, it is fully crawlable by search engines.… It feels 5x faster.</blockquote>

Who knew? The best way to ensure that everyone gets your content is to write real, semantic HTML, to style it with CSS and ensure sensible fallbacks for CSS gradients, to use SVG for icons, and to treat JavaScript as an enhancement, ensuring that core functionality works without scripts. Package up your website with a manifest file and associated icons, add a service worker, and you'll have a progressive web app in conforming browsers and a normal website everywhere else.

I call this amazing new technique "progressive enhancement."

You heard it here first, folks!

## What If We Threw A Party And Nobody Came?

We have supply-side improvements such as HTML responsive images, progressive web apps, renewed CSS work on vertical text. We have the methodology of progressive enhancement. We have proxy browsers that compress websites for people in low-bandwidth and expensive data plans. We have an explosion of ever-cheaper smartphones (and I'm not talking about the Galaxy Note 7 here). So, why aren't the next 4 billion already on the web?

There are demand-side problems in emerging markets.

One of those is that the market for smartphones is either <a href="https://www.mobileworldlive.com">flat</a> or <a href="https://www.strategyanalytics.com/strategy-analytics/blogs/devices/smartphones/smart-phones/2016/04/28/global-smartphone-shipments-decline-3-percent-in-q1-2016#.VyIu60GNL-Q">declining</a>, depending on which statistics you read. There are many potential reasons for this: the slowdown in the Chinese economy (China, India and the US are the <a href="https://businesskorea.co.kr/article/10453/poor-performance-samsung-phones-struggling-india-china">largest consumers of smartphones</a>); it could be a classic case of market saturation — everyone who wants a smartphone and can afford one already has one.

It could also have to do with devices like the one shown below, which was given to me at the Mobile World Congress SynergyFest.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e54262a6-8aee-494f-9b26-7c439d4dd59b/pt2-www-img2-lawson-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/24394fea-f695-423c-9490-3dc98b225836/pt2-www-img2-lawson-800w-opt.png" alt="$2.36 feature phone" width="800" height="600" /></a><figcaption>$2.36 feature phone (photo by the author) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e54262a6-8aee-494f-9b26-7c439d4dd59b/pt2-www-img2-lawson-large-opt.png">View large version</a>)</figcaption></figure>

It's a feature phone, made in China; it doesn't have Wi-Fi but is dual-SIM (very important in places like Africa and Asia); it has an FM radio; and it can connect to the web with a WAP-like browser. Its retail price in Africa and Latin America is $2.36 USD.

In a country like Cambodia, where a garment worker's <a href="https://business-humanrights.org/en/cambodia-2015-minimum-wage-negotiations">minimum wage is $140</a> a month, or Liberia, where an unskilled worker's <a href="https://www.liberianobserver.com/politics/passed-minimum-wage-set-us6day">minimum wage is $4</a> a day, even a $60 to $70 entry-level smartphone is practically unaffordable. But $2.36? That's affordable.

But it is not just affordability that stops people from coming to the web. As <a href="https://www.gsmaintelligence.com/research/2016/07/consumer-barriers-to-mobile-internet-adoption-in-africa/568/">GSMA Intelligence wrote</a> in July 2016:
<blockquote>Despite the fact that Africa has the lowest income per capita of any region, affordability was only identified as the most important barrier in one out of 13 markets in our survey.</blockquote>

And it's not just about networks either, as <a href="https://www.gsmaintelligence.com/research/2016/07/consumer-barriers-to-mobile-internet-adoption-in-africa/568/">GSMA Intelligence reports</a>:
<blockquote>Network coverage was not perceived as an issue in most countries, reflecting the increasing availability of mobile networks. However, mobile broadband (3G or 4G) coverage remains low in most parts of Africa.</blockquote>

The problem is much more profound, and doesn't have a technological solution. From the same report:
<blockquote>A lack of awareness and locally relevant content was considered the most important barrier to internet adoption in North Africa and the second biggest barrier in Sub-Saharan Africa.</blockquote>

There's also a worrying lack of digital skills that prevents people from using the web in Africa:
<blockquote>A lack of digital skills was identified as the biggest barrier to internet adoption in Sub-saharan Africa and the second biggest in North Africa.</blockquote>

The <a href="https://www.worldbank.org/en/publication/wdr2016">World Bank reports</a>:
<blockquote>In Africa, seven in ten people who do not use the internet say they just don't know how to use it, and almost four in ten say they do not know what the internet is.</blockquote>

This is true not only of developing economies, by the way. The World Bank continues:
<blockquote>In high-income Poland and the Slovak Republic, one-fifth of adults cannot use a computer.</blockquote>

And in 2014, <a href="https://www.pewinternet.org/2014/04/03/older-adults-and-technology-use/">Pew Research Centre reported</a>:
<blockquote>41% [of American seniors] do not use the internet at all, 53% do not have broadband access at home, and 23% do not use cell phones.</blockquote>

The lack of digital skills is felt acutely by Asia, too. In its January 2016 <a href="https://www.gsmaintelligence.com/research/2016/06/consumer-barriers-to-mobile-internet-adoption-in-asia/559/">Asia survey</a>, GSMA Intelligence wrote:
<blockquote>A lack of awareness and locally relevant content was the most commonly cited barrier to internet adoption: 72% of non-internet users across the six survey markets felt this was a barrier.… 50% of websites worldwide are in English, a language spoken by only 10% of speakers in the survey countries. By way of contrast, only 2% of websites worldwide are in Mandarin and less than 0.1% are in Hindi.</blockquote>

Below is a video made in a user-testing lab in rural Pakistan, featuring a man in his 20s. He has used a feature phone but never a smartphone. He's given a simple-sounding task: Go to Google and search for the the name of your favourite actress. Watch the video. Watch it all.</p>

{{< vimeo id="116787124" >}}

Presumably, he's stuck because he's been accustomed to a feature phone with physical keys, and he simply doesn't know how to call up the virtual keyboard. Anytime you believe that doing something in your web app is "obvious" or "intuitive", watch this video again.</p>

### Digital Divide

Just as there is a digital divide between "the West" and developing economies, there is a digital divide in income, age, rural and urban, and women and men across the developing world. The World Bank illustrates a divide in income, gender, age and location (rural and urban).</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4974eab5-7939-419b-98bf-196ddfe228d2/pt2-www-img3-lawson-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/45c15b23-01d2-4c32-8751-0e62571f07db/pt2-www-img3-lawson-800w-opt.png" alt="Digital divide in Africa" width="800" height="479" /></a><figcaption>Digital divide in Africa (World Bank figures) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4974eab5-7939-419b-98bf-196ddfe228d2/pt2-www-img3-lawson-large-opt.png">View large version</a>)</figcaption></figure>

In February 2016, <a href="https://www.gadgetsnow.com/tech-news/Only-9-of-rural-India-has-access-to-mobile-internet-Report/articleshow/50840296.cms">53% of urban areas</a> had mobile Internet connectivity, a growth of 71% in one year. In the same period, Internet usage in rural India increased by 93%, but that means that only 9% of people in rural India has access. As I write this, there is a copy of The Hindu newspaper next to my laptop, which <a href="https://www.thehindu.com/business/Wi-fi-hotspots-coming-soon-to-a-store-near-you/article17264038.ece">today reports</a> that the Indian government is recommending a community model of Wi-Fi hotspots, such as in neighborhood grocery stores, in rural areas where connectivity is poor and laying cables is not feasible.

The World Bank reports that in many countries (Cuba, Cambodia, Brazil and others), computers are taxed as luxury goods.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e81a095c-e406-4ebc-aace-ff47a13e1025/pt2-www-img4-lawson-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/75a8e9f7-c070-4259-9e16-8fcb5b7b25b1/pt2-www-img4-lawson-800w-opt.png" alt="Computers and laptops: import tariffs" width="800" height="517" /></a><figcaption>Computers and laptops: import tariffs (World Bank figures) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e81a095c-e406-4ebc-aace-ff47a13e1025/pt2-www-img4-lawson-large-opt.png">View large version</a>)</figcaption></figure>

Many countries, such as Fiji, Bangladesh and Pakistan, tax mobile phones as luxuries, too.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/654e5a90-6b11-42a3-a663-b0c014f188ba/pt2-www-img5-lawson-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/71d663b7-bfd3-4534-ac52-3dd69bb604c1/pt2-www-img5-lawson-800w-opt.png" alt="Mobile phones: import tariffs" width="800" height="484" /></a><figcaption>Mobile phones: import tariffs (World Bank figures) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/654e5a90-6b11-42a3-a663-b0c014f188ba/pt2-www-img5-lawson-large-opt.png">View large version</a>)</figcaption></figure>

## Pressure For Change

The World Bank recommends that:
<blockquote>Making the internet universally accessible and affordable should be a global priority.</blockquote>

There are moves afoot to make this happen, such as an initiative called <a href="https://webwewant.org/fast-africa/">FASTAfrica</a>. FAST stands for fast, affordable, secure and transparent. In a series of grassroots events across Africa in 2016, the organization has demanded:

*   fair and transparent taxes on information and communications technology (ICT),
*   greater effort from governments and donors,
*   agreement on affordability (1 GB for 2% of disposable income),
*   prioritization of getting women online.</p>

### World Wide Web Women

The World Bank writes:
<blockquote>Online work can prove particularly beneficial for women, youth, older workers, and the disabled, who may prefer the flexibility of working from home or working flexible hours.</blockquote>

<a href="https://www.gsmaintelligence.com/research/2016/07/consumer-barriers-to-mobile-internet-adoption-in-africa/568/">GSMA Intelligence writes</a>:
<blockquote>In India… women are 62% less likely to use the internet than men. Many of the underlying reasons for this — affordability, skills and content — are the same as for men; they are simply felt more acutely by women.</blockquote>

In rural India, only <a href="https://www.bcgperspectives.com/content/articles/globalization-customer-insight-rising-connected-consumer-rural-india/">2% of web users are women</a>.

Yet we know that the web empowers women. Across the world in non-agricultural employment, women make up 25% of the work force, but in online work, women make up 44% of the work force.

When asked why online work is advantageous, women overwhelmingly cited the ability to work flexible hours from home as the primary advantage. (32% of women, compared with 23% of men, said that the primary disadvantage to online work is that payment is not high enough, which suggests that Africa, too, has an unjustifiable difference between what women and men get paid.

One successful government initiative is the <a href="https://www.kudumbashree.org/">Kudumbashree project</a>, here in Kerala, India, where I'm writing this. "Kudumbashree" means "prosperity of the family" in the local Malayalm language. The World Bank reports:

<blockquote>The government of Kerala, India, outsources information technology services to cooperatives of women from poor families … Average earnings were US$45 a month, with close to 80 per-cent of women earning at least US$1 a day. Nine in ten of the women had previously not worked outside the home. Samasource, RuralShores, and Digital Divide Data are three private service providers. Samasource splits jobs into microwork for almost 6,400 workers, mostly in Ghana, Haiti, India, Kenya, and Uganda, on average more than doubling their previous income.</blockquote>

A similar story is happening in China:

<blockquote>Online shop owners using Alibaba in China, on average, employ 2.6 additional workers. Four in ten shop owners are women, 19 percent were previously unemployed, 7 percent were farmers, and about 1 percent are persons with disabilities.</blockquote>

## What Can Be Done, And How Can You Help?

The World Bank says that:

<blockquote>Access to the internet is critical, but not sufficient. The full benefits of the information and communication transformation will not be realized unless countries continue to improve their business climate, invest in people's education and health and promote good governance</blockquote>

Should you happen to be a politician in Africa, Asia or Latin America, please take note of the above. But, because you're reading this, I expect you're a web professional — but you can play your part! Make sure your websites are ready for the next 4 billion people, with their (potentially) slow networks and browsers and devices you may never have heard of.

*   Progressively enhance to make sure your core functionality works without JavaScript.
*   Use feature detection, rather than browser sniffing. You will never, ever be able to maintain a list of all devices in the world and their UA strings.
*   Compress images properly and remove unnecessary meta data with a tool such as [ImageOptim](https://imageoptim.com/).
*   Use HTML responsive images (and generate [WebP](https://www.smashingmagazine.com/2015/10/webp-images-and-performance/) versions of all of your assets), and send them to supporting browsers with the `picture` element.
*   Focus relentlessly on performance.
*   Write a progressive web app, rather than a native app.
*   Test in a proxy browser, such as Opera Mini.

Developing countries are home to 94% of the global offline population. These people may be your next potential customers. But if they can't buy from you because your website is a Wealthy Western Website rather than a World Wide Website, you can bet that your competitors will be happy to take their money.</p>

<a href="https://www.mckinsey.com/industries/high-tech/our-insights/internet-matters">McKinsey Global Institute writes</a>:

<blockquote>An increase in internet maturity similar to the one experienced in mature countries over the past 5 years creates an increase in real GDP per capita of $500 on average during this period. It took the industrial revolution of the 19th century 50 years to produce same result.</blockquote>

But it's not just about money. It's about doing the right thing and keeping the web open, democratic and global.

Millions of people in Bangladesh, Nepal and India have miles to walk to visit a doctor, so a feature phone and the free online book <a href="https://hesperian.org/books-and-resources/"><em>Where There Is No Doctor</em></a> (often translated to their local language) becomes first-line medical care.

Millions of people in Subsaharan Africa can't afford school textbooks, but <a href="https://www.worldreader.org/what-we-do/our-books/">Worldreader</a> has tens of thousands of books available for free online, and the books work fine even on old feature phones.

And millions of people in despotic regimes have the web as their only way to contact the outside world.

Please, do your part to ensure the health of the web that has provided you with so much, and pay it forward so the next people can benefit.</p>

<hr/>

<em>Thanks to <a href="https://mrunmaiy.com/">Mrunmaiy Abroal</a>, until recently Opera's Head of Comms in India, and <a href="https://twitter.com/peko0413">Peko Wan</a>, Head of PR &amp; Communications for Opera in Asia, for their help collecting some of the information in this article. Thanks to <a href="https://twitter.com/kgisdahl">Karin Greve-Isdahl</a>, VP Communications at Opera for allowing me to use charts and illustrations made while I was at Opera. Big thanks to Clara at <a href="https://www.damcho.com">Damcho Studio</a> for helping to prepare this article.</em>

{{< signature "vf, al, il" >}}

