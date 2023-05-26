---
title: User Interface Design - 12 Useful Techniques
slug: 12-useful-techniques-for-good-user-interface-design-in-web-applications
image: 'https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/afd7f1f5-fcc6-412e-978c-0f2929dc01c3/yammer-update.png'
date: 2009-01-20T04:00:31.000Z
author: dmitry-fadeyev
description: >-
  Last week, we presented [10 Useful Web Application Interface
  Techniques](https://www.smashingmagazine.com/2009/01/12/10-useful-web-application-interface-techniques/),
  the first part of our review of useful design trends in modern Web
  applications. Among other things, we highlighted embedded video blocks,
  specialized controls and context-sensitive navigation. We also encouraged
  designers to disable pressed buttons, use shadows around modal windows and
  link to the sign-up page from the log-in page.
categories:
  - UX
  - UX
  - Web Design
  - UI
  - Techniques
  - Personalization
  - Usability
  - Interfaces
---
Last week, we presented <a href="https://www.smashingmagazine.com/2009/01/12/10-useful-web-application-interface-techniques/">10 Useful Web Application Interface Techniques</a>, the first part of our review of useful design trends in modern Web applications. Among other things, we highlighted embedded video blocks, specialized controls and context-sensitive navigation. We also encouraged designers to disable pressed buttons, use shadows around modal windows and link to the sign-up page from the log-in page. 

This post presents the second part of our review: <strong>12 useful techniques for good user interface design in Web apps</strong>. We also discuss how to implement these techniques so that they are properly used. Please feel free to suggest further ideas, approaches and coding solutions in the comments below.

You may also want to take a look at the following related articles:

*   [5 Useful Coding Solutions For Designers and Developers](https://www.smashingmagazine.com/2008/08/11/5-useful-coding-solutions-for-designers-and-developers/)
*   [10 Principles Of Effective Design](https://www.smashingmagazine.com/2008/01/31/10-principles-of-effective-web-design/)
*   [Five More Principle Of Effective Design](https://www.smashingmagazine.com/2008/04/24/5-more-principles-of-effective-web-design/)

## 1. Highlight important changes

One of the most significant elements of a good user interface is <strong>visibility of the system's status</strong>. Users must notice immediately what's going on behind the scenes and whether their actions have actually led to the expected results. To achieve a more sophisticated level of system visibility, Web applications these days use AJAX (of course), which allows users to update portions of a Web page at any time without having to refresh the whole page. AJAX brings the level of responsiveness and interactivity of Web apps much closer to desktop-grade applications.

{{% feature-panel %}}

<a href="https://www.yammer.com/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c04e2b41-cfd2-4a66-a016-7f69ae8110e7/yammer-update.png" alt="User Interface Design" width="480" height="256" /></a><br>
<em><a href="https://www.yammer.com/">Yammer</a> applies not one but three effects on all new messages in a feed: fade in, slide down and highlight.</em>

However, this dynamic nature means that when you click on a button, the page doesn’t refresh but something <em>does</em> happen. The majority of websites still don’t use AJAX extensively, so some users may not be sure whether anything has happened at all or whether the button was properly clicked. To fix this, you need to provide some <strong>visual feedback</strong> for each of the user’s interactions.</p>

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d00c2660-4547-4eef-a1de-3ce3b9791442/backpack-highlight.png" alt="Backpack new task highlight" width="480" height="181" /><br>
<em>Backpack applies a highlight effect to all new items in a task list, which lasts for a second before fading out.</em>

One great way to do this is with animation. The human eye can <strong>notice movement</strong> fairly well, especially if the rest of the page is static. Playing a highlight animation when users add items to their shopping carts, for instance, will <strong>attract their eyes</strong> to those items. They’ll see that their action has worked. Animations can be implemented with JavaScript and are a nice way to provide visual feedback. Just be sure to not overdo it; adding too many animations could cause interface friction because the speed with which the user performs each action will be slowed down by the duration of the animation.</p>

## 2. Enable keyboard shortcuts in your web application

As the advanced features of modern Web applications (such as dragging and dropping, modal windows, etc.) steadily gain on those of desktop apps, developers of these applications are trying to offer users more responsive and interactive user interfaces. One of the techniques used to achieve this is the <strong>integration of keyboard shortcuts or navigation</strong>. Just as with classic applications, this little feature can significantly improve the workflow of your users and make it easier for them to get their tasks done.</p>

<a href="https://konigi.com/interface/mobileme-calendar-date-selector"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/edb941e9-a628-4625-84a7-df568a0294d3/action.gif" alt="User Interface Design" width="500" height="320" /></a>

In fact, various Web applications already use shortcuts (for example, <a href="https://docs.google.com/">Google Spreadsheets</a>, <a href="https://konigi.com/interface/mobileme-calendar-date-selector">MobileMe</a>, etc.), and even regular websites, such as <a href="https://www.ffffound.com">Ffffound</a> or <a href="https://www.boston.com/bigpicture/2008/10/earth_from_above_comes_to_nyc.html">Boston.com</a>, allow visitors to use them for basic navigation. Ffffound enables users to use shortcuts to switch from the thumbnail view to list view and vice versa (using "v"), go back to the top ("h") and navigate to the previous ("k") and next ("j") image. Boston.com also uses "k" and "j" for the same functions.

It's worth mentioning that your shortcuts should be intuitive and self-explanatory. For instance, it wouldn't make sense to make the shortcut letters for "Previous" and "Next" navigation too far apart from each other on the keyboard; rather, pick ones that are close together. The reason is, if a user makes a mistake and jumps to a page she doesn't want to visit, she can immediately return to her page without looking at the keyboard. The "j/k" configuration is one option. It would actually make perfect sense to have some common conventions for keyboard shortcuts used throughout various websites, but we haven't been able to detect such conventions thus far.</p>

<strong>How do you implement this</strong>? Essentially, you just have to use the <code>onKeyPress</code>-DOM event and manipulate the appearance of the document using the <code>window.scrollTo</code> function in JavaScript.

Ffffound.com uses an <code>onMouseDown</code> effect in its markup, which is not a good solution because it doesn't adhere to the <a href="https://www.smashingmagazine.com/2008/09/16/jquery-examples-and-best-practices/">main guideline of unobtrusive JavaScript coding</a>: Thou shalt separate JavaScript functionality from CSS style sheet and (X)HTML markup.</p>

<pre><code class="language-html">&lt;a id="float-navi-prev" href="javascript:void(0);"
	onmousedown="try { move_asset_auto(-1) ;} catch (e) { }"
	onclick="return false;"&gt;prev(&lt;span class="shortcut"&gt;k&lt;/span&gt;)
&lt;/a&gt;</code></pre>

<p>Here it would make more sense to use a JavaScript library instead (like jQuery) and call the element via its identifier or class. That's (almost) what <a href="https://www.boston.com/bigpicture/2008/10/earth_from_above_comes_to_nyc.html">Boston.com</a> does. All of the images in its gallery are labelled with the class <code>bpImage</code> in the markup, with the JavaScript pointers to them added to the array. The onKeyPress event triggers the scrolling window in the background, and the window's browser is manipulated using the <code>window.scrollTo()</code> function.</p>

Here is the (X)HTML:

<pre><code class="language-html">	...

	&lt;img src="[url]" class="bpImage" /&gt;
	&lt;div class="bpCaption"&gt;...&lt;/div&gt;

	&lt;img src="[url]" class="bpImage" /&gt;
	&lt;div class="bpCaption"&gt;...&lt;/div&gt;

	&lt;img src="[url]" class="bpImage" /&gt;
	&lt;div class="bpCaption"&gt;...&lt;/div&gt;

	...</p>

</code></pre>

<p>And the JavaScript:</p>

<pre><code class="language-js">function bpload(){ 

		// put pointers to all images with the class "bpImage" in an array
		imgArr = getElementsByClassName(document.body,"bpImage")
		isLoaded = 1;
	} 

	document.onkeypress = function(e) {
		if (!e) e = window.event; 

		// Pick up what key was pressed
		key = e.keyCode ? e.keyCode : e.which;

		// 107 is the ASCII code for 'k'
		if(( key == 107 ) &amp;&amp; ( isLoaded ) ) {

			// if there are images...
			if ( currImg &gt; 0 ) {

				// decrease the counter for the current image
				currImg--;

				// offsetTop returns the vertical coordinate of the
				// upper-left corner of the image
				// (we are not sure why the script adds 174px. Any idea?)
				window.scrollTo(0,imgArr[currImg].offsetTop+174)

			}
			else {
				if (currImg==0) {
					currImg--;
					window.scrollTo(0,325)
				}
				else
				{
					if (currImg&lt;0) {
						window.scrollTo(0,325)
						}
					}
				}
		}

		if ( ( key == 106 ) &amp;&amp; ( isLoaded )) {
			// a similar code snippet for 'j'
			...
		}
	} 

}

</code></pre>

<p>But you need to make sure that you clearly communicate that 1) keyboard shortcuts are available, and 2) they can be used to perform certain tasks more efficiently. If a user can easily manage his tasks with your application, he is less likely to switch to another application, if the feature set is more or less similar.</p>

## 3. Upgrade options from the account page

If your application features several subscription plans, make sure to <strong>remove any interface friction for customers deciding to upgrade</strong>. Most users like to try the basic version of an application first to get a better sense of what it offers and how it works. If they are convinced the application meets their expectations, they will consider upgrading to a more advanced plan. It's the designer's task to make sure this transition is as simple and intuitive as possible.</p>

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b664a500-7372-47a0-9afc-903a5c3ecb61/crazyegg.gif" alt="Crazyegg upgrade page" width="500" height="239" /><br>
<em>CrazyEgg integrates the option "Change plan" in its main navigation.</em>

In fact, a lot of Web applications <strong>put upgrade options right on the user’s account page</strong>, making them easily accessible. This design choice has the simple advantage of providing users with an overview of available options and supported functionalities right away.</p>

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7c79d344-3a1a-4446-8c01-113183565d19/cartel.jpg" alt="Bigcartel upgrade page" width="500" height="567" /><br>
<em>Bigcartel's upgrade plans are available in the app itself.</em>

Note, though, the importance not only of featuring the available upgrade plans, but also of identifying the plan that the user is <em>currently</em> using and the features that are <em>currently</em> available to her. It is vital to provide users with precise information about what advantages they gain by upgrading their account. Take a look at our article <a href="https://www.smashingmagazine.com/2008/10/13/pricing-tables-showcase-examples-and-best-practices/">Pricing Tables: Examples and Best Practices</a> as well.</p>

## 4. Advertise features of the application

Even though you’ve created a detailed marketing page, outlining your application’s every feature, and crafted a thorough help section on your website, your users are unlikely to have read it all. They’re probably not familiar with all the features of your product and would benefit from little tips inside the application itself.</p>

<strong>Advertise new features in your application.</strong> These would usually go in the sidebar, out of the way of the main functions. If a user is nearing the maximum capacity of a certain feature for her chosen subscription plan, you should point this out and give her an <strong>option to quickly upgrade</strong>.</p>

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bc35cd74-ca77-410a-a2bf-e93d811dc2b9/people.gif" alt="Freckle upgrade" width="500" height="264" /><br>
<em>The Freckle time</em>-<em>tracking app tells you when you’ve run out of people on your current plan. The message also links to actions you can take if you need to upgrade.</em>

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0179d603-82c3-4d61-b1d8-7596cfb4ee49/wufoo-small.png" alt="Wufoo feature highlight" width="480" height="70" /><br>
<em>Wufoo highlights its new form gallery feature at the bottom of the form creation page, making sure customers get the most value out of the app.</em>

## 5. Use color-coded lists

Some applications feature feeds that aggregate various types of content. For example, you may have a project management application that shows you all the latest messages, tasks and files on the home page. If these items all appear together in one list, it may be difficult to tell what’s what. Many applications use color coding to help <strong>visually distinguish between different types of entries</strong>. A simple way to do this is to place a text label inside a colored box. This way, the list becomes easily scannable.

It's important not to use various colors for the same task or similar colors for completely different tasks. The color scheme should not be random but should implicitly indicate the function each item serves.</p>

<a href="https://www.lighthouseapp.com"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/359c3a2d-d831-4362-806e-4284b6b63b77/lighthouse-color-codes.png" alt="Lighthouse color codes" width="480" height="208" /></a><br>
<em>The <a href="https://www.lighthouseapp.com">Lighthouse</a> issue-tracking app has color-coded labels on the right</em>-<em>hand side of each item on the overview page, which helps you quickly scan the list.</em>

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/eb8eccc7-f13d-4cef-a0d7-f6a352dd7780/goplan-color-codes.png" alt="Goplan color codes" width="480" height="282" /><br>
<em>The Goplan dashboard uses similar color</em>-<em>coded labels to differentiate various items, like tasks, notes and files, so you can quickly find what you need.</em>

## 6. Offer personalization options

Many applications provide custom workspaces for people and businesses. Personalization can help make your users <strong>feel more at home</strong>. This can be done by giving users options to customize the look and feel of the application interface. Let them select the color theme, the link colors, the background and so on. Even a small amount of customization will allow your users to make their pages their own.</p>

<a href="https://www.campaignmonitor.com/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f47f6f94-9b9b-424f-86c3-38bcc94f0b14/campaignmonitor-customization.png" alt="Campaign Monitor customization" width="480" height="230" /></a><br>
<em>Campaign Monitor lets you choose a color theme for your account and upload your business logo. This helps businesses infuse the colors of their brands into the Web apps they use.</em>

Personalization is certainly one of the simplest and most effective methods of binding your customers to your service, but it's important to understand that the various personalization options should never come at the expense of the core application's functionality. <strong>The system should always be capable of performing its functions</strong> and thus meet users' expectations, despite how exactly users have personalized the application.

One useful approach to finding a compromise between a website's core functionality and the user interface is to introduce various levels of personalization, depending on whether the user is a novice or an advanced user. It is also a good idea to allow the user to revert his account to the default settings or restore the settings that he had saved in his previous session.</p>

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/aa07e621-6a65-4a35-966f-816ee0239a99/tw.gif" alt="Twitter customization" width="500" height="538" /><br>
<em>Twitter lets the user customize his profile page background and colors, allowing him to craft a unique spot on the popular micro-blogging network.</em>

## 7. Display help messages that attract the eye

Every Web application is different and has its own way of doing things. If the function of a particular element isn’t immediately apparent, you can provide short <strong>help messages to get people started</strong>. One important thing to note is that if you want to help people who aren’t sure what they’re doing yet, you need to <strong>attract their attention</strong> to this message. One way to attract attention is with color -- putting a yellow “sticky” message in the sidebar, for example, is sure to stand out.</p>

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/53defbf0-5610-4d12-bd40-0774fcd98bb2/goplan-help-stickie.png" alt="Goplan help stickie" width="396" height="359" /><br>
<em>Goplan puts help messages in bright yellow boxes resembling paper stickies. The bright color ensures that users don’t miss them.</em>

Alternatively, if you are looking for a subtler solution that doesn't require much space to display and isn't obtrusive for regular users of your application, you can consider displaying vibrant visual graphics (for example, small icons) next to the design element needing explanation. For instance, pointing users to new, updated or useful features of an application's search engine, as <a href="https://www.wishlistr.com/">Wishlistr.com</a> does, makes sense.</p>

<a href="https://www.wishlistr.com/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9cdae49b-377c-4afc-9836-1f694a864b52/icons.gif" alt="Icons in use" width="500" height="189" /></a><br>
<em>Classic: Wishlistr uses a light bulb to focus the user's attention on the available search functionality of its system.</em>

## 8. Design feedback messages carefully

Pretty much every application has some form of feedback messages. These are little messages that pop out when there is an error or warning or perhaps when an action is completed successfully. Designing these messages correctly is important because you don’t want to confuse or startle your users when there’s nothing to worry about.

A good practice here is to do a couple of things. First, <strong>color code the different types of messages</strong>. Messages that notify users of successful actions are usually colored green. These employ the <strong>traffic-light analogy</strong> of green meaning "Go." Warning and error messages are colored yellow. Same traffic-light analogy here: yellow means slow down and wait. You can also distinguish between warning messages and error messages by coloring errors red and warnings yellow.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/acd97e0a-6ed4-4e96-b86f-995a2ffe6436/mailchimp-error.png" alt="Mailchimp error message" width="480" height="75" /><figcaption><em>Mailchimp uses color effectively for its error messages.</em></figcaption></figure>

The second thing to do is <strong>add a unique icon for each message type</strong>. Icons can convey meaning instantly, without the user having to read the message. For example, a tick icon can symbolize completion of a successful action. An exclamation mark in a triangle is a warning sign. People will instantly recognize that this message warns them about something and will pay attention.</p>

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1dbc5e15-4571-404e-9150-e1f27fa5ab55/getsignoff-notification.png" alt="GetSignOff notification" width="480" height="101" /><br>
<em>GetSignOff allows you to close notifications by using the little button in the top</em>-<em>right corner of the message box.</em>

Lastly, you should provide a way for users to <strong>close the notification</strong> if they are likely to remain on the page for a while.</p>

## 9. Use tabbed navigation

Many Web applications have adopted the tabbed navigation approach for their main navigation menu. Tabbed navigation is a menu that looks like each item is a tab on a file folder, with the active tab connected to the body of the page. Tabbed navigation isn’t just eye candy; it provides a usability benefit.</p>

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9126dc15-a5de-4f02-819a-cbae2be5093a/freckle-tabbed-navigation.png" alt="Freckle tabs" width="480" height="177" /><br>
<em>Freckle uses tabbed navigation in a sub</em>-<em>menu relating to the time input menu.</em>

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2fe180e2-fe17-403b-a0b9-dc45f6d4b8a2/basecamp-tabs.png" alt="Basecamp tabs" width="480" height="72" /><br>
<em>Basecamp features the standard tabbed menu for the main navigation of its app.</em>

If you make the menu look like tabs on folders, almost everyone will be able to figure out what it is and how it works. This is because the <strong>visual metaphor is strong and clear</strong>. The current page or section also becomes easy to see. Knowing where they are puts users at ease because they gain a <strong>greater sense of control</strong>.</p>

## 10. Darken background under modal windows

In some applications, you may want to display a bit of information or quick input form that doesn’t really deserve a full page of its own. Some developers put that message or form in a modal window. Modal windows are little windows that pop up on top of the current page and that users need to interact with to proceed.</p>

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bb642cf2-f78f-4cb3-b4a4-49afd4c4db63/squarespace-edit-box.png" alt="Squarespace edit box" width="480" height="416" /><br>
<em>When editing things in the <a href="https://www.squarespace.com">Squarespace</a> website creation app, the background darkens to shift focus to the edit window.</em>

To make this window stand out better, you can <strong>darken the content below it</strong>. The darker background will block out all the noise of the content behind the box and make the modal window the center of attention. This is very similar to using shadows around the window but is even more powerful in directing focus. The darker background also indicates that interaction with the content beneath is disabled and that the user should instead interact with the modal window.</p>

## 11. Lightboxes and Slideshows

Some applications include a lot of images that users may want to browse. Displaying every image on its own page may not be the most efficient way to do it — both for your visitors and your server. Your visitors will need to <strong>navigate back and forth</strong>, and your server will incur extra hits that can be avoided.</p>

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7681a0f9-3edd-4a20-9df0-4fa56db5913b/smugmug.jpg" alt="SmugMug lightbox" width="480" height="442" /><br>
<em><a href="https://www.smugmug.com">SmugMug</a> uses lightboxes to enlarge photos. (Photo by Kurt Preston.)</em>

Enter lightboxes and slideshows. Lightboxes and slideshows are used to display photos without having to load a new page. For example, the lightbox method will enlarge an image and place it as a <strong>modal window</strong> above the rest of the page, allowing the user to focus on the image itself while the background is darkened. This means less noise interfering with the viewing experience.</p>

## 12. Short sign-up forms

The sign-up form is potentially one of the biggest barriers between you and potential customers. The longer the form, the more effort your visitors will have to make before becoming members of your website or, perhaps, paying customers. To minimize the barrier, we’ve got to speed up the process. This means <strong>removing all optional elements</strong> from the form and leaving only the core essentials. The optional stuff can be filled in later.</p>

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/05f7ffca-9f4d-4dcd-8599-86f1a154795f/evernote-signup.png" alt="Evernote signup" width="452" height="455" /><br>
<em>Opening an Evernote account is easy, with only a handful of fields to fill in, all of which are grouped together in a compact box.</em>

## User Interface Design Conclusion

Making your application beautiful may lead to a satisfying user experience, but it will not guarantee a <em>usable product</em>. For example, an ugly website like Craigslist performs its function fairly well. Its poor aesthetic did not stop it from becoming hugely successful. Similarly, the minimalist interface of the Google search engine manages to fully accomplish its objectives without getting in your way. <strong>The interface disappears</strong>, letting you focus on getting things done.

Steve Jobs once said, “design is not just what it looks like and feels like. Design is how it works.” In fact, the usability and overall usefulness of a Web app is governed by how well it performs its functions and <strong>how easily those functions are accessed</strong>. Design with a goal in mind -- a goal that the interface helps your users achieve. Not every technique will work in every situation or for every application. Only implement interface elements if they make sense in your particular context.

{{< signature "al" >}}

