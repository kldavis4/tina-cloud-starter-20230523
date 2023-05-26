---
title: 'Wireframing: The Perfectionist’s Guide'
slug: wireframe-perfectionist-guide
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b9946976-ebb1-4416-9b28-9e41ee3065a3/nest-schedule-preview-opt.png
date: 2016-11-22T22:01:39.000Z
author: edriclapniramai
summary: >-
  In order to improve your workflow, in this article Edric Lapniramai provides a checklist to refer throughout the UX designer’s wireframing process. Divided in three sections &mdash; decisions to consider before wireframing, detailing the design elements, and annotations &mdash;, this guideline can help you perfect your wireframes and be practical with your time.
description: >-
  In this article, Edric Lapniramai provides a checklist to refer throughout the UX designer’s wireframing process. Divided in three sections, this guideline can help you perfect your wireframes and be practical with your time. 
categories:
  - UX
  - Wireframing
  - Prototyping
---

When I was a developer, I often had a hundred questions when building websites from wireframes that I had received. Some of those questions were:

*   How will this design scale when I shrink the browser window?
*   What happens when this shape is filled out incorrectly?
*   What are the options in this sorting filter, and what do they do?

These types of questions led me to miss numerous deadlines, and I wasted time and energy in back-and-forth communication. Sadly, this situation could have been avoided if the wireframes had provided enough detail. 

Now that I am a UX designer, I notice that some designers tend to forget that wireframes are equally creative <em>and</em> technical. We are responsible for designing great ideas, but we are also responsible for creating product specifications. I admit that there can be so many details to remember that it’s easy to lose track. To save time and energy for myself, I gathered all of my years of wireframing knowledge into a single checklist that I refer to throughout the process. And now I am sharing this knowledge with you, so that you can get back to being creative.

### Navigating The Guide

If you’re starting fresh on a wireframing project, I recommend going through each section’s guidelines like a checklist. If not, feel free to jump to the appropriate section.

1.  [Decisions to consider before wireframing](#decisions-to-consider-before-wireframing)
2.  [Detailing the design elements](#detailing-the-design-elements)
3.  [Annotating the wireframes](#annotating-the-wireframes)

### Considerations

**Note**: *These guidelines are more appropriate for wireframes &mdash; and prototypes, to an extent &mdash; during a production life cycle (i.e. preparing your product to be built). By this point, the main idea has been established, the features have been fairly locked down, and the core layouts are not going to dramatically change. That being said, some guidelines, like in the first section, can be used for conceptual wireframes in a discovery phase. Just be wary of getting too detailed, because your designs might drastically change, and you will have wasted time.*

Finally, onto the guide!

{{% feature-panel %}}

## Decisions To Consider Before Wireframing

These guidelines ensure that you ask the difficult but crucial questions early on and establish a foundation for a smooth wireframing process.

### Device Support

Usually, the stakeholders will dictate which devices to support, but sometimes you will have a reasonable suspicion that it will be cross-platform or responsive. Other times, you might have to select the best devices to use with your product. In either case, here’s a list of reference devices:

*   desktop browsers
*   mobile website (browser)
*   native mobile app: Android, iOS, Windows
*   tablet
*   smartwatch: Android Wear, Watch OS(iOS), WebOS, Band (Microsoft)
*   smart TV: Android TV, Tizen OS (Samsung), Firefox OS (Panasonic), WebOS (LG)
*   Facebook applications
*   virtual reality: HTC Vive, Oculus Rift, Samsung Gear VR, Playstation VR
*   kiosks
*   console gaming: Xbox One, Playstation 4, Wii U, Steam

#### Confirm Devices Expected To Be Supported

More often than not, responsive mobile wireframes are requested later in the process or are suddenly included by the client. These late requests can cause massive design reworking when you have already started on the wireframes. So, ensure the following:

*   Align with your team’s expectations.
*   Make sure you have client approval in writing, or refer to a statement of work.
*   While they are not devices, content management systems are frequently forgotten.

#### Match Features To Context Of Use

While composing a review for a product would work in a desktop browser, it might be seldom done on a mobile phone. Review your features one by one and determine whether your users will get added value from each device. If a feature does not match the user’s goals, either change it to be more device-specific or cut it out completely for the device in question. Reducing the design will save you time and money.

#### Verify Design Differences On Multiple Devices

A common scenario is building a desktop application with a mobile and tablet component. Discuss the following with your team and stakeholders:

*   Will the layout be identical (responsive) or completely separate?
*   Are features shared across all experiences, or will there be subsets?
*   Which operating systems are being supported? For instance, Android and iOS apps follow different design patterns.

Maintain documentation on differences in layouts and features, so that you can easily design for them later in your wireframes.

#### Consider Implications Of Screen Orientation

For mobile and tablet, designs can appear different in portrait and landscape modes.

*   Left alone, a landscape layout will appear like the portrait version but with the width stretched out and less horizontal viewing space.
*   Screens can be locked to an orientation. Tread carefully around design layouts that are exclusive to portrait or landscape, because you are forcing users to work a certain way. If in doubt, conduct a usability test.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/56891779-2f5f-4f26-bacb-e92528817bee/nest-schedule-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b9946976-ebb1-4416-9b28-9e41ee3065a3/nest-schedule-preview-opt.png" alt="wireframing" width="500" height="281" title="Wireframing â€“ The Perfectionist’s Guide" /></a><figcaption>Maintaining a portrait layout might have worked better here so that users would not have to rotate their phone back and forth on the scheduling screen of Nest’s mobile app. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/56891779-2f5f-4f26-bacb-e92528817bee/nest-schedule-large-opt.png">Large preview</a>)</figcaption></figure>

### Scaling The Design

A layout and its UI elements can scale in a variety of ways when the window’s size changes. The most popular scaling patterns are:

*   **Fixed or static**  
Remains the same no matter what.
*   **Fluid or liquid**  
Incrementally shrinks or stretches with each pixel.
*   **Adaptive**  
Layout changes at certain breakpoints in the window’s width.
*   **Responsive**  
Follows a mix of fluid and adaptive behavior.

<a href="https://www.liquidapsive.com/">Liquidapsive</a> is an interactive tool for visualizing how each scaling pattern affects the layout when the window’s size changes.

#### Get Team Consensus

First discuss with your team the best approach, because this will have an impact on the time for you, the developers and the visual designers. Users expect most websites to have desktop and mobile versions, although they don’t always have to share the same set of features.

#### Align With Your Developer On Mechanics

Consult with your developers on how the design should scale. Also, discuss breakpoints and the scaling behavior for layouts and UI elements that you are unsure of.

#### Prepare For Many Sets Of Wireframes

Responsive and adaptive layouts will need many sets of screens; so, let your project managers know it will require extra time. I usually add an extra 50 to 75% of the total time for each set.

### Default Screen Size Resolution

Establishing a default screen size is important for everyone on your team because they will need to know what to develop and design for. You also want to avoid accidentally starting too large and then realizing you need to shrink it down.

#### Start Small And Prepare For A Large Size

1024&times;768 pixels for desktop and tablet and 320 &times; 480 for mobile are generally safe resolutions to work with. Anything higher can be risky to begin with. It is prudent to start with a low resolution and then scale up so that the design still looks adequate when the window is larger.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4447c92d-3304-41c2-b275-695d1d16e012/safe-design-resolution-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a7169f75-4b1b-4186-89bb-03933b1946b6/safe-design-resolution-preview-opt.jpg" width="500" height="225" /></a><figcaption>Start with a low resolution and then scale up. Pixels for mobile, table and desktop. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4447c92d-3304-41c2-b275-695d1d16e012/safe-design-resolution-large-opt.jpg">Large preview</a>)</figcaption></figure>

Additionally, consider that many people do not maximize their browser window, so their view of the layout will be even smaller.

#### Use Analytics To Guide Your Decision

Analytics for screen resolutions can reveal interesting trends, which can help you make an informed decision. You might need the data to convince your client of the resolution you are pushing for as well. Remember that it’s better to be inclusive than exclusive.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/755cbfce-cdda-40d7-9e1c-c4f4d6daffd6/analytics-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b4053a1b-459c-4cf8-9087-affbd2124c10/analytics-preview-opt.png" alt="A list of screen resolution analytics" width="500" height="281" /></a><figcaption>Although 1366 Ã— 768 pixels has the highest number of users, 1280 Ã— 800 is the best to start with, despite having a usage of 3.76%. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/755cbfce-cdda-40d7-9e1c-c4f4d6daffd6/analytics-large-opt.png">Large preview</a>)</figcaption></figure>

Going for that larger, prettier resolution might cut off a chunk of your audience. To help with your analysis, here are some scenarios I have seen before:

*   The most popular resolution can sometimes be safe if it shows a trend of continued growth over many years, while the lower resolutions are declining.
*   A group of small resolutions with a low percentage of use could add up to a sizeable population &mdash; in which case, choose the lowest resolution.
*   For a large variation in resolutions, go with the lowest one.
*   If at least 5% of users have a a low resolution, such as 1024 Ã— 768, I would err on the side of caution and select that.
*   Viewing trends for the past year is sometimes better than viewing trends since the beginning, because the latter could include resolutions that are no longer relevant. Sanitize your data by removing old data and mobile and tablet resolutions &mdash; trends will be easier to identify.

#### Know Your Audience And Usage Environment

Although 1366&times;768 is the most common resolution for the desktop (as of May 2016, according to <a href="https://gs.statcounter.com/#resolution-ww-monthly-200903-201605">StatCounter</a> and <a href="https://www.w3counter.com/globalstats.php">W3Counter</a>), think about your audience’s context of use. For instance, 1024 Ã— 768 makes sense if you’re dealing with users who are on old computers and can’t change their equipment (usually corporate environments).

### Levels of Fidelity

Be clear on your definitions of fidelity because it can mean different things to different people. Below is how I define wireframe fidelity:

<strong>Low fidelity</strong> has these elements:

*   Focuses on layout and high-level interactions and concepts.
*   UI elements and content can be represented as boxes or lines, with or without label descriptions.
*   Gray-scale.
*   Can be paper sketch.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f65e3896-8432-47d6-9dd1-eb4af1cb85df/lowfi-wire-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f65e3896-8432-47d6-9dd1-eb4af1cb85df/lowfi-wire-preview-opt.png" alt="Low fidelity wireframe example" width="278" height="455" /></a><figcaption>Notice how abstract this wireframe is. It’s easy to get carried away with adding more detail, but imagine that people will only be able to see a zoomed-out wireframe.</figcaption></figure>

<strong>High fidelity</strong> has these elements:

*   Emphasizes visual aesthetics and branding, such as tone, colors, graphics and font style.
*   Can include realistic images and copy.
*   UI elements look realistic and might include aesthetic touches such as textures and shadows.
*   Sometimes known as a mockup.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/48b34ea9-6a9c-46d2-9f91-046a70e60fb9/hifi-wire-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/89fbdf68-7c2b-4aa4-adb1-fd4ae5d9d15e/hifi-wire-preview-opt.png" width="500" height="426" /></a><figcaption>Sometimes you need to create a small set of concept wireframes with visual themes to preview the overall look and feel. (Image: <a href="https://www.squarespace.com/websites/templates/five">Squarespace</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/48b34ea9-6a9c-46d2-9f91-046a70e60fb9/hifi-wire-large-opt.png">Large preview</a>)</figcaption></figure>

<strong>Medium fidelity</strong> has these elements:

*   Varies between low and high fidelity.
*   More realistic UI elements, but not styled.
*   Filler images and copy.
*   Gray-scale.
*   Has some visual design (such as hierarchical typography).

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1489e577-a084-42cc-b18a-d70013040423/medfi-wire-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9911fe07-5091-4d9c-b3c3-f979abfc6ba4/medfi-wire-preview-opt.jpg" width="500" height="357" /></a><figcaption>This wireframe uses various grayscale values to convey visual weight, without actually using color. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1489e577-a084-42cc-b18a-d70013040423/medfi-wire-large-opt.jpg">Large preview</a>)</figcaption></figure>

#### Indulge Your Stakeholders

Observe your stakeholders’ behavior to figure out what makes them happy, or have a discussion with them to determine what they expect.

*   Are they the type to hone in on minor irrelevant details? Start with low fidelity, and iterate on that until they are satisfied. Then, move up to medium or high fidelity. Gradually building fidelity over multiple check-ins will make approvals easier, while saving precious design time.
*   Are they the type to react to something flashy? Go with high fidelity, but create only a couple at first, so that the stakeholders get an idea of what to expect.
*   If in doubt, medium fidelity is always a safe bet, although it takes a bit more time.

#### Confirm The Expectations Of Fidelity

Whichever fidelity you decide on, make sure your team and stakeholders are on the same page &mdash; consider giving examples to be sure. It is scary to walk into a meeting with low-fidelity designs when “low fidelity” in people’s mind is actually “medium fidelity”.

{{% ad-panel-leaderboard %}}

### Grid Systems And Alignment

When used in a wireframe tool, a grid system saves you time by easily aligning your UI through snap-to-grid features. This feature basically keeps your designs looking aligned and polished.

Using a grid system will also help you maintain consistency in the layout and balance the design’s hierarchy. The article “<a href="https://medium.com/r/?url=http%3A%2F%2Fwebdesign.tutsplus.com%2Farticles%2Fall-about-grid-systems--webdesign-14471">All About Grid Systems</a>” does a great job of briefly explaining the theory behind grid systems and the key advantages to using them.

For design inspiration, I have used the article “<a href="https://www.designersinsights.com/designer-resources/using-layout-grids-effectively">Using Layout Grids Effectively</a>” for examples of grid layouts and patterns.

#### Know Your Alignment And Spacing Features

I achieve pixel-perfection by using the alignment and space-distribution features of many wireframe tools. Learn to use the most common keyboard shortcuts, such as centering, space distribution, grouping and ungrouping. It will save you from having to manually polish your layouts.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/30646592-c614-4e1b-9947-e8f1f0237a66/alignment-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0421fb16-b404-4522-ae2b-23ada1e9583d/alignment-preview-opt.png" alt="Omnigraffle’s alignment tool" width="500" height="160" /></a><figcaption>Shown here is Omnigraffle’s object-alignment module, which is somewhat similar in other tools such as InDesign and Axure. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/30646592-c614-4e1b-9947-e8f1f0237a66/alignment-large-opt.png">Large preview</a>)</figcaption></figure>

#### Perform Visual Checks

Your visual designer and developer will end up doing most of the actual pixel-pushing, but you’ll want to get it as close as possible; a sloppy design will lose the trust of your user. The key to saving time and cleaning up a design is to stand back a bit from the design and see if any misalignments are visible to the naked eye.

Now that you have checked off all of the pre-wireframing activities, you can start designing the actual wireframes. The next section will focus on polishing the design.

## Detailing The Design Elements

Once you have completed the bulk of your main designs, it’s time to include all of the cumbersome details. Go through each of your screens and use the guidelines below as a checklist to fill in anything missing.

### Interaction Feedback

For any action that a user executes, there should always be feedback to let them know what happened or what the next step is.

#### Validate Forms

Forms will usually have one of these validation responses:

*   Invalid syntax: For email address, phone number, area code, URLs and credit-card numbers.
*   Incorrect login: Include a message for the username or password being incorrect, but also include one for both being wrong.
*   Empty form fields.
*   Required check boxes: For agreeing to terms of service.
*   Age requirement: Dropdown to fill in birth date.

#### Intermediary Messages And Modals

Many user actions will generate some form of UI to inform the user of what is happening or to ask them to do something. These can include:

*   confirmation
*   warning or alert
*   success
*   failed action
*   error
*   long-term progress indicator: This is when the user might have to wait for a long behind-the-scenes process to complete (even days long).
*   progress indicator or bar: Include states for zero progress, in progress, completion and failure.
*   spinner: For indeterminate time estimations or short operations.

#### Write User-Friendly Messages

No one likes to read an obscure error message like “Exception 0xc000000933” or a generic one like “Login error”. And unless you have a technical writer on the team, you are actually the most qualified person to write user-friendly messaging.

For consistency, I follow these criteria when writing messages:

*   Include the specific problem if possible.
*   Mention the next step to resolve the issue.
*   Keep it brief and concise, about one to two sentences.
*   Explain in colloquial terms.
*   Avoid technical jargon.
*   Maintain a positive and apologetic tone. Pretend you’re a down-to-earth customer service rep.
*   Enhance with the brand’s tone, if there is one.

#### Implement Supportive Form-Input Techniques

Your developer will know clever tricks to show users error messages immediately or to support users with input fields. Below is a list of common techniques to think about:

*   “Remember me” checkbox for logging in.
*   Links for forgotten password or username. Don’t forget the extra screens such as for “Send a reset password to email” and confirmation that the reset was successfully sent.
*   Suggested results upon typing keywords in a search.
*   Validating each keyboard character entered.
*   Character limit, with a counter or some visual representation when reaching a character limit.
*   Dropdown lists that auto-filter items when typing. [Select2](https://select2.github.io/examples.html) is a great plugin for combo boxes.
*   Letting a user know when they have entered an old password.
*   A checklist for password strength or password syntax that marks off syntax requirements as the user types.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b4c46490-fe39-4ea4-97c6-f218329d98ef/password-verification-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/762d9718-2513-4fd1-b07c-f04a9b18a60a/password-verification-preview-opt.jpg" width="500" height="386" /></a><figcaption>This checklist clearly tells you what criteria has been fulfilled for your password. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b4c46490-fe39-4ea4-97c6-f218329d98ef/password-verification-large-opt.jpg">Large preview</a>)</figcaption></figure>

### Interaction States

Walk through each of your UI components, and design for best- and worst-case scenarios, as well as any other potential states.

#### Dropdown Lists

While the closed state will already be in your design, include the expanded state in your annotations or on a separate page. Do you have any of the following types of dropdowns?

*   navigation menu
*   combo box (states, date, age)
*   filter
*   sorting
*   context menu

#### Titles, Labels And Names

Account for all cases in which the text is exceptionally long in a confined space and can’t break to a new line (for example, in a table). Try to shorten the text as below, and then include the full-length text in a tooltip.

*   Ellipsis: “Deoxyribo”
*   Truncation: “Deoxy”
*   Abbreviations: “DNA”
*   Names: “G. Washington or George W.”
*   Numbers: “100K”, “50M”, “140+”

#### Dynamic Content

Your developers will need to know how content population scales or behaves in different situations:

*   Pagination: search result listings, forums, news articles
*   Scrolling and loading content
*   Brief paragraph text or tags
*   Galleries: image, video and banner carousels
*   Trees: nested file or folder directories
*   Comments and posts

These states are commonly associated with dynamic content:

*   First, middle and last pages: Pagination controls can sometimes appear different depending on where the user is, and final pages can include a “next step” action to fill in empty space.
*   Standard content length: This is default.
*   Empty or unpopulated content: Empty space can look awkward, so consider a friendly message or a subtle background image to fill the void.
*   Overflowing content: Try using “More” links or a form of truncation.
*   Nested posts: Stack Exchange has a [forum thread](https://ux.stackexchange.com/questions/1712/what-is-a-good-way-to-display-infinite-nested-comments) with a variety of suggestions to nest infinite posts.

#### Icons With Numbers

Icons sometimes include values such as how many notifications or emails the user has. You will want to include states for the following:

*   zero items
*   typical items: double or triple digits
*   large numbers: depending on the design, it could go up to hundreds or thousands, but indicating “100K” or “2000+” is also acceptable.

#### Form Fields

Forms will typically have a few states:

*   enabled: This is the default.
*   disabled: For fields that appear unusable in certain conditions.
*   corrected: Optionally have a different style for fields whose validation error has been corrected.
*   validation error: Some designers place error messages adjacent to the relevant field and/or provide an error list.

#### Tooltips

Consider adding a tooltip (a brief one to two sentences) for any interactions that fit these criteria:

*   New or uncommon interaction pattern: Helpful text for interactions that users wouldn’t intuitively understand at first glance. **Think of different design solutions before using this as a fallback.**
*   Advanced areas and actions: Common with programs such as Photoshop and Word, in which advanced functionality improves the user’s productivity or work quality.
*   Less frequent actions: Actions that rarely occur will need help text to jog the user’s memory.
*   Keyboard shortcuts.
*   Shortened content: Abbreviated or truncated text that needs a fully written version.
*   Content preview: Text or images that include previews of content. This is common with listings where users would want to peek at the content before committing to an action that would take them off the page.
*   Reference information: Extra details that quickly support the user with a task (for example, the security number on a credit card).

#### File Uploads

When the user uploads a file in the browser, there are a few states to design for:

*   File upload dialog: Usually provided by default in the OS or browser, but include your custom design if you have one.
*   Upload progress bar.
*   Upload completion bar: For having reached 100%.
*   Canceling in-progress upload: Cancelling an upload in progress can take time.
*   Success: Appears after the progress bar goes away. Include the file name that was uploaded and a way to remove the file.
*   Remove confirmation: Confirmation to remove the uploaded file.

### Gestures

There is typically one way your users will physically interact with your UI, but there can also be multiple gestures per interaction, as with a responsive design or buttons with keyboard shortcuts. For each user action, look for the other gestures below and note the differences in your annotations later.

*   click
*   double-click
*   right-click
*   swipe or flick
*   pinch and spread
*   press
*   hover
*   drag and drop
*   keyboard input
*   keyboard shortcut
*   link to external website
*   link to default application: email, phone number, map.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d4be3aad-de93-4069-b6bc-aba88f22c8e9/gestures-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1818a018-dd7a-4deb-b65e-9d1982b4733f/gestures-preview-opt.jpg" alt="A wireframe for smart TVs that shows annotations with multiple gestures" width="500" height="357" /></a><figcaption>This smart TV wireframe shows how various remote-control buttons interact with a UI element. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d4be3aad-de93-4069-b6bc-aba88f22c8e9/gestures-large-opt.jpg">Large preview</a>)</figcaption></figure>

<strong>Be sensitive to cross-device interaction.</strong> If you are working on a responsive website, be aware of gestures that will not translate smoothly:

*   Hovering: Some designers replace this with a touch gesture. But watch out for actions that already use touch for something else.
*   Dragging and dropping: An alternative design is best.
*   Uploading files: Not a common mobile task; consider removing it for mobile.

### Supplementary Areas and Pages

Aside from your core design, other miscellaneous areas tend to be forgotten, such as:

*   404 error page
*   Internet or service down
*   Logging in: Include CAPTCHA and social log-ins if necessary.
*   Forgotten username or password: Do not forget the successful “we sent you an email to reset” message.
*   Settings and configuration
*   Terms and conditions
*   Privacy policy
*   Email: Such as confirming the creation of an account or resetting the password.

### User Types

You may have users who see a different design or receive an interaction specifically for them. Include extra wireframes to show what each user sees.

*   New users: Users who just created an account.
*   Guests: Users who have no account yet.
*   First-time visitors: You might have a screen that is only seen once.
*   Returning visitors
*   Existing or logged-in users
*   Admins and super-users
*   Other roles

### Copy

Consider how much time you have and what would be useful to your audience. You can also mix and match styles, like using real text for the home-page banner but filler for other areas. Listed below are various styles, with their key advantages.

<strong>Lorem ipsum</strong> (such as the kind produced by <a href="https://www.blindtextgenerator.com/lorem-ipsum">Dummy Text Generator</a>) is great for:

*   previewing how short or long paragraphs will appear,
*   showing a page with filled-in content,
*   when you have no budget for copywriting.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9ffc367b-1103-4bf2-9a90-b838aefd1815/copy-lorem-large-opt-1.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c8a0ac61-8525-43c6-bcac-ade98d5346ce/copy-lorem-preview-opt-1.jpg" alt="Wireframe with lorem ipsum text" width="500" height="300" /></a><figcaption>Even the navigation titles can be lorem ipsum if you’re still working on them. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9ffc367b-1103-4bf2-9a90-b838aefd1815/copy-lorem-large-opt-1.jpg">Large preview</a>)</figcaption></figure>

<strong>Generic labels</strong> that describe the final copy are good for:

*   knowing what it should say but not having time to write it out,
*   giving direction to your writer,
*   avoiding political battles with branding team members or stakeholders,
*   steering stakeholders away from nitpicking about copy.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e4b4d179-b902-4b10-93f7-05e333632dba/copy-generic-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ac6f92a4-0fb7-460b-98f9-b20224e7c58f/copy-generic-preview-opt.jpg" alt="Wireframe with generic labels" width="500" height="300" /></a><figcaption>Describe what would be in a paragraph, and then repeat it for length. If you’re unsure, use lorem ipsum instead. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e4b4d179-b902-4b10-93f7-05e333632dba/copy-generic-large-opt.jpg">Large preview</a>)</figcaption></figure>

<strong>Realistic copy</strong> that closely reflects the content’s intent is helpful for:

*   increasing the fidelity and realism of a polished design.
*   showing the proper language and tone to use in the final copy.
*   conducting usability tests on the home page design.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/404888c3-4504-4a7c-ab20-297b4f12217b/copy-realistic-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/806b4da7-5f9d-40e3-8308-02d02257f3bc/copy-realistic-preview-opt.jpg" alt="Wireframe with realistic text" width="500" height="300" /></a><figcaption>If you are using realistic copy, fight for doing only top-level pages, like a landing page. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/404888c3-4504-4a7c-ab20-297b4f12217b/copy-realistic-large-opt.jpg">Large preview</a>)</figcaption></figure>

{{% ad-panel-leaderboard %}}

### Demonstrations

Demonstrating how an interaction works will reduce miscommunication with the developer and ensure that it is technically feasible. Typically, the developer will feel more confident about deciding which plugin or implementation to use. But if you feel technically savvy, then it would be really helpful for you, as the architect, to take the first step. Below are some useful tips.

#### Search For Plugins

If you are working online, you can often find the latest and trusted plugins being used by the development community on <a href="https://github.com/search?utf8=%E2%9C%93&amp;q=">GitHub</a>. Search for something like “accordion” to browse through accordion plugins. If you are working on other devices, such as Android mobile or Apple Watch, search the web for official design guideline documentation.

#### Select Relevant Plugins

Developers consider community approval, constant updates and framework compatibility to be important when selecting a plugin. On <a href="https://github.com/search?utf8=%E2%9C%93&amp;q=">GitHub</a>, you can sort for “most stars” and “recently updated”. Also, look for demo links in the documentation or website to see how it will work, and then share it with your developer to see if it is viable.

#### Build A Demonstration

If you are building a custom interaction or flow that does not yet exist, think about using prototyping tools or coding it yourself if you are technically savvy. Some prototyping tools with motion design features include <a href="https://principleformac.com/">Principle</a>, <a href="https://www.flinto.com/">Flinto</a> and <a href="https://www.axure.com/">Axure</a>. Some that might require a bit of programming knowledge are <a href="https://origami.design/">Origami</a> and <a href="https://framerjs.com/">Framer</a>.

If you can actually code, then <a href="https://codepen.io/">CodePen</a> is useful for building something quickly and easily.

Once you feel content with the level of polish in your design, finish up with annotations.

## Annotating The Wireframes

At this point, most of your design will be complete, and you are ready to annotate your work.

### Placing Annotations

Being strategic in where and how you place your annotations on the page can improve your workflow and overall quality.

#### Determine A Location

There are different advantages to where you place annotations. See which style below would be most useful to you:

*   Left or right column: Allows the reader to focus on the design or on reading the annotations.
*   Inline: Promotes a more connected reading experience by linking explanations directly to UI elements.
*   Marked tooltips: Similar to inline annotations. Prototyping software such as Axure allows you to place markers directly in the design that can be clicked on to reveal the annotation.
*   Separate page: Gives ample, dedicated space to view the design and annotations.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8e2e205c-67d9-4d6a-a327-5ec6da77727a/annotation-inline-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/73e9673b-4317-4e80-bf84-16847f2ab2a9/annotation-inline-preview-opt.png" alt="Wireframe of inline annotations" width="500" height="358" /></a><figcaption>I drew lines directly from an interaction to show the gesture used and what the resulting state would be. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8e2e205c-67d9-4d6a-a327-5ec6da77727a/annotation-inline-large-opt.png">Large preview</a>)</figcaption></figure>

#### Load In Wireframe Images

Designing for a large resolution can leave little space for annotations. Instead, you could wireframe your layouts with the accurate resolutions, and have another document where you drop the same wireframe images into a fixed-size container. This gives you consistent space for annotations, without having to worry about how big the design is.

I’ve <a href="https://www.edriclapniramai.com/s/Wireframe-Template-Public.zip">created a template</a> (Zip, 1.51 MB) that enables you simply to export wireframe images to the image folder and then drag and drop the same images to an annotated InDesign document. As long as you use the same file names for your export, you can continually overwrite the old wireframe images, and they will automatically update in the InDesign document.

### Writing Annotations

Follow these technical writing rules when revising your annotations:

*   Avoid being wordy. Be direct and concise. Excise words and sentences that do not add any information or that are redundant. Your team and stakeholders want to quickly and easily get the information they need.
*   Avoid figures of speech and metaphors if your audience might be foreign.
*   Stick to simple vocabulary so that everyone can understand, but use technical terms if the audience would understand them.
*   Favor the active voice over the passive voice to cut down wordiness and to be clearer in your explanations. [Purdue OWL has an article](https://owl.english.purdue.edu/owl/resource/539/02/) showing examples of the active and passive voice.

#### Write For Developers

Although stakeholders will enjoy story-driven annotations, developers will prefer straightforward, technical explanations. Be extremely detailed about how an interaction works, and include values if necessary. Write your annotations so that anyone could take the design and build it without needing to talk to you.

To compare and contrast, the annotation below is written for a stakeholder who is working on conceptual wireframes (notice the second-person usage and descriptive wording):
<blockquote>As you scroll toward the bottom of the page, you will seamlessly receive more search results so that you can continue reading without needing to perform another action.</blockquote>

Here is the same example written for a developer:

<blockquote>When scroll bar reaches last search result (about 25% height from bottom):
<ul>
  <li>Dynamically load 10 more search results below current list.</li>
  <li>If end of search results is reached, remove “Load more” button.</li>
  <li>Show spinner when loading; remove when finished.</li>
  <li>Use fade-in and fade-out animation when loading results.</li>
</ul>
</blockquote>

#### List Multiple Gestures, States And Demos

For each action, indicate the gesture(s), label each annotation by its state, and include demo links if available. If there are multiple states, define their conditions or business logic.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/91ae8160-b1de-4126-878d-5e087e517f5c/states-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7255de1a-8342-499f-9682-754c150bdf79/states-preview-opt.jpg" alt="Wireframe with multiple interaction states" width="500" height="287" /></a><figcaption>My wireframe shows a variety of styles for describing states and gestures. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/91ae8160-b1de-4126-878d-5e087e517f5c/states-large-opt.jpg">Large preview</a>)</figcaption></figure>

### UX Integration

One of the most common challenges for UX designers is convincing other people of your design decisions. There is a tendency among people to feel that your decisions are arbitrary. If you can muster the time, I have found it helpful to connect previous UX work to a finished design. It goes a long way to reminding your team or stakeholders of the evidence that supports your design.

#### Site Map

In each wireframe, show where this particular screen lives in your site map. Don’t show the entire site map, though, just the immediate parents, siblings and children. You can also refer to page IDs if you are using them in your site map.

#### Personas And User Goals

Include a label of the persona and the major user goals, tasks or behaviors that the screen is targeting. Alternatively, include user story statements and/or features from a feature priority matrix.

#### User Flows

Show the reader which step in the flow they are looking at. Include a portion of the user flow (enough for context), as opposed to the entire flow.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1041801b-2b00-4601-88d7-a3e30ac2414d/uxintegration-userflow-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6149b034-2bfc-4d8d-bfe7-e90cfc67b58f/uxintegration-userflow-preview-opt.jpg" alt="Wireframe with user flows embedded" width="500" height="435" /></a><figcaption>The flow below shows where the user is currently, but also shows the previous and next steps. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1041801b-2b00-4601-88d7-a3e30ac2414d/uxintegration-userflow-large-opt.jpg">Large preview</a>)</figcaption></figure>

#### User Research Findings

Include user research findings (as bullet points) that directly support your design decisions. These could come from user interviews, ethnographic studies, analytics, competitive analysis, surveys, focus groups or usability tests.

#### Open Questions

If you still need more information from stakeholders, developers or subject-matter experts, provide a list of questions under the annotation to give the reader context. Putting questions in the wireframe has several advantages:

*   reader will see that you are thinking deeply about the design.
*   promotes iteration and reduces anxiety about finalizing the design.
*   convenient for bringing up in presentations.

#### Usability Testing Questions

Your designs are not always going to be perfect from the first iteration. Minimize design “paralysis analysis” by choosing a hypothetical direction and then conducting usability tests to guide your design changes. List your user-testing questions so that people can see your thought process and so that you can keep track of contentious topics for your usability test plan.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/76fb65f1-6957-4a35-81b3-85129333dccb/uxintegration-usabilitytesting-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2f7519db-134d-41b0-b065-a29c0cf0d936/uxintegration-usabilitytesting-preview-opt.jpg" alt="Wireframe with usability testing questions" width="500" height="401" /></a><figcaption>I maintained a list of hypothetical questions on the side to show that I still need user feedback to move forward. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/76fb65f1-6957-4a35-81b3-85129333dccb/uxintegration-usabilitytesting-large-opt.jpg">Large preview</a>)</figcaption></figure>

### Wireframe Meta Data and Versioning

Inevitably, you will iterate through many versions of your wireframes. Including wireframe meta data and keeping track of changes will be helpful not only to other people, but also to you in the long run. Forming this habit takes time, but it’s well worth it.

<strong>Include a table of contents.</strong> A table of contents is especially important in production wireframes because there will be many pages. Also, InDesign can re-update your table of contents based on any new page changes. Setting up header styles can be finicky, so feel free to <a href="https://www.edriclapniramai.com/s/Wireframe-Template-Public.zip">use my template</a> (ZIP, 1.51 MB) if you need a quick start.

#### Add A Footer

The footer is the best place to include ancillary information about your wireframes. It also keeps your document together in case you print the wireframes and pages go missing. Consider including the following information:

*   Document name: Could simply include the project’s name, deliverable type and version number.
*   Page number
*   Confidential labels: Some companies require that you label documents “Private” or “Confidential”.

#### Track Wireframe Revisions

It can be difficult for readers to know what has changed when your wireframes have over 100 pages. So, ahead of your table of contents, include a table of revisions containing the following details:

*   date,
*   name of the person who made the revisions,
*   brief notes or bullet points about what has changed.

#### Maintain File Versioning

Every time you work on a new batch of wireframes (i.e. sending it out to people), create a copy of the previous file before working on the new one. Then, rename it and include at least these details:

*   Brand or client’s company name: Optional if it doesn’t make sense or if the file name gets too long.
*   Project name
*   Type of deliverable: wireframes, in this case.
*   Version number: lead with two 0’s for proper file sorting, because “1” can get incorrectly sorted with “10” and “100”.
*   Your name or initials: If you expect to collaborate with another designer
*   Delimiters: Use underscore or hyphen, instead of a space, which sometimes causes issues with file systems.

It could look like this: <code>Google_Youtube_Wireframes_001.graffle</code>.

Or, if you’re collaborating, it could look like this: <code>Apple-iTunes-Wireframes-EL-001.sketch</code>.

## Final Thoughts

Striving for perfection is a great goal, but be practical with your time, too. Most real-world projects don’t have ample timelines, so figure out your priorities, and use the guidelines that make sense.

My goal is to help fill in the gaps of every UX designer’s wireframing process with all of the knowledge I’ve gained over the years. I hope it helps you to perfect your wireframes.

I love to help people out, so let me know in the comments below or contact me if you have questions. Also, please share and spread the love if you’ve found this helpful!

### Resources

*   [Annotation wireframe template](https://www.edriclapniramai.com/s/Wireframe-Template-Public.zip), Edric Lapniramai (ZIP, 1.51 MB) 
An InDesign template for dropping in wireframe images and managing annotations.
*   [Liquidapsive](https://www.liquidapsive.com/)  
A website that shows exactly what happens with various scaling methods.
*   [StatCounter](https://gs.statcounter.com/#resolution-ww-monthly-200903-201605)  
A website that tracks currently used screen resolutions.
*   [W3Counter](https://www.w3counter.com/globalstats.php)  
Another website that tracks popular screen resolutions.
*   [Purdue Online Writing Lab](https://owl.english.purdue.edu/owl/resource/539/02/)  
Guidelines for technical writing techniques.
*   “[All About Grid Systems](https://webdesign.tutsplus.com/articles/all-about-grid-systems--webdesign-14471)”, Rachel Shillcock, Envato Tuts+  
An article on the theory behind grid systems.
*   “[Using Layout Grids Effectively](https://www.designersinsights.com/designer-resources/using-layout-grids-effectively)”, Designers Insights  
A brief article on some example layout grids and how to use them.
*   [Plugin search](https://github.com/search?utf8=%E2%9C%93&q=), GitHub  
A well-known source-code repository host that you can use to search for popular UI plugins.
*   [Principle](https://principleformac.com/)  
A prototyping tool for the Mac that enables you to fine-tune animations and transitions.
*   [Flinto](https://www.flinto.com/)  
Similar to Principle but a bit simpler with its motion design features.
*   [Axure](https://www.axure.com)  
A comprehensive prototyping tool that closely mimics what can be done with JavaScript.
*   [Origami](https://origami.design/)  
A prototyping tool that works from iOS and Android code.
*   [Framer](https://framerjs.com/)  
A prototyping tool that gives you greater control over the code for your transitions.
*   [Codepen](https://codepen.io/)  
A pure online code editor where you can quickly and easily test HTML, CSS and JavaScript animations.

#### Further Reading

- “[Creating Content Wireframes For Responsive Design](https://www.smashingmagazine.com/2016/02/create-content-wireframes-for-responsive-design/),” Tom Green
- “[The Skeptic’s Guide To Low-Fidelity Prototyping](https://www.smashingmagazine.com/2014/10/the-skeptics-guide-to-low-fidelity-prototyping/),” Laura Busche
- “[Beyond Wireframing: The Real-Life UX Design Process](https://www.smashingmagazine.com/2012/08/beyond-wireframing-real-life-ux-design-process/),” Marcin Treder

{{< signature "al, il, mrn" >}}
