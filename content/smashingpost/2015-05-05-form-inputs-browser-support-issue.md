---
title: 'Form Inputs: The Browser Support Issue You Didn’t Know You Had'
slug: form-inputs-browser-support-issue
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b5be72bc-a826-4c41-90ea-5fe31cbce064/zahlen-illu-opt.png
date: 2015-05-05T21:13:38.000Z
author: aaronladage
description: >-
  The lowly form input. It’s been a part of HTML for as long as HTML has had a
  formal specification; but before
  [HTML5](https://www.smashingmagazine.com/2013/01/18/the-importance-of-sections/),
  developers were hamstrung by its limited types and attributes. As the use of
  smartphones and their on-screen keyboards has flourished, however, inputs have
  taken on a new and incredibly important role — but they’re also riddled with
  browser and device inconsistencies. The eight original input types were
  brilliant in their simplicity. (Well, OK, maybe `<input type="image">` hasn’t
  aged very well.)

  Think about it: by inserting a single element in your markup, you can tell any
  web browser to
  [render](https://www.smashingmagazine.com/2015/01/26/inside-microsofts-new-rendering-engine-project-spartan/)
  an interaction control, and you can completely modify that interaction – from
  a text field to a checkbox to a radio button – by simply changing a keyword.
  Now imagine a world where creating these interactions means also creating
  custom interaction controls, and you begin to realize how taken for granted
  inputs really are.
categories:
  - Coding
  - Forms
  - Browsers
---
The lowly form input. It’s been a part of HTML for as long as HTML has had a <a href="https://www.w3.org/MarkUp/html-spec/">formal specification</a>; but before HTML5, developers were hamstrung by its limited types and attributes. As the use of smartphones and their on-screen keyboards has flourished, however, inputs have taken on a new and incredibly important role — but they’re also riddled with browser and device inconsistencies.

The eight original input types were brilliant in their simplicity. (Well, OK, maybe <code>&lt;input type="image"&gt;</code> hasn’t aged very well.)

## <span class="rh">Further Reading</span> on SmashingMag:

*   [The Problem Of CSS Form Elements](https://www.smashingmagazine.com/2013/02/css-form-elements-problem/)
*   [Auto-Save User’s Input In Your Forms](https://www.smashingmagazine.com/2011/12/sisyphus-js-client-side-drafts-and-more/)
*   [How I Ended Up With Element Queries](https://www.smashingmagazine.com/2016/07/how-i-ended-up-with-element-queries-and-how-you-can-use-them-today/)
*   [Forms On Mobile Devices: Modern Solutions](https://www.smashingmagazine.com/2010/03/forms-on-mobile-devices-modern-solutions/)

Think about it: By inserting a single element in your markup, you can tell any web browser to render an interaction control, and you can completely modify that interaction – from a text field to a checkbox to a radio button – by simply changing a keyword. Now imagine a world where creating these interactions means also creating custom interaction controls, and you begin to realize how taken for granted inputs really are.

{{% feature-panel %}}

Unfortunately, even Tim Berners-Lee and Co. couldn’t have anticipated the strain that mobile devices and interaction-hungry web applications would place on these original concepts for user input.

That’s what the HTML 5.0 specification was intended to solve, by expanding the concept of the text input to allow for specific data types, such as numbers and email addresses, as well as rich interactions, such as task-specific on-screen keyboards and date- and color-pickers. Most were designed with graceful degradation at their core, adding enhancements to supported browsers while falling back nicely to basic text inputs in older ones.

Or at least that was the intention. In the real world, many of these new inputs and attributes — even seemingly innocuous types like <code>&lt;input type="number"&gt;</code> — don’t always behave as you might expect.</p>

## Identifying The Problem

While not as fierce as battles of yore, input types are the cause of a new small-scale browser war. Despite the existence of standards, browser and device manufacturers have cherry-picked input feature support and taken different approaches to implementing these enhanced interactions.

Take <code>date</code>. Using <code>&lt;input type="date"&gt;</code> is a godsend to any front-end developer who has ever had to add a JavaScript-based date-picker to a website… or at least it would be if all browsers supported it. Desktop versions of Chrome and most mobile browsers display a native date-picker:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/44e00ef9-f3df-4ed4-af23-d5ec678d671b/01-date-input-example-opt-small.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/44e00ef9-f3df-4ed4-af23-d5ec678d671b/01-date-input-example-opt-small.jpg" alt="Native date-pickers shown when using the date input type in Chrome for iOS and Mac" /></a><figcaption>Native date-pickers shown when using the <code>date</code> input type in Chrome for iOS and Mac (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/44e00ef9-f3df-4ed4-af23-d5ec678d671b/01-date-input-example-opt-small.jpg">View large version</a>)</figcaption></figure>

However, as of Firefox 36 and Internet Explorer (IE) 11, that same input type defaults to a plain ol’ text field, forcing developers to use <a href="https://chemerisuk.github.io/better-dateinput-polyfill/">polyfills</a> or to continue building JavaScript-based date-picker solutions instead.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/21622b9c-e0fd-48fd-a7a6-bf58569338c1/02-date-firefox-example-opt-small.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/21622b9c-e0fd-48fd-a7a6-bf58569338c1/02-date-firefox-example-opt-small.jpg" alt="The date input type defaults to a plain text field in Firefox 36." /></a><figcaption>The <code>date</code> input type defaults to a plain text field in Firefox 36. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/21622b9c-e0fd-48fd-a7a6-bf58569338c1/02-date-firefox-example-opt-small.jpg">View large version</a>)</figcaption></figure>

The lack of date input support in Firefox seems at odds with the vendor’s overall support for these more visually and functionally advanced input types. For example, the <code>range</code> input type (<code>&lt;input type="range"&gt;</code>), which emerged from the same crop of proposed features as <code>date</code>, has been supported since <a href="https://html.spec.whatwg.org/#range-state-(type=range)">Firefox 23 and IE 10</a>.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/55d9c4bc-ea4d-491f-9237-e623465d0b64/02a-range-firefox-example-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/32510e72-3dc9-42c7-86b7-02cda6af2c49/02a-range-firefox-example-opt-small.jpg" alt="Firefox has supported the range input type since version 23." /></a><figcaption>Firefox has supported the <code>range</code> input type since version 23. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/55d9c4bc-ea4d-491f-9237-e623465d0b64/02a-range-firefox-example-opt.jpg">View large version</a>)</figcaption></figure>

In fact, IE’s implementation, although not the most visually attractive, has some added utility, allowing you to see incremental divisions within the range, as well as its current numeric value on mouse drag.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6531cc6a-28b2-433b-b98e-df3555754654/02b-range-ie-example-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f9b8051b-38fb-4dfc-9918-6e3405b8a48c/02b-range-ie-example-opt-small.jpg" alt="Internet Explorer 10+’s implementation of the range input type shows incremental divisions and its current numeric value on mouse drag." /></a><figcaption>IE 10+’s implementation of the <code>range</code> input type shows incremental divisions and its current numeric value on mouse drag. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6531cc6a-28b2-433b-b98e-df3555754654/02b-range-ie-example-opt.jpg">View large version</a>)</figcaption></figure>

We’re used to dealing with mixed browser support for emerging features. But when it comes to inputs, there’s a bigger problem: Even when an input feature is supported, it’s not always implemented in the same way across browsers or mobile platforms. Developers now have to take all of the following aspects of an input into account:

*   **type**.  Does the input’s type reflect the data that’s being entered (for semantic and validation purposes), and does it also trigger the correct keyboard in Android?
*   **validation pattern**.  Does your pattern allow for the correct characters to be entered, and does it also trigger the correct keyboard in iOS?
*   **`step` attribute** In certain browsers, do the small up and down arrows associated with a number input allow the user to increment or decrement their input in the correct steps?
*   **`required` attribute** If an input is required, do its `type`, `pattern` and `step` values all contribute to the format you’re expecting, and is this true across all browsers on mobile and desktop?

Imagine a situation in which you need to add a required input field for currency, and you want to display the best possible keyboard experience across all devices. “Simple,” you think, adding <code>&lt;input type="number" required&gt;</code> to your form. This works great for Android:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8a0ad8eb-4ff9-46de-9d2b-68ce5b8b32bc/03-number-nopattern-android-example-opt-small.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8a0ad8eb-4ff9-46de-9d2b-68ce5b8b32bc/03-number-nopattern-android-example-opt-small.jpg" alt="An appropriate keyboard is displayed to Android users for the numberinput type." /></a><figcaption>An appropriate keyboard is displayed to Android users for the <code>number</code> input type. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8a0ad8eb-4ff9-46de-9d2b-68ce5b8b32bc/03-number-nopattern-android-example-opt-small.jpg">View large version</a>)</figcaption></figure>

In iOS, your keyboard would be improved (the top row will show numbers):

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/604be8ef-b813-4fc2-955a-f1b686ff79e6/04-number-nopattern-ios-example-opt-small.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/604be8ef-b813-4fc2-955a-f1b686ff79e6/04-number-nopattern-ios-example-opt-small.jpg" alt="In iOS, the keyboard displayed in response to the number input type contains the number keys." /></a><figcaption>In iOS, the keyboard displayed in response to the <code>number</code> input type contains the number keys. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/604be8ef-b813-4fc2-955a-f1b686ff79e6/04-number-nopattern-ios-example-opt-small.jpg">View large version</a>)</figcaption></figure>

But that’s still not the fancy 10-key keyboard Android gives you. To achieve something similar in iOS, you need to set a <code>pattern</code> attribute with a value of <code>[0-9]*</code>:

<pre><code class="language-markup">
&lt;input type="number" pattern="[0-9]*" required&gt;
</code></pre>

In iOS, this combination gives us this:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/58274a75-7e49-4a4f-836c-65631abe1d61/05-number-pattern-ios-example-opt-small.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/58274a75-7e49-4a4f-836c-65631abe1d61/05-number-pattern-ios-example-opt-small.jpg" alt="Setting the pattern attribute to [0-9]* prompts iOS to display a number pad." /></a><figcaption>Setting the <code>pattern</code> attribute to <code>[0-9]*</code> prompts iOS to display a number pad. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/58274a75-7e49-4a4f-836c-65631abe1d61/05-number-pattern-ios-example-opt-small.jpg">View large version</a>)</figcaption></figure>

I believe this implementation to be a fundamentally shortsighted decision on Apple’s part. Not only does it ignore the input’s type altogether, it’s also based on a pattern that’s hardcoded into the OS, which means that if you alter that pattern in any way, you will lose the keyboard enhancement entirely in iOS.

In our currency example, this creates a problem, but not where you might expect. A required input with a <code>number</code> type and a <code>pattern</code> of <code>[0-9]*</code> will give us great results across mobile, but it’s easy to forget that these decisions also affect desktop browsers. On desktop, we can’t control the user’s keyboard, and if they enter a special character (such as a comma or dollar sign, which are both plausible for currency), both the type and the pattern will cause it to fail client-side validation. (In older versions of Chrome, decimals also cause validation errors, although adding <code>step="any"</code> solves this issue.) You can see the problem here:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b71053da-864e-406e-8df3-b065cb039b44/06-number-pattern-desktop-example-opt-small.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b71053da-864e-406e-8df3-b065cb039b44/06-number-pattern-desktop-example-opt-small.jpg" alt="06-number-pattern-desktop-example-opt-small" /></a><figcaption>Characters that don’t match the specified pattern will throw errors in desktop browsers, where keyboards cannot be controlled. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b71053da-864e-406e-8df3-b065cb039b44/06-number-pattern-desktop-example-opt-small.jpg">View large version</a>)</figcaption></figure>

This leaves developers in a bit of a lurch. We can choose to enhance one mobile OS experience at the expense of the other, enhance both of our mobile experiences at the expense of desktop, or enhance our desktop experience at the expense of mobile. And none of these options would make our stakeholders very happy.

## Zip It Up

Although currency is one of the most illustrative examples, almost any input that needs to allow for alphanumeric content with special characters can cause some of the heartburn that comes with using these new input types and patterns. This includes social security numbers, phone numbers or any number that could be entered in an unknown format, such as a bank account number. For this next example, let’s examine one that’s often overlooked: US ZIP codes.

Without giving them much thought, ZIP codes seem relatively simple: most people immediately think of them as a five-digit number. So, we can just use <code>&lt;input type="number"&gt;</code>, right? Wrong, for two reasons.

The more obvious reason is the extended US ZIP code format (i.e. 12345-6789). Although it may be less common, allowing our users to enter it this way is still important. And we also need to keep non-US users in mind, because several countries (including Canada and the UK) use letters and other special symbols in their postal code formats. Semantically, ZIP codes aren’t numbers: They’re numerical codes — you’d never refer to a certain ’90s teen television drama as “Beverly Hills Ninety Thousand Two Hundred Ten.”

The second reason is a little subtler: some ZIP codes on the far east coast of the US begin with a zero.

If you’re validating these fields, special characters will immediately cause a validation issue, and in many browsers (including old versions of Chrome), so will that leading zero. That means not being able to use a <code>number</code> input type and, therefore, no enhanced keyboard for Android.

Android users may be out of luck, but can we still enhance for iOS? If you want to validate the field, the answer again is no, caused in large part by Apple’s decision to base its enhanced keyboard on a single hardcoded validation pattern. If we want to use <code>&lt;input type="text" pattern="[0-9]*"&gt;</code> (the hardcoded pattern that triggers iOS’s 10-key keypad), our users won’t be able to enter special characters or letters. Even if you disregard non-US users and use a pattern that allows for extended ZIP codes, such as <code>&lt;input type="text" pattern="(\d{5}([\-]\d{4})?)"&gt;</code>, you’re still not going to get back that enhanced iOS experience that would benefit users.

These currency and postal code examples also don’t take into account support for other attributes that can be slapped on form inputs, such as <code>autocapitalize</code>, <code>autocomplete</code> and <code>autocorrect</code>. <code>Autocapitalize</code> and <code>autocorrect</code> are features created by Apple that work in iOS and Safari but aren’t officially part of the HTML specification and will fail W3C validation. <code>Autocomplete</code>, on the other hand, is part of the official specification, but as of version 34, <a href="https://webscripts.softpedia.com/blog/Chrome-34-Seeks-to-Save-All-Your-Passwords-436693.shtml">Chrome ignores and overrides this attribute by default</a> to support its built-in form autofill functionality.

It probably goes without saying, but also very little can be done to support users who install third-party keyboards on their devices. After all, if your user’s on-screen keyboard looks like <a href="https://gizmodo.com/12-smartphone-keyboards-that-are-trying-to-reinvent-mob-1695151919">two video-game joysticks or a rotary telephone</a>, then you will very likely be unable to reliably control how it responds to advanced input types and attributes.</p>

## Send In The Hacks

As with most standards issues, there are workarounds, and there are problems with the workarounds. The one I’ve seen advocated most frequently for dealing with numbers and currency is the use of <code>&lt;input type="tel"&gt;</code>, which creates the closest thing we’ve got to a cross-platform 10-key keyboard solution:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6b100fc3-d838-458f-8894-ea5a5c6b3ff0/07-tel-nopattern-iosandroid-example-opt-small.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6b100fc3-d838-458f-8894-ea5a5c6b3ff0/07-tel-nopattern-iosandroid-example-opt-small.jpg" alt="Setting an input’s type to tel will display a 10-key keypad on both iOS and Android." /></a><figcaption>Setting an input’s type to <code>tel</code> will display a 10-key keypad on both iOS and Android. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6b100fc3-d838-458f-8894-ea5a5c6b3ff0/07-tel-nopattern-iosandroid-example-opt-small.jpg">View large version</a>)</figcaption></figure>

This does produce a 10-key keypad on Android and iOS, without enforcing a pattern on desktop. But as you can see by this keyboard’s secondary screen, it’s also clearly not a best practice:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1a25e71f-c5bb-4d42-8f84-ad2b12b78542/08-tel2-nopattern-iosandroid-example-opt-small.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1a25e71f-c5bb-4d42-8f84-ad2b12b78542/08-tel2-nopattern-iosandroid-example-opt-small.jpg" alt="Unfortunately, the tel input type’s secondary keyboard is telephone-specific." width="500" height="443" /></a><figcaption>Unfortunately, the <code>tel</code> input type’s secondary keyboard is telephone-specific. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1a25e71f-c5bb-4d42-8f84-ad2b12b78542/08-tel2-nopattern-iosandroid-example-opt-small.jpg">View large version</a>)</figcaption></figure>

Do we really want to present users with a phone keypad that includes keys for “pause” and “wait” when they aren’t actually entering a phone number? And what happens to our websites if mobile platforms and browsers change the way telephone inputs are handled?

The second most common solution I’ve seen is to <a href="https://www.google.com/url?q=http%3A%2F%2Fcodepen.io%2Faladage%2Fpen%2FyyRyXw&amp;sa=D&amp;sntz=1&amp;usg=AFQjCNEsQeFSoaqKI7-sOMnjsPyrv6ZdEQ">use JavaScript to strip special characters from inputs</a> as our users enter content into them. This will get the job done, but it’s arguably not a good user experience. Users might be confused when the text they enter doesn’t appear on screen, or appears momentarily and then disappears.</p>

### Common Sense And Communication Are Key

Both of these solutions hark back to the days of using <a href="https://browserhacks.com/">star and underscore CSS hacks</a> to sidestep odd behaviors in old browsers (especially IE 6) — and we shouldn’t go there again. These hacks are a conscious decision to sidestep standards and best practices to complete the task at hand, without giving much thought to what will happen to our code base as browser support matures and feature implementations evolve.

Another solution may be on the horizon in the form of the WHATWG’s proposed <a href="https://html.spec.whatwg.org/multipage/forms.html#input-modalities:-the-inputmode-attribute"><code>inputmode</code> attribute</a>. By using this attribute, developers could declare a specific state that hints at which input mechanism would be most helpful, with a predefined fallback state. For example, <code>&lt;input inputmode="tel"&gt;</code> would fall back to a <code>numeric</code> state if a device’s keyboard doesn’t support telephone input, and <code>&lt;input inputmode="numeric"&gt;</code> would display a number keyboard but also allow for negative numbers and a thousands separator. Unfortunately, support for this proposed attribute is still <a href="https://www.wufoo.com/html5/attributes/23-inputmode.html">extremely limited</a>, and just like input types and patterns, we’ll have to wait and see if it’s implemented consistently across all browsers and devices.

For now, adhere to each input type’s intended purpose if you want to future-proof as much as possible. Assume that the rules for what triggers specific keyboards and behaviors on all platforms and browsers can — and will — change.

If you do use these newfangled input types and patterns, then test, test and test again, on as many devices as you can get your hands on. I created <a href="https://inputtypes.com">Input Type Sandbox</a>, a utility for trying out different combinations of types, patterns and attributes, for exactly this purpose.

Not shying away from discussing this up front with stakeholders is also important. It’s willful ignorance to think they’ve never used an enhanced keyboard on their mobile device and that they wouldn’t want the same experience on their own website. I can say from personal experience that if your website’s forms are lengthy, you’ll save hours of explanation and rework if stakeholders are made aware of the possibilities and limitations of form inputs from the beginning.</p>

## A Call To Action For Platforms And Browsers

The real issue here has nothing to do with the wonderful new abilities that HTML5 inputs give to us developers; the patchwork of support and implementation are the problem.

The only true solution is for all browser vendors and device manufacturers to operate from the same playbook. Specifically, we need to demand the following:

1.  Browser vendors need to support all standards-based input types as soon as possible. A powerful new feature on one platform isn’t truly powerful until it’s commonplace enough for us to confidently use in the real world.
2.  All mobile platforms should follow the same rules for what invokes a particular on-screen keyboard. Personally, I think Android has the right idea in using `type` and not the validation pattern, as iOS does. But what matters is not the method, but consistency.
3.  Client-side validation needs to work consistently across all browsers and platforms, and soon.

Tracking every browser vendor and device manufacturer’s plans for supporting this patchwork of types and patterns is tricky, although we can glean some information from their bug-tracking and support websites. For example, Microsoft says <code>&lt;input type="date"&gt;</code> <a href="https://status.modern.ie/daterelatedinputtypes?term=date%20related">will be supported</a> in its upcoming Spartan browser. This leaves Firefox as the lone holdout, despite a <a href="https://bugzilla.mozilla.org/show_bug.cgi?id=825294">Bugzilla ticket</a> that’s been open since 2012. I can’t find any official comment on whether Mozilla plans to add support anytime soon.

I also wasn’t able to find any information on Apple’s plan to enhance or alter its keyboard inputs for iOS, although its “<a href="https://developer.apple.com/library/ios/documentation/StringsTextFonts/Conceptual/TextAndWebiPhoneOS/KeyboardManagement/KeyboardManagement.html#//apple_ref/doc/uid/TP40009542-CH5-SW12">Text Programming Guide for iOS</a>” still recommends (inaccurately, I believe) using its notorious hardcoded <code>&lt;[0-9]*&gt;</code> pattern for ZIP codes.

In the near future, I expect most of these inconsistencies will be resolved, and we can once again start taking these glorious form inputs for granted all over again. But until that happens, let’s all agree to stick to the standards and best practices that have gotten us so far in the first place.

{{< signature "og, al, ml, il" >}}

