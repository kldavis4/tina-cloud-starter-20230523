---
title: How To Create A Tab Widget In WordPress
slug: create-tabber-widget-wordpress
image: >-
  https://www.smashingmagazine.com/general/2014/03/25/183835-revision-6/attachment/create-tabber-widget-splash/
date: 2013-04-04T09:21:41.000Z
author: milan-petrovic
description: >-
  In this tutorial, you’ll learn how to create the Tabber widget, which is very
  useful for when multiple widgets need to fit in a sidebar. It saves space and
  streamlines the appearance and functionality of your WordPress-powered
  website.
categories:
  - WordPress
  - Widgets
  - Techniques (WP)
---
In this tutorial, you'll learn how to create the Tabber widget, which is very useful for when multiple widgets need to fit in a sidebar. It <strong>saves space and streamlines the appearance</strong> and functionality of your WordPress-powered website.

In the past, there were different methods of doing this, most of which were theme-dependent. As we'll see in this tutorial, creating a tabbed widget that works on its own and with any theme is easily accomplished. So, let's jump in and learn how to create our own Tabber widget, which we’ve made available for downloading at the end of this article.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/115ae5b5-5d5c-44c5-b88e-30b16e6989c9/create-tabber-widget-splash.png"><img loading="lazy" decoding="async" class="108415" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/115ae5b5-5d5c-44c5-b88e-30b16e6989c9/create-tabber-widget-splash.png" alt="create-tabber-widget-splash" width="500" height="333" /></a>

## Saving Sidebar Space

The main advantage of tabs is that you can fit more widgets into the sidebar. And tabs look good. The image below shows how much vertical space is taken up by three standard widgets (using the default Twenty Ten theme). The default layout is on the left, and our tabber widget is on the right:

{{% feature-panel %}}

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fc06daaf-c888-4918-b230-0b35325cb982/tabber-example.png"><img loading="lazy" decoding="async" class="108407" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fc06daaf-c888-4918-b230-0b35325cb982/tabber-example.png" alt="tabber_example" width="560" height="350" /></a>

## Before We Start

A few things are useful to know. Because we are building a widget in this article, you might want to learn about WordPress’ Widgets API and how to create a basic widget:

*   “[Widgets API](https://codex.wordpress.org/Widgets_API),” WordPress Codex
*   “[Creating Widgets for WordPress 2.8](https://azuliadesigns.com/creating-widgets-wordpress-28/),” Tim Trott, Azulia Designs
*   “[Advanced WordPress Widgets](https://www.wproots.com/advanced-wordpress-widgets/),” WP Roots

Use these resources as needed while following the tutorial along.</p>

## The Basic Idea

The idea for this widget is simple: <strong>select a sidebar</strong>, and the Tabber widget will grab all of its widgets and display them as tabs. In the widget’s interface, you can select a sidebar, specify an extra CSS class and optionally apply your own styles. When enabled, the plugin will register an extra sidebar (which may be removed if you have other ways to add a sidebar). Then, using the same code, you can add more sidebars, and each of them can hold instances of the Tabber widget.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [How To Speed Up Your WordPress Website](https://www.smashingmagazine.com/2014/06/how-to-speed-up-your-wordpress-website/)
*   [A Look At The Modern WordPress Server Stack](https://www.smashingmagazine.com/2016/05/modern-wordpress-server-stack/)
*   [Secrets Of High-Traffic WordPress Blogs](https://www.smashingmagazine.com/2012/09/secrets-high-traffic-wordpress-blogs/)
*   [A Beginner’s Guide To Creating A WordPress Website](https://www.smashingmagazine.com/2016/02/beginners-guide-creating-wordpress-website/)

To control your widgets, Tabber uses <a href="https://www.sunsean.com/idTabs/">idTabs</a> for jQuery, created by Sean Catchpole, but you could always use another solution. Note that additional CSS is loaded to style the resulting widget.

Here is the basic HTML structure required to create tabs:

<pre><code class="language-markup tmp-html">
&lt;ul&gt;
  &lt;li&gt;&lt;a href="#widget-1"&gt;Widget one&lt;/a&gt;&lt;/li&gt;
  &lt;li&gt;&lt;a href="#widget-2"&gt;Widget two&lt;/a&gt;&lt;/li&gt;
&lt;ul&gt;
&lt;div id="widget-1"&gt;
  Widget one's content
&lt;/div&gt;
&lt;div id="widget-2"&gt;
  Widget two's content
&lt;/div&gt;
</code></pre>

Unfortunately, you can't get such a structure directly by using WordPress’ sidebar and widget rendering. Typically, WordPress’ widget structure looks like this:

<pre><code class="language-markup tmp-html">
&lt;div id="widget-1"&gt;
  &lt;h2&gt;Widget one&lt;/h2&gt;
  Widget one's content
&lt;/div&gt;
&lt;div id="widget-2"&gt;
  &lt;h2&gt;Widget two&lt;/h2&gt;
  Widget two's content
&lt;/div&gt;
</code></pre>

So, the goal with Tabber is to <strong>transform any widget’s output into markup that can be used to display tabs</strong>. To complicate matters, different themes might register sidebars that do not use a <code>&lt;div&gt;</code> to hold a widget or use <code>&lt;h2&gt;</code> to show its title. For example, WordPress’ new default theme, Twenty Twelve, uses <code>&lt;aside&gt;</code> and <code>&lt;h3&gt;</code> tags for this. Other themes may use complicated markup that can't be predicted or successfully transformed into the output needed for tabs.

The solution to this problem is to intercept the widget’s parameters before rendering, and then to restructure them into useful structures using JavaScript or jQuery for the tabbed output. More on that later.</p>

## Tabber Widget Loading

Now that we understand the goal, let's look at the demo plugin. Our plugin contains a main PHP file, one JavaScript file and one CSS file. The PHP file contains the widget and loads the CSS and JavaScript, like so:

<pre><code class="language-php">
add_action('init', 'd4p_st_init');
add_action('widgets_init', 'd4p_st_widgets_init');

function d4p_st_init() {
    register_sidebar(array('name' =&gt; 'Tabber Example Sidebar', 'description' =&gt; 'Add widgets to this sidebar to use it from Tabber widget.'));

    if (!is_admin()) {
        $url = plugins_url('d4p-smashing-tabber');

        wp_enqueue_script('jquery');
        wp_enqueue_script('d4p_st_tabber', $url.'/tabber.js', array('jquery'));
        wp_enqueue_style('d4p_st_tabber', $url.'/tabber.css');
    }
}

function d4p_st_widgets_init() {
    register_widget('d4p_sr_tabber');
}
</code></pre>

Here, the function <code>d4p_st_init</code> is run during WordPress’ <code>init</code> action. It will register one sidebar (line 5) and enqueue the jQuery, JavaScript and CSS files using the <code>wp_enqueue_script</code> and <code>wp_enqueue_style</code> functions (lines 10 to 12).

Then, the function <code>d4p_st_widgets_init</code> is called during WordPress’ <code>widgets_init</code> action. We register the widget on line 17.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7ec85d16-ef03-4d6a-bc4f-9ee08184b8a3/tabber-widget.png"><img class="108410" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7ec85d16-ef03-4d6a-bc4f-9ee08184b8a3/tabber-widget.png" alt="Widget Interface" width="252" height="228" /></a><br>
<em>Widget interface.</em>

## The Main Tabber Widget Class

Tabber is a normal widget, and in this case it is located in the <code>d4p_sr_tabber</code> class.</p>

### Settings: Plugin Interface

The widget has two settings:

*   “sidebar” to hold the ID of the selected sidebar
*   “css” for extra CSS classes to style the Tabber widget

When selecting which sidebar to use, you must <strong>avoid using the sidebar that holds the Tabber widget</strong>. Otherwise, it will spin into endless recursion. To avoid this, before rendering the widget’s content, check whether the selected sidebar is the same as the parent sidebar. This can't be prevented while the widget is set up, because the widget's panel affords very little control over this.

Also, using sidebars that are not normally used is a good idea. To help with this, the plugin includes sample code to help you add an extra sidebar.

The <code>form</code> and <code>update</code> methods contained in the <code>d4p_sr_tabber</code> class are used to display the widget’s interface in the “Widgets” panel and to save its settings, and they are not that interesting. But it is worth taking a closer look at how to display the widget on the front end.</p>

### Main Display Method

Here is the main <code>widget</code> method:

<pre><code class="language-php">
public function widget($args, $instance) {
  add_filter('dynamic_sidebar_params', array(&amp;$this, 'widget_sidebar_params'));

  extract($args, EXTR_SKIP);
  $this-&gt;id = $widget_id;

  echo $before_widget;
  if ($args['id'] != $instance['sidebar']) {
    echo '&lt;div id="'.$widget_id.'"&gt;';
    echo '&lt;ul&gt;&lt;/ul&gt;';
    dynamic_sidebar($instance["sidebar"]);
    echo '&lt;/div&gt;';
  } else {
    echo 'Tabber widget is not properly configured.';
  }
  echo $after_widget;

  remove_filter('dynamic_sidebar_params', array(&amp;$this, 'widget_sidebar_params'));
}
</code></pre>

In this code, line 2 adds a filter that modifies the widget’s rendering parameters before they are processed. With this filter, all widgets rendered after that point will have their parameters modified as needed for successful transformation to tabbed form. And that will be done for the widgets in the selected sidebar on line 11, using the <code>dynamic_sidebar</code> function.

This function requires the name of the sidebar, and it will display all widgets in it. Line 9 contains the check mentioned before, to prevent recursion when displaying sidebar content if the selected sidebar is the same as the parent sidebar.

Lastly, the filter is removed, and any widgets belonging to other sidebars are displayed normally, without modification.</p>

### Widget Modification

To prepare for the transformation done with JavaScript, the tabber widget includes the <code>d4p-tabber-widget</code> class, which contains an empty <code>&lt;ul&gt;</code> tag.

The filter used to modify the widget’s parameters looks like this:

<pre><code class="language-php">
public function widget_sidebar_params($params) {
  $params[0]['before_widget'] = '&lt;div id="'.$params[0]['widget_id'].'"&gt;';
  $params[0]['after_widget'] = '&lt;/div&gt;';
  $params[0]['before_title'] = '&lt;a href="#"&gt;';
  $params[0]['after_title'] = '&lt;/a&gt;';

  return $params;}
</code></pre>

Depending on how the sidebar is registered, this code will change the rendering parameters to a format that is close to the format needed for tabs. But JavaScript is still needed to move the widget's title into the <code>&lt;ul&gt;</code> tag for the control tabs. After this filter, the widget’s output will look like this:

<pre><code class="language-markup tmp-html">
&lt;div id="widget-1"&gt;
  &lt;a href="#"&gt;Widget one&lt;/a&gt;
  Widget one's content
&lt;/div&gt;
</code></pre>

## JavaScript For Widget Transformation

Once the widget’s presentation is modified, one thing remains: to complete the transformation and get the titles from the widgets and turn them into tabs:

<pre><code class="language-javascript">jQuery(document).ready(function(){
  jQuery(".d4p-tabber-widget").each(function(){
  var ul = jQuery(this).find("ul.d4p-tabber-header");

  jQuery(this).children("div.d4p-st-tab").each(function() {
    var widget = jQuery(this).attr("id");
    jQuery(this).find('a.d4p-st-title').attr("href", "#" + widget).wrap('&lt;li&gt;&lt;/li&gt;').parent().detach().appendTo(ul);
  });

  jQuery(this).idTabs();
  });
});
</code></pre>

This code uses jQuery to get all of the Tabber widgets based on the <code>.d4p-tabber-widget</code> CSS class, and each one gets the element (where the tabs will go):

*   With line 5, we find all individual widgets belonging to the Tabber widget.
*   On line 6, we get the widget’s ID needed for the tab to connect it to the widget's content.
*   On line 7, we find the title `<a>` element, set its `href` attribute to that of the widget’s ID, wrap it in a `</li>` element, remove it from its current location, and move it into the tab’s `<ul>` element.
*   After this, the `<div>` will hold only its content.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9920dde1-1221-4589-a401-50925e668bd7/tabber-example-final.png"><img class="108409" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9920dde1-1221-4589-a401-50925e668bd7/tabber-example-final.png" alt="Final Tabber Example" width="242" height="137" /></a><br>
<em>Final Tabber example.</em>

Finally, when all this is done, we enable idTabs to activate the tabs control. And with the default styling loaded from the <code>tabber.css</code> file, you can see how Tabber looks with three widgets in it (see screenshot above). Feel free to experiment and adjust the styling to your theme.</p>

## How To Install The Tabber Plugin

*   [Download version 1.0.0 of the Tabber plugin.](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ce9d6c1f-a24c-41c7-b956-6bcbe90fffa5/d4p-smashing-tabber.1)

As with any other plugin, unpack it, upload it to WordPress’ plugins folder, and activate it from the plugins panel. When you go to the “Widgets” panel, you will see an additional sidebar, “Tabber Example Sidebar,” at the end on the right. And “Available Widgets” will show one more widget, “D4P Smashing Tabber.”

Add this new widget to the “Main Sidebar.” From the “Sidebar” widget drop-down menu, select “Tabber Example Sidebar,” and save the widget. Now, open the “Tabber Example Sidebar” and add the widgets you want to be displayed as tabs. You can add as many widgets as you want, but pay attention because if you add too many, the tab’s control will break to two or more lines, and it will not look pretty. Starting with two or three widgets is best.</p>

## Conclusion

Creating one widget to display several other widgets as a tab isn't very difficult, as you can see. The trick is in adjusting the widgets’ output to a format that can be transformed into tabs, and then using JavaScript to display them. We’ve explored just one possible transformation method; you can always experiment with ways to rearrange widget elements.

We used idTabs here, but there are many methods of displaying tabs, and not all of them require JavaScript:

*   [idTabs](https://www.sunsean.com/idTabs/)
*   [EasyTabs](https://os.alfajango.com/easytabs/)
*   [jQueryUI Tabs](https://jqueryui.com/tabs/)
*   Tabify

I prefer using a jQuery-based solution, and idTabs is very easy to use and easy to style and it works in all browsers. Check out other solutions, and see what extra features they offer to enhance your own tabbed widgets.

{{< signature "al" >}}

