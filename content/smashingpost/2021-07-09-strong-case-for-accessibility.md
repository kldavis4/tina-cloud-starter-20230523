---
title: 'Making A Strong Case For Accessibility'
slug: strong-case-for-accessibility
author: todd-libby
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9c226eaa-3251-4d02-9ade-96a88ad759fc/strong-case-for-accessibility.jpg
date: 2021-07-09T10:30:00.000Z
summary: >-
  Accessibility is often overlooked or bolted on to the end of a project from the experiences in Todd’s career in web development and design. The case for accessibility is something we as people who create and build things for the web should be implementing and advocating for from the inception of a project to the release or handoff and beyond.
description: >-
  Accessibility is often overlooked or bolted on to the end of a project. Let’s figure out how to implement and advocate for accessibility from the inception of a project to the release or handoff and beyond.
categories:
  - Tools
  - Usability
  - Techniques
  - Accessibility
---

Imagine yourself as someone with a visual disability. Cataracts, or totally blind even. A site is not accessible because of many factors, willing and unwillingly. Accessibility may have been attended to at the end of the project or not in the budget, or maybe they just didn’t practice it. You can’t access the vital information on the site because it’s not accessible to people with visual disabilities.

Perhaps a person has arthritis, Multiple Sclerosis, or another form of motor skill disorder, and there is a part of the site that they cannot access because there is an issue that prevents them from obtaining that information they wish to on a site that they want to buy something on.

These are just a couple of **examples of what disabled users face daily** when they try and access a website that is inaccessible. The case for accessibility is this; we as stakeholders, managers, teams, designers and developers need to do better in not only practicing accessibility but advocating for it as well.

If you have ever read the [WebAIM Million](https://webaim.org/projects/million/) report, you can see where the breakdown is, and until 2021, there hasn’t been much in the way of improvement. Of the 1 million home pages that were tested, over 51 million errors were detected averaging 51.4 errors per page. While the number of errors decreased, home page complexity increased regarding the number of page elements that had detectable accessibility errors.

Inclusive design is a way of **creating digital products that are accessible to a wide range of people** regardless of who they are, disabled or not, where they are, and encapsulates a diverse spectrum of people. [The British Standards Institution (2005) defines inclusive design as](https://shop.bsigroup.com/upload/Download/30317424.pdf):

<blockquote>“The design of mainstream products and/or services that are accessible to, and usable by, as many people as reasonably possible ... without the need for special adaptation or specialized design.”</blockquote>

Practicing accessibility in your workflows and methodologies ensures people &mdash; disabled or not &mdash; that they can access your product, your website, and your brands. Inclusive design and accessibility go hand-in-hand. Let’s look at some examples of accessibility.

## Examples Of Practical Digital Accessibility

1. Your site has a color scheme that looks great after the designers are done with the mock-ups or the color scheme your brand uses is “perfect”’ in the eyes of people that do not have a visual disability. For people that have a visual disability like glaucoma, cataracts, or tritanopia (the deficiency of blue in one’s vision) they cannot make out that particular color and it does not meet [WCAG standards](https://www.w3.org/WAI/standards-guidelines/wcag/). 
2. If your light blue font color on a darker blue background did not meet those guidelines set in WCAG, then it would be inaccessible. If you switched to a lighter blue or white font within the [4.5 to 1 ratio guideline](https://www.w3.org/WAI/WCAG21/Understanding/contrast-minimum.html) that you can read about in [(Success Criterion 1.4.3: Contrast (Minimum))](https://www.w3.org/TR/WCAG21/#contrast-minimum), then it would meet the standard and be accessible to more people.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1db559d7-46a1-4ab1-881a-04d5876f0dd5/strong-case-for-accessibility-1.webp" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1db559d7-46a1-4ab1-881a-04d5876f0dd5/strong-case-for-accessibility-1.webp" width="499" height="225" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1db559d7-46a1-4ab1-881a-04d5876f0dd5/strong-case-for-accessibility-1.webp'>See large preview</a>)" alt="lighter blue and white font placed on darker blue background color" >}}

3. You have a site that does not traverse well (or at all) when disabled users use assistive technologies such as a screen reader, keyboard, or voice recognition to navigate around the site because they lack the motor skills or dexterity to do so. An accessible site makes sure there is a way for those users to navigate through the site with no issues. Examples of keyboard navigation [can be seen in this video](https://youtu.be/FvpUNiB-2T0) and in [this short video about voice recognition](https://youtu.be/7RHG_XiQ0ck).
4. An accordion component with information that creates content that is not scrollable. It is inaccessible to people that use the keyboard for navigation. Make sure that the content is accessible by keyboard in that instance.
5. Using alternative text to describe the information in a picture for Blind users. [Images that do not have alternative text that describes to screen reader users what the picture conveys](https://www.smashingmagazine.com/2021/06/img-alt-attribute-alternate-description-decorative/) are a barrier to blind people, e.g.

<pre><code class="language-markup">&lt;img src="" alt="This is my favorite kind of animal, a Maine Coon cat."&gt;
</code></pre>
6. Users of newer technologies, people that live in metropolitan areas, or people that can afford to buy the latest tech, for example, have fewer barriers to break through than people that cannot afford a new phone or tablet, or are in very remote or rural areas.
7. The glare of the sun on your mobile device as you’re on the beach on a sunny day. You’re shielding the screen or squinting to see the screen to read what restaurant to go to after you’re day at the beach is done. That is a situational impairment.
8. A fussy child on your lap moving around while you are trying to read an email or an injured arm as you try to answer an email, hindering your ability to type as you normally would is a situational impairment.

There are *a lot* more examples of accessibility I could mention but that would take a very long time to write, so these are just a few examples.

## Actionable Steps To Get Buy-In

Two of the most widely used reasons I hear as to why people or companies aren’t practicing accessibility are:

- “The client has no budget for it.”
- “My manager said we’ll get to it after launch.”

## Buy-In And Support From Executives/Stakeholders

From the outset, advocating for accessibility starts at the top. Once you have stakeholder support, then you may see support trickle down to managers, then teams, and then individuals. It all starts with you first. Buy-in and support from executives will continuously be successful across the organization. 

When the ethical approach doesn’t work, the approach I will take is the financial approach:

<blockquote>“You’ll be saving the company a lot of money when you do this from the start. When maintenance is needed, it won’t take the team as long to maintain the code because of accessibility and clean code.”</blockquote>

When, or if that fails, I’ll go for the legal ramifications and cite instances from the lawsuits that have been won against Target, Bank of America, Domino’s Pizza, and others. It’s amazing to see how fast executives and stakeholders do not want to get sued.

Keeping executives engaged and meeting with them regularly will ensure success with your accessibility initiatives, but will also provide support for when new accessibility initiatives need to be implemented or when there are disagreements among teams on the implementation or prioritization, you have the support of executives. 

Being accessible is a good way for a company to differentiate itself from other companies, when you make a quality product, then the company buy-in becomes greater in some instances. Teams that push for accessibility usually lead the way to getting buy-in from other departments and executives. If the product is high quality and makes the company money, that’s when the company is swayed to adopt the practice.

Demonstrations of **live testing with disabled users** are also another way to get buy-in across the board. To humanize the decision-making process and get executives and colleagues on board by showing them when design choices do not meet user needs by disabled users using inaccessible products. Or one that I have used in the past, don’t ask, just do it.

Most of the time, however, it is how the practice of accessibility can make the company money or the legal consequences that a company can face, that sways an executive to adopt the practice. Then, in those instances, is when an executive or stakeholder starts learning about accessibility if they want to invest in that time.

Coordinating efforts across departments may be difficult and time-consuming at first so that support from the top will help alleviate the pressures and burnout that can happen when taking on the task of creating and implementing an accessibility strategy.

{{% ad-panel-leaderboard %}}

## Have A Team Or Individual Who Is Your Accessibility Advocate(s)

Once you have buy-in from executives or stakeholders, having a person throughout each department or a team focused on accessibility. Throughout each department have an individual who is the liaison regarding accessibility. 

Have someone that can answer questions and work with others to practice the guidelines and work with others to make accessible products. Help set up documentation and tooling, serve as an intermediary between departments.

## Assess the Product and Proficiency Within the Company

Gauging the point where the product(s) are as far as how inclusive and accessible they are is a key priority. This ensures the team or individual that their efforts to make the product better and accessible are happening. What is the current state of the product? What is the current state of the website or mobile application?

Getting the general idea of the level of knowledge that teams and people in the company currently have is important going forward. How versed are they in accessibility guidelines and practices? Do they know anything about the Web Content Accessibility Guidelines (WCAG)? How much training do you have and will you need?

Maintaining a **written record of all accessibility training done** to meet the requirements that apply to your organization is a great way to keep data on all the training done within the organization. Recording the training and who and when it was completed. If there is no inter-organizational accessibility training available your organization can look into different methods of training like the kind [WebAIM](https://webaim.org/services/training/), [the ADA](https://www.adaanniversary.org/training), or [Knowbility](https://knowbility.org/services/training) has to offer.

## Establish Guidelines For The Company

Consistent implementation of the product greatly benefits the organization. It reduces the amount of work, which in turn can reduce the number of stress teams are under. **Design systems** should be used not only to ensure branding and consistency, but accessibility, inclusivity, and understanding of code better.

[Accessible components](https://www.smashingmagazine.com/2021/03/complete-guide-accessible-front-end-components/) help for obvious reasons and reduces the time it takes to implement, rather than start from nothing and try to re-invent something that has already been done. Testing procedures should be implemented so that departments do their jobs well and do them efficiently, especially QA and developers.

**Documenting guidelines** for your organization is as simple as creating a set of accessibility guidelines. You could internally document them in a collaborative software such as Notion or Dynalist; or an online documentation like Google Docs or Dropbox Paper. Somewhere that has a collaborative aspect where people can add to the documentation that the organization has.

{{% feature-panel %}}
## Getting Fellow Colleagues To Buy-In

In this landscape of frameworks and libraries, “going fast and breaking things”, and overlooking and undervaluing accessibility, people need to be educated and that also needs to happen at the team level. The people that do not have voices, the “people on the other side of the glass” need **YOU** to be their voice.

As a freelancer, setting up meetings or training sessions to onboard organization members that you may be working with can be beneficial to all. Holding a workshop or webinar is also an option to training colleagues to buy-in as well. 

Getting a team onboard because training brings the team together and people **know the importance of accessibility**, and they want to produce a quality product that people can use regardless of disability.

Pitching to those who do not or may not know that accessibility means less time spent working on what they work on, less stress and headaches, can sway a developer very fast from my experience.

## Sharing The Importance Of The Rules

Whether you live in the EU, the UK, Canada, or the United States, most countries have rules regarding standards for accessibility. Familiarity with those rules and guidelines only ensures compliance on another level. 

Whether it is the [ADA (American Disabilities Act)](https://www.dol.gov/general/topic/disability/ada) or [Section 508 (Government compliance)](https://section508.gov/) in the U.S., the [ACT (Accessible Canada Act)](https://laws-lois.justice.gc.ca/eng/acts/A-0.6/page-1.html) in Canada, or [EN 301 549](https://www.etsi.org/deliver/etsi_EN/301500_301599/301549/02.01.02_60/en_301549v020102p.pdf) in the EU, sharing the importance of the guidelines can be crucial to getting departments, executives, and the organization as a whole on board.

## Pick Examples From The Outside World As Use Cases

Test and record cases where a disabled user is trying to use the product, website, or mobile app. Showing colleagues and executives these tests and use cases will bolster the argument you have for implementing accessibility at your organization.

From there, you could get a source outside the organization that specializes in accessibility testing with disabled users, such as [Applause](https://www.applause.com/), for instance. The organization and people within may turn around and embrace accessibility at the company and in the workflow.

{{% ad-panel-leaderboard %}}

## Hire Disabled People

Whether it is internally or on a contract basis with an outside firm like Applause, there are the people with the lived experiences. They can benefit you and your company and team by having them aboard. These folks bring value to you and the organization.

Get executives and hiring managers on board to bring on people with disabilities to not only help with accessibility, but also teach and advocate for accessibility and inclusivity within the organization. 

## Best Practices For Maintaining Accessibility

Accessibility does not end at handoff or when the project is “finished” as is with the web, accessibility is ever-evolving and needs periodic checking when new features are implemented or changes are made to see if accessibility is still be practiced and adhered to.

Vigilance of the accessibility of the product(s) ensures a standard of accessibility. Automated testing of the product wherever possible that fits the strategy of the departments when it comes time to release new features or changes.

Any barriers that may arise (and they will) will be addressed and they can be handled in a manner that expedites the process and rolls out fixes for those barriers that take them down and makes the product accessible for those who need it.

Performing **screen reader analysis** before every release to ensure that users of screen readers and other assistive technologies can use the website or mobile app.

Annual audits and user testing is always important whether made internally by a team, or a third-party that specializes in accessibility auditing, especially with user testing by disabled users. What does that audit entail?

- An executive summary for stakeholders that details the needs of the product so that it can become compliant as well as addressing the current state of affairs as well.
- A developer report that details every possible path that can be taken through the website, mobile app, and product that addresses concerns and needs that will be encountered along the way.

## Summary

Accessibility matters. It matters to those who are getting shut out on a daily basis from some form of digital creation they encounter. Whether it is by design or not, the fact that accessibility is an afterthought in most cases is a critical oversight we all have to correct. 

Accessibility and accessible sites and apps make the web better, they make everyone feel included no matter what situation or disability. **Inclusion and accessibility remove barriers** for disabled people and accessibility and performance also make the web accessible for those that aren’t equipped with the latest and greatest phones or devices.

Getting on board with accessibility is something we should all do. Let’s remember the people on the other side of the glass. Accessibility is a right, not a privilege. Let’s make accessibility a priority.

{{< signature "vf, il" >}}
