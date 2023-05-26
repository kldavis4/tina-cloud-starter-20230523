---
title: 'Adapting Agile For Part-Time Teams'
slug: adapting-agile-part-time-teams
author: philip-kiely
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4e97d18f-57a9-4da2-a6ee-7605dfb7d8ef/adapting-agile-part-time-teams.png
date: 2019-11-12T12:00:00.000Z
summary: >-
  Agile has had a long time to infiltrate software development. While the methodology advocates for "co-located, dedicated teams," in its ubiquity Agile is frequently applied to teams partially or fully composed of part-time workers. While there are lessons to be taken from the practice, Agile must be adapted to support, rather than hinder, part-time teams.
description: >-
  Agile has had a long time to infiltrate software development. While the methodology advocates for "co-located, dedicated teams," in its ubiquity Agile is frequently applied to teams partially or fully composed of part-time workers. While there are lessons to be taken from the practice, Agile must be adapted to support, rather than hinder, part-time teams.
categories:
  - Workflow
  - Business
  - Teams
  - Communication
---
The formal notion of the Agile software development method is about as old as I am (the Agile Manifesto was published in February 2001). I point this out not to [make you feel old](https://xkcd.com/1686/), but instead to demonstrate that Agile has had a long time to infiltrate software development. While the methodology advocates for "co-located, dedicated teams," in its ubiquity Agile is frequently applied to teams partially or fully composed of part-time workers. While there are lessons to be taken from the practice, Agile must be adapted to support, rather than hinder, part-time teams.

In this article, we’ll consider applying Agile to a team of 5-10 people each working 20 hours per week on a project. We’ll further consider the frequent intersection of remote work with part-time teams and discuss situations where contributors work as few as 5 hours per week on a project. We’ll also hear from professors Armando Fox at the University of California, Berkeley and Barbara Johnson at Grinnell College with their thoughts on part-time Agile teams.

## Why Does Part-Time Work Happen?

While the "5 developers for 20 hours" example may seem contrived, many situations lead to the scenario. You may have:

- Developers assigned to multiple clients, projects, or teams within a single company,
- A team with contractors or co-op interns,
- Volunteers working on an open-source or community project, or
- An after-hours team working on a startup or product.

While we will examine the many challenges involved in managing teams under these constraints, usually the alternative to working part-time with someone isn’t their full-time efforts, the alternative is not being able to work with them at all. While part-time workers and teams often require extensive compromises, with clear and effective management they can still be a huge net positive to a team and business.

{{% feature-panel %}}

## Tenets Of Agile

Given its prevalence in the software development industry, everyone understands Agile slightly differently. To get through adapting the framework together, we need a shared vocabulary to define "regular" Agile, you know, the kind that advocates for "dedicated, co-located teams." Agile implements practices, rituals, and roles to promote effective work.

Agile, as implemented, involves certain practices:

- "Sprints" are discrete units of time, often 2 weeks, that determine the cycle of work for Agile teams.
- "Stories" or "user stories" are well-scoped units of work that a single team member can complete in some fraction of the sprint.
- Often, teams organize their stories on "kanban boards" or similar methods of tracking story state: to do, in progress, in review, and done in a given sprint.

Agile revolves around four rituals:

1. **Sprint Planning**  
This is a meeting that opens each sprint with writing, estimating, prioritizing, and assigning stories that the team intends to complete for the sprint.
2. **Daily Stand-Up**  
A chance for teams to meet every day to discuss the previous day’s progress, discuss the day’s work, and raise any roadblocks. Ideally, the meeting is very short (5-15 minutes) and is near the start of the workday to minimize the interruption of dedicated work time.
3. **Sprint Review**  
This is part of a meeting which ends each sprint with a review of work accomplished, new backlog items, missed estimates, and other quantifiers of team progress.
4. **Sprint Retrospective**  
A discrete meeting or block of time for discussing what went well and what to improve about how the team operates in qualitative terms.

Agile teams usually have distinct, cross-functional roles. Common roles include:

- The "project manager/team lead" manages the team, assigns work, reports to management, assists team members, and performs other managerial duties.
- The "scrum master" is responsible for leading Agile rituals.
- A "product owner/product manager" represents the client or end-user to the team. They have an active hand in writing stories, reviewing product functionality, and communicating progress to clients and expectations to the team.
- An "individual contributor" is any member of the team whose main responsibility is building the product. Developers, designers, QA specialists and writers are all examples of individual contributors.

While these definitions are important for our shared understanding, the major theme of this article is that achieving your team’s goals is more important than implementing "proper" Agile. If this doesn’t exactly match your setup, common elements should help apply upcoming recommendations to your experience.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e0200d18-740a-45d3-ab60-096581b5d70b/board-irfan-simsar-unsplash.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e0200d18-740a-45d3-ab60-096581b5d70b/board-irfan-simsar-unsplash.jpg" sizes="70vw" caption="(Image credit: ‘İrfan Simsar’ on <a href='https://unsplash.com/'>Unsplash</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e0200d18-740a-45d3-ab60-096581b5d70b/board-irfan-simsar-unsplash.jpg'>Large preview</a>)" alt="'Scrum Board' by İrfan Simsar on Unsplash" >}}

## Constraints Of Part-Time Work

Immediately, we see how the constraints of part-time work cut into standard Agile. First off, in a given two-week sprint, each employee may spend 2 hours in sprint planning, 10 times 15 minutes in stand-up, 1 hour in sprint review, and 30 minutes in sprint retrospective, for a total of 6 hours in Agile meetings. For a full-time employee, that’s only 7.5% of their 80-hour fortnight, for a half-time employee it doubles to 15%. Add in other meetings and account for context switching and suddenly your individual contributors have very little time left each week to individually contribute.

Thus, part-time work exacerbates the need for good capacity estimation and up-front planning while reducing the time available for it. Fortunately, Agile’s notion of story points applies well. Story points estimate effort rather than time and thus stay constantly effective between full-time and part-time workers, though of course part-time workers will take longer to achieve the same amount of story points, which you can account for by measuring the team’s velocity.

Even if your development team is part-time, your clients may not be. Customer support, emergency bug fixes, outage repairs, and even regular communication can be more difficult with part-time work adding additional overhead.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/107f0a17-6c3c-4678-ae1c-d67d231d80c4/watch-brad-neathery-unsplash.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/107f0a17-6c3c-4678-ae1c-d67d231d80c4/watch-brad-neathery-unsplash.jpg" sizes="100vw" caption="(Image credit: ‘Brad Neathery’ on <a href='https://unsplash.com/'>Unsplash</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/107f0a17-6c3c-4678-ae1c-d67d231d80c4/watch-brad-neathery-unsplash.jpg'>Large preview</a>)" alt="'Man in a watch typing' by Brad Neathery on Unsplash" >}}

{{% ad-panel-leaderboard %}}

## Frequently Intersecting Constraints

While not all part-time teams will experience these additional challenges, in my experience part-time work often overlaps with remote work, different time zones and availabilities, and classification of workers as temporary, contractors, or interns instead of employees. This is not an article about any of these things, but they bear mentioning. 

Part-time work adds significant overhead to the already difficult task of finding a regular time when everyone is available to meet. If some team members work in the mornings and others in the evenings or are located across the world from each other, scheduling quickly becomes impossible. GitLab has published [extensive documentation on remote communication](https://about.gitlab.com/handbook/communication/) that might be helpful.

Working with contractors, student interns, temporary hires, or other non-permanent teams or team members brings its own advantages and challenges. That said, however, someone got to the table, the Agile framework treats them as an equal member of the team and stakeholder in the project.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7abbdc79-3c84-487b-a3b9-c9b9d099b3d6/meeting-you-x-ventures-unsplash.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7abbdc79-3c84-487b-a3b9-c9b9d099b3d6/meeting-you-x-ventures-unsplash.jpg" sizes="100vw" caption="(Image credit: ‘You X Ventures’ on <a href='https://unsplash.com/'>Unsplash</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7abbdc79-3c84-487b-a3b9-c9b9d099b3d6/meeting-you-x-ventures-unsplash.jpg'>Large preview</a>)" alt="'Untitled' (Meeting) by You X Ventures on Unsplash." >}}

## Redefining Rituals For Part-Time Teams

Now that we’ve framed the challenges that part-time work creates, let’s focus on solutions. While I’ve seen a number of successful modifications to Agile rituals for part-time teams, I reached out to Professor Armando Fox, co-author of *Engineering Software as a Service: An Agile Approach Using Cloud Computing* with David Patterson. In an email interview, he emphasized two key goals of agile rituals to retain:

<blockquote>“The reason Agile is a good fit [for part-time teams] is the idea of using user stories as the unit of work. The key to doing this successfully is up-front planning and continuous check-ins.”<br /><br />&mdash; Armando Fox</blockquote>

Sprint planning condenses up-front planning to a single high-value meeting. For part-time teams, the product owner, scrum master, and team lead (who may be only one or two people, more on that later) should do as much pre-meeting work as possible to define well-scoped tickets for the individual contributors to estimate and take. Fox said "if stories are tightly-circumscribed, branches are short-lived, stories require modest amounts of code that can be delivered with good test coverage, and code quality is maintained through continuous code review (pull requests) as well as the use of code quality measurement tools, the team can successfully divide-and-conquer even if they’re not always working at the same time." That’s definitely a lot of "if" statements, working in this manner will take dedicated effort from the entire team, but should result in a quality product.

The other half of the equation is continuous check-ins. Agile’s daily stand-ups work great for co-located full-time teams, if everyone’s in the office by 9 or 10 AM the meeting happens more or less naturally. It’s tempting to replace this with an asynchronous check, like status-report emails, but Fox advocates that teams stick to the ritual. "The team needs to check-in frequently &mdash; we recommend daily 5-minute stand-ups &mdash; so that any red flags can be spotted early. Even part-time teams can find 5 minutes a day that the whole team is available. Email isn’t good for this; an interactive meeting, where people can also mention blocking items and others can immediately speak up with suggestions, is the best format," he wrote.

For a part-time team, it may also be tempting to do away with regular meetings entirely and rely solely on the start and end of sprint check-ins. Fox warns that "every team [that he has] coached at Berkeley has said that they quickly realized that once-a-week team meetings were nowhere near enough to keep everyone on the same page."

Sprint reviews and retrospectives are important components of Agile. If teams do not regularly evaluate their working practices and performance, bad interactions will continue unchecked and discontent will grow. However, the velocity measurement and end-of-sprint re-assignment tasks can be handled by the scrum master outside of meeting times, and the team leader can use one-on-one meetings and their perception of team mood in stand-ups and sprint planning to reduce the need for sprint review and retrospective. 

If you absolutely need to cut back on the number and duration of Agile meetings, cut review and retrospective first. That said, it is important to celebrate the team’s progress each sprint and give people space to air grievances. A decent compromise can be to extend the last stand-up of each sprint to accomplish this communication within the team.

{{% ad-panel-leaderboard %}}

## Defining Roles On A Part-Time Agile Team

This section depends entirely on the composition of the team. However, there are a few useful heuristics for assigning roles. Responsibilities assigned should minimize communication overhead (which scales worse-than-linearly with team size), fit individual contributors' abilities, and account for team members' schedules and availability.

For this section, I turned to Professor Barbara Johnson, who teaches a team software development course that I am currently enrolled in at Grinnell College. She wrote:

<blockquote>“I have sometimes seen teams come to rely upon what might be called a 'chief organizer' who combines the roles of not only a scrum master (who organizes the team) but also the product owner (who coordinates and documents the client’s needs and feedback).  This lessens the cognitive overhead of the rest of the team, who then can focus more on moving the project’s code and testing suite forward with each iteration.”</blockquote>

This matches my experience with part-time teams.

If possible, condense the managerial positions (team lead, product manager, scrum master) into a single role and assign that role to the "fullest-time" team member. If you have a team of 10 where only 1 person is full-time or otherwise has greater availability, that person should have as many organizational and communication responsibilities as feasible. Part-time teams require just as much communication as full-time teams and an even greater logistical effort, so concentrating that work in one person massively reduces communication overhead.

However, frequently this isn’t possible, either because no one has extra availability or because those people are better suited to individual contributor roles. In that case, I still advocate for condensing managerial responsibilities as much as possible but breaking the product owner back out into its own role. In this case, it’s important to be realistic when estimating how much further work these people will be able to do on user stories considering their other work for the team and client.

Most of the members of the part-time team will be individual contributors. There are two competing philosophies for individual contributors: generalist teams and teams of specialists. Imagine that your team is developing a web application. A generalist team would be composed of entirely full-stack developers. These developers would never be blocked on others' work as, in theory, they are equally comfortable on anything from design to deployment. Alternately, if a designer, front-end engineer, back-end engineer, and site reliability engineer comprise a team, they will be fast and effective at their own work because they only spend their time on the thing that they’re best at.

As a team organizer, you may find yourself with a team of generalists, a team of specialists, or a mix. Putting together a part-time team of solid performers is hard enough without restricting yourself to one type of individual contributor, so, fortunately, both types bring something useful to the table. If you can recognize which of your individual contributors are generalists and which are specialists, you can assign tasks more effectively to maximize the impact of their limited work time.

Finally, on teams where people are working ten or fewer hours per week, it is tempting to throw out roles entirely and just say "do what you can." Per our theme, these super-part-time teams need even more structured communication but have even less time for it. If everyone has such limited, scattered availability that you cannot justify assigning roles at all, it’s probably worth re-examining the structure, goals, and feasibility of the project.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6f510c00-a18e-41c2-87fc-899948283ffe/man-saulo-mohana-unsplash.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6f510c00-a18e-41c2-87fc-899948283ffe/man-saulo-mohana-unsplash.jpg" sizes="100vw" caption="(Image credit: ‘Saulo Mohana’ on <a href='https://unsplash.com/'>Unsplash</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6f510c00-a18e-41c2-87fc-899948283ffe/man-saulo-mohana-unsplash.jpg'>Large preview</a>)" alt="'At the bustling Times Square' by Saulo Mohana on Unsplash" >}}

## Client Communication

Software development is slow, complex work, and part-time teams only magnify that truth. Agile includes the client in the process by writing user stories, rapid prototyping, a quick release schedule, and consistent communication.

As a part-time team, communicate reasonable expectations to the client. For a half-time team, remember that development time is cut by more than half, build an extra buffer into doubled estimates. As development time is limited, it is critical to solicit complete, accurate specifications when meeting with the client or end-users to avoid wasting your efforts.

Don’t let part-time work make you fall behind on client communication. Even if there is very little progress to report, soliciting regular feedback and posting updates at a reasonable cadence should increase the client’s patience with the slow development pace.

## Conclusion: Goals > Methods

You can get a lot done in a part-time schedule. Outside of coding, 10-20 hours per week is enough time to train for a first marathon. With a strong team and good working practices, it is enough time to bring a great product to the market. Using Agile to encourage up-front planning and continuous check-ins with user stories, regular stand-ups, and well-defined roles will allow even part-time teams to overcome communication barriers and work effectively towards a shared goal.

### <span class="rh">Further Reading</span> on SmashingMag:

<ul>
	<li><a title="Read 'Bringing A Healthy Code Review Mindset To Your Team'" href="https://www.smashingmagazine.com/2019/06/bringing-healthy-code-review-mindset/" rel="bookmark">Bringing A Healthy Code Review Mindset To Your Team</a></li>
	<li><a title="Read 'Building Diverse Design Teams To Drive Innovation'" href="https://www.smashingmagazine.com/2018/05/building-diverse-design-teams-innovation/" rel="bookmark">Building Diverse Design Teams To Drive Innovation</a></li>
	<li><a title="Read 'The Case For Brand Systems: Aligning Teams Around A Common Story'" href="https://www.smashingmagazine.com/2019/06/case-brand-systems-align-teams/" rel="bookmark">The Case For Brand Systems: Aligning Teams Around A Common Story</a></li>
	<li><a title="Read 'Creating Authentic Human Connections Within A Remote Team'" href="https://www.smashingmagazine.com/2019/08/creating-authentic-human-connections-remote-team/" rel="bookmark">Creating Authentic Human Connections Within A Remote Team</a></li>
</ul>

{{< signature "dm, yk, il" >}}
