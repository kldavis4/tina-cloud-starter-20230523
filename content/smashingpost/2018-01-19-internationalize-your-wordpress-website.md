---
title: How To Internationalize Your WordPress Website
slug: internationalize-your-wordpress-website
author: lizziekardon-taylorhansen
image: >-
  //archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/666511c0-7f69-499c-9427-2d69067c470d/image4.png
date: 2018-01-19T08:43:49.000Z
summary: >-
  WordPress is currently fully localized for over 65 languages and offers
  partial translations for an additional 95 locales. If you haven't
  internationalized your WordPress website yet, it's probably time to do so.
description: >-
  WordPress is currently fully localized for over 65 languages and offers
  partial translations for an additional 95 locales. If you haven't
  internationalized your WordPress website yet, it's probably time to do so.
categories:
  - WordPress
  - Internationalization
---
<p>On September 30th, 2017, the international WordPress community united for 24 hours to translate the WordPress ecosystem. For the third time, #WPTranslationDay fused an all-day translating marathon with digital and contributor day events designed to promote the value of creating accessible experiences for global users, better known as "localization".</p>

<p>As an open-source community, we should all strive to localize our open-source contributions. Before you can transcribe your digital assets though, you have to internationalize your codebase.</p>

<p>The terms “internationalization” and “localization” are often used interchangeably, though they technically represent two different aspects of the translation process.</p>
<ul>
<li><strong>Internationalization (I18N)</strong> is the process of internationalizing or adapting your theme or plugin to translate it into any language in the world.</li>
<li><strong>Localization (L10N)</strong> is the subsequent process of localizing, or <em>translating</em> your internationalized tools into a given language.</li>
</ul>

<p>WordPress is currently fully localized for over 65 languages and offers partial translations for an additional 95 locales. International use continues to rise as more localizations are introduced.</p>

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/666511c0-7f69-499c-9427-2d69067c470d/image4.png" sizes="100vw" caption="Stats from WordPress.org (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/666511c0-7f69-499c-9427-2d69067c470d/image4.png'>Large preview</a>)" alt="Stats from WordPress.org" >}}

{{% feature-panel %}}

<p>Non-English speaking WordPress users surpassed English speaking users in 2014, and they inadvertently continue to dilute English users’ percentage of pie in 2017 as efforts like #WPTranslateDay grow.</p>

<p>As WordPress becomes more and more linguistically accessible, knowledge of I18N & L10N is essential for plugin and theme developers to thrive in the global WordPress economy. For scaling businesses, these development skills can open doors to foreign markets. Web accessibility, including language accessibility, is good for business, and better for people.</p>

<p>As a continuation of <strong>#WPTranslationDay</strong>, here’s an updated guide to internationalizing your WordPress plugins and themes.</p>

<p>Here is a brief overview of the process we’ll be exploring today.</p>

<ul>
<li>Discovery
<ul>
<li>Get to Know Translation Files
<ul>
<li>POT File</li>
<li>PO File</li>
<li>MO File</li>
</ul></li>
<li>GlotPress & Language Packs</li>
<li>Backup & Prepare Your Environment</li>
</ul></li>
<li>Plugin I18N
<ul>
<li>Plugin Header</li>
<li>Load Text Domain</li>
<li>Strings Audit</li>
<li>Generate POT File</li>
</ul></li>
<li>Theme I18N
<ul>
<li>Theme Header</li>
<li>Load Text Domain</li>
<li>Strings Audit</li>
<li>Generate POT File</li>
</ul></li>
<li>JavaScript I18N</li>
<li>Additional Resources</li>
</ul>

## Discovery

### Get To Know Translation Files

<p>WordPress uses the <a href="https://www.gnu.org/software/gettext/">GNU gettext</a> library to facilitate I18N.</p>

<p>First, let’s get familiar with the gettext translation files generated throughout the process.</p>

<p><strong>Portable Object Template File (POT)</strong></p>

<p>During the I18N process, we’ll use a tool to find internationalized strings and generate a <strong>POT file</strong> containing all of the translatable text in your plugins and theme.</p>

<p><strong>Portable Object File (PO)</strong></p>

<p>In appearance, there are no remarkable differences between a POT file and <strong>PO file</strong>. They’re syntactically the same and only differentiated by their intended purposes.</p>

<p>After generating a POT file, text strings should be interpreted by a translator into your preferred language. The PO file will eventually contain text strings in your native language, as well as the appropriate translations.</p>

<p><strong>Machine Object File (MO)</strong></p>

<p>Finally, the PO file is converted into a machine-readable document or Machine Object file. This file will live in your theme or plugin directory for WordPress to call upon when it’s time to serve a translated version.</p>

### Back-up And Prepare Your Environment

<p>Before modifying any markup, take a backup of your plugin, theme or your entire site (whatever you are internationalizing!) and get your development environments in order.</p>

<p>Be sure to do a quick plugin audit if you plan to localize your website. Delete or deactivate any plugins that you’re no longer actively using. This quick audit will save you time in the long run.</p>

## Internationalize Your Plugins

### PLUGIN HEADER

<p>First, we’ll update the plugin header. Specifically, the <strong>text domain</strong> and the <strong>domain path</strong>.</p>

<p><strong>Example Plugin Header</strong></p>

<pre><code class="language-php">/*
 Plugin Name: My Rad Plugin
 Plugin URI: https://myradplugin.com
 Description: Custom Plugin That Makes My Site Rad
 Author: Rad Plugin Creator
 Version: 1.0
 Author URI: https://radplugincreator.com
 Text Domain: rad-plugin
 Domain Path: /languages/
 */
</code></pre>

<p><strong>Text Domain</strong></p>

<p>The text domain is a unique identifier for WordPress to recognize all of the text belonging to a plugin and <strong>must match the plugin’s slug</strong>.</p>

<p>This is especially important if your plugin is hosted on WordPress.org; these need to match in order for GlotPress to properly import translations for your plugin.</p>

<p class="c-pre-sidenote--left">In our example, the plugin file is named <strong>rad-plugin.php</strong> and the text domain is <strong>rad-plugin</strong></p><p class="c-sidenote c-sidenote--right">You may already have a text domain set. If you don’t, remember to use hyphens, not underscores.</p>

<p><strong>Domain Path</strong></p>

<p>The domain path is the folder that the finalized translation files will live in. You should create a new folder within the plugin directory, such as <strong>/languages/</strong>, and update the domain path, so WordPress knows exactly where to search for translation files.</p>

### LOAD TEXT DOMAIN

<p>Next up, we’re going to the load the text domain by adding the following function to our code.</p>

<p><strong>load_plugin_textdomain()</strong></p>

<div class="break-out">

<pre><code class="language-php">load_plugin_textdomain( $domain, $abs_rel_path, $plugin_rel_path );
</code></pre></div>

<p>If a translation file is available for the user’s language, the load text domain function will tell WordPress to deliver it.</p>

<p><strong>Parameters</strong></p>
<ul>
<li><strong>$domain</strong> &mdash; text domain <em>(required)</em></li>
<li><strong>$abs_rel_path</strong> &mdash; false <em>(optional, deprecated)</em></li>
<li><strong>$plugin_rel_path</strong> &mdash; /languages/ <em>(optional, this is the relative path to the directory containing your translation files. In our example, /languages/. As of 4.6, WordPress will search for these files in the plugin’s /languages/ directory, if this goes unspecified.)</em></li>
</ul>

<p><strong>Rad Plugin Example</strong></p>

<p>To load the text domain, we’ll hook into the ‘plugins_loaded’ action.</p>

<div class="break-out">

<pre><code class="language-php">add_action( 'plugins_loaded', 'rad_plugin_load_text_domain' );
function rad_plugin_load_text_domain() {
    load_plugin_textdomain( 'rad-plugin', false, dirname( plugin_basename( __FILE__ ) ) . '/languages/' );
}
</code></pre></div>

### STRINGS AUDIT

<p>The next step is to wrap all of the plugin’s text strings in translation functions.</p>

<p>The most common translation functions are <code>__()</code> for returning a translated string and <code>_e()</code> for echoing a translated string.</p>

<p><strong>Rad Plugin Example</strong></p>

<pre><code class="language-php">__()
$text = __( 'Super Rad!', 'rad-plugin' );
</code></pre>

<p>This function will work for simple translations. It takes into account two parameters; the <strong>text string</strong> and the <strong>text domain</strong>.</p>

<pre><code class="language-php">_e( 'Super Rad!', 'rad-plugin' );
</code></pre>

<p>This function simply echoes the value. Otherwise, it works exactly as the previous function does.</p>

 <p>There are a slew of additional translation functions that should also be used when appropriate.</p>

<p><strong>Other Basic Functions</strong></p>

<pre><code class="language-php">__()
_e()
_x()
_ex()
_n()
_nx()
_n_noop()
_nx_noop()
translate_nooped_plural()
</code></pre>

<p><strong>Date & Number Functions</strong></p>

<pre><code class="language-php">number_format_i18n()
date_i18n()
</code></pre>

<p><strong>Escape Functions</strong></p>

<p>Don’t forget to escape any data that’s being output using the following escape functions.</p>

<pre><code class="language-php">esc_html__()
esc_html__()
esc_html_x()
esc_attr__()
esc_attr_e()
esc_attr_x()
</code></pre>

<p>In our Rad example, we might have a line of plugin code that looks like this:</p>

<div class="break-out">

<pre><code class="language-php">function create_section() {
    esc_html_e( 'Below are your settings for Rad Plugin', 'rad-plugin' );
}
</code></pre></div>

### CREATE A POT FILE

<p>The final step is to create a POT file. There are a <a href="https://www.gnu.org/software/trans-coord/manual/web-trans/html_node/PO-Editors.html">few different tools</a> available to generate this type of file, but for this tutorial, we’ll stick to recommendations from the WordPress codex and use <a href="https://poedit.net/wordpress">Poedit</a>, an easy-to-use GUI for managing translations.</p>

<p><strong>Note</strong>: If your plugin or theme is already in the WordPress.org repository, you can skip this process and <a href="https://developer.wordpress.org/plugins/internationalization/localization/#plugin-directory%c2%a0admin-tools">generate a POT file from the admin page</a>. In this case, it isn’t necessary to generate a .po file for each language. The introduction of GlotPress and language packs in 2015 simplified the translation process; all that is needed for GlotPress is the .pot file, which will be imported by WordPress.org and served to translators through the <a href="https://translate.wordpress.org">translate.wordpress.org</a> dashboard. Collaborators from around the world will use this dashboard to provide translations on #WPTranslateDay.</p>

### <a href="https://poedit.net/wordpress">Download Poedit</a>

<p><strong>Configuring Poedit</strong></p>

<p><em>Translation Properties</em></p>

<p>Start by going to <strong>File</strong> > <strong>New</strong>. Then select your plugin’s native language and hit <strong>OK</strong>.</p>

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/585e8e77-075c-4ffa-aade-1b33a660526d/image2.png" sizes="100vw" caption="<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/585e8e77-075c-4ffa-aade-1b33a660526d/image2.png'>Large preview</a>" alt="" >}}

<p>Next, select <strong>Catalog</strong> > <strong>New</strong>. Enter the project name, version, contact and language.</p>

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/91472832-8fb0-4d6a-8e5f-167ee9fffb86/image1.png" sizes="100vw" caption="<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/91472832-8fb0-4d6a-8e5f-167ee9fffb86/image1.png'>Large preview</a>" alt="" >}}

<p><em>Paths</em></p>

<p>Select the <strong>Sources Paths</strong> tab next. If this is a new file, you will have to save the file first.</p>

<p>Following our example, we’d select <strong>File</strong> > <strong>Save As</strong> to save as a .po file to the /languages/ directory inside of rad-plugin. Again, the file name should match your plugin’s slug.</p>

<pre><code class="language-php">rad-plugin.po
</code></pre>

<p>After saving, then enter the relative path to the directory where your translation files will live.In this scenario, <em>languages</em>.</p>

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4eb7b09a-842e-4756-a170-b9a4b5f77a1a/image3.png" sizes="100vw" caption="<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4eb7b09a-842e-4756-a170-b9a4b5f77a1a/image3.png'>Large preview</a>" alt="" >}}

<p><em>Keywords</em></p>

<p>Select the <strong>Sources Keywords</strong> tab. Click the <strong>+ icon</strong> to add the appropriate function names.</p>

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5234563c-cf1f-4d57-ac49-be6f13d24100/image5.png" sizes="100vw" caption="<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5234563c-cf1f-4d57-ac49-be6f13d24100/image5.png'>Large preview</a>" alt="" >}}

### Cheatsheet

<pre><code class="language-php">__
_e
_x
_ex
_n
_nx
_n_noop
_nx_noop
translate_nooped_plural
number_format_i18n
date_i18n
esc_html__
esc_html__
esc_html_x
esc_attr__
esc_attr_e
esc_attr_x
</code></pre>

<p>Afterwards, you can click OK and then <strong>File > Save</strong>.</p>

<p>Poedit will save both a .mo and a .po file. You can create the .pot file by copying the .po file and adding a .pot extension. International users can use the template .pot file to translate the strings into their language.</p>

## Internationalize Your Theme

<p>The process for internationalizing your theme is practically identical to I18N for plugins. We’ll start by checking the theme header and end by generating another POT file.</p>

### THEME HEADER

<p>Double check your theme header to make sure your text domain and domain path are set.</p>

<p><strong>Example Theme Header</strong></p>

<pre><code class="language-php">/*
Theme Name: Rad Theme
Author: Rad Theme Author
Text Domain: rad-theme
Domain Path: /languages/
*/
</code></pre>

### LOAD TEXT DOMAIN

<p>The next step is load a text domain in your theme’s <strong>functions.php</strong> file this time.</p>

<p><strong>load_theme_textdomain()</strong></p>

<div class="break-out">

<pre><code class="language-php">load_theme_textdomain( 'radtheme', get_template_directory() . '/languages' );
</code></pre></div>

<p>In order for these files to load, you have to register them with the after_setup_theme action.</p>

<div class="break-out">

<pre><code class="language-php">add_action( 'after_setup_theme', 'rad_theme_setup' );
function rad_theme_setup() {
    load_theme_textdomain( 'radtheme', get_template_directory() . '/languages' );
}
</code></pre></div>

### STRINGS AUDIT

<p>Time for another strings audit! You should be familiar with the basic translation functions at this point.</p>

 <p>Let’s take a look some trickier translations.</p>

<p><strong>Placeholders</strong></p>

<p>PHP variables like the example below will not be translated properly without the use of placeholders.</p>

<pre><code class="language-php">echo "We added $count rad points.";
</code></pre>

<p><strong>printf() & sprintf()</strong></p>

<p>These functions use placeholders such as <strong>%s</strong>, or <strong>%d</strong> for integers, to interpolate a string of text with dynamic content.</p>

<p><strong>Rad Theme Example</strong></p>

<div class="break-out">

<pre><code class="language-php">/* Translators: %d is the number of rad points added */

printf( esc_html__( 'We added %d rad points.', 'rad-plugin' ), $count );
</code></pre></div>

<p><strong>Plurals</strong></p>

<p>The <code>_n()</code> function can handle more complex string translations like plurals, but it’s not recommended because of its limitations within translation software. Instead you can write a simple <em>if statement</em> to distinguish between singular and plurals words.</p>

<p><strong>Rad Plugin Example</strong></p>

<div class="break-out">

<pre><code class="language-php">If ( 1 === $rad_points_found ) {
    $message = __( '1 rad point', 'rad-plugin' );
} else {
    /* Translators: %s is the number of rad points found */
    $message = sprintf( __( '%s rad points' , 'rad-plugin' ) , $rad_points_found );
}
</code></pre></div>

### GENERATE POT FILE

<p>The process for generating theme POT files is the same as generating plugin POT files. Explore some methods below.</p>

<p><strong>Command Line</strong></p>

<p>With <a href="https://develop.svn.wordpress.org/trunk/">WordPress Trunk</a> and the <a href="https://www.gnu.org/software/gettext/">gettext GNU package</a> installed, you can breeze through this step by running the <strong>makepot.php</strong> script in the command line.</p>

 <p>Open the command line and navigate to the I18N tools directory.</p>

<pre><code class="language-php">cd wpdev/tools/i18n/
</code></pre>

<p>The script should look something like this:</p>

<div class="break-out">

<pre><code class="language-php">php path/to/makepot.php wp-theme path/to/rad-theme rad-theme.pot
</code></pre></div>

<p>The script will do its thing and the finished file, <strong>rad-theme.pot</strong>, will end up in the current directory.</p>

<p><strong>Grunt Tasks</strong></p>

<p>Another method for creating a POT file is to run Grunt tasks using either <a href="https://github.com/cedaro/grunt-wp-i18n">grunt-wp-i18n</a> or <a href="https://www.npmjs.com/package/grunt-pot">grunt-pot</a>. Task runners like Grunt can automate lots of tedious tasks, such as generating POT files.</p>

 <p>To create your POT file, make sure you have <a href="https://nodejs.org/">node.js</a> installed first. Then, install Grunt in your language directory via the command line, and away you go. Now, you can quickly run these I18N commands and make your translation file without leaving the comfort of the command line.</p>

## JavaScript I18N

<p>If you’re a modern theme or plugin developer, chances are you use JavaScript to handle some component of your project. <strong>wp_localize_script</strong> is an effective function for <a href="https://pippinsplugins.com/use-wp_localize_script-it-is-awesome/">extracting PHP data to provide to your scripts</a>, and it’s the only way to translate JavaScript inside of WordPress.</p>

### WP_LOCALIZE_SCRIPT()

<p>This function will allow us to localize strings server-side in PHP and provide text strings as a JavaScript object to the script.</p>

<pre><code class="language-php">wp_localize_script( $handle, $name, $data );
</code></pre>

### PARAMETERS
<ul>
<li><strong>$handle</strong> &mdash; script handle the data needs to be available for <em>(required &mdash; needs to match the handle of the script this data is for, see example below)</em></li>
<li><strong>$name</strong> &mdash; name of the object to contain the data <em>(required &mdash; should be unique)</em></li>
<li><strong>$data</strong> &mdash; an array of data to pass to the script <em>(required)</em>.</li>
</ul>

### RAD PLUGIN EXAMPLE

<pre><code class="language-php">add_action( 'wp_enqueue_scripts', 'rad_theme_scripts' );
function rad_theme_scripts() {
    wp_enqueue_script( 'rad-theme-script', get_template_directory_url() . '/js/rad-theme-script.js' );
    wp_localize_script( 'rad-theme-script', 'rad-I18n',
        array(
            'message' => __( 'Super Rad!', 'rad-theme' ),
        ) 
    );
}
</code></pre>

### ACCESS DATA IN JAVASCRIPT

<p>The simple code snippet below is an example of how to access this data in your JavaScript file.</p>

<pre><code class="language-php">alert( rad-I18n.message );
</code></pre>

## Additional Resources
<ul>
<li><a href="https://codex.wordpress.org/I18n_for_WordPress_Developers">I18N for WordPress Developers</a></li>
<li><a href="https://developer.wordpress.org/themes/functionality/internationalization/">WordPress Theme Handbook: Internationalization</a></li>
<li><a href="https://developer.wordpress.org/plugins/internationalization/">WordPress Plugin Handbook: Internationalization</a></li>
<li><a href="https://wordpress.tv/?s=i18n">WordPress.tv: I18N</a></li>
</ul>

## Wrapping It Up

<p>Congratulations! You’ve just internationalized your theme and/or plugin, making it accessible for people of all native languages to benefit from. Whether your project is distributed through the WordPress repository, or custom-developed for your organization’s website, there’s only an upside to internationalizing your files from start.</p>
<ul>
<li>Make your <a href="https://pagely.com/blog/2017/05/citizen-guide-open-source-community/">open-source contributions</a> accessible globally.</li>
<li>Create conversations with new customers in foreign markets.</li>
<li>Save time and reduce laborious updates in future.</li>
</ul>

<p><strong>Always internationalize.</strong></p>

{{< signature "mc, ra, yk, il" >}}

