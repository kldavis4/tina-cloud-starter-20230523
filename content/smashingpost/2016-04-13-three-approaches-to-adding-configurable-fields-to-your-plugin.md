---
title: 3 Approaches To Adding Configurable Fields To Your WordPress Plugin
slug: three-approaches-to-adding-configurable-fields-to-your-plugin
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d3d2f8c1-a8f6-46a3-a732-d0d9b8efc1c0/01-plugin-starter-preview-opt.png
date: 2016-04-13T14:49:53.000Z
author: matthewray
description: >-
  Anyone who has created a WordPress plugin understands the need to create
  configurable fields to modify how the plugin works. **There are countless uses
  for configurable options in a plugin**, and nearly as many ways to implement
  said options. You see, WordPress allows plugin authors to create their own
  markup within their settings pages. As a side effect, settings pages can vary
  greatly between plugins.

  In this article we are going to go over three common ways you can make your
  plugin configurable. We will start by creating a settings page and create our
  fields using the default WordPress Settings API. I will then walk you through
  how to set up your fields with a custom handler. Finally, I will show you how
  to integrate a great configurable fields plugin Advanced Custom Fields (ACF)
  into your own plugin.
categories:
  - WordPress
  - Plugins
  - Techniques (WP)
---
Anyone who has created a WordPress plugin understands the need to create configurable fields to modify how the plugin works. <strong>There are countless uses for configurable options in a plugin</strong>, and nearly as many ways to implement said options. You see, WordPress allows plugin authors to create their own markup within their settings pages. As a side effect, settings pages can vary greatly between plugins.

In this article we are going to go over three common ways you can make your plugin configurable. We will start by creating a settings page and create our fields using the default WordPress Settings API.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Extend WordPress With Custom Fields](https://www.smashingmagazine.com/2010/04/extend-wordpress-with-custom-fields/)
*   [Custom Fields Hacks For WordPress](https://www.smashingmagazine.com/2009/05/10-custom-fields-hacks-for-wordpress/)
*   [Extending Advanced Custom Fields With Your Own Controls](https://www.smashingmagazine.com/2015/09/extending-advanced-custom-fields-with-your-own-controls/)
*   [<span class="headline">The Complete Guide To Custom Post Types</span>](https://www.smashingmagazine.com/2012/11/complete-guide-custom-post-types/)

I will then walk you through how to set up your fields with a custom handler. Finally, I will show you how to integrate a great configurable fields plugin Advanced Custom Fields (ACF) into your own plugin.

{{% feature-panel %}}

Since this is a long post, here is a table of contents with links to each of the major sections:

*   [Creating our Plugin and Settings Page](#plugin_setup)
*   [Approach 1: Using the Built-In WordPress Functionality](#approach_1)
*   [Approach 2: Setting Up a Custom Form and Handler](#approach_2)
*   [Approach 3: Integrating ACF (Advanced Custom Fields) Into Your Plugin](#approach_3)

For code examples please see <a href="https://github.com/rayman813/smashing-custom-fields">the repository</a> I have set up to accompany this post.</p>

## Creating Our Plugin And Settings Page

The first thing we need to do is set up our plugin and create a settings page. All three approaches outlined in this article start with the plugin structure below. <strong>This plugin structure is object-oriented</strong> so there may be a few differences in your own code if your plugin is written procedurally. Pay particular attention to the callback function format in the actions and filters.</p>

<pre><code class="language-php">
/*
	Plugin Name: Smashing Fields Plugin
	description: >-
  Setting up configurable fields for our plugin.
	Author: Matthew Ray
	Version: 1.0.0
*/
class Smashing_Fields_Plugin {
	// Our code will go here
}
new Smashing_Fields_Plugin();
</code></pre>

Inside our class we are going to add an action hook to add the settings page:

<pre><code class="language-php">public function __construct() {
	// Hook into the admin menu
	add_action( 'admin_menu', array( $this, 'create_plugin_settings_page' ) );
}</code></pre>

You can see that our action's callback is <code>create_plugin_settings_page</code>, so let's create that method. Note: I have set up the arguments as separate named variables to give some context to our code, but you can simply place the values directly in the function to save memory.</p>

<pre><code class="language-php">public function create_plugin_settings_page() {
	// Add the menu item and page
	$page_title = 'My Awesome Settings Page';
	$menu_title = 'Awesome Plugin';
	$capability = 'manage_options';
	$slug = 'smashing_fields';
	$callback = array( $this, 'plugin_settings_page_content' );
	$icon = 'dashicons-admin-plugins';
	$position = 100;

	add_menu_page( $page_title, $menu_title, $capability, $slug, $callback, $icon, $position );
}</code></pre>

Take a look at the WP codex for <code><a href="https://codex.wordpress.org/Function_Reference/add_menu_page">add_menu_page</a></code> for more information.

This function will create our page as well as the menu item. The important parts here are the slug, capability and callback arguments. The slug we will use later to register our fields, so write that down somewhere. You can change the <a href="https://codex.wordpress.org/Roles_and_Capabilities">capability</a> to allow different user levels access to your settings page. As for the callback, we will create that method shortly. Notice you can also put a <a href="https://developer.wordpress.org/resource/dashicons/">dashicon</a> class directly into the function to change the icon for the menu. The last argument is the position of the menu item within the menu; play around with this number to find the spot in the menu you'd like your settings to fall. Note: you can use decimal values to avoid conflicts with other menu items.

Our next step is to create the callback method <code>plugin_settings_page_content</code> for our settings page.

<pre><code class="language-php">public function plugin_settings_page_content() {
	echo 'Hello World!';
}</code></pre>

If you save your plugin and refresh the WordPress admin panel you should see the following:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/33e2b90e-4447-4d25-b4c7-a3efccb9ac18/01-plugin-starter-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/54e1a3b6-5fcb-4d21-83d6-7ce576f70ca7/01-plugin-starter-preview-opt.png" alt="Starting layout for settings page" /></a><figcaption>The starting state for the settings page. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/33e2b90e-4447-4d25-b4c7-a3efccb9ac18/01-plugin-starter-opt.png">View large version</a>)</figcaption></figure>

You can see that your settings page is a top-level menu item. You may prefer to leave it this way based on the needs of your settings page. However, you may also want to have your plugin settings under another menu item. In this case you will simply change the last line of the <code>create_plugin_settings_page</code> method to the following:

<pre><code class="language-php">add_submenu_page( 'options-general.php', $page_title, $menu_title, $capability, $slug, $callback );</code></pre>

Here we are changing the function <code>add_menu_page</code> to <code>add_submenu_page</code> and prepending a new argument. That argument is the parent menu item that the new settings page will be under. In the <code><a href="https://codex.wordpress.org/Function_Reference/add_submenu_page">add_submenu_page</a></code> documentation you can see a pretty good list for the parent menu items and their slugs. You might also see that we no longer have the last two arguments, <code>$icon</code> and <code>$position</code>. Since we are now in the submenu section, we no longer have control over the position of the element. Also, submenus don't have icons available to them so there is no need for that argument.

If you save this new code you will see that our settings page will be displayed under the Settings menu item:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9ac8a5dc-e770-4588-9854-e93d30eecfb6/02-plugin-submenu-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9885dcf3-018a-4dd9-87b1-6d494a221b94/02-plugin-submenu-preview-opt.png" alt="Sub menu page is now under settings" /></a><figcaption>The settings page has now been placed under the Settings menu. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9ac8a5dc-e770-4588-9854-e93d30eecfb6/02-plugin-submenu-opt.png">View large version</a>)</figcaption></figure>

In many cases, the most appropriate place to add a plugin settings page is under the Settings item. In the <a href="https://codex.wordpress.org/Administration_Menus">WordPress codex</a> it explains that the Settings section is used to "Display plugin options that only administrators should view." However, this is just a guideline, not a rule.

Now that we have our settings page set up and we know how to move the items around, we can start working on the fields. The work we have done thus far will be reused for the various methods below.</p>

## Approach 1: Using The Built-In WordPress Functionality

Before we get too deep into the code, let's go over some of the pros and cons of using this approach.</p>

### Pros

*   Easy to integrate into existing settings pages
*   Sanitization is done for you
*   Unlikely to break since the code is managed by WordPress
*   Can be used for both themes and plugins
*   Flexible, secure and extensible

### Cons

*   Custom data validation is manual
*   Advanced field types (repeaters, maps, uploads, etc.) are more difficult to implement

#### When should you use this approach?

This approach is flexible enough that it can be customized for very simple or very advanced settings pages. You can use this method in most situations if you don't mind doing some things manually.</p>

### Getting Started

Using this approach we'll need to follow the same markup that WordPress's own options pages use. We should modify our <code>plugin_settings_page_content</code> method to the following:

<pre><code class="language-markup">public function plugin_settings_page_content() { ?&gt;
	&lt;div class="wrap"&gt;
		&lt;h2&gt;My Awesome Settings Page&lt;/h2&gt;
		&lt;form method="post" action="options.php"&gt;
            &lt;?php
                settings_fields( 'smashing_fields' );
                do_settings_sections( 'smashing_fields' );
                submit_button();
            ?&gt;
		&lt;/form&gt;
	&lt;/div&gt; &lt;?php
}
</code></pre>

The markup above is directly from the WordPress codex on <a href="https://codex.wordpress.org/Creating_Options_Pages">creating options pages</a>. The method name should match the callback name we put in the <code>add_menu_page</code> function above. The wrapper <code>div</code> is actually the same as a default WordPress form and will pull in the styles from those sections. The <code>form</code> tag is pointing to the default options form handler for WordPress.

The three lines of PHP do several things:

*   The `settings_fields` function is basically a reference for the rest of our fields. The string argument you put in that function should match the `$slug` variable we set up earlier – it will be in all of the fields we register later in the plugin. This function also outputs a few hidden inputs for [the nonce](https://codex.wordpress.org/WordPress_Nonces), form action and a few other fields for the options page.
*   The next function, `do_settings_sections`, is a placeholder for the sections and fields we will register elsewhere in our plugin.
*   The last function, `submit_button`, will output the submit input, but it will also add some classes based on the status of the page. There may be other arguments you will want to pass into the `submit_button` function; they are outlined in the [codex](https://codex.wordpress.org/Function_Reference/submit_button).

If we refresh our settings page we should get something that looks like this:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4333c0b7-7ced-430e-b756-0ceadaddefd5/03-empty-settings-page-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4333c0b7-7ced-430e-b756-0ceadaddefd5/03-empty-settings-page-preview-opt.png" alt="Blank WordPress Settings Page" /></a><figcaption>Our settings page before registering sections and fields.</figcaption></figure>

It's looking a little sparse! Let's start setting up the fields now.</p>

### Sections And Fields

WordPress separates its options pages into sections. Each section can have a list of fields associated to it. We need to register a section in our plugin before we can start adding our fields. Add the following code to your constructor function:

<pre><code class="language-php">add_action( 'admin_init', array( $this, 'setup_sections' ) );</code></pre>

This hook will set up the sections for our page. Here is the code for the callback:

<pre><code class="language-php">public function setup_sections() {
	add_settings_section( 'our_first_section', 'My First Section Title', false, 'smashing_fields' );
}</code></pre>

The first argument is a unique identifier for the section and we will be using this for the fields we wish to assign to the section. These identifiers should be unique for all new sections on this page. The next argument is the title that is generated above the section – you can make it anything you want. The third argument is the callback. Right now I have it set to <code>false</code>, but we will revisit this shortly. The fourth argument is the options page to which the options will be added (the <code>$slug</code> variable from earlier).

So why is there a <code>false</code> in our callback? Well, something that isn't very clear when setting up WordPress options using their documentation is that multiple sections can share a callback. Often when you set up a callback there is a 1-for-1 relationship between the hook and the callback. So just for an example let's try creating three sections with the same callback:

<pre><code class="language-php">public function setup_sections() {
	add_settings_section( 'our_first_section', 'My First Section Title', array( $this, 'section_callback' ), 'smashing_fields' );
	add_settings_section( 'our_second_section', 'My Second Section Title', array( $this, 'section_callback' ), 'smashing_fields' );
	add_settings_section( 'our_third_section', 'My Third Section Title', array( $this, 'section_callback' ), 'smashing_fields' );
}</code></pre>

All three of these sections have the callback <code>section_callback</code> set in that third argument slot. If we then create a method that matches that callback and drop a "Hello World" in there:

<pre><code class="language-php">public function section_callback( $arguments ) {
 	echo '</code></pre>

Hello World

'; }

we get something that looks like this:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/16653910-7902-4794-8fdd-4fb341c5fd5c/04-same-callback-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/16653910-7902-4794-8fdd-4fb341c5fd5c/04-same-callback-preview-opt.png" alt="Three sections sharing the same callback function" /></a><figcaption>Three sections sharing the same callback.</figcaption></figure>

I know what you're thinking, "Why the heck would I want to have the same text under all of my sections?" The answer is that you probably wouldn't. This is where we can get a little tricky with the <code>add_settings_section</code> function. If you look at the <a href="https://codex.wordpress.org/Function_Reference/add_settings_section">documentation for that function</a> you will see that in the <strong>Notes</strong> portion of the page the callback function will be assigned an array of arguments that directly correlate to the arguments in our hook. If you go in and <code>var_dump( $arguments )</code> you will see all of the arguments getting passed into our function.

We can then write a simple switch in our callback to change out the text based on the ID that is passed into it:

<pre><code class="language-php">public function section_callback( $arguments ) {
	switch( $arguments['id'] ){
		case 'our_first_section':
			echo 'This is the first description here!';
			break;
		case 'our_second_section':
			echo 'This one is number two';
			break;
		case 'our_third_section':
			echo 'Third time is the charm!';
			break;
	}
}</code></pre>

Now we have custom text for each section that we can change out in one function!

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/27538bca-e40c-4728-b57f-c76eb02a7bcb/05-section-switch-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/27538bca-e40c-4728-b57f-c76eb02a7bcb/05-section-switch-preview-opt.png" alt="Custom text under each section" /></a><figcaption>Custom text under each section.</figcaption></figure>

Of course, you can specify unique callbacks for these sections as well, but this approach allows you to consolidate your code into a single function. This idea works the same for setting up fields. We can have all of our fields share a callback and have it output the correct field type based on the arguments we pass in. Let's add the fields to our constructor method. Put this code right after our sections hook in the constructor:

<pre><code class="language-php">add_action( 'admin_init', array( $this, 'setup_fields' ) );</code></pre>

Since you know the drill already, I'll just give you the callback for our action:

<pre><code class="language-php">public function setup_fields() {
    add_settings_field( 'our_first_field', 'Field Name', array( $this, 'field_callback' ), 'smashing_fields', 'our_first_section' );
}</code></pre>

The arguments in this function are similar to the ones in the sections function. The first argument is the unique identifier for the field. The second is the label that shows up next to the field. In the third argument you can see I am calling the method <code>field_callback</code>; we'll create that callback in just a second. The fourth is the options page we want to use (our <code>$slug</code> from earlier). The fifth argument is the <strong>unique identifier for the section</strong> to which we want to assign this field.

Here is the code for the callback in our third argument:

<pre><code class="language-php language-html">public function field_callback( $arguments ) {
	echo '&lt;input name="our_first_field" id="our_first_field" type="text" value="' . get_option( 'our_first_field' ) . '" /&gt;';
}</code></pre>

Here I am simply copying over the field's unique identifier into the name, ID and our <code>get_option</code> function. Let's see how our page looks with our new field attached:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cac99884-3445-4e5c-a76e-6dbb903c062d/06-field-attached-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cac99884-3445-4e5c-a76e-6dbb903c062d/06-field-attached-preview-opt.png" alt="Our settings page with our first field." /></a><figcaption>The setting page with our first field attached.</figcaption></figure>

Awesome, we have our field on the page! Try adding some content to it and hitting save changes, I'll wait here…

Did you do it? If you have done everything right up to this point you should have gotten an error saying something like <code>ERROR: options page not found</code>, or similar. The reason this happens is actually a security feature in WordPress.

You see, without this feature, a user could go into the HTML and change the name of a field to anything they wanted, hit save, and it would enter that option into the database with whatever name it was given (assuming it was a valid option name). This could allow any user to change options on other pages (even ones they couldn't normally access) by simply entering the correct name into the field and hitting save – not cool.

This problem is solved by adding a function called <code>register_setting</code>. Unless you specifically tell WordPress, "Hey, this field is allowed to be saved on this page", WordPress won't update a field in the database. So underneath our field markup, we will add this new function. Here is what the callback looks like after we add the code:

<pre><code class="language-php language-html">public function field_callback( $arguments ) {
	echo '&lt;input name="our_first_field" id="our_first_field" type="text" value="' . get_option( 'our_first_field' ) . '" /&gt;';
	register_setting( 'smashing_fields', 'our_first_field' );
}</code></pre>

The first argument in the new function is the options page we want to save the field on (the <code>$slug</code> from earlier) and the second argument is the field we want to save. Now try and update the field – it worked!

Congratulations! You just saved your first field using the WordPress Settings API. Now what if we want to have some different field types instead of just text? Let's revisit our field callback and talk about that <code>$arguments</code> variable getting passed into our function.</p>

### Field Arguments

If we go into our field callback and <code>var_dump( $arguments )</code> we will get an empty array. What gives? In our section callback we got a bunch of stuff about the section. Well, there is something different going on here. If you check out the <a href="https://codex.wordpress.org/Function_Reference/add_settings_field">documentation</a> for <code>add_settings_field</code> there is a fifth argument that can be passed into the function. That variable directly correlates to the <code>$arguments</code> variable in our callback. So we are going to want to put our new stuff in there.

If we look at one of the default fields in a WordPress settings page we can see there are several areas that we can add to our field to get some default formatting. Here is a screenshot of the timezone field in the general settings page:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7244a4e7-9f09-4eaf-81d5-4ccc61b71f49/07-timezone-field-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/56aa38aa-c614-48f0-92e8-f5cc3edbf35b/07-timezone-field-preview-opt.png" alt="The WordPress timezone field" /></a><figcaption>The WordPress timezone field. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7244a4e7-9f09-4eaf-81d5-4ccc61b71f49/07-timezone-field-opt.png">View large version</a>)</figcaption></figure>

Using this field as a starting point let's go over the data we want to pass into our field callback.

*   The unique identifier
*   The label for the field (Timezone in the example)
*   What section it should go into
*   The type of field (text, textarea, select, etc.)
*   In the case that there are multiple options, we'll want those
*   Maybe a placeholder if the field type supports one
*   Helper text (to the right of the field in the example)
*   Supplemental text (underneath the field in the example)
*   Maybe a default selection if there is one

From this list we can set up an associative array of fields and values that we can pass into our callback:

<pre><code class="language-phtml">public function setup_fields() {
	$fields = array(
		array(
			'uid' =&gt; 'our_first_field',
			'label' =&gt; 'Awesome Date',
			'section' =&gt; 'our_first_section',
			'type' =&gt; 'text',
			'options' =&gt; false,
			'placeholder' =&gt; 'DD/MM/YYYY',
			'helper' =&gt; 'Does this help?',
			'supplemental' =&gt; 'I am underneath!',
			'default' =&gt; '01/01/2015'
		)
	);
	foreach( $fields as $field ){
		add_settings_field( $field['uid'], $field['label'], array( $this, 'field_callback' ), 'smashing_fields', $field['section'], $field );
		register_setting( 'smashing_fields', $field['uid'] );
	}
}
</code></pre>

So the first thing we have here is a variable called <code>$fields</code> which will hold all of the fields we want to create. Inside that array we have another array that holds the specific data for each field. I have set up the data to exactly match our list above. Then, I loop through each field (we will add more shortly) in the array and add the field and register it. At the end of the <code>add_settings_field</code> function I am also adding the entire array of data for that specific field so we can do some stuff in the callback function. Let's take a look at that callback function here:

<pre><code class="language-php">public function field_callback( $arguments ) {
    $value = get_option( $arguments['uid'] ); // Get the current value, if there is one
    if( ! $value ) { // If no value exists
        $value = $arguments['default']; // Set to our default
    }

	// Check which type of field we want
    switch( $arguments['type'] ){
        case 'text': // If it is a text field
            printf( '&lt;input name="%1$s" id="%1$s" type="%2$s" placeholder="%3$s" value="%4$s" /&gt;', $arguments['uid'], $arguments['type'], $arguments['placeholder'], $value );
            break;
    }

	// If there is help text
    if( $helper = $arguments['helper'] ){
        printf( '&lt;span class="helper"&gt; %s&lt;/span&gt;', $helper ); // Show it
    }

	// If there is supplemental text
    if( $supplimental = $arguments['supplemental'] ){
        printf( '&lt;p class="description"&gt;%s&lt;/p&gt;', $supplimental ); // Show it
    }
}</code></pre>

In the example above, we are doing several things. We are setting the default values for fields if they are empty and adding the helper and supplemental text. The most important part in our code, though, is the switch statement. In this statement we are going to outline how our arguments will be handled based on the field type we want.

For example, if we have a text field, we have no need to have multiple options. However, a <code>&lt;select&gt;</code> dropdown must have options to work properly. Since we have text types already set up, let's run this code and see what we get.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/803577fd-6d03-46c2-8e0f-049a4e0be3f7/08-field-callback-array-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/803577fd-6d03-46c2-8e0f-049a4e0be3f7/08-field-callback-array-opt.png" alt="Our field filled out including placeholder" /></a><figcaption>Our field filled out including placeholder text. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/803577fd-6d03-46c2-8e0f-049a4e0be3f7/08-field-callback-array-opt.png">View large version</a>)</figcaption></figure>

When you load your plugin settings page you should see the top field in this image. The bottom is what you will see if you remove the content from the field (i.e. the placeholder). If I were to remove the <code>helper</code> or <code>supplimental</code> arguments from our fields array, they should disappear on the settings page. We can also change the <code>section</code> argument and move around the placement of the field in the sections.

OK, so we have text fields; how about some more complex field types? Let's take another look at our switch statement and add the option for text areas and single selects:

<pre><code class="language-phtml">switch( $arguments['type'] ){
	case 'text': // If it is a text field
		printf( '&lt;input name="%1$s" id="%1$s" type="%2$s" placeholder="%3$s" value="%4$s" /&gt;', $arguments['uid'], $arguments['type'], $arguments['placeholder'], $value );
		break;
	case 'textarea': // If it is a textarea
		printf( '&lt;textarea name="%1$s" id="%1$s" placeholder="%2$s" rows="5" cols="50"&gt;%3$s&lt;/textarea&gt;', $arguments['uid'], $arguments['placeholder'], $value );
		break;
	case 'select': // If it is a select dropdown
		if( ! empty ( $arguments['options'] ) &amp;&amp; is_array( $arguments['options'] ) ){
			$options_markup = ’;
			foreach( $arguments['options'] as $key =&gt; $label ){
				$options_markup .= sprintf( '&lt;option value="%s" %s&gt;%s&lt;/option&gt;', $key, selected( $value, $key, false ), $label );
			}
			printf( '&lt;select name="%1$s" id="%1$s"&gt;%2$s&lt;/select&gt;', $arguments['uid'], $options_markup );
		}
		break;
}
</code></pre>

In the code above you will notice several differences between each of the field types. Although text areas are functionally similar to regular text fields, they require different markup. Select dropdowns are a whole other animal because of the options. We need to loop through the options and set values, selected states, and labels. So our markup is drastically different.

Now that we have updated our callback function, let's see how the field data has changed:

<pre><code class="language-phtml">$fields = array(
	array(
		'uid' =&gt; 'our_first_field',
		'label' =&gt; 'Awesome Date',
		'section' =&gt; 'our_first_section',
		'type' =&gt; 'text',
		'options' =&gt; false,
		'placeholder' =&gt; 'DD/MM/YYYY',
		'helper' =&gt; 'Does this help?',
		'supplemental' =&gt; 'I am underneath!',
		'default' =&gt; '01/01/2015'
	),
	array(
		'uid' =&gt; 'our_second_field',
		'label' =&gt; 'Awesome Date',
		'section' =&gt; 'our_first_section',
		'type' =&gt; 'textarea',
		'options' =&gt; false,
		'placeholder' =&gt; 'DD/MM/YYYY',
		'helper' =&gt; 'Does this help?',
		'supplemental' =&gt; 'I am underneath!',
		'default' =&gt; '01/01/2015'
	),
	array(
		'uid' =&gt; 'our_third_field',
		'label' =&gt; 'Awesome Select',
		'section' =&gt; 'our_first_section',
		'type' =&gt; 'select',
		'options' =&gt; array(
			'yes' =&gt; 'Yeppers',
			'no' =&gt; 'No way dude!',
			'maybe' =&gt; 'Meh, whatever.'
		),
		'placeholder' =&gt; 'Text goes here',
		'helper' =&gt; 'Does this help?',
		'supplemental' =&gt; 'I am underneath!',
		'default' =&gt; 'maybe'
	)
);</code></pre>

Here are three fields, each one using a different field type in our plugin. The first one we've already gone over. The second is our new <code>textarea</code> field. We can pass the same parameters with the array (with the exception of the UID), but a simple change to our type and we will get a <code>textarea</code> instead. The last field in this array is the select dropdown. The main update here is the addition of the options array. We add a simple associative array with the array key as the HTML option value, and the label. Using this array, here is what our fields look like:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/84766141-7776-4e62-a638-19f8ecb48a36/09-all-fields-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/70853275-1e1b-45c2-91a7-f1b8ab3d1608/09-all-fields-preview-opt.png" alt="Our settings page after the fields are filled out" /></a><figcaption>Our settings page with fields. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/84766141-7776-4e62-a638-19f8ecb48a36/09-all-fields-opt.png">View large version</a>)</figcaption></figure>

### Almost done!

We now have a functioning plugin settings page. We've set up the sections for the page, the options, all of the callbacks and registered the fields. The only thing left is getting our setting values elsewhere. Believe it or not, we've already done this. At the top of our field callback you can see we are checking for the database value:

<pre><code class="language-php">$value = get_option( $arguments['uid'] );</code></pre>

We can use the same code in our plugin (or theme) and simply pass the <code>uid</code> into the function. So if I wanted to get the value of <code>our_first_field</code> I would simply write:

<pre><code class="language-php">get_option('our_first_field')</code></pre>

Hey presto! We have our awesome plugin and our awesome settings! Obviously we've only set up a few field types but I have gone through and added more in the <a href="https://github.com/rayman813/smashing-custom-fields/blob/master/smashing-fields-approach-1/smashing-fields.php">code repository for this approach</a> (specifically text fields, passwords, numbers, textareas, select dropdowns, multiselects, radio buttons and checkboxes).</p>

## Approach 2: Setting Up A Custom Form And Handler

In the past this approach was the only way to add settings pages. Before WordPress 2.7 plugin authors had to create their own custom forms and handlers. This obviously led to a lot of bugs and inconsistencies between plugins. While this approach is somewhat deprecated, it is still a viable option in some cases.</p>

### Pros

*   You can submit the form to custom and remote handlers
*   You can bypass some of the built-in Settings API restrictions

### Cons

*   Compatibility must be maintained by the developer
*   Must sanitize and validate manually

#### When should you use this approach?

Use this approach when you absolutely must have a custom handler or a highly custom interface. You can probably get away with Approach 1 in most cases, but you have more flexibility with validation and handling using this method.</p>

### Getting Started

Before we get into the details we need to come up with a scenario where we would use a custom handler. For simplicity's sake, let's make a form that will verify a username and an email address. We <em>could</em> pull the data from a database or even a remote server. In this case I will set up an array with valid usernames and email addresses for us to check against. We will then store the field values the user entered and store them in the database.</p>

### Creating the Form

Like I mentioned before, we will follow the same steps that we did in <a href="#plugin_setup">"Creating Our Plugin And Settings Page"</a>. For this approach we will set up our fields using static HTML markup. We will add this code to the callback from the <code>plugin_settings_page_content</code> function like this:

<pre><code class="language-phtml">public function plugin_settings_page_content() {
	?&gt;
	&lt;div class="wrap"&gt;
		&lt;h2&gt;My Awesome Settings Page&lt;/h2&gt;
		&lt;form method="POST"&gt;
			&lt;table class="form-table"&gt;
				&lt;tbody&gt;
					&lt;tr&gt;
						&lt;th&gt;&lt;label for="username"&gt;Username&lt;/label&gt;&lt;/th&gt;
						&lt;td&gt;&lt;input name="username" id="username" type="text" value="" class="regular-text" /&gt;&lt;/td&gt;
					&lt;/tr&gt;
					&lt;tr&gt;
						&lt;th&gt;&lt;label for="email"&gt;Email Address&lt;/label&gt;&lt;/th&gt;
						&lt;td&gt;&lt;input name="email" id="email" type="text" value="" class="regular-text" /&gt;&lt;/td&gt;
					&lt;/tr&gt;
				&lt;/tbody&gt;
			&lt;/table&gt;
			&lt;p class="submit"&gt;
				&lt;input type="submit" name="submit" id="submit" class="button button-primary" value="Check My Info!"&gt;
			&lt;/p&gt;
		&lt;/form&gt;
	&lt;/div&gt; &lt;?php
}
</code></pre>

You can see above that we are just adding some static HTML for our fields. We are duplicating the markup from the core WordPress settings pages. We are also omitting the form action so that it will submit the form to the current page as opposed to the default <i>options.php</i> handler.

Before we write our custom handler, let's put in some quick security features. The first thing we should do is put a <a href="https://codex.wordpress.org/WordPress_Nonces">nonce</a> in our form. Nonces will protect against cross-site request forgery attempts, which is similar to user spoofing or replay attacks. Let's put the nonce in our HTML:

<pre><code class="language-html">&lt;form method="POST"&gt;
	&lt;?php wp_nonce_field( 'awesome_update', 'awesome_form' ); ?&gt;
	&lt;table class="form-table"&gt;
</code></pre>

The <code><a href="https://codex.wordpress.org/Function_Reference/wp_nonce_field">wp_nonce_field</a></code> will add a couple of hidden fields to our form; the nonce and the referrer. We will come back to the nonce when we go through the handler code.

Next we need to add a field to detect when the form has been updated. We can do this by simply adding a hidden field at the top of our form:

<pre><code class="language-html">&lt;form method="POST"&gt;
	&lt;input type="hidden" name="updated" value="true" /&gt;
	&lt;?php wp_nonce_field( 'awesome_update', 'awesome_form' ); ?&gt;
	&lt;table class="form-table"&gt;
</code></pre>

Now we can put a snippet of code at the top of our page to detect when our form is submitted and send us to our custom handler:

<pre><code class="language-phmtl">public function plugin_settings_page_content() {
	if( $_POST['updated'] === 'true' ){
		$this-&gt;handle_form();
	} ?&gt;
	&lt;div class="wrap"&gt;
		&lt;h2&gt;My Awesome Settings Page&lt;/h2&gt;
</code></pre>

Here we are simply checking if the hidden <code>updated</code> field has been submitted and, if it has, we call a method in our plugin called <code>handle_form</code>. This is where we can start writing our custom handler.</p>

### Creating the handler

There are a couple of things we need to check in the handler before we actually manage the form data. We first need to check if our nonce exists and is valid:

<pre><code class="language-phtml">public function handle_form() {
    if(
		! isset( $_POST['awesome_form'] ) ||
		! wp_verify_nonce( $_POST['awesome_form'], 'awesome_update' )
	){ ?&gt;
    	&lt;div class="error"&gt;
           &lt;p&gt;Sorry, your nonce was not correct. Please try again.&lt;/p&gt;
    	&lt;/div&gt; &lt;?php
    	exit;
    } else {
    	// Handle our form data
    }
}
</code></pre>

The code above verifies that the nonce is correct. If it is invalid we give the user a message about why the form wasn't updated. If the nonce exists and is correct, we can handle our form. Let's write the code for our form handler now (this code will replace the comment in the snippet above):

<pre><code class="language-phtml">$valid_usernames = array( 'admin', 'matthew' );
$valid_emails = array( 'email@domain.com', 'anotheremail@domain.com' );

$username = sanitize_text_field( $_POST['username'] );
$email = sanitize_email( $_POST['email'] );

if( in_array( $username, $valid_usernames ) &amp;&amp; in_array( $email, $valid_emails ) ){
	update_option( 'awesome_username', $username );
	update_option( 'awesome_email', $email );?&gt;
	&lt;div class="updated"&gt;
		&lt;p&gt;Your fields were saved!&lt;/p&gt;
	&lt;/div&gt; &lt;?php
} else { ?&gt;
	&lt;div class="error"&gt;
		&lt;p&gt;Your username or email were invalid.&lt;/p&gt;
	&lt;/div&gt; &lt;?php
}</code></pre>

Let's go through the code in this section. The first couple of lines are the arrays of valid usernames/emails that we will be checking against. These array values could be populated from anywhere.

The next two lines are the values that our user has entered into the form. We are using the built-in <a href="https://codex.wordpress.org/Validating_Sanitizing_and_Escaping_User_Data">sanitization functions</a> that WordPress gives us. This step is important to avoid several vulnerabilities with web forms. Next, we are checking if the values supplied by the users are in our array of acceptable values. If they are, update the form options in the database. This step could also be replaced with a custom storage mechanism. We are also giving the user a message that their fields were saved. If the user's input is invalid, we tell them so.

The last thing we need to do is show the stored fields in the form after they have been input. We will do that in the same way we would retrieve these fields elsewhere in the plugin: with the <code>get_option</code> function. Here are the fields after we add the correct code:

<pre><code class="language-html">&lt;tr&gt;
	&lt;th&gt;&lt;label for="username"&gt;Username&lt;/label&gt;&lt;/th&gt;
	&lt;td&gt;&lt;input name="username" id="username" type="text" value="&lt;?php echo get_option('awesome_username'); ?&gt;" class="regular-text" /&gt;&lt;/td&gt;
&lt;/tr&gt;
&lt;tr&gt;
	&lt;th&gt;&lt;label for="email"&gt;Email Address&lt;/label&gt;&lt;/th&gt;
	&lt;td&gt;&lt;input name="email" id="email" type="text" value="&lt;?php echo get_option('awesome_email'); ?&gt;" class="regular-text" /&gt;&lt;/td&gt;
&lt;/tr&gt;
</code></pre>

Now we are ready to test our form. Try putting in the username <b>admin</b> and the email address <b>email@domain.com</b>. You should get the following on your form:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0cf78355-2f78-40a7-9848-5bb2528a3c79/10-saved-fields-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cac02600-13af-44ea-a3fd-a66efa83f1cf/10-saved-fields-preview-opt.png" alt="The saved fields after we enter correct values" /></a><figcaption>The saved fields after we enter correct values. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0cf78355-2f78-40a7-9848-5bb2528a3c79/10-saved-fields-opt.png">View large version</a>)</figcaption></figure>

If you try setting either field to an invalid value, you should get an error message and the fields shouldn't update because of our custom handler.

That's it for our second approach! You've now set up a custom form and handler to manage your plugin fields. The completed code for this approach can be found in <a href="https://github.com/rayman813/smashing-custom-fields">this article's repository</a>. Now, let's move on to our final approach.</p>

## Approach 3: Integrating ACF (Advanced Custom Fields) Into Your Plugin

If you haven't yet used <a href="https://www.advancedcustomfields.com/">ACF</a> by <a href="https://www.elliotcondon.com/">Elliot Condon</a>, let me introduce you. ACF is a wonderful field manager for WordPress. One of the best things about it is the field configuration interface. It makes it quite easy to spin up fields for a number of different pages within WordPress (such as posts, pages, users, taxonomies, even their own integrated options pages). You may think "I can't integrate someone else's plugin into my own – that's shady!" but Mr. Condon understands the plight of his fellow developers and has planned for this in his plugin. You can view <a href="https://www.advancedcustomfields.com/resources/including-acf-in-a-plugin-theme/">his documentation on this topic</a>, but I will be restating some of it here. Let's go over the rules.

1.  First, if you are distributing a free plugin, you **must** use the free version of ACF. This is so that people can't get hold of the PRO version from your free plugin – that would not be cool. You can use the PRO version in premium plugins and themes no problem, just make sure you buy the developer license.
2.  Second, do not modify ACF's copyright info. Give the man some credit!
3.  Lastly, don't distribute the license key with your plugin.

Now, the pros and cons of this approach:

### Pros

*   Very easy to integrate into themes and plugins
*   You can take advantage of the advanced fields that are part of ACF
*   Code and security updates are managed by the ACF team
*   ACF has great addons and support if you get stuck
*   Configuring your fields is super simple because of the field configuration UI

### Cons

*   Limited access to markup
*   Creates a dependency for your plugin or theme
*   To keep ACF current you must keep it updated in your plugin/theme files (more info below)

#### When should you use this approach?

When you want to build an advanced settings interface very quickly and you don't need to customize the look and feel.</p>

### Getting Started

For this approach I will show you how to set up the options page for the free version of ACF. To view a guide on setting up the PRO version check out the <a href="https://www.advancedcustomfields.com/resources/options-page/">ACF documentation</a>. To get started we will be adding ACF to our plugin directory. First, download the latest version of ACF and unzip its contents. In your plugin directory create a <i>vendor</i> directory and add ACF to it. Your files should look like this:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c70c5d0e-4536-4804-b7c3-715f927e95bf/11-acf-directory-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fda0fd27-abaa-48a1-845e-386475664afd/11-acf-directory-preview-opt.png" alt="ACF in the plugin vendor directory" /></a><figcaption>ACF in the plugin vendor directory. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c70c5d0e-4536-4804-b7c3-715f927e95bf/11-acf-directory-opt.png">View large version</a>)</figcaption></figure>

Again, we will follow the steps we did in <a href="#plugin_setup">"Creating Our Plugin And Settings Page"</a>. Before we get into that, though, we should include ACF in our plugin.</p>

### Include ACF In Your Plugin

It's actually pretty easy to include ACF in your plugin – there are only three steps. First we have to include the main ACF file with PHP. Add the following code to the bottom of our constructor function:

<pre><code class="language-php">include_once( plugin_dir_path( __FILE__ ) . 'vendor/advanced-custom-fields/acf.php' );</code></pre>

If you refresh the admin you should see a new menu item titled <strong>Custom Fields</strong>. Before we go into that page and start setting up our fields we need to update a couple of paths in ACF. We need to tell ACF to look for its front-end assets and file includes in our plugin directory instead of its normal place. Add these two hooks to your constructor:

<pre><code class="language-php">add_filter( 'acf/settings/path', array( $this, 'update_acf_settings_path' ) );
add_filter( 'acf/settings/dir', array( $this, 'update_acf_settings_dir' ) );</code></pre>

And the callbacks for those hooks:

<pre><code class="language-php">public function update_acf_settings_path( $path ) {
	$path = plugin_dir_path( __FILE__ ) . 'vendor/advanced-custom-fields/';
	return $path;
}

public function update_acf_settings_dir( $dir ) {
	$dir = plugin_dir_url( __FILE__ ) . 'vendor/advanced-custom-fields/';
	return $dir;
}</code></pre>

The first callback updates the include paths for the PHP files within the ACF plugin. The second updates the URIs for the ACF assets. Now we can set up our fields.</p>

### Configuring Your Fields

Now comes the fun part: the ACF field configuration UI. Add a title and any fields you'd like in your form. There is a great walkthrough of what everything on this page does in the <a href="https://www.advancedcustomfields.com/resources/creating-a-field-group/">ACF documentation</a>. Here's how I have set up mine:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9cd6f590-e3f6-413f-9ddd-798501e1d081/12-acf-fields-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8c603652-d3d4-4e96-b31f-7ca90f920d2d/12-acf-fields-preview-opt.png" alt="ACF fields configured" /></a><figcaption>My ACF fields in the configuration UI. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9cd6f590-e3f6-413f-9ddd-798501e1d081/12-acf-fields-opt.png">View large version</a>)</figcaption></figure>

Once you are ready hit the <strong>Publish</strong> button on the right and your fields will be saved. Now we have to get the fields we set up into our plugin. Right now they only exist in the database. On the left-hand navigation, click the <strong>Tools</strong> item. On the new page, select the field group we just created and hit <strong>Generate Export Code</strong>. This will create a chunk of PHP code that we can now include in our plugin.

To add the options, we need to add a method call to our constructor. Add this line to the end of your constructor after our ACF include:

<pre><code class="language-phtml">$this-&gt;setup_options();</code></pre>

Then we can create the method that will wrap our options:

<pre><code class="language-phtml">public function setup_options() {
	if( function_exists( 'register_field_group' ) ) {
		register_field_group(array (
			'id' =&gt; 'acf_awesome-options',
			'title' =&gt; 'Awesome Options',
			'fields' =&gt; array (
				array (
					'key' =&gt; 'field_562dc35316a0f',
					'label' =&gt; 'Awesome Name',
					'name' =&gt; 'awesome_name',
					'type' =&gt; 'text',
					'default_value' =&gt; ’,
					'placeholder' =&gt; ’,
					'prepend' =&gt; ’,
					'append' =&gt; ’,
					'formatting' =&gt; 'html',
					'maxlength' =&gt; ’,
				),
				array (
					'key' =&gt; 'field_562dc9affedd6',
					'label' =&gt; 'Awesome Date',
					'name' =&gt; 'awesome_date',
					'type' =&gt; 'date_picker',
					'date_format' =&gt; 'yymmdd',
					'display_format' =&gt; 'dd/mm/yy',
					'first_day' =&gt; 1,
				),
				array (
					'key' =&gt; 'field_562dc9bffedd7',
					'label' =&gt; 'Awesome WYSIWYG',
					'name' =&gt; 'awesome_wysiwyg',
					'type' =&gt; 'wysiwyg',
					'default_value' =&gt; ’,
					'toolbar' =&gt; 'full',
					'media_upload' =&gt; 'yes',
				),
			),
			'location' =&gt; array (
				array (
					array (
						'param' =&gt; 'options_page',
						'operator' =&gt; '==',
						'value' =&gt; 'smashing_fields',
					),
				),
			),
			'menu_order' =&gt; 0,
			'position' =&gt; 'normal',
			'style' =&gt; 'default',
			'label_placement' =&gt; 'top',
			'instruction_placement' =&gt; 'label',
			'hide_on_screen' =&gt; ’,
			'active' =&gt; 1,
			'description' =&gt; ’,
		));
	}
}
</code></pre>

Now that we have our fields ready to go, we can add them to the settings page.</p>

### Modifying The Settings Page Code

To add the fields we just created to the page we will need to update our <code>plugin_settings_page_content</code> method.

Previously, we set up the form tag for our page. In this case we will let ACF do that part for us. Here is what our updated function should look like:

<pre><code class="language-phtml">public function plugin_settings_page_content() {
	do_action('acf/input/admin_head'); // Add ACF admin head hooks
	do_action('acf/input/admin_enqueue_scripts'); // Add ACF scripts

	$options = array(
		'id' =&gt; 'acf-form',
		'post_id' =&gt; 'options',
		'new_post' =&gt; false,
		'field_groups' =&gt; array( 'acf_awesome-options' ),
		'return' =&gt; admin_url('admin.php?page=smashing_fields'),
		'submit_value' =&gt; 'Update',
	);
	acf_form( $options );
}</code></pre>

The first two lines of our function are adding the scripts and styles that we will need for the settings fields. After that we are configuring the options for our form. You may notice that the value in the <code>field_groups</code> argument matches the ID from our <code>register_field_group</code> function. To see the other configuration parameters take a look at the <a href="https://www.advancedcustomfields.com/resources/acf_form/"><code>acf_form</code> documentation</a>. The last line in our function is actually going to render the form.

If you try to load the settings page now, you may see that the page is actually broken. This is because ACF needs to localize a few variables for JavaScript. To do this, we need to add another hook to our constructor:

<pre><code class="language-php">add_action( 'admin_init', array( $this, 'add_acf_variables' ) );</code></pre>

Now we need to set up the callback:

<pre><code class="language-php">public function add_acf_variables() {
	acf_form_head();
}</code></pre>

You can try adding some content and saving and it should work just like our other two approaches. This is what our page should look like:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f1cf4114-f509-4dd3-b762-9b31ad9ee889/13-acf-form-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/19a4312d-8321-4f2e-90a7-dc2f3348947f/13-acf-form-preview-opt.png" alt="Finished ACF form" /></a><figcaption>Our completed ACF form. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f1cf4114-f509-4dd3-b762-9b31ad9ee889/13-acf-form-opt.png">View large version</a>)</figcaption></figure>

There are just a couple of clean-up items we need address:

*   You might want to hide the fact that you are using ACF for your plugin. If this is the case, you need to hide the **Custom Fields** menu item. You can do this by adding this snippet to your constructor function:

        add_filter( 'acf/settings/show_admin', '__return_false' );

*   We should remove the database version of our field group. Just go to the custom fields section and hit the trash button. This step is optional since it will only affect the environment where you built the plugin, but it could introduce issues if you are testing your plugin on the same environment.</p>

### Using ACF Fields Within Your Plugin

To get the ACF fields you created, you simply need use the default ACF <a href="https://www.advancedcustomfields.com/resources/get-values-from-an-options-page/"><code>get_field</code> function</a>. The first option should be the unique ID for the field and the second argument set to <code>'option'</code>. Here is how we would get the <strong>Awesome Date</strong> field:

<pre><code class="language-php">get_field( 'awesome_date', 'option' )</code></pre>

And that's it. You have now set up a plugin with ACF settings! You can view the code for this approach in the <a href="https://github.com/rayman813/smashing-custom-fields">repository</a>.</p>

## Conclusion

So there you have it: three ways to make your plugins configurable. I would love to hear about the plugins you are able to create using these methods. Once again, I have set up <a href="https://github.com/rayman813/smashing-custom-fields">a repository</a> that houses the code for each of these approaches. Please feel free to fork them and customize them to fit your own needs.

As for my personal preferences for these approaches, I tend to lean towards Approach 1. I prefer to keep as few dependancies in my plugins as possible and you can customize the markup to theme the settings page for custom projects. For rapid prototypes, or projects where I need to set up very advanced fields I will use ACF – but it adds a level of complexity to managing plugin updates.

It is also worth mentioning the <a href="https://github.com/sc0ttkclark/wordpress-fields-api">proposal for a Fields API</a> by <a href="https://github.com/sc0ttkclark">Scott Clark</a>. While it is currently still a work in progress, the API would essentially allow plugin and theme developers the ability to use the same interface as the <a href="https://codex.wordpress.org/Theme_Customization_API">Customizer API</a> to create settings fields on other areas of the admin panel.</p>

## ACF Alternatives

As pointed out in the comments below, and to give developers other options that are similar to the ACF approach you can check out some alternatives that may offer different features. If you have more please submit them in the comments below! Here they are in no particular order:

*   [CMB2](https://github.com/WebDevStudios/CMB2) by WebDevStudios
*   [Meta Box](https://metabox.io) by Tran Ngoc Tuan Anh ( Rilwis )

{{< signature "dp, ml, og, il" >}}

