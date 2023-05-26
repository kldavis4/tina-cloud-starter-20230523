---
title: 'Web Form Validation: Best Practices and Tutorials'
slug: web-form-validation-best-practices-and-tutorials
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0bfcb629-42b5-463e-89af-784dc998b982/validation.jpg
date: 2009-07-07T16:39:43.000Z
author: janko-jovanovic
description: >-
  Ideally, users will fill the web form with necessary information and finish their job successfully. However, people often make mistakes. This is where **web form validation** comes into play.
categories:
  - Forms
  - Design
  - Web Design
  - Captcha
  - Validation
---
The goal of web form validation is to ensure that the user provided necessary and properly formatted information needed to successfully complete an operation. In this article we will go beyond the validation itself and explore different validation and error feedback techniques, methods and approaches. 

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Form-Field Validation: The Errors-Only Approach](https://www.smashingmagazine.com/2012/06/form-field-validation-errors-only-approach/)
*   [Useful Ideas And Guidelines For Good Web Form Design](https://www.smashingmagazine.com/2011/06/useful-ideas-and-guidelines-for-good-web-form-design/)
*   [Web Form Design: Showcases And Solutions](https://www.smashingmagazine.com/web-form-design-showcases-and-solutions/)
*   [Improve The User Experience By Tracking Errors](https://www.smashingmagazine.com/2011/10/improve-the-user-experience-by-tracking-errors/)

## Validation methods

User's input can be validated on the server and on the client (web browser). Thus we have server-side and client-side validation. We'll discuss pros and cons of each.

{{% feature-panel %}}

### Server-side validation

In the server-side validation, information is being sent to the server and validated using one of server-side languages. If the validation fails, the response is then sent back to the client, page that contains the web form is refreshed and a feedback is shown. This method is secure because it will work even if JavaScript is turned off in the browser and it can't be easily bypassed by malicious users. On the other hand, users will have to fill in the information without getting a response until they submit the form. This results in a slow response from the server.

The exception is validation using <strong>Ajax</strong>. Ajax calls to the server can validate as you type and provide immediate feedback. Validation in this context refers to validating rules such as username availability. You can read more about validation with Ajax in this excellent tutorial on jQueryForDesigners.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/16441230-f61c-4a68-bd06-9ea32076c12d/validation.png" alt="Yahoo! sign-up form" width="500" height="417" /><br>
<figcaption>This diagram shows differences between client-side and server-side validation and other techniques.</figcaption></figure>

### Client-side validation

Server-side validation is enough to have a successful and secure form validation. For better user experience, however, you might consider using client-side validation. This type of validation is done on the client using script languages such as JavaScript. By using script languages user's input can be validated as they type. This means a more responsive, visually rich validation.

With client-side validation, form never gets submitted if validation fails. Validation is being handled in JavaScript methods that you create (or within frameworks/plugins) and users get immediate feedback if validation fails.

Main drawback of client-side validation is that it relies on JavaScript. If users turn JavaScript off, they can easily bypass the validation. This is why validation should always be implemented on both the client and server. By combining server-side and client-side methods we can get the best of the two: fast response, more secure validation and better user experience.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/51fadb60-6628-4bf2-ab2c-651e227b5404/typepad-validation2.png" alt="Typepad sign-up form" /><br>
<figcaption>Rich, instant validation feedback is done on the client on TypePad</figcaption></figure>

## What to validate

There are several different types of validation you can perform: required fields, correct format and confirmation fields.</p>

### Required information

The first and most obvious information that should be validated is required information – information without which operation cannot be completed successfully. Thus, validation has to ensure that the user provided all the necessary details in the web form and it has to fail if at least one of the fields is not provided. Required fields should be clearly marked in order to inform users about what information has to be provided up front.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7e339000-4ee9-4d5d-b6ee-3e7f96086711/komodomedia-required.png" alt="Komodo Media comment form" /><br>
<figcaption>Required fields on Komodo Media blog comment form are marked with "required" help text.</figcaption></figure>

A common way to mark required fields is with an <strong>asterisk (*)</strong>. However, not all users know the meaning of an asterisk sign. Beginners or older users are very likely to have only a general idea of what an asterisk might mean. This is the reason why it is a good practice to either put a note on the top of the form that indicates that all fields marked with an asterisk are required or to use required field markers. In case that all fields are required there is no need to place asterisks or markers in the form. A simple message that all fields are required is enough.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/02efc71c-1d77-47c5-96ff-5d9f627f0177/facebook-required.png" alt="Facebook sign-up form" /><br>
<figcaption>Facebook doesn't provide information about required fields. Users get information that all fields are required only after they press the "submit"-button.</figcaption></figure>

Last year, we conducted an <a href="https://www.smashingmagazine.com/2008/07/04/web-form-design-patterns-sign-up-forms/">survey on Web form design</a>. According to that survey "designers tend to remove all unnecessary details and distractions which don't help the user to complete the form". More detailed analysis showed a trend of using very few mandatory fields – more than 50% of forms used at most 5 mandatory fields, while optional fields were often avoided. This can be useful to you when deciding on required fields.</p>

### Correct format

Apart from ensuring that users provide necessary information, validation has to ensure that users provide information in the correct format. This applies to various cases such as email address, URL, dates, phone numbers and others. If the information is not in the correct format, users should be informed and correct format should be suggested. Probably the easiest way to validate the "correct" formatting is to use regular expressions.

Please notice that it is often a good idea to <strong>not impose a strict input pattern on the users</strong>; it's better to actually permit users to enter text in a variety of formats and syntaxes, and make the application interpret it intelligently. The user just wants to get something done, not think about "correct" formats and complex UIs. Let the user type whatever he needs, and if it's reasonable, make the software do the right thing with it. This design pattern is also often called <a href="https://designinginterfaces.com/Forgiving_Format">forgiving format UI design pattern</a>.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/272b6060-2af3-45f8-bcd3-b88e488ab910/carbonmade-format.png" alt="Carbonmade sign-up form" /><br>
<figcaption>Carbonmade sign-up form validates URL format, informs the user about the error and provides ways to correct it.</figcaption></figure>

To learn more about regular expressions be sure to read <a href="https://www.smashingmagazine.com/2009/06/01/essential-guide-to-regular-expressions-tools-tutorials-and-resources/">Essential Guide To Regular Expressions: Tools and Tutorials</a> or if you already know the basics: <a href="https://www.smashingmagazine.com/2009/05/06/introduction-to-advanced-regular-expressions/">Crucial Concepts Behind Advanced Regular Expressions</a>. We'll discuss some other format techniques later in the article.</p>

### Confirmation fields

When dealing with data that is important to the system, it is a good practice to let the users confirm their input using additional confirmation fields. This way users can be certain that they provided correct information. A typical case when confirmation field is used is for passwords, but it can be used in other cases like an email address.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4d251485-a15f-4fde-98b4-6acad4479b20/photobucket-confirmpassword.png" alt="Photobucket sign-up form" /><br>
<figcaption>Photobucket sign-up form required users to re-type password they previously entered in order to ensure it has been correctly entered.</figcaption></figure>

A confirmation field should be placed next (or below) the target field. It has to clearly describe the purpose of the field such as "Confirm your password". If two values do not match, the user should be informed. As an option, you can use a success indicator if values DO match.</p>

<a href="https://www.smashingmagazine.com/2008/07/08/web-form-design-patterns-sign-up-forms-part-2/">The second part of our survey</a> shows interesting information about confirmation fields. Email confirmation was mandatory in only 18% of sites, while password confirmation was mandatory in 72% of web sites. Surprisingly, large websites such as Facebook, LinkedIn, Stumbleupon and Twitter don't require password confirmation.

## Validation feedback

If validation fails, the system should let the users know it by providing a clear and unambiguous message (usually one or two sentences) and ways to correct errors. Since users need to notice an error message immediately, it is a good practice to position it at the top of a web form, before all the other fields. This will also allow screen readers to easily access the message.

The message should be shown preferably in red since this is the color that people usually associate with errors and it should contain an appropriate icon in order to get more attention. Icon should be globally recognizable, such as a red circle with white cross. This will also help people with visual impairments identify the meaning of the message. In addition to this, users should be informed about which input fields need to be checked.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4a9517e2-317d-4326-9d49-d0c75e2416cc/invoice-machine-feedback.png" alt="The Invoice Machine sign-up form" /><br>
<figcaption>The Invoice Machine Sign-up form doesn't provide error feedback. Error message is missing and input fields are colored with pastel red that is not easy to spot.</figcaption></figure>

Apart from the error message and a list of invalid fields, the system should clearly mark fields that are invalid. This can be done in one of the following ways (or any combination of them):

*   By providing red inline messages or markers next to every invalid field
*   By changing the background color or border color of invalid fields (to red)
*   By changing the color of field labels
*   By providing error tips (balloons) next to each field

If you provide error tips or help, be short and informative. For example, if date is in an incorrect, format provide users with details on how to format it properly: "The date should be in the <em>dd-mm-yyyy</em>-format". It is sometimes also a good idea to have these hints as the initial value of your input fields. Thus, the user will first read the hint inside the input box and when he/she will start typing the data, the hint will disappear.</p>

### Validation upon submit

The "classic" way to perform validation is when the <strong>user submits his data via the "submit"-button</strong>. The validation is executed and if any errors are found, feedback is returned and displayed to the user. This way users will be able to fill the form without any interruptions. But, that could be a disadvantage as well. Users will be able to fix the errors only after they try to submit the form and get the response back from the server. This technique is typical for server-side validation, but can also be done on the client side.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dd5386c7-63b0-447c-9090-1fee64eea64c/ballpark-feedback.png" alt="Ballpark sign-up form" /><br>
<figcaption>Feedback on Ballpark sign-up form occurs upon submit. It shows an obvious error message with incorrect fields at the top of the form and marks each incorrect field with a tip.</figcaption></figure>

### Real-time validation (or instant validation)

In contrast to the previous technique, <strong>real-time-validation alerts users while they are filling in the form</strong>. That doesn't necessarily mean that the validation is performed on every single key press but rather when a field loses focus. This way users will get immediate feedback about their input, e.g. if a username is available or if a date is in the correct format. Obviously, instant validation occurs during typing in an input field or after the input field loses focus. Usually, it is complemented with a text message, tip or a status icon.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c88083f8-a24a-4b0f-b411-6a6171217d70/yahoo-paswordstrength.png" alt="Yahoo! sign-up form" /><br>
<figcaption>Yahoo registration form implements password strength meter that gives feedback as you type in the letters.</figcaption></figure>

Instant validation should be implemented carefully and in appropriate cases because it might be distracting if overused or misused.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/80ada6ae-142e-42e7-979c-90af18b0078d/typepad-validation.png" alt="Typepad sign-up form" /><br>
<figcaption>Sign-up form on TypePad not just provides instant validation feedback that informs users of different validation errors – it also indicates successfully entered information.</figcaption></figure>

### What to avoid?

There are two things you should really try to avoid when designing form validation. First, <strong>single error pages are bad practice</strong>. Singe error page means that users are redirected from the Web form they filled to a page that shows some feedback. In this case, users are forced to browse back in order to fix errors. When they browse back they will have to memorize the information you provided in the error message. The same applies to feedback messages in popup windows. Not only are popups annoying, but once they are closed all the feedback is lost.

An interesting finding in <a href="https://www.smashingmagazine.com/2008/07/08/web-form-design-patterns-sign-up-forms-part-2/">the second part of SM survey</a> is that "30% of the forms displayed only an error-message at the top of the form (no input fields were highlighted)" while "29% had highlighted input fields with corresponding messages next to the input field (no error-messages were provided at the top of the page)". Only 25% used both error-messages and input fields.

Probably the most surprising facts are that 14% of sites still use JavaScript popup for showing validation feedback, while Ajax validation is present only on 22% of sites. This shows big variations in validation feedback.</p>

## Better safe than sorry

Apart from the pure validation, there are several techniques that can help users make fewer mistakes. Although not all of these techniques can be considered validation, they do help by guiding users and preventing them from making mistakes.</p>

### Help hints

If a web form requires complex information to be filled in, help hints can significantly help users in the process of filling in the correct information. By guiding them how to fill particular information, you let them fill the form faster and avoid potential validation errors. Help hints are usually shown as simple text next to or above the input field. The design of help hints should differ from the design of form labels. It is usually shown in smaller, grayed text. The advantage of help information is that it is always visible to the user even if JavaScript is turned off.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1e0e5367-3eb7-48d0-950f-86ebad020e1d/hints.jpg" alt="Wishlistr sign-up form" width="540" height="289" /><br>
<figcaption>WishListr provides useful help information on the right side of each field.</figcaption></figure>

### Help indicators (tooltips)

In contrast to help hints, tooltips initially hide information and make it visible "on demand". They are usually triggered by an icon with a question mark. Help information is shown by hovering over the help icon or clicking on it. Once the mouse is moved away from the icon, the tooltip disappears. Help indicators can reduce clutter, especially if help text is too long.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/48b5d52b-d25a-4489-9af5-33d87be65b28/ticket-trunk-help.png" alt="TicketTrunk sign-up form" /><br>
<figcaption>Sign-up form on TicketTrunk contains obvious help indicators that provide help information on hover.</figcaption></figure>

### Dynamic tips

Similar to the previous case, dynamic tips are initially not visible to users. Once the user enters a particular input field, related tip is shown. This way tips are emphasized and clutter in the form is reduced. Tips should be shown in such a way that they don't cover other information on the form. They are usually shown next to input fields, but you should always try to place them on the right side of the fields since that is less distracting.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ed98dc1f-6e15-4017-8a8e-55be00e87b43/digg-tips.png" alt="Digg sign-up form" /><br>
<figcaption>Digg registration form has discrete dynamic tips that show help information related to the field that has the focus.</figcaption></figure>

### Masking and reformatting user's input

Apart from validating user's input and assisting users, web applications can also take part in providing correct data by formatting user's input. This can be done by masking input fields in order to force users to enter information in an appropriate format. Mask is an expression that controls what users can enter in an input field. Masking can be implemented easily with one of the following plugins:

*   [iMask](https://zendold.lojcomm.com.br/imask/)
*   [TypeCast](https://typecast.arapehlivanian.com/index.html)
*   [jQuery Masked input plugin](https://digitalbush.com/projects/masked-input-plugin/)

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/41eb5a96-c160-466e-9bd1-0b010b6d1587/typecast-masks.png" alt="TypeCast masking demo" /><br>
<figcaption>Typecast demo page shows different masking options.</figcaption></figure>

In some cases users might fill partially correct information or correct information but in different format. In those cases web application can provide a mechanism to correct and rewrite the user's input. Some of the possible scenarios when you might consider rewriting user's input are:

*   if, for instance, a user enters URL without "https://" prefix, the system can just add this string to the beginning of URL.
*   if a user provides data in the _dd-mm-yyyy_-format, but the required format is _yyyy-mm-dd_, the system can rewrite the date so it is well-formed
*   if a user provides credit card number without dashes, the system can add dashes to appropriate positions in the credit card number

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/87610b36-f410-4bc8-b7e0-2d7bdf0d77e3/tumblr-masking.png" alt="Tumblr sign-up form" /><br>
<figcaption>Tumblr provides a sort of masking for URL.</figcaption></figure>

These ideas are just some of the cases when this technique can be used. However, auto-formatting should be used carefully and – if not used properly – can be confusing to users. Also, not all user's input is predictable. If, for example, user enters "www.smashingmagazine" and omits the extension, the system can't assume that the extension is ".com", but should rather raise a validation error.

In this context it's again worth mentioning the "forgiving format" design pattern. Instead of restricting user's input to a specific format you can allow users to provide various formats and let the system parse it. In many cases this would require a lot of server processing; back-end would be responsible for parsing the input, extracting information and converting it to appropriate formats for further processing.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/166cfef5-d186-4830-addd-d3e258dae9db/google-calendar-format.png" alt="Google calendar" /><br>
<figcaption>Google Calendar has a very clever implementation of this technique with one-field for adding events. Users can enter information in various formats (even use "tomorrow" instead of date); the system parses it and stores it as a new event. If user provides information that can't be parsed, system assumes that this information is event title and redirects the user to a longer version of the form with filled event name. This way Google completely omitted validation.</figcaption></figure>

According to our survey. 67% of sites use help text and tips, 10% of which use dynamic tips. Surprisingly, only 26% of tips are positioned on the right side of the fields, while in other cases tips are positioned above, below and even on the left side of input fields.</p>

## Are you human?

Web form validation wouldn't be complete without mentioning <strong>Captcha</strong>. Captcha is a significant part of validation as it is responsible for finding out if the user of a system is a human or a bot. In its simplest form, captcha consists of an image showing text, numbers or an expression and a field that expects content of the image as input. The earliest captcha generated images with numbers (e.g. "8356") and that number was expected to be entered by the user. If correct number wasn't entered (or not entered at all), the form couldn't be submitted. In fact, today most spam bots are able to recognize the text embedded in a simple captcha-image, so it's a good idea to pose some question that only humans could answer correctly, e.g. "What color does the Sun have?" with correct answer "yellow" in all its variations ("YELLOW", "yellow", "Yellow" etc.).

You may also want to consider the technique called <a href="https://haacked.com/archive/2007/09/11/honeypot-captcha.aspx">Honeypot Captcha</a> where the idea is to create hidden form elements and check on the server side that they remain blank. Another option is to create a form field with a label that says, “Leave this field blank” and then is marked as a required field (thank you, <em>Shawn McCool</em>).</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/89c59a9c-f220-49c7-aa4c-c0905bdefe0f/easy-captcha.png" alt="Captcha implementation" /><br>
<figcaption>Simple captcha requires an answer to a semantic question.</figcaption></figure>

The kind of captcha presented above caused a major problem in accessibility. Blind, visually impaired or dyslexic users have difficulties or are even impossible to complete the web form with Captchas. As the Web evolved, so did captchas and today there are implementations that have audio support for users with disabilities.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/410827ef-09c6-4946-a069-17cd79da057d/bad-captcha.png" alt="Recaptcha component" /><br>
<figcaption>Captchas can show hardly recognizable words. Can you easily read the word on the left?</figcaption></figure>

Still most users hate captchas (and there is a good reason for hating them!). Of course, people just don't like filling in forms. If they can't do it fast and effortlessly, there is a high probability that they won't do it at all. This is where a captcha doesn't help at all: it can take too much time for users to read (if text is messy) which happens oft in practice. Remember, Captcha helps site owners, not their users. Therefore it's always a good idea to avoid using Captchas if you can avoid them. To read more about Captchas and accessibility, read <a href="https://www.w3.org/TR/turingtest/">Inaccessibility of CAPTCHA</a>.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3a8431d8-6b01-4684-9897-861ed28a0d50/digg-captcha.png" alt="Captcha on Digg registration form" /><br>
<figcaption>Captcha on Digg registration form has audio support. If unable to read, users will be able to hear the letters shown in the image.</figcaption></figure>

## Useful resources

Here are some of the frameworks, plugins and tutorials that might help you easily implement validation in your forms.

*   [LiveValidation](https://developer.tizen.org/community/tip-tech/using-livevalidation-javascript-library) A small, open source JavaScript validation library. It enables real-time, rich client validation which can be implemented easily. The best way to see its capabilities is to check out the example page.
*   [Validanguage](https://www.drlongghost.com/validanguage.php) A validation framework that enables rich client-side validation.
*   [JavaScript Form Validation](https://code.google.com/p/javascriptformvalidation/) A JavaScript validation framework for creating inline validation. You can configure it through JavaScript code or by using XML configuration file.
*   [UniForm](https://www.sprawsm.com/uni-form/) An attempt to standardize form markup (xhtml) and CSS. It can help you style error messages, help text, indicators and so on.
*   [jQuery Validation plugin](https://jqueryvalidation.org/) One of the most popular validation plugins. As expected from jQuery plugin, it enables validation in one line of code, but you can also customise it. It has only 14 kb and is compatible with jQuery 1.3.2.
*   [jForm](https://frontendbook.com/projects/jform/) Another jQuery plugin that lets you implement validation easily. Not only that it performs validation but also has the support for live tips. It is still in development phase but is worth checking.
*   [Dynamic JavaScript Form Validation](https://www.scriptiny.com/2008/04/dynamic-inline-javascript-form-validation/) Provides easy validation and attractive error messages.
*   [jQuery Form Validator](https://www.position-absolute.com/articles/jquery-form-validator-because-form-validation-is-a-mess/) Another great jQuery validation plugin that performs live validation. It is fully customisable and supports localisation as well.
*   [Form field hints with CSS and JavaScript](https://www.askthecssguy.com/2007/03/form_field_hints_with_css_and.html) A useful tutorial on how to create help tips using CSS and JavaScript. Demo and source are included.
*   [PHP Contact Form with jQuery Validation](https://www.raymondselda.com/php-contact-form-with-jquery-validation/) This tutorial shows how to implement the validation of a contact form using PHP and JavaScript.
*   [How to Validate Forms on both sides using PHP and jQuery](https://www.taiijas.com/2012/04/03/how-to-validate-forms-in-both-sides-using-php-and-jquery/) Shows how to implement both client-side and server-side validation using PHP.
*   [Adding Form Validation to WordPress Comments using jQuery](https://net.tutsplus.com/tutorials/wordpress/adding-form-validation-to-wordpress-comments-using-jquery/) An interesting tutorial for all Wordpress users.</p>

## Conclusion

You saw different methods and techniques that you can use to implement validation in your forms. Although there are many possibilities, you should carefully plan validation for each project. Not all techniques provide a solution for everything. Some of them are very helpful and easy to implement, but some lack usability and simplicity. If you are new to web form design here is a short list of what to consider in Web form validation design). That might be enough for you to start.</p>

### Rules of thumbs in web form validation design

*   Never omit server-side validation.
*   Don't provide confusing validation feedback. It should clearly communicate the errors and ways to fix them.
*   Don't let users think about what information is required, always clearly mark required fields.
*   Never provide validation feedback on a single page or in a popup alert.
*   Don't use dynamic effects as compensation for a badly designed form. Fancy effects won't hide a poorly designed web form.
*   If you use Captcha, don't forget to provide audio support and enable users to "reload" the Captcha.
*   Don't forget to inform users when the form was completed successfully. It is as important as a good validation feedback.

