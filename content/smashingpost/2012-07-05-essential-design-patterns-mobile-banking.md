---
title: Essential Design Patterns For Mobile Banking
slug: essential-design-patterns-mobile-banking
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bb4c8e03-762e-4272-b385-a2d6634efc6a/colourful-universe-illu.jpg
date: 2012-07-05T12:24:51.000Z
author: greg-nudelman
description: >-
  Despite a great deal of mobile innovation, many creators of financial apps
  still copy their interface patterns from the desktop Web, even though these
  patterns are not as well suited to the mobile space. Small screens, custom
  controls, divided attention and fat fingers demand different thinking when
  designing for mobile.
categories:
  - Mobile
  - Design Patterns
---
Despite a great deal of mobile innovation, many creators of financial apps still copy their interface patterns from the desktop Web, even though these patterns are not as well suited to the mobile space. Small screens, custom controls, divided attention and fat fingers demand different thinking when designing for mobile.

I previously covered mobile wallet UX considerations in my article “<a href="https://www.designcaffeine.com/articles/ultimate-guide-to-designing-nfc-mobile-apps/">Ultimate Guide to Designing NFC Mobile Apps You Won’t be Ashamed Of</a>.” In this article, we will look specifically at simple mobile transfers of funds from checking to savings accounts, taking what works on the Web and converting it into authentically mobile flows using simple, effective design patterns. Similar analyses and design strategies can be applied to many other areas that involve complex forms, such as mobile e-commerce checkout and social network registration.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Currency Design – Designing The Most Desirable Product](https://www.smashingmagazine.com/2016/01/learn-from-the-history-of-banknote-design-most-desirable-product/)
*   [Testing Credit-Card Numbers In Checkouts](https://www.smashingmagazine.com/2016/07/testing-credit-card-numbers-in-e-commerce-checkouts-cheat-sheet/)
*   [Getting Started With The PayPal API](https://www.smashingmagazine.com/2011/09/getting-started-with-the-paypal-api/)
*   [Free PNG Credit Card, Debit Card and Payment Icons Set](https://www.smashingmagazine.com/2010/10/free-png-credit-card-debit-card-and-payment-icons-set-18-icons/)

We will not name any companies in this article. That is deliberate. If you are looking for company bashing, you won’t find it here. But if you want to know how to make mobile banking work, read on.

{{% feature-panel %}}

Let’s begin with the basic building block: selecting an account. It can be accomplished in two primary ways: via a “picker” (called “spinner” in Android) and via a dedicated selection page (also called “table view”).</p>

## Picker/Spinner

For system interactions, many app and mobile website designers start by looking at the desktop Web interface pattern: a form with drop-down menus. Here is a common pattern for me-to-me transfers (i.e. transfers between two of your own accounts, such as checking and savings):

<img loading="lazy" decoding="async" class="132573" title="figure-1-typical-web-form" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ad4aa72d-8a11-4b16-8db3-aba0f743f76f/figure-1-typical-web-form1.jpg" alt="Typical Web Form" width="475" height="270" /><br>
<em>Typical me-to-me transfer via Web form.</em>

The drop-down menu works reasonably well on the desktop Web, assuming the customer has between 1 and about 20 or 30 accounts. Each account can be listed in the drop-down menu by its full name, along with the account balance:

<img loading="lazy" decoding="async" class="132574" title="figure-2-web-form-options" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b6ef5077-be1f-45a7-b197-7bf8c7287f14/figure-2-web-form-options.jpg" alt="Web Form Options" width="547" height="412" /><br>
<em>Selecting an account via the Web form’s select control.</em>

How does this translate to mobile? Not very well. Blindly copying the desktop Web is a knee-jerk reaction, and it turns out that it’s mostly unsuccessful, resulting in a subpar experience. Here is why. Instead of the 20 or 30 selections that can be displayed in the drop-down menu, the iPhone’s standard picker control shows only 3 full and 2 partial choices:

<img loading="lazy" decoding="async" class="132575" title="figure-3-ios-picker" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/02c7a7a0-4534-4591-89f7-ec0fd4462b6d/figure-3-ios-picker.jpg" alt="ios Picker" width="303" height="455" /><br>
<em>Selecting an account via iOS’ picker control.</em>

In Android 4.0 (the latest public Android version, named Ice Cream Sandwich), the situation is slightly better. Instead of the picker, the Android OS uses the spinner overlay, which shows 8 options. Unfortunately, the formatting options are quite limited, and the text area in the overlay is about 20% narrower than the main screen because the spinner is not using the full width of the device. This leads to confusing double and triple wrapping of text and numbers:

<img loading="lazy" decoding="async" class="132585" title="figure-4-andorid-wheel" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e3fa6f67-67db-4af8-8b87-3fa421243e76/figure-4-andorid-wheel.jpg" alt="Andorid Wheel" width="255" height="453" /><br>
<em>Selecting an account via Android’s spinner control.</em>

Interestingly, some online banks use this pattern to display a list of accounts. However, by necessity (and to avoid the confusion of wrapping and truncation on older and smaller low-end devices), they use short codes for account names, such as CHK, SAV and CC1. These abbreviations work reasonably well for text banking, where the short-and-sweet mental model (“C U L8R”) reigns supreme. However, code abbreviations are far from the slick world-class UI elements that consumers have come to expect from their smartphones. Rather, they smack of “dim phones,” BlackBerrys, DOS and enterprise software. Having to remember codes to do mobile banking is a far cry from the experience of playing Angry Birds or shopping on Amazon or Gilt. To create a better experience on mobile, we need another design pattern: a dedicated selection page.</p>

## Dedicated Selection Page

A slicker and more usable mobile design pattern for listing accounts than pickers and spinners would be a dedicated selection page (also called “table view”) in which 10 or more account options could be listed comfortably. As Apple’s <a href="https://developer.apple.com/library/ios/#documentation/userexperience/conceptual/mobilehig/UIElementGuidelines/UIElementGuidelines.html#//apple_ref/doc/uid/TP40006556-CH13-SW23">iOS developer guidelines</a> state, “Consider using a table view, instead of a picker, if you need to display a very large number of values. This is because the greater height of a table view makes scrolling faster.”

This is how it looks wireframed using the agile, lightweight, sticky-note methodology (see the “References” at the end of this article):

<img loading="lazy" decoding="async" class="132577" title="figure-5-dedicated-page" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1ae4e76a-2c4c-4118-aba9-b62f13e1d043/figure-5-dedicated-page.jpg" alt="Dedicated Page" width="275" height="227" /><br>
<em>Selecting an account via a dedicated selection page (wireframe).</em>

The advantages of using a dedicated selection page over a picker or spinner include the following:

*   Any font and branding you like;
*   A platform-independent experience;
*   Use the entire width of the page;
*   Text wraps as needed, so multiple device profiles can use the page comfortably;
*   Display 10 or more options at a time, with comfortable scrolling.

The bottom line is that, with a dedicated selection page, you can easily display the account’s full name and balance.

How could this pattern be used with a form? One popular pattern is a form with dedicated selection pages. Unfortunately, this often creates very long flows.</p>

## Form With Dedicated Selection Pages

The idea behind this pattern is simple: copy the standard desktop Web form but use dedicated selection pages instead of pickers or spinners.

Using this mobile design pattern, our me-to-me transfer flow would look like this:

1.  Blank form;
2.  Dedicated page to select the “From” account;
3.  Back to the form (with the “From” field now filled in);
4.  Dedicated page to select the “To” account;
5.  Back to the form (with both the “To” and “From” fields now filled in);
6.  Fill in the amount, etc., and hit “Continue”;
7.  Verification page.

Here is the flow wireframed using the agile lightweight sticky-note methodology:

<img loading="lazy" decoding="async" class="132587" title="figure-6-dedicated-pages-form" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8799bbab-b2fd-43e0-81f2-add99d8a593b/figure-6-dedicated-pages-form.jpg" alt="Dedicated Pages Form" width="549" height="453" /><br>
<em>Me-to-me transfer via a form with dedicated selection pages (wireframe).</em>

While this pattern works, it makes the flow quite long: seven pages. Could it be shortened? Absolutely. One excellent mobile-first pattern is the dedicated wizard flow.

## Dedicated Wizard Flow

This is an extreme adaptation of the desktop Web form. This pattern works extremely well for short forms because it dispenses with desktop forms entirely, using a dedicated page for each attribute of the form.

Using this pattern, our me-to-me transfer flow would look like this:

1.  Dedicated page to select the “From” account;
2.  Dedicated page to select the “To” account;
3.  Dedicated page to enter the amount, with a numeric keyboard;
4.  Verification page.

And here is the flow using the agile methodology:

<img loading="lazy" decoding="async" class="132598" title="figure-7-dedicated-wizard-flow-mobile" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/71dd9420-d07b-4057-bc78-2b6fef459745/figure-7-dedicated-wizard-flow-mobile1.jpg" alt="Dedicated Wizard Flow Mobile" width="549" height="226" /><br>
<em>Me-to-me transfer via a dedicated wizard flow (wireframe).</em>

This pattern works very well for short forms, and it is a great example of Luke Wroblewski’s <a href="https://www.lukew.com/ff/entry.asp?933">mobile-first</a> design thinking. The entire flow is accomplished in only four steps. Note that a verification page (allowing the customer to review the entire transaction before tapping the final “Transfer” button) is recommended with this pattern. Note also the use of the breadcrumb pattern, which shows the customer which step of the workflow they are on and how many steps remain. The breadcrumb enhances this design pattern nicely.

Are we done? Should you create a dedicated wizard for every flow on your mobile banking website? Not so fast.

In mobile, nothing comes for free. That includes the dedicated wizard flow, which completely breaks down in longer forms. The basic idea is to have a dedicated page for each element of the form. But if the form has five or more elements, then the flow starts to get too long. Another issue is the inability of this pattern to distinguish between optional elements (such as “Memo”) and required elements (such as “Amount”). With this pattern, each element gets its own entry page with the appropriate keyboard and is likely to be treated as “required”. Even if the customer understands that they don’t need to enter anything, each element requires the customer to at least look at the page and click “Continue.”

So, is there another pattern for a page with five or more elements and many optional fields? I’m glad you asked. One of the most versatile yet underused patterns is the wizard flow with form. And as a bonus, this pattern dispenses with the need for a separate verification page.</p>

## Wizard Flow With Form

The idea here is very simple. Start with a dedicated page to select each account, and then show the rest of the fields in a form.

Using this pattern, our me-to-me flow would look like this:

1.  Dedicated page to select the “From” account;
2.  Dedicated page to select the “To” account;
3.  Continue to the form (with both the “To” and “From” fields now filled in);
4.  Fill in the amount, etc., and hit “Continue”.

Here is the wireframe using the agile methodology:

<img loading="lazy" decoding="async" class="132597" title="figure-8-wizard-flow-form" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c2250a29-b220-479e-b91e-eb7d795e2f16/figure-8-wizard-flow-form.jpg" alt="Wizard Flow Form" width="550" height="224" /><br>
<em>Me-to-me transfer via the wizard flow with form.</em>

This mobile design pattern combines the best features of Web forms, such as the flexibility of having optional fields and multiple input fields, with the vastly improved usability of dedicated, mobile-optimized selection pages. Another boon is the option to dispense completely with the verification page, because the form page itself acts as an editable verification page. Of course, you could always append a separate verification page if you really must.

Editing is also much easier than with most other patterns. Instead of having to go through the entire flow again, the customer only has to edit the fields that need correction. For example, to edit the “To” account, the customer would tap the corresponding field in the form and be taken to the dedicated “To” account page, and then immediately back to the form, without having to go through the entire <code>“From” account → “To” account → Amount</code> flow again.</p>

## Mobile: Thinking Differently

As we’ve seen now, mobile design itself is usually not complicated. In fact, because people will be using your app with fat meaty pointers (commonly called “fingers”) in a stressful multitasking environment (commonly called “life”), a less complicated design is virtually guaranteed to perform better. However, designing for mobile is one of the most sophisticated exercises any of us is likely to encounter. Simply copying successful desktop patterns is usually the worst choice, yet it is the one many designers naturally gravitate to.

Designing for mobile requires thinking differently. Remember that in mobile, each form field requires at least an extra tap to bring up the keyboard, picker, dedicated page or other element to enter data. Instead of a vertical flow to guide the person to the next field, consider using a horizontal flow instead. Look for options and inputs to eliminate. Whenever possible, minimize the number of pages the person has to go through in order to complete the workflow; this will reduce input errors and increase customer satisfaction. Last but not least, make user testing the core of your mobile design process, and be sure to user test everything you design as early as possible.</p>

### References

*   [_Rocket Surgery Made Easy_](https://www.sensible.com/rsme.html), Steve Krug (New Riders: New York, 2010)
*   “[How to Make Agile Work for Your Mobile Design Project](https://www.designcaffeine.com/articles/free-webinar-agile-mobile-design/),” (registration required) Greg Nudelman, video from the Mobile Design Essentials Virtual Seminar, DesignCaffeine
*   “[Ultimate Guide to Designing NFC Mobile Apps You Won’t be Ashamed Of](https://www.designcaffeine.com/articles/ultimate-guide-to-designing-nfc-mobile-apps/),” Greg Nudelman, DesignCaffeine
*   “[Mobile First](https://www.lukew.com/ff/entry.asp?933),” Luke Wroblewski

<em>(al) (da) (il) (jc)</em>

