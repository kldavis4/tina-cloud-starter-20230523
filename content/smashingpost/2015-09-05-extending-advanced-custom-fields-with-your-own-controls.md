---
title: Extending Advanced Custom Fields With Your Own Controls
slug: extending-advanced-custom-fields-with-your-own-controls
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8c5ac9bf-6ee0-4063-b895-0c90157eb40e/01-map-and-radio-opt-small.png
date: 2015-09-05T16:42:58.000Z
author: daniel-pataki
description: >-
  [Advanced Custom Fields](https://www.advancedcustomfields.com/) (ACF) is a free
  WordPress plugin that replaces the regular custom fields interface in
  WordPress with something far more powerful, offering a user-friendly interface
  for complex fields like location maps, date pickers and more.

  In this article I'll show you how you can extend ACF by adding your own
  controls to tailor the experience to your needs.
categories:
  - WordPress
  - Plugins
  - Techniques (WP)
---
<a href="https://www.advancedcustomfields.com/">Advanced Custom Fields</a> (ACF) is a free WordPress plugin that replaces the regular custom fields interface in WordPress with something far more powerful, offering a user-friendly interface for complex fields like location maps, date pickers and more.

In this article I'll show you how you can extend ACF by adding your own controls to tailor the experience to your needs.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Extend WordPress With Custom Fields](https://www.smashingmagazine.com/2010/04/extend-wordpress-with-custom-fields/)
*   [Custom Fields Hacks For WordPress](https://www.smashingmagazine.com/2009/05/10-custom-fields-hacks-for-wordpress/)
*   [How To Create Custom Post Meta Boxes In WordPress](https://www.smashingmagazine.com/2011/10/create-custom-post-meta-boxes-wordpress/)
*   [<span class="headline">The Complete Guide To Custom Post Types</span>](https://www.smashingmagazine.com/2012/11/complete-guide-custom-post-types/)

## How ACF Works

ACF is a collection of fields which can be added to a number of locations in WordPress, such as posts, taxonomies, users and so on. They share a common interface and a WordPress-compatible saving mechanism (using meta fields and options).

{{% feature-panel %}}

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/577ce81c-8f08-4e99-9883-b9e2ea6a4a05/01-map-and-radio-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8c5ac9bf-6ee0-4063-b895-0c90157eb40e/01-map-and-radio-opt-small.png" alt="A map and a radio field created with ACF" /></a><figcaption>A map and a radio field created with ACF. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/577ce81c-8f08-4e99-9883-b9e2ea6a4a05/01-map-and-radio-opt.png">View large version</a>)</figcaption></figure>

Each ACF field has field settings which you can think of as the back-end options for a field. Field settings allow you to control how the field behaves when displayed to the user. You may be able to control default values, how data is saved, and so on.

There is a default set shared by all fields, like field label, field name, field type, field instructions, required setting and conditional logic, but there are some field-specific settings as well.

A good example is the image field which allows users to select an image and save it. The field settings allow you to define the following:

*   Return value (image object, image URL or image ID)
*   Preview size (any defined image size)
*   Library (all or uploaded to post)

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5fc21591-7de5-4065-9a5b-db53db80c242/02-image-field-settings-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b01602e7-8328-4ac5-b844-3b6169b9ab25/02-image-field-settings-opt-small.png" alt="Settings for the image field in ACF" /></a><figcaption>Settings for the image field in ACF. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5fc21591-7de5-4065-9a5b-db53db80c242/02-image-field-settings-opt.png">View large version</a>)</figcaption></figure>

Fields are created within field groups which can be placed in a number of locations using powerful rule sets. Not only can you add your fields to edit profile pages, you can also restrict the visibility of a field group based on role, allowing access to admins only, for example.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f9b3255f-0a7d-4ee9-8e43-e1e9cb65891c/03-field-location-rules-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f3bbea77-43d7-4e4e-af57-3c49a8fc52e9/03-field-location-rules-opt-small.png" alt="Location rules for an ACF field group" /></a><figcaption>Location rules for an ACF field group. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f9b3255f-0a7d-4ee9-8e43-e1e9cb65891c/03-field-location-rules-opt.png">View large version</a>)</figcaption></figure>

## What's Available Out Of The Box

Right now ACF has 22 fields available, which includes basic fields like number, email, multi-select and radio, but more advanced ones as well, such as taxonomy selection and the user selector. You also get a few fields that use JavaScript to create a great interface, like the map field or the date and color-picker fields.

There are also quite a few fields available in the plugin repository. I've created <a href="https://profiles.wordpress.org/danielpataki#content-plugins">six ACF plugins myself</a>, like the Google Font Selector and Sidebar Selector, but a quick <a href="https://wordpress.org/plugins/search.php?type=term&amp;q=advanced+custom+fields">search in the repository</a> will come up with star rating fields, recent posts, link pickers, widget area fields and so on.

If you are a developer I can also heartily recommend the <a href="https://www.advancedcustomfields.com/pro/">pro version of ACF</a>. It costs $100 – which is quite a bit – but you can use it in unlimited projects. It contains a repeater field, a gallery field, a flexible content field and the ability to add options to options pages very easily.

The great thing about ACF is that the pro version is nice, but you don't need it in order to build something awesome. You can use the built-in fields or write your own if you need something different. Let's look at how that can be done.

## Extending Advanced Custom Fields

ACF can be extended by creating a separate plugin which integrates with the main ACF plugin. The heavy lifting is done by the <a href="https://github.com/elliotcondon/acf-field-type-template">ACF Field Type Template</a> which you can grab from GitHub.

This includes all the files you need and has great inline commenting that walks you through the process. It also contains all the possible functions you can use. You won't use all of them for each field, but you can leave the unwanted ones empty or delete them altogether.

In this tutorial I'll show you the steps I follow when creating an ACF plugin. I'll be creating a country selector which lets you select any country from a drop-down list. By the end you should be able to reproduce it and create your own, so let's get cracking!

### Step 1: A Local Environment

I like to do all my WordPress work locally. I won't go into too much detail here – you can take a look at Rachel Andrew’s “<a href="https://www.smashingmagazine.com/2015/07/development-to-deployment-workflow/">A Simple Workflow From Development To Deployment</a>” if you need some help. In a nutshell, I use a simple Vagrant box to create a local server and I use virtual hosts to create multiple projects.

The one additional aspect of my workflow is using symlinks to manage my plugins. I do this for three reasons:

*   I can keep my plugins separate from my WordPress installs.
*   A plugin can be symlinked to multiple WordPress installs which means I update the plugin in a central location and all installations use that code.
*   I can use any folder structure I like which comes in handy when working with Git packages.

The process isn't too difficult. Take a look at Tom McFarlin's “<a href="https://tommcfarlin.com/symbolic-links-with-wordpress/">Symbolic Links with WordPress</a>” article for more information. Since the template is designed to be a plugin, this step is not strictly necessary but I think symlinks are worth looking into for development purposes.</p>

### Step 2: Adding The Plugin And Renaming

Once you've grabbed the template from GitHub, copy and paste the whole directory into your plugins folder and rename it to <i>acf-country_selector</i>. You'll see that some of the files have <code>FIELD_NAME</code> in them; this is a placeholder for your actual field name which should be the same as the name of the folder (after "acf-"). In our case the field name is <code>country_selector</code>.

Some of you may be wondering why I've used an underscore instead of a dash: it's common practice to use dashes in file names. The use of an underscore relates to consistency and a rule for translatable strings.

We'll need to replace <code>FIELD_NAME</code> inside files as well. In some cases the placeholder is part of a function name where we can't use dashes. I could decide to use dashes in file names and underscores within files, but there would then be a problem with the text domain.

The text domain is set to <code>acf-FIELD_NAME</code>, which actually needs to be the same as the folder name. This excludes the use of a dash outside and an underscore inside files. Because of this I've decided to use underscores. There are simply fewer downsides to it.

Back to creating our plugin! Replace <code>FIELD_NAME</code> in all file names with <code>country_selector</code>. Once done, I recommend dropping the whole folder in a good editor such as <a href="https://www.sublimetext.com/">Sublime</a> or <a href="https://atom.io/">Atom</a>. Any editor that allows you to search and replace within multiple files at once will do.

Within our files there should be another set of placeholders: <code>FIELD_NAME</code> and <code>FIELD_LABEL</code>. There are a few more, but the others are used only once or twice and only in the readmes so you can replace those manually.

For this plugin I mass-replaced <code>FIELD_LABEL</code> with <code>Country Selector</code> and <code>FIELD_NAME</code> with <code>country_selector</code>.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/14669ac3-e4dd-4cda-a630-5fcca35cf843/04-search-replace-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3898f172-bf20-4533-841f-b1fcfb627a70/04-search-replace-opt-small.png" alt="Search and replace in a project in Atom" /></a><figcaption>Search and replace in a project in Atom. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/14669ac3-e4dd-4cda-a630-5fcca35cf843/04-search-replace-opt.png">View large version</a>)</figcaption></figure>

Finally, open <i>acf-country_selector.php</i> and fill out the meta information in the header. This will ensure that the plugin shows up in the admin with the data you provide. In this plugin's case I've filled it out like this:

<pre><code class="language-php">/*
Plugin Name: Advanced Custom Fields: Country Selector
Plugin URI: https://danielpataki.com
description: >-
  A plugin for ACF that allows you to select any country from a list
Version: 1.0.0
Author: Daniel Pataki
Author URI: https://danielpataki.com
License: GPLv2 or later
License URI: https://www.gnu.org/licenses/gpl-2.0.html
*/</code></pre>

At this stage you can go to the plugins section and activate it. You won't see any new fields just yet, but we can start chipping away at the code.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3f895f4b-dc28-455e-97b6-2caf27ff59f6/05-country-selector-plugin-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5119e9e1-690e-458f-9f35-2384ee089fc7/05-country-selector-plugin-opt-small.png" alt="Our country selector plugin displayed in the admin" /></a><figcaption>Our country selector plugin displayed in the admin. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3f895f4b-dc28-455e-97b6-2caf27ff59f6/05-country-selector-plugin-opt.png">View large version</a>)</figcaption></figure>

### Step 3: Field Basics

You may have noticed that there are two similar files: <i>acf-country_selector-v4.php</i> and <i>acf-country_selector-v5.php</i>. One is for version 4 of ACF, the other for version 5. Right now, version 5 is actually the pro version, but soon the free version will also be updated to 5.

This doesn't mean that the free version will have the premium fields, but it will run on a new and improved system. Since the free version is currently version 4, I will be looking at <i>acf-country_selector-v4.php</i> only. The methods for version 5 are very nearly the same, so it shouldn't be too difficult to create both.

If you're planning on releasing your plugin, I recommend using both files. Aside from some minor changes it's really a matter of copying and pasting than anything else.

Our first stop, then, is <i>acf-country_selector-v4.php</i>, and the <code>__construct()</code> function within. Most of this is filled out for us. We'll need to modify the value of <code>$this-&gt;category</code>. This determines which group our field type will be listed under. Since there's a "Choice" group and we'll be building a select field, let's use <code>Choice</code> as the value here.

I also want to allow the person who creates the field to set an initial value for the country field. This will be really useful if the field is used on a website which predominantly uses a specific country for the field. Instead of having to go down and select "Hungary", users could make that the initial value.

The <code>$this-&gt;defaults</code> array contains the defaults for our fields, like the <code>initial_value</code> field. I'll make the default "United States", which may be the most popular choice for the initial value. Here's the full contents of the <code>__contruct()</code> function at the end of all that:

<pre><code class="language-php">// vars
$this-&gt;name = 'country_selector';
$this-&gt;label = __( 'Country Selector' );
$this-&gt;category = __( 'Choice', 'acf' ); // Basic, Content, Choice, etc
$this-&gt;defaults = array(
	'initial_value' =&gt; 'United States'
);

// do not delete!
parent::__construct();

// settings
$this-&gt;settings = array(
	'path' =&gt; apply_filters('acf/helpers/get_path', __FILE__),
	'dir' =&gt; apply_filters('acf/helpers/get_dir', __FILE__),
	'version' =&gt; '1.0.0'
);</code></pre>

### Step 4: Field Settings

The next step is to configure the field settings we'll have. In our case this will be a single field for selecting the initial value of the front-end selector. This will be a selector with all countries selectable.

Before we create the selector, we need a list of countries. I created a little <a href="https://gist.github.com/danielpataki/2652bb42697b1a248761">Gist</a> which lists all of them in an array. I decided to create a method that returns all countries to make sure I can create country lists anywhere, without needing to add the large array more than once.</p>

<pre><code class="language-php">function get_countries() {
$countries = array( 'Afghanistan' =&gt; 'Afghanistan', 'Albania' =&gt; 'Albania', '...' );
return $countries;
}</code></pre>

I placed this function at the very end of the class, to separate it from the built-in ones. I can now use <code>$this-&gt;get_countries</code> within this class to return the array.

To add our initial value field we need to modify the contents of the <code>create_options()</code> method. Here's the full code for that function:

<pre><code class="language-php">function create_options( $field )
{
	$field = array_merge($this-&gt;defaults, $field);
	$key = $field['name'];

	// Create Field Options HTML
	?&gt;
&lt;tr class="field_option field_option_&lt;?php echo $this-&gt;name; ?&gt;"&gt;
&lt;td class="label"&gt;
	&lt;label&gt;&lt;?php _e("Initial Value",'acf'); ?&gt;&lt;/label&gt;
	&lt;p class="description"&gt;&lt;?php _e("The initial value of the country field",'acf'); ?&gt;&lt;/p&gt;
&lt;/td&gt;
&lt;td&gt;
	&lt;?php

	do_action('acf/create_field', array(
		'type'		=&gt;	'select',
		'name'		=&gt;	'fields['.$key.'][initial_value]',
		'value'		=&gt;	$field['initial_value'],
		'choices'	=&gt;	$this-&gt;get_countries()
	));

	?&gt;
&lt;/td&gt;
&lt;/tr&gt;
	&lt;?php

}</code></pre>

The main thing to keep in mind is that the name of the field <strong>must</strong> be <code>fields[field_key][field_name]</code>. My particular case translates to <code>fields[field_55e584fa90223][initial_value]</code>, but the key is generated for you, so you'll need a variable to reference it. Hence the use of <code>fields['.$key.'][initial_value]</code>.

If you need to add more field settings simply create some more defaults and add more fields following the pattern above. In version 5 the process is somewhat simpler as you don't have to wrap the whole thing in a bunch of HTML – that is done for you.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0a5228c4-3b2d-4288-a2d8-075951e327f6/06-country-settings-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2c26b826-bbe8-409e-ab0f-dce0b28c8fef/06-country-settings-opt-small.png" alt="Our custom setting for the country field" /></a><figcaption>Our custom setting for the country field. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0a5228c4-3b2d-4288-a2d8-075951e327f6/06-country-settings-opt.png">View large version</a>)</figcaption></figure>

### Step 5: Field Front-End

All that's left is to create the control the user will actually see. This is done in the <code>create_field()</code> method. You'll need to create the HTML yourself here but it shouldn't be too difficult to create a standard <code>&lt;select&gt;</code> field, right?

<pre><code class="language-php">function create_field( $field )
{
	$field = array_merge($this-&gt;defaults, $field);
	?&gt;
	&lt;div&gt;
		&lt;select name='&lt;?php echo $field['name'] ?&gt;'&gt;
			&lt;?php
				foreach( $this-&gt;get_countries() as $country ) :
			?&gt;
				&lt;option &lt;?php selected( $field['value'], $country ) ?&gt; value='&lt;?php echo $country ?&gt;'&gt;&lt;?php echo $country ?&gt;&lt;/option&gt;
			&lt;?php endforeach; ?&gt;
		&lt;/select&gt;
	&lt;/div&gt;
	&lt;?php
}</code></pre>

At this stage, your field is ready to go. If you add your field to a field group and view the field in action, you should see the country selector with the initial value selected. If you save the object you've added the field to, it will retain its value.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5818d402-5c36-4239-b29a-c44c9b8e7120/07-country-field-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ec70e55d-ebfd-4e07-a65a-991129f5b854/07-country-field-opt-small.png" alt="The completed country selector in action" /></a><figcaption>The completed country selector in action. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5818d402-5c36-4239-b29a-c44c9b8e7120/07-country-field-opt.png">View large version</a>)</figcaption></figure>

### Step 6: Adding Scripts And Styles

This plugin doesn't require any scripts and styles at the moment, but if we were to create a drop-down with the help of <a href="https://harvesthq.github.io/chosen/">Chosen</a>, for example, we would need to leverage the <code>input_admin_enqueue_scripts()</code> function.

In many cases you don't actually need to modify the code of this function. The enqueued script and style points to the already created files in the <i>js</i> and <i>css</i> folders – simply use those to add your code. If you enqueue third-party scripts like Chosen you should drop that in the <i>js</i> folder and enqueue it the same way.

Once downloaded, I placed the files required by Chosen in the correct directories. I put <i>chosen.min.css</i> in the <i>css</i> folder, <i>chosen.jquery.min.js</i> in the <i>js</i> directory, and the two images in the images directory. To make sure images are referenced correctly I replaced <code>url(</code> in the CSS file with <code>url(../img</code>.

With all the files in place, I used the <code>input_admin_enqueue_scripts()</code> to enqueue them, resulting in the following code.</p>

<pre><code class="language-php">function input_admin_enqueue_scripts() {

	// register ACF scripts
	wp_register_script( 'acf-input-country_selector', $this-&gt;settings['dir'] . 'js/input.js', array('acf-input'), $this-&gt;settings['version'] );

	// Chosen
	wp_register_script( 'chosen', $this-&gt;settings['dir'] . 'js/chosen.jquery.min.js', array('acf-input', 'jquery'), $this-&gt;settings['version'] );
	wp_register_style( 'chosen', $this-&gt;settings['dir'] . 'css/chosen.min.css', array('acf-input'), $this-&gt;settings['version'] );

	// scripts
	wp_enqueue_script(array(
		'acf-input-country_selector',
		'chosen',
	));

	// styles
	wp_enqueue_style(array(
		'chosen',
	));

}</code></pre>

Note that I removed the original CSS file that was added (<i>input.css</i>), but I kept the <i>input.js</i> file enqueued. We will need a little bit of JavaScript to apply Chosen, but we won't need any additional CSS, apart from Chosen's own.

The last step is to apply Chosen to our field, which is where <i>input.js</i> comes in handy. Opening up the file, you can see that it has a dedicated section for version 4 and for version 5. We'll be using the version 4 section, adding the Chosen initiation code. It's only one additional line which you need to add below <code>initialize_field( $(this) );</code>

<pre><code class="language-javascript">$(this).find('select').chosen()</code></pre>

Once in place, you should be able to search within the select field's values, making the UI that much better.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/de89231e-58d3-4362-97a0-01f332427439/08-chosen-opt.png" alt="08-chosen-opt" /><br>
<figcaption>Chosen applied to the select field. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/de89231e-58d3-4362-97a0-01f332427439/08-chosen-opt.png">View large version</a>)</figcaption></figure>

### Step 7: Modifying Values

There are a number of methods which serve to modify values after or before they are sent/received. These can be helpful for manipulating data between the user interface and the back-end logic. Here are the four most important methods, along with how they can be used:

*   `load_value()` is used to modify the value of the field after it is loaded from the database. This could be useful if you're saving complex things like geolocation. The saved value may be an array containing the latitude and longitude, but you actually want to display a string.
*   `update_value()` modifies the value before it is saved in the database. If the user enters a comma-separated value of IDs, you may want to save that as an array. Using the `update_value()` function you can modify it easily.
*   `load_field()` modifies the whole field after it is returned from the database.
*   `update_field()` modifies the whole field before it is saved to the database.</p>

## Further Possibilities

I hope you can see that creating your own field is actually a pretty simple matter. If you want to add elaborate JavaScript to make things as user-friendly as possible, that's all up to you – ACF supports it nicely. You can use a bunch of methods to play around with values and fields and much more. Browse through the template file for more information.

If that wasn't enough, ACF also has <a href="https://www.advancedcustomfields.com/resources/">powerful actions and filters</a>. Check out the documentation for more info.

If you'd like to check out a more complex field which contains JavaScript, styles and interaction with a third-party API, I invite you to check out the GitHub repository for my <a href="https://github.com/danielpataki/ACF-Google-Font-Selector">Google Font Selector Field</a>, which allows users to select fonts available from Google.

{{< signature "ml, og" >}}

