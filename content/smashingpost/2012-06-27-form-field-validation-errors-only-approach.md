---
title: 'Form-Field Validation: The Errors-Only Approach'
slug: form-field-validation-errors-only-approach
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4bac4d94-e34e-4e15-9a78-3cbf568f2efd/coversml.jpg
date: 2012-06-27T12:13:19.000Z
author: christian-holst
description: >-
  Error pages for form-field validation are dreadful. You’ve just filled out 20
  form fields, yet you get the same bloated page thrown back in your face
  because a single field failed to validate. I clearly recall the often loud
  **sighs of despair** during our last usability study each time a test subject
  encountered a validation error page.
categories:
  - UX
  - Forms
  - Usability
  - Interaction Design
---
Error pages for form-field validation are dreadful. You’ve just filled out 20 form fields, yet you get the same bloated page thrown back in your face because a single field failed to validate.

I clearly recall the often loud <strong>sighs of despair</strong> during our last usability study each time a test subject encountered a validation error page.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Web Form Validation: Best Practices and Tutorials](https://www.smashingmagazine.com/2009/07/web-form-validation-best-practices-and-tutorials/)
*   [Useful Ideas And Guidelines For Good Web Form Design](https://www.smashingmagazine.com/2011/06/useful-ideas-and-guidelines-for-good-web-form-design/)
*   [Web Form Design: Showcases And Solutions](https://www.smashingmagazine.com/web-form-design-showcases-and-solutions/)

We also noticed that test subjects who had been exposed to validation errors began to take <strong>preventive actions</strong> to avoid them in subsequent steps, by writing things such as “N/A” in the “Company name” field if in doubt about whether the field was optional.

{{% feature-panel %}}

<a href="https://www.bluenile.com/"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="112731" title="Form Field Validation Error Page at BlueNile.com" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2214f7b5-0177-40ed-bac9-6a628d52fe96/1-validation-error-blue-nile.png" alt="Form Field Validation Error Page at BlueNile.com" width="500" height="257" /></a><br>
<em>When getting the exact same page but with an error message, the user will feel they have made little or no progress, despite having typed 90% of the form fields correctly. (Image: <a title="Blue Nile" href="https://www.bluenile.com/">Blue Nile</a>)</em>

Some of the frustration with validation error pages likely stems from the user being returned to the same page they came from. Being returned to the exact same page is problematic for a couple of reasons:

1.  With all form fields still displayed (valid or not), the user might have difficulty **identifying the few** erroneous fields among the many valid ones.
2.  More critically, seeing the same page twice makes it seem like the user has made **no progress**, despite having just filled in numerous form fields correctly.

At Baymard Institute, we reflected on this problem and got an idea that we call “error fields only” — which is exactly what this article is about. Before exploring this idea, let’s look at three traditional types of validation techniques: “same page reload,” “optimized same page reload” and “live inline validation.”

## 1\. The Traditional Way: Same Page Reload

Here's a typical validation error page from Staples’ checkout process:

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1e4f8adc-635f-4a42-8d1d-387a21fb2127/2-staples-validation-error-full.png"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="112732" title="Staples validation error" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a662b694-9f36-4b10-a7f3-169810ed679c/2-staples-validation-error.png" alt="Staples validation error" width="500" height="793" /></a><br>
<em>The current error page for Staples’ checkout process. Besides having a subpar indication of errors, <a title="Staples" href="https://www.staples.com/">Staples</a> also breaks a handful of <a href="https://www.smashingmagazine.com/2011/04/06/fundamental-guidelines-of-e-commerce-checkout-design/">checkout usability guidelines</a>.</em>

When the user first submits the page, the entire page is reloaded, but with indications of validation errors. A message at the top of the page tells the user they have made an error and describes what the error is; further down the page, the label for the erroneous field is in bold and red.

This is significantly better than the sad practice some websites adopt of only highlighting the erroneous field in red or bold (without any description) and letting the user guess what went wrong. But the implementation could be much more thorough. Let's look at how Staples’ page could be improved.</p>

## 2\. Same Page Reload: Optimized

To have a fairer baseline for comparison, we’ve made three changes to substantially improve Staples’ error page:

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f98c0712-91c7-41bc-8c73-f1d13d8c1390/3-optimized-staples-validation-error-full.png"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="112733" title="Mock-up of an optimized Staples validation error page. Click for full size." src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c3239cc2-6c18-4a83-a10a-844449fc7970/3-optimized-staples-validation-error.png" alt="Mock-up of an optimized Staples validation error page. Click for full size." width="500" height="790" /></a><br>
<em>A simple mockup of an optimized version of Staples’ error page. Notice the anchor link at the top and the tailored description near the erroneous fields.</em>

The three changes are:

1.  The error description at the top indicates the number of errors (if there's more than one) and lists them.
2.  These listed errors are links that take the user directly to the corresponding field (especially important in long forms).
3.  A tailored message for each erroneous field shows either an example of correctly formatted data (for example, `john@example.com`) or a tip on what might be wrong with the data (for example, “Looks like the ending in the email address you provided is missing (.com, .org, etc.),” instead of just “Email wrong — please correct.”

Now, in addition to being able to locate the erroneous fields and spot multiple errors more easily, the user actually has guidance on how to correct their data. Some input errors are plain cases of mistyping or obvious details being forgotten, which most users will spot immediately; but if the user lacks clues and can’t instantly see why the data is invalid and has to guess in order to proceed, then they will likely abandon the process.

While better, this second implementation (and the first) <strong>still result</strong> in a poor experience. The user still gets the whole page with all 31 form fields thrown back at them, despite having inputted 90% of the fields correctly. The signal-to-noise ratio is still high (two errors among all valid fields). The user will likely scroll up and down the form to make sure all errors have been fixed and, finally, scroll down to click that “Continue” button once again. This diminishes the user’s sense of accomplishment and makes their effort to resolve the errors unnecessarily cumbersome.</p>

## 3\. Live Inline Validation

A very effective technique that resolves some of the issues with the last method is “live inline validation.”

<a href="https://twitter.com"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="112734" title="Twitter use Live Inline Validation at their sign-up page. Image credit: Twitter.com" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4302bfde-3125-4705-b486-c53196f40bb5/4-inline-validation-twitter.png" alt="Twitter use Live Inline Validation at their sign-up page. Image credit: Twitter.com" width="500" height="358" /></a>

Here, each form field is <strong>validated separately</strong> as the user types. The error handling is most often instant, with the user being told that their data doesn't match the expected format (although the user can scroll past and try to submit the form anyway). Luke Wroblewski has done some excellent usability research on the <a href="https://www.alistapart.com/articles/inline-validation-in-web-forms/">inline validation techniques</a> that work best.

Inline validation alleviates the aforementioned issues by indicating progress and by pointing out the erroneous fields (since the page does not reload). This makes the technique useful for forms in which the fields can be validated independently. In other cases, the data isn’t as simple as a user name, password and email address; sometimes the data needing validation is an array or a set of data. In the realm of e-commerce, one might need an address or credit card to be validated.

To live validate a credit card, you could perform a <a href="https://en.wikipedia.org/wiki/Luhn_algorithm">Luhn check</a> to verify the format of the number, and you could verify the expiration date and security code (or “card verification value”) for the correct number and type of characters. However, the validation could still fail if the data doesn't all match up when the payment vendor tries to authorize the card or if the card is declined. With live inline validation, the user would be first presented with a green checkmark as they input data in each field, and then they would see an error message after submitting the form if any of the fields didn’t check out. Alternatively, live inline validation could be disabled for just those fields for which the data has to be checked remotely. However, this has the drawback of an <strong>inconsistent UI</strong>, whereby some fields are validated live while others aren’t.

For address validators, the format of the inputted data could be correct, but the address itself could still fail validation (for example, if the address doesn't exist). Again, live inline validation would begin here with checkmarks indicating to the user that the inputted data is correct, but then, when the user submits the address form, the website would (confusingly) change its mind and tell the user that it doesn’t recognize the address after all.

Our suggested approach, the fourth and last validation technique, tackles these problems.</p>

## 4\. Error Fields Only Approach

As we’ve seen, there are different ways to display error messages, each with its own strengths and weaknesses. Based on these observations, we thought of a validation technique better suited to complex data. What if we removed all validated fields on the error page that reloads? What if we displayed only those fields that <strong>failed validation</strong>? So, instead of reloading the entire page and showing all 20 fields of the form when only the “Phone” and “Email” fields have errors, you would simply show a page with those two fields and the corresponding messages.

With this approach, the picture is quite different. The user now gets a new page, or an overlay, with just a <strong>couple of error fields</strong>. A summary of the validated data would also be displayed, along with an “Edit” link in case the user spots something they want to correct. Staples’ error page would then look something like this:

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/31a34044-0a49-4eed-adf1-58ba413f71b3/5-error-fields-only-mockup-full.png"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="112735" title="Mock-up of Error Fields Only approach" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ce22cd2b-9070-4057-9315-99107d1a815d/5-error-fields-only-mockup.png" alt="Mock-up of Error Fields Only approach" width="500" height="331" /></a><br>
<em>A simple mockup of what Staples’ error page would look like with this fourth approach. Only erroneous fields would be shown, and all validated data would be summarized below with an “Edit” link.</em>

This approach makes the error page much <strong>more digestible</strong> than the traditional technique, and it makes abundantly clear which fields are the problem, which is particularly helpful in long forms.

Now, the user simply has to fix the fields shown and hit “Continue” — no scrolling, no having to pick out erroneous fields from valid ones, no repetition of the same page, just a simple page explaining exactly what to fix and how to proceed.

## When To Use Each Validation Technique

Compared to the two traditional reloading techniques (i.e. 1 and 2), the “live inline validation” and “error fields only” techniques both offer the user a sense of progression and a clear distinction between erroneous and valid fields.

The “error fields only” approach is usually best when inline validation wouldn’t quite work. In April 2012, we benchmarked the top 100 e-commerce websites in the world and found that <strong>only 8%</strong> use live inline validation during checkout (likely due to having to validate both postal addresses and credit cards). In general, the longer the form and the more complex the inputted data and its dependencies, the more likely the error-fields-only approach is the best choice.

Inline validation is effective for simpler forms. When the data is an array or set, such as with postal addresses and credit cards, then the method becomes problematic. In this case, the UI would be illogical (the user would see each field validated individually and then suddenly fail collectively) or inconsistent (only some fields would validate as the user types). Of course, this technique would still require the page to be reloaded as a fallback, in case the user submits the form regardless of inline error messages (or if they have disabled JavaScript); therefore, the page reload techniques (the traditional and newer versions) might be best even for simple forms.

On smartphones, the error-fields-only approach has an advantage over the same-page-reload technique, because users typically lack an overview and context of the form due to the small screen. In such cases, displaying only the erroneous fields would help the user focus on the task at hand.</p>

## Rethinking Validation Error Pages

The error-field-only approach is <strong>merely a concept</strong>, and it needs both refinement and testing. An even better solution to these user experience problems most likely exists. Maybe having a traditional (although optimized) error page with green checkmarks next to the validated fields on the error page (to indicate the user’s progress) would be a better solution; or perhaps applying a slight fade to validated fields, making the erroneous ones stand out, while maintaining the context of the page.

The error-fields-only approach is more an attempt to inspire and a call to action to rethink how we handle validation errors and thus provide a better user experience.

While we can agree that validation pages aren’t the sexiest part of Web design, we should give them attention because their quality will determine whether the user comes to a screeching halt or feels a small bump on the road.

Got your own examples, mockups and ideas for validation errors? Share them in the comments!

{{< signature "al" >}}

