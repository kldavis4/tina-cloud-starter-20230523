---
title: Designing Modular UI Systems Via Style Guide-Driven Development
slug: designing-modular-ui-systems-via-style-guide-driven-development
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/142bbce3-2fb1-4d8d-ac49-d3317ea0321c/05-pinterest-card-desing-preview-opt.jpg
date: 2016-06-15T18:03:24.000Z
author: adrianadelacuadra
description: >-
  Using a style guide to drive development is a practice that is gaining a lot
  of traction in front-end development — and for good reason. **Developers will
  start in the style guide** by adding new code or updating existing code,
  thereby contributing to a modular UI system that is later integrated in the
  application. But in order to implement a modular UI system, we must approach
  design in a modular way.

  Modular design encourages us to think and design a UI and UX in patterns. For
  example, instead of designing a series of pages or views to enable a user to
  accomplish a task, we would start the design process by understanding how the
  UI system is structured and how its components can be used to create the user
  flow.
categories:
  - UX
  - Style Guides
  - UI
  - Design Systems
---
Using a style guide to drive development is a practice that is gaining a lot of traction in front-end development — and for good reason. **Developers will start in the style guide** by adding new code or updating existing code, thereby contributing to a modular UI system that is later integrated in the application. But in order to implement a modular UI system, we must approach design in a modular way.

Modular design encourages us to think and design a UI and UX in patterns. For example, instead of designing a series of pages or views to enable a user to accomplish a task, we would start the design process by understanding how the UI system is structured and how its components can be used to create the user flow.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [How To Make An Effective Style Guide](https://www.smashingmagazine.com/2014/02/effective-style-guides-with-adobe-fireworks/)
*   [An In-Depth Overview Of Living Style Guide Tools](https://www.smashingmagazine.com/2015/04/an-in-depth-overview-of-living-style-guide-tools/)
*   [Automating Style Guide-Driven Development](https://www.smashingmagazine.com/2015/03/automating-style-guide-driven-development/)
*   [Free Style Guides Icon Set For Writers And Editors](https://www.smashingmagazine.com/2011/06/free-style-guides-icon-set-for-writers-and-editors/)

In this post, I’ll explain the value of modularity in UI design and how it ties into the process of [style guide-driven development](https://blog.bitovi.com/style-guide-driven-development/), which improves the implementation of flexible and user-friendly applications, while helping designers and developers collaborate more productively.

{{% feature-panel %}}

## Modular Design In The UI

Modular design is about breaking down a design into small parts (modules), creating them independently, and then later combining them into a larger system. If we look around us, we will find many examples of modular designs: Cars, computers and furniture are all modular. Because of their modularity, parts of these systems can be exchanged, added, removed and rearranged. This is great for consumers because they get to **customize the system to fit their needs**. Do you want a sunroof, a more powerful motor, leather seats? You got it! The modular design of cars allows for these types of customizations and much more.

Another great example is IKEA furniture. In the illustrations below, you can see that the modularity of the design is not only in the shape of the bookcase, which allows it to be set in different directions, or in that you can add inserts in its openings, but also in the very parts that make the piece itself, which are rectangles of different sizes, repeating the same pattern.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0e8c1be4-4b04-42b7-a89b-34488b15173e/01-ikea-kalax-bookcase-parts-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/35b16ff7-7771-456e-b98b-a80603bb5a5b/01-ikea-kalax-bookcase-parts-preview-opt.png" alt="Ikea Kalax bookcase shown during assembly" width="500" height="269" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0e8c1be4-4b04-42b7-a89b-34488b15173e/01-ikea-kalax-bookcase-parts-opt.png">View large version</a>)</figcaption></figure>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/22ecdf75-9bd4-4dd5-938e-259f8763b539/02-ikea-kalax-bookcase-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fdbcb9e9-2fb9-4214-a2a3-5793aec39073/02-ikea-kalax-bookcase-preview-opt.png" alt="Ikea Kalax bookcase assembled" width="500" height="250" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/22ecdf75-9bd4-4dd5-938e-259f8763b539/02-ikea-kalax-bookcase-opt.png">View large version</a>)</figcaption></figure>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3e7288d9-ace4-4e53-a459-1042759d71cf/03-ikea-kalax-insert-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d8498d4f-0aad-4adb-bfed-5ad9f0b021c3/03-ikea-kalax-insert-preview-opt.png" alt="Ikea Kalax Bookcase insert" width="500" height="269" /></a><figcaption>The design of the Kallax bookcase by IKEA is a great example of modularity and customization: Modular parts are used to build the bookcase, and additional sections can be inserted to add functionality. (Image: <a href="https://www.ikea.com/">IKEA</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3e7288d9-ace4-4e53-a459-1042759d71cf/03-ikea-kalax-insert-opt.png">View large version</a>)</figcaption></figure>

From a manufacturing perspective, modular design is also cost-efficient. One important aspect of this is that building small simple parts that can be connected later is easier and cheaper than building one large complex piece at once. Additionally, the solution can be reused over and over, maximizing productivity.

The goals in creating a UI design are similar. As designers, we want to create a UI system that is efficient in both construction and operation. When we find a solution to a problem, we want to be able to reuse the solution in many places. This not only saves time, but also establishes a pattern that users can learn once and reapply in other areas of the application. We also want to be able to customize the system for certain scenarios without having to restructure everything.

This is exactly what modularity brings to UI design: It leads to a system that is **flexible, scalable and cost-efficient**, but also **customizable, reusable and consistent**.</p>

### Examples of Modular Design

Some examples of modular UI design can be seen in patterns such as **responsive grids, tile window design and card design**. In all of them, modules are used repeatedly to provide a flexible layout that easily adapts to different screen sizes. In addition, the modules act as containers for components, enabling us to insert different types of content and functionality, much like the inserts that can be added to an IKEA cabinet.</p>

<figure><div class="aspect-ratio">{{< vimeo 161011132 >}}</div><figcaption>Example of a responsive grid from the Bootstrap framework (Image: <a href="https://getbootstrap.com/">Bootstrap</a>) (<a href="https://vimeo.com/161011132">View video</a>)</figcaption></figure>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e1b53c7f-be73-402c-a43a-39d336dc87a3/04-nasa-homepage-cards-grid-design-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c9a8e088-7ab2-41fd-9993-7338d09ea128/04-nasa-homepage-cards-grid-design-preview-opt.jpg" alt="NASA home page" width="500" height="244" /></a><figcaption>NASA uses Bootstrap’s grid to display a card layout. (Image: <a href="https://www.nasa.gov/">NASA</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e1b53c7f-be73-402c-a43a-39d336dc87a3/04-nasa-homepage-cards-grid-design-opt.jpg">View large version</a>)</figcaption></figure>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c8a2b162-2203-40f0-b1b1-f862e6188442/05-pinterest-card-desing-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/142bbce3-2fb1-4d8d-ac49-d3317ea0321c/05-pinterest-card-desing-preview-opt.jpg" alt="pinterest.com grid page" width="500" height="239" /></a><figcaption>The card design used in a masonry layout on Pinterest (Image: <a href="https://www.pinterest.com/">Pinterest</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c8a2b162-2203-40f0-b1b1-f862e6188442/05-pinterest-card-desing-opt.jpg">View large version</a>)</figcaption></figure>

### Is This Homogeneous?

If modular design is about designing a system, and UI systems mostly comprise the same parts (buttons, typefaces, icons, grids, etc.), then you might be wondering:

*   Aren’t modular designs all going to look the same?
*   How will this affect brand identity?
*   How can the UI of a product be made to be unique?

<p>These questions, while valid, raise an underlying question: Where do innovation and uniqueness in product design lie? This debate has picked up lately (see “<a href="https://medium.com/@morgane/the-unbearable-homogeneity-of-design-fe1a44d48f3d#.2ju7zhzig">The Unbearable Homogeneity of Design</a>” and “<a href="https://medium.com/@yarcom/in-defense-of-homogeneous-design-b27f79f4bb87#.n0te3zqme">In Defense of Homogeneous Design</a>”), but I would say that, because visual design is what we see first, we tend to think that innovation and uniqueness lie in the way a design looks. However, visual design is just one part of that. Innovation and uniqueness in product design need to be accounted for in the entire product: in the intrinsic value that it provides and in the way people experience it, which includes its appearance.</a>

Take a chair. It is required to be a chair, but not all chair designs look, feel or work the same. In fact, chair design has historically been an area of innovation in design and materials. Similarly, UIs have their own requirements, and using patterns that are proven to work doesn’t mean sacrificing innovation and uniqueness. On the contrary, innovation and uniqueness will be needed to solve the particular problems your customers have. The beauty of modular design is that it encourages us to approach these solutions as a system of parts that are interconnected, rather than to find original solutions in an isolated way for the sake of being different. In other words, an innovative design applied to a UI control won’t stay relegated to one place in the application, but instead will permeate the entire system, maintaining cohesion and improving usability.</p>

## The Modularity Of Style Guide-Drive Development

From the implementation side, style guide-driven development is also very modular. For starters, the process begins with a **discovery** phase: understanding the problem that needs to be solved, gathering requirements and iterating through design solutions. While the design solutions are usually presented as an entire package or feature, they should really be the combination of the many parts of the system documented in the style guide. Some parts of the design might be new, but they should still be created as modules. The point is to use the style guide to determine which modules are available in the UI system that can be reused or extended to create the design.

(What if there is no style guide? Do not fret! I will show you in the next section how to design in a modular way, even if you are not using a style guide.)

The next step in style guide-driven development is the **abstraction** phase, which is basically the exercise of breaking down the design solution into smaller parts. During this phase, designers and developers work together to discern the proposed design and identify the elements and components (i.e. modules) that will be either used or enhanced or that will need to be created for implementation.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3189d824-a11e-4337-a376-c0f152db34a5/06-style-guide-driven-developement-process-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fee286e5-a6c1-4cd8-9a0a-0f58af346d6b/06-style-guide-driven-developement-process-preview-opt.jpg" alt="Style guide driven development process graphic" width="500" height="155" /></a><figcaption>Style guide-driven development in a nutshell (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3189d824-a11e-4337-a376-c0f152db34a5/06-style-guide-driven-developement-process-opt.jpg">View large version</a>)</figcaption></figure>

The abstraction phase serves as well to trace a plan for the next step: **implementation and documentation**. During this phase, the modules are either built or enhanced in isolation from the rest of the existing modules. In web development, this means building a component or defining the styles for an element independent of the application. This is an important aspect of modularity, because it helps you to identify any problems early in the process, preventing unforeseen dependencies with other parts of the system. The result is more stable parts that are easier to integrate in the whole.

Something unique about style guide-driven development is that, while implementation progresses, documentation also takes place, rather than being an afterthought. This is possible because when a style-guide generator is used, the documentation becomes a **living style guide**, serving as both a framework and a sandbox for implementation:

*   The living style guide serves as a **framework** of definitions for UI elements (such as headings, lists, links, input controls, etc.) and as a library of components (such as navigation systems, toolbars, search tools, grid tables, etc.) that are available for use. This means that development is not started from scratch every time. Instead, it builds upon existing definitions in the UI system and contributes to it.
*   It is also a **sandbox** because it serves as a demonstration space to build and test the implementation. This is exactly where the development takes place before it is integrated in the application.

The last step of style guide-driven development, the **integration** phase, resembles the assembly step in modular design. The UI elements or components that are needed have been developed and are ready to be integrated in the application. What remains is to configure and customize them. During integration, the style guide is like any good instruction manual that is used to assemble a physical modular design.

Now that we have identified the fundamental concepts of modular design and style guide-driven development, let’s put them to use.

## Designing In A Modular Way

Picture this: You have come up with a great user flow, put together mockups and prototypes to illustrate the interactions, and documented every single part. Chances are that your designs already follow a style guide, which could put you at a great advantage. (If not, don’t sweat it!) Just step back and start mapping out the main parts of your design solution at a high level. These parts could be the interaction points where certain things are accomplished. For example, a checkout flow could look like this:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2b0e66db-88c4-4e67-82f4-5843fee596e8/07-checkout-flow-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2786f2bb-4f06-49c9-9017-e649bf3e0267/07-checkout-flow-preview-opt.png" alt="Checkout flow graphic" width="500" height="73" /></a><figcaption>Illustration of checkout flow (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2b0e66db-88c4-4e67-82f4-5843fee596e8/07-checkout-flow-opt.png">View large version</a>)</figcaption></figure>

But hold your guns! These are not modules yet. To get to there, we need to identify the UI elements that are persistent in the flow, such as:

*   the checkout steps indicator,
*   form elements used to enter information,
*   the representation of products in the cart,
*   the representation of related products that others have bought,
*   policies about the purchase,
*   help text,
*   messages and alerts.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6c38b807-1028-46f6-96ec-16d74454b001/08-app-mockup-01-cart-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/94a0204b-541c-4e40-a0a3-45d94edf6653/08-app-mockup-01-cart-preview-opt.png" alt="Mockup design of a cart page" width="500" height="538" /></a><figcaption>Mockup design of the cart page (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6c38b807-1028-46f6-96ec-16d74454b001/08-app-mockup-01-cart-opt.png">View large version</a>)</figcaption></figure>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ff4d4c78-e1b1-45ba-bc7f-4eb571da74e0/09-app-mockup-02-shipping-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/95c8739b-05c7-47b2-988f-51a6dd7eab1e/09-app-mockup-02-shipping-preview-opt.png" alt="Mockup design of a shipping page" width="500" height="432" /></a><figcaption>Mockup design of the shipping page (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ff4d4c78-e1b1-45ba-bc7f-4eb571da74e0/09-app-mockup-02-shipping-opt.png">View large version</a>)</figcaption></figure>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/de893036-1659-4277-9938-66c0f1e79014/10-app-mockup-03-billing-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b8bad632-ef54-4936-b05f-9b1d1437be1a/10-app-mockup-03-billing-preview-opt.png" alt="Mockup design of a billing page" width="500" height="290" /></a><figcaption>Mockup design of the billing page (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/de893036-1659-4277-9938-66c0f1e79014/10-app-mockup-03-billing-opt.png">View large version</a>)</figcaption></figure>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3a2185c9-713d-4789-b385-beb2bd992bc4/11-app-elements-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9d5d4a1d-96e4-48b7-b483-0fb118c52186/11-app-elements-preview-opt.png" alt="UI elements extracted from the designs" width="500" height="585" /></a><figcaption>Some of the UI elements that persist in the design (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3a2185c9-713d-4789-b385-beb2bd992bc4/11-app-elements-opt.png">View large version</a>)</figcaption></figure>

Digging a little deeper, we will also find styles and interaction patterns:

*   **Styles:**

*   colors used to denote:
    *   error, success, warning and information messages;
    *   primary versus secondary actions;
    *   inactive versus selected versus disabled states;
    *   links versus regular text;
    *   branding;
*   typography used to denote different types of content:
    *   font size for laying out information hierarchically;
    *   font types for highlighting messages or providing additional information;
    *   lists to summarize information;
*   iconography to convey visual meaning and for quick reference to common actions.

*   **Interaction patterns:**
    *   showing upcoming steps (disabled);
    *   showing previous steps (enabled so that the information can be edited);
    *   displaying summaries that can be edited;
    *   validating information once the user has clicked out of the field;
    *   providing help text on rollover;
    *   updating the cart once a selection has been made.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6d505c2a-1220-45f5-a58b-b428e8232bb8/12-app-styles-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/68738add-1181-44b9-a1ce-7fac14bcfdde/12-app-styles-preview-opt.png" alt="Styles extracted from the designs" width="500" height="633" /></a><figcaption>Some of the styles persistent in the design (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6d505c2a-1220-45f5-a58b-b428e8232bb8/12-app-styles-opt.png">View large version</a>)</figcaption></figure>

Once the design has been broken down into all of these smaller pieces, we will finally have our modules. At this point, it’s easier to see that a lot of them apply not only to the checkout process, but to many other areas of the application. With a modular design approach, these modules can be created so that they are usable in this particular design as well as in future ones.

[Atomic design](https://bradfrost.com/blog/post/atomic-web-design/) is worth mentioning as a methodology that can accelerate this process of creating modular designs. This methodology analyzes the relationships between the different parts of the system and how they interrelate, using chemistry as an analogy. Going through the steps is pretty much the reverse of our previous exercise:

1.  We start from the **atoms**, which are the smallest modules in the system (in our example, the buttons, typography and iconography).
2.  The modules grow in complexity, binding together into **molecules**, which provide more functionality (in our example, the checkout steps indicators and the related products module).
3.  Then, there are **organisms**, which are molecules that are grouped together in the application (in our example, the application’s header and various forms).
4.  Leaving the chemistry analogy, the next level is the **templates**, which are predefined structures where organisms are placed.
5.  Lastly, there are **pages**, which are instances of templates.

The missing piece here is a way to document the modules that have been identified. This is not only a matter of creating a specification document to capture how the modules need to be built, or writing guidelines that capture high-level definitions such as brand colors and font families (which are typical of any standard style guide). Rather, the documentation needs to be more sophisticated and dynamic, so that when these modules change (and you know they will!), the documentation doesn’t become obsolete. This is exactly where living styles guides fill in the gap!

## Using A Living Style Guide

A living style guide can be very useful during the design process because it provides several things.</p>

### A Baseline to Work With

Instead of starting from scratch every time, the style guide provides the visual direction and the modules you should use to create the design.

Because a living style guide is generated from actual code, it reflects the latest and greatest version of the implemented design.</p>

### Documentation of Design Solutions

The knowledge that has been acquired to resolve a particular UI or UX problem can be consigned for later use.

This helps to maintain consistency in the implementation, encouraging you to fit any new solution into part of the current design.

You will be developing patterns that users can get familiar with, thus enhancing usability.</p>

### Ease of Communication

The guide helps to communicate the design by providing the most up-to-date representation of the UI (unlike static mockups, which get outdated quickly).

A common UI language is developed because you have to name the various elements in the style guide. This requires collaboration not only among UI designers, but between the designers and developers, which is a great advantage when you have to communicate how a design should be implemented.

Whether you have an existing style guide or are planning to create one, automating the process will put you in the right direction, driving the design process in a modular way. So, if you are ready to shop for a generator of living style guides, then I’d recommend the following resources:

*   “[An In-Depth Overview of Living Style Guide Tools](https://www.smashingmagazine.com/2015/04/an-in-depth-overview-of-living-style-guide-tools/),” Robert Haritonov, Smashing Magazine
*   “[Overview of Pattern Library Generators](https://github.com/davidhund/styleguide-generators),” David Hund, GitHub
*   “[Style Guide Generator Roundup](https://alistapart.com/blog/post/style-guide-generator-roundup),” Susan Robertson, A List Apart

## Don’t Take It To The Extreme!

Now that we have looked at how to finetune the design process to incorporate modularity, as well as the advantages of a living style guide, let’s explore some of the common pitfalls you might encounter along the way.</p>

### The Style Guide Does Not Replace Design Work

It’s not uncommon to hear from managers that, once the living style guide is in place, most of the design work is done. While a lot of the repetitive and trivial work is done (like prototyping the different states of a button over and over), consider that:

*   new features will continually need to be built,
*   finding a solution involves making design decisions.

So, yes, having a living style guide and following style guide-driven development improves the development workflow, but it doesn’t take the designer out of the equation. Having a tool that speeds up workflows and boosts communication is advantageous to both designers and developers. But the great thing about this approach is that it allows a lot of room for the UI to be customized, thereby enhancing the user experience — and figuring that out is part of the designer’s role.</p>

### Don’t Follow Patterns to the Extreme

We should always strive to use patterns in an application. For example, consistent use of colors and font sizes can quickly indicate to the user elements in the UI that can be interacted with. However, avoid using a pattern just because it has been implemented before; rather, use it because it really solves the problem at hand.

For example, if you have established the pattern of displaying toolbars at the top of the screen, this pattern will work in most cases, but there will be times when presenting a contextual toolbar, closer to where the user is taking action, makes more sense. So, always question whether reuse of a pattern prioritizes ease of implementation over the user experience.</p>

### Don’t Overlook Design Iteration

This ties in a bit to the previous point. Don’t overlook the value of iteration and innovation when trying new patterns and finding ways to design an interface, even if at first sight they do not follow the style guide. The style guide should not be a rein on your effort to create the best user experience possible. Rather, as the name suggests, it should be a guide, a starting point to help you resolve problems by tapping into previous work and experience. Iteration during the design phase should continue to be as important as ever and should spur you to improve on established patterns.</p>

### The Maintenance Burden

Among the gazillion things your job involves, maintaining the style guide should be the last thing that feels like a burden. To overcome this, I find the following practices helpful:

*   Find a documentation system that is easy to install and easy to interact with on a regular basis.
*   Make documentation updates a part of your workflow, rather than an afterthought once the implementation is already out. Document as you go!
*   Establish guidelines that make it easy for everybody to contribute to the documentation. This will distribute the workload and increase the sense of ownership.</p>

## Design Modular To Build Modular

Creating a flexible UI system that is consistent and easy to customize, while also scalable and cost-efficient, depends not only on how it is built, but on how it is designed. A library of components has very little value if every new design is created independently, ignoring established standards and patterns.

On the flip side, it’s not about making cookie-cutter interfaces that reuse the same styles and patterns because it’s convenient. A good design is effective not because of its uniqueness, but because it **combines both form and function to create a great experience**. This goal should always be top of mind, and using a method such as style guide-driven development to bring modularity to both design and development should help you to create a cohesive UI system that achieves this goal.

{{< signature "cc, ml, al, il" >}}

