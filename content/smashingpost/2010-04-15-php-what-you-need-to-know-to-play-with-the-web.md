---
title: 'PHP: What You Need To Know To Play With The Web'
slug: php-what-you-need-to-know-to-play-with-the-web
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/39442f29-7fb5-45af-9346-bd963c215dce/php-01.jpg
date: 2010-04-15T13:20:54.000Z
author: christian-heilmann
description: >-
  In this article, I'll introduce you to the fundamentals of PHP. We'll focus on
  **using PHP to access Web services** and on turning static HTML pages into dynamic ones by retrieving data from the Web and by showing different content depending on what the user has entered in a form or requested in the URL.
categories:
  - Coding
  - PHP
---
You won't come out a professional PHP developer, but you'll be well on your way to building a small page that uses Web services. You can find a lot of great PHP info on the Web, and most of the time you will end up on <a href="https://php.net">PHP.net</a> itself. But I was asked repeatedly on several hack days and competitions to write this quick introduction article, so here it is.

Also consider the following Smashing Magazine articles:

*   [50 Extremely Useful PHP Tools](https://www.smashingmagazine.com/2009/01/50-extremely-useful-php-tools/)
*   [Getting Started With PHP Templating](https://www.smashingmagazine.com/2011/10/getting-started-with-php-templating/)
*   [How Do You Design Interaction?](https://www.smashingmagazine.com/2014/07/how-do-you-design-interaction/)

## What Is PHP?

PHP is a server-side language that has become a massive success for three reasons:

{{% feature-panel %}}

*   It is a very easy and forgiving language. Variables can be anything, and you can create them anytime you want.
*   It is part of the free LAMP stack (Linux, Apache, MySQL, PHP) and thus available on almost any server you can rent on the Web.
*   It does not need a special editor, environment or build process. All you do is create a file of the _.php_ file type, mix PHP and HTML and then put it on your server for rendering.</p>

## Installing PHP Locally, And Your First Code

To run PHP locally on your computer, you'll need a local server with PHP enabled. The easiest way to do this is to download and install <a href="https://www.mamp.info/en/index.html">MAMP for OS X</a> or <a href="https://www.apachefriends.org/en/xampp-windows.html">XAMPP for Windows</a>. Once you've installed any of these packages, you can start using PHP. Simply create a file named <em>index.php</em> in the <em>htdocs</em> folder of your MAMP or XAMPP installation.

In this file, type (or copy and paste) the following:

<pre><code class="language-php">&lt;?php
  $myname = 'Chris';
  echo '&lt;p&gt;This is PHP&lt;/p&gt;';
  echo "&lt;p&gt;My name is $myname&lt;/p&gt;"
  echo '&lt;p&gt;My name in another notation is still  '.$myname.'&lt;/p&gt;';
?&gt;</code></pre>

If you open this file in a browser by accessing your XAMPP or MAMP installation (via <code>https://localhost/index.php</code> or <code>https://localhost:8888/index.php</code>), you should see the following:

<pre><code class="language-php">This is PHP
My name is Chris
My name in another notation is still Chris</code></pre>

But you won't see that. The problem is that the third line does not end in a semicolon (<code>;</code>). This is an error. Depending on your PHP installation, you'll get either an error message or simply nothing. If you get nothing, then find the file named <em>php_error.log</em> on your hard drive, and open it. It will tell you what went wrong.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1558a647-0c7c-485e-8bfc-371e97c2dfa4/phperrorlog1.jpg" alt="The PHP error log as shown on a Mac" width="450" />

The first thing to remember, then, is that every line of PHP has to end in a semicolon. If we fix this problem, we get this result:

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dd77fdd7-a630-4373-971d-7d24e41e2786/php-rendered1.jpg" alt="PHP rendered in a browser" width="450" />

<pre><code class="language-php">&lt;?php
  $myname = 'Chris';
  echo '&lt;p&gt;This is PHP&lt;/p&gt;';
  echo "&lt;p&gt;My name is $myname&lt;/p&gt;";
  echo '&lt;p&gt;My name in another notation is still  '.$myname.'&lt;/p&gt;';
?&gt;</code></pre>

We can see here the first few important features of PHP:

*   PHP blocks start with `<?php` and end with `?>`. Anything between these two commands is interpreted as being PHP and returned to the document as HTML.
*   Every line of PHP has to end with a semicolon (`;`), or else it is an error.
*   Variables in PHP start with a `$`, not with the `var` keyword as you do in JavaScript (this is where it gets confusing with jQuery and Prototype).
*   You print content to the document in PHP with the `echo` command. There is also a `print` command, which does almost the same, so you can use that, too.
*   In this example, we have defined a string named `myname` as "Chris". To print it with the `echo` command surrounded by other text, you need to either embed the variable name in a text with quotation marks or concatenate the string with a full stop when you use single quotation marks. This is line 3 and 4: they do the same thing but demonstrate the different syntax. Concatenation is always achieved with a full stop, never with a `+` as you do in JavaScript.

You can jump in and out of PHP anywhere in the document. Thus, interspersing PHP with HTML blocks is totally fine. For example:

<pre><code class="language-php">&lt;?php
  $origin = 'Outer Space';
  $planet = 'Earth';
  $plan = 9;
  $sceneryType = "awful";
?&gt;
&lt;h1&gt;Synopsis&lt;/h1&gt;

&lt;p&gt;It was a peaceful time on planet &lt;?php echo $planet;?&gt; 
and people in the &lt;?php echo $sceneryType;?&gt; scenery were unaware 
of the diabolical plan &lt;?php echo $plan;?&gt; from &lt;?php echo $origin;?&gt; 
that was about to take their senses to the edge of what could be endured.&lt;/p&gt;</code></pre>

This outputs the following:

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6fc354a8-0578-4bf4-85ca-e797bfa7557f/variables-rendered1.jpg" alt="Rendered variables in PHP" width="450" />

Are you with me so far? To show something on the screen, particularly numbers or a string, we use <code>echo</code>. To show more complex structures, we need loops or specialized debugging methods.</p>

## Displaying More Complex Data Types

You can define arrays in PHP using the <code>array()</code> method:

<pre><code class="language-php">$lampstack = array('Linux','Apache','MySQL','PHP');</code></pre>

If you simply want to display a complex data type like this in PHP for debugging, you can use the <code>print_r()</code> command:

<pre><code class="language-php">$lampstack = array('Linux','Apache','MySQL','PHP');
print_r($lampstack);</code></pre>

This gives you all the information, but it doesn't help you structure it as HTML:

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7ccbbd30-74b4-4113-bfa5-e18c3fb78df8/print-r-demo1.jpg" alt="Displaying arrays with print_r" width="450" />

For this, you need to access the elements with the array counter. In PHP this is done with the <code>[]</code> brackets:

<pre><code class="language-php">&lt;ul&gt;
&lt;?php
$lampstack = array('Linux','Apache','MySQL','PHP');
echo '&lt;li&gt;Operating System:'.$lampstack[0] . '&lt;/li&gt;';
echo '&lt;li&gt;Server:' . $lampstack[1] . '&lt;/li&gt;';
echo '&lt;li&gt;Database:' . $lampstack[2] . '&lt;/li&gt;';
echo '&lt;li&gt;Language:' . $lampstack[3] . '&lt;/li&gt;';
?&gt;
&lt;/ul&gt;</code></pre>

See this demo in action.

This is, of course, stupid programming because it is not flexible. If a computer is able to the dirty work for you, make it do it. In this case, we can define two arrays and use a loop:

<pre><code class="language-php">&lt;ul&gt;
&lt;?php
$lampstack = array('Linux','Apache','MySQL','PHP');
$labels = array('Operating System','Server','Database','Language');
$length = sizeof($lampstack);
for( $i = 0;$i &lt; $length;$i++ ){
  echo '&lt;li&gt;' . $labels[$i] . ':' . $lampstack[$i] . '&lt;/li&gt;';
}
?&gt;
&lt;/ul&gt;</code></pre>

The <code>for</code> loop works the same as it does in JavaScript. The only difference is that you read the size of an array not with <code>array.length</code> but with <code>sizeof($array)</code>.

Again, this example is not very clever because it assumes that both the <code>$lampstack</code> and the <code>$labels</code> array are of the same length and in the same order. Instead of using this, I'd use an associated array:

<pre><code class="language-php">&lt;ul&gt;
&lt;?php
$lampstack = array(
  'Operating System' =&gt; 'Linux',
  'Server' =&gt; 'Apache',
  'Database' =&gt; 'MySQL',
  'Language' =&gt; 'PHP'
);
$length = sizeof($lampstack);
$keys = array_keys($lampstack);
for( $i = 0;$i &lt; $length;$i++ ){
  echo '&lt;li&gt;' . $keys[$i] . ':' . $lampstack[$keys[$i]] . '&lt;/li&gt;';
}
?&gt;
&lt;/ul&gt;</code></pre>

The function <code>array_keys()</code> gives you back all the keys of an array as an array itself. This way, we can display the keys and the values at the same time.

A shorter way to achieve the same principle, and which works with both arrays and objects, is to use the <code>foreach()</code> loop construct:

<pre><code class="language-php">&lt;ul&gt;
&lt;?php
$lampstack = array(
  'Operating System' =&gt; 'Linux',
  'Server' =&gt; 'Apache',
  'Database' =&gt; 'MySQL',
  'Language' =&gt; 'PHP'
);
foreach( $lampstack as $key =&gt; $stackelm ){
  echo '&lt;li&gt;' . $key . ':' . $stackelm . '&lt;/li&gt;';
}
?&gt;
&lt;/ul&gt;</code></pre>

This is the shortest way to display a complex construct. But it will fail when <code>$lampstack</code> is not an array. So, checking for <code>sizeof()</code> is still a good plan. You can do this with a conditional.

## Using Conditionals

Conditionals are "if" statements, both in the English language and in almost any programming language I know. So, to test whether an array is safe to loop over, we could use the <code>sizeof()</code> test:

<pre><code class="language-php">&lt;ul&gt;
&lt;?php
$lampstack = array(
  'Operating System' =&gt; 'Linux',
  'Server' =&gt; 'Apache',
  'Database' =&gt; 'MySQL',
  'Language' =&gt; 'PHP'
);
if( sizeof($lampstack) &gt; 0 ){
  foreach( $lampstack as $key =&gt; $stackelm ){
    echo '&lt;li&gt;' . $key . ':' . $stackelm . '&lt;/li&gt;';
  }
}
?&gt;
&lt;/ul&gt;</code></pre>

Common conditionals are:

*   `if($x > 10 and $x < 20)` Is `$x` bigger than 10 and less than 20?
*   `if(isset($name))` Has the variable `$name` been defined?
*   `if($name == 'Chris')` Does the variable `$name` have the value of "Chris"?
*   `if($name == 'Chris' or $name == 'Vitaly')` Does the variable `$name` have the value of "Chris" or "Vitaly"?

Cool, but what if we want to make this reusable?

## Functions In PHP

To make a task even more generic, we can write a <code>function</code>. In this case, we put the loop and the testing in a function and simply call it with different arrays:

<pre><code class="language-php">&lt;?php
function renderList($array){
  if( sizeof($array) &gt; 0 ){
    echo '&lt;ul&gt;';
    foreach( $array as $key =&gt; $item ){
      echo '&lt;li&gt;' . $key . ':' . $item . '&lt;/li&gt;';
    }
    echo '&lt;/ul&gt;';
  }
}
$lampstack = array(
  'Operating System' =&gt; 'Linux',
  'Server' =&gt; 'Apache',
  'Database' =&gt; 'MySQL',
  'Language' =&gt; 'PHP'
);
renderList($lampstack);

$awfulacting = array(
  'Natalie Portman' =&gt; 'Star Wars',
  'Arnold Schwarzenegger' =&gt; 'Batman and Robin',
  'Keanu Reaves' =&gt; '*'
);
renderList($awfulacting);
?&gt;</code></pre>

Note that <code>function</code>s do not begin with a dollar sign.

We've already seen most of the magic of PHP. The rest is all about building functions to do all kinds of things: converting strings, sorting arrays, finding things in other things, accessing the file system, setting cookies and much more, each of which does one and only one thing right. I keep catching myself writing complex functions in PHP, only to realize from looking at the documentation that a native function already exists for it.</p>

## Interacting With The Web: URL Parameters

Let's start playing with the Web in PHP… or, more precisely, playing with information that comes from the browser's address bar or with forms that we can re-use. To get parameters from the current URL, we use the global <code>$_GET</code> array. So, if you call the <em>index.php</em> script with <code>https://localhost/index.php?language=fr&amp;font=large</code>, you can change the display and locale by checking for these settings. The <code>language</code> parameter will be available as <code>$_GET['language']</code>, and the <code>font</code> parameter as <code> $_GET['font']</code>:

<pre><code class="language-php">&lt;?php
$name = 'Chris';

// if there is no language defined, switch to English
if( !isset($_GET['language']) ){
  $welcome = 'Oh, hello there, ';
}
if( $_GET['language'] == 'fr' ){
  $welcome = 'Salut, ';
}
switch($_GET['font']){
  case 'small':
    $size = 80;
  break;
  case 'medium':
    $size = 100;
  break;
  case 'large':
    $size = 120;
  break;
  default:
    $size = 100;
  break;
}
echo '&lt;style&gt;body{font-size:' . $size . '%;}&lt;/style&gt;';
echo '&lt;h1&gt;'.$welcome.$name.'&lt;/h1&gt;';
?&gt;</code></pre>

This means we can now send URL parameters to change the behavior of this document:

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c4f27964-08f3-4b39-b642-1efc53347453/parameters1.jpg" alt="changing the content and look of a document with parameters" width="450" />

*   `https://localhost:8888/index.php`
*   `https://localhost:8888/index.php?language=fr`
*   `https://localhost:8888/index.php?language=fr&font=large`

Notice that predefining a set of values that are acceptable for a certain parameter is always best. In the earlier example, we may as well have set the font size in pixels as a parameter and then written that to the document—but then we would have needed a good validation script to prevent end users from sending bad values or even malicious code through the parameter.

Sending malicious code via a parameter without filtering is called <a href="https://www.owasp.org/index.php/Cross-site_Scripting_%28XSS%29">cross-site scripting</a> (XSS), and it is one of the big security problems of the Web. You can prevent it by not printing out the values of parameters, and instead using them in comparisons, and by using the <a href="https://uk.php.net/manual/en/intro.filter.php">filters provided by PHP</a>.

Say you want to allow users to enter data in a form that you will display later on. Make sure to filter out the results:

<pre><code class="language-php">&lt;?php
  $search_html = filter_input(INPUT_GET, 's',
                              FILTER_SANITIZE_SPECIAL_CHARS);
  $search_url = filter_input(INPUT_GET, 's',
                             FILTER_SANITIZE_ENCODED);
?&gt;
&lt;form action="index.php" method="get"&gt;
  &lt;div&gt;
    &lt;label for="search"&gt;Search:&lt;/label&gt;
    &lt;input type="text" name="s" id="search" 
           value="&lt;?php echo $search_html;?&gt;"&gt;
  &lt;/div&gt;
  &lt;div class="bar"&gt;&lt;input type="submit" value="Make it so"&gt;&lt;/div&gt;
&lt;/form&gt;
&lt;?php
if(isset($_GET['s'])){
  echo '&lt;h2&gt;You searched for '.$search_html.'&lt;/h2&gt;';
  echo '&lt;p&gt;&lt;a href="index.php?search='.$search_url.'"&gt;Search again.&lt;/a&gt;&lt;/p&gt;';
}
?&gt;</code></pre>

See this filtering example in action. Without the filters, attackers could send parameters like <code>index.php?s="&lt;script&gt;</code>, which would execute third-party code on your website. With filtering, this malicious code is converted to HTML entities.

If you want to use <code>POST</code> as the method to send the data in your form, then the PHP variables will change accordingly to <code>$_POST</code> for the array and <code>INPUT_POST</code> for the filter.</p>

## Loading Content From The Web

PHP comes with a lot of file functions that allow you to read and write files from the hard drive or to load content from the Web. I've found, however, that for security reasons a lot of hosting companies disable them, especially when you try to read content from a third-party resource. The workaround is to use cURL to load information from the Web. cURL is a tool that allows you to make HTTP requests to retrieve information—a kind of browser in command-line form. I've <a href="https://www.wait-till-i.com/2009/12/18/curl-your-view-source-of-the-web/">written a detailed post about cURL and how to use it</a>. Here, then, is a simple use case to illustrate:

<pre><code class="language-php">&lt;?php
  // define the URL to load
  $url = 'https://www.smashingmagazine.com';
  // start cURL
  $ch = curl_init(); 
  // tell cURL what the URL is curl_setopt($ch, CURLOPT_URL, $url); 
  // tell cURL that you want the data back from that URL curl_setopt($ch, CURLOPT_RETURNTRANSFER, 1); 
  // run cURL
  $output = curl_exec($ch); 
  // end the cURL call (this also cleans up memory so it is 
  // important)
  curl_close($ch);
  // display the output echo $output;
?&gt;</code></pre>

If you run this in the browser, you'll see Smashing Magazine's home page.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f8b8a3bc-f448-4106-9506-cd716145efcc/smashingmagwithcurl1.jpg" alt="Smashing Magazine homepage loaded with cURL" width="450" />

You could also strip out content from the data:

<pre><code class="language-php">&lt;?php
  // define the URL to load
  $url = 'https://www.smashingmagazine.com';
  // start cURL
  $ch = curl_init(); 
  // tell cURL what the URL is curl_setopt($ch, CURLOPT_URL, $url); 
  // tell cURL that you want the data back from that URL curl_setopt($ch, CURLOPT_RETURNTRANSFER, 1); 
  // run cURL
  $output = curl_exec($ch); 
  // end the cURL call (this also cleans up memory so it is 
  // important)
  curl_close($ch);
  // if a filter parameter with the value links was sent if($_GET['filter'] == 'links'){
    // get all the links from the document and show them
    echo '&lt;ul&gt;';
    preg_match_all('/&lt;a[^&gt;]+&gt;[^&lt;/a&gt;]+&lt;/a&gt;/msi',$output,$links);
    foreach($links[0] as $l){
      echo '&lt;li&gt;' . $l . '&lt;/li&gt;';      
    }
    echo'&lt;/ul&gt;';
  // otherwise just show the page
  } else {
    echo $output;
  }
?&gt;</code></pre>

If you open this in your browser, you'll get all of the links from Smashing Magazine and no other content.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/32ed08fc-aeae-42e7-b58f-e01d7142b76f/links1.jpg" alt="Smashing magazine links" width="450" />

Nowadays, though, we are more likely to use APIs than to load websites this way, which is why we need a way to convert the XML and JSON that are returned from Web services into PHP-friendly data.</p>

## Displaying XML Content

The easiest way to deal with XML content in PHP is to use the <a href="https://php.net/manual/en/book.simplexml.php">SimpleXML functions of PHP</a>. Using these, we can turn a bunch of XML into a PHP object and loop over it. To show Smashing Magazine's RSS feed, we can do the following:

<pre><code class="language-php">&lt;?php
  $url = 'https://rss1.smashingmagazine.com/feed/';
  $ch = curl_init(); 
  curl_setopt($ch, CURLOPT_URL, $url); 
  curl_setopt($ch, CURLOPT_RETURNTRANSFER, 1); 
  $output = curl_exec($ch); 
  curl_close($ch);
  $data = simplexml_load_string($output);
  echo '&lt;ul&gt;';
  foreach($data-&gt;entry as $e){
    echo '&lt;li&gt;&lt;a href="' . $e-&gt;link[0]['href'] .

         '"&gt;'.$e-&gt;title.'&lt;/a&gt;&lt;/li&gt;';
  }
  echo '&lt;/ul&gt;';
?&gt;</code></pre>

The <code>simplexml_load_string()</code> function turns the XML document into a PHP object with arrays. How did I figure out to loop over <code>data-&gt;entry</code> and get the <code>href</code> via <code>link[0]['href']</code>? Simple. I did a <code>print_r($output)</code> and checked the source of the document by hitting <em>Cmd + U</em> in Firefox on my Mac. That showed me that this <code>entry</code> is an array. I then did a <code>print_r($e)</code> in the loop to see all the properties of every entry. If it is part of the <code>@attributes</code> array, then you need to use the <code>[]</code> notation.

That's all. The only stumbling block you will encounter is CDATA blocks and namespaces in SimpleXML. Stuart Herbert <a href="https://blog.stuartherbert.com/php/2007/01/07/using-simplexml-to-parse-rss-feeds/">has a good introduction to these two issues in this article</a>.</p>

## Displaying JSON Content

The data format <a href="https://json.org">JSON</a> is the low-fat alternative to XML. It is far less complex (e.g. no namespaces), and if you work in a JavaScript environment, it is native to the browser. This makes it very fast and easy to use, and for this reason it has started to become a popular data format for APIs. In essence, JSON is a JavaScript object. For example, I could write the LAMP stack example as follows:

<pre><code class="language-php">{"lampstack":
  {
    "operatingsystem" : "Linux",
    "server" : "Apache",
    "database" : "MySQL",
    "language" : "PHP"
  }
}</code></pre>

You can convert this to PHP using the <code>json_decode()</code> method, and get it back as a PHP object:

<pre><code class="language-php">&lt;?php
  $json = '{
  "lampstack":
  {
    "operatingsystem":"Linux",
    "server":"Apache",
    "database":"MySQL",
    "language":"PHP"
    }
  }';
  print_r(json_decode($json));
?&gt;</code></pre>

One API that returns JSON is the Twitter trends API. If you load the API's URL with cURL and do a <code>print_r()</code> after <code>json_decode()</code>, you <span class="removed_link" title="https://icant.co.uk/articles/phpforhacks/index.php?demo=15">get the following back</span>:

<pre><code class="language-php">&lt;?php
  $url = 'https://search.twitter.com/trends.json';
  $ch = curl_init(); 
  curl_setopt($ch, CURLOPT_URL, $url); 
  curl_setopt($ch, CURLOPT_RETURNTRANSFER, 1); 
  $output = curl_exec($ch); 
  curl_close($ch);
  $data = json_decode($output);
  print_r($data);
?&gt;</code></pre>

<pre><code class="language-php">stdClass Object
(
[trends] =&gt; Array
  (
    [0] =&gt; stdClass Object
    (
      [name] =&gt; #nowplaying
      [url] =&gt; https://search.twitter.com/search?q=%23nowplaying
    )

    [1] =&gt; stdClass Object
    (
      [name] =&gt; #Didntwannatellyou
      [url] =&gt; https://search.twitter.com/search?q=%23Didntwannatellyou
    )

    [2] =&gt; stdClass Object
    (
      [name] =&gt; #HappyBirthdayGagaBR
      [url] =&gt; https://search.twitter.com/search?q=%23HappyBirthdayGagaBR
    )

    [3] =&gt; stdClass Object
    (
      [name] =&gt; Justin Bieber
      [url] =&gt; https://search.twitter.com/search?q=%22Justin+Bieber%22
    )

    [4] =&gt; stdClass Object
    (
      [name] =&gt; #FreakyFactSays
      [url] =&gt; https://search.twitter.com/search?q=%23FreakyFactSays
    )

    [5] =&gt; stdClass Object
    (
      [name] =&gt; #YouSoGangsta
      [url] =&gt; https://search.twitter.com/search?q=%23YouSoGangsta
    )

    [6] =&gt; stdClass Object
    (
      [name] =&gt; I ?
      [url] =&gt; https://search.twitter.com/search?q=%22I+%E2%99%A5%22
    )

    [7] =&gt; stdClass Object
    (
      [name] =&gt; #MeMyselfandTime
      [url] =&gt; https://search.twitter.com/search?q=%23MeMyselfandTime
    )

    [8] =&gt; stdClass Object
    (
      [name] =&gt; #2010yearofJonas
      [url] =&gt; https://search.twitter.com/search?q=%232010yearofJonas
    )

    [9] =&gt; stdClass Object
    (
      [name] =&gt; Easter
      [url] =&gt; https://search.twitter.com/search?q=Easter
    )
  )
  [as_of] =&gt; Sun, 28 Mar 2010 19:31:30 +0000
)</code></pre>

You can then use a simple loop to <span class="removed_link" title="https://icant.co.uk/articles/phpforhacks/index.php?demo=16">render the current trends as an unordered list</span>:

<pre><code class="language-php">&lt;?php
  $url = 'https://search.twitter.com/trends.json';
  $ch = curl_init(); 
  curl_setopt($ch, CURLOPT_URL, $url); 
  curl_setopt($ch, CURLOPT_RETURNTRANSFER, 1); 
  $output = curl_exec($ch); 
  curl_close($ch);
  $data = json_decode($output);
  echo '&lt;h2&gt;Twitter trending topics ('.$data-&gt;as_of.')&lt;/h2&gt;';
  echo '&lt;ul&gt;';
  foreach ($data-&gt;trends as $t){
    echo '&lt;li&gt;&lt;a href="'.$t-&gt;url.'"&gt;'.$t-&gt;name.'&lt;/a&gt;&lt;/li&gt;';
  }
  echo '&lt;/ul&gt;';
?&gt;</code></pre>

## Putting It All Together

Let's do a quick example using all of the things we've learned so far: a simple search interface for the Web.

Using <a href="https://developer.yahoo.com/yql/">Yahoo's YQL</a>, it is pretty easy to do a Web search for "cat" with the command <code>select * from search.web where query="cat"</code> sent to the YQL endpoint. You can define JSON as the return format, and the rest means you simply <span class="removed_link" title="https://icant.co.uk/articles/phpforhacks/index.php?demo=17">enhance the earlier form example</span>:

<pre><code class="language-php">&lt;?php
  $search_html = filter_input(INPUT_GET, 's', FILTER_SANITIZE_SPECIAL_CHARS);
  $search_url = filter_input(INPUT_GET, 's', FILTER_SANITIZE_ENCODED);
?&gt;
&lt;form action="index.php" method="get"&gt;
  &lt;div&gt;
    &lt;label for="search"&gt;Search:&lt;/label&gt;
    &lt;input type="text" name="s" id="search" 
           value="&lt;?php echo $search_html;?&gt;"&gt;
   &lt;input type="hidden" name="demo" value="17"&gt;
   &lt;input type="submit" value="Make it so"&gt;
  &lt;/div&gt;
&lt;/form&gt;
&lt;?php
if(isset($_GET['s'])){
  echo '&lt;h2&gt;You searched for '.$search_html.'&lt;/h2&gt;';
  $yql = 'select * from search.web where query="'.$search_url.'"';
  $url = 'https://query.yahooapis.com/v1/public/yql?q='.
          urlencode($yql).'&amp;format=json&amp;diagnostics=false';
  $ch = curl_init(); 
  curl_setopt($ch, CURLOPT_URL, $url); 
  curl_setopt($ch, CURLOPT_RETURNTRANSFER, 1); 
  $output = curl_exec($ch); 
  curl_close($ch);
  $data = json_decode($output);
  echo '&lt;ul&gt;';
  foreach ($data-&gt;query-&gt;results-&gt;result as $r){
    echo '&lt;li&gt;&lt;h3&gt;&lt;a href="'.$r-&gt;clickurl.'"&gt;'.$r-&gt;title.'&lt;/a&gt;&lt;/h3&gt;'.
         '&lt;p&gt;'.$r-&gt;abstract.' &lt;span&gt;('.$r-&gt;dispurl.')&lt;/span&gt;&lt;/p&gt;&lt;/li&gt;';
  }
  echo '&lt;/ul&gt;';

  echo '&lt;p&gt;&lt;a href="index.php?search='.$search_url.'&amp;demo=17"&gt;Search again.&lt;/a&gt;&lt;/p&gt;';
}
?&gt;</code></pre>

## Interaction With JavaScript

One thing people keep asking about is how to send information from PHP to JavaScript and back. This can be done in a few ways.

*   To send information from JavaScript to PHP, you need to either alter the `href` of a link or populate a hidden form field. The other solution of course is to use AJAX.
*   To send information from PHP to JavaScript, simply render a script element and write out the PHP information with an `echo` statement.
*   Using PHP's `header()` function and `json_encode()`, you can send data back to the browser as JavaScript, which allows us to use it as a `src` attribute of a `script` node.

For example, to get Smashing Magazine's RSS feed as a JavaScript object, <span class="removed_link" title="https://icant.co.uk/articles/phpforhacks/index.php?demo=18">you could do the following</span>:

<pre><code class="language-php">&lt;?php header('Content-type: text/javascript');
  $url = 'https://rss1.smashingmagazine.com/feed/';
  $ch = curl_init(); 
  curl_setopt($ch, CURLOPT_URL, $url); 
  curl_setopt($ch, CURLOPT_RETURNTRANSFER, 1); 
  $output = curl_exec($ch); 
  curl_close($ch);
  $data = simplexml_load_string($output);
  $data = json_encode($data);
  echo 'var smashingrss='.$data;
?&gt;</code></pre>

You could then use this in a JavaScript block:

<pre><code class="language-php">&lt;script src="https://icant.co.uk/articles/phpforhacks/index.php?demo=18"&gt;&lt;/script&gt;
&lt;script&gt;alert(smashingrss.title);&lt;/script&gt;</code></pre>

Using <code>header()</code> and <code>json_encode()</code>, you could do any complex conversion and filtering in PHP and re-use it in JavaScript.</p>

## Summary

I hope this gives you an idea of what PHP is and how you can use it to access Web services and to build your own APIs to re-use in JavaScript. Using PHP for the Web boils down to a few tricks:

*   Use cURL to load data from Web resources;
*   Convert information with `simplexml_load_string()` and `json_decode()`;
*   Check the structure of returned information with `print_r()`;
*   Loop over information with `foreach()`;
*   Use the `$_GET[]` and `$_POST[]` arrays to re-use form data and URL parameters;
*   Filter information from the user and from URLs using the built-in PHP filtering methods.

A lot of documentation is out there, and your best bet is to go directly to the <a href="https://php.net">PHP home page</a> to read or download the documentation. Check out the user comments in particular, because that is where the real gems and examples of implementation appear.

{{< signature "al" >}}

