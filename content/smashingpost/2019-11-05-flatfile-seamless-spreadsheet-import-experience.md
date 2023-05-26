---
title: 'Build A Seamless Spreadsheet Import Experience With The Help Of Flatfile'
slug: flatfile-seamless-spreadsheet-import-experience
author: suzanne-scacca
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/628ec3da-a70b-42c9-a5b2-4af4eddd1e35/flatfile-sharing-image.png
date: 2019-11-05T12:00:59+02:00
summary: >-
  Data import has historically been a time-consuming and frustrating task, especially for products that depend on ingesting a lot of data from users. That’s why many developers include CSV importers in their apps &mdash; to spare users from having to manually copy data from a spreadsheet into their database. But let’s face it: traditional data import solutions haven’t always been great. That’s why, today, we’re going to look at how <a href="https://flatfile.com/?utm_source=Smashing-Magazine-Article-November-2019&utm_medium=Display&utm_campaign=Smashing-Magazine-11052019-Article&utm_content=Product-Variant">Flatfile</a> helps you create a better import experience for your users, team, and product.
description: >-
  In this article, we’re going to look at how Flatfile helps you create a better import experience for your users, team and product.
categories:
  - Tools
  - Workflow
disable_ads: true
disable_panels: true
disable_newsletterbox: true
sponsor:
  title: Flatfile
  link: https://flatfile.com/?utm_source=Smashing-Magazine-Article-November-2019&utm_medium=Display&utm_campaign=Smashing-Magazine-11052019-Article&utm_content=Product-Variant
  image: https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5e348e27-1a19-4e7d-a92b-150c8d0f4f70/flatfile-horizontal-logo.svg
  description: >-
    This article has been kindly supported by our dear friends at <a href="https://flatfile.com/?utm_source=Smashing-Magazine-Article-November-2019&utm_medium=Display&utm_campaign=Smashing-Magazine-11052019-Article&utm_content=Product-Variant">Flatfile</a> who create beautiful, human-centric experiences to remove the barriers between people and data. <em>Thank you!</em>
---

If you’ve ever attempted to build a CSV importer before, you know how frustrating it is to dedicate valuable engineering time to this feature, only to watch your customers struggle with it.

In some cases, developers try to improve this experience by providing users with FAQs and tutorials that show them how to correctly use their importer. However, this merely shifts the burden from the product onto the user. The last thing users want is to sift through lengthy documentation or video tutorials to upload a simple spreadsheet.

**Should it be your users’ job to figure out why your importer isn’t working correctly?**

If you want to improve the experience users have with your product or service, you have to start with optimizing the experience of importing the data itself. Users rely on your product to extract value from it. Asking them to use a spreadsheet template, or to match their fields before they've even uploaded a file to your app is detrimental to their product experience and your team's resources.

Investing developer time to fix an existing data importer, or worse, building a CSV importer from scratch is a huge strain on resources. Let's look at Flatfile, which enables developers to integrate a robust CSV importer experience in as little as one day.

## Common Problems With Typical CSV Import Experiences

Data import is often one of the first interactions users have with an app. Unfortunately, there are too many ways that this import feature can cause frustration.

For your users, an inefficient importer experience will cause them to wonder whether the product itself is worth using.

<blockquote>If the app can’t import my data easily, what the heck is going to happen once my data is finally uploaded?</blockquote>

{{< rimg href="https://flatfile.com/?utm_source=Smashing-Magazine-Article-November-2019&utm_medium=Display&utm_campaign=Smashing-Magazine-11052019-Article&utm_content=Product-Variant" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/eb219adb-6e95-4aaa-9561-7daaae27046d/14-flatfile-inefficient-import.png" sizes="100vw" caption="Do you really want you and your users to battle with these kinds of errors? (Source: <a href='https://flatfile.com/?utm_source=Smashing-Magazine-Article-November-2019&utm_medium=Display&utm_campaign=Smashing-Magazine-11052019-Article&utm_content=Product-Variant'>Flatfile</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/eb219adb-6e95-4aaa-9561-7daaae27046d/14-flatfile-inefficient-import.png'>Large preview</a>)" alt="Text: inefficient import examples from Flatfile" >}}

An inefficient data importer strains internal resources. Not only have you invested significant time trying to build what is essentially *a second product* for your app, now you’re spending time dealing with:

<ul>
  <li>Emails and support tickets from frustrated users who can’t upload their data into your system.</li>
  <li>Broken data, which your team has to manually clean before it’s usable in your database.</li>
  <li>A never-ending string of inconsistent file uploads, due to lack of data normalization.</li>
</ul>

This is generally not a good position to be in, as users expect a seamless product experience from start to finish.

Worse, all that effort you spent building your importer could have been dedicated to building core product features your users need. 

One of Flatfile’s clients spoke to them about the pain of building and maintaining a proprietary data importer for their real estate product. The client’s engineers spent about eight to ten hours *per user*, cleaning up and formatting incoming data. Sometimes these users would churn, wasting valuable development time.

There is no point in building a custom feature that's supposed to automate and streamline the import experience. Ultimately, this sets you up for maintenance headaches down the road with features that won’t scale with your product.

**Wouldn’t it be better if there was an out-the-box CSV importer that could do this on its own?**

Flatfile is what you need.

<figure><a href="hhttps://flatfile.com/?utm_source=Smashing-Magazine-Article-November-2019&utm_medium=Display&utm_campaign=Smashing-Magazine-11052019-Article&utm_content=Product-Variant"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ad39468b-6f27-423f-963f-c8962c054f8d/15-flatfile-user-frustrations-800.gif" width="800" height="" alt="Flatfile fixes data import issues" /></a><figcaption>An illustration of some of the more frustrating data import experiences users have and how Flatfile fixes them. (Source: <a href='https://flatfile.com/?utm_source=Smashing-Magazine-Article-November-2019&utm_medium=Display&utm_campaign=Smashing-Magazine-11052019-Article&utm_content=Product-Variant'>Flatfile</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fd6436de-e503-4153-a80d-12a2668424ab/15-flatfile-user-frustrations.gif">Large preview</a>)</figcaption></figure>

Let’s look at some ways that importing data has gone awry and how it can be fixed when you let Flatfile do the heavy lifting.

### Issue #1: Unclear Guidance

In some cases, users struggle with your data importer because they have no idea what to do with it. Here are some questions they may ask during a CSV import:

<ul>
  <li>Does it accept XLS, XLSX, or XML file formats?</li>
<li>What do I do if my file is 97MB in size?</li>
<li>What if my file has special characters?</li>
<li>What happens if my columns don’t match?</li>
<li>How do I fix my data? Do I need to save a duplicate CSV and upload that file instead?</li>
<li>Can I update any incorrect data during import?</li>
<li>Do I need to download a template?</li>
</ul>

Unfortunately, unless your users are tech-savvy and spend a lot of time exporting and importing spreadsheets, they’re not going to think about these things until they're ready to provide their data.

It shouldn’t be up to your users to read through or watch a 15-minute tutorial on how to import spreadsheets into your product. Developers aren't spared either. Although engineers understand the complexities of importing data into an advanced system (like <a href="https://docs.microsoft.com/en-us/azure/machine-learning/studio/import-data">Microsoft Azure</a>), there is still an exhaustive amount of content they need to understand before the first import even happens.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c4ba20d5-7e67-4f36-8503-e93e00690c59/12-microsoft-azure-training.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c4ba20d5-7e67-4f36-8503-e93e00690c59/12-microsoft-azure-training.png" sizes="100vw" caption="A highly technical product like Microsoft Azure attempts to reasonably present developer users with extensive documentation for importing data. (Source: <a href='https://docs.microsoft.com/en-us/azure/machine-learning/studio/import-data'>Microsoft Azure</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c4ba20d5-7e67-4f36-8503-e93e00690c59/12-microsoft-azure-training.png'>Large preview</a>)" alt="Microsoft Azure data import guide" >}}

Your data import experience should make it simple to upload CSV data without requiring users to take a mini course on it. The same goes for your understanding of how to build it.

Here is an example of a simplified CSV import solution for a CRM from Flatfile (you can ignore the code on the left-hand side for now):

{{< rimg breakout="true" href="https://flatfile.com/?utm_source=Smashing-Magazine-Article-November-2019&utm_medium=Display&utm_campaign=Smashing-Magazine-11052019-Article&utm_content=Product-Variant" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4974a179-123a-4239-8071-cf54a5bb5c03/18-flatfile-demo-simplify-import.png" sizes="100vw" caption="A demonstration of how Flatfile helps developers simplify and clarify CSV import for users. (Source: <a href='https://flatfile.com/?utm_source=Smashing-Magazine-Article-November-2019&utm_medium=Display&utm_campaign=Smashing-Magazine-11052019-Article&utm_content=Product-Variant'>Flatfile</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4974a179-123a-4239-8071-cf54a5bb5c03/18-flatfile-demo-simplify-import.png'>Large preview</a>)" alt="Flatfile CRM data import demo" >}}

Notice how the preview of the importer shows a welcoming, yet basic setup. Your users would instantly know to:

<ul>
  <li>Upload their data as a CSV or XLS.</li>
  <li>Match their spreadsheet columns in the next step, if needed.</li>
  <li>Click “Continue” to begin the CSV upload.</li>
</ul>

Part of this is because the standardized UI presents no obstacles while the synchronous guidance prepares users for what’s to come. This way, users won’t worry right off the bat if their data will be imported incorrectly.

### Issue #2: Maxed-out Browser Memory Limits

Let's assume that your users have successfully exported their data from another system or compiled it into a CSV file on their own. Then, they initiate an upload using your product’s data importer.

However, after watching the upload progress for what feels like an eternity, they receive the dreaded “Upload Failed” message. This isn’t all that uncommon with traditional or self-made data importers.

It’s often why online forums and website support centers contain question-and-answer like this one on <a href="https://help.go1.com/en/articles/1785527-why-has-my-csv-upload-failed">the Go1 website</a>:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/13370612-d864-403a-8488-2cfa4f7c3335/4-go1-csv-upload-fail.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/13370612-d864-403a-8488-2cfa4f7c3335/4-go1-csv-upload-fail.png" sizes="100vw" caption="Go1’s support center answers the question “Why Has My CSV Upload Failed?”. (Source: <a href='https://help.go1.com/en/articles/1785527-why-has-my-csv-upload-failed'>Go1</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/13370612-d864-403a-8488-2cfa4f7c3335/4-go1-csv-upload-fail.png'>Large preview</a>)" alt="" >}}

Or this one on <a href="https://support.nimble.com/en/articles/1571813-why-am-i-getting-an-error-message-when-uploading-my-csv-file">the Nimble website</a>:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f67ed927-ad60-4ba9-9d0d-4180b3bafe20/11-nimble-csv-upload-fail.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f67ed927-ad60-4ba9-9d0d-4180b3bafe20/11-nimble-csv-upload-fail.png" sizes="100vw" caption="Nimble’s support center answers the question 'Why am I getting an error message when uploading my CSV file?'. (Source: <a href='https://support.nimble.com/en/articles/1571813-why-am-i-getting-an-error-message-when-uploading-my-csv-file'>Nimble</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f67ed927-ad60-4ba9-9d0d-4180b3bafe20/11-nimble-csv-upload-fail.png'>Large preview</a>)" alt="Go1 provides support for CSV upload failure" >}}

Or this one from <a href="https://www.nurturehq.com/help/why-is-my-csv-file-failing-upload/">Nurture’s knowledgebase</a>:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/81e7489b-2474-4ed8-9e48-e97a9298f91a/7-nurture-csv-upload-fail.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/81e7489b-2474-4ed8-9e48-e97a9298f91a/7-nurture-csv-upload-fail.png" sizes="100vw" caption="Nurture’s Help & FAQs answers the question 'Why is my CSV file failing to load?'. (Source: <a href='https://www.nurturehq.com/help/why-is-my-csv-file-failing-upload/'>Nurture</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/81e7489b-2474-4ed8-9e48-e97a9298f91a/7-nurture-csv-upload-fail.png'>Large preview</a>)" alt="Nimble provides support for CSV upload failure" >}}

Ultimately, it falls to your users to:

<ul>
  <li>Accept that CSVs have a tendency to fail.</li>
  <li>Debug what causes a failed CSV upload.</li>
<li>Figure out how to trim back their file size, rearrange their file, or download and use the product’s template in order to complete an upload.</li>
</ul>

Why should it be up to your users to figure out why *your* data importer failed? Shouldn’t you be the one to sort out the disconnect? Or, better yet, to build an importer that works without issue?

With Flatfile, you and your users won’t have to worry about things like file sizes or formats causing problems during import. For example, Flatfile helps you manage imported data via the browser or through a server-side process, enabling you to upload large CSV files without bothering your users. Another solution provided by Flatfile comes in the form of file-splitting.

{{< rimg href="https://flatfile.com/?utm_source=Smashing-Magazine-Article-November-2019&utm_medium=Display&utm_campaign=Smashing-Magazine-11052019-Article&utm_content=Product-Variant" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/51e61887-200e-4163-b9bb-797d0f409095/13-flatfile-multi-file-uploads.png" sizes="100vw" caption="A Flatfile demo that shows how you can reliably break up and import data from multiple files. (Source: <a href='https://flatfile.com/?utm_source=Smashing-Magazine-Article-November-2019&utm_medium=Display&utm_campaign=Smashing-Magazine-11052019-Article&utm_content=Product-Variant'>Flatfile</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/51e61887-200e-4163-b9bb-797d0f409095/13-flatfile-multi-file-uploads.png'>Large preview</a>)" alt="Flatfile demo of multi-file upload" >}}

Flatfile allows users to <a href="https://flatfile.com/developers/playgrounds/?utm_source=Smashing-Magazine-Article-November-2019&utm_medium=Display&utm_campaign=Smashing-Magazine-11052019-Article&utm_content=Product-Variant">import CSV data from multiple files intuitively</a>, without dropping data or doing manual splitting.

In this demo, users are allowed to upload CSV files containing three different sets of data. Not only will this help make their files more manageable, but it’ll make it much easier for your product to ingest and organize the data on your backend.

### Issue #3: Vague Errors

It’s not just vague upload instructions or stalled imports that are going to give your users a headache.

When the error message is vague, what is the user supposed to do with that? Without a specific explanation of the problem, your users are going to be stuck having to work through every possible fix until they find one that works (if any).

Take <a href="https://confluence.atlassian.com/jirakb/error-importing-csv-file-issueid-should-not-be-null-431194331.html">this reported issue with Jira</a>:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/93f0dc7b-4572-4540-b9b1-d7d01809e56d/6-jira-error-message.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/93f0dc7b-4572-4540-b9b1-d7d01809e56d/6-jira-error-message.png" sizes="100vw" caption="Jira knowledgebase tries to help users that see the vague error message that reads “Unexpected failure occurred.” (Source: <a href='https://confluence.atlassian.com/jirakb/error-importing-csv-file-issueid-should-not-be-null-431194331.html'>Jira</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/93f0dc7b-4572-4540-b9b1-d7d01809e56d/6-jira-error-message.png'>Large preview</a>)" alt="Jira knowledgebase answer about CSV file import error" >}}

The full error message reads:

<blockquote>Unexpected failure occurred. Importer will stop immediately. Data may be in an unstable state.</blockquote>

That’s not helpful. So, not only does the developer see a message calling their data “unstable”, but now they have to work through the issue from the scant details provided on this help page. The answer actually includes this as an explanation, which we can assume is only going to add to the frustration:

<blockquote>This happens because the JIRA Importers Plugin tries to validate if the issues are valid for importing, and when the validation fails the error above is thrown.</blockquote>

Essentially, the plugin is incapable of recognizing “Required” fields outside of the ones it deems as required. But rather than transmit that message in the importer, users have to figure that out from this resource.

Not only is there no explanation for why the CSV upload failed, but it then suggests that the data importer might’ve just goofed up (which won’t reflect well on your product experience). Chances are the importer isn’t going to accept the same file twice, so why bother suggesting a retry?

**It’s not your users’ job to think here.** CSV importers should be designed &mdash; error messages and all &mdash; to make this a quick and painless experience for your users.

### Issue #4: Mapping Is Inefficient

The next source of frustration often appears when poor column-matching functionality is in place.

As an example, let’s say that a <a href="https://mailchimp.com/">MailChimp</a> user wants to load as many contact details into the email marketing software as they want. After all, it might be useful to have their business title or phone number on hand for future list segmentation.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/85f204b5-9f3d-4df2-8b69-439a744e5bba/3-mailchimp-matching.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/85f204b5-9f3d-4df2-8b69-439a744e5bba/3-mailchimp-matching.png" sizes="100vw" caption="This is how MailChimp’s CSV field-mapping system displays uploaded results. (Source: <a href='https://mailchimp.com/'>MailChimp</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/85f204b5-9f3d-4df2-8b69-439a744e5bba/3-mailchimp-matching.png'>Large preview</a>)" alt="MailChimp mapping fail" >}}

The app doesn’t recognize three of the four columns in our file. In order to keep the unmatched column data, the user has to go through each field and manually assign a matching label that MailChimp accepts.

In this case, the only column that can be edited and matched is “Customer Name”. In this example, the user is going to lose the rest of their data.

We know what you’re thinking: “Why not just provide a pre-built spreadsheet template?” However, this is hardly a solution to the problem and will only create more work and frustration for your users.

**The problem here lies within the product experience, not the user.**

Historically, this has been a difficult and expensive project to take on, but that’s where Flatfile’s machine-learning, column-matching solution comes in handy.

<a href="https://clickup.com/">ClickUp</a>, powered by Flatfile, has leveraged this for its productivity web app.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/44ff93fb-729a-4c41-80ce-ad8a8e0f22b5/16-clickup-import.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/44ff93fb-729a-4c41-80ce-ad8a8e0f22b5/16-clickup-import.png" sizes="100vw" caption="The main data import modal for users that want to import tasks and projects into ClickUp. (Source: <a href='https://clickup.com/'>ClickUp</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/44ff93fb-729a-4c41-80ce-ad8a8e0f22b5/16-clickup-import.png'>Large preview</a>)" alt="ClickUp data import page" >}}

For starters, this import modal is really well designed. Instructions are clearly provided as to what the user can upload. In addition, the manual option lets users preview what sort of data can be imported into the productivity software. This helps users preserve as much data as possible, rather than realize too late that the data importer didn’t recognize their columns and dropped the data out without any notice.

Flatfile streamlines column-matching as well:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/efd046b3-f1f9-4368-9db9-a69c78d2df49/clickup-column-names.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/efd046b3-f1f9-4368-9db9-a69c78d2df49/clickup-column-names.png" sizes="100vw" caption="Flatfile asks users to identify column names for accurate mapping. (Source: <a href='https://clickup.com/'>ClickUp</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/efd046b3-f1f9-4368-9db9-a69c78d2df49/clickup-column-names.png'>Large preview</a>)" alt="ClickUp data import column identification" >}}

This step asks users to indicate where their column names live. This way, the importer can more effectively match them with its own or add labels if they’re missing.

Next, users get a chance to confirm or reject Flatfile’s column matching suggestions:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9182d87b-a4bb-471f-bae7-097a13d8c3ee/clickup-column-matching.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9182d87b-a4bb-471f-bae7-097a13d8c3ee/clickup-column-matching.png" sizes="100vw" caption="Flatfile uses a smart column-matching system to automatically map users’ imported data. (Source: <a href='https://clickup.com/'>ClickUp</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9182d87b-a4bb-471f-bae7-097a13d8c3ee/clickup-column-matching.png'>Large preview</a>)" alt="Smart column-matching system in ClickUp data import" >}}

On the left, they’ll find the columns and labels they imported. The white tab to the right provides them with automated column matching for ClickUp. So, “Task” will become “Task name”, “Assignee” will become “Task assignee(s)”, “Status” remains as is and so on.

If one of the labels in the CSV doesn’t have any match at all, the importer calls attention to it like this:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a80bef91-de79-4480-92b6-f1ec252dc51d/clickup-column-matching-error.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a80bef91-de79-4480-92b6-f1ec252dc51d/clickup-column-matching-error.png" sizes="100vw" caption="Flatfile calls attention to labels or values that don’t have an exact match in a product. (Source: <a href='https://clickup.com/'>ClickUp</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a80bef91-de79-4480-92b6-f1ec252dc51d/clickup-column-matching-error.png'>Large preview</a>)" alt="ClickUp data import label matching" >}}

In this example, the Priority response of “High” was detected. But “Medium” was not. However, there’s no need for the user to guess what the correct replacement should be. The importer provides relevant options like “Urgent”, “Normal” and “Low” to replace it with.

Once all spreadsheet labels have been resolved, the user can easily “Confirm Mapping” or discard the column altogether if it’s proven unnecessary.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0730895a-c8a0-49b7-b4b2-817c38294061/clickup-confirm-mapping.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0730895a-c8a0-49b7-b4b2-817c38294061/clickup-confirm-mapping.png" sizes="100vw" caption="Users get a chance to confirm CSV labels and clean up the spreadsheet results before importing their data. (Source: <a href='https://clickup.com/'>ClickUp</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0730895a-c8a0-49b7-b4b2-817c38294061/clickup-confirm-mapping.png'>Large preview</a>)" alt="" >}}

Finally, users get a chance to review any errors detected with their data:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0e3ee9a7-3083-405d-a801-37d93e904b30/clickup-review-errors.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0e3ee9a7-3083-405d-a801-37d93e904b30/clickup-review-errors.png" sizes="100vw" caption="Errors detected in ClickUp’s data import appear in red. (Source: <a href='https://clickup.com/'>ClickUp</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0e3ee9a7-3083-405d-a801-37d93e904b30/clickup-review-errors.png'>Large preview</a>)" alt="ClickUp data import cleanup" >}}

Flatfile highlights required fields that are empty, contain an obvious error or divert from the data model ClickUp specified in their back-end.

The user can rely on Flatfile’s detection system to find those import errors. The “Only show rows with problems” toggle in the left-hand corner makes it even easier to spot.

This keeps users from having to:

<ul>
  <li>Review the original CSV file and fix errors before re-importing again.</li>
  <li>Import the data and do the cleanup afterwards in the app.</li>
</ul>

How do you set up this system of column-mapping and error detection? Flatfile does most of the work for you.

{{< rimg breakout="true" href="https://flatfile.com/?utm_source=Smashing-Magazine-Article-November-2019&utm_medium=Display&utm_campaign=Smashing-Magazine-11052019-Article&utm_content=Product-Variant" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e4085e8f-37c6-4d18-bab7-80f4b19f571f/10-flatfile-column-matching.png" sizes="100vw" caption="There’s no need to build your data importer from-scratch with Flatfile. (Source: <a href='https://flatfile.com/?utm_source=Smashing-Magazine-Article-November-2019&utm_medium=Display&utm_campaign=Smashing-Magazine-11052019-Article&utm_content=Product-Variant'>Flatfile</a>)(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e4085e8f-37c6-4d18-bab7-80f4b19f571f/10-flatfile-column-matching.png'>Large preview</a>)" alt="Flatfile makes data import simple for developers" >}}

Flatfile is configured via a JSON code snippet. Any fields or labels you specify in this code will be reflected in the importer. This allows for column-matching and even complex validation for things like normalizing phone numbers or date formats:

{{< rimg breakout="true" href="https://flatfile.com/?utm_source=Smashing-Magazine-Article-November-2019&utm_medium=Display&utm_campaign=Smashing-Magazine-11052019-Article&utm_content=Product-Variant" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/99318844-4756-4be1-840a-7f3d97e16a26/1-flatfile-demo.png" sizes="100vw" caption="This Flatfile demo provides the pre-written JSON code on the left and a sample of the importer output on the right. (Source: <a href='https://flatfile.com/?utm_source=Smashing-Magazine-Article-November-2019&utm_medium=Display&utm_campaign=Smashing-Magazine-11052019-Article&utm_content=Product-Variant'>Flatfile</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/99318844-4756-4be1-840a-7f3d97e16a26/1-flatfile-demo.png'>Large preview</a>)" alt="Flatfile demo" >}}

Flatfile has already been coded for you. You just need to align your data model with what you expect your users to import into your product.

Here’s a JSON snippet you might use to customize the Flatfile importer for a basic contact list:

{{< rimg href="https://flatfile.com/?utm_source=Smashing-Magazine-Article-November-2019&utm_medium=Display&utm_campaign=Smashing-Magazine-11052019-Article&utm_content=Product-Variant" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/81fef5ca-d51e-478e-b7c6-29247450beed/2-flatfile-define-schema.png" sizes="100vw" caption="An example from Flatfile on how to code in your own keys and labels for a basic contact list import. (Source: <a href='https://flatfile.com/?utm_source=Smashing-Magazine-Article-November-2019&utm_medium=Display&utm_campaign=Smashing-Magazine-11052019-Article&utm_content=Product-Variant'>Flatfile</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/81fef5ca-d51e-478e-b7c6-29247450beed/2-flatfile-define-schema.png'>Large preview</a>)" alt="Flatfile code snippet for contact list import" >}}

You can then use validators to set strict rules for what can appear in the corresponding fields:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d89e35d0-9af6-4e2d-93a3-81350d5a800d/17-flatfile-validators.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d89e35d0-9af6-4e2d-93a3-81350d5a800d/17-flatfile-validators.png" sizes="100vw" caption="An example from Flatfile on how to code in complex validators including regex for CSV imports. (Source: <a href='https://www.flatfile.io/?utm_source=Smashing-Magazine-Article-November-2019&utm_medium=Display&utm_campaign=Smashing-Magazine-11052019-Article&utm_content=Product-Variant'>Flatfile</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d89e35d0-9af6-4e2d-93a3-81350d5a800d/17-flatfile-validators.png'>Large preview</a>)" alt="Flatfile code snippet for data import validation" >}}

Bottom line:

It’s not easy building a data importer yourself. Integrating Flatfile allows you to focus on other core features of your product’s experience, knowing that the CSV import experience is taken care of.

## Wrapping Up

One of the reasons we build SaaS products is so users can effectively manage their businesses without the costly overhead of outsourcing to a third party or the costly practice of trying to implement everything themselves.

However, just because you know how to build a feature that addresses those needs, doesn’t mean you should, or want to, build an importer.

Of all the things that can stand in the way of you getting and retaining users in your app, don’t let something like importing data be the reason for customer frustration or churn. You can see how easy it is for users to become soured on the slightest inconvenience with common CSV import errors. Take advantage of a tool like Flatfile whose sole focus is designing faster and more seamless CSV import experiences for your users, teams and products.

{{< signature "ms, ra, yk, il" >}}
