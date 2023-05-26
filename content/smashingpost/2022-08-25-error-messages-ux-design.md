---
title: 'Designing Better Error Messages UX'
slug: error-messages-ux-design
author: vitaly-friedman
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/93af7c7e-6484-4f47-9e79-fcf6aa24b3ce/better-error-messages-ux.jpg
date: 2022-08-25T15:00:00.000Z
summary: >-
  Error messages need to be easy to spot, but they also need to be helpful. Let’s explore when error messages should live above input fields and why toast error messages are usually not a very good idea.
description: >-
  Error messages need to be easy to spot, but they also need to be helpful. Let’s explore when error messages should live above input fields and why toast error messages are usually not a very good idea.
categories:
  - UX
  - Usability
  - Design Patterns
---

When we design interfaces, we rarely think about **error messages** first. After all, how much is there to design anyway? We highlight the error, display a message, and nudge users toward the correct input. As it turns out, a strategic and thorough design of these messages can be critical for businesses, especially if they struggle with high abandonment. Error messages can make or break the experience in situations when things go south.

**Errors are everywhere**, and so are error messages. They are of course common in web forms, but also in complex tables, incompatible filters, search queries and failed interactions. They can be small error notes and large error summaries; short tooltips and lengthy toast messages. So, where do we start? From the beginning.

<style>.course-intro{--shadow-color:206deg 31% 60%;background-color:#eaf6ff;border:1px solid #ecf4ff;box-shadow:0 .5px .6px hsl(var(--shadow-color) / .36),0 1.7px 1.9px -.8px hsl(var(--shadow-color) / .36),0 4.2px 4.7px -1.7px hsl(var(--shadow-color) / .36),.1px 10.3px 11.6px -2.5px hsl(var(--shadow-color) / .36);border-radius:11px;padding:1.35rem 1.65rem}@media (prefers-color-scheme:dark){.course-intro{--shadow-color:199deg 63% 6%;border-color:var(--block-separator-color,#244654);background-color:var(--accent-box-color,#19313c)}}</style>
  
<p class="course-intro"><em>Pssst!</em> This article is <strong>part of our ongoing series</strong> on <a href="/category/design-patterns">design patterns</a>. It’s also a part of <a style="font-weight:700" href="https://smart-interface-design-patterns.com/">Smart Interface Design Patterns</a>&nbsp;🍣 and is available in the <a href="https://smashingconf.com/online-workshops/workshops/interface-design-course-vitaly-friedman/">Live Interface Design Training</a>&nbsp;🍕 as well.</p>

## Not All Error Messages Are Equal

Not all errors are the same. As Page Laubheimer [has noted](https://www.nngroup.com/articles/slips/), there are actually **two different types of errors**. *Slips* occur when users intend to perform one action but do another (e.g., when filling in a form on autopilot). *Mistakes* occur when there is a mismatch between the mental model of a user and the system. Our interfaces need to support both types of errors, and slips are usually much easier to resolve than mistakes.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0d39da57-e7a1-435e-80ff-f844f6908dc7/1-error-messages-ux.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0d39da57-e7a1-435e-80ff-f844f6908dc7/1-error-messages-ux.png" width="800" height="394" sizes="100vw" caption="Error messages come in various flavours: they could be slips (unconscious) or actual mistakes (conscious). (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0d39da57-e7a1-435e-80ff-f844f6908dc7/1-error-messages-ux.png'>Large preview</a>)" alt="A screenshot with two types of errors: slips and mistakes" >}}

For **slips**, we can include helpful constraints (e.g. a reasonable width of a text box, [prefixes and suffixes](https://design-system.service.gov.uk/components/text-input/#prefixes-and-suffixes)), provide recovery suggestions (e.g. autocomplete), choose reasonable defaults, and use forgiving formatting.

To prevent **mistakes**, we need to confirm destructive actions (when users go back to the previous page), set expectations early on (password requirements or file size), allow users to change their minds (change email or payment method), and in general, always provide a way out.

To measure the success of our error messages, we can define error-focused [design KPIs](https://www.smashingmagazine.com/2022/04/boosting-ux-with-design-kpis/) and track them over time. These could include:

- the **average number of mistakes** in a user journey,
- the error recovery time,
- the completion rates, and
– completion times.

We can’t really eliminate mistakes altogether since no human input can be bulletproof, but we can reduce the number of errors by **making it more difficult to make mistakes**. One simple way of doing so is to improve the discovery errors, by never relying on the color of error messages alone.

## Never Rely On Red Color Alone

When we think of error messages, we almost subconsciously think of **bold red text errors**. That’s indeed a very established pattern, but often not enough to indicate to *all* users that something is wrong.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/717bc0b9-96d8-4c5d-9509-5d2d31f31659/2-error-messages-ux.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/717bc0b9-96d8-4c5d-9509-5d2d31f31659/2-error-messages-ux.jpg" width="800" height="328" sizes="100vw" caption="Just a regular plain error message: red and bold. As in use on Gov.uk. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/717bc0b9-96d8-4c5d-9509-5d2d31f31659/2-error-messages-ux.jpg'>Large preview</a>)" alt="A screenshot of a regular plain error message: red and bold" >}}

Due to color vision deficiencies, it’s a good idea to **always complement error messages with an icon**, e.g., a large exclamation mark on a red background &mdash; right next to the error message. We can also highlight the entire section, along with the field, label, the hint, the error message and the input field. For example, a **thick red vertical line** next to the error message is a [common pattern for error messages](https://design-system.service.gov.uk/components/error-message/) on Gov.uk.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/778c91d9-6e43-44f0-9df6-0c975b62c2e5/4-error-messages-ux.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/778c91d9-6e43-44f0-9df6-0c975b62c2e5/4-error-messages-ux.jpg" width="800" height="395" sizes="100vw" caption="Always a good idea: adding an icon and a thick vertical line for the entire section. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/778c91d9-6e43-44f0-9df6-0c975b62c2e5/4-error-messages-ux.jpg'>Large preview</a>)" alt="A screenshot of an error message with an icon of exclamation mark next to it" >}}

Sometimes the icon is displayed *inside* of the input field, on the right or on the left edge of the text box. When we display the icon on the right, users who zoom in and out might have difficulties spotting them. That’s why placing the icon **on the left edge** seems to be just a bit more reliable.

{{< rimg href="https://carbondesignsystem.com/components/notification/usage/#inline-notifications" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9c14c8de-d87a-438e-9051-4fe070706520/3-error-messages-ux.png" width="800" height="522" sizes="100vw" caption="Example of an icon displayed on the right edge of the text box. <a href='https://carbondesignsystem.com/components/notification/usage/#inline-notifications'>From Carbon Design System</a>. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9c14c8de-d87a-438e-9051-4fe070706520/3-error-messages-ux.png'>Large preview</a>)" alt="Example of an icon displayed on the right edge of the text box." >}}
 
Additionally, it might be a good idea to guide users towards specific issues of the form with an [error summary](https://design-system.service.gov.uk/components/error-summary/). That summary can contain links to the areas in the form which contain errors, so users can jump there directly.

The summary can appear on the top of the page, or **just above the action button**, as displayed in the example above.

Most importantly, error summary probably shouldn’t appear *under* the action button. Too often, especially on mobile, users don’t realize that there is any error message at all, and keep clicking on that poor submit button hoping to get any kind of feedback — be it a status update from the browser, or a change of the URL. The feedback is actually there, under the button, yet in testing, it often shows **very poor discovery rates**.  

If the page is fully *refreshed* upon validation, the error summary should be at the very top of the page. But if the page is updated without a refresh, it’s reasonable to add the error summary just above the action button where the user has just clicked or tapped — and highlight it with the red color and icon as well.

## Avoid Auto-Scrolling and Auto-Jumps

Once a user clicks on the submit button, should we **automatically scroll** them to the first error? There is no clear answer to that question. Personally, I saw this pattern working very well for some users, but failing miserably for others.

Any **sudden movements** on the page are likely to cause frustration with at least *some* users. If anything, users tend to find auto-jumps more annoying than auto-scrolling — as the latter at least communicates the direction of change and hints better at where users have moved to.

Short answer? **Start without auto-scrolling** and display just an error summary with links. If it’s too slow, or doesn’t work as expected, consider adding auto-scrolling. And by no means move users up and down the page for no obvious reason — that’s a safe way to increase completion times and introduce confusion when it’s probably not needed.
## Never Cover User’s Input

When we display error messages, we convey to users that **there is a problem**; a good error message, however, also guides users to a solution. This, however, requires the ability to **consult the error as the error is being fixed**. In other words, users should be able to edit the input field while also reviewing the error message(s) provided to them.

{{< rimg href="https://uxdworld.com/2020/04/22/inline-editing-and-validation-in-tables/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ed8986e2-1924-454b-b3dc-d1ffa31fbf53/5-error-messages-ux.png" width="800" height="271" sizes="100vw" caption="<a href='https://uxdworld.com/2020/04/22/inline-editing-and-validation-in-tables/'>Inline editing and validation in tables</a>. A typical example. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ed8986e2-1924-454b-b3dc-d1ffa31fbf53/5-error-messages-ux.png'>Large preview</a>)" alt="Inline editing and validation in tables" >}}

So far, so good. However, things become quite complicated once we also have a tooltip in play. Once a tooltip is open, users might lose sight of both the error message and the input. Should they desire to be able to see **all three pieces of information at once**, they’d be out of luck.

{{< rimg href="https://carbondesignsystem.com/static/f04044737e36df31baee6b2ae1cd9bad/3cbba/toggle-tip-usage-1.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/859e2fd1-e20b-46a3-b77e-92dbb83bfd0f/7-error-messages-ux.png" width="800" height="600" sizes="100vw" caption="When a tooltip blocks the content, an example from the <a href='https://carbondesignsystem.com/components/toggletip/usage/'>Carbon Design System</a>." alt="Overview of toggletip" >}}

However, we can fix it relatively easily. First of all, we avoid tooltips that open on hover and display the tooltip **only once tapped or clicked**. That means that a tooltip will never disappear automatically and must be closed manually.

Then, we use the [details component](https://design-system.service.gov.uk/components/details/) and **inline accordions** as an alternative to tooltips. Hence, we make space for the content of the tooltip to expand between the label and the other content, so nothing will be covered. The error message would be visible at all times as well, next to the input field.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7727504e-8799-49af-a04b-35c092522b4d/10-error-messages-ux.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7727504e-8799-49af-a04b-35c092522b4d/10-error-messages-ux.png" width="800" height="534" sizes="100vw" caption="The <a href='https://design-system.service.gov.uk/components/details/'>details component</a>, with the details appearing on tap/click. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7727504e-8799-49af-a04b-35c092522b4d/10-error-messages-ux.png'>Large preview</a>)" alt="A screenshot from Gov.uk with a tooltip opened and the error message above it" >}}

This way, we show all three pieces of information at the same time &mdash; and <strong>users always have a choice</strong> to select what exactly they’d like to see. Is it too much? Maybe. But that’s a great option to keep in mind: at least to always display the input field and the error at the same time without them being covered by the tooltip.


{{% feature-panel %}}


## In Forms, Display Error Messages Above Input

Now, this might sound a little bit confusing at first. Usually, error messages will be sitting conveniently *under* the input field, or perhaps &mdash; less frequently &mdash; on the right side of the input field. As it turns out, there are a few **accessibility issues** that come as a cost of these conventions. 

- **Users of a magnifying software** might miss the error message when it’s located on the right.
- **On mobile**, users might not be able to see the error message under the input because it will be [covered by the virtual keyboard](https://adrianroselli.com/2017/01/avoid-messages-under-fields.html).
- **When editing input**, error messages might be covered by the browser’s autofill or dropdown’s autocomplete suggestions.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e0ba87f7-87bf-43e8-abcc-80f7af45b294/12-error-messages-ux.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e0ba87f7-87bf-43e8-abcc-80f7af45b294/12-error-messages-ux.png" width="800" height="468" sizes="100vw" caption="We can avoid accessibility issues by displaying errors above erroneous input fields. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e0ba87f7-87bf-43e8-abcc-80f7af45b294/12-error-messages-ux.png'>Large preview</a>)" alt="A screenshot from gov.uk with the displaying error message above input fields" >}}

Displaying error messages **above input fields** typically helps us avoid the accessibility issues listed above. The cost of it, though, is **layout shifts**: with every new error appearing dynamically, the entire form has to shift *vertically* as we need to make space for the error message to appear. It might be noisy, but sometimes that noise might be very much worth it.

For lengthy error messages, it might sound tempting to display them as a tooltip, yet with it come all the usability issues discussed in the previous section. Using a **collapsible accordion** instead might be a better idea there.

{{% ad-panel-leaderboard %}} 

## In Tables, Display Error Messages Inline

When displaying error messages in tables, it might be a good idea to consider alternative approaches as otherwise we would end up with a lot of **layout shifts** for each row.

One of the simpler patterns is to **display the error message in the same row** where the content lives. In that case, the error message is more likely to live *under* the input field, not above it. Lengthy error messages could be collapsed and expanded with a tap/click on the entire row.

{{< rimg href="https://uxdworld.com/2020/04/22/inline-editing-and-validation-in-tables/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a67ce375-ca97-4588-976e-558625acebd6/15-error-messages-ux.webp" width="800" height="516" sizes="100vw" caption="Error messages could live in the same row where the erroneous content lives. Source: <a href='https://uxdworld.com/2020/04/22/inline-editing-and-validation-in-tables/'>UX Design World</a>. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a67ce375-ca97-4588-976e-558625acebd6/15-error-messages-ux.webp'>Large preview</a>)" alt="Visualization of inline editing and validation in tables" >}}

If the same error **affects multiple rows**, we might want to **highlight the rows** that contain errors and display an error message at the very top of the page that would explain the error and what needs to be done to fix it.

{{< rimg href="https://uxdworld.com/2020/04/22/inline-editing-and-validation-in-tables/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5f55e9ff-6f36-4d92-af20-3641c42afa4e/16-error-messages-ux.png" width="800" height="383" sizes="100vw" caption="If an error appears multiple times, and its simple to explain, it might be a good idea to show it on the very top of the page. Image source:  <a href='https://uxdworld.com/2020/04/22/inline-editing-and-validation-in-tables/'>UX Design World</a>. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5f55e9ff-6f36-4d92-af20-3641c42afa4e/16-error-messages-ux.png'>Large preview</a>)" alt="Visualization with highlighted rows which contain errors and an error message at the top of the page" >}}


<!-- 
## Inline Validation Is Problematic

But how would error messages above the input work with inline validation? Wouldn’t we distract users all the time if error messages keep popping up just above the input area where they are typing their data, hence pushing the rest of the form vertically? Yes, they absolutely would! However, [live validation is problematic](https://adamsilver.io/blog/live-validation-is-problematic/), too. It has become a common design pattern that’s often expected in web forms, but it also comes at a cost, and sometimes it can be quite severe.

With **inline validation**, we validate users’ input as they type or after they’ve left the input field. In both cases, the experience can be somewhat frustrating:

- Live validation interrupts users while they’re trying to answer the question.
- Live validation often kicks in either **too early**, when the user hasn’t finished the input, or **too late** when the user has moved to the next input field. Both of these options aren’t ideal.
- When we display an error after a user has left the input field, we distract them; the user is focused on the next question, yet we prompt them to fix their previous answer.
- Even though the inline validator might give input the green light, it might turn into an error message once the validation has happened on the server. The proper formatting of data doesn’t represent the accuracy of data.
- Usually, we’ll use **different validation rules** for different fields as some fields need to be validated later than the others, e.g., it doesn’t make sense to validate the email address unless the `@` symbol has been typed in.

Indeed there are major **advantages of inline validation** as well:

- If a customer is using the browser’s autofill, they can be certain that they haven’t missed anything since inline validation checks if the input is correct.
- Inline validation is useful with a password strength meter as it helps users choose a password that matches all requirements and is safe. 
- Because the user corrects a mistake close to when it happens, we shouldn’t expect them to fill out entire sections in the form just to realize that it does not apply to them.

We can make inline validation work with the [Reward Early, Punish Late pattern](https://medium.com/wdstack/inline-validation-in-forms-designing-the-experience-123fb34088ce), but the [implementation isn’t trivial](https://medium.com/@shanplourde/inline-form-validations-ux-design-considerations-and-react-examples-c2f53f89bebc). We need to **track the state of each input field**, and track how many characters the user has typed in already, and have thresholds for when we start validating and then have rules for changing input fields that have been validated already, or that contain errors.

A simple alternative to it &mdash; which isn’t ideal either but might perform better than inline validation &mdash; is to:

- split a complex form into small steps ([one-thing-per-page](https://www.smashingmagazine.com/2017/05/better-form-design-one-thing-per-page/)),
- accept any unambiguous input,
- **validate each step only on submit**.

Thus, we **avoid unnecessary distractions**, complex logic, and layout shifts altogether, and communicate errors without annoying users too early or too late. The downside is, of course, the error recovery speed, which will be slower, yet in the end, the number of errors might be lower as well because we’ve simplified the form massively. It’s just much more difficult to make mistakes if you have just 3–4 input fields in front of you.  -->

## Don’t Rely On Toast Error Messages

But what about good ol’ **toast error messages**? Those animated notifications, informing users about change of status of the system with **floating messages**. They might be uncommon for forms, but they frequently appear in tables and enterprise dashboards.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/83fc45a3-489d-47c3-b812-bda51fe3e353/13-error-messages-ux.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/83fc45a3-489d-47c3-b812-bda51fe3e353/13-error-messages-ux.png" width="800" height="556" sizes="100vw" caption="The world of toast notifications. <a href='https://designlibrary.sebgroup.com/components/component-toast-notifications'>Seb Group Design System</a>. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/83fc45a3-489d-47c3-b812-bda51fe3e353/13-error-messages-ux.png'>Large preview</a>)" alt="Examples of toast error messages" >}}

There are a few common **usability issues** with toast error messages:

- Users often **don’t get a chance to fully read or understand the error message** before it has disappeared, and there is no way to restore it or keep it floating. 
- Toast messages typically **appear on the edges of the screen**, and usually, it’s quite [far away from the problematic input](https://www.nngroup.com/articles/errors-forms-design-guidelines/) that has caused the error. There is quite a disconnect between the error message and the input, and it’s rarely possible to read the error message and correct the mistake simultaneously.
- Lengthy toast messages **usually block large areas of content** that a user might be relying on — and potentially even the input that has caused the error.
- Toast messages **need to be announced to screen reader users** while also allowing users to bring their focus back and forth between the error message and the erroneous input.
- With toasts, we usually don’t have enough space to provide a detailed help using **images or videos**, and have to rely on plain text and links leading to external help pages that would usually open in a new tab.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/34c14248-2049-4612-be1f-fb09893bd54d/14-error-messages-ux.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/34c14248-2049-4612-be1f-fb09893bd54d/14-error-messages-ux.png" width="800" height="417" sizes="100vw" caption="This might not be ideal: error messages <a href='https://github.com/elastic/kibana/issues/67270'>appearing as toasts in complex UIs</a>. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/34c14248-2049-4612-be1f-fb09893bd54d/14-error-messages-ux.png'>Large preview</a>)" alt="Examples of error messages appearing as toasts in complex UIs" >}}

If anything, toasts should be [persistent if displaying information that can be acted upon](https://www.benrajalu.net/articles/ux-of-notification-toasts), and users should be able to **manually dismiss** the notification.

Personally, I’d definitely **stay away from designing error messages as toasts**, even if they are persistent. The better we can connect an error with its cause visually, the less likely it is to be overlooked. And the better we can explain how to solve that error close to the erroneous input box, the faster users will understand what they need to do.

<!-- The visual design and the position of error messages matter for discoverability, but when it comes to resolving the issue at hand, we need to invest in the missing piece of the puzzle: error messaging.  -->

## Allow Users To Override An Error Message

We’ve all been there before: full of hope and passion, you type in your shipping address in an eCommerce checkout, willing to proceed with payment right away. Yet here it comes, an **aggressive address validator**, telling you that your address is wrong, and you better double check it. You have been living at that address for the last five years, yet for some reason, that’s not good enough for the address validator.

What options do you have? Unless you are willing to deliver the item to another address, this problem will likely cause a **100% abandonment** &mdash; an extremely high price to pay for a poor address validator. Surely you don’t want to deliver an item to non-existing addresses, yet you don’t want to abandon customers either. Indeed, it might be that only a small portion of customers will be affected by it, but why should we lose these customers either?

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/43df9fc1-8739-4397-9c4e-0d8bd8f2fe63/20-error-messages-ux.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/43df9fc1-8739-4397-9c4e-0d8bd8f2fe63/20-error-messages-ux.png" width="800" height="203" sizes="100vw" caption="What happens if the validator doesn’t know the address? We can allow users to override validator in some cases. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/43df9fc1-8739-4397-9c4e-0d8bd8f2fe63/20-error-messages-ux.png'>Large preview</a>)" alt="An example of an address validator which allows to override an error message " >}}

No single validation library is **100% reliable and bulletproof** for all the edge cases. Eventually some percentage of your customers will be left out there in the woods, trying to figure out what to do next to proceed.  **Aggressive validators cost money.** Especially when they come in tandem with [disabled buttons](https://www.smashingmagazine.com/2021/08/frustrating-design-patterns-disabled-buttons/) that literally block users without telling them what exactly needs to be done to fix the issue. 

For cases when a validator might be too restrictive, we can allow customers to **override validator’s warning**. Surely we will get some wrong addresses as a result of that. But as a business, we need to measure just **how much money we are losing** due to increase in service desk inquiries vs. how much money we gain by allowing people to find a way to proceed even although the interface doesn’t want to play along. More often than not, it’s worth it.

While this pattern works flawlessly for address input and telephone input, it probably won’t work for any input that needs to follow a particular convention — such as the length and checksum of an IBAN number or a credit card number. There, instead of giving customers a carte blanche, we need to **meticulously check user’s input** and guide them towards what exactly the problem seems to be.

## Establish Stop-Words For Your Error Messages

Many error messages in most web applications are remarkably generic. They do indicate errors, but they aren’t very helpful in **indicating solutions** on how to fix these errors. Most of the time, these messages don’t really refer to the specifics of the user’s input. They provide a **very general statement** explaining that the input is wrong, with plenty of floral and cryptic words along with it.

In my personal experience, starting a project off by exploring and defining error messaging can be a very valuable exercise. If we can convey friendliness and personality while being concise and helpful in our error messages, we should surely be able to achieve the same in our navigation, body copy and form labels. In many ways, the way we write error messages can help us figure out just the right **voice and tone of the entire design**.


{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4bf8eceb-a0b9-49a8-b9eb-ea411cb0c291/19-error-messages-ux.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4bf8eceb-a0b9-49a8-b9eb-ea411cb0c291/19-error-messages-ux.png" width="800" height="558" sizes="100vw" caption="No technical jargon, no cryptic wording, nothing left to interpretation: we just explain the problem. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4bf8eceb-a0b9-49a8-b9eb-ea411cb0c291/19-error-messages-ux.png'>Large preview</a>)" alt="Examples of error messages which are helpful and refer to the specifics of the user input" >}}


Depending on your product’s voice and tone, you might want to be very strategic about how your error messages should sound. Here are some of the [stop-words](https://design-system.service.gov.uk/components/error-message/) that Gov.uk tends to avoid in their interface:

- **technical jargon** like ‘form post error’, ‘unspecified error’, and ‘error 0x0000000643’;
- words like ‘forbidden’, ‘illegal’, ‘you forgot’, and ‘prohibited’;
- **‘please’** because it implies a choice;
- **‘sorry’** because it does not help fix the problem;
- **‘valid’** and **‘invalid’** because they do not add anything to the message;
- **humourous**, informal language like ‘oops’.

The choice of words matters. It’s worth emphasizing that spending time and effort on crafting helpful, [adaptive error messages](https://baymard.com/blog/adaptive-validation-error-messages) is probably **one of the best investments** a company might make to reduce abandonment and drive conversions.
## Provide Examples Of Correct Input

Talking about the choice of words, how do we make it more helpful? And in general, what makes an error message helpful? For example, a clear set of guidelines of what a correct input is. That means adding a hint under the label and **provide an example of correct input**, so users understand how to re-route and what is expected from them.


{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/67a5294f-ca2c-4257-b544-4cdf2042bdc2/17-error-messages-ux.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/67a5294f-ca2c-4257-b544-4cdf2042bdc2/17-error-messages-ux.png" width="800" height="536" sizes="100vw" caption="There is no need to include words that don’t help the user fix the problem. Instead, we can provide helpful, actionable hints and input examples. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/67a5294f-ca2c-4257-b544-4cdf2042bdc2/17-error-messages-ux.png'>Large preview</a>)" alt="Examples of error messages which are helpful and refer to the specifics of the user input" >}}


{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9c25d495-6043-4566-a664-946ab62e7654/18-error-messages-ux.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9c25d495-6043-4566-a664-946ab62e7654/18-error-messages-ux.png" width="800" height="278" sizes="100vw" caption="Providing example along with a helpful error message can go a long way to significantly reduce abandonment. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9c25d495-6043-4566-a664-946ab62e7654/18-error-messages-ux.png'>Large preview</a>)" alt="Examples of error messages which are helpful and refer to the specifics of the user input" >}}


Surely, sometimes adding an example **might feel unnecessary** and just taking up the space in design. I’d challenge you to tackle your conversion issues with well-crafted examples of corrent input. Often it’s the easiest way to improve conversion, as users otherwise just can’t find a way to make something work — even if it’s as simple as an extra empty space.

{{% ad-panel-leaderboard %}} 
## Display Error Summary On The Top

[Inline validation deserves a separate conversation](https://adamsilver.io/blog/live-validation-is-problematic/). As an alternative approach, of course we could **validate the form on submit only**. But it doesn’t mean that we have to drive users from one page to a separate new page with all the errors displayed. We could display an error summary just next to the <kbd>Submit</kbd> button (as displayed below, sketched by [Jordan Moore](https://twitter.com/jordanmoore/status/1250026238762266624)). It would probably be better to display the error message *above* the <kbd>Submit</kbd> button rather than below it to prevent it from being rendered below the bottom of the viewport and thus not to be visible (*thanks* [*Rik*](https://twitter.com/rikschennink/status/1250030873426251776)*!*).

{{< rimg href="https://twitter.com/jordanmoore/status/1250026238762266624" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/34f98ac4-a6de-4d04-bed0-16e27b2413e7/21-error-messages-ux.png" width="800" height="450" sizes="100vw" caption="An error message appearing next to <code>Submit</code> button. Sketched by <a href='https://twitter.com/jordanmoore/status/1250026238762266624'>Jordan Moore</a>. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/34f98ac4-a6de-4d04-bed0-16e27b2413e7/21-error-messages-ux.png'>Large preview</a>)" alt="A sketch of an error message appearing next to Submit button" >}}

However, if there are a few problems with the form, we can also use an [error summary component](https://design-system.service.gov.uk/components/error-summary/). With it, we highlight the errors as links so that users can jump to them via the keyboard as well. While doing so, we need to [bring focus to the first form field with an error](https://www.aaron-gustafson.com/notebook/bring-focus-to-the-first-form-field-with-an-error/). Preferably with a bit of [scroll-margin-top](https://developer.mozilla.org/en-US/docs/Web/CSS/scroll-margin-top), so screen reader users understand where they currently are.
 
{{< rimg href="https://nostyle.herokuapp.com/patterns/fix-form-errors" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ee71783f-a543-4f0f-9ddb-b150fc1134c5/22-error-messages-ux.png" width="800" height="509" sizes="100vw" caption="Error summary on the top, single error messages within each input field. From <a href='https://nostyle.herokuapp.com/patterns/fix-form-errors'>No Style Design System</a> by Adam Silver. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ee71783f-a543-4f0f-9ddb-b150fc1134c5/22-error-messages-ux.png'>Large preview</a>)" alt="An example of an error summary component" >}}

Additionally, you might want to adjust the **favicon and the title of the document** if errors do appear, so impatient users who might have already left the form perhaps have a chance to return back and fix the errors, rather than assuming that everything has worked flawlessly.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e05689d2-7098-4036-abeb-5f39ef0f4a3b/23-error-messages-ux.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e05689d2-7098-4036-abeb-5f39ef0f4a3b/23-error-messages-ux.png" width="800" height="149" sizes="50vw" caption="Indicate to users that there are some pending problems with the form by changing the favicon and the title of the tab upon validation. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e05689d2-7098-4036-abeb-5f39ef0f4a3b/23-error-messages-ux.png'>Large preview</a>)" alt="An example of the adjusted title of the document with a message '2 errors'" >}}

## Wrapping Up

At the first glance, dealing with error messages might not sound like a big deal. However, as we dive into fine details, there are **plenty of considerations** that might either cause high abandonment or help people resolve issues quickly.

Here’s a quick overview of what we can do to improve the Error Messages UX in our websites and applications:

- Define error-focused [design KPIs](https://www.smashingmagazine.com/2022/04/boosting-ux-with-design-kpis/) by measuring the average number of mistakes in a user journey, the **error recovery time**, the completion rates, and completion times.
- Never rely on the color of the error message alone, and **use icons, borders, and section highlights** to indicate erroneous input.
- **Never cover user’s input nor the error message.** Ideally, allow users to consult the error message, the tooltip, and their input at the same time, e.g., by using inline accordions and avoiding tooltips for important details.
- Consider displaying error messages **above input** to avoid issues with auto-fill, autocomplete, magnifying software, and virtual keyboard.
- Use inline validation for password strength meters, but not for validating every field as users type in. Consider breaking the form into small steps and validate each step only on submit.
- For complex tables, **don’t rely on toast error messages** and display errors within rows where an error has occurred.
- Be strategic about your **error messaging** and craft helpful messages that match the voice and tone of your brand, rather than being general and generic.
- Always provide examples of correct input, especially for complex input that are less likely to be auto-filled.
- Allow users to **override your validators** for address input and telephone input, but not for any input that needs to follow a particular convention.
- When validating on submit, display an error summary on the top of the page, or guide users to an error in a popover. Also, change the favicon and the title of the document to communicate to users who’ve already left that something went wrong.

With these guidelines, we should be better off when boosting our error messages UX. And if you can’t really do much around the way errors appear in your product, explore what you can do to **replace generic error messages** with helpful ones. This might be a small change with a huge impact that will eventually show up in large business KPIs dashboards.


## Meet “Smart Interface Design Patterns”

If you are interested in similar insights around UX, take a look at [**Smart Interface Design Patterns**](https://smart-interface-design-patterns.com/), our shiny new **9h-video course** with **100s of practical examples** from real-life projects. Plenty of design patterns, guidelines and a [live UX training](https://smashingconf.com/online-workshops/workshops/interface-design-course-vitaly-friedman/) &mdash; with 5 new segments added every year. *Just sayin’!* [Check a free preview](https://www.youtube.com/watch?v=aSP5oR9g-ss).

<figure style="margin-bottom: 1rem"><a href="https://smart-interface-design-patterns.com/"><img style="border-radius: 11px" decoding="async" fetchpriority="low" width="950" height="492" srcset="https://res.cloudinary.com/indysigner/image/fetch/f_auto,q_80/w_400/https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7cc4e1de-6921-474e-a3fb-db4789fc13dd/b4024b60-e627-177d-8bff-28441f810462.jpeg 400w,
https://res.cloudinary.com/indysigner/image/fetch/f_auto,q_80/w_800/https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7cc4e1de-6921-474e-a3fb-db4789fc13dd/b4024b60-e627-177d-8bff-28441f810462.jpeg 800w,
https://res.cloudinary.com/indysigner/image/fetch/f_auto,q_80/w_1200/https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7cc4e1de-6921-474e-a3fb-db4789fc13dd/b4024b60-e627-177d-8bff-28441f810462.jpeg 1200w,
https://res.cloudinary.com/indysigner/image/fetch/f_auto,q_80/w_1600/https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7cc4e1de-6921-474e-a3fb-db4789fc13dd/b4024b60-e627-177d-8bff-28441f810462.jpeg 1600w,
https://res.cloudinary.com/indysigner/image/fetch/f_auto,q_80/w_2000/https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7cc4e1de-6921-474e-a3fb-db4789fc13dd/b4024b60-e627-177d-8bff-28441f810462.jpeg 2000w" src="https://res.cloudinary.com/indysigner/image/fetch/f_auto,q_80/w_400/https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7cc4e1de-6921-474e-a3fb-db4789fc13dd/b4024b60-e627-177d-8bff-28441f810462.jpeg" sizes="100vw" alt="Smart Interface Design Patterns"></a><figcaption class="op-vertical-bottom">Meet <a href="https://smart-interface-design-patterns.com/">Smart Interface Design Patterns</a>, our new video course and <a href='https://smashingconf.com/online-workshops/workshops/interface-design-course-vitaly-friedman/'>live UX training</a> all around interface design &amp; UX.</figcaption></figure>

<div class="btn--lined btn--lined--white-border" style="margin-top: 0.75em; margin-bottom: 0.75em"><a class="btn btn--large btn--green btn--text-shadow" href="https://smart-interface-design-patterns.com/">Jump to the video course&nbsp;&rarr;</a></div>

<p class="ticket-price__desc" style="font-size: .8em!important; text-align: center; line-height: 1.5; margin-top: 0; display: block;">100 design patterns &amp; real-life 
examples.<br>9h-video course + live UX training. <a href="https://www.youtube.com/watch?v=aSP5oR9g-ss">Free preview</a>.</p>

## Useful Resources

- [Back Button Expectations](https://baymard.com/blog/back-button-expectations), Baymard Institute
- [Designing With the Web in Mind](https://uxdesign.cc/design-with-the-web-in-mind-d9f9df2e8812), Chloe Sanderson
- [Designing A Perfect Configurator](https://www.smashingmagazine.com/2018/02/designing-a-perfect-responsive-configurator/)
- [Designing A Perfect Accordion](https://www.smashingmagazine.com/2017/06/designing-perfect-accordion-checklist/)
- [Designing A Perfect Infinite Scroll](https://www.smashingmagazine.com/2022/03/designing-better-infinite-scroll/)
- [Designing A Perfect Feature Comparison](https://www.smashingmagazine.com/2017/08/designing-perfect-feature-comparison-table/)
- [Designing A Perfect Slider](https://www.smashingmagazine.com/2017/07/designing-perfect-slider/)

### Related Articles

- “[How To Design Error States For Mobile Apps](https://www.smashingmagazine.com/2016/09/how-to-design-error-states-for-mobile-apps/)”, Nick Babich
- “[Designing Better Tooltips For Mobile User Interfaces](https://www.smashingmagazine.com/2021/02/designing-tooltips-mobile-user-interfaces/)”, Eric Olive

{{< signature "vf, yk, il" >}}
