---
title: '6 Favorite Programming Mistakes'
slug: my-favorite-programming-mistakes
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/00622940-1f93-4168-b495-5ce18c51cdb5/mistakes-made-lessons-learned.jpg
date: 2011-07-07T11:04:23.000Z
author: paul-tero
summary: >-
  Programming mistakes come in many shapes and sizes. In this article, Paul Tero shares some of the mistakes he has made over his programming carrer, and the lessons learned from them. 
description: >-
  Programming mistakes come in many shapes and sizes. In this article, Paul Tero shares some of the mistakes he has made over his programming carrer, and the lessons learned from them.
categories:
  - Coding
  - PHP
  - JavaScript
---

Over my programming career, I have made a lot of mistakes in several different languages. In fact, if I write 10 or more lines of code and it works the first time, I’ll get a bit suspicious and test it more rigorously than usual. I would expect to find a syntax error or a bad array reference or a misspelled variable or *something*.

I like to classify these mistakes into three broad groups: cock-ups (or screw-ups in American English), errors and oversights. A cock-up is when you stare blankly at the screen and whisper “Oops”: things like deleting a database or website, or overwriting three-days worth of work, or accidentally emailing 20,000 people.

Errors cover everything, from simple syntax errors like forgetting a <code>}</code> to fatal errors and computational errors. When an error is so subtle and hard to find that it is almost beautiful, I would call it an oversight. This happens when a block of code is forced to handle a completely unforeseen and very unlikely set of circumstances. It makes you sit back and think “Wow”: like seeing a bright rainbow or shooting star, except a bit less romantic and not quite as impressive when described to one’s partner over a candlelit dinner.

<figure><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="104010" title="Mwnt beach" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7390f9b8-e36d-4aaf-ae27-65d7d912cb32/mwnt-beach.jpg" alt="Mwnt beach" width="542" height="214" /><figcaption>Coastline near Mwnt on the west coast of Wales. Read on to find out why this is halfway to being a very special place.</figcaption></figure>

This article discusses some of the spectacular and beautiful mistakes I have made, and the lessons learned from them. The last three are my favorites.

{{% feature-panel %}}

## Leaving Debug Mode On

The first two mistakes in this article were full-fledged cock-ups.

When I first started freelancing, I wrote a set of PHP libraries for handling database queries, forms and page templating. I built a debugging mode into the libraries at a fairly deep level, which depended on a global variable called <code>$DEBUG</code>.

I also kept a local copy of every major website I worked on, for developing, debugging and testing. So, whenever a problem occurred, I could set <code>$DEBUG=1;</code> at the top of the page, and it would tell me various things, such as all the database statements it was running. I rarely used this debug method on live websites; it was for local usage only.

Except for one day when I was working late at night, debugging a minor problem on a popular e-commerce website. I put <code>$DEBUG=1;</code> at the top of several pages and was switching between them. It was all a tired midnight blur, but in the end I somehow added the debugging variable to the most important page on the website, the one after the user clicks “Pay now,” and I uploaded it to the live website.

The next morning, I went out early for the whole day. I got home at 9:00 pm to find 12 increasingly frustrated messages on my answering machine and a lot more emails. For about 20 hours, whenever a customer clicked pay, they saw something like this:

*What customers saw when they clicked “Pay.”*

It took me about 10 seconds to fix, but a lot longer to apologize to my client for a day’s worth of lost orders.

### Lessons Learned

I held an internal inquiry into this issue and established the following:

1.  Avoid working late at night;
2.  Make a full test order whenever I make a change to the order processing, however minor;
3.  Make sure debug statements never see the light of day on a live website;
4.  Provide some emergency contact details for me and/or a back-up programmer.

### Thoughtful Debugging

For the third requirement, I implemented a couple of functions like this, to make sure that debugging messages are outputted only when *I* am looking at the website:

<pre><code class="language-php">function CanDebug() {
 global $DEBUG;
 $allowed = array ('127.0.0.1', '81.1.1.1');
 if (in_array ($_SERVER['REMOTE_ADDR'], $allowed)) return $DEBUG;
 else return 0;
}
function Debug ($message) {
  if (!CanDebug()) return;
  echo '&lt;div style="background:yellow; color:black; border: 1px solid black;';
  echo 'padding: 5px; margin: 5px; white-space: pre;"&gt;';
  if (is_string ($message)) echo $message;
  else var_dump ($message);
  echo '&lt;/div&gt;';
}</code></pre>

Then, whenever I want to output something for debugging, I call the <code>Debug</code> function. This calls <code>CanDebug</code> to check the requesting IP address and the <code>$DEBUG</code> variable. The <code>$allowed</code> array contains my IP address for local testing (<code>127.0.0.1</code>) and my broadband IP address, which I can get from <a href="https://whatismyipaddress.com">WhatIsMyIPAddress.com</a>.

Then I can output things like this:

<pre><code class="language-php">$DEBUG = 1;
Debug ("The total is now $total"); //about a debugging message
Debug ($somevariable); //output a variable
Debug ("About to run: $query"); //before running any database query
mysql_query ($query);</code></pre>

And I can be confident that no one but me (or anyone sharing my IP address, such as my boss) will ever see any debugging messages. Assuming that the variables above were set, the above code would look like this:

*Outputting debugging statements.*

For extra safety, I could have also put the error messages inside HTML comments, but then I would have had to sift through the HTML source to find the bit I was looking for.

I have another related useful bit of code that I can put at the top of a page or configuration file to ensure that all PHP notices, warnings and errors will be shown to me and only me. If the person is not me, then errors and warnings will be outputted to the error log but not shown on screen:

<pre><code class="language-php">if (CanDebug()) {ini_set ('display_errors', 1); error_reporting (E_ALL);}
else {ini_set ('display_errors', 0); error_reporting (E_ALL &amp; ~E_NOTICE);}</code></pre>

### Debuggers

The method above is useful for quickly finding errors in very specific bits of code. There are also various debugging tools, such as FirePHP and <a href="https://xdebug.org/">Xdebug</a>, that can provide a huge amount of information about a PHP script. They can also run invisibly, outputting a list of every function call to a log file with no output to the user.

Xdebug can be used like this:

<pre><code class="language-php">ini_set ('xdebug.collect_params', 1);
xdebug_start_trace ('/tmp/mytrace');
echo substr ("This will be traced", 0, 10);
xdebug_stop_trace();</code></pre>

This bit of code logs all function calls and arguments to the file */tmp/mytrace.xt*, which will look like this:

<figure><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="104759" title="Xdebug example" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/87bc2e29-1235-4e74-a12f-90a29f386408/xdebug-example.png" alt="screenshot" width="539" height="155" /><figcaption>Contents of an Xdebug stack trace showing every function call.</figcaption></figure>

Xdebug also displays much more information whenever there is a PHP notice, warning or error. However, it needs to be installed on the server, so it is probably not possible in most live hosting environments.

FirePHP, on the other hand, works as a PHP library that interacts with an add-on to Firebug, a plug-in for Firefox. You can output stack traces and debugging information directly from PHP to the Firebug console &mdash; again, invisible to the user.

For both of these methods, a function like <code>CanDebug</code> above is still useful for making sure that not everyone with Firebug can view the stack traces or generate big log files on the server.

## Turning Debug Mode Off

Debugging emailing scripts is more involved. Definitively testing whether a script is sending an email properly is hard without actually sending the email. Which I once did by mistake.

A few years ago, I was asked to create a bulk emailing script to send daily emails to over 20,000 subscribed users. During development, I used something similar to the <code>CanDebug</code> function above, so that I could test the emailing script without actually sending an email. The function to send emails looked something like this:

<pre><code class="language-php">function SendEmail ($to, $from, $subject, $message) {
  if (CanDebug() &gt;= 10) Debug ("Would have emailed $to:n$message");
  else {
    if (CanDebug()) {$subject = "Test to $to: $subject"; $to = "test@test.com";}
    mail ($to, $subject, $message, "From: $from");
  }
}</code></pre>

If I set <code>$DEBUG=1</code>, it would send the emails (all 20,000 of them) to a test address that I could check. If I set <code>$DEBUG=10</code>, it would tell me that it was trying to send an email but not actually send anything.

Soon after launch, a problem arose with the script. I think it ran out of memory from doing some inefficient processing 20,000 times. At some point, I went into fix something, forgot to set my <code>$DEBUG</code> variable (or else my broadband IP address had inconveniently changed) and mistakenly emailed 20,000 people.

I apologized to the agency I was working for, but thankfully nothing much came of it. I guess that spam filters blocked many of the messages. Or perhaps the recipients were merely pleased that the email did not contain anything for them to do or read.

### Lessons Learned

I was very glad that I just put “test” in the subject and message of the test email, and not some statement reflecting how frustrated I was getting at that particular bug. I learned a few lessons:

1.  Be extra careful when testing bulk emailing scripts &mdash; check that the debug mode is working.
2.  Send test emails to as few people as possible.
3.  Always send polite test messages, like “Please ignore, just testing.” Don’t say something like “My client is a ninny,” in case it gets sent to 20,000 unsuspecting investors.

## PHP Blank Page

Now we’re in the realm of hard-to-spot errors, rather than cock-ups. If you’d like to see a hard-to-debug error in PHP, bury the following somewhere deep in your code:

<pre><code class="language-php">function TestMe() {TestMe();}
TestMe();</code></pre>

Depending on the browser and the server’s Apache and PHP versions, you might get a blank page, a “This Web page is not available,” a fatal error due to running out of memory, or the option to “Save” or “Open” the page, like this:

<figure><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="104134" title="PHP recursive error" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b72d4e4c-4fe5-42dd-bfd1-c674a9393c08/test-save-as.png" alt="screenshot" width="542" height="473" /><figcaption>Infinite recursion, as dealt with by Firefox 3.6.</figcaption></figure>

It basically causes infinite recursion, which can cause a Web server thread to run out of memory and/or crash. If it crashes, a small trace may or may not be left in the error log:

<pre><code class="language-markup tmp-none">[Mon Jun 06 18:24:10 2011] [notice] child pid 7192
  exit signal Segmentation fault (11)</code></pre>

But this gives little indication of where or why the error occurred. And all of the quick debugging techniques of adding lines of output here or there may not help much, because as long as the offending code gets executed, the page will seem to fail in its entirety. This is mainly because PHP only periodically sends the HTML it generates to the browser. So, adding a lot of <code>flush();</code> statements will at least show you what your script was doing immediately before the recursive error.

Of course, the code that leads to this error might be much more convoluted than the above. It could involve classes calling methods in other classes that refer back to the original classes. And it might only happen in certain hard-to-duplicate circumstances and only because you’ve changed something else somewhere else.

### Lessons Learned

1.  Know the locations of error log files, in case something gets recorded there.
2.  This is where stack-tracing debuggers such as Xdebug can be really handy.
3.  Otherwise, set aside plenty of time to go through the code line by line, commenting out bits until it works.

## Wrong Variable Type

This error often happens with databases. Given the following SQL statements…

<pre><code class="language-php">CREATE TABLE products (
  id INT PRIMARY KEY AUTO_INCREMENT,
  name VARCHAR(60),
  category VARCHAR(10),
  price DECIMAL(6,2)
);
INSERT INTO products VALUES (1, 'Great Expectations', 'book', 12.99);
INSERT INTO products VALUES (2, 'Meagre Expectations', 'cd', 2.50);
INSERT INTO products VALUES (3, 'Flared corduroys', 'retro clothing', 25);</code></pre>

… can you guess what is returned when you run the following?

<pre><code class="language-php">SELECT * FROM products WHERE category='retro clothing';</code></pre>

The answer is nothing, because the category column is only 10 characters long, and so the category of the last product is cut off at <code>retro clot</code>. Recently edited products or new menu items suddenly disappearing can create a lot of confusion. But fixing this is generally very easy:

<pre><code class="language-php">ALTER TABLE products MODIFY category VARCHAR(30);
UPDATE products SET category='retro clothing' WHERE category='retro clot';</code></pre>

<figure><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="105366" title="Short database column error" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4294ebd3-c650-4ba1-b448-343caa0e4737/database-col-error.png" alt="screenshot" width="542" height="319" /><figcaption>The category has been cut off after 10 characters, as shown in phpMyAdmin.</figcaption></figure>

I made a more serious error with the first major e-commerce website that I worked on. At the end of the ordering process, the website would ask the customer for their credit card details and then call a Java program, which would send a request to Barclays ePDQ system to take the payment. The amount was sent as the number of pence. Not being very familiar with Java, I based the code on an example I found, which represented the total as a short integer:

<pre><code class="language-markup tmp-none">short total;</code></pre>

The Java program was called on the command line. If it returned nothing, then the transaction was considered successful, emails were sent, and the order was fulfilled. If there was an error in processing the card, the program returned something like “Card not authorized” or “Card failed fraud checks.”

Short integers can store a value between -32768 and +32767. This seemed plenty to me. But I neglected that this was in pence, not pounds, so the highest possible total was actually £327.67. And the really bad news was that if the amount was higher than that, then the Java program simply crashed and returned nothing, which looked exactly like a successful order and was processed as normal.

It took a few months and several large unpaid transactions before the error was spotted, either by the accounting department or a vigilant and honest customer. I believe they recovered all of the payments in the end.

{{% ad-panel-leaderboard %}}

### Lessons Learned

1.  When assigning a type to a database column or variable, be generous and flexible, and try to plan ahead.
2.  Make sure that a program succeeding responds differently to a program crashing.

## 1p Errors

Among my favorite mistakes are those that cause a discrepancy of just 1 pence (or cent, öre or other denomination). I like them because they are usually very subtle and hard to trace and often boil down to a rounding error. I have to become a mathematical detective, a job that I would readily do if enough work was available.

For a website a few years ago, I needed to create a quick JavaScript function to output a monetary amount. I used this:

<pre><code class="language-javascript">&lt;script type="text/javascript"&gt;
function GetMoney (amount) {return Math.round (amount * 100) / 100;}
&lt;/script&gt;</code></pre>

However, it was quickly discovered that amounts like 1.20 were displayed as 1.2, which looks unprofessional. So, I changed it to this:

<pre><code class="language-javascript">&lt;script type="text/javascript"&gt;
function GetMoney (amount) {
  var pounds = Math.floor (amount);
  var pence = Math.round (amount * 100) % 100;
  return pounds + '.' + (pence &lt; 10 ? '0' : ’) + pence;
}
&lt;/script&gt;</code></pre>

The main difference is the extra 0 in the last line. But now that the pence is computed separately, the modulus <code>%</code> operator is needed to get the remainder when the amount is divided by 100. Try to spot the unlikely circumstances under which this code would cause an error.

It happened on a website that sold beads. I have since learned that beads can be sold in a huge range of amounts and configurations, including customized mixes containing fractional quantities. Once, a customer bought 1.01 of an item costing £4.95, and ended up paying just £4.00. This is because the amount was passed as 4.9995. The rounded pence was 100, and <code>% 100</code> left 0 pence, and so the pounds were floored to 4.

<figure><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="106035" title="Rounding error" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e6c19bcc-207d-41ee-8e4f-977552d708bb/beads-getmoney.png" alt="screenshot" width="542" height="528" /><figcaption>A subtle rounding error, where 101 beads sold at £4.95 per 100 were billed as £4 instead of £5.</figcaption></figure>

This is still just a rounding error, a superset of 1p errors. I made a quick change to fix it:

<pre><code class="language-javascript">&lt;script type="text/javascript"&gt;
function GetMoney (amount) {
  var pounds = Math.floor (amount);
  var pence = Math.<strong>floor</strong> (amount * 100) % 100;
  return pounds + '.' + (pence &lt; 10 ? '0' : ’) + pence;
}
&lt;/script&gt;</code></pre>

This wasn’t a great fix, though, because it rounded £4.9995 down to £4.99, which put it out of sync with any corresponding server-side calculations. But even more dramatically, when someone ordered 0.7 of something costing £1.00, it ended up displaying 69p instead of 70p! This is because floating-point numbers like 0.7 are represented in binary as a number more like 0.6999999999999999 (as described in a <a href="https://www.smashingmagazine.com/2011/05/30/10-oddities-and-secrets-about-javascript/">recent Smashing Magazine article</a>), which would then be floored to 69 instead of rounded up to 70.

This is a true 1p error. To fix this, I added another rounding at the beginning:

<pre><code class="language-javascript">&lt;script type="text/javascript"&gt;
function GetMoney (amount) {
  var pence = Math.round (100 * amount);
  var pounds = Math.floor (pence / 100);
  pence %= 100;
  return pound + '.' + (pence &lt; 10 ? '0' : ’) + pence;
}
&lt;/script&gt;</code></pre>

Now, I had four fairly complicated lines of code to do one very simple thing. Today, while writing this article, I discovered a built-in Javascript function to handle all of this for me:

<pre><code class="language-javascript">&lt;script type="text/javascript"&gt;
function GetMoney (amount) {return amount.<strong>toFixed</strong> (2);}
alert (GetMoney (4.9995) + ' ' + GetMoney (0.1 * 0.7));
&lt;/script&gt;</code></pre>

### Discounting With PayPal

PayPal is a 1p error waiting to happen. Many websites offer voucher codes that give a percentage off each order, computed at the end of the order. If you ordered two items costing 95p, the subtotal would be £1.90, and you would receive a 19p discount, for a total of £1.71.

However, PayPal does not support this type of discounting. If you want PayPal to display the items in your shopping basket, you have to pass each one separately with a price and quantity:

<pre><code class="language-php">&lt;input name="item_name_1" type="hidden" value="My Difficult Product" /&gt;
&lt;input name="amount_1" type="hidden" value="0.99" /&gt;
&lt;input name="quantity_1" type="hidden" value="1" /&gt;</code></pre>

Thus, you have to discount each item separately. 10% off of 95p leaves 85.5p. PayPal doesn’t accept fractional amounts, so you have to round up to 86p, for a grand total of £1.72 in PayPal, or round down to 85p, for a total of £1.70.

To solve this, I had to also make the website discount each item individually. Instead of just doing 10% &times; £1.90, it accumulates the discount item by item, using a whole amount of pence each time. Assuming <code>$items</code> is a PHP array of order item objects:

<pre><code class="language-php">$discount = 0; $discountpercent = 10;
foreach ($items as $item) {
 $mydiscount = floor ($item-&gt;price * $discountpercent) / 100;
 $item-&gt;priceforpaypal = $item-&gt;price - $mydiscount;
 $discount += $mydiscount * $item-&gt;quantity;
}</code></pre>

### Lessons Learned

1.  Don't reinvent the wheel, even very small wheels that look easy from the outside.
2.  If you get a 1p discrepancy, check where and how numbers are rounded.
3.  Avoid representing prices using floats when possible. Instead, store the pence or cents as integers; and in databases, use a fixed-point type like `DECIMAL`.

## Daylights Savings

I would not call the last two mistakes in this list “errors.” They require a very specific set of fairly rare circumstances, so they are more “oversights” on the programmer’s part. Oversights are like the acts of terrorism that are excluded by home insurance policies. They go beyond what a programmer could reasonably be expected to think of in advance.

Can you guess what is wrong with the following seemingly innocuous line of code, which selects orders that were completed more than one week ago?

<pre><code class="language-php">mysql_query ("SELECT * FROM orders WHERE completeddate &lt; '" .
  date ('Y-m-d H:i:s', (time() - 7 * 86400 + 600)) . "'")</code></pre>

I used a similar line in a system for a weekly repeating order. It looked up orders that were completed last week, duplicated them, and processed them for the current week. 86,400 is the number of seconds in a day, so <code>time() - 7 * 86400</code> was exactly one week ago, and <code>+600</code> gives it a leeway of 10 minutes.

This was a low-budget method of implementing repeating orders. Given more time, I would have created a separate table and/or shopping basket to differentiate between repeating and non-repeating items. As it happened, this code worked well for several months and then mysteriously failed in late March.

It took ages to recover from the oversight and to process those orders manually. And even longer to find the reason, especially because I had to fool the whole website into thinking that it was a different date.

I’ve pretty much given the trick away in the title of the section: I forgot to account for daylight savings, when one week is less than <code>7\*86400 seconds</code>.

Compare the following three ways of getting the date exactly one week ago. The last is the most elegant. I only recently discovered it:

<pre><code class="language-php">$time = strtotime ('28 March 2011 00:01');
echo date ('Y-m-d H:i:s', ($time - 7 * 86400)) . '&lt;br/&gt;';
echo date ('Y-m-d H:i:s', mktime (date ('H', $time), date ('i', $time), 0,
  date ('n', $time), date ('j', $time) - 7, date ('Y', $time)));
echo date ('Y-m-d H:i:s', (<strong>strtotime ('-1 week', $time)</strong>)) . '&lt;br/&gt;';</code></pre>

### Lessons Learned

Drawing general lessons from a mistake like this is difficult, but there is a specific lesson here:

1.  On websites that repeat things, remember to consider time zones and daylight savings.
2.  Consider storing all times and dates in UTC (Coordinated Universal Time).
3.  Don't reinvent the time wheel either: `strtotime` is a powerful function.

The next time I do a website for repeating orders, I won’t make that mistake.

## Spam Error

My favorite mistake of all time is an even subtler oversight. Can you spot what is unusual about these made-up email addresses:

*   beckyrsmythe@somewhere.com
*   glynnfrenk@someplace.co.uk

A few years ago, spammers began targeting contact forms on websites, <a href="https://www.phpsecure.info/v2/article/MailHeadersInject.en.php">injecting headers</a> and forcing the forms to send millions of messages to harvested addresses and later just to the form’s usual recipient.

This necessitated anti-spam filtering directly on the Web page that processed the form. When I was first asked to do this, I <a href="https://www.tero.co.uk/scripts/spamzapper.php">combined a few anti-spam scripts</a> that I found on the Internet. Spammers now often put blocks of random letters in their messages to try to fool spam filters. So, one anti-spam technique is to check for these random letters by looking for certain consonants in a row.

I read somewhere that words with more than six consonants in a row are extremely rare in Latin-alphabet languages. The most consonants in a row in English is six: in “latchstring.” Other languages like Polish have many more diphthongs than English (dz, sz, cz), so I used seven to be on the safe side. The PHP code uses a regular expression and looks something like this:

<pre><code class="language-php">foreach ($_POST as $key=&gt;$val) {
        if (preg_match ('/[bcdfghjklmnpqrstvwxyz]{7,}/i', $val))
                die ("&lt;h1&gt;Spam Detected&lt;/h1&gt;&lt;p&gt;Too many consonants in $val&lt;/p&gt;");
}</code></pre>

I had to revisit the script when it blocked someone with an email address like the ones above:

<figure><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="106061" title="Spam error" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/58d54737-e035-4614-b5d6-ca0c6bca0105/spam-error.png" alt="" width="542" height="315" />
<figcaption>A customer whose email address had seven or more consonants in a row would have received this upon submitting a form.</figcaption></figure>

Based on a small sample of 10,000, I found that approximately 0.2% of all email addresses would be filtered as spam, according to the rule above. One valid email address had nine consonants in a row. Increasing the number of allowed consonants from seven to ten decreases the script’s usefulness significantly, so instead I considered the letter “y” a vowel.

This worked well, until a customer from Cwmtwrch near Swansea attempted to place an order. According to my sample, only 1 in 5000 customers have a name, email or address like this. Small but important, especially if you are one of them. So, I allowed “w” as a vowel, too. You can check for this in your own customer database with a MySQL query like the following:

<pre><code class="language-php">SELECT CONCAT_WS(' ',firstname,lastname,email,city,address1,address2) AS thefields
FROM visitors HAVING LENGTH(thefields)&gt;20 AND thefields RLIKE '[bcdfghjklmnpqrstvwxz]{7,}'</code></pre>

### Lessons Learned

I learned that my anti-spam script was blocking potential customers only once my client forwarded me their complaints. When I received the first one (an email address containing a couple of “y”s for vowels), I was amazed. It seemed so unlikely. A couple of weeks later, when shoppers in a small Welsh village were still mysteriously unable to place an order, I almost didn’t believe it. It seems that if a piece of code has a hole, someone somewhere will fall into it. So, I’ve learned to do the following:

1.  Take all error reports and complaints seriously. They may uncover something amazing like this.
2.  Jot down the really unlikely mistakes. You will impress other programmers… or me, at least

More specifically, logging everything that is processed by a spam filter is useful, because you can then try to spot any false positives or false negatives and use them to improve the filter.

## Conclusion

Programming mistakes come in many shapes and sizes. This article has ranged from the very obvious cock-ups to the extremely subtle oversights. And it looks like they all support <a href="https://en.wikipedia.org/wiki/Murphy%27s_law">Murphy’s Law</a>: if something can go wrong, it will.

However, for every mistake found, reported and fixed, probably a few more aren’t. Either they aren’t found (because they are so incredibly subtle that the set of circumstances that would cause them has never happened) or they aren’t reported (because most users don’t bother reporting errors &mdash; which is why any error reports that do come in should be taken seriously) or they aren’t fixed (because doing so would be too time-consuming or expensive).

Mistakes are also more likely to be found on popular websites, mainly because so many more people are putting those websites to work, but partly because fixing one mistake could cause another somewhere else.

The best lessons, therefore, are to plan ahead and to debug thoughtfully.

{{% ad-panel-leaderboard %}}

## <span class="rh">Further Reading</span> on SmashingMag:

*   [What Is The Worst Programming Mistake You’ve Ever Made?](https://www.smashingmagazine.com/2010/09/what-is-the-worst-design-or-programming-mistake-you-ve-ever-made/)
*   [Mistakes Developers Make When Learning Design](https://www.smashingmagazine.com/2016/12/mistakes-developers-make-when-learning-design/)
*   [Back-End and Server Administration Guidelines](https://www.smashingmagazine.com/back-end-server-administration-php-guidelines/)

{{< signature "kw, mrn" >}}
