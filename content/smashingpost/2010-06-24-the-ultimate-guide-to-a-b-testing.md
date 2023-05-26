---
title: The Ultimate Guide To A/B Testing
slug: the-ultimate-guide-to-a-b-testing
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c3a992f9-fb82-4b6f-9d39-f55192d377c9/content.jpg
date: 2010-06-24T09:05:30.000Z
author: paras-chopra
description: >-
  A/B testing isn’t a buzz term. A lot of savvy marketers and designs are using it right now to gain insight into visitor behavior and to increase conversion rate. And yet A/B testing is still not as common as such Internet marketing subjects as SEO, Web analytics and usability.
categories:
  - Design
  - Workflow
  - Testing
---
People just aren’t as aware of it. They don’t completely understand what it is or how it could benefit them or how they should use it. This article is meant to be the best guide you will ever need for A/B testing. 

## What Is A/B Testing?

At its core, A/B testing is exactly what it sounds like: you have two versions of an element (A and B) and a metric that defines success. To determine which version is better, you subject both versions to experimentation simultaneously. In the end, you measure which version was more successful and select that version for real-world use.

{{% feature-panel %}}

This is similar to the experiments you did in Science 101. Remember the experiment in which you tested various substances to see which supports plant growth and which suppresses it. At different intervals, you measured the growth of plants as they were subjected to different conditions, and in the end you tallied the increase in height of the different plants.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/afb5e8bb-23ac-4ea3-bc05-18db6be064ff/abtesting.gif"><img loading="lazy" decoding="async" class="alignnone" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9101cdea-2c14-4c82-ba49-56d16a4c7ee8/abtesting-small.gif" alt="a/b testing" width="500" height="393" /></a><figcaption><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/afb5e8bb-23ac-4ea3-bc05-18db6be064ff/abtesting.gif">Large version</a></figcaption></figure>

A/B testing on the Web is similar. You have two designs of a website: A and B. Typically, A is the existing design (called the control), and B is the new design. You split your website traffic between these two versions and measure their performance using metrics that you care about (conversion rate, sales, bounce rate, etc.). In the end, you select the version that performs best.</p>

## What To Test?

Your choice of what to test will obviously depend on your goals. For example, if your goal is to increase the number of sign-ups, then you might test the following: length of the sign-up form, types of fields in the form, display of privacy policy, "social proof," etc. The goal of A/B testing in this case is to figure out what prevents visitors from signing up. Is the form's length intimidating? Are visitors concerned about privacy? Or does the website do a bad job of convincing visitors to sign up? All of these questions can be answered one by one by testing the appropriate website elements.

Even though every A/B test is unique, certain elements are usually tested:

*   The call to action's (i.e. the button's) wording, size, color and placement,
*   Headline or product description,
*   Form's length and types of fields,
*   Layout and style of website,
*   Product pricing and promotional offers,
*   Images on landing and product pages,
*   Amount of text on the page (short vs. long).</p>

## Create Your First A/B Test

Once you've decided what to test, the next step, of course, is to select a tool for the job. If you want a free basic tool and don’t mind fiddling with HTML and JavaScript, go with <a href="https://www.google.com/websiteoptimizer">Google Website Optimizer</a>. If you want an easier alternative with extra features, go with <a href="https://visualwebsiteoptimizer.com/">Visual Website Optimizer</a> (<strong>disclaimer</strong>: my start-up). Other options are available, which I discuss at the end of this post. Setting up the core test is more or less similar for all tools, so we can discuss it while remaining tool-agnostic.

You can set up an A/B test in one of two ways:

*   **Replace the element to be tested before the page loads**.  If you are testing a single element on a Web page—say, the sign-up button—then you'll need to create variations of that button (in HTML) in your testing tool. When the test is live, the A/B tool will randomly replace the original button on the page with one of the variations before displaying the page to the visitor.
*   **Redirect to another page**.  If you want to A/B test an entire page—say, a green theme vs. a red theme—then you'll need to create and upload a new page on your website. For example, if your home page is `https://www.example.com/index.html`, then you'll need to create a variation located at `https://www.example.com/index1.html`. When the test runs, your tool will redirect some visitors to one of your alternate URLs.

Once you have set up your variations using one of these two methods, the next step is to set up your conversion goal. Typically, you will get a piece of JavaScript code, which you would copy and paste onto a page that would represent a successful test were a visitor to arrive there. For example, if you have an e-commerce store and you are testing the color of the "Buy now" button, then your conversion goal would be the "Thank you" page that is displayed to visitors after they complete a purchase.

As soon as a conversion event occurs on your website, the A/B testing tool records the variation that was shown to the visitor. After a sufficient number of visitors and conversions, you can check the results to find out which variation drove the most conversions. That’s it! Setting up and running an A/B test is indeed quite simple.</p>

## Do’s And Don’ts

Even though A/B testing is super-simple in concept, keep some practical things in mind. These suggestions are a result of my real-world experience of doing many A/B tests (read: making numerous mistakes).</p>

### Don’ts

*   When doing A/B testing, never ever wait to test the variation until after you've tested the control. Always test both versions simultaneously. If you test one version one week and the second the next, you're doing it wrong. It's possible that version B was actually worse but you just happened to have better sales while testing it. Always split traffic between two versions.
*   Don’t conclude too early. There is a concept called "statistical confidence" that determines whether your test results are significant (that is, whether you should take the results seriously). It prevents you from reading too much into the results if you have only a few conversions or visitors for each variation. Most A/B testing tools report statistical confidence, but if you are testing manually, consider accounting for it with an [online calculator](https://visualwebsiteoptimizer.com/ab-split-significance-calculator/).
*   Don't surprise regular visitors. If you are testing a core part of your website, include only new visitors in the test. You want to avoid shocking regular visitors, especially because the variations may not ultimately be implemented.
*   Don’t let your gut feeling overrule test results. The winners in A/B tests are often surprising or unintuitive. On a green-themed website, a stark red button could emerge as the winner. Even if the red button isn’t easy on the eye, don’t reject it outright. Your goal with the test is a better conversion rate, not aesthetics, so don’t reject the results because of your arbitrary judgment.</p>

### Do’s

*   Know how long to run a test before giving up. Giving up too early can cost you because you may have gotten meaningful results had you waited a little longer. Giving up too late isn’t good either, because poorly performing variations could cost you conversions and sales. Use a calculator (like [this one](https://visualwebsiteoptimizer.com/ab-split-test-duration/)) to determine exactly how long to run a test before giving up.
*   Show repeat visitors the same variations. Your tool should have a mechanism for remembering which variation a visitor has seen. This prevents blunders, such as showing a user a different price or a different promotional offer.
*   Make your A/B test consistent across the whole website. If you are testing a sign-up button that appears in multiple locations, then a visitor should see the same variation everywhere. Showing one variation on page 1 and another variation on page 2 will skew the results.
*   Do many A/B tests. Let’s face it: chances are, your first A/B test will turn out a lemon. But don’t despair. An A/B test can have only three outcomes: no result, a negative result or a positive result. The key to optimizing conversion rates is to do a ton of A/B tests, so that all positive results add up to a huge boost to your sales and achieved goals.</p>

## Classic A/B Testing Case Studies

Here are some case studies to give you an idea of how people test in the wild.</p>

<a href="https://37signals.com/svn/posts/1525-writing-decisions-headline-tests-on-the-highrise-signup-page">Writing Decisions: Headline Tests on the Highrise Sign-Up Page</a>
37signals tested the headline on its pricing page. It found that “30-Day Free Trial on All Accounts” generated 30% more sign-ups than the original “Start a Highrise Account.”

<a href="https://37signals.com/svn/posts/1525-writing-decisions-headline-tests-on-the-highrise-signup-page"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/13d73562-ef8b-4249-885a-dd4cc95acb9e/hrhq-signuphead-30day60sec.png" alt="37signals A/B test" width="530" height="140" /></a>

<a href="https://founderdaily.wordpress.com/2011/05/05/dustin-curtis-awkwardly-ending-all-conversations-in-you-should-follow-me-on-twitter-here/">You Should Follow Me on Twitter Here</a> (Dustin Curtis)
This much-hyped split-test involved testing multiple versions of a call to action for Twitter followers. Dustin found that “You should follow me on Twitter here” worked 173% better than his control text, “I’m on Twitter.”

<a href="https://founderdaily.wordpress.com/2011/05/05/dustin-curtis-awkwardly-ending-all-conversations-in-you-should-follow-me-on-twitter-here/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/858450db-1079-4fe4-b143-cc20fe4edfa0/dustin.png" alt="You should follow me on Twitter here" width="488" height="59" /></a>

<a href="https://vwo.com/blog/human-landing-page-increase-conversion-rate/">Human Photos Double Conversion Rates</a>
A surprising conclusion from two separate A/B tests: putting human photos on a website increases conversion rates by as much as double. Scientific research backs this up, saying that we are subconsciously attracted to images with people.</p>

<a href="https://vwo.com/blog/human-landing-page-increase-conversion-rate/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/38f651fd-d154-4dce-8f1d-ee3dac36cf01/human.png" alt="Human photos vs. generic icon" width="415" height="184" /></a>

<a href="https://www.fourhourworkweek.com/blog/2009/08/12/google-website-optimizer-case-study/">Google Website Optimizer Case Study: Daily Burn, 20%+ Improvement</a> (Tim Ferriss)
A simple variation that gave visitors fewer options too choose from resulted in a 20% increase in conversions. The winning version was also much easier on the eye than the control in its detail and text.</p>

<a href="https://www.fourhourworkweek.com/blog/2009/08/12/google-website-optimizer-case-study/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2a4c12b3-ccf2-4932-af00-2c4bb75634d7/gymnii.jpg" alt="Home page screenshot" width="300" height="241" /></a>

<a href="https://visualwebsiteoptimizer.com/split-testing-blog/ab-test-case-study-how-two-magical-words-increased-conversion-rate-by-28/">Two Magical Words Increased Conversion Rate by 28%</a>
The words “It’s free” increased the clicks on this sign-up button by 28%, illustrating the importance of testing call-to-action buttons and how minor changes can have surprisingly major results.</p>

<a href="https://visualwebsiteoptimizer.com/split-testing-blog/ab-test-case-study-how-two-magical-words-increased-conversion-rate-by-28/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e22ce855-a45a-4fd1-a14d-f0ec2244ccdb/its-free-shot.png" alt="It's free screenshot" width="440" height="70" /></a>

<strong>Changing the Sign-Up Button from Green to Red</strong>
Along with its other A/B tests, CareLogger increased its conversion rate by 34% simply by changing the color of the sign-up button from green to red!

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a14f4225-df6a-456e-9b5d-2786af208537/get-started.png" alt="Green v/s Red" width="580" height="122" />

<a href="https://www.getelastic.com/single-vs-two-page-checkout/">Single page vs. multi-step checkout</a>
If you have an online store, it is quite common to see visitors abandoning the purchase process at the time of checkout. This A/B test found out that a single page checkout process works much better at completing sales than multiple-page checkout process.</p>

<a href="https://www.getelastic.com/single-vs-two-page-checkout/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/55944187-fc32-4532-bca9-35475762bd72/getelastic.jpg" alt="checkout" width="300" height="283" /></a>

<a href="https://www.lukew.com/ff/entry.asp?1007">"Mad Libs" style form increases conversion 25-40%</a>
Defeating conventional wisdom, in this A/B test it was found out that a <em>paragraph-styled</em> form with inline input fields worked much better than traditional form layout. Though the result was probably specific to their offering as it wasn't replicated in <a href="https://www.kalzumeus.com/2010/02/27/lesson-from-madlibs-signup-fad-do-your-own-tests/">another, separate A/B test</a>.</p>

<a href="https://www.lukew.com/ff/entry.asp?1007"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a86ab715-ff00-41e4-846d-29e4466ee8ee/madlibs.gif" alt="madlibs" width="558" height="164" /></a>

<a href="https://vwo.com/blog/how-aquasoft-increased-their-sales-by-20-doing-ab-split-tests-in-multiple-phases/">Complete redesign of product page increased sales by 20%</a>
A software product company redesigned their product page to give it a modern look and added trust building elements (such as seals, guarentees, etc.). End result: they managed to increase total sales by 20%. This case study demonstrates the effect of design on sales.</p>

<a href="https://vwo.com/blog/how-aquasoft-increased-their-sales-by-20-doing-ab-split-tests-in-multiple-phases/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/21f879d2-8aec-4666-a3ab-62e034376731/aquasoft.png" alt="aquasoft" width="450" height="291" /></a>

<a href="https://www.marketingexperiments.com/blog/research-topics/response-capture-case-study.html">Marketing Experiments response capture case study – triple digit increase in conversions</a>
Through a series of A/B tests they optimized the mailing list opt-in rate by 258%. Focus was to remove all distractions and require the visitor to only provide email address. For completing his/her complete profile, the landing page motivated the visitors with an Amazon gift card (which was again split tested).</p>

<a href="https://www.marketingexperiments.com/blog/research-topics/response-capture-case-study.html"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e3fd26e1-02ec-485d-8f40-cea1c5288435/marketing-experiments.jpg" alt="marketing-experiments" width="300" height="225" /></a>

## Resources For Deep-Diving Into A/B Testing

If you’ve read this far, then A/B testing has presumably piqued your interest. Here, then, are some cherry-picked resources on A/B testing from across the Web.

*   [A Roadmap To Becoming An A/B Testing Expert](https://www.smashingmagazine.com/2014/07/roadmap-to-becoming-an-a-b-testing-expert/)
*   [Multivariate Testing 101: A Scientific Method Of Optimizing Design](https://www.smashingmagazine.com/2011/04/multivariate-testing-101-a-scientific-method-of-optimizing-design/)
*   [Multivariate Testing In Action: Five Simple Steps](https://www.smashingmagazine.com/2010/11/multivariate-testing-in-action-five-simple-steps-to-increase-conversion-rates/)
*   [In Defense Of A/B Testing](https://www.smashingmagazine.com/2010/08/in-defense-of-a-b-testing/)

### Get Ideas for Your Next A/B Test

*   [Which Test Won?](https://whichtestwon.com/) A game in which you guess which variation won in a test.
*   [101 A/B Test Tips](https://www.conversion-rate-experts.com/articles/101-google-website-optimizer-tips/) A comprehensive resource of tips, tricks and ideas.
*   [ABtests.com](https://abtests.com/) A place to share and read A/B test results.
*   [A/B Ideafox](https://visualwebsiteoptimizer.com/ideafox.php) A search engine for A/B and multivariate case studies.</p>

### Introductory Presentations and Articles

*   [Effective Testing](https://elem.com/~btilly/effective-ab-testing/) By Ben Tilly.
*   [Practical Guide to Controlled Experiments on the Web](https://exp-platform.com/Documents/GuideControlledExperiments.pdf) (PDF) From Microsoft Research.
*   [Introduction to A/B Tests](https://20bits.com/articles/an-introduction-to-ab-testing/) From the 20bits blog

### The Mathematics of A/B Testing

*   [Statistics for A/B Tests](https://20bits.com/articles/statistical-analysis-and-ab-testing/) From the 20bits blog.
*   [How Not to Do A/B Tests](https://www.evanmiller.org/how-not-to-run-an-ab-test.html)
*   [What You Should Know About the Mathematics of A/B Tests](https://vwo.com/blog/what-you-really-need-to-know-about-mathematics-of-ab-split-testing/) From my own blog.
*   [Easy Statistics for AdWords A/B and Hamsters](https://blog.asmartbear.com/easy-statistics-for-adwords-ab-testing-and-hamsters.html)
*   [Statistical Significance and Other A/B Test Pitfalls](https://www.cennydd.co.uk/2009/statistical-significance-other-ab-test-pitfalls/)

{{< signature "al" >}}

