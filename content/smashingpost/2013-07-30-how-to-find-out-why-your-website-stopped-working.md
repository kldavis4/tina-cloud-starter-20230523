---
title: How To Find Out Why Your Website Stopped Working
slug: how-to-find-out-why-your-website-stopped-working
image: null
date: 2013-07-30T11:03:37.000Z
author: paul-tero
description: >-
  Imagine that you wake up one morning, reach groggily for your laptop and fire
  it up. You’ve just finished developing a brand new website and last night you
  were proudly clicking through the product list. The browser window is still
  open, the Widget 3000 is still sparkling in its AJAXy newness.
categories:
  - Coding
  - PHP
  - Techniques
  - Backend
---
Today we are happy to present to you the second part of the sample chapter from <a href="https://shop.smashingmagazine.com/products/smashing-book-4-ebooks">Smashing Book #4</a>. You might want to read the <a href="https://www.smashingmagazine.com/2013/07/23/how-to-fix-the-web-obscure-back-end-techniques-and-terminal-secrets/">first part</a> of this chapter beforehand — if you haven't already.

Just a little reminder before you start: In part 1 we explored the infrastructure of the Internet and the make-up of a Web server. We left off at the stage where our Web server software is up and running again, and we've just double-checked this by telnetting an HTTP request and received the successful response code. It's now time for...</p>

## <span class="rh">Further Reading</span> on SmashingMag: [Link](https://www.smashingmagazine.com/2010/12/what-to-do-when-your-website-goes-down/#further-reading-on-smashingmag)

*   [<span class="headline">Obscure Back-End Techniques And Terminal Secrets</span>](https://www.smashingmagazine.com/2013/07/how-to-fix-the-web-obscure-back-end-techniques-and-terminal-secrets/)
*   [9 Steps To A Happy Relationship With Your Hosting Provider](https://www.smashingmagazine.com/2009/03/9-steps-to-a-happy-relationship-with-your-hosting-provider/)
*   [Effective Maintenance Pages: Examples and Best Practices](https://www.smashingmagazine.com/2009/06/effective-maintenance-pages-examples-and-best-practices/)

## Finding Your Website

The 200 code means that your home page is okay, and you should be able to visit it in your browser. However, it may not show what you expected, and your fabulous Widget 3000 page may still be absent.

{{% feature-panel %}}

### Virtual Hosts and Streams

As mentioned above, many servers host multiple websites. One of these is the default website. It is the website you get when you visit the server by IP address https://80.72.139.101/ instead of by name, or when you leave off the <code>Host:</code> line in the HTTP request while telnetting. The rest of the websites are known as virtual hosts. Every one of these websites has a physical location on the server known as its document root. To further investigate your website woes, <strong>you need to discover its document root.</strong>

Fortunately and sensibly, most server management packages like Plesk store their virtually hosted websites according to their domain name, so you can usually just <code>find</code> directly on the domain name. The / in the command below tells <code>find</code> to search the whole file system, the <code>-type d</code> looks only for <u>d</u>irectories, and the <code>-name</code> part searches for any directories containing "smashingmagazine". The asterisks are wild cards. You'll need to either escape them <code>*smashingmagazine*</code> or put them in quotes <code>"*smashingmagazine*"</code>:

<pre><code class="language-javascript">$ find / -type d -name "*smashingmagazine*"
find: '/var/run/cups/certs': Permission denied
find: '/var/run/PolicyKit': Permission denied
/var/www/vhosts/smashingmagazine.com
/var/www/vhosts/smashingmagazine.com/httpdocs...</code></pre>

If you run this command as a normal unprivileged user, you will probably see lots of "Permission denied" as <code>find</code> tries to explore forbidden places. You are actually seeing two types of output here: <code>stdout</code> for "standard output" and <code>stderr</code> for "standard error". They are called output streams and are confusingly mixed together.

You have already encountered the pipe symbol | for piping the output stream (<code>stdout</code>) of one command into the input stream (<code>stdin</code>) of another. The symbol <code>&gt;</code> can redirect that output into a file. Try this command to send all the matches into a file called matches.txt:

<pre><code class="language-javascript">$ find / -type d -name "*smashingmagazine*" &gt; matches.txt
find: '/var/run/cups/certs': Permission denied
find: '/var/run/PolicyKit': Permission denied...</code></pre>

In this case, all the <code>stdout</code> is redirected into the file matches.txt and only the error output stream <code>stderr</code> is displayed on the screen. By adding the number 2 you can instead redirect <code>stderr</code> into a file and just display <code>stdout</code>:

<pre><code class="language-javascript">$ find / -type d -name "*smashingmagazine*" 2&gt; matcherrors.txt
/var/www/vhosts/smashingmagazine.com
/var/www/vhosts/smashingmagazine.com/httpdocs...</code></pre>

There is a special file on Linux, UNIX and Mac computers which is basically a black hole where stuff gets sent and disappears. It's called /dev/null, so to only see <code>stdout</code> and ignore all errors:

<pre><code class="language-javascript">$ find / -type d -name "*smashingmagazine*" 2&gt; /dev/null
/var/www/vhosts/smashingmagazine.com
/var/www/vhosts/smashingmagazine.com/httpdocs...</code></pre>

The end result is that this <code>find</code> command tells you roughly where your document root is. In Plesk, all the virtual hosts are generally stored within the <code>/var/www/vhosts</code> directory, with the document roots in <code>/var/www/vhosts/domain.com/httpdocs.</code>

### The Long Way

You can find the document root more accurately by looking through the configuration files. For Apache servers, you can find the default website's document root by looking through the main configuration file which is usually <code>/etc/apache2/apache2.conf</code> or <code>/etc/httpd/conf/httpd.conf</code>.

<pre><code class="language-javascript">$ grep DocumentRoot /etc/httpd/conf/httpd.conf
DocumentRoot "/var/www/html"</code></pre>

Somewhere inside this conf file will also be an <code>Include</code> line which references other conf files, which may themselves include further conf files. To find the DocumentRoot for your virtual host, you'll need to search through them all. You can do this using <code>grep</code> and <code>find</code> but its a long command, so we will build it up gradually.

First, we will find all the files (because of the <code>-type f</code>) on the whole server (the <code>/</code>) whose names end in "conf" or "include". The <code>-type f</code> finds only files and the <code>-o</code> lets us look for files ending in "conf" <u>o</u>r "include", with surrounding escaped parentheses. As above, the errors are banished into the ether:

<pre><code class="language-javascript">$ find / -type f ( -name *conf -o -name *include ) 2&gt; /dev/null
/var/spool/postfix/etc/resolv.conf
/var/some file with spaces.conf
/var/www/vhosts/myserv.com/conf/last_httpd.include...</code></pre>

This is not quite complete as any files with spaces will confuse the <code>grep</code> command we are about to attempt. To fix that you can pipe the output of the <code>find</code> command through the <code>sed</code> command which allows you to specify a regular expression. Regular expressions are a huge topic in their own right. In the command below, the <code>s/ /\ /g</code> will replace all spaces with a slash followed by a space:

<pre><code class="language-javascript">$ find / -type f ( -name *conf -o -name *include ) 2&gt;/dev/null | sed 's/ /\ /g'
/var/spool/postfix/etc/resolv.conf
/var/some file with spaces.conf
/var/www/vhosts/myserv.com/conf/last_httpd.include...</code></pre>

Now you can use a backtick to embed the results of that <code>find</code> command into a <code>grep</code> command. Using ` is different than | as it actually helps to build a command, rather than just manipulating its input. The <code>-H</code> option to <code>grep</code> tells it so show file names as well. So, now we will look for any reference to "smashingmagazine" in any conf files.

<pre><code class="language-javascript">$ grep -H smashingmagazine `find / -type f ( -name *conf -o -name *include ) 2&gt; /dev/null | sed 's/ /\ /g'`
/var/www/vhosts/smashingmagazine.com/conf/last_httpd.include: ServerName "smashingmagazine.com"...</code></pre>

This may take a few seconds to run. It is finding every conf file on the server and searching through all of them for "smashingmagazine". It may reveal the DocumentRoot directly. If not, it will at least reveal the file where the ServerName or VirtualHost is defined. You can then use <code>grep</code> or <code>less</code> to look through that file for the DocumentRoot.

You can also use the <code>xargs</code> command to do the same thing. It also allows the output from one command to be embedded into another:

<pre><code class="language-javascript">$ find / -type f ( -name *conf -o -name *include ) 2&gt; /dev/null | sed 's/ /\ /g' | xargs grep -H smashingmagazine
/var/www/vhosts/smashingmagazine.com/conf/last_httpd.include: ServerName "smashingmagazine.com"...
$ grep DocumentRoot /var/www/vhosts/smashingmagazine.com/conf/last_httpd.include
DocumentRoot "/var/www/vhosts/smashingmagazine.com/httpdocs"</code></pre>

The end result, hopefully, is that <strong>you've definitively found the document root for your website</strong>.

You can use a similar technique for nginx. It also has a main conf file, usually in <code>/etc/nginx/nginx.conf</code>, and it can also include other conf files, however its document root is just called "root".</p>

### Apache Control Interface

With Apache, there is yet another way to find the right conf file, using the <code>apachectl</code> or newer <code>apache2ctl</code> command with the <code>-S</code> option.

<pre><code class="language-javascript">$ apachectl -S
VirtualHost configuration:
80.72.139.101:80 is a NameVirtualHost
default server default (/usr/local/psa/admin/conf/generated/13656495120.10089200_server.include:87)
port 80 namevhost default (/usr/local/psa/admin/conf/generated/13656495120.10089200_server.include:87)
port 80 namevhost www.smashingmagazine.com (/var/www/vhosts/smashingmagazine.com/conf/last_httpd.include:10)...</code></pre>

If this whizzes by too fast, you can try piping the results through <code>grep</code>. It won't work, however, because <code>grep</code> only operates on <code>stdout</code> and for some reason <code>apachectl</code> outputs its information to <code>stderr</code>. So, you have to first direct <code>stderr</code> into <code>stdout</code> and then send it through <code>grep</code>. This is done by redirecting the error stream 2 into the output stream 1 with <code>2&gt;&amp;1</code>, like this:

<pre><code class="language-javascript">$ apachectl -S 2&gt;&amp;1 | grep smashingmagazine
port 80 namevhost smashingmagazine.com (/var/www/vhosts/smashingmagazine.com/conf/13656495330.08077300_httpd.include:10)</code></pre>

This also reveals the conf file which contains the DocumentRoot for this website. As above further <code>grep</code> or <code>less</code> will reveal the DocumentRoot.</p>

### Checking the Document Root

Now that you've found the document root, you can snoop around to make sure it's alright. Change to the directory with <code>cd</code>:

<pre><code class="language-javascript">$ cd /var/www/vhosts/smashingmagazine.com/httpdocs
bash: cd: /var/www/vhosts/smashingmagazine.com/httpdocs: No such file or directory</code></pre>

If you get the error message "No such file or directory", that is bad news. Either the DocumentRoot has been incorrectly set or your whole website has been deleted. If it is there, you can list the files with <code>ls</code>. The <code>-a</code> also shows hidden files which start with a dot, and <code>-l</code> displays them in <u>l</u>ong format with permissions and dates:

<pre><code class="language-javascript">$ ls -al
drwxrwxrwx  8 nobody  nogroup  4096 May  9 14:03 .
drwxr-xr-x 14 root    root     4096 Oct 13  2012 ..</code></pre>

Every folder will at least show these two entries. The single "." is for the current directory and ".." is for the parent directory. If that's all there is, then the directory is empty.

While you're there, you can double-check you are in the correct place. Create a new file using echo and again using the &gt; symbol to send the output to a file.

<pre><code class="language-javascript">$ echo "&lt;h1&gt;My test file&lt;/h1&gt;" &gt; testfile.html</code></pre>

This will create a file called testfile.html containing a bit of HTML. You can use your browser or <code>telnet</code> or <code>curl</code> or <code>wget</code> to see if the file is where it should be.

<pre><code class="language-javascript">$ curl https://www.smashingmagazine.com/testfile.html
&lt;h1&gt;My test file&lt;/h1&gt;</code></pre>

If that worked, then well done, you have found your website! Remove that test file to clean up after yourself with <code>rm testfile.html</code> and keep going.</p>

### Back up and Restore

The <code>tar</code> and zip commands can be used to back up and restore. If your website is missing, then restore won't help you much unless you have previously backed up. So go back in time and backup your data with one of the commands below. To go back a whole day:

<pre><code class="language-javascript">$ gobackintime 86400
It is now Sat May 10 20:30:57 BST 2013</code></pre>

Just kidding — but it would be nice! The <code>tar</code> command stands for <u>t</u>ape <u>a</u>rchive and comes from the days when data was backed up on magnetic tapes. To create an archive of a directory, pass the <code>cfz</code> options to <code>tar</code> which will <u>c</u>reate a new archive in a <u>f</u>ile and then <u>z</u>ip it in the gzip format.

<pre><code class="language-javascript">$ tar cfz backupfile.tgz /var/www/vhosts/smashingmagazine.com/httpdocs
tar: Removing leading `/' from member names</code></pre>

All Mac and Linux computers support the <code>tar</code> command and most also have <code>zip</code>. To do the same with <code>zip</code>:

<pre><code class="language-javascript">$ zip -r backupfile.zip /directory/to/backup</code></pre>

<strong>To see what an archive contains, run:</strong>

<pre><code class="language-javascript">tar tfz backupfile.tgz
var/www/vhosts/smashingmagazine.com/httpdocs/
var/www/vhosts/smashingmagazine.com/httpdocs/.htaccess...</code></pre>

Or for zip format:

<pre><code class="language-javascript">unzip -l backupfile.zip
Archive:  test.zip
  Length      Date    Time    Name
---------  ---------- -----   ----
        0  2012-05-28 00:33   var/www/vhosts/smashingmagazine.com/httpdocs
      234  2012-05-28 00:33   var/www/vhosts/smashingmagazine.com/httpdocs/.htaccess...</code></pre>

Both <code>tar</code> and <code>zip</code> strip the leading slashes when they backup. So when you restore the files, they will be restored within the current directory. To restore them in the same location they were backed up from, first <code>cd</code> to <code>/</code>.

<pre><code class="language-javascript">$ tar xfzv backupfile.tgz
var/www/vhosts/smashingmagazine.com/httpdocs/...</code></pre>

The "v" above stands for <u>v</u>erbose and causes <code>tar</code> to show what it's doing. <code>zip</code> has a similar option:

<pre><code class="language-javascript">$ unzip -v backupfile.zip
Archive:  backupfile.zip
 Length   Method    Size  Cmpr    Date    Time   CRC-32   Name
--------  ------  ------- ---- ---------- ----- --------  ----
       0  Stored        0   0% 2012-05-28 00:33 00000000  var/www/vhosts/smashingmagazine.com/httpdocs/...</code></pre>

### Website Errors

Let's assume your website hasn't actually disappeared. The next place to look is the error log file.</p>

### Finding the Log File

When using a server management package like Plesk, each website probably has its own log file. You can find it by grepping for the word "log" in the conf file you identified above. The -i means case-insensitive.

<pre><code class="language-javascript">$ grep -i log /var/www/vhosts/smashingmagazine.com/conf/last_httpd.include
CustomLog /var/www/vhosts/smashingmagazine.com/statistics/logs/access_log plesklog
ErrorLog  "/var/www/vhosts/smashingmagazine.com/statistics/logs/error_log"...</code></pre>

There is also a server-wide log where any non-website-specific errors go. You can find this in the main conf file:

<pre><code class="language-javascript">$ grep -i log /etc/apache2/apache2.conf
ErrorLog /var/log/apache2/error.log...</code></pre>

### Htaccess Errors

It is very easy to screw up a website. You can quite readily bring down a very big website by removing a single character from the .htaccess file. Apache uses the file .htaccess to provide last-minute configuration options for a website. It is most often used for URL rewriting rules. They look like this:

<pre><code class="language-javascript">RewriteRule   ^products/.*/([0-9]+)$   products/view.php?id=$1   [L,QSA]</code></pre>

This rule says to rewrite any URL in the form "products/widget-3000/123" to the actual URL "products/view.php?id=123". The <code>L</code> means that this is the <u>l</u>ast rule to be applied and <code>QSA&lt;</code> means that Apache should <u>a</u>ttach any <u>q</u>uery <u>s</u>tring to the new URL. URL rewriting is often used for search engine optimization so that Web managers can get the name of the product into the URL without actually having to create a directory called "widget-3000".

However, make a single typo and your whole website will give a 500 Internal Server Error.

The <code>tail</code> command will display the last 10 lines of a log file. Give it a <code>-1</code> to display the single last line instead. An .htaccess problem will look like this:

<pre><code class="language-javascript">$ tail -1 /var/www/vhosts/smashingmagazine.com/statistics/logs/error_log
[Thu May 06 11:04:00 2013] [alert] [client 81.106.118.59] /var/www/vhosts/smashingmagazine.com/httpdocs/.htaccess: Invalid command 'RewiteRule', perhaps misspelled or defined by a module not included in the server configuration</code></pre>

You can grep for all of these types of errors:

<pre><code class="language-javascript">$ grep alert /var/www/vhosts/smashingmagazine.com/statistics/logs/error_log
[Thu May 06 11:04:00 2013] [alert] [client 81.106.118.59]...</code></pre>

### PHP Parse and Runtime Errors

Many websites use the LAMP combination: Linux, Apache, MySQL and PHP. A common reason for Web pages not showing up is that they contain a PHP error. Fortunately, these are quite easy to discover and pinpoint.

There are two broad classes of PHP errors: parse errors and runtime errors. Parse errors are syntax errors and include leaving off a semicolon or forgetting the $ in front of a variable name. Running errors include undefined functions or referencing objects which don't exist.

Like .htaccess errors, parse errors will cause an HTML response code 500 for Internal Server Error, often with a completely blank HTML page. Runtime errors will give a successful HTML response of 200 and will show as much HTML as they have processed (and flushed) before the error happened. You can use <code>telnet</code> or <code>wget -S</code> or <code>curl -i</code> to get only the headers from a URL. So now, copy and paste your erroneous page into a command:

<pre><code class="language-javascript">$ curl -i https://www.smashingmagazine.com/products/widget-3000/123
HTTP/1.0 500 Internal Server Error
Date: Sun, 12 May 2013 17:44:49 GMT
Server: Apache
Vary: Accept-Encoding
Content-Length: 0
Connection: close
Content-Type: text/html</code></pre>

### PHP Error Settings

To find the exact error, you need to make sure errors are being reported in the log file.

There are several PHP settings which cover errors. <code>display_errors</code> determines if errors are shown to the website visitor or not, and <code>log_errors</code> says whether they will appear in log files. <code>error_reporting</code> specifies the types of errors that are reported: only fatal errors, for example, or warnings and notices as well. All of these can be set in a configuration file, in .htaccess or within the PHP script itself.

You can find out your current settings by running the PHP function <code>phpinfo</code>. Create a PHP file which calls the function and visit it in your browser:

<pre><code class="language-javascript">$ echo "&lt;?php phpinfo()?&gt;" &gt; /var/www/vhosts/smashingmagazine.com/httpdocs/phpinfo.php</code></pre>

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6547f695-553b-4da5-995b-46dd36f15e52/phpinfo.png" alt="phpinfo" /><br>
<em> phpinfo function showing configuration settings.</em>

The two columns show the website and server-wide settings. This shows that <code>display_errors</code> is off, which is good, because it should be off on live websites. It means that no PHP errors will ever be seen by the casual visitor. <code>log_errors</code> on the other hand should be on. It is very handy for debugging PHP issues.

The <strong>error_reporting value is 30719</strong>. This number represents bit flags or bit fields. This is a technique for storing multiple yes/no values in a single number. In PHP there are a series of <a href="https://php.net/manual/en/errorfunc.constants.php">constants representing different types of errors</a>. For example, the constant E_ERROR is for fatal errors and has the value 1; E_WARNING is for warnings and equals 2; E_PARSE is for parsing or syntax errors and has the value 4. These values are all powers of two and can be safely added together. So the number 7 means that all three types of errors should be reported, as E_ERROR + E_WARNING + E_PARSE = 7. A value of 5 will only report E_ERROR + E_PARSE.

In reality, there are 16 types of errors from 1 for E_ERROR to 16384 for E_USER_DEPRECATED. You can type "30719 in binary" into Google and it will give you the binary equivalent: 0b111011111111111. This means that all errors are switched on except the twelfth, which is E_STRICT. This particular setup has also been given a constant E_ALL = E_ERROR + E_WARNING + E_PARSE + etc = 30719. From PHP version 5.4.0, E_ALL is actually 32767 which includes all the errors include E_STRICT.

If your <code>error_reporting</code> setting is 0, then no errors will show up in the log file. You can change this setting in the file php.ini, but then you have to restart Apache to make it have an effect. An easier way to change this setting in Apache is to add a line in a file called .htaccess in your document root: <code>php_value error_reporting 30719</code>.

Or you can do that on the command line, using the double arrow which appends to an existing file or creates the file if it doesn't exist:

<pre><code class="language-javascript">$ echo "php_value error_reporting 30719" &gt;&gt; .htaccess
$ echo "php_value log_errors On" &gt;&gt; .htaccess</code></pre>

Refresh your erroneous Web page. If there is a PHP error in your page it should now show up in the error log. <strong>You can grep the log for all PHP errors:</strong>

<pre><code class="language-javascript">grep PHP /var/www/vhosts/smashingmagazine.com/statistics/logs/error_log
[Sun May 12 18:19:09 2013] [error] [client 81.106.118.59] PHP Notice:  Undefined variable: total in /var/www/vhosts/smashingmagazine.com/httpdocs/products/view.php on line 10...</code></pre>

If you have referenced variables or array indices before assigning them values, you may see thousands of PHP notices like the one above. It happens when you do things like <code>&lt;? $total = $total + 1 ?&gt;</code> without initially setting $total to 0. They are useful for finding potential bugs, but they are not show stoppers. Your website should work anyway.

You may have so many notices and warnings like this that the real errors get lost. You can change your error_reporting to 5 to only show <code>E_ERROR</code> and <code>E_PARSE</code> or you can <code>grep</code> specifically for those types of errors. It is very common to chain <code>grep</code> commands together like this when you want to filter by multiple things. The <code>-e</code> option below tells the second <code>grep</code> to use a regular expression. This command finds all log entries containing "PHP" and either "Parse" or "Fatal".

<pre><code class="language-javascript">$ grep PHP /var/www/vhosts/smashingmagazine.com/statistics/logs/error_log | grep -e "Parse|Fatal"
[Thu Jul 19 12:26:23 2012] [error] [client 81.106.118.59] PHP Fatal error:  Class 'Product' not found in /var/www/vhosts/smashingmagazine.com/httpdocs/library/class.product.php on line 698
[Sun May 12 18:16:21 2013] [error] [client 81.106.118.59] PHP Parse error:  syntax error, unexpected T_STRING in /var/www/vhosts/smashingmagazine.com/httpdocs/products/view.php on line 100...</code></pre>

### Seeing Errors in the Browser

If you are tracing a runtime error rather than a parse error, you can also change the <code>error_reporting</code> setting directly in PHP. And you can quickly turn <code>display_errors</code> on, so you will see the error directly in your browser. This makes debugging quicker, but means everyone else can see the error too. Add this line to the top of your PHP page:

<pre><code class="language-javascript">&lt;? ini_set ('display_errors', 1); error_reporting (E_ERROR | E_WARNING); ?&gt;</code></pre>

These two functions change the two PHP settings. The <code>|</code> in the <code>error_reporting</code> call is a bit OR operator. It effectively does the same as the <code>+</code> above but operates on bits, so is the correct operator to use with bit flags.

Any fatal errors or warnings later in the PHP page will now be shown directly in the browser. This technique won't work for parse errors as none of the page will run if there's a parse error.</p>

### Bit Flags

Using bit flags for <code>error_reporting</code> avoids having 15 separate arguments to the function for each type of error. Bit flags can also be useful in your own code. To use them, you need to define some constants, use the bit OR operator <code>|</code> when calling the function and the bit AND operator &amp; within the function.

Here's a simple PHP example using bit flags to tell a function called showproduct which product properties to display:

<pre><code class="language-javascript">&lt;?
define ('PRODUCT_NAME', 1);
define ('PRODUCT_PRICE', 2);
function showproduct ($product, $flags) {
  if ($flags &amp; PRODUCT_NAME) echo $product['name'];
  if ($flags &amp; PRODUCT_PRICE) echo ': $' . $product['price'];
}
$product = array ('name'=&gt;'Widget 3000', 'price'=&gt;10);
showproduct ($product, PRODUCT_NAME | PRODUCT_PRICE);
?&gt;</code></pre>

This will display "Widget 3000: $10" in the browser.</p>

### Infinite Loops

PHP's error reporting may struggle with one class of error: an infinite loop. A loop may just keep executing until it hits PHP's time limit, which is usually 30 seconds (PHP's <code>max_execution_time setting</code>), causing a fatal error. Or if the loop allocates new variables or calls functions, it may keep going until PHP runs out of workable memory (PHP's <code>memory_limit</code> setting).

It may, however, <strong>cause the Apache child process to crash</strong>, which means nothing will get reported, and you'll just see a blank or partial page. This type of error is increasingly rare, as PHP and Apache are now very mature and can detect and handle runaway problems like this. But if you are about to bang your head against the wall in frustration because none of the above has worked, then give it some consideration. Deep within your code, you may have a function which calls some other function, which calls the original function in an infinite recursion.</p>

### Debuggers

If you've gotten this far, and your page is still not showing up, then you're entering more difficult territory. Your PHP may be executing validly and doing everything it should, but there's <strong>some logical error in your programming</strong>. For quick debugging you can <code>var_dump</code> variables to the browser, perhaps wrapping them in an <code>if</code> statement so that only your IP address sees them:

<pre><code class="language-javascript">&lt;? if ($_SERVER['REMOTE_ADDR'] == '85.106.118.199') var_dump ($product); ?&gt;</code></pre>

This method will narrow down an error but it is ungraceful and error-prone, so you might consider a debugging tool such as Xdebug or FirePHP. They can provide masses of information, and can also run invisibly to the user, saving their output to a log file. Xdebug can be used like this:

<pre><code class="language-javascript">&lt;?
ini_set ('xdebug.collect_params', 1);
xdebug_start_trace ('/tmp/xdebugtrace');
echo "This will get traced.";
xdebug_stop_trace();
?&gt;</code></pre>

This bit of code logs all function calls and arguments to the file <code>/tmp/xdebugtrace.txt</code>. It displays even more information when there is a PHP notice or error. However, the overhead may not be suitable for a live environment, and it needs to be installed on the server, so it's probably not available in most hosting environments.

FirePHP, on the other hand, is a PHP library that interacts with an add-on to Firebug, a plugin for Firefox. You can output debugging information and stack traces from PHP to the Firebug console.</p>

## Security Issues

By this point, you should have some HTML reaching your browser. If it's not what you expect, then there's a chance that your website has been compromised. Don't take it personally (at first). There are many types of hacks and most of them are automated. Someone clever but unscrupulous has written a program which detects vulnerabilities and exploits them. The purpose of the exploit may simply be to send spam, or to use your server as part of a larger attack on a more specific target (a DDoS).</p>

### Server Hacks

Operating systems are very complex pieces of software. They may be built from millions of lines of programming code. They are quite likely to have loopholes where sending the wrong message at just the wrong time will cause some kind of blip which allows someone or something to gain entry. That's why Microsoft, Apple, Ubuntu and others are constantly releasing updates.

Similarly, Apache, nginx, IIS and all the other software on a typical server is complicated. The best thing you can do is keep it up to date with the latest patches. Most good hosts will do this for you.

A hacker can use these flaws to log in to your server and engineer themselves a terminal session. They may initially gain access as an unprivileged user and then try a further hack to become the root user. You should make this as hard as possible by using good passwords, restrictive permissions, and being careful to run software (like Apache) as an unprivileged user.

If someone does gain access, they may leave behind a bit of software which they can later use to take control of your server. This may be detectable by an antivirus scanner or something like the Rootkit Hunter, which looks for anomalies like unexpected hidden files. But there are also a few things you can do if you suspect an intrusion.

The <code>w</code> command <strong>shows <u>w</u>ho is currently logged in to a server and what they are doing</strong>:

<pre><code class="language-javascript">$ w
 20:44:32 up 44 days,  7:51,  2 users,  load average: 0.07, 0.03, 0.05
USER     TTY      FROM              LOGIN@   IDLE   JCPU   PCPU WHAT
root     pts/0    cpc1-brig17-2-0- 17:54    1:02m  0.15s  0.13s -bash
root     pts/1    cpc1-brig17-2-0- 20:44    0.00s  0.02s  0.00s w...</code></pre>

The <code>last</code> command shows who has logged in recently in date order. Pipe it through head to show only the first 10 lines.

<pre><code class="language-javascript">$ last
paul     pts/0        :0.0             Sun May 12 17:21   still logged in
paul     tty7         :0               Sun May 12 17:20   still logged in
reboot   system boot  2.6.32-41-386    Sun May 12 17:18 - 20:48  (03:29)
fred     tty7         :0               Sat May 11 10:10 - down   (01:12)...</code></pre>

It tells you who has logged in and for how long, plus any terminal session they have open. down means until the server shut down. Look for unexpected entries and consult your host or a security expert if you are in doubt.</p>

### PHP Hacks

More common are hackers who gain entry though vulnerabilities in PHP scripts, especially popular content management systems like WordPress. Anybody can write a plugin for WordPress and, if it's useful, people will install it. When writing a plugin, most developers think primarily about the functionality and little about security. And because WordPress allows file uploading, <strong>hackers who find vulnerabilities can use them to upload their own PHP scripts</strong> and later take control of a computer.

These PHP scripts can use the PHP <code>mail</code> function to send out spam on demand, but they can also try to execute commands in much the same way as you can via a terminal session. PHP can execute commands with its <code>exec</code> or <code>system</code> functions. If you do not need to use these functions, <strong>it is advisable to disable them</strong>. You can do this by adding the <code>disable_functions</code> directive to your server's php.ini file (or php5.ini for PHP 5) or to the file php.ini within your document root. If you search for "php disable functions" in Google, you will find a whole list of functions which should be disabled in this way:

<pre><code class="language-javascript">disable_functions=fpassthru,crack_check,crack_close...</code></pre>

A quick check you can make for this type of hack is to look for all PHP files modified recently and make sure there are no anomalies. The <code>-mtime -1</code> option tells <code>find</code> to only consider files modified within the last day. There's also <code>-mmin</code> for minutes. This command searches all websites within /var/www/vhosts for recently modified files ending in "php" or "inc":

<pre><code class="language-javascript">$ find /var/www/vhosts -mtime -1 ( -name *php -o -name *inc ) -printf "%t %h/%fn"
Sun May 12 21:20:17.0000000000 2013 /var/www/vhosts/smashingmagazine.com/httpdocs/products/view.php</code></pre>

PHP hacks are difficult to detect because they are designed to not stick out. One method hackers use is to gzip their PHP and then encode it as base64. In that case, you may have a PHP file on your system with something like this in it:

<pre><code class="language-javascript">eval(gzinflate(base64_decode('HJ3HkqNQEkU/ZzqCBd4t8V4YAQI2E3jvPV8...</code></pre>

Another method is to <strong>encode text within variables</strong> and then combine them and evaluate them:

<pre><code class="language-javascript">$unywlbxc = " uwzsebpgi840hk2a jf";
$hivjytmne = "  jqs9m4y 1znp0  ";
eval ( "m"."i". "croti"...</code></pre>

Both these methods use the PHP <code>eval</code> function, so you can use <code>grep</code> to look for <code>eval</code>. Using a regular expression with <code>bevalb</code> means that the word "eval" must have a word boundary before and after it, which prevents it being found in the middle of words. You can combine this with the <code>find</code> command above and pipe through <code>less</code> for easy reading:

<pre><code class="language-javascript">$ find /var/www/vhosts -mtime -1 ( -name *php -o -name *inc ) | sed 's/ /\ /g' | xargs grep -H -e "bevalb" | less
/var/www/vhosts/config.php:eval(gzinflate(base64_decode('HJ3HkqNQE...</code></pre>

If you do find this type of hack in your website, try to discover how they got in before completely removing all the tainted files.</p>

### Access Logs

Along with error logs, Apache also keeps access logs. You can browse these for suspicious activity. For example, if you found a PHP hack inside an innocuous looking file called test.php, you can look for all activity related to that file. The access log usually sits alongside the error log and is specified with the <code>CustomLog</code> directive in Apache configuration files. It contains the IP address, date and file requested. Search through it with <code>grep</code>:

<pre><code class="language-javascript">$ grep -e "(GET|POST) /test.php" /var/www/vhosts/smashingmagazine.com/statistics/logs/error_log
70.1.5.12 - - [12/May/2013:20:10:49 +0100] "GET /test.php HTTP/1.1" 200 1707 "-" "Mozilla/5.0 (X11; Ubuntu; Linux i686;...</code></pre>

This looks for GET and POST requests for the file test.php. It provides you with an IP address, so you can now look for all other access by this address, and also look for a specific date:

<pre><code class="language-javascript">$ grep 70.1.5.12 /var/www/vhosts/smashingmagazine.com/statistics/logs/error_log | grep "12/May/2013"
70.1.5.12 - - [12/May/2013:20:10:49 +0100] "GET /products/view.php?something HTTP/1.1" 200 1707 "-"...
70.1.5.12 - - [12/May/2013:20:10:49 +0100] "GET /test.php HTTP/1.1" 200 1707 "-" "Mozilla/5.0 (X11; Ubuntu; Linux i686;...</code></pre>

This kind of debugging can be very useful for normal website errors too. If you have a feedback form on your website, add the user's IP address to the message. If someone reports an error, you can later look through the logs to see what they have been up to. This is far better than relying on vague second-hand information about reported problems.

It can also be useful for detecting SQL injection attacks, whereby hackers try to extract details from your database by fooling your database retrieval functions. This often involves a lot of trial and error. You could send yourself an email whenever a database query goes wrong and include the user's IP address. You can then cross-reference with the logs to see what else they have tried.</p>

## Last Resorts

William Edward Hickson is credited with popularizing the saying:
<blockquote>"If at first you don't succeed, try, try, try again."</blockquote>

Hickson was a British educational writer living in early Victorian times. His advice is not appropriate for the modern Web developer, lying in bed on a Saturday morning, drowning in frustration, staring at a blank Web page, preparing to chuck an expensive laptop against a brick wall.

You've now been through all the advice above. You've checked that the world hasn't ended, verified your broadband box, tested the Internet and reached your server. You've looked for hardware problems and software problems, and delved into the PHP code. But somehow or other, your Widget 3000 is still not there. The next thing to do is...</p>

### Have Breakfast

Get out of bed and <strong>take your mind off the problem for a little while</strong>. Have some toast, a bowl of cereal, something to drink. Maybe even indulge in a shower. Try that new lavender and citrus shampoo you bought by mistake. While you're doing all this, your subconscious is busily working on the website issue, and may unexpectedly pop a solution into your thoughts. If so, give it a try. If not…

### Ask for Help

Check the level of support that you are entitled to by your hosting company. If you are paying $10 per month, it's probably not much. You may be able to get them to cast a vague glance in your direction within the next 72 hours. If it's substantially more, they may log in and have a look within the next few minutes. They should be able to help with hardware or software issues. They won't help with Web programming issues. Alternatively, ring a colleague or freelancer. If you are still stuck…

### Prepare

…to release some nervous energy. Find one of those squidgy balls that you can squeeze mercilessly in your hands, or a couple pencils to use as drumsticks, or a pack of cigarettes and a pot full of coffee. And then try the last resort to any computing problem…

### Reboot

When your laptop or desktop goes wrong, a common solution is to reboot it. You can try the same trick on your Web server. This is a quite risky. Firstly, it may not solve the problem. If it's a PHP error, then nothing will change. If, however, your issue is caused by some obscure piece of software becoming unresponsive, then it may well help, though it may not fix the problem permanently. The same thing may happen next week.

Secondly, if the reboot fails then you will be really stuck. If the server shuts down but fails to start back up again, then someone may have to go and press the power button on the physical machine. That someone is an employee of your hosting company, and they may be enjoying their breakfast too, in a nice comfortable office somewhere. They may have left their jumper at home. They may not want to enter the air-conditioned bunker where all the servers are kept. You will be thoroughly dependent on their response time.

Given all the risks, the command is:

<pre><code class="language-javascript">$ sudo /sbin/reboot
Broadcast message from admin@thisserver.com (/dev/pts/1) at 13:21 ...
The system is going down for reboot now.</code></pre>

The <code>reboot</code> command is really just a wrapper for <code>/sbin/shutdown -r now</code>. It causes the server to shut down and then restart. That may take a few minutes. Soon after issuing the command above your SSH session will come to an abrupt end. You will then be left for a few nervous minutes wondering if it will come back up again. Use the tools you prepared above.

While you are waiting, you can <strong>issue a ping to see if and when your server comes back</strong>. On Windows use <code>ping -t</code> for an indefinite <code>ping</code>:

<pre><code class="language-javascript">$ ping www.smashingmagazine.com
PING www.smashingmagazine.com (80.72.139.101) 56(84) bytes of data.
Request timeout for icmp_seq 0
Request timeout for icmp_seq 0
Request timeout for icmp_seq 0...
64 bytes from www.smashingmagazine.com (80.72.139.101): icmp_seq=1 ttl=52 time=39.4 ms
64 bytes from www.smashingmagazine.com (80.72.139.101): icmp_seq=1 ttl=52 time=32.4 ms...</code></pre>

You can breathe a sigh of relief when ping finally responds. Wait a couple more minutes and you'll be able to use <code>ssh</code> again and then try to view the Widget 3000 in your Web browser.</p>

## Conclusion

This has been an epic journey, from the end of the world to a single misplaced character in a file. Hopefully, it will help you through the initial few minutes of panic when you wake up one morning and the beautiful product page you created last night is gone.

Some of the reasons and solutions above are very rare. The most likely cause is simply a slight malfunction in your broadband box. Running out of disk space or getting hacked are the only other things that are in any way likely to happen in the middle of the night when nobody else is working on the website. But throw in other developers, server administrators and enthusiastic clients — and anything is possible. Good luck!

### Footnotes

1. Oxford Dictionary of Quotations (3rd edition), Oxford University Press, 1979

<em>Paul Tero's chapter has been reviewed by <a href="https://twitter.com/coderholic">Ben Dowling</a> and <a href="https://twitter.com/chikuyonok">Sergey Chikuyonok</a>.</em>

(og) (il) (vf) (ea) (cm)

