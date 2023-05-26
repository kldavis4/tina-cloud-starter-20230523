---
title: User Interfaces In Business Web Application Design
slug: designing-user-interfaces-for-business-web-applications
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1cd4faad-2559-4421-98ec-5cd486d5d07c/apple-keyboard-illu88.jpg
date: 2010-02-25T13:55:15.000Z
author: janko-jovanovic
summary: >-
  Despite the difficulties when designing business web applications, the job is interesting, and you learn many new things on each project that influence the way you design websites. It is based on compromises between client and user needs, business requirements and users, novice and expert users, functionality and simplicity, and so much more. In this article, Janko Jovanovic explains the different approaches, techniques and principles you can use when working on any business web application.
description: >-
  In this article, Janko Jovanovic explains the different approaches, techniques and principles you can use when working on business web applications.
categories:
  - UX
  - Web Design
  - UI
---
Business web application design is too often neglected. I see a lot of applications that don't meet the needs of either businesses or users and thus contribute to a loss of profit and poor user experience. It even happens that designers are not involved in the process of creating applications at all, putting all of the responsibility on the shoulders of developers.

This is a tough task for developers, who may have plenty of back-end and front-end development experience but limited knowledge of design. This results in unsatisfied customers, frustrated users and failed projects.

So, we will cover the basics of user interface design for business Web applications. While one could apply many approaches, techniques and principles to UI design in general, our focus here will be on <em>business</em> Web applications.

### <span class="rh">Further Reading</span> on SmashingMag:

*   [40+ Helpful Resources On User Interface Design Patterns](https://www.smashingmagazine.com/2009/06/40-helpful-resources-on-user-interface-design-patterns/)
*   [Lean UX: Getting Out Of The Deliverables Business](https://www.smashingmagazine.com/2011/03/lean-ux-getting-out-of-the-deliverables-business/)
*   [45 Incredibly Useful Web Design Checklists and Questionnaires](https://www.smashingmagazine.com/2009/06/45-incredibly-useful-web-design-checklists-and-questionnaires/)
*   [Taking Pattern Libraries To The Next Level](https://www.smashingmagazine.com/taking-pattern-libraries-next-level/)

{{% feature-panel %}}

## Webdesign vs. Web Application Design

Confusing Web applications and websites is easy, as is confusing user interface design and website design. But they are different both in essence and in so many other ways, which we'll explore in this article.

A website is a collection of pages consisting mostly of static content, images and video, with limited interactive functionality (i.e. except for the contact form and search functionality). <strong>The primary role of a website is to inform</strong>. Some websites use content management systems to render dynamic content, but their nature is still informational.

<figure><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="30402" title="Website vs. web application" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5abfa137-ea3a-4e25-a814-f5b2a336c504/website-webapp.jpg" alt="Website vs. web application" width="500" height="299" /><figcaption>CampaignMonitor is powerful email marketing software, while Jeff Sarimento's website is intended to inform readers about his life and work.</figcaption></figure>

Web applications, on the other hand, are <strong>dynamic, interactive systems</strong> that help businesses perform business critical tasks and that increase and measure their productivity. Thus, the primary role of a Web application is to perform a function that serves the user's tasks and according to defined business rules.

Web applications require a higher level of involvement and knowledge of the system on the part of the user. They don't just stumble upon the application, do their work and bounce off. They use it as a tool to perform critical business tasks in their daily work. In the end, they cannot easily discontinue using the application and switch to another if they don't like how it's working, as is the case with websites.

### Different Types of Web Applications

Business applications range in type from invoicing for freelancers to content management systems to document management systems to banking and financial systems.

We can distinguish between <strong>open and closed applications</strong>. Open systems are online applications that are easily accessible to anyone who opens an account. Users can access such applications via the Web and can open an account for free or by paying a fee. Closed systems (or line-of-business applications) are usually not accessible outside the company that uses it, and they can be considered “offline” applications (though many systems expose their functionality to business partners via either services or specialized interfaces). Such systems usually run on the company's local network and are available only to employees.

I don't know who coined it, but one term I like especially is <strong>weblication</strong>, which describes what a Web application is in general. This doesn't mean, though that a Web application is a half-website half-application hybrid. It is far more complex that that.

## First, Know Your Users

You've probably heard this a thousand times, and for good reason. A successful user interface focuses on users and their tasks. This is key, and too many developers have failed to create a good user experience. As Steve Krug said, "Developers like complexity; they enjoy discovering how something works."

<figure><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="30500" title="users" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/03786fe3-9aa7-4834-9175-29a8d6dbd1bc/users1.jpg" alt="users" width="500" height="352" /></figure>

When identifying your users, keep in mind that <a href="https://52weeksofux.com/post/385981879/you-are-not-your-user">clients are not users, and you are not a user</a>. Although a client's management team will usually be interested in the project and try to influence decisions, remember that they won't be sitting in front of the computer several hours a day (unless the application is specifically for them).

### How to Identify Users?

Identifying users can be done using several techniques, such as user interviews, business stakeholder interviews and the “shadowing” method of observation. Interviews can give you answers to questions about the users' knowledge of the system and computers in general, while shadowing can yield more detailed information about how users perform tasks and what errors they make. The method is called shadowing because the observer is like a shadow, watching and noting the steps a user takes.

If you don't have access to real users—either because you don't have permission or are designing for open application—you can use personas, a tool to help identify users. Personas are a representation of real users, including their habits, goals and motivation. Because certain information about users is often identified through business analysis, you can make use of it to create personas. If you are not familiar with the tool, a comic by Brad Colbow will help.

<figure><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="30489" title="personas" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/937cce34-92a6-4b4e-9bca-b2222267481d/personas.jpg" alt="personas" width="469" height="203" /></figure>

Task analysis helps identify what tasks users perform in their jobs, how they do them, how long they take and what errors they make. Sometimes clients will be using an old version of the application that you are designing to replace. Make use of that old system and watch how users use it. Understanding their tasks and challenges will be easier that way.

Regardless of who your users are, one thing is certain: in most cases, you will have to consider both <strong>novices and experts</strong>. Novice users should be enabled to learn as fast as possible, while expert users should be enabled to perform their tasks extremely efficiently. This may mean creating separate interfaces. But in many cases you will be able to accommodate both types of users in the same interface through various techniques, such as progressive disclosure.

Such research is usually done by business analysts. But if no one else is responsible for it, you should do it. Once you have the necessary information, you can begin with design.

## Design Process

You can follow one of any number of processes in designing the user interface. You might already have one. However, I would suggest that you consider the Agile approach. Why, you ask? Well, because for users (and clients), the user interface is the product. The bottom line is that they don't care about your sketches or about fantastic back ends or powerful servers. All they want to see is the user interface.

So, how does Agile help? It helps through its key principle: the iterative approach. Each iteration consists of all of the phases defined by your process. This means that at the end of the first iteration, you will have a product that can be tested, a prototype.

<figure><img loading="lazy" decoding="async"  class="alignnone wp-image-28730 size-full" title="Process" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c0b1d3f5-cc66-41d6-a998-ba7030db734e/process.jpg" alt="application design process" width="500" height="364" /></figure>

### Sketching

<a href="https://www.smashingmagazine.com/2011/12/the-messy-art-of-ux-sketching/">Sketching is a powerful way to explore ideas</a>. The goal is to arrive at the solution by sketching out different concepts. Most sketches will be thrown out, but that is okay. As Bill Buxton says in his "Sketching User Experience" book, sketches are fast to create and easy to dispose of, which is why they are so powerful.

Are sketches the same as wireframes? Well, the differences can be blurry, but I would say no. Wireframes don't capture rough ideas but rather develop them. Read a fantastic discussion on IxDA: Sketching Before the Wireframes.

Once you get the "right" sketches, or at least the ones that you think are right, you can create more detailed wireframes or go straight to creating interactive prototypes.

<figure><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="30501" title="sketch" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/18c01a3e-fb8f-4302-88f2-5082a60a89a8/sketch.jpg" alt="sketch" width="500" height="375" /><figcaption>Sketch by <a href="https://www.flickr.com/photos/jasonrobb/3836463737/">Jason Robb</a>.</figcaption></figure>

Interesting reading on sketching and wireframing:

*   [35 Excellent Wireframing Resources](https://www.smashingmagazine.com/2009/09/01/35-excellent-wireframing-resources/)
*   [Tools for Sketching User Experiences](https://www.uxbooth.com/blog/tools-for-sketching-user-experiences/)
*   [20 Steps to Better Wireframing](https://blog.teamtreehouse.com/20-steps-to-better-wireframing)

### Prototyping

The next step in the process is to create prototypes that will simulate the real application. A prototype can contain one or more features (or all of them), but it actually does nothing. It merely simulates the behavior of a real application, and users will feel that they are actually doing something. Prototypes may contain some functionality if needed (such as complex calculations).

Because the nature of a prototype done in HTML is temporary—its purpose, after all, is to <em>test</em> ideas—don't bother with the code; just make it work with minimal bugs. You will throw it away anyway. You can also use specialized prototyping software such as <a href="https://www.smashingmagazine.com/2016/07/a-deep-dive-into-axure-8-a-comprehensive-review/">Axure</a>. Some people even prototype in PowerPoint.

<figure><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="30502" title="prototype" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d0c50709-f3b1-441e-8ca0-c5821a3ab7f4/prototype.jpg" alt="prototype" width="487" height="508" /><figcaption>An Axure interactive prototype for an e-commerce website, by e-maujean.</figcaption></figure>

Further reading and tools for prototyping:

*   [5 Useful Online Tools for Web Design Planning and Prototyping](https://blog.webdistortion.com/2009/02/22/useful-online-tools-for-easier-website-planning-and-prototyping/)
*   [A Practitioner’s Guide to Prototyping](https://www.rosenfeldmedia.com/books/prototyping/): A book from Rosenfeld Media
*   [16 Design Tools for Prototyping and Wireframing](https://articles.sitepoint.com/article/tools-prototyping-wireframing)

{{% ad-panel-leaderboard %}}

### Testing

Prototypes are useless unless you test them. This is not rocket science. People like Jakob Nielsen and Steve Krug support so-called “discount usability testing,” which is cheap and fast and yields valuable insight into your design decisions. You will use this information as the basis of another iteration of sketching, prototyping and testing. Do this at least until major issues have been fixed. We all know that software projects are tight on time and budget, so to be more efficient, <strong>test early and test often</strong>.

One of the best resources for discount usability testing is a new book by Steve Krug, "Rocket Surgery Made Easy." Pick up a copy and read it.

<figure><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="30503" title="usability_test" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/86761236-4a51-4f12-9619-312a92530d2a/usability-test.jpg" alt="usability_test" width="500" height="335" /><figcaption>Snapshot of usability testing for Delicious, by <a href="https://www.flickr.com/photos/nzdave/491411546/">(nz)dave</a>.</figcaption></figure>

Further reading:

*   [Why You Only Need to Test with 5 Users](https://www.useit.com/alertbox/20000319.html)
*   [Usability Testing Demystified](https://www.alistapart.com/articles/usability-testing-demystified/)
*   [The Myth of Usability Testing](https://www.alistapart.com/articles/the-myth-of-usability-testing/)

## Design Principles

There are many design principles, but there doesn't seem to be a general consensus on definitive ones. So, we'll go through design principles more informally, leaving out strict definitions.

### No One Likes Surprises

Probably the key factors in a good UI are consistency and familiarity. A user interface should be consistent across all parts of the application, from navigation to color to terminology. This is known as <strong>internal consistency</strong>. But a user interface should also be consistent within its context, such as the operating system or other applications in its group or family. A typical example is the applications in the Microsoft Office family. This is called <strong>external consistency</strong>.

A good approach to consistency is to define user interface guidelines for each project or for a group of projects. These should guide the decisions you make for all of the details. This will not only maintain consistency but also serve as documentation to help team members better understand your decisions.

<figure><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="30522" title="sprinkle_penny" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d85a0afa-7495-4fc0-ab35-60a506e908bf/sprinkle-penny.jpg" alt="sprinkle_penny" width="500" height="393" /><figcaption>Although a simple example, SprinklePenny achieves consistency and familiarity across the application.</figcaption></figure>

Consistent user interfaces have a shorter learning curve, because users will recognize parts of the system and be able to fall back on prior experience. But <strong>familiarity</strong> is sometimes confused with consistency. Familiar user interfaces draw on concepts from the users' previous experiences and use appropriate metaphors. Folders, for example, are a well-known metaphor for file organization, and they have replaced “directories,” which were used previously in command-line operating systems. In short, speak the language of your users.

A common belief among business owners is that a great user interface should look like a Microsoft Office product, especially Outlook. I won't go into explaining how pointless this is. Rather, I will offer alternative advice: defend the user-centric approach, and explain why creating an application for employees, clients and partners (i.e. <strong>their users</strong>) is so important.

All the same, most businesses are unique, as are their work processes. For example, two businesses from the same branch could have significantly different processes, forcing you to go beyond what is familiar and start to <strong>innovate</strong>. This part of the design process can be very interesting, although you have to be careful in how far you go with innovation.

Further reading:

*   [Designing and Selecting Components for UIs](https://uxmag.com/design/designing-amp-selecting-components-for-uis)
*   [Why Consistency Is Critical](https://articles.sitepoint.com/article/why-consistency-is-critical)

### Users Should Be Able to Be Efficient

Without a doubt, users should be able to be efficient when using business applications. This is what they are paid for, and this is what managers expects from the application. User interfaces should allow users to be efficient and should focus them on completing tasks in the easiest and fastest way. But this is not always the case. There is an opinion, or at least practice, among developers that says the user interface should be as complex as the back end system. No matter how ridiculous this sounds, the problem is real and might give you a headache. This is one reason why good communication and collaboration between developers is a must.

Users are efficient when they <strong>focus on a particular task</strong>. As mentioned, task analysis can help you identify tasks and determine how users perform them. If tasks are long, accelerate them by breaking them up into smaller units. You can also increase efficiency by providing <strong>keyboard support and shortcuts</strong>. Think how inefficient it is for a user to have to switch back and forth between mouse and keyboard. In some cases, you will be designing for users who are accustomed to working on command-line operating systems and the applications made for them. They will be keen to have keyboard support. One suggestion: when defining keyboard shortcuts, keep them consistent with those of common applications. For example, <em>Ctrl + S</em> should always be save, and so on.

<figure><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="30456" title="google_docs" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2d746c45-8814-40ac-8d30-197443995e30/google-docs.jpg" alt="google_docs" width="500" height="324" /><figcaption>Google Docs Spreadsheet enables users to be efficient by providing keyboard shortcuts and context menus, as well as by taking advantage of users' familiarity with common desktop applications.</figcaption></figure>

Efficiency can also be enhanced through <strong>personalization</strong>. Users who can personalize an environment will learn it faster and, more importantly, will be more confident using it. Personalization can be done in many ways: choosing widgets for the dashboard; defining shortcut options and favorites; changing the order of elements; etc.

Pay attention to <strong>accessibility</strong>. Although many assume that accessibility doesn't matter in Web applications, it certainly does. Treat the application as if it were a public website.

A Web application also has to be efficient in the speed with which it processes information. So, consider heavy interactions that result from partial renderings and <a href="https://www.jankoatwarpspeed.com/post/2009/11/01/usability-tips-visualizing-ajax-requests.aspx">AJAX requests</a>.

### Help!

An interface should provide <strong>meaningful feedback</strong> that describes the state of the system to users. If an error occurs, users should be notified and informed of ways to recover. If an operation is in progress, users should be notified about the progress.

We can go even further and declare that user interfaces should prevent users from making errors. This principle, called <strong>forgiveness</strong>, can be followed with confirmation dialogs, undo options, forgiving formats and more. Forgiveness makes it safe to explore the interface, decreases the learning curve and increases overall satisfaction.

Because of the complexity of business Web applications, you would also need to provide a <strong>comprehensive help system</strong>. This can be done with inline help, a support database, a knowledge base and guided tours (which mix video, images and text).

Further reading:

*   [Forgiveness in UI design](https://www.jankoatwarpspeed.com/post/2009/11/17/Forgiveness-UI-design.aspx)
*   [Web Form Validation: Best Practices and Tutorials](../2009/07/07/web-form-validation-best-practices-and-tutorials/)
*   [Handling User Error with Care: Getting Users Back on Track](https://www.uxbooth.com/blog/showing-error-messages-to-users/)

### Can't Get No Satisfaction

Satisfaction is a subjective term that refers to how pleasant an interface is to use. Every design principle we have described here affects  satisfaction. And a few more principles are worth mentioning here.

<strong>Simplicity</strong> is a basic principle of UI design. The simpler a user interface, the easier it is to use. But keeping user interfaces for business applications simple is a challenge because the apps often have a lot of functionality. The key is to balance functionality and simplicity. Restraint is one of the most efficient ways to achieve this balance: i.e. finding the simplest way to solve a problem.

<figure><img loading="lazy" decoding="async"  title="buildwithme" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d26705ee-5727-4150-859b-a5c96e2887e9/buildwithme.jpg" alt="buildwithme" width="500" height="282" /><figcaption>BuildWith.me has a simple and effective user interface, without sacrificing aesthetics.</figcaption></figure>

<strong>Aesthetics</strong>, though subjective and somewhat arbitrary, play an important role in overall satisfaction. Users respond positively to pleasing user interfaces, sometimes even overlooking missing functionality. But you're not creating a work of art. One of the best articles that explains aesthetics is <a href="https://www.alistapart.com/articles/indefenseofeyecandy/">In Defense of Eye Candy</a>.

In the end, users will be spending a lot of time in front of a business application, and no matter how usable, consistent or forgiving the interface is, satisfaction will be critical in determining how good the user interface is.

Further reading:

*   [7 Interface Design Techniques to Simplify and De-clutter Your Interfaces](https://www.webdesignerdepot.com/2009/02/7-interface-design-techniques-to-simplify-and-de-clutter-your-interfaces/ "Permanent Link to 7 Interface Design Techniques to Simplify and De-clutter Your Interfaces")
*   [Restraint](https://www.usabilitypost.com/2009/10/02/restraint/)
*   [In Defense of Eye Candy](https://www.alistapart.com/articles/indefenseofeyecandy/)

### Other resources related to UI design:

*   [12 Useful Techniques for Good User Interface Design](../2009/01/19/12-useful-techniques-for-good-user-interface-design-in-web-applications/)
*   [8 Characteristics of Successful User Interfaces](https://www.usabilitypost.com/2009/04/15/8-characteristics-of-successful-user-interfaces/ "Permanent Link to 8 Characteristics Of Successful User Interfaces")
*   [Principles of User Interface Design (Wikipedia)](https://en.wikipedia.org/wiki/Principles_of_User_Interface_Design)
*   [10 Principles of the UI Design Masters](https://net.tutsplus.com/articles/10-principles-of-the-user-interface-masters/)
*   [20 Websites to Help You Master User Interface Design](https://sixrevisions.com/usabilityaccessibility/20-websites-to-help-you-master-user-interface-design/ "Permanent Link to 20 Websites to Help You Master User Interface Design")

{{% ad-panel-leaderboard %}}

## Essential Components Of Web Applications

Every Web application is unique, but many of them contain common features. Although the implementation of any one of these features will vary, let's look at the basic concept of the three most common ones.

### Web Forms

Forms in general are important to Web applications. But as Luke Wroblewski says in his Web Form Design book, "No one likes filing in forms." That includes sign-up forms, including business applications with dozens of fields.

Minimize the frustration of filling in forms. Provide inline validation and good feedback. Use defaults when possible. Don't forget about novice users. Use wizards to help them complete tasks faster, or use progressive disclosure to hide advanced (or infrequently used) features.

### Master-Detail Views

This is the technique of showing data in two separate but related views. One view shows a list of items, while the other shows details of the selected item. Master-detail views can be implemented across multiple pages or on individual ones.

### Dashboards

Many Web applications have dashboards. A dashboard is a view of the most important information needed to take action and make decisions. It is confined to a single page and is usually the starting point of an application. Dashboards are important because they enable users to access information and take action without having to dig through the application.

<figure><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="30466" title="xero" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e556e94c-d784-425b-8b51-541e7c3b4939/xero.jpg" alt="xero" width="500" height="367" /><figcaption>Xero shows a user's most important financial information (e.g. bank accounts and credit cards) in its dashboard, making it easy for users to quickly see the status of their financial data.</figcaption></figure>

### Heavy Use of Tables

Because Web applications typically deal with large quantities of data that are easily accessible and sortable, tables are unavoidable. But this is not a bad thing. In fact, tables were made for this purpose. Don't confuse this with table-less layouts. <a href="https://designshack.co.uk/articles/css/15-tips-for-designing-terrific-tables">Effective tables</a> are easily readable. So, in most cases you will need a meaningful header, an optimal number of columns, pagination, alternating row colors, proper column alignment, sorting and filtering capabilities and much more.

Tables can also be interactive, meaning they can generate additional info and even modify the data they contain.

<figure><img loading="lazy" decoding="async"  title="pulseapp" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9a9d6359-09b2-4c93-aa78-367734e3467f/pulseapp1.jpg" alt="pulseapp" width="500" height="481" /><figcaption>PulseApp is a good example of how tables can be used to efficiently present and manipulate complex data.</figcaption></figure>

### Reports

Most businesses work with some kind of reports. Printed reports are usually required, so pay attention to the design of reports. Printed (or exported) reports are usually simplified versions of online reports, optimized for monochrome printers.

<figure><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="30470" title="fresh_books" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/22c40302-a2c5-4a9b-b7dd-3c8eb555464a/fresh-books.jpg" alt="fresh_books" width="500" height="285" /><figcaption>FreshBooks has printing, PDF exporting and "Send to email" features. It also shows a print preview.</figcaption></figure>

## Don't Forget UI Design Patterns

We're so used to hearing and talking about UI design patterns that we sometimes forget about them! UI design patterns are helpful for designing user interfaces. The important thing is to consider them early on in the design process, ideally at the sketching stage. Because patterns often solve common problems, the right pattern can facilitate the user's familiarity with an interface and increase the speed at which they learn it.

<a href="https://designingwebinterfaces.com/designing-web-interfaces-12-screen-patterns"><img loading="lazy" decoding="async"  title="Standard screen patterns" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ea9c050b-e96b-42ff-8be9-ed8f7b4db0a8/standard-screen-patterns.png" alt="Standard screen patterns" width="476" height="705" /></a>

This screenshot is from the article <a href="https://designingwebinterfaces.com/designing-web-interfaces-12-screen-patterns">12 Standard Screen Patterns</a>, which goes over the most common screen patterns.

### <span class="rh">Further Reading</span>

*   [Designing Web Interfaces: Principles and Patterns for Rich Interactions](https://www.amazon.com/Designing-Web-Interfaces-Principles-Interactions/dp/0596516258/ref=sr_1_3?ie=UTF8&s=books&qid=1264343645&sr=8-3) A fantastic book that covers more that 70 Web design patterns.
*   [40+ Helpful Resources On User Interface Design Patterns](https://www.smashingmagazine.com/2009/06/15/40-helpful-resources-on-user-interface-design-patterns/)

## Case Study: Online Banking Application

To take an example from the real world, I will briefly explain the process of designing the user interface for one small bank's online banking system. The team I worked with was hired to improve the system. The main reason for the redesign was that, according to management, "users complained and many stopped using it."

After only a couple of hours spent with actual users, the main problems were uncovered. Information about accounts and credit cards was buried in poor navigation. Understanding how much money users were spending and the state of their accounts and credit cards was also hard. The application, however, was obvious to bank employees; they were familiar with the terminology and could interpreted the numbers in the application perfectly well.

Give the tight deadlines, we followed the process I have described, and we partially succeeded. Despite the short time, the major problems were so obvious that we clearly understood our main task and how to go about it. We created a dashboard that provided clear information on the state of all accounts and credit cards. With this new navigation, finding information became easier. Reports were easier to understand, and several new features were implemented.

Although we made only a few changes, the changes affected critical user tasks and resulted in significant improvements to the overall experience.

## Final Thoughts

Designing user interfaces for business Web applications is a challenging job that is full of compromises. You have to make compromises between client and user needs; business requirements and users; novice and expert users; functionality and simplicity. It requires a solid understanding of users and their tasks, as well as of UI design principles and patterns. Despite the difficulties, the job is interesting, and you learn many new things on each project that influence the way you design websites.

While this article reflects some well-known concepts and things I have learned from designing business applications over the years, I look forward to hearing your experiences and stories.

{{< signature "al" >}}

