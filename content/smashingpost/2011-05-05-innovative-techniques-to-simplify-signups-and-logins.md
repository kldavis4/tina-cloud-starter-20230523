---
title: 'Innovative Techniques To Simplify Sign-Ups And Log-Ins'
slug: innovative-techniques-to-simplify-signups-and-logins
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1aa11a8f-2192-4231-af9b-0b0478777d17/usernameafter.png
date: 2011-05-05T12:23:26.000Z
author: anthony-t
summary: >-
  In this article, we present a couple of new ideas to design sign-up and log-in forms that might be useful for your next designs. Find some innovative techniques that could make your forms simpler and more efficient to fill out.
description: >-
  In this article, we present a couple of new ideas to design sign-up and log-in forms that might be useful for your next designs. Find some innovative techniques that could make your forms simpler and more efficient to fill out.
categories:
  - UX
  - Forms
  - Design
  - Captcha
  - Security
  - Usability
  - UX
---

There are many ways to design sign-up and log-in forms. Most designers are familiar with the conventional ways. But understanding and applying a few innovative techniques could make your forms simpler and more efficient to fill out. In this article, we’d like to present a couple of new ideas that might be useful for your next designs. Please notice that before using these techniques, you should make sure that they make sense in the context in which you are going to use them. We’d love to hear about your case-studies and usability tests that affirm or dismiss the suggestions proposed below.

{{% feature-panel %}}

## Simplifying Sign-Ups

The purpose of every sign-up form is for users to complete it successfully and send it in. However, if the form is long and complicated, then the user’s excitement for your website could turn to displeasure. Here are a few innovative techniques that will make your forms faster and easier to fill out.

### Ask for a User Name After The User Has Signed Up

Sign-up forms typically ask users to create a name that is unique to the website. However, coming up with a unique user name that’s not taken could take trial and error and, thus, time. Instead of hassling people for a user name when they sign up, you might want to consider asking afterwards. This way, you won’t lose sign-ups from frustrated users, and you’ll prevent users from creating random and forgettable names just to satisfy the form’s requirements.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1aa11a8f-2192-4231-af9b-0b0478777d17/usernameafter.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1aa11a8f-2192-4231-af9b-0b0478777d17/usernameafter.png" alt="" width="310" height="190" /></a><figcaption>Username</figcaption></figure>

### Require Users to Type Their Password Only Once

Many sign-up forms ask users to type their password in two different fields. The reason is understandable. Forms mask passwords for security reasons, so that snoopers can’t see them. And to cut down on typographical mistakes and increase the chances of correct input, two separate entries are required.

In reality, though, this allows for greater error, because it forces users to type more. They can’t see the characters they’re inputting, making it difficult to know whether they’re typing the right password each time.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ea94dd5a-438f-4398-a068-e8fa210037a8/signup2.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ea94dd5a-438f-4398-a068-e8fa210037a8/signup2.png" alt="" width="471" height="139" /></a><figcaption>Password in two different fields.</figcaption></figure>

A more efficient approach would be to ask users to type their password in once, but then include a box they can check to unmask the password, so that they can check it. This option could reduce the number of text fields and decrease the work that users have to do to sign up.

*   jQuery Plug-In for Masking Passwords

### Auto-Fill City and State Fields Based on User’s ZIP Code

If you require the user’s home address, then consider auto-filling the city and state fields based on the ZIP code. The form will be faster to fill out because users won’t have to waste time and energy manually selecting their city and state from drop-down lists.

*   <span class="removed_link" title="https://forumsblogswikis.com/2007/08/15/using-ajax-to-get-city-and-state-from-zip-code/">Using AJAX to Get City and State from ZIP Code</span>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6f754f59-f169-4163-b3a3-c8330c60d378/signup3.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6f754f59-f169-4163-b3a3-c8330c60d378/signup3.png" alt="" width="513" height="69" /></a><figcaption>Auto-filling the city and state fields based on the ZIP code.</figcaption></figure>

### Auto-Complete the Country Field

The conventional way for users to specify their country is to select it from a drop-down list. A more efficient way would be to use an auto-complete text field. Instead of making users scroll through an alphabetical list of every country in the world, the text field would allow users to select their country from a small subset of countries that match the letters they type. The user needs only to type a few letters to see their country in the menu.

*   [AJAX Auto-Complete for jQuery](https://www.devbridge.com/projects/autocomplete/jquery/)

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7e1c0cd1-48ae-4ade-b197-57096dd0d2a2/signup4.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7e1c0cd1-48ae-4ade-b197-57096dd0d2a2/signup4.png" alt="" width="300" height="133" /></a><figcaption>Auto-complete the country field.</figcaption></figure>

### Allow Users to Auto-Fill Their Payment Address From the Shipping Address

If a user is buying a product, they’ll have to submit payment and shipping information. Most of the time, the addresses will be the same, so let them auto-fill one from the other. You could include a link saying “Same as shipping information” in the payment section, and when clicked, it would repeat the shipping data in the payment fields.

*   [Copying Billing and Shipping Address Information with jQuery](https://www.encaffeinated.com/articles/view/copying_billing_and_shipping_address_information_with_jquery/)
*   Copy Form Input Data to Another Input Field with jQuery

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f05f634a-4059-4b81-bffe-9a87ed39f000/signup5.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f05f634a-4059-4b81-bffe-9a87ed39f000/signup5.png" alt="" width="345" height="197" /></a><figcaption>Include a link saying “Same as shipping information” in the payment section.</figcaption></figure>

### Don’t Check the Newsletter Option by Default. Offer a Preview Instead

Most website owners pre-check the newsletter box, hoping to get more subscribers. Chances are, it will work. But a subscription is meaningless if the user has done so only because they have overlooked or misunderstood the option. If they’re not interested, they’ll unsubscribe sooner or later. Forcing them to subscribe won’t help you in the long run. And receiving a newsletter without having explicitly asked for it can turn users off.

A more effective approach would be to make users want to subscribe by showing them a preview or excerpt of the newsletter. This way, they’ll know what they’re missing if they don’t subscribe. You’ll also sleep well knowing that users who subscribe have done so because they’re genuinely interested in your content.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1fc1bba2-1228-4b87-8218-75a42b875074/simplify6.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1fc1bba2-1228-4b87-8218-75a42b875074/simplify6.png" alt="" width="336" height="24" /></a><figcaption>Show a preview or excerpt of the newsletter to make users want to subscribe.</figcaption></figure>

### Combat Spam by Hiding a Text Field With JavaScript, Instead of Using CAPTCHA

If you get a lot of spam, then putting a CAPTCHA on your form may be necessary. What’s *not* necessary is making the CAPTCHA an obstacle that turns users away. Traditional CAPTCHAs that ask users to retype distorted letters have been proven to hurt conversion rates. With the extra hassle they force on users, it’s no wonder.

*   [CAPTCHA’s Effect on Conversion Rates](https://www.seomoz.org/blog/captchas-affect-on-conversion-rates)
*   [F**k CAPTCHA](https://www.90percentofeverything.com/2011/03/25/fk-captcha/)

A simpler approach that won’t lower your conversion rate is to use a hidden and required text field generated with client-side Javascript. Spambots can’t fill in the field because they can’t interact with objects in client-side JavaScript; only users can. This method is simpler and less intrusive and so will reduce spam without hurting your conversion rate. The only problem is that it relies on JavaScript to work which might be suboptimal in some cases. You could also use <a href="https://haacked.com/archive/2007/09/11/honeypot-captcha.aspx">Honeypot Captcha approach</a>: you can create a honeypot form field that should be left blank and then use CSS to hide it from human users, but not bots. When the form is submitted, you check to make sure the value of that form field is blank. If it isn’t, then you can safely ignore the submission because it was submitted by a spam bot.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/550ef4ab-debb-4fb4-b7ac-c9138e14145e/javascript-captcha.png"><img loading="lazy" decoding="async" class="99150" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/550ef4ab-debb-4fb4-b7ac-c9138e14145e/javascript-captcha.png" alt=" " width="455" height="145" /></a><figcaption>Combat spam by hiding a text field with JavaScript.</figcaption></figure>

{{% ad-panel-leaderboard %}}

## Simplifying Log-Ins

The purpose of every log-in form is to get the user into their account. Some log-in forms do this better than others. Here are a few innovative techniques that will help your users log in more efficiently.

### Allow Users to Log in With Their Email Address

Remembering an email address is easier than remembering a user name. User names can be unwieldy, and people remember their email address because they use email all the time. Give users the option to log in with their email address as well as a user name. The flexibility could save them the time and headache of recovering the user name if they forget it.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0ad4c2df-f92e-4c29-bd5c-faec8b7d0278/email-login.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0ad4c2df-f92e-4c29-bd5c-faec8b7d0278/email-login.png" alt=" " width="283" height="102" /></a><figcaption>Allow users to log in with their email address.</figcaption></figure>

### Log Users in Without Leaving the Page

Logging in is a common task, and users will want to be able to log in from anywhere on your website. So, as soon as they do it, redirect them back to the current page. This will make logging in faster and allow users to get right back to their task.

There are a couple of ways to make this happen: a drop-down box or a modal window.

The drop-down box will open without taking users off the page. It takes up only a small part of the page, making it a fast and lightweight option.

*   [A Simple and Effective jQuery Dropdown Login Form](https://thefinishedbox.com/freebies/scripts/jquery-dropdown-login/)
*   [jQuery Drop Down AJAX Sign In Form](https://www.jqeasy.com/jquery-drop-down-ajax-sign-in-form/)

<figure><a href="https://www.wsj.com"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/517d9b01-cf22-4727-9e53-fa1e67c14476/dropdown-login.png" alt=" " width="358" height="203" /></a><figcaption>Drop-down box to log in without leaving the page.</figcaption></figure>

A modal window also keeps users on the current page, but it opens up at the center of the window, putting the focus entirely on the log-in form. This option gives you room to add supplemental information to the form.

*   [How to Implement a jQuery AJAX Login Form Into a Modal Box](https://www.bitrepository.com/ajax-login-modal-box.html)
*   [Simple jQuery Modal Window Tutorial](https://www.queness.com/post/77/simple-jquery-modal-window-tutorial)

<figure><a href="https://www.cnn.com"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d4714b1e-8b63-48a5-8d6f-db95f6f378e6/modal-login.png" alt="" width="467" height="287" /></a><figcaption>Modal window to log in without leaving the page.</figcaption></figure>

### Auto-Focus the First Text Field

Once the user sees the log-in form, they’ll be ready to log in. Make the process more efficient by automatically focusing on the first field. This saves them the time and effort of hovering and clicking. The user can keep their hands on the keyboard and start typing away. The auto-focus should also clearly highlight the text field so that the user knows they can start typing.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3828a74d-83ac-4dd8-8403-350e3f92773d/picture-1.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3828a74d-83ac-4dd8-8403-350e3f92773d/picture-1.png" alt=" " width="322" height="136" /></a><figcaption>Auto-focus the first text field.</figcaption></figure>

### Allow Users to Unmask Their Password

This option is almost as useful for logging in as it is for signing up. If users can’t see the characters in the field, they could easily mistype the password. If their input is rejected, they’ll know that they mistyped something and will have to re-enter their password until they get it right.

The problem is that users don’t know which character was mistyped and so can’t fix the mistake before submitting the form on the first attempt. This creates more work than necessary and makes users slow down their typing. Avoid this by adding a checkbox that allows users to unmask their password before submitting it.

*   [Stop Password Masking](https://www.useit.com/alertbox/passwords.html)

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a05f755b-2d9b-47e5-8453-f40a6a57949c/login4.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a05f755b-2d9b-47e5-8453-f40a6a57949c/login4.png" alt=" " width="487" height="69" /></a><figcaption>Allow users to unmask their password.</figcaption></figure>

### Use a Question Mark Icon for the Password Recovery Link

Users should have no trouble finding the password recovery link on your form. Instead of using a “Forgot your password” link, consider using a simple question mark button, which won’t take up a lot of room or get lost among other links. Because the question mark is a universal symbol for help, users will not wonder where to go when they’re having password trouble.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a5a64cbe-2a80-4ade-99dc-772fb4eb26db/login5.png" alt="" width="216" height="97" /></figcaption>Use a question mark icon for the password recovery link.</figcaption></figure>

### Make the “Submit” Button as Wide as the Text Fields

The log-in button isn’t just for taking action: it also lets users know what action they’re about to take. A small log-in button has weak affordance and can make users feel uncertain about logging in.

A wide button gives users more confidence and is hard to miss. The button’s label also becomes more visible, so that users are clearer about the action they’re taking.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2a2db8a1-a695-4ae0-9a52-4e31551d907e/account-login.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2a2db8a1-a695-4ae0-9a52-4e31551d907e/account-login.png" alt=" " width="216" height="155" /></a></figcaption>Make the “Submit” button as wide as the text fields.</figcaption></figure>

### Allow Users to Log in Via Facebook, Twitter or OpenID

Nearly everyone has a Facebook, Twitter or OpenID account, and letting them log in with it brings big benefits. They can use your website almost instantly, without having to go through the sign-up process. Also, they won’t have to manage multiple user names and passwords across different websites.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0981046a-cca3-4520-890f-5f533a303e32/social-logins.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0981046a-cca3-4520-890f-5f533a303e32/social-logins.png" alt="" width="250" height="150" /></a></figcaption>Allow users to log in via Facebook, Twitter or OpenID.</figcaption></figure>

Of course, you could even go further and use Facebook Connect to actually prefill data that your users might have to type; in the example below, on <a href="https://www.friend.ly/">Friend.ly</a>, a Facebook application, the only thing that the user needs to do before starting using the service is just click on the "Register" button. The information about the user is loaded automatically which raises a huge privacy concern. You might not want to use this approach in practice.

<figure><a href="https://www.friend.ly/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/72133281-76f3-452e-93c8-dbb8dfc3a16e/facebook-vitaly2.jpg" alt=" " width="560" height="303" /></a></figcaption>Use Facebook Connect to actually prefill data.</figcaption></figure>

## Conclusion

Your sign-up and log-in forms shouldn’t make the user’s life difficult. Spending time filling out a form is no one’s idea of a party. These innovative techniques will make your forms simple and efficient, so that users can sign up and log in quickly and start enjoying your content. For further ideas and examples, you might want to consider taking a look at Joshua Johnson’s article <a href="https://designshack.co.uk/articles/inspiration/20-great-sign-up-form-examples-to-learn-from">20 Great Sign Up Form Examples to Learn From</a>.

{{% ad-panel-leaderboard %}}

### Further Reading

*   [Logins, Menus, Toggles And Other Fancy Modules](https://www.smashingmagazine.com/2016/04/inspiring-ui-demos-logins-menus-toggles-and-more/)
*   [New Approaches To Designing Log-In Forms](https://www.smashingmagazine.com/2011/08/new-approaches-to-designing-login-forms/)
*   [Better Password Masking For Sign-Up Forms](https://www.smashingmagazine.com/2012/10/password-masking-hurt-signup-form/)
*   [How To Log In To WordPress Using A Social Network](https://www.smashingmagazine.com/2012/05/login-wordpress-using-social-network/)

{{< signature "vf, ik, al, mrn" >}}
