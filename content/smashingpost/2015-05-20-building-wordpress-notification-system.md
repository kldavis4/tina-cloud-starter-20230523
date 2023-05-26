---
title: Building An Advanced Notification System For WordPress
slug: building-wordpress-notification-system
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/84691732-2ac6-4159-b916-716e4b8539f4/database-description-preview-opt.png
date: 2015-05-20T21:12:13.000Z
author: carlodaniele
description: >-
  A lot of tools enable us to distribute a website’s content, but when we need
  to promptly reach a target group, an [email notification
  system](https://www.smashingmagazine.com/2011/10/25/create-perfect-emails-wordpress-website/)
  might be the best option. If your website is not frequently updated, you could
  notify all subscribers each time a post is published. However, if it’s updated
  frequently or it covers several topics, you could filter subscribers before
  mailing them.

  If you opt for the latter, you could set up a user meta field that stores a
  bit of information to identify the subscribers to be notified. The same bit of
  information would label the posts you’re publishing. Depending on the
  website’s architecture, you could store the metadata in a category, a tag, a
  [custom
  taxonomy](https://www.smashingmagazine.com/2012/01/04/create-custom-taxonomies-wordpress/)
  or a [custom
  field](https://www.smashingmagazine.com/2010/04/29/extend-wordpress-with-custom-fields/).
  In this article we’ll show you how to **let your website’s subscribers
  decide** when they want notifications, and linked to a particular location.
categories:
  - WordPress
  - Techniques (WP)
---
A lot of tools enable us to distribute a website’s content, but when we need to promptly reach a target group, an email notification system might be the best option. If your website is not frequently updated, you could notify all subscribers each time a post is published. However, if it’s updated frequently or it covers several topics, you could filter subscribers before mailing them.

If you opt for the latter, you could set up a user meta field that stores a bit of information to identify the subscribers to be notified. The same bit of information would label the posts you’re publishing. Depending on the website’s architecture, you could store the meta data in a category, a tag, a custom taxonomy or a custom field. In this article we’ll show you how to let your website’s subscribers decide when they want notifications, and linked to a particular location.</p>

## <span class="rh">Further Reading</span> on SmashingMag: [Link](https://www.smashingmagazine.com/2011/09/how-to-create-a-wordpress-plugin/#further-reading-on-smashingmag)

*   [Ten Things Every WordPress Plugin Developer Should Know](https://www.smashingmagazine.com/2011/03/ten-things-every-wordpress-plugin-developer-should-know/)
*   [Making A WordPress Plugin That Uses Service APIs](https://www.smashingmagazine.com/2016/03/making-a-wordpress-plugin-that-uses-service-apis/)
*   [How Commercial Plugin Developers Are Using The Repository](https://www.smashingmagazine.com/2012/01/commercial-plugin-developers-wordpress-repository/)
*   [How To Improve Your WordPress Plugin’s Readme.txt](https://www.smashingmagazine.com/2011/11/improve-wordpress-plugins-readme-txt/)

## Can I Use A Plugin?

If WordPress is your CMS, you can choose from a number of plugins, such as the comprehensive <a href="https://jetpack.me/support/subscriptions/">JetPack</a> or the more specialized <a href="https://wordpress.org/plugins/subscribe2/">Subscribe 2</a>.

{{% feature-panel %}}

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0fb0f07e-5652-4a07-9eba-00ee952477ce/subscribe2-large-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/afd84fec-afaa-46eb-a4e9-3324bbba94b9/subscribe2-preview-opt.png" alt="Subscribe 2 settings page" /></a><figcaption>Subscribe 2’s settings page. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0fb0f07e-5652-4a07-9eba-00ee952477ce/subscribe2-large-preview-opt.png">View large version</a>)</figcaption></figure>

Jetpack is easy to use, whereas Subscribe 2 is specialized and full-featured. Both plugins enable you to send email notifications to subscribers whenever a post is published. Unfortunately, neither allows you to notify specific users about specific content. And we want to select posts based on custom fields, mailing them to specific groups of users. Unfortunately, no plugin seems able to help us with this.</p>

## Things To Do

We are going to add several functionalities to WordPress’ core, and the CMS allows us to declare our own custom functions in the main file of a plugin. We’re not going to dive deep into plugin development, but you can get the information you need directly <a href="https://codex.wordpress.org/Writing_a_Plugin">from the Codex</a>.

We have to accomplish the following tasks:

1.  add two meta fields to the user’s profile, the first of which stores the name of a location and the second of which determines whether the user will receive emails;
2.  add a custom meta box to the post-editing page containing the location-related custom field;
3.  select the users to be notified and send an email to them.</p>

## Add Meta Fields To User Profiles

WordPress stores user data in the <code>wp_users</code> and <code>wp_usermeta</code> tables.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/84691732-2ac6-4159-b916-716e4b8539f4/database-description-preview-opt.png" alt="WordPress database description" /><br>
<figcaption>WordPress’ database description. (Image: <a href="https://codex.wordpress.org/Database_Description">Codex</a>)</figcaption></figure>

Here, <code>wp_users</code> holds the list of all website users, while <code>wp_usermeta</code> contains all meta data associated with each user’s profile. Meta data is registered as key-value pairs in the <code>meta_key</code> and <code>meta_value</code> fields.

WordPress generates a bunch of meta data, such as <code>nickname</code>, <code>first_name</code>, <code>last_name</code>, <code>description</code> and <code>wp_capabilities</code>. Much of this data is automatically assigned to each user’s profile, and a user is able to edit it later from their profile page.

To perform our first task, we’ll add two meta fields to the profile pages of users. These fields will store the name of a geographic location and will allow the user to activate (or deactivate) the notification feature.

In the main file of the plugin, let’s define a global associative array whose elements consist of the names of US states:

<pre><code class="language-php">
$smashing_notification_states = array( 'AL' =&gt; 'Alabama', 'AK' =&gt; 'Alaska', 'AZ' =&gt; 'Arizona', 'AR' =&gt; 'Arkansas', 'CA' =&gt; 'California', 'CO' =&gt; 'Colorado', 'CT' =&gt; 'Connecticut', 'DE' =&gt; 'Delaware', 'FL' =&gt; 'Florida', 'GA' =&gt; 'Georgia', 'HI' =&gt; 'Hawaii', 'ID' =&gt; 'Idaho', 'IL' =&gt; 'Illinois', 'IN' =&gt; 'Indiana', 'IA' =&gt; 'Iowa', 'KS' =&gt; 'Kansas', 'KY' =&gt; 'Kentucky', 'LA' =&gt; 'Louisiana', 'ME' =&gt; 'Maine', 'MD' =&gt; 'Maryland', 'MA' =&gt; 'Massachusetts', 'MI' =&gt; 'Michigan', 'MN' =&gt; 'Minnesota', 'MS' =&gt; 'Mississippi', 'MO' =&gt; 'Missouri', 'MT' =&gt; 'Montana', 'NE' =&gt; 'Nebraska', 'NV' =&gt; 'Nevada', 'NH' =&gt; 'New Hampshire', 'NJ' =&gt; 'New Jersey', 'NM' =&gt; 'New Mexico', 'NY' =&gt; 'New York', 'NC' =&gt; 'North Carolina', 'ND' =&gt; 'North Dakota', 'OH' =&gt; 'Ohio', 'OK' =&gt; 'Oklahoma', 'OR' =&gt; 'Oregon', 'PA' =&gt; 'Pennsylvania', 'RI' =&gt; 'Rhode Island', 'SC' =&gt; 'South Carolina', 'SD' =&gt; 'South Dakota', 'TN' =&gt; 'Tennessee', 'TX' =&gt; 'Texas', 'UT' =&gt; 'Utah', 'VT' =&gt; 'Vermont', 'VA' =&gt; 'Virginia', 'WA' =&gt; 'Washington', 'WV' =&gt; 'West Virginia', 'WI' =&gt; 'Wisconsin', 'WY' =&gt; 'Wyoming' );
</code></pre>

Thanks to this array, we will generate a select menu to avoid input errors by users. Now, we need to add two form fields to the user’s profile page. To do this, we will use two action hooks:

<pre><code class="language-php">
add_action( 'show_user_profile', 'smashing_show_user_meta_fields' );
add_action( 'edit_user_profile', 'smashing_show_user_meta_fields' );
</code></pre>

Here, <a href="https://codex.wordpress.org/Plugin_API/Action_Reference/show_user_profile">show_user_profile</a> is triggered when a user is viewing their own profile, while <a href="https://codex.wordpress.org/Plugin_API/Action_Reference/edit_user_profile">edit_user_profile</a> is triggered when a user is viewing another user’s profile.

The callback function prints the markup.</p>

<pre><code class="language-php">
/**
 * Show custom user profile fields.
 *
 * @param obj $user The user object.
 */
function smashing_show_user_meta_fields( $user ) { 
    global $smashing_notification_states;
    ?&gt;
    &lt;h3&gt;&lt;?php _e( 'Smashing profile information', 'smashing' ); ?&gt;&lt;/h3&gt;
    &lt;table class="form-table"&gt;
        &lt;tr&gt;
            &lt;th scope="row"&gt;&lt;?php _e( 'State', 'smashing' ); ?&gt;&lt;/th&gt;
            &lt;td&gt;
                &lt;label for="state"&gt;
                    &lt;select name="state"&gt;
                        &lt;option value="" &lt;?php selected( get_user_meta( $user-&gt;ID, 'state', true ), "" ); ?&gt;&gt;Select&lt;/option&gt;
                        &lt;?php foreach ($smashing_notification_states as $key =&gt; $value) { ?&gt;
                            &lt;option value="&lt;?php echo $key; ?&gt;" &lt;?php selected( esc_attr( get_user_meta( $user-&gt;ID, 'state', true ) ), $key ); ?&gt;&gt;&lt;?php echo $value; ?&gt;&lt;/option&gt;
                        &lt;?php } ?&gt;
                    &lt;/select&gt;
                    &lt;?php _e( 'Select state', 'smashing' ); ?&gt;
                &lt;/label&gt;
            &lt;/td&gt;
        &lt;/tr&gt;
        &lt;tr&gt;
            &lt;th scope="row"&gt;&lt;?php _e( 'Notifications', 'smashing' ); ?&gt;&lt;/th&gt;
            &lt;td&gt;
                &lt;label for="notification"&gt;
                    &lt;input id="notification" type="checkbox" name="notification" value="true" &lt;?php checked( esc_attr( get_user_meta( $user-&gt;ID, 'notification', true ) ), 'true' ); ?&gt; /&gt;
                    &lt;?php _e( 'Subscribe to email notifications', 'smashing' ); ?&gt;
                &lt;/label&gt;
            &lt;/td&gt;
        &lt;/tr&gt;
    &lt;/table&gt;
&lt;?php }        

</code></pre>

This table contains two custom meta fields. The first is a select menu whose options are generated by a <code>foreach</code> loop that iterates over the <code>$smashing_notification_states</code> global array. This way, the user doesn’t have to type the name of their state, but instead chooses it from a dropdown list.

As you can see, we’re calling <a href="https://codex.wordpress.org/Function_Reference/selected">the <code>selected()</code> function</a> twice from inside two <code>&lt;option&gt;</code> tags; <code>selected()</code> is a WordPress function for comparing two strings. When the strings have the same value, the function prints <code>selected='selected'</code>; otherwise, it echoes an empty string.

The first time we call <code>selected()</code>, we’re comparing the current option’s value (<code>'state'</code>) with an empty string (which means no state was selected). When iterating over the <code>$smashing_notification_states</code> array, we’re comparing the value of each element to the current value of the <code>'state'</code> meta field. This way, we can automatically select the option corresponding to the existing <code>'state'</code> value.

The second meta field to be added to users’ profiles is a checkbox. Its value will be <code>'true'</code> or <code>'false'</code> depending on whether the user chooses to receive notifications. Similar to <code>selected()</code>, <a href="https://codex.wordpress.org/Function_Reference/checked">checked()</a> prints out the string <code>checked='checked'</code> when its two arguments have the same value. Of course, <code>checked()</code> applies to checkboxes and radio buttons.

Now that we’ve got the fields, we can save the user’s input. We need two action hooks to store the user data:

<pre><code class="language-php">
add_action( 'personal_options_update', 'smashing_save_user_meta_fields' );
add_action( 'edit_user_profile_update', 'smashing_save_user_meta_fields' );
</code></pre>

Here, <code>personal_options_update</code> is triggered when the user is viewing their own profile page, while <code>edit_user_profile_update</code> is triggered when a user with sufficient privileges is viewing another user’s profile page. We have two hooks but just one callback:

<pre><code class="language-php">
/**
 * Store data in wp_usermeta table.
 *
 * @param int $user_id the user unique ID.
 */
function smashing_save_user_meta_fields( $user_id ) {

    if ( !current_user_can( 'edit_user', $user_id ) )
        return false;

    if( isset($_POST['state']) )
        update_user_meta( $user_id, 'state', sanitize_text_field( $_POST['state'] ) );

    if( !isset($_POST['notification']) ) 
        $_POST['notification'] = 'false';

    update_user_meta( $user_id, 'notification', sanitize_text_field( $_POST['notification'] ) );

}
</code></pre>

This function verifies whether the user is allowed to <code>edit_user</code>, and if <code>current_user_can</code> is true, it checks the data and saves it in the <code>wp_usermeta</code> table.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7eb91b48-f4f7-439a-bd9c-592cbe2ede2a/profile-info-preview-opt.png" alt="Custom meta fields" /><br>
<figcaption>The custom meta fields added to the user’s profile page.</figcaption></figure>

## Custom Meta Box And Custom Fields

We have to decide what kind of content should be included in the notification to subscribers. This decision will depend on your website’s architecture. In this example, we’ll go for regular posts, but you could choose a custom post type instead. The choice depends on your needs.

That being said, we are going to build a custom meta box containing a set of custom fields. These fields will be used to store an address, city, state and some other data related to location. Two other custom fields will enable and disable notifications on a per-post basis, and they will register the number of emails sent to users whenever a new post has been published. Let’s put another action hook to work:

<pre><code class="language-php">
add_action( 'add_meta_boxes', 'smashing_add_meta_box' );
function smashing_add_meta_box(){

    $screens = array( 'post' ); // possible values: 'post', 'page', 'dashboard', 'link', 'attachment', 'custom_post_type'

    foreach ($screens as $screen) {
        add_meta_box(
            'smashing_metabox',                     // $id - meta_box ID
            __( 'Venue information', 'smashing' ),  // $title - a title for the meta_box container
            'smashing_meta_box_callback',           // $callback - the callback that outputs the html for the meta_box
            $screen,                                // $post_type - where to show the meta_box. Possible values: 'post', 'page', 'dashboard', 'link', 'attachment', 'custom_post_type'
            'normal',                               // $context - possible values: 'normal', 'advanced', 'side'
            'high'                                  // $priority - possible values: 'high', 'core', 'default', 'low'
            );
        }
}
</code></pre>

Here, <a href="https://codex.wordpress.org/Function_Reference/add_meta_box">add_meta_box</a> accepts seven arguments: a unique ID for the meta box, a title, a callback function, a value for <code>screen</code>, the context (i.e. the part of the page where to show the meta box), and priority and callback arguments. Because we are not setting a value for the callback argument parameter, the <code>$post</code> object will be the only argument passed to <code>smashing_meta_box_callback</code>. Finally, let’s define the callback function to print out the meta box:

<pre><code class="language-php">
/*
 * Print the meta_box
 *
 * @param obj $post The object for the current post
 */
function smashing_meta_box_callback( $post ){
    global $smashing_notification_states;

    // Add a nonce field
    wp_nonce_field( 'smashing_meta_box', 'smashing_meta_box_nonce' );

    $address = esc_attr( get_post_meta( get_the_ID(), 'address', true ) );
    $city = esc_attr( get_post_meta( get_the_ID(), 'city', true ) );
    $state = esc_attr( get_post_meta( get_the_ID(), 'state', true ) );
    $zip = esc_attr( get_post_meta( get_the_ID(), 'zip', true ) );
    $phone = esc_attr( get_post_meta( get_the_ID(), 'phone', true ) );
    $website = esc_attr( get_post_meta( get_the_ID(), 'website', true ) );
    $disable = esc_attr( get_post_meta( get_the_ID(), 'disable', true ) );
    ?&gt;
&lt;table id="venue"&gt;
    &lt;tbody&gt;
        &lt;tr&gt;
            &lt;td class="label"&gt;&lt;?php _e( 'Address', 'smashing' ); ?&gt;&lt;/td&gt;
            &lt;td&gt;&lt;input type="text" id="address" name="venue[address]" value="&lt;?php echo $address; ?&gt;" size="30" /&gt;&lt;/td&gt;
        &lt;/tr&gt;
        &lt;tr&gt;
            &lt;td&gt;&lt;?php _e( 'City', 'smashing' ); ?&gt;&lt;/td&gt;
            &lt;td&gt;&lt;input type="text" id="city" name="venue[city]" value="&lt;?php echo $city; ?&gt;" size="30" /&gt;&lt;/td&gt;
        &lt;/tr&gt;
        &lt;tr&gt;
            &lt;td&gt;&lt;?php _e( 'State', 'smashing' ); ?&gt;&lt;/td&gt;
            &lt;td&gt;
                &lt;select name="venue[state]"&gt;
                    &lt;option value="" &lt;?php selected( $state, "" ); ?&gt;&gt;Select&lt;/option&gt;
                    &lt;?php foreach ($smashing_notification_states as $key =&gt; $value) { ?&gt;
                        &lt;option value="&lt;?php echo $key; ?&gt;" &lt;?php selected( $state, $key ); ?&gt;&gt;&lt;?php echo $value; ?&gt;&lt;/option&gt;
                    &lt;?php } ?&gt;
                &lt;/select&gt;
            &lt;/td&gt;
        &lt;/tr&gt;
        &lt;tr&gt;
            &lt;td&gt;&lt;?php _e( 'Disable notification', 'smashing' ); ?&gt;&lt;/td&gt;
            &lt;td&gt;&lt;input id="disable" type="checkbox" name="venue[disable]" value="true" &lt;?php checked( $disable, 'true' ); ?&gt; /&gt;&lt;/td&gt;
        &lt;/tr&gt;
    &lt;/tbody&gt;
&lt;/table&gt;
&lt;?php
}
</code></pre>

First, we’re initializing the <code>global</code> array and registering a <a href="https://codex.wordpress.org/WordPress_Nonces">nonce field</a>. We then add two simple text fields. The <code>name</code> attribute is set in the form of an array element, while the value is set to the corresponding custom field’s value. Finally, the main custom fields are added.

Just like with the user’s meta data, we add a select menu whose options are echoed, iterating over the elements in the <code>$smashing_notification_states</code> global array. Once we have built the select menu, let’s continue with a checkbox to enable and disable the single post notification.

Now we have to save the data: Our action hook is <code>save_post</code>. We’ll perform a number of tasks with the callback function. Take a look at the inline documentation for more information.</p>

<pre><code class="language-php">
add_action( 'save_post', 'smashing_save_custom_fields' );

/*
 * Save the custom field values
 *
 * @param int $post_id the current post ID
 */
function smashing_save_custom_fields( $post_id ){

    // Check WP nonce
    if ( !isset( $_POST['smashing_meta_box_nonce'] ) || ! wp_verify_nonce( $_POST['smashing_meta_box_nonce'], 'smashing_meta_box' ) )
        return;

    // Return if this is an autosave
    if ( defined( 'DOING_AUTOSAVE' ) &amp;&amp; DOING_AUTOSAVE )
        return;

    // check the post_type and set the correspondig capability value
    $capability = ( isset( $_POST['post_type'] ) &amp;&amp; 'page' == $_POST['post_type'] ) ? 'edit_page' : 'edit_post';

    // Return if the user lacks the required capability
    if ( !current_user_can( $capability, $post_id ) )
        return;

    if( !isset($_POST['venue']['disable']) ) 
        $_POST['venue']['disable'] = 'false';

    // validate custom field values
    $fields = ( isset( $_POST['venue'] ) ) ? (array) $_POST['venue'] : array();
    $fields = array_map( 'sanitize_text_field', $fields );

    foreach ($fields as $key =&gt; $value) {
        // store data
        update_post_meta( $post_id, $key, $value );
    }
}
</code></pre>

Our custom meta box is up and running, and it looks like this:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/87ad4ff4-fcd2-4d98-99b4-21e4cc0e2cc2/venue-large-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e5c0eff8-1c79-43c1-a13b-5cc0e4933684/venue-preview-opt.png" alt="Custom meta box" /></a><figcaption>The custom meta box showing the location details. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/87ad4ff4-fcd2-4d98-99b4-21e4cc0e2cc2/venue-large-preview-opt.png">View large version</a>)</figcaption></figure>

## Building The Notification System

If you were working with custom post types, you would need the <code>publish_{$post_type}</code> hook (i.e. <code>publish_recipes</code>, <code>publish_events</code>, etc.). But since we are working with posts, <code>publish_post</code> is the hook for us:

<pre><code class="language-php">
add_action( 'publish_post', 'smashing_notify_new_post' );

/*
 * Notify users sending them an email
 *
 * @param int $post_ID the current post ID
 */
function smashing_notify_new_post( $post_ID ){
    global $smashing_notification_states;

    $url = get_permalink( $post_ID );
    $state = get_post_meta( $post_ID, 'state', true );

    if( 'true' == get_post_meta( $post_ID, 'disable', true ) )
        return;

    // build the meta query to retrieve subscribers
    $args = array(
            'meta_query' =&gt; array(
                    array( 'key' =&gt; 'state', 'value' =&gt; $state, 'compare' =&gt; '=' ),
                    array( 'key' =&gt; 'notification', 'value' =&gt; 'true', 'compare' =&gt; '=' )
                ),
            'fields' =&gt; array( 'display_name', 'user_email' )
        );
    // retrieve users to notify about the new post
    $users = get_users( $args );
    $num = 0;
    foreach ($users as $user) {

        $to = $user-&gt;display_name . ' &lt;' . $user-&gt;user_email . '&gt;';

        $subject = sprintf( __( 'Hei! We have news for you from %s', 'smashing' ), $smashing_notification_states[$state] );

        $message = sprintf( __( 'Hi %s!', 'smashing' ), $user-&gt;display_name ) . "\r\n" .
        sprintf( __( 'We have a new post from %s', 'smashing' ), $smashing_notification_states[$state] ) . "\r\n" .
        sprintf( __( 'Read more on %s', 'smashing' ), $url ) . '.' . "\r\n";   

        $headers[] = 'From: Yourname &lt;you@yourdomain.com&gt;';
        $headers[] = 'Reply-To: you@yourdomain.com';

        if( wp_mail( $to, $subject, $message, $headers ) )
            $num++;
    }
    // a hidden custom field
    update_post_meta( $post_ID, '_notified_users', $num );
    return $post_ID;
}
</code></pre>

Once again, we declare the global array <code>$smashing_notification_states</code>. The two variables <code>$url</code> and <code>$state</code> will store the post’s permalink and state. The succeeding condition checks the value of the <code>disable</code> custom field: If it’s <code>'true'</code>, we exit the function. We have to retrieve from the database all users whose <code>state</code> meta field has the same value as the <code>state</code> custom field of the current post, and we use the <code>get_users()</code> function to accomplish this.

The <a href="https://codex.wordpress.org/Function_Reference/wp_mail">wp_mail</a> function accepts five arguments: recipient(s), subject, message, headers, attachments. The recipients could be passed as an array or as a comma-separated strings of addresses. So, we could have passed to the function all of the addresses together, but doing so would have made them publicly visible (this is the way <code>wp_mail()</code> works).

So, we’ll iterate over the <code>$users</code> array and call <code>wp_mail</code> repeatedly (which shouldn’t be done with a huge number of emails, as we’ll see in a moment). In case of success, <code>wp_mail</code> returns <code>true</code>. The counter is incremented by 1, and the loop continues with the next user.

When the <code>foreach</code> cycle ends, the current value of <code>$num</code> is registered in the hidden <code>_notified_users</code> custom field (notice the underscore preceding the name of the custom field).

Unfortunately, a loop iterating over and over hundreds of times could considerably slow down the script, as pointed out in the reference on the <a href="https://php.net/manual/it/function.mail.php">PHP mail() function</a>:
<blockquote>It is worth noting that the <code>mail()</code> function is not suitable for larger volumes of email in a loop. This function opens and closes an SMTP socket for each email, which is not very efficient.

For the sending of large amounts of email, see the <a href="https://pear.php.net/package/Mail">» PEAR::Mail</a>, and <a href="https://pear.php.net/package/Mail_Queue">» PEAR::Mail_Queue</a> packages.</blockquote>

We could work around this, passing to the function the email addresses as BCCs, <a href="https://codex.wordpress.org/Function_Reference/wp_mail#Using_.24headers_To_Set_.22From:.22.2C_.22Cc:.22_and_.22Bcc:.22_Parameters">setting them in the headers</a>, as shown here:

<pre><code class="language-php">
function smashing_notify_new_post( $post_ID ){
    global $smashing_notification_states;

    $url = get_permalink( $post_ID );
    $state = get_post_meta( $post_ID, 'state', true );

    if( 'true' == get_post_meta( $post_ID, 'disable', true ) )
        return;

    // build the meta query to retrieve subscribers
    $args = array(
            'meta_query' =&gt; array(
                    array( 'key' =&gt; 'state', 'value' =&gt; $state, 'compare' =&gt; '=' ),
                    array( 'key' =&gt; 'notification', 'value' =&gt; 'true', 'compare' =&gt; '=' )
                ),
            'fields' =&gt; array( 'display_name', 'user_email' )
        );
    // retrieve users to notify about the new post
    $users = get_users( $args );

    $num = 0;

    $to = 'Yourname &lt;you@yourdomain.com&gt;';

    $subject = sprintf( __( 'Hei! We have news for you from %s', 'smashing' ), $smashing_notification_states[$state] );

    $message = __( 'Hi ', 'smashing' ) . "\r\n" .
        sprintf( __( 'We have a new post from %s', 'smashing' ), $smashing_notification_states[$state] ) . "\r\n" .
        sprintf( __( 'Read more on %s', 'smashing' ), $url ) . '.' . "\r\n";  

    $headers[] = 'From: Yourname &lt;you@yourdomain.com&gt;';
    $headers[] = 'Reply-To: you@yourdomain.com';

    foreach ($users as $user) {
        $headers[] = 'Bcc: ' . $user-&gt;user_email;
        $num++;
    }

    if( wp_mail( $to, $subject, $message, $headers ) )
        update_post_meta( $post_ID, '_notified_users', $num );

    return $post_ID;
}
</code></pre>

As you can see, in case of <code>wp_mail()</code>’s success, we update the <code>_notified_user</code> custom field with <code>$num</code>’s value. However, in the code above, <code>$num</code> stores the number of retrieved users, not the number of times we call <code>wp_mail()</code>.

Finally, if none of the solutions presented fit your needs, you could consider a third-party email notification system, such as <a href="https://kb.mailchimp.com/campaigns/rss-in-campaigns/create-an-rss-driven-campaign">MailChimp</a> or <a href="https://support.google.com/feedburner/answer/78982?hl=en">FeedBurner</a>, which enable you to deliver notifications from a website’s feed.</p>

## A Note About Status Transitions

We hooked the <code>smashing_notify_new_post</code> callback to the <code>publish_post</code> action. This hook is triggered each time the status of an existing post is changed to <code>publish</code>. Unfortunately, <code>publish_post</code> is not fired when a new post is published. So, to send notifications, first save the post as “draft” (or “pending”). If you prefer to email subscribers each time a post is published, consider calling the <code>save_post</code> action instead:

<pre><code class="language-php">
add_action( 'save_post', 'smashing_notify_new_post' );
/*
 * Save the custom field values
 *
 * @param int $post_id the current post ID
 */
function smashing_notify_new_post( $post_ID ){
    global $smashing_notification_states;

    if( 'publish' != get_post_status( $post_ID ) )
        return;

    ...
}
</code></pre>

Check the Codex for further information about <a href="https://codex.wordpress.org/Post_Status_Transitions">status transitions</a> and the <a href="https://codex.wordpress.org/Plugin_API/Action_Reference/save_post"><code>save_post</code> action hook</a>.</p>

## A Confirmation Message

When you work with the <code>publish_post</code> action hook, you will soon realize that testing your scripts can get a little tricky. When a new post is published, WordPress loads a script that saves data and, when it is done, redirects the user to the post-editing page. This double redirection does not allow variable values to be printed on the screen.

A confirmation message could be a good workaround. This solution allows us to check a variable’s values and to give the publisher useful information: specifically, the number of times <code>wp_mail</code> has been called (or the number of users to be notified).

Remember the <code>$num</code> variable? Its value was stored in a hidden custom field, <code>_notified_users</code>. Now we have to retrieve that value and print it out in a message using a filter hook.

Thanks to the <code>post_updated_messages</code> filter, we can customize WordPress confirmation messages and output them to the screen whenever a new post is saved or published (the Codex does not provide a reference for this filter hook, only an <a href="https://codex.wordpress.org/Function_Reference/register_post_type#Example">example of usage</a>). Here is the callback function we can use to customize the message when a post is published:

<pre><code class="language-php">
add_filter( 'post_updated_messages', 'smashing_updated_messages' );

/**
 * Post update messages.
 *
 * See /wp-admin/edit-form-advanced.php
 *
 * @param array $messages Existing post update messages.
 *
 * @return array Amended post update messages with new update messages.
 */
function smashing_updated_messages( $msgs ){

    $post = get_post();
    $post_type = get_post_type( $post );
    $post_type_object = get_post_type_object( $post_type );

    $num = get_post_meta( $post-&gt;ID, '_notified_users', true );

    if ( $post_type_object-&gt;publicly_queryable ) {
        $msgs[$post_type][6] .= ' - ' . $num . __( ' notifications sent.', 'smashing' );
    }
    return $msgs;
}
</code></pre>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/07b07065-fdc7-4302-a6f0-772c9481b8fa/custom-message-preview-opt.png" alt="A custom message" /><br>
<figcaption>When a post is published, a custom message is printed informing the author about the number of emails sent to users.</figcaption></figure>

## wp_mail Function And SMTP

WordPress’ <code>wp_mail()</code> function works the same way as PHP’s <code>mail()</code> function. Whether an email has been successfully sent will depend on <code>php.ini</code>’s settings, but most hosts include SMTP in their services. If you aren’t able to set that up, you could choose an external SMTP service and use it in tandem with the <a href="https://wordpress.org/plugins/wp-mail-smtp/">WP Mail SMTP</a> plugin, which routes your emails through an SMTP service.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fc926115-1f72-4b1d-a943-21711d8ef167/wp-email-smtp-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d4d53587-12ba-4be9-8cb1-9f462e0ef332/wp-email-smtp-preview-opt.png" alt="WP Mail SMTP configuration panel" /></a><figcaption>WP Mail SMTP’s settings page. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fc926115-1f72-4b1d-a943-21711d8ef167/wp-email-smtp-large-opt.png">View large version</a>)</figcaption></figure>

Be careful when you save data: the “from” field should have the same value as your account’s email address; otherwise, the server might respond with an error message.

Be aware that a plugin is not necessary: WordPress allows for the possibility of overwriting <code>php.ini</code>’s settings from within a script, with the <code>phpmailer_init</code> action hook. This hook allows us to pass our own parameters to the <a href="https://phpmailer.worxware.com/">PHPMailer</a> object. <a href="https://codex.wordpress.org/Plugin_API/Action_Reference/phpmailer_init">See the Codex for more information</a> on this.</p>

## Designing Better Emails

Just like the PHP <code>mail()</code> function, <code>wp_mail()</code>’s default <code>Content Type</code> is <code>text/plain</code>. And just like the <code>mail()</code> function, <code>wp_mail()</code> allows us to set the <code>Content Type</code> to <code>text/html</code>. You can specify a different <code>Content Type</code> using the <code>wp_mail_content_type</code> filter or by setting the following headers:

<pre><code class="language-php">
$headers[] = "MIME-Version: 1.0";
$headers[] = "Content-Type: text/html; charset=ISO-8859-1";
</code></pre>

Of course, a number of plugins allow you to manage your email’s <code>Content Type</code> from the administration panel. <a href="https://wordpress.org/plugins/wp-better-emails/">WP Better Emails</a> is just one, but it’s one of the most appreciated. This plugin forces WordPress to send HTML emails, but it’s not its only feature. It also allows administrators to build their own email templates and to send arbitrary emails for testing purposes.

Finally, the following image shows what will be delivered to a Gmail user’s inbox.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/70765b6b-bbd3-4a43-a423-af74c33453de/better-email-large-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ece52f2f-fb84-4df3-97c8-5d5b8bef7556/better-email-preview-opt.png" alt="Description of the image." /></a><figcaption>The result in Gmail: The content has been generated by our code; SMTP parameters have been saved on WP Mail SMTP’s settings page; and the template is provided by WP Better Emails. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/70765b6b-bbd3-4a43-a423-af74c33453de/better-email-large-preview-opt.png">View large version</a>)</figcaption></figure>

## Conclusion

Our notification system is ready to be used. In building it, we’ve toured many of WordPress’ core features: user meta fields, custom meta boxes, custom queries, the mailing from script and more. If you’re interested, download the <a href="https://smashingmagazine.com/provide/sm-email-notification.zip">full code</a> (ZIP file), and remember to switch each occurrence of the <code>you@yourdomain.com</code> string with your own email address.

You can expand on this a lot more. You could integrate this system with a third-party email management application such as <a href="https://mailchimp.com/">MailChimp</a> or <a href="https://madmimi.com/">Mad Mimi</a>. You could design flashy email templates. Or you could create even more personalized notifications.</p>

### Further Reading

*   “[Create Perfect Emails For Your WordPress Website](https://www.smashingmagazine.com/2011/10/25/create-perfect-emails-wordpress-website/),” Daniel Pataki, Smashing Magazine
*   “[Post Status Transitions](https://codex.wordpress.org/Post_Status_Transitions),” WordPress Codex
*   “[Plugin API/Action Reference](https://codex.wordpress.org/Plugin_API/Action_Reference),” WordPress Codex
*   “[Plugin API/Filter Reference](https://codex.wordpress.org/Plugin_API/Filter_Reference),” WordPress Codex
*   “[Custom Fields](https://codex.wordpress.org/Custom_Fields),” WordPress Codex
*   “[Creating Custom Meta Boxes](https://developer.wordpress.org/plugins/metadata/custom-meta-boxes/),” Plugin Handbook, WordPress
*   “[Validating Sanitizing and Escaping User Data](https://codex.wordpress.org/Validating_Sanitizing_and_Escaping_User_Data),” WordPress Codex
*   “[Data Validation](https://codex.wordpress.org/Data_Validation),” WordPress Codex

{{< signature "dp, al, ml" >}}

