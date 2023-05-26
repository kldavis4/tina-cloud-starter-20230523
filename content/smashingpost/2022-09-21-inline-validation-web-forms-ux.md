---
title: 'A Complete Guide To Live Validation UX'
slug: inline-validation-web-forms-ux
author: vitaly-friedman
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/64066efe-71fa-45b6-8e86-caf46c423b64/clean-up-input-ux-pattern.jpg
date: 2022-09-21T11:30:00.000Z
summary: >-
  Live, or inline validation in web forms is useful when it works, but frustrating when it fails. Too often it leads to an endless stream of disruptive error messages or dead-ends without any chance of getting out. Let’s fix it.
description: >-
  Live, or inline validation in web forms is useful when it works, but frustrating when it fails. Too often it leads to an endless stream of disruptive error messages or dead-ends without any chance of getting out. Let’s fix it.
categories:
  - UX
  - Design Patterns
---

Undoubtedly, there are major **advantages of live validation**. We validate input as users type, and so as people move from one green checkmark to another, we boost their confidence and create a sense of progression. If an input expects a particular type of content, we can **flag errors immediately**, so users can fix them right away. This is especially useful when choosing a secure password, or an available username.

<figure><a href="https://www.nngroup.com/articles/errors-forms-design-guidelines/"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/52200522-e541-4a63-b807-84f3b745030b/password-reset.gif" width="800" height="400" alt="Password reset" /></a><figcaption>Sometimes live validation works really well, for example with a <a href='https://www.nngroup.com/articles/errors-forms-design-guidelines/'>password strength meter</a>, as used by Slack. (Image credit: <a href="https://www.nngroup.com/articles/errors-forms-design-guidelines/">Error Forms Design Guidelines</a>)</figcaption></figure>

However, [live validation can be problematic](https://adamsilver.io/blog/live-validation-is-problematic/). Mostly because we can’t really show an error at just the right time when it occurs. And the reason for that is that we can’t *really* know for sure when a user has actually *finished* their input, unless they explicitly tell us that they have.

Clicking on a “Submit” button is a **very clear signal** that users *think* they are done, but our implementations usually consider leaving an input field as a **strong enough signal** to kick off the validation for that input field. Often it will be a correct assumption, but since it’s merely an assumption, eventually it will be wrong for *some* users &mdash; we just don’t know how many people, and how often, will be affected by it.

Surely we don’t want to show **“wrong” errors**; nor do we want to confuse and frustrate users with flashing error messages as they type. We want to show errors as they happen, and we want to replace them with friendly green checkmarks once they are fixed. How challenging can that be to implement? As it turns out, it is indeed quite challenging.

<!-- ## How Users Perceive Live Validation

As designers, when we think about inline validation, we primarily think about the **error recovery**. Surely if we validate *inline*, as users complete their input, we should be quite efficient in helping them fix errors almost instantly. However, as it turns out, sometimes it doesn’t quite work like that.

### Some People Never Notice Live Validation

When filling in web forms, some people heavily rely on **browser’s auto-fill**, so there isn’t really a lot of manual typing that would benefit from inline validation.

On the other hand, **some people never look at the screen when typing** &mdash; they look at the keyboard, jumping between the keys on their physical or virtual keyboard. Hence they might not even notice that there is any sort of real-time inline validation in place.

And if they do, sometimes inline validation actually slows them down. When an error appears, most users almost instinctively head to the erroneous input field to fix it right away, rather than fixing it later. After all, some sections often appear and disappear based on one or another selection. As a result, with errors showing up, users **keep switching** between the keyboard and the screen to fix errors or just double-check if the input is still correct.

{{< rimg breakout="true" href="https://carbondesignsystem.com/components/notification/usage/#inline-notifications" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d4f09e4c-b7c2-4b27-b739-67794ed90992/inviting-users-team-collaboration.jpeg" width="800" height="796" sizes="100vw" caption="When should the error message appear? On submitting the data, or when a user leaves the field? (Image credit: <a href='https://carbondesignsystem.com/components/notification/usage/#inline-notifications'>Carbon Design System</a>)" alt="A screenshot of a form allowing users to be innvited to get the team to collaborate with Email band Role being required to be filled out" >}}

### Early Validation Is Disruptive

And then there is the issue of the timing. Especially for complex forms, **premature error messages** are often perceived as an annoyance, and a very distracting one. They might even lead to more errors, reduced accuracy of data and increased completion times. It isn’t really *that* surprising as fixing all errors at once is likely to be faster than jumping between input fields every single time an error occurs.

One thing to keep in mind is that in all these situations, users often rely on the so-called **pattern matching**. Since lengthy strings are often broken down into chunks by delimeters, when typing, we enter the entire input in steps, with one chunk at a time, matching the pattern of the string, hence the name.

{{< rimg breakout="true" href="https://levelup.gitconnected.com/using-stripe-components-in-a-vue-app-with-typescript-146c008ed017" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2c30011b-0eb4-47b8-93e5-91173e917bb6/1-kwtexv6ymauinbsk7o87mq.png" width="800" height="796" sizes="100vw" caption="Credit card number input is typically done in 6 steps &mdash; 4 chunks for the card number, and one chunk for expiration date and CVC. (Image credit: <a href='https://levelup.gitconnected.com/using-stripe-components-in-a-vue-app-with-typescript-146c008ed017'>Image source</a>" alt="A screenshot of a form allowing users to be innvited to get the team to collaborate with Email band Role being required to be filled out" >}}

For example, when typing a credit card number, we typically type **4 chunks of 4 numbers**, rather than memorizing the entire string at once. And as we type the chunks, we follow the same process over and over again:

- We focus on the input field first,
- Then we look at the card and memorize the number,
- Then we head to the keyboard and type the numbers,
- Sometimes we switch to the screen to make sure the input is being registered,
- For the next chuck, we head to back to the card and then back to the keyboard &mdash; repeating the process multiple times. 

Of course another way of typing complex data is to simply **copy-paste the input** as a whole. Sadly, this often doesn’t work as expected as delimeters get copied as well, and the input is poorly truncated or breaks the form altogether. Plus, as users edit the input to match the expected format, they get disrupted by a flash of error messages.

### Disruptions Are Expensive

How big of a deal is it though? 
We know that [disruptions are expensive](https://www.frontiersin.org/articles/10.3389/fpsyg.2014.00841/full) and [time-consuming](https://www.sciencedirect.com/science/article/abs/pii/S074756320500107X). Even if they are helpful, and even if they effectively prevent mistakes, they also come at a cost: 

- Once interrupted, people need **3–27% more time** to complete tasks,
- Once distracted, people commit **twice the number of errors** across tasks,
- When switching contexts, people often forget the as-left conditions,
- Eventually people sometimes forget to return to the original task,
- With interruptions, task completion times tend to increase.
- Fixing all errors at once is faster than fixing errors individually.

In the situations listed above any kind of distraction is **highly unwanted and counter-productive**. And because early inline validation disrupts copy-pasting, causing mistakes, re-starts and a healthy dose of frustration, it’s probably a good idea to avoid it.

### Users Don’t Rely On Inline Validation Alone

Does live validation help with complex input? It does. If we expect a **particular prefix or postfix** in an input field, or if we can determine that the input is wrong based on a checksum, then it’s definitely a good idea to **flag the error right away** as users are still in the input field. This applies, for example, to VAT-numbers, which always start with a 2-digit-prefix, such as `DE` or `LT`. But it also helps with IBAN numbers, credit card details, lengthy policy insurance numbers and convoluted 16-digits-gift-coupon-codes.

On the other hand, inline validation is supposed to make sure that users don’t miss required fields or send ill-formatted data, yet just before moving to the next step in the form process, many people &mdash; despite green checkmarks all over the fields &mdash; **review their input meticulously**, from start to finish, sometimes even multiple times.

Why is that? Well, we all do trust inline validation, but usually we **don’t trust it enough** to prevent severe and critical errors &mdash; the errors that go beyond simple formatting issues. So for important forms, users review their entire input, field by field, watch out for typos, double check if auto-filled values are correct, and try to spot any kind of outdated input.

Users perceive inline validation as a helpful tool for a **structure/formatting check**; but they also need to perform an additional **data accuracy check** on their own. It’s not a big revelation, but worth emphasizing: a correct formatting of data doesn’t mean that the data is accurate. -->

<style>.course-intro{--shadow-color:206deg 31% 60%;background-color:#eaf6ff;border:1px solid #ecf4ff;box-shadow:0 .5px .6px hsl(var(--shadow-color) / .36),0 1.7px 1.9px -.8px hsl(var(--shadow-color) / .36),0 4.2px 4.7px -1.7px hsl(var(--shadow-color) / .36),.1px 10.3px 11.6px -2.5px hsl(var(--shadow-color) / .36);border-radius:11px;padding:1.35rem 1.65rem}@media (prefers-color-scheme:dark){.course-intro{--shadow-color:199deg 63% 6%;border-color:var(--block-separator-color,#244654);background-color:var(--accent-box-color,#19313c)}}</style>
  
<p class="course-intro"><em>Pssst!</em> This article is <strong>part of our ongoing series</strong> on <a href="/category/design-patterns">design patterns</a>. It’s also a part of <a style="font-weight:700" href="https://smart-interface-design-patterns.com/">Smart Interface Design Patterns</a>&nbsp;🍣 and is available in the <a href="https://smashingconf.com/online-workshops/workshops/interface-design-course-vitaly-friedman/">Live Interface Design Training</a>&nbsp;🍕 as well.</p>

## The Many Faces Of Live Validation

There are surprisingly many flavours of **live validation**. Over the years, we’ve learned to avoid [premature validation](https://baymard.com/blog/inline-form-validation#pitfall-1-premature-inline-validation) &mdash; live validation that happens when a user just focuses on an empty input field. In that case, we would display errors way too early, before users even have a chance to type anything. This isn’t helpful, and it is frustrating.

{{< rimg href="https://premium.zeit.de/bestellung/1597905" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0cb224ad-dc05-4105-bde6-dc7fe2913719/premature-validation.jpg" width="633" height="607" sizes="100vw" caption="Once a mistake has been done, and user is trying to correct it, we should remove the error message the moment the input becomes valid. It’s not the case at <a href='https://premium.zeit.de/bestellung/1597905'>Zeit.de</a>" alt="A screenshot of a form that shows error messages as a user has typed in a correct input." >}}

Eventually we moved to **real-time validation** which happens as users are typing. To do that, for every single field, we define a threshold of entered characters, after which we start validating. This doesn’t really *remove* frustration entirely, but rather *delays* it. As users eventually reach the threshold, if the input isn’t complete or properly formatted yet, they start getting confronted with flashes of premature error messages.

Live validation also typically requires quite elaborate and **strict formatting rules**. For example, at which point should we validate a day and a month for a date input? Would we validate them separately, or validate the date as a whole? Because both day and month inputs are interdependent, getting live validation right there is difficult. From testing, it seems that validating the date *at once* helps avoid premature errors for good. In practice, each input, and each type of input, requires a conversation about custom validation rules. 

{{< rimg href="https://www.ableton.com" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f4af5e8d-012f-4b84-ac27-f66ed20443a1/validate-on-submit-or-not.jpg" width="633" height="607" sizes="100vw" caption="Every input fields needs a conversation. For some fields, <a href='https://www.ableton.com'>Ableton</a> validates on blur, and for others validates only on submit." alt="A screenshot of a form that doesn’t show error messages unless a user chooses to submit the form." >}}

The most common type of live validation is **late validation**: we validate input once a user has *left* the input field (on `blur`), and just let them be as they are filling in the data or copy-paste it. This surely helps us avoid flashes of errors. However, we assume a particular order of progression from one field to another. We also prompt users to interrupt their progression and head back to fix an error once it has happened.


{{< rimg href="https://www.bestbuy.com/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/911bfc2b-89a4-4c4c-9637-fc0910891852/no-inline-validation.jpg" width="633" height="607" sizes="100vw" caption="The one that often gets forgotten: an alternative to live validation is validation only on submit, as it’s (partly) done on <a href='https://www.bestbuy.com/'>BestBuy.com</a>" alt="A screenshot of a form that doesn’t show error messages unless a user chooses to submit the form." >}}

So which live validation technique works best? As it turns out in usability testing, **users sincerely appreciate both** &mdash; the *live* validation and the *late* validation &mdash; if things go perfectly smoothly. Ironically, they also feel utterly frustrated by *any* kind of live validation once errors start showing up one after another.

## The Downsides Of Live Validation

This frustration shows up in different ways, from the task abandonment to the increased frequency of errors. And usually it’s related to a few well-known issues that live validation always entails:

- **Live validation always interrupts users**.  
A user might be just trying to answer a question, but error messages keep flashing in front of them as they type. That’s annoying, [disruptive](https://www.frontiersin.org/articles/10.3389/fpsyg.2014.00841/full) and [expensive](https://www.sciencedirect.com/science/article/abs/pii/S074756320500107X).
- **Live validation often kicks in too early or too late**.  
Errors appear either when the user is typing, or once they have moved to the next input field. Both of these options aren’t ideal: the user is interrupted as they type, or they are focused on the **next question**, yet we prompt them to fix their previous answer.
- **Live validation isn’t reliable enough**.  
Even though an live validator might give the user’s input green light, it can still flash an error message once the input has been re-checked on the server. A correct format of the input doesn’t mean that the input is also accurate.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dc78fa4c-56b0-449c-acae-30e9cfd766a9/when-live-validation-fails-ux.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dc78fa4c-56b0-449c-acae-30e9cfd766a9/when-live-validation-fails-ux.jpg" width="836" height="500" sizes="100vw" caption="Eventually, almost every validator will fail. Here are just a few examples of when it happens. What do we do in such situations? The best way is to always provide a way out. <a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dc78fa4c-56b0-449c-acae-30e9cfd766a9/when-live-validation-fails-ux.jpg'>Large view</a>." >}}

- **Validation rules aren’t error-prone to exceptions**.  
Validation rules rarely account for a much-needed wide range of exceptions and custom rules. They are often based on common assumptions that will eventually fail for some users &mdash; we just don’t know for how many.
- **Live validation demands immediate attention**.  
When an error appears, most users almost instinctively head to the erroneous input field to fix it right away. But with errors showing up frequently, users keep switching between the keyboard, mouse and the screen, rather than fixing all errors at once.
- **Often error messages are removed too late**.  
While the user is editing their input, often error messages remain visible until the user has left the input field again. This leaves users in the dark as they think they’ve fixed the problem already, but the interface doesn’t react accordingly.

Let’s see how we can use some simple techniques to address these issues effectively.

## 1. Show Errors Immediately If Issues Are Severe

Sometimes it’s critical to show an error immediately as it occurs to prevent unnecessary work and inaccurate input. For example, we probably want to **prevent unnecessary typing** if we know that the first few characters don’t match an expected format of the input.

Neither do we want to allow for Latin characters in a policy number that may contain only digits. In these cases, we need to communicate to users immediately that their input **can’t be right** &mdash; no matter how many more characters they would type in the input field.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d2e4d530-123f-482c-b1ef-629ef9dcbf46/wrong-iban-number.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d2e4d530-123f-482c-b1ef-629ef9dcbf46/wrong-iban-number.png" width="633" height="607" sizes="100vw" caption="We need to display errors if we know that users will appreciate the interruption. For severe mistakes, we need to flag issues right away. A <a href='https://www.gov.uk/'>Gov.uk</a>-inspired design." alt="Gov.uk-inspired example with an error for an incorrect IBAN number." >}}

This applies, for example, to ill-formatted VAT-numbers, which always start with a 2-digit-prefix, such as `DE` or `LT`. But it also helps with any standardized input such as IBAN number, credit card number, prefixed policy insurance number or lengthy digits-only gift-coupon-codes.

We also want to avoid wrong assumptions or wasted time between pages that potentially don’t even apply to users. The more severe an error is, the more likely it is that users might want to see it **sooner, rather than later**. However, when we do display errors, we need to ensure users will appreciate the interruption.

<!-- Surely if a required field is left empty, users won’t be able to continue. However, they can still correct their mistake before moving to the next step. Rather than throwing an error prematurely, we can allow them to fill in the data in any way they prefer, and flag the issue once they choose to move to the next step. -->

## 2. Late Validation Is Almost Always Better

Especially for complex forms, with plenty of columns, view switchers and filters, **premature error messages** are often perceived as an annoyance, and a very distracting one. As users are typing, any kind of distraction in such environments is highly unwanted and counter-productive. In fact, distraction often leads to even more errors, but also reduced accuracy of data and increased completion times.

Late validation almost always performs better. It’s just that by validating late, we can be more confident that the user isn’t still in the process of typing the data in the input field. The main exception would be any kind of input, for which users can benefit from real-time feedback, such as **password strength meter**, or a choice of an available username, or the character count limit. There we need to respond to user’s input immediately, as not doing so would only slow down users desperately trying to find they way around system’s requirements.

{{< rimg href="https://www.airbnb.com/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bc97e285-e9b4-4c78-befe-949032b8057f/password-strenght-meter-airbnb.png" width="633" height="607" sizes="100vw" caption="For password strength indicators (like <a href='https://www.airbnb.com/'>AirBnB</a>’s), we probably don’t want to validate late. But that might be one of the very few exceptions." alt="AirBnB example with a real-time updated password strength indicator." >}}

In practical terms, that means that for every input in a form, we need to review just what kind of feedback is needed, and design the interaction accordingly. It’s unlikely that one single rule for all inputs will work well: to be effective, we need a more granular approach, with a few **validation modes** that could be applied separately for each individual input.

## 3. Validate Empty Fields Only On Submit

Not all errors are **equally severe**, of course. Surely sometimes input is just ill-formatted or erroneous, but how do we deal with **empty form fields** or indeterminate radio buttons that are required? Users might have left them empty accidentally or intentionally, and there isn’t really a sure way for us to predict it. Should we throw an error *immediately* once the user has left the field empty? The answer isn’t obvious at all.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fa0bbe70-6b6d-4a27-bc96-1fc62e4a388a/premature-validation.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fa0bbe70-6b6d-4a27-bc96-1fc62e4a388a/premature-validation.png" width="633" height="607" sizes="100vw" caption="What should happen when a user leaves an empty field? Instead of displaying an error message, we could validate these input fields on submit only to avoid premature errors.  (Source: <a href='https://www.ae.com/intl/en/checkout'>American Eagle</a>)" alt="A screenshot of a form that shows error messages on empty input fields the moment user leaves them." >}}

The user might have indeed overlooked the input field, but that’s not the only option. They might as well just have **jumped in a wrong field** by mistake, and left it right away. Or they had to **jump back** to the previous field to correct an error triggered by the validator. Or they skipped the input field because they just wanted to get something else out of the way. Or maybe they just had to clear up their input and then move to another browser’s tab to copy-paste a string of text.

In practice, getting the UX around empty fields right is **surprisingly difficult**. Yet again, we can’t predict the context in which a user happens to find themselves. And as it turns out, they don’t always have a perfectly linear experience from start to finish &mdash; it’s often chaotic and almost unpredictable, with plenty of jumps and spontaneous corrections, especially in complex multi-column forms. And as designers, we **shouldn’t assume a particular order** for filling out the form, nor should we expect and rely on a particular tabbing behavior.

In my experience, whenever we try to flag the issues with empty fields, too often we will be pointing out mistakes prematurely. A calmer option is to validate empty fields **only on submit**, as it’s a clear indicator that a user indeed has overlooked a required input as they wish to proceed to the next step.

The earliest time to show an error message is when a user leaves a **non-empty input field**. Alternatively, depending on the input at hand, we might want to define a minimum threshold of characters, after which we start validating.

<!-- 
For example, if we expect a **particular prefix or postfix** in an input field, or if we can determine that the input is wrong based on a checksum, then it’s definitely a good idea to **flag the error right away** as users are still in the input field.  -->

## 4. Reward Early, Punish Late

Another issue that shows up eventually is what should happen if a user chooses to **change an input field that’s already been validated**? Do we validate immediately as they edit the input, or do we wait until they leave the input field?

As Mihael Konjević wrote in his article on the [Reward Early, Punish Late pattern](https://medium.com/wdstack/inline-validation-in-forms-designing-the-experience-123fb34088ce), if a user edits an **erroneous field**, we should be validating immediately, removing the error message and confirming that the mistake has been fixed as soon as possible (*reward early*). However, if the input was valid already and it is being edited, it’s probably better to wait until the user moves to the next input field and flag the errors then (*punish late*).


{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7b146191-97c9-4a90-bbd2-6fcb32c64b1c/reward-early-inline-validation-ux.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7b146191-97c9-4a90-bbd2-6fcb32c64b1c/reward-early-inline-validation-ux.png" width="633" height="607" sizes="100vw" caption="Reward users early if they fixed a mistake, and punish them later, once they’ve left the input field. A solution by <a href='https://medium.com/wdstack/inline-validation-in-forms-designing-the-experience-123fb34088ce'>Mihael Konjević</a>." alt="An animation of the reward-early/punish-late approach." >}}

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/33c6712e-4bb1-4979-a9d4-0c0a8ad71970/reward-early-punish-late-ux.gif"><img loading="lazy" decoding="async" fetchpriority="low" width="633" height="607" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/33c6712e-4bb1-4979-a9d4-0c0a8ad71970/reward-early-punish-late-ux.gif" sizes="100vw" alt="An animation of the reward-early/punish-late approach."></a><figcaption class="op-vertical-bottom">Reward users early if they fixed a mistake, and punish them later, once they’ve left the input field. A solution by <a href="https://medium.com/wdstack/inline-validation-in-forms-designing-the-experience-123fb34088ce">Mihael Konjević</a>.</figcaption></figure>

In technical terms, we need to **track the state and contents of each input field**, and have thresholds for when we start validating, and then have rules for changing input fields that have been validated already, or that contain errors.

As it turns out, the [implementation isn’t trivial](https://medium.com/@shanplourde/inline-form-validations-ux-design-considerations-and-react-examples-c2f53f89bebc), and making it work in a complex form will require quite a bit of **validation logic**. Beware that this logic might also be difficult to maintain if some fields have dependencies or show up only in certain conditions.

## 5. Prioritize Copy-Paste UX Over Live Validation

For pretty much any form, **copy-paste is almost unavoidable**. To many users, this seems like a much more accurate way of typing data as they are less likely to make mistakes or typos. While this is less typical for simple forms such as eCommerce checkout or sign up forms, it is a common strategy for complex enterprise forms, especially when users complete repetitive tasks.

However, **copy-paste is often inaccurate**, too. People tend to copy-paste too few or too many characters, sometimes with delimeteres, and sometimes with “too many” empty spaces or line breaks. Sadly, this often doesn’t work as expected as the input gets truncated, causes a flash of error messages or breaks the form altogether. Not to mention friendly websites that sometimes conveniently attach a string of text (URL or something similar) to the copied string, making copy-pasting more difficult.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/64066efe-71fa-45b6-8e86-caf46c423b64/clean-up-input-ux-pattern.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/64066efe-71fa-45b6-8e86-caf46c423b64/clean-up-input-ux-pattern.jpg" width="633" height="607" sizes="100vw" caption="Mistakes are too common with copy-paste. Perhaps we could allow users to clean up their input, either automatically or manually." alt="A screenshot with an error message providing an option to clean up the input" >}}

In all of these situations, live validation will flag errors, and rightfully so. Of course, in an ideal world, pasting would automatically remove all unnecessary characters. However, as text strings sometimes get appended to copied text automatically, even it wouldn’t really help. So if it’s not possible, an interesting alternative would is to add the **“clean-up” feature** that would cleanse the input and remove all unnecessary characters from it. Surely we’d also need to confirm with the user if the input is still right.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4f648fc6-5723-4f2e-b908-6e9819f18acb/clean-up-auto-fix-ux.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4f648fc6-5723-4f2e-b908-6e9819f18acb/clean-up-auto-fix-ux.jpg" width="633" height="607" sizes="100vw" caption="Copy-pasted input could be automatically corrected, with an option to cancel auto-correct. This requires auto-correct to be smart and reliable. And this isn’t easy to accomplish." alt="A screenshot with a hint explaining that the input has been auto-corrected." >}}

If instead, after copy-pasting, some parts of the input are **automatically removed**, or auto-formatted in a wrong way, it can become quite a hassle to correct the input. If we can auto-correct reliably, it’s a good idea to do so; but often getting it right can be quite difficult. Rather than correcting their own mistakes, users now have to correct *system’s mistakes*, and this rarely results in improved user satisfaction. In such situations, users sometimes would remove the entire input altogether, then take a deep breath and start re-typing from scratch. 

Typically, wrong auto-correct happens because the validator expects a **very specific format of input**. But should it actually? As long as the input is unambiguous, shouldn’t we accept pretty much *any* kind of input, in a form that users would prefer, rather than the one that the system expects?

{{< rimg breakout="true" href="https://github.com/jackocnr/intl-tel-input" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4dadd25b-f6e8-456d-a45c-0c856e2a73a5/drop-down-countries-number-codes.png" width="800" height="464" sizes="100vw" caption="Telephone input with auto-masking. This is difficult to copy-paste, and will cause errors with some users. (Image credit: <a href='https://github.com/jackocnr/intl-tel-input'>Jack O’Connor</a>)" alt="An example of a drop-down menu of telephone code numbers worldwide" >}}

A good example of that is a **phone number input**. In most implementations, one would often integrate fancy drop-downs and country selectors, along with auto-masking and auto-formatting in the phone number input field. Sometimes they work beautifully, but sometimes they fail miserably — mostly because they **collide with the copy-paste**, literally breaking the input. Not to mention that carefully selecting a country’s international code from a drop-down is much slower than just typing the number directly.

{{< rimg breakout="true" href="https://design-system.service.gov.uk/patterns/telephone-numbers/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9151e1f3-9397-41f7-8a8e-0886d69bbf4e/phone-international-numbers.png" width="800" height="215" sizes="100vw" caption="As long as the input is unambiguous, we should allow and support any input, with or without <code>+</code>, <code>00</code> or any delimeters. Auto formatting is fine, but it should work well with copy-paste. This is copy-paste-friendly UX. (Image credit: <a href='https://design-system.service.gov.uk/patterns/telephone-numbers/'>GOV.UK Design System</a>)" alt="A field to fill out in a form asking for a phone number including the country code" >}}

What’s wrong with the **auto-formatting**, by the way? Just like live validation is never reliable, so is auto-formatting. The phone number, for example, could start with `+49`, or `0049` or just the country code `49`. It might contain an extension code, and it might be a mobile phone number or a landline number. The question is, how can we **auto-format reliably and correctly** most of the time? This requires a sophisticated validator, which isn’t easy to build. In practical terms, for a given implementation, we need to test just how often auto-formatting fails and how exactly it fails, and refine the design (and implementation) accordingly.

One more thing that’s worth mentioning: **disabling copy-paste is never a good idea**. When we disable copy-paste for the purpose of security (e.g. email confirmation), or to prevent mistakes, people often get lost in the *copy-paste-loop*, wasting time trying to copy-paste multiple times, or in chunks, until they eventually give up. This doesn’t leave them with a thrilling sense of accomplishment, of course. And it does have an impact on the user satisfaction KPI.

In general, we should always allow users to type in data **in their preferred way**, rather than imposing a particular way that fits us well. The validation rules should support and greenlight *any* input as long as it’s unambiguous and not invalid (e.g. containing letters for phone input doesn’t make sense). The **data cleaning**, then, can be done either with late validation or on the server-side in a post-processing step.

{{% feature-panel id="vitaly-friedman" %}}

## 6. Allow Users to Override Live Validation

Because live validation is never bulletproof, there will be situations when users will be locked-out, without any option to proceed. That’s not very different from [disabled buttons](https://www.smashingmagazine.com/2021/08/frustrating-design-patterns-disabled-buttons/), which often cause nearly 100% abandonment rates. To avoid it, we always need to provide users with **a way out** in situations when live validation fails. That means adding an option to **override validation** if the user is confident that they are right.

To support overrides, we can simply add a note next to the input that seems to be erroneous, prompting users to review their input and **proceed despite the live validation error**, should they want to do so.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9770475b-2563-460d-861f-815f2714f4d1/german-street-house-number.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9770475b-2563-460d-861f-815f2714f4d1/german-street-house-number.png" width="800" height="203" sizes="100vw" caption="What happens if the validator doesn't know the address? We can allow users to override validator in some cases." alt="A screenshot of a fill-out form requesting a German street name and house number but the validator does not recognize or accept the address" >}}
 
We surely will end up with *some* wrong input in our database, but it might be quite manageable and easy to correct — and also worth it, if we manage to **boost conversion** as a result of that. Eventually, it’s all about making a case around the value of that design decision. 

To get there, we need to **measure the impact of overrides** for a few weeks. We need to understand just how much more revenue is coming through with the override and just how much inaccurate input and expenses or costs we produce because of it. The decision, then, should be based on these metrics and data, captured by [design KPIs](https://www.smashingmagazine.com/2022/04/boosting-ux-with-design-kpis/). This will give you a comparison to see **how costly live validation actually is** and make a case about having one, getting a buy-in to adjust it, or making a case for abandoning it.

{{% ad-panel-leaderboard %}}

## 7. Just-In-Time Validation

It might feel perfectly obvious that live validation is a perfect tool to **validate complex input**. If a user types in a 16-digits-gift-code, or a lengthy insurance policy number, providing them with confidence about their input is definitely a good idea.

But typing complex data takes time and effort. For lengthy input, users often copy-paste or type chunks of data in multiple steps, often with live validation flashing left and right as they enter and leave input fields. And because the input isn’t simple, they often **review their input** before proceeding to ensure that they haven’t made any mistakes. This might be one of the cases where **live validation is too much of a distraction** at the time when users are heavily focused on a task at hand.

{{< rimg href="https://ec.europa.eu/taxation_customs/vies/#/vat-validation" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/742c7358-7afd-4a92-b7b3-9b4ec3456e2b/vat-number-validation.jpg" width="949" height="635" sizes="70vw" caption="Not very exciting, but might be just right. We allow users to validate when they are confident that their input is complete. <a href='https://ec.europa.eu/taxation_customs/vies/#/vat-validation'>European Commission</a>." alt="An example of a VAT validation, with a Verify button acting only on submit. No live validation in place." >}}

So what do we do? Well, again, we could allow users to validate their input only when they are confident that it is complete. That’s the case with the **just-in-time validation**: we provide users with a **“Validate” button** that kicks off the validation on request, while the other fields are validated live, immediately.

However, whenever many pieces of content are **compounded in a large group** and have restrictive rules &mdash; like the credit card details, for example &mdash; it’s better to live validate them all immediately. This can help users avoid unnecessary input and change the type of input if needed.

## 8. For Short Forms, Consider Validation on Submit Only

Once we validate *just-in-time*, we can of course go even further and validate only on submit. The benefit of it is obvious: users are **never distracted or annoyed** by validation, and have full control over when their input is validated.

However, the pattern **doesn’t seem to work well** for lengthy pages with dozens and dozens of input fields. There, users often end up typing a lot of unnecessary data before they realize that their initial input isn’t really applicable. But perhaps we could avoid the issue altogether.

{{< rimg href="https://design-system.service.gov.uk/patterns/task-list-pages/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/aa18b524-2af1-4e52-a3e1-5274ecdc43b2/service-name-apply-application.jpeg" width="800" height="1052" sizes="100vw" caption="Many shorter pages tend to perform better than one long page. We can frame them as a part of the journey with a <a href='https://design-system.service.gov.uk/patterns/task-list-pages/'>task list pattern</a>. (Image credit: <a href='https://design-system.service.gov.uk/patterns/task-list-pages/'>GOV.UK Design System</a>)" alt="An example of a task list pattern" >}}

As it turns out, **shorter pages usually perform better than one long page**. In fact, for sophisticated forms, a better way to deal with complex journeys is to simplify them. We product a sort of a dashboard of tasks that a user has to complete in our complex journey, and dedicate single pages for single tasks. In details, it works like this:

- We split a complex form into small tasks = pages (with the [one-thing-per-page pattern](https://www.smashingmagazine.com/2017/05/better-form-design-one-thing-per-page/));
- For every page, we **validate (mostly) on submit**, as users are moving from one page to the next;
- We provide users with a [task list pattern](https://design-system.service.gov.uk/patterns/task-list-pages/) and support navigation between them, with the option to save input and continue later.

Not only does the approach make form much simpler to manage; because each part of the journey is quite simple and predictable, users are also **less likely to make mistakes**, but if they do make these mistakes, they can recover from them quickly — without jumping all over the entire form. Definitely an approach worth testing once you end up with a slightly more complex user journey.

{{% ad-panel-leaderboard %}}

## When Live Validation Works

We’ve gone all the way from the issues around live validation towards the option to abandon it altogether. However, it’s worth stating that **live validation can be very helpful** as well. It seems to be most effective when mistakes are common and quite severe.

For example, live validation is very useful with a **password strength meter**. When we describe and live-update password rules as users type, it helps users choose a password that matches all requirements, is secure and won’t trigger any error messages.

Users also appreciate **immediate help** with any kind of complex input. And, with live validation, users woul never fill out entire sections in the form just to realize that these sections do not apply to them.

All of these advantages make live validation a thrilling and thriving UX technique &mdash; especially in situations when most form fields are likely to be completed by [browser’s autofill](https://web.dev/learn/forms/autofill/). However, if the live validation is too eager, users quickly get utterly frustrated by it when errors start creeping out.

## Wrapping Up

Live validation is useful, but when it fails, its costs can be quite high. With just-in-time validation, *reward-early-punish-late*-pattern and validating on submit, we **avoid unnecessary distractions**, complex logic and layout shifts altogether, and communicate errors without annoying users too early or too late.

The downside is, of course, the **error recovery speed**, which certainly will be slower, yet in the end, the number of errors might be lower as well because we’ve simplified the form massively. It’s just much more difficult to make mistakes if you have just 3–4 input fields in front of you. And that might be just enough to reduce the frequency of errors and increase completion rates.



## Meet “Smart Interface Design Patterns”

If you are interested in similar insights around UX, take a look at [**Smart Interface Design Patterns**](https://smart-interface-design-patterns.com/), our shiny new **9h-video course** with 100s of practical examples from real-life projects. Design patterns and guidelines on everything from mega-dropdowns to complex enterprise tables &mdash; with 5 new segments added every year. *Just sayin’!* [Check a free preview](https://www.youtube.com/watch?v=aSP5oR9g-ss).

<figure style="margin-bottom: 1rem"><a href="https://smart-interface-design-patterns.com/"><img style="border-radius: 11px" decoding="async" fetchpriority="low" width="950" height="492" srcset="https://res.cloudinary.com/indysigner/image/fetch/f_auto,q_80/w_400/https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7cc4e1de-6921-474e-a3fb-db4789fc13dd/b4024b60-e627-177d-8bff-28441f810462.jpeg 400w,
https://res.cloudinary.com/indysigner/image/fetch/f_auto,q_80/w_800/https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7cc4e1de-6921-474e-a3fb-db4789fc13dd/b4024b60-e627-177d-8bff-28441f810462.jpeg 800w,
https://res.cloudinary.com/indysigner/image/fetch/f_auto,q_80/w_1200/https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7cc4e1de-6921-474e-a3fb-db4789fc13dd/b4024b60-e627-177d-8bff-28441f810462.jpeg 1200w,
https://res.cloudinary.com/indysigner/image/fetch/f_auto,q_80/w_1600/https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7cc4e1de-6921-474e-a3fb-db4789fc13dd/b4024b60-e627-177d-8bff-28441f810462.jpeg 1600w,
https://res.cloudinary.com/indysigner/image/fetch/f_auto,q_80/w_2000/https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7cc4e1de-6921-474e-a3fb-db4789fc13dd/b4024b60-e627-177d-8bff-28441f810462.jpeg 2000w" src="https://res.cloudinary.com/indysigner/image/fetch/f_auto,q_80/w_400/https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7cc4e1de-6921-474e-a3fb-db4789fc13dd/b4024b60-e627-177d-8bff-28441f810462.jpeg" sizes="100vw" alt="Smart Interface Design Patterns"></a><figcaption class="op-vertical-bottom">Meet <a href="https://smart-interface-design-patterns.com/">Smart Interface Design Patterns</a>, our new video course on interface design &amp; UX.</figcaption></figure>

<div class="btn--lined btn--lined--white-border" style="margin-top: 0.75em; margin-bottom: 0.75em"><a class="btn btn--large btn--green btn--text-shadow" href="https://smart-interface-design-patterns.com/">Jump to the video course&nbsp;&rarr;</a></div>

<p class="ticket-price__desc" style="font-size: .8em!important; text-align: center; line-height: 1.5; margin-top: 0; display: block;">100 design patterns &amp; real-life 
examples.<br>9h-video course + live UX training. <a href="https://www.youtube.com/watch?v=aSP5oR9g-ss">Free preview</a>.</p>

## Related UX Articles

- [Designing Better Error Messages UX](https://www.smashingmagazine.com/2022/08/error-messages-ux-design/)
- [Rethinking Authenticaiton UX](https://www.smashingmagazine.com/2022/08/authentication-ux-design-guidelines/)
- [Disabled Buttons UX](https://www.smashingmagazine.com/2021/08/frustrating-design-patterns-disabled-buttons/)
- [Designing A Perfect Infinite Scroll](https://www.smashingmagazine.com/2022/03/designing-better-infinite-scroll/)
- [Design Patterns and UX on SmashingMag](https://www.smashingmagazine.com/category/ux/)

{{< signature "yk, il" >}}
