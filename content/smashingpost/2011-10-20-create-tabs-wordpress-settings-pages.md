---
title: How To Create Tabs On WordPress Settings Pages
slug: create-tabs-wordpress-settings-pages
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/aab11dee-69f7-4cd1-a096-a24e8424eb34/wordpress-arrow-illu.jpg
date: 2011-10-20T14:01:40.000Z
author: elio-rivero
description: >-
  Using tabs in a user interface can help you better organize content, so it’s only natural that WordPress themes that have a lot of options would benefit from tabs on their settings page. In this tutorial, you will learn how to create a tabbed settings page, and you’ll get to download a WordPress theme that implements the code.
categories:
  - WordPress
  - Tutorials
  - Tabs
---

### Overview

To get a quick grasp of the tabs we’ll be creating, go to <code>Appearance/Themes</code> in the WordPress admin area. You will find two tabs there: “Manage Themes” and “Install Themes.” When you click on one, the content changes and the tab’s title is highlighted.

{{% feature-panel %}}

<a href="https://www.smashingmagazine.com/2011/10/20/create-tabs-wordpress-settings-pages/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4db86b47-a7e3-40e4-93ad-ecf6168aa2f0/tabbed-theme-settings-wordpress.png" alt="tabbed-theme-settings-wordpress" width="550" height="300" /></a>

The process is actually fairly simple: we set and send a <code>tab</code> variable when a tab is clicked. By querying this tab variable later, in <code>$_GET['tab']</code>, we will know which tab was selected so that we can highlight the corresponding title and display the corresponding tab.

In our approach, there are three times when we will need to know which tab the user is currently on:

1.  When we initially display the tabs and the form fields for the settings (in order to display the correct set of fields);
2.  When the user saves their settings (in order to save the correct fields);
3.  When redirecting the user after they have saved their settings (in order to redirect the user to the correct tab).

For the sake of brevity, we won’t explain all of the code, only the snippets that are relevant to this approach. You can, however, find all of the code in the accompanying theme.</p>

## Creating The Tabs

The first snippet we will inspect is the code that produces the tabs:

<pre><code class="language-php">function ilc_admin_tabs( $current = 'homepage' ) {
    $tabs = array( 'homepage' =&gt; 'Home Settings', 'general' =&gt; 'General', 'footer' =&gt; 'Footer' );
    echo '&lt;div id="icon-themes" class="icon32"&gt;&lt;br&gt;&lt;/div&gt;';
    echo '&lt;h2 class="nav-tab-wrapper"&gt;';
    foreach( $tabs as $tab =&gt; $name ){
        $class = ( $tab == $current ) ? ' nav-tab-active' : ’;
        echo "&lt;a class='nav-tab$class' href='?page=theme-settings&amp;tab=$tab'&gt;$name&lt;/a&gt;";

    }
    echo '&lt;/h2&gt;';
}</code></pre>

This function will be called later in the content for the settings page. We first define an array that contains all of our tabs. The first tab, which is displayed first by default, is <code>homepage</code>, where we can set up some option for the appearance of the home page. Then we have <code>general</code>, which could be a page containing options used throughout the website, and, finally, <code>footer</code>, to include a tracking code in the footer.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b48e441b-bf5a-4608-9acb-c1a1e79653ff/tabbed-theme-settings.png"><img loading="lazy" decoding="async" class="103974" title="Tabbed settings page for WordPress themes" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b48e441b-bf5a-4608-9acb-c1a1e79653ff/tabbed-theme-settings.png" alt="" width="550" height="350" /></a>

We then set up the URL links for each tab and output them. Notice that if the tab is open, an additional class, <code>nav-tab-active</code>, is added.

## Displaying The Tabbed Content

The content for the settings page is displayed in the callback function for <code>add_theme_page</code> (which is an abstraction of <a href="https://codex.wordpress.org/Function_Reference/add_submenu_page"><code>add_submenu_page</code></a>, with the parent slug set to <em>themes.php</em>), which in our theme will be named <code>ilc_settings_page</code>. This is where you will call the function that we just went over.

<pre><code class="language-php">function ilc_settings_page() {
   global $pagenow;
   $settings = get_option( "ilc_theme_settings" );

//generic HTML and code goes here

if ( isset ( $_GET['tab'] ) ) ilc_admin_tabs($_GET['tab']); else ilc_admin_tabs('homepage');</code></pre>

If the tab is the default one, then <code>$_GET['tab']</code> is not defined, in which case the current tab will be <code>homepage</code> and, thus, the highlighted one. Otherwise, the highlighted tab will be the one defined in <code>$_GET['tab']</code>.

Following the same function, we now need to display the right set of fields. Depending on the value of <code>$tab</code>, we would display the fields for the settings tab for the home page or for one of the other tabs:

<pre><code class="language-php">&lt;form method="post" action="&lt;?php admin_url( 'themes.php?page=theme-settings' ); ?&gt;"&gt;
&lt;?php
wp_nonce_field( "ilc-settings-page" );

if ( $pagenow == 'themes.php' &amp;&amp; $_GET['page'] == 'theme-settings' ){

   if ( isset ( $_GET['tab'] ) ) $tab = $_GET['tab'];
   else $tab = 'homepage';

   echo '&lt;table class="form-table"&gt;';
   switch ( $tab ){
      case 'general' :
         ?&gt;
         &lt;tr&gt;
            &lt;th&gt;Tags with CSS classes:&lt;/th&gt;
            &lt;td&gt;
               &lt;input id="ilc_tag_class" name="ilc_tag_class" type="checkbox" &lt;?php if ( $settings["ilc_tag_class"] ) echo 'checked="checked"'; ?&gt; value="true" /&gt;
               &lt;label for="ilc_tag_class"&gt;Checking this will output each post tag with a specific CSS class based on its slug.&lt;/label&gt;
            &lt;/td&gt;
         &lt;/tr&gt;
         &lt;?php
      break;
      case 'footer' :
         ?&gt;
         &lt;tr&gt;
            &lt;th&gt;&lt;label for="ilc_ga"&gt;Insert tracking code:&lt;/label&gt;&lt;/th&gt;
            &lt;td&gt;
               Enter your Google Analytics tracking code:
               &lt;textarea id="ilc_ga" name="ilc_ga" cols="60" rows="5"&gt;&lt;?php echo esc_html( stripslashes( $settings["ilc_ga"] ) ); ?&gt;&lt;/textarea&gt;&lt;br /&gt;

            &lt;/td&gt;
         &lt;/tr&gt;
         &lt;?php
      break;
      case 'homepage' :
         ?&gt;
         &lt;tr&gt;
            &lt;th&gt;&lt;label for="ilc_intro"&gt;Introduction&lt;/label&gt;&lt;/th&gt;
            &lt;td&gt;
               Enter the introductory text for the home page:
               &lt;textarea id="ilc_intro" name="ilc_intro" cols="60" rows="5" &gt;&lt;?php echo esc_html( stripslashes( $settings["ilc_intro"] ) ); ?&gt;&lt;/textarea&gt;
            &lt;/td&gt;
         &lt;/tr&gt;
         &lt;?php
      break;
   }
   echo '&lt;/table&gt;';
}

?&gt;
   &lt;p class="submit" style="clear: both;"&gt;
      &lt;input type="submit" name="Submit"  class="button-primary" value="Update Settings" /&gt;
      &lt;input type="hidden" name="ilc-settings-submit" value="Y" /&gt;
   &lt;/p&gt;
&lt;/form&gt;</code></pre>

All of the settings will be stored in a single array in order to prevent several queries from being made.

## Saving The Tabbed Fields

Now we need to know which slots of the array to save. Depending on the tab being displayed, certain options stored in the settings array will be displayed. If we just save all of the array slots, then we would overwrite some of the positions not shown in the current tab and thus not meant to be saved.

<pre><code class="language-php">function ilc_save_theme_settings() {
   global $pagenow;
   $settings = get_option( "ilc_theme_settings" );

   if ( $pagenow == 'themes.php' &amp;&amp; $_GET['page'] == 'theme-settings' ){
      if ( isset ( $_GET['tab'] ) )
           $tab = $_GET['tab'];
       else
           $tab = 'homepage';

       switch ( $tab ){
           case 'general' :
         $settings['ilc_tag_class'] = $_POST['ilc_tag_class'];
      break;
           case 'footer' :
         $settings['ilc_ga'] = $_POST['ilc_ga'];
      break;
      case 'homepage' :
         $settings['ilc_intro'] = $_POST['ilc_intro'];
      break;
       }
   }
   //code to filter html goes here
   $updated = update_option( "ilc_theme_settings", $settings );
}</code></pre>

We’ve used a <code>switch</code> conditional again to query the value of <code>$tab</code> and store the right values in the array. After that, we’ve updated the option in the WordPress database.</p>

## Redirecting The User To The Right Tab

Now that the contents are saved, we need WordPress to redirect the user back to the appropriate tab on the settings page.

<pre><code class="language-php">function ilc_load_settings_page() {
  if ( $_POST["ilc-settings-submit"] == 'Y' ) {
   check_admin_referer( "ilc-settings-page" );
   ilc_save_theme_settings();

   $url_parameters = isset($_GET['tab'])? 'updated=true&amp;tab='.$_GET['tab'] : 'updated=true';
   wp_redirect(admin_url('themes.php?page=theme-settings&amp;'.$url_parameters));
   exit;
  }
}</code></pre>

Depending on whether the <code>$_GET['tab']</code> variable is set, we use <code>wp_redirect</code> to send the user either to the default tab or to one of the other tabs.

Now our tabs are working, displaying the right set of fields, saving the right fields, and then redirecting the user to the correct tab.</p>

## Download The Theme

Almost any theme with a moderate number of options would benefit from tabs on the settings page. Just remember that this is one approach. Another approach would be to add several collapsable meta boxes, as seen on the page for writing posts, and to automatically collapse the boxes that are not frequently used. However, tabs enable you to better separate each set of options.

Finally, here is the theme, so that you can take a closer look:

*   [Theme with tabbed settings page](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/77802b74-7e2f-4811-9ddf-ede390ffc2e1/sample-theme-tabbed.zip "Download theme with tabbed settings page")

The theme also implements the function whereby <a href="https://www.ilovecolors.com.ar/tag-class/">each tag is outputted with a unique CSS class</a>, so you can check that out, too.

## <span class="rh">Further Reading</span> on SmashingMag:

*   [The WordPress Theme Customizer](https://www.smashingmagazine.com/2013/03/the-wordpress-theme-customizer-a-developers-guide/)
*   [Developing WordPress Locally With MAMP](https://www.smashingmagazine.com/2011/09/developing-wordpress-locally-with-mamp/)
*   [Checklist To Creating The Perfect WordPress Website](https://www.smashingmagazine.com/2011/12/15-step-checklist-creating-perfect-wordpress-website/)
