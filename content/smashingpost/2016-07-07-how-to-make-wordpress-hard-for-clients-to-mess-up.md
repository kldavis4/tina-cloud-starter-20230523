---
title: How To Make WordPress Hard For Clients To Mess Up
slug: how-to-make-wordpress-hard-for-clients-to-mess-up
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/68ff0ff1-5dfe-4ee3-ba26-1f8f6a9ee4cd/05-posts-menu-preview-opt.png
date: 2016-07-07T16:20:36.000Z
author: emersonloustau
description: >-
  WordPress is a wonderfully powerful CMS that ships with many versatile
  features giving it **the flexibility to work out of the box** for a wide range
  of users. However, if you are a professional building custom themes and
  plugins, sometimes these features can be problematic.

  The same features and options that allow off-the-shelf themes to adapt to many
  different use cases can sometimes also be used to undermine a carefully
  designed custom theme built for a specific use case.
categories:
  - WordPress
  - Techniques (WP)
---
WordPress is a wonderfully powerful CMS that ships with many versatile features giving it <strong>the flexibility to work out of the box</strong> for a wide range of users. However, if you are a professional building custom themes and plugins, sometimes these features can be problematic. The same features and options that allow off-the-shelf themes to adapt to many different use cases can sometimes also be used to undermine a carefully designed custom theme built for a specific use case.

The following article comprises a collection of code snippets that I use again and again on almost every WordPress project. What they all have in common is that they limit functionality that is either unnecessary, confusing, or unsafe. Everything that follows can be used on any site, but these tips are especially applicable for professionals making custom themes and plugins for clients.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [How To Create And Customize A WordPress Child Theme](https://www.smashingmagazine.com/2016/01/create-customize-wordpress-child-theme/)
*   [Writing Effective Documentation For WordPress End Users](https://www.smashingmagazine.com/2012/07/writing-effective-wordpress-documentation/)
*   [Limiting The Visibility Of Posts In WordPress Via Usernames](https://www.smashingmagazine.com/2012/01/limiting-visibility-posts-username/)
*   [Utilizing User Roles In WordPress](https://www.smashingmagazine.com/2012/10/utilizing-user-roles-wordpress/)

The notable distinction is that custom themes can be built to serve a specific purpose. So the blanks for the authors' content can and <em>should</em> also be much narrower. A well-designed WordPress theme should make as many design decisions as possible so the author doesn't have to.

{{% feature-panel %}}

## Disable The Plugins And Theme Editor

There is no good reason why anyone should be live-editing your custom theme or plugin files via the WordPress dashboard. Professionals don't work that way, and <a href="https://en.wikipedia.org/wiki/Muggle">muggles</a> typically don't realize just how easy it is to break a site by skipping a single semicolon. It is also a security vulnerability hackers can exploit. Fortunately, our friends at WordPress.org made it really easy to disable this feature. Simply add the following snippet to the <i>wp-config.php</i> file.</p>

<pre><code class="language-php">define( 'DISALLOW_FILE_EDIT', true );</code></pre>

In addition to the theme editor, this will also disable the plugin editor. I consider this a feature not a bug.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b228e279-0ff3-455f-8674-9e1b75315027/01-plugin-editor-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d593153e-46d8-40f0-bd02-bf56043c178e/01-plugin-editor-preview-opt.png" alt="Wordpress plugins editor" /></a><figcaption>Wordpress plugins editor. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b228e279-0ff3-455f-8674-9e1b75315027/01-plugin-editor-opt.png">View large version</a>)</figcaption></figure>

## Limit The Visual And Text Editor

By default, the WordPress WYSIWYG editor supports far too many formatting options for a well-designed custom theme. Letting clients override text colors or font sizes is a fast way to make even the most chic site look cheap and ugly. If blog post text is designed to always be left-aligned, why give the author a button to right-align it? Do you think it will look good if the text on the About page is purple, bold, and italicized? Then don’t arm your client with the means to do it. In most situations I recommend disabling the visual editor entirely.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ba64dd2d-42a1-487b-8d87-57c90678e819/02-creative-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a5f8d0f6-6b92-4f6e-8557-dcee0d0287df/02-creative-preview-opt.png" alt="Ugly typography page" /></a><figcaption>Ugly typography page. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ba64dd2d-42a1-487b-8d87-57c90678e819/02-creative-opt.png">View large version</a>)</figcaption></figure>

### Disabling The Visual Editor

Add the following snippet to your theme's <i>functions.php</i> file and the tab to toggle the WYSIWYG editor will disappear.</p>

<pre><code class="language-php">function emersonthis_disable_visual_editor(){
    # add logic here if you want to permit it selectively
    return false;
}
add_filter('user_can_richedit' , 'emersonthis_disable_visual_editor', 50);</code></pre>

This is a good start, but you'll notice that the bold and italic buttons are still present on the plain text editor. In my experience, clients abuse these buttons much less often when the instant gratification of the WYSIWYG editor is gone. But I still prefer to remove them if they are not necessary.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/21daa08a-c7dc-440a-b580-a074aac46f8e/03-visual-editor-tab-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b3d9457b-1ebd-4d6c-88dd-f03e3c33649d/03-visual-editor-tab-preview-opt.png" alt="The visual editor tab" /></a><figcaption>The visual editor tab. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/21daa08a-c7dc-440a-b580-a074aac46f8e/03-visual-editor-tab-opt.png">View large version</a>)</figcaption></figure>

### Removing Bold And Italic Quicktags From The Text Editor

The text editor has quicktag buttons that will wrap selected text with <code>&lt;strong&gt;</code> and <code>&lt;em&gt;</code> tags. Add the following code in your theme's <i>functions.php</i> file and authors will no longer have bold or italics buttons.</p>

<pre><code class="language-php"># Removes bold and italic quicktags from text editor
function emersothis_quicktags_settings( $qtInit  ) {
    //To disable ALL butons it must be set to "," (not "")
    $qtInit['buttons'] = 'more,';
    return $qtInit;
}
add_filter('quicktags_settings', 'emersonthis_quicktags_settings');</code></pre>

This removes the possibility that your client will decide to, say, italicize an entire article. But this does not remove the ability to write markup into the text editor by hand. Every now and then that can come in handy when you're in a pinch.

If you are in a rare situation where the user should be formatting text themselves, you can leave the visual editor enabled but disable specific buttons individually.</p>

### Disabling Buttons On The Visual Editor

One of the few times I leave the visual editor enabled is when authors are writing long posts or pages that have internal structure of their own. For example, an author of a 10-page article might need the ability to add subheadings. In these situations I set up custom classes for the subsections and then disable all the other formatting buttons that are not needed.

The WordPress API for modifying the <a href="https://www.tinymce.com/">TinyMCE</a> editor is a bit tricky because you need to look up the code names used to refer to each button you want to remove. You get the most bang for your buck by removing the “kitchen sink” button which toggles the entire second row that contains the most problematic formatting buttons. Adding the following code to your theme's <i>functions.php</i> file will do this.</p>

<pre><code class="language-php"># Remove visual editor buttons
function emersonthis_tinymce_buttons($buttons)
{
    # Remove the text color selector
    $remove = array('wp_adv'); //Add other button names to this array
    # Find the array key and then unset
    return array_diff($buttons,$remove);
}
add_filter(
    'mce_buttons',
    'emersonthis_tinymce_buttons'
);</code></pre>

One trick to figuring out the code name of the button you want to remove is by inspecting the markup of the form. At the time of writing, each button has a class name that begins with <code>mce-i-</code> followed by the code name you would put in the array above.</p>

## Remove The "Add Media" Button

The “Add media” button appears by default whenever a custom post type supports the editor feature. But custom post types can be used for a wide range of things, and often it is inappropriate for that field to include images.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d4126364-5869-4110-9d8e-40408cc26e0d/04-ugly-photos-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8ddcdafb-717a-4d0c-87f2-c30b04c85bb2/04-ugly-photos-preview-opt.png" alt="Blog post filled with ugly images" /></a><figcaption>Blog post filled with ugly images. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d4126364-5869-4110-9d8e-40408cc26e0d/04-ugly-photos-opt.png">View large version</a>)</figcaption></figure>

Most of the time, when I expect the author to publish an image to accompany text, I use post thumbnails (aka featured images). This makes it easy to integrate the images into theme templates, and it also gives the developer more control over the size and specifications for the images.

Ad hoc photos embedded using the “Add media” button in the editor are hard to control and they have a tendency to look awkward depending on where the author inserts the image in relation to the surrounding text. They also cause confusion for many authors, because at a glance the “Add media” button is easily confused with the “Featured image” upload button that appears further down the page (by default), and may be used very differently by the theme. I almost always remove it, by adding the following code to the theme's <i>functions.php</i> file.</p>

<pre><code class="language-php"># Remove media buttons
function emersonthis_remove_add_media(){
    # do this conditionally if you want to be more selective
    remove_action( 'media_buttons', 'media_buttons' );
}
add_action('admin_head', 'emersonthis_remove_add_media');</code></pre>

You can add logic before the <code>remove_action()</code> to remove only the media button conditionally for certain post types. For example, you might want to let authors add images to pages, but not blog posts which instead use thumbnails.

## Disable Theme Customizer Options

If you are working on a child theme, the parent theme may offer customization options that are inappropriate for the child. The customization options may be unused in your child theme, or have the potential to break things. Either way, the <a href="https://codex.WordPress.org/Class_Reference/WP_Customize_Manager/remove_section">WordPress theme customizer API</a> makes it easy to get rid of them by adding the following snippet to your theme's <i>functions.php</i> file.</p>

<pre><code class="language-php"># Remove customizer options.
function emersonthis_remove_customizer_options( $wp_customize ) {
    // $wp_customize-&gt;remove_section( 'static_front_page' );
    // $wp_customize-&gt;remove_section( 'title_tagline' );
    $wp_customize-&gt;remove_section( 'colors' );
    $wp_customize-&gt;remove_section( 'header_image' );
    $wp_customize-&gt;remove_section( 'background_image' );
    // $wp_customize-&gt;remove_section( 'nav' );
    // $wp_customize-&gt;remove_section( 'themes' );
    // $wp_customize-&gt;remove_section( 'featured_content' );
    // $wp_customize-&gt;remove_panel( 'widgets' );
}
add_action( 'customize_register',
            'emersonthis_remove_customizer_options',
            30);</code></pre>

Each line in the snippet above corresponds to an individual theme customization option that you can disable by uncommenting it.</p>

## Hide Unused Dashboard Menu Items

Not every site has the same types of content; some sites have no blog, for example. If we apply the same logic to the WordPress dashboard that we apply to any other user interface, it is confusing and unnecessary to show buttons that do not do anything. In this example, the Posts menu item would be unnecessary, so let’s remove it by adding the following snippet to <i>functions.php</i>:

<pre><code class="language-php">function emersonthis_custom_menu_page_removing() {
  // remove_menu_page( 'index.php' );                  //Dashboard
  // remove_menu_page( 'jetpack' );                    //Jetpack* 
  remove_menu_page( 'edit.php' );                   //Posts
  remove_menu_page( 'upload.php' );                 //Media
  // remove_menu_page( 'edit.php?post_type=page' );    //Pages
  remove_menu_page( 'edit-comments.php' );          //Comments
  // remove_menu_page( 'themes.php' );                 //Appearance
  // remove_menu_page( 'plugins.php' );                //Plugins
  // remove_menu_page( 'users.php' );                  //Users
  // remove_menu_page( 'tools.php' );                  //Tools
  // remove_menu_page( 'options-general.php' );        //Settings
}
add_action( 'admin_menu', 'emersonthis_custom_menu_page_removing' );</code></pre>

Each line corresponds to a specific menu in the dashboard. The file names do not always match the name that appears in the dashboard menu, so the commented lines are left in as a quick reference.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/34012278-94a7-46a9-9305-06d3f6756f36/05-posts-menu-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/68ff0ff1-5dfe-4ee3-ba26-1f8f6a9ee4cd/05-posts-menu-preview-opt.png" alt="The Posts menu appears by default whether or not the site has a blog" /></a><figcaption>The Posts menu item appears by default whether or not the site has a blog. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/34012278-94a7-46a9-9305-06d3f6756f36/05-posts-menu-opt.png">View large version</a>)</figcaption></figure>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/01d8489b-844b-40a5-a81e-79c9c652b349/06-posts-menu-hidden-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/24bf0822-e5f4-4c64-a9d1-54ce9e406a92/06-posts-menu-hidden-preview-opt.png" alt="06-posts-menu-hidden-preview-opt" /></a><figcaption>The WordPress dashboard without the Posts menu item. (<a href="//www.smashingmagazine.com/wp-content/uploads/2016/05/06-posts-menu-hidden-opt.png">View large version</a>)</figcaption></figure>

It is important to understand that removing these menu items does not actually revoke the user's permissions. A user could still access the hidden menu item directly using the URL. If the goal is to make the dashboard less cluttered by hiding superfluous controls, then this is probably fine. If the goal is to actually <em>prevent</em> a user from accessing those controls, then you will need to modify <a href="https://codex.wordpress.org/Roles_and_Capabilities">the capabilities of the user's role</a>. To accomplish this, add a snippet like the following to the activation hook of a plugin (it only needs to run once):

<pre><code class="language-php">global $wp_roles; // global class
$role = 'author';
$cap = 'delete_published_posts';
$wp_roles-&gt;remove_cap( $role, $cap );</code></pre>

Use this comprehensive <a href="https://codex.wordpress.org/Roles_and_Capabilities#Capabilities">table of all capabilities</a> to find the specific capabilities you can add or remove for each of the default roles.</p>

## Add A Hint About How Line Breaks Work In The Editor

By default the visual editor (TinyMCE) will create a new paragraph when the author presses <kbd>Return</kbd>. If you just want an old fashioned line break (aka carriage return) you need to press <kbd>Shift+Return</kbd>. This is nifty and powerful but not intuitive for many authors. I've started adding a quick reminder to avoid the inevitable complaint about “a bunch of weird white space” showing up in a post or page.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/35d05bc6-91e2-4316-b07d-03a12d00f2f5/07-extra-white-space-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7c237d7c-c8cb-4543-8a5e-a45882f21e2a/07-extra-white-space-preview-opt.png" alt="Blog post with ugly extra white space" /></a><figcaption>Blog post with ugly extra white space. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/35d05bc6-91e2-4316-b07d-03a12d00f2f5/07-extra-white-space-opt.png">View large version</a>)</figcaption></figure>

Add the following snippet to your <i>functions.php</i> file. Change the value of <code>$tip</code> to say whatever you want to remind your authors of.</p>

<pre><code class="language-php"># Adds instruction text after the post title input
function emersonthis_edit_form_after_title() {
    $tip = '&lt;strong&gt;TIP:&lt;/strong&gt; To create a single line break use SHIFT+RETURN. By default, RETURN creates a new paragraph.';
    echo '&lt;p style="margin-bottom:0;"&gt;'.$tip.'&lt;/p&gt;';
}
add_action(
    'edit_form_after_title',
    'emersonthis_edit_form_after_title'
);
</code></pre>

This technique could be used to inject a reminder about anything you want authors to remember when adding or editing content.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/aded0518-99fd-4a8e-967d-3f027f65db2e/08-tip-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f5142a0f-171f-4144-abf5-f5099047e89e/08-tip-preview-opt.png" alt="Posts page with whitespace tip added" width="1756" height="749" /></a><figcaption>Posts page with white space tip added. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/aded0518-99fd-4a8e-967d-3f027f65db2e/08-tip-opt.png">View large version</a>)</figcaption></figure>

## Do Not Dole Out Administrator Accounts

The WordPress administrator role is very powerful and <a href="https://www.youtube.com/watch?v=b23wrRfy7SM&amp;feature=youtu.be&amp;t=11s">with great power comes great responsibility</a>. Some clients are experienced WordPress power users who administer their site competently. Many of them are not. The latter should not be poking around as administrators. Instead, make them an editor and create a separate admin account with a super strong password. If you have an ongoing affiliation with the client you can hang on to those credentials until the client is ready to administer the site themselves.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/de86a2a1-7164-4cb0-9ee6-dd4ab4f0c739/09-too-many-admins-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d6a805a9-4ff6-4d9f-b13e-b3d8f58add69/09-too-many-admins-preview-opt.png" alt="Users list full of admins" /></a><figcaption>Users list full of admins. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/de86a2a1-7164-4cb0-9ee6-dd4ab4f0c739/09-too-many-admins-opt.png">View large version</a>)</figcaption></figure>

Alternatively, give the client both sets of credentials and have them store the admin credentials somewhere safe and only use it to perform admin tasks. Many clients will promptly lose the admin credentials but that is fine: the password can always be reset, and these are often the types of clients who will rehire you to do the routine site maintenance for them anyway.

The most important reason for being stingy with admin accounts is that they are a security vulnerability. A pleasant side effect is that beginner WordPress users often find the dashboard UI less overwhelming when they log in as authors or editors because there are fewer menus to sort through while learning basic skills such as adding or editing posts.</p>

## Use mu-Plugins

The <i>mu-plugins/</i> directory has existed for a long time, but most WordPress hackers I meet have never heard of it. The “mu” stands for <em>must use</em>. The directory is an alternative location where plugins can be installed.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1fbbc83a-ddbe-4da4-afed-89bdc5d70066/10-mu-plugin-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f7c3b823-c332-435a-9f46-182fe82f6ccf/10-mu-plugin-preview-opt.png" alt="Must use plugins interface in Wordpress dashboard" /></a><figcaption>Must use plugins interface in WordPress dashboard. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1fbbc83a-ddbe-4da4-afed-89bdc5d70066/10-mu-plugin-opt.png">View large version</a>)</figcaption></figure>

The difference is that “must use” plugins are automatically active and cannot be disabled by accident throughout the dashboard. They are also loaded <em>before</em> the other plugins. This is ideal for plugins that must be present for the site to run properly. It's also a great alternative for non-presentational hacks that might normally get jammed into your custom theme's <i>functions.php</i> file. For example, I like to define custom post types in a mu-plugin, because that content should persist whether or not a particular theme is active.

The <i>mu-plugins/</i> directory does not exist out of the box. You create it manually inside <i>wp-content/</i>.</p>

<pre><code class="language-php">wp-content/
    mu-plugins/
    plugins/
    themes/
    ...</code></pre>

The biggest limitation is that WordPress only looks for files in the top level of <i>mu-plugins/</i> and will ignore code inside a subdirectory. However, you can work around this by creating a single PHP file at the top of <i>mu-plugins/</i> that loads code from a sibling subdirectory. Also keep in mind that update notifications do not apply to mu-plugins. I think of <i>mu-plugins/</i> as the place to put important code that the client should never have to think about.

Read more about <a href="https://codex.WordPress.org/Must_Use_Plugins">must use plugins</a> in the Codex. If you want to require other plugins by preventing the ability to deactivate them, you might find the <a href="https://github.com/WebDevStudios/WDS-Required-Plugins">WDS-Required-Plugins</a> library useful.</p>

## Final Note

You may find it counterintuitive to disable functionality that WordPress gives you for free. But remember that your client is not paying you to give them a lot of buttons. Your job is to make an effective, robust website that is tailored to match the client's goals. By disabling problematic or extraneous functionality you are actually delivering <em>more value</em>.

If you want more snippets, I have created a <a href="https://github.com/emersonthis/WordPress-snippets">public GitHub repository of useful WordPress snippets</a> which contains up-to-date versions of the hacks above, as well as others I add periodically. If you have your own handy snippets you want to share, pull requests are more than welcome!

{{< signature "dp, ml, og" >}}

