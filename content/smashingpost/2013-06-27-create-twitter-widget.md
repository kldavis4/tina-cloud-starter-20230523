---
title: How To Create A Twitter Widget
slug: create-twitter-widget
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2498c837-766e-4bf5-8fcd-38d9a2dd4bcb/wp-3.jpg
date: 2013-06-27T08:07:37.000Z
author: daniel-pataki
description: >-
  Twitter needs no introduction. It has become the way to reach audiences for
  some people and companies and a place to hang out for others. Placing a
  Twitter feed on one’s website has almost become compulsory.
categories:
  - WordPress
  - Workflow
  - Techniques
  - Widgets
  - Techniques (WP)
---
Embedding a feed isn’t all that difficult if you are comfortable with Twitter’s default widget, but making your own will enable you to blend it into your website seamlessly.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a36fb345-235b-4853-9f9a-ed5080c76b3f/photodune-4052663-twitter-on-keyboard-xs-mini.jpg"><img loading="lazy" decoding="async" class="aligncenter size-full wp-image-109426" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/017952da-5ba0-4f0e-b3b1-43e7c9091c8c/photodune-4052663-twitter-on-keyboard-xs-500-mini.jpg" alt="photodune-4052663-twitter-on-keyboard-xs" width="500" height="333" /></a>

## The Result

The result of our effort will be a WordPress widget that can be placed in a widgetized sidebar. It will display the user’s details on top and the latest few items from the user’s feed. You can see it in action in our Musico theme, although the screenshot below says it all.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2768ef37-0c91-4e53-92df-25e26e71b342/finished-widget-mini.png"><img loading="lazy" decoding="async" loading="lazy" decoding="async" class="108921" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2768ef37-0c91-4e53-92df-25e26e71b342/finished-widget-mini.png" alt="finished_widget" width="354" height="723" /></a>

{{% feature-panel %}}

## About The Twitter Terms Of Service

Because this is a custom widget, you control what and how elements are displayed. Make sure to read Twitter’s “<a href="https://dev.twitter.com/terms/display-requirements">Developer Display Requirements</a>” to find out what you need to display. I will be breaking some of the rules for simplicity’s sake, but bolting on stuff will be a trivial matter once you’ve finished this article.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [How To Get The Most Out Of A Premium WordPress Theme](https://www.smashingmagazine.com/2013/02/get-the-best-out-of-premium-wordpress-theme/)
*   <span>[How To Contribute To WordPress](https://www.smashingmagazine.com/2013/05/contributing-to-wordpress/)</span>
*   [WordPress Functions To Make Blogging Easier](https://www.smashingmagazine.com/2013/06/five-wordpress-functions-blogging-easier/)
*   [How To Improve The Deployment Of WordPress Websites](https://www.smashingmagazine.com/2013/04/wordpress-deployment-survey/)

Note that <strong>conforming to the requirements is a must</strong>. If you do not, you run the risk of your ID being banned which means that your widget will not display any tweets.</p>

## First Step: Create A Twitter App

Before writing any code, we’ll have to get our hands on a Twitter app or, more appropriately, Twitter API credentials. The process is explained in a video that I made:

In case you prefer reading to watching a video, <strong>here are the basic steps</strong>:

1.  Log into Twitter’s [developers section](https://dev.twitter.com/).
2.  Go to “[My Applications](https://dev.twitter.com/apps),” and click “Create a new application.”
3.  Fill out the required fields, accept the rules of the road, and then click on the “Create your Twitter application” button. You will not need a callback URL for this app, so feel free to leave it blank.
4.  Once the app has been created, click the “Create my access token” button.
5.  You’re done! You will need the following data later on:
    *   consumer key,
    *   consumer secret,
    *   access token,
    *   access token secret.</p>

## Add Our App’s Details

To add some options to our theme quickly, we’ll be using the theme customizer, introduced in WordPress 3.4. Smashing Magazine has an <a href="https://www.smashingmagazine.com/2013/03/05/the-wordpress-theme-customizer-a-developers-guide/">exhaustive article on it</a>, if you’re interested to learn more. For now, we’ll just add the bare necessities.

To enable quick access to the theme customizer, I like to use the following snippet:

<pre><code class="language-php">
add_action ('admin_menu', 'my_theme_customizer');
function my_theme_customizer() {
  add_theme_page(
    __( 'Customize Theme Options', THEMENAME ),
    __( 'Customize Theme', THEMENAME ),
    'edit_theme_options',
    'customize.php'
  );
}
</code></pre>

Adding the code above to your theme’s <code>functions.php</code> file will generate a link to the customizer in the “Appearance” section of the admin area. To add some options, we’ll need to create a class. Add a file named <code>MyCustomizer.class.php</code> to the theme’s directory, and paste the following code in it:

<pre><code class="language-php">
&lt;?php
class MyCustomizer {
  public static function register ( $wp_customize ) {

    /** Sections **/
    $wp_customize-&gt;add_section( 'twitter_api' , array(
      'title'    =&gt; __( 'Twitter API Details', 'mytextdomain' ),
      'priority' =&gt; 10,
    ));

    /** Settings **/
    $wp_customize-&gt;add_setting( 'twitter_consumer_key' );
    $wp_customize-&gt;add_setting( 'twitter_consumer_secret' );
    $wp_customize-&gt;add_setting( 'twitter_access_token' );
    $wp_customize-&gt;add_setting( 'twitter_access_token_secret' );

    /** Controls **/
    $wp_customize-&gt;add_control(
      'twitter_consumer_key',
       array(
        'label' =&gt; __( 'Consumer Key', 'mytextdomain' ),
        'section' =&gt; 'twitter_api',
        'priority' =&gt; 10,
       )
    );
    $wp_customize-&gt;add_control(
      'twitter_consumer_secret',
       array(
        'label' =&gt; __( 'Consumer Secret', 'mytextdomain' ),
        'section' =&gt; 'twitter_api',
        'priority' =&gt; 20,
       )
    );
    $wp_customize-&gt;add_control(
      'twitter_access_token',
       array(
        'label' =&gt; __( 'Access Token', 'mytextdomain' ),
        'section' =&gt; 'twitter_api',
        'priority' =&gt; 30,
       )
    );
    $wp_customize-&gt;add_control(
      'twitter_access_token_secret',
       array(
        'label' =&gt; __( 'Access Token Secret', 'mytextdomain' ),
        'section' =&gt; 'twitter_api',
        'priority' =&gt; 40,
       )
    );
   }
}
add_action( 'customize_register' , array( 'MyCustomizer' , 'register' ) );
?&gt;
</code></pre>

There are a couple of things to note about the code above. <strong>All of the details we need to add to the customizer are encapsulated in a class.</strong> The class is registered at the bottom of the code block, using a hook.

We need to do three things with the class to get our options to show up:

*   Create a new section to house these options in one logical group. We use the `add_section()` function to do this; all we need to add is a title.
*   We need to tell WordPress that we are adding particular settings. The function used is `add_setting`, which can take a default parameter as well, but we don’t really need it here.
*   Finally, we tie a control to the setting so that the user can manipulate it. A number of controls are available; here, we need a simple text box. Using the `add_control()` function, we specify the setting to be modified, the label of the control and the section it is in. The type of control is not specified because the default is the usual input box.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9400159a-2a49-4f5d-bd51-5de2f0b7320a/apisettings.png"><img loading="lazy" decoding="async" loading="lazy" decoding="async" class="108920" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9400159a-2a49-4f5d-bd51-5de2f0b7320a/apisettings.png" alt="apisettings" width="329" height="312" /></a>

Notice the “priority” setting for some elements. This determines the order they show up in. The reason they are multiples of 10 is that, if you realize later that you need to add something between two settings, <strong>you won’t need to rewrite all of the priorities</strong>; you would just use “15” for the new element.

Don’t forget to include this class in <code>functions.php</code> so that the code is executed.

<pre><code class="language-php">
include( 'MyCustomizer.class.php' );
</code></pre>

Once all that is done, you can fill out the details. You will be able to access the values using the <code>get_theme_mod( 'option_name' )</code> function (more on that below).

## Integrate The API

We now have a way to retrieve our API details, but we are not in contact with the API just yet. Doing that is a bit difficult; luckily, others have done the grunt work for us. For this tutorial, I’ll use Codebird, a PHP class for interacting with the Twitter API.

Download the <code>codebird.php</code> file from <a href="https://github.com/mynetx/codebird-php">Codebird</a>, put it in your main theme folder, and set it up like so:

<pre><code class="language-php">
add_action( 'init', 'my_twitter_api' );
function my_twitter_api() {
  global $cb;
  $consumer_key = get_theme_mod( 'consumer_key' );
  $consumer_secret = get_theme_mod( 'consumer_secret' );
  $access_token = get_theme_mod( 'access_token' );
  $access_secret = get_theme_mod( 'access_secret' );

  include( 'codebird.php' )
  Codebird::setConsumerKey( $consumer_key, $consumer_secret );
  $cb = Codebird::getInstance();
  $cb-&gt;setToken( $access_token, $access_secret );
}
</code></pre>

Now you’ll be able to use Codebird by invoking the <code>$cb</code> instance. Let’s set this aside for now; we’ll get back to it later!

## Create A Widget

I like to separate widgets into individual files. So, before we do anything else, create a <code>widgets</code> directory and put a file in it named <code>MyTwitterWidget.class.php</code>. Include this file in <code>functions.php</code> just as we did above:

<pre><code class="language-php">
include( 'widgets/MyTwitterWidget.class.php' );
</code></pre>

Add the following PHP code to the file. <strong>This is the general starting point for widgets.</strong>

<pre><code class="language-php">
&lt;?php
class MyTwitterWidget extends WP_Widget {
  /** Widget setup **/
      function MyTwitterWidget() {
      parent::WP_Widget(
      false, __( 'My Twitter Widget', 'mytextdomain' ),
      array('description' =&gt; __( 'Displays a list of tweets from a specified user name', 'mytextdomain' )),
      array('width' =&gt; '400px')
    );
  }
  /** The back-end form **/
  function form( $instance ) {

  }
  /** Saving form data **/
  function update( $new_instance, $old_instance ) {

  }
  /** The front-end display **/
  function widget( $args, $instance ) {

  }
}
register_widget('MyTwitterWidget');
?&gt;
</code></pre>

There are four functions here, each with a particular role in creating the widget.

*   The first function is the constructor. The widget’s title and description may be specified here.
*   The `form` function takes care of the back-end form. Putting a few functions in there makes it very easy to assemble a form. WordPress takes care of the rest.
*   The `update` function enables you to add any special code to the saving process.
*   The `widget` function handles the front-end display of the widget.

As we build the widget, you’ll see that we’ll need some custom functions. But until then, <strong>let’s go function by function</strong>.</p>

### The Back-End Form

We want to give the user the option to change the title of the widget, to specify how many tweets to show, and to specify their Twitter user name. The basic pattern for creating these options is as follows:

<pre><code class="language-php">
&lt;p&gt;
  &lt;label for='&lt;?php echo $this-&gt;get_field_id( 'option_name' ); ?&gt;'&gt;
    &lt;?php _e( 'Title:', 'mytextdomain' ); ?&gt;
    &lt;input class='widefat' id='&lt;?php echo $this-&gt;get_field_id( 'option_name' ); ?&gt;' name='&lt;?php echo $this-&gt;get_field_name( 'option_name' ); ?&gt;' type='text' value='&lt;?php echo $values['option_name']; ?&gt;' /&gt;
  &lt;/label&gt;
&lt;/p&gt;
</code></pre>

The <code>$values</code> array is a list of all of this widget’s options, which are specified elsewhere. All of our options will follow the pattern below. Here are the functions to look out for:

*   `get_field_id()`Outputs the ID of the field for your option.
*   `get_field_name()`Outputs the name of the field for your option.

Using these functions is crucial because the name and ID of these fields can get pretty funky when multiple widget instances are in multiple sidebars.

<strong>The complete code for our form</strong> looks something like this:

<pre><code class="language-php">
&lt;?php
  $defaults = array(
    'title'    =&gt; ’,
    'limit'    =&gt; 5,
    'username' =&gt; 'bonsaished'
  );
  $values = wp_parse_args( $instance, $defaults );
?&gt;
&lt;p&gt;
  &lt;label for='&lt;?php echo $this-&gt;get_field_id( 'title' ); ?&gt;'&gt;
    &lt;?php _e( 'Title:', 'mytextdomain' ); ?&gt;
    &lt;input class='widefat' id='&lt;?php echo $this-&gt;get_field_id( 'title' ); ?&gt;' name='&lt;?php echo $this-&gt;get_field_name( 'title' ); ?&gt;' type='text' value='&lt;?php echo $values['title']; ?&gt;' /&gt;
  &lt;/label&gt;
&lt;/p&gt;

&lt;p&gt;
  &lt;label for='&lt;?php echo $this-&gt;get_field_id( 'limit' ); ?&gt;'&gt;
    &lt;?php _e( 'Tweets to show:', 'mytextdomain' ); ?&gt;
    &lt;input class='widefat' id='&lt;?php echo $this-&gt;get_field_id( 'limit' ); ?&gt;' name='&lt;?php echo $this-&gt;get_field_name( 'limit' ); ?&gt;' type='text' value='&lt;?php echo $values['limit']; ?&gt;' /&gt;
  &lt;/label&gt;
&lt;/p&gt;

&lt;p&gt;
  &lt;label for='&lt;?php echo $this-&gt;get_field_id( 'username' ); ?&gt;'&gt;
    &lt;?php _e( 'Twitter user name:', 'mytextdomain' ); ?&gt;
    &lt;input class='widefat' id='&lt;?php echo $this-&gt;get_field_id( 'username' ); ?&gt;' name='&lt;?php echo $this-&gt;get_field_name( 'username' ); ?&gt;' type='text' value='&lt;?php echo $values['username']; ?&gt;' /&gt;
  &lt;/label&gt;
&lt;/p&gt;
</code></pre>

The only addition made to this code is the retrieval of the values. The function is passed the current values in the <code>$instance</code> parameter. I’ve added a <code>defaults</code> array in case no values have been set. The <code>defaults</code> and the <code>instance</code> data arrays have been merged, resulting in the final <code>$values</code> array.</p>

## Save The Form’s Data

I’m sure you’ll be relieved by the simplicity of this. Here’s the complete code in the <code>update()</code> functions.

<pre><code class="language-php">
return $new_instance;
</code></pre>

The <code>$new_instance</code> parameter has all of the new data in it. All we need to do is return it. The purpose of the <code>update</code> function is to allow for some validation or manipulation.</p>

## Display The Tweets

Now for the hard part! Retrieving the tweets is not that difficult, but if we do it on every page load, we’ll be rate-limited by Twitter in no time. We’ll need to find a way to cache the results <strong>so that we only bother Twitter, say, every five minutes</strong>. The way I like to handle these problems is to side-step them altogether and code as if the solution were already in place. Let’s assume that we’ve already written the functions that we need for this and proceed to create the front end:

First, let’s look at the general template needed to display widgets:

<pre><code class="language-php">
echo $args['before_widget'];
echo $args['before_title'] . $instance['title'] .  $args['after_title'];
echo $args['after_widget'];
</code></pre>

The <code>$args</code> parameter holds some structural information from the sidebar you created. We just output these to make sure that this widget conforms to all of your other widgets.

Now, let’s list some tweets:

<pre><code class="language-php">
$tweets = $this-&gt;get_tweets( $args['widget_id'], $instance );
if( !empty( $tweets['tweets'] ) AND empty( $tweets['tweets']-&gt;errors ) ) {

  echo $args['before_widget'];
  echo $args['before_title'] . $instance['title'] .  $args['after_title'];

  $user = current( $tweets['tweets'] );
  $user = $user-&gt;user;

  echo '
    &lt;div class="twitter-profile"&gt;
    &lt;img src="' . $user-&gt;profile_image_url . '"&gt;
    &lt;h1&gt;&lt;a class="heading-text-color" href="https://twitter.com/' . $user-&gt;screen_name . '"&gt;' . $user-&gt;screen_name . '&lt;/a&gt;&lt;/h1&gt;
    &lt;div class="description content"&gt;' . $user-&gt;description . '&lt;/div&gt;
    &lt;/div&gt;  ';

  echo '&lt;ul&gt;';
  foreach( $tweets['tweets'] as $tweet ) {
    if( is_object( $tweet ) ) {
      $tweet_text = htmlentities($tweet-&gt;text, ENT_QUOTES);
      $tweet_text = preg_replace( '/https://([a-z0-9_.-+&amp;!#~/,]+)/i', '<a class="primary" href="https://$1">https://$1</a>', $tweet_text );

      echo '
        &lt;li&gt;
          &lt;span class="content"&gt;' . $tweet_text . '&lt;/span&gt;
          &lt;div class="date"&gt;' . human_time_diff( strtotime( $tweet-&gt;created_at ) ) . ' ago &lt;/div&gt;
        &lt;/li&gt;';
    }
  }
  echo '&lt;/ul&gt;';
  echo $args['after_widget'];
}
</code></pre>

Let’s dissect this to understand what’s going on.

*   **Line 1**We’re assuming that we have a `get_tweets()` function that will return a list of tweets in some form. We haven’t written this yet, but by assuming that we have done so, we’ll know what to include in the function’s code.
*   **Line 2**If the tweets list is not empty and there are no errors, we can display the widget.
*   **Lines 7–8**All tweets are from the same user, and each tweet contains the user’s data. In line 7, we’re just grabbing the first tweet. In line 8, we’re pulling the user’s details into the `$user` variable.
*   **Lines 10–16**We use data from the `$user` object to build a simple display for the user’s account. It includes the image, short description and user name.
*   **Lines 18–29**Using data in the `$tweets['tweets']` variable, we build a list of tweets. The `preg_replace()` in there is needed to convert links (which arrive as plain text) into clickable elements.

All that’s left is to figure out how the <code>get_tweets()</code> function should work. We already know that it can’t directly get the tweets from Twitter, so we’ll need to use some trickery!

To pull this off, our <code>get_tweets()</code> function will need to do the following:

1.  Get the list of tweets from our own database.
2.  If no list is there or the list is more than five minutes old, then it needs to grab the list from Twitter.
3.  Once we get results from Twitter, we save them to our database and add a timestamp to make sure we don’t grab it again before the five minutes is up.

To make things more modular, we’ll create three functions.

*   `get_tweets()`Pulls a list of tweets from our database.
*   `retrieve_tweets()`Pulls a list of tweets from Twitter.
*   `save_tweets()`Saves a list of tweets from Twitter to our database.</p>

### Retrieve Tweets From Twitter

In the <code>MyTwitterWidget</code> class, let’s create this function and make it retrieve some tweets:

<pre><code class="language-php">
function retrieve_tweets( $widget_id, $instance ) {
  global $cb;
  $timeline = $cb-&gt;statuses_userTimeline( 'screen_name=' . $instance['username']. '&amp;count=' . $instance['limit'] . '&amp;exclude_replies=true' );
  return $timeline;
}
</code></pre>

As you can see, this is pretty easy, thanks to the Codebird class. We simply use one of its functions, <code>statuses_userTimeline()</code>, to retrieve our list. Our own functions receive the widget’s ID and the <code>instance</code> data, which we use to tell Codebird which user’s tweets we want and how many to retrieve.</p>

### Save Tweets to the Database

To save the tweets to the database, we’ll need to use the ID of the widget and the actual tweets, and we’ll need to store the time when we last updated them.

<pre><code class="language-php">
function save_tweets( $widget_id, $instance ) {
  $timeline = $this-&gt;retrieve_tweets( $widget_id, $instance );
  $tweets = array( 'tweets' =&gt; $timeline, 'update_time' =&gt; time() + ( 60 * 5 ) );
  update_option( 'my_tweets_' . $widget_id, $tweets );
  return $tweets;
}
</code></pre>

This widget also receives the widget’s ID and the <code>instance</code> data. We use these to retrieve the tweets, using the <code>retrieve_tweets()</code> function that we created above. We’ll add that to our <code>$tweets</code> array, which contains the data returned from Twitter and the time of update.

The time of update is five minutes from now. When we display our tweets, we’ll use this value to determine whether to display the tweets in the database or to grab the list from Twitter again (to ensure we have the most recent ones).

We use the widget’s ID to save the list to the database, using WordPress’ options table. This ensures that we can save the proper Twitter details for each instance of our Twitter widget.</p>

### Get Tweets From the Database

We’ve finally arrived at the <code>get_tweets()</code> function. Let’s take a look. Explanation ensues!

<pre><code class="language-php">
function get_tweets( $widget_id, $instance ) {
  $tweets = get_option( 'my_tweets_' . $widget_id );
  if( empty( $tweets ) OR time() &gt; $tweets['update_time'] ) {
    $tweets = $this-&gt;save_tweets( $widget_id, $instance );
  }
  return $tweets;
}
</code></pre>

First, we retrieve the tweets from the database using the options table. If the options table is empty or the update time has past our limit, then we use the <code>save_tweets()</code> function. This will retrieve the tweets from Twitter and save them to the database (and also return them so that we can use them right away).</p>

## Conclusion

While this methodology does not lack complexity, it has a <strong>tight and clear logic</strong> to it, which arises from the thoughtful way that WordPress implements widgets and the new theme customizer.

Once you grasp the basic idea behind how this widget is created, you can add many of your own and customize them to your (or your client’s) delight.

{{< signature "al, ea" >}}

