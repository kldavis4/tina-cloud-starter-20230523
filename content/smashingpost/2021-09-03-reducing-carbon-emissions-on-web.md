---
title: 'Reducing Carbon Emissions On The Web'
slug: reducing-carbon-emissions-on-web
author: bezpowell
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bdef7e38-4e37-4177-a7b3-d74860c7724f/reducing-carbon-emissions-on-web.jpg
date: 2021-09-03T11:30:00.000Z
summary: >-
  Websites, unfortunately, aren’t as environmentally friendly as we might like them to be. This article contains some thoughts and experiences from trying to clean them up.
description: >-
  Websites, unfortunately, aren’t as environmentally friendly as we might like them to be. This article contains some thoughts and experiences from trying to clean them up.
categories:
  - Performance
  - Optimization
  - Opinion Column
---

As is the case with many other developers, the reports over the last few years of the huge energy requirements of the web have prompted me to take a look at my own websites and see what I can do to minimize their impact. This piece will cover some of my experiences in doing this, as well as my current thoughts on **optimizing websites for carbon emissions**, and some practical examples of things you can do to improve your own pages.

But first, a confession: When I first heard about the environmental impact of websites, I didn’t quite believe it. After all, digital is supposed to be better for the planet, isn’t it?

I’ve been involved in various green and environmental groups for decades. In all of that time, I can’t consciously remember anyone ever discussing the possible **environmental impacts of the web**. The focus was always on reducing consumption and moving away from burning fossil fuels. The only time the Internet was mentioned was as a tool for communicating with one another without the need to chop down more trees, or for working without a commute.

So, when people first started talking about the [Internet having similar carbon emissions to the airline industry](https://www.bbc.com/future/article/20200305-why-your-internet-habits-are-not-as-clean-as-you-think), I was a bit skeptical.

## Emissions

It can be hard to visualize the huge network of hardware that allows you to send a request for a page to a server and then receive a response back. Most of us don’t live in data centers, and the cables that carry the signals from one computer to another are often buried beneath our feet. When you can’t see a process in action, the whole thing can feel a little bit like magic &mdash; something that isn’t helped by the insistence of certain companies on adding words like “cloud” and “serverless” to their product names.

As a result of this, my view of the Internet for a long time was a little ephemeral, a sort of mirage. When I started writing this article, however, I performed a little thought experiment: **How many pieces of hardware does a signal travel through from the computer I’m writing at to get outside of the house?**

The answer was quite shocking: 3 cat cables, a switch, 2 powerline adapters, a router and modem, an RJ11 cable, and several meters of electrical wiring. Suddenly, that mirage was beginning to look rather more solid.

Of course, the web (any, by extension, the websites we make) does have a carbon footprint. All of the servers, routers, switches, modems, repeaters, telephone cabinets, optical-to-electrical converters, and satellite uplinks of the Internet must be built from metals extracted from the Earth, and from plastics refined from crude oil. To then provide data to the estimated [20 billion connected devices](https://www.gartner.com/imagesrv/books/iot/iotEbook_digital.pdf) worldwide, they need to consume electricity, which also releases carbon when it is generated (even renewable electricity is not carbon neutral, although it is a lot better than fossil fuels).

Accurately measuring just what those emissions are is probably impossible &mdash; **each device is different** and the energy that powers them can vary over the course of a day &mdash; but we can get a rough idea by looking at typical figures for power consumption, user bases, and so on. One tool that uses this data to estimate the carbon emissions of a single page is the [Website Carbon Calculator](https://www.websitecarbon.com/). According to it, the average page tested “produces 1.76 grams of CO2 per page view”.

If you’ve been used to thinking about the work you do as essentially harmless to the environment, this realization can be quite disheartening. The good news is that, as developers, we can do an awful lot about it.

**Recommended reading**: [*How Improving Website Performance Can Help Save The Planet*](https://www.smashingmagazine.com/2019/01/save-planet-improving-website-performance/)

{{% feature-panel %}}

## Performance And Emissions

If we remember that viewing websites uses electricity and that producing electricity releases carbon, then we’ll know that the emissions of a page must heavily depend on the amount of work that both the server and client have to perform in order to display the page. Also, the amount of data that is required for the page, and the complexity of the route it must travel through, will determine the amount of carbon released by the network itself.

For example, downloading and rendering [example.com](https://example.com/) will likely consume far less electricity than [Apple’s home page](https://www.apple.com/), and it will also be much quicker. In effect, what we are saying is that high emissions and slow page loads are just two symptoms of the same underlying causes.

It’s all very well to talk about this relationship in theory, of course, but having some real-world data to back it up would be nice. To do just that, I decided to conduct a little study. I wrote a simple command-line interface program to take a list of the 500 most popular websites on the Internet, [according to MOZ](https://moz.com/top500), and check their home pages against both Google’s PageSpeed Insights and the Website Carbon Calculator.

Some of the checks timed out (often because the page in question simply took too long to load), but in total, I managed to collect results for over 400 pages on 14 July 2021. You can download the [summary of results](https://moz.com/top-500/download/?table=top500Domains) to examine yourself but to provide a visual indication, I have plotted them in the chart below:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/92553f73-8a45-4830-b666-e74671313616/1-reducing-carbon-emissions-on-web.jpeg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/92553f73-8a45-4830-b666-e74671313616/1-reducing-carbon-emissions-on-web.jpeg" width="800" height="452" sizes="100vw" caption="Carbon versus PageSpeed of 400 popular websites. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/92553f73-8a45-4830-b666-e74671313616/1-reducing-carbon-emissions-on-web.jpeg'>Large preview</a>)" alt="Chart showing trend of almost 6 grams of carbon at 0 PageSpeed, dropping to 1 gram of carbon at 100 PageSpeed." >}}

As you can see, while the variation between individual websites is very high, there is a strong trend towards lower emissions from faster pages. The mean average emissions for websites with a PageSpeed score of 100 is about 1 gram of carbon, which rises to a projected almost 6 grams for websites with a score of 0. I find it slightly reassuring that, despite there being many websites with very low speeds and high emissions, most of the results are clustered in the bottom right of the chart.

{{% ad-panel-leaderboard %}}

## Taking Action

Once we understand that much of a page’s emissions originate from poor performance, we can start taking steps to reduce them. Many of the things that contribute to a website’s emissions are beyond our control as developers. We can’t, for example, choose the devices that our users access our pages from or decide on the network infrastructure that their requests travel through, but we can take steps to improve our websites’ performance.

Performance optimization is a broad topic, and many of you reading this likely have more experience than I do, but I would like to briefly mention **a few things that I have observed recently** when optimizing various pages’ loading speed and carbon emissions.

### Rendering Is Much Slower on Mobile

I recently reworked the design of my personal blog in order to make it a little more user-friendly. One of my hobbies is photography, and the website had previously featured a full-height header image.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2b6230bc-00fe-434f-8cd4-63d44ee5e530/2-reducing-carbon-emissions-on-web.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2b6230bc-00fe-434f-8cd4-63d44ee5e530/2-reducing-carbon-emissions-on-web.png" width="800" height="432" sizes="100vw" caption="The old home page showing a full-height image header. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2b6230bc-00fe-434f-8cd4-63d44ee5e530/2-reducing-carbon-emissions-on-web.png'>Large preview</a>)" alt="Full-height image of trees on website. No content visible." >}}

While the design did a good job of showcasing my photographs, it was a complete pain to scroll past, especially when moving through pages of blog posts. I didn’t want to lose the feeling of having a photo in the header, however, and eventually settled on using it as a background for the page title.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9e6dfcee-5e6a-40a9-a9c6-11b813c2a25d/3-reducing-carbon-emissions-on-web.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9e6dfcee-5e6a-40a9-a9c6-11b813c2a25d/3-reducing-carbon-emissions-on-web.png" width="800" height="432" sizes="100vw" caption="The new home page with a greatly reduced image. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9e6dfcee-5e6a-40a9-a9c6-11b813c2a25d/3-reducing-carbon-emissions-on-web.png'>Large preview</a>)" alt="Web page with text and image as background for title." >}}

The full-height header had been using `srcset` in order to make loading as fast as possible, but the images were still very big on high-resolution screens, and my longest contentful paint (LCP) time on mobile for the old design was almost 3 seconds. A big advantage of the new design was that it allowed me to make the images much smaller, which reduced the LCP time to about 1.5 seconds.

On laptops and desktops, people wouldn’t have noticed a difference, because both versions were well under a second, but on much less powerful mobile devices, it was quite dramatic. What was the effect of this change on carbon emissions? 0.31 grams per view before, 0.05 grams after. **Decoding and rendering images is very resource-intensive**, and this grows exponentially as the images get bigger.

The size of images isn’t the only thing that can have an impact on the time to decode; the format is important as well. Google’s Lighthouse often recommends serving images in next-generation formats to reduce the amount of data that needs to be downloaded, but [new formats are often slower to decode](https://calendar.perfplanet.com/2018/dont-use-jpeg-xr-on-the-web/), especially on mobile. Sending less data over the wire is better for the environment, but it is possible that consuming more energy to decode could offset that benefit. As with most things, testing is key here.

From my own testing in trying to add support for AVIF encoding to the Zola static site generator, I found that AVIF, which promises [much smaller file sizes than JPG at the same quality](https://netflixtechblog.com/avif-for-next-generation-image-coding-b1d75675fe4), took orders of magnitude longer to encode; something that bunny.net’s observation that [WebP outperforms AVIF by as much as 100 times](https://bunny.net/blog/lets-talk-avif-and-why-we-are-not-adding-support-just-yet/) supports. While doing this, the server will be consuming electricity, and I do wonder whether, for websites with low visitor counts, switching to the new format might actually end up increasing emissions and reducing performance.

Images, of course, are not the only component of modern web pages that take a long time to process. Small JavaScript files, depending on what they are doing, can take a long time to execute and the same potential pitfalls as images will apply.

**Recommended reading**: [*The Humble `img` Element And Core Web Vitals*](https://www.smashingmagazine.com/2021/04/humble-img-element-core-web-vitals/)

### Round-Trips Add Up

Another thing that can have a surprising impact on performance and emissions is where your data is coming from. Conventional wisdom has long said that serving assets such as frameworks from a central content delivery network (CDN) will improve performance because getting data from local nodes is generally faster for users than from a central server. jQuery, for example, has the option to be loaded from a CDN, and its maintainers say that this can improve performance, but real-world testing by Harry Roberts has shown that [self-hosting assets is generally faster](https://csswizardry.com/2019/05/self-host-your-static-assets/).

This has also been my experience. I recently helped a gaming website improve its performance. The website was using a fairly large CSS framework and loading all of its third-party assets via a CDN. We switched to self-hosting all assets and removed unused components from the framework.

None of the optimizations resulted in any visual changes to the website, but together they increased the **Lighthouse score from 72 to 98** and reduced carbon emissions from 0.26 grams per view to 0.15.

### Send Only What You Need

This leads nicely onto the subject of sending users only the data they actually need. I’ve worked on (and visited) many, many websites that are dominated by stock images of people in suits smiling at one another. There seems to be a mentality amongst certain organizations that what they do is really boring and that adding photos will somehow convince the general public otherwise.

I can sort of understand the thinking behind this because there are numerous pieces on how the [amount of time people spend reading is declining](https://www.amacad.org/humanities-indicators/public-life/time-spent-reading). Text, we are repeatedly told, is going out of fashion; all people are interested in now are videos and interactive experiences.

From that point of view, stock photos could be seen as a useful tool to liven up pages, but eye-tracking studies show that [people ignore images that aren’t relevant](https://www.nngroup.com/articles/photos-as-web-content/). When people aren’t looking at your images, the images might as well be empty space. And when every byte costs money, contributes to climate change, and slows down loading times, it would be better for everyone if they actually were.

Again, what can be said for images can be said for everything else that isn’t the page’s core content. If something isn’t contributing to a user’s experience in a meaningful way, it shouldn’t be there. I’m not for a moment advocating that we all start serving unstyled pages &mdash; some people, such as those with dyslexia, do find large blocks of text difficult to read, and other users almost certainly would find such pages boring and go elsewhere &mdash; but **we should look critically at every part of our websites** to consider whether they are earning their keep.

{{% ad-panel-leaderboard %}}

## Accessibility and the Environment

Another area where performance and emissions converge is in the field of accessibility. There is a common misconception that making websites accessible involves adding `aria` attributes and JavaScript to a page, but often what you leave out is more important than what you put in, making an accessible website relatively lightweight and performant.

### Using Standard Elements

MDN Web Docs has some very good tutorials on accessibility. In “[HTML: A Good Basis for Accessibility](https://developer.mozilla.org/en-US/docs/Learn/Accessibility/HTML)”, they cover how the best foundation of an accessible website lies in using the correct HTML elements for the content. One of the most interesting sections of the article is where they try to recreate the functionality of a `button` element using a `div` and custom JavaScript.

This is obviously a minimal example, but I thought it would be interesting to compare the size of this button version to one using standard HTML elements. The fake button example in this case weighs around 1,403 bytes uncompressed, whereas an actual `button` with less JavaScript and no styling weighs 746 bytes. The `div` button will also be semantically meaningless and, therefore, much harder for people with screen readers to use and for bots to parse.

**Recommended reading**: [*Accessible SVGs: Perfect Patterns For Screen Reader Users*](https://www.smashingmagazine.com/2021/05/accessible-svg-patterns-comparison/)

When scaled up, these sorts of things make a difference. Parsing minimal markup and JavaScript is easier for a browser, just as it is easier for developers.

On a larger scale, I was recently **refactoring the HTML of a website** that I work on &mdash; doing things like removing redundant title attributes and replacing `div`s with more semantic equivalents. The original page had a structure like the following (content removed for privacy and brevity):

<pre><code class="language-html">&lt;div class="container"&gt;
    &lt;section&gt;
        &lt;div class="row"&gt;

            &lt;div class="col-md-3"&gt;
                &lt;aside&gt;
                    &lt;!-- Sidebar content here --&gt;
                &lt;/aside&gt;
            &lt;/div&gt;

            &lt;div class="col-md-9"&gt;
                &lt;!-- Main content here --&gt;
                &lt;h4&gt;Content piece heading&lt;/h4&gt;
                &lt;p&gt;
                    Some items;&lt;br&gt;
                    Item 1 &lt;br&gt;
                    Item 2 &lt;br&gt;
                    Item 3 &lt;br&gt;
                &lt;br&gt;
                &lt;/p&gt;
                &lt;!-- More main content here --&gt;
            &lt;/div&gt;

        &lt;/div&gt;
    &lt;/section&gt;
&lt;/div&gt;</code></pre>

With the full content, this weighed 34,168 bytes.

After refactoring, the structure resembled this:

<pre><code class="language-html">&lt;div class="container"&gt;
    &lt;div class="row"&gt;

        &lt;main class="col-md-9 col-md-push-3"&gt;
            &lt;!-- Main content here --&gt;
            &lt;h3&gt;Content piece heading&lt;/h3&gt;
            &lt;p&gt;Some items;&lt;/p&gt;
            &lt;ul&gt;
              &lt;li&gt;Item 1&lt;/li&gt;
              &lt;li&gt;Item 2&lt;/li&gt;
              &lt;li&gt;Item 3&lt;/li&gt;
            &lt;/ul&gt;
            &lt;!-- More main content here --&gt;
        &lt;/main&gt;

        &lt;aside class="col-md-3 col-md-pull-9"&gt;
            &lt;!-- Sidebar content here --&gt;
        &lt;/aside&gt;

    &lt;/div&gt;
&lt;/div&gt;</code></pre>

It weighed 32,805 bytes.

The changes are currently ongoing, but already the markup is far more accessible according to WebAIM, Lighthouse, and manual testing. The file size has also gone down, and, when averaging the time from five profiles in Chrome, the time to parse the HTML has dropped by about 2 milliseconds.

These are obviously small changes and probably won’t make any perceptual difference to users. However, it is nice to know that **every byte costs users and the environment** &mdash; making a website accessible can also make it a little bit lighter as well.

{{% ad-panel-leaderboard %}}

### Videos

Project Gutenberg’s HTML version of [_The Complete Works of William Shakespeare_](https://www.gutenberg.org/files/100/100-h/100-h.htm) is approximately 7.4 MB uncompressed. According to Android Authority in “[How Much Data Does YouTube Actually Use?](https://www.androidauthority.com/how-much-data-does-youtube-use-964560/)”, a 360p YouTube video weighs about 5 to 7.5 MB per minute of footage and 1080p about 50 to 68. So, for the same amount of bandwidth as all of Shakespeare’s plays, you will get only about 7 seconds of high-definition video. Video is also very intensive to encode and decode, and this is probably a major contributing factor to [estimates of Netflix’s carbon emissions](https://www.iea.org/commentaries/the-carbon-footprint-of-streaming-video-fact-checking-the-headlines) being as high as 3.2 KG per hour.

Most videos rely on both visual and auditory components to communicate their message, and **large files sizes require a certain level of connectivity**. This obviously places limits on who can benefit from such content. [Making video accessible](https://www.w3.org/WAI/media/av/) is possible but far from simple, and many websites simply don’t bother.

If video was only ever treated as a form of progressive enhancement, this would perhaps not be a problem, but I have lost count of the number of times I have been searching for something on the web, and the only way to find the information I wanted was by watching a video. On YouTube, the [average number of monthly users](https://backlinko.com/youtube-users#usage-growth) grew from 20 million in 2006 to 2 billion in 2020. Vimeo also has a [continually growing user base](https://www.statista.com/statistics/705598/vimeo-subscribers-worldwide/).

Despite the huge number of visitors to video-sharing websites, many of the most popular ones [do not seem to be fully compliant with accessibility legislation](https://www.vyond.com/resources/508-compliance-and-accessible-video/). In contrast to this, numerous [types of assistive technologies](https://www.w3.org/WAI/people-use-web/tools-techniques/) are designed to make plain text accessible to as wide a variety of people as possible. Text is also easy to convert from one format to another, so it can be used in a number of different contexts.

As we can see from the example of Shakespeare, plain text is also incredibly space-efficient, and it has a far lower carbon footprint than any other form of human-friendly information transmitted on the web.

Video can be great, and many people learn best by watching a process in action, but it also leaves some people out and has an environmental cost. To keep our websites as lightweight and inclusive as possible, we should treat text as the primary form of communication wherever possible, and offer things such as audio and video as an extra.

**Recommended Reading**: [*Optimizing Video For Size And Quality*](https://www.smashingmagazine.com/2021/02/optimizing-video-size-quality/)

## In Conclusion

Hopefully, this brief look at my experience in trying to make websites better for the environment has given you some ideas for things to try on your own websites. It can be quite disheartening to run a page through the *Website Carbon Calculator* and be told that it could be emitting hundreds of kilograms of CO2 a year. Fortunately, the sheer size of the web can amplify positive changes as well as negative ones, and **even small improvements soon add up on websites** with thousands of visitors a week.

Even though we are seeing things like a 25-year-old website [increasing 39 times in size](https://mxb.dev/blog/space-jam/) after a redesign, we are also seeing websites being made to [use as little data as possible](https://www.wholegraindigital.com/blog/designing-web-services-for-people-living-in-data-poverty/), and clever people are figuring out how to [deliver WordPress in 7 KB](https://css-tricks.com/delivering-wordpress-in-7kb/). So, in order for us to reduce the carbon emissions of our websites, we need to make them faster &mdash; and that benefits *everybody*.

### Further Reading

- [World Wide Waste](https://gerrymcgovern.com/books/world-wide-waste/), Gerry McGovern
- “[Is WebP Really Better Than JPEG?](https://siipo.la/blog/is-webp-really-better-than-jpeg)”, Johannes Siipola
- “[Make Jamstack Slow? Challenge Accepted.](https://css-tricks.com/make-jamstack-slow-challenge-accepted/)”, Steve Keep, CSS-Tricks
- “[Can the Internet Ever Be Green?](https://www.bbc.co.uk/programmes/w3ct0xbc)”, The Climate Question, BBC
- “[Could Your Data Center Not Just Power Your Website, But Also Grow Your Salad?](https://www.wholegraindigital.com/blog/data-center-salad/)”, Tom Greenwood, Wholegrain Digital
- [The Better Web Alliance](https://www.better-web-alliance.net/) (my own project)
- [Sustainable Web Manifesto](https://www.sustainablewebmanifesto.com/)

{{< signature "vf, yk, il, al" >}}
