---
title: How Usability Testing Drastically Improved My Client's App
slug: how-usability-testing-drastically-improved-my-clients-app
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5b679efa-ef54-41f8-a86e-de3d45334f13/usability-tests.jpg
date: 2013-11-19T14:30:14.000Z
author: joshua-gross
description: >-
  Most designers spend too much time with their designs to be objective about
  them. The best thing any designer can do is to collect feedback from real
  users. **Testing uncovers pain points** and flaws in a design that are not
  otherwise obvious.
categories:
  - UX
  - Clients
  - Usability
  - Responsive Design
  - Interfaces
  - Interaction Design
---
Most designers spend too much time with their designs to be objective about them. The best thing any designer can do is to collect feedback from real users. <strong>Testing uncovers pain points</strong> and flaws in a design that are not otherwise obvious.

Recently, I had an opportunity to experience this firsthand when iterating on <em>HelloSign</em>, the iOS app that enables users to scan, sign and send documents from their phone using the built-in camera. Thanks to testing, the app went from four stars to a solid five stars after a redesign. We’ll look at how the app started, how we ran the tests and how the product ended up with five stars.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Prioritizing Devices: Testing And Responsive Web Design](https://www.smashingmagazine.com/2016/11/worlds-best-open-device-labs/)
*   [Noah’s Transition To Mobile Usability Testing](https://www.smashingmagazine.com/2016/02/mobile-usability-testing/)
*   [Where Are The World’s Best Open Device Labs?](https://www.smashingmagazine.com/2016/11/worlds-best-open-device-labs/)
*   [A Guide To Simple And Painless Mobile User Testing](https://www.smashingmagazine.com/2015/12/simple-and-painless-mobile-user-testing/)

## The Original Design

This app has four primary sections: authentication, welcome, document creation and document editing. The biggest changes we made to the app were on the authentication and welcome screens. We’ll first briefly review the original designs of these screens, as well as the document creation and editing screens, to understand how the app works.

{{% feature-panel %}}

### Authentication and Welcome

The authentication and welcome screens are important moments in the user’s initial experience of the product, because we want to move the user from signing up or — if they already have an account on the <a href="https://hellosign.com">HelloSign website</a> — signing in to creating documents. <strong>The app was designed to complement the website</strong>, with the understanding that users would already be somewhat familiar with the product and would likely have a user name. Had this been designed as a standalone app, authentication would have been a secondary option, rather than a requirement.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/47994cdc-70dc-4975-bee7-65234fb16af6/10-final-opt.png"><img loading="lazy" decoding="async" class="139315" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3cd8d17c-e85b-4496-a2a4-0115cf2a0d40/10-final-500-opt.png" alt="" width="500" height="303" /></a><br>
<em>The original versions of the sign-in, sign-up and welcome screens.</em>

### Document Creation

The document creation process consists, in essence, of a camera, with guides to position the document in the frame. In designing this process, we looked to the camera screens of the iPhone’s native Camera app and of Instagram, as well as to the framing markers found in products such as Schwab’s app for depositing checks and Card.io’s app for scanning credit cards.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fd6a7be8-1139-4ad5-8b23-7e0eb42585c2/13-creation-opt.png"><img loading="lazy" decoding="async" class="139550" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fd6a7be8-1139-4ad5-8b23-7e0eb42585c2/13-creation-opt.png" alt="Document Creation" width="384" height="350" /></a><br>
<em>The final document creation screens.</em>

### Document Editing

After creating a document, the user is presented with the editing screen. Here, they can modify the document by adding signatures, text, checkboxes and date stamps.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5d9f7e0e-fca2-4dfa-a76d-4fc568ab1ecc/14-editor-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5d9f7e0e-fca2-4dfa-a76d-4fc568ab1ecc/14-editor-opt.png" alt="Document Editor" width="384" height="350" /></a><br>
<em>The final document editing screens.</em>

## User Testing

A few months after the initial version landed in the App Store, I was given an opportunity to iterate on the app. Before beginning, I decided to run a user test to better understand what in the app was effective and what could be improved.

While several user-testing services are available, such as <a href="https://verifyapp.com/">Verify</a> and <a href="https://www.utest.com/">uTest</a>, I decided on <a href="https://usertesting.com">UserTesting.com</a> because of the quality and value that you get for the relatively inexpensive price. Different testing services offer different benefits, features and options; <a href="https://www.smashingmagazine.com/2011/10/20/comprehensive-review-usability-user-experience-testing-tools/">review them</a> for yourself, and select the one that best fits your goals and needs. With UserTesting.com, you purchase a package of tests, and <strong>users will record videos</strong> as they go through whatever task you’ve assigned to them. You may also ask several follow-up questions of each user, such as, “What was the most frustrating part of your experience?” Conveniently, UserTesting.com provides four very strong default questions that will suit most tests.

As <a href="https://www.nngroup.com/articles/why-you-only-need-to-test-with-5-users/">explained by Jakob Nielsen</a>, testing interfaces on many users is not necessary in order to identify issues; even three to five users might suffice. Because this app is for on-the-fly document signing, we ran a test that took users through a typical use case: creating, editing and sending a document. Follow-up questions were based on UserTesting.com’s suggestions and queried users on ease of use, areas of difficulty and areas for improvement. You could ask <a href="https://www.smashingmagazine.com/2009/06/29/45-incredibly-useful-web-design-checklists-and-questionnaires/">many different questions</a>. Once the tests were completed, after just a couple of hours, I could immediately identify several issues.

I reviewed each video twice. The first pass was merely to identify any glaring issues and to familiarize myself with the tester’s recording style. On the second pass, I paid closer attention, noting specific problems. During testing, most users won’t articulate problems they’re having, but <strong>the problems will be fairly obvious from their behavior</strong>. A problem is obvious when the user does any of the following:

*   pauses for a few seconds when trying to complete a task,
*   stumbles and has to backtrack in their steps or has to undo an action,
*   expresses audible frustration (a sigh or grumble),
*   takes a longer route to achieve a goal than expected,
*   fails entirely at a task.

While there are certainly many others, these are some of the most common indicators of a problem worth delving into. The more tests you run (with small groups), the more problems you will identify. Running a test after each new design iteration is highly valuable, if you can afford to do so. Some problems might affect only a small percentage of your user base, while others might affect the vast majority. Spend time prioritizing the problems that you identify according to your existing list of features, goals and user requests. Not every problem is worth resolving.</p>

## The Redesign

The goal of HelloSign’s redesign was to identify and fix any major problems for users. As mentioned, one can take forever to resolve every last issue; budget limitations kept our scope small.</p>

### What Did We Learn?

The tests revealed a major problem with the authentication screens. It seemed to be a stumbling block because most users weren’t clear about whether they were in the “sign up” or “sign in” state. Users often tapped back and forth between authentication states before understanding which screen was for signing up and which was for signing in.

We also discovered the following:

*   **Creating pages was too repetitive a process.**.  After taking each photo, the user had to tap “Add page,” take another photo and then repeat. This was tedious, and some testers remarked that the process felt unnecessarily repetitive, while others expressed audible frustration.
*   **Users could not edit a date after adding one.**.  One tester wanted to add a past date to a document. While a “date” object could be added to the document, it showed only the current date (i.e. of creation) and could not be edited. This was confusing and unnecessarily restrictive.
*   **Markers for aligning the document during scanning needed refinement.**.  Users had trouble lining up the document with the boundaries on the camera screen, with some expressing frustration and with many giving up.</p>

### Fixing Authentication

Our most substantial changes were to the authentication process, which was changed almost entirely. Dumping the user right into the sign-up screen, with only a “Sign up” button as a state indicator, proved to be confusing. During testing, most users seemed to expect this screen to let them sign in, not register. The revised screen added a step, forcing the user to <strong>explicitly select “Sign up” or “Sign in,”</strong> making it a conscious decision. An alternative solution could have been to add distinct labeling above the user name and password fields, because users typically read from top to bottom, although I was afraid that wouldn’t entirely resolve the issue.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a8146a9d-4dfc-421a-a82f-fe0114f1a68a/19-final-start-opt.png"><img loading="lazy" decoding="async" class="139547" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/65ce826b-138d-4871-adde-234a8cd47399/19-final-start-500-opt.png" alt="Original vs. New Start Screen" width="500" height="371" /></a><br>
<em>The original (left) and revised (right) welcome screens.</em>

After selecting one of the two options, users were brought to one of two nearly identical screens, the difference being only in the labelling of the button, “Sign up” or “Sign in”. As you can see in the revision, the layout was simplified and Google authentication was added. Despite both screens being the same, <strong>forcing the user to choose a path</strong> cleared up any confusion.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f343cef4-83d4-4489-9128-c25e87d0641d/20-final-signin-opt.png"><img loading="lazy" decoding="async" class="139548" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bd95a792-f6e8-4231-a63e-2e8383525a0d/20-final-signin-500-opt.png" alt="Original vs. New Sign In Screen" width="500" height="371" /></a><br>
<em>The original (left) and revised (right) sign-in screens.</em>

Lastly, the home screen was heavily revised. While certainly clear before, it de-emphasized “Help” far too much and generally felt clunky and heavy-handed. The revision brought “Help” to the forefront and <strong>highlighted the “Scan” action</strong>, scanning being the primary purpose of the app.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e525f337-a6cd-4033-94ae-75b27b005a28/21-final-home-opt.png"><img loading="lazy" decoding="async" class="139549" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/778bfdba-d00a-438a-b84e-4afa7487d33c/21-final-home-500-opt.png" alt="Original versus final home screen" width="500" height="371" /></a><br>
<em>The original (left) and revised (right) home screens.</em>

## The Takeaway

Design is a highly iterative process, and all of the intuition in the world won’t help you to identify gaps in your product. As designers, <strong>we’re just too familiar with our own work</strong> to be able to easily spot where it fails. The only way to truly improve a design is to test it on real users and watch how they interact with it. Testing with a live app uncovered problems that led us to turn a four-star effort into a five-star product, with only a little work.

There are many ways to test a app, at an array of price points. It could be as simple as sitting down with a few friends and having each of them use your app for a few minutes, or as complex as hiring a moderator to bring in a variety of users to your office. There is also <a href="https://www.wired.com/wiredenterprise/2013/11/leanplum/">A/B testing</a>, which can — and probably should — be done in conjunction with user testing. While user testing is great for big updates and for identifying major problems, A/B testing, which is less costly, is great for continually testing new ideas and underlying assumptions.

Remote services are inexpensive, and they structure the tests for you and free you from having to hunt down users. No matter how tight your budget or how simple the app, <strong>testing your design on real users is always worthwhile</strong> and will help you better understand where the product can be improved.

{{< signature "al, ea" >}}

