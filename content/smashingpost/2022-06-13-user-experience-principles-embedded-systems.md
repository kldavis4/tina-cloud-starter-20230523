---
title: 'How To Apply UX Principles To Embedded Systems: Learnings From The Field'
slug: user-experience-principles-embedded-systems
author: eva-rio
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3223ce3b-fbdf-44dc-aae4-149d03b2ce75/user-experience-principles-embedded-systems.jpg
date: 2022-06-13T11:00:00.000Z
summary: >-
  Embedded systems make our lives easier. We unawarely interact with embedded systems all the time, and they go largely unnoticed &mdash; until things do not work as expected. In this article, Eva gives an overview of what embedded systems are and how they impact our lives. She presents three main learnings gained across her quest for creating better-embedded systems to enable the world as we know it.
description: >-
  In this article, Eva gives an overview of what embedded systems are and how they impact our lives. She presents three main learnings gained across her quest for creating better-embedded systems to enable the world as we know it.
categories:
  - UX
  - Devices
  - Usability
  - User Experience
---

[Embedded systems mean different things to different people](https://www.oreilly.com/library/view/making-embedded-systems/9781449308889/ch01.html); they can be standalone and independent, working by themselves, or be a part of a larger system. They are purpose-built for a particular application, designed to perform a specific function or set of tasks. Complexities of embedded systems range [from very simple to highly sophisticated implementations](https://embeddedcomputing.com/technology/software-and-os/embedded-software-how-complex-can-it-get), depending on the functions and features that need to be performed and its interactions and connections with other systems. Some examples are autonomous driving, artificial intelligence, and the internet of things. 

To provide some context, embedded systems have been around for a long-time. Two examples are the [difference engine devised by Charles Babbage](https://plato.stanford.edu/entries/computing-history/) in the 1830s and the [Apollo Guidance Computer](https://en.wikipedia.org/wiki/Apollo_Guidance_Computer) built in the 1960s and considered to be the first modern embedded system. A key component of an embedded system is its software. Embedded software brings a system to life, performing tasks on your behalf. [Software is where most of the design effort and complexity of embedded systems lie](https://www.mckinsey.com/industries/advanced-electronics/our-insights/cracking-the-complexity-code-in-embedded-systems-development). 

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f640bfdb-b2b7-4d1e-87a8-ee06a7dd071b/2-papplying-user-experience-principles-embedded-systems.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f640bfdb-b2b7-4d1e-87a8-ee06a7dd071b/2-papplying-user-experience-principles-embedded-systems.jpg" width="800" height="529" sizes="100vw" caption="Extremely simplified architecture of an embedded device. Architectural choices depend on the function the device needs to fulfill, the underlying hardware, non-functional requirements like security, and many other factors. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f640bfdb-b2b7-4d1e-87a8-ee06a7dd071b/2-papplying-user-experience-principles-embedded-systems.jpg'>Large preview</a>)" alt="Architecture of an embedded device" >}}

In this article, I share three key learnings I have gained from applying UX and human-centered approaches when working with embedded software. These three takeaways include the complexity and advantage of addressing the needs of multiple stakeholders, how to benefit from understanding the dependencies between different components (by definition, embedded means integrated onto something), and how to overcome the challenge of communicating the value of technology that’s often invisible.

1. [Embrace Complexity In Your Projects And Designs](##learning-1-embrace-complexity-in-your-projects-and-designs)
2. [Find Ways To Learn Fast And Don’t Go Solo](#learning-2-find-ways-to-learn-fast-and-don-t-go-solo)
3. [Communicate The Value Of Embedded Software](#learning-3-communicate-the-value-of-embedded-software)

{{% feature-panel %}}

## Learning #1: Embrace Complexity In Your Projects And Designs

<blockquote>Different stakeholders will have different sets of challenges and goals interacting with your product.</blockquote>

Let’s take a typical car as an example and imagine you develop software for its [advanced driver-assistance (ADAS) system](https://en.wikipedia.org/wiki/Advanced_driver-assistance_systems). There are three stakeholders in this example:

- the driver of the car, who is the end-user; 
- the person that integrates the software into the car is the user;
- the person in charge of purchasing what goes into the final car is the customer.

Even then, this is a bit of a simplification. In real-life projects, there are even more dependencies and stakeholders involved. 

Thus, who should you take into account when building and designing your solution? More than who to design software for, it is about thinking of what’s important for each stakeholder. In this example, the end-user cares about the experience and that everything works as expected or even better; the user is after a complete feature set and possibilities; the customer tends to care about cost-efficiency. In the end, you need to meet end-user expectations (who don’t even know they are interacting with embedded software) while making your product easy to integrate for the user and ensuring the customer that they are getting the best solution for an optimal price. 

Additionally, embedded systems are, in many cases, resource-constrained in power processing or memory, yet the expectation is that the whole system works seamlessly and in a sophisticated way. Therefore, you need to find a balance between performance and reliability without hurting the experience. Optimizing this interaction requires a great level of expertise and specialized knowledge, which comes at a price. 

When designing embedded software, it’s critical to spend time researching and understanding the [problem space](https://onlinelibrary.wiley.com/doi/10.1002/9781119154822.ch2), the goals, and [jobs to be done](https://jtbd.info/2-what-is-jobs-to-be-done-jtbd-796b82081cca) by the different stakeholders in real life. The better you understand each stakeholder’s expectation, the less risk of spending time building features that would have no use in a real environment or falling short of features for the future. Performing software upgrades to support new use cases in embedded systems can be very challenging because sometimes these devices are located in places that are hard to reach or have no connectivity. 

Problem space exploration is [closely related to user research](https://interactions.acm.org/archive/view/january-february-2018/launching-problem-space-research-in-the-frenzy-of-software-production). As such, there is plenty of literature, case studies, materials, frameworks and tools that you can use to collect data and gain insights into users’ needs and challenges. These activities usually include surveys, interviews, questionnaires, or market research. 

Here are some examples:

- “[Map the Problem Space](https://dschool.stanford.edu/resources/map-the-problem-space)”, Carissa Carter, Megan Stariha, Mark Grundberg
- [The Problem Space Workshop](https://miro.com/miroverse/the-problem-space-workshop/), Christy Cattin
- “[Product Strategy &mdash; Insights](https://www.svpg.com/product-strategy-insights/)”, Marty Cagan

A key aspect of understanding the problem space is to be able to map the different [journeys](https://www.toptal.com/designers/product-design/customer-journey-maps) for each of your stakeholders and their touchpoints and where in those journeys you could implement those research tools and feedback mechanisms to help you with your planning of user research and problem discovery.

The [template below from Columbia Road](https://www.columbiaroad.com/blog/why-and-how-to-create-a-customer-journey-map-download-free-template) is a great starting point. I have simply added a new dimension &mdash; **Feedback tools** &mdash; to be able to link feedback activities to the journey stages. There are also other activities that you don’t necessarily think of as feedback or research tools. Yet, there are incredibly rich practices for gathering information, and I will cover some of those in the next point. 

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/559b6b5b-c6b7-407b-831a-9c1f18db00ae/1-applying-user-experience-principles-embedded-systems.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/559b6b5b-c6b7-407b-831a-9c1f18db00ae/1-applying-user-experience-principles-embedded-systems.png" width="800" height="481" sizes="100vw" caption="Customer journey map template from Columbia Road with an extra dimension for feedback mechanisms. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/559b6b5b-c6b7-407b-831a-9c1f18db00ae/1-applying-user-experience-principles-embedded-systems.png'>Large preview</a>)" alt="A customer journey map template" >}}

{{% ad-panel-leaderboard %}}

## Learning #2: Find Ways To Learn Fast And Don’t Go Solo

As mentioned, embedded systems have many dependencies. Something as trivial as a fridge can have [dozens of interrelated embedded systems](https://www.st.com/en/applications/home-and-professional-appliances/refrigerators-and-freezers.html).

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3bf20b62-7b19-496a-b3c6-5becd4f492b5/3-applying-user-experience-principles-embedded-systems.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3bf20b62-7b19-496a-b3c6-5becd4f492b5/3-applying-user-experience-principles-embedded-systems.jpg" width="800" height="530" sizes="100vw" caption="Diagram of embedded systems of a freezer by STMicroelectronics. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3bf20b62-7b19-496a-b3c6-5becd4f492b5/3-applying-user-experience-principles-embedded-systems.jpg'>Large preview</a>)" alt="Embedded systems on a refrigerator" >}}

The software runs on the hardware. Multiple systems need to interact in consonance with one another to deliver the expected functionality to the end-user. In practice, this dependency means that no matter how good of an idea you have, you will have to collaborate with someone to make it happen. Collaborations and joint efforts can take different shapes and forms, and here are a couple of tools and practices that I’ve found helpful:

- **Workshops and [roadmap alignment](https://link.springer.com/chapter/10.1007/978-3-030-58858-8_6) sessions involving customers and partners** (handled as interactive events, not one-way presentations)  
These sessions give you the opportunity to explain how you perceive the market and what end-users are doing based on data and experiences you’ve collected, and check with customers and partners whether they see the same problems in the field and align on a future direction. There isn’t a universal way of doing this. Still, there are multiple templates and resources available for building roadmaps that allow you to group features under the key categories &mdash; *themes* &mdash; that are relevant to your markets and customers and that also let you prioritize your initiatives in a way that is flexible to account for changes and potential scenarios for the product:
    - [Roadmapping From A to Z](https://airfocus.com/resources/ebook/roadmapping.pdf) (pdf)
    - [Agile Roadmap Template](https://miro.com/templates/agile-roadmap/)
    - “[What is a Theme-Based Roadmap and Why Is it Important?](https://www.productplan.com/learn/theme-based-roadmap/)”
    - “[Outcome Roadmaps](http://www.productstride.com/outcome-roadmaps/)”, Sean Sullivan

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/41e66eec-b33d-4805-b3c0-c0994ccdc615/4-applying-user-experience-principles-embedded-systems.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/41e66eec-b33d-4805-b3c0-c0994ccdc615/4-applying-user-experience-principles-embedded-systems.png" width="800" height="308" sizes="100vw" caption="Example of a roadmap with themes and broad timelines. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/41e66eec-b33d-4805-b3c0-c0994ccdc615/4-applying-user-experience-principles-embedded-systems.png'>Large preview</a>)" alt="Roadmap example" >}}

An initiative, theme-based roadmap with broad timelines (now/next/later) helps you drive a discussion where to align your current focus, explore together ideas for the future, and discuss expectations. In other words, it helps to validate that you and the customer have the same understanding of the current landscape, a willingness to collaborate in the future and that your efforts are going into addressing the right problems. The cadence will vary depending on your business and your product release planning.

- **Joint demos and joint prototyping** can also be used to validate assumptions, increase your knowledge, and test potential solutions. Research shows that [inter-organizational product development initiatives have been growing](https://osuva.uwasa.fi/bitstream/handle/10024/10665/Inter-organizational%20collaboration%20in%20software%20product%20development.pdf?sequence=2&isAllowed=y) and that co-development [positively affects innovation](https://www.researchgate.net/publication/328701312_Antecedents_of_co-development_and_its_effect_on_innovation_performance_A_business_ecosystem_perspective). In embedded fairs and events, it is common to see demos of a company on display at other vendors’ booths. Hardware vendors and manufacturers tend to lack software skills in-house, and software companies can better tune and optimize their products if they have a deeper access to the underlying hardware. 

Talent is highly specialized, and hiring prices in the industry can be relatively costly. Collaboration is a cost-effective way to work on proof of concepts for addressing emerging demands, finding new revenue streams, or reaching new markets. Joint prototyping can help you identify potential challenges and gather early feedback, as well as speed up the development process, spread out risks, and support your [time-to-market](https://www.eetimes.com/timing-to-market-is-everything/) strategy.

In embedded, the saying “the whole is more/something else than the sum of its parts” is accurate. Being able to show how systems “talk” to each other and what is the jointly created value is very useful, especially when it comes to complex systems that can have a [lifecycle of 5 to +10 years](https://blog.seco-usa.com/designing-long-life-cycle-minimizing-cost-new-product-development/). In these cases, it is essential to get things right or rather spot design mistakes early on and [validate your concepts](https://www.smashingmagazine.com/2021/11/concept-testing-part-of-product-design/) whenever possible.

- **Take all the chances you get for sharing your insights and ideas in panel discussions**, contributing to communities specialized in a particular domain, or working on collaborative content like blog posts, whitepapers, and videos with other companies. This is a great way to gauge the interest in a given topic and get reactions and comments on your hypotheses.

The embedded systems industry is highly competitive, with multiple players developing products in the same category. However, paradoxically, there’s still a reluctance to publicly engage in dialogues that may challenge the status quo and provoke new ways of thinking.

I have found that the companies that end up being trusted ([and building trust is one of the central goals of user experience and goes beyond the bare visuals of a product ](https://www.smashingmagazine.com/2021/02/building-user-trust-in-ux-design/)) and respected are those who show up and spark discussion, and share their points of view and ideas without fear of others taking credit. To quote a sentence from the TV series [Billions](https://www.sho.com/billions), *“A lot of people watch Bruce Lee movies. It doesn’t mean they can do karate.”*

{{% ad-panel-leaderboard %}}

## Learning #3: Communicate The Value Of Embedded Software

<blockquote>When software is hidden and goes unnoticed, find ways to communicate its value by pointing out the needs it solves and the impact it has on the end-user in real life.</blockquote>

You cannot differentiate your product with graphical interfaces, visual design elements, or aesthetics for software that performs tasks in the background and controls systems behind the scenes. Therefore, you need to find different ways to convey its value and relevance. Even if you are not able to directly interact with it, this type of software plays a key role in the end-user experience, impacting, for example, the performance of a device, its battery life, power consumption, and its overall behavior. Let’s see some examples:

- **Your Smart TV And Power Outage**  
There was a power outage at home, and you were recording a program on it. What would you expect after the power comes back? Your TV is able to recover. You can turn it on again and boot successfully; all its settings are there, and even the program you were recording when losing power is there. To support this experience, the system needs to be designed to support power losses and not corrupt the file system or lose data &mdash; the software embedded in the TV should be reliable enough to take care of that.
- **Smartwatches And Battery Life**  
Smartwatches are notoriously famous for their [challenges with battery life](https://www.sciencedirect.com/science/article/pii/S1389128621001651). The need to regularly charge the battery affects the user experience, and it’s something that can be affected by optimizing memory and CPU consumption at the software level.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/047d0c93-8a94-42b0-9031-211e84b515a0/5-applying-user-experience-principles-embedded-systems.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/047d0c93-8a94-42b0-9031-211e84b515a0/5-applying-user-experience-principles-embedded-systems.png" width="800" height="249" sizes="100vw" caption="Extract from a <a href='http://chulhongmin.com/paper/p11-min.pdf'>study about the level of satisfaction with the battery life of smartwatches</a>. Only 35% of smartwatch users were satisfied or very satisfied with the battery level of their devices. Note, however, that the study is from 2015 with a sample of 59 participants. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/047d0c93-8a94-42b0-9031-211e84b515a0/5-applying-user-experience-principles-embedded-systems.png'>Large preview</a>)" alt="Roadmap example" >}}

- **Navigation Systems In Your Car And Network Communications**  
When driving, you expect your maps and traffic info to be updated in real-time with minimal [latency](https://en.wikipedia.org/wiki/Latency_(engineering)), yet on the road, it is easy to lose network connectivity. Embedded software can help smooth that experience, gracefully behaving when the system is offline and caching the data until the system is back online and ensuring no data is missing. 

Thinking of the scenarios and systems holistically and then being able to explain how you help in the field and the impact you can make for the final user is an effective way to communicate the value of software and the impact it has in providing seamless experiences and meeting expectations. Find a story that resonates with your audience first, and from there, you can always go into more details for those interested in the hows and why their devices operate.

## Conclusion

We interact with embedded systems all the time by unawarely experiencing how they make our lives easier and enjoying all the features and benefits they bring. Quietly in the background, performing the tasks they were meant to, embedded systems are ubiquitous and have different levels of complexity, such as smartphones, traffic lights, manufacturing appliances, satellites, vehicles, medical equipment, and countless other devices. They are present in nearly every aspect of our lives.

{{% pull-quote %}}
 No matter how advanced or simple your product is and what is its place in the system, embedded systems will certainly play a role in the final user experience.
{{% /pull-quote %}}

Understanding the multiple dependencies to other components, the different needs of all the stakeholders you need to consider, and being able to validate your concepts and communicate your ideas early is crucial. It will help you design your embedded product in a way that lets you differentiate yourself through a better overall user experience and, silently behind the scenes, improve people’s lives.

{{< signature "yk, il" >}}
