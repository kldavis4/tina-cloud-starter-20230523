---
title: How To Secure Your WordPress Website
slug: securing-your-wordpress-website
image: 'https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/39bd8b27-7eee-44dd-8d09-070d040973ab/illu-wp-14.jpg'
date: 2011-11-10T16:04:05.000Z
author: daniel-pataki
description: >-
  Security has become a foremost concern on the Web in the past few years.
  Hackers have always been around, but with the increase in computer literacy and the ease of access to virtually any data, the problem has increased exponentially. It is now rare for a new website to _not_ get comment spam within _days_ of its release, even if it is not promoted at all.
categories:
  - WordPress
  - Security
  - Techniques (WP)
---
This increase in naughty behavior, however, has spurred developers to write better code, and framework vendors have implemented many functions to help coders in their battle against the dark side.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [<span class="headline">Common WordPress Malware Infections</span>](https://www.smashingmagazine.com/2012/10/four-malware-infections-wordpress/)
*   [10 Useful WordPress Security Tweaks](https://www.smashingmagazine.com/2010/07/10-useful-wordpress-security-tweaks/)
*   [Checklist To Creating The Perfect WordPress Website](https://www.smashingmagazine.com/2011/12/15-step-checklist-creating-perfect-wordpress-website/)
*   [10 Steps To Protect The Admin Area In WordPress](https://www.smashingmagazine.com/2009/01/10-steps-to-protect-the-admin-area-in-wordpress/)

Because data validation and sanitization is a big part of both security safeguards and normal user-input processing, by securing our code we will be not only protecting our behinds, but offering a better, more solid user experience.

{{% feature-panel %}}

<a href="https://www.smashingmagazine.com/2011/11/10/securing-your-wordpress-website/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dc26f789-0716-456d-b52d-1a1ff1c0e5cf/securityimage.jpg" alt="securityimage" width="525" height="312" /></a>

While a large part of this article is specific to WordPress, a sizeable chunk is about general practices that anyone can use. Even the WordPress-centric sections contain useful logic, so reading them may well be worth it even if you use a different framework.</p>

## URL-Based Exploits

With URL-based exploits, hackers try to find weak spots on your website by making requests that would normally return an error but for some reason are completed.
<blockquote><code>https://mysite.com/trying/to/exploit/%2F/config</code></blockquote>

The above hypothetical URL is essentially a stab in the dark by a hacker. But if the request is met, even though the URL is clearly not meant to go anywhere, the hacker might be able to make use of it.</p>

### Using .htaccess as a Firewall

One of the best methods I’ve found against this kind of threat is an <em>.htaccess</em> firewall. It basically consists of rules that automatically block requests based on strings in the URL.

For example, there is no good reason for an opening bracket (<code>[</code>) to be in a URL. If a request is made using a URL that contains a bracket, then either the user has mistyped something or someone is looking for a security hole. Either way, generating a “403 Forbidden” page is good practice in this case.

<pre><code class="language-javascript">
RedirectMatch 403 [
</code></pre>

Paste the line above in your <em>.htaccess</em> file to block any request that contains an opening bracket.

To guard against more than just brackets, you will need a more complex ruleset. Luckily, our awesome editor Jeff Starr has gone out of his way to create a great <em>.htaccess</em> ruleset. The latest iteration is called <a href="https://perishablepress.com/5g-firewall-beta/">5G Firewall</a> and is freely available from Perishable Press for your copy-and-pasting pleasure.

The firewall is modular, so you can delete lines from it without breaking the functionality. If something goes wrong when you’re using it, you can usually track down the problem by deleting lines until it starts working again. Once you’ve found the offending line, you can delete it and paste back the rest.</p>

## Protecting Directories

On many servers, it is possible to view the contents of a directory simply by typing it in the URL bar.
<blockquote><code>https://myblog.com/wp-content/uploads/2011/08/</code></blockquote>

Visiting this typical URL for a WordPress blog will list the contents of that directory, showing all of the uploads from August 2011. You might want this, but you can also disable or fine tune it using the good ol’ <em>.htaccess</em> file.

<pre><code class="language-php">
Options -Indexes
</code></pre>

Popping the above line into your <em>.htaccess</em> file will disable directory listings; so, users will get a “403 Forbidden” message if they try to view a directory. While many people seem to be aware of this, far fewer know of the other options besides allowing or disallowing access. You can control which file types are listed using the <code>IndexIgnore</code> directive. Take these three examples:

<pre><code class="language-php">
IndexIgnore *
IndexIgnore *.php 
indexIgnore *.jpg *.gif *.png
</code></pre>

If directory listing is enabled, then the directory will be displayed in the first example, but no files will be listed because all will be ignored. The second example will list all files except ones with a <em>.php</em> extension. The third example will omit the three image types specified.

Note that some hosts (such as MediaTemple) disable directory browsing by default, so you won’t need to modify the <em>.htaccess</em> file. To verify this, just type a directory location in the URL bar and see what happens.</p>

### Additional Server-Level Protection

So far, the measures we have taken have nothing to do with our website’s actual code. However secure your code is, you will still need to implement something like what we did above. We don’t have time to look at all tips and tricks for <em>.htaccess</em>, but you can do quite a few other things:

*   Password-protect directories,
*   Use smart redirects,
*   Deny access based on IP or an IP range,
*   Force downloading of files,
*   Disable hotlinking,
*   The list goes on.

Look at the “Further Reading” section at the end of this article, and become good friends with your <em>.htaccess</em> file. It might seem daunting and confusing at first, but solid knowledge of how to use it will go a long way.</p>

## Protecting Against Malicious Users

The second type of problem that can arise is when someone performs an action that they are not supposed to do. This doesn’t necessarily mean that they intended to harm the website, but it could happen.

If users are listed somewhere in the admin part of your website, chances are that a link is displayed to delete each user. The link could point to the script in the following location:
<blockquote><code>https://mysite.com/admin/scripts/delete_user.php?user_id=5</code></blockquote>

This link is relatively obscure; that is, a normal user doesn’t have a good chance of stumbling on it. But if directory listings are enabled, then someone naughty could go to <code>https://mysite.com/admin/scripts/</code>, see that you have a <em>delete_user.php</em> file there, and make various requests to try to delete a user.

If the script does not check permission or intent, then anyone who visits the link above could delete user 5.</p>

### Authority and Intent

Whenever a user initiates an action, we need to take two things into consideration. Does the user have authority to perform the action (i.e. do they have permission)? If the user does have authority, do they also intend to complete the action (i.e. do they mean to do what they’re doing)?

WordPress has functions to help you make sure that both conditions are met before an action in the script is triggered. We will look at these in detail shortly. If you are building your website from scratch, then you will need to make sure that each user has associated permissions and that you know which action can be performed under which condition.

For example, you would probably want only administrators to be able to delete content from the website. Every time a user tries to delete content, you would need to make sure that they are actually an administrator — this is the “authority” part.

Intent is best described with an example. Let’s assume you can use the following link to delete a comment:
<blockquote><code>https://mysite.com/admin/scripts/delete_comment.php?comment_id=5</code></blockquote>

The script itself will check that the user is currently logged in and is an administrator, so it takes care of the authority check. Could someone still wreak havoc? Sure they could! A sneaky hacker could put a link on their own website pointing to the same location:
<blockquote><code>&lt;a href="https://mysite.com/admin/scripts/delete_comment.php?comment_id=5"&gt;Super-Happy Times Here!&lt;/a&gt;</code></blockquote>

Because everyone likes super-happy times, many users would click the link. In 99% of cases, nothing would happen, because those visitors would not be administrators of <code>mysite.com</code>. But if a logged-in administrator of <code>mysite.com</code> did click on the link, then the action would execute, even though the link was actually clicked from <code>vilehackerperson.com</code>.

You might think that the odds of this happening are astronomical. In a way you’d be right, but remember that a hacker can do this extremely easily and can automate it. Millions of people get spam email saying that Bill Gates will take away the Internet unless they pay $1,000. Most recipients don’t see the email or throw it out or mark it as spam or what have you, but perhaps 1 out of every 2 million people is lured in. A thousand bucks for basically doing nothing is not bad at all. And a hacker probably wouldn’t put the link on their own website; all they would need to do is hack a big website and embed the link there without anyone noticing.</p>

## Checking For Authority In WordPress

WordPress has a permissions system built in referred to as “<a href="https://codex.wordpress.org/Roles_and_Capabilities">Roles and Permissions</a>.” Capabilities are the basis of the whole system; roles are just a way to group a set of capabilities together.

If a user has the <code>delete_posts</code> capability, then they have the authority to delete posts. If a user has the <code>edit_posts</code> capability, then they can edit their posts. Quite a few capabilities are available, and you can even create your own.

Roles are basically groups of capabilities. A user with the role of “contributor” has three capabilities: <code>read</code>, <code>delete_posts</code> and <code>edit_posts</code>. These give the user the authority to read posts and to edit or delete their own posts. These capabilities could be granted individually to any user, but grouping them into frequently used bundles is much easier and more practical.

With that in mind, let’s look at how to use WordPress functions to ensure that a user has the authority to complete an action that they initiate.

<pre><code class="language-php">
if(current_user_can("delete_users")) {
    wp_delete_user(5);
}
else {
    die("You naughty, naughty person. Of course, you could just be logged out…");
}
</code></pre>

Here, we’ve made sure that the user has the <code>delete_users</code> capability before they are able to complete the action. Don’t make premature assumptions when protecting your scripts; in many cases, especially those of authority, the intent is not malicious.

The <code>current_user_can()</code> function takes one argument, which can be a role or a permission. We could let “editors” (who don’t normally have the <code>delete_users</code> capability) delete users in the following way:

<pre><code class="language-php">
if(current_user_can("editor")) {
    wp_delete_user(5);
}
else {
    die("You must be an editor to delete a user");
}
</code></pre>

Be careful with the method above because the roles are not inclusive. This function doesn’t require the user to be <em>at least</em> an editor; it requires them to be <em>exactly</em> an editor (if that makes sense). Because of this, I find it preferable to use capabilities, especially if I have modified the default permissions extensively.

Two other similar functions enable you to examine the capabilities of users other than the currently logged-in one.

<pre><code class="language-php">
if(user_can(5, "manage_links")) {
    echo "User 5 is allowed to manage links";
}
else {
    echo "Sadness! User 5 may not manage links";
}
if(author_can(1879, "update_themes")) {
    echo "The author of post #1879 is allowed to update themes";
}
else {
    echo "Oh noes, our friend, the author of post #1879 may not update themes";
}
</code></pre>

The <code>user_can()</code> function checks whether a given user has the given capability (or role). The first argument is the user’s ID or a user object; the second argument is the name of the capability or role that we want to check for.

The <code>author_can()</code> function checks whether the author of a given post has the given capability (or role). The first parameter should be a post ID or a post object; the second is the capability or role that we are examining.</p>

## Checking For Intent In WordPress

Intent is a bit more difficult to check. In the good ol’ days, a check of <code>$_SERVER['HTTP_REFERER']</code> was the way to go. This stored the page that the user came from. If the domain name was their own, then the user was probably OK… unless, of course, someone had gotten into their files and inserted a link that deleted the user’s database if they clicked on it as an administrator.

A newer more secure method was implemented in WordPress 2.03 — quite some time ago — called nonces. Nonce stands for “number used once” and is used frequently in cryptography to secure communications. It is a number that is generated before an action is initialized, then attached to the action’s call, and then checked before the action completes.

In WordPress, you would generally use nonces in one of two places: forms and normal links. Let’s look first at how to generate a nonce in a form.</p>

### Nonces in Forms

<pre><code class="language-markup">
&lt;form id="myform" method="post" action="myawesomescript.php"&gt;
    &lt;h2&gt;Enter an awesome word here&lt;/h2&gt;
    &lt;input type='text' name='word'&gt;
    &lt;?php wp_nonce_field( 'awesome_name_nonce') ?&gt;
&lt;/form&gt;
</code></pre>

This will generate a hidden input field containing your generated nonce, which will be sent along with all of the form’s other data. The <code>wp_nonce_field</code> function takes four parameters:

1.  The first parameter is optional, but recommended because it gives the nonce a unique identifier.
2.  The second parameter is the name of the field. This is also optional and defaults to `_wpnonce`.
3.  The third parameter is boolean. If set to `true`, it will also send the referrer for validation.
4.  The fourth parameter is also a boolean and controls whether the field is echoed right then and there.

The resulting hidden field would look something like this:

<pre><code class="language-markup">
&lt;input type="hidden" id="_wpnonce" name="_wpnonce" value="d6d71w4664"&gt;
</code></pre>

Setting all of this up won’t make a huge difference if it isn’t used when the form is actually processed. We need to check for the presence and the value of the nonce before allowing any actions to be performed. Here is one way to do that:

<pre><code class="language-php">
if (!wp_verify_nonce($_POST['_wpnonce'],'awesome_name_nonce') ) {
   die('Oops, your nonce didn't verify. So there.');
}
else {
   awesome_word_inserter($_POST["word"]);
}
</code></pre>

Here, we’ve used the <code>wp_verify_nonce()</code> function to make sure that our nonce is correct. This function takes two parameters: the first is the value of the nonce field, and the second is the name of the action that we defined (this was the first parameter for the <code>wp_nonce_field()</code> function). If the nonce is verified, then the function will return <code>true</code>; otherwise, it will return <code>false</code>.</p>

### Nonces in Links

In some cases, you will want a link, instead of a form, to perform an action. This would typically look like our previous examples:
<blockquote><code>https://mysite.com/admin/scripts/deletethatthing.php?thing_id=231</code></blockquote>

To generate a nonce for a link, we can use the following method:

<pre><code class="language-php">
$base_url = "https://mysite.com/admin/scripts/deletethatthing.php?thing_id=231";
$nonce_url = wp_nonce_url( $base_url, "thingdeleter_nonce");
echo "&lt;a href='".$nonce_url."'&gt;Delete that thing&lt;/a&gt;";
</code></pre>

The resulting link would be something like this:
<blockquote><code>https://mysite.com/admin/scripts/deletethatthing.php?thing_id=231&amp;_wpnonce=d6f77f1364</code></blockquote>

When we actually go to the script, we can check the nonce using the same method as before:

<pre><code class="language-php">
if (!wp_verify_nonce($_GET['_wpnonce'],'thingdeleter_nonce') ) {
   die('Oops, your nonce didn't verify. So there.');
}
else {
   delete_that_thing($_GET["thing_id"]);
}
</code></pre>

## Checking Authority And Intent At The Same Time

We need to look at both aspects at once; although, now that we’ve looked at all of the components, it won’t exactly be rocket science! Let’s take a simple link that lets the user delete a comment. We would have this on the page that lists comments:

<pre><code class="language-php">
$nonce_url = wp_nonce_url("https://mysite.com/scripts/delete_comment.php?comment_id=1451", "delete_comment_nonce");
echo "&lt;a href='".$nonce_url."'&gt;dispose of this comment&lt;/a&gt;";
</code></pre>

And here is the script itself:

<pre><code class="language-php">
if (wp_verify_nonce($_GET['_wpnonce'],'delete_comment_nonce') AND current_user_can("edit_comment")) {
   wp_delete_comment($_GET["comment_id"]);
}
else {
   die('Oops, your nonce didn't verify, or you are not permission-endowed enough.');
}
</code></pre>

## Data Security

Our work might seem to be done, but if you’ve been developing for a while, then you know it never is. An additional layer of security needs to be added to stop insecure data (or erroneous data) from entering our database. Adding this additional layer is called data sanitization.

A quick clarification: data sanitization refers to the process of cleaning up our data to make sure that nothing suspicious gets sent to the database. Validation refers to all of the checks we perform on data to make sure they are the types of data we need; it is typically done to ensure that the user has entered a valid email address, a well-formed URL, etc. The two terms are sometimes used interchangeably, and other methods may be similar, but they are quite different things. For our purposes, sanitization is a bit more important, because it has more to do with security.

The main thing we are trying to protect against is SQL injection. SQL injection is a technique used by hackers to exploit a database’s weaknesses. Take the following example:

<pre><code class="language-php">
// A hacker goes to your search field and searches for elephant' - note the apostrophe at the end. In the script, the following SQL is run:
SELECT ID, post_title FROM wp_posts WHERE post_title LIKE '%elephant'%'
</code></pre>

In the example above, the user’s search for <code>elephant'</code> has resulted in unclosed quotes in your script. While the hacker might not be able to do much with this, an error message would be generated, indicating to them that at the very <em>least</em> you are not sanitizing your data.

In some cases, the SQL itself could be harmful or could give the hacker much more information than you’d like. Take the example of an administrator being able to enter a user’s log-in name in a form and getting back the user’s email address.

<pre><code class="language-php">
SELECT user_email FROM wp_users WHERE user_login = 'danielp'
</code></pre>

If the hacker manages to perform an SQL injection attack, they could type <code>' OR 1=1 '</code> in the form, which would result in the following query:

<pre><code class="language-php">
SELECT user_email FROM wp_users WHERE user_login = ’ OR 1=1 ’
</code></pre>

This would return all email addresses in the database, because we would be retrieving all addresses for which the user’s log-in name is an empty string, or <code>1=1</code>, which is always <code>true</code>.

There are two ways to protect against this kind of problem — implementing both is good practice. In round one, we validate the data. If an email address needs to be entered, we can filter out user data that does not conform to the format of email addresses. We simply make sure that the format is right, otherwise we redirect the user, stating that the address is invalid. If the data passes round one, we move to round two, where we remove all characters that could mess up the query. This usually entails escaping quotes so that they can be used only as actual quotes in the SQL query.

When working without a framework, you would typically use <code>addslashes()</code> or something similar, but WordPress offers its own solution…

### Data Sanitization In WordPress

When communicating with the database in WordPress, the preferred method is to use the <code>$wpdb</code> class. You can read all about this in “<a href="https://www.smashingmagazine.com/2011/09/21/interacting-with-the-wordpress-database/">WordPress Essentials: Interacting With the WordPress Database</a>.” The class offers a number of methods to alleviate your SQL injection worries.

Before jumping in, let’s look at some examples to get a basic understanding of how the class works.

<pre><code class="language-php">
// Perform any query
$wpdb-&gt;query("DELETE FROM wp_users WHERE user_id = 5");
// Get one column of data
$posts = $wpdb-&gt;get_col("SELECT post_title FROM wp_posts WHERE post_status = 'publish' ORDER BY comment_count DESC LIMIT 0,10");
// Get a row of data
$post = $wpdb-&gt;get_row("SELECT * FROM wp_posts WHERE ID = 1453");
// Get multiple rows and columns
$posts = $wpdb-&gt;get_results("SELECT ID, post_title, post_date FROM wp_posts WHERE post_type = 'publish' ORDER BY post_date DESC LIMIT 0, 12 ");
// Get a single value 
$author_id = $wpdb-&gt;get_var("SELECT post_author FROM wp_posts WHERE ID = 2563");
// Insert a record
$wpdb-&gt;insert("wp_postmeta", array("post_id" =&gt; 2323,  "meta_key" =&gt; "favorite_count", "meta_value" =&gt; 224 ), array("%d", "%s", "%d"));
// Update a record
$wpdb-&gt;update("wp_postmeta", array("meta_value" =&gt; 225), array("meta_key" =&gt; "favorite_count", "post_id" =&gt; 2323), array("%d"), array("%s", "%d"));
</code></pre>

The <code>insert()</code> and <code>update()</code> methods are helper methods, and they’re great because, apart from modularizing your database interactions a bit, they also take care of sanitization for you. If you want to use the general <code>query()</code> method, though, you will need to take care of it on your own.

The easier way is just to use the <code>escape()</code> method:

<pre><code class="language-php">
$data = $wpdb-&gt;escape($_POST[about_me]);
$wpdb-&gt;query("UPDATE wp_usermeta SET meta_value = '$data' WHERE meta_key = 'description' AND user_id = 154  ");
</code></pre>

A slightly harder but better way to go about this is to use the <code>prepare()</code> method. An example from the WordPress Codex illustrates this perfectly:

<pre><code class="language-php">
$metakey = "Harriet's Adages";
$metavalue  = "WordPress' database interface is like Sunday Morning: Easy.";
$wpdb-&gt;query( $wpdb-&gt;prepare( 
   "
      INSERT INTO $wpdb-&gt;postmeta
      ( post_id, meta_key, meta_value )
      VALUES (Â %d,Â %s,Â %s )
   ", 
        10, 
   $metakey, 
   $metavalue 
) );
</code></pre>

### Further Protection Using Sanitization

Sanitization is a fairly big topic and requires quite some time to master. For now, you’ll be busy mostly determining which characters to allow and which to disallow, and then finding ways to parse out the latter. Some common needs are to parse HTML out of addresses, filter numbers out of strings, validate email addresses and so on, but you will need to implement your own solutions for more complex needs. See the “Further Reading” section for more on this topic.</p>

## Final Thoughts

The measures needed to secure a website cannot be discussed in a single book, let alone a poor article. There are many methods and topics we did not look at, such as advanced password encryption, salts and so on. But hopefully, by implementing what we’ve discussed, your website will be much safer. Hackers usually go for the weakest link, so if your website is not insanely popular and is fairly secure, you should be OK.

While I have a lot of experience in this field, I am far from being a security expert. If you know of any other or better methods, do share them in the comments. There is always something new to learn about website security.</p>

### General Reading

*   [5G Firewall](https://perishablepress.com/5g-firewall-beta/), Perishable Press
*   [Security tips for _.htaccess_](https://users.telenet.be/ws36178/security/webmaster/htaccess.html)
*   “[SQL Injection](https://en.wikipedia.org/wiki/SQL_injection),” Wikipedia
*   “[SQL Injection Attacks by Example](https://www.unixwiz.net/techtips/sql-injection.html),” Steve Friedl
*   “[MySQL: SQL Injection Prevention](https://www.tizag.com/mysqlTutorial/mysql-php-sql-injection.php),” Tizag
*   “[filter_var](https://www.php.net/manual/en/function.filter-var.php),” PHP.net
*   “[Sanitize and Validate Data with PHP Filters](https://net.tutsplus.com/tutorials/php/sanitize-and-validate-data-with-php-filters/),” Nettuts+

### WordPress-Specific Reading

*   “[Roles and Capabilities](https://codex.wordpress.org/Roles_and_Capabilities#edit_comment),” WordPress Codex
*   “<span class="removed_link" title="https://www.garyc40.com/2010/04/ultimate-guide-to-roles-and-capabilities/">Ultimate Guide to Roles and Capabilities</span>,” Gary Cao
*   “[WordPress 2.0.3: Nonces](https://markjaquith.wordpress.com/2006/06/02/wordpress-203-nonces/),” Mark Jaquith
*   “[Improving Security in WordPress Plugins Using Nonces](https://www.prelovac.com/vladimir/improving-security-in-wordpress-plugins-using-nonces),” Vladimir Prelovac
*   “[WordPress Nonces](https://codex.wordpress.org/WordPress_Nonces),” WordPress Codex
*   “[Class Reference/wpdb](https://codex.wordpress.org/Class_Reference/wpdb),” WordPress Codex
*   “[Data Validation](https://codex.wordpress.org/Data_Validation),” WordPress Codex

{{< signature "al" >}}

