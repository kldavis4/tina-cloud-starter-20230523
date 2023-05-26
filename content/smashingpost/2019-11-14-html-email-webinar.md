---
title: 'Become An HTML Email Geek With These Videos From Rémi Parmentier'
slug: html-email-webinar
author: rachel-andrew
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/59052d9f-c018-4903-86c0-836eaed38b13/html-email-webinar-startslide.png
date: 2019-11-14T12:00:00.000Z
summary: >-
  In these two videos (a webinar recorded for our Smashing Members and a presentation from SmashingConf Freiburg), you can discover all the tips and tricks you need to help you design HTML emails. Follow along as Rémi Parmentier shares what he knows about taming email clients.
description: >-
  In these two videos (a webinar recorded for our Smashing Members and a presentation from SmashingConf Freiburg), you can discover all the tips and tricks you need to help you design HTML emails. Follow along as Rémi Parmentier shares what he knows about taming email clients.
categories:
  - Smashing TV
  - SmashingConf
  - Membership
disable_ads: true
disable_panels: true
disable_newsletterbox: true
---

Creating an HTML email can feel like stepping back a few years as a web developer. All of our new layout functionality is unavailable to us &mdash; email clients render the same layout in completely different ways. Just when we think we have it all fixed, another email client shows up with a new set of bugs.

Not too long ago, Rémi Parmentier, an HTML Email developer, ran a session with practical front-end techniques for building modern, cross-client emails. A few weeks later, he gave a wonderful talk at SmashingConf Freiburg highlighting some of the common struggles and shared **useful strategies for avoiding problems in email development**.

There was so much useful information contained in these sessions that we wanted to release them more widely &mdash; including the webinar transcript and references to slides and resources. If you have ever struggled with email development, these will give you a great starting point to understand why an email isn’t rendered properly, and how to squash those nasty bugs quickly.

If you enjoy learning from these videos, check out Smashing Membership. Starting from this month, we will be **showing some of the live sessions we run every month** to a wider audience &mdash; absolutely free of charge to view. However, if you’d like to join the discussion live and perhaps have your work reviewed by an expert, [join Smashing Membership](https://www.smashingmagazine.com/membership). For the price of one coffee a month, you can support the creation of more content like this.

Now get ready to learn everything you need to know about HTML email!

<ul>
	<li><a href="#webinar">Webinar</a></li>
	<li><a href="#webinar-resources-and-transcript">Webinar resources and transcript</a></li>
	<li><a href="#smashingConf-2019-presentation">SmashingConf 2019 Presentation</a></li>
</ul>

## Webinar: HTML Email with Rémi Parmentier

{{< vimeo id="349773125" >}}

### Resources And Transcript

* <a href="https://drive.google.com/file/d/1VzFT2BvMPZmpJAnJjw9U7-crURe-eqWA/view?usp=sharing">Slides</a>
* Follow <a href="https://email.geeks.chat">#emailgeeks Slack</a>
* <a href="https://twitter.com/search?q=%23emailgeeks">#emailgeeks on Twitter</a>
* <a href="https://thebetter.email/resources">A huge list of resources</a> maintained by Jason Rodriguez.

<span class="smashing-tv-speaker">Rémi Parmentier: </span>  Thanks, everyone, for coming to my presentation. My name is Rémi Parmentier. Some of you might know me from Twitter or from my blog under the nickname hteumeuleu. I’ve been doing HTML emails for as long as I’ve been working in this industry. For the past few years, I’ve started to give training in HTML emails as well I am spending a lot of time online on Slack, on Twitter, on forums to help people find solutions for their email problems. This gave me a pretty good view of most of the coding problems that people have and how to actually solve them. I started working on this email coding guidelines project this year. This was greatly inspired by some of the work that’s been done on the web about I think a decade ago.

<span class="smashing-tv-speaker">Rémi Parmentier: </span>  About a decade ago, there was a lot of trends of web guidelines being shared by people from many different companies. First one was the most famous one was this code guide by Mark Otto, who was then working at Twitter. The point of the document was to share a lot of guidelines about how HTML and CSS should be coded within the company. There was a lot of good practices shared in this document, like which doctype you should use or to close your tag and such. I think this is really interesting to have.

<span class="smashing-tv-speaker">Rémi Parmentier: </span>  In the email world, Ted Goas from Stack Overflow actually made a very similar document with a lot of content as well about how they’re building the emails at Stack Overflow. This really gave me the lust to make a similar document that everyone could share within their company or everyone could pick good practices for building HTML emails. We’re going to see a few of these best practices and you’ll be able to see the document afterwards online. Let’s start ahead.

<span class="smashing-tv-speaker">Rémi Parmentier: </span>  The first thing that I usually share is to use the HTML5 doctype. Whenever I help people online of open HTML email, it makes me sad to see that a lot of people are still using HTML4 doctype or XHTML 1. The first reason to use the HTML5 doctype is that it’s really nice. Actually, it’s very short. You can type it by hand, you can remember it, and that’s already a good reason to use it.

<span class="smashing-tv-speaker">Rémi Parmentier: </span>  The most important reason to use the HTML5 doctype is that when an email is displayed in webmail, our doctype is usually removed and we inherit from the webmail’s doctype. Most webmails use the HTML5 doctype, so even for you wish you could use HTML1 or HTML4 doctype, this won’t work because webmails will remove it.

<span class="smashing-tv-speaker">Rémi Parmentier: </span>  I made this little illustration of how this actually works. On the left, you can see an email address coded. It’s got a style tag and it’s got a div and an H1 inside. What happens when a webmail like Gmail, for example, wants to display this content, it will pick the style tags and pick the content within the body, and it will prefix the styles, it will remove all the styles that it won’t support, and then it will include this inside the HTML of the actual webmail, because webmails are actually just HTML and CSS. This means that even if I use an HTML4 doctype, because Gmail uses HTML5 doctype, my code will be random thanks to that doctype. This is a good thing to have in mind.

<span class="smashing-tv-speaker">Rémi Parmentier: </span>  I made this about this, about which doctype you should use in HTML emails, about three years ago already, but what I saw back then was that most of the email clients already were using an HTML5 doctype. A few of them didn’t have a doctype at all, like on mobile apps sometimes, but a lot of them were on HTML5.

<span class="smashing-tv-speaker">Rémi Parmentier: </span>  It’s important to know that you can end up on different doctypes because there can be differences. The first one is that HTML5 actually have spaces between images. If you slice some big image inside your email, you will see something like this if you try it with an HTML5 doctype.

<span class="smashing-tv-speaker">Rémi Parmentier: </span>  Let me actually show you this with a little demo. Here, I have this ... Oops, it’s the wrong one. Here I have this little demo of a T-Rex. It’s actually three images. Here with an HTML1 doctype, everything is working fine, but if I use an HTML5 doctype instead, boom, you have white lines appearing between each images.

<span class="smashing-tv-speaker">Rémi Parmentier: </span>  Now, I’m not exactly sure why this happens, but I think it’s because when HTML5 upgraded, they cannot change some of the way that images are supposed to behave according to the specification, so now it looks more like a paragraph with text, so there are lines in between images.

<span class="smashing-tv-speaker">Rémi Parmentier: </span>  Email Geeks have found very good solutions to the service. One of the solutions is to actually add a display block style to every images. Once you do this, it will remove the white lines between the images. Another solution to avoid this if you can’t use display block is to add a vertical align middle style and then you will remove these white lines as well.

<span class="smashing-tv-speaker">Rémi Parmentier: </span>  This is a first quirk that you can encounter with HTML5 doctype, but there is another interesting case is that you can’t display block a table cell in WebKit without a doctype. This one is really interesting as well. I’ve got a table for this as well, which would be right here.

<span class="smashing-tv-speaker">Rémi Parmentier: </span>  Here I’ve got a table with three little dinosaurs next to each others. Usually when we’ve got tables like this and we want to make our emails optimized for mobiles, what we can do is apply the display block to our TDs and then they will stack on each others like this.

<span class="smashing-tv-speaker">Rémi Parmentier: </span>  As we can see here, we have an HTML5 doctype. This is working fine, but if I would ever end up in an image client that will remove the doctype, then this won’t work anymore in WebKit. As you can see now, it’s back to the regular pattern display.

<span class="smashing-tv-speaker">Rémi Parmentier: </span>  I think this has to do with legacy websites and quirk modes and all of these things, but one solution that was found by the email community is to actually use TH tags instead of TD. If I remove every TD here by TH, you can see that, here, even without a doctype, it’s working again. This is some kind of the quirks that you have to deal with in HTML emails because of not only email clients behave but also rendering engines like WebKit here.

<span class="smashing-tv-speaker">Rémi Parmentier: </span>  The second best practice I’d want to share with you today is to use the lang attributes. The lang attribute in HTML is to define the language of your document. This is very important for accessibility, and mostly this is because accessibility tools like screen readers will be able to pick the right voice for it.

<span class="smashing-tv-speaker">Rémi Parmentier: </span>  Once again, let me show you a demo of this live, and hopefully it won’t crash. Here I have this very nice email from Mailchimp. As it was said before, I am French, so my computer is set in French. My screen reader is in French as well, so every time we’ll see some new content, it will try to read it in French. I will stop my screen reader now. You try to see when we’ll get to this paragraph and see how it will read it.

<span class="smashing-tv-speaker">Rémi Parmentier: </span>  I know that I don’t really have a good English accent, but this is even worse than mine. If you don’t set the lang attributes, your content will be read on whatever default language is for your users. The quick phase here is to add the lang attributes, and then I can restart my screen reader.

<strong>Screenreader:</strong>:  Mailchimp Presents has a new collection of original content made with entrepreneurs in mind. In recent months, we’ve rolled out documentaries, short-form series and podcasts that live only on Mailchimp. Today, we officially launch a platform.

<span class="smashing-tv-speaker">Rémi Parmentier: </span>  As you can hear, even for my screen reader, and my system is still set in French, once the screen reader is actually on HTML contents, it will use another voice, an English voice there, to read the content which makes the experience much, much better here.

<span class="smashing-tv-speaker">Rémi Parmentier: </span>  One small difference that we have in HTML emails with the lang attribute is that, just like for the doctype, the doctype might not be picked up by webmails, because webmails will only take just styles and the content of the body. It’s usually a good practice to add the lang attribute as well on the wrapper that you have on your content inside your body, so you’ll make sure that this will get picked by webmails as well.

<span class="smashing-tv-speaker">Rémi Parmentier: </span>  Now a third best practice that I like is to actually use styles over HTML attributes. This is really something that people hate about HTML emails because they feel that they have to use all the HTML attributes, they have to use all code, and this makes emails look very different from the web, but there is really no reason for this at all unless you need to support very old email clients like Lotus Notes 6 or similar.

<span class="smashing-tv-speaker">Rémi Parmentier: </span>  In this example here, in the first example, you can see I’ve used valign, align and bgcolor attributes in HTML, but all of those can be very easily and robustly replaced by the corresponding styles. Here I only have one style attribute and inside I have the vertical align CSS property, text align and background color.

<span class="smashing-tv-speaker">Rémi Parmentier: </span>  One reason I like to do this is because it makes go cleaner and more readable. All your presentational properties are grouped in a single style attribute instead of being all over the place with valign, align and all the stuff. This makes it, in my opinion, very, very better to read and to maintain.

<span class="smashing-tv-speaker">Rémi Parmentier: </span>  There’s another reason I like to use styles over attributes is that it helps taking over email clients' own styles. For example, on the French webmail of Orange, the webmail’s UI actually has a CSS that has a rule that sets every TD to vertical align top. Because of this rule, if you were to use only HTML attributes like valign=middle, the CSS role from the webmail would override with the HTML attributes because this is how the cascade works in HTML and CSS.

<span class="smashing-tv-speaker">Rémi Parmentier: </span>  Instead, if we use an inline style with a vertical align property on the TD here, well, this style will take over the webmail style because inline styles are more important than external style sheets. Using styles over attributes is also a good way to fight other email clients' and webmails' default styles.

<span class="smashing-tv-speaker">Rémi Parmentier: </span>  There are a few exceptions to the attributes that I still use. The first exceptions is to center a table in Outlook 2007 to 2019 on Windows, because as Scott said in the introduction, Outlook uses Word as a rendering engine in those versions and it’s not really good at understanding CSS, at least for some properties.

<span class="smashing-tv-speaker">Rémi Parmentier: </span>  For example, here, it would understand the margin properties for pixel values, but it wouldn’t understand the margin zero auto value to center a table. We still need the align=center attribute to center elements and data, especially in Outlook, but we no longer need to use which attributes as in the first example here. This can be replaced by the width style instead.

<span class="smashing-tv-speaker">Rémi Parmentier: </span>  Now other exception in Outlook as well is when you want to define a fluid image width. In the first example, I use a width attribute with 100% value. The thing is that Outlook actually doesn’t deal with percentage width for images the same way as it should be in CSS.

<span class="smashing-tv-speaker">Rémi Parmentier: </span>  The percentage in Outlook is actually matching the physical image size and not the parent size in the HTML. If you’ve got an image that’s 600-pixel wide and you use a width=50%, then your image will actually be 300 pixels no matter what the size of your parent in HTML is.

<span class="smashing-tv-speaker">Rémi Parmentier: </span>  Usually, to avoid any quirks with this is then I always define a fixed width in pixels for Outlook using the width attribute in HTML, and then using a style, I use a width with 100%. Outlook will only pick the attribute value here and not the style value.

<span class="smashing-tv-speaker">Rémi Parmentier: </span>  Then, another exception I have when I use styles over attributes is to reset the default styles of the table. By default, the HTML tables have borders and padding inside and cells, et cetera. The proper way to do this in CSS is to set border zero, border spacing zero, our padding is zero, our border is zero, the first ones on the table, and expanding your border actually for each cell of your table.

<span class="smashing-tv-speaker">Rémi Parmentier: </span>  This is pretty much why I don’t really like to do it the CSS way because you need to repeat the padding and border for every TD of your table, while if you use the attributes, you only need to use them on the table, and then you’re all set for any ... no matter on any cells you have inside your table. This is probably something I will change my mind in a few years maybe, I hope, but for now, I’m still used and I prefer using the attribute way for resetting default styles on tables.

<span class="smashing-tv-speaker">Rémi Parmentier: </span>  Now another best practice I’d like to share is, do not split the visuals. This was actually a very common practice maybe a decade ago. When we had large images, it was always better, at least it was always shared that you should split it to make download faster and things like that, but this is not true today.

<span class="smashing-tv-speaker">Rémi Parmentier: </span>  Not splitting visual actually has a lot of benefits. The first one is that it’s easier to maintain. If you have a big visual in your email and it’s Friday night and your project manager comes at you and asks you to change it at the last minute, well, you don’t have to open Photoshop and slice your images again and where you’ve got everything. You can just replace that image and you’re done.

<span class="smashing-tv-speaker">Rémi Parmentier: </span>  It’s also better for accessibility because you have a single image, you have a single element, so a single alt attribute. This is simpler and better for accessibility. One thing it’s also better for is for web performance, because downloading 100 kilobytes image is theoretically faster than downloading five image of 20 kilobytes.

<span class="smashing-tv-speaker">Rémi Parmentier: </span>  That’s because for each image of 20 kilobytes, the request to the server needs to be made and we need to wait the answer five times. Even for the really small micro-transactions between the client and the server, this add up the more image you have, and it can slow down the download of your email image, so this is something to avoid.

<span class="smashing-tv-speaker">Rémi Parmentier: </span>  Next, on the WebKit, there’s also a very weird behavior. Whenever you use a CSS transform on sliced images, WebKit will have very thin lines between split images. I would just show you a demo of this as well. Back to my first T-Rex image here, if I add a small transform here that will scale the image, here you can see that at this ratio, there are very small lines that appear within each slices of my image.

<span class="smashing-tv-speaker">Rémi Parmentier: </span>  This is really due to WebKit not handling well the way they should scaled images like this. Maybe there’s a node size somewhere and it doesn’t compute properly, so you end up with small hair lines like this. Yes, the best practice here is to avoid to split your visuals.

<span class="smashing-tv-speaker">Rémi Parmentier: </span>  This is actually something that will happen inside email clients because in Outlook.com, for example, if your email is bigger than the actual view of emails inside the clients, then your email will be resized using a CSS transform to feed the view port of the email client. This is something that you should be wary of.

<span class="smashing-tv-speaker">Rémi Parmentier: </span>  Finally about splitting visual, I always try not to do it because this kind of things happens. This is something that was shared on Reddit almost 10 years ago. This is an email by LinkedIn and the face of this young lady, it was cut in half, maybe because some text was longer than expected or maybe because here the user chose to set up his email client with a bigger font than expected, so all kind of things can happen inside email clients, just like on the web. If you want to avoid these kind of strange situations, just don’t split visuals.

<span class="smashing-tv-speaker">Rémi Parmentier: </span>  Next, this is a big one. This is tables for layouts. This surely is the most common thing that people think about when they think about HTML emails. It always annoys because we mostly don’t really need tables for layouts, except for one email client, and that is the Outlooks on Windows from 2007 to the latest 2019 version.

<span class="smashing-tv-speaker">Rémi Parmentier: </span>  The reason of that, as we said before, is because all of those versions of Outlooks use Word as a rendering engine. Word is not really good in interpreting HTML and CSS. There is this documentation online about what it should be capable of, but it’s pretty hard to read and to make sense of, so I try to make this diagram to actually make sense of it.

<span class="smashing-tv-speaker">Rémi Parmentier: </span>  From this documentation, what it says is that CSS supports in Outlook will actually vary from which elements you use CSS on. It will be different in body and span than in div and p and then all the other supported HTML tags.

<span class="smashing-tv-speaker">Rémi Parmentier: </span>  First, if you have a body and span, you can only use what Microsoft calls Core CSS properties. That’s the color property, the font, text align and background color property. On the body element and the span element, you can only use those four CSS properties.

<span class="smashing-tv-speaker">Rémi Parmentier: </span>  Then, on divs and paragraphs, you can use all those four properties from the Core level, but you can also use two new properties from what Microsoft calls the Coreextended level. In this level, you have two new properties, the text indent and margin properties.

<span class="smashing-tv-speaker">Rémi Parmentier: </span>  Then, for all the other tags, you can use properties of the two previous levels, and you have what Microsoft calls the Full CSS support with many more CSS properties, but I think the most interesting are the width, height, padding, border and this kind of properties for defining elements.

<span class="smashing-tv-speaker">Rémi Parmentier: </span>  This means here that if you want to use width and height properties and make it work in Outlook, you won’t be able to do this on a div because div only support Coreextended and Core CSS properties. You will need to use tables for those CSS properties, and the same thing for padding and border.

<span class="smashing-tv-speaker">Rémi Parmentier: </span>  I usually narrow it down to the few following guidelines to use tables. I try to only use a table when I want to set a fixed width on an element. If I need an element to be a certain width, then I will use a table and define the width from that table.

<span class="smashing-tv-speaker">Rémi Parmentier: </span>  Also, if I want to set two block elements side by side, because even Outlook doesn’t really support any advanced CSS layout property, so even float is not really well-supported, so if you need to have two elements side by side, then as you make a table with two cells, and those two elements will be next to each others then. Then I use tables whenever I need to set a padding, a background color or border style. This make it very reliant, very robust to use a table for those styles only.

<span class="smashing-tv-speaker">Rémi Parmentier: </span>  Now a problem with tables is something we’ve learned in the way a long time ago is that tables are not made for presentation. They are made for actual data tables. This can be very problematic for screen readers especially. In order to improve accessibility here, we will use the role=presentation attribute whenever we will make a layout table.

<span class="smashing-tv-speaker">Rémi Parmentier: </span>  Let me show you a quick example of how this will change the way your email is interpreted by a screen reader. I will take a new demo here. I’ve got this email from Jacadi, which is a French children clothing brand. They have this table here with different sizes of products. This is actually a table inside the code. I’ve pre-recorded a video here to show you how this is read by a screen reader.

 <strong>Screenreader:</strong> Counting pairs, web content. Blank, blank, blank. Table 1 column. Nine rows. Blank. Column 1 of 1. Row 2. Nine Level 2 tables, seven columns. One row, Column 1 of 1. Blank. Column 3 of 7. Blank. Column 4 of 7. Blank. Column 5 of 7. Blank. Column 7 of 7. End of table. Row 3 of 9, blank. Column 1 of 1. Row 4 of 9, Row 2 table, seven columns, one blank. Column 1 of 7. Blank. Blank. End of table. Row 5 of 9, blank. Row 6 of 9, blank. Column, blank, blank, column end of table. Row 7 of 9, blank. Row 8 of 9 Row 2 table, blank. Column 1, blank. Column end of table. Row 9 of 9 blank. Column end of table.

<span class="smashing-tv-speaker">Rémi Parmentier: </span>  This is terrible. This is so annoying. Now let’s see how we can fix these cells. The way we can fix this is by adding the role=presentation attributes. This is not something that it reads from tables to tables, so we need to add this attribute whenever we’ll have a new table. We have a few nested tables here, so we’ll add a few. Here is how the results sound.

<strong>Screenreader:</strong> Blank. Blank. Voice-over off.

<span class="smashing-tv-speaker">Rémi Parmentier: </span>  This is so much better. This is so much smoother and it makes for much nicer experience. I hope this convinced you that you should always use as less tables as you can, but if you do, use role=presentation attributes on those tables.

<span class="smashing-tv-speaker">Rémi Parmentier: </span>  Now, one step that we can take even further is that since tables are mostly for Outlook, we can use conditional comments to make those tables only visible on Outlook. Conditional comments are actually something that was available in Internet Explorer as well until I think I9. With these, if MSOs are in text, we can tell the borders that all the following contents within that conditional comment will be available only for MSO clients, so that’s mostly Outlook.

<span class="smashing-tv-speaker">Rémi Parmentier: </span>  Then, between those opening and closing tables comments, we can have a div with a role or stuff that will come just like for a regular web border, although webmails will pick the div and Outlook will pick the table. This is video how I got most of my emails.

<span class="smashing-tv-speaker">Rémi Parmentier: </span>  Now another small good practice to have is to use margin or padding for spacing. This is mostly to avoid empty containers, empty cells like this where we have a role within a cell with a height of 20 and then we have TDs with width of 20 to create margin all along with this content. I still see this done a lot, and this make your code really, really heavy. It’s less readable and it’s really bad in my opinion.

<span class="smashing-tv-speaker">Rémi Parmentier: </span>  The proper way to do something like this would be to use a table as well if you want and have the padding style on the first TD, and then inside use margin to space tags between each others. This works again really well in every popular image client and in Outlook as well.

<span class="smashing-tv-speaker">Rémi Parmentier: </span>  Now the small quirk that can happen in the Outlook and Windows is that there is the background color. If you use the background color on any of these elements with margin, it actually bleeds through the margin. Here’s an example where I should have a margin between the red background and blue background, but in Outlook, the margin is actually the same color of the background of that element. In those cases, then the solution is to maybe use another table and nest your content like this to space elements, but if you don’t use background, then margin is really safe even in Outlook.

<span class="smashing-tv-speaker">Rémi Parmentier: </span>  Finally, this is perhaps my favorite recommendation. It’s to make it work without style tags. It’s not necessarily about having this raw HTML rendering, but thinking about progressive enhancements and graceful degradation and about how your emails will look without this guideline. This is something pretty unusual in cooperation of the web because it doesn’t happen on the web, but not having a style tag actually happens a lot on email clients.

<span class="smashing-tv-speaker">Rémi Parmentier: </span>  First, not all email clients support style tags. Perhaps one of the most common example I see is Gmail on its mobile applications on iOS and Android lets you configure a third-party email address. You can use your Yahoo or Outlook.com address inside the Gmail app. If you do so, then every emails that you check won’t have support for style tags. This is what Email Geeks have nicknamed GANGA for Gmail apps with non-Gmail accounts. This is a very common occurrence that you can have.

<span class="smashing-tv-speaker">Rémi Parmentier: </span>  Then you have a lot of cases for smaller or local or international email clients like SFR in France or Yandex and Mail.ru in Russia, et cetera. Even to this day, there are a lot of email clients that don’t support style tag, so if you want to make your code more robust, make sure that it can work without style tag.

<span class="smashing-tv-speaker">Rémi Parmentier: </span>  Sometimes it’s also temporary. For example, in the past year or so, Gmail has had two days where style tags were completely removed from every email on every one of their email clients. We don’t know why this happened. There has been zero communication on that, but there’s a good chance that maybe they detected some kind of attacks that use certain styles, and so they needed to remove it very fastly and secure their users, so they removed style tag support for a few hours or almost a day. If you were to send a campaign that day, you were out of luck if your emails required style tags to work.

<span class="smashing-tv-speaker">Rémi Parmentier: </span>  Sometimes also it’s contextual. For example, in Gmail, when you forward an email to someone, then you won’t have any style tags anymore, or when an email is viewed in its unclean version, you know when you have a view entire messaging at the bottom of your email because it was too long, if you view your email in that window, you won’t be able to have a style tag.

<span class="smashing-tv-speaker">Rémi Parmentier: </span>  Then finally, sometimes it’s buggy. For example, in Yahoo Android in the app, the head is removed, so every style tag inside it are removed as well, but only the first head. We don’t really usually think as HTML documents are in multiple heads, but you can actually totally do this.

<span class="smashing-tv-speaker">Rémi Parmentier: </span>  This has been pretty much a common practice now for a few years to deal with this bug in Yahoo. If you have a second head with your style with it, then it will work fine in Yahoo Android and in most email clients as well. We have just this empty head first so that Yahoo will strip it, and this will work.

<span class="smashing-tv-speaker">Rémi Parmentier: </span>  Now, what I mean by making an email works is that the email should adjust its layer to any width without horizontal scroll and the email should reflect the branding of the sender. This can be colors often, this can be fonts or whatever, but make sure that it works without styles.

<span class="smashing-tv-speaker">Rémi Parmentier: </span>  In order to do this, we can use inline styles. This is why most emails still use inline style, and I really recommend to do this for most of your styles. Make sure that the brand, the colors and everything can come up with just inline style.

<span class="smashing-tv-speaker">Rémi Parmentier: </span>  Then, to tackle mobile emails to make sure that your emails can work fine from desktop to mobile, we have different solutions. The first one is to make your email fluid. I’ve got a little demo here as well, which I will show you right now.

<span class="smashing-tv-speaker">Rémi Parmentier: </span>  This is an email that I’ve worked on almost four years ago for a French magazine, GEO. It’s got a lot of interesting things here. The first one is this grid here. If I try to resize it to make it responsive, you can see that it’s 100% fluid and it will scale accordingly to whatever the width for the image client is.

<span class="smashing-tv-speaker">Rémi Parmentier: </span>  This works absolutely well without even a single style tag. This is just two tables on top, one for each lines, and we’ve got image inside it and the image are set with a fluid width, and so this works well enough even without style tags. This is good to have elements like this that can scale accordingly.

<span class="smashing-tv-speaker">Rémi Parmentier: </span>  Now, this might not be the most optimal for every email, so another technique is to make your content hybrid. "Hee-breed," or "hi-breed," I’m not sure how you pronounce it, sorry for that, hybrid comes from the fact that you can still use media queries, but only as progressive enhancements, and then you need to make sure that your layout can fall back gracefully even without styles.

<span class="smashing-tv-speaker">Rémi Parmentier: </span>  I would go back to this exact same email that I just showed you. A little bit lower here, we’ve got this gallery of user portraits. We can scale it as well. We have three columns here and then it will get on to two columns, and then only to one column.

<span class="smashing-tv-speaker">Rémi Parmentier: </span>  The way this works here is using div width display in my block. We’ve got actually three divs like this next to each others and they all have a width of 33%. They will set so three can sit next to each others. They all have a minimum width of 140 pixels, so if there is no longer enough room to fit all those three elements because they’re in display inline block, they will naturally match even CSS flow down next to each others. This is a pretty good way to make it work like this.

<span class="smashing-tv-speaker">Rémi Parmentier: </span>  I also use CSS and media queries here to make it a little bit more graceful when you have content here. If I disable the styles here, if I remove all of this, you can see that the layout has changed a little bit. We still have two columns, but they’re more stuck together. The layout still works appropriately where we can go from three to two to one layouts even without any styles, just with both div display and line blocks.

<span class="smashing-tv-speaker">Rémi Parmentier: </span>  Then, perhaps the final, most popular way to make your emails work on mobiles is to make them mobile-first, to code them mobile-first. I will once again go back to that exact same email. You can see here that ... Oops, it’s not fitting. I’ve got these two email columns next to each others. If I resize my window a little bit smaller, they will stack on each others.

<span class="smashing-tv-speaker">Rémi Parmentier: </span>  Now because this is coded mobile-first, it means that this is actually the default layout for this zoom. On them, I use a min-width media query to change the layouts on desktop, on larger window sizes to make this work. If I remove all the styles here, just like I did before, you can see that now, our images are stacked on each others just like on mobile. This is what you’ll get when you code mobile-first. You get mostly your mobile view, but larger on desktop. This is really a lot of considerations to have when you’re coding emails for mobiles and for every email clients.

<span class="smashing-tv-speaker">Rémi Parmentier: </span>  That’s pretty much it for me. All those recommendations, all those guidelines, you can find them online on GitHub, where I have these documents available. I really strongly encourage you really to share it within your colleagues and also to contribute to it.

<span class="smashing-tv-speaker">Rémi Parmentier: </span>  If you think you have good recommendations that could apply to every emails you will code, feel free to share with me, feel free to contribute to this document as well. Hopefully you will have some questions. You can find me on Twitter or on my blog or you can send me an email as well if you have any questions after this session. Thank you.

<span class="smashing-tv-host">Scott: </span> Thank you very much, Rémi. "Re-my." That was really very good. I’ve had a lot of questions about ... Oh, hey, Vitaly.

<span class="smashing-tv-host">Vitaly: </span> Hello. Hello, Rémi. I’m so sorry about being late. Hello, everybody, dear Smashing members. I had a train delay and all. Scott, you wanted to say something? Sorry I interrupted you.

<span class="smashing-tv-host">Scott: </span> No. There was just two questions I was going to get out of the way. One was from Pawan, who’s a very, very active member of the Smashing membership. He is asking us, any thoughts on applying fonts consistently through HTML email?

<span class="smashing-tv-speaker">Rémi Parmentier: </span>  Sorry, can you repeat?

<span class="smashing-tv-host">Scott: </span> Do you have any thoughts about applying fonts consistently through HTML email?

<span class="smashing-tv-speaker">Rémi Parmentier: </span>  Yes. Well, for fonts, I usually encourage my clients to use web fonts in emails because it’s always better when you can have your own brand fonts. Now the thing to have in mind is that it won’t work everywhere. When using web fonts, especially, it almost works nowhere. It works in Apple Mail and in Thunderbird and maybe a few local email clients, but that’s really it. It doesn’t work in Gmail, it doesn’t work in Yahoo. If you can adapt to that, if that’s good for you, then go ahead and do it.

<span class="smashing-tv-speaker">Rémi Parmentier: </span>  Now, the problem that you can have with web fonts like this is that if you try to use really funky fonts like Lobster or Pacifico on Google fonts, if it falls back to something like Arial or Helvetica, your email will definitely look very, very different. If you can use Montserrat and it falls back to Helvetica, that’s less a problem in my opinion. It really depends on the fonts you want to use and how much you are ready to not have this font in the cases where it won’t work.

<span class="smashing-tv-host">Scott: </span> That’s a really good point. There’s Zach Leatherman, who’s a very active member with Smashing and a presenter at SmashingConf, he’s done a lot of presentations about the fallback on fonts, so that’s interesting to make that correlation between email and web-based fonts.

<span class="smashing-tv-host">Scott: </span> Before I hand it over to Vitaly, my other question is, a lot of people are talking about interactive emails. There was actually, not this past SmashingConf, I believe the SmashingConf before, there was a presentation about interactive emails where you can actually complete an action just with one click of a button in an email, and mostly it’s based on AMP email. I was just curious, what do you know, what is AMP email and what’s the support for it currently?

<span class="smashing-tv-speaker">Rémi Parmentier: </span>  AMP for Email is still something relatively new. It was announced by Google about a year ago, but it was only made available in Gmail desktop webmail about a few months ago, I think, in maybe April or something. AMP for Email is basically bringing the AMP Javascript framework to HTML email so that now inside Gmail, you can use interactive components like carousels or accordions, and you’ve got also, more interestingly, in my opinion, have live data.

<span class="smashing-tv-speaker">Rémi Parmentier: </span>  If you’re selling clothes, for example, you can make sure that the clothes you’re presenting in your email are available in stock and are the ones in the best interest for your customer that’s viewing this email. This brings a lot of new customizations and possibilities for emails like that.

<span class="smashing-tv-speaker">Rémi Parmentier: </span>  The thing is that it’s very still in its infancy and it mostly only works on Gmail desktops so far. It should come in on Gmail mobiles in the coming months, but then, there is also Yahoo and Outlook.com I think who said they were interested in implementing it.

<span class="smashing-tv-speaker">Rémi Parmentier: </span>  Maybe this is something that will actually grab attention and go in the future. Yes, this is something I’m looking into and I’m really interested in. It’s still very hard to say if it will work and be successful, but there are a lot of interesting things in it.

<span class="smashing-tv-host">Scott: </span> Definitely. That falls back on what I was asking at the beginning before you started the presentation is, is there going to be some sort of standard that comes across for email clients? That’s my dream is that that will happen. On that note, Vitaly, I’m going to hand over to you for some questions.

<span class="smashing-tv-host">Vitaly: </span> Excellent. Thank you so much, Scott. Actually, Rémi, that was a brilliant presentation. Thank you so much. I learned-

<span class="smashing-tv-speaker">Rémi Parmentier: </span>  Oh, thank you.

<span class="smashing-tv-host">Vitaly: </span> ... a lot. I was a little bit not shocked, but in a way, I felt like it’s just wrong that we’re preaching these best practices for email which are not necessarily best practices full stop in 2019. It’s really about time that web standards have evolved.

<span class="smashing-tv-host">Vitaly: </span> We do have an open question from Pawan. Just before we do that, I have a couple, but one thing I wanted to know from somebody who’s so deeply motivated by the beauty and horror of email, I do have to find out, do you sleep well at night?

<span class="smashing-tv-speaker">Rémi Parmentier: </span>  Oh, yes.

<span class="smashing-tv-host">Vitaly: </span> Excellent.

<span class="smashing-tv-speaker">Rémi Parmentier: </span>  It depends because I have two small children, so not every night, but it’s not because of email.

<span class="smashing-tv-host">Vitaly: </span> Okay. The thing is, if you look back, let’s say, over the last, I don’t know, how many years have you been now in this madness?

<span class="smashing-tv-speaker">Rémi Parmentier: </span>  Almost 15 years, but I really started digging into emails maybe five years ago, or maybe a little bit more, but yeah, about five years.

<span class="smashing-tv-host">Vitaly: </span> I’m curious, then, do you see that there has been a lot of progress in terms of email client supporting new features, broadening CSS support, Gmail, support of media queries and all? Do you see that the differences have been remarkable over the last five years or is it a very slow progress? Just so we can set expectations of what we should be expecting coming up next on the platform.

<span class="smashing-tv-speaker">Rémi Parmentier: </span>  I would say both. It’s been both slow, but there has been progress. If you look back five years ago, five years ago, Gmail didn’t support media queries, and neither did Yahoo, I think, and neither did Outlook.com. Media queries are a huge tool to make email works well on mobile. The simple fact that those emails were able to adapt and add this to their list of CSS properties and features supported is actually a very good thing.

<span class="smashing-tv-speaker">Rémi Parmentier: </span>  Now, it’s always a bit frustrating because it definitely doesn’t move as fast as the web is moving nowadays where you can see new features added in Chrome or Firefox every week and new articles about it. Things are moving slowly for really unknown reasons. That’s perhaps the biggest problem of emails is that everything is really opaque.

<span class="smashing-tv-speaker">Rémi Parmentier: </span>  We don’t know how things work within Gmail or within Outlook and we have a lot of advantages for the web, people from the Chrome team, from the Firefox team sharing all the new advances in their browsers, but this is not the case in email clients, and this is really perhaps the most frustrating thing is that if you see a bug, if you have a problem, you pretty much have no one to talk to.

<span class="smashing-tv-host">Vitaly: </span> It’s a little bit loud here. I’m just in a park, I promise. Pawan is wondering, do you have any thoughts on embedding HTML forms in emails? Is it a good idea or not?

<span class="smashing-tv-speaker">Rémi Parmentier: </span>  It can work. This is actually something that’s done a lot by us in the presentation you mentioned. Mark Robbins was the godfather of interactive emails. A lot of people actually use form in emails. Just like everything, you just need to realize that this won’t work everywhere. You need to think about, what happens if my form doesn’t work? Do I show something different? Do I have a link that sets to a form on my website? This is perhaps the hardest part, when you try to think of advances in emails like that. Every time, you need to think about what happens if this doesn’t work and what will I show to the people when it won’t work.

<span class="smashing-tv-host">Vitaly: </span> That makes sense. Well, I have so many questions. If you do have a few minutes, I just wanted-

<span class="smashing-tv-speaker">Rémi Parmentier: </span>  Yeah, sure.

<span class="smashing-tv-host">Vitaly: </span> Because just today, I had to send out a wonderful email to our wonderful Smashing subscribers. One thing that stuck with me, and I wasn’t really sure how to deal with it. Not every client who understand media queries. Gmail does. You will have the media rule and then it will be all fine, but then, for some reason, when we’re sending out with Mailchimp and we do inline styles, actually inline styles in the attributes, what happens is you have the inline styles say font size 21 pixel, let’s say, on H2. Then you have a media that overrides it with font size 28 or something else.

<span class="smashing-tv-host">Vitaly: </span> Am I correct to assume that it’s probably a good idea to avoid bang importance one way or the other, because it will override whatever you have in the inline styles? If you have a media rule, and then that media rule, you actually have font size 30 pixels importance, will it override inline styles or not in most-

<span class="smashing-tv-speaker">Rémi Parmentier: </span>  Yeah, definitely importance will override inline style.

<span class="smashing-tv-host">Vitaly: </span> But then it’s included in the media rule, right? If a client doesn’t understand media, they wouldn’t know-

<span class="smashing-tv-speaker">Rémi Parmentier: </span>  Yes, exactly. Yes, which is why you once again need to think what happens if media is not supported. There, your inline style will be picked up. Maybe you will need to have the mobile-first approach and have the smaller font size inline and then use a min-width media query to have the different font size on desktop.

<span class="smashing-tv-host">Vitaly: </span> Makes sense. When you start building, do you actually build mobile-first or do you build desktop-first?

<span class="smashing-tv-speaker">Rémi Parmentier: </span>  Well, it really depends. As I just show in my last three examples between-

<span class="smashing-tv-host">Vitaly: </span> Oh, sorry, I must have missed a few things.

<span class="smashing-tv-speaker">Rémi Parmentier: </span>  Yeah. Between the three examples or if we do mobile-first, these are different approaches that you can have and that makes sense, depending on the contents you have. Most of the time, I usually go mobile-first, but it really depends on how you want your fallback to display. Sometimes it makes sense to have more desktop layouts and sometimes it makes more sense to have more mobile layouts.

<span class="smashing-tv-host">Vitaly: </span> For testing, we’re using Mailchimp just to see how it looks in different clients, but Doug Working is asking, do you have any recommendations for tools to test email code to see how it looks in different email clients?

<span class="smashing-tv-speaker">Rémi Parmentier: </span>  Yes. There are two very good and very popular email tools that will allow you to take screenshots of how your email render across many, many email clients. Those are Litmus and Email on Acid. They work really similarly for email testing.

<span class="smashing-tv-speaker">Rémi Parmentier: </span>  You just import your code and you will get screenshots very fast of how your email looks. This is really how I recommend to test emails because, of course, you need to do some ports manually as well, but it’s so much faster when you have a tool like this that it’s really more professional and you will win a lot of time by working with tools like this.

<span class="smashing-tv-host">Vitaly: </span> But then, it basically takes screenshots that you have to analyze. If you discover something like a major bug, how do you debug? Any tools for remote debugging, so to say?

<span class="smashing-tv-speaker">Rémi Parmentier: </span>  Yeah. Debugging is the hardest part. In webmails, actually, it’s pretty easy because since the webmail is just a webpage, you can fire up your browser inspector tools and inspect the webmail’s code. This is really something interesting to do. I encourage everyone to do it at least once in a while because you will see how the webmail transforms your code in ways that you maybe have never imagined, like prefixing and renaming the classes you can have in your code.

<span class="smashing-tv-speaker">Rémi Parmentier: </span>  This is a good way to see if maybe an image client has removed some of your styles or maybe if you did a mistake somewhere. For webmail, this is the best way to debug. For other email clients like Outlook, this is really a try-and-retry approach where you just send a code, change something, resend the email-

<span class="smashing-tv-host">Vitaly: </span> It sounds like fun.

<span class="smashing-tv-speaker">Rémi Parmentier: </span>  Yeah, this can be a bit irritating. With the experience, you do less and less of this, but yes, unfortunately, there are no developer to see in Outlook.

<span class="smashing-tv-host">Vitaly: </span> That makes sense. One more thing that actually came up as well, is it safe to use SVG in emails? Or if you’re having the same image, would you prefer to use SVG or would you recommend to stay away from SVG and use PNG or JPEG instead, or God forbid GIF?

<span class="smashing-tv-speaker">Rémi Parmentier: </span>  GIFs are actually still very popular in email-

<span class="smashing-tv-host">Vitaly: </span> I know. I noticed.

<span class="smashing-tv-speaker">Rémi Parmentier: </span>  ... but there are actually no reason because PNG is just as well-supported as GIFs for that matter. Regarding SVGs, just as my previous answers, I will say do it if you can manage to make it fall back to something I think for other email clients.

<span class="smashing-tv-speaker">Rémi Parmentier: </span>  I think SVG works very well in Apple Mail, in Mac OS and iOS. It might work in a few more email clients, but I don’t think it works well in webmails. If you can have a distant SVGs that you call maybe in ... For example, if you use a picture tag, you can have a source with your SVG, so this will be picked up by Apple Mail. Inside this picture, you can have an image tag as a fallback with a regular PNG or JPEG. This will work in other email clients.

<span class="smashing-tv-speaker">Rémi Parmentier: </span>  There are different ways to tackle this kind of things, but SVG is definitely not the first format for images that you were shown when you built emails, but this is definitely something you can use, even though it won’t work everywhere. If you can have the proper fallback, then go ahead and use it.

<span class="smashing-tv-host">Vitaly: </span> Willow Cheng is asking, would you have recommendation on design tools which could let you design and export email in HTML?

<span class="smashing-tv-speaker">Rémi Parmentier: </span>  No. Unfortunately, nothing that I can think of right now. Because most of the time, tools that will offer you to generate your HTML from design tool will be really rubbish because it will be either completely outdated and not work well in most modern versions of email clients, so I would actually recommend to stay away from those tools. From design point of view, I’m not sure there are any tools that will let you export clean, proper HTML for emails.

<span class="smashing-tv-host">Vitaly: </span> That’s actually an answer I was expecting, to be honest. Maybe just one final question. I’m sure I’ll have more later, but I know you do also have family and all and it’s quite late as well, and I get to meet you in Freiburg, so this is just a couple of weeks from now, so at SmashingConf Freiburg. This is going to be exciting.

<span class="smashing-tv-host">Vitaly: </span> I do have a question, though, still. I remember for a while, maybe a year ago, maybe two years ago, I found these two resources which were great. One of them was responsiveemailpatterns.com. The other is responsiveemailresources, or something like that, .com. One of them has gone away. It’s just down I think at this point, but I will also post the link later. Can you recommend some websites, resources where you can get copy-pastes almost email codes, snippets or something that you can reuse on a daily basis? I have heard that you might be working on something. Was I wrong?

<span class="smashing-tv-speaker">Rémi Parmentier: </span>  I’m not sure, but I won’t talk about this for now, but it’s always [inaudible 01:04:56] snippets of codes that you can share because there are a lot of factors inside an email that can make your code behave differently. Every time there’s a tool that says it makes bulletproof backgrounds or bulletproof buttons, for example, you can always very easily, very shortly find email clients in which this doesn’t work properly. This is always a problem.

<span class="smashing-tv-speaker">Rémi Parmentier: </span>  I remember the websites we were talking about, about responsive patterns, but I actually don’t know who were maintaining those. I don’t think they are ever really updated. As for websites, I can’t think of any right now. Maybe it will come later, that’s too bad, but the two things I will recommend is, if you’re into Twitter, follow the Email Geeks hashtag. That’s #emailgeeks, G-E-E-K-S. There are always a lot of people sharing good resources and the latest good articles that are always interesting.

<span class="smashing-tv-speaker">Rémi Parmentier: </span>  The other thing I recommend is to join the Email Geeks at Slack channel. This is a really good community that’s growing a lot. There are all sorts of channels for marketing or for design or for code. People are really, really nice there and really always trying to help and almost available at any hours of the day, so this is incredible. If you look up for Email Geeks Slack on Google, you will see a subscription page that you can join. I hope you can join and just say "Hi" if you come.

<span class="smashing-tv-host">Vitaly: </span> Just one final, just the really, really last one, and then I’ll let you go. Sorry, excuse me if you mentioned it already in the session, but I’m wondering, as of today, as of 2019, looking at the best practices and the email clients, what are the baseline where you would say, let’s support this kind of client?

<span class="smashing-tv-host">Vitaly: </span> Because at this point, when we think about a 8, sometimes you obviously want to search something accessible to a 8, but you’re not going to optimize for a 8. We’re getting to the point where some companies can actually start dropping a 9 in the same way, but again, we’re quite far away yet.

<span class="smashing-tv-host">Vitaly: </span> When it comes to email clients, is Outlook 2013 still a thing? I remember the big update that Outlook brought in 2013 changed a lot of things in email, if I remember correctly. As of today, when we look into the landscape of email clients, what is the baseline we absolutely have to support at least?

<span class="smashing-tv-speaker">Rémi Parmentier: </span>  I think the-

<span class="smashing-tv-host">Vitaly: </span> To support.

<span class="smashing-tv-speaker">Rémi Parmentier: </span>  The others' basis is Outlook 2007, because this is something actually pretty annoying is that this is used in a lot of big companies, and those big companies don’t pays new license for new versions of Outlook every year and they pay for a decade or so. There are still quite a lot of people I think using those older versions. This is still something that we have to account for.

<span class="smashing-tv-speaker">Rémi Parmentier: </span>  Now, it’s not really that much a problem because between Outlook 2007 and Outlook 2019, unfortunately there weren’t that much of progress made because it’s still Word as a rendering engine. I think this is maybe the worst case we have to support mainly because, yes, we are not getting rid of those versions of Outlook anytime soon, I think.

<span class="smashing-tv-host">Vitaly: </span> That’s very optimistic, a bright outlook in life. I like that. I respect that. Thank you so much, Rémi, for being with us today and sharing all the wonderful insights.

<span class="smashing-tv-speaker">Rémi Parmentier: </span>  Thank you for having me.

<span class="smashing-tv-host">Vitaly: </span> Of course. Will you be kind enough to share the slides of your presentation as well?

<span class="smashing-tv-speaker">Rémi Parmentier: </span>  Yes, absolutely.

<span class="smashing-tv-host">Vitaly: </span> If you have any other resources that come to your mind, please send them over to us and we’ll publish them, too.

<span class="smashing-tv-speaker">Rémi Parmentier: </span>  Sure.

<span class="smashing-tv-host">Vitaly: </span> All right? That’s been very exciting. It wasn’t actually as dirty as I thought it would be. Just humble in a way, even. I didn’t see anything that would screech and make me feel uncomfortable at night when I want to sleep. Thank you so much for that, Rémi.

<span class="smashing-tv-speaker">Rémi Parmentier: </span>  Thank you.

<span class="smashing-tv-host">Vitaly: </span> On that note, Scott, any other updates we should keep in mind or anything we need to mention?

<span class="smashing-tv-host">Scott: </span> I was going to ask you, Vitaly. Tomorrow, we have another Smashing TV.

<span class="smashing-tv-host">Vitaly: </span> Yes. Friends, we’re trying something else and something new every time. Apparently, well, finally, today we got ... I hope we received, because I didn’t get the confirmation yet, but we’re supposed to receive the first copies of the Smashing Print or our new printed magazine dedicated to topics that are often not covered well enough on the web, or maybe that just got lost in the myriad of workflows.

<span class="smashing-tv-host">Vitaly: </span> The first issue is dedicated to ethics and privacy. As a dedication to that, we’re going to have a live session, a live stream on Smashing TV tomorrow with five panelists, all contributors to this first issue of Smashing Print. It’s going to be broadcasted on YouTube. If you go on Smashing.TV, you’ll find the links, but we also will be publishing an article tomorrow featuring the links and everything.

<span class="smashing-tv-host">Vitaly: </span> The printed magazine, that by the way, Smashers, the ones with $9 plan are getting it for free, and the members with $5 plan are getting the ebook and the heavy discount on the ebook as well. Rémi is getting a printed magazine as well just because he’s so awesome.

<span class="smashing-tv-speaker">Rémi Parmentier: </span>  Thank you.

<span class="smashing-tv-host">Scott: </span> Thanks, Rémi.

<span class="smashing-tv-host">Vitaly: </span> Beyond that, we also have a few more things coming up, I think.

<span class="smashing-tv-host">Scott: </span> On the 13th, Mr. Paul Boag, who has been a very prominent mentor in the Smashing community, many Smashing Conferences, many webinars, August 13th, Paul Boag is doing the customer journey mapping where UX and marketing meet.

<span class="smashing-tv-host">Vitaly: </span> Then we have Cassie Evans on August 20th exploring the interactive web animation with SVG. This is going to be fun as well. If you actually ever wanted to do a bit more or try to figure out a better workflow for SVG animation, that’s definitely a session not to miss, so looking forward to that.

<span class="smashing-tv-host">Vitaly: </span> All right, I think we’re good here. Any more announcements, major announcements, Scott, that we need to share with the world around us?

<span class="smashing-tv-host">Scott: </span> You’re making me feel like I’m forgetting something, but ... SmashingConf Freiburg?

<span class="smashing-tv-host">Vitaly: </span> Yes, we do have a SmashingConf Freiburg, where Rémi is going to speak as well, but we also have the videos of Toronto conference which will be released today, or maybe tomorrow. Maybe they already released. See how well-prepared I am. Watch out for that and you’ll get them, you’ll find them also in your dashboard, so keep that in mind. All right. I think we’re good!

<span class="smashing-tv-host">Scott: </span> Okay. Thank you everybody for attending. Thank you-

<span class="smashing-tv-host">Vitaly: </span> Thanks, everyone, for attending.

<span class="smashing-tv-speaker">Rémi Parmentier: </span>  Bye! Thank you and bye.

<span class="smashing-tv-host">Vitaly: </span> Thank you and see you next time. Thank you, Rémi. Bye-bye.

<span class="smashing-tv-speaker">Rémi Parmentier: </span>  Thanks. Bye.

<span class="smashing-tv-host">Vitaly: </span> See you next time.

## SmashingConf Freiburg Presentation “Think Like An Email Geek”

At the end of the Webinar, Vitaly mentions that Remi will be speaking at Freiburg. You don’t have to wait for that as we also have that video to share with you, along with the [slides and resources](https://noti.st/hteumeuleu/16YThT/think-like-an-email-geek).

{{< vimeo id="362137699" >}}

We hope you enjoyed this look into HTML email. If you would like to enjoy more of this kind of content, plus the chance to interact with the presenters and other members while helping to support the creation of independent content for web designers and developers <a href="https://www.smashingmagazine.com/membership">join us here</a>.

{{< signature "ra, vf, il" >}}
