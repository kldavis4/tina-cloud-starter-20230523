---
title: A Guide To Designing Touch Keyboards (With Cheat Sheet)
slug: guide-to-designing-touch-keyboards-with-cheat-sheet
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2c35869f-4887-4316-9dbb-80b72472b984/ux-10.jpg
date: 2013-08-13T08:37:47.000Z
author: christian-holst
description: >-
  Touch devices have rightfully been praised for generally being much more
  intuitive than the decades-old computer mouse and keyboard. Users interact
  directly with touch interfaces, which narrows the gap between human act and
  software response.
categories:
  - UX
  - Mobile
  - Usability
  - UX
---
Touch devices have rightfully been praised for generally being much more intuitive than the decades-old computer mouse and keyboard. Users interact directly with touch interfaces, which narrows the gap between human act and software response. Yet typing on mobile devices — in particular on smartphones — is quite the horror story. It’s <strong>slow, painful and error-prone</strong>.

The obvious culprits are keyboard character size and proximity of the keys, but there are many other important aspects to consider, including:

*   using auto-correct dictionaries appropriately,
*   auto-capitalizing relevantly,
*   hinting at the input type,
*   honoring the tab sequence,
*   invoking custom keyboards consistently.

<img loading="lazy" decoding="async" class="118727" title="Typing on mobile devices is slow and error-prone." src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/165f19c4-fbaf-4772-8a5f-25cedd99aa62/mobile-touch-keyboards-500-mini.jpg" alt="Typing on mobile devices is slow and error-prone." width="500" height="200" />

During a recent large-scale 1:1 mobile usability study of 18 of the largest mobile commerce websites, we observed how certain features and limitations of modern touch keyboards can collide with the user’s expectations of how to fill out a form. When this happens, users quickly grow frustrated, as one form-field validation error pops up after another or, worse yet, the user gets stuck and ultimately abandons the website.

{{% feature-panel %}}

## <span class="rh">Further Reading</span> on SmashingMag:

*   [The Thumb Zone: Designing For Mobile Users](https://www.smashingmagazine.com/2016/09/the-thumb-zone-designing-for-mobile-users/)
*   [Finger-Friendly Design: Ideal Mobile Touchscreen Target Sizes](https://www.smashingmagazine.com/2012/02/finger-friendly-design-ideal-mobile-touchscreen-target-sizes/)
*   [Beyond The Button: Embracing The Gesture-Driven Interface](https://www.smashingmagazine.com/2013/05/gesture-driven-interface/)
*   [Browser Input Events: Can We Do Better Than The Click?](https://www.smashingmagazine.com/2015/03/better-browser-input-events/)

When faced with a suboptimal touch keyboard implementation, users lose confidence in the website, and some even doubt their own ability to fill out a form on a smartphone. Clearly, a good mobile experience requires good form usability, and implementing touch keyboards is a key part of that.

In this article, we will look a bit deeper into the usability issues surrounding touch keyboards, including <strong>five design guidelines</strong> that will alleviate some of these pains. The guidelines are an excerpt from the 147 guidelines in the <a href="https://baymard.com/mcommerce-usability">M-Commerce Usability Report</a>. We previously looked into <a title="Exploring Ten Fundamental Aspects Of M-Commerce Usability" href="https://www.smashingmagazine.com/2013/05/21/recommendations-mobile-commerce-websites/">10 guidelines for mobile e-commerce</a> here on Smashing Magazine; these 5 guidelines on touch keyboards are more generic and apply to any mobile website on which the user interacts with a touch keyboard.

Furthermore, we’ve also benchmarked the mobile websites of the top 50 online retailers against these five guidelines and found that an astounding 98% get one or more of these wrong, and 70% of the top mobile websites get at least two wrong (as of 31 July 2013). While some of the guidelines might seem obvious at first, clearly we all need to pay better attention when so many multi-million dollar e-commerce stores get them wrong.</p>

## 1\. Disable Auto-Correction When The Dictionary Is Weak (92% Get It Wrong)

<strong>Issue:</strong> Poor auto-correction is frustrating when users actually notice it, and can be detrimental when they do not.

Auto-correction often works very poorly for abbreviations, street names, email addresses and other words that are not in the dictionary. This caused significant issues throughout testing and resulted in a great deal of erroneous data being submitted as test subjects completed their purchases.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8acdb274-a2e4-4f55-a588-b409bcbe8deb/auto-correction-mini.png"><img loading="lazy" decoding="async" class="size-large wp-image-118730" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2539fb7c-6b59-40dc-b3b9-4b70ff035c49/auto-correction-500-mini.png" alt="auto-correction" width="500" height="242" /></a><br>
<em>As this subject typed in the street name “westheimer” on the website for Toys’R’Us, the phone incorrectly auto-corrected to “weathermen” (left). However, the subject did not notice this, submitted the form and received a validation error (right). (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8acdb274-a2e4-4f55-a588-b409bcbe8deb/auto-correction-mini.png">Large view</a>)</em>

One major problem with auto-correction is that <strong>users often fail to notice the correction</strong> (because they are focused on what they are typing instead of what they have typed). This is fine if the correction is correct, but it can be detrimental if it is wrong. For example, in multiple instances during testing, valid addresses were auto-corrected to invalid ones and submitted because the subject didn’t notice the auto-correction.

On websites without address validators, this resulted in orders being shipped to wrong addresses, unless the subject was particularly attentive on the order-review page (after all, auto-corrected data often looks very similar to the intended input, making users less likely to notice the error). Of course, auto-correction fails miserably in the address field not just in edge cases (such as with “weatherman”), but with common (and standardized) abbreviations, such as “Rd” being auto-corrected to “Ed.”

That being said, <strong>auto-correction did prove helpful in other scenarios</strong> when it corrected invalid data to valid data. Disabling auto-correction on all fields (such as comment fields), therefore, is not recommended. Instead, use discretion, and disable it on fields for which the dictionaries are weak. This typically includes proper names of various sorts (streets, cities, persons) and other identifiers (email addresses, coupon codes, etc.).

While seemingly simple, in practice this is by far the most neglected part of touch keyboard usability; almost every single top mobile commerce website gets this one wrong. The <a title="Touch Keyboard Benchmark of the Top 50 Mobile Commerce Sites" href="https://baymard.com/labs/touch-keyboard-types#benchmark">benchmark</a> reveals that 92% of them haven’t disabled auto-correction on the address field. Given the severity of the problems caused by auto-correction on address and email fields, it’s astonishing how few actually disable auto-correction here.

You can disable auto-correction by adding the <code>autocorrect</code> attribute to the input tag and setting it to <code>off</code>, like so:

<pre><code class="language-markup">
&lt;input type="text" autocorrect="off" /&gt;
</code></pre>

## 2\. Show The Appropriate Keyboard Layout (60% Get It Wrong)

<strong>Issue:</strong> Inappropriate keyboard layouts slow down typing, and users generally mistype long number sequences on standard keyboards because of the small hit area and the close proximity of the numeric keys.

One of the main limitations of touch keyboards on smartphones is their size. The letters themselves are minuscule. In fact, a character on an iPhone 4 in portrait mode measures 4 × 5.9 millimeters.

<img loading="lazy" decoding="async" class="size-medium wp-image-118735" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/26cfdbab-76f9-4358-bab7-5dc9f1835d69/2a-small-keyboard-letters-300x201.png" alt="small-keyboard-letters" width="300" height="201" />

Compare this to Apple’s own design guidelines, which recommend that all clickable interface elements be of least 6.85 × 6.85 millimeters because anything below that would yield very poor click accuracy. (Microsoft and Nokia also recommend a minimum hit area of approximately 7 × 7 millimeters). Predictably, this results in misspellings.

But by changing an attribute or two in the code of your input fields, you can instruct the user’s phone to automatically show a keyboard optimized for the requested input. For example, you can invoke a numeric keyboard for a credit-card field, a phone keyboard for a telephone field, and an email keyboard for an email address. This saves the user from having to switch from the traditional keyboard layout, and, in the case of numeric inputs, <strong>minimizes typos</strong> because these dedicated keyboards have much larger keys, thus reducing the chance of accidental taps.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fb89b98a-5e6e-4ae3-8a45-334ce629b632/keyboard-layout-1-mini.png"><img loading="lazy" decoding="async" class="118738" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/34bef11c-5d54-4241-9eda-889f9d4528bb/keyboard-layout-1-500-mini.png" alt="2b - keyboard-layout-1" width="500" height="262" /></a><br>
<em>The credit-card input on Best Buy invokes the standard keyboard layout, so the user has to first switch to the numbers and special characters view (middle) and then type out the 16 digits without a single typo. This was a difficult task for many subjects, who looked to and from their card and phone while trying to hit the miniature buttons stacked against one another. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fb89b98a-5e6e-4ae3-8a45-334ce629b632/keyboard-layout-1-mini.png">Large view</a>)</em>

Throughout testing, multiple subjects noticed these dedicated keyboards and commented on them approvingly. In fact, on iOS, the hit area of a key is 471% larger on the numeric keyboard than on the traditional keyboard (209 × 108 pixels versus 52 × 76 pixels). More importantly, we recorded significantly fewer typos in numeric inputs when a numeric keyboard layout was displayed. This led to <strong>fewer validation errors</strong>, which, in turn, resulted in a better and more seamless shopping experience on those websites. This was especially true of long sequences, such as phone and credit-card numbers.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d89539d6-5938-46cd-b613-fcac3988d021/keyboard-layout-2-mini.png"><img loading="lazy" decoding="async" class="118741" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4c7a83a1-9d99-45e3-9677-c1398f6df0a5/keyboard-layout-2-500-mini.png" alt="keyboard-layout-2" width="500" height="289" /></a><br>
<em>On the left, a subject accidentally hits the dash button instead of the “1” button due to the small size and proximity of buttons on the standard keyboard layout. A number-optimized keyboard layout would have been more appropriate. On the right, when the user fills out the “Day phone” field on GAP’s website, a special phone-optimized keyboard appears, showing buttons that are 471% larger than those on the traditional keyboard. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d89539d6-5938-46cd-b613-fcac3988d021/keyboard-layout-2-mini.png">Large view</a>)</em>

Another benefit of dedicated keyboard layouts is that they indicate the required input, which is helpful if the label is out of sight or the user is unsure of what to enter. However, note that numeric keyboard layouts can be limiting because they do not allow the user to enter alphabetic characters and allow only a few, if any, special characters or separators. Invoking these keyboards on fields where they are the best match, therefore, is important, which includes <strong>phone numbers, ZIP codes, credit-card numbers and credit-card security codes</strong>. Similarly, make sure your formatting examples are actually possible to replicate using the invoked keyboard.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e7a260ae-f57d-4cde-bf43-42964126ed06/keyboard-layout-3-mini.png"><img loading="lazy" decoding="async" class="118760" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5434adf0-a868-4dcd-8f14-9c6117dae784/2d-keyboard-layout-240.png" alt="keyboard-layout-3" width="240" height="360" /></a><br>
<em>Typing a phone number according to the example format given here (“555-555-5555”) is not possible on iOS because the keyboard layout does not include the dash character. (Interestingly, entering it on Android is possible, which goes to show why testing on multiple platforms helps to ensure that you don’t require formatting that is only possible on some.) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e7a260ae-f57d-4cde-bf43-42964126ed06/keyboard-layout-3-mini.png">Large view</a>)</em>

Given these substantial usability benefits, one would think that these dedicated keyboards are widely used. Yet, 60% of the top mobile commerce websites do not invoke them for one or more of the layouts for email addresses (email keyboard), phone numbers (phone keyboard) or credit-card numbers (numeric keyboard).

Technically, there are a few ways to invoke the numeric keyboard layouts, and also slight distinctions between them (i.e. phone versus number), with slightly different behaviors across platforms (iOS, Android, etc.). In general, two HTML attributes will invoke a numeric keyboard layout, namely the <code>type</code> and <code>pattern</code> attributes.

The <code>type</code> attribute carries semantic meaning and should be used only when an appropriate type is available for your input, which is the case for phone numbers and email addresses. For numeric inputs, however, providing a <code>pattern</code> attribute instead is recommended. (Note that you might want to add a <code>novalidate</code> attribute if you only want the browser to invoke the keyboard and not enforce this format.)

<strong>For any phone fields, use this:</strong>

<pre><code class="language-markup">
&lt;input type="tel" /&gt;
</code></pre>

For any other fields where you want to invoke a numeric keyboard, use this:

<pre><code class="language-markup">
&lt;input type="text" pattern="d*" novalidate /&gt;
</code></pre>

For any email fields, use this:

<pre><code class="language-markup">
&lt;input type="email" /&gt;
</code></pre>

As mentioned, there are some distinctions between the types of numeric keyboard layouts, as well as some <strong>differences between mobile platforms</strong>. For example, on iOS, the code provided above to invoke the phone layout would produce a keyboard that allows the user to enter digits and a small set of phone-related special characters and separators, whereas the code for invoking the numeric keyboard would allow the user to enter only digits. Meanwhile, on Android, the phone keyboard layout is also invoked but with vastly more special characters, allowing for richer formatting of the phone number.

Yet, the numeric keyboard invoked by the <code>pattern</code> attribute isn’t support by Android at all; instead, it simply invokes the regular alphanumeric keyboard. While you could use <code>type="number"</code> to invoke a numeric keyboard on both iOS and Android, setting the type to <code>number</code> carries semantic meaning that in many cases wouldn’t be appropriate (for example, a credit-card number is a numeric sequence, not a number).

Therefore, we recommend the more defensive strategy of using <code>pattern="d*"</code>, which produces an enhanced experience on iOS while having no implications on other platforms that do not yet support this behavior. (Of course, if the field does represent a number, such as a price or quantity, then <code>type="number"</code> should obviously be used.)

## 3\. Invoke Keyboard Layouts Consistently (54% Get It Wrong)

<strong>Issue:</strong> When one field invokes a dedicated keyboard layout but other similar fields do not, users are confused and begin to question the type of input requested by the field without the dedicated keyboard.

Invoking the appropriate keyboard layout for a particular input field is great (see the previous recommendation), but be sure to do it consistently throughout your website, or else you could greatly confuse the user. In other words, if a ZIP code field invokes a numeric keyboard, then similar input fields should have the same behavior.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0d5c20e9-c572-40aa-921c-2b6274685a0d/consistently-invoke-keyboard-mini.png"><img loading="lazy" decoding="async" class="118745" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ecd9574c-bb92-4afe-be63-9cc964474f65/consistently-invoke-keyboard-500-mini.png" alt="consistently-invoke-keyboard" width="500" height="357" /></a><br>
<em>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0d5c20e9-c572-40aa-921c-2b6274685a0d/consistently-invoke-keyboard-mini.png">Large view</a>)</em>

While this might sound obvious, <strong>many websites fail to invoke dedicated keyboard layouts consistently</strong>. For instance, the flower store FTD (pictured above) invokes a numeric keyboard for the credit-card number but not for the very next security-code field, even though both values are always numeric.

Of the top 50 grossing online retailers, 54% get this wrong on their mobile websites, where one or more of the telephone, credit-card or CVV fields don’t invoke a numeric touch keyboard. These 54% break down as follows (in absolute numbers): 24% invoke the numeric inputs for none of these three numeric inputs (which, although consistent, is consistently bad), and the remaining 30% (including FTD) are inconsistent, with the numeric keyboard layout being invoked on only some of the fields.

Even more surprising is just how confused some of the test subjects were by this during the usability tests. They began questioning their initial interpretation of individual fields, thinking that perhaps something else was required. For example, upon seeing the standard keyboard layout for the “Card security code” (pictured on FTD’s website above), the subjects began wondering whether this was the three-digit code on the back of their credit card or one of the many other strings printed on the card.</p>

## 4\. Honor The Behavior Of The “Next” and “Previous” Buttons (4% Get It Wrong)

<strong>Issue:</strong> Users are either vexed or confused when “Next” and “Previous” buttons take them to fields that are illogically sequenced.

During testing, the subjects struggled with websites that failed to honor the behavior of the “Next” and “Previous” buttons. The expected behavior is straightforward: When the user clicks the “Next” button, they expect to be taken to the next logical field in the form, without any changes and without the form being submitted. The same goes for the “Previous” button, just in the opposite direction, of course.

This goes beyond just having the right tab sequence (although that is a good start). Things often go awry when dealing with dynamic fields that depend on the user’s prior selection. In these instances, we’ve seen the data of users get deleted or the tab sequence violated. One must be particularly careful with the interfaces of custom forms, too. For example, in the Disney Store, a custom-designed state selector isn’t part of the tabbing sequence (because it technically isn’t an input element), and so users are sent right past the state field.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b8cd1acb-60ac-4396-9714-3908444ab588/next-previous-buttons-1-mini.png"><img loading="lazy" decoding="async" class="size-large wp-image-118746" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/296ccb84-272a-418b-9edd-e25b332b45c4/next-previous-buttons-500-mini.png" alt="next-previous-buttons" width="500" height="226" /></a><br>
<em>After filling in her ZIP code here (left), the subject hit the “Next” button, which correctly took her to the “Location Type” drop-down menu (right). But, as shown, the website cleared the subject’s previously inputted data. Obviously, data should persist when “Next” and “Previous” buttons are used. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b8cd1acb-60ac-4396-9714-3908444ab588/next-previous-buttons-1-mini.png">Large view</a>)</em>

These buttons essentially function as the mobile version of keyboard tabbing; therefore, they should adopt the same sequential principles as desktop tabbing. They should provide a fast way to get from one field to the next without having to use a pointer (whether a mouse or finger). This is particularly important on mobile because screen space is so limited when the keyboard is open that the next field might be partially obstructed, making the “Next” button even more convenient to use. So, while the “Next” and “Previous” buttons might not be used by all users, the consequence of dishonoring the behavior of these buttons is significant.

Luckily, most websites get this one right. As long as the code is clean, mobile browsers will, by default, set the tabbing sequence according to the order of appearance of the fields. Of the top mobile websites, only 4% get this wrong.</p>

## 5\. Disable Auto-Capitalization Where Appropriate (38% Get It Wrong)

<strong>Issue:</strong> Nearly all subjects believed their email address had to be in lowercase, so auto-capitalizing this data adds needless friction to the process.

The default behavior of smartphones is to auto-capitalize the first letter in standard text fields, which is usually desirable. However, disabling this auto-capitalization is preferable in a few cases, especially for email addresses, which most test subjects wanted to be in lowercase.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6c0be78f-2cbc-437b-9b36-0b5d500a35df/auto-capitalization-mini.png"><img loading="lazy" decoding="async" class="118749" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/044bbf5c-8842-4bbb-a87b-84dec0a4e70c/auto-capitalization-500-mini.png" alt="auto-capitalization" width="500" height="338" /></a><br>
<em>This subject noticed the capital “J” and went back to replace it with a lowercase “j” because he was unsure whether the capitalized version would work. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6c0be78f-2cbc-437b-9b36-0b5d500a35df/auto-capitalization-mini.png">Large view</a>)</em>

Multiple times during testing, subjects noticed an uppercase letter and made an explicit effort to replace it with the lowercase equivalent. Most explained that they were unsure whether uppercase characters were allowed or whether email addresses in general were case-sensitive. On websites that had disabled auto-capitalization in the email field, no subject ever actively capitalized the first character. Disabling auto-capitalization for email and other appropriate fields (such as URLs) is recommended, then.

Among the top mobile commerce websites, 38% don’t disable auto-capitalization on email address fields, leaving them as plain-text input fields, and leaving less technically inclined users in doubt.

Auto-capitalization can be disabled by adding the <code>autocapitalize</code> attribute to the <code>&lt;input&gt;</code> tag and setting it to <code>off</code>, like so:

<pre><code class="language-markup">
&lt;input type="text" autocapitalize="off" /&gt;
</code></pre>

Of course, for email fields, you should set the <code>type</code> attribute to <code>email</code>:

<pre><code class="language-markup">
&lt;input type="email" autocapitalize="off" /&gt;
</code></pre>

On iOS, setting the <code>type</code> to <code>email</code> will automatically disable auto-capitalization. However, still set the <code>autocapitalize</code> attribute because that will also work on iOS and might be needed on other platforms that do not yet support the <code>email</code> input type or that implement it differently.</p>

## Testing And The Cheat Sheet

While these fundamentals might seem obvious at first, remember that 98% of the world’s largest mobile commerce websites violate at least one of these (see the <a title="Touch Keyboard Benchmark of the Top 50 Mobile Commerce Sites" href="https://baymard.com/labs/touch-keyboard-types#benchmark">complete list</a>). And 70% get two or more of these “basic” touch keyboard guidelines wrong. In fact, 24% haven’t optimized their inputs for touch keyboards at all, whether by omitting basic keyboard layouts (phone, email, numeric), invoking them inconsistently (or consistently poorly), not disabling auto-correction where appropriate, or not disabling auto-capitalization for email fields.

One reason for this lack of compliance might be that very thorough testing would be required to spot all of the pitfalls across a large website — hence, the third recommendation of invoking keyboard layouts consistently, which in an ideal world shouldn’t even need to be mentioned. Another reason, mentioned in a <a title="Exploring Ten Fundamental Aspects Of M-Commerce Usability" href="https://www.smashingmagazine.com/2013/05/21/recommendations-mobile-commerce-websites/">prior Smashing Magazine article</a>, is that <strong>mobile and touch interfaces represent a relatively new platform</strong>, with an entirely new interaction method that requires attention to a myriad of small details — details that we as Web designers and developers are not yet accustomed to actively looking and designing for.

For this reason, we’ll end this article with a cheat sheet of the most common pitfalls when working with input fields for touch interfaces, along with copy-and-pastable code and a mobile touch-optimized demo of fields that invoke the correct keyboards, which you can use as a checklist when designing and developing mobile- and tablet-optimized websites.

*   Interactive [cheat sheet for touch keyboards](https://baymard.com/labs/touch-keyboard-types "Touch Keyboard Type Cheat Sheet"), with mobile-optimized demo

These fields are typically included in the following types of forms: account registration, account sign-in, search, surveys, the entire checkout process, comment forms, and contact forms. We recommend searching your entire code repository to catch every single instance of these.

<em>(al) (ea)</em>

