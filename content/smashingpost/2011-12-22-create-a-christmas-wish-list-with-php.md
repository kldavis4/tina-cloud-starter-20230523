---
title: Create A Christmas Wish List With PHP (For Beginners)
slug: create-a-christmas-wish-list-with-php
image: null
date: 2011-12-22T13:09:52.000Z
author: daniel-pataki
description: >-
  Please notice that this article doesn't provide production code to use in your live websites. Make sure to read the full article and study more on PHP security before using the code listed in this article.
categories:
  - Coding
  - PHP
  - MySQL
---
’Tis the season to be jolly, and how much jollier could we make it than with a helpful Christmas wish list crafted for your family to ensure that you get maximum presentage this holiday? In this article, we will focus on creating a very simple system that allows you to add gift ideas to a Web page, and for your family (or whoever) to view the list.

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Getting Started With PHP Templating](https://www.smashingmagazine.com/2011/10/getting-started-with-php-templating/)
*   [A Beginner’s Guide To jQuery-Based JSON API Clients](https://www.smashingmagazine.com/2012/02/beginners-guide-jquery-based-json-api-clients/)
*   [50 Extremely Useful PHP Tools](https://www.smashingmagazine.com/2009/01/50-extremely-useful-php-tools/)
*   [60 Beautiful Christmas Photoshop Tutorials – 2016/2017 Edition](https://www.smashingmagazine.com/2008/12/beautiful-christmas-photoshop-tutorials/)

{{% feature-panel %}}

Please notice that this article was <strong>written for beginners who already grasp HTML and CSS</strong>, know a bit of PHP and have seen phpMyAdmin before. I will not go into best practices, safety and all the rest of it; let’s just have fun with this one!

### Preparing Our Resources

Before creating the website, let’s see the finished product:

<img style="border: 1px solid #CCC" title="Product" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1af4a116-d6bf-48ad-b19e-f17c0e498c8c/product.png" alt="screenshot" width="500" /><br>
<em>The finished Christmas wish list.</em>

The result will contain three pages: the list itself, a log-in page and an admin page. We will also have a style sheet, two scripts (for logging people in and saving items) and some images. You can view an online demo of the code to see the end result.

Below is a list of the resources I have used. Go ahead and grab them, but feel free to use your own! Please note the licence on each; some are free for commercial use, but some are free only for personal use.

*   I based the colors on the “[’Tis the Season](https://www.colourlovers.com/palette/130451/Tis_the_Season)” color palette from COLOURlovers.
*   The Santa icon in the logo is from the [“Santa” icon set](https://www.iconfinder.com/icondetails/40232/102/5_christmas_sack_santa_icon), downloaded from Iconfinder.
*   The Christmas style font is called “[Mountains of Christmas](https://www.google.com/webfonts#ChoosePlace:select/Collection:Mountains+of+Christmas)” and was obtained from Google Web Fonts
*   I created the background pattern by playing around with the background maker on [BG Patterns](https://bgpatterns.com/).</p>

## File Structure

We know that we’ll need three pages (list, log-in and admin), but let’s look at the full list of files that we will need. Feel free to create these as empty files in advance.

*   `index.php`
*   `login.php`
*   `admin.php`
*   `header.php`
*   `footer.php`
*   `config.php`
*   `script-login.php`
*   `script-additem.php`
*   `images`
*   `uploads`

The first three files should be self-explanatory; they will handle the content of our three main pages. We will also use a separate header and footer file; the purpose of these files is to minimize duplicate code.

For all three of our pages, we’ll need to create the code for the header section (i.e. the Santa icon and the title, plus the actual HTML head section and so on). Instead of writing the code three times (which would make the code hard to update), we will write it out once and include the code in all three files.

We’ll also include the <code>config.php</code> file in each file. This sets up the database connection and handles a few other things that are needed for every page.

The next two files in the list are scripts that handle logging in and adding new items to the list.

Finally, we have two directories. The <code>images</code> directory will contain the images we need for our website’s framework. The <code>uploads</code> directory will contain all of the images for our uploaded items.</p>

## A Word Of Warning

Note that this is meant as a beginner’s exercise. The code you see here will give you the intended result, but a lot of it is not safe for production websites. It lacks a lot of safeguards, such as data validation, salts for passwords (for better security), htaccess rules and so on. The goal of this article is to let beginners forget about all of these things and just concentrate on building something nice.

Neither does this article promote best practices. You may find yourself adopting different methods later on, or I may write in another article that we shouldn’t do something you see here. The article is intended as a fun little example for beginners to spice up their boring theory sessions. I believe that the best way to learn is through increasingly difficult examples.

That said, I encourage you to try all of this out and play around with it at home or on your servers. If you put this on a live server, I recommend using an account that has only this website on it (or only test websites). I also recommend using passwords for user accounts that are not the same as your other passwords.</p>

## Creating Our Framework

Our mini-framework consists of the header and the basic structure of the page. Let’s see what this would look like in HTML:

<pre><code class="language-markup tmp-html">&lt;!DOCTYPE html&gt;
&lt;html&gt;
   &lt;head&gt;
      &lt;meta http-equiv="Content-Type" content="text/html; charset=UTF-8"&gt;

      &lt;title&gt;My Christmas List&lt;/title&gt;

      &lt;!-- Style sheets --&gt;
      &lt;link href='style.css' rel='stylesheet' type='text/css'&gt;

   &lt;/head&gt;
   &lt;body&gt;

      &lt;div id="site_header"&gt;
         &lt;img id="site_logo" src='images/santa_logo.png' alt='The Santa Logo' &gt;
         &lt;h1&gt;Daniel Pataki's Christmas List&lt;/h1&gt;
         &lt;div class="clear"&gt;&lt;/div&gt;
      &lt;/div&gt;

      &lt;div id="site_container"&gt;

      &lt;/div&gt;

   &lt;/body&gt;
&lt;/html&gt;</code></pre>

### The Head

As you know from your studies in HTML, the code above consists of two main sections. The code inside the <code>&lt;head&gt;</code> section is not visible to the user. The <code>&lt;head&gt;</code> contains meta information (such as keywords and a description of the website), the title, the style sheets used, the JavaScript files needed and so on.

Your Web page must have the <code>&lt;head&gt;</code> element and at the very least must contain a <code>&lt;title&gt;</code> element. The content of the <code>&lt;title&gt;</code> tag will be seen in the browser tab. In our case, we have also tied a style sheet to our website using a <code>&lt;link&gt;</code> element.</p>

### The Body

Your Web page must also contain a <code>&lt;body&gt;</code> element, even an empty one. Of course, nothing much would happen if we left it empty, so I’ve added the header of our website and the main content area.

The header of our website will be seen on all pages. This is the section with the Santa logo and the title “Daniel Pataki’s Christmas List.”

I’ve used a regular image tag to set the image, and a top-level heading to create the title. I’ve also used an empty <code>&lt;div&gt;</code> element, giving it a class of <code>clear</code>. The reason for this has to do with positioning (more on this when we get to the CSS).

Once we’re done with the header, we need a big white container to hold our list. This is done with a simple <code>&lt;div&gt;</code>, which we’ve given a class of <code>site_container</code>.

Finally, we close the <code>&lt;body&gt;</code> and <code>&lt;html&gt;</code> tags, and we make sure our code is valid by running it through the HTML Validator. Don’t worry yet if your code is invalid. Try to fix what you can, but don’t worry if something isn’t working. Your goal now is to get things working; you’ll have plenty of time later to worry about best practices.</p>

### Splitting Up

The code we’ve just written will be common to all of our pages. The only thing we’ll change is the content inside the <code>site_container</code> div (which is currently empty). To avoid having to add this same code three times, it is a good practice to separate it into two files: a header and footer file.

Everything common to the top part of each page should go in <code>header.php</code>, and everything common to the bottom part should go in <code>footer.php</code>.

Copy and paste everything up to and including <code>&lt;div id='site_container'&gt;</code> into the <code>header.php</code> file. Copy and paste everything else into the <code>footer.php</code> file.

If you load the website right now, you should see an empty page with no content. This is because <code>index.php</code> is being shown but is currently empty, so we need to pull in the header and footer code. Use the following code to make that happen.

<pre><code class="language-php">&lt;?php include('header.php'); ?&gt;

&lt;?php include('footer.php') ?&gt;</code></pre>

If you load the Web page now, you should see the code in place. It will be awfully ugly, but we’ll change all that in a jiffy.</p>

### Adding Some Style

Now that our structure is in place, it’s time to make it look nice. Achieving what you see in the finished product is actually very easy, so let’s jump right in.

<strong>Resetting styles</strong>
The first thing to do with many websites is to reset all browser-specific properties. Each browser handles headings, tables, inputs and other elements slightly differently, so let’s reset all of these styles, which will make the page ugly but at least uniform on every platform.

<pre><code class="language-css">body,div,dl,dt,dd,ul,ol,li,h1,h2,h3,h4,h5,h6,pre,form,fieldset,input,textarea,p,blockquote,th,td {
   margin:0;
   padding:0;
}

table {
   border-collapse:collapse;
   border-spacing:0;
}

fieldset,img {
   border:0;
}

address,caption,cite,code,dfn,em,strong,th,var {
   font-style:normal;
   font-weight:normal;
}

ol,ul {
   list-style:none;
}

caption,th {
   text-align:left;
}

h1,h2,h3,h4,h5,h6 {
   font-size:100%;
   font-weight:normal;
}

q:before,q:after {
   content:’;
}

abbr,acronym {
   border:0;
}</code></pre>

This is a commonly used reset called <a href="https://developer.yahoo.com/yui/reset/">YUI 2 Reset CSS</a>. You can copy and paste it from here, and you can also find it on the Yahoo Developer Network.

<strong>Overall structure</strong>
The overall structure consists of the body, the header section and the website container. Let’s concentrate on putting these in the right places and adding the proper background to our website.

<pre><code class="language-css">html, body {
   background:url('images/bg.png');
   color:#555;
   font-size:14px;
}

#site_header {
   width:740px;
   margin:0 auto;
}

#site_header h1 {
   font-family: Mountains of Christmas;
   font-size:42px;
   letter-spacing:1px;
   color:#fff;
   position:relative;
   top:60px;
   font-weight:700;
   text-shadow:-1px -1px 1px #3a5e40
}

#site_logo {
   float:left;
   position:relative;
   top:36px;
   left:-24px;
}

#site_container {
   background:#fff;
   width:700px;
   padding:42px 20px;
   margin:0 auto;
   border:3px solid #7b9971;
}</code></pre>

This should be pretty easy to follow. Let me expand on a few points of interest.

<strong>Embedding fonts</strong>
It’s a good bet that the Mountains of Christmas font is not installed on your or your visitors’ computers, but we can still use it through the magic of CSS3 and with help from <a href="https://www.google.com/webfonts">Google Web Fonts</a>. Go to Google’s website now, choose any font, and follow the instructions to use it.

Before referring to a font in your CSS file, you need to embed it with the following code, which goes in the <code>&lt;head&gt;</code> section of your website:

<pre><code class="language-markup tmp-html">&lt;link href='https://fonts.googleapis.com/css?family=Mountains+of+Christmas:700' rel='stylesheet' type='text/css'&gt;</code></pre>

<strong>Clearing elements</strong>
If you load the website with this code, the header will seem to collapse into the content area, because the image inside the header is floated left. Whenever you float an element inside another element, you need to make sure the floats are cleared to prevent the content from collapsing like this.

While this behavior might seem odd, it has a logic. Have a look at A List Apart for a <a href="https://www.alistapart.com/articles/css-floats-101/">good article on floats</a>. Right now, all we need to do is create an empty element at the bottom of the parent element, which will clear the floats above it. To accomplish this, paste the following into the CSS sheet:

<pre><code class="language-css">.clear {
   clear:both;
}</code></pre>

Now that we’re done with our little framework, let’s add some content to the website!

## Creating The Database

Before moving on, you’ll need to put a database structure in place. If you are using your localhost to follow along, you should be able to get to your database through one of the following:

*   `https://localhost/phpMyAdmin`
*   `https://localhost/phpMyAdmin`
*   `https://localhost:8888/phpMyAdmin`
*   `https://localhost:8888/phpMyAdmin`

The usual problem with accessing phpMyAdmin is that it needs to be capitalized in some installations but not in others. If you use a port number after localhost, make sure to add it.

Once you’re there, find the “Create a new database” field and type <code>christmaslist</code> to create the database. Then, create two new tables with the following structure:

<img style="border: 1px solid #CCC" title="user-schema" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/91250722-ba73-4774-a8bb-6144471b99fc/user-schema.png" alt="screenshot" width="500" height="289" /><br>
<em>Creating the user table.</em>

<img style="border: 1px solid #CCC" title="item-schema" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a9d9ed32-390b-490d-b246-a6e7b0bbb043/item-schema.png" alt="screenshot" width="500" height="285" /><br>
<em>Creating the item table.</em>

Go to the “Privileges” tab in phpMyAdmin to set up a user who can access the database that you just created. Later on, you will need the name of the database, the user name and the password to access it.

Once that’s done, manually create a user in the database. Make sure to select the SHA1 function next to the password field.

<img style="border: 1px solid #CCC" title="sha1" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c1c2745d-25f7-4519-b1cd-f4bc8a4a1e63/sha1.png" alt="screenshot" width="500" /><br>
<em>Encoding a field with SHA1.</em>

### Connecting to the Database

While you now have a database, you will need to actually connect to it before you are able to use it. Whenever you need data from the database, you will need to connect to it, retrieve the data and then close the connection.

Just like with the header section of the website, you will be using this database so often that writing the code once and including it on every page would be best.

Let’s go into <code>config.php</code> and add the following code.

<pre><code class="language-php">&lt;php
$db = new mysqli("localhost", "db_username", "db_password", "db_name");
?&gt;</code></pre>

This code connects to your database and makes it possible for you to read the data and write to the database. But you might have noticed that the <code>config.php</code> file is not referred to anywhere on our page. Let’s fix that by including it in the <code>header.php</code> file, which is included on every page.

<pre><code class="language-php">include("config.php");</code></pre>

Our code now opens a connection to the database. Because it is included in the header file, we will be able to grab data on any page that we are on. Once we’ve done that, we’ll need to close the connection. We can do this in the <code>footer.php</code> file, because that is the last thing on the page and we won’t need to perform any database actions after the <code>&lt;html&gt;</code> closing tag. So, paste the following line there:

<pre><code class="language-php">&lt;?php $db-&gt;close(); ?&gt;</code></pre>

## Logging In

We want to let only people who we know in on this project, so let’s protect it with a log-in function. A user will enter their name and password, and our script will check whether a user with these credentials is in the database.</p>

### HTML and CSS

Go to the <code>login.php</code> file, and create a log-in form like this:

<pre><code class="language-markup tmp-html">&lt;form method="post" action="script-login.php"&gt;

   &lt;h1&gt;Please log in&lt;/h1&gt;

   &lt;label for="username"&gt;username&lt;/label&gt;
   &lt;input type="text" name="username" id="username"&gt;
   &lt;br&gt;
   &lt;label for="password"&gt;password&lt;/label&gt;
   &lt;input type="password" name="password" id="password"&gt;
   &lt;br&gt;

   &lt;input type="submit" value="Log In" class='submit'&gt;

&lt;/form&gt;</code></pre>

While the form is usable as is, it looks a bit funny, so let’s add some CSS style to spruce it up:

<pre><code class="language-css">h1 {
   font-family:georgia;
   margin:0 0 12px 0;
   font-size:32px;
   color:#7b9971;
}

input, textarea {
   border:1px solid #7b9971;
   background:#e9fce3;
   padding:5px;
   font-size:16px;
   width:300px;
   margin:0 0 6px 0;
   display:block;
}
textarea {
   height:140px;
}
label {
   font-size:13px;
   margin:0 0 4px 0;
}
input.submit {
   border:0px;
   width:auto;
   color:#fff;
   background:#941f1f;
   font-size:12px;
   padding:5px 12px;
   border:1px solid #7d1515;
}</code></pre>

The data from this form will be submitted using the <code>POST</code> method, which is safer for most data transfers. The difference between the <code>POST</code> and <code>GET</code> methods is mainly that data transmitted via the <code>GET</code> method can be seen in the URL, while data passed with the <code>POST</code> method cannot.</p>

### The PHP Script

Once the user has submitted the form, the data will be transferred to <code>script-login.php</code>, so let’s go there now and deal with the data:

<pre><code class="language-php">include("config.php");

$username = $_POST['username'];
$password = sha1($_POST['password']);

$query = "SELECT ID FROM user WHERE username = '$username' AND password = '$password'";

if ($result = $db-&gt;query($query)) {
   while ($user = $result-&gt;fetch_object()) {
      $_SESSION['user'] = $user-&gt;ID;
      header("Location: index.php");
   }
}
else {
   header("Location: login.php");
}

$db-&gt;close();</code></pre>

Remember how we included <code>config.php</code> file in every file? What gives? Why are we including it here as well? Since this is a script, we do not need our usual header section. We just need to process some data and move the user along.

Our <code>config.php</code> file is included in <code>header.php</code>, so if there’s no <code>header.php</code> file here, then there won’t be any <code>config.php</code> code either. So, we need pull in the <code>config.php</code> file separately and also close the database connection in the last line.

Let’s break the code down. First, we store the user name and password in two separate variables. This is not necessary but adds clarity. You might have noticed the <code>sha1()</code> function being used. This is an algorithm that converts plain-text passwords into a string that is almost impossible to decipher.

When a user registers and gives “superawesome” as their password, this is immediately run through the SHA1 algorithm. Instead of storing the plain-text password, we store the result of the algorithm, which is <code>0ac45a31f4576e727746e0ab26b916df0e0eb890</code>.

When the user logs in, we don’t actually know (or care) what the plain-text password is. We simply take the value that they’ve entered and use the SHA1 algorithm to see whether the SHA1-encoded password stored for the user’s name is the same as this SHA1-encoded string. If it is, then the user is allowed to log in.

The power of this method is that an intruder would not be able to see the user’s password even if they had direct access to the database. Sure, they’d see that the user’s SHA1-encoded password is <code>0ac45a31f4576e727746e0ab26b916df0e0eb890</code>, but they wouldn’t be able to do a whole lot with that.

Moving on, we write our query and store it in a variable. We check that the ID of the person whose user name has been entered is correct <em>and</em> that the password belonging to that user name is the given password. If both criteria are met at once, we can log the user in.

The query is executed by the following code: <code>$result = $db-&gt;query($query)</code>. I have encased this in an <code>if</code> statement. If we get a result, we will be able to use it through the <code>$result</code> variable. If we don’t get a result, then the whole expression will be <code>false</code>, and so we wouldn’t let the user log in and would just redirect them to the <code>login.php</code> page.

If we do get a result, then we know that the user has already entered a correct user name and password combination, so we’d let them log in and redirect them to the main list.

We do this by looping over the retrieved users (there will be only one) and storing the user’s data in the <code>$user</code> variable. We then create a session variable using the user’s ID and check for its presence on every page. If it is not present, then we’d know that the user is not logged in and so we would redirect them to <code>login.php</code>. Finally, we would direct the user to the main list.

To make this work, we need to do one more thing. Session variables can be used to pass data from one page to another, but we need to start a session first. As long as a session has been started on a page, we can pass values to it from other pages. This sounds like something we’ll need on all pages, so let’s add it to our <code>config.php</code> file, right at the top.

<pre><code class="language-php">session_start();</code></pre>

If you go now to the log-in form and enter a valid user name and password combination, the following should happen. You should be directed to the script that checks for a user with the given credentials. If it finds them, it creates <code>$_SESSION['user']</code> with the value of the user’s ID. It will then direct you to main list (<code>index.php</code>), where the session variable should be available.

You can check this by going to the <code>index.php</code> file and echoing the contents of <code>$_SESSION['user']</code>.</p>

### Redirecting Logged-Out Users

Because we’ve set the session variable for all logged-in users, we can redirect anyone who doesn’t have this variable set to the log-in page. By the way, these session variables will remain usable until the user closes the browser.

We will also need redirection on all pages, so let’s add it to the <code>config.php</code> file at the very bottom, like so:

<pre><code class="language-php">if( (!isset($_SESSION['user']) OR empty($_SESSION['user'])) AND $_SERVER['REQUEST_URI'] != '/login.php') {
   header("Location: login.php");
}</code></pre>

If the session variable is not set or is empty (and the user is not on the log-in page), then we redirect the user to the log-in page. The last bit is needed because we want to allow everyone on to the log-in page — even people without a session variable, of course.</p>

## The Admin Page

Our <code>admin.php</code> file will consist of a simple form to add new items. By now you should not be able to visit this page if you are merely logged in. Open up the <code>admin.php</code> file and let’s add our form.

<pre><code class="language-markup tmp-html">&lt;form method="post" action="script-additem.php" enctype="multipart/form-data"&gt;
   &lt;h1&gt;Add an Item&lt;/h1&gt;

   &lt;label for="name"&gt;name&lt;/label&gt;
   &lt;input id="name" name="name" type="text"&gt;

   &lt;label for="description"&gt;description&lt;/label&gt;
   &lt;textarea id="description" name="description"&gt;&lt;/textarea&gt;

   &lt;label for="link"&gt;link&lt;/label&gt;
   &lt;input id="link" name="link" type="text"&gt;

   &lt;label for="price"&gt;price&lt;/label&gt;
   &lt;input id="price" name="price" type="text"&gt;

   &lt;label for="image"&gt;image&lt;/label&gt;
   &lt;input type="file" name="file" id="file"&gt;

<pre><code class="language-php">include("config.php");</code></pre>

Our code now opens a connection to the database. Because it is included in the header file, we will be able to grab data on any page that we are on. Once we’ve done that, we’ll need to close the connection. We can do this in the <code>footer.php</code> file, because that is the last thing on the page and we won’t need to perform any database actions after the <code>&lt;html&gt;</code> closing tag. So, paste the following line there:

<pre><code class="language-php">&lt;?php $db-&gt;close(); ?&gt;</code></pre>

## Logging In

We want to let only people who we know in on this project, so let’s protect it with a log-in function. A user will enter their name and password, and our script will check whether a user with these credentials is in the database.</p>

### HTML and CSS

Go to the <code>login.php</code> file, and create a log-in form like this:

<pre><code class="language-markup tmp-html">&lt;form method="post" action="script-login.php"&gt;

   &lt;h1&gt;Please log in&lt;/h1&gt;

   &lt;label for="username"&gt;username&lt;/label&gt;
   &lt;input type="text" name="username" id="username"&gt;
   &lt;br&gt;
   &lt;label for="password"&gt;password&lt;/label&gt;
   &lt;input type="password" name="password" id="password"&gt;
   &lt;br&gt;

   &lt;input type="submit" value="Log In" class='submit'&gt;

&lt;/form&gt;</code></pre>

While the form is usable as is, it looks a bit funny, so let’s add some CSS style to spruce it up:

<pre><code class="language-css">h1 {
   font-family:georgia;
   margin:0 0 12px 0;
   font-size:32px;
   color:#7b9971;
}

input, textarea {
   border:1px solid #7b9971;
   background:#e9fce3;
   padding:5px;
   font-size:16px;
   width:300px;
   margin:0 0 6px 0;
   display:block;
}
textarea {
   height:140px;
}
label {
   font-size:13px;
   margin:0 0 4px 0;
}
input.submit {
   border:0px;
   width:auto;
   color:#fff;
   background:#941f1f;
   font-size:12px;
   padding:5px 12px;
   border:1px solid #7d1515;
}</code></pre>

The data from this form will be submitted using the <code>POST</code> method, which is safer for most data transfers. The difference between the <code>POST</code> and <code>GET</code> methods is mainly that data transmitted via the <code>GET</code> method can be seen in the URL, while data passed with the <code>POST</code> method cannot.</p>

### The PHP Script

Once the user has submitted the form, the data will be transferred to <code>script-login.php</code>, so let’s go there now and deal with the data:

<pre><code class="language-php">include("config.php");

$username = $_POST['username'];
$password = sha1($_POST['password']);

$query = "SELECT ID FROM user WHERE username = '$username' AND password = '$password'";

if ($result = $db-&gt;query($query)) {
   while ($user = $result-&gt;fetch_object()) {
      $_SESSION['user'] = $user-&gt;ID;
      header("Location: index.php");
   }
}
else {
   header("Location: login.php");
}

$db-&gt;close();</code></pre>

Remember how we included <code>config.php</code> file in every file? What gives? Why are we including it here as well? Since this is a script, we do not need our usual header section. We just need to process some data and move the user along.

Our <code>config.php</code> file is included in <code>header.php</code>, so if there’s no <code>header.php</code> file here, then there won’t be any <code>config.php</code> code either. So, we need pull in the <code>config.php</code> file separately and also close the database connection in the last line.

Let’s break the code down. First, we store the user name and password in two separate variables. This is not necessary but adds clarity. You might have noticed the <code>sha1()</code> function being used. This is an algorithm that converts plain-text passwords into a string that is almost impossible to decipher.

When a user registers and gives “superawesome” as their password, this is immediately run through the SHA1 algorithm. Instead of storing the plain-text password, we store the result of the algorithm, which is <code>0ac45a31f4576e727746e0ab26b916df0e0eb890</code>.

When the user logs in, we don’t actually know (or care) what the plain-text password is. We simply take the value that they’ve entered and use the SHA1 algorithm to see whether the SHA1-encoded password stored for the user’s name is the same as this SHA1-encoded string. If it is, then the user is allowed to log in.

The power of this method is that an intruder would not be able to see the user’s password even if they had direct access to the database. Sure, they’d see that the user’s SHA1-encoded password is <code>0ac45a31f4576e727746e0ab26b916df0e0eb890</code>, but they wouldn’t be able to do a whole lot with that.

Moving on, we write our query and store it in a variable. We check that the ID of the person whose user name has been entered is correct <em>and</em> that the password belonging to that user name is the given password. If both criteria are met at once, we can log the user in.

The query is executed by the following code: <code>$result = $db-&gt;query($query)</code>. I have encased this in an <code>if</code> statement. If we get a result, we will be able to use it through the <code>$result</code> variable. If we don’t get a result, then the whole expression will be <code>false</code>, and so we wouldn’t let the user log in and would just redirect them to the <code>login.php</code> page.

If we do get a result, then we know that the user has already entered a correct user name and password combination, so we’d let them log in and redirect them to the main list.

We do this by looping over the retrieved users (there will be only one) and storing the user’s data in the <code>$user</code> variable. We then create a session variable using the user’s ID and check for its presence on every page. If it is not present, then we’d know that the user is not logged in and so we would redirect them to <code>login.php</code>. Finally, we would direct the user to the main list.

To make this work, we need to do one more thing. Session variables can be used to pass data from one page to another, but we need to start a session first. As long as a session has been started on a page, we can pass values to it from other pages. This sounds like something we’ll need on all pages, so let’s add it to our <code>config.php</code> file, right at the top.

<pre><code class="language-php">session_start();</code></pre>

If you go now to the log-in form and enter a valid user name and password combination, the following should happen. You should be directed to the script that checks for a user with the given credentials. If it finds them, it creates <code>$_SESSION['user']</code> with the value of the user’s ID. It will then direct you to main list (<code>index.php</code>), where the session variable should be available.

You can check this by going to the <code>index.php</code> file and echoing the contents of <code>$_SESSION['user']</code>.</p>

### Redirecting Logged-Out Users

Because we’ve set the session variable for all logged-in users, we can redirect anyone who doesn’t have this variable set to the log-in page. By the way, these session variables will remain usable until the user closes the browser.

We will also need redirection on all pages, so let’s add it to the <code>config.php</code> file at the very bottom, like so:

<pre><code class="language-php">if( (!isset($_SESSION['user']) OR empty($_SESSION['user'])) AND $_SERVER['REQUEST_URI'] != '/login.php') {
   header("Location: login.php");
}</code></pre>

If the session variable is not set or is empty (and the user is not on the log-in page), then we redirect the user to the log-in page. The last bit is needed because we want to allow everyone on to the log-in page — even people without a session variable, of course.</p>

## The Admin Page

Our <code>admin.php</code> file will consist of a simple form to add new items. By now you should not be able to visit this page if you are merely logged in. Open up the <code>admin.php</code> file and let’s add our form.

<pre><code class="language-markup tmp-html">&lt;form method="post" action="script-additem.php" enctype="multipart/form-data"&gt;
   &lt;h1&gt;Add an Item&lt;/h1&gt;

   &lt;label for="name"&gt;name&lt;/label&gt;
   &lt;input id="name" name="name" type="text"&gt;

   &lt;label for="description"&gt;description&lt;/label&gt;
   &lt;textarea id="description" name="description"&gt;&lt;/textarea&gt;

   &lt;label for="link"&gt;link&lt;/label&gt;
   &lt;input id="link" name="link" type="text"&gt;

   &lt;label for="price"&gt;price&lt;/label&gt;
   &lt;input id="price" name="price" type="text"&gt;

   &lt;label for="image"&gt;image&lt;/label&gt;
   &lt;input type="file" name="file" id="file"&gt;

   &lt;input type="submit" class="submit" value="add item"&gt;

&lt;/form&gt;</code></pre>

Our existing styles should make this look OK, so we can go straight to the points of interest. This is all pretty standard unless you’ve never looked at file uploads.

To enable file uploads, we need to add two things to the form: an input field of the type <code>file</code>, and the encoding type (in this case, <code>multipart/form-data</code>). If you want to be able to upload files, you will always have to specify the <code>enctype</code> parameter.

We blew through that pretty quickly, so let’s continue with the script that does the heavy lifting, <code>script-additem.php</code>:

<pre><code class="language-php">include("functions.php");

$target_path = $_SERVER['DOCUMENT_ROOT']."/uploads/";
$target_path = $target_path . basename( $_FILES['file']['name']);
$file_location = "uploads/".$_FILES['file']['name'];
move_uploaded_file($_FILES['file']['tmp_name'], $target_path);

$query = "INSERT INTO item (name, description, price, link, image) VALUES ('$_POST[name]', '$_POST[description]', '$_POST[price]', '$_POST[link]', '$file_location')";
$result = $db-&gt;query($query);

$db-&gt;close();
header("Location: admin.php?uploaded=true");</code></pre>

The first thing to take care of is file uploading. We created the uploads directory for this purpose, so let’s pass the path to it to our script.

Take care because this may not be the code you need to use. If you are using a subdirectory, you may need to use <code>$_SERVER['DOCUMENT_ROOT']."/subdirectory/uploads/"</code> or something like it. If in doubt, print out the contents of the <code>$_SERVER</code> variable and try to find your path from there.

Once our target directory path is set, we need to add the file name to it to make it a complete path. Our target path now contains the absolute path to the file, something like <code>/home/username/public_html/christmaslist/uploads/myuploadedimage.jpg</code>.

To make sure we have the URL that we’ll add to the database, we store it in the <code>$file_location</code> variable. This is different from <code>$target_path</code> because it doesn’t have the <code>/home/username/public_html/christmaslist</code> part of the URL.

We use the <code>move_uploaded_file($_FILES['file']['tmp_name'], $target_path);</code> line to upload the files. The <code>move_uploaded_file()</code> function takes two arguments: the temporary location of the file and the new location that we want to put it in.

At this point, our image has been uploaded. It’s time to add the data of the item to the database. The data we need contains the URL of the image as well, which is why we had to upload the image before adding the item to the database.

We store our query inside the <code>$query</code> variable, execute it, close the connection and redirect the user back to <code>admin.php</code>. I added the <code>?uploaded=true</code> query string to the URL; we will use this to show the user a confirmation message. Head back to the <code>admin.php</code> file and paste the following in it just under the include:

<pre><code class="language-php">&lt;?php
   if(isset($_GET['uploaded']) AND $_GET['uploaded'] == "true") {
      echo "
&lt;div class="success"&gt;The item has been added&lt;/div&gt;
";
   }
?&gt;</code></pre>

This is the <code>GET</code> method, and as you can see, the data is visible in the URL. Using this here is OK, of course; we’re just using it to detect whether an item has been successfully added. To make it prettier, we’ll style this <code>div</code> like so:

<pre><code class="language-css">.success {
   padding:5px 12px;
   background:#7b9971;
   border:#7b9971 - #222 solid 1px;
   color:#fff;
   margin:0 0 12px 0;
}</code></pre>

The form should now be ready to use, so go ahead and add three to four test items, complete with images and all.</p>

## Listing Our Gift Ideas

The only thing left to do is list the items in the database for our visitors. Let’s head over to the <code>index.php</code> file and add the following code to do this:

<pre><code class="language-php">&lt;?php include('header.php'); ?&gt;

&lt;table class='item_list'&gt;

&lt;?php
   $query = "SELECT * FROM item";
   $result = $db-&gt;query($query);

   if($result) : while ($item = $result-&gt;fetch_object()):
?&gt;

   &lt;tr class='item'&gt;
      &lt;td class='item_image'&gt;
         &lt;img width="150" src='&lt;?php echo $item-&gt;image ?&gt;'&gt;
      &lt;/td&gt;
      &lt;td class='item_content'&gt;
         &lt;h2 class='item_name'&gt;&lt;?php echo $item-&gt;name ?&gt;&lt;/h2&gt;
         &lt;div class='item_description'&gt;&lt;?php echo nl2br($item-&gt;description) ?&gt;&lt;/div&gt;
      &lt;/td&gt;
      &lt;td class='item_price'&gt;
         &lt;h3&gt;
            &lt;a href='&lt;?php echo $item-&gt;link ?&gt;'&gt;
               &lt;span class='price'&gt;$&lt;?php echo number_format($item-&gt;price) ?&gt;&lt;/span&gt;
            &lt;/a&gt;
         &lt;/h3&gt;
         &lt;a class='text' href='&lt;?php echo $item-&gt;link ?&gt;'&gt;Buy This&lt;/a&gt;
      &lt;/td&gt;
   &lt;/tr&gt;

&lt;?php endwhile; endif; ?&gt;
&lt;/table&gt;

&lt;?php include('footer.php') ?&gt;</code></pre>

The frame of this page is created by including the header at the top and the footer at the bottom. This includes pulling in our <code>config.php</code> file and closing our connection, so we can forget about that here.

We’ll pull in all of the items and show them using a table. We use <code>while ($item = $result-&gt;fetch_object())</code> to iterate through all of the results. We want the exact same structure for each results: a three-column row. The first column will show the image, the second will show the name and a description, and the third will show the price and a purchase link.

The two functions worth mentioning here are <code>nl2br()</code> and <code>number_format()</code>. The former converts line breaks into <code>&lt;br&gt;</code> tags. The latter converts numbers into a nicely formatted string, adding in thousand separators as needed.

To make this all nice and proper, let’s add some CSS:

<pre><code class="language-css">.item td {
   border-bottom:1px solid #ccc;
   padding:12px 0;
}

.item_image img {
   margin:0 16px 0 0;
}

.item_price h3 {
   margin:0px;
}

.item_price a {
   font-weight:700;
   font-family:Mountains of Christmas;
   color:#941f1f;
   text-decoration:none;
}

.item_price a:hover {
   color:#941f1f + #252525;
}

.item_price .price {
   font-size:52px;
}

.item_price .text {
   position:relative;
   top:-12px;
}

.item_content {
   padding:0 42px 0 0;
   width:340px;
}

.item_content h2 {
   font-size:24px;
   font-family:georgia;
}</code></pre>

## A Note On SQL Security

While this article as a whole should not be used in production environments (it is only a basic example to aid in your studies) commenters have pointed out - correctly - that some level of SQL security should be added.

A great (and simple) method of protecting against any naughtiness (like <a href="https://en.wikipedia.org/wiki/SQL_injection">SQL injection</a>) is to escape strings.

Instead of using the data from variables directly we'll first run them through the <a href="https://php.net/manual/en/mysqli.real-escape-string.php"><code>mysqli_real_escape_string() </code></a> function which will take care of the work for us. Let's take a look at an example which we could use to search our items.

<pre><code class="language-php">$term = $_GET['term']; // This is the term the user searched for
$term = $db-&gt;real_escape_string($term);
$query = "SELECT * FROM item WHERE name LIKE '%$term%' ";
$result = $db-&gt;query($query);</code></pre>

You can use this method to make sure all your SQL code is better suited to a working environment. A more elaborate (but even safer) way to go is preparing your statements. Preparing your statements using <a href="https://php.net/manual/en/mysqli.prepare.php"><code>mysqli_prepare()</code></a> is a more effective way of ensuring proper safety.

In addition to all this you should be sanitizing and validating any data that your application receives. This involves making sure that when you're looking for a date you receive the correct format (or convert into it), if a value needs to be between 1-10 it indeed is, and so on.

Creating a secure environment is a mammoth task which you won't be able to lear all at once. However there are many small things (like escaping string) you can do which will make your site much more secure.</p>

## The Way Forward

If you’ve been following along, you should now have a rudimentary but functioning website that lists your gift ideas. It is far from complete, but you can already expand on the knowledge and practice you’ve gained here by adding a user-registration form to <code>admin.php</code> that enables you to add users from the back end.

If you use a couple of other readily available techniques, you can add a whole bunch of other useful features, such as:

*   Enabling pagination of gift items (if you have a ton of requests);
*   Enabling public access to the list but not the admin section;
*   Enabling public access to the list but restricting access to the admin section so that only you can use it (i.e. not even other logged-in users);
*   Enabling themes for other holidays;
*   Allowing logged-in users to reserve gifts or indicate that they have bought one;
*   Enabling different currencies;
*   So much more.</p>

### Closing Thoughts

I would like to stress again that this was not an exercise in best practices, safety, security or flawless coding standards. It was an exercise to get beginners started, without bogging them down with a lot of supplementary information; a fun exercise to give you something tangible quite quickly. You can work on making it better and more secure and feature-rich on your own.

If you have any questions or get stuck, do drop a comment. I or someone in the community will surely help out as soon as we can! Don't forget to check out the online demo.

Happy holidays, and I hope you get all the items on your list!

