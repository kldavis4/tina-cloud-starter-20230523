---
title: Obfuscating Blacklisted Words In WordPress With ROT13
slug: encrypting-blacklisted-words-in-wordpress-with-rot13
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/caad8a2a-1588-4c58-8d28-a41c012dd236/caesar-cipher-illu.png
date: 2014-12-11T22:08:09.000Z
author: agbonghamacollins
description: >-
  Countless algorithms for encrypting data exist in computer science. One of the
  lesser known and less common encryptions is ROT13, a derivative of the [Caesar
  cypher](https://en.wikipedia.org/wiki/Caesar_cipher) encryption technique.

  In this tutorial, we’ll learn about ROT13 encryption and how it works. We’ll
  see how text (or strings) can be programmatically encoded in ROT13 using PHP.
  Finally, we’ll code a WordPress plugin that scans a post for blacklisted words
  and replaces any in ROT13 encryption.
categories:
  - WordPress
  - Techniques (WP)
---
Countless algorithms for encrypting data exist in computer science. One of the lesser known and less common encryptions is ROT13, a derivative of the <a href="https://en.wikipedia.org/wiki/Caesar_cipher">Caesar cypher</a> encryption technique.

In this tutorial, we’ll learn about ROT13 encryption and how it works. We’ll see how text (or strings) can be programmatically encoded in ROT13 using PHP. Finally, we’ll code a WordPress plugin that scans a post for blacklisted words and replaces any in ROT13 encryption.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [A Look At The Modern WordPress Server Stack](https://www.smashingmagazine.com/2016/05/modern-wordpress-server-stack/)
*   [Secrets Of High-Traffic WordPress Blogs](https://www.smashingmagazine.com/2012/09/secrets-high-traffic-wordpress-blogs/)
*   [Speeding Up Your Website’s Database](https://www.smashingmagazine.com/2011/03/speeding-up-your-websites-database/)
*   [<span class="headline">Do-It-Yourself Caching Methods With WordPress</span>](https://www.smashingmagazine.com/2012/06/diy-caching-methods-wordpress/)

If you own a blog on which multiple authors or certain group of people have the privilege of publishing posts, then a plugin that encrypts or totally removes inappropriate words might come in handy

{{% feature-panel %}}

Before we begin let's clear up something about ROT13. It should <strong>never</strong> be used to encrypt sensitive data. While it is considered an encryption technique, it is the "Hello World" example of encryption. It can be broken extremely easily and thus is never used on data which is encrypted for security reasons. Since our goal isn't to protect data it is to hide profanity, it will do just fine for our example.</p>

## Introduction

ROT13 (short for “rotate by 13 places,” sometimes abbreviated as ROT-13) is a simple encryption technique for English that replaces each letter with the one 13 places forward or back along the alphabet. So, A becomes N, B becomes O and so on up to M, which becomes Z. Then, the sequence continues at the beginning of the alphabet: N becomes A, O becomes B and so on up to Z, which becomes M.

A major advantage of ROT13 over other <code>rot(N)</code> techniques (where “N” is an integer that denotes the number of places down the alphabet in a Caesar cypher encryption) is that it is “self-inverse,” meaning that the same algorithm is applied to encrypt and decrypt data.

Below is a ROT13 table for easy reference.</p>

<pre><code class="language-markup">
| A | B | C | D | E | F | G | H | I | J | K | L | M | N | O | P | Q | R | S | T | U | V | W | X | Y | Z |
--------------------------------------------------------------------------------------------------------  
| N | O | P | Q | R | S | T | U | V | W | X | Y | Z | A | B | C | D | E | F | G | H | I | J | K | L | M |
</code></pre>

If we encrypted the domain <code>smashingmagazine.com</code> in ROT13, the result would be <code>fznfuvatzntnmvar.pbz</code>, and the sentence “Why did the chicken cross the road?” would become “Jul qvq gur puvpxra pebff gur ebnq?”

Note that only letters in the alphabet are affected by ROT13. Numbers, symbols, white space and all other characters are left unchanged.</p>

## Transforming Strings To ROT13 In PHP

PHP includes a function, <code>str_rot13()</code>, for converting a string to its ROT13-encoded value. To encode text in ROT13 using this function, pass the text as an argument to the function.</p>

<pre><code class="language-php">
&lt;?php

echo str_rot13('smashingmagazine.com'); // fznfuvatzntnmvar.pbz

echo str_rot13('The best web design and development blog'); // Gur orfg jro qrfvta naq qrirybczrag oybt
</code></pre>

## Using ROT13 In WordPress

Armed with this knowledge, I thought of ways it might be handy in WordPress. I ended up creating a plugin that encodes blacklisted words found in posts using ROT13.

The plugin consists of a <code>textearea</code> field (located in the plugin’s settings page) in which you input blacklisted words, which are then saved to the database for later reuse in WordPress posts.

Without further fussing, let’s start coding the plugin.</p>

### Setting Up the Plugin

First, include the plugin’s <a href="https://codex.wordpress.org/File_Header">file header</a>.</p>

<pre><code class="language-php">
&lt;?php

/*
Plugin Name: Rot13 Words Blacklist
Plugin URI: https://smashingmagazine.com/
Description: A simple plugin that detects and encrypts blacklisted words in ROT13
Version: 1.0
Author: Agbonghama Collins
Author URI: https://w3guy.com
Text Domain: rot13
Domain Path: /lang/
License: GPL2
*/
</code></pre>

As mentioned, the plugin will have a settings page with a <code>textarea</code> field that collects and saves blacklisted words to WordPress’ database (specifically the <code>options</code> table).

Below is a screenshot of what the plugin’s settings (or admin) page will look like.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f3904402-1308-4303-bf0e-ed8649768652/rot13-plugin-settings-page-large-opt.jpg"><img title="Settings page of the plugin." src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1e811853-b393-4534-be0d-8bee780dfee3/rot13-plugin-settings-page-opt.jpg" alt="Settings page of the plugin." width="500" height="273" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f3904402-1308-4303-bf0e-ed8649768652/rot13-plugin-settings-page-large-opt.jpg">See large version</a>)</figcaption></figure>

Now that we know what the options page will look like, let’s build it using WordPress’ <a href="https://codex.wordpress.org/Settings_API">Settings API</a>

### Building the Settings Page

First, we create a submenu item in the main “Settings” menu by using <code>add_options_page()</code>, with its parent function hooked to <code>admin_menu</code> action.</p>

<pre><code class="language-php">
add_action( 'admin_menu', 'rot13_plugin_menu' );

/**
 * Add submenu to main Settings menu
 */
function rot13_plugin_menu() {
	add_options_page(
		__( 'Rot13 Blacklisted Words', 'rot13' ),
		__( 'Rot13 Blacklisted Words', 'rot13' ),
		'manage_options',
		'rot13-words-blacklist',
		'rot13_plugin_settings_page'
	);
}
</code></pre>

The fifth parameter of <code>add_options_page()</code> is the function’s name (<code>rot13_plugin_settings_page</code>), which is called to output the contents of the page.

Below is the code for <code>rot13_plugin_settings_page()</code>.</p>

<pre><code class="language-php">
/**
 * Output the contents of the settings page.
 */
function rot13_plugin_settings_page() {
	echo '&lt;div class="wrap"&gt;';
	echo '&lt;h2&gt;', __( 'Rot13 Blacklisted Words', 'rot13' ), '&lt;/h2&gt;';
	echo '&lt;form action="options.php" method="post"&gt;';
	do_settings_sections( 'rot13-words-blacklist' );
	settings_fields( 'rot13_settings_group' );
	submit_button();
}
</code></pre>

Next, we add a new section to the “Settings” page with <code>add_settings_section()</code>. The <code>textarea</code> field we mentioned earlier will be added to this section with <code>add_settings_field()</code>. Finally, the settings are registered with <code>register_setting()</code>.

Below is the code for <code>add_settings_section()</code>, <code>add_settings_field()</code> and <code>register_setting()</code>.</p>

<pre><code class="language-php">
	// Add the section
	add_settings_section(
		'rot13_setting_section',
		’,
		'rot13_setting_section_callback_function',
		'rot13-words-blacklist'
	);

	// Add the textarea field to the section.
	add_settings_field(
		'blacklisted_words',
		__( 'Blacklisted words', 'rot13' ),
		'rot13_setting_callback_function',
		'rot13-words-blacklist',
		'rot13_setting_section'
	);

	// Register our setting so that $_POST handling is done for us
	register_setting( 'rot13_settings_group', 'rot13_plugin_option', 'sanitize_text_field' );
</code></pre>

The three functions above must be enclosed in a function and hooked to the <code>admin_init</code> action, like so:

<pre><code class="language-php">
/**
 * Hook the Settings API to 'admin_init' action
 */
function rot13_settings_api_init() {
	// Add the section
	add_settings_section(
		'rot13_setting_section',
		’,
		'rot13_setting_section_callback_function',
		'rot13-words-blacklist'
	);

	// Add the textarea field to the section
	add_settings_field(
		'blacklisted_words',
		__( 'Blacklisted words', 'rot13' ),
		'rot13_setting_callback_function',
		'rot13-words-blacklist',
		'rot13_setting_section'
	);

	// Register our setting so that $_POST handling is done for us
	register_setting( 'rot13_settings_group', 'rot13_plugin_option', 'sanitize_text_field' );
}

add_action( 'admin_init', 'rot13_settings_api_init' );
</code></pre>

Lest I forget, here is the code for the <code>rot13_setting_callback_function()</code> and <code>rot13_setting_section_callback_function()</code> functions, which will output the <code>textarea</code> field and the description of the field (at the top of the section), respectively.</p>

<pre><code class="language-php">
/**
 * Add a description of the field to the top of the section
 */
function rot13_setting_section_callback_function() {
	echo '&lt;p&gt;' . __( 'Enter a list of words to blacklist, separated by commas (,)', 'rot13' ) . '&lt;/p&gt;';
}

/**
 * Callback function to output the textarea form field
 */
function rot13_setting_callback_function() {
	echo '&lt;textarea rows="10" cols="60" name="rot13_plugin_option" class="code"&gt;' . esc_textarea( get_option( 'rot13_plugin_option' ) ) . '&lt;/textarea&gt;';
}
</code></pre>

At this point, we are done building the settings page for the plugin.

Up next is getting the plugin to detect blacklisted words and encrypt them with ROT13.</p>

### Detecting Blacklisted Words and Encrypting in ROT13

Here is an overview of how we will detect blacklisted words in a WordPress post:

*   A post’s contents are broken down into individual words and saved to an array (`$post_words`).
*   The blacklisted words that were saved by the plugin to the database are retrieved. They, too, are broken down into individual words and saved to an array (`$blacklisted_words`).
*   We iterate over the `$post_words` arrays and check for any word that is on the blacklist.
*   If a blacklisted word is found, then `str_rot13()` encodes it in ROT13.

It’s time to create the PHP function (<code>rot13_filter_post_content()</code>) that filters the contents of a post and then actually detects blacklisted words and encrypts them in ROT13.

Below is the code for the post’s filter.</p>

<pre><code class="language-php">
/**
 * Encrypt every blacklisted word in ROT13
 *
 * @param $content string post content to filter
 *
 * @return string
 */
function rot13_filter_post_content( $content ) {

	// Get the words marked as blacklisted by the plugin
	$blacklisted_words = esc_textarea( get_option( 'rot13_plugin_option' ) );

    // If no blacklisted word are defined, return the post's content.
	if ( empty( $blacklisted_words ) ) {
		return $content;
	}

	else {

		// Ensure we are dealing with "posts", not "pages" or any other content type.
		if ( is_singular( 'post' ) ) {

			// Confine each word in a post to an array
			$post_words = preg_split( "/\b/", $content );

			// Break down the post's contents into individual words
			$blacklisted_words = explode( ',', $blacklisted_words );

			// Remove any leading or trailing white space
			$blacklisted_words = array_map(
				function ( $arg ) {
					return trim( $arg );
				},

				$blacklisted_words
			);

			// Iterate over the array of words in the post
			foreach ( $post_words as $key =&gt; $value ) {

				// Iterate over the array of blacklisted words
				foreach ( $blacklisted_words as $words ) {

					// Compare the words, being case-insensitive
					if ( strcasecmp( $post_words[ $key ], $words ) == 0 ) {

						// Encrypt any blacklisted word
						$post_words[ $key ] = '&lt;del&gt;' . str_rot13( $value ) . '&lt;/del&gt;';
					}
				}
			}

			// Convert the individual words in the post back into a string or text
			$content = implode( ’, $post_words );
		}

		return $content;
	}
}

add_filter( 'the_content', 'rot13_filter_post_content' );
</code></pre>

While the code above for the <code>filter</code> function is quite easy to understand, especially because it is so heavily commented, I’ll explain a bit more anyway.

The <code>is_singular( 'post' )</code> conditional tag ensures that we are dealing with a post, and not a page or any other content type.

With <code>preg_split()</code>, we are breaking down the post’s contents into individual words and saving them as an array by searching for the RegEx pattern <code>\b</code>, which matches <a href="https://www.regular-expressions.info/wordboundaries.html">word boundaries</a>.

The list of blacklisted words is retrieved from the database using <code>get_option()</code>, with <code>rot13_plugin_option</code> as the option’s name.

From the screenshot of the plugin’s settings page above and the description of the <code>textarea</code> field, we can see that the blacklisted words are separated by commas, our delimiter. The <code>explode</code> PHP function breaks down the blacklisted words into an array by searching for those commas.

A <a href="https://www.smashingmagazine.com/2014/12/encrypting-blacklisted-words-in-wordpress-with-rot13/">closure</a> is applied to the <code>$blacklisted_words</code> array via <code>array_map()</code> that will trim leading and trailing white spaces from the array values (the individual blacklisted words).

The <code>foreach</code> construct iterates over the post’s words and check whether any word is in the array of blacklisted words. Any blacklisted word that gets detected is encrypted in ROT13 and enclosed in a <code>&lt;del&gt;</code> tag.

The <code>$post_words</code> array is converted back to a string or text and subsequently returned.

Finally, the function is hooked to the <code>the_content</code> filter action.

Below is a screenshot of a post with the words “love” and “forever” blacklisted.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/91ca041a-1ab2-437d-9771-64903d763316/post-with-blacklisted-word-opt.jpg"><img title="A post with the blacklisted word love encoded in ROT13" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/91ca041a-1ab2-437d-9771-64903d763316/post-with-blacklisted-word-opt.jpg" alt="A post with the blacklisted word love encoded in ROT13" width="427" height="546" /></a></figure>

## Wrapping Up

ROT13 is a simple encryption technique that can be easily decrypted. Thus, you should never use it for serious data encryption.

Even if you don’t end up using the plugin, the concepts you’ve learned in creating it can be applied to many situations, such as obfuscating or encrypting inappropriate words (such as profanities) in ROT13, which would be a nice feature in a forum where people have the freedom to post anything.

Hopefully, you have learned a thing or two from this tutorial. If you have any question or a contribution, please let us know in the comments.

{{< signature "dp, al, il" >}}

<em>Front page image credit: <a href="https://en.wikipedia.org/wiki/Caesar_cipher">Wikipedia</a>.</em>

