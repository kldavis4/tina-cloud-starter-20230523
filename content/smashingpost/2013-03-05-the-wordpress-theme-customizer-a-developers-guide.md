---
title: The WordPress Customizer – A Theme Developer's Guide
slug: the-wordpress-theme-customizer-a-developers-guide
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9d23f388-399a-4095-8b25-5cadc26e8126/wp-14.jpg
date: 2013-03-05T11:30:44.000Z
author: rachel-mccollin-2
description: >-
  In case you missed it, WordPress release 3.4 included a very exciting new
  development - the theme customizer. This allows users to tweak theme settings
  using a WYSIWYG interface and customise a theme so it includes the colours,
  fonts, text and pretty much anything else they want.
categories:
  - WordPress
  - Themes
  - Techniques (WP)
---
In case you missed it, release 3.4 included a very exciting new development: the WordPress Customizer for Themes. This allows users to <strong>tweak theme settings using a WYSIWYG interface</strong> and customize the theme so it includes the colors, fonts, text — and pretty much anything else — they want.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a1df19eb-691c-4d9c-9b23-c3763fcfc1ac/wp-theme-customizer.jpg"><img loading="lazy" decoding="async" title="WordPress 3.4 allows you to make extensive customizations to a theme, including colors, fonts, and text." src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a1df19eb-691c-4d9c-9b23-c3763fcfc1ac/wp-theme-customizer.jpg" alt="wordpress customizer" width="500" height="315" /></a><br>
<em>WordPress 3.4 allows you to make extensive customizations to a theme, including colors, fonts, and text.</em>

The purists out there may be throwing their hands up in horror — a WYSIWYG interface! Letting users alter themes themselves! Surely that opens the floodgates for the creation of thousands of ugly, messy WordPress websites? Well, yes, there is a risk of that. But more importantly, the Customizer means that if you're developing custom themes for client websites, or themes for other developers to use, you have a whole new set of tools to play with.</p>

## <span class="rh">Further Reading</span> on SmashingMag: [Link](https://www.smashingmagazine.com/2013/02/wordpress-community-offers-advice-beginners/#further-reading-on-smashingmag)

*   [How To Contribute To WordPress](https://www.smashingmagazine.com/2013/05/contributing-to-wordpress/)
*   [<span class="headline">How To Become A Top WordPress Developer</span>](https://www.smashingmagazine.com/2012/08/how-to-become-a-top-wordpress-developer/)
*   [The Design Community Offers Its Favorite Bits of Advice](https://www.smashingmagazine.com/2011/03/the-design-community-offers-its-favorite-bits-of-advice/)
*   [The Smashing Guide To Moving The Web Forward](https://www.smashingmagazine.com/2011/11/the-smashing-guide-to-moving-the-web-forward-community/)

<strong>With the Theme Customizer:</strong>

{{% feature-panel %}}

*   If you're developing free or premium themes for others to use, integrating the Customizer will make your themes much more appealing to developers and website owners.
*   If you're building client websites, you can let your client tweak the template content of their website such as the logo, tagline and contact details in a more intuitive way than by using a theme options page.
*   For both groups, you can let website users and developers make changes without having to rely on widgets or theme options pages — a less risky and less time-consuming approach.

So, let's start by having a look at what the Theme Customizer is and how it works for the user.</p>

## How The Theme Customizer Works For Users

The Theme Customizer has been integrated into the Twenty Eleven Theme, so you can try it out using that theme. There's a great video on the Ottopress blog showing you <a href="https://ottopress.com/2012/how-to-leverage-the-theme-customizer-in-your-own-themes/">how the Customizer works with Twenty Eleven</a>. Using it is simple:

1.  On the “Themes” page, search for and activate the Twenty Eleven Theme.
2.  On the same page, click on the “Customize” link under the current theme's description.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/93a4d2d3-15c6-4370-81d3-60fe2becb13c/themes-screen-showing-customiser-2.png"><img title="The “Customize” link is right below the current theme's description on the “Themes” page." src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b99db4b7-1330-47b5-9be2-37e3cdd80bbf/themes-screen-showing-customiser.png" alt="The “Customize” link is right below the current theme's description on the “Themes” page." width="500" height="233" /></a><br>
<em>The “Customize” link is right below the current theme's description on the “Themes” page. <a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/93a4d2d3-15c6-4370-81d3-60fe2becb13c/themes-screen-showing-customiser-2.png">Larger view</a>.</em>

1.  This brings up the Theme Customizer in the left column, along with a preview of your website on the right.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7f78a707-14d1-46a6-9bb6-188a6298229e/theme-customiser-twentyeleven-beforev2.png"><img loading="lazy" decoding="async" class="107949" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/79160712-aee2-4ca9-a165-34a8d5fe6ad0/theme-customiser-twentyeleven-beforev2.jpg" alt="The theme customizer shown with the twenty eleven theme" width="500" height="292" /></a><br>
<em>The Customizer options are shown side-by-side with a preview of your website, so you can test the effect of changes. <a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7f78a707-14d1-46a6-9bb6-188a6298229e/theme-customiser-twentyeleven-beforev2.png">Larger view</a>.</em>

1.  To make changes, all you have to do is select each of the available options and edit their settings. The options are:
    *   **Site title and tagline**.  Edit the title and tagline of the website without having to go to the “Settings” page.
    *   **Colors**.  In the Twenty Eleven theme, you can only change the color of the header text and website background, but as we'll see, this can potentially be used for much more.
    *   **Header image**.  Choose from one of the default images or remove the header image altogether.
    *   **Background image**.  Upload an image to use as the background of the website. The image below is what happens when I upload an image of some hang gliders to my website. The image can be tiled but unfortunately doesn't stretch.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/79af426f-7c31-4673-9664-a38da15b2080/theme-customiser-twentyeleven-background-image.png"><img title="You can set your background image to tile, but not stretch." src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b57b15ad-fd14-4092-9e33-0895f667bd38/theme-customiser-twentyeleven-background-image.png" alt="You can set your background image to tile, but not stretch." width="500" height="313" /></a><br>
<em>You can set your background image to tile, but not stretch. <a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/79af426f-7c31-4673-9664-a38da15b2080/theme-customiser-twentyeleven-background-image.png">Larger view</a>.</em>

*   *   **Navigation**.  Select which menu you want to use for the primary navigation of your website.
    *   **Static Front Page**.  Specify whether the front page of the website should be a listing of your latest posts, or a static page of your choosing.

1.  Once you've made the changes you want, you must click the “Save & Publish” button. Until this is clicked, none of the changes are reflected in the live website. This means you can play to your heart's content without your visitors seeing your experiments.

Another really exciting way to use the customizer is when <strong>previewing themes</strong>. If a theme has the Customizer built in, you can use it to make tweaks before downloading and activating the theme.

This demonstrates the Customizer in action with the Twenty Eleven theme, but what about your own themes? How would you harness this to add more functionality in themes you are selling or developing for clients?

## How The Theme Customizer Is Coded

The underlying code is actually pretty simple. It consists of two main hooks plus some actions which we'll look at shortly. To understand how the Customizer is coded and how it can be customized, there are two important things you need to know:

*   The Customizer **doesn't save any changes** in the actual theme files, either the template files or the stylesheet. When the website is rendered in a browser, WordPress outputs inline CSS generated by the Theme Customizer to the `<head>`, which overrides the stylesheet. This means users can easily revert to the standard theme and nothing is lost, but it also means that any changes made using the Customizer aren't as long-lasting as if you used a child theme, for example.
*   The Customizer **uses a set of new functions** which you add to the `functions.php` file. The main functions are:
    *   **`$wp_customize`** An object which is passed to a function you specify in your `functions.php` file, which effectively activates the Theme Customizer in your theme.
    *   **`customize_register`** The hook that lets you define all aspects of your Theme Customizer: its sections, settings and controls.
    *   **`wp_head`** The hook that outputs CSS based on the options selected by the user, so that changes show up on the live website.

Detailed guidance is available on the <a href="https://codex.wordpress.org/Theme_Customization_API">Theme Customization API</a> page in the WordPress codex.

So let's take a look at how to implement Customizer in your theme, and how to add your own customization options.</p>

## How To Add Customizer To Your Theme

### 1. Activating the Theme Customizer

The first stage is to add the Theme Customizer to your theme. I'm going to start with <a href="https://wordpress.org/extend/themes/ari">Ari</a>, a free theme available in the plugin repository that doesn't have the Theme Customizer included by default. I'm going to add Customizer so we can make some changes:

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fe03fd2c-b02e-4668-8f19-9df552a9b533/ari-before-bigger.png"><img title="The Ari theme on my website - white background, green header text, black body text." src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b19c7325-0b55-4ec1-a73a-4b0f09ce9ff2/ari-before.png" alt="The Ari theme on my website - white background, green header text, black body text." width="500" height="455" /></a><br>
<em>This is how it looks when I activate the Ari theme on my website. <a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fe03fd2c-b02e-4668-8f19-9df552a9b533/ari-before-bigger.png">Larger view</a>.</em>

The first step is to add the Theme Customizer with the following code in <code>functions.php</code>:

<pre><code class="language-php">function Ari_customize_register( $wp_customize ) {
  //All our sections, settings, and controls will be added here
}
add_action( 'customize_register', 'Ari_customize_register' );</code></pre>

All code to specify how the Theme Customizer will work goes inside the function. You can give the function whatever name you want, but you will have to use that name throughout your code.

When I click the “Customize” link on the “Themes” page, I see the default Theme Customizer:

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a50be28b-8a79-4502-af07-144e8fc37e0e/ari-customiser-before-bigger.png"><img title="The Theme Customizer shows default options when you first add it to your website." src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/79ffe9da-77ef-4563-a0fc-2643f83784a3/ari-customiser-before.png" alt="The Theme Customizer shows default options when you first add it to your website." width="500" height="251" /></a><br>
<em>The Theme Customizer shows default options when you first add it to your website. <a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a50be28b-8a79-4502-af07-144e8fc37e0e/ari-customiser-before-bigger.png">Larger view</a>.</em>

Now I have the Customizer set up, and I'm ready to add some controls.</p>

### 2. Letting Users Modify the Theme Colors

I'll start by adding a a section for colors, with controls for the user to change specific colors in the theme. I'll add this inside the function I've already added, with the following code:

<pre><code class="language-php">$colors = array();
$colors[] = array(
  'slug'=&gt;'content_text_color',
  'default' =&gt; '#333',
  'label' =&gt; __('Content Text Color', 'Ari')
);
$colors[] = array(
  'slug'=&gt;'content_link_color',
  'default' =&gt; '#88C34B',
  'label' =&gt; __('Content Link Color', 'Ari')
);
foreach( $colors as $color ) {
  // SETTINGS
  $wp_customize-&gt;add_setting(
    $color['slug'], array(
      'default' =&gt; $color['default'],
      'type' =&gt; 'option',
      'capability' =&gt;
      'edit_theme_options'
    )
  );
  // CONTROLS
  $wp_customize-&gt;add_control(
    new WP_Customize_Color_Control(
      $wp_customize,
      $color['slug'],
      array('label' =&gt; $color['label'],
      'section' =&gt; 'colors',
      'settings' =&gt; $color['slug'])
    )
  );
}</code></pre>

<strong>What does this code do?</strong>

1.  First, it defines the options which the user can change: the color of content text and the color of content link text. For each of these, it defines a default which corresponds to the CSS in the theme's stylesheet. Doing it this way saves defining the settings for each color option.
2.  It then adds the settings which will enable any changes the user makes in the Theme Customizer to be implemented in the theme. Without this, the new section and controls won't appear in the Customizer.
3.  Finally, it specifies the control which this setting will customize — `new WP_Customize_Color_Control`, which activates the color picker that is part of WordPress 3.4 and upwards.

Note that I haven't had to specify a section as the “Colors” section is automatically created by default when controls are set up that go in it.

After saving <code>functions.php</code>, this is how the Theme Customizer looks:

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2088ffec-95d7-4a72-b7a4-bc1f5c6b2823/theme-customiser-colours-before-v2.png"><img class="107950 alignnone" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0fe7fb4e-4661-4135-bd76-6d310d951035/theme-customiser-colours-beforev2.png" alt="The “Colors” section is now available in the Theme Customizer." width="500" height="317" /></a><br>
<em>The “Colors” section is now available in the Theme Customizer. <a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2088ffec-95d7-4a72-b7a4-bc1f5c6b2823/theme-customiser-colours-before-v2.png">Larger view</a>.</em>

As you can see, this isn't working correctly. I've tweaked the link color but it isn't showing up in the preview. The reason for this is simple: I haven't set up the connection between our settings and the CSS classes in the theme yet.

I'll add the relevant code in the <code>&lt;head&gt;</code> section in <code>header.php</code>, just before the closing tag:

<pre><code class="language-markup tmp-html">&lt;?php
  $content_text_color = get_option('content_text_color');
  $content_link_color = get_option('content_link_color');
?&gt;
&lt;style&gt;
  #content { color:  &lt;?php echo $content_text_color; ?&gt;; }
  #content a { color:  &lt;?php echo $content_link_color; ?&gt;; }
&lt;/style&gt;</code></pre>

This defines two variables, one for each option I've defined, and then assigns those variables to the relevant CSS selectors. In this case, I've just added a setting for all links, but by changing the CSS selectors, you could use this setting for page and post titles, links in different states, website header links and much more.</p>

### 3. Using the Theme Customizer to Add Content

In its default state, the Theme Customizer lets the user amend the website title and tagline. But <strong>what if we could use it to amend other content</strong>, such as a telephone number displayed in the header? That's entirely possible, using a similar approach.

I start by adding the relevant options, settings and controls to my function, plus the code to create a custom control not provided by default: a text box:

<pre><code class="language-php">&lt;?php
class Ari_Customize_Textarea_Control extends WP_Customize_Control {
  public $type = 'textarea';
  public function render_content() {
?&gt;

  &lt;label&gt;
    &lt;span class="customize-control-title"&gt;&lt;?php echo esc_html( $this-&gt;label ); ?&gt;&lt;/span&gt;
    &lt;textarea rows="5" style="width:100%;" &lt;?php $this-&gt;link(); ?&gt;&gt;&lt;?php echo esc_textarea( $this-&gt;value() ); ?&gt;&lt;/textarea&gt;
  &lt;/label&gt;

&lt;?php
  }
}
$wp_customize-&gt;add_setting('textarea_setting', array('default' =&gt; 'default text',));
$wp_customize-&gt;add_control(new Ari_Customize_Textarea_Control($wp_customize, 'textarea_setting', array(
  'label' =&gt; 'Telephone number',
  'section' =&gt; 'content',
  'settings' =&gt; 'textarea_setting',
)));
$wp_customize-&gt;add_section('content' , array(
  'title' =&gt; __('Content','Ari'),
));</code></pre>

This code does a few things:

*   It sets a new class of `Ari_Customize_Textarea_Control`, which extends the built-in `WP_Customize_control` class enabling us to use our custom control.
*   It defines how the new control will display as a text area.
*   It adds a setting of default to define the content to be customized.
*   It defines the the setting, label, section and content of the custom control.
*   Finally, it sets up a section for our content.

<strong>Having done this, the “Content” section appears in our Theme Customizer</strong>:

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/13b83e70-84bf-4e36-a6e0-0e2a894f39d0/theme-customiser-textarea.png"><img title="The “Content” section is now available in the Theme Customizer." src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cc58b204-9d2f-4feb-97fb-c44d402e199d/theme-customiser-textarea.png" alt="The “Content” section is now available in the Theme Customizer." width="500" height="245" /></a><br>
<em>The “Content” section is now available in the Theme Customizer. <a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/13b83e70-84bf-4e36-a6e0-0e2a894f39d0/theme-customiser-textarea.png">Larger view</a>.</em>

As in the previous example, this doesn't compete the process — I still need to ensure that any content added here is output to the website in the correct location. I add the following code in the relevant place in my <code>header.php</code> file:

<pre><code class="language-php">&lt;?php echo get_theme_mod( 'textarea_setting', 'default_value' ); ?&gt;</code></pre>

Which adds the phone number to the website:

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1146fcbb-3571-4143-a514-b79c8289fae7/phone-number-displayed-2.png"><img title="The phone number now appears, directly below the tagline." src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d4f07a23-f702-4e57-9fb6-c7a73def4993/phone-number-displayed.png" alt="The phone number now appears, directly below the tagline." width="500" height="174" /></a><br>
<em>The phone number now appears, directly below the tagline. <a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1146fcbb-3571-4143-a514-b79c8289fae7/phone-number-displayed-2.png">Larger view</a>.</em>

So far I've added content and altered the colors. Another feature which users might like is the ability to alter the layout.</p>

### 4. Adding Options to Alter the Layout

For this example, we'll let users choose whether they want the sidebar on the left or right side of the page. This will also change the CSS, but the Customizer will display a different control from the previous examples: radio buttons. I'll set up a layout section and add two radio buttons for the user to specify left or right.

<pre><code class="language-php">$wp_customize-&gt;add_setting('sidebar_position', array());
$wp_customize-&gt;add_control('sidebar_position', array(
  'label'      =&gt; __('Sidebar position', 'Ari'),
  'section'    =&gt; 'layout',
  'settings'   =&gt; 'sidebar_position',
  'type'       =&gt; 'radio',
  'choices'    =&gt; array(
    'left'   =&gt; 'left',
    'right'  =&gt; 'right',
  ),
));
$wp_customize-&gt;add_section('layout' , array(
    'title' =&gt; __('Layout','Ari'),
));</code></pre>

This code adds the following:

1.  A setting for the sidebar position radio buttons, followed by a radio button control for that setting.
2.  A section in the Customizer for this to go in.

The next step is to add the output of these settings to our <code>&lt;head&gt;</code> section in order to amend the CSS:

<pre><code class="language-php">&lt;?php
$sidebar_position = get_theme_mod('sidebar_position');
?&gt;
&lt;style&gt;
  #sidebar-primary {float:  &lt;?php echo $sidebar_position; ?&gt;;}
&lt;/style&gt;</code></pre>

ote that here I used <code>get_theme_mod</code> instead of <code>get_option</code>, which I used in the previous example. This is because existing or default WordPress settings are called via <code>get_option()</code>, while added settings are called via <code>get_theme_mod</code>.

This is the effect it has in the Theme Customizer (with some tweaks to the existing theme CSS so the floats work). First, with the sidebar to the left:

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/97a8d66b-225a-4cf9-9437-22e2c502a633/theme-customiser-layout-left-2.png"><img title="The Theme Customizer with our sidebar at the left" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fc23bbcd-d276-4105-8433-4a547a7769e6/theme-customiser-layout-left.png" alt="The Theme Customizer with our sidebar at the left." width="500" height="244" /></a><br>
<em><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/97a8d66b-225a-4cf9-9437-22e2c502a633/theme-customiser-layout-left-2.png">Larger view</a>.</em>

And then with the sidebar on the right:

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cdf8c5fa-4bbd-4b9f-a211-8f66cbd8afe8/theme-customiser-layout-right-2.png"><img title="The Theme Customizer with our sidebar at the right" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/86aa96ae-28ed-4756-a11d-d60d934a33f3/theme-customiser-layout-right.png" alt="The Theme Customizer with our sidebar at the right." width="500" height="199" /></a><br>
<em><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cdf8c5fa-4bbd-4b9f-a211-8f66cbd8afe8/theme-customiser-layout-right-2.png">Larger view</a>.</em>

This is a fairly straightforward solution, using the values of the settings in the CSS itself. Another approach would be to use conditional functions to check those values and output custom CSS.</p>

## Summary

The Theme Customizer is still very new, so its potential hasn't been fully explored yet. It'll be worth keeping an eye on new WordPress themes as they come out to <strong>see what other developers are doing with the Theme Customizer</strong>. This is a capability that developers and vendors of popular themes and theme frameworks are likely to take on board, as it will help non-coders create a website with a customized look and feel. Whether professional WordPress developers will be happy about that is another matter!

I've explored a few options here but <strong>there are more possibilities</strong>:

*   Add an upload control so that website owners can upload their logo or mugshot,
*   Add checkboxes to specify whether content is displayed or CSS is switched on,
*   Take the layout options further by allowing the user to specify whether the website will make use of media queries,
*   Add more custom colors so website owners can fully customize their website's look,
*   Add radio buttons to select custom fonts.

And the list goes on! Please use the comments section below to post examples of how you're using the Theme Customizer or how you've seen it in action.

{{< signature "cp" >}}

