---
title: How To Design Error States For Mobile Apps
slug: how-to-design-error-states-for-mobile-apps
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/893434c4-d6a8-4fc0-ab32-64c1e0d2668d/error-state-image21-opt-1.png
date: 2016-09-21T16:51:50.000Z
author: nickbabich
summary: >-
  The best error message is the one that never shows up. It is always better to prevent errors from happening in the first place by guiding users in the right direction ahead of time. But, when errors do arise, well-designed error handling not only helps teach users how to use the app as you intended, but also prevents users from feeling ignorant.
description: >-
  The best error message is the one that never shows up. It is always better to prevent errors from happening in the first place by guiding users in the right direction ahead of time. But, when errors do arise, well-designed error handling not only helps teach users how to use the app as you intended, but also prevents users from feeling ignorant.
categories:
  - Mobile
  - Forms
  - Interaction Design
  - Experience Design
  - Sponsored Content
disable_ads: true
disable_panels: true
---
(This is a sponsored article.) To err is human. Errors occur when people engage with user interfaces. Sometimes, they happen because users make mistakes. Sometimes, they happen because an app fails. Whatever the cause, these errors and how they are handled, have a huge impact on the user experience. Bad error handling paired with useless error messages can fill users with frustration, and can lead to users abandoning your app.

In this article, we’ll examine **how the design of apps can be optimized to prevent user errors** and how to create effective error messages in cases when errors occur independently of user input. We’ll also see how well-crafted error handling can turn a moment of failure into a moment of delight. Adobe introduced a new design and wireframing app called Experience Design (Adobe XD) that lets you design interactive wireframes and error states. You can download and test [Adobe XD](https://adobe.ly/2bs2eXP) **for free**.

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Animated Microinteractions In Mobile Apps](https://www.smashingmagazine.com/2016/08/experience-design-essentials-animated-microinteractions-in-mobile-apps/)
*   [How To Create Icons With Adobe XD](https://www.smashingmagazine.com/2016/07/how-to-create-icons-adobe-xd/)
*   [Useful Prototyping Tricks in Adobe XD](https://www.smashingmagazine.com/2016/07/quick-ux-prototyping-with-adobe-xd-shortcuts-pdf-cheatsheet/#comments)
*   [How Prototyping Made Us More Efficient](https://www.smashingmagazine.com/2016/08/prototyping-for-success/)

## What Is An Error State?

An error state is a screen that is shown when things go wrong. It is an example of a situation where the user is getting something other than their desired state. Since errors can occur in surprising combinations, these states can include anything from incompatible user operations (such as invalid data input), to the inability of an app to connect to the server, or even the inablity to process a user request.

{{% feature-panel %}}

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/67fbb64d-5c5d-4e26-acb5-ec5b3026e509/errorstate10-768x628-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a2ea0522-028d-4481-affc-9dfb5f3af30a/error-state-image11-opt.jpg" width="500" height="409" alt="errorstate(10)" /></a><figcaption>Error state screens. Image credit: <a href="https://material.google.com/">Material Design</a>. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/67fbb64d-5c5d-4e26-acb5-ec5b3026e509/errorstate10-768x628-opt.jpg">Large view</a>)</figcaption></figure>

Every error, regardless of cause, becomes a point of friction for your users and blocks them from moving forward in their experience. Luckily, well-designed error handling can help reduce that friction.</p>

## Prevention Is Better Than Cure

If you design apps, you should be familiar with the most common in-app interactions that could lead to the error state (error-prone conditions). For example, it’s usually hard to correctly fill out a form on the first attempt, or it’s impossible to properly sync data if the device has a poor network connection. You should take these cases into account to minimize the possibility of errors. In other words, it’s better to prevent users from making errors in the first place by offering suggestions, utilizing constraints, and being flexible.

For instance, if you’re allowing people to search for a hotel reservation, why make past dates available and display an error if users select dates that are in the past?

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/70dc9b91-3a1f-4022-8f97-4d6d978eec95/errorstate4-600x274-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/32e7be9f-14cc-4b44-add5-2c168720acf5/errorstate4-600x274-500-opt.png" width="500" height="228" alt="errorstate(4)" /></a><figcaption><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/70dc9b91-3a1f-4022-8f97-4d6d978eec95/errorstate4-600x274-opt.png">Large view</a></figcaption></figure>

As shown in the Booking.com example, you can simply use a date selector that allows users to only choose today’s date or dates in the future. This will force users to pick a date range that fits.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3f87a1a5-959d-4025-a2c7-99d15f045737/error-state-image14-opt.jpg"><img loading="lazy" decoding="async" alt="Use a date selector that allows users to choose only today's date or dates in the future. This will force users to pick a date range that fits." src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3f87a1a5-959d-4025-a2c7-99d15f045737/error-state-image14-opt.jpg" width="250" /></a><figcaption>The date picker in the Booking.com app displays a full monthly calendar, but grays out past dates so users can choose proper dates. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3f87a1a5-959d-4025-a2c7-99d15f045737/error-state-image14-opt.jpg">Large preview</a>)</figcaption></figure>

## Error Screen For Form Validation

A form is a conversation. Like any conversation, it should be represented by a consistent communication between two parties — the user and your app. Validation plays an essential part of this conversation. Form validations are meant to have conversations with users and guide them through the difficult times of errors and uncertainty. When done right, it can turn an ambiguous interaction into a clear one. Generally speaking, there are four important elements that good form validation consists of:

*   Right time of informing about errors (or success)
*   Right place for validation output
*   Right color for the message
*   Clear language for your message

### Right Time (Inline Validation)

Form validation errors are inevitable and are a natural part of a user’s data input (since user’s input is error-prone). Yes, error-prone conditions should be minimized, but validation errors won’t ever be eliminated. So, the most important question is, "How do you make it easy for the user to recover from form errors?"

Users dislike going through the process of filling out a form, only to find out at submission that they’ve made an error. It’s especially frustrating when you complete a long form and once you’ve pressed submit, you are rewarded with multiple error messages. And it’s even more annoying when it isn’t clear what errors you’ve committed, and where.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fd2dc167-fd06-4dd9-8967-a3c9f4f1e8cf/error-state-image-24-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fd2dc167-fd06-4dd9-8967-a3c9f4f1e8cf/error-state-image-24-opt.png" width="250" alt="It’s especially frustrating when you complete a long form and once you’ve pressed submit you are rewarded with multiple error messages. And it’s even more annoying when it isn’t clear what errors you’ve committed, and where." /></a><figcaption>Image credit: <a href="https://ux.stackexchange.com/questions/33108/how-to-best-show-connectivity">Stackexchange</a>. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fd2dc167-fd06-4dd9-8967-a3c9f4f1e8cf/error-state-image-24-opt.png">Large view</a>)</figcaption></figure>

Validation should immediately inform users about the correctness of a provided answer right after the user has submitted the data. The primary principle of good form validation is this: “Talk to the users! Tell them what is wrong!” and real-time inline validation immediately informs users about the correctness of provided data. This approach allows users to correct the errors they make faster without having to wait until they press the submit button to see the errors.

However, avoid validating on each keystroke because, in most cases, you simply cannot verify until someone has finished typing their answer. Forms that perform the validation during the data entry punish the users as soon as they start entering the data.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6cbe1a05-abd8-4f99-9d10-6f6e9de51719/error-state-image20-opt.gif"><img loading="lazy" decoding="async" data-src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6cbe1a05-abd8-4f99-9d10-6f6e9de51719/error-state-image20-opt.gif" width="500"></a><figcaption>Google Forms states the email isn’t valid when you’re not done typing it. (Image credit: <a href="https://medium.com/wdstack/inline-validation-in-forms-designing-the-experience-123fb34088ce#.fl86493cl">Medium</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6cbe1a05-abd8-4f99-9d10-6f6e9de51719/error-state-image20-opt.gif">Large preview</a>)</figcaption></figure>

On the other hand, forms that perform validation after the data entry are not informing the user soon enough that they fixed the error.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a88f0dcd-2e70-41cc-9298-6831a41c8d98/error-state-image17-opt.gif"><img loading="lazy" decoding="async" alt="Validation in Apple Store is performed after the data entry" data-src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a88f0dcd-2e70-41cc-9298-6831a41c8d98/error-state-image17-opt.gif" width="500" /></a><figcaption>Validation in Apple Store is performed after the data entry. (Image credit: <a href="https://medium.com/wdstack/inline-validation-in-forms-designing-the-experience-123fb34088ce#.fl86493cl">Medium</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a88f0dcd-2e70-41cc-9298-6831a41c8d98/error-state-image17-opt.gif">Large preview</a>)</figcaption></figure>

Mihael Konjević in his [article](https://medium.com/wdstack/inline-validation-in-forms-designing-the-experience-123fb34088ce#.fl86493cl) “Inline validation in forms — designing the experience” examined different validation strategies and propose a hybrid validation strategy: reward early, punish late.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f6991e43-48d0-4466-8a74-3a1ff289de7a/error-state-image16-opt.gif"><img loading="lazy" decoding="async" alt="The reward early, punish late approach" data-src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f6991e43-48d0-4466-8a74-3a1ff289de7a/error-state-image16-opt.gif" width="500" /></a><figcaption>Hybrid — reward early, punish late — approach. (Image credit: <a href="https://medium.com/wdstack/inline-validation-in-forms-designing-the-experience-123fb34088ce#.fl86493cl">Medium</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f6991e43-48d0-4466-8a74-3a1ff289de7a/error-state-image16-opt.gif">Large preview</a>)</figcaption></figure>

### Right Place

Proximity is another important tool. When you’re wondering what place to choose for your validation messages, follow this rule of thumb — always put the message in the context of action. If you want to inform the user about an error occurring in a particular field — show it next to the field. Instant validation is best positioned to the right-hand side of the input, or failing that, immediately below.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2af71233-3ac6-4103-9183-50c843514c5d/error-state-image-08-opt.png"><img loading="lazy" decoding="async" alt="Communicate form errors in real time" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2af71233-3ac6-4103-9183-50c843514c5d/error-state-image-08-opt.png" width="500" /></a><figcaption>Communicate form errors in real time. (Image credit: <a href="https://thinkwithgoogle.com">ThinkwithGoogle</a>( (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2af71233-3ac6-4103-9183-50c843514c5d/error-state-image-08-opt.png">Large preview</a>)</figcaption></figure>

### Right Color (Intuitive Design)

Color is one of the best tools to use when designing validation. Because it works on an instinctual level, adding red to error messages, yellow to warning messages, and green to success messages is incredibly powerful. But, make sure that colors in your digital interface are accessible for your users. It’s a crucial aspect of a well-executed visual design.</p>

<figure><img loading="lazy" decoding="async" alt="Error text should be legible, with a proper color and noticecable contrast" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b2eb163d-ace1-4f7f-a267-59a92cfdaf69/error-state-image-09-opt.jpg" width="250" /><figcaption>Error text should be legible, with a proper color and noticecable contrast against its background. Image credit: <a href="https://material.google.com">Material Design</a></figcaption></figure>

### Clear Message

A typical error might state, “the email is invalid,” without telling the user why it’s invalid. (Is it a typo? Is it occupied?) Straightforward instructions, or guidelines, make all the difference. There is no guessing for the user who receives this error, and also no confusion or frustration. You can see in the example, the form informs the user that this email is already in use. It then offers some options (either to login or recover my password).</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/521a8bd5-54c0-4bad-88ee-ac49a8b68f70/error-state-image-06-opt.png"><img loading="lazy" decoding="async" alt="A form saying that this email is already in use and offers some options" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/521a8bd5-54c0-4bad-88ee-ac49a8b68f70/error-state-image-06-opt.png" width="500" /></a><figcaption>App Errors: Failure To Load Data (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/521a8bd5-54c0-4bad-88ee-ac49a8b68f70/error-state-image-06-opt.png">Large preview</a>)</figcaption></figure>

Okay, it’s time to display an error page to indicate that something has gone wrong. As an example, let’s take a situation when connectivity is down and a user is on a screen that is only available online. You should use this opportunity to make people aware that you know what is happening and follow the model of immediate helpfulness — your error message should be a helping hand for your users. That’s why you should **never** show:

*   **A raw error message**. Messages which contain an app’s internal error codes or abbreviations such as “an error of type 2 has occurred” are cryptic and scary.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2e999b2f-de14-4f47-b737-887835676f5f/errorstate9-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2e999b2f-de14-4f47-b737-887835676f5f/errorstate9-opt.png" width="250" alt="This error message was written by a developer for a developer" /></a><figcaption>This error message was written by a developer for a developer. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2e999b2f-de14-4f47-b737-887835676f5f/errorstate9-opt.png">Large preview</a>)</figcaption></figure>

*   **A dead-end error message**. Simply because, such error states don’t provide any helpful information for users.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0dc88fa9-429b-4b27-8fff-dae1d7b49d45/errorstate-2-335x675-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0dc88fa9-429b-4b27-8fff-dae1d7b49d45/errorstate-2-335x675-opt.jpg" width="250" alt="Spotify error screen just states ‘An error occurred’ and doesn’t provide any constructive advice on how to fix the problem." /></a><figcaption><a href="https://itunes.apple.com/en/app/spotify-music/id324684580?mt=8">Spotify’s</a> error screen just states ‘An error occurred’ and doesn’t provide any constructive advice on how to fix the problem. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0dc88fa9-429b-4b27-8fff-dae1d7b49d45/errorstate-2-335x675-opt.jpg">Large preview</a>)</figcaption></figure>

*   **A vague error message**. The error screen in the example below gives users the same amount of information as the previous one. Users won’t have any clue what it means and what to do next.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8602cfd9-b01e-46b8-9c81-1eaca987401d/errorstate11-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8602cfd9-b01e-46b8-9c81-1eaca987401d/errorstate11-opt.png" width="250" alt="Buffer has a well-designed error state, but the copy won’t mean much to users." /></a><figcaption><a href="https://buffer.com/">Buffer</a> has a well-designed error state, but the copy won’t mean much to users. (Image credit: <a href="https://emptystat.es/post/42539678731/buffer-shows-a-nice-error-state-but-the-copy-wont">emptystat.es</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8602cfd9-b01e-46b8-9c81-1eaca987401d/errorstate11-opt.png">Large preview</a>)</figcaption></figure>

Don’t scare users with errors. Also, don’t assume people know about the context of a message or assume they are tech-savvy enough to figure things out. Instead, tell people what’s wrong in plain language. To achieve this, you should avoid using technical jargon and express everything in the user’s vocabulary.

Make your error message both readable and helpful — error states must include concise, polite, and instructive copy that clearly states:

*   What went wrong and possibly why.
*   What’s the next step the user should take to fix the error.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/839e5dfb-3a8d-48e4-82d4-7810b693cba4/error-state-image-04-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/839e5dfb-3a8d-48e4-82d4-7810b693cba4/error-state-image-04-opt.jpg" width="250" height="510" alt="Remote app explains why user cannot see anything, and how to solve this." /></a><figcaption><a href="https://itunes.apple.com/en/app/remote/id284417350?mt=8">Remote app</a> explains why a user cannot see anything, and how to solve it. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/839e5dfb-3a8d-48e4-82d4-7810b693cba4/error-state-image-04-opt.jpg">Large preview</a>)</figcaption></figure>

## Incorporate Imagery And Humor Into Error States

Error states are an excellent opportunity to utilize icons and illustrations, because people respond better to visual information than plain text. But, you can go further and incorporate unique imagery that is branded to match your app, yet still be helpful for your users. It’s a good way to both humanize your message and communicate the app’s personality.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a5ed00aa-7b15-4089-b42e-0b8183691df4/error-state-image15-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a5ed00aa-7b15-4089-b42e-0b8183691df4/error-state-image15-opt.jpg" width="250" height="510" alt="A funny Azendoo error message saying Keep Calm and light a fire" /></a><figcaption><a href="https://www.azendoo.com/">Azendoo</a> uses a memorable illustration and humorous copy which encourage users to solve the problem. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a5ed00aa-7b15-4089-b42e-0b8183691df4/error-state-image15-opt.jpg">Large preview</a>)</figcaption></figure>

Humor is the spice of life. A bit of humor never hurts and can help diffuse the frustration of an error. You can find plenty of great examples of humorous error messages at [Littlebigdetails](https://littlebigdetails.com). Here are some of my favorites:

*   Basecamp: when there is a form field error, the character on the left makes a surprising facial expression.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ed559c5f-6ae7-4d78-9ec5-a07bf44d9f96/error-state-image18-opt.png"><img loading="lazy" decoding="async" alt="" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ed559c5f-6ae7-4d78-9ec5-a07bf44d9f96/error-state-image18-opt.png" width="500" /></a></figure>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fd43bf9d-b51a-4b9a-92f1-fb04c91b54f4/error-state-image13-opt.png"><img loading="lazy" decoding="async" alt="" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fd43bf9d-b51a-4b9a-92f1-fb04c91b54f4/error-state-image13-opt.png" width="500" /></a><figcaption>Image credits: <a href="https://twitter.com/destraynor">Des Traynor</a></figcaption></figure>

*   A cheeky error message is displayed when you type too many full-stops when creating a new account in [Gmail](https://gmail.com/).</p>

<figure><img loading="lazy" decoding="async" alt="A cheeky error message is displayed when you type too many full-stops when creating a new account in GMail" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/40637b93-c609-40a3-8e5e-90ece1b4da82/error-state-image-02-opt.png" width="329" height="109" /><figcaption>Image credit: <a href="https://simonsouris.com/">Simon Souris</a></figcaption></figure>

However, be careful with humor because it may not always be appropriate to use in your error message; it really depends on the severity of the error. For instance, humor is good for a simple validation problem such as a "404 Page Not Found" error. But when a user is losing a significant amount of time due to a failure saying “Uh oh!” is entirely inappropriate.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ac8647c4-f00e-47cd-8d0c-9f630124fc74/error-state-image-05-opt.png"><img loading="lazy" decoding="async" alt="saying Uh-oh is entirely inappropriate." src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ac8647c4-f00e-47cd-8d0c-9f630124fc74/error-state-image-05-opt.png" width="500" /></a><figcaption>(Image credit: <a href="https://medium.com/@thomasfuchs">Thomas Fuchs</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ac8647c4-f00e-47cd-8d0c-9f630124fc74/error-state-image-05-opt.png">Large preview</a>)</figcaption></figure>

## Comprehensive Checklist Of A Perfect Error Page

Perfect error pages are a helping hand for your users and should have the following six qualites:

1.  Error messages occur dynamically, just as the problem appears. This immediately informs users about the problem.
2.  Keep all user input safe. Your app shouldn’t undo, destroy, or delete anything entered or uploaded by user in the event of an error.
3.  Speak the same language as the user. It should clearly state what went wrong and possibly why; what’s the next step the user should take to fix the error?
4.  Don't shock or confuse users. (The message shouldn’t be dramatic).
5.  Don't hijack control of the system. (If problem isn’t critical, the user should be able to interact with as much of the rest of the app as possible).
6.  Use a little sense of humor to humanize the problem.</p>

## Solutions For The Most Popular Error States

### 404 Not Found Error

The main goal of 404 page is to direct your user to the page they were looking for as quickly as possible. Your 404 page should offer a few key links and directions your user can choose between. A safe bet is to have a “Home” link as a primary action on the 404 page — a quick and friendly way to start over. You can also place “Report this Page” to quickly report that the page is broken, but make sure that the primary action (link to the “Home” page) carries a stronger visual weight.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8489dd57-a62a-4f4d-a5fe-d08d6fd59e6e/error-state-image23-opt.png"><img loading="lazy" decoding="async" alt="Your 404 page should offer a few key links and directions your user can choose between" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8489dd57-a62a-4f4d-a5fe-d08d6fd59e6e/error-state-image23-opt.png" width="500" /></a><figcaption>(Image credit: <a href="https://dribbble.com/shots/2296102-Error-500-page">Natalie Kirejczyk</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8489dd57-a62a-4f4d-a5fe-d08d6fd59e6e/error-state-image23-opt.png">Large preview</a>)</figcaption></figure>

### Cannot Login

Login screens are usually relatively minimal, with a field for a username and another for a password. But, minimal doesn’t always equal simple. There are many reasons why a user might be stuck on the login screen. The main rule for a login page is very simple - don’t make the user guess.

Let’s propose solutions for the most common problems using examples from [MailChimp](https://mailchimp.com/), which does a great job with error messaging.

*   User forgets his username. If you detect that the problem is an unknown username, you should offer a link to let the user fix it. Tell users where they can get it (e.g. “check email from us”) or provide a link to the username recovery.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5bbd6fd7-3598-4fe0-8296-377d6db88f8b/error-state-image26-opt.png"><img loading="lazy" decoding="async" alt="Tell users where they can get the username or password recovery link e.g. check your email" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5bbd6fd7-3598-4fe0-8296-377d6db88f8b/error-state-image26-opt.png" width="250" /></a></figure>

Users make multiple attempts to log in using an incorrect password. To prevent brute force attacks, user accounts are often temporarily locked after too many failed login attempts. This is a necessary security practice, but be sure to warn users before their account is locked.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/49b91921-14d1-4d3a-af05-ba04e6750cf0/error-state-image-00-opt.png"><img loading="lazy" decoding="async" alt="Be sure to warn users before their account is to be locked" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/49b91921-14d1-4d3a-af05-ba04e6750cf0/error-state-image-00-opt.png" width="250" /></a></figure>

### Credit Card Rejection

Credit card rejection error page can be caused by (1) errors in the data formatting (typo or missing data) or (2) a card can be declined (expired card or fraud). [Gabriel Tomescu](https://uxdesign.cc/@gabrieltomescu) in his article “The anatomy of a credit card form,” suggested the following strategy for both error states:

For the first problem, you should follow standard real-time inline validation practice and visually indicate an error:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/937b8cee-54ff-40cb-9066-9d22b8cdb95f/error-state-image22-opt.png"><img loading="lazy" decoding="async" alt="Notify the user with a real-time inline error message" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/937b8cee-54ff-40cb-9066-9d22b8cdb95f/error-state-image22-opt.png" width="250" /></a><figcaption>(Image credit: <a href="https://uxdesign.cc/the-anatomy-of-a-credit-card-payment-form-32ec0e5708bb#.3i8tpzdy7">uxdesign</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/937b8cee-54ff-40cb-9066-9d22b8cdb95f/error-state-image22-opt.png">Large preview</a>)</figcaption></figure>

However, when a card is declined by the payment network for some reason, it usually looks like fraud. You need to clear the data entered by the user. Even then, you still need to notify the user what has happened; the error message should be as clear as possible.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/16cd0449-9ecf-45d5-8c87-a46f701988d7/error-state-image12-opt.png"><img loading="lazy" decoding="async" alt="Notify the user what just happened, as clear as possible" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/16cd0449-9ecf-45d5-8c87-a46f701988d7/error-state-image12-opt.png" width="500" /></a><figcaption>(Image credit: <a href="https://uxdesign.cc/the-anatomy-of-a-credit-card-payment-form-32ec0e5708bb#.53wocu264">uxdesign</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/16cd0449-9ecf-45d5-8c87-a46f701988d7/error-state-image12-opt.png">Large preview</a>)</figcaption></figure>

### Connectivity Is Down

Internet access is not ubiquitous, and offline support should be a crucial consideration for nearly every modern app. When connectivity is down, you should try to provide a rich offline experience. Users should be able to interact with as much of the rest of your app as possible. This means the app should have cached content to provide a good offline experience.

Daniel Sauble in his [article](https://uxdesign.cc/offline-93c2f8396124#.6xmbytkso) provides perfect insight on how social, mapping, and productivity apps function offline. It’s totally clear why he suggests that it’s better to cache a little of everything than a lot of some things and nothing of others. Because, when a user opens an app, they expect to see content, regardless of whether they’re connected to the internet or not. If the content isn’t there, they’ll get frustrated and switch to a different app which does a better job of caching the information they want to see.

Make sure your app functions offline as well as it possibly can. Here is some practical advise from [Robert Woo](https://www.rocketfarmstudios.com/author/robert/) that can be incorporated almost in every app on the market.

Save the last state. Below you can see two apps made for content delivery. The CNN app provides a better user experience by caching the last view and providing users with the headlines for the articles that were last loaded.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d34082b5-93bd-468e-9a9c-652295c04543/error-state-image19-opt.png"><img loading="lazy" decoding="async" alt="CNN app provides a better user experience by caching the last view and providing users with the headlines for the articles that were last loaded." src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d34082b5-93bd-468e-9a9c-652295c04543/error-state-image19-opt.png" width="500" /></a><figcaption>(Image credit: <a href="https://www.rocketfarmstudios.com/blog/4-ways-to-improve-offline-mobile-apps/">rocketfarmstudios</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d34082b5-93bd-468e-9a9c-652295c04543/error-state-image19-opt.png">Large preview</a>)</figcaption></figure>

**Provide offline functionality and features.** There are features on every app that can (and should) work without an internet connection. Let’s take Evernote as an example. The app is entirely functional offline: you can edit existing notes or write a new one, and the app will sync everything up with the cloud once you’re connected again.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/abe6d4fd-281d-4c19-a763-c64ec7f7e5ee/error-state-image-07-opt.png"><img loading="lazy" decoding="async" alt="Evernote is entirely functional offline — you can edit existing notes or write a new one, and the app will sync everything up with the cloud once you’re connected again" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/abe6d4fd-281d-4c19-a763-c64ec7f7e5ee/error-state-image-07-opt.png" width="250" /><figcaption>(Image credit: <a href="https://emptystat.es/">emptystates</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/abe6d4fd-281d-4c19-a763-c64ec7f7e5ee/error-state-image-07-opt.png">Large preview</a>)</figcaption></figure>

## Conclusion

The best error message is the one that never shows up. It is always better to prevent errors from happening in the first place by guiding users in the right direction ahead of time. But, when errors do arise, well-designed error handling not only helps teach users how to use the app as you intended, but also prevents users from feeling ignorant. Of course, the error state is one of the least-desirable states to design for. However, if you put a lot of effort into this state, your product will be infinitely more enjoyable to use.</p>

## Recommended Materials

*   [The Ultimate UX Design of Form Validation](https://designmodo.com/ux-form-validation/) by Marcin Treder
*   [Inline Validation in Web Forms](https://alistapart.com/article/inline-validation-in-web-forms) by Luke Wroblewski
*   [Improve Validation Errors with Adaptive Messages](https://baymard.com/blog/adaptive-validation-error-messages) by Jamie Appleseed
*   [How to write a great error message](https://medium.com/@thomasfuchs/how-to-write-an-error-message-883718173322#.6rlptz1gj) by Thomas Fuchs

<blockquote style="border-radius: 8px;">This article is part of the UX design series sponsored by Adobe. The newly introduced <a href="https://adobe.ly/2bs2eXP">Experience Design app</a> is made for a fast and fluid UX design process, as it lets you go from idea to prototype faster. Design, prototype and share — all in one app.<br /><br />You can check out more inspiring projects created with Adobe XD on <a href="https://www.behance.net/search?content=projects&sort=appreciations&time=week&tools=387566349">Behance</a>, and also visit the <a href="https://blogs.adobe.com/creativecloud/design/">Adobe XD blog</a> to stay updated and informed. Adobe XD is being updated with new features frequently, and since it's in public Beta, you can <a href="https://adobe.ly/2bs2eXP">download and test it for free</a>.</blockquote>

{{< signature "ms, il, at" >}}
