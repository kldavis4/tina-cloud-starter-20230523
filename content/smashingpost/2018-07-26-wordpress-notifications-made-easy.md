---
title: 'WordPress Notifications Made Easy'
slug: wordpress-notifications-made-easy
author: jakub-mikita
image: >-
  //archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3a8149d0-4712-4217-b329-5c7748d27ef6/custom-notification-800w.png
date: 2018-07-26T14:20:27+02:00
summary:
  Have you been looking for a way to create a notification system when using WordPress? Meet the ‘Notification’ plugin, an all-in-one solution for any custom WordPress notification system.
description:
  Have you been looking for a way to create a notification system when using WordPress? Meet the ‘Notification’ plugin, an all-in-one solution for any custom WordPress notification system.
categories:
  - Plugins
  - WordPress
---
<p>WordPress doesn’t offer any kind of notification system. All you can use is the <code>wp_mail()</code> function, but all of the settings have to be hardcoded, or else you have to create a separate settings screen to allow the user tweak the options. It takes many hours to write a system that is reliable, configurable and easy to use. But not anymore. I’ll show you how to create your own notification system within minutes with the free Notification plugin. <strong>By notification, I mean any kind of notification</strong>. Most of the time, it will be email, but with the plugin we’ll be using, you can also send webhooks and other kinds of notifications.</p>

<p>While creating a project for one of my clients, I encountered this problem I’ve described. The requirement was to have multiple custom email alerts with configurable content. Instead of hardcoding each and every alert, I decided to build a system. I wanted it to be very flexible, and the aim was to be able to code new scenarios as quickly as possible.</p>

<p>The code I wrote was the start of a great development journey. It turned out that the system I created was flexible enough that it could work as a separate package. This is how the <a href="https://wordpress.org/plugins/notification/">Notification</a> plugin was born.</p>

<p>Suppose you want to send an email about a user profile being updated by one of your website’s members. WordPress doesn’t provide that functionality, but with the Notification plugin, you can create such an email in minutes. Or suppose you want to synchronize your WooCommerce products with third-party software by sending a webhook to a separate URL every time a new product is published. That’s easy to do with the plugin, too.</p>

<div class="c-felix-the-cat">
<h4 class="h3">Lessons Learned While Developing WordPress Plugins</h4>
<p>Good plugin development and support lead to more downloads. More downloads mean more money and a better reputation. Learn how you can develop good-quality products with seven golden rules. <a href="https://www.smashingmagazine.com/2018/05/developing-wordpress-plugins/" class="btn btn--medium btn--blue">Read a related article&nbsp;&rarr;</a></p>
</div>

<p>In this article, you’ll learn how to integrate the plugin in your own application and how to create an advanced WordPress notification system more quickly and easily than ever.</p>

<p>In this article, we’ll cover:</p>

<ol>
<li>how to install the plugin,</li>
<li>the idea behind the plugin and its architecture,</li>
<li>creating a custom scenario for notifications,</li>
<li>creating the action (step 1 of the process),</li>
<li>creating the trigger (step 2 of the process),</li>
<li>creating the custom notification type,</li>
<li>how to enable white-label mode and bundle the plugin in your package.</li>
</ol>

{{% feature-panel %}}

## Installing The Plugin

<p>To create your own scenarios, you are going to need the Notification plugin. Just install it from the WordPress.org repository in your WordPress dashboard, or download it from the <a href="https://github.com/BracketSpace/Notification/">GitHub repository</a>.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2371ca91-f930-4373-ba15-559bb4e8bcc2/wordpress-notification-plugin.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/911515c1-71ab-4ed9-a885-fffaa8b61221/wordpress-notification-plugin-800w.gif" width=“800" height="400" alt="" /></a><figcaption><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2371ca91-f930-4373-ba15-559bb4e8bcc2/wordpress-notification-plugin.gif">Large preview</a></figcaption></figure>

<p>Later in the article, you’ll learn how to hide this plugin from your clients and make it work as an integrated part of your plugin or theme.</p>

## The Idea Of The Plugin

<p>Before going into your code editor, you’ll need to know what the plugin’s architecture looks like. The plugin contains many various components, but its core is really <a href="https://github.com/BracketSpace/Notification/tree/develop/class/Abstracts">a few abstract classes</a>.</p>

<p>The main components are:</p>

<ul>
<li><strong>The notification</strong><br />This could be an email, webhook, push notification or SMS.</li>
<li><strong>The trigger</strong><br />This is what sends the notification. It’s effectively the WordPress action.</li>
<li><strong>The merge tag</strong><br />This is a small portion of the dynamic content, like <code>{post_title}</code>.</li>
</ul>

<p>To give you a better idea of how it all plays together, you can watch this short video:</p>

<figure class="video-container"><iframe loading="lazy" src="https://www.youtube.com/embed/UPqVBhLGTek" width="600" height="480" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe></figure>

<p>The core of the Notification plugin is really just an API. All of the default triggers, like <em>Post published</em> and <em>User registered</em> are things built on top of that API.</p>

<p>Because the plugin was created for developers, adding your own triggers is very easy. All that’s required is a <a href="https://developer.wordpress.org/plugins/hooks/actions/">WordPress action</a>, which is just a single line of code and a class declaration.</p>

## Custom Scenario

<p>Let’s devise a simple scenario. We’ll add a text area and button to the bottom of each post, allowing bugs in the article to be reported. Then, we’ll trigger the notification upon submission of the form.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/392ff7af-4c1d-42f9-9658-297be6897a2e/implementing-ajax-in-wp-3.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/392ff7af-4c1d-42f9-9658-297be6897a2e/implementing-ajax-in-wp-3.gif" width=“547" height="340" alt="" /></a></figure>

<p>This scenario was covered in another article, “<a href="https://www.smashingmagazine.com/2018/02/submitting-forms-without-reloading-ajax-implementation-wordpress/">Submitting Forms Without Reloading the Page: AJAX Implementation in WordPress</a>”.</p>

<p>For simplicity, let’s make it a static form, but there’s no problem putting the action in an AJAX handler, instead of in the <code>wp_mail()</code> function.</p>

<p>Let’s create the form.</p>

### The Form

<div class="break-out">

<pre><code class="language-php">add_filter( 'the_content', 'report_a_bug_form' );
function report_a_bug_form( $content ) {

    // Display the form only on posts.
    if ( ! is_single() ) {
        return $content;
    }

    // Add the form to the bottom of the content.
    $content .= '&lt;form action="' . admin_url( 'admin-post.php' ) . '" method="POST">
        &lt;input type="hidden" name="post_id" value="' . get_ID() . '">
        &lt;input type="hidden" name="action" value="report_a_bug">
        &lt;textarea name="message" placeholder="' . __( 'Describe what\'s wrong...', 'reportabug' ) . '">&lt;/textarea>
        &lt;button>' . __( 'Report a bug', 'reportabug' ) . '&lt;/button>
    &lt;/div>';

    return $content;

}
</code></pre></div>

<p>Please note that many components are missing, like WordPress nonces, error-handling and display of the action’s result, but these are not the subject of this article. To better understand how to handle these actions, please read the <a href="https://www.smashingmagazine.com/2018/02/submitting-forms-without-reloading-ajax-implementation-wordpress/">article mentioned above</a>.</p>

## Preparing The Action

<p>To trigger the notification, we are going to need just a single action. This doesn’t have to be a custom action like the one below. You can use any of the actions already registered in WordPress core or another plugin.</p>

### The Form Handler And Action

<div class="break-out">

<pre><code class="language-php">add_action( 'admin_post_report_a_bug', 'report_a_bug_handler' );
add_action( 'admin_post_nopriv_report_a_bug', 'report_a_bug_handler' );
function report_a_bug_handler() {

	do_action( 'report_a_bug', $_POST['post_id'], $_POST['message'] );

	// Redirect back to the article.
	wp_safe_redirect( get_permalink( $_POST['post_id'] ) );
	exit;

}
</code></pre></div>

<p>You can read more on how to use the <code>admin-post.php</code> file in the <a href="https://codex.wordpress.org/Plugin_API/Action_Reference/admin_post_(action)">WordPress Codex</a>.</p>

<p>This is all we need to create a custom, configurable notification. Let’s create the trigger.</p>

## Registering The Custom Trigger

<p>The trigger is just a simple class that extends the abstract trigger. The abstract class does all of the work for you. It puts the trigger in the list, and it handles the notifications and merge tags.</p>

<p>Let’s start with the trigger declaration.</p>

### Minimal Trigger Definition

<div class="break-out">

<pre><code class="language-php">class ReportBug extends \BracketSpace\Notification\Abstracts\Trigger {

	public function __construct() {

		// Add slug and the title.
		parent::__construct(
			'reportabug',
			__( 'Bug report sent', 'reportabug' )
		);

		// Hook to the action.
		$this->add_action( 'report_a_bug', 10, 2 );

	}

	public function merge_tags() {}

}
</code></pre></div>

<p>All you need to do is call the parent constructor and pass the trigger slug and nice name.</p>

<p>Then, we can hook into our custom action. The <code>add_action</code> method is very similar to the <code>add_action()</code> function; so, the second parameter is the priority, and the last one is the number of arguments. Only the callback parameter is missing because the abstract class does that for us.</p>

<p>Having the class, we can register it as our new trigger.</p>

<pre><code class="language-php">register_trigger( new ReportBug() );
</code></pre>

<p>This is now a fully working trigger. You can select it from the list when composing a new notification.</p>

{{< rimg  href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a6eb58f6-39a8-443a-95fb-4d0d1fbec1d1/trigger.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a6eb58f6-39a8-443a-95fb-4d0d1fbec1d1/trigger.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a6eb58f6-39a8-443a-95fb-4d0d1fbec1d1/trigger.png'>Large preview</a>)" alt="" >}}

<p>Although the trigger is working and we can already send the notification we want, it’s not very useful. We don’t have any way to show the recipient which post has a bug and what the message is.</p>

<p>This would be the time, then, to register some merge tags and set up the trigger context with the action parameters we have: the post ID and the message.</p>

<p>To do this, we can add another method to the trigger class. This is the action callback, where we can catch the action arguments.</p>

{{% ad-panel-leaderboard %}}

### Handling Action Arguments

<pre><code class="language-php">public function action( $post_ID, $message ) {

	// If the message is empty, don't send any notifications.
	if ( empty( $message ) ) {
		return false;
	}

	// Set the trigger properties.
	$this->post    = get_post( $post_ID );
	$this->message = $message;

}
</code></pre>

<p>Note the <code>return false;</code> statement. If you return <code>false</code> from this method, the trigger will be stopped, and no notification will be sent. In our case, we don’t want a notification to be submitted with an empty message. In the real world, you’d want to validate that before the form is sent.</p>

<p>Then, we just set the trigger class’ properties, the complete post object and the message. Now, we can use them to add some merge tags to our trigger. We can just fill the content of the <code>merge_tags</code> method we declared earlier.</p>

### Defining Merge Tags

<div class="break-out">

<pre><code class="language-php">public function merge_tags() {

	$this->add_merge_tag( new \BracketSpace\Notification\Defaults\MergeTag\UrlTag( array(
		'slug'        => 'post_url',
		'name'        => __( 'Post URL', 'reportabug' ),
		'resolver'    => function( $trigger ) {
			return get_permalink( $trigger->post->ID );
		},
	) ) );

	$this->add_merge_tag( new \BracketSpace\Notification\Defaults\MergeTag\StringTag( array(
		'slug'        => 'post_title',
		'name'        => __( 'Post title', 'reportabug' ),
		'resolver'    => function( $trigger ) {
			return $trigger->post->post_title;
		},
	) ) );

	$this->add_merge_tag( new \BracketSpace\Notification\Defaults\MergeTag\HtmlTag( array(
		'slug'        => 'message',
		'name'        => __( 'Message', 'reportabug' ),
		'resolver'    => function( $trigger ) {
			return nl2br( $trigger->message );
		},
	) ) );

	$this->add_merge_tag( new \BracketSpace\Notification\Defaults\MergeTag\EmailTag( array(
		'slug'        => 'post_author_email',
		'name'        => __( 'Post author email', 'reportabug' ),
		'resolver'    => function( $trigger ) {
			$author = get_userdata( $trigger->post->post_author );
			return $author->user_email;
		},
	) ) );

}
</code></pre></div>

<p>This will add four merge tags, all ready to use while a notification is being composed.</p>

<p>The merge tag is an instance of a special class. You can see that there are many types of these tags, and we are using them depending on the value that is returned from the resolver. You can see all merge tags in the <a href="https://github.com/BracketSpace/Notification/tree/develop/class/Defaults/MergeTag">GitHub repository</a>.</p>

<p>All merge tags are added via the <code>add_merge_tag</code> method, and they require the config array with three keys:</p>

<ul>

<li><strong>slug</strong><br />The static value that will be used in the notification (i.e. <code>{post_url}</code>).</li>
<li><strong>name</strong><br />The translated label for the merge tag.</li>
<li><strong>resolver</strong><br />The function that replaces the merge tag with the actual value.</li>
</ul>

<p>The resolver doesn’t have to be the closure, as in our case, but using it is convenient. You can pass a function name as a string or an array if this is a method in another class.</p>

<p>In the resolver function, only one argument is available: the trigger class instance. Thus, we can access the properties we just set in the <code>action</code> method and return the value we need.</p>

<p>And that’s all! The merge tags are not available to use with our trigger, and we can set up as many notifications of the bug report as we want.</p>

{{< rimg  href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/42d32928-bb71-4f69-a42f-45f74250ee89/notification.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/42d32928-bb71-4f69-a42f-45f74250ee89/notification.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/42d32928-bb71-4f69-a42f-45f74250ee89/notification.png'>Large preview</a>)" alt="" >}}

## Creating The Custom Notification Type

<p>The Notification plugin offers not only custom triggers, but also custom notification types. The plugin ships with two types, email and webhook, but it has a simple API to register your own notifications.</p>

<p>It works very similarly to the custom trigger: You also need a class and a call to one simple function to register it.</p>

<p>I’m showing only an example; the implementation will vary according to the system you wish to integrate. You might need to include a third-party library and call its API or operate in WordPress’ file system, but the guide below will set you up with the basic process.</p>

<p>Let’s start with a class declaration:</p>

<div class="break-out">

<pre><code class="language-php">class CustomNotification extends \BracketSpace\Notification\Abstracts\Notification {

	public function __construct() {

		// Add slug and the title.
		parent::__construct(
			'custom_notification',
			__( 'Custom Notification', 'textdomain' )
		);

	}

	public function form_fields() {}

	public function send( \BracketSpace\Notification\Interfaces\Triggerable $trigger ) {}

}
</code></pre></div>

<p>In the constructor, you must call the parent’s class constructor and pass the slug and nice name of the notification.</p>

<p>The <code>form_fields</code> method is used to create a configuration form for notifications. (For example, the email notification would have a subject, body, etc.)</p>

<p>The <code>send</code> method is called by the trigger, and it’s where you can call the third-party API that you wish to integrate with.</p>

<p>Next, you have to register it with the <code>register_notification</code> function.</p>

<pre><code class="language-php">register_trigger( new CustomNotification() );
</code></pre>

### The Notification Form

<p>There might be a case in which you have a notification with no configuration fields. That’s fine, but most likely you’ll want to give the WordPress administrator a way to configure the notification content with the merge tags.</p>

<p>That’s why we’ll register two fields, the title and the message, in the <code>form_fields</code> method. It looks like this:</p>

<div class="break-out">

<pre><code class="language-php">public function form_fields() {

	$this->add_form_field( new \BracketSpace\Notification\Defaults\Field\InputField( array(
		'label'       => __( 'Title', 'textdomain' ),
		'name'        => 'title',
		'resolvable'  => true,
		'description' => __( 'You can use merge tags', 'textdomain' ),
	) ) );

	$this->add_form_field( new \BracketSpace\Notification\Defaults\Field\TextareaField( array(
		'label'       => __( 'Message', 'textdomain' ),
		'name'        => 'message',
		'resolvable'  => true,
		'description' => __( 'You can use merge tags', 'textdomain' ),
	) ) );

}
</code></pre></div>

<p>As you can see, each field is an object and is registered with the <code>add_form_field</code> method. For the list of all available field types, please visit <a href="https://github.com/BracketSpace/Notification/tree/develop/class/Defaults/Field">the GitHub repository</a>.</p>

<p>Each field has the translatable label, the unique name and a set of other properties. You can define whether the field should be resolved with the merge tags with the <code>resolvable</code> key. This means that when someone uses the <code>{post_title}</code> merge tag in this field, it will be changed with the post’s actual title. You can also provide the <code>description</code> field for a better user experience.</p>

<p>At this point, your custom notification type can be used in the plugin’s interface with any available trigger type.</p>

{{< rimg  href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/121010fd-aba6-47e2-b889-de2312903d0e/custom-notification.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/121010fd-aba6-47e2-b889-de2312903d0e/custom-notification.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/121010fd-aba6-47e2-b889-de2312903d0e/custom-notification.png'>Large preview</a>)" alt="" >}}

### Sending The Custom Notification

<p>In order to make it really work, we have to use the <code>send</code> method in our notification class declaration. This is the place where you can write an API call or use WordPress’ file system or any WordPress API, and do whatever you like with the notification data.</p>

<p>This is how you can access it:</p>

<div class="break-out">

<pre><code class="language-php">public function send( \BracketSpace\Notification\Interfaces\Triggerable $trigger ) {

	$title   = $this->data['title'];
	$message = $this->data['message'];

	// @todo Write the integration here.

}
</code></pre></div>

<p>At this point, all of the fields are resolved with the merge tags, which means the variables are ready to be shipped.</p>

<p>That gives you endless possibilities to integrate WordPress with any service, whether it’s your local SMS provider, another WordPress installation or any external API you wish to communicate with.</p>

{{% ad-panel-leaderboard %}}

## White Labeling And Bundling The Plugin

<p>It’s not ideal to create a dependency of a plugin that can be easily deactivated and uninstalled. If you are building a system that really requires the Notification plugin to be always available, you can bundle the plugin in your own code.</p>

<p>If you’ve used the Advanced Custom Fields plugin before, then you are probably familiar with the bundling procedure. Just copy the plugin’s files to your plugin or theme, and invoke the plugin manually.</p>

<p>The Notification plugin works very similarly, but invoking the plugin is much simpler than with Advanced Custom Fields.</p>

<p>Just copy the plugin’s files, and require one file to make it work.</p>

<pre><code class="language-php">require_once( 'path/to/plugin/notification/load.php' );
</code></pre>

<p>The plugin will figure out its location and the URLs.</p>

<p>But bundling the plugin might not be enough. Perhaps you need to completely hide that you are using this third-party solution. This is why the Notification plugin comes with a white-label mode, which you can activate at any time.</p>

<p>It also is enabled as a single call to a function:</p>

<pre><code class="language-php">notification_whitelabel( array(
	// Admin page hook under which the Notifications will be displayed.
	'page_hook'       => 'edit.php?post_type=page',
	// If display extensions page.
	'extensions'      => false,
	// If display settings page.
	'settings'        => false,
	// Limit settings access to user IDs.
	// This works only if settings are enabled.
	'settings_access' => array( 123, 456 ),
) );
</code></pre>

<p>By default, calling this function will hide all of the default triggers.</p>

<p>Using both techniques, white labeling and bundling, will completely hide any references to the plugin’s origin, and the solution will behave as a fully integrated part of your system.</p>

## Conclusion

<p>The Notification plugin is an all-in-one solution for any custom WordPress notification system. It’s extremely easy to configure, and it works out of the box. All of the triggers that are registered will work with any notification type, and if you have any advanced requirements, you can save some time by using an existing <a href="https://bracketspace.com/downloads/category/notification/">extension</a>.</p>

<p>If you’d like to learn more details and advanced techniques, go to the <a href="https://docs.bracketspace.com/docs-category/developer/">documentation website</a>.</p>

<p>I’m always open to new ideas, so if you have any, you can reach out to me here in the comments, via the <a href="https://github.com/BracketSpace/Notification/issues">GitHub issues</a> or on <a href="https://twitter.com/kubamikita">Twitter</a>.</p>

<p><a href="https://wordpress.org/plugins/notification/">Download the plugin</a> from the repository, and give it a try!</p>

{{< signature "ra, yk, il" >}}
