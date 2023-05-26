---
title: 'Multivariate Testing 101: A Scientific Method Of Optimizing Design'
slug: multivariate-testing-101-a-scientific-method-of-optimizing-design
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/418868ef-a80b-491c-be67-0d72f6a300aa/testing.jpg
date: 2011-04-04T09:09:02.000Z
author: paras-chopra
summary: >-
  Paras Chopra goes into the technical details of multivariate testing. Get to know the types of multivariate tests, the do’s and don’ts and more!
description: >-
  Paras Chopra goes into the technical details of multivariate testing. Get to know the types of multivariate tests, the do’s and don’ts and more!
categories:
  - Design
  - Testing
  - Usability
---

In a previous article on Smashing Magazine, I described [A/B testing](https://www.smashingmagazine.com/2010/06/24/the-ultimate-guide-to-a-b-testing/) and various resources related to it. I have also covered the [basics of multivariate testing](https://www.smashingmagazine.com/2010/11/24/multivariate-testing-in-action-five-simple-steps-to-increase-conversion-rates/) in the past, yet in this post I’ll go deeper in the technical details of multivariate testing which is similar to A/B testing but with crucial differences.

In a multivariate test, a Web page is treated as a combination of elements (including headlines, images, buttons and text) that affect the conversion rate. Essentially, you decompose a Web page into distinct units and create variations of those units. For example, if your page is composed of a headline, an image and accompanying text, then you would create variations for each of them. To illustrate the example, let’s assume you make the following variations:

*   Headline: headline 1 and headline 2
*   Text: text 1 and text 2
*   Image: image 1 and image 2

The scenario above has three variables (headline, text and image), each with two versions. In a multivariate test, your objective is to see which combination of these versions achieves the highest conversion rate. By combinations, I mean one of the eight (2 &times; 2 &times; 2) versions of the Web page that we’ll come up with when we combine variations of the sections:

*   Headline 1 + Text 1 + Image 1
*   Headline 1 + Text 1 + Image 2
*   Headline 1 + Text 2 + Image 1
*   Headline 1 + Text 2 + Image 2
*   Headline 2 + Text 1 + Image 1
*   Headline 2 + Text 1 + Image 2
*   Headline 2 + Text 2 + Image 1
*   Headline 2 + Text 2 + Image 2

In multivariate testing, you **split traffic between these eight different versions** of the page and see which combination produces the highest conversion rate &mdash; just like in A/B testing, where you split traffic between two versions of a page.

{{% feature-panel %}}

## Getting Started With Multivariate Testing

To create your first multivariate test, first choose a tool or framework that supports multivariate testing. You can use one of the tools listed in the section “Tools” in the end of this article. Please note that not all A/B testing tools support multivariate testing, so make sure your tool of choice allows it.

Once you’ve decided which tool to use, choose which sections to include in the test. As you know, a Web page can contain tens or hundreds of different sections (footer, headline, sidebar, log-in form, navigation buttons, etc.). You cannot include all of these sections in the test; creating variations for all of them would be an enormous task (and, as you’ll read below, the traffic requirements for the test will grow exponentially with each new section). Narrow it down to the few sections of the page that you think are most important to the conversion goal.

The following parts of a page (listed in order of importance) are typically included in a multivariate test:

*   Headline and heading,
*   Call-to-action buttons (color, text, size, placement),
*   Text copy (content, length, size),
*   Image (type, placement, size),
*   Form length.

## The Difference Between A/B Testing And Multivariate Testing

Conceptually, the two techniques are similar, but there are crucial differences. First and foremost, the traffic requirements are different. As I said, the number of combinations that need to be tested grows exponentially in a multivariate test. You can test three or four versions in an A/B test and tens or hundreds of versions in a multivariate test. Clearly, then, a lot of traffic &mdash; and time &mdash; is required to arrive at meaningful results.

For example, if you have three sections with three variations each, the number of combinations is 27. Add another section with three variations, and the total number of combinations jumps to 81. If you want meaningful results, you can’t keep adding sections to the test. Be selective. A good rule is to limit the total number of combinations to 25 or fewer.

<figure><a href="https://www.flickr.com/photos/thechorompys/2683414975/in/photostream/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d5189579-d20f-44c5-b984-1d81a05db686/variation-testing.png" alt="Varation Testing" /></a><figcaption>Use A/B testing for large scale changes, not to refine or optimize existing designs. Image by <a href="https://www.flickr.com/photos/thechorompys/2683414975/in/photostream/">Meet the Chumbeques</a></figcaption></figure>

Another difference is in how these techniques are used. A/B testing is usually reserved for large radical changes (such as completely changing a landing page or displaying two different offers). Multivariate testing is used to refine and optimize an existing design. For the mathematically inclined, A/B testing is used to optimize for a global optimum, while multivariate testing is used to optimize for a local optimum.

One advantage of multivariate testing over A/B split testing is that it can tell you which part of the page is most influential on conversion goals. Say you’re testing the headline, text and image on your landing page. How do you know which part has the most impact? Most multivariate testing tools will give you a metric, called the “impact factor,” in their reports that tells you which sections influence the conversion rate and which don’t. You don’t get this information from A/B testing because all sections are lumped into one variation.

## Types Of Multivariate Tests

Based on how you distribute traffic to your combinations, there are several types of multivariate tests (MVT):

**Full factorial testing**<br>
This is the kind people generally refer to when they talk about multivariate testing. By this method, one distributes website traffic equally among all combinations. If there are 16 combinations, each one will receive one-sixteenth of all the website traffic. Because each combination gets the same amount of traffic, this method provides all of the data needed to determine which particular combination and section performed best. You might discover that a certain image had no effect on the conversion rate, while the headline was most influential. Because the full factorial method makes no assumptions with regard to statistics or the mathematics of testing, I recommend it for multivariate testing.

<figure><a href="https://www.flickr.com/photos/33131592@N05/4362940980/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0dfd6081-2e72-4511-a156-7ba5ac711cea/results-by-world.png" alt="Results for ItoWorld" /></a><figcaption>Record and compare the resulting traffic for each tested version. Image by <a href="https://www.flickr.com/photos/33131592@N05/4362940980/">ItoWorld</a></figcaption></figure>

**Partial or fractional factorial testing**<br>
As the name suggests, in this method only a fraction of all combinations are exposed to website traffic. The conversion rate for unexposed combinations is inferred from the ones that were included in the test. For example, if there are 16 combinations, then traffic is split among only eight of those. For the remaining eight, we get no conversion data, and hence we need to resort to fancy mathematics (with a few assumptions) for insight. For obvious reasons, I don’t recommend this method: even though there are fewer traffic requirements for partial factorial testing, the method forces too many assumptions. No matter how advanced the mathematics are, hard data is always better than inference.

**Taguchi testing**<br>
This is the most esoteric method of all. A quick Google search reveals a lot of tools claiming to cut your testing time and traffic requirements drastically with Taguchi testing. Some might disagree, but I believe the Taguchi method is bit of a sham; it’s a set of heuristics, not a theoretically sound method. It was originally used in the manufacturing industry, where specific assumptions were made in order to decrease the number of combinations needing to be tested for QA and other experiments. These assumptions are not applicable to online testing, so you shouldn’t need to do any Taguchi testing. Stick to the other methods.

{{% ad-panel-leaderboard %}}

## Do’s And Don’ts

I have observed hundreds of multivariate tests, and I have seen many people make the same mistakes. Here is some practical advice, direct from my experience.

### Don’ts

*   **Don’t include a lot of sections in the test**. Every section you add effectively doubles the number of combinations to test. For example, if you’re testing a headline and image, then there are a total of four combinations (2 × 2). If you add a button to the test, there are suddenly eight combinations to test (2 × 2 × 2). The more combinations, the more traffic you’ll need to get significant results.

### Do’s

*   **Do preview all combinations.**.  In multivariate testing, variations of a section (image, headline, button, etc.) are combined to create page variations. One of the combinations might be odd-looking or, worse, illogical or incompatible. For example, one combination might put together a headline that says “$15 off” and a button that says “Free subscription.” Those two messages are incompatible. Detect and remove incompatibilities at the preview stage.
*   **Do decide which sections are most worthy of inclusion in the test.**.  In a multivariate test, not all sections will have an equal impact on the conversion rate. For example, if you include a headline, a call-to-action button and a footer, you might come to realize that footer variations have little impact, and that headline and call-to-action variations produce winning combinations. You get a powerful section-specific report. Below is a sample report from Visual Website Optimizer. Notice how the button has more impact (91%) than the headline (65%): [![MVT report](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7834c0d3-e28a-49cc-8cdb-14ec014a5041/mvt-small.gif "mvt-report-scaled")](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/836d178b-3882-4811-92de-711b50e6f414/mvt-report.png)
*   **Do estimate the traffic needed for significant results.**.  Before testing, get a clear idea of how much traffic you’ll need in order to get statistically significant results. I’ve seen people add tens of sections to a page that gets just 100 visitors per day. Significant results from such a test would take months to accumulate. I suggest using a calculator, such as this [A/B split and multivariate testing duration calculator](https://visualwebsiteoptimizer.com/ab-split-test-duration/), to estimate how much traffic your test will require. If it’s more than what’s acceptable, reduce some sections.

## Case Studies

A lot of A/B testing case studies are on the Web, but unfortunately, finding multivariate test case studies is still difficult. So, I scoured the Internet and compiled relevant ones.

<a href="https://www.smashingmagazine.com/2010/11/24/multivariate-testing-in-action-five-simple-steps-to-increase-conversion-rates/">Software Download Case Study: downloads increased by 60%</a>
This is one multivariate test I did to compare different versions of headlines and links. In the end, one of the variations resulted in a more than 60% increase in downloads.

<a href="https://www.smashingmagazine.com/2010/11/24/multivariate-testing-in-action-five-simple-steps-to-increase-conversion-rates/"><img title="mvt-case-3" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/df2ce9f6-cc9d-4fdb-890a-f320d5804081/mvt-case-3.png" alt="" width="559" height="163" /></a>

<a href="https://www.slideshare.net/Widemile/widemile-and-microsoft-multivariate-testing-case-study">Microsoft Multivariate Testing Case Study</a><br>
This presentation details the variations that were tested for this website and the ultimate winner.

<a href="https://www.sitespect.com/case-studies.shtml">SiteSpect Case Studies</a><br>
This page presents a dozen of multivariate testing case studies of large companies using multivariate testing and behavioral targeting to optimize their sites.

<a href="https://www.maxymiser.com/customers/client-success-stories">Maxymiser Case Studies</a><br>
Another set of multivariate testing case studies.

<a href="https://youtube-global.blogspot.com/2009/08/look-inside-1024-recipe-multivariate.html">Look Inside a 1,024-Recipe Multivariate Experiment</a><br>
YouTube did a gigantic multivariate test in 2009. It can afford to do tests with a thousand-plus combinations because it has sufficient traffic.

Multivariate testing of an email newsletter<br>
An agency tested color and text on the call-to-action button of its email newsletter. The best button had the highest CTR: 60%.

## Multivariate Testing Tools And Resources

### Tools

<a href="https://www.google.com/websiteoptimizer/">Google Website Optimizer</a><br>
A free basic multivariate testing tool by Google. It’s great if you want to test the waters before investing money in multivariate testing. The downside? You’ll need to tag different sections of the Web page with JavaScript, which can be cumbersome. It’s also prone to error and forces you to rely on others (like the technology department) for implementation.

<a href="https://visualwebsiteoptimizer.com/" rel="nofollow">Visual Website Optimizer</a> (Disclaimer: I am the developer of this tool)<br>
The main advantage of this paid tool is that you can create a multivariate test visually in a WYSIWYG editor by choosing different sections of the page. You can then run the test without having to tag sections individually (although a snippet of code is required in the header). The tool includes heat map and click map reports.

<a href="https://www.whichmvt.com">WhichMVT</a><br>
A website that publishes user reviews of all of the multivariate testing tools available on the market. If you are planning to adopt a multivariate testing tool for your organization, do your research on this website.

**Enterprise testing tools**<br>
Omniture’s <a href="https://www.omniture.com/en/products/conversion/testandtarget">Test&amp;Target</a>, Autonomy’s <a href="https://www.optimost.com/">Optimost</a>, <a href="https://www.vertster.com/">Vertster</a>, Webtrends’ <a href="https://www.webtrends.com/Products/Optimize.aspx">Optimize</a>, and <a href="https://www.sitespect.com/">SiteSpect</a>.

### Resources

<a href="https://www.optimizeandprophesize.com/jonathan_mendezs_blog/2008/05/expert-guide-to.html">Expert Guide to Multivariate Testing Success</a>, by Jonathan Mendez<br>
A series of blog posts detailing different aspects of multivariate testing.

<a href="https://www.ektron.com/literature/whitepapers/fail_faster_with_multivariate_testing.pdf">Fail Faster With Multivariate Testing</a> (PDF)<br>
An excellent free mini-guide to multivariate testing.

<a href="https://www.forrester.com/rb/Research/online_testing_vendor_landscape/q/id/53637/t/2">Online Testing Vendor Landscape</a><br>
A commercial report by Forrester that compares the various testing vendors out there.

<a href="https://www.seomoz.org/blog/lessons-learned-from-21-case-studies-in-conversion-rate-optimization-10585">Lessons Learned from 21 Case Studies in Conversion Rate Optimization</a><br>
This article discusses ideas for conversion rate optimization detailed through different case studies.

{{% ad-panel-leaderboard %}}

### Further Reading

You may be interested in the following related articles:

*   [Ultimate Guide to A/B Testing](https://www.smashingmagazine.com/2010/06/24/the-ultimate-guide-to-a-b-testing/)
*   [Getting Started With E-Commerce: Your Options When Selling Online](https://www.smashingmagazine.com/2010/06/02/getting-started-with-e-commerce-your-options-when-selling-online/)
*   [Improve Your E-Commerce Design With Brilliant Product Photos](https://www.smashingmagazine.com/2010/08/24/improve-your-e-commerce-design-with-brilliant-product-photos/)
*   Our 3-part-series “[Optimizing Conversion Rates](https://www.smashingmagazine.com/2009/05/23/optimizing-conversion-rates-less-effort-more-customers/)”.

{{< signature "al, mrn" >}}
