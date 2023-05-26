---
title: Internationalizing And Localizing Your WordPress Theme In 6 Steps
slug: internationalizing-localizing-wordpress-theme
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a7412374-60fe-46fd-a9d2-b5388bb34ddd/globewp.jpg
date: 2011-12-29T15:53:37.000Z
author: konstantinos-kouratoras
description: >-
  A very important part of WordPress theme development is preparing it so that users from every corner of the planet can translate its messages to any language.
categories:
  - WordPress
  - Themes
  - Localization
---
This article covers the basics of internationalization, which is the process of designing a theme in such a way that the end user can adapt it to various languages without having to change the source code, and localization, which is the process of translating text messages to a particular language. <strong>Expanding the range of our theme’s users is a big deal</strong>, and WordPress provides a simple way to do that.

*   [How To Conduct Website Localization](https://www.smashingmagazine.com/2014/12/how-to-conduct-website-localization/)
*   [CSS-Driven Internationalization In JavaScript](https://www.smashingmagazine.com/2014/06/css-driven-internationalization-in-javascript/)
*   [<span class="headline">Should You Ask The User Or Their Browser?</span>](https://www.smashingmagazine.com/2013/02/remove-interface-elements/)
*   [Diary Of A WordCamp](https://www.smashingmagazine.com/2012/05/diary-of-a-wordcamp/)

### Overview of Process

Here is a brief overview of the process of internationalizing and localizing a WordPress theme:

{{% feature-panel %}}

1.  Load a text domain,
2.  Process text messages with WordPress functions,
3.  Extract these messages with the appropriate software,
4.  Provide a translation for each message,
5.  Create a language file for a particular locale,
6.  Instruct WordPress to enable localization and to load the language file.</p>

## Adding WordPress Functions

The first thing to do is load a text domain by adding the following line in the <code>functions.php</code> file of our theme:

<pre><code class="language-php">load_theme_textdomain('mytheme', get_template_directory() . '/languages');</code></pre>

The first argument must be a <strong>unique identifier</strong> (a good practice is to use your theme’s name); it defines the theme’s domain, as the text for translation will not be in WordPress’ core translation files. The second argument defines the folder of the language files. To load these files, the function must be tied to the <code>after_setup_theme</code> action:

<pre><code class="language-php">add_action('after_setup_theme', 'my_theme_setup');
function my_theme_setup(){
    load_theme_textdomain('mytheme', get_template_directory() . '/languages');
}</code></pre>

## Processing Text Messages

After editing <code>functions.php</code>, the next step is to look through the source files, find the messages that need to be translated and process them with the appropriate WordPress function. The two most important and commonly used are <code>_e($text_message)</code> and <code>__($text_message)</code>. The first function searches for the translation of <code>$text_message</code> and prints it. If the translation does not exist, then it prints <code>$text_message</code>. This function is used for text messages that are not in PHP functions, as it prints the result. Take the following line:

<pre><code class="language-php">echo ‘Hello user’;</code></pre>

This should be transformed to:

<pre><code class="language-php">_e(‘Hello user’,’mytheme’);</code></pre>

The second function searches for the translation of <code>$text_message</code> and returns it. If a translation does not exist, then it returns <code>$text_message</code>. It is used for text that is in PHP functions. For example:

<pre><code class="language-php">the_content( ‘Read more’ );</code></pre>

This function call should be transformed to:

<pre><code class="language-php">the_content( __(‘Read more’,’mytheme’) );</code></pre>

Sometimes, a text message includes dynamic data, such as a number from a PHP variable. In this case, we use the <code>sprintf</code> PHP function to produce the final message string:

<pre><code class="language-php">$results_found = 12;
$message = sprintf( __(‘%s results found’ , ‘mytheme’) , $results_found );</code></pre>

### Singular and Plural

WordPress provides a function for singular and plural translation of the same text message:

<pre><code class="language-php">_n( $single, $plural, $number, $domain )</code></pre>

The first argument is the text that will be used for singular, and the second is the text that will be used for plural. The third argument is the number to compare in order to decide which to use.

Although the <code>_n()</code> function is built into WordPress, <strong>using it is discouraged</strong> because the translation software parses only the first parameter of a function, and so these two text messages would not be fetched. Instead, we can use the PHP <code>if</code> statement:

<pre><code class="language-php">if($results_found == 1)
    $message = __(‘1 result found’ , ‘my-text-domain’);
else
    $message = sprintf( __(‘%s results found’ , ‘my-text-domain’) , $results_found );</code></pre>

## Language Files

Once we ensure that we’ve processed every text message with the functions mentioned above, our theme is ready for translation. For this purpose, there are three types of language files:

*   The **POT** file contains a list of all translatable messages in our theme.
*   The **`.po`** file is created when we translate a POT file to a particular locale.
*   The **`.mo`** is a binary file that is created automatically by translation software and is not human-readable.</p>

### Messages List

The first thing to do is create a POT file, which contains all of the text messages of our source files and which will be the file that the translator uses to translate the messages to another locale. There are several tools for creating POT files. The most popular, and the one we will use in this article, is a cross-platform tool called <a href="https://www.poedit.net/">Poedit</a>.

1.  Open Poedit, and create a new catalog.
2.  Fill in the project’s information in the “Project info” tab: ![Project info tab of Poedit](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3bf0c229-f8e9-4465-8b61-8d0b24ba8f55/image01.png "Project info tab of Poedit")
3.  In the “Paths” tab, identify the folder for Poedit to search for source files that contain translatable text messages. These folders are relative to the folder of our language file, so if we save the file in a folder in our theme folder, then we should add `..`: ![Paths info tab of Poedit](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/03e65ab7-f1c0-4d4a-9a06-63a2eebb2fa6/image02.png "Paths info tab of Poedit")
4.  In the “Keywords” tab, define the WordPress functions used to translate messages (keep in mind that Poedit is not only for WordPress). In our theme, the two keywords we used are `__` and `_e`. ![Keywords info tab of Poedit](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8add9159-041f-4658-9285-3fefa4ab0a66/image03.png "Keywords info tab of Poedit")
5.  After you click “OK,” Poedit will scan the folders you’ve provided in the Paths tab and will list the text messages in the source files. [![Messages list in Poedit](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/49157eea-a1c8-41d9-9ad1-ba6d4e4a727a/image04.png "Messages list in Poedit")](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/49157eea-a1c8-41d9-9ad1-ba6d4e4a727a/image04.png)
6.  Save the POT file in a folder named `languages` in your theme directory: ![Languages directory with POT file](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/65238488-2e85-476d-b1ce-5516710beb82/pot-file-folder.png "Languages directory with POT file")

<strong>Please note:</strong> WordPress does not need a POT file to load a particular translation. The file is just a template that contains all of the translatable message strings, which you can provide to the translator to translate and return to you as a <code>.po</code> file.</p>

### Providing Translation

Our POT file is now created! The next step is to translate the messages of this POT file to a particular locale and then save it as a <code>.po</code> file:

1.  Select the string you want from the list, and type the translation into the field at the bottom of the window. [![Type translation for a text message in Poedit](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8dd0b2af-c7b7-4d15-b1f5-513612b554d2/image05.png "Type translation for a text message in Poedit")](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8dd0b2af-c7b7-4d15-b1f5-513612b554d2/image05.png)
2.  Repeat this action until all messages have been translated.
3.  Save the file as a `.po` file in the same folder, **setting the language code and country code as the file name** (sometimes they are identical), as defined by [ISO 639-1](https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes "Language Code") and [ISO 3166-1](https://en.wikipedia.org/wiki/ISO_3166-1 "Country Code"), respectively. For example, if the language of the translation is British English, then the name would be `en_GB.po`. Now, the `languages` folder will contain the `.po` and `.mo` files of our translation as well as the POT file: ![Languages directory with .po files](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1a314b88-f32e-458b-9658-3e1275fa18c7/po-file-folder.png "Languages directory with .po files")

<strong>Please note:</strong> When saving a <code>.po</code> file, Poedit will automatically create an <code>.mo</code> file, which is a binary file and is not human-readable.</p>

### Updating the Configuration File

Once we’ve created the <code>.po</code> and <code>.mo</code> files, it’s time to instruct WordPress to enable the localization and to load the language files. Edit the <code>wp-config.php</code> file in WordPress’ root folder, and set the <code>WPLANG</code> variable to the relevant locale. For example:

<pre><code class="language-php">define('WPLANG', ’);</code></pre>

If we’re using the British English locale, then we would change the line above to:

<pre><code class="language-php">define('WPLANG', 'en_GB');</code></pre>

## What About Plugins?

Although this article deals with WordPress themes, it’s worth mentioning that the differences in the process of internationalizing a plugin are minor. Similar to what we did, we tell WordPress where to find the language files by adding the following function in the plugin’s main file:

<pre><code class="language-php">load_plugin_textdomain('myplugin', false, basename( dirname( __FILE__ ) ) . '/languages' );</code></pre>

The first parameter defines the text domain; using the plugin’s name is recommended, as it must be unique. The second parameter defines a path of a folder, where the <code>.mo</code> file resides. It corresponds to a deprecated function that was valid until WordPress 2.7, so we specify it as <code>false</code>. The third parameter is the folder where the language files reside (in this case, we assume they are located in a directory named <code>languages</code>).

To load the language files, we need to add a hook and tie this function into the <code>init</code> WordPress action:

<pre><code class="language-php">function myplugin_internationalization()
{
    load_plugin_textdomain('myplugin', false, basename( dirname( __FILE__ ) ) . '/languages' );
}
add_action('init', 'myplugin_internationalization');</code></pre>

Finally, we process the text messages the same way as before, using the <code>_e($text_message)</code> and <code>__($text_message)</code> functions. After we’ve processed all of the text messages, our plugin is ready for localization.</p>

## Conclusion

WordPress’ user base is growing rapidly, making the CMS one of the most popular tools in the world of Web development. With people coming from all over the world and speaking different languages, WordPress offers a flexible platform and provides an easy method of internationalization, enabling users to translate with no modification to the source code.</p>

### Other Resources

This article covers the basics of internationalizing and localizing a WordPress theme. For more in-depth information, have a look at the following related resources, available in the <a title="WordPress Codex" href="https://codex.wordpress.org/">WordPress Codex</a>:

*   “[Internationalization for WordPress Developers](https://codex.wordpress.org/I18n_for_WordPress_Developers "Internationalization for WordPress Developers")”
*   “[Translating WordPress](https://codex.wordpress.org/Translating_WordPress "Translating WordPress")”

{{< signature "al" >}}

