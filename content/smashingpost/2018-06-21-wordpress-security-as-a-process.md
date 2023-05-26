---
title: 'WordPress Security As A Process'
slug: wordpress-security-as-a-process
author: luc-princen
image: >-
  //archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/66c98514-358e-4351-8e87-d98b095340b8/wordpress-security-as-a-proces-800w.png
date: 2018-06-21T12:30:13+02:00
summary: >-
  Last year, WordPress was responsible for 83% of infected content management sites. Make sure you're not contributing to those infections and learn how to securely manage WordPress.
description: >-
  Last year, WordPress was responsible for 83% of infected content management sites. Make sure you're not contributing to those infections and learn how to securely manage WordPress.
categories:
  - Security
  - WordPress
disable_ads: true
disable_panels: true
canonical: 'https://sucuri.net/guides/wordpress-security'
---
<p>(<em>This article is kindly sponsored by Sucuri</em>.) WordPress security doesn’t have a good reputation. More than 70% of all WordPress sites carry some kind of vulnerability according to research done on <a href="https://www.wpwhitesecurity.com/wordpress-security-news-updates/statistics-70-percent-wordpress-installations-vulnerable/">+40.000 WordPress sites by Alexa</a>. If you develop WordPress themes or plugins &mdash; or use WordPress for your websites &mdash; that number should scare you.</p>

<p>There’s a lot you can do to make sure you’re not part of the 70%, but it takes more work than just installing a plugin or escaping a string. A lot of advice in this article comes from <a href="https://sucuri.net/guides/wordpress-security">Sucuri’s guide on WordPress security</a> and years of personal experience.</p>

## Is WordPress Insecure?

<p>WordPress has the largest market share among content management systems and a 30% market share among the most popular 10 million sites on the web. That kind of success makes it a big target for hacks. WordPress isn’t less secure than other content management systems &mdash; it’s just more successful.</p>

<p>Vulnerabilities in WordPress core are responsible for less than 10% of all WordPress hacks. Most of those are from out-of-date WordPress installs. The amount of hacks that happen on actual security holes in up-to-date versions (also known as zero-day exploits) in WordPress core account for a tiny percentage of all hacks.</p>

<p>The rest of the infected sites were caused by plugins, themes, hosting, and users. And you, as a WordPress website developer, have control over all of those. If this seems like a big hassle to you, then I can recommend <a href="https://sucuri.net/custom/agency/">Sucuri’s agency plan</a>. Otherwise, let’s find out how to deal with WordPress security ourselves!
</p>

## Who’s Attacking You And Why?

<p>Let’s bust a myth first: A small WordPress website is still an attractive target for hackers. Attacks on a personal basis are very rare. Most hacked WordPress websites are compromised automatically by either a bot or a botnet.</p>

<p>Bots are computer programs that constantly search for websites to hack. They don’t care who you are; they just look for a weakness in your defences. A botnet combines the computing power of many bots to tackle bigger tasks.</p>

<p>Hackers are primarily looking for a way into your server so that they can use your server’s computing power and turn it loose on some other goal or target. Hackers want your server for the following reasons.</p>

### Sending Spam

<p>Spam accounts for about 60% of all email, and it has to be sent from somewhere. Many hackers want to gain entry to your server through a faulty plugin or an ancient version of WordPress core so that they can turn your server into a spamming machine.</p>

### Attacking Other Websites

<p>Distributed denial-of-service attacks use many computers to flood a website with so much traffic that they can’t keep up. These attacks are very difficult to mitigate, especially when they are done right. Hackers who break into your server can add it to a pool of servers to attack websites.</p>

### Stealing Resources

<p>Mining cryptocurrency is very popular now, but it takes a lot of computing power. Hackers who don’t want to spend a lot of money on a server farm will break into unprotected WordPress websites and gain access to servers or to your websites’ visitors and steal computing power.</p>

### Bumping SEO Scores

<p>A particularly popular hack for WordPress is to gain access to its database and add a bunch of (hidden) text underneath each post, linking to another website. It’s a really quick way to bump one’s SEO score, although Google is getting more vigilant about this behavior, and blacklistings are increasing.<p>

### Stealing Data

<p>Data is valuable, especially when it’s linked to user profiles and e-commerce information. Getting this data and selling it can make an attacker a handsome profit.</p>

## Why Does Security Matter?

<p>Apart from not giving criminals the satisfaction, there are plenty of reasons why your website should be secure by default. Having cleaned and dealt with plenty of WordPress hacks myself, I can surely say that they never occur at a convenient time. Cleaning up can take hours and will cost either you or your client money.</p>

<p>To get a hacked WordPress website up and running again, you’ll need to remove and replace every bit of third-party code (including WordPress core); comb through your own code line by line and all other folders on the server to make sure they are still clean; check whether unauthorized users have gained access; and replace all passwords in WordPress, on your server and on your database.</p>

<p>Plenty of services can clean up a WordPress website for you, but prevention is so much better in the long run.</p>

<p>Apart from the cost of cleaning up, hacks can also cost you a lot in missed sales or leads. Hacks move you lower in search rankings, resulting in fewer visitors and fewer conversions.</p>

<p>More than the financial cost, getting hacked hurts your reputation. Visitors come to your website because they trust you. Getting hacked damages your reputation, and that takes a long time to repair.</p>

<p>There’s also a real possibility of legal issues, especially if you have customers in the EU, where <a href="https://en.wikipedia.org/wiki/General_Data_Protection_Regulation">GDPR legislation</a> will go into effect in the summer of 2018. That new legislation includes a hefty fine for data breaches that aren’t handled properly.</p>

<p>Money, reputation and legal problems: Bad security can cost you a lot. Investing some time in getting your website, code and team set up with a mindset of security will definitely pay off.</p>

<p>Let’s find out how we can prevent all of this nastiness.</p>

## The CIA Triad

<p>The CIA triad is a basic framework for every digital security project. It stands for confidentiality, integrity and availability. CIA is a set of rules that limits information access to the right parties, makes sure the information is trustworthy and accurate, and guarantees reliable access to that information.</p>

<p>For WordPress, the CIA framework boils down to the following.</p>

### Confidentiality

<p>Make sure logged-in users have the right roles assigned and that their capabilities are kept in check. Only give users the minimum access they need, and make sure that administrator information doesn’t leak out to the wrong party. You can do so by hardening WordPress’ admin area and being careful with usernames and credentials.</p>

### Integrity

<p>Show accurate information on your website, and make sure that user interactions on your website happen correctly.</p>

<p>When accepting requests on both the front and back end, always check that the intent matches the actual action. When data is posted, always filter the data in your code for malicious content by using sanitization and escapes. Make sure spam gets removed by using a spam protection service such as Akismet.</p>

### Availability

<p>Mak sure your WordPress, plugins and themes are up to date and hosted on a reliable (preferably managed) WordPress host. Daily automated backups also help to ensure that your website stays available to the public.</p>

<p>All three elements lean on each other for support. Code integrity will not work on its own if a user’s confidential password is easily stolen or guessed. All aspects are important to a solid and secure platform.</p>

<p>Security is a lot of hard work. Apart from the work that can be done in code, there’s a huge human element to this framework. Security is a constant process; it can’t be solved by a single plugin.</p>

## Part 1: Integrity &mdash; Trust Nothing

<p>Verify the intent of user actions and the integrity of the data you’re handling. Throw your inner hippie out the door. Nothing can be trusted online, so double-check everything you do for possible malicious intent.</p>

### Data Validation and Sanitization

<p>WordPress is excellent at handling data. It makes sure that every interaction is validated and that every bit of data is sanitized, but that’s only in WordPress core. If you’re building your own plugin or theme or even just checking a piece of third-party code, knowing how to do this is essential.</p>

<div class="break-out">

<pre><code class="language-php">//Cast our variable to a string, and sanitize it.
update_post_meta( $post->ID,  ‘some-meta’,  sanitize_text_field( (string)$_POST[‘some-meta’] ) );

//Make sure our variable is an absolute integer.
update_post_meta( $post->ID, ‘some-int’, absint( $_POST[‘int’] ) );
</code></pre></div>

<p>In this example, we’ve added two pieces of data to a WordPress post using <a href="https://codex.wordpress.org/Function_Reference/update_post_meta">update_post_meta</a>. The first is a string; so, we cast it as a string in PHP and strip unwanted characters and tags with <code>sanitize_text_field</code>, one of WordPress’ <a href="https://developer.wordpress.org/themes/theme-security/data-sanitization-escaping/">many sanitization functions</a>.</p>

<p>We’ve also added an integer to that post and used <a href="https://codex.wordpress.org/Function_Reference/absint">absint</a> to make sure this is an absolute (and non-negative) integer.</p>

<p>Using core WordPress functions such as <code>update_post_meta</code> is a better idea than using the WordPress database directly. This is because WordPress checks everything that needs to be stored in the database for so-called SQL injections. A SQL injection attack runs malicious SQL code through the forms on your website. This code manipulates the database to, for instance, destroy everything, leak user data or create false administrator accounts.</p>

<p>If you ever need to work with a custom table or perform a complicated query in WordPress, use the native <a href="https://codex.wordpress.org/Class_Reference/wpdb">WPDB</a> class, and use the <code>prepare</code> function on all your queries to prevent SQL injection attacks:</p>

<div class="break-out">

<pre><code class="language-php">$tableName = $wpdb->prefix . “my_table”;
$sql = $wpdb->prepare( “SELECT * FROM %s”, $tableName );
$results = $wpdb->get_results( $sql );
</code></pre></div>

<p><a href="https://developer.wordpress.org/reference/classes/wpdb/prepare/">$wpdb->prepare</a> goes through every variable to make sure there’s no chance of a SQL injection attack.</p>

### Escaping

<p>Escaping output is just as important as sanitizing input. Validating data before you save it is important, but you can’t be 100% sure it’s still safe. Trust nothing. WordPress uses a lot of filters to enable plugins and themes to change data on the fly, so there’s a good chance that your data will get parsed through other plugins as well. Escaping data before adding it to your theme or plugin is a smart thing to do.</p>

<p>Escaping is mainly meant to prevent <a href="https://en.wikipedia.org/wiki/Cross-site_scripting">cross-site scripting</a> (XSS) attacks. XSS attacks inject malicious code into the front end of your website. An added bonus of escaping data is that you can be sure that your markup is still valid afterwards.</p>

<p>WordPress has <a href="https://codex.wordpress.org/Validating_Sanitizing_and_Escaping_User_Data">many escaping functions</a>. Here’s a simple example:</p>

<div class="break-out">

<pre><code class="language-php">&lt;a href=“&lt;?php echo esc_url( $url );?>” title=“&lt;?php echo esc_attr( $title );?>”>&lt;?php echo esc_html( $title );?>&lt;/a>
</code></pre></div>

<p>Escape as late as possible. This ensures that you have the final say over your data.</p>

### Securing Requests

<p>WordPress admin requests are already pretty secure if you have SSL enabled and if you have a decent host, but some vulnerabilities still exist. You need to check a user’s intent and validate that the incoming request is something that was done by the actual logged-in user.</p>

<p>WordPress <a href="https://codex.wordpress.org/WordPress_Nonces">validates intent with nonces.</a>. A nonce (or “number used only once”) isn’t really an accurate description of this API in WordPress. It doesn’t only use numbers, and it is much more like a cross-site request forgery (CSRF) token that you’ll find in every modern web framework. These tokens make sure hackers can’t repeat requests. It’s a lot more than just a nonce, but WordPress likes backwards-compatibility, so the name stuck.</p>

<p>Nonces are sent along with every vulnerable request that a user makes. They’re attached to URLs and forms, and they always need to be checked on the receiving end before performing the request. You can add a nonce to a form or a URL. Here’s an example used in a form:</p>

<pre><code class="language-php">&lt;form method= “post”&gt;
&lt;!-- Add a nonce field: --&gt;
&lt;?php wp_nonce_field( ‘post_custom_form’ );?&gt;

&lt;!-- other fields: →
...
&lt;/form&gt;
</code></pre>

<p>In this case, we’re just using the simple helper function <code>wp_nonce_field()</code>, which generates two hidden fields for us that will look like this:</p>

<div class="break-out">

<pre><code class="language-php">&lt;input type="hidden" id="_wpnonce" name="_wpnonce" value="e558d2674e" />

&lt;input type="hidden" name="_wp_http_referer" value="/wp-admin/post.php?post=2&action=edit" />
</code></pre></div>

<p>The first field checks intent by using a generated code with the <code>'post_custom_form'</code> string that we’ve passed to the function. The second field adds a referrer to validate whether the request was made from within the WordPress installation.</p>

<p>Before processing your task on the other end of the form or URL, you would check the nonce and its validity with <code>wp_verify_nonce</code>:</p>

<div class="break-out">

<pre><code class="language-php">if( wp_verify_nonce( $_REQUEST[‘_wpnonce’], ‘post_custom_form’ ) == false ){
    wp_die( “Nonce isn\’t valid” );
}
</code></pre></div>

<p>Here, we’re checking the nonce with our action name, and if it doesn’t match, we stop processing the form.</p>

### Third-Party Code

<p>Third-party plugins and themes are a hotbed for hacks. They’re also the toughest nut to crack when ensuring the security of your website.</p>

<p><strong>Most WordPress hacks are caused by plugins, themes, and out-of-date copies of WordPress</strong>. No piece of software is 100% secure, but a lot of plugins and themes out there either haven’t been updated in a while by their developers or weren’t secure to begin with.</p>

<p>Less code means less to hack. So, before installing yet another plugin, ask yourself whether you really need it. Is there another way to solve this problem?</p>

<p>If you’re sure you need a plugin or theme, then judge it carefully. Look at the rating, the “last updated” date and the required PHP version when browsing through WordPress’ plugin directory. If you’ve found what you’re looking for and everything seems to work, search for any mentions of it on a trusted security blog, such as Sucuri or WordFence.</p>

<p>Another option is to scan the code and make sure it contains proper nonces, sanitation and escaping; these are usually signs of well-written and secure code. You don’t have to know PHP or do a complete code review. A simple and quick way to verify proper use of WordPress security functions is to search the plugin’s code for these strings:</p>

<ul>
<li><code>esc_attr</code></li>
<li><code>esc_html</code></li>
<li><code>wp_nonce_field</code></li>
<li><code>wp_nonce_url</code></li>
<li><code>sanitize_text_field</code></li>
<li><code>$wpdb->prepare</code></li>
</ul>

<p>A plugin could still be secure if it doesn’t include all of these strings, but if none or a low number of these strings are found, that is a red flag. If you do find a vulnerability, please share it with the creator in private, and allow them time to fix it.</p>

<p>Keeping track of vulnerabilities in the WordPress plugin space is getting easier with initiatives such as <a href="https://wpvulndb.com/">wpvulndb</a>.</p>

<p><strong>Note:</strong> Some themes out there bundle versions of plugins with their code. This is a symptom of WordPress not having great out-of-the-box dependency management, but it’s also a sign of a very poorly written theme. Always avoid these themes because they include code bases that can’t be updated.</p>

<p>Themes and plugins rarely contain code written by only one developer. <strong>Composer and NPM</strong> have made it so much easier to depend on other libraries that it’s become a popular attack vector. If you’re downloading a cut-and-dry WordPress theme or plugin, this really isn’t a concern, but if you’re working with tools that use Composer or NPM, then it doesn’t hurt to check their dependencies. You can check Composer dependencies with a free command-line interface (CLI) tool by <a href="https://github.com/sensiolabs/security-checker">SensioLabs</a>. A service such as <a href="https://snyk.io/">Snyk</a> (which you can use for free but which also has premium options) enables you to check every dependency in your project.</p>

## Part 2: Availability: Keep It Simple

<p>Your main goal is to keep your website online without interruptions. Even with top-notch security, you can still get in trouble. When that happens, a great backup will save you a big headache.</p>

### Updates

<p>Open-source can’t exist without updates. Most attacks on WordPress websites happen on outdated versions of either the core software or plugins. Security updates to WordPress’ core are now dealt with automatically (unless you’ve disabled this, you monster!), but security updates in plugins are a different story.</p>

<p>Updating is normally safe with popular, trusted plugins, but all plugins should be tested before they go live on your website. Tools such as WP CLI make updating everything much easier. WordPress lead developer Mark Jaquith had an excellent blog <a href="https://markjaquith.wordpress.com/2018/02/12/updating-plugins-using-git-and-wp-cli/">post on updating all plugins</a> automatically yet gradually, so that you can filter out possible errors.</p>

### Users, Roles and Capabilities

<p>“Availability” in the CIA triad has to do with getting information in the right hands. Our main priority with this is limiting the capabilities of your back-end users. Don’t give everyone an admin account.</p>

<p>The admin account in WordPress is unusually powerful. There’s even an option in vanilla WordPress to alter your complete code base from within the WordPress admin account. (If this is new to you and you haven’t disabled this, <a href="https://www.wpbeginner.com/wp-tutorials/how-to-disable-theme-and-plugin-editors-from-wordpress-admin-panel/">please do</a>.)</p>

<p>The roles and capabilities system in WordPress is powerful and is very easy to alter in code. I create a lot of new roles when working with WordPress. The main benefit of this is that you get full control over which parts of the system various users get to access, but another huge benefit is that it prevents third-party code from altering the standard capabilities of WordPress core.</p>

### Email

<p>WordPress usually handles email via the server it’s on, but this makes all of your email completely dependent on the server it’s running on. Prevent your emails from getting intercepted and seen as spam by using an SMTP service. A lot of plugin options are available to make sure that all of your mail is sent over a secure SMTP connection.</p>

<p>You will, however, need access to the domain name’s DNS settings to add a Sender Policy Framework (SPF) record. All good SMTP services will provide the exact record that needs to be added. An SPF record ensures that your SMTP service is authorized by the domain to send email in its name.</p>

### Monitoring

<p>Monitoring your website online is a 24/7 task that can be fully automated. In the case of WordPress, we’re interested in uptime and file integrity.</p>

<p>Monitoring <strong>uptime</strong> is usually something a good host will do for you. Tools such as Uptime Robot add even more security. Your first 50 websites are completely free.</p>

<p>Regarding <strong>file integrity</strong>, if a hacker gains access to your server they can change your code.</p>

<p>In this case, plugins are the answer to your problem. Sucuri has a great auditing plugin. It checks all files in your installation against a vast database of known malicious code. It also checks whether WordPress core is still 100% WordPress core, and it gives you a heads up if there’s been a breach, so that you can fix it as soon as possible.</p>

### Backups

<p>The ultimate fail-safe of every security process is automated backups. Most good hosts will do this for you, but there are other good options if your host doesn’t offer backups. Automattic makes one named <a href="https://vaultpress.com/">VaultPress</a>, and tools such as <a href="https://ithemes.com/purchase/backupbuddy/">BackupBuddy</a> back up to a Dropbox account or an Amazon S3 bucket.</p>

<p>Most of the reliable services in the WordPress backup space are either premium services or premium plugins. Depending on whether you need to fully control your data, you might prefer a plugin that comes with a cloud host, instead of a service. Either one is worth every penny, though.</p>

### Hosting

<p>WordPress isn’t the only piece of software running on your server. Plenty of attack vectors are open when you’re on crappy hosting. In fact, bad hosting is the main reason why WordPress still supports outdated versions of PHP. At time of writing, WordPress’ own statistics page reports that 32.5% of all WordPress installations are running on PHP versions that do not receive security updates anymore.</p>

{{< rimg breakout="true" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/969f2505-9358-48cf-a617-2f487a4318b9/wordpress-security-as-a-proces.png" sizes="100vw" caption="PHP versions in WordPress as of 10 May 2018. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/969f2505-9358-48cf-a617-2f487a4318b9/wordpress-security-as-a-proces.png'>View large version</a>)" alt="" >}}

<p>Note the almost 60% of installations running on PHP 5.6 and 7.0, which will receive security patches only until the end of this year.</p>

<p>Hosting is important not only for keeping your server’s software up to date, though. A good host will offer many more services, such as automated daily backups, automated updates, file-integrity monitoring and email security. There’s a big difference between managed WordPress hosts and hosts that give you an online folder with database access.</p>

<p>The best advice is to find a decent managed WordPress host. They cost a little more, but they provide a great backbone for your WordPress website.</p>

## Part 3: Confidentiality

<p>If you’ve made sure that your code base is as secure as it can be and you’re on a great WordPress host, surrounded by malware scanners and backups, then you’re still going to experience security problems, because people are the worst… at Internet security.</p>

<p>Confidentiality is about educating yourself, your client and the users of the website.</p>

### Confidential Data

<p>You might not know it, but your plugins and themes are probably showing valuable confidential data. If, for instance, you have <code>WP_DEBUG</code> set to <code>true</code>, then you’re showing every hacker your website’s root path on the server. Debugging data should have no place in your production website.</p>

<p>Another valuable data source are comments and author pages. These are filled with usernames and even email addresses. A hacker could use these in combination with a weak password to get into your website. Be wary of what you show the outside world.</p>

<p>Also, double-check that you’ve put <code>wp-config.php</code> in your <code>.gitignore</code>.</p>

### Don’t Code Alone

<p>A way to prevent a lot of mistakes from sneaking into your code base is to practice pair programming. If you’re by yourself, this a lot harder, but many online communities are available that are willing to do quick code audits. WordPress for instance, uses Slack to communicate everything about the development of its platform. You will find a lot of people on there who are willing to help. Slower but better alternatives are the WordPress forums, StackOverflow and GitHub Issues, where your questions (and their answers!) are saved so that other people can benefit from them.</p>

<p>Asking for input can be tough, but people love showing their expertise, and WordPress in general has a very open and welcoming community. The point is that if you never ask for input on the quality of your code, then you will have no idea whether your code is secure.</p>

### Logins and Passwords

<p>Your clients will need to log into WordPress to manage their content. WordPress core does what it can to prevent weak passwords from getting through, but this usually isn’t enough.</p>

<p>I’d recommend adding a plugin for two-factor authentication to your website, along with a limit on login attempts. Even better, do away with passwords entirely and work with magic links.</p>

### Trust But Verify

<p>So far in this article, we haven’t talked about social engineering at all. It’s a form of hacking that’s gaining momentum, but it generally isn’t used to hack into WordPress websites. It is, however, an excellent way to set up the culture around your website with security in mind. That’s because the best defense against social engineering is “Trust but verify”.</p>

<p>Whenever a client, a user or your boss asks for something related to security, the best way to deal with it is to trust but first to verify whether what they are saying is true.</p>

<p>A client can claim they need administrator access to WordPress, but your job is to verify whether this is true. Do they actually need access, or are they missing just a single capability in their role? Is there a way to solve this problem without adding possibly new attack vectors?</p>

<p>“Trust but verify” is a simple yet effective mantra when it comes to security questions, and it can really help get people up to speed.</p>

## Conclusion

<p>Is WordPress insecure? No, it’s not. WordPress core is constantly being updated and fixed, and most reported WordPress hacks aren’t from WordPress itself. Is the culture surrounding WordPress insecure? You betcha!</p>

<p>But by having security in mind with every line of code you write, every user you add, every plugin you enable and every hosting bill you pay, you can at least ensure that you’re running a secure website that keeps your reputation intact and your data safe.</p>

{{< signature "ms, ra, yk, il, al" >}}
