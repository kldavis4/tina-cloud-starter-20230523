---
title: How To Improve Your Email Workflow With Modular Design
slug: improve-your-email-workflow-with-modular-design
image: 'https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4a7bb423-0fe5-48b5-8626-343819e9b8c9/email.png'
date: 2014-08-04T16:32:49.000Z
author: briangraves
description: >-
  Whether you’re in a Fortune 500 company or part a two-person team launching
  your first web app, email is one of the most important tools for reaching your
  customer base. But with the [ever-growing
  number](https://www.smashingmagazine.com/2013/08/14/email-marketing-for-mobile-app-creators-2/)
  of [emails to
  send](https://medium.com/the-growth-hackers-cookbook/c6303f3b6e8c), getting
  them all out the door can seem a little overwhelming.

  By putting in place a solid email design workflow, you’ll be able to regularly
  **ship engaging and mobile-friendly emails with ease**.
categories:
  - Coding
  - Workflow
  - Marketing
  - HTML Emails
  - Emails
  - Design Systems
  - Modular Design
---
Whether you’re in a Fortune 500 company or part a two-person team launching your first web app, email is one of the most important tools for reaching your customer base. But with the <a href="https://www.smashingmagazine.com/2013/08/14/email-marketing-for-mobile-app-creators-2/">ever-growing number</a> of <a href="https://medium.com/the-growth-hackers-cookbook/c6303f3b6e8c">emails to send</a>, getting them all out the door can seem a little overwhelming. By putting in place a solid email design workflow, you’ll be able to regularly ship engaging and mobile-friendly emails with ease.</p>

## Complexity Meets Adaptation

In addition to the increasing number of emails, the need for personalization and high quality and the introduction of responsive design have turned what was once a simple process of writing HTML and CSS in your favorite text editor into something seemingly more complex. A number of <a href="https://github.com/mailchimp/Email-Blueprints">customizable templates</a>, <a href="https://www.campaignmonitor.com/blog/post/4211/introducing-canvas-a-new-way-to-build-emails">editors</a>, <a href="https://responsiveemailresources.com/">tools</a> and even full-fledged <a href="https://zurb.com/ink/">email frameworks</a> have popped up to deal with this newfound complexity.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [The Art And Science Of The Email Signature](https://www.smashingmagazine.com/2010/02/the-art-and-science-of-the-email-signature/)
*   [Email Is (Still) Important And Here Is Why](https://www.smashingmagazine.com/2011/07/email-is-still-important-and-here-is-why/)
*   [Making Responsive HTML Email Coding Easy With MJML](https://www.smashingmagazine.com/2017/01/making-responsive-html-email-coding-easy-with-mjml/)
*   [An Introduction To Building HTML Email For Web Developers](https://www.smashingmagazine.com/2017/01/introduction-building-sending-html-email-for-web-developers/)

{{% feature-panel %}}

All of these new tools have their advantages, and many can be <a href="https://medium.com/@victorgarcia/a-workflow-for-responsive-emails-using-ink-and-grunt-32d607879082">combined</a> into a workflow that best fits you and your team. But even with a great set of new tools at your disposal, <strong>how do you structure your workflow</strong> to allow for continual iteration and quick turnaround?

## Enter Modular Design

Modular design is the method of creating a system of self-contained components that can be stacked, rearranged and used or not used, case by case. The goal is to be able to easily change or adapt individual design patterns without altering the system as a whole. Adopting modular design and reusable patterns into your email design workflow can <strong>improve the quality and consistency</strong> of what you send, while speeding up your daily output.

Setting up a modular email design workflow involves three basic steps:

1.  Create the design system.
2.  Set up a reusable framework.
3.  Test and iterate on what you send.

Let’s look in depth at how we can accomplish each step in the process.</p>

## 1\. Create A Design System

The easiest way to streamline iteration is to break down each of your common design use cases into a system of self-contained components, each one a LEGO block, made up of content and media, that you can snap together into numerous configurations. Doing this will enable you to build a nearly infinite number of emails with ease.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6fa76f1c-6c07-438a-95e9-aa5a28aec49f/01-modular-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8e4059fb-a275-45ff-9294-6e0bbd8feb88/01-modular-opt-500.png" alt="Think of your designs as Lego blocks, made up of content &amp; media." width="477" height="278" /></a><figcaption>Think of your designs as LEGO blocks, made up of content and media. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6fa76f1c-6c07-438a-95e9-aa5a28aec49f/01-modular-opt.png">View large version</a>)</figcaption></figure>

### Anticipate Use Cases

When designing your modular email system, the first step is to anticipate your use cases. Ask yourself what type of emails you typically send. Are they mostly transactional? Promotional? Informational? While all emails will likely have the same basic elements, such as a header and footer, a transactional email might need shipment information, ordering details, payment details, a contact section, and product upsells or similar products.

A newsletter might have simpler needs, such as introductory copy, a featured story, a hero image and secondary stories. <strong>Defining the content needs of the emails</strong> that you send will enable you to anticipate the common use cases that you’ll need to plan for along the way.</p>

### Design A Pattern Library

Once you determine common use cases, you can start to design individual components according to your needs. Whether you use Photoshop or jump right into the browser, remember to keep each component as self-contained as possible. Designing several variations of each use case might also be helpful.

Having several options for a “featured story” component, for instance, allows for flexibility and keeps things from getting stagnant over time. The patterns in your library will eventually become partials within your framework, easily referred to and called upon when needed.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/314a86b7-f73c-4aeb-a3e7-a79e675216e9/02-patterns-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/60c04315-ef1b-44c5-9dff-deac07b5e118/02-patterns-opt-500.png" alt="Turn your use cases into modular patterns" width="476" height="287" /></a><figcaption>Turn your use cases into modular patterns. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/314a86b7-f73c-4aeb-a3e7-a79e675216e9/02-patterns-opt.png">View large version</a>)</figcaption></figure>

### Keep Your Pattern Library Up To Date

As new use cases arise, use your existing patterns as necessary. However, unexpected use cases will probably arise; one benefit of the modular system is that you need to design only a single component to address this situation. As you create and add patterns, make sure to <strong>keep the entire design system up to date and organized</strong>. Leaving components scattered or out of sync will make the system difficult to use. The easiest way to keep everything in sync is to turn your system into a framework.</p>

## 2\. Set Up A Framework

From here, incorporating your design patterns into an out-of-the-box templating system or framework is possible. And if you’re not interested in navigating the chaotic world of Outlook or Gmail, with all of their quirks, or if you need to get something out the door with minimal configuration, then options like Zurb’s <a href="https://zurb.com/ink/">Ink</a> will do a lot of the heavy lifting for you.

But if you send a decent volume of email, then creating your own custom framework could lead to huge gains. By creating your own framework, you can add in time-saving custom helpers, keep the markup light and easy to work with, and even hook directly into your email service provider. Not to mention that you can <strong>create more customized layouts</strong> to complement all-in-one solutions. The long-term gains in quality and efficiency from setting up your own framework can be huge.</p>

### Build on Top of a Static Website Generator

Adding features and tools such as Sass, YAML data and localization to your framework could also be beneficial. The easiest way to do this is by integrating your framework with a static website generator. The building blocks that are common to email and the web will enable you to repurpose almost any website generator for your email workflow.</p>

<a href="https://middlemanapp.com/">Middleman</a> is a great option and one that I’ve found ticks all of the major boxes:

*   The structure of projects as layouts, partials and pages perfectly fits our mental model of modular email.
*   [Sass](https://sass-lang.com/) is already integrated. Sass is an amazing addition to any responsive email workflow. Common workarounds such as the one for [Yahoo Mail’s attribute selector](https://www.emailonacid.com/blog/details/C13/stop_yahoo_mail_from_rendering_your_media_queries) become an afterthought through the clever use of selector inheritance. Sass also provides powerful features such as variables, mixins and CSS minification to cut down on file size.
*   YAML data and front matter allow you to fully separate content from design and loop through data for easy prototyping.
*   If you’re sending to a large and diverse audience in multiple languages, then localization can dynamically generate that diverse set of data relatively painlessly.
*   A myriad of hooks enable us to easily create custom helpers for email platform-specific needs.
*   Middleman is Ruby-based, making it easily extensible.</p>

### Set Up A Boilerplate

Once you’ve chosen a static website generator that meets your needs, then it’s time to set up your base boilerplate. A boilerplate includes such things as a reset file, the CSS or Sass structure, an optional custom grid system and a base template.</p>

<strong>Base Layout Template</strong>

A basic template will serve as your base layout structure and will allow global elements to be shared across all emails. Preheaders, headers and footers will usually stay consistent across emails. If this is the case with your designs, then you can safely build these into your layout’s template. The safer approach is either to build out and include these elements as partials or, if these elements will likely move or change in particular emails, to wrap the markup in conditional statements.

Your base email template should include at least the following:

*   `DOCTYPE` HTML5 is the friendliest for designing responsive emails. Remember that certain clients will either strip out or change your `DOCTYPE`.
*   `head` A lot is important to include here: meta tags for proper character encoding, title tags for anyone viewing the standalone version of your email in a browser, reset styles, embedded media query styles, any styles to be inlined and the `viewport` meta tag to set the viewport’s width.
*   `body` In addition to the standard `body` tag, wrap your entire email in a 100%-width table and cell structure, as shown below. The table with the `body` class will act as the `body`, thereby overcoming the drawback of certain clients removing the `body` tag.
*   `yield` This is from where all of your modules for individual emails will be pulled.</p>

<pre><code class="language-markup">
&lt;!DOCTYPE html&gt;
&lt;html lang="en"&gt;

&lt;head&gt;
  &lt;meta http-equiv="Content-Type" content="text/html; charset=utf-8" /&gt;
  &lt;meta name="viewport" content="width=device-width"&gt;
  &lt;title&gt;&lt;%= data.page.title %&gt;&lt;/title&gt;

  &lt;%= inline_stylesheet 'template/inline' %&gt;
  &lt;%= stylesheet_link_tag 'template/mq' %&gt;
&lt;/head&gt;

&lt;body&gt;
  &lt;table class="body"&gt;
    &lt;tr&gt;
      &lt;td class="header" &gt;
        [Header content]
      &lt;/td&gt;
    &lt;/tr&gt;
    &lt;tr&gt;
      &lt;td class="main" &gt;
        &lt;%= yield %&gt;
      &lt;/td&gt;
    &lt;/tr&gt;
    &lt;tr&gt;
      &lt;td class="footer" &gt;
        [Footer content]
      &lt;/td&gt;
    &lt;/tr&gt;
  &lt;/table&gt;
&lt;/body&gt;
&lt;/html&gt;</code></pre>

**Partials Based on Modules**

Keep the markup of your individual design patterns inside of partials, to keep the design system truly modular. This will allow the markup for each module to be self-contained. Taking a modular approach with both your designs and your markup becomes truly powerful. Once it’s built, you should be able to <strong>move each design pattern around to different areas of the template</strong> without breaking the module, the template or any other modules surrounding it. When you’re setting up the framework, build out each module that you’ve planned for in this way.

Taking the use case from our last example, the modular markup for a featured story would look like this:

<pre><code class="language-markup">&lt;table class="featured-story"&gt;
  &lt;tr&gt;
    &lt;td class="col"&gt;
      &lt;img src="#" alt="" /&gt;
    &lt;/td&gt;
    &lt;td class="col"&gt;
      &lt;table&gt;
        &lt;tr&gt;
          &lt;td class="title"&gt;
            [Story Title]
          &lt;/td&gt;
        &lt;/tr&gt;
        &lt;tr&gt;
          &lt;td class="abstract"&gt;
            [Story Abstract]
          &lt;/td&gt;
        &lt;/tr&gt;
        &lt;tr&gt;
          &lt;td class="cta"&gt;
            &lt;a href="#"&gt;CTA&lt;/a&gt;
          &lt;/td&gt;
        &lt;/tr&gt;
      &lt;/table&gt;
    &lt;/td&gt;
  &lt;/tr&gt;
&lt;/table&gt;</code></pre>

**Sass Structure**

Following OOCSS or <a href="https://smacss.com/">SMACSS</a> will maintain the modularity of your Sass. In general, keep your styles as modular as possible, just like your designs and markup.

One caveat when writing CSS or Sass in an email framework is that all media query-based styles must begin with an attribute selector (such as <code>td[class=example]{}</code>) in order to <a href="https://www.emailonacid.com/blog/details/C13/stop_yahoo_mail_from_rendering_your_media_queries">avoid rendering issues in Yahoo Mail</a>. An easy workaround is Sass’ ability to nest styles. Nesting all media queries in a single attribute-based selector will prevent them from being applied to each individual style. Writing your Sass in this way will increase both readability and speed while maintaining visual consistency across clients.

Following this method, the basic media queries for optimizing the template and content area above for mobile would be this:

<pre><code class="language-css">td[class=body] {
  @media only screen and (max-width: 600px) {
    .col { 
      display: block; 
      width: 100%; 
    }
    .title { 
      font-size: 22px !important; 
    }
    .abstract { 
      font-size: 16px !important; 
    }
    .cta a { 
      display: block;
      width: 100%;
    }
  }
}</code></pre>

### Put It All Together

With a base framework and modular design patterns in place, it’s now time to snap all of the LEGO blocks together. Create a page for each email that you’re building for your framework. This page should be wrapped with your base template and should call any modular patterns that you need.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1c4579b6-3a4c-4f19-90da-287d4862db21/03-email-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ab386461-25ad-4dce-98c1-bf2ddb8931b4/03-email-opt-500.png" alt="Thinking in a modular way will enable you to build emails like LEGO blocks." width="372" height="278" /></a><figcaption>Thinking in a modular way will enable you to build emails like LEGO blocks. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1c4579b6-3a4c-4f19-90da-287d4862db21/03-email-opt.png">View large version</a>)</figcaption></figure>

<pre><code class="language-ruby">---
title: Example Email
layout: template
---
&lt;%= partial "featured-story" %&gt;
&lt;%= partial "responsive-image" %&gt;
&lt;%= partial "social-callout" %&gt;</code></pre>

### Automate Common Tasks

One of the greatest efficiencies you can gain in your workflow is to automate frequent tasks. This typically means inlining CSS, optimizing images, sending tests, and integrating templates and modules with your email service provider. Most common tasks can be easily integrated with Rake tasks, Ruby Gems and/or Grunt.</p>

<strong>CSS Inlining</strong>

The safest method is to inline styles whenever possible because certain email clients strip out styles from the head of documents. If you’re used to the common web workflow of writing styles in a separate sheet, then getting used to this will be hard. It can become a hindrance to modularity, and if you’re trying to use Sass to style, then this obviously becomes impossible to do manually.

Luckily, we have several options to automatically inline styles at build time. If you’re using a Ruby-based tempting engine, then the best option is to include the <a href="https://github.com/premailer/premailer">Premailer Gem</a> in your project. Premailer automatically runs through your style sheet and inlines styles while preserving any existing styles when called. This is a huge time-saver, and it keeps markup manageable.</p>

<strong>Testing</strong>

There are several ways to test how your email looks. The first stage in my process is to design and check the rendering in Chrome. Once the designs are completed, it’s time to jump into a more automated tool to check rendering across the board. <a href="https://litmus.com/">Litmus</a> is a web application, like <a href="https://www.browserstack.com/">BrowserStack</a> but focused on delivering screenshots of your email across a wide variety of clients.

You can send your emails to Litmus in a variety of ways, but if you’re using Grunt in the framework, then the easiest way is by using <a href="https://www.npmjs.org/package/grunt-litmus">Grunt-Litmus</a>. Grunt-Litmus automates the process of getting tests to your account and lets you check rendering in clients of your choice.</p>

<pre><code class="language-javascript">module.exports = {
  test: {
    src: ['email.html'],
    options: {
      clients: ['android22', 'android4'...]
      username: "username",
      password: "password",
      url: "https://yourcompany.litmus.com"            
    }
  }
};</code></pre>

Testing on real devices is another common approach, especially vital with things like CSS animation and embedded video. If you have a device lab set up with a common email address, an easy way to trigger an email delivery directly from your framework is to use the Ruby Mail Gem.</p>

<strong>Hook Into Your Email Service Provider</strong>

If you’re using an email platform that provides access (such as <a href="https://help.exacttarget.com/en-US/technical_library/web_service_guide/getting_started_developers_and_the_exacttarget_api/">ExactTarget</a> or <a href="https://apidocs.mailchimp.com/">MailChimp</a>), then you can set up your project to hook directly into the API and push your template along with individual modules into the system on command. Doing this allows you to build locally in the framework, keeping everything modular and under source control, and still push to your email service provider quickly and easily as you iterate. How you hook into your provider will obviously vary by platform, but definitely keep this in mind when setting up a modular framework.</p>

## 3\. Iterate On Your Designs

The periodical nature of email lends itself well to design iteration. If you’re sending emails daily or weekly, then you have ample room to A/B test your design decisions. No matter what workflow options you adopt, make sure to <a href="https://marketingland.com/the-email-metric-you-should-be-tracking-but-arent-8879">track important email metrics</a> and use available data to improve your core design, remembering that a better experience is usually more important than any single data point.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6321048b-22ce-4ac7-99c4-1c302e10e0de/04-iterate-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ad273754-c38b-4b55-8610-dddc03a3663b/04-iterate-opt-500.png" alt="The periodical nature of email makes for easy testing and iteration." width="476" height="278" /></a><figcaption>The periodical nature of email makes for easy testing and iteration. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6321048b-22ce-4ac7-99c4-1c302e10e0de/04-iterate-opt.png">View large version</a>)</figcaption></figure>

Don’t reinvent the wheel every time you send an email; rather, make continual incremental changes as warranted by your metrics. The benefits of a modular design workflow should make these incremental changes fairly painless as you swap components in and out. The important thing is not to let your designs stagnate.</p>

## Conclusion

Incorporating a modular approach and a custom framework into your email workflow can lead to increased productivity and make it easier for you to iterate on your designs. You will have to <strong>make an initial investment of time</strong> to get everything up and running, but if you send a decent volume of email and can afford the initial investment, then the result will improve your designs, the customer experience and your engagement rates, leading to happier customers and increased revenue.</p>

### Links

*   [Ink](https://zurb.com/ink/), Zurb A framework for rapid development of responsive emails.
*   “[A Workflow for Responsive Emails Using Ink and Grunt](https://medium.com/@victorgarcia/a-workflow-for-responsive-emails-using-ink-and-grunt-32d607879082),” Victor Garcia, Medium
*   [Middleman Email Template](https://github.com/degdigital/MiddlemanEmailTemplate), DEG A Middleman project template customized for building emails.
*   [Middleman 3.0.x Project Template: HTML Email Boilerplate HAML](https://github.com/dannyprose/Middleman-HTML-Email-HAML), Danny Prose A Middleman template for [HTML Email Boilerplate](https://htmlemailboilerplate.com/), converted to HAML.

{{< signature "al, , il, ml" >}}

