---
title: 'Designing Efficient Web Forms: On Structure, Inputs, Labels And Actions'
slug: designing-efficient-web-forms
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f313a929-80e3-4830-ae5d-1d51464e4c0c/designing-more-efficient-forms-500w-opt.png
date: 2017-06-01T17:13:09.000Z
author: nickbabich
description: >-
  Someone who uses your app or website has a particular goal. Often, the one
  thing standing between the user and their goal is a form. Forms remain **one
  of the most important types of interactions** for users on the web and in
  apps.

  In fact, forms are often considered the final step in the journey of
  completing their goals. Forms are just a means to an end. Users should be able
  to complete them quickly and without confusion.
categories:
  - Coding
  - Forms
  - Usability
  - Sponsored Content
---
In this article, you’ll see practical techniques that have been gleaned from [usability testing](https://www.smashingmagazine.com/2013/01/improving-your-website-usability-tests/), field testing, eye-tracking studies and actual complaints from disgruntled users. These techniques — when used correctly — enable designers to produce faster, easier and more productive form experiences. There’s a way you can create and design your own prototypes: All you need to do is to download [Adobe XD](https://adobe.ly/2rVwVsU) (for free) and get started right away. At the end of the article, you’ll also find new ways to design forms.</p>

### <span class="rh">Further Reading</span> on SmashingMag:

*   [Icons As Part Of A Great User Experience](https://www.smashingmagazine.com/2016/10/icons-as-part-of-a-great-user-experience/)
*   [How To Design Error States For Mobile Apps](https://www.smashingmagazine.com/2016/09/how-to-design-error-states-for-mobile-apps/)
*   [An Extensive Guide To Web Form Usability](https://www.smashingmagazine.com/2011/11/extensive-guide-web-form-usability/)
*   [Web Form Design: Showcases And Solutions](https://www.smashingmagazine.com/web-form-design-showcases-and-solutions/)

## The Components Of Forms

The typical form has the following five components:

{{% feature-panel %}}

*   **Structure**  
    This includes the order of fields, the form’s appearance on the page and the logical connections between multiple fields.
*   **Input fields**  
    These include text fields, password fields, checkboxes, radio buttons, sliders and any other fields designed for user input.
*   **Field labels**  
    These tell users what the corresponding input fields mean.
*   **Action button**  
    When the user presses this button, an action is performed (such as submission of the data).
*   **Feedback**  
    The user is made to understand the result of their input through feedback. Most apps and websites use plain text as a form of feedback. A message will notify the user about the result and can be positive (indicating that the form was submitted successfully) or negative (“The number you’ve provided is incorrect”).

Forms may also have the following components:

*   **Assistance**  
    This is any explanation of how to fill out the form.
*   **Validation**  
    This automatic check ensures that the user’s data is valid.

This article covers many aspects related to structure, input fields, labels, action buttons and validation.</p>

## Form Structure

A form is a type of conversation. And like any conversation, it should consist of logical communication between two parties: the user and the app.</p>

### Ask Only What's Required

Make sure to ask only what you really need. Every extra field you add to a form will affect its conversion rate. Always consider why you are requesting certain information from the user and how you will use it.

{{% feature-panel %}}

### Order the Form Logically

Ask details logically from the user's perspective, not from the application or database’s perspective. Typically, asking for someone's address before their name would be unusual.</p>

### Group Related Information

Group related information into logical blocks or sets. The flow from one set of questions to the next will better resemble a conversation. Grouping together related fields will also help users make sense of the information they must fill in. Compare how it works in the contact information form below.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/11a25465-3f60-4a15-8038-f79ea3be523a/1-designing-more-efficient-forms-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/11a25465-3f60-4a15-8038-f79ea3be523a/1-designing-more-efficient-forms-preview-opt.png" width="700" height="589" alt="" /></a><figcaption>Group together related fields (Image: <a href="https://www.nngroup.com/">Nielsen Norman Group</a>)</figcaption></figure>

### One Column Vs. Multiple Columns

One of the problems with arranging form fields into multiple columns is that users will likely interpret the fields inconsistently. If a form has horizontally adjacent fields, then the user must scan in a Z pattern, slowing the speed of comprehension and muddying the path to completion. But if a form is in a single column, the path to completion is a straight line down the page.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/320747db-b9a6-4463-b75a-5bb24586c2a8/2-designing-more-efficient-forms-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/320747db-b9a6-4463-b75a-5bb24586c2a8/2-designing-more-efficient-forms-preview-opt.png" width="800" height="406" alt="" /></a><figcaption>On the left, one of many ways to interpret how the form fields relate when they are arranged in a standard two-column layout, versus on the right, a straight line down the page.
</figcaption></figure>

## Input Fields

Input fields are what enable users to fill in a form. Various types of fields exist for the information you need: text fields, password fields, dropdowns, checkboxes, radio buttons, date-pickers and more.</p>

### Number of Fields

A rule of thumb in form design is that shorter is better. And this certainly seems intuitive: Less effort on the part of the user will lead to higher conversion. Thus, minimize the number of fields as much as possible. This will make your form feel less loaded, especially when you’re requesting a lot of information. However, don't overdo it; no one likes a three-field form that turns into a 30-field interrogation. Displaying only [five to seven input fields](https://en.wikipedia.org/wiki/The_Magical_Number_Seven,_Plus_or_Minus_Two) at a given time is a common practice.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a9cb2311-c1a5-4167-ae89-d0e4a4ce5c2f/3-designing-more-efficient-forms-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5962c850-f58a-4bf1-8a68-9af923d3c24e/3-designing-more-efficient-forms-800w-opt.png" width="800" height="427" alt="" /></a><figcaption>Combine multiple fields in one easy-to-fill field. (Image: <a href="https://www.lukew.com/ff/entry.asp?1950">Luke Wroblewski</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a9cb2311-c1a5-4167-ae89-d0e4a4ce5c2f/3-designing-more-efficient-forms-large-opt.png">View Large version</a>)
</figcaption></figure>

### Mandatory Vs. Optional

Try to avoid optional fields in forms. But if you use them, at least clearly distinguish which input fields may not be left blank. The convention is to use an asterisk (*) for required fields or the word “optional” for non-required fields (which is preferable in long forms with multiple required fields). If you decide to use an asterisk for mandatory fields, show a hint at the bottom of the form explaining what the asterisk is for, because not everyone understands what it means.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9cab6d70-40f2-4d01-834d-f8917645db4b/4-designing-more-efficient-forms-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9cab6d70-40f2-4d01-834d-f8917645db4b/4-designing-more-efficient-forms-preview-opt.png" width="800" height="658" alt="" /></a><figcaption>MailChimp’s mailing-list subscription form.
</figcaption></figure>

### Setting Default Values

Avoid setting defaults unless you believe a large portion of your users (for example, 90% of them) will select that value. Particularly avoid it for required fields. Why? Because you're likely to introduce errors. People scan online forms quickly, so don't assume they will take the time to parse through all of the choices. They might skip something that already has a value.

But this rule doesn't apply to smart defaults — that is, values set based on information available about the user. Smart defaults can make form completion faster and more accurate. For example, preselect the user's country based on geo-location data. Still, use these with caution, because users tend to leave preselected fields as they are.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0ee45a18-50ef-4118-afa1-4edfbc4e494e/5-designing-more-efficient-forms-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0ee45a18-50ef-4118-afa1-4edfbc4e494e/5-designing-more-efficient-forms-preview-opt.png" width="541" height="" alt="" /></a><figcaption>An intelligently preselected country in the checkout form
</figcaption></figure>

### Input Masks

Field masking is a technique that helps users format inputted text. A mask appears once a user focuses on a field, and it formats the text automatically as the field is being filled out, helping users to focus on the required data and to more easily notice errors. In the example below, the parentheses, spaces and dashes are applied automatically as the phone and credit-card numbers are entered. This simple technique saves time and effort with phone numbers, credit cards, currencies and more.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ecf14d97-92a9-4ab0-a18b-1344445b0286/6-designing-more-efficient-forms.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ecf14d97-92a9-4ab0-a18b-1344445b0286/6-designing-more-efficient-forms.gif" width="480" height="" alt="" /></a><figcaption>(Image: <a href="https://www.joshmorony.com/wp-content/uploads/2017/01/input-mask.gif">Josh Morony</a>)
</figcaption></figure>

### Desktop-Only: Make Form Keyboard-Friendly

Users should be able to focus on and edit every field using only the keyboard. Power users, who tend to use the keyboard heavily, should be able to easily tab through and edit fields, all without lifting their fingers off the keyboard. You can find detailed requirements for keyboard interaction in the [W3C’s guidelines on design patterns](https://www.w3.org/TR/wai-aria-practices/#aria_ex).</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c1d6290b-dcf6-4f21-a041-78c33a7233ab/7-designing-more-efficient-forms-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/158ef652-882d-4817-bf87-44db8d9462c8/7-designing-more-efficient-forms-800w-opt.png" width="800" height="326" alt="" /></a><figcaption>Even a simple date-picker should adhere to the W3C’s guidelines. (Image: Salesforce) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c1d6290b-dcf6-4f21-a041-78c33a7233ab/7-designing-more-efficient-forms-large-opt.png">View Large version</a>)
</figcaption></figure>

### Desktop-Only: Autofocus for Input Field

Autofocusing a field gives the user an indication and a starting point to quickly begin filling out a form. Provide a clear visual signal that focus has moved there, whether by changing a color, fading in a box, flashing an arrow, whatever. Amazon’s registration form has both autofocus and visual indicators.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/90b91d49-caf0-4aa7-babb-7650257c631c/8-designing-more-efficient-forms-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f0810c94-5dff-4ce3-bf64-9b858947ec44/8-designing-more-efficient-forms-800w-opt.png" width="800" height="426" alt="" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/90b91d49-caf0-4aa7-babb-7650257c631c/8-designing-more-efficient-forms-large-opt.png">View large version</a>)
</figcaption></figure>

### Mobile-Only: Match Keyboard to Input

Phone users appreciate apps that provide the appropriate keyboard for text being requested. Implement this consistently throughout the app, rather than merely for certain tasks but not others.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f049db67-1c5b-45b6-8e93-79182099ed94/9-designing-more-efficient-forms-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f049db67-1c5b-45b6-8e93-79182099ed94/9-designing-more-efficient-forms-preview-opt.png" width="750" height="" alt="" /></a><figcaption>(Image: <a href="https://www.thinkwithgoogle.com/articles/chapter-5-form-entry.html">Google</a>)
</figcaption></figure>

### Limit Typing (Autocompletion)

With more and more people using mobile screens, anything that can be done to prevent unnecessary typing will improve the user experience and decrease errors. Autocompletion makes it possible to eliminate a huge amount of typing. For example, filling out an address field is often the most problematic part of any registration form. A tool such as [Place Autocomplete Address Form](https://developers.google.com/maps/documentation/javascript/examples/places-autocomplete-addressform) (which uses both geo-location and address prefilling to provide accurate suggestions based on the user's exact location) enables users to enter their address with fewer keystrokes than regular input fields.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c1d57d05-228f-418c-a7d4-a58f24462399/10-designing-more-efficient-forms.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c1d57d05-228f-418c-a7d4-a58f24462399/10-designing-more-efficient-forms.gif" width="490" height="" alt="" /></a></figure>

## Labels

Clearly written labels are one of the primary ways to make a UI more accessible. A good label tells the user the purpose of the field, maintains its usefulness when focus is on the field itself, and remains visible even after the field has been filled in.</p>

### Number of Words

Labels are not help text. Use succinct, short, descriptive labels (a word or two) so that users can quickly scan your form. Previous versions of Amazon’s registration form contained a lot of words, which resulted in slow completion rates. The current version is much better and has short labels.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1091bad2-5ca7-40a2-af59-b93a88495451/amazon-sign-in-comparison-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/91e8e61b-8b03-4a69-b831-3f38e8887828/amazon-sign-in-comparison-800w-opt.png" width="800" height="526" alt="" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1091bad2-5ca7-40a2-af59-b93a88495451/amazon-sign-in-comparison-large-opt.png">View large version</a>)
</figcaption></figure>

### Sentence Case Vs. Title Case

In most digital products today, there are two ways to capitalize words:

*   title case: capitalize every word. “This Is Title Case.”
*   sentence case: capitalize the first word. “This is sentence case.”

Sentence case used for labels has one advantage over title case: It is slightly easier (and, thus, faster) to read. While the difference for short labels is negligible (“Full Name” and “Full name”), for longer labels, sentence case is better. Now You Know How Difficult It Is to Read Long Text in Title Case.</p>

### Avoid All Caps

Never use all caps, or else the form will be difficult to read and much harder to scan quickly, because there will be no variation in character height.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/38667abd-6b40-4a43-a8c3-66da979fce0e/12-designing-more-efficient-forms-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/38667abd-6b40-4a43-a8c3-66da979fce0e/12-designing-more-efficient-forms-preview-opt.png" width="491" height="" alt="" /></a><figcaption>All-caps labels are very hard to read.
</figcaption></figure>

### Alignment of Labels: Left Vs. Right Vs. Top

Matteo Penzo's 2006 [article on label placement](https://www.uxmatters.com/mt/archives/2006/07/label-placement-in-forms.php) suggests that forms are completed faster if labels are on top of the fields. Top-aligned labels are good if you want users to scan the form as quickly as possible.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/37856bc3-f458-489f-a330-e1763d542ca0/13-designing-more-efficient-forms-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/56cb2c8f-75a6-4711-847c-25b703dbfeac/13-designing-more-efficient-forms-800w-opt.png" width="800" height="221" alt="" /></a><figcaption>Left-aligned, right-aligned and top-aligned labels (Image: UX Matters) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/37856bc3-f458-489f-a330-e1763d542ca0/13-designing-more-efficient-forms-large-opt.png">View Large version</a>)
</figcaption></figure>

The biggest advantage of **top-aligned labels** is that different-sized labels and localized versions can more easily fit the UI. (This is especially good for screens with limited space.)

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/37dfb3a3-5ef0-4df7-ad4f-8092dfbfa5a1/16-designing-more-efficient-forms-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/37dfb3a3-5ef0-4df7-ad4f-8092dfbfa5a1/16-designing-more-efficient-forms-preview-opt.png" width="526" height="" alt="" /></a><figcaption>(Image: <a href="https://css-tricks.com/label-placement-on-forms/">CSS-Tricks</a>)</figcaption></figure>

The biggest disadvantage to **left-aligned labels** is that it has the slowest completion times. This is likely because of the visual distance between the label and input field. The shorter the label, the further away it will be from the input. However, a slow completion rate isn't always a bad thing, especially if the form asks for sensitive data. If you are asking for something like a driver's license number or a social security number, you might deliberately want to slow down users a bit to make sure they enter it correctly. Thus, the time spent reading labels for sensitive data is insignificant. Left-aligned labels have another disadvantage: They require more horizontal space, which might be a problem for mobile users.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1764fa05-7404-4b78-899e-2ef0ab0cd5d8/14-designing-more-efficient-forms-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1764fa05-7404-4b78-899e-2ef0ab0cd5d8/14-designing-more-efficient-forms-preview-opt.png" width="529" height="" alt="" /></a><figcaption>(Image: <a href="https://css-tricks.com/label-placement-on-forms/">CSS-Tricks</a>)</figcaption></figure>

The big advantage of **right-aligned labels** is the strong visual connection between the label and input. Items near each other appear to be related. This principle isn't new; it derives from the [law of proximity](https://en.wikipedia.org/wiki/Principles_of_grouping), from Gestalt psychology. For short forms, right-aligned labels can have great completion times. The disadvantage is discomfort; such forms lack that hard left edge, which makes it less comfortable to look at and harder to read.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4cfc3cc0-efba-4411-9b1f-affa02aab55d/15-designing-more-efficient-forms-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4cfc3cc0-efba-4411-9b1f-affa02aab55d/15-designing-more-efficient-forms-preview-opt.png" width="570" height="" alt="" /></a><figcaption>(Image: <a href="https://css-tricks.com/label-placement-on-forms/">CSS-Tricks</a>)</figcaption></figure>

**Takeaway:** If you want users to scan a form quickly, put labels above the fields. The layout will be easier to scan because the eye will move straight down the page. However, if you want users to read carefully, put labels to the left of the fields. This layout will slow down the reader and make them scan in a Z-shaped motion.</p>

### Inline Labels (Placeholder Text)

A label set as a placeholder in an input field will disappear once the field gains focus; the user will no longer be able to view it. While placeholder text might work for two-field forms (a simple log-in form with username and password fields), it's a poor substitute for visual labels when more information is required from the user.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8c689b96-fba0-4004-8e9a-b0633b9005ec/17-designing-more-efficient-forms.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8c689b96-fba0-4004-8e9a-b0633b9005ec/17-designing-more-efficient-forms.gif" width="400" height="" alt="" /></a><figcaption>(Image: <a href="https://www.snapwi.re/">snapwi</a>)</figcaption></figure>

Once the user clicks on the input field, the label will disappear, and so the user cannot double-check that they wrote what was being asked of them. This increases the chance of error. Another problem is that users could mistake placeholder text for prefilled data and, hence, ignore it (as [Nielsen Norman Group’s eye-tracking study](https://www.nngroup.com/articles/form-design-placeholders/) confirms).</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/41cfed37-2a6b-4da8-a784-f301995c2782/18-designing-more-efficient-forms-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/41cfed37-2a6b-4da8-a784-f301995c2782/18-designing-more-efficient-forms-preview-opt.png" width="529" height="" alt="" /></a><figcaption>Placeholder text as field label
</figcaption></figure>

A good solution for placeholder text is a floating label. The placeholder text would be shown by default, but once an input field is tapped and text is entered, the placeholder text fades out and a top-aligned label animates in.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ec360907-1454-4666-9a33-6a34ade70b7c/19-designing-more-efficient-forms.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ec360907-1454-4666-9a33-6a34ade70b7c/19-designing-more-efficient-forms.gif" width="800" height="600" alt="" /></a><figcaption>(Image: <a href="https://dribbble.com/mds">MDS</a>)</figcaption></figure>

**Takeaway:** Don't just rely on placeholders; include a label as well, because once a field has been filled out, the placeholder will no longer be visible. Use a floating label so that users are sure they’ve filled out the correct field.</p>

## Action Buttons

When clicked, an action [button](https://www.smashingmagazine.com/2016/11/a-quick-guide-for-designing-better-buttons/) triggers some activity, such as submission of the form.</p>

### Primary Vs. Secondary Actions

A lack of visual distinction between primary and secondary actions can easily lead to failure. Reducing the visual prominence of secondary actions minimizes the risk of error and reinforces people’s path to a successful outcome.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9d7baee8-b8b2-48b4-8842-cc7994324877/20-designing-more-efficient-forms-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9d7baee8-b8b2-48b4-8842-cc7994324877/20-designing-more-efficient-forms-preview-opt.png" width="450" height="" alt="" /></a><figcaption>Equal visual weight versus visual distinction (Image: Luke Wroblewski)
</figcaption></figure>

### Button Location

Complex forms usually need a back button. If such a button is located right below an input field (like in the first screenshot below), a user could accidentally click it. Because a back button is a secondary action, make it less accessible (the second form below has the right location for buttons).</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a1e0c5dd-a99c-43b2-bf8c-b6f8ae568544/21-designing-more-efficient-forms-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6f0108eb-e77f-44d4-baa8-07eee10885e6/21-designing-more-efficient-forms-800w-opt.png" width="800" height="296" alt="" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a1e0c5dd-a99c-43b2-bf8c-b6f8ae568544/21-designing-more-efficient-forms-large-opt.png">View large version</a>)</figcaption></figure>

### Naming Conventions

Avoid generic words such as “Submit” for actions, because they give the impression that the form itself is generic. Instead, state what action the button will perform when clicked, such as “Create my account” or “Subscribe to weekly offers.”

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/48cbbb5b-ac4d-4719-8273-065b05dc2ca1/22-designing-more-efficient-forms-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8e5e500f-a261-4b05-b5bf-e13eaf619a9a/22-designing-more-efficient-forms-800w-opt.png" width="780" height="" alt="" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/48cbbb5b-ac4d-4719-8273-065b05dc2ca1/22-designing-more-efficient-forms-large-opt.png">View large version</a>)</figcaption></figure>

### Multiple Action Buttons

Avoid multiple action buttons because they might distract users from their goal of submitting the form.</p>

### The Reset Button Is Pure Evil

Don't use a reset button. This button almost never helps users and often hurts them. The web would be a happier place if almost all reset buttons were removed.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/616aa4f7-c9ce-40d3-a595-d63b097f3f40/23-designing-more-efficient-forms-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/616aa4f7-c9ce-40d3-a595-d63b097f3f40/23-designing-more-efficient-forms-preview-opt.png" width="547" height="" alt="" /></a></figure>

### Visual Appearance

Make sure action buttons look like buttons: Indicate that it is possible to click or tap them.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ef37bce4-85c8-4746-a3fc-5102ebb07631/24-designing-more-efficient-forms.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ef37bce4-85c8-4746-a3fc-5102ebb07631/24-designing-more-efficient-forms.gif" width="800" height="600" alt="" /></a><figcaption>Shading indicates that it is possible to click. (Image: <a href="https://dribbble.com/shots/1898320-Material-Design-Button">Vadim Gromov</a>)</figcaption></figure>

### Visual Feedback

Design the “Submit” button in a way that clearly indicates the form is being processed after the user's action. This provides feedback to the user while preventing double submission.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4bd5d289-878f-438c-a8b2-ecca7af5c3d9/25-designing-more-efficient-forms.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4bd5d289-878f-438c-a8b2-ecca7af5c3d9/25-designing-more-efficient-forms.gif" width="800" height="517" alt="" /></a><figcaption>(Image: <a href="https://medium.com/@michaelvillar?source=post_header_lockup">Michaël Villar</a>)</figcaption></figure>

## Validation

Form validation errors are inevitable and are a natural part of data entry (because users are prone to making errors). Yes, error-prone conditions should be minimized, but validation errors will never be eliminated. So, the most important question is, How do you make it easy for the user to recover from errors?

### Inline Validation

Users dislike having to go through the process of filling out a form, only to find out upon submission that they've made an error. Especially frustrating is completing a long form and upon pressing “Submit,” you are rewarded with multiple error messages. It's even more annoying when it isn't clear what errors you've committed and where.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d85b07af-f4a7-4167-adb0-4f4e8784a880/26-designing-more-efficient-forms-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d85b07af-f4a7-4167-adb0-4f4e8784a880/26-designing-more-efficient-forms-preview-opt.png" width="750" height="" alt="" /></a><figcaption>(Image: <a href="https://ux.stackexchange.com/questions/33108/how-to-best-show-connectivity">Stack Exchange</a>)</figcaption></figure>

Validation should inform users about the correctness of text **as soon as the user has inputted the data**. The primary principle of good form validation is this: Talk to the user! Tell them what is wrong! Real-time inline validation immediately informs the user about the correctness of their data. This approach allows them to correct any errors faster, without having to wait until they press the “Submit” button to see the errors.

However, avoid validating on each keystroke because, in most cases, you simply cannot verify until someone has finished typing an answer. Forms that validate during data entry punish the user as soon as they start entering data.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/19755592-b6aa-40c9-afbb-ec57309c5ff1/27-designing-more-efficient-forms.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/19755592-b6aa-40c9-afbb-ec57309c5ff1/27-designing-more-efficient-forms.gif" width="676" height="" alt="" /></a><figcaption>Google Forms states the email address isn't valid before you've finished typing. (Image: <a href="https://medium.com/wdstack/inline-validation-in-forms-designing-the-experience-123fb34088ce#.fl86493cl">Medium</a>)</figcaption></figure>

On the other hand, forms that validate after data entry do not inform the user soon enough that they’ve fixed an error.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/46d20e24-0374-4a82-a29e-9a9c615162a4/28-designing-more-efficient-forms.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/46d20e24-0374-4a82-a29e-9a9c615162a4/28-designing-more-efficient-forms.gif" width="800" height="502" alt="" /></a><figcaption>Validation in the Apple Store is performed after data entry. (Image: <a href="https://medium.com/wdstack/inline-validation-in-forms-designing-the-experience-123fb34088ce#.fl86493cl">Medium</a>)
</figcaption></figure>

Mihael Konjević, in his article “[Inline Validation in Forms: Designing the Experience](https://medium.com/wdstack/inline-validation-in-forms-designing-the-experience-123fb34088ce#.fl86493cl),” examines different validation strategies and proposes a hybrid strategy to satisfy both sides: **Reward early, punish late**.

*   If the user enters data in a field that was in a valid state (i.e. previously inputted data was valid), then validate after data entry.
*   If the user enters data in a field that was in an invalid state (i.e. previously entered data was invalid), then validate during data entry.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ee520d67-1f0f-40dd-a7b7-970e0ab66c17/29-designing-more-efficient-forms.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ee520d67-1f0f-40dd-a7b7-970e0ab66c17/29-designing-more-efficient-forms.gif" width="788" height="" alt="" /></a><figcaption>A hybrid approach: Reward early, punish late. (Image: <a href="https://medium.com/wdstack/inline-validation-in-forms-designing-the-experience-123fb34088ce#.fl86493cl">Medium</a>)
</figcaption></figure>

## Protecting Data

Jef Raskin once said, “The system should treat all user input as sacred.” This is absolutely true for forms. It's great when you start filling in a form and then accidentally refresh the page but the data remains in the fields. Tools like [Garlic.js](https://garlicjs.org) help you to persist a form’s values locally until the form is submitted. This way, users won't lose any precious data if they accidentally close the tab or browser.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c6e4fc5c-073f-402d-8141-a5e68e72b67f/30-designing-more-efficient-forms.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c6e4fc5c-073f-402d-8141-a5e68e72b67f/30-designing-more-efficient-forms.gif" width="800" height="" alt="" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0703e67c-17d5-47a1-ba28-f784d8f5b35c/image05.gif">View large version</a>)</figcaption></figure>

## Conversational Interfaces: New Ways Of Designing Forms

Recently, we’ve seen a lot of excitement around conversational interfaces and [chatbots](https://www.smashingmagazine.com/2016/12/conversational-design-essentials-tips-for-building-a-chatbot/). Several trends are contributing to this phenomenon, but one in particular is that people are [spending more time in messaging apps](https://www.businessinsider.com/the-messaging-app-report-2015-11) than on social networks. This has led to a lot of experimentation with supporting a range of interactions, such as shopping, in threaded conversations, often in a way that mimics messaging. Even as established an element as a web form has undergone a change under this trend. Designers are looking to transform traditional web forms into interactive conversational interfaces.</p>

### Natural Language Interface

**Every interface is a conversation.** Traditional forms (the ones we design every day) are quite similar to a conversation. The only difference is the way we ask the questions. But what if we designed our forms to ask questions in a format that more closely reflects real human (not machine) conversation? So, instead of communicating with a machine on its own inhuman terms, you would interact with it on yours. The form shown below creates a conversational context, facilitating understanding without relying on the traditional elements of web forms (such as labels and input fields).</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4998de9d-c8e6-493d-a741-fdef72ffa629/31-designing-more-efficient-forms.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2447f2af-ad48-42a0-b69e-95481051465a/31-designing-more-efficient-forms-780w.gif" width="780" height="370" alt="" /></a><figcaption>This <a href="https://tympanus.net/Tutorials/NaturalLanguageForm">form design from Codrops</a> uses a conversational pattern to better resemble the task. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4998de9d-c8e6-493d-a741-fdef72ffa629/31-designing-more-efficient-forms.gif">View large version</a>)
</figcaption></figure>

### Conversational Form

[Conversational Form](https://github.com/space10-community/conversational-form) is an open-source concept that easily turns any form on a web page into a conversational interface. It features conversational replacement of all input elements, reusable variables from previous questions, and complete customization and control over the styling. This project represents an interesting shift in how we think about user experiences and interactions, leaning more towards text-based conversation to help users achieve their goals.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/112684ea-279b-4a2e-be69-0a567d941c8c/32-designing-more-efficient-forms.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/112684ea-279b-4a2e-be69-0a567d941c8c/32-designing-more-efficient-forms.gif" width="574" height="" alt="" /></a></figure>

## Conclusion

Users can be reluctant to fill out forms, so make the process as easy as possible. Minor changes — such as grouping related fields and indicating what information goes in each field — can significantly increase usability. Usability testing is simply indispensable in form design. Very often, testing with just a few people or simply asking a colleague to go through a prototype can give you good insight into how usable a form is.</p>

<blockquote>This article is part of the UX design series sponsored by Adobe. The newly introduced Adobe Experience Design CC (Beta) tool is made for a <a href="https://adobe.ly/2rVwVsU">fast and fluid UX design process</a>, as it lets you go from idea to prototype faster. Design, prototype and share — all in one app.
You can check out more inspiring projects created with Adobe XD on <a href="https://www.behance.net/galleries/adobe/5/Experience-Design">Behance</a>, and also visit the <a href="https://adobe.ly/2rOmEi0">Adobe XD blog</a> to stay updated and informed. Adobe XD is being updated with new features frequently, and since it’s in public Beta, you can <a href="https://adobe.ly/2rVwVsU">download and test it for free</a>.</blockquote>

{{< signature "ms, vf, al, yk, il" >}}

