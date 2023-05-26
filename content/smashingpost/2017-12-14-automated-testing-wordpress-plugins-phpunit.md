---
title: An Introduction To Automated Testing Of WordPress Plugins With PHPUnit
slug: automated-testing-wordpress-plugins-phpunit
author: agbonghamacollins
image: >-
  //archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ab04b6d1-8532-438b-b0a0-695b157ec43b/1-phpunit-command-800w-opt.png
date: 2017-12-14T14:38:50.000Z
summary: >-
  You really don't want to spend hours manually testing every part of your
  WordPress plugin to ensure nothing is broken every time you deploy a new
  version — do you? In this tutorial, you will learn how to test efficiently
  with automated testing.
description: >-
  You really don't want to spend hours manually testing every part of your
  WordPress plugin to ensure nothing is broken every time you deploy a new
  version — do you? In this tutorial, you will learn how to test efficiently
  with automated testing.
categories:
  - WordPress
  - Plugins
  - PHP
  - Testing
---
<p>WordPress is a popular content management system for building websites because it is easy to get started with and a ton of themes and plugins are available to extend its feature set. The main reason WordPress has a lot of plugins and themes is because it's easy for developers of any level to start building one. Most of its developers are not experienced, and they do not write tests for their work, perhaps because of the following reasons:</p>

<ul>
<li>There aren't many discussions going on about unit testing, so they might not know that testing is even possible.</li>
<li>They do not believe in the value of writing tests for their code, or they think it will slow them down.</li>
<li>They believe that testing to see whether their plugin or theme works in the browser is enough.</li>
</ul>

<p>In this tutorial, we will learn what automated testing is and its importance, get to know PHPUnit and WP-CLI, learn how to write a test and, finally, set up continuous automated testing with Travis CI.</p>

<p>We are opting to use Travis CI because it offers seamless integration with GitHub; you don't have to go to your repository and set up any connection between them. And it is free for public repositories. Unlike its competitors, such as Semaphore CI, GitLab CI and CircleCI, Travis CI does not offer a free private repository plan. However, none of its competitors offer seamless integration with GitHub as it does.</p>

## What Is Automated Testing?

<p><a href="https://en.wikipedia.org/wiki/Software_testing">According to Wikipedia</a>, automated testing, or test automation, is the use of special software (separate from the software being tested) to control the execution of tests and the comparison of actual outcomes with predicted outcomes. Test automation can automate some repetitive but necessary tasks in a formalized testing process already in place, or perform additional testing that would be difficult to do manually.</p>

{{% feature-panel %}}

<p>There are several types of testing. Of all, unit testing is the most popular. Unit tests verify that a block of code, function or class method does what it is intended to do. We'll be doing unit testing in this tutorial.</p>

<p>Automated testing helps to detect bugs so that they don't make their way to production. No doubt, a plugin coded and tested would take longer to complete than one that is not tested. However, the resulting plugin would contain fewer or no bugs.</p>

<p>Let’s see a simple real-world example of how unit tests are invaluable and what we can use them for.</p>

<p>My WordPress <a href="https://mailoptin.io/">lead-generation plugin</a> has an <code>OptinThemesRepository</code> class, with an <code>add()</code> method for adding new opt-in form templates, and a <code>get()</code> method for the retrieval of an opt-in form template.</p>

<p>To ensure both <code>add()</code> and <code>get()</code> work as intended now and in the future, I wrote the test below.</p>

<pre><code class="language-php">public function testAddGetMethods()
{
	$kick_optin_form = array(
		'name' =&gt; 'Kick',
		'optin_class' =&gt; 'kick',
		'optin_type' =&gt; 'kick',
		'screenshot' =&gt; MAILOPTIN_ASSETS_URL . 'img/kick.png'
	);

	// add kick optin theme
	OptinThemesRepository::add($kick_optin_form);

	$result = OptinThemesRepository::get('kick');

	$this-&gt;assertEquals($kick_optin_form, $result);
}</code></pre>

<p>If, in future, this test started to fail, I would know there is a problem and would know the exact function, class method or spot in my plugin where it is occurring.</p>

## Benefits Of Automated Testing

<p>Now that we know what automated testing is, let's see more benefits.</p>

### Early Bug Detection

<p>While developing software, you can easily find bugs with automated testing tools. This can save a lot of time and effort in tracking down bugs.</p>

### Higher Software Quality

<p>A tester with many years of experience can make mistakes when they have to prepare the same boring manual test scripts over and over again. Automated testing not only yields accurate results, but also saves time.</p>

### Easy and Robust Reporting

<p>Automated testing tools can track each and every test script. The execution of each test script can be seen in visual logs. The visual log, or report, typically displays the number of test scripts executed and their status (for example, passed, failed or skipped), their reported bugs and hints on how to fix the bugs.</p>

<p>Before we go over how to set up and write tests, let's create a simple plugin to use as a case study.</p>

{{% ad-panel-leaderboard %}}

## Building A WordPress Plugin

<p>We are going to build a simple plugin that displays Google and Bing webmaster verification meta tags in the header of WordPress’ front end. The plugin is hosted <a href="https://github.com/collizo4sky/wp-meta-verify">in my GitHub account</a>.</p>

<p>The code for this plugin below will go in the <code>wp-meta-verify.php</code> file.</p>

<div class="break-out">

<pre><code class="language-php">&lt;?php 

class WP_Meta_Verify 
{
	public function __construct()
	{
		add_action('wp_head', \[$this, 'header_code']);
	}

	public function header_code()
	{
		$google_code = get_option('wpmv_google_code');
		$bing_code = get_option('wpmv_google_code');

		echo $this-&gt;google_site_verification($google_code);
		echo $this-&gt;bing_site_verification($bing_code);
	}

	public function google_site_verification($code)
	{
		return "&lt;meta name=\"google-site-verification\" content=\"$code\"&gt;";
	}

	public function bing_site_verification($code)
	{
		return "&lt;meta name=\"msvalidate.01\" content=\"$code\"&gt;";
	} 
} 

new WP_Meta_Verify();</code></pre></div>

<p>You might notice that we didn't include a settings page in the plugin, where you would typically save the Google and Bing verification code to. I did this on purpose to keep this simple and to focus our attention on what matters most. However, <code>get_option('wpmv_google_code')</code> and <code>get_option('wpmv_bing_code')</code> assume that there is a settings page, and they retrieve the verification codes from there.</p>

## Unit Testing A WordPress Plugin

<p><a href="https://phpunit.de/">PHPUnit</a> is the <em>de facto</em> testing tool for PHP, whereas <a href="https://wp-cli.org/">WP-CLI</a> is the official command line interface for WordPress.</p>

<p>Prior to WP-CLI, <a href="https://make.wordpress.org/core/handbook/testing/automated-testing/phpunit/">setting up PHPUnit testing</a> for WordPress plugins was a pain. WP-CLI has a great <a href="https://make.wordpress.org/cli/handbook/plugin-unit-tests/">guide on setting it up</a>; however, we will still go over the steps here.</p>

### Install PHPUnit

<p>To <a href="https://phpunit.de/manual/current/en/installation.html">install PHPUnit</a>, run the following commands.</p>

<pre><code class="language-php">composer global require phpunit/phpunit:5.*</code></pre>

<p><strong>Note:</strong> We are explicitly installing <code>5.x</code> because that's what WordPress supports when you’re running PHP 7 or above, which I have on my machine. Install PHPUnit 4.8 if you are running PHP version 5.</p>

<p>Run <code>phpunit --version</code> to confirm it's been installed.</p>

### Install WP-CLI

<p>To install WP-CLI, run the following commands.</p>

<pre><code class="language-bash">curl -O https://raw.githubusercontent.com/wp-cli/builds/gh-pages/phar/wp-cli.phar 

chmod +x wp-cli.phar 

sudo mv wp-cli.phar /usr/local/bin/wp</code></pre>

<p>Run <code>wp --info</code> to confirm its installation.</p>

<p>Having installed PHPUnit and WP-CLI, we will use the latter to set up the unit test for the plugin.</p>

{{% ad-panel-leaderboard %}}

### Set Up Plugin Unit Test

<p>Change your terminal’s directory to the root of your WordPress installation, and run the command below to generate the plugin test files.</p>

<pre><code class="language-bash">wp scaffold plugin-tests wp-meta-verify</code></pre>

<p>Below is what the structure of the plugin will look like after the command above generates the test files.</p>

<pre><code>|-bin/
|----install-wp-tests.sh
|-tests/
|----bootstrap.php
|----test-sample.php
|-.travis.yml
|-phpcs.xml.dist
|-phpunit.xml.dist
|-wp-meta-verify.php</code></pre>

<p><strong>Note:</strong> By default, the <code>wp scaffold plugin-tests</code> command generates a Travis CI configuration file. You can specify a <code>--ci</code> flag to generate a configuration file for the CI service you use, like so: <code>wp scaffold plugin-tests --c gitlab</code>. As at the time of writing, only Travis CI, CircleCI and GitLab CI are supported.</p>

<p>Change your terminal’s directory to your plugin’s directory, and run the installation script:</p>

<pre><code class="language-bash">cd path-to-wordpress-plugin</code></pre>

<pre><code class="sourceCode bash">bin/install-wp-tests.sh wordpress_test root '' localhost latest</code></pre>

<p>If you’re like me, then your MySQL username is not <code>root</code>, and the password is not empty. For example, suppose the username is <code>homestead</code> and the password is <code>secret</code>. You would run the installation script like so:</p>

<pre><code class="language-bash">bin/install-wp-tests.sh wordpress_test homestead 'secret' localhost latest</code></pre>

<p>Run the <code>phpunit</code> command to run the default test in <code>tests/test-sample.php</code>.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c92d3a38-73e8-41d9-95d8-756f7440e53e/1-phpunit-command-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ab04b6d1-8532-438b-b0a0-695b157ec43b/1-phpunit-command-800w-opt.png" width="800" height="343" alt="PHPUnit test result" /></a><figcaption>PHPUnit test result (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c92d3a38-73e8-41d9-95d8-756f7440e53e/1-phpunit-command-large-opt.png">Large preview</a>)</figcaption></figure>

### Write Our Plugin Tests

<p>Create a <code>test-wp-meta-verify.php</code> file in the <code>tests</code> folder. It will contain our plugin tests with the following <code>setUp</code> class.</p>

<pre><code class="language-php">&lt;?php 

class WP_Meta_VerifyTest extends WP_UnitTestCase
{
	public function setUp()
	{
		parent::setUp();

		$this-&gt;class_instance = new WP_Meta_Verify();
	}

	public function test_google_site_verification()
	{

	}

	public function test_bing_site_verification()
	{

	}
}</code></pre>

<p>It is worth noting that in order for a method to be considered a unit test, it must be prefixed with <code>test</code>. A best practice is to add a <code>Test</code> suffix to every test class, although it is not required. See <code>WP_Meta_VerifyTest</code>.</p>

<p>Confused about what <code>setUp()</code> does? Just know that PHPUnit runs it once before each test method (and on fresh instances) of the test case class. There is also <code>tearDown()</code>, but it is run after each test method. There are also <code>setUpBeforeClass()</code> and <code>tearDownAfterClass()</code>, which run before and after each test case, respectively. A test case is basically a class that contains a number of test methods. See the <a href="https://make.wordpress.org/core/handbook/testing/automated-testing/writing-phpunit-tests/#advanced-topics">WordPress Handbook</a> and the <a href="https://phpunit.de/manual/current/en/fixtures.html">PHPUnit documentation</a> for more information.</p>

<p>From the class above, it is pretty obvious we are going to be writing tests for the <code>google_site_verification</code> and <code>bing_site_verification</code> methods of our plugin class.</p>

<pre><code class="language-php">public function test_google_site_verification()
{
	$meta_tag = $this-&gt;class_instance-&gt;google_site_verification('B6wFaCRbzWE42SyxSvKUOyyPxZfJCb5g');
	$expected = '&lt;meta name="google-site-verification" content="B6wFaCRbzWE42SyxSvKUOyyPxZfJCb5g"&gt;';

	$this-&gt;assertEquals($expected, $meta_tag);
}</code></pre>

<pre><code class="language-php">public function test_bing_site_verification()
{
	$meta_tag = $this-&gt;class_instance-&gt;bing_site_verification('B6wFaCRbzWE42SyxSvKUOyyPxZfJCb5g');
	$expected = '&lt;meta name="msvalidate.01" content="B6wFaCRbzWE42SyxSvKUOyyPxZfJCb5g"&gt;';

	$this-&gt;assertEquals($expected, $meta_tag);
}</code></pre>

<p>Basically, the tests will ensure that both methods return the correct meta tag when Google and Bing webmaster verification codes are passed to them as arguments.</p>

<p>Run <code>phpunit</code>, and you should see an output similar to the screenshot below.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c11f167f-3111-4452-b8ae-ca751b115d24/2-phpunit-command-output-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e49004d0-af58-428b-82be-ba9be27be047/2-phpunit-command-output-800w-opt.png" width="800" height="347" alt="PHPUnit output" /></a><figcaption>PHPUnit output (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c11f167f-3111-4452-b8ae-ca751b115d24/2-phpunit-command-output-large-opt.png">Large preview</a>)</figcaption></figure>

## Continuous Automated Testing With Travis CI

<p><a href="https://travis-ci.org/">Travis CI</a> is a hosted, distributed continuous integration service used to build and test software projects hosted on GitHub.</p>

<p>To use Travis CI, therefore, we have to publish our plugin on GitHub. Go ahead and <a href="https://help.github.com/articles/adding-an-existing-project-to-github-using-the-command-line/">do that now</a>. Feel free to <a href="https://github.com/collizo4sky/wp-meta-verify">refer to mine</a>.</p>

<p>Thanks to WP-CLI, we already have it set up in our plugin, courtesy of the <code>.travis.yml</code> file.</p>

<p>I would like to mention that I adhere not to <a href="https://make.wordpress.org/core/handbook/best-practices/coding-standards/php/">WordPress coding standards</a>, but rather to <a href="https://www.php-fig.org/psr/">PHP Standards Recommendations</a>, and my plugins require at least PHP 5.4. In order for my <a href="https://travis-ci.org/collizo4sky/wp-meta-verify/builds/264324465">builds not to fail</a>, I had to replace their matrix with the following in <code>.travis.yml</code> file.</p>

<pre><code class="language-markup">matrix:
	include:
		- php: 7.1
		env:&nbsp;WP_VERSION=latest
		- php: 7.0
		env:&nbsp;WP_VERSION=latest
		- php: 5.6
		env:&nbsp;WP_VERSION=latest
		- php: 5.6
		env:&nbsp;WP_VERSION=trunk
		- php: 5.5
		env:&nbsp;WP_VERSION=latest
		- php: 5.4
		env:&nbsp;WP_VERSION=latest</code></pre>

<p>Head over to <a href="https://travis-ci.org/">Travis CI</a> and sign in with your GitHub account. Follow the on-screen guide to add your GitHub repository.</p>

<p>After account synchronization with GitHub, scroll to your plugin’s repository and activate.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9efa469e-8432-4e99-a234-522de79b6ca3/3-phpunit-activate-plugin-repository-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4e18ae68-527a-4409-83c4-20ce0714a114/3-phpunit-activate-plugin-repository-800w-opt.png" width="800" height="242" alt="Setting up Travis CI repository" /></a><figcaption>Setting up Travis CI repository (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9efa469e-8432-4e99-a234-522de79b6ca3/3-phpunit-activate-plugin-repository-large-opt.png">Large preview</a>)</figcaption></figure>

The next time you make a code change and push to GitHub, a build will be triggered on Travis CI.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5497aa2b-b4f4-47f1-9ee6-8add99c364d2/4-phpunit-build-travisci-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0e6aa73b-0627-49ed-873b-6d38bf54e5e6/4-phpunit-build-travisci-800w-opt.png" width="800" height="501" alt="" /></a><figcaption>Travis CI build result (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5497aa2b-b4f4-47f1-9ee6-8add99c364d2/4-phpunit-build-travisci-large-opt.png">Large preview</a>)</figcaption></figure>

I’ve made available a <a href="https://travis-ci.org/collizo4sky/wp-meta-verify/builds/264329247">successful build result</a> for your viewing pleasure.</p>

## Wrapping Up

<p>It's no secret that a lot of developers, not just WordPress ones, do not write tests for their projects because they don't know about them. Even some of the experienced and advanced among us don't apparently because they consider it a waste of time.</p>

<p>Granted, setting up automated testing can be boring and time-consuming. Nevertheless, it's an investment that will ensure that few or no bugs creep into your software, thereby saving you the time and resources (including financial) that bugs in your software would have cost you.</p>

<p>Always write a test before implementing a feature, so that you don't forget or feel lazy to do it after the feature has been implemented.</p>

<p>I hope you now recognize the importance of writing tests and how to start writing one for your own WordPress plugin.</p>

<p>If you have any questions or comments, please let me know in the comments section.</p>

{{< signature "mc, ra, al, il" >}}

