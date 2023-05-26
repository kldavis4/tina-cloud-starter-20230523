---
title: 'Things To Expect From A Smashing Workshop: Form Design Masterclass'
slug: smashing-workshop-form-design-masterclass
author: adam-silver
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1b425dc9-02b3-4a73-907c-cc96f5a83489/poster-form-design-masterclass-preview.png
date: 2021-02-15T12:00:00.000Z
summary: >-
  A couple of weeks ago, we organized a [Form Design Masterclass](https://smashingconf.com/online-workshops/workshops/adam-silver), an online workshop with Adam Silver alongside 81 friendly and smart people. Today, Adam shares his experience and details by highlighting what you as an attendee can expect from a <a href="https://smashingconf.com/online-workshops/">Smashing Workshop</a>, and things to keep in mind when running one.
description: >-
  A couple of weeks ago, we organized a [Form Design Masterclass](https://smashingconf.com/online-workshops/workshops/adam-silver), an online workshop with Adam Silver alongside 81 friendly and smart people. Today, Adam shares his experience and details by highlighting what you as an attendee can expect from a <a href="https://smashingconf.com/online-workshops/">Smashing Workshop</a>, and things to keep in mind when running one.
categories:
  - SmashingConf
  - Workshops
disable_ads: true
disable_panels: true
disable_newsletterbox: true
---

It took me around six months on and off to write the content for the workshop. After a lot of deliberation, I decided to structure it like I do in my book, [Form Design Patterns](https://www.smashingmagazine.com/printed-books/form-design-patterns/).

It was a 4-day workshop split into two 45-minute segments, with 15-minute breaks followed by a 30-minute Q&amp;A with optional homework between days. Each day we set out to solve one big problem. This provided a way to approach the problem like we do in real life: by analyzing and discussing the options before arriving at a good solution.

Overall, it was a fun experience. I learned a lot and had a great time teaching and chatting with everyone. I’m already looking forward to the next one which is tentatively planned for late 2021.

<style>
  ol.start {
      counter-reset: perfcounter;
  }
  ol.start > li:before, ol.continue > li:before {
      content: counters(perfcounter, '.', decimal-leading-zero);
      counter-increment: perfcounter;
  }
</style>

## Some Of The Highlights Of Each Day

Here’s a quick rundown of each day including some of the highlights.

### Day 1: Nailing The Basics Of Form Design

On the first day, we designed a simple registration form from scratch. This provided a perfect way to nail the basics of form design. It covered things like **label positioning**, form styling and input types. At the end of day 1, we had ourselves a registration form that covered the basics and made the form as simple as possible for users.

My highlight of this session was the **question protocol** exercise. Instead of focusing on how to artificially save space on forms (by using things like float labels, tooltips, left-aligned labels and placeholder text), we used a spreadsheet to help know why every question is being asked and the best way to elicit the answer.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7e6dd98c-2cae-430a-8ad7-56eb8c2fe86b/question-protocol-form-design-masterclass.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7e6dd98c-2cae-430a-8ad7-56eb8c2fe86b/question-protocol-form-design-masterclass.png" width="800" height="450" sizes="100vw" caption="The question protocol spreadsheet to understand why every question is being asked and the best way to elicit the answer (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7e6dd98c-2cae-430a-8ad7-56eb8c2fe86b/question-protocol-form-design-masterclass.png'>Large preview</a>)" alt="Question protocol spreadsheet" >}}

For our registration form, this meant a thorough analysis of asking for someone’s name, email address and password. And by the end of the exercise we had halved the number of form fields and had clear justification for the ones that remained.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b7caecf4-b802-462a-a5db-f699eb0993f5/registration-form-before-after-form-design-masterclass.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b7caecf4-b802-462a-a5db-f699eb0993f5/registration-form-before-after-form-design-masterclass.png" width="800" height="486" sizes="100vw" caption="Registration form: before and after applying a question protocol (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b7caecf4-b802-462a-a5db-f699eb0993f5/registration-form-before-after-form-design-masterclass.png'>Large preview</a>)" alt="Registration form: before and after applying a question protocol" >}}

### Day 2: Form Validation And Writing Good Error Messages

On the second day, we took our well-designed registration form and looked at how to help users recover from errors in two ways:

1. We decided when to validate forms and how to display error messages;
2. We learnt how to write clear, concise, consistent and specific error messages that help users get back on track quickly.

My highlight of this session was the exercise to **redesign the error messages** on Smashing Magazine’s very own membership sign up form.

[Sophy Colbert](https://twitter.com/sophycolbert), a content designer who attended the workshop, volunteered to share her new error messages explaining her rationale for each one.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a8661ae5-81f9-44be-ba3f-01e04e79a88d/sophy-colbert-error-messages-form-design-masterclass.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a8661ae5-81f9-44be-ba3f-01e04e79a88d/sophy-colbert-error-messages-form-design-masterclass.png" width="800" height="450" sizes="100vw" caption="Sophy Colbert running through her improved error messages (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a8661ae5-81f9-44be-ba3f-01e04e79a88d/sophy-colbert-error-messages-form-design-masterclass.png'>Large preview</a>)" alt="Sophy Colbert running through her improved error messages" >}}

Both the messages and the rationale were superb, and I think the group got a lot out of it as they could get an insight into Sophy’s content designer mindset.

### Day 3: Redesigning A Real World Checkout Form

On day 3, we redesigned the ASOS checkout flow from scratch. This included guest checkout (first time experience) and checking out as someone with an account (repeat-use experience). We covered a lot of ground such as whether to use tabs, accordions or radio buttons. And we also looked at single page checkouts versus multi-page checkouts.

My highlight of this session was that the process of **redesigning several interactions**, exposed new content design and service design challenges. For example, we converted the tabs that ask the user to specify whether they have an account or not:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7b4cf5a7-d93d-4db5-903b-63cc9991e494/asos-tabs-form-design-masterclass.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7b4cf5a7-d93d-4db5-903b-63cc9991e494/asos-tabs-form-design-masterclass.png" width="800" height="386" sizes="100vw" caption="Original design of ASOS page using tabs to let users switch between ‘New to ASOS?’ and ‘Already registered?’ options (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7b4cf5a7-d93d-4db5-903b-63cc9991e494/asos-tabs-form-design-masterclass.png'>Large preview</a>)" alt="Original design of ASOS page using tabs to let users switch between ‘New to ASOS?’ and ‘Already registered?’ options" >}}

And we redesigned them into a form with radio buttons:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/01f1336d-c8c6-4a30-8f70-e50a985de5f4/asos-radios-form-design-masterclass.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/01f1336d-c8c6-4a30-8f70-e50a985de5f4/asos-radios-form-design-masterclass.png" width="800" height="292" sizes="100vw" caption="New design of ASOS page using radio buttons to let users choose whether they have an account or not (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/01f1336d-c8c6-4a30-8f70-e50a985de5f4/asos-radios-form-design-masterclass.png'>Large preview</a>)" alt="New design of ASOS page using radio buttons to let users choose whether they have an account or not" >}}

And this exposed the problem that in real life, choices are rarely binary. So I asked the group what the missing option was and they rightly said: ‘What if the user can’t remember?’

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fd58abb7-37ad-4470-8b2c-28a931ed786d/asos-cant-remember-form-design-masterclass.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fd58abb7-37ad-4470-8b2c-28a931ed786d/asos-cant-remember-form-design-masterclass.png" width="800" height="292" sizes="100vw" caption="New design of ASOS page with the added option of ‘Can’t remember’ to the question ‘Do you have an account or not?’ (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fd58abb7-37ad-4470-8b2c-28a931ed786d/asos-cant-remember-form-design-masterclass.png'>Large preview</a>)" alt="New design of ASOS page with the added option of ‘Can’t remember’ to the question ‘Do you have an account or not?’" >}}

So even though we originally looked at this primarily as an interaction design problem, it became an issue of content and service design.

All of these problems nicely encapsulated one of the form UX rules: ‘Make friends with other departments’. As designers, we have to work effectively with stakeholders across the organisation to make sure we avoid as much complexity as possible. And this again is where the question protocol really shines.

### Day 4: Using Shorthand Syntax And Designing Long And Complex Forms

Day 4 was split into two parts which I’ll discuss in reverse order.

In the second part, we looked at various patterns that help users fill out long and **complex forms** &mdash; the kind of forms that take days, weeks or even months to complete. I was really looking forward to running this because the design challenges around this are interesting and not well trodden.

In the first part, we redesigned Smashing Magazine’s registration form using shorthand syntax.

**My highlight of this session** was that Vitaly, Mr. Smashing Magazine himself, came along to be our business stakeholder. The group asked him questions to work out why the form was designed the way it was and asking why certain questions were asked.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e9fab25b-a340-4137-a836-6bf86b94ba4d/smashing-form-design-masterclass.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e9fab25b-a340-4137-a836-6bf86b94ba4d/smashing-form-design-masterclass.png" width="800" height="450" sizes="100vw" caption="The Smashing Magazine membership registration form (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e9fab25b-a340-4137-a836-6bf86b94ba4d/smashing-form-design-masterclass.png'>Large preview</a>)" alt="The Smashing Magazine membership registration form" >}}

Here are a few examples:

*   [Sophy O](https://github.com/sssoz) asked why the **country field** is being asked for. Vitaly said that it depends on what the user is doing. If the user is buying a book, we need to know where it’s going. And the taxes on the book are based on the destination country. This resulted in either removing the field and asking for this information when someone buys the book &mdash; or just being clearer in hint text about why we’re asking for this information.
*   [Milos Lazarevic](https://www.nishville.com/) questioned the need for the ‘Do you like cats?’ checkbox. And Dana Cottreau and [Jaclyn Ziegler](https://jaclynziegler.com/) enjoyed the **playfulness of the checkbox**. But I would weigh up the joy it brings some people against the risk of alienating people who are, for example, less digitally savvy or are simply in a rush to access the content.
*   [Emma Stotz](https://github.com/emmastotz) questioned the use of **live validation** given all the [usability issues](https://adamsilver.io/blog/live-validation-is-problematic/) that pop up around that. And Vitaly was keen to explore instantly validating the fields on submit instead.

## My Overall Impression

For me, the workshop went very well overall and I was chuffed with the way things went and the feedback I received from the attendees. Everyone was so friendly, and tolerant of a couple of technical difficulties I had on the first day (*thanks again, everyone!*). Running the workshop remotely over Zoom has its problems (we won’t talk about how I accidentally left the meeting in a panic by accident on day 1), but actually I found the **remote aspect** useful on the whole.

For example, all being connected to Zoom, meant it was seamless for attendees to ask questions while **sharing their screen** to bring the problems to life.

I also really enjoyed **meeting people** across the world, something that would have been difficult with in-person workshops I think. Also, during the break, I got to quickly dash to put my kids to bed, so I imagine that also worked well for the attendees, too.

But there’s one thing I wish I knew earlier. I was worried, that with such a large group of people (81 to be exact), letting people talk freely would end up in a chaos. As a result, on day 1, I read out and answered group's questions from the shared Google Doc during the Q&amp;A. This meant that other people’s voices weren’t heard and there was more of a barrier between me and the group.

This is something I rectified for day 2 and it really made a difference. It was nice to **hear people’s voices** and thoughts in their own words and it created more of an open dialogue where other people started to answer other people’s questions which I loved.

I remember Alex Price jumping in once to talk about his experience in dealing with a complicated form that needed to be completed by different people.

## What I’ll Change For Next Time

While my overall impression of the workshop was very positive, there were some things I’d look to improve for next time.

### 1. Show The Basics, Not Learn The Basics

Day 1 covered a lot of the basics before going into greater detail on the following days, but it bothered me a bit to teach some of these things as I thought many attendees knew a lot of this stuff already. So next time I'd like to acknowledge that some people have come with a lot of knowledge and set the scene as ‘this is how I teach the basics’ as opposed to ‘this is how to learn the basics’ &mdash; thanks to [Caroline Jarrett](https://twitter.com/cjforms) for this tip.

Also, I’ll probably ask the group if there’s any form design approach that they’ve **struggled to convince** teammates about as that’s certainly something I’ve struggled with before.

### 2. Split People Up In Bigger Groups

One of the exercises involved people splitting up into groups of 2 using the Zoom breakout rooms, but because people came to this workshop from all over the world, some of the people listening were not able to take part in the exercises.

For example, some people really needed to take a lunch break because their time zone was ahead of mine. This meant one or two people who did want to participate found themselves in a group on their own. Next time, I’d put people into groups of say 4 and make sure the exercises still work.

### 3. Add More Group Exercises

Despite the issue I just mentioned, the **group exercises** worked well. People enjoyed them, and it sparked some really interesting ideas from the participants. Some people messaged me after saying that they wished there were more group exercises, so I’ll aim to do just that.

## A Poster Of All The Rules

As we moved through the workshop, we ticked off over **40 rules and principles of form design** which brought a nice additional structure to the sessions.

A few of the attendees asked me if I had a poster of all the rules and I didn’t &mdash; so now I’ve made one.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/19a44f71-893f-4af0-a6b2-56139b720e7f/poster-form-design-masterclass.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/19a44f71-893f-4af0-a6b2-56139b720e7f/poster-form-design-masterclass.png" width="800" height="1132" sizes="100vw" caption="All 42 rules from the workshop captured in a handy poster. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/19a44f71-893f-4af0-a6b2-56139b720e7f/poster-form-design-masterclass.png'>Download the poster</a>)" alt="All 42 rules from the workshop captured in a handy poster" >}}

## Form Design Masterclass Poster (Plain Text Version)

For your convience, here’s a simple text version of the poster &mdash; feel free to adjust it and customize it to your needs.

### Day 1: Nailing The Basics Of Form Design

<ol class="start">
<li>Make forms work well for everyone</li>
<li>Every form control needs a label</li>
<li>Only add hint text if it adds value</li>
<li>Don’t use placeholder text</li>
<li>Put hint text between the label and the input</li>
<li>Put labels above the input</li>
<li>Don’t use tooltips for hint text</li>
<li>Know why you’re asking every question<sup>*</sup></li>
<li>Give text boxes a distinct border</li>
<li>Position labels to be associated with the input</li>
<li>Give inputs a clear focus state</li>
<li>Use the right input type for the job</li>
<li>Align the button to the left edge of the inputs</li>
<li>Label the button with exactly what it does</li>
<li>Make sure your form is actually necessary</li>
<li>Avoid putting two forms on one page</li>
<li>Use multiple inputs as a last resort</li>
<li>Don’t use input masks</li>
</ol>

### Day 2: Validating Forms And Writing Good Error Messages

<ol class="continue">
<li>Don’t disable the submit button</li>
<li>Don’t trigger errors when the user is answering</li>
<li>Only validate when the user submits</li>
<li>Put errors above the input</li>
<li>Forgive trivial mistakes</li>
<li>Track your errors</li>
<li>Give users clear, concise and specific errors</li>
</ol>

### Day 3: Redesigning A Real Checkout Flow

<ol class="continue">
<li>Postpone questions you could ask later<sup>**</sup></li>
<li>Use form controls inside forms</li>
<li>Start without a progress bar<sup>*</sup></li>
<li>Begin prototyping with one thing per page<sup>**</sup></li>
<li>Ask questions in a sensible order</li>
<li>Use select boxes as a last resort</li>
<li>Use sensible defaults</li>
<li>Provide help in context of the question</li>
<li>Avoid optional fields wherever possible</li>
<li>Don’t hide the submit button</li>
<li>Make the field width match the expected value</li>
<li>Let users check their answers</li>
<li>Put the back link at the top left of the form</li>
<li>Make friends with other departments</li>
</ol>

### Day 4: Using Shorthand And Designing Long And Complex Forms

<ol class="continue">
<li>Break down huge forms into small tasks</li>
<li>Tell users what they need before they start</li>
<li>Help users check their eligibility</li>
</ol>

<p><em><sup>*</sup> This principle is from the <a href="https://www.gov.uk/service-manual">GOV.UK Service Manual</a></em><br /><em><sup>**</sup> This principle is from the NHS Service Manual.</em></p>

Thanks again to everyone who came for all their contributions. I’m looking forward to the next one.

*Thanks to [Caroline Jarrett](https://twitter.com/cjforms) for not only reviewing every detail of my workshop but for also editing this article.*

<hr />

<p><em>Editor’s Note</em>: You can also check a detailed overview of <a href="https://www.smashingmagazine.com/2020/10/how-we-run-smashing-online-workshops/">How We Run Smashing Online Workshops</a>, and if you are interested in attending one, we have plenty of <a href="https://smashingconf.com/online-workshops/">online workshops on front-end &amp; UX</a> coming up soon. We’d love to see you there!</p>

{{< signature "vf, il" >}}
