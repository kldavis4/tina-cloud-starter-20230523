---
title: 'Standardizing <code>&lt;select&gt;</code> And Beyond: The Past, Present And Future Of Native HTML Form Controls'
slug: standardizing-select-native-html-form-controls
author: stephanie-stimac
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2b7dc50f-b0c2-4055-81cb-edb2b992daf1/standardizing-select-native-html-form-controls.png
date: 2020-11-18T12:00:00.000Z
summary: >-
  Working with native HTML Form Controls has been such a pain point for web developers, from styling to extending them, the limitations are so great that countless dev hours have been spent recreating them. But why are form controls so difficult to work with?<br /><br />In this article, Stephanie dives into the past by going back to the beginning of HTML and tracing the evolution of form controls through to the present and the current state of working with them. She shares her thoughts and takes a glimpse at what the future holds for working with these essential pieces of the web.
description: >-
  In this article, Stephanie dives into the past by going back to the beginning of HTML and tracing the evolution of form controls through to the present and the current state of working with them.
categories:
  - HTML
  - Browsers
  - Coding
  - Forms
---

Whether it’s an input to search a website or a text input field and submit button for comments on a blog or a checkbox to accept the terms and conditions of a website, form controls are some of the most common components and provide the foundation for interactivity on the web. They are everywhere online and have been since the beginning of HTML.

They were introduced in the [HTML 2.0 specification](https://www.w3.org/MarkUp/html-spec/html-spec_toc.html) in 1995, but, despite their early origins, the ease with which developers can style or customize them ranges from extremely easy to nearly impossible. This has led to developers scrapping these native controls altogether and building custom ones from scratch which can be problematic and time-consuming.

Controls built from scratch lack the features that come with native ones, such as accessibility and security, so there’s a plethora of extra work to make custom controls accessible and secure. We’ll look at the history of form controls that led us to where we are today, the current state of working with them, and a brief glimpse of the work being done to fix this space.

## A Brief History Of HTML Controls

After the release of the first web browser in the early ’90s from Tim Berners-Lee called WorldWideWeb (later renamed to Nexus), multiple other web browsers were being developed and made available to the public. But the preliminary HTML specification was extremely basic at the time, with only a handful of tags available for text markup.

As the new vendors started to iterate on their new browsers, each one started to implement new HTML tags to help fill out feature gaps and start to add support for things like images and other interactive elements. This created a growing rift in HTML as there was no standard or specification for it yet.

In 1993, Berners-Lee and Dan Connolly had worked on defining the first specification for HTML but the draft expired in early 1994. The first HTML Working Group was established after that first draft expired and completed the first specification for [HTML 2.0](https://www.w3.org/MarkUp/html-spec/html-spec_toc.html) that would become the basis for HTML Standards going forward.

The HTML 2.0 specification took note of the current landscape of HTML features across different browsers, and rather than break the web, included those features that were already available in browsers in the spec.  

HTML 2.0 gave the web the first specifications for form functionality for the following form types:  

*   `form`
*   `input (type=):`
    *   `text`
    *   `password`
    *   `radio`
    *   `image`
    *   `hidden`
    *   `submit`
    *   `reset`
*   `select`
*   `option`
*   `textarea`

The spec standardized the method for users to enter data into an HTML document and how that data was to be used to perform an action such as logging into a website. It did not, however, define the different parts of the controls or how each control would be constructed and rendered in the browser.

{{% feature-panel %}}

### Technical And Style Limitations

In 1995, there was no styling language established yet, which is where the first style of limitations with form controls came into play. Browsers had to rely on the operating system to style and render form controls, which at the time meant there was a dependency on the operating system both technically and stylistically.

This wasn’t something developers could access to customize, and there wasn’t even a way to do so without a styling language. Despite the idea of style sheets in browsers having been around since 1990 with Berners-Lee’s initial browser, not all the browsers that had appeared in the 90s offered a way for developers to style things. If they did, they heavily limited what was style-able.

But as the web flourished and CSS was established as the styling language for it, form controls were still off the table when it came to styling or customizing them. They were meant to be a reflection of the operating system they were on. That level of styling and customization wasn’t a requirement at the time.

The CSS 2.1 specification, which waffled between working draft status and candidate recommendation from 2004-2010, even specified that [browsers didn’t have to apply CSS to form controls](https://www.w3.org/TR/CSS21/conform.html%22%20/l%20%22conformance).

<blockquote>“CSS 2.1 does not define which properties apply to form controls and frames, or how CSS can be used to style them. User agents may apply CSS properties to these elements. Authors are recommended to treat such support as experimental. A future level of CSS may specify this further.”<br /><br /><a href="https://www.w3.org/TR/CSS21/conform.html#conformance">UA Conformance</a>, CSS 2.1 Specification, W3C</blockquote>

It was left entirely up to user agents to provide styling for the form controls. Even as multiple browsers became available on operating systems, [rendering wasn’t consistent across browsers](https://www.456bereastreet.com/archive/200410/styling_even_more_form_controls/).

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bee0fa57-1c83-4c63-8432-13486f12df7a/buttons-456bereastreet.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bee0fa57-1c83-4c63-8432-13486f12df7a/buttons-456bereastreet.jpg" sizes="100vw" caption="Multiple form controls across browsers in 2004 (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bee0fa57-1c83-4c63-8432-13486f12df7a/buttons-456bereastreet.jpg'>Large preview</a>)" alt="A group of native <button> controls from different browsers and operating systems that highlights the varying native styles between the same component." >}}

As developers started to ask for control over styling various controls, a proposal for the <code>[appearance property](https://developer.mozilla.org/en-US/docs/Web/CSS/appearance)</code> was included, but later dropped from the CSS Basic User Interface Module Level 3 standard. The appearance proposal was supposed to “provide additional CSS mechanisms to simulate the appearance of various standard form elements” but was never actually implemented as designed and support across browsers varies wildly.

Developers started to use `appearance: none;` to remove all native styling and attempt to apply their own CSS to form controls. However, the inconsistency in what can be styled across different form controls once `appearance: none;` is applied varies widely and inconsistently across browsers, and doesn’t solve the real problem of not being able to style form controls.

## Working With HTML Controls On The Modern Web

With the pace at which the web evolves, you might think that this problem around styling form controls would be closer to being solved, or at least easier than it was 10-15 years ago. While a handful of form controls can be easily styled by CSS, like the button element, most form controls fall into a bucket of either [requiring hacky CSS or are still unable to be styled at all by CSS](https://developer.mozilla.org/en-US/docs/Learn/Forms/Styling_web_forms).

Despite form controls no longer taking a style or technical dependency on the operating system and using modern rendering technology from the browser, developers are still unable to style some of the most used form control elements such as `<select>`. The root of this problem lies in the way the specification was originally written for form controls back in 1995.

The initial specification never standardized the parts that comprise each form control, it only standardized the method to enter data into an HTML document and for that data to be used to perform an action leading to browsers defining how they each built their form controls. Each form control had a standardized purpose, but how that purpose was constructed was up to interpretation.

Without standardized parts, trying to open the different parts of more complex controls to enable developers to have more control over styling creates issues with cross-browser compatibility. If only one browser has implemented access to different parts of a select to customize the appearance fully, that is ultimately useless for the developer if the end goal is to have controls render the same across all browsers.

But rendering inconsistency and inability to style consistently across browsers is not the only thing developers are missing from native form controls. There is a lack of extensibility with native controls. Developers cannot add or remove functionality to native controls.

The video element is a great example of this:

<pre><code class="language-markup">&lt;video controls width="1080"&gt;&lt;/video&gt;
</code></pre>

The `controls` attribute is the only way to show or hide the playback controls for the video element with no option to customize or extend what is shown. You either get all the video controls or none leading to a poor experience with the native element.

Between a severe lack of control over styling and a lack of extensibility, it’s no wonder developers have abandoned using native controls and gone about rebuilding them from scratch.

When rebuilding from scratch though, a developer has to consider all the different pieces they need to add back into the control to reach parity with a native control’s features to test in the first place. With accessibility, for example, it’s not just adding the appropriate [ARIA roles](https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/Roles) or attributes, as ARIA only provides the semantics that hook up the different parts to the correct accessibility APIs. Keyboard functionality to tab through a control and focus needs to be added back in on top of ARIA. JavaScript may be required for some of this functionality, so developers need to consider what happens to that control if a user has JavaScript disabled. There are performance implications to consider as more JavaScript is added to controls as well.

And then there’s developer time going toward testing for accessibility, performance, and security, things that are built in with native controls, and they may not always have the support to properly test those things across all browsers.

It’s also not a situation where a developer can write that code once and be done with it.  

When a developer creates these custom elements, they also need to be maintained in the long run. What if a piece of the code being used is deprecated from the web platform that breaks functionality? What if accessibility requirements change or evolve? What if there is a security vulnerability? The cost of maintaining the custom elements over time can end up being more expensive and more time-consuming.

The current state of working with controls on the modern web is that countless developer hours are being lost to rewriting controls from scratch, as custom elements due to [a lack of flexibility in customizability and extensibility of native form controls](https://www.gwhitworth.com/blog/2019/10/can-we-please-style-select/). This is a massive gap in the web platform and has been for years. Finally, something is being done about it.

{{% ad-panel-leaderboard %}}

## Solving The Pain Points Around Form Controls  

[Greg Whitworth conducted some research on form controls](https://gwhitworth.com/blog/2019/07/form-controls-components/) while working on the Microsoft Edge web platform team last year to validate everything we’ve heard candidly from developers: that native form controls are difficult to work with and don’t meet their needs.

In an initial survey that had 1,400 respondents, one of the questions asked was which form controls did respondents re-create.

The top 3 were: 

1. Select (10.7%) 
1. Checkbox (10.2%) 
1. Date (9.5%) 

One of the follow-up questions then asked of respondents was “why are you recreating form controls?” and these were the top 3 responses:

*   36.6% said they couldn’t change the appearance sufficiently 
*   31.6% wanted to add functionality
*   27.3% said browser inconsistencies

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3f31f32e-f462-40cf-884a-2f675867a8e7/controls-pie-chart.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3f31f32e-f462-40cf-884a-2f675867a8e7/controls-pie-chart.jpg" sizes="100vw" caption="A breakdown of all the different reasons controls are created from scratch. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3f31f32e-f462-40cf-884a-2f675867a8e7/controls-pie-chart.jpg'>Large preview</a>)" alt="Pie chart breakdown of the reasons why controls are created from scratch: 36.6% said they couldn’t change the appearance sufficiently, 31.6% wanted to add functionality, 27.3% said browser inconsistencies, 2.8% accessibility issues, 1.8% other" >}}

Browser inconsistencies in the context of controls usually relate to appearance. If we group those respondents in with those who marked “couldn’t change appearance sufficiently”, that’s over 60% of respondents sacrificing built-in accessibility and performance with native controls because of appearance.

### Open UI

There is a huge opportunity to fix this problem space for developers and it’s incredibly important that those in positions to drive a solution for this space do so in the right way. That means working through standards proposals and drafts in the public and with the community’s feedback.

[Open UI](https://open-ui.org/) is an initiative under the [Web Incubator Community Group](https://wicg.io/), that is undertaking the task of documenting control components across design systems and analyzing design system terminology to find patterns and similarities that will help set the path for standards and native support in the browser. This work is being driven by browser vendors, framework authors, design system maintainers and is open to participation by anyone interested in this space.

This initiative isn’t to standardize how a form control looks, but to standardize form control names, their parts, states, and behaviors. This involves a heavy amount of research for each control, exploring use cases, functionality, and features that developers add to their custom components and deciding when that added functionality equates to a new control (`<select>` vs combobox is a great example of this). We expect the work being done in Open UI to integrate with other working groups by passing along recommendations and filing issues in the appropriate venues to move this work forward.

If you’re interested in getting involved in any part of Open UI, check out the [GitHub repository](https://github.com/WICG/open-ui) and the open issues. Not only is it a great project to dip your toes into if you’re interested in standards work, but the contributions and research will contribute to solving a huge pain point for developers and even designers. If you’re a designer who works with controls and components, this space is also open to you as this work integrates with design system frameworks.

{{% ad-panel-leaderboard %}}

## Standardizing Without Breaking The Web

Watching as different solutions for enabling customization of control UI have evolved over the last few months, one of the concerns that arose was around breaking native controls already out on the web.

Existing native controls will continue to work, but with the current proposal, there will be additional code that developers can use to style arbitrary parts of native control, add arbitrary content into any part of native control (with limitations, things like iframes will be blocked), and customize the UI without having to rebuild anything from scratch.

The ultimate goal is to provide developers with a high degree of flexibility over appearance and extensibility of controls. The initial explainer document on enabling custom control UI is now available for public review. This is the first step towards standardization; these changes are being driven and brought into standards bodies because of feedback from developers, so take a moment to read the explainer and the open questions and provide your feedback or thoughts on GitHub.

## A Promising Future

Developers and web designers have been asking for years for improved controls and flexibility with styling, but when we really get to the heart of it, there are so many different use cases and extensibility features that developers have implemented in custom components, especially when we start to explore controls like `<select>`.

They may seem like a small or arbitrary part of the web, but HTML Controls provide the functionality for logging into a website or submitting an order, and are essential to the web ecosystem we rely on today.

Meaningful steps are being taken to solve the pain points that developers have had for years with these components and to put standards in place that will allow for the customization that has been so highly requested.

On browser teams, we’re investing in this space because developer feedback was so consistent and abundant. If you work on the web and are interested in helping to drive this space forward, I invite you to get involved in [Open UI](https://open-ui.org/) or [provide feedback on the initial explainer for customizing controls UI](https://github.com/MicrosoftEdge/MSEdgeExplainers/blob/main/ControlUICustomization/explainer.md). We want to ensure we’re taking into consideration the needs of all developers and making the right decisions as we pursue this space.

{{< signature "jw, ra, il" >}}
