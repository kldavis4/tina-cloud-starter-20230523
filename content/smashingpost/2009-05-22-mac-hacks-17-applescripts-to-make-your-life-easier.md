---
title: 'Mac Hacks: 17 AppleScripts To Make Your Life Easier'
slug: mac-hacks-17-applescripts-to-make-your-life-easier
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/11fb7c69-ce81-4eab-a1b5-a731198e3d34/applescripts.jpg
date: 2009-05-22T11:28:18.000Z
author: diogo-terror
description: >-
  If you are an experienced professional, chances are you have a good set of
  tools and a work process that you repeat on a daily basis to handle your work.
  That's good; it's how you become more productive, and become an expert. But
  with repetitive processes come repetitive mechanical work. Whether it's
  opening a file in Photoshop to change the format or adding an iCal to-do item
  based on an email you received, these little tasks **can be streamlined**.
  That's the purpose of **AppleScripts**.
categories:
  - Productivity
  - Mac
  - Scripting
  - Workflow
---
If you are an experienced professional, chances are you have a good set of tools and a work process that you repeat on a daily basis to handle your work. That's good; it's how you become more productive, and become an expert. But with repetitive processes come repetitive mechanical work. Whether it's opening a file in Photoshop to change the format or adding an iCal to-do item based on an email you received, these little tasks <strong>can be streamlined</strong>. That's the purpose of AppleScripts.

AppleScript is a scripting language developed by Apple to help people automate their work processes on the Mac operating system. It accomplishes this by exposing every element of the system's applications as an object in an extremely simple, English-like language. AppleScript is to the Mac OS as JavaScript is to browsers.

You may also be interested in the following related posts:

*   [25 Free Mac Apps That Will Boost Your Productivity](https://www.smashingmagazine.com/2009/07/25-open-source-mac-apps-that-will-boost-your-productivity/)
*   [Five Reasons Why <del>Designers</del> Developers are Switching to Mac](https://www.smashingmagazine.com/2009/04/five-reasons-why-designers-are-switching-to-mac/)
*   [Why Web Developers Don’t Need A Mac](https://www.smashingmagazine.com/2009/06/why-web-developers-dont-need-a-mac/)

Quite a few AppleScripts are available on the Web, ready for you to use, so you don't even need to look at their code. This article presents you with 17 of the most useful ones.

{{% feature-panel %}}

If you're interested in learning this language, here are some good resources to get started:

*   [Official AppleScript Website](https://developer.apple.com/library/content/documentation/AppleScript/Conceptual/AppleScriptLangGuide/introduction/ASLR_intro.html "Official AppleScript Site") Apple's page on AppleScript.
*   [AppleScript Language Guide](https://developer.apple.com/documentation/AppleScript/Conceptual/AppleScriptLangGuide/introduction/ASLR_intro.html "AppleScript Language Guide") Apple's in-depth guide to AppleScript.
*   [Learning AppleScript](https://www.macworld.com/article/49438/2006/02/asexcerpt.html "Learning AppleScript") Macworld's article on the fundamentals of writing AppleScripts.
*   [AppleScript Users](https://lists.apple.com/mailman/listinfo/applescript-users "AppleScript Users") AppleScript Mailing List.</p>

## First, Where To Put Your AppleScripts

After you download a script, you have to know where to put it to start using it. For this purpose, let's say that there are <strong>three different kinds of AppleScripts</strong>, each of which is used for a different purpose.</p>

### Simple Scripts

You put these scripts in a special folder and call them when you need them. You can invoke them just by double clicking on them, but calling them contextually is a lot more effective. Using the <strong>Script Menu</strong> is one way to achieve this.

To activate the Script Menu, first open the <strong>AppleScript Utility</strong> app in the <em>/Applications/AppleScript</em> folder and check "Show Script Menu in menu bar."

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9e18c4bf-517d-4721-957c-73014de07e8c/script-utilities.jpg" alt="AppleScript Utility screenshot" />

The Script Menu will show a list of AppleScripts that come with Mac OS X, plus your application-specific scripts. To add a script to an application, simply put it in <em>~/Library/Scripts/Applications/&lt;NAME_OF_THE_APPLICATION&gt;</em>. If that folder doesn't exist, you can create it.

For example, if you had a Safari AppleScript, you'd put it in <em>~/Library/Scripts/Applications/Safari</em>. From then on, if you clicked the Script Menu when Safari was active, your script would appear at the top of the list for you to use.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3b34b1a3-cb42-46d1-bf3b-72804c77e795/contextual-script-menu.jpg" alt="Simple Script screenshot" />

### Droplets

Droplets are AppleScripts that live in the Finder's toolbar. To use it, all you need to do is drop a file or folder into it. This is very useful for when a script affects a file or the contents of a folder, because all you have to do is drop the target of the action onto the script's icon.

To "install" a Droplet, first save it in a folder of your choosing: <em>~/Library/Scripts/Droplets</em> is a good place. Then just drag the script to the Finder's toolbar.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b72306eb-7c2a-407b-83ca-8256dcac6316/finders-toolbar.jpg" alt="Droplet Screenshot" />

### Folder Actions

Folder Actions are AppleScripts that are "attached" to a folder. They are executed every time you perform an action with that folder. Folder Actions can get triggered every time you add a file to a folder, remove a file, modify its items, etc. The behavior depends on how the script works, but you can imagine how useful that would be.

To add a Folder Action to a folder, right-click it to bring up the contextual menu, and click <em>Attach a Folder Action</em>. The default location for Folder Action scripts is <em>/Library/Scripts/Folder Action Scripts</em>, but if you want to keep all your custom-installed scripts in one place, <em>~/Library/Scripts/Folder Actions</em> is a good place to keep them.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9f04873f-7248-4c72-9aea-def520598eb9/folder-actions.jpg" alt="Folder Action Screenshot" />

## Multimedia Processing

### 1. ConvertImage

This is a great example of how Droplets are useful. Just drop an image file into ConvertImage, and you will be prompted to choose from a list of file formats. Pick a format, and it saves it in the same folder as your original file.

ConvertImage
<strong>Type:</strong> Droplet
<strong>Requirements:</strong> OS X 10.4+, <span class="removed_link" title="https://www.apple.com/applescript/imageevents/">Image Events</span>

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6e15376f-7ccd-4d2b-ba3a-bee8af372c1e/convert-image1.jpg" alt="Convert Image Screenshot" />

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1ece7083-09f5-49e2-ace8-500c7144d23a/convert-image2.jpg" alt="Conver Image Screenshot with file formats" />

### 2. QuickTime to Photoshop

Exports QuickTime frames directly to Photoshop. All you have to do is pause a video at the frame that you want to export, and then invoke the script. If Photoshop is closed, the script will activate it for you. After it imports the frame, it will ask you if you want another frame from the QuickTime file.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/58632075-7f05-4073-bc04-c21118a79d09/quicktimetophotoshop.zip" rel="nofollow">QuickTime to Photoshop</a><br>
<strong>Type:</strong> Simple Script
<strong>Requirements:</strong> Adobe Photoshop CS4

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/832cd4b9-526e-4bd2-9977-89e12c3f4208/qt2photoshop1.jpg" alt="Quick Time to photoshop Screenshot asking where to use the frame" />

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/06f8bbff-ce65-4cd6-b1ba-7f6dc1451934/qt2photoshop2.jpg" alt="Quick Time to photoshop Screenshot asking another frame" />

### 3. iPhoto to Photoshop

This opens the currently selected iPhoto image in Photoshop. It is a simple automation leap that gets you where you want without intervening steps.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e43d4730-7a1b-4825-b230-93c6ff2d9698/iphototophotoshop.zip" rel="nofollow">iPhoto to Photoshop</a><br>
<strong>Type:</strong> Simple Script
<strong>Requirements:</strong> Adobe Photoshop CS4

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/22239fb3-a089-4c89-93c1-5c7b1238adcb/iphoto2photoshop.jpg" alt="iPhoto to Photoshop Screenshot" />

### 4. Rampage

Drop an image file or a folder with image files in Rampage, and you get a text file with a lot of information about the file(s): size, resolution, color mode, ICC Profiles and more. It also reports warnings and errors about the file(s). The script currently supports TIFF, GIF, BMP, PNG and JPG image formats.

Rampage
<strong>Type:</strong> Droplet
<strong>Requirements:</strong> None

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d9cacda3-13b2-4b00-8a81-ff2035b200f2/rampage1.jpg" alt="Rampage Screenshot on dropping" />

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/93c0fe8a-b1a7-47c7-a23f-6332e3c1e9c4/rampage2.jpg" alt="Rampage Screenshot with report file" />

### 5. SWF Extractor

This extract SWF files from Flash projectors (Windows or Mac executables) that are dropped into it.

SWF Extractor
<strong>Type:</strong> Droplet
<strong>Requirements:</strong> None

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/923adac1-7f9f-4ad6-864f-fe0110e7cccf/swf-extractor1.jpg" alt="SWF extractor Screenshot on dropping" />

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/47069988-93a1-4bf3-949f-f0a7d3fdf9cd/swf-extractor2.jpg" alt="SWF extractor Screenshot on result" />

## Safari Tools

### 6. Safari Web Site Validator

Safari Web Site Validator gets the HTML or XHTML from the current active Safari tab and sends the code to the W3C Markup Validation Service in a separate window. It then asks if you want to validate the page's CSS file as well.

Safari Web Site Validator
<strong>Type:</strong> Simple Scripts
<strong>Requirements:</strong> OS X 10.4.4+

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/aa8c9931-c4c7-4481-a21c-8a6443d61bfe/safari-validator1.jpg" alt="Safari Validator screenshot on asking for CSS" />

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/23204a98-e000-4c05-9c7d-ab0872b4bcb8/safari-validator2.jpg" alt="Safari Validator screenshot on the validation report" />

### 7. Tiny URL

Despite its name, the Tiny URL script doesn't use the TinyUrl application. It's based on another URL shortening service called Metamark. It goes to the currently active Safari tab and puts the shortened URL directly in your clipboard.

Tiny URL
<strong>Type:</strong> Simple Scripts
<strong>Requirements:</strong> None

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1805643a-d832-41b6-8bb2-6edac94df909/tiny-url.jpg" alt="Tiny URL Screenshot with shortened url" />

### 8. Safari Cleannup

This automates the deletion of Safari icons and cache and plist files. Getting rid of these extraneous files can boost Safari's performance.

Safari Cleannup
<strong>Type:</strong> Simple Scripts
<strong>Requirements:</strong> None

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/124316b0-92c5-4a79-845d-48050770eb2d/safari-cleanup.jpg" alt="Safari Cleannup Screenshot on asking for options" />

### 9. Scour Web Page

This script scans the current Web page in Safari looking for MP3, AAC and PDF media files. If it finds multiple files, it prompts you to select the ones you want to keep, and then downloads them and adds them to your iTunes media library.

<a href="https://dougscripts.com/itunes/scripts/ss.php?sp=scourwebpage" rel="nofollow">Scour Web Page</a><br>
<strong>Type:</strong> Simple Scripts
<strong>Requirements:</strong> None

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/df1b9dcf-6b71-4931-869b-e654f4d83205/scour-page.jpg" alt="Scour web page screenshot on asking which files to look for" />

## Mail And iCal

### 10. Fuhgeddaboutit

In Sopranos-speak, fuhgeddaboutit means "forget about it." Indeed, one of the purposes of GTD is to free your brain from having to keep track of everything. Just relax, forget about it now and be confident that you'll remember when you need to.

This script make that possible by making iCal To-Do items from an Apple Mail email. Just invoke the script with the email you want, and it will create an iCal item with a due time set relative to the email's arrival.

Fuhgeddaboutit
<strong>Type:</strong> Simple Scripts
<strong>Requirements:</strong> None

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3a01047d-59e4-4ae1-9e58-636a815d40a9/mail2ical1.jpg" alt="Fuhgeddaboutit screenshot on aking which calendar to use" />

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/020109fd-20d7-4906-a7c5-5f3440da3e93/mail2ical2.jpg" alt="Fuhgeddaboutit asking for a due date" />

### 11\. Send Attachment Droplet

Just drop a file into this Droplet, and it will make a new Mail email with the file as an attachment and the subject set to the file's name. If the Mail app is closed, the script will open it for you.

Send Attatchment Droplet
<strong>Type:</strong> Droplet
<strong>Requirements:</strong> None

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7f78a6fc-79b7-4ab3-80d3-a8dc55cf6396/attatchment-droplet1.jpg" alt="send attachment screenshot on dropping" />

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2d9e323f-3e1d-4f4d-ac0d-ef26ffc471e3/attatchment-droplet2.jpg" alt="send attachment screenshot on the created email" />

### 12\. Remove iCal Duplicates

When you sync and share many calendars in iCal, you often end up with a lot of duplicates. This simple script helps you remove those. But once you ask it to delete duplicates, there's no undoing. So, be sure to back up your calendar first.

Remove iCal Duplicates
<strong>Type:</strong> Simple Script
<strong>Requirements:</strong> None

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/05b65b02-88ab-4d1d-8bf4-c60964f1b766/ical-duplicates1.jpg" alt="Remove iCal Duplicates on which calendar to choose" />

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4359e566-6782-4307-b19a-f9b3bf2fa2fa/ical-duplicates2.jpg" alt="Remove iCal Duplicates on the result of the removal" />

### 13\. iCalculate

Invoke this script, create an iCal calendar item and start date, and it will generate a text file reporting how many hours you have worked on the project. It even calculates the total cost of the project, based on the hourly rate your specify. Especially suited to freelancers.

iCalculate
<strong>Type:</strong> Simple Script
<strong>Requirements:</strong> None

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e8a5f4bf-db73-4047-8c36-aca60fc961b5/icalculate1.jpg" alt="iCalculate screenshot on prompt for start date" />

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6d5cf471-2051-4836-93c4-2dd4c1bdf8c2/icalculate2.jpg" alt="iCalculate screenshot on the generated report" />

## Finder Utilities

### 14\. Pack'em

Pack'em takes one or more items from Finder, packs them with tar, compresses them with either bzip2 or gzip and saves the compressed archive in the same folder as the original items. A great companion to the Send Attachment Droplet. With these two AppleScripts, you can compress and email a set of files or folders directly from Finder.

Pack'em
<strong>Type:</strong> Simple Script
<strong>Requirements:</strong> None

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b4826116-2908-4339-a220-fc1048b36a62/packem1.jpg" alt="Pack'em screenshot on choosing the compression format" />

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/eeccbc20-8b92-4020-b797-cec1a6b49092/packem2.jpg" alt="Pack'em screenshot on the result of packing" />

### 15\. Rename Files

Just drop a folder into this Droplet, and it will give you a lot of options to batch process its contents. You can rename the files according to names specified in a particular text file or change the files individually. Either way accomplishes your task much faster than by changing every file name independently.

Rename Files
<strong>Type:</strong> Droplet
<strong>Requirements:</strong> None

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/92722677-2aa2-4ab6-86ef-4e6ad1fbf5e2/rename-files1.jpg" alt="Rename Files screenshot on dropping" />

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f24f6895-7b07-482c-b9ef-12b1ebdb1955/rename-files2.jpg" alt="Rename Files screenshot on first level script options" />

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/65649b6b-224f-4f82-b041-e100bfc3938f/rename-files3.jpg" alt="Rename Files screenshot on second level script options" />

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/23204a98-e000-4c05-9c7d-ab0872b4bcb8/safari-validator2.jpg" alt="Rename Files screenshot on third level script options" />

### 16\. Websafe Name

If you develop websites, you are probably accustomed to giving your files Web-friendly names. But there are times when you have to upload a whole set of files sent to you by a client, or upload things that you weren't expecting to use. Websafe Name is very useful for this kind of task. You don't even need to look through the list of files; just drop them into this script, and it will rename them to something Web-friendly.

Websafe Name
<strong>Type:</strong> Droplet
<strong>Requirements:</strong> None

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c0509e9b-8386-4f3a-8a23-e7ee6e93b795/web-safe1.jpg" alt="Web safe name screenshot on dropping" />

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1938b133-e1aa-431c-9d0a-7aaec8947b3c/web-safe2.jpg" alt="Web safe name screenshot on the resulting file" />

### 17\. Tagger

Safari Web Site Validator gets the HTML or XHTML from the current active Safari tab and sends the code to the W3C Markup Validation Service in a separate window. It then asks if you want to validate the page's CSS file as well.

Safari Web Site Validator
<strong>Type:</strong> Simple Scripts
<strong>Requirements:</strong> OS X 10.4.4+

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/aa8c9931-c4c7-4481-a21c-8a6443d61bfe/safari-validator1.jpg" alt="Safari Validator screenshot on asking for CSS" />

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/23204a98-e000-4c05-9c7d-ab0872b4bcb8/safari-validator2.jpg" alt="Safari Validator screenshot on the validation report" />

### 7. Tiny URL

Despite its name, the Tiny URL script doesn't use the TinyUrl application. It's based on another URL shortening service called Metamark. It goes to the currently active Safari tab and puts the shortened URL directly in your clipboard.

Tiny URL
<strong>Type:</strong> Simple Scripts
<strong>Requirements:</strong> None

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1805643a-d832-41b6-8bb2-6edac94df909/tiny-url.jpg" alt="Tiny URL Screenshot with shortened url" />

### 8. Safari Cleannup

This automates the deletion of Safari icons and cache and plist files. Getting rid of these extraneous files can boost Safari's performance.

Safari Cleannup
<strong>Type:</strong> Simple Scripts
<strong>Requirements:</strong> None

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/124316b0-92c5-4a79-845d-48050770eb2d/safari-cleanup.jpg" alt="Safari Cleannup Screenshot on asking for options" />

### 9. Scour Web Page

This script scans the current Web page in Safari looking for MP3, AAC and PDF media files. If it finds multiple files, it prompts you to select the ones you want to keep, and then downloads them and adds them to your iTunes media library.

<a href="https://dougscripts.com/itunes/scripts/ss.php?sp=scourwebpage" rel="nofollow">Scour Web Page</a><br>
<strong>Type:</strong> Simple Scripts
<strong>Requirements:</strong> None

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/df1b9dcf-6b71-4931-869b-e654f4d83205/scour-page.jpg" alt="Scour web page screenshot on asking which files to look for" />

## Mail And iCal

### 10. Fuhgeddaboutit

In Sopranos-speak, fuhgeddaboutit means "forget about it." Indeed, one of the purposes of GTD is to free your brain from having to keep track of everything. Just relax, forget about it now and be confident that you'll remember when you need to.

This script make that possible by making iCal To-Do items from an Apple Mail email. Just invoke the script with the email you want, and it will create an iCal item with a due time set relative to the email's arrival.

Fuhgeddaboutit
<strong>Type:</strong> Simple Scripts
<strong>Requirements:</strong> None

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3a01047d-59e4-4ae1-9e58-636a815d40a9/mail2ical1.jpg" alt="Fuhgeddaboutit screenshot on aking which calendar to use" />

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/020109fd-20d7-4906-a7c5-5f3440da3e93/mail2ical2.jpg" alt="Fuhgeddaboutit asking for a due date" />

### 11\. Send Attachment Droplet

Just drop a file into this Droplet, and it will make a new Mail email with the file as an attachment and the subject set to the file's name. If the Mail app is closed, the script will open it for you.

Send Attatchment Droplet
<strong>Type:</strong> Droplet
<strong>Requirements:</strong> None

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7f78a6fc-79b7-4ab3-80d3-a8dc55cf6396/attatchment-droplet1.jpg" alt="send attachment screenshot on dropping" />

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2d9e323f-3e1d-4f4d-ac0d-ef26ffc471e3/attatchment-droplet2.jpg" alt="send attachment screenshot on the created email" />

### 12\. Remove iCal Duplicates

When you sync and share many calendars in iCal, you often end up with a lot of duplicates. This simple script helps you remove those. But once you ask it to delete duplicates, there's no undoing. So, be sure to back up your calendar first.

Remove iCal Duplicates
<strong>Type:</strong> Simple Script
<strong>Requirements:</strong> None

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/05b65b02-88ab-4d1d-8bf4-c60964f1b766/ical-duplicates1.jpg" alt="Remove iCal Duplicates on which calendar to choose" />

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4359e566-6782-4307-b19a-f9b3bf2fa2fa/ical-duplicates2.jpg" alt="Remove iCal Duplicates on the result of the removal" />

### 13\. iCalculate

Invoke this script, create an iCal calendar item and start date, and it will generate a text file reporting how many hours you have worked on the project. It even calculates the total cost of the project, based on the hourly rate your specify. Especially suited to freelancers.

iCalculate
<strong>Type:</strong> Simple Script
<strong>Requirements:</strong> None

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e8a5f4bf-db73-4047-8c36-aca60fc961b5/icalculate1.jpg" alt="iCalculate screenshot on prompt for start date" />

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6d5cf471-2051-4836-93c4-2dd4c1bdf8c2/icalculate2.jpg" alt="iCalculate screenshot on the generated report" />

## Finder Utilities

### 14\. Pack'em

Pack'em takes one or more items from Finder, packs them with tar, compresses them with either bzip2 or gzip and saves the compressed archive in the same folder as the original items. A great companion to the Send Attachment Droplet. With these two AppleScripts, you can compress and email a set of files or folders directly from Finder.

Pack'em
<strong>Type:</strong> Simple Script
<strong>Requirements:</strong> None

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b4826116-2908-4339-a220-fc1048b36a62/packem1.jpg" alt="Pack'em screenshot on choosing the compression format" />

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/eeccbc20-8b92-4020-b797-cec1a6b49092/packem2.jpg" alt="Pack'em screenshot on the result of packing" />

### 15\. Rename Files

Just drop a folder into this Droplet, and it will give you a lot of options to batch process its contents. You can rename the files according to names specified in a particular text file or change the files individually. Either way accomplishes your task much faster than by changing every file name independently.

Rename Files
<strong>Type:</strong> Droplet
<strong>Requirements:</strong> None

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/92722677-2aa2-4ab6-86ef-4e6ad1fbf5e2/rename-files1.jpg" alt="Rename Files screenshot on dropping" />

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f24f6895-7b07-482c-b9ef-12b1ebdb1955/rename-files2.jpg" alt="Rename Files screenshot on first level script options" />

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/65649b6b-224f-4f82-b041-e100bfc3938f/rename-files3.jpg" alt="Rename Files screenshot on second level script options" />

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/23204a98-e000-4c05-9c7d-ab0872b4bcb8/safari-validator2.jpg" alt="Rename Files screenshot on third level script options" />

### 16\. Websafe Name

If you develop websites, you are probably accustomed to giving your files Web-friendly names. But there are times when you have to upload a whole set of files sent to you by a client, or upload things that you weren't expecting to use. Websafe Name is very useful for this kind of task. You don't even need to look through the list of files; just drop them into this script, and it will rename them to something Web-friendly.

Websafe Name
<strong>Type:</strong> Droplet
<strong>Requirements:</strong> None

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c0509e9b-8386-4f3a-8a23-e7ee6e93b795/web-safe1.jpg" alt="Web safe name screenshot on dropping" />

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1938b133-e1aa-431c-9d0a-7aaec8947b3c/web-safe2.jpg" alt="Web safe name screenshot on the resulting file" />

### 17\. Tagger

The "folder" is a computer interface paradigm that is a very powerful way to organize files. But it's neither the only paradigm nor the best solution for all scenarios. Many sub-folders nested deep is a sign that a folder structure may not be appropriate. Another great paradigm, coming straight from the Web, is "tagging." You keep all your files flat in a common location, but group them by tags so that you can retrieve or filter them by tags. It so happens that the Mac OS X has very good support for this. You can use Spotlight Comments to tag files and Smart Folders to dynamically retrieve them. All you need now is an easy way to do this, and this Folder Action does exactly that.

To use Tagger, attach it to a folder. Then, every time you add a file to that folder via Finder, the script will prompt you to tag that file. It also automatically creates Smart Folders for all of your defined tags.

Tagger
<strong>Type:</strong> Folder Action
<strong>Requirements:</strong> None

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f48cb29a-1acd-4b75-9383-3d4612da810f/tagger1.jpg" alt="Tagger screenshot on prompt for tag name" />

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e58c70b2-81f6-4547-866d-e62f0ced6bb9/tagger2.jpg" alt="Tagger screenshot on the generated smart folder" />

## Further Resources

If you like the scripts above, you may also be interested in the following articles and related resources:

*   [Automation Life Hacks You Can't Live Without](https://www.clicktime.com/blog/automation-life-hacks-you-cant-live-without) Eight automation life hacks for home, work, and life in general. No coding skills required.
*   [Doug's AppleScripts for iTunes](https://dougscripts.com/itunes/) A huge collection of AppleScripts for iTunes.
*   [Studio Log](https://www.blankreb.com/studiosnips.php) Scripts and discussion on how to make them.
*   [AppleScripts on Github](https://github.com/search?langOverride=&q=applescripts&repo=&start_value=1&type=Repositories) A search list of AppleScripts hosted on Github

{{< signature "al" >}}

