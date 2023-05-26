---
title: 'How To Bake Layers Of Accessibility Testing Into Your Process'
slug: bake-layers-accessibility-testing-process
author: katekalcevich-mikegifford
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/908a72e9-3b82-484e-8256-e4e324a6afcb/dc-videocall-dfa8cdd8.png
date: 2021-04-26T11:00:00.000Z
summary: >-
  Accessibility experts Kate Kalcevich and Mike Gifford introduce readers to "layered accessibility testing”, a practice of using a variety of tools and approaches at different stages in the digital product lifecycle to catch accessibility issues early &mdash; when it’s easier and cheaper to fix them. 
description: >-
  Accessibility experts Kate Kalcevich and Mike Gifford introduce readers to "layered accessibility testing”, a practice of using a variety of tools and approaches at different stages in the digital product lifecycle to catch accessibility issues early &mdash; when it’s easier and cheaper to fix them. 
categories:
  - UI
  - Testing
  - Usability
  - Accessibility
---

When building websites or apps, accessibility testing is critical to ensure that what you build will work for all your users. This includes users with disabilities and also people with temporary and situational limitations (like that coworker who broke their arm skiing or the customer who is outdoors on their phone with glare on the screen). 

We’re going to share how to "layer" accessibility testing by using a variety of tools and approaches at different stages in the digital product lifecycle to catch accessibility issues early &mdash; when it’s easier and cheaper to fix them. Taking **a layered approach to testing** your site for accessibility also improves the usability of your site &mdash; which in turn increases your customer base and reduces customer service inquiries. It can both make and save you money.

We’ll use a layered cake analogy to talk about the different layers of accessibility testing and when to use them. [Food analogies](https://www.lflegal.com/2020/05/accessibility-is-delicious/) have become quite popular in the accessibility world! 

{{< rimg href="https://affecttheverb.com/collection/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b476fd4b-d154-41f3-a167-f9725e009857/dah-kitchen06.jpeg" width="800" height="543" sizes="100vw" caption="(Image credit: <a href='https://affecttheverb.com/collection/'>Dana Chan for Disabled And Here</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b476fd4b-d154-41f3-a167-f9725e009857/dah-kitchen06.jpeg'>Large preview</a>)" alt="A picture of three people gathered in a kitchen preparing and tasting food" >}}

This approach has worked well for both of us. Mike is a seasoned accessibility advocate and senior strategist at a government technology firm ([CivicActions](https://civicactions.com/)), and Kate is the Head of Services at an accessibility testing platform ([Fable](https://makeitfable.com/)).

While Mike looks at **accessibility testing** from a more technical angle early in the development phase and scanning for compliance on live sites, Kate focuses on the **user experience**. Both of us realized that combining many types of accessibility testing throughout the product development life cycle is a powerful way to improve overall product accessibility. In this article, we’ll share some of the things we’ve learned.

Most organizations approach accessibility in three main ways:

<ol>
	<li><strong>Running tools to check your code and/or user interface.</strong><br />This is often referred to as “<a href="https://accessibility.blog.gov.uk/2017/02/24/what-we-found-when-we-tested-tools-on-the-worlds-least-accessible-webpage/">automated testing</a>” because you use software to automatically test many accessibility issues at once.</li>
	<li><strong>Using your computer in a way that is different than you normally do.</strong><br />For example, by <a href="https://www.w3.org/WAI/test-evaluate/preliminary/#interaction">not using a mouse</a>, <a href="https://www.boia.org/blog/give-yourself-an-accessibility-test-zoom-your-page-to-200">zooming your browser to 200%</a>), or <a href="https://support.microsoft.com/en-us/windows/use-high-contrast-mode-in-windows-10-fedc744c-90ac-69df-aed5-c8a90125e696">switching to Windows high contrast mode</a>.   

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/35831339-5455-42d7-9488-fb9010fcdf25/image3bake-layers-accessibility-testing-process.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/35831339-5455-42d7-9488-fb9010fcdf25/image3bake-layers-accessibility-testing-process.png" width="800" height="454" sizes="100vw" caption="The high contrast mode asks you to select a specific colored rectangle to customize high contrast colors. (Image credit: <a href='https://support.microsoft.com/en-us/windows/use-high-contrast-mode-in-windows-10-fedc744c-90ac-69df-aed5-c8a90125e696'>Microsoft</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/35831339-5455-42d7-9488-fb9010fcdf25/image3bake-layers-accessibility-testing-process.png'>Large preview</a>)" alt="An image from Microsoft showing how high contrast colors shift for white, yellow, green, and blue" >}}
</li>
<li><strong>Using assistive technology and users with disabilities to check for usability issues.</strong><br />This is often referred to as “<a href="https://www.smashingmagazine.com/2018/09/importance-manual-accessibility-testing/">manual testing</a>” because it requires a person to evaluate accessibility issues.</li>
</ol>

Far too many organizations rely exclusively on a single accessibility solution to validate their site. No one tool or process can give an organization the confidence that they are actually meeting the needs of the greatest possible number of people.

{{% feature-panel %}}

## How To Secure Buy-In For Accessibility

In many organizations, in order to do accessibility testing, you’ll need executives to prioritize and support the work. Here are tips on how to make that happen if you don’t already have buy-in for accessibility:

- **Check if there is a legal requirement for your organization to be accessible.**  
“Accessibility Act” and “Disability Act” are search terms that should pull up relevant laws in most countries. Sharing the legal risk can be the right incentive for some organizations.
- **Find out what your competitors are doing.**  
Check for an accessibility statement on their websites. Most organizations are keen to stay ahead of the competition and knowing that others are prioritizing accessibility could do the trick.
- **Connect with customer service to find out if there are accessibility complaints.**  
If possible, reach out to customers directly to hear about their experiences and share those stories with company leaders. Hearing about dissatisfied customers can be a huge motivator. If you can get permission from the customers, record a demo of them facing challenges with your products. A video like that can be very compelling.
- **Explain the financial costs and rewards.**  
Many companies think they can’t afford to do accessibility, but it’s much more affordable when it’s integrated into the day-to-day work and not an afterthought. There’s also the potential revenue from people with disabilities &mdash; globally they represent more than [3 trillion dollars in disposable income](https://rod-group.com/sites/default/files/Summary%20Report%20-%20The%20Global%20Economics%20of%20Disability%202020.pdf).

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/737e4887-b8ae-4126-a219-c3f50a7818c3/1-bake-layers-accessibility-testing-process.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/737e4887-b8ae-4126-a219-c3f50a7818c3/1-bake-layers-accessibility-testing-process.png" width="800" height="346" sizes="100vw" caption="A chart from a report summary of the Global Economics of Disability (Image credit: Rich Donovan) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/737e4887-b8ae-4126-a219-c3f50a7818c3/1-bake-layers-accessibility-testing-process.png'>Large preview</a>)" alt="A chart from a report summary of the Global Economics of Disability. It shows a y-axis of opportunity and an x-axis of market size/population. In a diagonal line up the graph, it shows increasingly larger clusters of 1)  people with disabilities as having 29 percent visible disabilities and 2) 71 percent having non-visible disabilities including sensory, cognitive, and chronic. 3) friends and family who are EvangelistsReady to act and ‘preach’ to others about the value inherent in People with Disabilities. 5) Broader Market: Everyone benefits from innovations and insights derived from disability. Design for All equals to Scale" >}}

- **Find the right champion.**  
Chances are there’s already someone at the highest levels of the organization who cares about people and doing the right thing. This may be a Diversity and Inclusion lead, someone fighting for environmental sustainability, or other issues. Perhaps it’s someone with a disabled friend or family member. Making them aware of accessibility may be all that’s needed to add a new focus to their efforts.

## Gathering Your Ingredients

Accessibility should be baked into your process as early as possible. One place to start is with the procurement process. You can incorporate accessibility as part of the review process for any technology systems you are buying or building. DisabilityIN has some excellent resources on [accessible IT procurement](https://private.disabilityin.org/procurementtoolkit/).  

Looking for vendor accessibility statements or VPATs for products can help, but so can doing a quick review with some of the tools mentioned in the recipe below. Not all software is created equally, so you want to be sure you’re working with vendors who are actively contributing to **tools and processes that help you prioritize accessibility** from the start.   

Another way to bake in accessibility early, if you’re creating or updating a design system, is to choose a component library that has been built with accessibility in mind. Look for libraries with a clear accessibility statement and an open issue queue that allows you to review problems. 

Examples:

*   The Angular Components team has built accessibility into the **Material UI library**. For example, the [radio button component](https://material.angular.io/components/radio/overview) uses a radio group with an aria-label. Each radio button reads as checked or not checked to a screen reader user, the buttons can be selected using the arrow keys like standard HTML radio buttons, and the focused state is clearly visible.
*   **Reakit for React** describes an [accessibility warning feature](https://reakit.io/docs/accessibility/) on their accessibility page that will tell developers when an aria-label is needed.
*   The **Lion accessible web components library** uses an a11y label to tag [accessibility issues in GitHub](https://github.com/ing-bank/lion/issues?q=is%3Aissue+is%3Aopen+label%3Aa11y) so you can see what’s being improved and open your own issue if needed.

Another way to embed accessibility into your process is to update one of the personas your team uses to include disabilities. Many people have more than one disability, so creating at least one persona with several disabilities will ensure you keep that audience top-of-mind in all your early design work.

{{< rimg href="https://affecttheverb.com/collection/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/908a72e9-3b82-484e-8256-e4e324a6afcb/dc-videocall-dfa8cdd8.png" width="800" height="600" sizes="100vw" caption="(Image credit: <a href='https://affecttheverb.com/collection/'>Disabled And Here</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/908a72e9-3b82-484e-8256-e4e324a6afcb/dc-videocall-dfa8cdd8.png'>Large preview</a>)" alt="An illustration of a disabled person using a laptop to connect with other folks online" >}}

To flesh out that persona, **talk to people with real disabilities** &mdash; including temporary and situational limitations &mdash; to help you understand how they use technology, sites, and apps in the real world. One in five people have a permanent disability, but 100% of the population will be faced with vision, hearing, motion, or cognitive disabilities at some point in their lives. Our personas can reflect: 

*   people with allergies, insomnia, or broken bones; 
*   people using outdated technology or using their computers outside; or even 
*   people who change their technology use according to their location (for example, disabling images when they need to save internet bandwidth).

Little changes like these can have a big impact on how your team thinks. One way to pitch this change to leadership and teams is to talk about how it will **make your personas more reflective** of your actual users &mdash; which is the whole point of personas. They must be realistic.

One of the most impactful ways to involve people with disabilities is to have them help co-design services and products. Australia has a free [training toolkit](https://www.pwdwa.org/documents/connect_with_me/co-design-toolkit/index.htm) on how to do co-design with people with disabilities. There’s also a great [case study](https://medium.com/swlh/running-inclusive-research-sessions-beyond-wheelchairs-and-screen-readers-488362c7103d) on how one company ran co-design sessions with people with learning disabilities on behalf of the UK government.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/63b8cdf6-2fd5-45d9-9df9-51c41fa40aef/image2bake-layers-accessibility-testing-process.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/63b8cdf6-2fd5-45d9-9df9-51c41fa40aef/image2bake-layers-accessibility-testing-process.png" width="700" height="525" sizes="100vw" caption="Group research activity (adapted usability testing) (Image credit: <a href='https://medium.com/swlh/running-inclusive-research-sessions-beyond-wheelchairs-and-screen-readers-488362c7103d'>Vita Mangan</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/63b8cdf6-2fd5-45d9-9df9-51c41fa40aef/image2bake-layers-accessibility-testing-process.pngs'>Large preview</a>)" alt="People holding up a red or a green card to tell the facilitator how they got on with the task" >}}

## Legacy IT

Whether we like it or not, most of the decisions about organizational IT were made months (if not years) ago. Even when you are in the heat of a procurement process, accessibility is typically just one of many considerations. This is to be expected &mdash; even in organizations that are passionate about accessibility. 

With legacy technology, the first step is simply to **raise awareness** with the vendor or team about the importance of accessibility. If you can detail accessibility issues that you want to be fixed using automated tools, it can help adjust how a vendor ranks their issue queue. There isn’t always a community portal to post concerns like this, but there might be a community on Twitter or Reddit where you could bring issues to light. 

Additionally, there might be a customizable theme that could be adjusted to address some of the concerns. Some solutions may offer an Application Programming Interface (API) that would allow a developer to build an accessible user interface around it. 

If a vendor has competitors, it can be useful to **highlight the accessibility features** that are included in that product. It can be beneficial to remind vendors that you do have options. 

If legacy IT is an internally built product, a good way to quickly evaluate it is using the keyboard only. If you can’t use the product with a keyboard (for example, there’s no visible focus or the UI is only mouse clickable), it’s likely going to be a lot of effort to improve the accessibility of the product. 

Consider offering **alternative ways to access the service** (e.g. phone support, in-person service, or email) so that people who can’t access the product digitally because of accessibility barriers can still get what they need. 

Think about the organizational roadmap and when it might be feasible to upgrade or retire the product and weigh the cost and effort of accessibility against that. If you have other, newer products that aren’t accessible, it might be more productive to focus your efforts on those products if a legacy tool is nearing the end of life.

{{% ad-panel-leaderboard %}}

## The Recipe

Here is an example of a comprehensive accessibility testing approach, with five layers for a really delicious accessibility testing cake. Figure out what your budget is going to be and then price out all the various testing approaches. Some are free, others will cost money. In the next section, we provide advice on where to start if all these layers of testing won’t fit in your budget.

1. **Research User Needs**  
Ensure the questionnaire that you use to screen potential research participants asks about assistive technology use. This will make it easy to integrate people with disabilities into your existing research process at no extra cost. If you don’t have luck finding participants this way, try reaching out to disability organizations.  
	
	You can also modify your existing user personas to include users with disabilities. You can borrow aspects of [user profiles from Gov.UK](https://www.gov.uk/government/publications/understanding-disabilities-and-impairments-user-profiles) if you need to do this quickly and cheaply. If you have the budget for it, add people with disabilities into prototype and design reviews. This may be easiest to do if you engage a vendor that offers this type of service, hence the need for a budget. Alternatively, you can pay participants directly.
2. **Refine Your Process**  
Encourage developers, designers, and content authors to include accessibility checks as part of their process. Here are ways to do that using free automated testing tools:  
	- Download free browser extensions/plug-ins to do page specific testing for design reviews ([WAVE](https://wave.webaim.org/) or [Accessibility Insights](https://accessibilityinsights.io/en/downloads/))
	- If you use continuous integration testing as part of the build pipeline for developers, make sure you are evaluating accessibility (there are free open-source tools for this like [Axe Core](https://github.com/dequelabs/axe-core#axe-core)  and [Pa11y](https://pa11y.org/))
	- Give content authors tools in the WYSIWYG interface to identify barriers that they have added ([HTML Code Sniffer](https://squizlabs.github.io/HTML_CodeSniffer/))
	- Ensure you are crawling your site regularly to catch accessibility issues. If possible, run crawlers in both staging and production environments ([Purple Hats](https://github.com/GovTechSG/purple-hats#purple-hats) is a free open source option)
3. **Manual QA**  
You don’t have to add extra people to do QA, just integrate it into your existing process. If you only do one thing, then stop using the mouse during your regular QA. You’ll catch accessibility bugs along with other functional bugs. If you want to do more, test with screen readers, and magnifiers too.  
	
	Here are various ways you can do manual accessibility QA without purchasing any tools:  
	- Can you access your site without your mouse? Use simple keyboard-only manual testing to evaluate new components and content. 
	- Browse your site with magnification set to 200% or greater using the built-in magnification tools in your browser (<kbd>Ctrl</kbd> + <kbd>+</kbd>). 
	- Flip your browser or OS to dark mode and see if your site works well for people with light sensitivity. 
	- Perform sprint-level testing with developers and designers using assistive technology (VoiceOver, Microsoft Narrator, and NVDA are free options).
4. **User Testing**  
In large corporate environments with a dedicated budget for accessibility, you can pay assistive technology users to test functionality on your staging environment before launch.  
	
	Nothing gives you greater certainty that your product will work for people with disabilities than validating with users. Not even a perfect WCAG compliance score can give you that assurance the way a real person using the product can.  
	
	People with disabilities are often asked to do work for free, which is problematic as many with disabilities are already at an economic disadvantage. If you’re working on a personal project and there’s no budget, look at your network and see if there are people who would be interested in helping in exchange for an equivalent favor. 
5. **Specialist Review**  
If your organization has an accessibility team, have them do User Acceptance Testing pre-release. This is where you can get detailed feedback on WCAG compliance that you may have missed in earlier steps.  
	
	Think of it as a final check; your accessibility team isn’t doing all of the work on accessibility, everyone has a role to play. Accessibility teams are most effective when they set standards, provide training, give guidance and evaluate compliance. They support accessibility efforts but aren’t the only ones doing accessibility work. That way no one person or team becomes a bottleneck.  
	
	If you don’t have a team, you can hire accessibility professionals to do the reviews prior to release.

## Where To Start

Start where you are. The goal isn’t perfection, but ongoing improvement. Implementing all layers at once doesn’t have to be the goal. Rather, it’s about starting with one or two layers and then gradually adding more layers as your team gets better at accessibility testing. A small slice of cake is better than no cake.

### Individuals

*   If you are new to accessibility, start by adding a free browser extension to find accessibility issues and start by learning how to fix the errors that are displayed. WebAIM’s WAVE Toolbar is great for this.
*   Start sharing accessibility information that you have found useful. This could be just on Twitter or Reddit, but you could also start a newsletter to help raise awareness. 
*   Sign up for webinars or events focused on accessibility so that you can learn more. 

### Teams

*   A team with a strong user-centered design approach might want to start with layer one: interviewing people with disabilities as part of user research.
*   A team with a strong IT compliance process might invest in tighter integration of automated testing in their continuous integration process or a site-wide crawler first.
*   Find ways to incorporate accessibility earlier in the design/development process. 

### Organizations

*   Make sure you have meaningful accessibility statements which reflect your organization’s commitment to remove barriers to people with disabilities.
*   Build a champions network that allows a community of practice to grow and learn from each other. 

{{% ad-panel-leaderboard %}}

## Limitations Of Automated Tools

Every baker needs to have an arsenal of tools they can rely on. There are proprietary accessibility tools worth considering, but there are also excellent open-source tools including the ones we mentioned in the “recipe” above that are available for free. 

In modern dynamic sites, it is important to **use automated tools to catch accessibility errors early** before they are published to the live site. It’s also important to crawl the site to see that all the pages still comply after they’ve been published and continuously updated. 

The challenge is that designers and developers often assume that if the tests don’t report any errors, a site is good. When you give people a test, people tend to write towards it. Unfortunately, many designers and developers stop when they eliminate the errors that they see with WAVE or Axe.

To be clear, it is a small fraction of teams that even do this, but if we want to make sites that are perceivable, operable, and understandable for more people using different types of technology, we have to do better. 

Automated tools are great but limited. Even the best available automated tools only catch about [30 to 40% of WCAG compliance accessibility errors](https://alphagov.github.io/accessibility-tool-audit/index.html). An automated tool can tell you if an image is missing an alternative description, but what it can’t tell you is if the description is entirely inaccurate or used in the wrong context and therefore useless. That still requires a person to evaluate.

To get past these limits, it’s important to recognize that **accessibility doesn’t automatically mean usability** for people with disabilities. Think of accessibility as the lowest bar; it works with assistive technology, but to go beyond “it works” to “it’s enjoyable and easy to use” you’ll need to test with real users.

Many organizations already do usability testing, but most don’t include people with disabilities. If you’re having trouble recruiting more diverse participants, consider working with an organization that has a community of assistive technology users and a platform to make testing quick and easy.

## Let’s Get Baking!

Use a layered accessibility testing approach when you are working to build an inclusive website. Don’t rely on just one type of testing to find barriers for people with disabilities.

- Test your ideas with assistive technology users early in the process
- Integrate regular automated code checks into the process of building the site
- Do manual testing using assistive technology as part of QA
- Test with people with disabilities prior to launch
- Perform comprehensive accessibility reviews on staging

{{< rimg href="https://www.freepik.com/free-photo/gourmet-dessert-celebration-decoration-food-velvet_1254667.htm#page=1&query=cake%20topntp26&position=3" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/73f0ac6a-18e0-46fc-836b-2059a49acb5d/gourmet-dessert-cake.jpeg" width="800" height="534" sizes="100vw" caption="A layered approach to testing your site for accessibility improves the usability of your site and should be baked into your process as early as possible. (Image credit: <a href='https://www.freepik.com/free-photo/gourmet-dessert-celebration-decoration-food-velvet_1254667.htm#page=1&query=cake%20topntp26&position=3'>topntp26</a>)" alt="A colorful layered cake with five colors from top to bottom: red, orange, yellow, blue and purple - covered in white and red frosting" >}}

Remember the goal isn’t to score high in a testing tool, or even to meet a WCAG guideline, but rather to make your content more widely available, including to assistive technology users.

Ultimately, accessibility statements are the icing on the cake. Include an [accessibility statement](https://medium.com/civicactions/whitehouse-gov-makes-an-accessibility-statement-5de37580209) with contact information on your site to provide a feedback loop. Your users are the experts and everyone should be part of making a site better over time.

{{< signature "vf, il" >}}
