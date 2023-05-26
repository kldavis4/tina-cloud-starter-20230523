---
title: How To Use AJAX In WordPress
slug: how-to-use-ajax-in-wordpress
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e2da9cc6-52ad-4b5d-bae2-ba3a66a8bf75/illusearch11.jpg
date: 2011-10-18T13:56:05.000Z
author: daniel-pataki
description: >-
  In the last few years AJAX has creeped into websites and has slowly become THE way to create dynamic, user friendly and responsive websites. AJAX is the technology that lets you update the contents of a page without actually having to reload it in a browser. For example, Google Docs utilizes this technology when saving your work every few minutes. This article has been reviewed and updated on July 14, 2017.
categories:
  - WordPress
  - PHP
  - JavaScript
---
While there are a number of ways to use AJAX in WordPress — and all are “correct,” in the loose sense of the word — there is one method that you should follow for a few reasons: WordPress supports it, it is future-proof, it is very logical, and it gives you numerous options right out of the box.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Web Design Industry Jargon and Web Terms](https://www.smashingmagazine.com/2009/05/web-design-industry-jargon-glossary-and-resources/)
*   [Why AJAX Isn’t Enough](https://www.smashingmagazine.com/2015/01/why-ajax-isnt-enough/)
*   [<span class="headline">How To Become A Top WordPress Developer</span>](https://www.smashingmagazine.com/2012/08/how-to-become-a-top-wordpress-developer/)
*   [<span class="headline">A Beginner’s Guide To Creating A WordPress Website</span>](https://www.smashingmagazine.com/2016/02/beginners-guide-creating-wordpress-website/)

{{% feature-panel %}}

## What Is AJAX?

AJAX is a combination of HTML, CSS and JavaScript code that enables you to send data to a script and then receive and process the script’s response without needing to reload the page.

If you’re not familiar with AJAX, I suggest continuing to the end of this article and <em>then</em> reading the <a href="https://en.wikipedia.org/wiki/Ajax_(programming)">Wikipedia article on AJAX</a>, followed by some <a href="https://www.smashingmagazine.com/2008/10/50-excellent-ajax-tutorials/">AJAX tutorials</a>. This is a rare case when I recommend reading as little about it as possible before trying it out, because it confused the heck out of me at first; and the truth is, you will rarely interact with AJAX in its “raw” state — you will usually use helpers such as jQuery.

If you are creating a page on your website where users can modify their profile, you could use AJAX to update a user’s profile without needing to constantly reload the page whenever they submit the form. When the user clicks the button, the data they have entered into the form is sent via AJAX to the processing script, which saves the data and returns the string “data saved.” You can then output that data to the user by inserting it onto the page.

The thing to grasp about AJAX is how <em>not</em> different it is from what you’re already doing. If you have a contact form, chances are that the form is marked up with HTML, some styles are applied to it, and a PHP script processes the information. The only difference between this and AJAX is <em>how</em> the information that the user inputs gets to the script and back to the user — everything else is the same.

To exploit the full potential of AJAX and get the most out of this article, you will need to be familiar with JavaScript (jQuery will suffice), as well as HTML, CSS and PHP. If your JavaScript knowledge is a bit iffy, don’t worry; you’ll still be able to follow the logic. If you need a hand, just submit a comment, and I’ll try to help out.</p>

### How Not To Use AJAX

One method that has been around, and which I used myself back in the bad old days, is to simply load the <em>wp-load.php</em> file at the top of your PHP script. This let’s you use WordPress functions, detect the current user and so on. But this is basically a hack and so is not future-proof. It is much less secure and does not give you some of the cool options that the WordPress system does.</p>

## How AJAX Works In WordPress Natively

Because AJAX is already used in WordPress’ back end, it has been basically implemented for you. All you need to do is use the functions available. Let’s look at the process in general before diving into the code.

Every AJAX request goes through the <em>admin-ajax.php</em> file in the <code>wp-admin</code> folder. That this file is named <em>admin-ajax</em> might be a bit confusing. I quite agree, but this is just how the development process turned out. So, we should use <em>admin-ajax.php</em> for back-end and user-facing AJAX.

Each request needs to supply at least one piece of data (using the <code>GET</code> or <code>POST</code> method) called <code>action</code>. Based on this action, the code in <em>admin-ajax.php</em> creates two hooks, <code>wp_ajax_my_action</code> and <code>wp_ajax_nopriv_my_action</code>, where <code>my_action</code> is the value of the <code>GET</code> or <code>POST</code> variable <code>action</code>.

Adding a function to the first hook means that that function will fire if a logged-in user initiates the action. Using the second hook, you can cater to logged-out users separately.

## Implementing AJAX In WordPress

Let’s build a rudimentary voting system as a quick example. First, create an empty plugin and activate it. If you need help with this part, look at the tutorial on <a href="https://www.smashingmagazine.com/2011/09/30/how-to-create-a-wordpress-plugin/">creating a plugin</a>. Also, find your theme’s <em>single.php</em> file, and open it.</p>

### Preparing to Send the AJAX Call

Let’s create a link that enables people to give a thumbs up to our articles. If a user has JavaScript enabled, it will use JavaScript; if not, it will follow the link. Somewhere in your <em>single.php</em> file, perhaps near the article’s title, add the following code:

<pre><code class="language-php">&lt;?php
   $votes = get_post_meta($post-&gt;ID, "votes", true);
   $votes = ($votes == "") ? 0 : $votes;
?&gt;
This post has &lt;div id='vote_counter'&gt;&lt;?php echo $votes ?&gt;&lt;/div&gt; votes&lt;br&gt;

&lt;?php
   $nonce = wp_create_nonce("my_user_vote_nonce");
    $link = admin_url('admin-ajax.php?action=my_user_vote&amp;post_id='.$post-&gt;ID.'&amp;nonce='.$nonce);
    echo '&lt;a class="user_vote" data-nonce="' . $nonce . '" data-post_id="' . $post-&gt;ID . '" href="' . $link . '"&gt;vote for this article&lt;/a&gt;';
?&gt;</code></pre>

First, let’s pull the value of the <code>votes</code> meta key related to this post. This meta field is where we will store the total vote count. Let’s also make sure that if it doesn’t exist (i.e. its value is an empty string), we show <code>0</code>.

We’ve also created an ordinary link here. The only extra bit is a pinch of security, using <a title="Excellent article about how nonces work" href="https://markjaquith.wordpress.com/2006/06/02/wordpress-203-nonces/">nonces</a>, to make sure there is no foul play. Otherwise, this is simply a link pointing to the <em>admin-ajax.php</em> file, with the action and the ID of the post that the user is on specified in the form of a query string.

To cater to JavaScript users, we have added a <code>user_vote</code> class, to which we will attach a click event, and a <code>data-post_id</code> property, which contains the ID of the post. We will use these to pass the necessary information to our JavaScript.</p>

### Handling the Action Without JavaScript

If you click this link now, you should be taken to the <em>admin-ajax.php</em> script, which will output <code>-1</code> or <code>0</code>. This is because no function has been created yet to handle our action. So, let’s get cracking!

In your plugin, create a function, and add it to the new hook that was created for us. Here’s how:

<pre><code class="language-php">add_action("wp_ajax_my_user_vote", "my_user_vote");
add_action("wp_ajax_nopriv_my_user_vote", "my_must_login");

function my_user_vote() {

   if ( !wp_verify_nonce( $_REQUEST['nonce'], "my_user_vote_nonce")) {
      exit("No naughty business please");
   }   

   $vote_count = get_post_meta($_REQUEST["post_id"], "votes", true);
   $vote_count = ($vote_count == ’) ? 0 : $vote_count;
   $new_vote_count = $vote_count + 1;

   $vote = update_post_meta($_REQUEST["post_id"], "votes", $new_vote_count);

   if($vote === false) {
      $result['type'] = "error";
      $result['vote_count'] = $vote_count;
   }
   else {
      $result['type'] = "success";
      $result['vote_count'] = $new_vote_count;
   }

   if(!empty($_SERVER['HTTP_X_REQUESTED_WITH']) &amp;&amp; strtolower($_SERVER['HTTP_X_REQUESTED_WITH']) == 'xmlhttprequest') {
      $result = json_encode($result);
      echo $result;
   }
   else {
      header("Location: ".$_SERVER["HTTP_REFERER"]);
   }

   die();

}

function my_must_login() {
   echo "You must log in to vote";
   die();
}</code></pre>

First of all, we’ve verified the nonce to make sure that the request is nice and legit. If it isn’t, we simply stop running the script. Otherwise, we move on and get the vote count from the database; make sure to set it to <code>0</code> if there is no vote count yet. We then add <code>1</code> to it to find the new vote count.

Using the <code>update_post_meta()</code> function, we add the new vote count to our post. This function creates the post’s meta data if it doesn’t yet exist, so we can use it to create, not just update. The function returns <code>true</code> if successful and <code>false</code> for a failure, so let’s create an array for both cases.

I like to create these result arrays for all actions because they standardize action handling, giving us good debugging information. And, as we’ll see in a second, the same array can be used in AJAX and non-AJAX calls, making error-handling a cinch.

This array is rudimentary. It contains only the type of result (error or success) and the vote count. In the case of failure, the old vote count is used (discounting the user’s vote, because it was not added). In the case of success, we include the new vote count.

Finally, we detect whether the action was initiated through an AJAX call. If so, then we use the <code>json_encode()</code> function to prepare the array for our JavaScript code. If the call was made without AJAX, then we simply send the user back to where they came from; obviously, they should be shown the updated vote count. We could also put the array in a cookie or in a session variable to return it to the user the same way, but this is not important for this example.

Always end your scripts with a <code>die()</code> function, to ensure that you get back the proper output. If you don’t include this, you will always get back a <code>-1</code> string along with the results.

The function to handle logged-out users is obviously poor, but it is meant merely as an example. You can expand on it by having it redirect the user to a registration page or by displaying more useful information.</p>

### Adding JavaScript to the Mix

Because we’ve now handled the user’s action using regular methods, we can start building in the JavaScript. Many developers prefer this order because it ensures graceful degradation. In order for our system to use AJAX, we will need to add jQuery, as well as our own JavaScript code. To do this, WordPress-style, just go to your plugin and add the following.

<pre><code class="language-php">add_action( 'init', 'my_script_enqueuer' );

function my_script_enqueuer() {
   wp_register_script( "my_voter_script", WP_PLUGIN_URL.'/my_plugin/my_voter_script.js', array('jquery') );
   wp_localize_script( 'my_voter_script', 'myAjax', array( 'ajaxurl' =&gt; admin_url( 'admin-ajax.php' )));        

   wp_enqueue_script( 'jquery' );
   wp_enqueue_script( 'my_voter_script' );

}</code></pre>

This is the WordPress way of including JavaScript files. First, we register the JavaScript file, so that WordPress knows about it (so make sure to create the file and place it somewhere in the plugin). The first argument to the <code>wp_register_script()</code> function is the “handle” of our script, which is a unique identifier. The second is the location of the script. The third argument is an array of dependencies. Our script will require jQuery, so I have added it as a dependency. WordPress has already registered jQuery, so all we needed to add was its handle. For a detailed list of the scripts that WordPress registers, look at the <a title="List of WordPress default scripts" href="https://codex.wordpress.org/Function_Reference/wp_enqueue_script#Default_scripts_included_with_WordPress">WordPress Codex</a>.

Localizing the script is not strictly necessary, but it is a good way to define variables for our script to use. We need to use the URL of our <em>admin-ajax.php</em> file, but because this is different for every domain, we need to pass it to the script. Instead of hard-coding it in, let’s use the <code>wp_localize_script()</code> function. We add the script handle as the first argument, an object name as the second argument, and we can add object members as an array in the third parameter. What this all boils down to is that, in our <em>my_voter_script.js</em> file, we will be able to use <code>myAjax.ajaxurl</code>, which contains the URL of our <em>admin-ajax.php</em> file.

Once our scripts have been registered, we can actually add them to our pages by enqueueing them. We don’t need to follow any particular order; WordPress will use the correct order based on the dependencies.

Once that’s done, in the <em>my_voter_script.js</em> JavaScript file, paste the following code:

<pre><code class="language-javascript">jQuery(document).ready( function() {

   jQuery(".user_vote").click( function(e) {
      e.preventDefault(); 
      post_id = jQuery(this).attr("data-post_id")
      nonce = jQuery(this).attr("data-nonce")

      jQuery.ajax({
         type : "post",
         dataType : "json",
         url : myAjax.ajaxurl,
         data : {action: "my_user_vote", post_id : post_id, nonce: nonce},
         success: function(response) {
            if(response.type == "success") {
               jQuery("#vote_counter").html(response.vote_count)
            }
            else {
               alert("Your vote could not be added")
            }
         }
      })   

   })

})</code></pre>

Let’s go back to the basics. This would be a good time for those of us who are new to AJAX to grasp what is going on. When the user clicks the vote button without using JavaScript, they open a script and send it some data using the <code>GET</code> method (the query string). When JavaScript is used, it opens the page for them. The script is given the URL to navigate to and the same parameters, so apart from some minor things, from the point of view of the script being run, there is no difference between the user clicking the link and an AJAX request being sent.

Using this data, the <code>my_user_vote()</code> function defined in our plugin should process this and then send us back the JSON-encoded result array. Because we have specified that our response data should be in JSON format, we can use it very easily just by using the response as an object.

In our example, all that happens is that the vote counter changes its value to show the new vote count. In reality, we should also include some sort of success message to make sure the user gets obvious feedback. Also, the alert box for a failure will be very ugly; feel free to tweak it to your liking.</p>

## Conclusion

This concludes our quick tutorial on using AJAX in WordPress. A lot of functionality could still be added, but the main point of this article was to show how to properly add AJAX functionality itself to plugins. To recap, the four steps involved are:

1.  Make the AJAX call;
2.  Create the function, which will handle the action;
3.  Add the function to the hook, which was dynamically created for us with the action parameter;
4.  Create success handlers as needed.

As mentioned, make sure everything works well without JavaScript before adding it, so that the website degrades properly for people who have disabled it.

Keep in mind that, because we are using hooks, we can also tie existing WordPress functions to our AJAX calls. If you already have an awesome voting function, you could just tie it in after the fact by attaching it to the action. This, and the ease with which we can differentiate between logged-in states, make WordPress’ AJAX-handling system very powerful indeed.

{{< signature "al" >}}

