---
title: 'How To Build Resilient JavaScript UIs'
slug: build-resilient-javascript-ui
author: callum-hart
image: >-
  blob:https://www.smashingmagazine.com/c8b93225-8b34-431c-94f1-2f2d0a4fb95a
date: 2021-08-03T11:00:00.000Z
summary: >-
  Embracing the fragility of the web empowers us to build UIs capable of adapting to the functionality they can offer, whilst still providing value to users. This article explores how graceful degradation, defensive coding, observability, and a healthy attitude towards failures better equips us before, during, and after an error occurs.
description: >-
  Resilience is intrinsic to the web and therefore us, web developers. This article explores how graceful degradation, defensive coding, observability, and a healthy attitude towards failures better equips us before, during, and after an error occurs.
categories:
  - UI
  - UX
  - Workflow
  - JavaScript
---

Things on the web can break &mdash; the odds are stacked against us. Lots can go wrong: a network request fails, a third-party library breaks, a JavaScript feature is unsupported (assuming JavaScript is even available), a CDN goes down, a user behaves unexpectedly (they double-click a submit button), the list goes on.

Fortunately, we as engineers can avoid, or at least mitigate the impact of breakages in the web apps we build. This however requires a conscious effort and mindset shift towards thinking about unhappy scenarios just as much as happy ones.

**The User Experience (UX) doesn’t need to be all or nothing &mdash; just what is usable.** This premise, known as graceful degradation allows a system to continue working when parts of it are dysfunctional &mdash; much like an electric bike becomes a regular bike when its battery dies. If something fails only the functionality dependent on that should be impacted.

UIs should adapt to the functionality they can offer, whilst providing as much value to end-users as possible.

## Why Be Resilient

Resilience is [intrinsic to the web](https://www.w3.org/TR/html-design-principles/#degrade-gracefully).

Browsers ignore invalid HTML tags and unsupported CSS properties. This liberal attitude is known as Postel’s Law, which is conveyed superbly by Jeremy Keith in [Resilient Web Design](https://resilientwebdesign.com/chapter4/):

<blockquote>“Even if there are errors in the HTML or CSS, the browser will still attempt to process the information, skipping over any pieces that it can’t parse.”</blockquote>

JavaScript is less forgiving. Resilience is extrinsic. We instruct JavaScript what to do if something unexpected happens. If an API request fails the onus falls on us to catch the error, and subsequently decide what to do. And that decision directly impacts users.

Resilience builds trust with users. A buggy experience reflects poorly on the brand. According to [Kim and Mauborgne, convenience (availability, ease of consumption)](https://hbr.org/2000/09/knowing-a-winning-business-idea-when-you-see-one) is one of six characteristics associated with a successful brand, which makes graceful degradation synonymous with brand perception.

A robust and reliable UX is a signal of quality and trustworthiness, both of which feed into the brand. A user unable to perform a task because something is broken will naturally face disappointment they could associate with your brand.

Often system failures are chalked up as "corner cases" &mdash; things that rarely happen, however, the web has many corners. Different browsers running on different platforms and hardware, respecting our user preferences and browsing modes (Safari Reader/ assistive technologies), being served to geo-locations with varying latency and intermittency increase the likeness of something not working as intended.

{{% feature-panel %}}

## Error Equality

Much like content on a webpage has hierarchy, failures &mdash; things going wrong &mdash; also follow a pecking order. Not all errors are equal, some are more important than others.

We can categorize errors by their impact. How does XYZ not working prevent a user from achieving their goal? The answer generally mirrors the content hierarchy.

For example, a dashboard overview of your bank account contains data of varying importance. The total value of your balance is more important than a notification prompting you to check in-app messages. [MoSCoWs method of prioritization](https://en.wikipedia.org/wiki/MoSCoW_method) categorizes the former as a must-have, and the latter a nice to have.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f7486947-6755-43ad-9426-5b3773aa7b14/8-resilience-is-a-feature.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f7486947-6755-43ad-9426-5b3773aa7b14/8-resilience-is-a-feature.png" width="800" height="525" sizes="100vw" caption="An example of primary versus secondary information. The account balance (£500) is primary information integral to the user experience, whereas unread notifications are a non-essential enhancement (secondary information). (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f7486947-6755-43ad-9426-5b3773aa7b14/8-resilience-is-a-feature.png'>Large preview</a>)" alt="Wireframe of a banking website. Black text on a white background. The left side displays the account balance of £500. The top right contains a notification (bell) icon and count of 3. Below the icon is a popup displaying the 3 unread items." >}}

If primary information is unavailable (i.e: network request fails) we should be transparent and let users know, usually via an error message. If secondary information is unavailable we can still provide the core (must have) experience whilst gracefully hiding the degraded component.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/09ab88dd-1e87-4c40-995f-9cbf380e4fe3/3-resilience-is-a-feature.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/09ab88dd-1e87-4c40-995f-9cbf380e4fe3/3-resilience-is-a-feature.png" width="800" height="536" sizes="100vw" caption="When the account balance is unavailable we show an error message. When unread notifications are unavailable we simply remove the count and popup from the UI, whilst preserving the semantic link <code>a href='/notifications'</code> to the notification center. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/09ab88dd-1e87-4c40-995f-9cbf380e4fe3/3-resilience-is-a-feature.png'>Large preview</a>)" alt="Wireframe of a banking website. A red icon with error message reads: Sorry, unable to load your bank balance. The top right contains a notification (bell) icon." >}}

Knowing when to show an error message or not can be represented using a simple decision tree:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f3b257e8-88c8-4c84-b567-b30641195f2d/14-resilience-is-a-feature.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f3b257e8-88c8-4c84-b567-b30641195f2d/14-resilience-is-a-feature.png" width="800" height="231" sizes="100vw" caption="Primary errors should surface to the UI, whereas secondary errors can be gracefully hidden. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f3b257e8-88c8-4c84-b567-b30641195f2d/14-resilience-is-a-feature.png'>Large preview</a>)" alt="Decision tree with 2 leaf nodes that read (from left to right): Primary error? No: Hide degraded component, Yes: Show error message." >}}

Categorization removes the 1-1 relationship between failures and error messages in the UI. Otherwise, we risk bombarding users and cluttering the UI with too many error messages. Guided by content hierarchy we can cherry-pick what failures are surfaced to the UI, and what happen unbeknownst to end-users.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/86ca5913-57f4-44e7-a77f-20a119a1de39/2-resilience-is-a-feature.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/86ca5913-57f4-44e7-a77f-20a119a1de39/2-resilience-is-a-feature.png" width="800" height="388" sizes="100vw" caption="Just because 3 errors occurred (left) doesn’t automatically mean 3 error messages should be shown. An action, such as a retry button, or a link to the previous page helps guide users what to do next. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/86ca5913-57f4-44e7-a77f-20a119a1de39/2-resilience-is-a-feature.png'>Large preview</a>)" alt="Two wireframes of different error states. The left one titled: Error message per failure, displays 3 red error notifications (1 for each failure). The right one titled: Single error message with action, shows a single error notification with a blue button below." >}}

## Prevention is Better than Cure

Medicine has an adage that prevention is better than cure.

Applied to the context of building resilient UIs, preventing an error from happening in the first place is more desirable than needing to recover from one. **The best type of error is one that doesn’t happen.**

It’s safe to assume never to make assumptions, especially when consuming remote data, interacting with third-party libraries, or using newer language features. Outages or unplanned API changes alongside what browsers users choose or must use are outside of our control. Whilst we cannot stop breakages outside our control from occurring, we can protect ourselves against their (side) effects.

Taking a more defensive approach when writing code helps reduce programmer errors arising from making assumptions. Pessimism over optimism favours resilience. The code example below is too optimistic:

<pre><code class="language-javascript">const debitCards = useDebitCards();

return (
  &lt;ul&gt;
    {debitCards.map(card =&gt; {
      &lt;li&gt;{card.lastFourDigits}&lt;/li&gt;
    })}
  &lt;/ul&gt;
);
</code></pre>

It assumes that debit cards exist, the endpoint returns an Array, the array contains objects, and each object has a property named `lastFourDigits`. The current implementation forces end-users to test our assumptions. It would be safer, and more user friendly if these assumptions were embedded in the code:

<pre><code class="language-javascript">const debitCards = useDebitCards();

if (Array.isArray(debitCards) && debitCards.length) {
  return (
    &lt;ul&gt;
      {debitCards.map(card =&gt; {
        if (card.lastFourDigits) {
          return &lt;li&gt;{card.lastFourDigits}&lt;/li&gt;
        }
      })}
    &lt;/ul&gt;
  );
}

return "Something else";
</code></pre>

Using a third-party method without first checking the method is available is equally optimistic:

<pre><code class="language-javascript">stripe.handleCardPayment(/* ... */);
</code></pre>

The code snippet above assumes that the `stripe` object exists, it has a property named `handleCardPayment`, and that said property is a function. It would be safer, and therefore more defensive if these assumptions were verified by us beforehand:

<pre><code class="language-javascript">if (
  typeof stripe === 'object' && 
  typeof stripe.handleCardPayment === 'function'
) {
  stripe.handleCardPayment(/* ... */);
}
</code></pre>

Both examples check something is available before using it. Those familiar with feature detection may recognize this pattern:

<pre><code class="language-javascript">if (navigator.clipboard) {
  /* ... */
}
</code></pre>

Simply asking the browser whether it supports the Clipboard API before attempting to cut, copy or paste is a simple yet effective example of resilience. The UI can adapt ahead of time by hiding clipboard functionality from unsupported browsers, or from users yet to grant permission.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/788ea5b0-a67a-43e8-a2f3-80e1bbb0de6e/5-resilience-is-a-feature.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/788ea5b0-a67a-43e8-a2f3-80e1bbb0de6e/5-resilience-is-a-feature.png" width="800" height="340" sizes="100vw" caption="Only offer users functionality when we know they can use it. The copy to clipboard buttons (right) are conditionally shown based on whether the Clipboard API is available. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/788ea5b0-a67a-43e8-a2f3-80e1bbb0de6e/5-resilience-is-a-feature.png'>Large preview</a>)" alt="Two black and white wireframes. The left one titled: Clipboard unavailable, displays 2 rows of numbers. The right one titled: Clipboard available, shows the same 2 numbers alongside a clipboard icon." >}}

User browsing habits are another area living outside our control. Whilst we cannot dictate how our application is used, we can instill guardrails that prevent what we perceive as "misuse". Some people double-click buttons &mdash; a behavior mostly redundant on the web, however not a punishable offense.

Double-clicking a button that submits a form should not submit the form twice, especially for [non-idempotent HTTP methods](https://developer.mozilla.org/en-US/docs/Glossary/Idempotent#technical_knowledge). During form submission, prevent subsequent submissions to mitigate any fallout from multiple requests being made.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/396cd330-df81-4582-a8e2-24c189329dd9/12-resilience-is-a-feature.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/396cd330-df81-4582-a8e2-24c189329dd9/12-resilience-is-a-feature.png" width="800" height="375" sizes="100vw" caption="Users should not be punished for their browsing habits or mishaps. Preventing multiple form submissions because of intentional or accidental double-clicks is easier than cancelling duplicate transactions at a later date. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/396cd330-df81-4582-a8e2-24c189329dd9/12-resilience-is-a-feature.png'>Large preview</a>)" alt="Two black and white wireframes. The left one titled: Double-click = 2 requests, displays a form and button (labelled submit) above a console showing 2 XHR requests to the orders endpoint. The left one titled: Double-click = 1 request, displays a form and button (labelled submitting) above a console showing 1 XHR request to the orders endpoint." >}}

Preventing form resubmission in JavaScript alongside using `aria-disabled="true"` is more usable and accessible than the `disabled` HTML attribute. Sandrina Pereira explains [Making Disabled Buttons More Inclusive](https://css-tricks.com/making-disabled-buttons-more-inclusive/) in great detail.

{{% ad-panel-leaderboard %}}

## Responding to Errors

Not all errors are preventable via defensive programming. This means responding to an operational error (those occurring within correctly written programs) falls on us.

Responding to an error can be modelled using a decision tree. We can either recover, fallback or acknowledge the error:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4804ef49-a1b1-463f-a579-f290871ca53d/6-resilience-is-a-feature.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4804ef49-a1b1-463f-a579-f290871ca53d/6-resilience-is-a-feature.png" width="800" height="385" sizes="100vw" caption="Decision tree representing how we can respond to runtime errors. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4804ef49-a1b1-463f-a579-f290871ca53d/6-resilience-is-a-feature.png'>Large preview</a>)" alt="Decision tree with 3 leaf nodes that read (from left to right): Recover from error? No: Fallback from error?, Yes: Resume as usual. The decision node: Fallback from error? has 2 paths: No: Acknowledge error, Yes: Show fallback." >}}

When facing an error, the first question should be, “can we recover?” For example, does retrying a network request that failed for the first time succeed on subsequent attempts? Intermittent micro-services, unstable internet connections, or eventual consistency are all reasons to try again. Data fetching libraries such as [SWR](https://swr.vercel.app/) offer this functionality for free.

Risk appetite and surrounding context influence what HTTP methods you are comfortable retrying. At Nutmeg we retry failed reads (GET requests), but not writes (POST/ PUT/ PATCH/ DELETE). Multiple attempts to retrieve data (portfolio performance) is safer than mutating it (resubmitting a form).

The second question should be: If we cannot recover, can we provide a fallback? For example, if an online card payment fails can we offer an alternative means of payment such as via PayPal or Open Banking.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f115d83a-b305-421d-91b6-f8799c1c5a08/1-resilience-is-a-feature.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f115d83a-b305-421d-91b6-f8799c1c5a08/1-resilience-is-a-feature.png" width="800" height="533" sizes="100vw" caption="When something goes wrong offering an alternative helps users help themselves, and avoids dead ends. This is especially important for time sensitive transactions such as buying stock, or contributing to an ISA before the tax year ends. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f115d83a-b305-421d-91b6-f8799c1c5a08/1-resilience-is-a-feature.png'>Large preview</a>)" alt="Wireframe of a red error notification above a form. The error message reads: Card payment failed. Please try again, or use a different payment method. The text: different payment method is underlined denoting it's a link." >}}

Fallbacks don’t always need to be so elaborate, they can be subtle. Copy containing text dependant on remote data can fallback to less specific text when the request fails:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8a9290b3-a920-4fe4-ba95-32740fb3d100/4-resilience-is-a-feature.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8a9290b3-a920-4fe4-ba95-32740fb3d100/4-resilience-is-a-feature.png" width="800" height="399" sizes="100vw" caption="UIs can adapt to what data is available and still provide value. The vaguer sentence (left) still reminds users that ISA allowances lapse each year. The more enriched sentence (right) is an enhancement for when the network request succeeds. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8a9290b3-a920-4fe4-ba95-32740fb3d100/4-resilience-is-a-feature.png'>Large preview</a>)" alt="Two black and white wireframes. The left one titled: Remote data unavailable, displays a paragraph that reads: Make the most of your remaining ISA allowance for the current tax year. The right wireframe titled: Remote data available, shows a paragraph that reads: Make the most of your £16500 ISA allowance for April 2021-2022" >}}

The third and final question should be: If we cannot recover, or fallback how important is this failure (which relates to "Error Equality"). The UI should acknowledge primary errors by informing users something went wrong, whilst providing actionable prompts such as contacting customer support or linking to relevant support articles.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/66669728-b30a-42f3-ac19-16241d06959b/7-resilience-is-a-feature.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/66669728-b30a-42f3-ac19-16241d06959b/7-resilience-is-a-feature.png" width="800" height="430" sizes="100vw" caption="Avoid unhelpful error messages. The helpful error message (right) prompts the user to contact CS, including how (phone/ email) and what hours they operate to manage expectations. It’s not uncommon to provide errors with a unique identifier that users can reference when making contact. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/66669728-b30a-42f3-ac19-16241d06959b/7-resilience-is-a-feature.png'>Large preview</a>)" alt="Two wireframes, each containing a red error notification. The left one titled: Unhelpful error message, displays the text: Something went wrong. The right one titled: Helpful error message shows a paragraph that reads: Sorry, unable to load your bank balance. Please try again, or. Below the paragraph is a list of the following items, phone us on 01234567890 8am to 8pm Mon to Fri, email us on support at email dot com and search ‘bank balance’ in our knowledge base" >}}

## Observability

UIs adapting to something going wrong is not the end. There is another side to the same coin.

Engineers need visibility on the root cause behind a degraded experience. Even errors not surfaced to end-users (secondary errors) must propagate to engineers. Real-time error monitoring services such as [Sentry](https://sentry.io/) or [Rollbar](https://rollbar.com/) are invaluable tools for modern-day web development.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/49acff6d-a19d-4d40-a317-6c55fffb59b5/11-resilience-is-a-feature.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/49acff6d-a19d-4d40-a317-6c55fffb59b5/11-resilience-is-a-feature.png" width="800" height="458" sizes="100vw" caption="A screenshot of an error captured in Sentry. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/49acff6d-a19d-4d40-a317-6c55fffb59b5/11-resilience-is-a-feature.png'>Large preview</a>)" alt=" A screenshot taken from Sentry’s online sandbox of a TypeError. An error message reads: Cannot read property func of undefined. Below the error is a stack trace of where the exception was thrown" >}}

Most error monitoring providers capture all unhandled exceptions automatically. Setup requires minimal engineering effort that quickly pays dividends for an improved healthy production environment and MTTA (mean time to acknowledge).

{{% ad-panel-leaderboard %}}

The real power comes when explicitly logging errors ourselves. Whilst this involves more upfront effort it allows us to enrich logged errors with more meaning and context &mdash; both of which aid troubleshooting. Where possible aim for error messages that are understandable to non-technical members of the team.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/637a48c0-d69b-40de-8e96-1a715233ce01/13-resilience-is-a-feature.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/637a48c0-d69b-40de-8e96-1a715233ce01/13-resilience-is-a-feature.png" width="800" height="170" sizes="100vw" caption="Naming conventions help standardise explicit error messages, which make them easier to find/ read. The diagram above uses the format: [Domain] Context &mdash; Problem. You needn’t be an engineer to understand a bank transfer failed, and that the payments teams should investigate (if they aren’t already doing so). (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/637a48c0-d69b-40de-8e96-1a715233ce01/13-resilience-is-a-feature.png'>Large preview</a>)" alt="Grey text on white background showing a function logging an error. The 1st function argument reads: Payment Bank transfer – Unable to connect with ${bank}. The 2nd argument is the error. Below the function are 3 labels: Domain, Context, and Problem." >}}

Extending the earlier Stripe example with an else branch is the perfect contender for explicit error logging:

<pre><code class="language-javascript">if (
  typeof stripe === "object" &&
  typeof stripe.handleCardPayment === "function"
) {
  stripe.handleCardPayment(/* ... */);
} else {
  logger.capture(
    "[Payment] Card charge — Unable to fulfill card payment because stripe.handleCardPayment was unavailable"
  );
}
</code></pre>

**Note**: *This defensive style needn’t be bound to form submission (at the time of error), it can happen when a component first mounts (before the error) giving us and the UI more time to adapt.*

Observability helps pinpoint weaknesses in code and areas that can be hardened. Once a weakness surfaces look at if/ how it can be hardened to prevent the same thing from happening again. Look at trends and risk areas such as third-party integrations to identify what could be wrapped in an operational feature flag (otherwise known as kill switches).

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6e961101-47fc-4939-be4e-fb59d2990c13/10-resilience-is-a-feature.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6e961101-47fc-4939-be4e-fb59d2990c13/10-resilience-is-a-feature.png" width="800" height="401" sizes="100vw" caption="Not all fallbacks need to be digital. This is especially true for processes that already involve manual steps, such as transferring an ISA from one bank to another. When everything is operational (left) users submit an online form that populates a PDF they print and sign. When the third-party suffers an outage or is down for maintenance (right) a kill switch allows users to download a blank PDF form they can fill in (by hand), print and sign. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6e961101-47fc-4939-be4e-fb59d2990c13/10-resilience-is-a-feature.png'>Large preview</a>)" alt="Two black and white wireframes. The left one titled: Kill switch off, displays 3 form fields above a blue button. The right one titled: Kill switch on, shows the text: Download PDF next to a download icon." >}}

Users forewarned about something not working will be less frustrated than those without warning. Knowing about road works ahead of time helps manage expectations, allowing drivers to plan alternative routes. When dealing with an outage (hopefully discovered by monitoring and not reported by users) be transparent.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5d900508-6f8f-4fc7-878c-c4e3f2242936/9-resilience-is-a-feature.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5d900508-6f8f-4fc7-878c-c4e3f2242936/9-resilience-is-a-feature.png" width="800" height="340" sizes="100vw" caption="Avoid offloading observability to end users. Finding and acknowledging issues before customers do leads to a better user experience. The information banner above is clear, concise, and reassures users that the issue is known about, and a fix is incoming. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5d900508-6f8f-4fc7-878c-c4e3f2242936/9-resilience-is-a-feature.png'>Large preview</a>)" alt="Wireframe of a blue banner atop of a page. The banner reads: We’re currently experiencing problems with online payments and are working on resolving the issue" >}}

## Retrospectives

It’s very tempting to gloss over errors.

However, they provide valuable learning opportunities for us and our current or future colleagues. Removing the stigma from the inevitability that things go wrong is crucial. In [Black box thinking](https://www.goodreads.com/book/show/24611735-black-box-thinking) this is described as:

<blockquote>“In highly complex organizations, success can happen only when we confront our mistakes, learn from our own version of a black box, and create a climate where it’s safe to fail.”</blockquote>

Being analytical helps prevent or mitigate the same error from happening again. Much like black boxes in the aviation industry record incidents, we should document errors. At the very least documentation from prior incidents helps reduce the MTTR (mean time to repair) should the same error occur again.

Documentation often in the form of RCA (root cause analysis) reports should be honest, discoverable, and include: what the issue was, its impact, the technical details, how it was fixed, and actions that should follow the incident.

## Closing Thoughts

Accepting the fragility of the web is a necessary step towards building resilient systems. A more reliable user experience is synonymous with happy customers. Being equipped for the worst (proactive) is better than putting out fires (reactive) from a business, customer, and developer standpoint (less bugs!).

Things to remember:

* UIs should adapt to the functionality they can offer, whilst still providing value to users;
* Always think what can wrong (never make assumptions);
* Categorize errors based on their impact (not all errors are equal);
* Preventing errors is better than responding to them (code defensively);
* When facing an error, ask whether a recovery or fallback is available;
* User facing error messages should provide actionable prompts;
* Engineers must have visibility on errors (use error monitoring services);
* Error messages for engineers/ colleagues should be meaningful and provide context;
* Learn from errors to help our future selves and others.

{{< signature "vf, il" >}}
