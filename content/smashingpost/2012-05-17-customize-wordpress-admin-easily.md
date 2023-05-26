---
title: How To Customize The WordPress Admin Easily
slug: customize-wordpress-admin-easily
image: 'https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/39bd8b27-7eee-44dd-8d09-070d040973ab/illu-wp-14.jpg'
date: 2012-05-17T13:55:39.000Z
author: aurelien-denis
description: >-
  In this article, we take a break from some of the more advanced ways to customize WordPress, and share some super-easy customization techniques for the WordPress Admin area.\n\nIf you're just getting started with WordPress, or have been running with default functionality for a while and now want to dig in with some useful and easy ways to customize your WordPress site, a great place to start is the WordPress Admin area, or backend. One of the great things about WordPress is that each part of the backend is easily customized using simple PHP functions.
categories:
  - WordPress
  - Admin
  - Techniques (WP)
---
In this article, we take a break from some of the more advanced ways to customize WordPress, and share some super-easy customization techniques for the WordPress Admin area.

If you're just getting started with WordPress, or have been running with default functionality for a while and now want to dig in with some useful and easy ways to customize your WordPress site, a great place to start is the WordPress Admin area, or backend. One of the great things about WordPress is that each part of the backend is easily customized using simple PHP functions.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5d0fefdf-fb21-4f9f-a7e0-659707be7754/customize-wp-admin.jpg" alt="customize-wp-admin" width="500" height="331" />

In this article, you'll learn how to customize the login page with your own logo, add new widgets to the dashboard, add custom content to the admin footer, make it easier to get in and out of the Admin area, and more. When combined, these techniques can improve branding, accessibility, and usability of your WordPress-powered site.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Modifying Admin Post Lists In WordPress](https://www.smashingmagazine.com/2013/12/modifying-admin-post-lists-in-wordpress/)
*   [Useful Free Admin Plugins For WordPress](https://www.smashingmagazine.com/2012/03/useful-free-admin-plugins-wordpress/)
*   [Ten Things Every WordPress Plugin Developer Should Know](https://www.smashingmagazine.com/2011/03/ten-things-every-wordpress-plugin-developer-should-know/)
*   [Inside The WordPress Toolbar](https://www.smashingmagazine.com/2012/03/inside-the-wordpress-toolbar/)

{{% feature-panel %}}

### Changing the Default WordPress Login URL

By default, logging in to the WordPress Admin area requires either <code>/wp-admin</code> or <code>/wp-login.php</code> in the URL, which isn't a lot to type. You can, however, make it even easier by changing the login URL to something more memorable and better branded.

This technique requires <code>.htaccess</code> file manipulation. Usually, this is a file hidden in the root of your WordPress installation. It's automatically created by WordPress after setting custom permalinks using URL rewriting.

First, check your SFTP/FTP client preferences to show hidden files—most FTP clients manage that. Then, check that the file <code>.htaccess</code> exists. If that is not the case, create it by using your favorite notepad. On Windows, use the Notepad++ software to create it. Open it and add this line on top:

<pre><code class="language-markup tmp-xml">RewriteRule ^login$ https://YOUR_SITE.com/wp-login.php [NC,L]</code></pre>

Just replace the <strong>login</strong> keyword with one of your choice and your website's URL.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/135633ce-8a90-4341-953e-28e646f61964/htaccess-rewrite-login-url.jpg"><img loading="lazy" decoding="async" class="105665" title="htaccess-rewrite-login-url" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/135633ce-8a90-4341-953e-28e646f61964/htaccess-rewrite-login-url.jpg" alt="" width="514" height="206" /></a>

Now, open your favorite browser and go to https://yoursite.com/login. You'll be redirected to the WordPress login page. Remember that your clients are not supposed to know everything about WordPress usages—a user-friendly URL is far better to remember than <code>/wp-login.php.</code>

Easy to remember, easy to teach, easy to learn!

### Changing the Default External Link of the WordPress Login Page

When you log into WordPress, the default logo links to <em>WordPress.org</em>. Let me show you a quick tip for using your own link. Open the <strong>functions.php</strong> file. Then, add the following lines of code. And be sure to remember the PHP tag enclosure.

<pre><code class="language-php">// Use your own external URL logo link
function wpc_url_login(){
	return "https://wpchannel.com/"; // your URL here
}
add_filter('login_headerurl', 'wpc_url_login');</code></pre>

Don't forget to save the file. Log out to view the result. Better, no?

### Customizing the Login logo Without a Plugin

Reinforce your brand by changing the default WordPress login logo. The logo is one of the most important elements of your brand! People will memorize it to find you quickly. Showcase it!

This is the default WordPress login screen:

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2c118daf-5ade-49e7-a18b-82173cc51356/wordpress-default-login-screen.jpg"><img loading="lazy" decoding="async" class="105662" title="wordpress-default-login-screen" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2c118daf-5ade-49e7-a18b-82173cc51356/wordpress-default-login-screen.jpg" alt="" width="359" height="403" /></a>

To enhance it, add these lines of code in your <strong>functions.php</strong>:

<pre><code class="language-php">// Custom WordPress Login Logo
function login_css() {
	wp_enqueue_style( 'login_css', get_template_directory_uri() . '/css/login.css' );
}
add_action('login_head', 'login_css');</code></pre>

The third line points towards a separate stylesheet. Even though it's possible to use that of your default CSS theme, I advise you to use <a href="https://getfirebug.com/">Firebug</a>—a useful Firefox add-on—or any other Web development tool that allows you to edit your website in real-time. As you can see, just one line of code is needed to change the default logo.

<pre><code class="language-css">#login h1 a {
	background-image: url("https://YOUR-WEBSITE.com/wp-content/themes/YOUR_THEME/images/custom_logo.png") !important;
	}</code></pre>

Feel free to change the logo URL if it's not located in your theme folder. Now have a look at your login page: your custom logo appears!

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2ac9008b-9fd3-4634-9248-8c1ada0a427c/login-custom-logo-wordpress.jpg"><img loading="lazy" decoding="async" class="105663" title="login-custom-logo-wordpress" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2ac9008b-9fd3-4634-9248-8c1ada0a427c/login-custom-logo-wordpress.jpg" alt="" width="333" height="373" /></a>

If that is not the case, make sure that no white lines are present at the end of your <code>functions.php</code> file.</p>

### Changing the Footer of Your WordPress Administration

The default WordPress administration footer thanks you for using their content management system and links to <em>WordPress.org</em>. For professional use and website branding, you'll want to customize this area.

Open the <strong>Appearance</strong> menu and click on <strong>Editor</strong>. Click on <strong>functions.php</strong> on the right side of your screen. You can also access the footer by using an FTP client to locate <code>/wp-content/themes/NAME_OF_YOUR_THEME/functions.php</code>.

Now, add the following lines of code, taking care to place them between PHP tags:

<pre><code class="language-php">// Custom WordPress Footer
function remove_footer_admin () {
	echo '&amp;copy; 2012 - WordPress Channel, Aur&amp;eacute;lien Denis';
}
add_filter('admin_footer_text', 'remove_footer_admin');</code></pre>

To customize the content, just change the second line inside the <code>echo</code>, between the quotes.

Finally, refresh your browser to see the result.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8eabbab0-0d91-44e7-9eb0-abcfa05cd5e1/custom-footer-admin-wordpress.jpg"><img loading="lazy" decoding="async" class="105664" title="custom-footer-admin-wordpress" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8eabbab0-0d91-44e7-9eb0-abcfa05cd5e1/custom-footer-admin-wordpress.jpg" alt="" width="243" height="63" /></a>

### Adding Custom Widgets to Your Dashboard

It can be useful to add your own widget to provide general or commercial information. Adding a widget to the WordPress dashboard can be done very quickly. Again, open the <strong>functions.php</strong> file, then, add the following lines of code:

<pre><code class="language-php">// Add a widget in WordPress Dashboard
function wpc_dashboard_widget_function() {
	// Entering the text between the quotes
	echo "&lt;ul&gt;
	&lt;li&gt;Release Date: March 2012&lt;/li&gt;
	&lt;li&gt;Author: Aurelien Denis.&lt;/li&gt;
	&lt;li&gt;Hosting provider: my own server&lt;/li&gt;
	&lt;/ul&gt;";
}
function wpc_add_dashboard_widgets() {
	wp_add_dashboard_widget('wp_dashboard_widget', 'Technical information', 'wpc_dashboard_widget_function');
}
add_action('wp_dashboard_setup', 'wpc_add_dashboard_widgets' );</code></pre>

In this example, add the desired text between the <code>echo</code> tag, after the quotes. You could also insert HTML; an unordered list for example. Name your widget—this will be the widget title—by replacing "Technical informations" with your title of choice. This is what it will look like.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/61c776c5-ede4-4f34-b656-1136b827a8b2/widget-dashboard.jpg"><img loading="lazy" decoding="async" class="105666" title="widget-dashboard" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/61c776c5-ede4-4f34-b656-1136b827a8b2/widget-dashboard.jpg" alt="" width="229" height="134" /></a>

If you do not see your custom widget, click on the <strong>Options</strong> menu screen located in the top right of the window to display it.</p>

### Hiding Unwanted WordPress Dashboard Widgets

The WordPress dashboard displays multiple widgets that you can easily move by dragging and dropping. To mask them definitively, just add the following lines in the <strong>functions.php</strong> file:

<pre><code class="language-php">add_action('wp_dashboard_setup', 'wpc_dashboard_widgets');
function wpc_dashboard_widgets() {
	global $wp_meta_boxes;
	// Today widget
	unset($wp_meta_boxes['dashboard']['normal']['core']['dashboard_right_now']);
	// Last comments
	unset($wp_meta_boxes['dashboard']['normal']['core']['dashboard_recent_comments']);
	// Incoming links
	unset($wp_meta_boxes['dashboard']['normal']['core']['dashboard_incoming_links']);
	// Plugins
	unset($wp_meta_boxes['dashboard']['normal']['core']['dashboard_plugins']);
}</code></pre>

You can choose what widgets you'd like to hide. In this case, "Right Now", "Recent comments", "Incoming links" and "Plugins" have been removed from your WordPress dashboard. To learn more about this feature, have a look at the <a href="https://codex.wordpress.org/Dashboard_Widgets_API">codex</a>.</p>

### Creating Your Own Custom Admin Color Scheme

If you're not totally satisfied with the WordPress admin color scheme, this is how you can customize it. All you need to do is create a new CSS stylesheet. In this example, we'll call it <code>admin.css</code> and place it in a folder <code>entitled/css</code>. Once again, edit the <strong>functions.php</strong> file and add this snippet:

<pre><code class="language-php">// Custom WordPress Admin Color Scheme
function admin_css() {
	wp_enqueue_style( 'admin_css', get_template_directory_uri() . '/css/admin.css' );
}
add_action('admin_print_styles', 'admin_css' );</code></pre>

Your <code>admin.css</code> file must contain styles that are compatible with WordPress. Again, I recommend you use Firebug or Web Inspector to identify the right ones.</p>

### Conclusion

That's all folks! I hope you have learned a few good tips to make WordPress act more like a white label CMS. Remember that customization is not just a branding technique, but also a way to boosting your productivity, by increasing user-friendliness.

If you're not comfortable with PHP, you can make most of these changes with the <a href="https://www.videousermanuals.com/white-label-cms/">White Label CMS WordPress</a> plugin. Do you know any other great tips? Share them with us!

{{< signature "jc" >}}

