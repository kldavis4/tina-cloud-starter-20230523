---
title: How To Start An Open-Source Project
slug: starting-an-open-source-project
image: null
date: 2013-01-03T11:45:43.000Z
author: nicholas-c-zakas
description: >-
  At Velocity 2011, Nicole Sullivan and I introduced [CSS
  Lint](https://csslint.net), the first code-quality tool for CSS. We had spent
  the previous two weeks coding like crazy, trying to create an application that
  was both useful for end users and easy to modify. Neither of us had any
  experience launching an open-source project like this, and we learned a lot
  through the process.
categories:
  - Coding
  - Workflow
  - Open Source
  - Resources
---
At Velocity 2011, <a href="https://stubbornella.org">Nicole Sullivan</a> and I introduced <a href="https://csslint.net">CSS Lint</a>, the first code-quality tool for CSS. We had spent the previous two weeks coding like crazy, trying to create an application that was both useful for end users and easy to modify. Neither of us had any experience launching an open-source project like this, and we learned a lot through the process.

<img loading="lazy" decoding="async" loading="lazy" decoding="async" class="124016" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8ec436d6-175a-4346-9b86-9bfcd99e5266/opensource-1.jpg" alt="open-source" width="500" height="281" /><br>
<em>Image Credit: <a href="https://www.flickr.com/photos/opensourceway/6554314981">opensourceway</a>.</em>

After some initial missteps, the project finally hit a groove, and it now regularly get compliments from people using and contributing to CSS Lint. It’s actually not that hard to create a successful open-source project when you stop to think about your goals.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [So You’ve Decided To Open-Source A Project At Work. What Now?](https://www.smashingmagazine.com/2013/12/open-sourcing-projects-guide-getting-started/)
*   [I Contributed To An Open-Source Editor, And So Can You](https://www.smashingmagazine.com/2016/08/contributing-open-source/)
*   [A Short Guide To Open-Source And Similar Licenses](https://www.smashingmagazine.com/2010/03/a-short-guide-to-open-source-and-similar-licenses/)
*   [So You Want To Crowdfund Your Startup App?](https://www.smashingmagazine.com/2015/08/crowdfunding-a-startup-app/)

{{% feature-panel %}}

## What Are Your Goals?

These days, it seems that anybody who writes a piece of code ends up pushing it to GitHub with an open-source license and says, “I’ve open-sourced it.” Creating an open-source project isn’t just about making your code freely available to others. So, before announcing to the world that you have open-sourced something that hasn’t been used by anyone other than you in your spare time, stop to ask yourself what your goals are for the project.

The first goal is always to <strong>create something useful</strong>. For CSS Lint, our goal was to create an extensible tool for CSS code quality that could easily fit into a developer’s workflow, whether the workflow is automated or not. Make sure that what you’re offering is useful by looking for others who are doing similar projects and figuring out how large of a user base you’re looking at.

After that, decide why you are open-sourcing the project in the first place. Is it because you just want to share what you’ve done? Do you intend to <strong>continue developing the code</strong>, or is this just a snapshot that you’re putting out into the world? If you have no intention of continuing to develop the code, then the rest of this article doesn’t apply to you. Make sure that the readme file in your repository states this clearly so that anyone who finds your project isn’t confused.

If you are going to continue developing the code, do you want to <strong>accept contributions</strong> from others? If not, then, once again, this article doesn’t apply to you. If yes, then you have some work to do. Creating an open-source project that’s conducive to outside contributions is more work than it seems. You have to create environments in which those who are unfamiliar with the project can get up to speed and be productive reasonably quickly, and that takes some planning.

This article is about starting an open-source project with these goals:

1.  Create something useful for the world.
2.  Continue to develop the code for the foreseeable future.
3.  Accept outside contributions.</p>

## Choosing A License

Before you share your code, the most important decision to make is what license to apply. The open-source license that you choose could greatly help or hurt your chances of attracting contributors. All licenses allow you to retain the copyright of the code you produce. While the concept of licensing is quite complex, there are a few common licenses and a few basic things you should know about each. (If you are open-sourcing a project on behalf of a company, please speak to your legal counsel before choosing a license.)

*   [GPL](https://www.gnu.org/licenses/gpl.html) The GNU Public License was created for the GNU project and has been credited with the rise of Linux as a viable operating system. The GPL license requires that any project using a GPL-licensed component must also be made available under the GPL. To put it simply, any project using a GPL-licensed component in any way must also be open-sourced under the GPL. There is no restriction on the use of GPL-licensed applications; the restriction only has to do with the modification and distribution of derived works.
*   [LGPL](https://www.gnu.org/licenses/lgpl.html) The Lesser GPL is a slightly more permissive version of GPL. An LGPL-licensed component may be linked to from an application without the application itself needing to be open-sourced under GPL or LGPL. In all other ways, LGPL is the same as GPL, so any derived works must also be open-sourced under GPL or LGPL.
*   [MIT](https://opensource.org/licenses/MIT) Also called X11, this licence is permissive, allowing for the use and redistribution of code so long as the license and copyright are included along with it. MIT-licensed code may be included in proprietary code without any additional restrictions. Additionally, MIT-licensed code is GPL-compatible and can be combined with such code to create new GPL-licensed applications.
*   [BSD3](https://opensource.org/licenses/BSD-3-Clause) This is also a permissive license that allows for the use and redistribution of code as long as the license and copyright are included with it. In addition, any redistribution of the code in binary form must include a license and copyright in its available documentation. The clause that sets BSD3 apart from MIT is the prohibition of using the copyright holder’s name to promote a product that uses the code. For example, if I wrote some code and licensed it under BSD3, then an application that uses that code couldn’t use my name to promote the product without my permission. BSD3-licensed code is also compatible with GPL.

There are many other open-source licenses, but these tend to be the most commonly discussed and used.

<img loading="lazy" decoding="async" loading="lazy" decoding="async" class="124019" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8dbe116d-b3f0-46db-8323-d4d5b49967bb/opensource-3.jpg" alt="open-source" width="500" height="281" /><br>
<em>Image Credit: <a href="https://www.flickr.com/photos/opensourceway/5751646633">opensourceway</a>.</em>

One thing to keep in mind is that <a href="https://creativecommons.org">Creative Commons</a> licenses are <em>not</em> designed to be used with software. All of the Creative Commons licenses are intended for “creative work,” including audio, images, video and text. The Creative Commons organization itself <a href="https://wiki.creativecommons.org/Frequently_Asked_Questions#Can_I_apply_a_Creative_Commons_license_to_software.3F">recommends</a> not using Creative Commons licenses for software and instead to use licenses that have been specifically formulated to cover software, as is the case with the four options discussed above.

<strong>So, which license should you choose</strong>? It largely depends on how you intend your code to be used. Because LGPL, MIT and BSD3 are all compatible with GPL, that’s not a major concern. If you want any modified versions of your code to be used only in open-source software, then GPL is the way to go. If your code is designed to be a standalone component that may be included in other applications without modification, then you might want to consider LGPL. Otherwise, the MIT or BSD3 licenses are popular choices. Individuals tend to favor the MIT license, while businesses tend to favor BSD3 to ensure that their company name can’t be used without permission.

To help you decide, look at how some popular open-source projects are licensed:

*   jQuery: MIT license
*   [YUI](https://yuilibrary.com/license/): BSD3 license
*   Dojo Toolkit: dual-licenced under BSD3 and Academic Free License
*   [Backbone](https://github.com/documentcloud/backbone/blob/master/LICENSE): MIT license

Another option is to release your code into the <a href="https://en.wikipedia.org/wiki/Public_domain">public domain</a>. Public-domain code has no copyright owner and may be used in absolutely any way. If you have no intention of maintaining control over your code or you just want to share your code with the world and not continue to develop it, then consider releasing it into the public domain.

To learn more about licenses, their associated legal issues and how licensing actually works, please read David Bushell’s “<a href="https://www.smashingmagazine.com/2011/06/14/understanding-copyright-and-licenses/">Understanding Copyright and Licenses</a>.”

## Code Organization

After deciding how to license your open-source project, it’s almost time to push your code out into the world. But before doing that, look at how the code is organized. <strong>Not all code invites contributions.</strong> If a potential contributor can’t figure out how to read through the code, then it’s highly unlikely any contribution will emerge. The way you lay out the code, in terms of file and directory structure as well as coding style, is a key aspect to consider before sharing it publicly. Don’t just throw out whatever code you have been writing into the wild; spend some time figuring out how others will view your code and what questions they might have.

For CSS Lint, we decided on a basic <a href="https://github.com/stubbornella/csslint/">top-level directory structure</a> of <code>src</code> for source code, <code>lib</code> for external dependencies, and <code>tests</code> for all test code. The <code>src</code> directory is further subdivided into directories that group together related files. All CSS Lint rules are in the <code>rules</code> subdirectory; all output formatters are in the <code>formatters</code> directory; etc. The <code>tests</code> directory is split up into the same subdirectories as <code>src</code>, thereby indicating the relationship between the test code and the source code. Over time, we’ve added top-level directories as needed, but the same basic structure has been in place since the beginning.</p>

## Documentation

One of the biggest complaints about open-source projects is the lack of documentation. Documentation isn’t as fun or exciting as writing executable code, but it is critical to the success of an open-source project. The best way to discourage use of and contributions to your software is to have no documentation. This was an early mistake we made with CSS Lint. When the project launched, we had no documentation, and everyone was confused about how to use it. Don’t make the same mistake: get some documentation ready before pushing the project live.

The documentation should be easy to update and shouldn’t require a code push, because it will need to be changed very quickly in response to user feedback. This means that the best place for documentation isn’t in the same repository as the code. If your code is hosted on GitHub, then make use of the built-in wiki for each project. All of the <a href="https://github.com/stubbornella/csslint/wiki">CSS Lint documentation</a> is in a GitHub wiki. If your code is hosted elsewhere, consider setting up your own wiki or a similar system that enables you to update the documentation in real time. A good documentation system must be easy to update, or else you will never update it.</p>

### End-User Documentation

Whether you’re creating a command-line program, an application framework, a utility library or anything else, keep the end user in mind. The end user is not the person who will be modifying the code; it’s the one who will be using the code. People were initially confused about CSS Lint’s purpose and how to use it effectively because of the lack of documentation. Your project will never gain contributors without first gaining end users. Satisfied end users are the ones who will end up becoming contributors because they see the value in what you’ve created.</p>

### Developer Guide

Even if you’ve laid out the code in a logical manner and have decent end-user documentation, contributions are not guaranteed to start flowing. You’ll need a developer guide to help get contributors up and running as quickly as possible. A good developer guide covers the following:

1.  **How to get the source code** Yes, you would hope that contributors would be familiar with how to check out and clone a repository, but that’s not always the case. A gentle introduction to getting the source code is always appreciated.
2.  **How the code is laid out** Even though the code and directory structures should be fairly self-explanatory, writing down a description for posterity always helps.
3.  **How to set up the build system** If you are using a build system, then you’ll need to include instructions on how to set it up. These instructions should include where to get build-time dependencies that aren’t already included in the repository.
4.  **How to run a build** These are the steps necessary to run a development build and to execute unit tests.
5.  **How to contribute** Spell out the criteria for contributing to the project. If you require unit tests, then state that. If you require documentation, mention that as well. Give people a checklist of things to go over before submitting a contribution.

I spent a lot of time refining the “<a href="https://github.com/stubbornella/csslint/wiki/Developer-Guide">CSS Lint Developer Guide</a>” based on conversations I had had with contributors and questions that others would ask. As with all documentation, the developer guide should be a living document that continues to grow as the project grows.</p>

## Use A Mailing List

All good open-source projects give people a place to go to ask questions, and the easiest way to achieve that is by setting up a mailing list. When we first launched CSS Lint, Nicole and I were inundated with questions. The problem is that those questions were coming in through many different channels. People were asking questions on Twitter as well as emailing each of us directly. That’s exactly the situation you don’t want.

Setting up a mailing list with <a href="https://groups.yahoo.com">Yahoo Groups</a> or <a href="https://groups.google.com">Google Groups</a> is easy and free. Make sure to do that before announcing the project’s availability, and actively encourage people to use the mailing list to ask questions. Link to the mailing list prominently on the website (if you have one) or in the documentation.

The other important part of running a mailing list is to actively monitor it. Nothing is more frustrating for end users or contributors than being ignored. If you’ve set up a mailing list, take the time to monitor it and <strong>respond to people who ask questions</strong>. This is the best way to foster a community of developers around the project. Getting a decent amount of traffic onto the mailing list can take some time, but it’s worth the effort. Offer advice to people who want to contribute; suggest to people to file tickets when appropriate (don’t let the mailing list turn into a bug tracker!); and use the feedback you get from the mailing list to improve documentation.

<img loading="lazy" decoding="async" loading="lazy" decoding="async" class="124021" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d985dfcc-8f68-40ba-848c-82ab70b4de3c/opensource-2.jpg" alt="open-source" width="500" height="281" /><br>
<em>Image Credit: <a href="https://www.flickr.com/photos/opensourceway/7496803264">opensourceway</a>.</em>

## Use Version Numbers

One common mistake made with open-source projects is neglecting to use version numbers. Version numbers are incredibly important for the long-term stability and maintenance of your project. CSS Lint didn’t use version numbers when it was first released, and I quickly realized the mistake. When bugs came in, I had no idea whether people were using the most recent version because there was no way for them to tell when the code was released. Bugs were being reported that had already been fixed, but there was no way for the end user to figure that out.

Stamping each release with an official version number puts a stake in the ground. When somebody files a bug, you can ask what version they are using and then check whether that bug has already been fixed. This greatly reduced the amount of time I spent with bug reports because I was able to quickly determine whether someone was using the most recent version.

Unless your project has been previously used and vetted, start the version number at 0.1.0 and go up incrementally with each release. With CSS Lint, we increased the second number for planned releases; so, 0.2.0 was the second planned release, 0.3.0 was the third and so on. If we needed to release a version in between planned releases in order to fix bugs, then we increased the third number. So, the second unplanned release after 0.2.0 was 0.2.2. Don’t get me wrong: there are no set rules on how to increase version numbers in a project, though there are a couple of resources worth looking at: <a href="https://apr.apache.org/versioning.html">Apache APR Versioning</a> and <a href="https://www.semver.org">Semantic Versioning</a>. Just pick something and stick with it.

In addition to helping with tracking, version numbers do a number of other great things for your project.</p>

### Tag Versions in Source Control

When you decide on a new release, use a source-control tag to mark the state of the code for that release. I started doing this for CSS Lint as soon as we started using version numbers. I didn’t think much of it until the first time I forgot to tag a release and a bug was filed by someone looking for that tag. It turns out that developers like to check out particular versions of code.

Tie the tag obviously to the version number by including the version number directly in the tag’s name. With CSS Lint, our tags are in the format of “v0.9.9.” This will make it very easy for anyone looking through tags to figure out what those tags mean — including you, because you’ll be able to better keep track of what changes have been made in each release.</p>

### Change Logs

Another benefit of versioning is in producing change logs. Change logs are important for communicating version differences to both end users and contributors. The added benefit of tagging versions and source control is that you can automatically generate change logs based on those tags. CSS Lint’s build system automatically creates a change log for each release that includes not just the commit message but also the contributor. In this way, the change log becomes a record not only of code changes, but also of contributions from the community.</p>

### Availability Announcements

Whenever a new version of the project is available, announce its availability somewhere. Whether you do this on a blog or on the mailing list (or in both places), formally announcing that a new version is available is very important. The announcement should include any major changes made in the code, as well as who has contributed those changes. Contributors tend to contribute more if they get some recognition for their work, so reward the people who have taken the time to contribute to your project by acknowledging their contribution.</p>

## Managing Contributions

Once you have everything set up, the next step is to figure out how you will accept contributions. Your contribution model can be as informal or formal as you’d like, depending on your goals. For a personal project, you might not have any formal contribution process. The developer guide would lay out what is necessary in order for the code to be merged into the repository and would state that as long as a submission follows that format, then the contribution will be accepted. For a larger project, you might want to have a more formal policy.

The first thing to look into is whether you will require a contributor license agreement (CLA). CLAs are used in many large open-source projects to protect the legal rights of the project. Every person who submits code to the project would need to fill out a CLA certifying that any contributed code is original work and that the copyright for that work is being turned over to the project. CLAs also give the project owner license to use the contribution as part of the project, and it warrants that the contributor isn’t knowingly including code to which someone else has a copyright, patent or other right. jQuery, <a href="https://yuilibrary.com/contribute/cla/">YUI</a> and <a href="https://dojofoundation.org/about/cla">Dojo</a> all require CLAs for code submissions. If you are considering requiring a CLA from contributors, then getting legal advice regarding it and your licensing structure would be worthwhile.

Next, you may want to establish a hierarchy of people working on the project. Open-source projects typically have three primary designations:

*   **Contributor**.  Anyone who has had source code merged into the repository is considered a contributor. The contributor cannot access the repository directly but has submitted patches that have been accepted.
*   **Committer**.  People who have direct access to the repository are committers. These people work on features and fix bugs regularly, and they submit code directly to the repository.
*   **Reviewer**.  The highest level of contributor, reviewers are commanders who also have directional impact on the project. Reviewers fulfill their title by reviewing submissions from contributors and committers, approving or denying patches, promoting or demoting committers, and generally running the project.

If you’re going to have a formal hierarchy such as this, you’ll need to draft a document that describes the role of each type of contributor and how one may be promoted through the ranks. YUI has just created a formal “<a href="https://github.com/yui/yui3/wiki/Contributor-Model">Contributor Model</a>,” along with excellent documentation on roles and responsibilities.

At the moment, CSS Lint doesn’t require a CLA and doesn’t have a formal contribution model in place, but everyone should consider it as their open-source project grows.</p>

## The Proof

It probably took us about six months from its initial release to get CSS Lint to the point of being a fully functioning open-source project. Since then, over a dozen contributors have submitted code that is now included in the project. While that number might seem small by the standard of a large open-source project, we take great pride in it. Getting one external contribution is easy; getting contributions over an extended period of time is difficult.

And we know that we’ve been doing something right because of the feedback we receive. Jonathan Klein recently took to the mailing list to ask some questions and ended up submitting a pull request that was accepted into the project. He then emailed me this feedback:
<blockquote>I just wanted to say that I think CSS Lint is a model open-source project — great documentation, easy to extend, clean code, fast replies on the mailing list and to pull requests, and easily customizable to fit any environment. Starting to do development on CSS Lint was as easy as reading a couple of wiki pages, and the fact that you explicitly called out the typical workflow of a change made the barrier to entry extremely low. I wish more open-source projects would follow suit and make it easy to contribute.</blockquote>

Getting emails like this has become commonplace for CSS Lint, and it can become the norm for your project, too, if you take the time to set up a sustainable eco-system. We all want our projects to succeed, and we want people to want to contribute to them. As Jonathan said, make the barrier to entry as low as possible and developers will find ways to help out.

{{< signature "al" >}}

