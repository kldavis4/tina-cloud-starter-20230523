---
title: 'Material Design Text Fields Are Badly Designed'
slug: material-design-text-fields
author: adam-silver
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0fef5d1d-7c73-48af-b4bc-c5cb8c9672b6/material-design-text-fields.jpg
date: 2021-02-24T12:00:00.000Z
summary: >-
  Where to put the label in a web form? In the early days, we talked about left-aligned labels versus top-aligned labels. These days we talk about floating labels. Let’s explore why they aren’t a very good idea, and what to use instead.
description: >-
  Where to put the label in a web form? In the early days, we talked about left-aligned labels versus top-aligned labels. These days we talk about floating labels. Let’s explore why they aren’t a very good idea, and what to use instead.
categories:
  - UI
  - Design Patterns
  - UX
  - Forms
  - Web Design
---

I’ve been designing forms for over 20 years now, and I’ve tested many of them for large organizations like *Boots*, *Just Eat* and *Gov.uk*. One topic that comes up a lot with forms is: where to put the label. In the early days, we talked about left-aligned labels versus top-aligned labels.

These days the focus is more about placeholders that replace labels and **float labels**. The latter start off inside the input. When the user starts typing, the label ‘floats’ up to make space for the answer:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/53bb9871-acdf-4769-9330-b865b282a6e4/material-design-text-field-example.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/53bb9871-acdf-4769-9330-b865b282a6e4/material-design-text-field-example.png" width="780" height="616" sizes="100vw" caption="Material Design text fields use the float label pattern. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/53bb9871-acdf-4769-9330-b865b282a6e4/material-design-text-field-example.png'>Large preview</a>)" alt="Material Design text fields use the float label pattern" >}}

Some people assume float labels are best because [Google’s Material Design](https://material.io/components/text-fields) uses them. But in this case, Google is wrong.

Instead, I recommend using conventional text fields which have:

- The label outside the input (to tell the user what to type),
- A distinct border all the way around (to make it obvious where the answer goes).

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/52af2001-ee2e-436b-9f1c-74174fec93c9/2-material-design-text-fields-1.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/52af2001-ee2e-436b-9f1c-74174fec93c9/2-material-design-text-fields-1.jpg" width="780" height="680" sizes="100vw" caption="A conventional text field" alt="A conventional text field" >}}

In this article, I’ll explain why I always recommend **conventional text fields** and why Google is wrong about using float labels for Material Design.

## Float Labels Are Better Than A Common Alternative But They’re Still Problematic

Float labels were designed to address some problems with a commonly used alternative: **placeholder labels**. That’s where the label is placed *inside* the input but disappears when the user starts typing:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/76c71c6f-7a63-4b70-b695-fb530727112a/6-material-design-text-fields.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/76c71c6f-7a63-4b70-b695-fb530727112a/6-material-design-text-fields.jpg" width="780" height="582" sizes="100vw" caption="Placeholder label text field." alt="Placeholder label text field" >}}

Having seen lots of people interacting with forms through my work first hand I know that [placeholder labels are problematic](https://adamsilver.io/articles/placeholders-are-problematic/).

This is because, for example, they:

- **disappear as soon as the user types** which can make it harder to remember what the input is for, especially for users with cognitive impairments;
- may be [mistaken for an actual answer causing users to accidentally skip the field](https://www.uxmatters.com/mt/archives/2010/03/dont-put-hints-inside-text-boxes-in-web-forms.php);
- are greyed out to indicate that it’s a label and not an answer &mdash; but this can make it harder to read.

Float labels don’t solve 2 of these problems: poor contrast and the chance of the label being mistaken for an actual answer. And while they attempt to address the problem of the label disappearing, in doing so, [float labels introduce lots of other problems](https://adamsilver.io/blog/float-labels-are-problematic/), too.

For example, the size of the label has to be tiny in order to fit inside the box, which can make it hard to read. And long labels cannot be used as they’ll get **cropped by the input**:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ef3a224c-382c-492a-832a-6a6d782477cd/float-label-overflow-example.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ef3a224c-382c-492a-832a-6a6d782477cd/float-label-overflow-example.png" width="780" height="616" sizes="100vw" caption="Long labels get cut off with Material Design text fields. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ef3a224c-382c-492a-832a-6a6d782477cd/float-label-overflow-example.png'>Large preview</a>)" alt="Long labels get cut off with Material Design text fields" >}}

{{% feature-panel %}}

## Conventional Text Fields Are Better Than Both Placeholder Labels And Float Labels

Conventional text fields don’t have the above problems because it’s clear where the answer goes and they have a legible, readily available label. The **labels can be of any length** and hint text, should it be needed, is easy to accommodate as well.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/00832fcb-d727-42cf-b8b7-538572102585/3-material-design-text-fields.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/00832fcb-d727-42cf-b8b7-538572102585/3-material-design-text-fields.jpg" width="780" height="680" sizes="100vw" caption="Conventional text fields can easily contain long label text." alt="Conventional text fields can easily contain long label text" >}}

I’ve watched **hundreds of people** interact with forms and seen many of them struggle. But not once was that down to the use of a conventional text field. They take up a bit more vertical space. But saving space at the cost of clarity, ease of use and accessibility is a bad tradeoff to make.

## Google’s Test Didn’t Include Conventional Text Fields

Google’s article, [The Evolution of Material Design’s Text Fields](https://medium.com/google-design/the-evolution-of-material-designs-text-fields-603688b3fe03) shows that only 2 variants were tested, both of which used float labels.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7088fbd6-001e-4134-ac17-9b5df5c0041c/4-material-design-text-fields.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7088fbd6-001e-4134-ac17-9b5df5c0041c/4-material-design-text-fields.jpg" width="800" height="530" sizes="100vw" caption="The 2 variants of text fields that Google tested: float labels with underlines and a white transparent background (left) and float labels with grey backgrounds (right). (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a45bcda7-4200-430f-8806-4df0579c94e8/4-material-design-text-fields.png'>Large preview</a>)" alt="The 2 variants of text fields that Google tested: float labels with underlines and a white transparent background (left) and float labels with grey backgrounds (right)." >}}

Crucially the test didn’t include conventional text fields which means they haven’t actually compared the usability of their float label design **against conventional text fields**. And having read Google’s responses to the comments on their article, it seems that usability was not their top priority.

{{% ad-panel-leaderboard %}}

## Google Inadvertently Prioritized Aesthetics Over Usability

I looked into why Material Design uses float labels and discovered comments from Michael Gilbert, a designer who worked on them.

The comments indicate that they tried to balance aesthetics and usability.

[Matt Ericsson commented](https://medium.com/@mattericsson/this-seems-to-imply-that-there-was-more-of-an-emphasis-on-form-over-function-in-the-original-dbefb328c21e):

<blockquote><p>This seems to imply that there was more of an emphasis on form over function [...] or even a desire to simply differentiate Material components from tried and true (boring) input boxes. [...] was there research conducted on the original inputs that validated that they met a goal that was not being met by box inputs? Is there something that stood out as valuable going with a simple underline?</p></blockquote>

[Google’s response](https://medium.com/@mdgilbert/hi-matt-1ab1b86e53a4):

<blockquote><p>The design decisions behind the original text field predate my time on the team, but I think the goal was likely similar [to this research]: Balance usability with style. I believe at the time we were leaning towards <strong>minimalism</strong>, emphasizing color and animation to highlight usability.</p></blockquote>

[Denis Lesak commented](https://medium.com/@denislesak/really-appreciate-you-sharing-the-behind-the-scenes-story-98c5d2896637):

<blockquote><p>[...] this is one of those moments where I wonder why all of this research was necessary as I have long thought that the old design was flawed for all the reasons you mentioned.</p></blockquote>

[Google’s response](https://medium.com/@mdgilbert/hello-denis-a0fcdb7c40a4):

<blockquote><p>[...] the goal of the research here wasn’t to simply determine that one version was better than another [...]. This study was instead focused on identifying the characteristics of the design that led to the most usable, most <strong>beautiful experiences</strong>.</p></blockquote>

Even though Google aimed for balance, in the end they inadvertently sacrificed usability for ‘minimalism’ and ‘a beautiful experience’.

But [aesthetics and usability are not in competition with each other](https://uxdesign.cc/accessibility-drives-aesthetics-5aef77b5d2aa). Something can look good without causing problems for users. In fact, these qualities go hand in hand.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/64430ba0-4402-45a1-a133-b0dcedff9b29/example-form.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/64430ba0-4402-45a1-a133-b0dcedff9b29/example-form.png" width="800" height="824" sizes="100vw" caption="An example form using conventional text fields that look good and function well too. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/64430ba0-4402-45a1-a133-b0dcedff9b29/example-form.png'>Large preview</a>)" alt="An example form using conventional text fields that look good and function well too" >}}

## Conclusion

Float labels are certainly less problematic than placeholder labels. But conventional text fields are better than float labels because they look like form fields and the label is easy to read and available at all times.

Aesthetics are important, but putting the label inside the box does not make it look beautiful. What it does do, however, is make it demonstrably harder to use.

### Smashing Editor's note

At the moment of writing, here at Smashing Magazine we are actually using the floating label pattern that Adam heavily criticizes in this article. From our usability tests we can confirm that **floating labels aren't a particularly great idea**, and we are looking into adjusting the design — by moving to conventional text fields — soon.

### Acknowledgments

*Thanks to [Caroline Jarrett](https://twitter.com/cjforms) and [Amy Hupe](https://twitter.com/Amy_Hupe) for helping me write this. And thanks to [Maximilian Franzke](https://twitter.com/maedmaex), [Olivier Van Biervliet](https://twitter.com/ovan), [Dan Vidrasan](https://twitter.com/danvdrsn), [Fabien Marry](https://twitter.com/Fabien_UX) for their feedback on an earlier draft of this article.*

{{< signature "vf, yk, il" >}}
