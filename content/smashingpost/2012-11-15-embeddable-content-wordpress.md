---
title: How To Create An Embeddable Content Plugin For WordPress
slug: embeddable-content-wordpress
image: >-
  https://www.smashingmagazine.com/general/2014/02/20/180051-revision-120/attachment/wordpress-embed-opt/
date: 2012-11-15T11:49:52.000Z
author: sameer-borate
summary: >-
  WordPress is one of the most deployed content management systems around. One of the main reasons is the number of plugins available and the ease with which we can use the system. It is not uncommon to find websites using tens of plugins to accomplish various tasks and functions. Wouldn’t it be nice if you could share your site content with other websites?
description: >-
  WordPress is one of the most deployed content management systems around. One of the main reasons is the number of plugins available and the ease with which we can use the system.
categories:
  - WordPress
  - Plugins
  - Widgets
  - Techniques (WP)
---
You may have a need to share advertisements, product information or, if you are a designer, your photo gallery. Whatever the reason, this article will show you a way to create an embeddable content plugin to share your WordPress content with other websites.

There are various ways with which one can share content across websites: RSS and Atom feeds, APIs and embeddable widgets. RSS feeds on WordPress are usually restricted to posts, while APIs are not easy to integrate on other websites without adding some extra code. This leaves us with embeddable widgets, like the ones used by Google AdSense to display advertisements on websites or Facebook “Share” and “Like” buttons &mdash; all of these rely on embeddable JavaScript code to display specific content on a website.

The idea mentioned in this article is certainly not new, but in the context of WordPress it opens up many possibilities. The advantages of the technique mentioned here compared with others is that it will enable you to share almost any content, even content from other plugins on your blog, with other websites.

Our goal in this article is to create widget code that a user could insert in their website to display a list of recent posts from the parent website. Of course, this can also be easily accomplished using RSS, but this is just an example to show the technique. In reality, you would use it for more interesting purposes, like sharing popular product images if you are running a WordPress e-commerce website.

{{% feature-panel %}}

## The Widget Code

The embeddable code will look something like the following. This is the code the user will insert into their webpage, which will allow them to display the content from the parent website. The crucial element of this widget is the <code>wp-widget.js</code> file, which calls the remote WordPress website, gets the content and embeds it as an iframe in the calling page.

<pre><code class="language-markup">&lt;script type="text/javascript"&gt;
  var widget_embed = 'posts';
&lt;/script&gt;
&lt;script src="https://www.example.com/widget/wp-widget.js"
type="text/javascript"&gt;
&lt;/script&gt;
&lt;div id="embed-widget-container"&gt;&lt;/div&gt;</code></pre>

Adding this block of code to any website page will display the list of recent posts from <code>example.com</code>. The content can be anything besides posts &mdash; images, comments, tags, data from other plugins &mdash; anything you as a WordPress website owner would like to share with other people. For this example, I’ve limited the content to a simple posts list, as this is a common denominator across all WordPress websites and will be easy to start with. Of course, you will need to add some extra code to share other content, but the base plugin skeleton will remain the same.

## Creating The Plugin

The fist step in creating an embeddable widget is to design a small WordPress plugin that will intercept the widget calls from another website and return the required data. You may be thinking that this will be a knotty job, but nothing could be easier. Just a few lines of code and our plugin is ready. The complete code for the plugin is shown below. I’ll explain how this works as we proceed along.

To get the content from the plugin, we will need to pass a query parameter of what content we would like from the remote server in the <code>em_embed</code> variable. This query parameter will then be intercepted by the plugin and the corresponding content returned. We will also pass along implicitly the domain URL of the calling page, so we can later use it for analytics purposes or for restricting the websites which can embed our widget.

For example, to get the list of recent posts, we need to send a <code>GET</code> query to the main WordPress website as shown below. Of course this query will be created by our JavaScript widget, <code>wp-widget.js</code>.

<pre><code class="language-markup">https://www.example.com/?em_embed=posts</code></pre>

The complete code for the plugin is given below.

<div class="break-out">

 <pre><code class="language-php">&lt;?php

/&#42;&#42;
 &#42; Plugin Name: WordPress Widget Embed
 &#42; Description: Allow people to embed WordPress content in an iframe on other websites
 &#42; Version: 1.0
 &#42; Author: Sameer Borate
 &#42; Author URI: https://www.codediesel.com
 &#42;/

class WPWidgetEmbed  
{
    public function &#95;&#95;construct()
    {
        add_action('template_redirect', array($this, 'catch_widget_query'));
        add_action('init', array($this, 'widget_add_vars'));
    }

    /&#42;&#42;
     &#42; Adds our widget query variable to WordPress $vars
     &#42;/
    public function widget_add_vars() 
    { 
        global $wp; 
        $wp-&gt;add_query_var('em_embed'); 
        $wp-&gt;add_query_var('em_domain'); 
    }

    private function export_posts()
    {
        $outstring  = '&lt;html&gt;';
        $outstring .= '&lt;head&gt;&lt;style&gt;';
        $outstring .= 'ul {
                padding:0;
                margin:0;
              }
              li {
                 list-style-type:none;
               }';
        $outstring .= '&lt;/style&gt;&lt;/head&gt;&lt;body&gt;';

        /* Here we get recent posts for the blog */
        $args = array(
            'numberposts' =&gt; 6,
            'offset' =&gt; 0,
            'category' =&gt; 0,
            'orderby' =&gt; 'post_date',
            'order' =&gt; 'DESC',
            'post_type' =&gt; 'post',
            'post_status' =&gt; 'publish',
            'suppress_filters' =&gt; true
        );

        $recent_posts = wp_get_recent_posts($args);

        $outstring .= '&lt;div class="widget-posts"&gt;&lt;ul&gt;';
        foreach($recent_posts as $recent)
        {
            $outstring .= '&lt;li&gt;&lt;a target="_blank" href="' . get_permalink($recent["ID"]) . '"&gt;' . $recent["post_title"]. '&lt;/a&gt;&lt;/li&gt;';
        }

        $outstring .= '&lt;/ul&gt;&lt;/div&gt;';
        $outstring .= '&lt;/body&gt;&lt;/html&gt;';

        return $outstring;
    }

    /**
     &#42; Catches our query variable. If it’s there, we’ll stop the
     &#42; rest of WordPress from loading and do our thing, whatever 
     &#42; that may be.

     &#42;/
    public function catch_widget_query()
    {
        /&#42; If no 'embed' parameter found, return &#42;/
        if(!get_query_var('em_embed')) return;

        /&#42; 'embed' variable is set, export any content you like &#42;/

        if(get_query_var('em_embed') == 'posts')
        { 
            $data_to_embed = $this-&gt;export_posts();
            echo $data_to_embed;
        }

        exit();
    }
}

$widget = new WPWidgetEmbed();

?&gt;
</code></pre>
</div>

To successfully intercept calls from another website, we need to first add the <code>em_embed</code> and <code>em_domain</code> parameters to our WordPress <code>query_var</code> variable. This will be used later to see what kind of data needs to be sent to the remote website. This is done by the following function.

<pre><code class="language-php">public function widget_add_vars() 
{ 
    global $wp; 
    $wp-&gt;add_query_var('em_embed'); 
    $wp-&gt;add_query_var('em_domain');
}</code></pre>

Next, we will need to catch the query variable on the <code>template_redirect</code> hook and process any data if the <code>em_embed</code> variable is set in the global variable.

<div class="break-out">

 <pre><code class="language-php">public function catch_widget_query()
{
    /* If no 'embed' parameter found, return */
    if(!get_query_var('em_embed')) return;

    /* 'embed' variable is set, export any content you like */

    if(get_query_var('em_embed') == 'posts')
    { 
        $data_to_embed = $this-&gt;export_posts();
        echo $data_to_embed;
    }

    exit();
}</code></pre>
</div>

In our example, we will be exporting a list of recent post titles, so our <code>export_posts</code> function will look like below.

<div class="break-out">

 <pre><code class="language-php">private function export_posts()
{
    $outstring  = '&lt;html&gt;';
    $outstring .= '&lt;head&gt;&lt;style&gt;';
    $outstring .= 'ul {
             padding-left:10px;
             margin:0;
          }

          li &gt; a {
             text-decoration: none;
             font-family: Arial, Helvetica, Sans-serif;
             font-size:12px;

          }

          li {
             border-bottom: 1px solid #c0c0c0;
             padding: 3px 0 3px 0;
          }

          .widget-posts {
             width: 250px;
             border: 1px solid #c0c0c0;
             padding: 12px;
             margin-left: 3px;
          }';
    $outstring .= '&lt;/style&gt;&lt;/head&gt;&lt;body&gt;';

    /* Here we get recent posts for the blog */
    $args = array(
        'numberposts' =&gt; 6,
        'offset' =&gt; 0,
        'category' =&gt; 0,
        'orderby' =&gt; 'post_date',
        'order' =&gt; 'DESC',
        'post_type' =&gt; 'post',
        'post_status' =&gt; 'publish',
        'suppress_filters' =&gt; true
    );

    $recent_posts = wp_get_recent_posts($args);

    $outstring .= '&lt;div id="widget-posts"&gt;&lt;ul&gt;';
    foreach($recent_posts as $recent)
    {
        $outstring .= '&lt;li&gt;&lt;a target="_blank" href="' . get_permalink($recent["ID"]) . '"&gt;' . $recent["post_title"]. '&lt;/a&gt;&lt;/li&gt;';
    }

    $outstring .= '&lt;/ul&gt;&lt;/div&gt;';
    $outstring .= '&lt;/body&gt;&lt;/html&gt;';

    return $outstring;
}</code></pre>
</div>

This is all there is to the plugin. If you need to export any other data, you will need to replace the code for getting posts with code for getting the data you like.

{{% ad-panel-leaderboard %}}

## Writing The Embeddable Widget Code

We have now completed only the part for the WordPress plugin. We still have to write the JavaScript embed code which will remotely access our website and insert the appropriate content into the calling page. The easiest way to display content from another website into your Web page is by using an iframe. The code needed to embed the content on a website is shown below.

<pre><code class="language-markup tmp-html">&lt;script type="text/javascript"&gt;
  var widget_embed = 'posts';
&lt;/script&gt;
&lt;script src="https://www.example.com/widget/wp-widget.js"
type="text/javascript"&gt;
&lt;/script&gt;
&lt;div id="embed-widget-container"&gt;&lt;/div&gt;</code></pre>

If you are going to use the widget for returning only a single type of data,you can do away with the <code>widget_embed</code> variable. So you will have something like the following.

<pre><code class="language-markup tmp-html">&lt;script src="https://www.example.com/widget/wp-widget.js"
type="text/javascript"&gt;
&lt;/script&gt;
&lt;div id="embed-widget-container"&gt;&lt;/div&gt;</code></pre>

<code>wp-widget.js</code> is the JavaScript that does all the work of calling the remote WordPress website and adding the content to the iframe. You need to place the <code>wp-widget.js</code> file in a subdirectory on your WordPress website; the exact name and location does not matter.

The complete code for the <code>wp-widget.js</code> is shown below, and is self-explanatory.

<div class="break-out">

 <pre><code class="language-javascript">/**
  * wp-widget.js
  *
  * Inserts an iframe into the DOM and calls the remote embed plugin
  * via a get parameter:
  * e.g https://www.example.com/?embed=posts
  * This is intercepted by the remote 'WordPress Widget Embed' plugin
  *
  */

(function() {

// Localize jQuery variable
var jQuery;

/&#42; Load jQuery if not present &#42;/
if (window.jQuery === undefined || window.jQuery.fn.jquery !== '1.7.2') 
{
    var script_tag = document.createElement('script');
    script_tag.setAttribute("type","text/javascript");
    script_tag.setAttribute("src",
        "https://ajax.googleapis.com/ajax/libs/jquery/1.7.2/jquery.min.js");
    if (script_tag.readyState) 
    {
      script_tag.onreadystatechange = function () 
      { // For old versions of IE
          if (this.readyState == 'complete' || this.readyState == 'loaded') 
          {
              scriptLoadHandler();
          }
      };
    } 
    else 
    {
      script_tag.onload = scriptLoadHandler;
    }

    (document.getElementsByTagName("head")[0] || document.documentElement).appendChild(script_tag);
} 
else 
{
    // The jQuery version on the window is the one we want to use
    jQuery = window.jQuery;
    main();
}

/&#42; Called once jQuery has loaded &#42;/
function scriptLoadHandler() 
{
    jQuery = window.jQuery.noConflict(true);
    main(); 
}

/&#42; Our Start function &#42;/
function main() 
{ 
    jQuery(document).ready(function($) 
    { 
        /&#42; Get 'embed' parameter from the query &#42;/
        var widget = window.widget_embed;
        var domain = encodeURIComponent(window.document.location);

        /&#42; Set 'height' and 'width' according to the content type &#42;/
        var iframeContent = '&lt;iframe style="overflow-y: hidden;" 
                             height="550" width="400" frameborder="0" 
                             border="0" cellspacing="0" scrolling="no" 
                             src="https://www.example.com/?em_embed=' + widget + '&amp;em_domain=' + domain + '"&gt;&lt;/iframe&gt;';

        $("#embed-widget-container").html(iframeContent);
    });
}

})();
</code></pre>
</div>

The task of inserting the iframe and the WordPress content in the DOM is accomplished by the <code>main()</code> function. The iframe size needs to be changed depending on your requirements or created dynamically by letting the user pass additional parameters along with the <code>widget_embed</code> variable in the main widget code.

## Adding Custom CSS To The Content

You can also add custom CSS to the displayed content through the plugin. Sample CSS to go with the above plugin is given below. You can also specify a style sheet URL if needed.

<pre><code class="language-php">private function export_posts()
{
    $outstring  = '&lt;html&gt;';
    $outstring .= '&lt;head&gt;&lt;style&gt;';
    $outstring .= 'ul {
             padding-left:10px;
             margin:0;
          }

          li &gt; a {
             text-decoration: none;
             font-family: Arial, Helvetica, Sans-serif;
             font-size:12px;
          }

          li {
             border-bottom: 1px solid #c0c0c0;
             padding: 3px 0 3px 0;
          }

          .widget-posts {
             width: 250px;
             border: 1px solid #c0c0c0;
             padding: 12px;
             margin-left: 3px;
          }';
    $outstring .= '&lt;/style&gt;&lt;/head&gt;&lt;body&gt;';
    .
    .</code></pre>

The type of CSS you add to the content will depend on what content you are displaying. With a little creative coding, you can also allow the user to add certain display options to the widget with which they can control the display style of the embedded widget.

{{% ad-panel-leaderboard %}}

## Restricting Display To Certain Domains

You may want to allow only certain domains to be able to display your content using the widget. This can easily be made possible, as we already have the calling website’s url in the <code>em_domain</code> variable. All we have to do is check the domain and selectively allow the content to be displayed.

<div class="break-out">

 <pre><code class="language-php">public function catch_widget_query()
{
    /* If no 'embed' parameter found, return */
    if(!get_query_var('em_embed')) return;

    /* 'embed' variable is set, export any content you like */

    if(get_query_var('em_embed') == 'posts')
    { 
        $allowed_domains = array('site1.com',
                                 'site2.com',
                                 'site3.com');

        $calling_host = parse_url(get_query_var('em_domain'));

        /* Check if the calling domain is in the allowed domains list */
        if(in_array($calling_host['host'], $allowed_domains))
        {
            $data_to_embed = $this-&gt;export_posts();
            echo $data_to_embed;
        }
        else
        {
            echo "Domain not registered!";
        }
    }

    exit();
}
</code></pre>
</div>

## Performance Concerns

Allowing other websites to access your content via widgets means additional load on your servers. A few hundred websites using your widget could easily slow down your server, so take this factor into consideration when promoting widgets. However, plugins like WP Super Cache can be used to cache widget data and reduce server load. If you are not using WP Super Cache or any other cache plugin, you can try using the <a href="https://codex.wordpress.org/Transients_API">WordPress Transients API </a> to save the results into the database.

The WordPress Transients API offers a simple and standardized way of storing cached data in the database temporarily by giving it a custom name and a time frame, after which it will expire and be deleted. The <code>catch_widget_query()</code> function after adding the WP Transient API code is shown below.

<div class="break-out">

 <pre><code class="language-php">public function catch_widget_query()
{
    /* If no 'embed' parameter found, return */
    if(!get_query_var('em_embed')) return;

    /* 'embed' variable is set, export any content you like */

    if(get_query_var('em_embed') == 'posts')
    { 
        /* Here we are now using the 'WP Transient API'.

           See if we have any saved data for the 'ewidget' key.
         */
        $cached = get_transient('ewidget');

        /* Oops!, the cache is empty */
        if(empty($cached))
        {
            /* Get some fresh data */
            $data_to_embed = $this-&gt;export_posts();

            /* Save it using the 'WP Transient API' using the 'ewidget' key,
               set it to expire after 12 hours.
             */
            set_transient('ewidget', $data_to_embed, 60 * 60 * 12);
            echo $data_to_embed;
        }
        /* Yes we found some, so we return that to the user */
        else
        {
            echo $cached;
        }
    }

    exit();
}</code></pre>
</div>

## In Conclusion

Sharing your content across different websites is a nice way to market your services and create brand awareness. With millions of WordPress websites around, there is a huge amount of content out there that can be profitably shared among users. Not just text, but also images, videos, advertisements, etc. This article is just a simple implementation of an embeddable widget. You can customize it in various ways to include security, analytics code to track widget usage and other functionality.

### <span class="rh">Further Reading</span> on SmashingMag:

*   [Utilizing User Roles In WordPress](https://www.smashingmagazine.com/2012/10/utilizing-user-roles-wordpress/)
*   [How To Become A Top WordPress Professional](https://www.smashingmagazine.com/2012/12/become-top-wordpress-professional/)
*   [Useful WordPress Tools, Themes And Plugins](https://www.smashingmagazine.com/2012/03/useful-wordpress-tools-themes-plugins/)
*   <span>[Inside WordPress Actions And Filters](https://www.smashingmagazine.com/2012/02/inside-wordpress-actions-filters/)</span>

{{< signature "cp, il" >}}
