---
title: How We Started Releasing Features Twice As Fast (Case Study)
slug: how-we-started-releasing-features-twice-as-fast-a-case-study
image: 'https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5762f434-12a8-4503-9b24-5e052337e9cc/bughunt-opt.png'
date: 2016-07-12T18:57:32.000Z
author: vanyamimic
description: >-
  When businesses rely on your app for their day-to-day work, you have to be
  agile enough to quickly address their needs. If you don’t, others definitely
  will. In the unforgiving world of SaaS, delaying a critical feature (or
  rushing a bug-ridden piece of code) will mean losing clients. A solid agile
  workflow can make all the difference.
categories:
  - Business
  - Workflow
  - Strategy
---
When businesses rely on your app for their day-to-day work, you have to be agile enough to quickly address their needs. If you don’t, others definitely will. In the unforgiving world of SaaS, delaying a critical feature (or rushing a bug-ridden piece of code) will mean losing clients. A <strong>solid agile workflow</strong> can make all the difference.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/83125e84-272e-45b5-8362-fea9779a69a5/process-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/20755174-a4e4-4f6a-b93f-9a5fcda7f56f/process-opt.png" alt="Agile development process" /></a><figcaption>The development cycle, the core of any agile approach, is constantly being revised and improved. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/83125e84-272e-45b5-8362-fea9779a69a5/process-large-opt.png">View large version</a>)</figcaption></figure>

We’re the team behind <em>Active Collab</em>, a project-management app with an ever-growing set of features and a sizeable user base. This means that even the smallest change in functionality will affect a large number of people.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [How To Roll Out New Features Without Hurting Loyal Users](https://www.smashingmagazine.com/2016/06/rolling-features-without-hurting-loyal-users/)
*   [The Website Launch Checklist – 15 Essential Checks Before You Go Live](https://www.smashingmagazine.com/2009/04/15-essential-checks-before-launching-your-website/)
*   [A User-Centered Approach To Web Design For Mobile Devices](https://www.smashingmagazine.com/2011/05/a-user-centered-approach-to-web-design-for-mobile-devices/)
*   [How To Launch Anything](https://www.smashingmagazine.com/2013/06/how-to-launch-anything/)

{{% feature-panel %}}

Therefore, the development process needs to run smoothly and up to a standard, with delays reduced to a bare minimum. Before any change makes its way to the end user, it goes through five crucial phases: <strong>feedback, design, development, quality assurance and deployment</strong>. In this article, I will share what we’ve learned (the hard way) about each of the stages from over eight years in the business.</p>

## A Wake-Up Call

Before I get into the details, let’s look at how this all came about. After years of adding features without enough scrutiny, our app was suffering from feature bloat. We’ve added so much functionality over the years that new users were intimidated by the sheer complexity of the UI (never to return again). We knew we had to rebuild from the ground up, even if that meant rewriting every single feature from scratch.

Then came the delays. The features for new versions were constantly lagging behind schedule. For example, a junior developer was supposed to develop an integration with QuickBooks. We didn’t accurately predict the complexity, skills or knowledge needed. Plus, he was the only one assigned to that task, and no one could quickly jump in to help him out. As a result, what was supposed to be a two-week job ended up taking five. Those were a few red flags.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d5d7fe3a-5596-4dc6-9c06-72e8ad7da7ff/deadlines-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/02a7f1c1-44e4-4295-9ae0-a9584e83568e/deadlines-opt.png" alt="Deadline" /></a><figcaption>Missed deadlines can have severe implications. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d5d7fe3a-5596-4dc6-9c06-72e8ad7da7ff/deadlines-large-opt.png">View large version</a>)</figcaption></figure>

It was clearly time to switch to a more agile approach. We took what we liked from various agile (and not so agile) methods, combined it with experience, and came up with our own version, which has been delivering great results ever since.

Let’s take a closer look at the road that a feature must travel before it’s offered to the end user.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0088959c-b9ef-4f1b-8dad-3d4faf97bc6c/process2-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cffcec11-8e1e-4741-8dc1-3d5772612356/process2-opt.png" alt="Feedback-Decision-Design-Development-Testing-Release" /></a><figcaption>To ensure quality, a new feature is introduced only after it has gone though all of these stages. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0088959c-b9ef-4f1b-8dad-3d4faf97bc6c/process2-large-opt.png">View large version</a>)</figcaption></figure>

## From Suggestion To Feature

In our workflow, a new feature starts taking shape long before it reaches the development team, and it’s usually born of user feedback. This is no coincidence — we used to release features no one needed, usually just because one user was particularly loud or we simply thought something would be great to have. Instead of imagining what features our users might need, we now make decisions based on actual demand.

If you’re into lean manufacturing, you’d say that our <strong>customers “pull” certain features</strong> by requesting them more often than others. Our support and sales teams are a big part of the process because they’re constantly in touch with users who share their needs and ideas.

Based on the feedback, our teams update a form that looks like this:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/94404e13-4185-4227-9010-4fc046d43498/feedback-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7dba1f8b-b87c-46c9-9113-ba122e72943d/feedback-opt.png" alt="Feedback form" /></a><figcaption>Feedback collected and saved using this form is essential for deciding which features make their way onto the road map. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/94404e13-4185-4227-9010-4fc046d43498/feedback-large-opt.png">View large version</a>)</figcaption></figure>

When we don’t have all of the information we need, we’ll reach out to customers directly. This is usually done with targeted surveys on a carefully selected sample. The point is that we listen. No feedback is lost on us. It’s always acknowledged and documented.

The next step is analysis. We tally the scores each month to see which feature got the most votes. Also, with proper categorization, we get a broader perspective on which parts of our software need work. For example, if the calendar is getting many complaints, we’ll consider revamping the entire section, rather than introducing the feature that got the most votes (such as calendar exporting).

However, even when the results are in, the decision to introduce a feature isn’t final. Before it makes it onto our to-do list, we always do a thorough sanity check:

*   What benefits will this feature bring to users?
*   Does it fit our product philosophy?
*   Will it add unnecessary complexity?
*   Does it blend in nicely with the existing interface and functionality?
*   Do we have the resources to deliver it in a reasonable timeframe?

When a feature passes the checklist and the product owners approve it, it’s time to go to the drawing board.</p>

## Designing For The User

Experience has taught us that adding a new feature doesn’t just mean sticking it on top of the UI — you have to blend it with the existing design, with the user in mind. If you don’t do this, you’ll soon end up with an app so complex that only a brave few will make it through the first five minutes of the trial (yes, we’ve been there). Aesthetics are also important for a good first impression, but our <strong>main concern is ease of use</strong>. A feature needs to be added in a way that feels natural to the user.

We keep things in perspective by asking, Where would the user expect this option to be?

For existing users, it’s important that the new design follows the patterns they’re familiar with and <a href="https://www.smashingmagazine.com/2016/06/rolling-features-without-hurting-loyal-users/">doesn’t disrupt their workflow</a>. Also, there are industry standards and conventions that we’re all (unconsciously) used to. Never expect your users to change their habits completely. They’ll more likely look elsewhere if the interface is not intuitive.

Take keyboard shortcuts. You could make your own set of shortcuts and expect users to learn them (they probably won’t). Or you could add ones that people already use. A lot of our users already use Slack, for example, so we added a shortcut they are already familiar with (<code>Command + K</code> for quick jumps works in <em>Active Collab</em> as well).</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ad0dbe0c-482d-40aa-96c1-14736163a08f/quickjump-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0bc3a2d7-bd1f-4792-8194-ebb0835af540/quickjump-opt.png" alt="Quick jump window in Active Collab" /></a><figcaption>Command + K opens this window, which enables a user to quickly jump to a page in Active Collab. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ad0dbe0c-482d-40aa-96c1-14736163a08f/quickjump-large-opt.png">View large version</a>)</figcaption></figure>

When the user flows are in place, our UX designer mocks up the design in Sketch. We rarely use HTML in the early stages. Well-thought-out Sketch visualizations give us enough flexibility that we don’t have to do any backtracking when we start coding. The initial design usually ends up matching about 80% of the final product. The rest is added and adjusted along the way.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/83c0a9d4-d32f-4852-ac42-6975c822f47f/design-mockups-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/12943143-1bd6-4d95-96b7-950b12c73855/design-mockups-opt.png" alt="Feature design mockups" /></a><figcaption>Initial design mockups are the basis for further development. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/83c0a9d4-d32f-4852-ac42-6975c822f47f/design-mockups-large-opt.png">View large version</a>)</figcaption></figure>

Another important step of the design process is copy. Our copywriters devote a great deal of attention to every single word. We even have our own style guide, to sound as approachable and to be as easy to understand as possible. For example, saying “security certificate” instead of “SSL certificate” conveys in layman’s terms something an average user might not be familiar with.

When all this is done, the feature is assigned to a development team. The team is made up of a project manager, a lead developer and a number of back- and front-end developers, depending on the workload. The project manager makes sure everything runs smoothly and on schedule, while the lead developer takes care of the technical side of things. They also coordinate and mentor junior developers.

## Time To Kick Things Off

Our kickoff meetings aren’t boring motivational get-togethers. They are opportunities for a development team (consisting of junior and senior developers) to meet with the project manager and product owner.

Instead of allowing empty monologues, we focus on putting everyone’s words into actionable tasks. Throughout the day, <strong>three important meetings</strong> take place:

*   The product owner presents the given feature to the team, the ideas behind it, the initial designs and the expected results.
*   Then, the team has its own meeting in which it discusses the action plan, potential problems and the testing schedule.
*   The final meeting is attended by everyone involved, and the plan takes its final shape. At the end of this meeting, the team gives estimates for demos and a final due date.

Three meetings might sound like a lot for one day, but that’s how we make sure problems are solved early on. Filling in the blanks at this stage saves our developers a lot of time, false starts and backtracking. The meetings also encourage teamwork and make everyone feel that their contributions are welcomed.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/354218a8-49c3-460a-8934-c4accf0252ad/kickoff-meeting-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c3ff5fa6-27c1-4170-993f-70ebfc77a2c9/kickoff-meeting-opt.png" alt="Team meeting" /></a><figcaption>Teams spend as much time as they need discussing all aspects of the work ahead.</figcaption></figure>

After the meetings, the team will have all of the necessary information:

1.  **What?** This is the **scope of the feature** and includes everything that needs to get done, as well as potential blockers and bottlenecks. We try to anticipate as many scenarios and edge cases as possible. Predicting all of them is not easy; they often come up as we go.
2.  **Why?** The product owner estimates the **business value** of a feature and explains why it’s worth the effort. This way, the team gets a clear picture of the benefits to customers and the product. The prime motivator here is that everyone should understand why their work matters and how it contributes to the company as a whole.
3.  **How?** By outlining the **steps required to complete a feature**, we make sure our developers never lose their compass. We also set realistic expectations by adding a complexity tag. We went with t-shirt sizes — S can be solved within a few hours, while XXL takes weeks or more to complete.
4.  **Who?** The **team lead is responsible** for finishing a feature or task on time and for updating the product owner on the progress. Other team members are assigned to their own set of subtasks, so that it’s perfectly clear who is accountable for what. Keeping this as transparent as possible helps us to see whether someone is struggling or causing delays.
5.  **When?** With everything taken into account, a **due date is estimated**. If a task is delayed, we analyze the reasons and use that experience the next time. That way, a missed deadline becomes a learning opportunity and not a source of stress.

Kickoff day can get hectic, but it’s also very fruitful. Everyone pitches in with ideas and comments. A task transforms from an empty slate to a hub for comments, edits and updates. By the end of the day, the development team has a clear picture of the work ahead and solid ground to build upon.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/65e2a147-cd30-4c5a-b1b3-6dae8a62b600/task-view-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/33123fda-aaac-4834-8b6c-1b49f2061da3/task-view-opt.png" alt="A task in Active Collab" /></a><figcaption>All important information is available in the task item. This is also where team members communicate and post updates on their progress. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/65e2a147-cd30-4c5a-b1b3-6dae8a62b600/task-view-large-opt.png">View large version</a>)</figcaption></figure>

We go through this checklist before beginning work:

*   feature explained,
*   steps for completion outlined,
*   business value assigned by product owner,
*   complexity assigned by team,
*   feature and bug dependencies identified,
*   performance criteria identified (if needed),
*   demos scheduled,
*   start and end dates set by team leader.

This is the moment when a task moves to the “In progress” column.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ab8d9624-e548-499e-8670-47d094b3d2bd/in-progress-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/edd048ff-e961-4a55-9d41-0aa14df3a664/in-progress-opt.png" alt="Task moved to In Progress column" /></a><figcaption>When a feature is kicked off, the task moves into the “In Progress” column. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ab8d9624-e548-499e-8670-47d094b3d2bd/in-progress-large-opt.png">View large version</a>)</figcaption></figure>

It’s coding time!

## Teamwork On Display

Our developers never work alone — it’s always a team effort, and it’s by far the most efficient way to release new features. Before teams were introduced, a (junior) developer would get stuck with a problem and might have gone round in circles for days (without anyone realizing it). Or, if they weren’t the lone-ranger type, they’d constantly be distracting colleagues and managers.

On the other hand, with teams, we mix people with different skill sets and levels of experience. This means that everyone is assigned a set of tasks appropriate to their level. Plus, seniors get the benefit of learning how to manage and coach junior teammates — and juniors get to ask for help. Because it’s a team effort and everyone is working towards the same goal, questions aren’t regarded as distractions, and the team can tackle any issue much more efficiently. The team becomes a self-organizing entity, splitting work into phases (or sprints) and presenting their work during demos.</p>

## Show And Tell

According to the schedule, the team will demo for the product owner. The purpose of the demos is to show how well a feature is performing in its current state and where it needs more polish. It’s a reality check that doesn’t allow for excuses like, “It just needs a few finishing touches” (touches that would take another month). Also, if things start to take a wrong turn, product owners get to react quickly.</p>

## Weekly Meetings

We started off with regular short daily meetings attended by all developers. Each developer would briefly describe what they were working on, their problems, their blockers and whether they needed help. It soon became obvious that these meetings needed to be more focused and to provide tangible results. So, we switched to having meetings with individual teams about once a week. This is how the product owners and project manager are kept in the loop and all potential problems are dealt with on the spot.</p>

## Putting It To The Test

The code is written, the demos have been successful, everything seems to be wrapping up nicely… until you release the feature and see that the app crashes. That’s why <strong>every feature we make goes through quality assurance</strong> (Q/A). Always. Our tester meticulously goes through every possible scenario, checking all options and running tests in different environments. A feature rarely passes Q/A on the first go.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6b58667b-b1ea-4305-93e2-372c1ec33502/qa-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/16ea3ab8-2493-47c5-bf40-a7ae10c9c6fd/qa-opt.png" alt="Searching for bugs" /></a><figcaption>Q/A makes sure no bug slips through. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6b58667b-b1ea-4305-93e2-372c1ec33502/qa-large-opt.png">View large version</a>)</figcaption></figure>

To increase productivity, we used to let developers start on new features during this phase, but that just resulted in a lot of delayed, half-finished features. So, now the development team keeps busy by working on small maintenance tasks while their feature is being reviewed. If Q/A finds a problem, the developers immediately fix it and resubmit. The process is repeated until the feature passes Q/A and moves on to code review.

This is when a senior developer makes sure the code is written according to our standards. One final step before the release is writing the documentation — you don’t want to get swamped by support emails after releasing a feature that no one knows how to use. Our copywriters also update the release notes and write marketing materials, such as email announcements and blog posts.

Here’s our definition of “done”:

*   auto-tests written,
*   Q/A done and all resulting tasks completed,
*   code review done and code merged to master,
*   release notes updated,
*   feature and bug dependencies identified.

The task has reached the final stage, called “Release Q.”

## Release Day

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4dd64e9d-0568-4fc2-998d-107497fb6779/release-day-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c3ff2d96-de3a-4b34-b3b7-26dbc6e8941c/release-day-opt.png" alt="Release day: Tuesday" /></a><figcaption>We aim for a Tuesday release. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4dd64e9d-0568-4fc2-998d-107497fb6779/release-day-large-opt.png">View large version</a>)</figcaption></figure>

When choosing a day for new releases, we immediately decided against Friday and Monday. Friday is not good because any potential issues wouldn’t get resolved until Monday; plus, the support team was already pretty busy then. Monday is not the best time because any major update requires preparation, which would have to be done on the weekend. It’s always good to leave a day for final touch-ups. This narrows down the options to three days — and we went with Tuesday. Here’s why:

*   We have Monday to review the release and add finishing touches before deploying.
*   If there are any untranslated phrases (our web app is available in seven languages), we have enough time to finish the translation.
*   The marketing team has plenty of time to send out newsletters and announcements via social media.
*   We are available to provide upgrade support quickly and efficiently for the rest of the week.
*   If a deadline has passed for whatever reason, we still have Wednesday or Thursday to complete the work.</p>

## Free Activity Day

The day after a major release is a free day for the team. This is when they learn new skills or do anything work-related that they find interesting. Even though everyone’s eager to know which feature we’ll be kicking off the following day, the team doesn’t discuss that just yet. Instead, they’ll relax and maybe watch a presentation about the history of Erlang, or finish reading that article about why <a href="https://www.php-fig.org/psr/psr-7/">PSR-7</a> and middleware are important to modern PHP development, or have their own retrospective discussion. It’s a well-deserved day to recharge their battery and celebrate a job well done.</p>

## Bug Hunt Day

Apart from developing major new features, there is always work to be done on existing ones. Whether it’s a bug fix, a design update or a small change in functionality, the team needs to take care of it in a reasonable time.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b9e61ed7-9c84-4b91-9ead-fb3c72752f6d/bughunt-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5762f434-12a8-4503-9b24-5e052337e9cc/bughunt-opt.png" alt="Hunting bugs" /></a><figcaption>Clearing the backlog of bugs is much faster when a day is dedicated just to that. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b9e61ed7-9c84-4b91-9ead-fb3c72752f6d/bughunt-large-opt.png">View large version</a>)</figcaption></figure>

This is why we have bug-hunting days at least once a month. It’s when all developers stop working on their main projects and turn their attention to maintenance. This focused effort has proven to be a great success. When everyone works solely on bugs on the same day and is available to help each other, the team solves a huge number of issues.</p>

## What Is The Result?

Releasing a big feature now takes about three weeks on average, from the kickoff to development, testing, code review, documentation and final release. A feature of equivalent complexity used to take us 45 days. From our perspective, that’s a <strong>100% increase in productivity</strong>. We accomplished it with the same resources and people, the only difference being an improved workflow.

So, if we have one takeaway for you, it’s this: Nurturing a company culture that eliminates fear of change will make your team better at what it does. Whether you call it Scrum, Kanban or Lean doesn’t matter, as long as it helps your company grow. Experimentation and innovation lie at the heart of any agile approach. Don’t be afraid to test different solutions, measure results and, based on the results, modify existing practices. Good results will follow.

{{< signature "ms, vf, al, il" >}}

