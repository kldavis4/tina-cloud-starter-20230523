---
title: 'A Comprehensive Guide To Mobile App Design'
slug: comprehensive-guide-to-mobile-app-design
author: nickbabich
image: >-
  //archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4d4a8a86-1d74-4fee-bdb9-fc5f1ba88c66/mobile-app-design-image57-opt.png
date: 2018-02-12T18:00:25+01:00
summary: >-
  There are many things to consider when designing for mobile. We're sure that this detailed guide will help you get rid of that headache when building apps.
description: >-
  There are many things to consider when designing for mobile. We're sure that this detailed guide will help you get rid of that headache when building apps.
categories:
  - Mobile
  - Apps
  - Design
  - Guides
---
(*This is a sponsored article*.) More than ever, people are engaging with their phones in crucial moments. The average US user spends [5 hours per day on mobile](https://flurrymobile.tumblr.com/post/157921590345/us-consumers-time-spent-on-mobile-crosses-5). The vast majority of that time is spent in apps and on websites.

The difference between a good app and a bad app is usually the quality of its user experience (UX). A good UX is what separates successful apps from unsuccessful ones. Today, mobile users expect a lot from an app: fast loading time, ease of use and delight during interaction. If you want your app to be successful, you have to consider UX to be not just a minor aspect of design, but an essential component of product strategy.

There are many things to consider when designing for mobile. In this article, I've summarized a lot of practical recommendations that you can apply to your design.

## Minimize Cognitive Load

Cognitive load refers here to the amount of brain power required to use the app. The human brain has a limited amount of processing power, and when an app provides too much information at once, it might overwhelm the user and make them abandon the task.

{{% feature-panel %}}

### Decluttering

Cutting out the clutter is one of the major recommendations in “[10 Do’s and Don’ts of Mobile UX Design](https://theblog.adobe.com/10-dos-donts-mobile-ux-design/).” Clutter is one of the worst enemies of good design. By cluttering your interface, you overload users with too much information: Every added button, image and icon makes the screen more complicated.

Clutter is terrible on desktop, but it’s far worse on mobile (simply because we don’t have as much real estate on mobile devices as we do on desktops and laptops). It’s essential to get rid of anything in a mobile design that isn’t absolutely necessary because reducing clutter will improve comprehension. The technique of [functional minimalism](https://www.smashingmagazine.com/2017/10/functional-minimal-web-design/) can help you deal with the problem of a cluttered UI:

- Keep content to a minimum (present the user with only what they need to know).

- Keep interface elements to a minimum. A simple design will keep the user at ease with the product.

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/366208b7-5820-4dc1-b7c4-9ec12122666c/mobile-app-design-image67-opt.png" sizes="100vw" caption="The clear tab bar (right) is much better than the cluttered one (left). (Image: Apple)" alt="The clear tab bar (right) is much better than the cluttered one (left)." >}}

- Use the technique of progressive disclosure to show more options.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4149f7df-312e-4a3b-b2ee-ace7510bfb32/mobile-app-design-image107.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4149f7df-312e-4a3b-b2ee-ace7510bfb32/mobile-app-design-image107.gif" width="800" alt="ramotion" /></a><figcaption>The interface reveals more options after interaction. (Image source: <a href="https://ramotion.com">Ramotion</a>)</figcaption></figure>

### Offload Tasks

Look for anything in the design that requires user effort (this might be entering data, making a decision, etc.), and look for alternatives. For example, in some cases you can reuse previously entered data instead of asking the user to type more, or use already available information to set a smart default.

### Break Tasks Into Bite-Sized Chunks

If a task contains a lot of steps and actions required from the user’s side, it’s better to divide such tasks into a number of subtasks. This principle is extremely important in mobile design because you don’t want to create too much complexity for the user at one time. One good example is a step-by-step checkout flow in an e-commerce app, where the designer breaks down a complex checkout task into bite-sized chunks, each requiring user action.

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e5725ec4-09a9-4757-af00-f5393dbcce3f/mobile-app-design-image54-opt.png" sizes="100vw" caption="Chunking makes a form look less loaded, especially when you’re requesting a lot of information from the user. (Image source: <a href='https://dribbble.com/mutlu82'>Murat Mutlu</a>)" alt="Chunking makes a form look less loaded, especially when you’re requesting a lot of information from the user." >}}

Chunking can also help to connect two different activities (such as browsing and purchasing). When a flow is presented as a number of steps logically connected to each other, the user can more easily proceed through it.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1d568615-e477-4a1c-b885-66e72dda1ed0/mobile-app-design-image86.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1d568615-e477-4a1c-b885-66e72dda1ed0/mobile-app-design-image86.gif" width="800" alt="purchasing movie tickets example" /></a><figcaption>Finding a film and purchasing tickets to the cinema. (Image source: <a href="https://twitter.com/anton_skv">Anton Skvortsov</a>)</figcaption></figure>

### Use Familiar Screens

Familiar screens are screens that users see in many apps. Screens such as “Gettings started,” “What’s new” and “Search results” have become de facto standards for mobile apps. They don’t require additional explanation because users are already familiar with them. This allows users to use prior experience to interact with the app, with no learning curve.

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ce3386b4-5e77-4bda-b102-ade4258f145e/mobile-app-design-image74-opt.png" sizes="100vw" caption="User profile screen in Quora app" alt="User profile screen in Quora app" >}}

Consider reading “[The 11 Screens You’ll Find in Many of the Most Successful Mobile Apps](https://theblog.adobe.com/11-screens-youll-find-many-successful-mobile-apps/)” for more information on familiar screens.

### Minimize User Input

Typing on a small mobile screen isn't the most comfortable experience. In fact, it’s often error-prone. And the most common case of user input is filling out a form. Here are a few practical recommendations to make this process easy:

- Keep forms as short as possible by removing any unnecessary fields. The app should ask for only the bare minimum of information from the user.

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4d4a8a86-1d74-4fee-bdb9-fc5f1ba88c66/mobile-app-design-image57-opt.png" sizes="100vw" caption="A rule of thumb in form design is that shorter is better. Combine multiple fields into one easy-to-fill field. (Image source: Luke W.)" alt="A rule of thumb in form design is that shorter is better. Combine multiple fields into one easy-to-fill field." >}}

- Provide input masks. Field masking is a technique that helps users format inputted text. A mask appears once a user focuses on a field, and it formats the text automatically as the field is being filled out, helping users to focus on the required data and to more easily notice errors.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fa12c37f-8350-4a8f-a1d2-d05530d7415c/mobile-app-design-image105.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fa12c37f-8350-4a8f-a1d2-d05530d7415c/mobile-app-design-image105.gif" width="800" alt="input mask example" /></a><figcaption>(Image credit: <a href="https://www.joshmorony.com/wp-content/uploads/2017/01/input-mask.gif">Josh Morony</a>)</figcaption></figure>

- Use smart features such as autocomplete. For example, filling out an address field is often the most problematic part of any registration form. Using tools like [Place Autocomplete Address Form](https://developers.google.com/maps/documentation/javascript/examples/places-autocomplete-addressform) (which uses both geo-location and address prefilling to provide accurate suggestions based on the user’s exact location) enables users to enter their address with fewer keystrokes than they would have to with a regular input field.

- Dynamically validate field values. It’s frustrating when, after submitting data, you have to go back and correct mistakes. Whenever possible, check field values immediately after entry so that users can correct them right away.

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7b40e5d1-eede-4440-aa9d-f430846d0fb0/mobile-app-design-image70-opt.png" sizes="100vw" caption="Inline validation (Image source: <a href='https://cdn.baymard.com/data-broker/graphic-548-df365441c389949fc9dbf39ed204de5f.jpg'>Baymard</a>)" alt="Inline validation" >}}

- Customize the keyboard for the type of query. Display a numeric keyboard when asking for phone number, and include the @ button when asking for an email address. Ensure that this feature is implemented consistently throughout the app, rather than only for certain forms.

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/11aa6d9d-8151-41c5-afb6-e51a2fd7bc66/mobile-app-design-image95-opt.png" sizes="100vw" caption="Match the keyboard to the required text input. (Image: ThinkWithGoogle)" alt="Match the keyboard to the required text input." >}}

### Anticipate Users Needs

Proactively look for steps in the user journey where users might need help. For example, the screenshot below shows a part where users need to provide specific information.

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bd2ec68f-8fed-48bc-8ea4-f02218fb8ed0/mobile-app-design-image93-opt.png" sizes="100vw" caption="It is not obvious where the user can find the barcode. Concise help text next to the input field would be very useful. (Image source: <a href='https://www.hotjar.com/hs-fs/hub/1951809/file-4003469976-png/blog-files/help.png?t=1517831187847'>Hotjar</a>)" alt="It is not obvious where the user can find the barcode. Concise help text next to the input field would be very useful." >}}

### Use Visual Weight to Convey Importance

The most important element on the screen should have the most visual weight. Adding more weight to an element is possible with font weight, size and color.

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/881fb3c5-784e-412b-bf1d-aece0403ca69/mobile-app-design-image81-opt.jpg" sizes="100vw" caption="Large items catch the eye and appear more important than smaller ones. The “Request Lyft” button will capture user attention." alt="Large items catch the eye and appear more important than smaller ones. The “Request Lyft” button will capture user attention." >}}

### Avoid Jargon

Clear communication should always be a top priority in any mobile app. Use what you know about your target audience to determine whether certain words or phrases are appropriate.

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1ef283ca-deb6-42b0-9321-4a04b971c713/mobile-app-design-image87-opt.png" sizes="100vw" caption="Unknown terms or phrases will increase cognitive load for the user. (Image source: ThinkWithGoogle)" alt="Unknown terms or phrases will increase cognitive load for the user." >}}

### Make The Design Consistent

Consistency is a fundamental principle of design. Consistency eliminates confusion. Maintaining an overall consistent appearance throughout an app is essential. Regarding mobile app, consistency means the following:

- **Visual consistency**  
Typefaces, buttons and labels need to be consistent across the app.

- **Functional consistency**  
Interactive elements should work similarly in all parts of your app.

- **External consistency**  
Design should be consistent across multiple products. This way, the user can apply prior knowledge when using another product.

Here are a few practical recommendations on how to make a design consistent:

- **Respect platform guidelines.**  
Each mobile OS has standard guidelines for interface design: [Apple’s Human Interface Guidelines](https://developer.apple.com/ios/human-interface-guidelines/) and [Google’s Material Design Guidelines](https://material.io/guidelines/). When designing for native platforms, follow the OS’ design guidelines for maximum quality. The reason why following design guidelines is important is simple: Users become familiar with the interaction patterns of each OS, and anything that contradicts the guidelines will create friction.

- **Don’t mimic UI elements from other platforms.**  
As you build your app for Android or iOS, don’t carry over UI elements from other platforms. Icons, functional elements (input fields, checkboxes, switches) and typefaces should have a native feel. Use native components as much as possible, so that people trust your app.

- **Keep the mobile app consistent with the website.**  
This is an example of external consistency. If you have a web service and a mobile app, make sure that both of them share similar characteristics. This will allow users to make frictionless transitions between the mobile app and the mobile web. Inconsistency in design (for example, a different navigation scheme or different color scheme) might cause confusion.

## Put The User In Control

### Keep Interactive Elements Familiar And Predictable

Predictability is a fundamental principle of UX design. When things work in the way users predict, they feel a stronger sense of control. Unlike on desktop, where users can use hover effects to understand whether something is interactive or not, on mobile, users can check interactivity only by tapping on an element. That’s why, with buttons and other interactive elements, it’s essential to think about how the design communicates affordance. How do users understand an element as a button? Form should follow function: The way an object looks tells users how to use it. Visual elements that look like buttons but aren’t clickable will easily confuse users.

### The “Back” Button Should Work Properly

An improperly created “back” button can cause a lot of problems for users. Prevent situations when tapping the “back” button in a multi-step process would take users all the way back to the home screen.

A good design makes it easier for users to go back and make corrections. When users know that they can take a second look at data they’ve provided or options they’ve selected, this allows them to proceed with ease.

### Meaningful Error Messages

To err is human. Errors occur when people engage with apps. Sometimes, they happen because the user makes a mistake. Sometimes, they happen because the app fails. Whatever the cause, these errors and how they are handled have a huge impact on the UX. Bad error handling paired with useless error messages can fill users with frustration and could be the reason why users abandon your app.

Take an error-state screen from Spotify as an example. It doesn’t help users understand the context and doesn’t help them find the answer to the question, “What can I do about it?”

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/92a405e7-77ae-4111-b235-1d6a9330cb0d/mobile-app-design-image199-opt.png" sizes="100vw" caption="<a href='https://itunes.apple.com/us/app/spotify-music/id324684580?mt=8'>Spotify</a>’s error screen just states “An error occurred” and doesn’t provide any constructive advice on how to fix the problem." alt="Spotify’s error screen just states “An error occurred” and doesn’t provide any constructive advice on how to fix the problem." >}}

Don’t assume users are tech-savvy enough to figure things out. Always tell people what’s wrong in plain language. Each error message should tell users:

- what went wrong and possibly why,
- what’s the next step the user should take to fix the error.

Consider reading “[How to Design Error States for Mobile Apps](https://www.smashingmagazine.com/2016/09/how-to-design-error-states-for-mobile-apps/)” for more information on error handling.

## Design An Accessible Interface

Accessible design allows users of all abilities to use products successfully. Consider how users with vision loss, hearing loss and other disabilities can interact with your app.

### Be Aware Of Color-Blindness

[4.5% of the global population experience color-blindness](https://www.colourblindawareness.org/colour-blindness/) (that’s 1 in 12 men and 1 in 200 women), 4% suffer from low vision (1 in 30 people), and 0.6% are blind (1 in 188 people). It’s easy to forget that we’re designing for this group of users because most designers don’t experience such problems.

Let me give you a simple example. Success and error messages in mobile forms are often colored green and red, respectively. But red and green are the colors most affected by color-vision deficiency (these colors can be difficult to distinguish for people with deuteranopia or protanopia). Most probably you’ve seen the following error message when filling out a form: “The fields marked in red are required”? While it might not seem like a big thing, this error message combined with the form in the example below can be an extremely frustrating experience for people who have color-vision deficiency.

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c4996a88-58c4-4eaf-96e4-7ea6a3e54698/mobile-app-design-image94-opt.png" sizes="100vw" caption="The form field’s design relies only on red and green to indicate fields with and without an error. Color-blind users cannot differentiate the fields highlighted in red." alt="The form field’s design relies only on red and green to indicate fields with and without an error. Color-blind users cannot differentiate the fields highlighted in red." >}}

As the [W3C’s guidelines](https://www.w3.org/TR/UNDERSTANDING-WCAG20/visual-audio-contrast-without-color.html) state, color shouldn’t be used as the only visual means of conveying information, indicating an action, prompting a response or distinguishing a visual element. It’s important to use other visual signifiers to ensure that users will be able to interact with an interface.

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d8316f62-cea1-4508-88ff-e66afb56dd50/mobile-app-design-image104-opt.png" sizes="100vw" caption="The use of icons and labels to show which fields are invalid better communicates the information to a color-blind user." alt="The use of icons and labels to show which fields are invalid better communicates the information to a color-blind user." >}}

### Make Animations Optional

Users who suffer from motion sickness often turn off the animated effects in their OS settings. When the option to reduce motion is enabled in accessibility preferences, your app should minimize or eliminate its own animations.

## Make The Navigation Simple

Helping users navigate should be a high priority for every app. All the cool features and compelling content that your app has won’t matter if people can’t find them; also, if it takes too much time or effort to discover how to navigate your product, chances are you’re just going to lose users. Users should be able to explore the app intuitively and to complete all primary tasks without any explanation.

### Use Standard Navigation Components

It’s better to use standard navigation patterns, such as the [tab bar](https://developer.apple.com/ios/human-interface-guidelines/bars/tab-bars/) (for iOS) and the [navigation drawer](https://material.io/guidelines/patterns/navigation-drawer.html) (for Android). The majority of users are familiar with both navigation patterns and will intuitively know how to get around your app.

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4ead9319-1144-4e00-975c-64799016c692/mobile-app-design-image100-opt.png" sizes="100vw" caption="Side drawer (Android). (Image source: Material Design)" alt="Side drawer (Android)." >}}

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8a4f456f-1ea2-4c22-9713-e2f70c5d0b09/mobile-app-design-image63.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8a4f456f-1ea2-4c22-9713-e2f70c5d0b09/mobile-app-design-image63.gif" width="800" alt="tab bar on ios" /></a><figcaption>Tab bar (iOS). (Image source: <a href="https://www.ramotion.com">Ramotion</a>)</figcaption></figure>

For more information on navigation patterns, read the article “[Basic Patterns for Mobile Navigation: Pros and Cons.](https://www.smashingmagazine.com/2017/05/basic-patterns-mobile-navigation/)”

### Prioritize Navigation Options

Prioritize navigation based on the way users interact with your app. Assign different priority levels (high, medium, low) to common user tasks. Give prominence in the UI to paths and destinations with high priority levels and frequent use. Use those paths to define your navigation. Organize your information structure in a way that requires a minimum number of taps, swipes and screens.

### Don’t Mix Navigation Patterns

When you choose a primary navigation pattern for your app, use it consistently. There shouldn't be a situation in which part of your app has a tab bar, while another part has a side drawer.

### Make Navigation Visible

As <a href="https://www.nngroup.com/articles/ten-usability-heuristics/">Jakob Nielsen says</a>, recognizing something is easier than remembering it. Minimize the user’s memory load by making actions and options visible. Navigation should be available at all times, not just when we anticipate that the user needs it.

### Communicate Current Location

Failing to indicate the current location is a very common problem of many mobile app menus. “Where am I?” is one of the fundamental questions users need to answer in order to successfully navigate. People should know where they are in your app at any moment.

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9bb19b26-0086-4dc4-a53b-626b441b557b/mobile-app-design-image56-opt.png" sizes="100vw" caption="The Health app (designed by Apple) provides information about the current section (the navigation option “Health data” is highlighted) and subsection (the headline “Activity” is visible at the top of the layout)." alt="The Health app (designed by Apple) provides information about the current section (the navigation option “Health data” is highlighted) and subsection (the headline “Activity” is visible at the top of the layout)." >}}

## Use Functional Animation to Clarify Navigational Transitions

Animation is the best tool to describe state transitions. It helps users comprehend a state change in the page’s layout, what has triggered the change and how to initiate the change again when needed.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3f148997-00b3-4105-9922-66c5cf569f11/mobile-app-design-image108.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3f148997-00b3-4105-9922-66c5cf569f11/mobile-app-design-image108.gif" width="800" alt="functional animation example" /></a><figcaption>Functional animation can efficiently guide the user’s attention and make complex transitions easy to understand. (Image source: <a href="https://twitter.com/jaeseongjeong">Jae-seong, Jeong</a>)</figcaption></figure>

### Be Careful With Using Gestures In The UI

Using gestures in interaction design can be tempting. But in most cases, it’s better to avoid this temptation. When gestures are used as a primary navigation option, they can cause a terrible UX. Why? Because **gestures are hidden controls**.

As Thomas Joos [points out](https://www.smashingmagazine.com/2013/05/gesture-driven-interface/#the-learning-curve) in his article “Beyond the Button: Embracing the Gesture-Driven Interface,” the biggest downside of using gestures in a user interface is the learning curve. Every time a visible control is replaced with a gesture, the app’s learning curve goes up. This happens because gestures have lower discoverability &mdash; they are always hidden, and people need to be able to identify these options in order to use them. That’s why it’s essential to use only widely accepted gestures (the ones that users expect in your app).

When it comes to using gestures in a UI, follow a few simple rules:

- **Use standard gestures.**  
By “standard,” I mean gestures that are most natural for the app in your category. People are familiar with the standard gestures, so no extra effort is required to discover or remember them.
- **Offer gestures as a supplement to, not a replacement for, visible navigation options.**  
Gestures might work as shortcuts for navigation, but not as a complete replacement for visible menus. Thus, always offer a simple, visible way to navigate, even if it means a few extra actions.

For more information on using gestures in your UI, consider reading “[In-App Gestures and Mobile App User Experience](https://www.smashingmagazine.com/2016/10/in-app-gestures-and-mobile-app-user-experience/).”

## Focus On The First-Time Experience

The first-time experience is a make or break part of mobile apps. You only get one shot at a first impression. And if you fail, there's a huge probability that users won't launch your app again. (Research by Localytics shows that [24% of users](https://info.localytics.com/blog/24-of-users-abandon-an-app-after-one-use) never return to an app after the first use.)

### Avoid Sign-In Walls

A sign-in wall is mandatory registration before using an app. It is a common source of friction for users and one of the reasons why users abandon apps. The number of users who abandon the process of registration is especially significant for apps with low brand recognition or those in which the value proposition is unclear.

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/01456013-8cff-45bf-bb72-38f844e77955/mobile-app-design-image99-opt.png" sizes="100vw" caption="Pinterest asks users to create a new account or log in upon first loading." alt="Pinterest asks users to create a new account or log in upon first loading." >}}

As a rule of thumb, only ask users to register if it's essential (for example, if core features of your app are available only when users complete registration). And even in this case, it’s better to delay sign-in as long as possible &mdash; allow users to experience the app for a little while (for example, take a tour), and only then gently remind them to sign up. This will give your users a taste of the experience, and they will be more likely to commit to it.

### Design A Good Onboarding Experience

In the context of the mobile UX, delivering an excellent onboarding experience is the foundation for retaining users. The goal of onboarding is to show the value your app provides.

Among the many strategies for onboarding, one is especially effective: contextual onboarding. Contextual onboarding means that instructions are provided only when the user needs them. Duolingo is an excellent example. This app pairs an interactive tour with progressive disclosure to show users how the app works. Users are encouraged to jump in and do a quick test in their selected language. This makes learning fun and discoverable.

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6ab075b2-13df-4f11-9bf6-fa42a85e42c6/mobile-app-design-image90-opt.png" sizes="100vw" caption="Duolingo has a user-guided tour that consists of a quick test." alt="Duolingo has a user-guided tour that consists of a quick test." >}}

Another thing that can be very helpful during onboarding is an empty state. An empty state is a screen whose default state is empty and requires users to go through one or more steps to populate it with data. Besides informing the user of what content to expect on the page, an empty state can also teach people how to use an app. Even if the onboarding process consists of just one step, the guidance will reassure users that they are doing the right thing.

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/af404a03-15f7-4cf7-bc48-52f5ffd46ec4/mobile-app-design-image83-opt.png" sizes="100vw" caption="The empty state in Expensify reassures users by telling them how to get started." alt="The empty state in Expensify reassures users by telling them how to get started." >}}

Consider reading “[The Role of Empty States in User Onboarding](https://www.smashingmagazine.com/2017/02/user-onboarding-empty-states-mobile-apps/#comments-user-onboarding-empty-states-mobile-apps)” for more information on onboarding.

## Don’t Ask for Set-Up Information Up Front

A mandatory set-up phase creates friction and can lead to abandonment of the app. When users launch an app, they expect it to just work. Thus, design your app for the majority of users, and let the few who want a different configuration adjust their settings to meet their needs any time they want.

**Tip**: Try to infer what you need from the system. If you need information about the user, device or environment, query the system for that whenever possible, instead of asking the user.

### Avoid Asking For Permissions Right At The Start

Avoid a situation in which the first thing a user sees when launching the app is a dialog requesting permission. Similar to a sign-in wall or up-front set-up phase, requesting permission at launch should be done only when it’s necessary for your app’s core function. Users won’t be bothered by this request if it’s evident that your app depends on that permission in order to operate (for example, it’s clear why a photo editor would request access to photos).

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/db4ebbbe-ac30-4c48-91b2-c74d1838f1ae/mobile-app-design-image60-opt.png" sizes="100vw" caption="Permission request patterns proposed by Google. (Image: Material Design)" alt="Permission request patterns proposed by Google." >}}

But for any other cases, ask for permissions in context. Users are more likely to grant permission if asked during a relevant task.

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b7945569-7455-4f29-9a92-46d9b758a3dc/mobile-app-design-image68-opt.png" sizes="100vw" caption="Apps should ask for permissions in context and should communicate the value that the access will provide. Prompt users to accept permissions only when they try to use the feature. (Image: Cluster)" alt="Apps should ask for permissions in context and should communicate the value that the access will provide. Prompt users to accept permissions only when they try to use the feature." >}}

**Tips**:

- **Ask only for what your app clearly needs.**  
Don’t ask for all possible permissions. It would be suspicious if an app requests something that it has no obvious need for.  For example, an alarm clock app asking for permission to access your list of contacts would be suspect.

- **Explain why your app needs the information, if it’s not obvious.**  
Sometimes you need to provide more context for your request. For this reason, you can design a custom alert to request permission.

## Make Your App Appear Fast And Responsive

Loading time is extremely important for the UX. As technology progresses, we get more impatient, and today, [47% of users](https://www.bluecorona.com/blog/20-web-design-facts-small-business-owners/) expect a page to load in 2 seconds or less.

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/05453c6d-f90c-4d50-aefe-ce63fd3de6c0/mobile-app-design-image92-opt.png" sizes="100vw" caption="The faster your app, the better the experience will be. (Image source: <a href='https://www.thinkwithgoogle.com/marketing-resources/data-measurement/mobile-page-speed-new-industry-benchmarks/'>Google</a>)" alt="The faster your app, the better the experience will be." >}}

If a page takes more time to load, visitors might become frustrated and leave. That’s why speed should be a priority when building a mobile app. But no matter how fast you make an app, some things will take time to process. A slow response could be caused by a bad Internet connection, or an operation could be taking a long time. But even if you can’t shorten the line, at least try to make the wait more pleasant.

### Concentrate On Loading Content In The Visible Area Of The Screen

Load just enough content to fill the screen when a page opens. Content available on scroll should continue to load in the background. The benefit of this approach is that users will be engaged in reading the initial content and, in some cases, won’t even notice that content is still loading.

### Make It Clear When Loading Is Occuring

A blank or static screen that users see when content is loading can make it seem like your app is frozen, resulting in confusion and frustration, and potentially causing people to leave your app. At a minimum, show a loading spinner that makes it clear that something is happening. For a longer wait time (more than 10 seconds), it’s essential to display a progress bar so that the user can gauge how long they’ll be waiting.

Consider reading “[Best Practices for Animated Progress Indicators](https://www.thinkwithgoogle.com/marketing-resources/data-measurement/mobile-page-speed-new-industry-benchmarks/)” for more information on loading indicators.

### Offer A Visual Distraction

If an app gives users something interesting to look at while waiting, users will pay less attention to the wait itself. Thus, to ensure people don’t get bored while waiting for something to happen, offer them a distraction. A fine animated waiting indicator can retain users’ attention while they wait.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ae008f73-2766-455a-9fd7-7dbf302fa996/mobile-app-design-image78.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ae008f73-2766-455a-9fd7-7dbf302fa996/mobile-app-design-image78.gif" width="800" alt="animation delighting user example" /></a><figcaption>Attention to fine movement can delightfully surprise the user. (Image credit: <a href="https://dribbble.com/UI8">UI8</a>)</figcaption></figure>

**Tip**: Keep longevity in mind. Even good animation can be annoying when it’s overused. When designing an animation, ask yourself, “Will the animation get annoying on the hundredth use, or is it universally clear and unobtrusive?”

## Skeleton Screens

Skeleton screens (i.e. temporary information containers) are essentially a blank version of a page into which information is gradually loaded.

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/03b958d9-37cb-4318-ab02-b4917dd0aabe/mobile-app-design-image64-opt.png" sizes="100vw" caption="A skeleton screen shows the screen immediately. Placeholders replace any elements in the layout whose content isn't available yet. (Image: Slack)" alt="A skeleton screen shows the screen immediately. Placeholders replace any elements in the layout whose content isn't available yet." >}}

A skeleton screen would appear the moment your app starts loading data, giving users the impression that your app is fast and responsive.  Unlike a loading indicator, which just conveys that something is happening, a skeleton screen focuses on actual progress.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e0891fd0-143a-41b2-a4b8-053cbd45dc9f/mobile-app-design-image-55.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e0891fd0-143a-41b2-a4b8-053cbd45dc9f/mobile-app-design-image-55.gif" width="800" alt="skeleton screen example" /></a><figcaption>A skeleton screen fills out the UI as content is loaded incrementally. (Image source: <a href="https://www.tandemseven.com/blog/how-to-use-disneys-principles-of-animation-to-improve-ux/">Tandem Seven</a>)</figcaption></figure>

## Optimize Content For Mobile

Content plays a significant role in design. In most cases, the primary reason why people use an app is the content it provides. But it’s not enough just to have clear, well-crafted content. The content has to be easy to digest.

### Make Text Readable and Legible

When we think about content, in most cases we mean typography.  As Oliver Reichenstein states in his essay “[Web Design Is 95% Typography](https://ia.net/topics/the-web-is-all-about-typography-period/)”:

<blockquote>“Optimizing typography is optimizing readability, accessibility, usability(!), overall graphic balance.”</blockquote>

The key to mobile typography is readability and legibility. If users can’t read your content, there’s no point in offering content in the first place.

First, a few practical recommendations on legibility:

- **Font size**  
Generally, anything smaller than 16 pixels (or 11 points) is challenging to read on any screen.

- **Font family**  
Most users prefer a clear, easy-to-read font. A safe bet is the system’s default typeface (Apple iOS uses the [San Francisco font](https://developer.apple.com/fonts/); Google Android uses [Roboto](https://fonts.google.com/specimen/Roboto)).

- **Contrast**  
Light-colored text (such as light gray) might look aesthetically appealing, but users will have a hard time reading it, especially against a light background. Make sure there is plenty of contrast between the font and the background for easy readability. The [WC3’s web content accessibility guidelines](https://www.w3.org/TR/UNDERSTANDING-WCAG20/visual-audio-contrast-contrast.html) provide contrast ratio recommendations for images and text.

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/403a2629-204f-4907-a16d-815983286038/mobile-app-design-image101-opt.png" sizes="100vw" caption="Even high-contrast text is hard to read when there is glare, but low-contrast text is nearly impossible to read." alt="Even high-contrast text is hard to read when there is glare, but low-contrast text is nearly impossible to read." >}}

And now, a few recommendations for readability:

- **Avoid all caps.**  
All caps text &mdash; meaning text with all letters cap­i­tal­ized &mdash; is fine in contexts that don’t involve attentive reading (such as acronyms and logos), but avoid it when your message requires heavy reading.

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/aff81945-204f-406b-a517-6a7dae3a372e/mobile-app-design-image75-opt.png" sizes="100vw" caption="" alt="capitalizing full paragraphs is bad and even harder to read when bolden" >}}

- **Limit the length of text lines.**  
A good rule of thumb is to use 30 to 40 characters per line for mobile.

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1eab8413-730d-4f27-b279-0f278552e26f/mobile-app-design-image96-opt.png" sizes="100vw" caption="Left: The text is too small to read on a small device without pinching and zooming. Right: The text is comfortable to read on a mobile screen." alt="Left: The text is too small to read on a small device without pinching and zooming. Right: The text is comfortable to read on a mobile screen." >}}

- **Don’t squeeze lines.**  
Adding space between text aids the user in reading and creates a feeling that there isn’t so much information to take in.

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/70d7ce01-8f17-46e4-8417-0f190845e4b2/mobile-app-design-image79-opt.png" sizes="100vw" caption="Too tight, too much, and just right. By adding the right amount of space to text &mdash; both between lines and in the margins &mdash; you help users better absorb the words." alt="Too tight, too much, and just right. By adding the right amount of space to text &mdash; both between lines and in the margins &mdash; you help users better absorb the words." >}}

### HD-Quality Images And The Right Aspect Ratio

The rise of devices with high-resolution screens sets a bar for the quality of images. Images shouldn’t appear pixelated on HD screens.

Images should always appear in the right aspect ratio, so that they don’t look distorted. Images that are stretched too wide or too long just to fit in a space will look unappealing and out of place.

The latest challenge many mobile designers face is optimizing the UX for the iPhone X. Designing for the iPhone X requires a different size of artboard that any other iPhone (you’ll need 375 x 812-point resolution images at 3x).

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d0296194-91dc-4c09-bdff-fbac751ae264/mobile-app-design-image71-opt.png" sizes="100vw" caption="(Image credit: Apple)" alt="(Image credit: Apple)" >}}

Consider reading “[Designing Apps for iPhone X: What Every UX Designer Needs to Know About Apple’s Latest Device](https://theblog.adobe.com/designing-apps-iphone-x-every-ux-designer-needs-know-apples-latest-device/)” for more information on designing for the iPhone X.

### Video Content Is Optimized For Portrait Mode

Video is quickly becoming a standard method of content consumption for many users. According to YouTube, [mobile video consumption grows by 100% every year](https://www.forbes.com/sites/forbesagencycouncil/2017/02/03/video-marketing-the-future-of-content-marketing/#5953328f6b53). By 2020, over [75% of global mobile data traffic will be video content](https://www.cisco.com/c/en/us/solutions/collateral/service-provider/visual-networking-index-vni/mobile-white-paper-c11-520862.html). This means that it’s essential to optimize video content for portrait mode.

According to ScientiaMobile, [94% of users use their mobile device in portrait mode](https://twitter.com/lukew/status/563010808641490944?lang=en). If your app provides video content, it should be optimized to allow users to watch it in portrait mode.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/06148134-af53-4c7a-bf3e-8fa7df26ee1e/mobile-app-design-image58.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/06148134-af53-4c7a-bf3e-8fa7df26ee1e/mobile-app-design-image58.gif" width="800" alt="facebook app portrait mode" /></a><figcaption>Facebook Live allows you to watch video in Facebook’s timeline. (Image source: Giphy)</figcaption></figure>

## Design For Touch

Designing for touch has a goal of reducing the number of incorrect inputs and making interaction with an app more comfortable.

### Design For Fingers, Not Cursors

When you’re designing actionable elements in a mobile interface, it’s vital to make targets big enough so that they’re easy for users to tap. Mistaken taps often happen due to small touch controls.

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d8a12bdc-0085-4b18-ac09-1019f288fc0b/mobile-app-design-image102-opt.png" sizes="100vw" caption="A small touch target increases the chance of false selection. (Image source: Apple)" alt="A small touch target increases the chance of false selection." >}}

When designing a touch target, you can rely on the [MIT Touch Lab’s study](https://touchlab.mit.edu/publications/2003_009.pdf) (PDF) to choose a proper size for interactive elements. This study found that the average size of finger pads are between 10 and 14 mm and fingertips are 8 to 10 mm, making 10 by 10 mm a good minimum touch target size.

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/76b9d985-ac43-43cd-925d-6dc2f5392964/mobile-app-design-image299-opt.png" sizes="100vw" caption="10 by 10 mm is a good minimum touch target size. (Image source: UXmag)" alt="10 by 10 mm is a good minimum touch target size." >}}

Not only is the size of the target important, but it’s also essential to have the right amount of space between targets. If multiple touch targets are near each other (for example, “Agree” and “Disagree” buttons), ensure that there is good amount of space between them.

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fffd41a5-0351-49dc-ac21-9367bcbef03c/mobile-app-design-image73-opt.png" sizes="100vw" caption="An example of space between buttons. (Image source: Material Design)" alt="An example of space between buttons." >}}

### Consider Thumb Zone

Designing for thumbs isn’t only about making targets big enough, but also about considering the way we hold our devices. A lot of users hold their phone with one hand. Only a part of the screen would be a genuinely effortless territory for their thumbs. This territory is called the natural thumb zone. Other zones require finger stretching or even changing the grip to reach them. Below, you can see what the safe zone looks like on a modern mobile device.

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/33e34642-f6e3-4468-a7f4-75c718171dd4/mobile-app-design-image98-opt.png" sizes="100vw" caption="Thumb zones, according to research by Scott Hurff. (Image source: Smashing Magazine)" alt="Thumb zones, according to research by Scott Hurff." >}}

The bigger the display, the more of the screen is less easily accessible.

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/38819605-b566-40d2-acd2-8cd951641671/mobile-app-design-image66-opt.png" sizes="100vw" caption="Thumb zones for a right-handed person, according to <a href='https://scotthurff.com/posts/how-to-design-for-thumbs-in-the-era-of-huge-screens'>research by Scott Hurff</a>." alt="Thumb zones for a right-handed person, according to research by Scott Hurff." >}}

Consider all zones when designing for mobile:

- The green zone is the best place for navigation options or frequent interactive actions (such as call-to-action buttons).

- The red zone is the best place for potential danger options (such as “Delete” or “Erase”). Users are less likely to trigger this option accidentally.

### Feedback on Interaction

In the physical world, objects respond to our interaction. People expect a similar level of responsiveness from digital UI controls. You’ll need to provide instant feedback on every user interaction. If your app doesn’t provide feedback, the user will wonder if it has frozen or if they missed the target. The feedback could be visual (highlighting a tapped button) or tactile (a device vibration on input).

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/64058f47-90aa-4cde-a357-517472efffab/mobile-app-design-image88.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/64058f47-90aa-4cde-a357-517472efffab/mobile-app-design-image88.gif" width="800" alt="apps visual animation example" /></a><figcaption>Apps that provide a visual animation or other type of visual eliminate this guesswork for the user. (Image credit: <a href="https://www.behance.net/motioq">Vadim Gromov</a>)</figcaption></figure>

## Humanize The Digital Experience

UX isn’t only about usability; it’s mostly about feelings. And when we think about what makes us feel great, we often think about well-crafted design.

### Personalized Experience

Personalization is one of the most critical aspects of mobile apps today. It’s an opportunity to connect with users and provide the information they need in a way that feels genuine.

There are countless ways to improve the mobile UX by incorporating personalization. It’s possible to offer personalized content depending on the user’s location, their past searches and their past purchases. For example, if your users prefer to purchase particular groups of products each month, an app might track that and offer them special deals on those types of products.

Starbucks’ mobile app is an excellent example that follows this approach. The app uses information provided by users (for example, the type of coffee they usually order) to craft special offers.

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c01c7243-9c50-4614-b345-bfb910172096/mobile-app-design-image84-opt.png" sizes="100vw" caption="Starbucks provides offers and services tailored to individual customers" alt="Starbucks provides offers and services tailored to individual customers" >}}

### Delightful Animation

Unlike functional animation, which is used to improve the clarity of a user interface, delightful animation is used to make an interface feel human. This type of animation makes it clear that the people who crafted the app care about their users.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f849fffb-bfa8-4f35-afff-374dbb5874eb/mobile-app-design-image89.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f849fffb-bfa8-4f35-afff-374dbb5874eb/mobile-app-design-image89.gif" width="800" alt="delightful app details that create emotional connection with users" /></a><figcaption>Using delightful details is an opportunity to create an emotional connection with your users. (Image credit: <a href="https://twitter.com/sganushchak">Serhii Hanushchak</a>)</figcaption></figure>

## Optimize Push Notifications

Annoying notifications are the number 1 reason people uninstall mobile apps (according to 71% of respondents).

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e625001d-a599-4964-9f4b-3b510efe67a8/mobile-app-design-image72-opt.png" sizes="100vw" caption="(Image source: Appiterate Survey)" alt="top 7 reasons why people uninstall mobile apps" >}}

Don’t send push notifications just because you can. Each notification should be valuable and well timed.

### Push The Value

When a user starts using your app, they won’t mind getting notifications, as long as the value they get is sufficiently greater than the interruption. Almost [50% of users](https://info.localytics.com/blog/the-inside-view-how-consumers-really-feel-about-push-notifications) are grateful for notifications that interest them. Personalizing content to inspire and delight is critical. Netflix is an excellent example of a company that “pushes the value.” It carefully uses viewing data to present recommendations that feel tailor-made.

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e2c13776-34ba-4109-8f89-ba4fdd001486/mobile-app-design-image85-opt.png" sizes="100vw" caption="Netflix does a great job of personalizing its push notifications, letting users know when their favorite shows are available." alt="Netflix does a great job of personalizing its push notifications, letting users know when their favorite shows are available." >}}

### Avoid Sending Many Notifications In A Short Period Of Time

Too many notifications delivered in a short period of time can lead to the situation known as notification overkill &mdash; where a user can’t process the information and simply skips it. Limit the total number of notifications by combining different messages.

### Time Your Notifications

Not only is what you say important, but also when you say it. Don’t send push notifications at weird hours (such as in the middle of the night). The best time for push notifications is peak hours of mobile usage: from 6:00 pm till 10:00 pm.

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/47722c42-0ede-4780-a244-7cc24f31742d/mobile-app-design-image76-opt.png" sizes="100vw" caption="(Image source: comScore)" alt="device preferences throughout the day" >}}

### Consider Other Channels To Deliver Your Message

Push notifications aren’t the only way to deliver a message. Use email, in-app notifications and news feed messaging to notify users about important events, according to the level of urgency and type of content you would like to share.

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/216cabb2-e81b-4a6a-914b-0b799f9348f3/mobile-app-design-image61-opt.png" sizes="100vw" caption="Select the proper notification type based on the urgency and content. (Image: Appboy)" alt="Select the proper notification type based on the urgency and content." >}}

## Optimize For Mobile

### Design For Interruption

We live in a world of interruption. Something is constantly trying to distract us and direct our attention elsewhere. Not to mention, a lot of mobile sessions happen when users on the go. For example, users might use your app while waiting for the train. Such sessions can be interrupted at any time. Users can be easily frustrated when an app forgets their current progress as soon as they close it.

When an interruption occurs, your app should save the current state (context) and allow users to continue where they left off. This will make it easier for users to re-engage with the app when they return to it after the interruption.

### Take Advantage Of The Device’s Capabilities

Mobile devices have a lot of sensors (camera, location tracking, accelerometer) that can be used to improve the UX. Here are just a few features that you can use to do that:

- **Camera**  
It’s possible to simplify data input operations by using a camera. For example, you could use the digital camera to read credit card numbers automatically.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9aecf7e7-bcf4-4577-a672-5d71629fd295/mobile-app-design-image69.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9aecf7e7-bcf4-4577-a672-5d71629fd295/mobile-app-design-image69.gif" width="800" alt="app using phone camera to read credit card numbers" /></a><figcaption>(Image credit: Business Insider)</figcaption></figure>

- **Location awareness**  
Apps can use a device’s location data to provide content relevant to the user’s location or to simplify certain operations. For example, if you’re designing an app for food delivery, instead of asking the user to provide an address for delivery, you can auto-detect their current location and ask the user to confirm that they want to receive a delivery to that location.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/efa77457-9a55-4e17-b83d-c13ee807957a/mobile-app-design-image-103.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/efa77457-9a55-4e17-b83d-c13ee807957a/mobile-app-design-image-103.gif" width="800" alt="uber eat app example" /></a><figcaption>Apps like Uber Eat already use this property to reduce the number of actions required by the user.</figcaption></figure>

- **Biometric authentication**  
It’s possible to minimize the number of steps required to log in to an app using features like fingerprint touch login or facial identification.

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/523fe356-fcba-42b1-ba0e-ae5474c58ffc/mobile-app-design-image97-opt.png" sizes="100vw" caption="Chase Mobile’s app provides a one-touch log-in feature." alt="Chase Mobile’s app provides a one-touch log-in feature." >}}

**Tip**: You can find practical recommendations on how to use Apple’s Face ID in our article “[Designing Apps for iPhone X: What Every UX Designer Needs to Know About Apple’s Latest Device](https://theblog.adobe.com/designing-apps-iphone-x-every-ux-designer-needs-know-apples-latest-device/).”

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b4a4343b-1423-4041-9a8b-220f785eb668/mobile-app-design-image65-opt.png" sizes="100vw" caption="Use Face ID during sign-in for the iPhone X (as a replacement for a password). (Image source: Tesco)" alt="Use Face ID during sign-in for the iPhone X (as a replacement for a password)." >}}

### Strive To Create A Multi-Channel Experience

Don’t think of your mobile app as an isolated experience. When it comes to creating a user journey, the ultimate goal is to create a seamless experience, across all devices. Users should be able to switch to a different medium and continue the journey.

According to Appticles, [37% of users](https://www.appticles.com/blog/2016/03/mobile-vs-desktop-13-essential-user-behaviors/) do research on mobile but switch to desktop to complete a purchase. Thus, if you’re designing an e-commerce app, mobile users should be able to switch to their desktop or laptop to continue the journey. Synchronization of user progress across devices is a key priority for creating a seamless experience. It makes users feel that their workflow isn’t interrupted.

## Adapt Mobile Design To Emerging Markets

According to Google, [a billion new users are expected to come online](https://www.blog.google/topics/next-billion-users/) in the next couple of years. And the vast majority of them will be from emerging markets (or so-called mobile-first countries, like India, Indonesia, Brazil and Nigeria). They will gain access through a mobile phone. These users will have very different experiences and expectations from those who are in the US and Europe.

If you’re interested in going global, it’s important to consider their experiences.

### Poor Internet Connectivity

In the US and Europe, users are accustomed to ubiquitous connectivity. But that certainly isn’t true worldwide. Products in emerging markets have to be able to perform over slow or intermittent connectivity. Depending on a person’s location, the network might switch from Wi-Fi to 3G to 2G to no connectivity at all, and your product has to accommodate that.

If you plan to design for such market, consider the following:

- Make sure your product works when it isn’t connected to the Internet at all. Allow caching of data.

- Optimize your product for fast loading. Minimize page size by keeping images and other weighty content to a minimum; and reduce the size of that content.

[YouTube Go](https://youtubego.com/signup/) is an excellent example of a mobile app designed around connectivity constraints. The app was designed to be offline-first (meaning that it’s usable even when it isn’t connected to the Internet). The app lets users preview videos first and allows them to select a video’s file size before saving it offline to watch later. It also has a great feature that lets users share videos easily with friends and family nearby, without using any data.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f7d027ea-b141-4707-8529-35241e4a4b38/mobile-app-design-image77.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f7d027ea-b141-4707-8529-35241e4a4b38/mobile-app-design-image77.gif" width="800" alt="youtube go app example" /></a><figcaption>YouTube Go lets users send and receive videos when they’re together, using offline peer-to-peer sharing.</figcaption></figure>

[Google News & Weather](https://play.google.com/store/apps/details?id=com.google.android.apps.genie.geniewidget) is another great example of an app that was designed around bad connections. The app has a feature called “Lite mode” for people on low-bandwidth connections. When this mode is activated, it trims content down to its essentials, so that the app loads more quickly. According to Google, this mode uses less than one third of the normal data, and it activates automatically when the app detects a slow network.

### Limited Data

In about [95% of emerging markets](https://design.google/library/connectivity-culture-and-credit/), people rely almost entirely on expensive prepaid mobile data. People buy a fixed amount of data, and many can only afford something like 250 MB of data per month.

These users appreciate transparency when it comes to understanding their data consumption. They also value the ability to control whether a product downloads over Wi-Fi or uses data.

Below, you can see another example from YouTube Go. After selecting a video, users can choose the quality of the video. The app lets them know up front how much data they’ll spend before committing to an action.

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/85400162-fad8-400b-8326-a7d5f3f65c51/mobile-app-design-image82-opt.png" sizes="100vw" caption="YouTube Go lets you preview videos and choose their file size before saving it offline to watch later." alt="YouTube Go lets you preview videos and choose their file size before saving it offline to watch later." >}}

### Limited Device Capabilities

Smartphones in mobile-first countries have dramatically different capabilities from the Pixels and iPhones popular in the US. Most emerging-market devices cost below $100 and might come with limited storage and processing power. Make sure that the product you design works with older, low-end devices and software.

### Local Aesthetics

Minimalist design, which is popular in the Western world today, might be considered too bare for other cultures. If you want your product to succeed in emerging markets, pay attention to the cultural aesthetics. You can get inspiration from regionally popular products or hire local designers who are familiar with user preferences. Designing according to local aesthetics will make your product feel more relatable.

### Specifics of Region

When Google adapted Google Maps for India, it considered that India is the largest two-wheeler market in the world, and the millions of motorcycle and scooter riders have different needs than drivers of automobiles. It released two-wheeler mode in Maps. This mode shows trip routes that use shortcuts, not accessible to cars and trucks.

## Testing And Feedback

All of the principles you’ve just read can help you design a better experience for mobile, but they won’t replace the need for user research and testing. You’ll still need to test your solution with real users to understand which parts of the UI require improvement.

### Feedback Loop

Encourage user feedback at every opportunity. In order to collect valuable feedback, you need to make it easy for users to provide it. Thus, build a feedback mechanism right into your product. This could be as simple as a form marked “Leave feedback.” Just make sure that it works seamlessly for your users.

### Design Is A Never-Ending Process

It’s fair to say that design is a process of continual improvement. As product designers, we use analytics and user feedback to improve the experience continually.

## Helpful Tools And Resources For Designers

### Color Contrast Checker

It’s surprising how many mobile apps don’t pass the AA test. Don’t be one of them! It’s essential to check the accessibility of your color contrast. Use WebAIM’s Color Contrast Checker to test color combinations.

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/db8168c0-e035-468a-bbf5-809475c9e468/mobile-app-design-image59-opt.png" sizes="100vw" caption="WebAIM Color Contrast Checker" alt="WebAIM Color Contrast Checker" >}}

### UI Kits For Adobe XD

A well-designed user interface will make your app shine. It’s great when you can design your UI not from scratch, but using a solid foundation such as a UI kit. [Adobe XD has five UI kits](https://theblog.adobe.com/five-top-ux-designers-five-ui-kits-adobe-xd-now-available-free/) that you can download absolutely for free.These kits will boost your creativity and help you deliver visually interesting UI designs.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3135f86d-2f2b-4f21-8adb-e8514ce7faca/mobile-app-design-image91.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3135f86d-2f2b-4f21-8adb-e8514ce7faca/mobile-app-design-image91.gif" width="800" alt="Navigo Transportation UI Kit" /></a><figcaption>Navigo Transportation UI Kit (Image credit: <a href="https://theblog.adobe.com/five-top-ux-designers-five-ui-kits-adobe-xd-now-available-free/">Adobe</a>)</figcaption></figure>

## Conclusion

A great design is the perfect combination of beauty and functionality, and that is exactly what you should be aiming for when building an app. But don’t try to build a perfect app right on the first attempt. It almost impossible. Instead, treat your app as a continually evolving project, and use data from testing sessions and user feedback to constantly improve the experience.

*This article is part of the UX design series sponsored by Adobe. [Adobe XD is made for a fast and fluid UX design process](https://adobe.ly/2DIoDKh), as it lets you go from idea to prototype faster. Design, prototype, and share &mdash; all in one app. You can check out more inspiring projects created with [Adobe XD on Behance](https://www.behance.net/galleries/adobe/5/XD), and also [sign up for the Adobe experience design newsletter](https://adobe.ly/2yKueO8) to stay updated and informed on the latest trends and insights for UX/UI design.*

{{< signature "ra, al, il" >}}

