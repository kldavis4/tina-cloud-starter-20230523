---
title: 'Web Accessibility In Context'
slug: web-accessibility-context
author: be-birchall
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5679cfb1-c542-4c20-bbcb-3d11889396e9/web-accessibility-be-birchall-sharing-card.png
date: 2019-06-07T12:00:59+02:00
summary: >-
  How do browsers and HTML support screen readers today? In this article, Be Birchall explains why it’s so important to prioritize accessibility among teams and why there needs to be more awareness raised among developers. Lack of awareness and prioritization, rather than any technical limitation, is currently the main barrier to an accessible web.
description: >-
  In this article, Be Birchall explains why it’s so important to prioritize accessibility among teams and why there needs to be more awareness raised among developers.
categories:
  - Accessibility
  - Usability
  - UX
---
<p>Haben Girma, disability rights advocate and Harvard Law’s first deafblind graduate, made the following statement in her keynote address at the AccessU digital accessibility conference last month:</p>

<blockquote>“I define disability as an opportunity for innovation.”</blockquote>

<p>She charmed and impressed the audience, telling us about learning sign language by touch, learning to surf, and about the keyboard-to-braille communication system that she used to take questions after her talk.</p>

<p>Contrast this with the perspective many of us take building apps: <strong>web accessibility is treated as an afterthought</strong>, a confusing collection of rules that the team might look into for version two. If that sounds familiar (and you’re a developer, designer or product manager), this article is for you.</p>

<p>I hope to shift your perspective closer to Haben Girma’s by showing how web accessibility fits into the broader areas of technology, disability, and design. We’ll see how designing for different sets of abilities leads to insight and innovation. I’ll also shed some light on how the history of browsers and HTML is intertwined with the history of assistive technology.</p>

## Assistive Technology

<p>An <em>accessible</em> product is one that is usable by all, and <em>assistive technology</em> is a general term for devices or techniques that can aid access, typically when a disability would otherwise preclude it. For example, captions give deaf and hard of hearing people access to video, but things get more interesting when we ask what counts as a disability.</p>

<p>On the ‘social model’ definition of disability adopted by the World Health Organization, a disability is not an intrinsic property of an individual, but <strong>a mismatch between the individual’s abilities and environment</strong>. Whether something counts as a ‘disability’ or an ‘assistive technology’, doesn’t have such a clear boundary and is contextual.</p>

<p>Addressing mismatches between ability and environment has lead to not only technological innovations but also to new understandings of how humans perceive and interact with the world.</p>

{{% feature-panel %}}

<p><a href="https://collection.cooperhewitt.org/exhibitions/1141959921/">Access + Ability</a>, a recent exhibit at the Cooper Hewitt Smithsonian design museum in New York, showcased some recent assistive technology prototypes and products. I’d come to the museum to see a large exhibit on designing for the senses, and ended up finding that this smaller exhibit offered even more insight into the senses by its focus on cross-sensory interfaces.</p>

<p><strong>Seeing is done with the brain</strong>, and not with the eyes. This is the idea behind one of the items in the exhibit, Brainport, a device for those who are blind or have low vision. Your representation of your physical environment from sight is based on interpretations your brain makes from the inputs that your eyes receive.</p>

<p>What if your brain received the information your eyes typically receive through another sense? A camera attached to Brainport’s headset receives visual inputs which are translated into a pixel-like grid pattern of gentle shocks perceived as “bubbles” on the wearer’s tongue. Users report being able to “see” their surroundings in their mind’s eye.</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/55c827f2-654d-4f1b-89bb-cd75b71c8995/brainport.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/55c827f2-654d-4f1b-89bb-cd75b71c8995/brainport.jpg" sizes="100vw" caption="Brainport turns images from a camera into a pixel-like pattern of gentle electric shocks on the tongue. (Image Credit: <a href='https://collection.cooperhewitt.org/objects/1158794687'>Cooper Hewitt</a>)(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/55c827f2-654d-4f1b-89bb-cd75b71c8995/brainport.jpg'>Large preview</a>)" alt="The Brainport is a camera attached to the forehead connected to a rectangular device that comes in contact with the wearer’s tongue." >}}

<p><a href="https://cutecircuit.com/soundshirt/">Soundshirt</a> also translates inputs typically perceived by one sense to inputs that can be perceived by another. This wearable tech is a shirt with varied sound sensors and subtle vibrations corresponding to different instruments in an orchestra, enabling a tactile enjoyment of a symphony. Also on display for interpreting sound was an empathetically designed hearing aid that looks like a piece of jewelry instead of a clunky medical device.</p>

<p>Designing for different sets of abilities often leads to innovations that turn out to be useful for people and settings beyond their intended usage. Curb cuts, the now familiar mini ramps on the corners of sidewalks useful to anyone wheeling anything down the sidewalk, <a href="https://99percentinvisible.org/episode/curb-cuts/">originated from disability rights activism in the ’70s</a> to make sidewalks wheelchair accessible. Pellegrino Turri invented the early typewriter in the early 1800s to help his blind friend write legibly, and the first commercially available typewriter, the Hansen Writing Ball, was created by the principal of Copenhagen’s Royal Institute for the Deaf-Mutes.</p>

<p>Vint Cerf <a href="https://www.blog.google/inside-google/googlers/vint-cerf-accessibility-cello-and-noisy-hearing-aids/">cites his hearing loss</a> as shaping his interest in networked electronic mail and the TCP/IP protocol he co-invented. Smartphone color contrast settings for color blind people are useful for anyone trying to read a screen in bright sunlight, and have even found an unexpected use in <a href="https://lifehacker.com/change-your-screen-to-grayscale-to-combat-phone-addicti-1795821843">helping people to be less addicted to their phones</a>.</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/079a9990-f590-4906-878d-779960c4c91d/writingball.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/079a9990-f590-4906-878d-779960c4c91d/writingball.jpg" sizes="100vw" caption="The Hansen Writing Ball was developed by the principal of Copenhagen’s Royal Institute for the Deaf-Mutes. (Image Credit: <a href='https://commons.wikimedia.org/wiki/File:Malling_Hansen,1867,_Dänemark.jpg'>Wikimedia Commons</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/079a9990-f590-4906-878d-779960c4c91d/writingball.jpg'>Large preview</a>)" alt="The Hansen Writing Ball has brass colored keys arranged as if on the top half of a ball, with a curved sheet of paper resting under them." >}}

<p>So, designing for different sets of abilities gives us new insights into how we perceive and interact with the environment, and leads to innovations that make for a blurry boundary between assistive technology and technology generally.</p>

<p>With that in mind, let’s turn to the web.</p>

{{% ad-panel-leaderboard %}}

## Assistive Tech And The Web

<p>The web was intended as accessible to all from the start. A quote you’ll run into a lot if you start reading about web accessibility is:</p>
 
<blockquote>“The power of the Web is in its universality. Access by everyone regardless of disability is an essential aspect.”<br /><br />&mdash; Tim Berners-Lee, W3C Director and inventor of the World Wide Web</blockquote>

<p>What sort of assistive technologies are available to perceive and interact with the web? You may have heard of or used a screen reader that reads out what’s on the screen. There are also braille displays for web pages, and alternative input devices like an eye tracker I got to try out at the <em>Access + Ability</em> exhibit.</p>

<p>It’s fascinating to learn that web pages are displayed in braille; the web pages we create may be represented in 3D! Braille displays are usually made of pins that are raised and lowered as they “translate” each small part of the page, much like the device I saw Haben Girma use to read audience questions after her AccessU keynote. A newer company, Blitab (named for “blind” + “tablet”), is creating a <a href="https://www.perkinselearning.org/technology/posts/blitab-android-tablet-14-row-braille-display">braille Android tablet</a> that uses a liquid to alter the texture of its screen.</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/edca5ad3-e1f0-4338-9cef-3186381b7fcb/haben-girma.JPG" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/edca5ad3-e1f0-4338-9cef-3186381b7fcb/haben-girma.JPG" sizes="100vw" caption="Haben Girma uses her braille reader to have a conversation with AccessU conference participants. (Photo used with her permission.) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/edca5ad3-e1f0-4338-9cef-3186381b7fcb/haben-girma.JPG'>Large preview</a>)" alt="Haben Girma sits at a conference table and uses her braille reader." >}}

<p>People proficient with using audio screen readers get used to faster speech and can adjust playback to an impressive rate (as well as saving battery life by turning off the screen). This makes the screen reader seem like an equally useful alternative mode of interacting with web sites, and indeed many people take advantage of audio web capabilities to dictate or hear content. An interface intended for some becomes more broadly used.</p>

<p><strong>Web accessibility is about more than screen readers</strong>, however, we’ll focus on them here because &mdash; as we’ll see &mdash; screen readers are central to the technical challenges of an accessible web.</p>

<p><strong>Recommended reading</strong>: <em><a href="https://www.smashingmagazine.com/2018/04/designing-accessibility-inclusion/">Designing For Accessibility And Inclusion</a> by Steven Lambert</em></p>

## Technical Challenges And Early Approaches

Imagine you had to design a screen reader. If you’re like me before I learned more about assistive tech, you might start by imagining an audiobook version of a web page, thinking your task is to automate reading the words on the page. But look at this page. Notice how much you use visual cues from layout and design to tell you what its parts are for how to interact with them.

- How would your screen reader know when the text on this page belongs to clickable links or buttons?
- How would the screen reader determine what order to read out the text on the page?
- How could it let the user “skim” this page to determine the titles of the main sections of this article?

<p>The earliest screen readers were as simple as the audiobook I first imagined, as they dealt with only text-based interfaces. These “<a href="https://web.archive.org/web/20060625225004/https://www.edstoffel.com/david/talkingterminals.html">talking terminals</a>,” developed in the mid-’80s, translated ASCII characters in the terminal’s display buffer to an audio output. But graphical user interfaces (or GUI’s) soon became common. “<a href="https://developer.paciellogroup.com/blog/2015/01/making-the-gui-talk-1991-by-rich-schwerdtfeger/">Making the GUI Talk</a>,” a 1991 BYTE magazine article, gives a glimpse into the state of screen readers at a moment when the new prevalence of screens with essentially visual content made screen readers a technical challenge, while the freshly passed Americans with Disabilities Act highlighted their necessity.</p>

<p>OutSpoken, discussed in the BYTE article, was one of the first commercially available screen readers for GUI’s. OutSpoken worked by intercepting operating system level graphics commands to build up an <em>offscreen model</em>, a database representation of what is in each part of the screen. It used heuristics to interpret graphics commands, for instance, to guess that a button is drawn or that an icon is associated with nearby text.  As a user moves a mouse pointer around on the screen, the screen reader reads out information from the offscreen model about the part of the screen corresponding to the cursor’s location.</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0b7ac995-b233-4e80-96c2-d9af5ea0b5fb/offscreen-model.jpeg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0b7ac995-b233-4e80-96c2-d9af5ea0b5fb/offscreen-model.jpeg" sizes="100vw" caption="The offscreen model is a database representation of the screen based on intercepting graphics commands. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0b7ac995-b233-4e80-96c2-d9af5ea0b5fb/offscreen-model.jpeg'>Large preview</a>)" alt="Graphics commands build a GUI from code. Graphics commands are also used to build a database representation of the screen, which can then be used by screen readers." >}}

<p>This early approach was difficult: intercepting low-level graphics commands is complex and operating system dependent, and relying on heuristics to interpret these commands is error-prone.</p>

{{% ad-panel-leaderboard %}}

## The Semantic Web And Accessibility APIs

<p>A new approach to screen readers arose in the late ’90s, based on the idea of the <em>semantic web</em>. Berners-Lee wrote of his dream for a semantic web in his 1999 book <em>Weaving the Web: The Original Design and Ultimate Destiny of the World Wide Web</em>:</p>

<blockquote>I have a dream for the Web [in which computers] become capable of analyzing all the data on the Web &mdash; the content, links, and transactions between people and computers. A "Semantic Web", which makes this possible, has yet to emerge, but when it does, the day-to-day mechanisms of trade, bureaucracy, and our daily lives will be handled by machines talking to machines. The "intelligent agents" people have touted for ages will finally materialize.</blockquote>

<p>Berners-Lee defined the semantic web as “a web of data that can be processed directly and indirectly by machines.” It’s debatable how much this dream has been realized, and many now think of it as unrealistic. However, we can see the way assistive technologies for the web work today as a part of this dream that did pan out.</p>

<p>Berners-Lee emphasized accessibility for the web from the start when founding the W3C, the web’s international standards group, in 1994. In a <a href="https://www.w3.org/WAI/history">1996 newsletter to the W3C’s Web Accessibility Initiative</a>, he wrote:</p>

<blockquote>The emergence of the World Wide Web has made it possible for individuals with appropriate computer and telecommunications equipment to interact as never before. It presents new challenges and new hopes to people with disabilities.</blockquote>

<p>HTML4, developed in the late ’90s and released in 1998, emphasized separating document structure and meaning from presentational or stylistic concerns. This was based on semantic web principles, and <a href="https://www.w3.org/TR/REC-html40/intro/intro.html#h-2.3.2">partly motivated by improving support for accessibility</a>. The HTML5 that we currently use builds on these ideas, and so supporting assistive technology is central to its design.</p>

<p><strong>So, how exactly do browsers and HTML support screen readers today?</strong></p>

<p>Many front-end developers are unaware that the browser parses the DOM to create a data structure, especially for assistive technologies. This is a tree structure known as the <em>accessibility tree</em> that forms the API for screen readers, meaning that we no longer rely on intercepting the rendering process as the offscreen model approach did. HTML yields one representation that the browser can use both to render on a screen, and also give to audio or braille devices.</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f7f68bf1-52bc-44d8-9eda-687cb57f29c5/semantic-model.jpeg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f7f68bf1-52bc-44d8-9eda-687cb57f29c5/semantic-model.jpeg" sizes="100vw" caption="Browsers use the DOM to render a view, and to create an accessibility tree for screen readers. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f7f68bf1-52bc-44d8-9eda-687cb57f29c5/semantic-model.jpeg'>Large preview</a>)" alt="HTML yields a DOM tree, which can be used to render a view, and to build up an accessibility tree that assistive tech like screen readers use." >}}

<p>Let’s look at the accessibility API in a little more detail to see how it handles the challenges we considered above. Nodes of the accessibility tree, called “accessible objects,” correspond to a subset of DOM nodes and have attributes including <strong>role</strong> (such as <code>button</code>), <strong>name</strong> (such as the text on the button), and <strong>state</strong> (such as <code>focused</code>) inferred from the HTML markup. Screen readers then use this representation of the page.</p>

<p>This is how a screen reader user can know an element is a button without making use of the visual style cues that a sighted user depends on. How could a screen reader user find relevant information on a page without having to read through all of it? In a <a href="https://webaim.org/projects/screenreadersurvey7/#finding">recent survey</a>, screen reader users reported that the most common way they locate the information they are looking for on a page is via the page’s headings. If an element is marked up with an <code>h1</code>&ndash;<code>h6</code> tag, a node in the accessibility tree is created with the role <code>heading</code>. Screen readers have a “skip to next heading” functionality, thereby allowing a page to be skimmed.</p>

<p>Some HTML attributes are specifically for the accessibility tree. ARIA (Accessible Rich Internet Applications) attributes can be added to HTML tags to specify the corresponding node’s name or role. For instance, imagine our button above had an icon rather than text. Adding <code>aria-label="sign up"</code> to the button element would ensure that the button had a label for screen readers to represent to their users. Similarly, we can add <code>alt</code> attributes to image tags, thereby supplying a name to the corresponding accessible node and providing alternative text that lets screen reader users know what’s on the page.</p>

<p>The downside of the semantic approach is that it requires developers to use HTML tags and aria attributes in a way that matches their code’s intent. This, in turn, <strong>requires awareness among developers</strong>, and prioritization of accessibility by their teams. Lack of awareness and prioritization, rather than any technical limitation, is currently the main barrier to an accessible web.</p>

<p>So the current approach to assistive tech for the web is based on semantic web principles and baked into the design of browsers and HTML. Developers and their teams have to be aware of the accessibility features built into HTML to be able to take advantage of them.</p>

<p><strong>Recommended reading</strong>: <em><a href="https://www.smashingmagazine.com/2015/03/web-accessibility-with-accessibility-api/">Accessibility APIs: A Key To Web Accessibility</a> by Léonie Watson</em></p>

## AI Connections

<p><a href="https://www.smashingmagazine.com/2018/09/getting-started-with-machine-learning/">Machine Learning</a> (ML) and <a href="https://www.smashingmagazine.com/2017/01/algorithm-driven-design-how-artificial-intelligence-changing-design/">Artificial Intelligence</a> (AI) come to mind when we read Berners-Lee’s remarks about the dream of the semantic web today. When we think of computers being intelligent agents analyzing data, we might think of this as being done via machine learning approaches. The early offscreen model approach we looked at used heuristics to classify visual information. This also feels reminiscent of machine learning approaches, except that in machine learning, heuristics to classify inputs are based on an automated analysis of previously seen inputs rather than hand-coded.</p>

<p>What if in the early days of figuring out how to make the web accessible we had been thinking of using machine learning? Could such technologies be useful now?</p>

<p>Machine learning has been used in some recent assistive technologies. Microsoft’s SeeingAI and Google’s Lookout use machine learning to classify and narrate objects seen through a smartphone camera. CTRL Labs is working on a technology that detects micro-muscle movements interpreted with machine learning techniques. In this way, it seemingly <strong>reads your mind about movement intentions</strong> and could have applications for helping with some motor impairments. AI can also be used for character recognition to read out text, and even <a href="https://www.newscientist.com/article/2140592-glove-turns-sign-language-into-text-for-real-time-translation/">translate sign language to text</a>. <a href="https://www.blog.google/outreach-initiatives/accessibility/making-audio-more-accessible-two-new-apps/">Recent Android advances</a> using machine learning let users augment and amplify sounds around them, and to automatically live transcribe speech.</p>

<p>AI can also be used to help improve the data that makes its way to the accessibility tree. Facebook introduced automatically generated alternative text to provide user images with screen reader descriptions. The results are imperfect, but point in an interesting direction. Taking this one step further, Google recently announced that Chrome will soon be able to <a href="https://twitter.com/googleaccess/status/1106247539894829056">supply automatically generated alternative text for images</a> that the browser serves up.</p>

## What’s Next

<p>Until (or unless) machine learning approaches become more mature, an accessible web depends on the API based on the accessibility tree. This is a robust solution, but taking advantage of the assistive tech built into browsers requires people building sites to be aware of them. Lack of awareness, rather than any technical difficulty, is currently the main challenge for web accessibility.</p>

### Key Takeaways

<ul>
<li>Designing for different sets of abilities can give us new insights and lead to innovations that are broadly useful.</li>
<li>The web was intended to be accessible from the start, and the history of the web is intertwined with the history of assistive tech for the web.</li>
  <li>Assistive tech for the web is baked into the current design of browsers and HTML.</li>
<li>Designing assistive tech, particularly involving AI, is continuing to provide new insights and lead to innovations.</li>
<li>The main current challenge for an accessible web is awareness among developers, designers, and product managers.</li>
</ul>

### Resources

<ul>
  <li><a href="https://web.dev/accessible/">Google’s web.dev accessibility guide</a> is concise and has interactive Glitch demos.</li>
<li><a href="https://chrome.google.com/webstore/detail/accessibility-insights-fo/pbjjkligggfmakdaogkfomddhfmpjeni">Accessibility Insights</a> is a Chrome extension from Microsoft that highlights issues in the browser.</li>
<li>To learn more about the accessibility tree, see Leonie Watson’s Smashing Magazine article “<a href="https://www.smashingmagazine.com/2015/03/web-accessibility-with-accessibility-api/">Accessibility API’s: A Key to Web Accessibility</a>,” Marcy Sutton’s Egghead video “<a href="https://egghead.io/lessons/html-5-what-is-the-accessibility-tree">What is the Accessibility Tree?</a>” and Rob Dodson’s “<a href="https://robdodson.me/why-you-cant-test-a-screen-reader-yet/">Why you can’t test a screen reader (yet)!</a>”</li>
<li>Read more about the social model of disability and how it can inform inclusive design in Kat Holmes’ book <a href="https://mitpress.mit.edu/books/mismatch">Mismatch: How Inclusion Shapes Design</a>.</li>
</ul>

{{< signature "dm, yk, il" >}}
