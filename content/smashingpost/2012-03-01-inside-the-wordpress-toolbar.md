---
title: Inside The WordPress Toolbar
slug: inside-the-wordpress-toolbar
image: null
date: 2012-03-01T15:57:47.000Z
author: dominic-giglio
description: >-
  The WordPress Admin Bar, first introduced in [version
  3.1](https://codex.wordpress.org/Version_3.1 "Codex: Version 3.1"), debuted to
  mixed reactions. A Google search for “[wordpress admin
  bar](https://www.google.com/#sclient=psy-ab&hl=en&site=&source=hp&q=wordpress+admin+bar&pbx=1&oq=wordpress+admin+bar&aq=f&aqi=g4&aql=&gs_sm=e&gs_upl=1000l1000l0l1615l1l1l0l0l0l0l147l147l0.1l1l0&bav=on.2,or.r_gc.r_pw.,cf.osb&fp=ceb820cf9728aefb&biw=1365&bih=978)”
  returns multiple articles about how to disable or remove it. [Version
  3.2](https://codex.wordpress.org/Version_3.2 "Codex: Version 3.2") of WordPress
  introduced new features and functionality, and [version
  3.3](https://codex.wordpress.org/Version_3.3 "Codex: Version 3.3") has not only
  further enhanced it but integrated the header of the admin section into the
  bar itself.
categories:
  - WordPress
  - PHP
  - Functions
  - Guides
---
The WordPress Admin Bar, first introduced in <a title="Codex: Version 3.1" href="https://codex.wordpress.org/Version_3.1">version 3.1</a>, debuted to mixed reactions. A Google search for “<a href="https://www.google.com/#sclient=psy-ab&amp;hl=en&amp;site=&amp;source=hp&amp;q=wordpress+admin+bar&amp;pbx=1&amp;oq=wordpress+admin+bar&amp;aq=f&amp;aqi=g4&amp;aql=&amp;gs_sm=e&amp;gs_upl=1000l1000l0l1615l1l1l0l0l0l0l147l147l0.1l1l0&amp;bav=on.2,or.r_gc.r_pw.,cf.osb&amp;fp=ceb820cf9728aefb&amp;biw=1365&amp;bih=978">wordpress admin bar</a>” returns multiple articles about how to disable or remove it. <a title="Codex: Version 3.2" href="https://codex.wordpress.org/Version_3.2">Version 3.2</a> of WordPress introduced new features and functionality, and <a title="Codex: Version 3.3" href="https://codex.wordpress.org/Version_3.3">version 3.3</a> has not only further enhanced it but integrated the header of the admin section into the bar itself. Since this feature is not going anywhere and it figures largely in WordPress’ plan to implement front-end editing, I think we would all benefit from looking at where its features come from and how best to make this sometimes controversial feature work <em>for</em> us.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9194a258-1473-4119-9235-0c47b5d90b0f/smwp-featured-image.png" alt="Inside the WordPress Toolbar" width="500" height="300" />

In addition to the explanations of how to get rid of the Admin Bar, you will also find on the Web no shortage of <a title="DigWP Admin Bar Tricks" href="https://digwp.com/2011/04/admin-bar-tricks/">techniques and tips for customization</a>, as well as a multitude of <a title="Admin Bar Plugins" href="https://wordpress.org/extend/plugins/search.php?q=admin+bar&amp;sort=">plugins</a> that make working with the Admin Bar a little more enjoyable.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [How Commercial Plugin Developers Are Using The WordPress Repository](https://www.smashingmagazine.com/2012/01/commercial-plugin-developers-wordpress-repository/)
*   [WordPress Essentials: How To Create A WordPress Plugin](https://www.smashingmagazine.com/2011/09/how-to-create-a-wordpress-plugin/)
*   <span>[Help Us Help WordPress](https://www.smashingmagazine.com/2012/08/help-us-help-wordpress/)</span>
*   [Writing Unit Tests For WordPress Plugins](https://www.smashingmagazine.com/2012/03/writing-unit-tests-for-wordpress-plugins/)

{{% feature-panel %}}

While I am a huge fan of plugins, knowing where a feature comes from is important before deciding whether to customize it. In this article, we’ll look at the history of the Admin Bar, when (and from where) the bar is enabled, the particular functions that WordPress’ core developers have given us, and how to make the Admin Bar more personal and useful.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [What’s Going On In The WordPress Economy?](https://www.smashingmagazine.com/2012/04/wordpress-economy-part-1/)
*   [Writing Effective Documentation For WordPress End Users](https://www.smashingmagazine.com/2012/07/writing-effective-wordpress-documentation/)
*   [How To Create Custom Taxonomies In WordPress](https://www.smashingmagazine.com/2012/01/create-custom-taxonomies-wordpress/)
*   [Adding Custom Fields In WordPress’ Comment Form](https://www.smashingmagazine.com/2012/05/adding-custom-fields-in-wordpress-comment-form/)

## Genesis

In the beginning, the Admin Bar didn’t do a whole lot. I suspect this was the main cause of the negative feedback. Initially, it was enabled on the front end of the website and disabled in the admin section. If you were logged in while viewing a public page, the Admin Bar provided a new conduit to the admin section. It had:

*   Links to edit your profile, view the dashboard and log out;
*   An “Add New” drop-down menu, containing links for only “Post” and “Page”;
*   A link to the admin page for comments, alongside the number of comments pending approval;
*   An “Appearance” drop-down menu, with direct links to the admin section’s widget and menu pages;
*   A link to the admin page for updates, alongside the number of pending updates;
*   An “Edit Post” link displayed when viewing an individual post.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fa405ce8-d334-4c2a-bd6b-2a28e47ce1d1/admin-bar-3-1.png"><img class="105169" title="admin_bar_3_1" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fa405ce8-d334-4c2a-bd6b-2a28e47ce1d1/admin-bar-3-1.png" alt="WordPress 3.1 Admin Bar" width="500" height="74" /></a><br>
<em>The Admin Bar in WordPress 3.1</em>

While this was a great start, some found the limited functionality to be more of an eyesore than a revolutionary enhancement to the administration of their blog. Couldn’t the venerable minds that brought us custom fields, custom post types and automatic updates do more? Yes, they could.

Version 3.2 brought a lot of great new features and fixes to WordPress blogs, and the Admin Bar was on the receiving end of some of these enhancements. Most importantly, the new version distinguished between the Admin Bar on public pages and the one in the admin section. The Admin Bar was evolving, growing more dynamic. Although still not a game-changer by any stretch, it was an improvement.

The updates included the following:

*   The “Dashboard” link was moved from the user menu to its own slot on the public-facing Admin Bar;
*   A “View Post/Page” link was added to the admin section for when you’re editing a post or page;
*   “Media,” “Link,” “User,” “Theme” and “Plugin” links were added to the “Add New” drop-down menu;
*   “Themes,” “Background” and “Header” links were added to the “Appearance” drop-down menu.

Now we’re getting somewhere! These updates were an improvement, but we were still far from a WordPress-worthy tool. It still felt out of place and didn’t look like it belonged. The shouts were heard once more: “Give me an Admin Bar that WordPress can be proud of!”

## Version 3.3 Steps Up

The server-stretching features that rolled out with the current 3.3 version are slick to say the least. Until this latest release, our poor Admin Bar, the one we were beginning to have such high hopes for, was practically lost in a forest of features. Now this update has brought the potential power of the Admin Bar into focus. No longer does the bar look like it’s hanging over the page: it’s sleek, it’s clean, it blends in. Now it looks like it’s supposed to be there. Finally, an Admin Bar we can get behind!

Foremost among the improvements: <strong>it’s not called the Admin Bar anymore!</strong> It is now the WordPress Toolbar. All of the admin section’s contact and informational links have been integrated into a drop-down menu denoted by the WordPress logo, which is more logical. The “Visit Site” link is now hidden under a drop-down menu displaying the website’s name (a nice addition for those of us who routinely use the admin sections of multiple websites). When the toolbar is displayed on a public page, the drop-down menu with the website’s name doubles as the old “Appearance” menu, linking to the most viewed pages of the admin section. Most importantly, it has been drastically simplified.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/017bc996-dc10-4db5-85bc-79d621599589/admin-bar-3-3-updates.png"><img class="105171" title="admin_bar_3_3_updates" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/017bc996-dc10-4db5-85bc-79d621599589/admin-bar-3-3-updates.png" alt="WordPress 3.3 Toolbar showing updates" width="500" height="74" /></a><br>
<em>The WordPress 3.3 Toolbar, showing updates.</em>

The comments link has been replaced by a comments bubble, which is visually more descriptive, and the “Appearance” drop-down menu has been removed from the toolbar in the admin section since the addition of the fly-out menus has made it mostly redundant. The drive towards a more dynamic toolbar continues with the updates link being displayed only when a newer version has been detected, and it, too, has been replaced by an icon. These small but powerful changes all lead to the unmistakable feeling that <strong>the toolbar looks empty</strong>. We’ll get back to that in a minute.</p>

## Going To The Source

Back in August 2011, I wrote about how <a title="WordPress Initialization" href="https://humanshell.net/wordpress/wordpress-initialization/">WordPress initializes itself when a page is requested from the server</a>. In that post, I walk through, almost line by line, where the majority of WordPress’ core functionality comes from. The file <a title="v3.3 Trac: wp-settings.php" href="https://core.trac.wordpress.org/browser/branches/3.3/wp-settings.php"><code>wp-settings.php</code></a> is responsible for loading the lion’s share of what we consider to be “WordPress,” including the toolbar. As of version 3.3, the toolbar’s code is required from an external file on line 145 of <code>wp-settings.php</code>. The name of this file is (oddly enough still) <a title="v3.3 Trac: admin-bar.php" href="https://core.trac.wordpress.org/browser/branches/3.3/wp-includes/admin-bar.php"><code>admin-bar.php</code></a>, and it lives in the <code>/wp-includes</code> directory (along with the vast majority of the rest of WordPress’ core). This file is no slouch: it clocks in at 745 lines of code and defines a good deal of the functions needed for us to be able to work with the toolbar.

When analyzing the source code for WordPress, I turn to a certain command frequently to get a quick idea of the functionality that a file does (or doesn’t) provide. If you’re running Linux or on a Mac, try this in your favorite terminal (from your WordPress root directory):

<pre><code class="language-php">
cat wp-includes/admin-bar.php | grep ^function
</code></pre>

That command should produce something similar to the following output:

<pre><code class="language-php">
function _wp_admin_bar_init() {
function wp_admin_bar_render() {
function wp_admin_bar_wp_menu( $wp_admin_bar ) {
function wp_admin_bar_my_account_item( $wp_admin_bar ) {
function wp_admin_bar_my_account_menu( $wp_admin_bar ) {
function wp_admin_bar_site_menu( $wp_admin_bar ) {
function wp_admin_bar_my_sites_menu( $wp_admin_bar ) {
function wp_admin_bar_shortlink_menu( $wp_admin_bar ) {
function wp_admin_bar_edit_menu( $wp_admin_bar ) {
function wp_admin_bar_new_content_menu( $wp_admin_bar ) {
function wp_admin_bar_comments_menu( $wp_admin_bar ) {
function wp_admin_bar_appearance_menu( $wp_admin_bar ) {
function wp_admin_bar_updates_menu( $wp_admin_bar ) {
function wp_admin_bar_search_menu( $wp_admin_bar ) {
function wp_admin_bar_add_secondary_groups( $wp_admin_bar ) {
function wp_admin_bar_header() { ?&gt;
function _admin_bar_bump_cb() { ?&gt;
function show_admin_bar( $show ) {
function is_admin_bar_showing() {
function _get_admin_bar_pref( $context = 'front', $user = 0 ) {
</code></pre>

This obviously doesn’t tell us a whole lot about what <em>exactly</em> the file does, but the core developers have named functions descriptively enough to give us an inkling of the responsibilities of the files that define them.

The output above tells us that this file contains 20 functions. But you will eventually come across a file that outputs so many functions that you couldn’t possibly count them (I’m talking to you, <a title="v3.3 Trac: functions.php" href="https://core.trac.wordpress.org/browser/branches/3.3/wp-includes/functions.php"><code>functions.php</code></a>!). To quickly count how many functions are in a file, you can append <code>wc -l</code> to the above command:
<pre class="brush: php">cat wp-includes/admin-bar.php | grep ^function | wc -l
</pre>

This returns a line count in the output of the preceding <code>grep</code> command.

Enough <a title="commandlinefu.com" href="https://www.commandlinefu.com/commands/browse">command-line fu</a>. Let’s talk about how these functions bestow the toolbar upon our website! With a quick glance, we can glean some valuable information from the names of these function. Obviously, the first one initializes the toolbar. The second is also pretty self-explanatory: it renders the toolbar. The next 14 functions add the default items to the toolbar and set its initial styling. The name <code>_admin_bar_bump_cb()</code> is not as revealing; this is a callback function that outputs to the page a style tag that creates enough margin at the top to display the toolbar. The final three are fairly easy: <code>show_admin_bar()</code> shows and hides the toolbar; <code>is_admin_bar_showing()</code> can be used in your plugin or theme’s <code>functions.php</code> file to check whether the toolbar should be displayed at all; and <code>_get_admin_bar_pref()</code> is used by <code>is_admin_bar_showing()</code>.

By far the most important function is <code>_wp_admin_bar_init()</code>. On line 39 of <code>admin-bar.php</code>, this function is added to the <code>init</code> action hook. This hook is one of the last to be executed during WordPress’ initialization. If you look at this function, you will see its true importance: it is responsible for loading the <code>WP_Admin_Bar</code> class from <code>class-wp-admin-bar.php</code>. After instantiating this class, it executes two of its methods that use most of the functions discussed above: <code>initialize()</code> and <code>add_menus()</code>. The former is responsible for creating our toolbar object in memory, while the latter attaches 11 of the functions defined in <code>admin-bar.php</code> to the action hook <code>admin_bar_menu</code>, which ensures that they are executed at the right time. These 11 functions are responsible for populating the toolbar with all of its default functionality. Basically, <code>admin-bar.php</code> defines the functions that give life to the toolbar, and <code>class-wp-admin-bar.php</code> defines the methods that enable us to interact with it once it’s alive.

## Boring!

I know, I know. Reading source code is never glamorous. But it is essential to learning about capabilities that are not apparent from other resources and tutorials. Earlier, I said that the toolbar in version 3.3 looks a little empty. And when I see empty space, I can’t help but want to fill it with cool stuff! So, let’s get our fingers dirty and start poking the toolbar to make it wake up and do some tricks. To keep these examples normalized, we’ll use the TwentyEleven theme for all of the following code. If you want to follow along at home, just pop open the <code>functions.php</code> file in TwentyEleven and hack along with me. Your mileage will vary with other themes.</p>

### Showing and Hiding

Let’s start with an easy task. We saw above that <code>admin-bar.php</code> defines the <code>show_admin_bar()</code> function. While you can disable the toolbar by unchecking a box in your user profile, let’s see how to do it in code. Add the following to the end of <code>functions.php</code>:
<pre class="brush: php">/**
* Hide the Toolbar if not in the admin section
*/
if ( ! is_admin() ) {
show_admin_bar(false);
}
</pre>

Three lines — no more toolbar! Hardly a profound example, but it’s a start. This code first checks whether we are on an admin page, and if we are <em>not</em>, then we tell WordPress to hide the toolbar.</p>

### Removing Default Items

I’m not feeling that “+ New” menu. It has an attitude, and I want to show it who’s boss. Let’s dump it.
<pre class="brush: php">/**
* Remove the "+ New" menu from the Toolbar
*/
function remove_toolbar_new_menu() {
global $wp_admin_bar;
$wp_admin_bar-&gt;remove_menu('new-content');
}
add_action('admin_bar_menu', 'remove_toolbar_new_menu', 300);
</pre>

Take that, “+ New” menu! The code is fairly straightforward, but let’s walk through it anyway. Back in <code>admin-bar.php</code>, the <code>_wp_admin_bar_init()</code> function assigns our new <code>WP_Admin_Bar</code> class to the variable <code>$wp_admin_bar</code>. So, first we have to use PHP’s <code>global</code> keyword to bring that variable into our function’s scope. After that, all we have to do is call the <code>remove_menu()</code> method and pass it the ID we want to remove.

The trick is getting this function to be called at the right time. There are a few ways to accomplish this. Remember that <code>_wp_admin_bar_init()</code> calls the <code>add_menus()</code> method after initialization. Looking at that method in <code>class-wp-admin-bar.php</code>, we see that all of the default items in the toolbar are created by adding them to the <code>admin_menu_bar</code> action hook. So, one way to do this is to have our custom function executed on the <strong>same</strong> hook <strong>after</strong> all of the defaults (which kind of makes sense since we are removing a default item). This is accomplished in the example above by passing the number 300, which is a priority argument that is passed to the <code>add_action()</code> hook, thus ensuring that our function executes after all of the defaults.

But this is a bit dirty. Messing around with the hook used to set up all of the defaults is not a good idea. For one thing, we don’t know when the priority numbers in the core will be changed. A cleaner way is to attach our custom function to a hook that is better suited to what we’re trying to do. The core developers always do a great job of providing additional hooks and filters for occasions such as this. Jumping back into <code>admin-bar.php</code>, we can see that the second function, <code>wp_admin_bar_render()</code>, wraps the call to the admin bar’s class method, <code>render()</code>, in <code>before</code> and <code>after</code> hooks. You’ll also notice that <code>wp_admin_bar_render()</code> is attached to the <code>footer</code> action hooks. This is a far more appropriate place to attach our custom function, because the priority numbers in the core are much more likely to change before these two hooks do. Let’s update our code, then, to future-proof it a bit:
<pre class="brush: php">/**
* Remove the "+ New" menu from the Toolbar
*/
function remove_toolbar_new_menu() {
global $wp_admin_bar;
$wp_admin_bar-&gt;remove_menu('new-content');
}
add_action('wp_before_admin_bar_render', 'remove_toolbar_new_menu');
</pre>

Much better. However, these two techniques are explained elsewhere on the Web. Also, I lose focus easily; if the task at hand isn’t sufficiently engaging, I run the risk of Netflix-ing an old episode of <a title="History Channel: Ancient Aliens" href="https://www.history.com/shows/ancient-aliens">Ancient Aliens</a>, at which point my project is done for. One would also expect more from an article titled “Inside the WordPress Toolbar.” So, let’s do more… a lot more.</p>

## Outta This World

At 10:49 pm EST on 6 March 2009, a Delta II rocket lifted off from Launch Complex 17-B at Cape Canaveral Air Force Station in Florida. Atop the 10,000 gallons of liquid oxygen propellant sat a little telescope that was destined to forever change how we view our little corner of the Milky Way galaxy. <a title="Kepler Mission Homepage" href="https://www.nasa.gov/mission_pages/kepler/main/index.html">Kepler</a> — named after Johannes Kepler, who defined the <a title="Wikipedia: Laws of Planetary Motion" href="https://en.wikipedia.org/wiki/Kepler%27s_laws_of_planetary_motion">laws of planetary motion</a>, which later served as the foundation of Isaac Newton’s theory of <a title="Wikipedia: Law of Universal Gravitation" href="https://en.wikipedia.org/wiki/Newton%27s_law_of_universal_gravitation">universal gravitation</a> — was engineered and constructed to study 100,000 stars in our galactic neighborhood for at least three and a half years. The mission’s goal is to find Earth-sized terrestrial extrasolar planets in the <a title="Wikipedia: Habitable Zone" href="https://en.wikipedia.org/wiki/Habitable_zone">habitable zone</a> of their host star(s).

To help our fellow WordPressers keep up on the progress of this monumental mission, as well as the ongoing efforts of other planet-hunters, we are going to build a menu for the Toolbar that displays the current number of confirmed exoplanets, as well as the number of candidates that have yet to be independently verified. We’ll use <a title="Exoplanet Archive API" href="https://exoplanetarchive.ipac.caltech.edu/docs/program_interfaces.html">an API</a> from the <a href="https://exoplanetarchive.ipac.caltech.edu/">NASA Exoplanet Archive</a> that enables us to query for both confirmed and unconfirmed exoplanet candidates in XML format. But before we get into the code, let’s outline what exactly the code needs to do.

1.  We need a new drop-down menu titled “ExoplanetArchive.”
2.  The title of the new menu should link to the archive’s home page, which will contain more information
3.  The menu should display the current number of both confirmed and candidate exoplanets.

Sounds easy enough. Let’s see if it is.</p>

### A New Item

I like seeing data quickly, so let’s put the new item in the top level of the toolbar. The <code>WP_Admin_Bar</code> class provides a method called <code>add_menu()</code> that (surprise!) does the opposite of what is done by the method that we used above (which got rid of the “+ New” menu). If you’re following along at home, add the following code to the bottom of the <code>functions.php</code> file:
<pre class="brush: php">/**
* Add the Smashing WP Exoplanets menu
*/
function smashing_wp_exoplanets_menu() {
global $wp_admin_bar;
$wp_admin_bar-&gt;add_menu(array(
'id' =&gt; 'smashing-wp-exoplanets',
'title' =&gt; __('ExoplanetArchive'),
'href' =&gt; 'https://exoplanetarchive.ipac.caltech.edu/index.html'
));
}
add_action('wp_before_admin_bar_render', 'smashing_wp_exoplanets_menu');
</pre>

As you can see, the process of adding an item to the toolbar isn’t that different from removing one. We’ve defined a new custom function named <code>smashing_wp_exoplanets_menu()</code>; brought the <code>WP_Admin_Bar</code> class instance into our function’s scope with PHP’s <code>global</code> keyword; and instructed the class to add a new menu. The <code>add_menu()</code> method takes an array as an argument. Internally, the <code>WP_Admin_Bar</code> class will pass this array to another function, named <code>add_node()</code>, that handles all of the heavy lifting. The <code>add_node()</code> function will accept six elements from the array that you pass to <code>add_menu()</code>:

*   `id`,
*   `title`,
*   `parent`,
*   `href`,
*   `group`
*   `meta`.

The <code>id</code> is required, and <code>meta</code> should be an array of additional attributes made up of the following six keys:

*   `html`,
*   `class`,
*   `onclick`,
*   `target`,
*   `title`,
*   `tabindex`.

We are using the same action hook to add our new menu to the toolbar right before it is rendered. If all has gone well on your end, the toolbar should now look like this:

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7b5168ad-92bd-4d6f-9c97-1e123a734177/smashing-wp-exoplanet-1.png"><img class="105172" title="smashing_wp_exoplanet_1" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7b5168ad-92bd-4d6f-9c97-1e123a734177/smashing-wp-exoplanet-1.png" alt="Smashing WP Exoplanets 1" width="495" height="82" /></a><br>
<em>The beginning of the exoplanets menu in our WordPress installation for Smashing Magazine.</em>

### Drop Down Like It’s Hot

Not a bad start, but still far from what we’re aiming for. Still, with only nine lines of code, we’ve accomplished about half of the tasks we set out to do. The toolbar item has the correct title, and the title links to Exoplanet Archive’s home page. It’s not a drop-down menu yet, though. Fortunately, transforming this featureless link into a menu is a snap. Let’s update our custom function to include the following code:
<pre class="brush: php">/**
* Add the Smashing WP Exoplanets menu
*/
function smashing_wp_exoplanets_menu() {

…existing code…

$wp_admin_bar-&gt;add_menu(array(
'id' =&gt; 'smashing-wp-confirmed-count',
'parent' =&gt; 'smashing-wp-exoplanets',
'title' =&gt; __('Confirmed Exoplanets')
));

$wp_admin_bar-&gt;add_menu(array(
'id' =&gt; 'smashing-wp-candidate-count',
'parent' =&gt; 'smashing-wp-exoplanets',
'title' =&gt; __('Candidate Exoplanets')
));
}
add_action('wp_before_admin_bar_render', 'smashing_wp_exoplanets_menu');
</pre>

I’ve omitted the existing code for brevity and so that you can see how simple adding items to a parent really is. We replaced the <code>href</code> attribute with a <code>parent</code> attribute that instructs WordPress to place this menu under our original. All we had to do was list the parent’s ID in the <code>parent</code> array element of each new menu. How great is that? Poof! Our link to the Exoplanet Archive magically becomes a drop-down menu. Of course, there really isn’t any magic — just the ingenuity of the core’s developers. When the toolbar is being rendered, a protected function named <code>_bind()</code> is called that handles all of the details about what belongs to what and where they’re supposed to be rendered. You gotta love WordPress!

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e948ad4f-8d33-4c6c-9cd7-881cca96302f/smashing-wp-exoplanet-2.png"><img class="105173" title="smashing_wp_exoplanet_2" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e948ad4f-8d33-4c6c-9cd7-881cca96302f/smashing-wp-exoplanet-2.png" alt="Smashing WP Exoplanets 2" width="443" height="111" /></a><br>
<em>Dropping down our Exoplanets menu</em>

### Get Your Count On

Only one thing left: the counter for the number of exoplanets. Initially, I tried fetching the XML feeds using <a title="Codex: fetch_feed()" href="https://codex.wordpress.org/Function_Reference/fetch_feed"><code>fetch_feed()</code></a>. After some research, I decided that <code>fetch_feed()</code> should be used only when you need to pull in well-formed RSS. I decided instead to use the <code>DOMDocument</code> PHP class to create an instance of an XML document that can be queried and manipulated. It turns out that this works quite well. Here is the final code, from start to finish, with some helpful comments. This should now be at the bottom of your <code>functions.php</code> file:
<pre class="brush: php">/**
* Add the Smashing WP Exoplanets menu
*/
function smashing_wp_exoplanets_menu() {

// bring the admin bar class into this function's scope
global $wp_admin_bar;

// create new DOMDocuments to store the responses from the Exoplanet Archive
$confirmed_object = new DOMDocument();
$candidate_object = new DOMDocument();

// load XML feeds for confirmed and candidate exoplanets
$confirmed_object-&gt;load('https://exoplanetarchive.ipac.caltech.edu/cgi-bin/
nstedAPI/nph-nstedAPI?table=exoplanets&amp;select=pl_hostname&amp;format=xml');
$candidate_object-&gt;load('https://exoplanetarchive.ipac.caltech.edu/cgi-bin/
nstedAPI/nph-nstedAPI?table=keplercandidates&amp;select=kepid&amp;format=xml');

// get arrays of confirmed exoplanets and candidates
$confirmed = $confirmed_object-&gt;getElementsByTagName("TR");
$candidates = $candidate_object-&gt;getElementsByTagName("TR");

// create titles to be used in submenus
$confirmed_title = 'Confirmed Exoplanets: ' . $confirmed-&gt;length;
$candidate_title = 'Candidate Exoplanets: ' . $candidates-&gt;length;

// create top-level drop-down menu
$wp_admin_bar-&gt;add_menu(array(
'id' =&gt; 'smashing-wp-exoplanets',
'title' =&gt; __('ExoplanetArchive'),
'href' =&gt; 'https://exoplanetarchive.ipac.caltech.edu/index.html'
));

// create confirmed exoplanet submenu item
$wp_admin_bar-&gt;add_menu(array(
'id' =&gt; 'smashing-wp-confirmed-count',
'parent' =&gt; 'smashing-wp-exoplanets',
'title' =&gt; $confirmed_title
));

// create candidate exoplanet submenu item
$wp_admin_bar-&gt;add_menu(array(
'id' =&gt; 'smashing-wp-candidate-count',
'parent' =&gt; 'smashing-wp-exoplanets',
'title' =&gt; $candidate_title
));
}
add_action('wp_before_admin_bar_render', 'smashing_wp_exoplanets_menu');
</pre>

In the final code here, we created two new instances of the <code>DOMDocument</code> class, and then called their <code>load()</code> method to pull in the XML feeds from the Exoplanet Archive. Once the feeds are loaded, we call <code>getElementsByTagName()</code> on each object to create an array of planets from each feed. If you look at the <a title="XML Response from Exoplanet Archive API" href="https://exoplanetarchive.ipac.caltech.edu/cgi-bin/nstedAPI/nph-nstedAPI?table=exoplanets&amp;select=pl_hostname&amp;format=xml">XML that is returned</a> in a browser, you will see that each row from the Exoplanet Archive database is wrapped in a <code>tr</code> element. By creating an array of all <code>tr</code> elements, we are able to count the elements in the array to get the number of planets returned. You can see that we’re doing just that in the next step. We take the count (i.e. length) returned from each array and concatenate it onto the end of each title string. The only change to the code from the previous snippets is that we’re now using the title variables when creating each “submenu.”

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/539604e7-6d51-44ec-b864-40a06297d7b8/smashing-wp-exoplanet-3.png"><img class="105174" title="smashing_wp_exoplanet_3" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/539604e7-6d51-44ec-b864-40a06297d7b8/smashing-wp-exoplanet-3.png" alt="Smashing WP Exoplanets 3" width="508" height="116" /></a><br>
<em>The final exoplanets menu, with planet counters.</em>

This code will obviously strain your bandwidth because every single page load requires a call to the Exoplanets Archive to update the planet counters. The sample code above needs drastic optimization and refactoring cycles before it can be considered both robust and stable. For the purposes of this article, though, our hack-ish attempts to just make it work will have to do. This could be an ideal scenario in which to use the <a title="Codex: Transients API" href="https://codex.wordpress.org/Transients_API">Transients API</a>, which enables us to stick the planet counters in our database and assign an expiration value that triggers an update far less frequently. But that’s an article for another day. Perhaps we’ll follow up by turning this example into a full-blown toolbar plugin!

## Conclusion

Despite the mixed reactions following the debut of the Admin Bar, tremendous progress has been made, and a <em>lot</em> of functionality has been added. If your toolbar is currently disabled, please give it a second look. You just might find that this tempting 28-pixel-tall canvas is not that difficult to customize. The core team had reasons for adding its features, even if they’re not immediately apparent.

This research has made use of the NASA Exoplanet Archive, which is operated by the California Institute of Technology, under contract with the National Aeronautics and Space Administration under the Exoplanet Exploration Program.</p>

### Other Resources

*   [Plugins for the Admin Bar](https://wordpress.org/extend/plugins/search.php?q=admin+bar "Admin Bar Plugins"), WordPress
*   [Plugins for the Toolbar](https://wordpress.org/extend/plugins/search.php?q=wordpress+toolbar&sort= "Toolbar Plugins"), WordPress
*   [Plugin API](https://codex.wordpress.org/Plugin_API "The WordPress Plugin API"), WordPress Codex Introduction to WordPress’ Plugin API (including action and filter hooks).
*   [PlanetQuest](https://planetquest.jpl.nasa.gov/ "JPL: PlanetQuest"), NASA Jet Propulsion Laboratory Currently hosts information about and the status of the ongoing Kepler mission.
*   [NASA Exoplanet Archive](https://exoplanetarchive.ipac.caltech.edu/index.html "NASA Exoplanet Archive") Public data from the search for extrasolar planets, made available through the [Infrared Processing and Analysis Center](https://www.ipac.caltech.edu/ "Infrared Processing and Analysis Center") (IPAC) at the California Institute of Technology.
*   “[The DOMDocument Class](https://www.php.net/manual/en/class.domdocument.php "PHP Manual: DOMDocument Class"),” PHP.net The manual page outlining everything you’ve ever wanted to know about PHP’s DOMDocument class.

{{< signature "al" >}}

