---
title: Are You Getting Cheated When Buying A WordPress Theme?
slug: ripped-off-buying-wordpress-themes
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/172d2d45-5e94-4fda-97aa-ea6558400338/00-wordpress-themes-tin-opt.png
date: 2015-11-10T00:08:05.000Z
author: philipblomsterberg
description: >-
  I’ve been around the block quite a bit as an SEO specialist, and in my
  experience website speed has emerged as an increasingly important search
  engine ranking factor over the last few years. [Google, in
  particular](https://www.mattcutts.com/blog/site-speed/), considers **website
  loading speed to be very important** and has made it one of the more important
  factors in its ranking algorithm.

  How does speed affect your rankings? The truth is, as with everything
  concerning Google, we don’t really know — we cannot isolate that factor alone.
categories:
  - WordPress
  - Performance
---
I’ve been around the block quite a bit as an SEO specialist, and in my experience website speed has emerged as an increasingly important search engine ranking factor over the last few years. <a href="https://www.mattcutts.com/blog/site-speed/">Google, in particular</a>, considers <strong>website loading speed to be very important</strong> and has made it one of the more important factors in its ranking algorithm.

How does speed affect your rankings? The truth is, as with everything concerning Google, we don’t really know — we cannot isolate that factor alone. Here, however, are three articles that shed some light on the subject:

*   “[How Website Speed Actually Impacts Search Ranking](https://moz.com/blog/how-website-speed-actually-impacts-search-ranking),” Billy Hoffman, Moz
*   “[How Important Is Site Speed in 2014?](https://www.searchenginejournal.com/seo-101-important-site-speed-2014/111924/),” Albert Costill, Search Engine Journal
*   “[18 Questions (and Answers) About Google, Site Speed, and SEO](https://blog.radware.com/applicationdelivery/applicationaccelerationoptimization/2014/06/updated-18-questions-and-answers-about-google-site-speed-and-seo/),” Tammy Everts, Radware

Based on my work with clients, I’ve seen evidence that <strong>websites that have better loading times rank higher than others</strong>. Accordingly, as I work on my upcoming website, my team and I have engineered good loading time into its design, its layout and all other infrastructure. We were prepared to test just about any approach, even if it meant just a minute in improvement.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [How To Speed Up Your WordPress Website](https://www.smashingmagazine.com/2014/06/how-to-speed-up-your-wordpress-website/)
*   [A Look At The Modern WordPress Server Stack](https://www.smashingmagazine.com/2016/05/modern-wordpress-server-stack/)
*   [<span class="headline">Do-It-Yourself Caching Methods With WordPress</span>](https://www.smashingmagazine.com/2012/06/diy-caching-methods-wordpress/)
*   [A Beginner’s Guide To Creating A WordPress Website](https://www.smashingmagazine.com/2016/02/beginners-guide-creating-wordpress-website/)

{{% feature-panel %}}

The theme we started out with seemed very good, offering speeds that were quite good, especially for a news website or portal. We tested the theme with demo content; however, regardless of how hard we tried, speeds and scores never reached those on the vendor’s website. This led us to believe that theme vendors sometimes set up demos to make their websites appear faster than they really are.

So, the question is, when we shop for a theme, do we get what’s on the tin?

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/172d2d45-5e94-4fda-97aa-ea6558400338/00-wordpress-themes-tin-opt.png" alt="Preview image" /></figure>

## Test Method

We set out to test this idea, using the following method to produce our loading-time comparison data:

*   Test the speed of 25 themes on the vendors’ websites.
*   Test the speed of the themes on a [shared hosting](https://inmotion-hosting.evyy.net/c/1233229/260033/4222) account.
*   Test the speed of the themes on a low-budget virtual private server (VPS) running Apache.
*   Test the speed of the themes on a highly optimized cloud server running NGINX and Varnish and located in a top-class data center with very low latency.

After conducting all speed tests, my <strong>team compared speeds between the different platforms</strong> and also tried to find signs of “cheating.” We used online services to detect content management systems (CMS), as well as manually analyzed the source code.</p>

## Tools Used

We used three popular tools to test the websites: Google PageSpeed Insights (GPI), GTmetrix and Pingdom. For this report, I’ll refer mainly to Google, partly to show what it favors, although when it comes to accuracy and analysis options, GTmetrix and Pingdom are far superior.

GPI will survey a website and then give it a score between 1 and 100. The score depends not only on speed, but on quality of code — minimization of HTML, CSS and JavaScript, caching, compression and so on.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2ea2774d-ec1a-48dd-abdb-1cd9642580f6/01-google-pagespeed-insights-opt.png" alt="Google Pagespeed" /></figure>

The score shows how well your website performs:

*   **Green: 100 to 85** This is a very well-optimized website. Scores above 90 are very rare for websites that are not static — that is, those that use a CMS.
*   **Orange: 84 to 60** If a website scores at the lower end of this range, it might be on the slow side. If it falls in the upper range — say, around 73 — it’s considered to be relatively quick.
*   **Red: 59 to 0** This is definitely a slow or poorly optimized website. Even on a fast system or connection, users will notice this. Websites whose structure has not been thought through and media-laden news websites often fall in this range. Though rare, I have seen websites get a GPI score of less than 1 (one).

While we’re on the subject, I might as well throw in some criticism of GPI. It is very sparse in its feedback, especially for dynamic websites, which most of us use today, and sometimes the advice on optimization is borderline rubbish.

GTmetrix and Pingdom, on the other hand, are <strong>more thorough and provide much more data</strong>. Nevertheless, an excellent (speed) ranking with them doesn’t necessarily correlate with a similar score from GPI. For example, consider that GTmetrix will add points to a low score if a website uses a CDN. A website that uses a CDN might get marginally slower if a user is geographically close to the server, but for the broad majority of people, it will indeed get faster. Google does not seem to account for this.

In fact, the whole subject is a bit tricky, because many seem to treat a GPI score as a measure of speed, although I would consider it to be more a measure of optimization. I have <a href="https://seolo.gy/understand-google-pagespeed/">written about this before</a>, and below are some examples showing how speed and page score don’t necessarily go hand in hand.</p>

### GTmetrix Example

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b7e00034-e0ac-496a-9090-3e909f920485/02-gtmetrix-results-opt.png" alt="Here, GTmetrix grades a website at 94%, although the loading time amounts to a far-from-acceptable 14 seconds." /><figcaption>Here, GTmetrix grades a website at 94%, although the loading time amounts to a far-from-acceptable 14 seconds.</figcaption></figure>

### Pingdom Example

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cf038b05-8fdb-4560-96bb-88a8defc7d7a/03-pingdom-speed-results-opt.png" alt="Another website, tested with Pingdom, shows a perfection grade of 95, although you need 60 seconds to load it" /><figcaption>Another website, tested with Pingdom, shows a performance score of 95, although it needs 60 seconds to load.</figcaption></figure>

So, evidently, GTmetrix and Pingdom just look at optimization.</p>

## What’s A Good Speed Or Score?

What’s a good score, and are there any benchmarks? On my blog, I’ve tested Alexa’s top-100 shopping websites, measuring loading time and GPI score. Here are the results for the top 10 and bottom 10:

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e7c82918-7c7f-4f0d-9559-058255a43e01/04-top100-ecommerce-loading-times-opt.png" alt="I measured the loading time of Alexa's top-100 shopping websites, and these were the 10 quickest and 10 slowest" /><figcaption>I measured the loading time of Alexa’s top-100 shopping websites, and these were the 10 quickest and 10 slowest.</figcaption></figure>

The chart below shows the GPI scores for the same websites.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/43e4c37c-21d4-4908-8176-c80814acf52c/05-top100-ecommerce-google-score-opt.png" alt="GPI gave these same websites the scores above" /><figcaption>GPI gave these same websites these scores.</figcaption></figure>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/80cfe25a-6db2-4b3a-b15c-1086cbfa16f9/06-google-pagespeed-per-theme-opt.png" alt="The above table shows the GPI score for each individual theme on each single hosting platform" /><figcaption>This table shows the GPI score for each individual theme on each individual hosting platform.</figcaption></figure>

Assessment of the results is quite subjective, but it’s safe to say that anything above 75 can be considered good, and anything below approximately 40 is very bad. However, it very much depends on the category of your website. It’s a sure bet that a personal blog will have a better score than a big portal like the Huffington Post.

## Benchmarking

Back to the tests. All tests were conducted when we could assume that traffic to the (demo) website in question was low; if we did get abnormal results, we would crosscheck on another occasion. All of the tests were performed with the caching plugin in use on the demo website, if any. Also, note that the VPS’ used were 100% idle — they had no traffic during the tests.

Here is all of the raw data from the test.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ddd18bca-95b1-4ef6-8815-65a4664372f4/07-benchmarking-chart-opt.png" alt="In this illustration of the data, the y axis shows the GPI score, and the x axis marks each individual theme" /><figcaption>In this illustration of the data, the y axis shows the GPI score, and the x axis marks each individual theme.</figcaption></figure>

The summary below shows the differences (not the actual GPI scores) between the three different server configurations and the reference (i.e. demo) websites.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e7558a14-f8c5-44e6-91db-0831382da121/08-wordpress-themes-speed-benchmarks-opt.png" alt="The key results from the tests" /><figcaption>The key results from the tests</figcaption></figure>

## Findings And Thoughts

Does a theme <strong>generally perform worse than the demo</strong> when you host it yourself? Do some theme vendors simply make static HTML versions of their demos to boost loading time and speed metrics?

Here are some of my key findings.

*   The average score of the budget VPS and shared host was **13% and 26% lower**, respectively, than the reference websites. Only the NGINX server came close to matching the reference websites, with an average 6% lower score.
*   For the optimized VPS, the two websites with the highest deviations had a negative score difference of 27 and 22 points.
*   For the budget VPS, the two websites with the highest deviations had a negative score difference of 35 and 20 points.
*   For the shared server, the two websites with the highest deviations had a negative score difference of 33 and a whopping 53 points.
*   On the optimized VPS, 19 themes (approximately 80%) had a score lower than the reference websites.
*   On the budget VPS, as above, 19 themes (approximately 80%) had a score lower than the reference websites.
*   On the shared host, 22 themes (approximately 88%) had a score lower than the reference websites.</p>

## Tricks Employed

As mentioned above, we wanted to check not only the speeds of the themes on different platforms, but also whether we are being misled to believe that they are quicker. In as many as 5 of the tested themes (20%), we found signs of cheating.

Based on what we detected, here are the tricks employed by these theme vendors:

*   Some created a pure **static website** — a demo with no dynamic parts at all. This would increase the GPI score by a whole lot, and loading time would, of course, lower significantly. This is what we anticipated because we were mislead by this ourselves.
*   Some **run local optimization of JavaScript, CSS, HTML**, etc. This means that the theme delivered to the client is different than the one used on the demo website. I wouldn’t consider this to be cheating, however, and so didn’t count it as such.
*   In two cases, websites seemed to **have multiple optimized files that could not be retrieved**. They would block calls to the files unless the referrer showed that the request was coming from one of the demo pages. However, by faking our referrer to reflect the optimized files’ required request source, we got around the block. Yes, the files were different from what is offered out of the box.
*   Some websites **masquerade as WordPress** by inserting comments and familiar footprints in the code. Comments might be drawn from sources such as Yoast’s SEO plugin and W3 Total Cache, and also the generator tags might be set as `wordpress`. This seemed to fool some of the online CMS identifiers out there.
*   A few vendor also seem to block the GPI bot, which seems kind of odd.</p>

## Summary

As you might already have noticed, we have not named names in this survey. We didn’t write this to out any company, but rather to show the importance of doing one’s due diligence when buying a theme that is marketed as being “fast loading” or “well optimized.”

This was not an “official” test either. Accordingly, we cannot conclusively say that the page-loading “cheats” we detected will continue to be present or whether they were intentional. Some cases seemed quite suspicious, though. We also tested some free, non-commercial themes, such as <a href="https://somerandomdude.com/work/frank/">Frank</a>, which follow what we would expect. This reinforces our hypothesis that <strong>some themes aren’t as fast as what is advertised</strong> on the demo websites. When running small tests on themes for other CMS’, like Joomla, we had the same findings.</p>

### So, Are Theme Vendors Scamming Us?

Whether theme vendors are scamming us depends on whether they intentionally want to mislead buyers. There is certainly a big difference between the figures claimed by vendors on their sales websites and the speeds actually experienced by buyers. Double-dealers might have a lot of leeway, in practical terms. Why? Because <strong>most buyers don’t care</strong>; they buy based merely on appearance. Other buyers are very lenient; if a website gets a GPI score of 70 or higher, then they don’t care. But for serious online publishers, a seemingly small difference in ranking could mean a difference of thousands of dollars every month.

However, keep in mind that developers in general do what they can to obfuscate the technology behind a website — that is, they hide the fact that they are using WordPress. I expect that top-class theme shops optimize just as much as we do when setting up their server. The average Joe being hosted on an oversold server would, thus, have a hard time getting anywhere close to the performance figures cited by theme vendors.

Still, this ordeal set my company back quite some time when we built our website; and, in this case, I am quite certain we were right. I sent a quite detailed email to the theme’s vendor, telling them what we had done and ending by saying that things didn’t really add up. We never heard a peep from them, but a few days later their demo website was performing a whole lot worse.

Once again, when looking for a theme, <strong>do a fair amount of research</strong>. Look through the review websites, look for websites with the same theme, and compare.

I hope you like this article. If you would like to see more detailed data and to download my layman’s infographic, you may do so on <a href="https://intripid.com/wordpress-experiment/">my website</a>. And you’ll find two excellent articles by Marcus Taylor here on Smashing Magazine: “<a href="https://smashingmagazine.com/2014/12/04/what-to-consider-when-choosing-a-wordpress-theme/">What to Consider When Choosing a WordPress Theme</a>” and “<a href="https://www.smashingmagazine.com/2014/06/25/how-to-speed-up-your-wordpress-website/">How to Speed Up Your WordPress Website</a>.”

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/741cb37c-cdb1-43d3-a613-753a2e052866/09-wordpress-speed-infographic-opt.png" alt="09-wordpress-speed-infographic-opt" /></figure>

## TL;DR

*   Website speed is becoming increasingly important for SEO and usability.
*   We tested 25 WordPress themes on three different server configurations not only to compare scores, but to find signs of theme vendors cheating to inflate their score.
*   Of the 25 themes tested, five vendors seemed suspicious at best.
*   On a budget [shared hosting](https://inmotion-hosting.evyy.net/c/1233229/260033/4222) place, **88% of the themes got lower scores than their demos**.

{{< signature "al" >}}

