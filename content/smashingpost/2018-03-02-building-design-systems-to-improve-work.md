---
title: 'Beyond Tools: How Building A Design System Can Improve How You Work'
slug: building-design-systems-to-improve-work
author: amy-thibodeau
image: >-
  //archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/faa5bfb0-4833-4447-9481-b2ed52cc6658/design-systems-iceberg.jpg
date: 2018-03-02T15:00:26+01:00
summary: >-
  This article includes practical advice that will be useful to anyone who is thinking about creating a design system to enable harmonious, integrated, and fundamentally successful product development.
description: >-
  This article includes practical advice that will be useful to anyone who is thinking about creating a design system to enable harmonious, integrated, and fundamentally successful product development.
categories:
  - Design Systems
  - Style Guides
  - UX
  - UX
---
When high potential projects fall apart, it’s often a failure of collaboration and alignment. The tools, the assumptions, the opportunity, and the intentions may line up, but if people don’t communicate or don’t have a clear map to help them move in the same direction, even the best projects falter.

Communication failures are human problems, so they’re messy and hard to solve. They involve feelings and a willingness to have uncomfortable conversations. Human problems are abstract &mdash; sometimes it’s hard to even define the issue &mdash; and progress may be hard to see and measure. Because of this ambiguity, people often look to tools to fix things. Tools for better collaboration, task management, and to enable people to talk to each other.

Design systems are one kind of tool that people look to in order to solve problems that are fundamentally about failures in collaboration and alignment. Often, when people talk about design systems, they’re really talking about style guides because that’s the most tangible part of the work. The style guide is like the tip of an iceberg. It rises majestically up out of the surface, and it’s easy to forget the larger stabilizing force beneath the surface of the water that keeps the whole thing afloat.

{{< rimg href="https://www.flickr.com/photos/kmortara4/39097905821/in/photolist-22yWZfv-HCfQQT-9dRU6F-dBfaYh-9dT5Qn-4SyNQi-9dVvkY-br4aPy-dKKiPo-KHYUNW-4SyP4V-3LP9cm-dWyDTq-dKJsS6-VvMoDK-dKDQqV-4KkJNy-p2AjKG-6weBij-JWtKp5-md52Ug-HCfM8x-SNwru7-qCCMeQ-qPc17B-21zQeyE-SC1N3N-9dVtm9-pVQUcL-3cGsiy-qAB4kN-q3NU6f-KTh81M-5CeBjt-VpB6ft-9dW61Y-np77ik-smdTpX-SUv1iv-5ZQboq-h4Lvve-dLH2ro-RCaBMt-h2jj1H-4XYKxz-S3MSj1-fiwz8m-8ZpdeG-qcPZ7i-SjN7Hf" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/faa5bfb0-4833-4447-9481-b2ed52cc6658/design-systems-iceberg.jpg" sizes="100vw" caption="Image credit: <a href='https://www.flickr.com/photos/kmortara4/39097905821/in/photolist-22yWZfv-HCfQQT-9dRU6F-dBfaYh-9dT5Qn-4SyNQi-9dVvkY-br4aPy-dKKiPo-KHYUNW-4SyP4V-3LP9cm-dWyDTq-dKJsS6-VvMoDK-dKDQqV-4KkJNy-p2AjKG-6weBij-JWtKp5-md52Ug-HCfM8x-SNwru7-qCCMeQ-qPc17B-21zQeyE-SC1N3N-9dVtm9-pVQUcL-3cGsiy-qAB4kN-q3NU6f-KTh81M-5CeBjt-VpB6ft-9dW61Y-np77ik-smdTpX-SUv1iv-5ZQboq-h4Lvve-dLH2ro-RCaBMt-h2jj1H-4XYKxz-S3MSj1-fiwz8m-8ZpdeG-qcPZ7i-SjN7Hf'>Kyle Mortara</a>" alt="Iceberg" >}}

Among the most important and overlooked forces behind your style guide are the internal workings and culture on your team or with your client. In fact, a style guide is just a map of how a group of people approaches their work. It documents and operationalizes the internal process and culture that already exist. If you’re not careful, it can even reinforce bad habits and dysfunctional, siloed ways of working.

{{% feature-panel %}}

Since Shopify launched the [style guide for the Polaris design system](https://polaris.shopify.com/) last year, many of the questions I’ve been asked have been about how we were able to produce something that feels so integrated - where design, content strategy, and front-end development come together to form a holistic picture of how we build our product. These questions usually assume that we were battling to fill a gap between developers and designers, or that some kind of peace treaty must have been brokered between different disciplines to achieve the kind of unity reflected in Polaris.  

This article will outline some of the ways Shopify structures its UX team and how we used the process of building our style guide to rethink and reinforce the integrated way we approach product development. Whether you work in-house on a team or as a freelancer with different clients, it includes practical advice to help you think about creating a system to enable harmonious, integrated, and fundamentally successful product development.

## Design System vs. Style Guide

A style guide is the map of your design system. It’s the place where you can bring together and make explicit many of the elements related to how you approach UX.

It can help to think of design systems as made up of tangible and intangible assets. Most industries have some version of this concept. For example, in [the investment world](https://www.investopedia.com/ask/answers/012815/what-difference-between-tangible-and-intangible-assets.asp), tangible assets are things like “land, vehicles, equipment, machinery, furniture, inventory, stock, bonds and cash.” Intangible assets are defined as “nonphysical, such as patents, trademarks, franchises, goodwill, and copyrights.”

At Shopify, we think of our design system as being made up of tangible and intangible elements. For example:

<table class="table-overview tablesaw break-out" data-tablesaw-mode="swipe" data-tablesaw-minimap>
    <thead>
        <tr>
            <th data-tablesaw-priority="persist">Tangible elements</th>
            <th>Intangible elements</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>Team members</td>
            <td>Opinions and assumptions about quality</td>
        </tr>
        <tr>
            <td>Defined roles and responsibilities</td>
            <td>Communication between individuals and teams</td>
        </tr>
        <tr>
            <td>Components in our product</td>
            <td>Aspirations about the future of our product</td>
        </tr>
         <tr>
            <td>UI Kit</td>
            <td>Skills graph</td>
        </tr>
         <tr>
            <td>Content and visual rules</td>
            <td>Alignment between teams</td>
        </tr>
         <tr>
            <td>Research and data</td>
            <td>UX culture</td>
        </tr>
    </tbody>
</table>

A large part of the early work of creating the Polaris style guide was to determine which of these elements we could and should make explicit in our map.

## Define The Problem You’re Trying To Solve

The first step towards being intentional about your design system is being honest about where you are today. Whether you have a style guide or not, if you build products and have a UX team, you have a design system. It may be a dysfunctional system, but the fact that you have people working together to build something means that it exists. People you’re working with likely have all kinds of assumptions about how a product is designed and built &mdash; this is the scaffolding of your system.

Prior to building Polaris, Shopify had internal documents that defined some of our most common interface components and some of our content and design rules. We also had ways of working together, including rituals like regular critiques to help build alignment.

As the team, product, and even our user base grew, the informal system we were using became disjointed and, because no one team was responsible for it, hard to manage. We were also undertaking a redesign of our core product, and we knew that without a more intentional approach to our system, it would be very hard to coordinate all the different teams and changes that would need to click together. These were some of the problems that led us to revisiting and documenting our design system.

Building an intentional design system and the documentation to formalize it are a big investment. Before you start, ask yourself and stakeholders:

- How does the system function today?
- What would be gained or lost from more formal ownership and documentation of the system?
- What are the key problems that a more intentional design system would solve?

## Inventory Tangible And Intangible Elements

Creating an inventory of the tangible and intangible elements of your existing system will help you identify the biggest gaps in how your team is working. It will also point to existing processes and documentation to be clarified, streamlined, and refined.

Creating an inventory can be a great kick-off activity that will get you thinking through how people currently approach their work.

- How does everyone know what to do?
- What are the common assumptions people hold about how products are designed and built?
- What resources and documentation already exists?
- How do people know they’re aligned?
- How are different disciplines currently collaborating?

We found that different teams had different ways of working and had created their own parallel documentation to define processes and opinions. For example, the product content strategy team and the team that writes and maintains the [Help Center](https://help.shopify.com/) had both created artifacts related to content standards. In some cases, those documents were aligned, in other cases, they were in conflict. This pointed to a good opportunity to talk about the gaps and work together to define [holistic content documentation](https://polaris.shopify.com/content/product-content). We might not have identified this gap without the important step of doing an inventory.

{{% pull-quote %}}The design system that you build, and the documentation you create for it, will reflect and reinforce any assumptions and biases in how you work.{{% /pull-quote %}}

## Take A Multidisciplinary Approach

A design system is inherently about being intentional about how you approaches creating, building, and maintaining the user experience of your product. Having clear documentation (like a style guide) to map out the different pieces of your system is a pretty critical way to operationalize this work. For most companies, the effort required to do this is larger than a side project. It’s not something that can be slapped together at a hackathon and then magically stays in sync. It requires some number of people to steward and maintain it. Depending on the size of your company and the complexity of your systems, this could mean one (if you’re a freelancer) or dozens of people. The important thing is that someone, or some group of people, is responsible and accountable for establishing and documenting the design system.

If you want to build holistic products that are easy to understand and use, the people thinking about your design system need to be equipped with a breadth of UX skills. For example, if you don’t include a content strategist on your team, or at least someone with deep experience and interest in how content works in the interface, it’s likely that the interfaces built on the scaffolding of your system won’t leverage the full power of language. If you don’t have a multidisciplinary UX team to lean on, it’s important for you to consider the different dimensions that make up a good user experience and represent them accordingly.

Our UX practice is comprised of four disciplines: design, front-end development, research, and content strategy. Since we’ve defined these are the UX perspectives we value most on our product teams, we’ve made sure they’re well represented on our systems team. When we defined the team that would work on Polaris back in January 2017, it was important to have representatives from each of these disciplines as contributors and as stakeholders.

If you approach UX from a holistic point of view, that multidisciplinarity will be reflected in your design system. If you work in silos or you de-prioritize or devalue certain parts of the user experience, that bias will also be reflected in the design systems you build and document.

Shopify’s multidisciplinary approach to product development comes across most clearly in how we document [components in Polaris](https://polaris.shopify.com/components/get-started). We wanted people to have the functional building blocks to recreate components in code or to design with them in Sketch, but we also wanted everyone to understand the fundamental utility of each component &mdash; the purpose it solves &mdash; for Shopify merchants. It was also critical that people had access to the usability rules and content standard for each component, all in one place.

As I wrote in [an article](https://ux.shopify.com/locating-polaris-21b917f37fd5) published shortly after the launch of the Polaris style guide,

<blockquote>“When people understand the logic behind design decisions, they’re positioned to build better experiences for merchants. Including this information was fundamental if we wanted our style guide to be a map of our design system and reflect the way we believe a product should be built at Shopify.”</blockquote>

{{< rimg href="https://www.flickr.com/photos/kmortara4/39097905821/in/photolist-22yWZfv-HCfQQT-9dRU6F-dBfaYh-9dT5Qn-4SyNQi-9dVvkY-br4aPy-dKKiPo-KHYUNW-4SyP4V-3LP9cm-dWyDTq-dKJsS6-VvMoDK-dKDQqV-4KkJNy-p2AjKG-6weBij-JWtKp5-md52Ug-HCfM8x-SNwru7-qCCMeQ-qPc17B-21zQeyE-SC1N3N-9dVtm9-pVQUcL-3cGsiy-qAB4kN-q3NU6f-KTh81M-5CeBjt-VpB6ft-9dW61Y-np77ik-smdTpX-SUv1iv-5ZQboq-h4Lvve-dLH2ro-RCaBMt-h2jj1H-4XYKxz-S3MSj1-fiwz8m-8ZpdeG-qcPZ7i-SjN7Hf" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bf116f49-f4a1-431d-8139-de617b018c01/design-systems-polaris.jpeg" sizes="100vw" caption="Image credit: <a href='https://www.flickr.com/photos/kmortara4/39097905821/in/photolist-22yWZfv-HCfQQT-9dRU6F-dBfaYh-9dT5Qn-4SyNQi-9dVvkY-br4aPy-dKKiPo-KHYUNW-4SyP4V-3LP9cm-dWyDTq-dKJsS6-VvMoDK-dKDQqV-4KkJNy-p2AjKG-6weBij-JWtKp5-md52Ug-HCfM8x-SNwru7-qCCMeQ-qPc17B-21zQeyE-SC1N3N-9dVtm9-pVQUcL-3cGsiy-qAB4kN-q3NU6f-KTh81M-5CeBjt-VpB6ft-9dW61Y-np77ik-smdTpX-SUv1iv-5ZQboq-h4Lvve-dLH2ro-RCaBMt-h2jj1H-4XYKxz-S3MSj1-fiwz8m-8ZpdeG-qcPZ7i-SjN7Hf'>Shopify</a>" alt="Polaris illustration" >}}

Our ability to build a design system and style guide that reinforces the multidisciplinary way we work (which is one of the core ways we build great user experiences) depended on assembling a core systems team that reflected our different UX disciplines. We also agreed on some ways of working to encourage deep, integrated collaboration between disciplines. This was important because we were a large team. If you’re working with a smaller team, some of this may happen organically out of necessity:

- Encourage people to move between swim lanes. Designers and front-end developers are encouraged to write, content strategists are encouraged to design, but everyone is encouraged to code. Embrace the fact that UX roles overlap and intersect.
- Hold cross-disciplinary sprints, critiques, and project planning sessions. Make it clear that everyone is accountable for the breadth of the user experience.
- Appoint team leaders from different disciplines and give them shared authority.
- Make everyone, including team leads, responsible for the “dirty work.” For the launch of Polaris, this meant that everyone on the team submitted diffs, reviewed pull requests for code changes, and edited content in markdown. No job was too small or inconsequential for anyone, regardless of discipline or job title.

## Build Your Map

Creating the documentation for your design system can be labor intensive, but it’s easier once you’ve defined your purpose, created and analyzed the inventory of your system, and assembled a strong, multidisciplinary team. One of the most valuable outcomes of creating documentation is that writing is a great way to clarify what you think.

For Polaris, the bulk of our new documentation was about our components. Content strategists created a template that outlined the different content chunks the team believed were critical to creating useful documentation about each component. Then it was a shared responsibility across the team to write that documentation. The goal in sharing writing responsibilities wasn’t for everyone to generate perfect prose, but to have everyone on the team use language as a way to think through the utility, functionality, and UX best practices for each component.

One of the ways we encouraged collaboration was to use tools that were accessible to people from different disciplines and teams. We used a gigantic Google Document as a scrappy content management system as we were writing and editing our map. At its longest, this document was 180 pages of mainly text. Internally, Shopify defaults to open, so we gave everyone in the company access to our draft and encouraged people to add comments, make edits, and to contribute. Doing this was noisy at times, but the challenge of managing lots of input was far outweighed by the goodwill and buy-in it resulted in. Design systems are relevant to people outside of UX and giving a wide range of people the opportunity to give feedback was an important way of making sure our assumptions were challenged and rigorously tested.

In addition to using Google Docs to manage our content creation and editing process, we used markdown in GitHub for our style guide because it lowered the bar for contributions. This decision continues to be an important way the Polaris team is able to encourage people from across Shopify to edit and add to the style guide.

Your style guide helps make the system explicit and gets people moving in the same direction. The way that you go about creating this documentation and the decisions around what you choose to include or exclude will inform how people use it and whether they recognize it as relevant to them.

## Last Thoughts

Building a design system and the documentation that defines it can be an opportunity to rethink how you approach UX, or it can be a vanity project that reinforces existing problems. This is true whether you’re working in-house at a large company, or trying to bring order to a product you’re designing for a client.

Launching the Polaris style guide was just the most visible outcome of a lot of deep thinking and work across multiple disciplines and many different teams. The long, hard work is what came before the launch, and what has continued behind the scenes since then &mdash; lots of people working together to iterate on how we build products and how we document what we’ve learned. This quiet, deep work is where the real value lives.

A style guide is simply a map. It can orient you and show you the way. But whether you get there, and who you bring along, are up to you.

{{< signature "da, ra, hj, il" >}}
