---
title: 'Be Watchful: PHP And WordPress Functions That Can Make Your Site Insecure'
slug: php-wordpress-functions-site-insecure
author: david-hayes
image: >-
  //archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f4929244-c9c4-41a6-b138-cdcbcd82a879/wp-ranking-semrush-site-audit-example-800w-opt.png
date: 2018-01-25T15:50:56+01:00
summary: >-
  Before deploying a new plugin in WordPress, it's a good idea to keep a list of easy-to-misuse functions by your side. Let's take a closer look at some functions which you can and should use as part of a broader security strategy.
description: >-
  Before deploying a new plugin in WordPress, it's a good idea to keep a list of easy-to-misuse functions by your side. Let's take a closer look at some functions which you can and should use as part of a broader security strategy.
categories:
  - WordPress
  - PHP
  - Plugins
  - Security
---
Security of a WordPress (or any) website is a multi-faceted problem. The most important step anyone can take to make sure that a site is secure is to keep in mind that no single process or method is sufficient to ensure nothing bad happens. But there are things you can do to help. One of them is to be on the watch, in the code you write and the code from others you deploy, for functions that can have negative consequences. In this article, we'll cover exactly those: functions that a WordPress developer should think clearly before using.

WordPress itself provides a sizable library of functions, some of which can be dangerous. Beyond that, there are lots of PHP functions that a WordPress (PHP) developer will use with some frequency that can be dangerous when used.

All of these functions have legitimate and safe uses, but they're also functions that can make it easy for your code to be abused for bad ends. We'll cover the stuff most likely to be the cause of a security vulnerability, and why you must watch for them. We'll first run down PHP functions in your code that bad actors can use for evil, and then talk about WordPress-specific PHP functions that can also cause headaches.

## PHP Functions To Watch Out For

As we said, PHP contains a lot of easy-to-use functions. Some of those functions are notorious for the ease with which people can do bad things with them. All of these functions have a proper use, but be careful about how you use them and how other code you pull into a project does.

We're going to assume you've already got [magic quotes](https://php.net/manual/en/security.magicquotes.php) and [register globals](https://php.net/manual/en/security.globals.php) turned off if your version of PHP supports them. They were off by default in PHP 5 and up, but could be turned on for versions below 5.4. Few hosts allowed it, but I don't think a PHP security article is truly complete without including them.

{{% feature-panel %}}

Or a mention that PHP 5.6 is the last 5.x version still with ongoing security support. You should be on it, at least. And you should have a plan to move onto PHP 7 before 5.6 support ends at the end of 2018.

After that, you'll just have some risky functions to deal with. Starting with...

### `extract` Is Bad News, Especially On `$_POST` Or Similar

Fortunately, use of [PHP's `extract` function](https://php.net/manual/en/function.extract.php) has largely fallen out of favor. The core of its use was that you could run it on an array of data, and its key-value pairs would become living variables in your code. So

<pre><code class="language-php">$arr = array(
    'red' => 5
);
extract($arr);
echo $red; // 5
</code></pre>

would work. This is cool, but it's also really dangerous if you're extracting `$_GET`, `$_POST`, etc. In those cases, you're essentially recreating the `register_globals` problem yourself: an outside attacker can change your variable values easily by adding a query string or form field. The best solution is simple: don't use `extract`.

If you create the array you extract yourself, it's not specifically a security problem to use `extract`, and in some cases, it can be useful. But all uses of it have the problem of confusing future readers. Creating an array and calling `extract` is more confusing than just declaring your variables. So I encourage you to do manual declarations instead, unless it's completely unfeasible.

If you must use `extract` on user input, you should always use the `EXTR_SKIP` flag. This still has the confusion problem, but it gets rid of the possibility that your preset values can be changed by a malicious outsider via a simple query string or web form modification. (Because it "skips" already set values.)

### "`eval` Is Evil" Because Arbitrary Code Is Scary

[`eval` in PHP](https://php.net/manual/en/function.eval.php) and just about any other language that carries it is always high up on lists like this. And for good reason. PHP's official documentation on PHP.net says it pretty frankly:

**CAUTION**: The eval() language construct is very dangerous because it allows execution of arbitrary PHP code. Its use thus is discouraged. If you have carefully verified that there is no other option than to use this construct, pay special attention not to pass any user provided data into it without properly validating it beforehand.

`eval` lets any arbitrary string in your program be run as if it's PHP code. That means that it's useful for "meta-programming" where you're building a program that can itself build a program. It's also really dangerous because if you ever allow arbitrary sources (like a text box on a web page) to be passed immediately to your `eval` string evaluator, you've suddenly made it trivially easy for a malicious attacker to do pretty much *anything* PHP can do on your server. This includes, obviously, connecting to the database, deleting files, and just about anything else someone can do when SSHed into a machine. This is bad.

If you must use `eval` in your program, you should go out of your way to make sure that you don't allow arbitrary user input to be passed into it. And if you *must* allow arbitrary users access to the inputs to `eval`, confine what they can do via a blacklist of commands you don't let them run, or (better, but far harder to implement) a whitelist which is only the commands you consider safe. Better still, only allow a small number of specific parameter changes, like only validated integers.

But always keep in mind this line from Rasmus Lerdorf, the founder of PHP:

<blockquote>"If `eval()` is the answer, you're almost certainly asking the wrong question."</blockquote>

### Variations On `eval`

There are, in addition to the well-known `eval`, a variety of other ways that PHP has historically supported strings-evaluated-as code. The two that are most relevant for WordPress developers are `preg_replace` with the `/e` modifier, and `create_function`. Each works a little differently, and `preg_replace` after PHP 5.5.0 doesn't work at all. (PHP 5.5 and below are no longer getting official security updates, and are thus best not used.)

### `/e` Modifiers In Regex Are Also "Evil"

If you're running PHP 5.4.x or below, you'll want to keep an eye out for PHP `preg_replace` calls that end with an e. That can look like:

<pre><code class="language-php">$html = preg_replace(
    '(<h([1-6])>(.*?)</h\1>)e',
    '"<h$1>" . strtoupper("$2") . "</h$1>"',
    $html
);)
// or
$html = preg_replace(
    '~<h([1-6])>(.*?)</h\1>~e',
    '"<h$1>" . strtoupper("$2") . "</h$1>"',
    $html
);)
</code></pre>

PHP offers various ways to "fence" in your regular expression, but the core thing you want to be on the lookout for is "e" as the last character to the first argument of `preg_replace`. If it's there, you're actually passing the whole found segment as the argument to your inline PHP, and then `eval`ing it. This has the exact same issues as `eval` if you're letting user-input go into your function. The example code can be replaced by instead using `preg_replace_callback`. The advantage of this is that you've written out your function, so it's harder for an attacker to change what gets evaluated. So you'd write the above as:

<pre><code class="language-php">// uppercase headings
$html = preg_replace_callback(
    '(<h([1-6])>(.*?)</h\1>)',
    function ($m) {
        return "<h$m[1]>" . strtoupper($m[2]) . "</h$m[1]>";
    },
    $html
);
</code></pre>

### Letting User Input `create_function`s Is Also Bad...

PHP also has the `create_function` function. This is now deprecated in PHP 7.2, but it was very similar to `eval` and had the same basic drawbacks: it allows a string (the second argument) to be turned into executable PHP. And it had the same risks: it's too easy for you to accidentally give a smart cracker the ability to do *anything* on your server if you weren't careful.

This one, if you're on PHP above 5.3, is even easier to fix than `preg_replace` though. You can just create your own anonymous function without using strings as intermediaries. This is both more secure and more readable, at least to my eyes.

### `assert` Is Also `eval`-Like

[`assert`](https://php.net/manual/en/function.assert.php) isn't a function I see many PHP developers use, in WordPress or outside of it. Its intent is for very-lightweight assertions about preconditions for your code. But it does, also, support an `eval`-type operation. For that reason, you should be as wary of it as you are of `eval`. String-based assertions (the heart of why this is bad) are also deprecated in PHP 7.2, which means it should be less of concern in the future.

### Including Variable Files Is A Way Of Possibly Allowing Uncontrolled PHP Execution

We've pretty well explored why `eval` is bad, but something like `include` or `require($filename'.php')` can, especially where `$filename` is set from a user-controllable value, be similarly bad news. The reason is subtly different from `eval`. Variable file names are often used for things like simple URL-to-file routing in non-WordPress PHP apps. But you might see them used in WordPress as well.

The heart of the issue that when you `include` or `require` (or `include_once` or `require_once`) you're making your script execute the included file. It's, more or less, conceptually `eval`ing that file, though we rarely think about it that way.

If you've written all the files that your variable `include` might pull in, and have considered what would happen when it does, you're fine. But it's bad news if you've not considered what `include`ing `password.php` or `wp-config.php` will do. It's also bad news if someone could add a malicious file and then execute your `include` (although at that point you probably have bigger problems).

The solution to this isn't too hard though: hard-code includes when you can. When you can't, have either a whitelist (better) or a blacklist of files that can be included. If the files in the whitelist (that is: you've audited what it does when added), you'll know you're safe. If it's not on your whitelist, your script won't include it. With that simple tweak, you're pretty secure. A whitelist would look something like this:

<pre><code class="language-php">$white_list = [‘db.php’, filter.php’, ‘condense.php’]
If (in_array($white_list, $file_to_include)) {
include($file_to_include);
}
</code></pre>

### Never Pass User Input To `shell_exec` And Variants

This is a big one. `shell_exec`, `system`, `exec`, and backticks in PHP all allow the code you're running to talk to the underlying (usually Unix) shell. This is similar to what makes `eval` dangerous but doubled. Doubled because if you let user-input through here carelessly, the attacker isn't even bound by the constraints of PHP.

The ability to run shell commands from PHP can be *very* useful as a developer. But if you ever let a user's input in there, they have the ability to surreptitiously gain lots of dangerous powers.  So I'd go so far as to say that user input should *never* be passed to `shell_exec`-type functions.

The best way I could think to handle this type of situation, if you were tempted to implement it, would be to provide users access to a small set of known-safe predefined shell commands. That *might* be possible to secure. But even then I'd warn you to be very careful.

### Watch For `unserialize`; It Runs Code Automatically

The core action of calling `serialize` on a living PHP object, storing that data off somewhere, and then using that stored value later to `unserialize` that object back to life is cool. It's also reasonably common, but it can be risky. Why risky? If the input to that `unserialize` call is not completely secure (say it is stored as a cookie rather than in your database…), an attacker can change the internal state of your object in a way that makes the `unserialize` call do something bad.

This exploit is more esoteric and less likely to be noticed than an `eval` issue. But if you're using a cookie as a storage mechanism for serialized data, don't use `serialize` for that data. Use something like `json_encode` and `json_decode`. With those two PHP will never auto-execute any code.

The core vulnerability here is that when PHP `unserialize`s a string into a class, it calls the magic `__wakeup` method on that class. If unvalidated user input is allowed to be `unserialized`, something like a database call or file deletion in the `__wakeup` method could potentially be pointed at a dangerous or undesirable location.

`unserialize` is distinct from the `eval` vulnerabilities because it requires the use of magic methods on objects. Rather than creating their own code, the attacker is forced to abuse your already-written methods on an object. Both the `__destruct` and `__toString` magic methods on objects are also risky, as [this OWASP Wiki page explains](https://www.owasp.org/index.php/PHP_Object_Injection).

In general, you're OK if you don't use the `__wakeup`, `__destruct`, or `__toString` methods in your classes. But because you may later see someone add them to a class, it's a good idea to never let a user near your calls to `serialize` and `unserialize` and pass all public data for that sort of use though something like JSON (`json_encode` and `json_decode`) where there is never automatic code execution.

### Fetching URLs With `file_get_contents` Is Risky

A common practice when quickly writing some PHP code that has to call an external URL is to reach for `file_get_contents`. It's quick, it's easy, but it's not super secure.

The issue with `file_get_contents` is subtle, but it's common enough that hosts will sometimes configure PHP not to even allow you to access external URLs. This is meant to protect you.

The issue here is that `file_get_contents` will fetch remote pages for you. But when it does that, it doesn't check on the integrity of the HTTPS protocol connection. What that means is that your script could potentially be a victim of a man-in-the-middle attack which would allow an attacker to put pretty much whatever they want into your `file_get_contents` page result.

This is a more esoteric attack. But to protect against it when I write modern (Composer-based) PHP, I almost always use [Guzzle](https://docs.guzzlephp.org/en/stable/) to wrap the more-secure cURL API. In WordPress, it's even easier: use [`wp_remote_get`](https://codex.wordpress.org/Function_Reference/wp_remote_get). It works much more consistently than `file_get_contents`, and it'll default to verifying SSL connections. (You can toggle that off, but, um, maybe don't...) Better still, but slightly more annoying to talk about, are [`wp_safe_remote_get`](https://developer.wordpress.org/reference/functions/wp_safe_remote_get/), etc. These work identically to the functions without `safe_` in their name, but they’ll make sure that unsafe redirects and forwards do not happen along the way.

### Don't Blindly Trust URL Validation From `filter_var`

So this one's a little obscure, so props to Chris Weigman for explaining it in [this WordCamp talk](https://wordpress.tv/2014/10/17/chris-wiegman-securing-your-code-wordpress-security-for-developers/). In general, PHP's `filter_var` is a great way to either validate or sanitize data. (Although, don't get confused about which you're trying to do...)

The issue here is pretty specific: if you're trying to use it to ensure that a URL is safe, `filter_var` doesn't validate the protocol. That isn't often an issue, but if you're passing user input to this method for validation, and are using `FILTER_VALIDATE_URL`, something like `javascript://comment%0aalert(1)` will get through. That is, this can be a very good vector for a basic XSS attack in a place you won't have expected.

For validating a URL, WordPress's `esc_url` function will have a similar impact, but only lets through allowed protocols. `javascript` is not in the default list, so it would keep you safe. However, unlike `filter_var`, it'll return an empty string (not a false) for a disallowed protocol that is passed to it.

## WordPress-specific Functions To Keep An Eye On

In addition to core-PHP potentially-vulnerable functions, there are some WordPress-specific functions that can be a bit of a gotcha. Some of these are very similar to the variety of dangerous functions listed above, some a little different.

### WordPress Unserializes With `maybe_unserialize`

This one's probably obvious if you read the above. In WordPress there's a function called `maybe_unserialize` and, as you’d guess, it unserializes what's passed to it if need be.

There's not any new vulnerability that this introduces, the issue is simply that just like the core `unserialize` function, this one can cause a vulnerable object to be exploited when it's unserialized.

### `is_admin` Doesn't Answer If A User Is An Administrator!

This one's pretty simple, but the function is ambiguous in name, and so it's prone to confuse people or be missed if you're in a hurry. You should always check that a user who's trying to perform an action in WordPress has the rights and privileges necessary to perform that action. In order to that, you *should* use the [`current_user_can`](https://developer.wordpress.org/reference/functions/current_user_can/) function.

But you might, mistakenly, think that `is_admin` will tell if you if the current user is an Administrator-level account and thus should be able to set an option your plugin uses. This is a mistake. What `is_admin` does in WordPress is instead telling you if the current page load is on the administration side of the site (vs. the front-side). So every user who can access an administration page (like the "Dashboard") will be able to potentially pass this check. As long as you remember that `is_admin` is about the type of page, not the current user, you'll be fine.

### `add_query_arg()` Doesn't Sanitize URLs

This isn't so common, but there was a big wave of updates in the WordPress ecosystem a few years ago because the public documentation on this functions wasn't correct. The core issue is that the `add_query_arg` function (and its inverse `remove_query_arg`) doesn't automatically sanitize the site URL if a URL wasn't passed to it, and people had thought that it did. [Many plugins had been misled by the Codex, and were using this unsafely as a result.](https://make.wordpress.org/plugins/2015/04/20/fixing-add_query_arg-and-remove_query_arg-usage/)

The core thing they had to do different: sanitize the result of a call to this function before using it. If you do that, you're really safe from the XSS attacks that you thought they were. So that looks something like:

<pre><code class="language-php">echo esc_url( add_query_arg( 'foo', 'bar' ) );
</code></pre>

### `$wpdb->query()` Is Open To SQL Injection Attack

If you know about [SQL injection](https://en.wikipedia.org/wiki/SQL_injection), this may seem silly, even superfluous to list. Because the thing is that any way you access a database (say using PHP's `mysqli` or PDO database drivers) for creating database queries that allow for SQL injection attacks.

The reason I'm specifically calling out `$wpdb->query` is that some other methods (like `insert`, `delete`, etc.) on `$wpdb` take care of injection attacks for you. Additionally, if you're used to making basic WordPress database queries with `WP_Query` or similar, you won't have needed to consider SQL injection. This is why I'm calling it out: to make sure you understand an injection attack on the database is possible when you first try to use `$wpdb` to make your own query.

What to do? Use [`$wpdb->prepare()`](https://developer.wordpress.org/reference/classes/wpdb/prepare/) and *then* `$wpdb->query()`. You’ll also want to make sure you prepare before other “getting” methods of `$wpdb` like, `get_row()` and `get_var()`. Otherwise [Bobby Tables](https://xkcd.com/327/) might get you.

### `esc_sql` Doesn’t Secure You From SQL Injection Either

For most WordPress developers, I’d say that `esc_sql` doesn’t register with any meaning, but it should. Ase we just mentioned, you should be using `wpdb->prepare()` before you make any database query. This’ll keep you safe. But it’s tempting and understandable that a developer may reach for `esc_sql` instead. And they might expect it’d be safe.

The issue is that [`esc_sql`](https://codex.wordpress.org/Function_Reference/esc_sql) doesn’t have as robust protections against SQL injection. It’s really [a glorified version of PHP’s `add_slashes` function](https://php.net/manual/en/function.addslashes.php), which you’ve been discouraged from using to protect your database for years.

## There's More To Do, But This Is A Big Start

There's a lot more to security than just being on the lookout for functions in your code that attackers can misuse. We didn't, for example, discuss in much depth the need to validate and sanitize all data you receive from users and escape it before you put it into a webpage (though I did recently publish an article on that topic, "[Protecting Your WordPress Site Against A Cross-Site Scripting Attack](https://wpshout.com/complete-guide-sanitizing-escaping/)"). But you can and should use this as part of a broader security strategy.

Keeping this list of easy-to-misuse functions by your side as you do a final inspection before deploying a new plugin in WordPress is a great idea. But you'll also want to make sure you trust the security of your hosting, make sure your users have good passwords, and much more.

The core thing to remember about security is that your weakest link is the one that matters. Good practices in one area bolster possible weak-points somewhere else, but they can never totally correct it. But be watchful of these functions, and you'll have a leg-up on most.

{{< signature "mc, ra, il" >}}

