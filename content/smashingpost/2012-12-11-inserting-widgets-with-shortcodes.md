---
title: Inserting Widgets With Shortcodes
slug: inserting-widgets-with-shortcodes
image: 'https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/39bd8b27-7eee-44dd-8d09-070d040973ab/illu-wp-14.jpg'
date: 2012-12-11T14:05:56.000Z
author: daniel-pataki
description: >-
  The shortcode ability of WordPress is extremely underrated. It enables the end
  user to create intricate elements with a few keystrokes while also
  modularizing editing tasks. In a new theme we're developing, I decided to look
  into adding widgets anywhere with shortcodes and it turns out that it isn't
  that difficult.
categories:
  - WordPress
  - Widgets
  - Shortcodes
  - Techniques (WP)
---
The shortcode ability of WordPress is extremely underrated. It enables the end user to create intricate elements with a few keystrokes while also modularizing editing tasks. In a new theme we're developing, I decided to look into adding widgets anywhere with shortcodes, and it turns out that it isn't that difficult.

<img loading="lazy" decoding="async" class="107888" title="Some of the widgets that can be added with shortcodes." src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/871a024c-3cb5-40a5-a29d-38dfabba6c13/insertingwidgets-500.jpg" alt="Some of the widgets that can be added with shortcodes." width="500" height="337" /><br>
<em>Some of the widgets that can be added with shortcodes.</em>

This tutorial is for experienced WordPress users; we will be looking at the widgets object and shortcodes without delving into too much detail about how and why they work. If you are looking for more information, I suggest reading <a href="https://www.smashingmagazine.com/2009/02/02/mastering-wordpress-shortcodes/">Mastering WordPress Shortcodes</a> and the <a href="https://codex.wordpress.org/Widgets_API">Widgets API</a> article in the Codex.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [WordPress Shortcodes: A Complete Guide](https://www.smashingmagazine.com/2012/05/wordpress-shortcodes-complete-guide/)
*   [Mastering WordPress Shortcodes](https://www.smashingmagazine.com/2009/02/mastering-wordpress-shortcodes/)
*   [WordPress Functions To Make Blogging Easier](https://www.smashingmagazine.com/2013/06/five-wordpress-functions-blogging-easier/)

{{% feature-panel %}}

## Grabbing A Random Widget

The first thing I looked into was how to output any widget without shortcodes. Once done, implementing a shortcode is a relatively trivial matter. Digging around in the Codex, I found the <a href="https://codex.wordpress.org/Function_Reference/the_widget"><code>the_widget()</code></a> function, which does just what I want.

It takes three parameters:

*   The widget's class name,
*   The widget's instance settings,
*   The widget's sidebar arguments.

Once I saw this, my face lit up. Not only can I output a widget anywhere, but I can pass different sidebar arguments to any widget. This is great because I can specify parameters such as <code>before_widget</code> and <code>after_widget</code>.

This also opens up the possibility of easily changing the style of the widget from within the shortcode, but more on that later.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7023be8a-c568-4669-b3f2-0f8a59c7438e/calendarwidget.png"><img title="After applying some CSS, the calendar widget can be added anywhere." src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7023be8a-c568-4669-b3f2-0f8a59c7438e/calendarwidget.png" alt="After applying some CSS, the calendar widget can be added anywhere." width="366" height="366" /></a><br>
<em>After applying some CSS, the calendar widget can be added anywhere.</em>

## Output Buffering

When adding a shortcode, you scan the text for a particular string, do something with it and return the result you want to see. It's obvious that we will be using <code>the_widget()</code>, but that function only echoes content. To get around this problem we'll be using output buffering.

Take a look at the following two examples; the result is exactly the same.

<pre><code class="language-php">the_widget( 'WP_Widget_Archives' );</code></pre>

<pre><code class="language-php">ob_start();
the_widget( 'WP_Widget_Archives' );
$contents = ob_get_clean();
echo $contents;</code></pre>

First we start our buffer. From this point on, anything that is echoed goes into our buffer instead of actually being echoed. By using <code>ob_get_clean()</code>, we can pull the contents of the buffer into a variable (and also clear the buffer). Once this is done we can echo that variable, or pass it on by returning it if we're in a function.

## Creating The Shortcode

Now we know everything we need, so let's create the skeleton of our shortcode. First we need to figure out what arguments we need to pass, and what arguments we want to allow the user to pass via the shortcode tag.

*   Widget type – Which widget do we want to show;
*   Title – The title of the widget (used in the instance parameter);
*   Other instance parameters;
*   Other sidebar arguments.

I'll admit that this is a bit vague. The reason is that each widget will need a separate set of possible arguments due to the varied functionality they have. For an archive widget, we can specify whether or not we want the post count. For a category widget, we could also specify the hierarchical attribute.

Solving this problem requires a flexible shortcode, and good end-user documentation.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2e824da4-9724-4bbb-8dd0-71d9a339b770/docs.png"><img title="The best way to make sure the shortcode is used properly is to provide good documentation." src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2861789d-20a8-4db6-b29b-7cee88df379a/docs-500.jpg" alt="The best way to make sure the shortcode is used properly is to provide good documentation." width="500" height="350" /></a><br>
<em>The best way to make sure the shortcode is used properly is to provide good documentation.</em>

### The Shortcode Skeleton

<pre><code class="language-php">add_shortcode( 'widget', 'my_widget_shortcode' );
function my_widget_shortcode( $atts ) {

// Configure defaults and extract the attributes into variables
extract( shortcode_atts(
	array(
		'type'  =&gt; ’,
		'title' =&gt; ’,
	),
	$atts
));

$args = array(
	'before_widget' =&gt; '&lt;div class="box widget"&gt;',
	'after_widget'  =&gt; '&lt;/div&gt;',
	'before_title'  =&gt; '&lt;div class="widget-title"&gt;',
	'after_title'   =&gt; '&lt;/div&gt;',
);

ob_start();
the_widget( $type, $atts, $args );
$output = ob_get_clean();

return $output;</code></pre>

There are two common attributes all shortcodes will have. The type is where the user will specify the widget type, and the title is where the user specifies the title (no surprises there).

Once we have our <code>$atts</code>, we figure out the <code>$args</code> — the widget's sidebar parameters. Since this is a commercial theme, we don't need to give the user control over these arguments, so they are just hard coded for now.

In the final section we'll put it all together to create the final widget.</p>

### Extending the Shortcode

Once this is done we can get crazy with our shortcode parameters. One example is allowing the user to pick a scheme. For our example, this is dark or light, but you could easily specify an exact color.

All we need to do is add an argument to the shortcode, add a CSS class to our widget based on this argument and let our style sheet do the rest.

<pre><code class="language-php">add_shortcode( 'widget', 'my_widget_shortcode' );

function my_widget_shortcode( $atts ) {

// Configure defaults and extract the attributes into variables
extract( shortcode_atts(
	array(
		'type'   =&gt; ’,
		'title'  =&gt; ’,
		'scheme' =&gt; 'light'
	),
	$atts
));

$args = array(
	'before_widget' =&gt; '&lt;div class="box widget scheme-' . $scheme . ' "&gt;',
	'after_widget'  =&gt; '&lt;/div&gt;',
	'before_title'  =&gt; '&lt;div class="widget-title"&gt;',
	'after_title'   =&gt; '&lt;/div&gt;',
);

ob_start();
the_widget( $type, $atts, $args );
$output = ob_get_clean();

return $output;</code></pre>

If you need to make this even more flexible, you can allow a background color to be specified, you can add the <code>$args</code> using parameters from the shortcode, and <strong>much</strong> more.

This solution works perfectly with custom widgets as well. All you need to do is add the class name as the type and accommodate for its specific instance settings

## Conclusion

By now you should be on your way to creating wonderful things with this shortcode. It is great for end users and also a very useful tool to test widgets before releasing a theme.

We use this in our themes to make them even more flexible for our users. The ability to put anything anywhere, easily, is one that all themes should have!

{{< signature "cp" >}}

