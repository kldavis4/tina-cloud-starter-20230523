---
title: 'Accessible Images For When They Matter Most'
slug: accessible-images
author: carie-fisher
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a56c3c17-0d11-4755-916e-483ba80bc899/accessible-images-sharing-card.png
date: 2020-05-15T09:30:00.000Z
summary: >-
  Creating accessible images seems like a simple topic at first glance &mdash; you just need to add alt text to an image, right? But the topic is much more nuanced than some people think. In this article, we will review the different types of images, dive into some real-world examples of inaccessible public service announcements (PSAs), and discuss which elements matter most when critical messages need to reach everyone.
description: >-
  In this article, we will review the different types of images, dive into some real-world examples of inaccessible public service announcements, and discuss which elements matter most when critical messages need to reach everyone.
categories:
  - Accessibility
  - UX
  - Usability
---

<p>When it comes to informing the public about critical health issues, timing is everything. The information you consume today could save your life tomorrow. And with more than <a href="https://www.inc.com/molly-reynolds/how-to-spot-visual-auditory-and-kinesthetic-learni.html">65% of the population being visual learners</a> &mdash; meaning they learn and remember best through visual communication &mdash; the job of creating and sharing accessible images has never been more important. This is especially true for public service announcements (PSAs) aimed at providing crucial and urgent information to the public.</p>

<p>But what happens when your users have visual impairments? Or dyslexia? Or cognitive disorders? How do they receive and understand this visual information? What elements make an image accessible or inaccessible?</p>

## Image Types And Alts

<p>Before we dissect an image and examine each element that can make or break its accessibility, we first need to take a step back and think about the purpose of the image. Is it to inform a user? Elicit an emotion? Is the image acting as a link? Or is it purely eye-candy?</p>

<p>There are a number of questions that can help you determine how best to convey the image information to a person using an <a href="https://www.nichd.nih.gov/health/topics/rehabtech/conditioninfo/device">assistive technology</a> (AT) device, like a screen reader.</p>

<blockquote>“What type of message is the image trying to convey?”<br /><br />“Is the message simple, complex, emotional, or actionable?”</blockquote>

<p>Using a tool such as an online <a href="https://www.w3.org/WAI/tutorials/images/decision-tree/">image decision tree</a> or the simplified chart shown below can help you decide which category your image belongs to. Or just imagine your image has &mdash; <em>poof!</em> &mdash; vanished. Then ask yourself:</p>

<blockquote>“Do I understand the content that remains?”</blockquote>

<p>If the answer is yes, it is <a href="#decorative">decorative</a>. If not, the image is <a href="#informative">informative</a> and contextually necessary. Once you determine what kind of image you are working with, there are some basic accessibility guidelines to consider.</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/15b92e6f-1a81-4339-9c14-efb9103a5573/1-accessible-images.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/15b92e6f-1a81-4339-9c14-efb9103a5573/1-accessible-images.png" sizes="100vw" caption="Image alt flow chart (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/15b92e6f-1a81-4339-9c14-efb9103a5573/1-accessible-images.png'>Large preview</a>)" alt="Image alt flow chart showing the steps to help decide whether an image is decorative or informative and what subtype it might fall under" >}}

### Decorative Images

<p>If you decide your image is decorative, then programmatically the image needs to be hidden. One way to do this is to use an empty/null alternative text attribute. This sends a signal to the AT devices to ignore this image as it is not needed to understand the content or action on the page. There are many ways to hide alternative text including using an empty/null alt (e.g. <code>&lt;img alt=""&gt;</code>), <a href="https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA">using ARIA</a> (e.g. <code>&lt;img role="presentation"&gt;</code>, <code>&lt;img role="none"&gt;</code>, or <code>&lt;img aria-hidden="true"&gt;</code>), or by implementing the image as a CSS background.</p>

<p><strong>Note:</strong> <em>An empty/null alternative text attribute is not the same as a missing alternative text attribute. If the alternative text attribute is missing, the AT device might read out the file name or surrounding content in an attempt to give the user more information about the image. While</em> <code>aria-hidden="true"</code> <em>is an option to hide images, be cautious where you apply it as it will remove the entire element from the accessibility API.</em></p>

{{% feature-panel %}}

<p>In the example below, we see a giant letter “S” and a drawing of a black cat with green eyes used to make the <a href="https://www.smashingmagazine.com/2012/04/drop-caps-historical-use-and-current-best-practices/">drop cap</a> look a bit more fun on a Smashing Magazine article.</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e94a1937-5afc-4704-979e-a2ceffa1c406/smashing-cat.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e94a1937-5afc-4704-979e-a2ceffa1c406/smashing-cat.png" sizes="100vw" caption="Article screenshot with S drop cap and cat illustration (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e94a1937-5afc-4704-979e-a2ceffa1c406/smashing-cat.png'>Large preview</a>)" alt="Article screenshot with the S drop cap and a curious black cat with green eyes illustration" >}}

<p>When we remove the drop cap illustration, what changes? Certainly, there are visual differences, but no information is lost.</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/462dd026-48da-4b2e-94fb-afdd031fbe03/smashing-cat-cropped.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/462dd026-48da-4b2e-94fb-afdd031fbe03/smashing-cat-cropped.jpg" sizes="100vw" caption="Article screenshot without a drop cap or illustration (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/462dd026-48da-4b2e-94fb-afdd031fbe03/smashing-cat-cropped.jpg'>Large preview</a>)" alt="Article screenshot without a drop cap or illustration" >}}

<pre><code class="language-html">&lt;div class="drop-caps" aria-hidden="true"&gt;
	&lt;img src=".../images/drop-caps/s.svg" alt=""&gt;
	&lt;img src=".../images/drop-caps/character-12.svg" alt=""&gt;
&lt;/div&gt;
</code></pre>

<p>In this drop cap example, both <code>aria-hidden="true"</code> and an empty/null alt <code>&lt;img alt=""&gt;</code> were used to hide the images from assistive technology devices. While this kind of redundancy is not necessary to make it accessible &mdash; it is also not harmful in this particular situation since the drop caps <code>&lt;div&gt;</code> does not contain any additional information we would need to expose to an AT user. Just remember: <strong>when it comes to accessible code, more is not always better</strong>.</p>

<p>Beyond programmatically hiding your image &mdash; there is not much more you need to consider when it comes to decorative images. If you are saying “But wait, what about X?” or “How about Y?” then you might need to go back to the image decision tree tools and re-evaluate your image &mdash; it might not be 100% decorative after all. One of the most difficult types of images to categorize tends to be the “emotional/mood” based images since this subtype is a bit subjective. What one person considers decorative another person might consider informative, so use your best judgment.</p>

### Informative Images

<p>If you decide your image is informative, there are a lot more things to consider. For AT devices to understand the message or intent of an image, informative images must have <a href="https://www.w3.org/WAI/WCAG21/Understanding/non-text-content.html">programmatically-discernible alternative text</a>. Typically, this is accomplished using the <code>alt="[some description]"</code> method, but there are many <a href="https://cariefisher.com/a11y-svg/">alternative ways to add image information</a> depending on its subtype, type of image, and context (e.g. complex vs simple, SVG vs img). But <strong>having alternate text is not enough</strong> &mdash; it must also be meaningful. For example, if your image is about feeling safe at home, but your alternative information says “house” &mdash; does that convey the full message?</p>

<p>An example of an informative image is the following Smashing Magazine logo. If we ask the same question as before (does the context or content change if this image is missing?), then the answer is “yes.” In this example, the logo is both informative and actionable since it is both an image and a link. We can see from the code snippet that <code>&lt;a title="Back to the homepage"&gt;</code> is the link title and the image alternative text is <code>&lt;img alt="Smashing Magazine"&gt;</code>. When we fire up an AT device &mdash; like a screen reader &mdash; we should hear both pieces of information conveyed.</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d99ea7f0-5ad1-4c8a-a8da-bde58a39785c/smashing-logo.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d99ea7f0-5ad1-4c8a-a8da-bde58a39785c/smashing-logo.png" sizes="100vw" caption="Smashing Magazine logo (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d99ea7f0-5ad1-4c8a-a8da-bde58a39785c/smashing-logo.png'>Large preview</a>)" alt="Smashing Magazine logo" >}}

<div class="break-out">

<pre><code class="language-html">&lt;div class="logo"&gt;
	&lt;a href="/" title="Back to the homepage"&gt;
		&lt;picture&gt;
		&lt;source media="(min-width: 1350px)" srcset=".../images/logo-full.svg"&gt;
		&lt;img src=".../images/logo/logo.svg" alt="Smashing Magazine"&gt;
		&lt;/picture&gt;
	&lt;/a&gt;
&lt;/div&gt;
</code></pre>
</div>

<p>Hearing both the phrase “back to the homepage” and “Smashing Magazine” in one feature is OK since each phrase is unique and connected to a different purpose.</p>

<p>For more complex alternative text phrases, <strong>conduct the telephone test</strong>. For example, if you called up a friend and said “purple slug” and hung up the phone your friend would probably be confused, but also might think of a purple slug &mdash; but in what context? If you called a friend and said “the purple slug is eating my hydrangeas,” that would paint a more vivid picture &mdash; without adding a lot of additional characters or effort.</p>

<p>Of course, an AT user will have to listen to your alternative text, so don’t go overboard. That is why it is suggested to cap your text at 150 characters. If you need to add more context to the image (e.g. complex image), there are other, more descriptive patterns or methods you can use to add more detail.</p>

{{% ad-panel-leaderboard %}}

## World Beyond Image Alts

<p>Now that we covered image types and alternative text attribute basics, let’s look beyond and consider some additional image elements:</p>

<ul>
<li><a href="#color-and-contrast">Color and Contrast</a></li>
<li><a href="#typography-and-layout">Typography and Layout</a></li>
<li><a href="#copy-and-icons">Copy and Icons</a></li>
</ul>

<p>In each real-world PSA example, we will look at the image <strong>through the lens of a different type of disability</strong> &mdash; keeping in mind that simulators are tools and may not represent an individual’s true experience. Yet, by using such tools, we can begin to build empathy into our designs and really consider the different ways our images are being consumed.</p>

<p><strong>Note</strong>: <em>To be clear, the following examples are for illustrative and educational purposes only and not meant to call-out or otherwise pass judgment about the designs in question. Also, there may be multiple issues in one PSA, but we will just focus on one issue type per example. There will be a lot of opportunities for improvement in the area of digital communications when the dust settles on COVID-19 and accessibility is just one more area to consider reviewing.</em></p>

### Color And Contrast

<p>The beating heart of design arguably is color, and if color is the heart of design, then contrast is the muscle. Without good color contrast levels in place elements like words, icons, and other graphical shapes are hard to discern and the design can quickly become inaccessible. But what happens when you perceive color and contrast differently than others &mdash; does the same message and intent come through? How can we reach people with color-sensing issues? <a href="https://en.wikipedia.org/wiki/Color_blindness">Color blindness</a> &mdash; is a real concern for accessibility-focused designers.</p>

#### Who Color And Contrast Can Affect

<ul>
<li>It is estimated that <a href="https://www.colourblindawareness.org/colour-blindness/">300 million</a> people worldwide are <strong>color blind</strong>, and approximately 95% of those inflicted are male (1 in 12 men vs 1 in 200 women are color blind). There are many different variants of color blindness, with red/green color blindness being the most common, followed by blue/yellow, and total color blindness being the most rare.</li>
<li>Globally there are <a href="https://www.who.int/blindness/publications/globaldata/en/">246 million</a> people with <strong>low vision</strong>. People with <a href="https://en.wikipedia.org/wiki/Visual_impairment">visual impairments</a> such as glaucoma, cataracts, macular degeneration, diabetic retinopathy, corneal clouding, etc, may have issues with text contrast. People with partial sight and older adults also often experience limited color vision.</li>
<li>People using monochrome displays or in certain situations (e.g. low lighting in a room) might have <strong>trouble with contrast</strong>. People using text-only, limited-color stylesheets, or in certain situations (e.g. too much glare on a screen) might have trouble discerning colors, too.</li>
</ul>
 
#### PSA Color Review

<p>In the first example, we are reviewing PSAs from the non-profit group called the Ad Council &mdash; one of the oldest and most prolific producers of such material in the US. The aim of these “<a href="https://coronavirus.adcouncilkit.org/share-on-social/">higher risk assets</a>” is to reach populations considered more susceptible to contracting and becoming seriously ill by the novel coronavirus (one of the groups that need this information the most).</p>

<p>First, we see the unedited version of the PSAs:</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/97d1f1dd-cac6-409a-8930-fe72ab8e3939/3-accessible-images.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/97d1f1dd-cac6-409a-8930-fe72ab8e3939/3-accessible-images.png" sizes="100vw" caption="Original CDC + Ad Council PSAs on COVID-19 (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/97d1f1dd-cac6-409a-8930-fe72ab8e3939/3-accessible-images.png'>Large preview</a>)" alt="Unedited teal blue, salmon pink, and blush colored public service announcements created by the CDC and the Ad Council which have color contrast issues" >}}

<p>Next, we can see two types of color blindness simulated using the <a href="https://chrome.google.com/webstore/detail/chromelens/idikgljglpfilbhaboonnpnnincjhjkd?hl=en">ChromeLens extension</a>. ChromeLens is a Google Chrome extension that provides a suite of tools to help with web accessibility development and includes the Lens Vision Simulator, which transforms the colors on a website simulating what a colorblind person might see.</p>

<p>Simulated PSA with Deuteranopia (red/green-blindness):</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b0c74f71-3fe1-428e-b95a-fc0e78a237d6/5-accessible-images.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b0c74f71-3fe1-428e-b95a-fc0e78a237d6/5-accessible-images.png" sizes="100vw" caption="PSA with Deuteranopia (red/green-blindness) color filter applied (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b0c74f71-3fe1-428e-b95a-fc0e78a237d6/5-accessible-images.png'>Large preview</a>)" alt="PSA with Deuteranopia (red/green-blindness) color filter applied" >}}

<p>Simulated PSAs with Protanomaly (red-weak):</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/be35e30e-2e49-499b-b82e-e8f0e3c79023/6-accessible-images.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/be35e30e-2e49-499b-b82e-e8f0e3c79023/6-accessible-images.png" sizes="100vw" caption="PSAs with Protanomaly (red-weak) color filter applied (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/be35e30e-2e49-499b-b82e-e8f0e3c79023/6-accessible-images.png'>Large preview</a>)" alt="PSAs with Protanomaly (red-weak) color filter applied" >}}

<p>Below is a breakdown of some color contrast ratios found on the PSAs between the different color blindness simulators.</p>

<p>Original PSA &mdash; color contrast ratio of 1.26:1 with the text “Have” against the background:</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/856fc334-fd83-4329-9261-8d7538638cf8/7-accessible-images.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/856fc334-fd83-4329-9261-8d7538638cf8/7-accessible-images.png" sizes="100vw" caption="Original PSA – color contrast ratio of 1.26:1 with the text “Have” against the background (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/856fc334-fd83-4329-9261-8d7538638cf8/7-accessible-images.png'>Large preview</a>)" alt="Original PSA – color contrast ratio of 1.26:1 with the text “Have” against the background with salmon colored PSA" >}}

<p>Deuteranopia simulation filter applied &mdash; color contrast ratio of 1.07:1 with the text “Have” against the background:</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/14c75b6c-b823-43dc-b14a-bcb84ad6e137/8-accessible-images.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/14c75b6c-b823-43dc-b14a-bcb84ad6e137/8-accessible-images.png" sizes="100vw" caption="Deuteranopia simulation filter applied – color contrast ratio of 1.07:1 with the text “Have” against the background (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/14c75b6c-b823-43dc-b14a-bcb84ad6e137/8-accessible-images.png'>Large preview</a>)" alt="Deuteranopia simulation filter applied – color contrast ratio of 1.07:1 with the text “Have” against the background with lime green colored PSA" >}}

<p>Protanomaly simulation filter applied &mdash; color contrast ratio of 1:15:1 with the text “Have” against the background:</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b7b8adea-6219-4105-a1ee-ae388498d30a/9-accessible-images.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b7b8adea-6219-4105-a1ee-ae388498d30a/9-accessible-images.png" sizes="100vw" caption="Protanomaly simulation filter applied – color contrast ratio of 1:15:1 with the text “Have” against the background (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b7b8adea-6219-4105-a1ee-ae388498d30a/9-accessible-images.png'>Large preview</a>)" alt="Protanomaly simulation filter applied – color contrast ratio of 1:15:1 with the text “Have” against the background with tan-orange colored PSA" >}}

<p>While these PSAs incorporate a variety of striking color choices and are visually appealing (when testing the text against the background in these images), many of the combinations do not pass the <a href="https://www.w3.org/WAI/standards-guidelines/wcag/">Web Content Accessibility Guidelines</a> (WCAG) color contrast ratios. This is true even for the unedited versions of these designs, but when we apply the ChromeLens color blindness simulator for Deuteranopia (red/green-blindness) Protanomaly (red-weak), the color contrast ratios get even worse (1.26:1 vs 1.07:1 and 1:15:1). To make these PSAs more accessible, we would want to bump up the contrast so people with color-related vision disorders could read the text.</p>

#### PSA Contrast Review

<p>Going back to the “higher-risk assets” from the Ad Council, we can see how the PSAs look like to people in two different low vision situations.</p>

<p>First, we see the unedited version of the PSAs:</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/97d1f1dd-cac6-409a-8930-fe72ab8e3939/3-accessible-images.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/97d1f1dd-cac6-409a-8930-fe72ab8e3939/3-accessible-images.png" sizes="100vw" caption="Original CDC + Ad Council PSAs on COVID-19  (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/97d1f1dd-cac6-409a-8930-fe72ab8e3939/3-accessible-images.png'>Large preview</a>)" alt="Unedited teal blue, salmon pink, and blush colored public service announcements created by the CDC and the Ad Council which have color contrast issues" >}}

<p>Next, using the <a href="https://chrome.google.com/webstore/detail/nocoffee/jjeeggmbnhckmgdhmgdckeigabjfbddl">NoCoffee Vision Simulator</a> tool, we can see how the PSAs might look to someone with low vision and cataracts.</p>

<p>PSAs with simulated low vision filter applied:</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0aa1e941-149f-494b-b727-a09116629393/2-accessible-images.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0aa1e941-149f-494b-b727-a09116629393/2-accessible-images.png" sizes="100vw" caption="PSAs with simulated low vision filter applied (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0aa1e941-149f-494b-b727-a09116629393/2-accessible-images.png'>Large preview</a>)" alt="PSAs with low vision filter applied" >}}

<p>PSAs with simulated cataract filter applied:</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f42641cf-f06e-4e8d-b9bd-8f23857d2894/4-accessible-images.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f42641cf-f06e-4e8d-b9bd-8f23857d2894/4-accessible-images.png" sizes="100vw" caption="PSAs with cataract filter applied (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f42641cf-f06e-4e8d-b9bd-8f23857d2894/4-accessible-images.png'>Large preview</a>)" alt="PSAs with cataract filter applied" >}}

<p>Below is a breakdown of some color contrast ratios found on the PSAs between the different low vision simulators.</p>

<p>Original PSA &mdash; color contrast ratio of 1.33:1 with the word “Undergoing” against the background:</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/34d6ceca-cfc0-49e2-88d4-91dc6f436dac/10-accessible-images.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/34d6ceca-cfc0-49e2-88d4-91dc6f436dac/10-accessible-images.png" sizes="100vw" caption="Original PSA – color contrast ratio of 1.33:1 with the word “Undergoing” against the background (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/34d6ceca-cfc0-49e2-88d4-91dc6f436dac/10-accessible-images.png'>Large preview</a>)" alt="Original PSA – color contrast ratio of 1.33:1 with the word “Undergoing” against the background with teal blue colored PSA" >}}

<p>PSA with low vision simulation filter applied &mdash; color contrast ratio of 1.25:1 with the word “Undergoing” against the background:</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d149a2e9-8b46-4b88-9ae8-f037fd497830/11-accessible-images.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d149a2e9-8b46-4b88-9ae8-f037fd497830/11-accessible-images.png" sizes="100vw" caption="PSA with low vision simulation filter applied – color contrast ratio of 1.25:1 with the word “Undergoing” against the background (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d149a2e9-8b46-4b88-9ae8-f037fd497830/11-accessible-images.png'>Large preview</a>)" alt="PSA with low vision simulation filter applied – color contrast ratio of 1.25:1 with the word “Undergoing” against the background with teal blue colored PSA" >}}

<p>PSA with cataract simulation filter applied &mdash; color contrast ratio of 1.06:1 with the word “Undergoing” against the background:</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f3bab6de-3a31-4b3a-92e4-c712fdc9c967/12-accessible-images.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f3bab6de-3a31-4b3a-92e4-c712fdc9c967/12-accessible-images.png" sizes="100vw" caption="PSA with cataract simulation filter applied – color contrast ratio of 1.06:1 with the word “Undergoing” against the background (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f3bab6de-3a31-4b3a-92e4-c712fdc9c967/12-accessible-images.png'>Large preview</a>)" alt="PSA with cataract simulation filter applied – color contrast ratio of 1.06:1 with the word “Undergoing” against the background with teal blue colored PSA" >}}

<p>A lot of people blame color for their design accessibility issues, but these examples show that <strong>contrast plays a key role as well</strong>. Without changing the colors on these PSAs, but by changing the user perspective and blurring or obfuscating the text, we can see that the text on the images is more difficult to read &mdash; even though the contrast ratios didn’t change by much (1.33:1 vs 1.25:1 and 1.06:1). Similar to the color examples (to make these PSAs more accessible), we need to increase the contrast on these images so people with low vision and eye disorders could read the text.</p>

#### Next Steps For Accessible Color And Contrast

<p>Review the <a href="https://www.w3.org/WAI/WCAG21/Understanding/non-text-contrast.html">WCAG color contrast ratio guidelines</a> and use tools like the <a href="https://developer.paciellogroup.com/resources/contrastanalyser/">Colour Contrast Analyser</a> to check your designs. Your images with copy need a color contrast ratio of at least 4.5:1 for regular-sized text, and at least 3:1 for large-sized text (18pt and larger). The color contrast ratio of 3:1 also applies to essential icons. Try a tool like the <a href="https://a11yrocks.com/colorPalette/">A11y Color Palette</a> where you can quickly review all the possible accessible color combinations and create a palette with accessibility in mind. Or use the accessibility features built-in into the palette generator <a href="https://coolors.co/">Coolors</a>.</p>

<p>Next, utilize solid color backgrounds (reading text on busy backgrounds, overlays, textures, or gradients is difficult in general), but especially when the text does not have enough contrast. By picking colors on the opposite ends of the color spectrum and <strong>avoiding red/green and blue/yellow combinations</strong>, you will increase the likelihood that your color and contrast ratios are robust. Use a tool like the <a href="https://chrome.google.com/webstore/detail/chromelens/idikgljglpfilbhaboonnpnnincjhjkd?hl=en">ChromeLens extension</a> to double-check the color contrast with color blindness in mind. Also, be careful with light shades of color &mdash; especially grays &mdash; they are difficult to see for people with low vision. Use tools like <a href="https://chrome.google.com/webstore/detail/nocoffee/jjeeggmbnhckmgdhmgdckeigabjfbddl">NoCoffee Vision Simulator</a> to simulate low vision issues and see how your design holds up in these situations.</p>

<p>Going beyond color contrast ratios, it is also important to not use <a href="https://www.w3.org/WAI/WCAG21/Understanding/use-of-color.html">color alone to convey information</a>. For example, “contact information can be seen in red” or “click the blue button to learn more.” The same is true for <a href="https://www.w3.org/WAI/WCAG21/Understanding/sensory-characteristics.html">sensory characteristics</a> such as shape, color, size, visual location, orientation, or sound &mdash; they cannot be used on their own. For example, if you said "Please click the link to the left of the image for more information," an AT user could have difficulty finding the correct link.</p>

{{% ad-panel-leaderboard %}}

### Typography and Layout

<p>In a perfect world, we would keep our text and images separated. This would allow users to manipulate the typography and layout in any way they would want: font size, letter spacing/kerning, justification, margins/padding, and more. But unfortunately, there are a lot of formats that this kind of separation is difficult or impossible, such as social media posts, emails, PDFs, and other fixed form media.</p>

#### Who Typography And Layout Can Affect

<ul>
<li>Typography is especially important to the estimated <a href="https://dyslexiaida.org/dyslexia-basics/">15–20% of the world’s population with dyslexia</a> &mdash; a learning disorder in which certain letters, numbers, or combinations of letters can be confusing or seem to flip/move around.</li>
<li>People with low vision can have issues with tight letter spacing/kerning, morphing words like “barn” into “bam” or “modern” into “modem” while reading.</li>
<li>For people with attention-deficit disorders and reading or vision-based disabilities, a complex layout is a real barrier. These users have trouble keeping their place and following the flow of the content due to the lack of whitespace and clear linear pathways.</li>
</ul>

#### PSA Typography And Layout Review

<p>Let’s first take a look at a PSA from California’s <a href="https://www.longbeach.gov/globalassets/airport/media-library/images/covid-2019-flyer-english2.jpg">Long Beach Health and Human Services</a>.</p>

<p>If we are looking at this PSA from an accessibility point of view, what typography and layout issues do you see? In what ways could we improve this image?</p>

<p>Original PSA:</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f707ac98-4f56-4e22-95b4-b851d77d616e/14-accessible-images.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f707ac98-4f56-4e22-95b4-b851d77d616e/14-accessible-images.png" sizes="100vw" caption="PSA from Long Beach Health and Human Services (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f707ac98-4f56-4e22-95b4-b851d77d616e/14-accessible-images.png'>Large preview</a>)" alt="PSA from Long Beach Health and Human Services" >}}

<p>Unedited PSA with mark-up and notes:</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/89a58213-010e-4051-b019-29a979570245/15-accessible-images.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/89a58213-010e-4051-b019-29a979570245/15-accessible-images.png" sizes="100vw" caption="PSA from Long Beach Health and Human Services marked up with accessibility design notes (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/89a58213-010e-4051-b019-29a979570245/15-accessible-images.png'>Large preview</a>)" alt="PSA from Long Beach Health and Human Services marked up with accessibility design notes" >}}

<p>If we focus on the typography and layout the following elements stand out:</p>

<table class="tablesaw break-out" data-tablesaw-mode="swipe" data-tablesaw-minimap>
	<tbody>
		<tr>
			<td>Red hand-drawn lines</td>
			<td>Illustrating the multiple “rivers of space” created by the justified alignment.</td>
		</tr>
		<tr>
			<td>Blue dotted boxes</td>
			<td>Outlining six different layout changes.</td>
		</tr>
		<tr>
			<td>Pink numbers</td>
			<td>Highlighting the 14 different typography treatments discovered (ignoring the logo). Some changes are more obvious like font family or color changes, some are more subtle like alignment, size, or weight changes in the typography.</td>
		</tr>
		<tr>
			<td>Green question marks</td>
			<td>What does this equation even mean? Cognitively this is a difficult thing to ascertain given the odd layout.</td>
		</tr>
		<tr>
			<td>Black lines and dots</td>
			<td>Expected 12 points of visual interest in an UX eye-tracking test based on the order of the content blocks (top to bottom, left to right) and typical equation flow <code>(X + Y = Z)</code>.</td>
		</tr>
	</tbody>
</table>

<p>Let’s look at another PSA and again evaluate the typography and layout from an accessibility point of view. This time, the image was created by the <a href="https://content.govdelivery.com/attachments/fancy_images/MDPGC/2020/03/3197829/2994306/infographic-illness-prevention_crop.jpg">Health Department of Prince George County</a> in Maryland.</p>

<p>Original PSA:</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ae306563-e124-442f-b922-146aeb376095/16-accessible-images.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ae306563-e124-442f-b922-146aeb376095/16-accessible-images.png" sizes="100vw" caption="PSA from the Health Department of Prince George County (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ae306563-e124-442f-b922-146aeb376095/16-accessible-images.png'>Large preview</a>)" alt="PSA from the Health Department of Prince George County" >}}

<p>Unedited PSA with mark-up and notes:</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3b3574c7-f1fd-4bac-b6b7-fb69fc9a0381/17-accessible-images.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3b3574c7-f1fd-4bac-b6b7-fb69fc9a0381/17-accessible-images.png" sizes="100vw" caption="PSA from the Health Department of Prince George County marked up with accessibility design notes (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3b3574c7-f1fd-4bac-b6b7-fb69fc9a0381/17-accessible-images.png'>Large preview</a>)" alt="PSA from the Health Department of Prince George County marked up with accessibility design notes" >}}

<p>If we focus on the typography and layout the following elements stand out:</p>

<table class="tablesaw break-out" data-tablesaw-mode="swipe" data-tablesaw-minimap>
	<tbody>
		<tr>
			<td>Blue dotted boxes</td>
			<td>Outlining nine different layout changes.</td>
		</tr>
		<tr>
			<td>Green numbers</td>
			<td>Highlighting the 11 different typography treatments discovered (ignoring the logos). Some changes are more obvious like font family or color changes, some are more subtle like alignment, size, or weight changes in the typography.</td>
		</tr>
		<tr>
			<td>Black lines and dots</td>
			<td>Expected 10 points of visual interest in an UX eye-tracking test based on the order of the content blocks (top to bottom, left to right) and numbering order (1 to 6) forming a zig-zag type eye movement.</td>
		</tr>
	</tbody>
</table>

<p>So far we’ve seen some examples where there are a lot of typography changes and the layouts are complex. Now, let’s review a cleaner PSA. This one is from the <a href="https://preventionactionalliance.org/wp-content/uploads/2020/03/StopSpreadOfGerms_8.5x11_CPHFCPH_3.9.2020-791x1024.png">Prevention Action Alliance</a> out of Columbus, Ohio.</p>

<p>Original PSA:</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a5d23158-8ef0-4742-936e-59c1dd570099/19-accessible-images.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a5d23158-8ef0-4742-936e-59c1dd570099/19-accessible-images.png" sizes="100vw" caption="PSA from the Prevention Action Alliance (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a5d23158-8ef0-4742-936e-59c1dd570099/19-accessible-images.png'>Large preview</a>)" alt="PSA from the Prevention Action Alliance" >}}

<p>Unedited PSA with mark-up and notes:</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/faf151ab-4111-436a-afd9-b7c49d6cdc0a/18-accessible-images.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/faf151ab-4111-436a-afd9-b7c49d6cdc0a/18-accessible-images.png" sizes="100vw" caption="PSA from the Prevention Action Alliance marked up with accessibility design notes (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/faf151ab-4111-436a-afd9-b7c49d6cdc0a/18-accessible-images.png'>Large preview</a>)" alt="PSA from the Prevention Action Alliance marked up with accessibility design notes" >}}

<table class="tablesaw break-out" data-tablesaw-mode="swipe" data-tablesaw-minimap>
	<tbody>
		<tr>
			<td>Blue dotted boxes</td>
			<td>Outlining three different layout changes.</td>
		</tr>
		<tr>
			<td>Pink numbers</td>
			<td>Highlighting the four different typography treatments discovered (ignoring the logos). In this case, only one font family was used, with variations only on size, color, and weight.</td>
		</tr>
		<tr>
			<td>Black lines and dots</td>
			<td>Expected eight points of visual interest in an UX eye-tracking test based on the order of the content blocks (top to bottom).</td>
		</tr>
	</tbody>
</table>
 
<p>The third PSA example is more consistent when it comes to typography and layout, and has more overall whitespace and a linear visual pathway compared to the first two examples.</p>

#### Next Steps For Accessible Typography And Layout

<p>Less is more when it comes to accessible typography, so limit the number of different font families and variations such as <em>italic</em>, <strong>bold</strong>, ALL CAPS, or other styling methods that may make the content difficult to read. The research is not conclusive about whether <a href="https://alexpoole.info/blog/which-are-more-legible-serif-or-sans-serif-typefaces/">serif or sans-serif typefaces are easier to read</a>, but if you choose font families that have clearly defined letter shapes it is more likely that the font will be accessible. Some common offenders to look out for when choosing an inclusive font include the “I” (ex. India), “l” (ex. lettuce), and “1” (ex. one). Likewise, characters like “b” and “d” and “q” and “p” can sometimes be mirrored (either left-right or up-down), and the letter “B” and the number “8” oftentimes look too similar.</p>

<p><strong>In regards to layout, less is also more</strong>. Try and repeat patterns whenever possible and limit the width of any blocked section to 80 characters (or 40 characters for logograms). Likewise, avoid paragraph alignment which creates whitespace or “rivers of space” within the content (e.g. justified alignment). Line spacing (leading) is at least space-and-a-half within paragraphs, and paragraph spacing is at least 1.5 times larger than the line spacing. Incorporating all of these <a href="https://www.w3.org/WAI/WCAG21/Understanding/visual-presentation.html">layout guidelines</a> will help people with attention-deficit disorders, reading and vision-based disabilities focus more on the content.</p>

### Copy And Icons

<p>Last but not least, let’s focus on the actual PSA message. Arguably, copy is the key element in informing the public on the latest COVID-19 updates and providing information about preventing the spread of the virus. But icons in this situation serve up more than just decoration; these elements visually repeat the same message as the copy. No pressure, but both copy and icons need to be spot-on to reach the widest array of people.</p>

#### Who Copy and Icons Can Affect

<ul>
<li>People with attention-deficit disorders &mdash; estimated at <a href="https://chadd.org/about-adhd/general-prevalence/">129 million people worldwide</a> &mdash; can have issues focusing on copy that is too long, does not break items into lists, and lacks whitespace (think: line height, paragraph margins, etc).</li>
<li>For people with certain cognitive disabilities, it is difficult to understand figurative language or specialized usage like the phrases “it’s raining cats and dogs” or “that test was a piece of cake.”</li>
<li>People with cognitive, language, and learning disabilities may need visual icons, graphics, and symbols to understand the accompanying copy.</li>
</ul>

#### PSA Copy Review

<p>For this example, let’s test the copy of two PSAs from the Centers for Disease Control and Prevention (CDC) for readability. Readability is the ease with which a reader can understand a written text. <a href="https://en.wikipedia.org/wiki/Readability">Readability</a> of copy depends on both the content and presentation.</p>

<p>CDC created PSA &mdash; <a href="https://www.cdc.gov/coronavirus/2019-ncov/downloads/2019-ncov-factsheet.pdf">What you should know about COVID-19 to protect yourself and others</a>:</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c48c7a6b-f3eb-4e06-ba25-3775c72de9eb/20-accessible-images.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c48c7a6b-f3eb-4e06-ba25-3775c72de9eb/20-accessible-images.png" sizes="100vw" caption="CDC created PSA – What you should know about COVID-19 to protect yourself and others (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c48c7a6b-f3eb-4e06-ba25-3775c72de9eb/20-accessible-images.png'>Large preview</a>)" alt="CDC created PSA – What you should know about COVID-19 to protect yourself and others" >}}

<p class="c-pre-sidenote--left">If we evaluate the main body copy using readability indicator tools like <a href="https://app.readable.com/text/">Readable</a> and <a href="https://www.webfx.com/tools/read-able/check.php">The Readability Test</a>, we see that the “What you should know about COVID-19 to protect yourself and others” PSA has 388 words at an average reading grade level of 9 and a <a href="https://en.wikipedia.org/wiki/Flesch%E2%80%93Kincaid_readability_tests">Flesch Kincaid Reading Ease</a><sup>1</sup> of 64.6. In addition to those metrics (for accessible copy), we also want to look at the number of complex words and their frequency &mdash; in this case, 35 and 9.02% respectively.</p>

<p class="c-sidenote c-sidenote--right"><sup>1</sup> The <em>Flesch Kincaid Reading Ease</em> level is out of 100. The lower the number, the more difficult the copy is to read. For reference, a reading ease score of 60-70 is considered acceptable for basic web copy.</p> ￼

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9ffa7992-6112-4c95-ac53-c8347e58516e/21-accessible-images.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9ffa7992-6112-4c95-ac53-c8347e58516e/21-accessible-images.png" sizes="100vw" caption="Test results for the PSA – What you should know about COVID-19 to protect yourself and others (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9ffa7992-6112-4c95-ac53-c8347e58516e/21-accessible-images.png'>Large preview</a>)" alt="Test results for the PSA – What you should know about COVID-19 to protect yourself and others" >}}

<p>While the copy in the first image was adequate and falls in the suggested readability ranges for web-based copy, let’s compare it to another PSA created by the CDC on the same subject.</p>

<p>CDC created PSA &mdash; <a href="https://www.cdc.gov/coronavirus/2019-ncov/downloads/stop-the-spread-of-germs.pdf">Stop the Spread of Germs</a>:</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a30c4f1b-c902-4c04-a2cd-66b46688831e/22-accessible-images.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a30c4f1b-c902-4c04-a2cd-66b46688831e/22-accessible-images.png" sizes="100vw" caption="CDC created PSA – Stop the Spread of Germs (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a30c4f1b-c902-4c04-a2cd-66b46688831e/22-accessible-images.png'>Large preview</a>)" alt="CDC created PSA – Stop the Spread of Germs" >}}

<p>This PSA has a lot more imagery and a lot less text. If we again evaluate the main copy, we see that our copy now has a total of 90 words with an average grade of 6 and a Flesch Kincaid Reading Ease of 83.6. The number of complex words is now down to 4 with a frequency of 4.44%.</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3b1b1bf6-5323-4844-9f7d-0a3dfbfe7d95/23-accessible-images.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3b1b1bf6-5323-4844-9f7d-0a3dfbfe7d95/23-accessible-images.png" sizes="100vw" caption="Test results for the PSA – Stop the Spread of Germs (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3b1b1bf6-5323-4844-9f7d-0a3dfbfe7d95/23-accessible-images.png'>Large preview</a>)" alt="Test results for the PSA – Stop the Spread of Germs" >}}

<p>Compared to the first PSA, the “Stop the Spread of Germs” PSA one has 298 fewer words and is easier to read by 3rd-grade levels. It has a reading ease level increase of 19 points, and is less complex. Based on these numbers, we can extrapolate that the second PSA is more inclusive than the first when looking at copy alone.</p>

#### PSA Icon Review

<p>But testing the readability of copy isn’t the only way to measure the effectiveness of a PSA when it comes to message accessibility. Another element we need to look at are the icons accompanying the copy. If we are presented only the icons, will the same message be received?</p>

<p>Let’s now look at a couple of examples. Based on the icons alone, what is the message that the image is trying to convey about riding your bicycle safely during COVID-19?</p>

<p>Edited PSA from the <a href="https://ecf.com/sites/ecf.com/files/Cycling_COVID19_infographics_1b.png">European Cyclists’ Federation</a>:</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/53184d7f-283d-4780-a17e-6ecf5b0b9d9b/24-accessible-images.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/53184d7f-283d-4780-a17e-6ecf5b0b9d9b/24-accessible-images.jpg" sizes="100vw" caption="Edited PSA from the European Cyclists’ Federation (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/53184d7f-283d-4780-a17e-6ecf5b0b9d9b/24-accessible-images.jpg'>Large preview</a>)" alt="Edited PSA from the European Cyclists’ Federation hiding the text and showing just the icons" >}}

<p>Original PSA:</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d17394d0-fd9b-49dd-8ef3-2f9da4c928cc/25-accessible-images.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d17394d0-fd9b-49dd-8ef3-2f9da4c928cc/25-accessible-images.png" sizes="100vw" caption="Original PSA from the European Cyclists’ Federation (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d17394d0-fd9b-49dd-8ef3-2f9da4c928cc/25-accessible-images.png'>Large preview</a>)" alt="Original PSA from the European Cyclists’ Federation showing the text and related icons" >}}

<p>This is the unedited PSA. Were you able to figure out the full message? While you might have been able to guess correctly for a couple of icons, were there parts of the message you missed not having the copy?</p>

<p>OK, let’s take a look at another example. This next PSA comes from the <a href="https://www.health.pa.gov/topics/disease/PublishingImages/tw%201%20doh%20corona.png">Pennsylvania Department of Health</a>. Let’s do the same exercise as before: can you understand the message in this PSA (without the icon copy)?</p>

<p>Edited PSA:</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c6973cc4-0f77-4709-8ff0-834b4ebeeb4a/26-accessible-images.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c6973cc4-0f77-4709-8ff0-834b4ebeeb4a/26-accessible-images.jpg" sizes="100vw" caption="Edited PSA from the Pennsylvania Department of Health (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c6973cc4-0f77-4709-8ff0-834b4ebeeb4a/26-accessible-images.jpg'>Large preview</a>)" alt="Edited PSA from the Pennsylvania Department of Health hiding the text and showing just the icons" >}}

<p>Original PSA:</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bc5e835f-66c4-4ad4-985a-831aee159558/27-accessible-images.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bc5e835f-66c4-4ad4-985a-831aee159558/27-accessible-images.png" sizes="100vw" caption="Original PSA from the Pennsylvania Department of Health (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bc5e835f-66c4-4ad4-985a-831aee159558/27-accessible-images.png'>Large preview</a>)" alt="Original PSA from the Pennsylvania Department of Health showing the text and related icons" >}}

<p>Now we can see the PSA with copy. Were you able to figure out the full message? While there may have been an icon or two that tripped you up, was it easier to decipher the icons on the second PSA versus the first? Hopefully, this quick exercise helped you understand the critical role icons play in the message.</p>

#### Next Steps for Accessible Copy and Icons

<p>Be clear and concise. The unofficial rule of thumb is to write for a <a href="https://www.w3.org/WAI/WCAG21/Understanding/reading-level.html">9th-grade reading level</a>. This level is based on the assumption that most people reach the 12th-grade reading level, but in times of peak stress, they might not be reading at their highest level. Try and use plain language and avoid technical jargon, fancy words, colloquialisms, and expressions. Likewise, make sure any <a href="https://www.w3.org/WAI/WCAG21/Understanding/readable">acronyms, abbreviations, or unusual words</a> are explained in more detail or linked out to additional resources. Tools like <a href="https://app.readable.com/text/">Readable</a> and <a href="https://www.webfx.com/tools/read-able/check.php">The Readability Test</a> can help you determine the reading level of your copy, while tools like <a href="https://www.hemingwayapp.com/">Hemingway Editor</a> or <a href="https://www.grammarly.com/">Grammarly</a> can suggest edits to make your copy more inclusive.</p>

<p>Use icons, graphics, and symbols to supplement copy whenever possible. Adding imagery allows you to break down some language and cognitive barriers and not rely on your typography to carry all the weight. Just be sure to choose icons that are common or don’t require a lot of thought.</p>

## Wrapping Up

<p>Creating accessible images involves a lot more than just adding alt text. It is important to consider how all image elements &mdash; color, contrast, typography, layout, copy, and icons &mdash; affect your users as well. By taking a bit more time and building these accessibility principles into your images you will undoubtedly reach more people &mdash; on their terms. In uncertain times like these, we need to be sure we are addressing all the ways we can improve our images to be more inclusive in our messaging.</p>

{{< signature "ra, yk, il" >}}
