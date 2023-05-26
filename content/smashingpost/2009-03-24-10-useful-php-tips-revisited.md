---
title: 10 Advanced PHP Tips
slug: 10-useful-php-tips-revisited
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2e4f5557-3d2f-4c82-8cff-78ba40be02a6/php.jpg
date: 2009-03-24T15:24:45.000Z
author: chris-shiflett
description: >-
  Here, on the Smashing Editorial team, we always try to meet the expectations
  of our readers. We do our best to avoid misunderstandings, and we try to
  spread knowedge and present only the best design practices and development
  techniques. However, sometimes we do make mistakes. And when we do, we
  apologize and do our best to correct what we've done.

  In November 2008 we published the article [10 Advanced PHP Tips To Improve
  Your
  Programming](https://smashingmagazine.com/2008/11/18/10-advanced-php-tips-to-improve-your-progamming/).
  Apparently, according to negative comments to the post, it contained some
  errors and some statements that are just wrong. **We sincerely apologize for
  our mistake**, and we are truly sorry for any inconvenience we caused by it.
  However, this simple apology is not good enough.

  To solve the problem, we asked Chris Shiflett and Sean Coates, two PHP gurus,
  to take a closer look at the article, explain its errors and make it perfectly
  clear what is actually right and wrong in the theory and practice. This
  article is **a professional response** to our article published a couple of
  months ago.
categories:
  - Coding
  - PHP
  - Tutorials
  - Programming
---
PHP programming has climbed rapidly since its humble beginnings in 1995. Since then, PHP has become the most popular programming language for Web applications. Many popular websites are powered by PHP, and an overwhelming majority of scripts and Web projects are built with the popular language.

Because of PHP’s huge popularity, it has become almost impossible for Web developers not to have at least a working knowledge of PHP. This tutorial is aimed at people who are just past the beginning stages of learning PHP and are ready to roll up their sleeves and get their hands dirty with the language. Listed below are 10 excellent techniques that PHP developers should learn and use every time they program. These tips will speed up proficiency and make the code much more responsive, cleaner and more optimized for performance.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [PHP: What You Need To Know To Play With The Web](https://www.smashingmagazine.com/2010/04/php-what-you-need-to-know-to-play-with-the-web/)
*   [50 Extremely Useful PHP Tools](https://www.smashingmagazine.com/2009/01/50-extremely-useful-php-tools/)
*   [A Guide To PHP Error Messages For Designers](https://www.smashingmagazine.com/2011/11/a-guide-to-php-error-messages-for-designers/)

## 1\. Use an SQL Injection Cheat Sheet

This particular tip is just a link to a useful resource with no discussion on how to use it. Studying various permutations of one specific attack can be useful, but your time is better spent learning how to safeguard against it. Additionally, there is much more to Web app security than SQL injection. <a href="https://shiflett.org/articles/cross-site-scripting">XSS (Cross-Site Scripting)</a> and <a href="https://shiflett.org/articles/cross-site-request-forgeries">CSRF (Cross-Site Request Forgeries)</a>, for example, are at least as common and at least as dangerous.

{{% feature-panel %}}

We can provide some much-needed context, but because we don’t want to focus too much on one attack, we'll first take a step back. Every developer should be familiar with good security practices, and apps should be designed with these practices in mind. A fundamental rule is to never trust data you receive from somewhere else. Another rule is to escape data before you send it somewhere else. Combined, these rules can be simplified to make up a basic tenet of security: filter input, escape output (FIEO).

The root cause of SQL injection is a failure to escape output. More specifically, it is when the distinction between the format of an SQL query and the data used by the SQL query is not carefully maintained. This is common in PHP apps that construct queries as follows:

<pre><code class="language-php">&lt;?php

$query = "SELECT *
          FROM   users
          WHERE  name = '{$_GET['name']}'";

?&gt;</code></pre>

In this case, the value of $_GET['name'] is provided by another source, the user, but it is neither filtered nor escaped.

Escaping preserves data in a new context. The emphasis on escaping output is a reminder that data used outside of your Web app needs to be escaped, else it might be misinterpreted. By contrast, filtering ensures that data is valid before it’s used. The emphasis on filtering input is a reminder that data originating outside of your Web app needs to be filtered, because it cannot be trusted.

Assuming we're using MySQL, the SQL injection vulnerability can be mitigated by escaping the name with mysql_real_escape_string(). If the name is also filtered, there is an additional layer of security. (Implementing multiple layers of security is called "defense in depth" and is a very good security practice.) The following example demonstrates filtering input and escaping output, with naming conventions used for code clarity:

<pre><code class="language-php">&lt;?php

// Initialize arrays for filtered and escaped data, respectively.
$clean = array();
$sql = array();

// Filter the name. (For simplicity, we require alphabetic names.)
if (ctype_alpha($_GET['name'])) {
    $clean['name'] = $_GET['name'];
} else {
    // The name is invalid. Do something here.
}

// Escape the name.
$sql['name'] = mysql_real_escape_string($clean['name']); 

// Construct the query.
$query = "SELECT *
          FROM   users
          WHERE  name = '{$sql['name']}'";

?&gt;</code></pre>

Although the use of naming conventions can help you keep up with what has and hasn't been filtered, as well as what has and hasn't been escaped, a much better approach is to use prepared statements. Luckily, with <abbr title="PHP Data Objects">PDO</abbr>, PHP developers have a universal <abbr title="application programming interface">API</abbr> for data access that supports prepared statements, even if the underlying database does not.

Remember, SQL injection vulnerabilities exist when the distinction between the format of an SQL query and the data used by the SQL query is not carefully maintained. With prepared statements, you can push this responsibility to the database by providing the query format and data in distinct steps:

<pre><code class="language-php">&lt;?php

// Provide the query format.
$query = $db-&gt;prepare('SELECT *
                       FROM   users
                       WHERE  name = :name');

// Provide the query data and execute the query.
$query-&gt;execute(array('name' =&gt; $clean['name']));

?&gt;</code></pre>

The <a href="https://php.net/pdo">PDO manual page</a> provides more information and examples. Prepared statements offer the strongest protection against SQL injection.</p>

## 2\. Know the Difference Between Comparison Operators

This is a good tip, but it is missing a practical example that demonstrates when a non-strict comparison can cause problems.

If you use strpos() to determine whether a substring exists within a string (it returns FALSE if the substring is not found), the results can be misleading:

<pre><code class="language-php">&lt;?php

$authors = 'Chris &amp; Sean';

if (strpos($authors, 'Chris')) {
    echo 'Chris is an author.';
} else {
    echo 'Chris is not an author.';
}

?&gt;</code></pre>

Because the substring Chris occurs at the very beginning of Chris &amp; Sean, strpos() correctly returns 0, indicating the first position in the string. Because the conditional statement treats this as a Boolean, it evaluates to FALSE, and the condition fails. In other words, it looks like Chris is not an author, but he is!

This can be corrected with a strict comparison:

<pre><code class="language-php">&lt;?php

if (strpos($authors, 'Chris') !== FALSE) {
    echo 'Chris is an author.';
} else {
    echo 'Chris is not an author.';
}

?&gt;</code></pre>

## 3\. Shortcut the else

This tip accidentally stumbles upon a useful practice, which is to always initialize variables before you use them. Consider a conditional statement that determines whether a user is an administrator based on the username:

<pre><code class="language-php">&lt;?php

if (auth($username) == 'admin') {
    $admin = TRUE;
} else {
    $admin = FALSE;
}

?&gt;</code></pre>

This seems safe enough, because it’s easy to comprehend at a glance. Imagine a slightly more elaborate example that sets variables for name and email as well, for convenience:

<pre><code class="language-php">&lt;?php

if (auth($username) == 'admin') {
    $name = 'Administrator';
    $email = 'admin@example.org';
    $admin = TRUE;
} else {
    /* Get the name and email from the database. */
    $query = $db-&gt;prepare('SELECT name, email
                           FROM   users
                           WHERE  username = :username');
    $query-&gt;execute(array('username' =&gt; $clean['username']));
    $result = $query-&gt;fetch(PDO::FETCH_ASSOC);
    $name = $result['name'];
    $email = $result['email']; 
    $admin = FALSE;
}

?&gt;</code></pre>

Because $admin is still always explicitly set to either TRUE or FALSE, all is well, but if a developer later adds an elseif, there’s an opportunity to forget:

<pre><code class="language-php">&lt;?php

if (auth($username) == 'admin') {
    $name = 'Administrator';
    $email = 'admin@example.org';
    $admin = TRUE;
} elseif (auth($username) == 'mod') {
    $name = 'Moderator';
    $email = 'mod@example.org';
    $moderator = TRUE;
} else {
    /* Get the name and email. */
    $query = $db-&gt;prepare('SELECT name, email
                           FROM   users
                           WHERE  username = :username');
    $query-&gt;execute(array('username' =&gt; $clean['username']));
    $result = $query-&gt;fetch(PDO::FETCH_ASSOC);
    $name = $result['name'];
    $email = $result['email']; 
    $admin = FALSE;
    $moderator = FALSE;
}

?&gt;</code></pre>

If a user provides a username that triggers the elseif condition, $admin is not initialized. This can lead to unwanted behavior, or worse, a security vulnerability. Additionally, a similar situation now exists for $moderator, which is not initialized in the first condition.

By first initializing $admin and $moderator, it’s easy to avoid this scenario altogether:

<pre><code class="language-php">&lt;?php

$admin = FALSE;
$moderator = FALSE;

if (auth($username) == 'admin') {
    $name = 'Administrator';
    $email = 'admin@example.org';
    $admin = TRUE;
} elseif (auth($username) == 'mod') {
    $name = 'Moderator';
    $email = 'mod@example.org';
    $moderator = TRUE;
} else {
    /* Get the name and email. */
    $query = $db-&gt;prepare('SELECT name, email
                           FROM   users
                           WHERE  username = :username');
    $query-&gt;execute(array('username' =&gt; $clean['username']));
    $result = $query-&gt;fetch(PDO::FETCH_ASSOC);
    $name = $result['name'];
    $email = $result['email'];
}

?&gt;</code></pre>

Regardless of what the rest of the code does, it’s now clear that $admin is FALSE unless it is explicitly set to something else, and the same is true for $moderator. This also hints at another good security practice, which is to fail safely. The worst that can happen as a result of not modifying $admin or $moderator in any of the conditions is that someone who is an administrator or moderator is not treated as one.

If you want to shortcut something, and you’re feeling a little disappointed that our example includes an else, we have a bonus tip that might interest you. We’re not certain it can be considered a shortcut, but we hope it’s helpful nonetheless.

Consider a function that determines whether a user is authorized to view a particular page:

<pre><code class="language-php">&lt;?php

function authorized($username, $page) {
    if (!isBlacklisted($username)) {
        if (isAdmin($username)) {
            return TRUE;
        } elseif (isAllowed($username, $page)) {
            return TRUE;
        } else {
            return FALSE;
        }
    } else {
        return FALSE;
    }
}

?&gt;</code></pre>

This example is actually pretty simple, because there are only three rules to consider: administrators are always allowed access; those who are blacklisted are never allowed access; and isAllowed() determines whether anyone else has access. (A special case exists when an administrator is blacklisted, but that is an unlikely possibility, so we’re ignoring it here.) We use functions for the rules to keep the code simple and to focus on the logical structure.

There are numerous ways this example can be improved. If you want to reduce the number of lines, a compound conditional can help:

<pre><code class="language-php">&lt;?php

function authorized($username, $page) {
    if (!isBlacklisted($username)) {
        if (isAdmin($username) || isAllowed($username, $page)) {
            return TRUE;
        } else {
            return FALSE;
        }
    } else {
        return FALSE;
    }
}

?&gt;</code></pre>

In fact, you can reduce the entire function to a single compound conditional:

<pre><code class="language-php">&lt;?php

function authorized($username, $page) {
    if (!isBlacklisted($username) &amp;&amp; (isAdmin($username) || isAllowed($username, $page)) {
        return TRUE;
    } else {
        return FALSE;
    }
}

?&gt;</code></pre>

Finally, this can be reduced to a single return:

<pre><code class="language-php">&lt;?php

function authorized($username, $page) {
    return (!isBlacklisted($username) &amp;&amp; (isAdmin($username) || isAllowed($username, $page));
}

?&gt;</code></pre>

If your goal is to reduce the number of lines, you’re done. However, note that we’re using isBlacklisted(), isAdmin(), and isAllowed() as placeholders. Depending on what’s involved in making these determinations, reducing everything to a compound conditional may not be as attractive.

This brings us to our tip. A return immediately exits the function, so if you return as soon as possible, you can express these rules very simply:

<pre><code class="language-php">&lt;?php

function authorized($username, $page) {

    if (isBlacklisted($username)) {
        return FALSE;
    }

    if (isAdmin($username)) {
        return TRUE;
    }

    return isAllowed($username, $page);
}

?&gt;</code></pre>

This uses more lines of code, but it’s very simple and unimpressive (we’re proudest of our code when it’s the least impressive). More importantly, this approach reduces the amount of context you must keep up with. For example, as soon as you’ve determined whether the user is blacklisted, you can safely forget about it. This is particularly helpful when your logic is more complicated.</p>

## 4\. Drop Those Brackets

Based on the content of this tip, we believe the author means "braces," not brackets. "Curly brackets" may mean braces to some, but "brackets" universally means "square brackets."

This tip should be unconditionally ignored. Without braces, readability and maintainability are damaged. Consider a simple example:

<pre><code class="language-php">&lt;?php

if (date('d M') == '21 May')
    $birthdays = array('Al Franken',
                       'Chris Shiflett',
                       'Chris Wallace',
                       'Lawrence Tureaud');

?&gt;</code></pre>

If you’re good enough, smart enough, secure enough, notorious enough, or pitied enough, you might want to party on the 21st of May:

<pre><code class="language-php">&lt;?php

if (date('d M') == '21 May')
    $birthdays = array('Al Franken',
                       'Chris Shiflett',
                       'Chris Wallace',
                       'Lawrence Tureaud');
    party(TRUE);

?&gt;</code></pre>

Without braces, this simple addition causes you to party every day. Perhaps you have the stamina for it, so the mistake is a welcome one. Hopefully, the silly example doesn’t detract from the point, which is that the excessive partying is an unintended side effect.

In order to promote the practice of dropping braces, the previous article uses short examples such as the following:

<pre><code class="language-php">&lt;?php

if ($gollum == 'halfling') $height --;  
else $height ++;

?&gt;</code></pre>

Because each condition is constrained to a single line, such mistakes might be less likely, but this leads to another problem: inconsistencies are jarring and require more time to read and comprehend. Consistency is such a valued quality that developers often abide by a coding standard even if they dislike the coding standard itself.

We recommend always using braces:

<pre><code class="language-php">&lt;?php

if (date('d M') == '21 May') {
    $birthdays = array('Al Franken',
                       'Chris Shiflett',
                       'Chris Wallace',
                       'Lawrence Tureaud');
    party(TRUE);
}

?&gt;
 </code></pre>

You’re welcome to party every day, but make sure it’s deliberate, and please be sure to invite us!

## 5\. Favor str_replace() Over ereg_replace() and preg_replace()

We hate to sound disparaging, but this tip demonstrates the sort of misunderstanding that leads to the same misuse it’s trying to prevent. It’s an obvious truth that string functions are faster at string matching than regular expression functions, but the author’s attempt to draw a corollary from this fails miserably:
<blockquote>If you’re using regular expressions, then ereg_replace() and preg_replace() will be much faster than str_replace().</blockquote>

Because str_replace() does not support pattern matching, this statement makes no sense. The choice between string functions and regular expression functions comes down to which is fit for purpose, not which is faster. If you need to match a pattern, use a regular expression function. If you need to match a string, use a string function.</p>

## 6\. Use Ternary Operators

The benefit of the ternary operator is debatable (there’s only one, by the way). Here is a line of code from an audit we performed recently:

<pre><code class="language-php">&lt;?php

$host = strlen($host) &gt; 0 ? $host : htmlentities($host);

?&gt;</code></pre>

Oops! The author actually means to escape $host if the string length is greater than zero, but instead accidentally does the opposite. Easy mistake to make? Maybe. Easy to miss during a code audit? Certainly. Concision doesn’t necessarily make the code any better.

The ternary operator may be fine for one-liners, prototypes, and templates, but we strongly believe that an ordinary conditional statement is almost always better. PHP is descriptive and verbose. We think code should be, too.</p>

## 7\. Memcached

Disk access is slow. Network access is slow. Databases typically use both.

Memory is fast. Using a local cache avoids the overhead of network and disk access. Combine these truths and you get memcached, a “distributed memory object caching system” originally developed for the Perl-based blogging platform LiveJournal.

If your application isn’t distributed across multiple servers, you probably don’t need memcached. Simpler caching approaches — serializing data and storing it in a temporary file, for example — can eliminate a lot of redundant work on each request. In fact, this is the sort of low-hanging fruit we consider when helping our clients tune their apps.

One of the easiest and most universal ways to cache data in memory is to use the shared memory helpers in <a href="https://pecl.php.net/apc"><abbr title="Alternative PHP Cache">APC</abbr></a>, a caching system originally developed by our colleague George Schlossnagle. Consider the following example:

<pre><code class="language-php">&lt;?php

$feed = apc_fetch('news');

if ($feed === FALSE) {
    $feed = file_get_contents('https://example.org/news.xml');
    // Store this data in shared memory for five minutes.
    apc_store('news', $feed, 300);
}

// Do something with $feed.

?&gt;</code></pre>

With this type of caching, you don’t have to wait on a remote server to send the feed data for every request. Some latency is incurred — up to five minutes in this example — but this can be adjusted to as close to real time as your app requires.</p>

## 8\. Use a Framework

All decisions have consequences. We appreciate frameworks — in fact, the main developers behind <a href="https://cakephp.org/">CakePHP</a> and <a href="https://solarphp.com/">Solar</a> work with us at OmniTI — but using one doesn’t magically make what you’re doing better.

In December, our colleague Paul Jones wrote an article for PHP Advent called The Framework as Franchise, in which he compares frameworks to business franchises. He refers to a suggestion by Michael Gerber from his book "The E-Myth Revisited":
<blockquote>Gerber notes that to run a successful business, the entrepreneur needs to act as if he is going to sell his business as a franchise prototype. It is the only way the business owner can make the business operate without him being personally involved in every decision.</blockquote>

This is good advice. Whether you’re using a framework or defining your own standards and conventions, it’s important to consider the value from the perspective of future developers.

Although we would love to give you a universal truth, extending this idea to suggest that a framework is always appropriate isn’t something we’re willing to do. If you ask us whether you should use a framework, the best answer we could give is, “It depends.”

## 9\. Use the Suppression Operator Correctly

Always try to avoid using the error suppression operator. In the previous article, the author states:
<blockquote>The @ operator is rather slow and can be costly if you need to write code with performance in mind.</blockquote>

Error suppression is slow. This is because PHP dynamically changes error_reporting to 0 before executing the suppressed statement, then immediately changes it back. This is expensive.

Worse, using the error suppression operator makes it difficult to track down the root cause of a problem.

The previous article uses the following example to support the practice of assigning a variable by reference when it is unknown if $albus is set:

<pre><code class="language-php">&lt;?php

$albert =&amp; $albus;

?&gt;</code></pre>

Although this works — for now — relying on strange, undocumented behavior without a very good understanding of why it works is a good way to introduce bugs. Because $albert is assigned to $albus by reference, future modifications to $albus will also modify $albert.

A much better solution is to use isset(), with braces:

<pre><code class="language-php">&lt;?php

if (!isset($albus)) {
    $albert = NULL;
}

?&gt;</code></pre>

Assigning $albert to NULL is the same as assigning it to a nonexistent reference, but being explicit greatly improves the clarity of the code and avoids the referential relationship between the two variables.

If you inherit code that uses the error suppression operator excessively, we’ve got a bonus tip for you. There is a new <abbr title="PHP Extension Community Library">PECL</abbr> extension called <a href="https://pecl.php.net/package/scream">Scream</a> that disables error suppression.</p>

## 10\. Use isset() Instead of strlen()

This is actually a neat trick, although the previous article completely fails to explain it. Here is the missing example:

<pre><code class="language-php">&lt;?php

if (isset($username[5])) {
    // The username is at least six characters long.
}

?&gt;</code></pre>

When you treat strings as arrays, each character in the string is an element in the array. By determining whether a particular element exists, you can determine whether the string is at least that many characters long. (Note that the first character is element 0, so $username[5] is the sixth character in $username.)

The reason this is slightly faster than strlen() is complicated. The simple explanation is that strlen() is a function, and isset() is a language construct. Generally speaking, calling a function is more expensive than using a language construct.

{{< signature "al" >}}

