---
title: How To Create Perfect Emails For Your WordPress Website
slug: create-perfect-emails-wordpress-website
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ff4d6c29-2a0b-4f4a-accf-da6149e6c725/writing-code-illu22.jpg
date: 2011-10-25T13:58:33.000Z
author: daniel-pataki
summary: >-
  Whatever type of website you operate, its success will probably hinge on your interaction with your audience. If executed well, one of the most effective tools can be a simple email.
description: >-
  Whatever type of website you operate, its success will probably hinge on your interaction with your audience. If executed well, one of the most effective tools can be a simple email.
categories:
  - WordPress
  - Plugins
  - Content Strategy
  - Emails
---
Whatever type of website you operate, its success will probably hinge on your interaction with your audience. If executed well, one of the most effective tools can be a **simple email**.

WordPress users are in luck, since WordPress already has easy-to-use and extendable functions to give you a lot of power and flexibility in handling your website’s emails.

In order to create our own system, we will be doing four things. First, we will create a nice email template to use. We will then modify the mailer function so that it uses our new custom template. We will then modify the actual text of some of the built-in emails. Then we will proceed to hook our own emails into different events in order to send some custom emails. Let’s get started!

## How WordPress Sends Emails

WordPress has a handy function built in called <code>wp_mail()</code>, which handles the nitty-gritty of email sending. It is able to handle almost anything you throw at it, from custom HTML emails to modifications to the “From” field.

WordPress itself uses this function, and you can, too, by using WordPress hooks. You can read all about <a href="https://codex.WordPress.org/Plugin_API#Hooks.2C_Actions_and_Filters">how hooks work in WordPress</a>, but here is the nutshell version, and we will be working with them in this article so much that you’ll learn it by the end.

Hooks enable you to add your own functions to WordPress without modifying core files. Without hooks, if you wanted to send a publication notice to the author of a post, you would have to find the function that published the post and add your own code directly to it. With hooks, you write the function for sending the email, and then hook it into the function that publishes the post. Basically, you are telling WordPress to run your custom function whenever the function for publishing posts runs.

{{% feature-panel %}}

## Setting Up Shop

The first thing we’ll have to do is create a plugin. We could get away without it and just use our theme’s functions file, but this would become clunky in the long run. Don’t worry: setting up a plugin is super-easy.

Go to your website’s plugins folder, which can be found under <code>wp-content</code>. Create a new folder named <code>my_awesome_email_plugin</code>. If you want a different name, use something unique, not <code>email</code> or <code>email_plugin</code>; otherwise, conflicts might arise with other plugins.

Create a file named <em>my_awesome_email_plugin.php</em> in the new folder. The name of the file (without the extension) must be the same as the name of the folder.

Edit the contents of <em>my_awesome_email_plugin.php</em> by copying and pasting the code below and modifying it where necessary. This is just some default information that WordPress uses to show the plugin in the plugins menu in the admin area.

<div class="break-out">

 <pre><code class="language-php">&lt;?php
/*
Plugin Name: My Awesome Email Plugin
Plugin URI: https://myawesomewebsite.com
description: >-
  I created this plugin to rule the world via awesome WordPress email goodness
Version: 1.0
Author: Me
Author URI: https://myself.me
*/

?&gt;</code></pre>
</div>

Once that’s done, save the file, go to the WordPress admin section, and activate your new plugin. If you’re new to this, then congratulations! You have just created your first working WordPress plugin! It doesn’t really do anything yet, but don’t let that bother you. Just read on, because we’ll be adding some functionality after the next section.

## Creating An Email Template

Creating good email templates is worth an article on its own. I will just share the method that I use, which does not mean that doing it differently is not allowed. Feel free to experiment!

I am not a big fan of using images in emails, so we will be building an HTML template using only CSS. Our goal is to come up with a template to which we can add a header and footer section. We will send our emails in WordPress by pulling in the header, putting the email text under that and then pulling in the footer. This way, you can change the design of your emails very easily just by modifying the templates.

Without further ado, here’s the code for the email template that I made. Or you can <a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fee84467-a892-4e53-b6f1-1f8deceadcb6/email-template.html">download it as an HTML file</a> (right-click, and then select “Save as”). If you want a quick preview of what it looks like, just click the link.

<div class="break-out">

 <pre><code class="language-markup tmp-html">&lt;html&gt;
	&lt;head&gt;

		&lt;title&gt;The Subject of My Email&lt;/title&gt;

	&lt;/head&gt;
	&lt;body&gt;
		&lt;div id="email_container" style="background:#444"&gt;
			&lt;div style="width:570px; padding:0 0 0 20px; margin:50px auto 12px auto" id="email_header"&gt;
				&lt;span style="background:#585858; color:#fff; padding:12px;font-family:trebuchet ms; letter-spacing:1px;
					-moz-border-radius-topleft:5px; -webkit-border-top-left-radius:5px;
					border-top-left-radius:5px;moz-border-radius-topright:5px; -webkit-border-top-right-radius:5px;
					border-top-right-radius:5px;"&gt;
					MyAwesomeWebsite.com
				&lt;/div&gt;
			&lt;/div&gt;

			&lt;div style="width:550px; padding:0 20px 20px 20px; background:#fff; margin:0 auto; border:3px #000 solid;
				moz-border-radius:5px; -webkit-border-radius:5px; border-radius:5px; color:#454545;line-height:1.5em; " id="email_content"&gt;

				&lt;h1 style="padding:5px 0 0 0; font-family:georgia;font-weight:500;font-size:24px;color:#000;border-bottom:1px solid #bbb"&gt;
					The subject of this email
				&lt;/h1&gt;

				&lt;p&gt;
					Lorem ipsum dolor sit amet, consectetuer adipiscing
					elit. Aenean commodo ligula eget dolor. Aenean massa
					&lt;strong&gt;strong&lt;/strong&gt;. Cum sociis natoque penatibus
					et magnis dis parturient montes, nascetur ridiculus
					mus. Donec quam felis, ultricies nec, pellentesque
					eu, pretium quis, sem. Nulla consequat massa quis
					enim. Donec pede justo, fringilla vel, aliquet nec,
					vulputate eget, arcu. In enim justo, rhoncus ut.
				&lt;/p&gt;
				&lt;p&gt;
					Imperdiet a, venenatis vitae, justo. Nullam dictum
					felis eu pede &lt;a style="color:#bd5426" href="#"&gt;link&lt;/a&gt;
					mollis pretium. Integer tincidunt. Cras dapibus.

  			Vivamus elementum semper nisi. Aenean vulputate
					eleifend tellus. Aenean leo ligula, porttitor eu,
					consequat vitae, eleifend ac, enim. Aliquam lorem ante,
					dapibus in, viverra quis, feugiat a, tellus. Phasellus
					viverra nulla ut metus varius laoreet. Quisque rutrum.

  			Aenean imperdiet. Etiam ultricies nisi vel augue.

  			Curabitur ullamcorper ultricies nisi.
				&lt;/p&gt;

				&lt;p style=""&gt;
					Warm regards,&lt;br&gt;
					The MyAwesomeWebsite Editor
				&lt;/p&gt;

				&lt;div style="text-align:center; border-top:1px solid #eee;padding:5px 0 0 0;" id="email_footer"&gt;
					&lt;small style="font-size:11px; color:#999; line-height:14px;"&gt;
						You have received this email because you are a member of MyAwesomeSite.com.
						If you would like to stop receiving emails from us, feel free to
						&lt;a href="" style="color:#666"&gt;unregister&lt;/a&gt; from our mailing list
					&lt;/small&gt;
				&lt;/div&gt;

			&lt;/div&gt;
		&lt;/div&gt;
	&lt;/body&gt;
&lt;/html&gt;</code></pre>
</div>

Remember that this is an email, so the HTML won’t be beautiful. The safest styling method is inline, so the fewer frills you can get away with, the better.

Let’s split this into two parts. The header part of the email is everything from the top right up to and including the <code>h1</code> heading on row 23 (i.e. lines 01 to 23). Copy that bit and paste it into a new file in your <code>my_email_plugin</code> folder, and name it <em>email_header.php</em>. The footer part of the email is everything from the paragraph tag before “Warm regards” right until the end (i.e. lines 48 to 64). The text between the header and footer is just a placeholder so that you can see what the finished product will look like. We will fill it with whatever content we need to send at the time.

{{% ad-panel-leaderboard %}}

## Preparing The WordPress System For Our Emails

By default, WordPress sends plain-text emails. In order to accommodate our fancy HTML email, we need to tell the <code>wp_mail()</code> function to use the HTML format. We will also set up a custom “From” name and “From” address in the process, so that the email looks good in everyone’s inbox. To accomplish this, we’ll be using the previously mentioned hooks. Let’s look at the code; explanation follows.

<div class="break-out">

 <pre><code class="language-php">add_filter ("wp_mail_content_type", "my_awesome_mail_content_type");
function my_awesome_mail_content_type() {
	return "text/html";
}

add_filter ("wp_mail_from", "my_awesome_mail_from");
function my_awesome_mail_from() {
	return "hithere@myawesomesite.com";
}

add_filter ("wp_mail_from_name", "my_awesome_mail_from_name");
function my_awesome_email_from_name() {
	return "MyAwesomeSite";
}</code></pre>
</div>

On line 01, we have defined that we are adding a filter to the WordPress function <code>wp_mail_content_type()</code>. Our filter will be called <code>my_awesome_mail_content_type</code>. A filter is nothing more than a function, so we need to create the function <code>my_awesome_mail_content_type()</code>.

Remember that actions are functions called from within other functions? We add an action to the <code>wp_insert_user()</code> function, and the action is performed whenever <code>wp_insert_user()</code> runs. Filters are specified in much the same way; but, instead of running alongside the function that it is called from, it modifies the value of the entity that it is called on.

In our case, this means that somewhere inside the <code>wp_mail()</code> function is a variable that holds the email type, which is by default <code>text/plain</code>. The filter hook <code>wp_mail_content_type</code> is called on this variable, which means that all attached filters will be run. We happen to have attached a filter to it on line 01, so our function will perform its task. All we need to do is return the value <code>text/html</code>, which will modify the value of the variable in the <code>wp_mail</code> function to <code>text/html</code>.

The logic behind the rest of the code is exactly the same. Adding a filter to <code>wp_mail_from</code> enables us to change the sender’s address to <code>hithere@myawesomewebsite.com</code>, and adding a filter to <code>wp_mail_from_name</code> enables us to change the sender’s name.

{{% ad-panel-leaderboard %}}

## Modifying Existing WordPress System Emails

### Welcoming New Users

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d9c60935-41df-4f02-a4d2-9012946bd912/email-before.jpg"><img class="105133" title="email_before" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d9c60935-41df-4f02-a4d2-9012946bd912/email-before.jpg" alt="" width="224" height="76" /></a>

This is the content of the default WordPress email.

As mentioned, WordPress has a bunch of built-in emails that can be easily controlled (using hooks, of course). Let’s modify the default greeting email that WordPress sends out to new users. This email is sent out using a so-called “pluggable function.” This function is supplied by WordPress, but, contrary to the usual core functions, you are allowed to overwrite it with your own code.

The function in question is called <code>wp_new_user_notification()</code>. To modify it, all we need to do is create a function with the same name. Due to the method by which WordPress calls pluggable functions, there will not be any conflict, even though you are creating a function with the same name. Below is the function that I wrote. See the explanation and preview of it further below.

<div class="break-out">

 <pre><code class="language-php">function wp_new_user_notification($user_id, $plaintext_pass) {
	$user = new WP_User($user_id);

	$user_login = stripslashes($user-&gt;user_login);
	$user_email = stripslashes($user-&gt;user_email);

	$email_subject = "Welcome to MyAwesomeSite ".$user_login."!";

	ob_start();

	include("email_header.php");

	?&gt;

	&lt;p&gt;A very special welcome to you, &lt;?php echo $user_login ?&gt;. Thank you for joining MyAwesomeSite.com!&lt;/p&gt;

	&lt;p&gt;
		Your password is &lt;strong style="color:orange"&gt;&lt;?php echo $plaintext_pass ?&gt;&lt;/strong&gt; &lt;br&gt;
		Please keep it secret and keep it safe!
	&lt;/p&gt;

	&lt;p&gt;
		We hope you enjoy your stay at MyAwesomeSite.com. If you have any problems, questions, opinions, praise,
		comments, suggestions, please feel free to contact us at any time
	&lt;/p&gt;

	&lt;?php
	include("email_footer.php");

	$message = ob_get_contents();
	ob_end_clean();

	wp_mail($user_email, $email_subject, $message);
</code></pre>
</div>

As you can see, the function is passed two arguments: the ID of the new user and the generated password. We will be using these to generate the variable parts of our message. On line 2, we’ve built a user object that will contain the data of the user in question. On line 7, we’ve created an email subject using the variable <code>$email_subject</code>.

Before we move on, let’s go back to our <em>email_header.php</em> file. Replace “The Subject of My Email” and “The subject of this email” (lines 04 and 22 if you’re looking at the code here) with <code>&lt;?php echo $email_subject ?&gt;</code>. We don’t want all of our subjects to be “The Subject of My Email,” so we need to pull that data from the email that we are building.

From lines 09 to 31, we are using a handy technique called “output buffering.” Because the content <em>email_header.php</em> is not stored inside a variable, it is included directly; this would result in it being printed right away, and we would not be able to use it in our function. To get around this problem, we output buffering. When it is turned on (using <code>ob_start()</code>), no output is sent from the script; instead, it is stored in an internal buffer.

So, first, we include the header, then we write our our message content, then include the footer. Because we are buffering the content, we can simply close our PHP tags and use regular HTML for our message, which I find much cleaner than storing all of it in a variable. On line 30, we pull the contents of the buffer into a variable; and on line 31, we discard the buffer’s content, since we don’t need it anymore.

With that done, we have all of the information needed to use <code>wp_mail()</code>. So, on line 33, we send our email to the user, which should look something like this:

<img class="105134" title="email_after" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/521c5e55-36fd-4de7-8e27-1d456f61c4f8/email-after1.jpg" alt="" width="466" height="414" />

### Password Retrieval Emails

For some reason, WordPress doesn’t use the same pluggable functions to handle all emails. For example, to modify the look and feel of the password retrieval emails, we have to resort to hooks. Let’s take a look.

<div class="break-out">

 <pre><code class="language-php">add_filter ("retrieve_password_title", "my_awesome_retrieve_password_title");

function my_awesome_retrieve_password_title() {
	return "Password Reset for MyAwesomeWebsite";
}

add_filter ("retrieve_password_message", "my_awesome_retrieve_password_message");
function my_awesome_retrieve_password_message($content, $key) {
	global $wpdb;
	$user_login = $wpdb-&gt;get_var("SELECT user_login FROM $wpdb-&lt;users WHERE user_activation_key = '$key'");

	ob_start();

	$email_subject = imp_retrieve_password_title();

	include("email_header.php");
	?&gt;

	&lt;p&gt;
		It likes like you (hopefully) want to reset your password for your MyAwesomeWebsite.com account.
	&lt;/p&gt;

	&lt;p&gt;
		To reset your password, visit the following address, otherwise just ignore this email and nothing will happen.
		&lt;br&gt;
		&lt;?php echo wp_login_url("url") ?&gt;?action=rp&amp;key=&lt;?php echo $key ?&gt;&amp;login=&lt;?php echo $user_login ?&gt;
	&lt;p&gt;

	?&gt;

	include("email_footer.php");

	$message = ob_get_contents();

	ob_end_clean();

	return $message;
}</code></pre>
</div>

First, we’ve added a filter to <code>retrieve_password_title</code>, which will modify the default value of the email’s title to our own. Then, we’ve added a filter to <code>retrieve_password_message</code>, which will modify the contents of the message.

On line 10, we’ve used the <code>$wpdb</code> object to query the database for the user’s name based on the key that was generated when the retrieval was initiated. We then do the same thing as before: we start the content buffering, pull our email header, add our message content, and pull our email footer.

One fantastic part about using hooks can be seen on line 14. Our password title needs to be “Password Reset for MyAwesomeWebsite.” We could well have typed that in, but instead we created a function (<code>imp_retrieve_password_title()</code>) that outputs exactly the same thing. It should be clear by now that all we are doing with these hooks is creating regular ol’ functions that can just be plugged into WordPress as actions (which run when initiated by something) or filters (which run and modify data when they are initiated).

This time, instead of using <code>wp_mail()</code>, all we need to do is return the message’s content. This is because we are creating a filter that modifies the contents of the password-retrieval email, nothing else. WordPress will do whatever it usually does to send that email, but now it will use our content.

### Pluggable Function and Hooks

This question is not easily answered, because this is not too well documented yet. Your best bet is looking in the file <em>pluggable.php</em> (in your <code>wp-includes</code> folder) to see which emails are controlled from there. Remember not to edit this file; use the plugin we are creating here. You can scan the <a href="https://adambrown.info/p/wp_hooks/hook/filters">list of WordPress filters</a> to find filters that control email content.

Right now, most emails are handled through pluggable functions; only the password-retrieval email and some WordPress MU emails are handled using hooks. This might change, as development is quite active, but I would guess that if any new emails are added, you will be able to use pluggable functions.

Here is a list of emails that you can modify using pluggable functions:

*   Notify authors of comments: `wp_notify_postauthor()`
*   Notify moderator of comments waiting for approval: `wp_notify_moderator()`
*   Notify administrator of password changes on the website: `wp_password_change_notification()`
*   Notify administrator of new registrations: `wp_new_user_notification()`

## Adding New Emails To The System

So far, we’ve just been modifying what WordPress has to offer. Now it’s time to add some emails of our own! Let’s implement an email that will notify an author when you have published their post.

To accomplish this, we need to find the WordPress action hook that publishes a post when we press the “Publish” button. We then have to hook our own function into that, which will perform the task of sending the email.

Looking at the <a href="https://adambrown.info/p/wp_hooks/hook/actions">list of action hooks</a>, we can see that the hook we are looking for is called <code>{$new_status}&#95;{$post-&gt;post_type}</code>. This looks a bit different than what we’re used to, but it’s really very simple. A post can go through numerous statuses. It can be a draft, it can be private, published and so on. There are also a lot of potential post types, such as “Post” and “Page,” not to mention that you can create custom post types. This hook simply enables us to put a status and a post type together and then get the hook that runs when that post’s type changes to the indicated status. So, **our hook will be called <code>publish_post</code>**.

<div class="break-out">

 <pre><code class="language-php">add_action("publish_post", "my_awesome_publication_notification");

function my_awesome_publication_notification($post_id) {
	$post = get_post($post_id);
	$author = get_userdata($post-&gt;post_author);

	$author_email = $author-&gt;user_email;
    $email_subject = "Your article has been published!";

	ob_start();

	include("email_header.php");

	?&gt;

	&lt;p&gt;
		Hi, &lt;?php echo $author-&gt;display_name ?&gt;. I've just published one of your articles
		(&lt;?php echo $post-&gt;post_title ?&gt;) on MyAwesomeWebsite!
	&lt;/p&gt;

	&lt;p&gt;
		If you'd like to take a look, &lt;a href="&lt;?php echo get_permalink($post-&gt;ID) ?&gt;"&gt;click here&lt;/a&gt;.

  I would appreciate it if you could come back now and again to respond to some comments.
	&lt;/p&gt;

	&lt;?php

	include("email_footer.php");

	$message = ob_get_contents();

	ob_end_clean();

	wp_mail($author_email, $email_subject, $message);

}</code></pre>
</div>

By now, this should be second nature to you. The only real difference here is that we have to retrieve the data of the post, and the author’s data on lines 4 and 5, so that we have the necessary data for the email.

One thing you might be wondering is how I know that my function takes the ID of this post as its argument. I cannot freely choose this value, of course; it is dictated by how WordPress is built. Every hook supplies different arguments; some even supply more than one. To find out what arguments are at your disposal, you will have to go into some core files.

I suggest browsing the <a href="https://adambrown.info/p/wp_hooks/">hooks database</a>, clicking on the hook that you need, and then clicking on “View hook in source” next to your version of WordPress (preferably the latest one). Once there, scroll down, and find the highlighted line, which is where the hook is called. It will be in the form of <code>do_action( $tag, $arg_a, $arg_b, $etc )</code> or <code>apply_filters( $tag, $arg_a, $arg_b, $etc )</code>.

## Extending Our Functions

Interestingly, the <code>wp_mail()</code> function itself is a pluggable function, so you can completely override how it works. This may be going a bit over the top, but if you need some serious email-sending power (for example, you want a system that notifies your 120,000 registered users about new posts), you can completely modify it to use your mass-mailer application.

Because we are using a template for email headers and footers, a lot can be done to extend our emails. We can distinguish between emails to staff and emails to users by using different header files; we can add the latest three posts to the bottom of each email by using footer templates; and so on.

We can add a table to our database that holds information about which users are emailed the most, who responds to emails, and so on. Whenever you plug a function into something, it can contain any sort of code you’d like. You could include code for increasing the email count for user #112 inside the function that sends them the email, for example. This is not a good practice (you should create separate functions and plug them both in), but getting to grips with the vast power that this methodology offers is important.

## A Word Of Warning

While the method described here is great, I am not an expert in creating HTML emails. The code for the HTML email above is tested to work in Gmail and some other applications, but each email application handles email differently. Some strip out all CSS, some strip out just background colors, and so on.

Before using the template, please test it with the most common applications (Gmail, Yahoo Mail, Apple Mail, Outlook, Entourage, Thunderbird, etc.) to make sure it works as expected.

## Conclusion

Hopefully by now you have learned how to modify the emails that WordPress sends out, how to create your own emails, and how to plug them into different actions.

I also hope that your knowledge of WordPress hooks has expanded, because they are <em>the</em> tool for creating great plugins and add-ons for WordPress, and the thinking behind them is a glimpse into the world of object-oriented programming.

If you have any questions or comments, let me know: I am at your disposal. Also, if you’ve created a similar system, do share your thoughts, I would be happy to hear how you’ve accomplished the same, or better!

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Building An Advanced Notification System For WordPress](https://www.smashingmagazine.com/2015/05/building-wordpress-notification-system/)
*   [Schedule Events Using WordPress Cron](https://www.smashingmagazine.com/2013/10/schedule-events-using-wordpress-cron/)
*   [Improve Your Email Workflow With Modular Design](https://www.smashingmagazine.com/2014/08/improve-your-email-workflow-with-modular-design/)
*   [Design and Build Email Newsletters](https://www.smashingmagazine.com/2010/01/design-and-build-an-email-newsletter-without-losing-your-mind/)

{{< signature "al" >}}
