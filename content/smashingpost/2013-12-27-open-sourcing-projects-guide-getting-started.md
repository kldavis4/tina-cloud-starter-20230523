---
title: So You've Decided To Open-Source A Project At Work. What Now?
slug: open-sourcing-projects-guide-getting-started
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/83d92a45-ca64-4cb1-a7be-8a8be73fbf97/open-source-icon.png
date: 2013-12-27T16:57:23.000Z
author: nicholas-c-zakas
description: >-
  A while back, I wrote a post about [starting an open-source
  project.](https://www.smashingmagazine.com/2013/01/03/starting-open-source-project/)
  The focus of that article was on starting an open-source project as an individual. I received a lot of positive feedback and also some questions about how the process changes when you’re open-sourcing a project at work.
categories:
  - Community
  - Workflow
  - Open Source
  - Career
  - Licenses
  - Copyright
---
Many companies are starting to investigate and participate in the open-source community, and yet few guides for doing so exist. This article focuses primarily on the <strong>process of open-sourcing a project at work</strong>, which brings with it other concerns and decisions.

{{% feature-panel %}}

## Why Open Source?

Before delving into the how, it’s useful to step back and talk about the why. Why is it that so many companies have or are starting to establish an open-source presence? There are actually a number of reasons:

- **Technical brand**.  Companies want to be known as a place where smart people work. One excellent way to show this is by releasing code that has been written at the company. Doing so creates mindshare in the community, familiarity with the company and its contributions, and fodder for future technical brand initiatives (such as giving talks at meetups and conferences).
- **Recruiting**.  Time and again, you’ll see contributors joining companies that sponsor open-source projects. I saw this happen frequently while at Yahoo, where YUI contributors would sometimes end up as Yahoo employees after having contributed to the project on an ongoing basis. Similar hires have occurred in the Node.js community. The reason is pretty clear: If you work on an open-source project in your spare time, imagine how great it would be to turn that hobby into a job. Additionally, allowing job candidates to see some of the company’s code gives some good insight into what working at the company would be like.
- **Giving back**.  A lot of companies benefit from open-source software, and contributing open-source software back into the world is a way of giving back. These days, it’s part of what it means to be involved in the technical community. When you receive, find a way to give back. A lot of companies are embracing this philosophy.

There are many more reasons why companies are choosing to open-source, but these are the primary drivers. Therefore, the process of open-sourcing a project must be aligned with these goals while protecting the company’s interests.

## Getting Started

Suppose someone at your company wants to open-source something. This has never happened before and you’re not sure what to do. Do you just put it up on GitHub? Announce it in a press release or blog post? How do you know that the code is OK to open-source? There is a lot of planning to do, and it all starts (unfortunately) with the legal department.

Giving away company assets is <strong>as much a legal issue as anything</strong> else. The very first conversation should be with an appropriate member of your company’s legal team to discuss the ins and outs of open-sourcing. In larger companies, one or more intellectual property (IP) attorneys are likely on staff or on retainer; in smaller companies, this conversation might start with the general counsel. In either case, it’s important to lay out exactly what you want to do and to clarify that you’d like to formalize a repeatable process for open-sourcing projects.

The primary legal concerns tend to be around licensing, code ownership and trade secrets. These are all important to discuss openly. Because many companies have done this already, you should have a fair amount of evidence of how other companies have established their processes. The most important thing is to engage the legal department early in the process and to have a champion on the legal team who you can work with should any issues arise.

Recommended reading: [I Contributed To An Open-Source Editor, And So Can You](https://www.smashingmagazine.com/2016/08/contributing-open-source/)

## Choose A Default License

One of the first topics of discussion should be which open-source license the company will use as its standard. Leaving the team for each project to decide for itself which license to use is a bad idea, because a lack of awareness could quite possibly lead to two projects from the same company having incompatible licenses. Decide up front exactly which license to use, and use it for <em>all</em> open-source projects in your company.

I touched on the different types of licenses in my previous article (also, see “<a href="https://www.smashingmagazine.com/2011/06/14/understanding-copyright-and-licenses/">Understanding Copyright and Licenses</a>”). In general, companies tend to standardize <strong>either the three-clause BSD license or the Apache license</strong>. Very rarely will a company standardize the MIT license, because the standard MIT license doesn’t contain a clause that prevents use of the company’s name in advertisements for software that makes use of the project. The Apache license has additional clauses related to patent protection, which some companies prefer.

The ultimate choice of a license typically comes down to legal considerations on the nature of the code being released. The philosophical implications of which license you choose are not important; using the same license for all projects in your company <em>is</em> important.</p>

Recommended reading: [A Short Guide To Open-Source And Similar Licenses](https://www.smashingmagazine.com/2010/03/a-short-guide-to-open-source-and-similar-licenses/)

## Outgoing Review

The next topic of discussion should be to define an outgoing review process. Just putting code out in the public without some sort of review is neither safe nor sane. In general, a request to open-source a project should be reviewed by the following:

- **Legal**.  As mentioned, the legal department needs to be kept in the loop during this process. They will likely not review the code, but rather will want to understand what the code does and whether it could be considered a company secret.
- **Security**.  Someone with a security mindset should actually look at the code to make sure it doesn’t reveal any security issues or contain code that should not be made public. This process could be manual or automated, depending on the complexity of the code.
- **Executive**.  Someone on the executive team needs to approve the request, basically saying that they believe this code is safe to share and that they are aware that the code is being published.

Exactly how an outgoing review gets started tends to be company-specific. It could be done by <strong>submitting a request to a mailing list</strong>, filling out a form or just setting up a meeting. How it’s implemented isn’t as important as the fact that the review occurs and is done quickly. So, setting a deadline for a response is a good idea. Depending on the size of the company, this could range from a few days to a few weeks, but setting up the expectation ahead of time helps to alleviate any scheduling issues.</p>

## Accepting Contributions

One part of the process that is often forgotten is figuring out <strong>rules for accepting external contributions</strong>. Open-sourcing a project is basically a way of saying, “Hey, we’d love to have you fix our bugs!” Part of the point is to get people interested enough to want to contribute to the project. Establish a process so that you know how and from whom external contributions may be made.

<a href="https://www.flickr.com/photos/opensourceway/7496803638/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f01fd594-04ce-4225-bc67-f42af23f11c4/open3.jpg" alt="Open-source projects" width="500" height="281" /></a><br>
<em>When building something, accepting external contributions can significantly benefit the project, but you need to establish a process for contributions first. Image credit: <a href="https://www.flickr.com/photos/opensourceway/7496803638/">open source way</a>.</em>

The company should require a contributor license agreement (CLA) to be signed before accepting contributions from external developers. A CLA is a legal document that typically states a few things:

*   The contributor asserts that they are the original author of the code they are submitting.
*   The contributor grants the project the right to use and distribute the code they are submitting.
*   The contributor has the right to grant the previous two points.
*   Any code submitted by a contributor is not guaranteed to be accepted or used.

Take the Node.js CLA. It’s a pretty straightforward form that defines the expectations for contributors and asks for the contributor’s name and other information. These days, asking for someone’s GitHub user name as well is quite common (to help automate the process of checking CLAs for commits).

The CLA will be important should any legal action be taken against your company as a result of the code contained in the project. Because the company is the maintainer of the project, any legal action would likely be directed at the company itself, rather than any individual contributor.

CLAs are sometimes controversial, and some developers refuse to sign them. That’s an acceptable loss to protect yourself and your company from the legal risks of open-source projects. Those who are familiar with the open-source community and the reason behind CLAs will be more than happy to sign on and contribute to your project.

Recommended reading: [So You Want To Crowdfund Your Startup App?](https://www.smashingmagazine.com/2015/08/crowdfunding-a-startup-app/)

## Maintaining The Project

An overlooked part of the open-source process is maintaining the project once it’s been published. Many developers (and some companies) view the step of open-sourcing a project as the end of the process — they’ve already spent considerable time creating software that they now want to share with the world. In truth, open-sourcing a project is the beginning of a journey. The act of sharing now makes it, effectively, communal software, and you can now expect the project to be discussed and to evolve as a whole.

<a href="https://www.flickr.com/photos/opensourceway/5009661706/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/457bb5a5-017d-4b3d-8c20-968af34ab9da/open1.jpg" alt="open1" width="500" height="281" /></a><br>
<em>Once a new project is open-sourced, eventually you'll start receiving suggestions, requests and pull-requests. Maintenance is a task that is often overlooked in open-source projects. <a href="https://www.flickr.com/photos/opensourceway/5009661706/">Image credit.</a></em>

Many companies that are new to the open-source community make the mistake of publishing their code and leaving it behind. Issues are left unresolved and unanswered, road maps are not shared, pull requests are ignored, and there is no way to get in contact with the people behind the project. As much as open-source projects can enhance your technical brand, leaving projects in this state can hurt it.

Once you’ve open-sourced a project, you <strong>must commit to maintain it</strong>. Even stable software will have bugs, and some of those bugs could be found by people outside of your company. If you have no intention of interacting with anyone outside of the company on this project, then you might want to consider simply distributing the compiled binary or library freely, and not actually open-sourcing the code.

While there are no established rules for maintaining a project, here are some guidelines I follow:

1.  **The public repo is the source of truth.** Once you’ve published your source code to a public repository (or repo), all development should happen in that repository. The public repo shouldn’t simply be a clone of an internal one. If the project is being actively developed, then that development should happen exclusively in the public repo in order to be as transparent as possible. Developing in private and then updating periodically prevents the use of pull requests and makes forking your project extremely difficult and frustrating.
2.  **Plan in public.** Use a public bug tracker to track all issues, so that others can see what’s being worked on and what’s already been reported. Post a road map somewhere public that shows plans for development. Be as transparent about the development process as possible. In short, open-source the way your project will grow and evolve.
3.  **Dedicate company time.** If you are the primary author of the project and you’ve open-sourced the code, then you (or a delegate) should set aside time to interact with external contributors. That means making timely responses to pull requests and issues, which in turn means setting aside time daily or weekly. This has now become part of your full-time job, not just a hobby.
4.  **Open channels of communication.** Give external contributors a way to interact directly with the maintainers. This could be through a forum, mailing list, IRC chat or another channel. Make sure that these systems are public; for example, an IRC chat should not be on your company’s chat server. Plenty of free communication services exist to make use of. The simplest and least disruptive method is to create a free mailing list using Google Groups or Yahoo Groups.
5.  **Commit to document.** Lack of documentation is a huge problem with open-source projects. From the start, commit to writing good documentation that explains not only how to use the project but also how to set up a development environment, run tests and work effectively with the code as a contributor. There is no better way to discourage people from using your software than to give them no way to get up and running on their own.
6.  **Maintain regular outgoing communication.** There should be a steady stream of outgoing communication about the project. At a minimum, post announcements about new releases and security issues that require immediate upgrading. Maintain changelogs that describe differences between versions, and follow a predictable and regular scheme in your versioning (such as by following [semantic versioning](https://semver.org)). This will help both users and contributors understand the impact of filing issues and submitting pull requests.

An open-source project very quickly takes on a life of its own once released. If a community forms around the project, then it could take up more and more of your time. That’s why a commitment to maintain the project needs to be a part of the open-sourcing process. Letting a project languish without any attention sends a horrible message to those outside of your company and will discourage people from contributing.

## Warning Signs

Most open-source projects, whether by individuals or companies, are started with the best of intentions. Typically, the goal is to share learning and code with the world. However, the Internet is littered with abandoned projects. If your project ends up like this, it could hurt your and your company’s reputation. Projects <strong>slowly decay over time</strong> and can usually be identified by one or more of the following characteristics:

- **“Not enough time”** The more frequently this phrase appears in responses to pull requests and issues, the more likely the project is headed for the graveyard. This is one of the top reasons why projects die: The maintainer runs out of time to maintain it. As should be obvious from this article, maintaining a project requires a significant amount of work, which is frequently not sustainable in the long term.
- **Too few contributors**.  If most contributions come from one person, then the project is likely either early in its life (on the upswing) or close to the end. You can easily tell which is the case by looking at the date of the first commit. Thriving projects tend to have a large number of commits from the maintainer and a small number of frequent commits from a few others. Another good way to measure this activity is in the number of merged pull requests in the last year.
- **Too many open issues and pull requests**.  A surefire sign that a project is on its way out is issues and pull requests that are left open with no comment. More than a few issues that have been open for a year means that the project isn’t being cared for.
- **No way to contact the maintainer**.  If you can’t find a reliable way to contact the maintainer, whether through email, a mailing list, Twitter, issues or pull requests, then there’s not much hope for the project. Maintainers aren’t maintaining if they aren’t communicating.

Keep an eye on these patterns in your own project. If you recognize the warning signs, then you’ll have to decide what to do with the project. Either someone else should become the maintainer or it’s time to end-of-life the project.</p>

## End-Of-Lifing Projects

At some point, you or your company might find that there is no longer interest in maintaining the project. This is a natural evolution of software — sometimes a project outlives its usefulness. When this happens, you need to appropriately end-of-life the project.

End-of-lifing typically starts with a <strong>public announcement</strong> that the project is no longer being actively maintained (along with a post in the project’s <code>README</code> file). The announcement should address the following:

*   Why is the project being end-of-lifed? Has it been superseded by something else? Is it no longer in use? Do you recommend different software written by someone else?
*   What will happen to outstanding issues? Will bugs still be fixed? Will all outstanding issues be closed without being fixed?
*   Is there an opportunity to transfer ownership? If someone really likes the project, is your company willing to transfer ownership to them or their organization?

Ultimately, you might decide to delete the repository completely. While being able to see all of a company’s projects, even those that have been end-of-lifed, is sometimes nice, that comes at a cost, and so removing repositories from time to time might be prudent. In doing so, be certain that you have effectively communicated that the project is going away, and give at least 30 days notice to allow others to fork the project if they are so inclined.</p>

## Conclusion

Open-sourcing projects at work is a great initiative for many reasons. When done correctly, an open-source presence will do a lot to promote your company and its employees. Active open-source involvement signals your company’s willingness to interact with the technical community and to contribute back, both signs of a strong technical brand.

On the other hand, a poor open-source presence is worse than no presence at all. It signals general laziness or apathy towards a community of developers, a community that might very well want to help your project succeed. Few things are as demoralizing as trying to work on an open-source project that has been abandoned. Don’t be that company.

{{< signature "al" >}}

