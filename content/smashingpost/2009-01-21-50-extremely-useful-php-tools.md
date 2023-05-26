---
title: 50 Extremely Useful PHP Tools
slug: 50-extremely-useful-php-tools
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2e4f5557-3d2f-4c82-8cff-78ba40be02a6/php.jpg
date: 2009-01-21T04:00:19.000Z
author: jacob-gube
description: >-
  **PHP** is one of the most widely used open-source server-side scripting
  languages that exist today. With over 20 million indexed domains using PHP,
  including major websites like Facebook, Digg and WordPress, there are good
  reasons why many Web developers prefer it to other server-side scripting
  languages, such as Python and Ruby.

  [PHP is
  faster](https://shootout.alioth.debian.org/gp4/benchmark.php?test=all&lang=php&lang2=ruby)
  (_updated_), and it is [the most used scripting
  language](https://www.tiobe.com/index.php/content/paperinfo/tpci/index.html) in
  practice; it has detailed documentation, a huge community, numerous
  ready-to-use scripts and well-supported frameworks; and most importantly, it’s
  much easier to get started with PHP than with other scripting languages
  (Python, for example). That’s why it makes perfect sense to provide the huge
  community of PHP developers with an overview of useful tools and resources
  that can make their development process easier and more effective.

  [![Webgrind](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9efefb0f-6269-4fc8-8554-775ead1d444a/webgrind.jpg)](https://www.smashingmagazine.com/2009/01/20/50-extremely-useful-php-tools/)

  This post presents **50 useful PHP tools that can significantly improve your
  programming workflow**. Among other things, you’ll find a plethora of
  libraries and classes that aid in debugging, testing, profiling and
  code-authoring in PHP.

  You may also want to take a look at the following related posts:

  *   [50 Extremely Useful And Powerful CSS
  Tools](https://www.smashingmagazine.com/2008/12/09/50-really-useful-css-tools/)

  *   [15 Helpful In-Browser Web-Development
  Tools](https://www.smashingmagazine.com/2008/11/18/15-helpful-in-browser-web-development-tools/)
categories:
  - Coding
  - Tools
  - PHP
  - Resources
---
**PHP** is one of the most widely used open-source server-side scripting languages that exist today. With over 20 million indexed domains using PHP, including major websites like Facebook, Digg and WordPress, there are good reasons why many Web developers prefer it to other server-side scripting languages, such as Python and Ruby.

PHP is faster (_updated_), and it is [the most used scripting language](https://www.tiobe.com/index.php/content/paperinfo/tpci/index.html) in practice; it has detailed documentation, a huge community, numerous ready-to-use scripts and well-supported frameworks; and most importantly, it’s much easier to get started with PHP than with other scripting languages (Python, for example). That’s why it makes perfect sense to provide the huge community of PHP developers with an overview of useful tools and resources that can make their development process easier and more effective.

This post presents **50 useful PHP tools that can significantly improve your programming workflow**. Among other things, you’ll find a plethora of libraries and classes that aid in debugging, testing, profiling and code-authoring in PHP.

You may also want to take a look at the following related posts:

*   [50 Extremely Useful And Powerful CSS Tools](https://www.smashingmagazine.com/2008/12/09/50-really-useful-css-tools/)
*   [15 Helpful In-Browser Web-Development Tools](https://www.smashingmagazine.com/2008/11/18/15-helpful-in-browser-web-development-tools/)

## Debugging Tools

*   [Webgrind](https://code.google.com/p/webgrind/)  
    Webgrind is an [Xdebug](https://www.xdebug.org/) profiling Web front end in PHP 5\. It implements a subset of the features of [kcachegrind](https://kcachegrind.sourceforge.net/cgi-bin/show.cgi), installs in seconds and works on all platforms. For quick ‘n’ dirty optimizations, it does the job.

    [![Webgrind](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9efefb0f-6269-4fc8-8554-775ead1d444a/webgrind.jpg)](https://code.google.com/p/webgrind/)

{{% feature-panel %}}

*   [Xdebug](https://xdebug.org/index.php)  
    Xdebug is one of the most popular debugging PHP extensions. It provides a ton of useful data to help you quickly find bugs in your source code. Xdebug plugs right into many of the most popular PHP applications, such as PHPEclipse and phpDesigner.
*   [Gubed PHP Debugger](https://gubed.mccabe.nu/)  
    As the name implies, Gubed PHP Debugger is a PHP debugging tool for hunting down logic errors.
*   [DBG](https://www.php-debugger.com/dbg/)  
    DBG is a robust and popular PHP debugger for use in local and remote PHP debugging. It plugs into numerous PHP IDE’s and can easily be used with the command line.
*   [PHP_Debug](https://www.php-debug.com/www/)  
    PHP_Debug is an open-source project that gives you useful information about your PHP code that can be used for debugging. It can output processing times of your PHP and SQL, check the performance of particular code blocks and get variable dumps in graphical form, which is great if you need a more visual output than the one given to you by print_r() or var_dump().
*   [PHP_Dyn](https://sourceforge.net/projects/php-dyn/)  
    PHP_Dyn is another excellent PHP debugging tool that’s open-source. You can trace execution and get an output of the argument and return values of your functions.
*   [MacGDBp](https://www.bluestatic.org/software/macgdbp/)  
    MacGDBp is a live PHP debugger application for the Mac OS. It has all the features you’d expect from a fully featured debugger, such as the ability to step through your code and set breakpoints.</p>

## Testing and Optimization Tools

*   [PHPUnit](https://www.phpunit.de/)  
    PHPUnit is a complete port of the popular [JUnit](https://www.junit.org/) unit testing suite to PHP 5\. It’s a tool that helps you test your Web application’s stability and scalability. Writing test cases within the PHPUnit framework is easy; here’s [how to do it](https://www.phpunit.de/manual/current/en/writing-tests-for-phpunit.html).
*   [SimpleTest](https://www.simpletest.org/)  
    SimpleTest is a straightforward unit-testing platform for PHP applications. To get up and running with SimpleTest quickly, read through this pragmatic [tutorial](https://www.simpletest.org/en/first_test_tutorial.html) that shows you how to create a new test case.

    [![Simpletest](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0c2154bc-31bc-4aad-80a8-5e817610eb6d/simpletest.gif)](https://www.simpletest.org/)

*   [Selenium](https://selenium-rc.openqa.org/)  
    Selenium Remote Control (RC) is a test tool that allows you to write automated Web application UI tests in any programming language against any HTTP website using any mainstream JavaScript-enabled browser. It can be used in conjunction with PHPUnit to create and run automated tests within a Web browser.
*   PHP_CodeSniffer  
    PHP_CodeSniffer is a PHP 5 script for detecting conformance to a predefined PHP coding standard. It’s a helpful tool for maintaining uniform coding styles for large projects and teams.
*   [dBug](https://dbug.ospinto.com/)  
    dBug is ColdFusion’s cfDump for PHP. It’s a simple tool for outputting data tables that contain information about arrays, classes and objects, database resources and XML resources, making it very useful for debugging purposes.

    [![dBug - Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6c549b56-4cb8-4b28-97ef-497ccdf0d040/11-dbug.jpg)](https://dbug.ospinto.com/)

*   [PHP Profile Class](https://www.coderholic.com/php-profile-class/)  
    PHP Profile Class is an excellent PHP profiling tool for your Web applications. Using this class will help you quickly and easily gain insight into which parts of your app could use some refactoring and optimization.</p>

## Documentation Tools

*   [phpDocumentor](https://phpdoc.org/)  
    phpDocumentor (also known as phpdoc and phpdocu) is a documentation tool for your PHP source code. It has an innumerable amount of features, including the ability to output in HTML, PDF, CHM and XML DocBook formats, and has both a Web-based and command-line interface as well as source-code highlighting. To learn more about phpDocumentor, check out the online manual.
*   [PHP DOX](https://phpdox.net/)  
    An AJAX-powered PHP documentation search engine that enables you to search titles from all PHP documentation pages.</p>

## Security Tools

*   [Securimage](https://www.phpcaptcha.org/)  
    Securimage is a free, open-source PHP CAPTCHA script for generating complex images and CAPTCHA codes to protect forms from spam and abuse.
*   [Scavenger](https://trac.anl.gov/scavenger/wiki/WikiStart)  
    Scavenger is an open-source, real-time vulnerability management tool. It helps system administrators respond to vulnerability findings, track vulnerability findings and review accepted and false-positive answered vulnerabilities, without “nagging” them with old vulnerabilities.
*   [PHP-IDS](https://php-ids.org/)  
    PHP-IDS (PHP-Intrusion Detection System) is a simple-to-use, well-structured, fast and state-of-the-art security layer for your PHP-based Web application.
*   [Pixy: PHP Security Scanner](https://blog.evaria.com/2007/pixy-the-php-security-scanner/)  
    Pixy is a Java program that performs automatic scans of PHP 4 source code, aimed to detect XSS and SQL injection vulnerabilities. Pixy takes a PHP program as input and creates a report that lists possible vulnerable points in the program, along with additional information for understanding the vulnerability.</p>

## Image Manipulation and Graphs

*   [PHP/SWF Charts](https://www.maani.us/charts4/)  
    PHP/SWF Charts is a powerful PHP tool that enables you to create attractive Web charts and graphs from dynamic data. You can use PHP scripts to generate and gather data from databases, then pass it to this tool to generate Flash (SWF) charts and graphs.
*   [pChart - a chart-drawing PHP library](https://pchart.sourceforge.net/index.php)  
    pChart is a PHP class-oriented framework designed to create aliased charts. Most of today’s chart libraries have a cost; this one is free. Data can be retrieved from SQL queries or CSV files or can be manually provided.

    [![Chart - Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/122a7616-1c19-4995-aa8c-bffcf1dec31f/chart.gif)](https://simplepie.org/)

*   [WideImage](https://wideimage.sourceforge.net/wiki/MainPage)  
    WideImage is a PHP library for dynamic image manipulation and processing for PHP 5\. To be able to use the library, you should have the [GD PHP extension](https://us2.php.net/gd) installed on your Web server.
*   [MagickWand For PHP](https://www.magickwand.org/)  
    MagickWand For PHP is a PHP module suite for working with the [ImageMagick](https://www.imagemagick.org/script/index.php) API, which lets you create, compose and edit bitmap images. It’s a useful tool for quickly incorporating image-editing features in your PHP applications.</p>

## PHP Code Beautifier

*   [PHP_Beautifier](https://pear.php.net/package/PHP_Beautifier)  
    PHP Beautifier is a PEAR package for automatically formatting and “beautifying” PHP 4 and PHP 5 source code.
*   PHPCodeBeautifier  
    PHPCodeBeautifier is a tool that saves you from hours of reformatting code to suit your own way of presenting it. A GUI version allows you to process files visually; a command-line version can be batched or integrated with other tools (like CVS, SubVersion, IDE, etc.); and there is also an integrated tool of PHPEdit.
*   [GeSHi - Generic Syntax Highlighter](https://qbnz.com/highlighter/)  
    GeSHi is designed to be a simple but powerful highlighting class, with the goal of supporting a wide range of popular languages. Developers can easily add new languages for highlighting and define easily customizable output formats.</p>

## Version-Control Systems

*   [Phing](https://phing.info/trac/)  
    Phing is a popular project version-control system for PHP. It is a useful tool for organizing and maintaining different builds of your project.
*   [xinc](https://code.google.com/p/xinc/)  
    xinc is a [continuous integration server](https://www.martinfowler.com/articles/continuousIntegration.html#EveryCommitShouldBuildTheMainlineOnAnIntegrationMachine) version-control system written in PHP 5 (i.e. continuous builds instead of nightly builds). It works great with other systems such as [Subversion](https://subversion.tigris.org/) and [Phing](https://phing.info/).

## Useful Extensions, Utilities and Classes

*   [SimplePie](https://simplepie.org/)  
    SimplePie is a PHP class that helps you work with RSS feeds. Check out the online [RSS and Atom feed reader](https://simplepie.org/demo/), which demonstrates a simple Web application that uses SimplePie.

    [![SimplePie - Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/640bdfa0-787e-4e2b-8e32-faa9b2c8a2ff/spie.jpg)](https://simplepie.org/)

*   [HTML Purifier](https://htmlpurifier.org/)  
    HTML Purifier is a standards-compliant HTML filter library written in PHP. HTML Purifier not only removes all malicious code (better known as XSS) with a thoroughly audited, secure yet permissive white list, it also makes sure your documents are standards-compliant. Open source and highly customizable.
*   TCPDF  
    TCPDF is an open-source PHP class for generating PDF documents.
*   [htmlSQL](https://www.jonasjohn.de/lab/htmlsql.htm)  
    htmlSQL is a unique tool. It is a PHP class for querying HTML values in an SQL-like syntax. Check out the [live demonstration of how htmlSQL works](https://www.jonasjohn.de/lab/htmlsql/).
*   [The Greatest PHP Snippet File Ever (Using Quicktext for Notepad++)](https://searchlightdigital.com/the-greatest-php-snippet-file-ever-using-quicktext-for-notepad)  
    “A little something for all coders: a snippets file that I use for PHP coding. This is designed to be used with Quicktext for Notepad++, but feel free to adapt it to whatever text editor you prefer.”
*   Creole  
    Creole is a database abstraction layer for PHP5\. It abstracts PHP’s native database-specific API to create more portable code while also providing developers with a clean, fully object-oriented interface based loosely on the API for Java’s JDBC.
*   [PHPLinq](https://www.codeplex.com/PHPLinq)  
    LINQ is a component that adds native data querying capabilities to PHP using a syntax reminiscent of SQL. It defines a set of query operators that can be used to query, project and filter data in arrays, enumerable classes, XML, relational databases and third-party data sources. [[via](https://phpimpact.wordpress.com/2008/05/29/30-useful-php-classes-and-components/)]
*   [PHPMathPublisher](https://www.xm1math.net/phpmathpublisher/)  
    With PhpMathPublisher, you can publish mathematical documents on the Web using only a PHP script (no LaTeX programs on the server and no MathML).

    [![Math - Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9b5aff2e-2b17-4ba9-b0d3-f408768b18bc/math.gif)](https://www.xm1math.net/phpmathpublisher/)

*   [phpMyAdmin](https://www.phpmyadmin.net/home_page/index.php)  
    If you’re working with PHP, there’s a big chance you’re set up in a LAMP configuration. phpMyAdmin is Web-based tool for managing, building, importing, exporting and exploring MySQL databases.
*   [PHPExcel](https://www.codeplex.com/PHPExcel)  
    PHPExcel is a set of useful PHP classes for working with Microsoft Excel files. PHPExcel allows you to read Excel files and write to them. This is useful for dynamically generating Excel spreadsheets for downloading.
*   [Phormer](https://p.horm.org/er/)  
    Phormer is a PHP-based photo gallery management application that helps you to store, categorize and trim your photos online.
*   [xajax PHP Class Library](https://www.xajaxproject.org/)  
    xajax is a PHP class for easily working with PHP AJAX applications. It gives you an easy-to-use API for quickly managing AJAX-related tasks. Check out the [xajax Multiplier demo](https://www.xajaxproject.org/examples/multiply/multiply.php) and the [Graffiti Wall demo](https://www.xajaxproject.org/examples/thewall/thewall.php) to see the xajax PHP class in action.
*   [PHP User Class](https://phpuserclass.com/)  
    PHP User Class is an excellent script that helps you create a system for user authentication (i.e. registration, log in, account profile, etc.). It’s a useful utility to have around if you require user registration for your Web applications.
*   [PHP-GTK](https://gtk.php.net/)  
    PHP-GTK is a PHP extension for the [GTK+](https://www.gtk.org/) toolkit (a robust toolkit for developing GUIs). It is a suite of useful OOP functions and classes to help you rapidly build cross-platform, client-side GUI’s for your application.</p>

## PHP Online Tools and Resources

*   [Minify!](https://code.google.com/p/minify/)  
    Minify is a PHP 5 app that can combine multiple CSS or JavaScript files, compress their content (i.e. remove unnecessary white space and comments) and serve the results with HTTP encoding (via Gzip/deflate) and headers that allow optimal client-side caching. This will help you follow several of Yahoo!’s [Rules for High Performance Websites](https://developer.yahoo.com/performance/index.html#rules).

    [![minify - Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e9074820-cb3d-4a24-8410-a1145c51c757/minify.gif)](https://code.google.com/p/minify/)

*   [HTTP_StaticMerger: Automatic “merging” of CSS and JavaScript files](https://en.dklab.ru/lib/HTTP_StaticMerger/)  
    This library automatically merges sets of static files (CSS or JavaScript) and speeds up page loading (by lowering the number of HTTP queries). It is recommended to use this together with caching reverse-proxy to minimize the response time.
*   [PHP Object Generator](https://www.phpobjectgenerator.com/)  
    PHP Object Generator is an open-source Web-based tool that helps you quickly construct PHP objects and leverage object-oriented programming (OOP) principles in your code.

    [![Php Object Generator - Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f526ab7a-077d-4b52-a606-840ef62edff2/03-object-generator.jpg)](https://www.phpobjectgenerator.com/)

*   gotAPI/PHP  
    gotAPI is a useful online tool for quickly looking up PHP functions and classes. Also check out the Quick PHP look-up widget example in case you’d like to include this awesome look-up feature on your website.![gotAPI/PHP - Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5e448248-a6e6-4115-a09f-83f85a066331/04-gotapi.jpg)</li> 
<li><a href="https://www.koders.com/">koders</a><br />koders is a search engine for open-source and downloadable code. It currently has over a billion lines of code indexed and isn&#8217;t limited to just PHP.</li> 
<li><a href="https://pecl.php.net/">PECL</a><br />PECL is a directory of all known PHP extensions and a hosting facility for downloading and developing PHP extensions.</li>

## In-Browser Tools (Firefox Add-Ons)

*   FirePHP  
    FirePHP is a Firefox extension that allows you to log data in [Firebug](https://getfirebug.com/). It has a variety of useful logging features, such as the ability to change your error and exception handling on the fly and to log errors directly to the Firebug console. To learn more about what FirePHP can do, check out the FirePHP guide on how to use FirePHP. For developers using the [Zend PHP framework](https://framework.zend.com/), you might find this guide on [using FirePHP with Zend](https://www.christophdorn.com/Blog/2008/09/02/firephp-and-zend-framework-16/) useful.![FirePHP - Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a9e010e8-ca22-4e9a-b031-616e9fc7dc88/01-firephp.jpg)</li> 

*   [phpLangEditor](https://phplangeditor.mozdev.org/)  
    phpLangEditor is a very handy Firefox add-on for translating language files and variables in your script.[![phpLangEditor - Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b91ece8a-8182-419e-950a-0b8ff610feb7/02-phplangeditor.jpg)](https://phplangeditor.mozdev.org/)</li> 
<li><a href="https://addons.mozilla.org/en-US/firefox/addon/3505">PHP Lookup</a><br />PHP Lookup is a built-in search bar to help you quickly look up references to PHP syntax.</li> 
<li><a href="https://addons.mozilla.org/en-US/firefox/addon/8984">PHP Manual Search</a><br />PHP Manual Search is a handy search bar that searches <a href="https://www.php.net/docs.php">official PHP documentation</a> from within your Web browser.</li>

## Frameworks for PHP

*   [Dwoo](https://dwoo.org/)  
    Dwoo is a PHP 5 template engine positioned as an alternative to Smarty. It is (nearly) fully compatible with its templates and plug-ins, but it is being written from scratch and is aimed to go one step further with a cleaner code base.
*   CodeIgniter  
    CodeIgniter is a powerful, high-performance, open-source PHP framework that helps you author PHP applications rapidly. CodeIgniter is known for having a light footprint, thereby reducing your server’s work. You can get up and running with CodeIgniter in a jiffy: it has an awesome online manual, a couple of helpful video tutorials and an active user forum.

    ![CodeIgniter - Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/83a07daf-8d6c-4f58-aed3-da42889c3cff/codeigniter.jpg)

*   [YII Framework](https://www.yiiframework.com/)  
    Here is a high-performance component-based PHP framework that is supposed to be more efficient than CodeIgniter, CakePHP, ZF and Symfony. An optimal solution for developing large-scale Web applications. Yii supports MVC, DAO/ActiveRecord, I18N/L10N, caching, jQuery-based AJAX support, authentication and role-based access control, scaffolding, input validation, widgets, events, theming and Web services.
*   [NetBeans](https://www.netbeans.org/features/php/index.html)  
    A dedicated PHP coding environment and complete integration with web standards. The NetBeans PHP editor is dynamically integrated with NetBeans HTML, JavaScript and CSS editing features such as syntax highlighting and the JavaScript debugger. NetBeans IDE 6.5 fully supports iterative development, so testing PHP projects follows the classic patterns familiar to web developers.
*   Solar  
    Solar is a PHP 5 development framework for Web applications derived from the [Savant](https://phpsavant.com/) templating engine. Solar uses the MVC architectural pattern and has a host of classes and functions for securing your Web app against SQL injection, cross-website scripting (XSS) and other common exploits.

    ![Solar - Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/84c7da10-01ca-45a9-92a2-37f5494bcfe4/solar.jpg)

*   [symfony](https://www.symfony-project.org/)  
    symfony is an open-source PHP 5 Web application framework that is well known for its modularity and useful library of classes. To get up and running as fast as possible, you should check out the pragmatic symfony online tutorial called “The symfony 1.2 advent calendar tutorial,” which takes you through a step-by-step example of building your own symfony-based Web application.
*   [PEAR - PHP Extension and Application Repository](https://pear.php.net/)  
    PEAR is a popular framework and distribution system for reusable PHP components. The purpose of the framework is to provide a structured library of open-source code for PHP users, a system for code distribution and package maintenance and a standard style for PHP code.
*   Propel  
    Propel is an Object-Relational Mapping (ORM) framework for PHP 5\. It allows you to access your database using a set of objects, providing a simple API for storing and retrieving data.
*   {{macro}} template engine  
    {{macro}} compiles initial templates into executable PHP scripts with very clean syntax (much cleaner than WACT and Smarty) and executes them very fast. The engine doesn’t use an XML-like syntax; there are only two data scopes, global and local, and no more data sources (all data is displayed with regular PHP variables); and the system supports all WACT features such as templates wrapping and including.![minify - Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a3194ebb-19ac-4469-ac04-395b2f77b6e7/macro.gif)
*   [Zend Framework](https://framework.zend.com/)  
    The Zend Framework by [Zend Technologies](https://www.zend.com/en/company/) (the creators of PHP’s scripting engine) is a popular PHP Web application framework that embraces the principles of PHP OOP; it’s very extensible and has built-in utilities for working with free Web service APIs, such as those of [Google](https://code.google.com/apis/gdata/), [Flickr](https://flickr.com/services/) and [Amazon](https://aws.amazon.com/).
*   Qcodo  
    Qcodo is an excellent open-source PHP Web application framework. It’s subdivided into two parts: (1) Code Generator, and (2) Qforms. Code Generator handles the creation of object code and PHP and HTML front-end code from your data model. Qforms is an intuitive system for handling and creating complex PHP-driven HTML Web forms. Check out demos of applications that use Qcodo and presentational material that covers Qcodo.

    ![Qcodo - Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/af6ee4d6-6e93-44ba-a6b1-979864b42635/qc.gif)

*   [SAJAX](https://www.modernmethod.com/sajax/)  
    SAJAX is a JavaScript and AJAX application framework that works well with PHP (as well as several other server-side scripting languages). See SAJAX at work by going to [Wall live demonstration](https://www.modernmethod.com/sajax/sajax-0.12/php/example_wall.php).
*   [Smarty](https://www.smarty.net/)  
    Smarty is a popular PHP templating system to help you separate PHP logic and front-end code (HTML, CSS, JavaScript). It will keep your projects modular and easier to maintain.
*   [CakePHP](https://cakephp.org/)  
    CakePHP is one of the leading PHP frameworks for creating robust, fully-featured Web applications. CakePHP has an extensive and well-organized [online manual](https://book.cakephp.org/). If you want to learn via video tutorials, check out the CakePHP screencasts.

    [![CakePHP - Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/436832f3-2558-4718-b175-adbd98798e30/cake.jpg)](https://cakephp.org/)

*   [Savant2](https://phpsavant.com/yawiki/)  
    Savant2 is another popular object-oriented PHP templating system. Instead of a special syntax unique to Savant2, you use PHP syntax to develop your project’s template.
*   [PHPSpec](https://www.phpspec.org/)  
    PHPSpec is a simple and intuitive PHP framework. It follows the Behavior-Driven Development principle and therefore allows you to write behavior-oriented code, oftentimes in plain English.</p>

## PHP IDEs and Editors

*   <span class="removed_link" title="https://www.phpeclipse.com/">PHPEclipse</span>  
    PHPEclipse is a popular PHP source-code editor that is open source and runs on all the major operating systems, such as Windows, Linux and Mac OS. It has all the features you’d expect from a PHP source-code editor, such as code-folding, syntax highlighting, hover-over tool tips and support for XDebug and DBG.

    <span class="removed_link" title="https://www.phpeclipse.com/">![PHPEclipse - Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/639771d6-8981-4952-8cbb-e522fe2dd583/07-php-eclipse.jpg)</span>

*   [PhpED](https://www.nusphere.com/products/phped.htm)  
    PhpED is an excellent IDE for Windows users. It is one of the most robust and feature-packed IDEs currently out on the market and has useful features such as a built-in [source-code profiler](https://www.nusphere.com/products/php_profiler.htm) to find bottlenecks in your PHP source code and excellent integration with third-party apps and services just as front-end code validation.

    [![PhpED - Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fa9603a6-aad5-40f8-807c-0afa99931a02/08-phped.jpg)](https://www.nusphere.com/products/phped.htm)

*   [phpDesigner](https://www.mpsoftware.dk/phpdesigner.php)  
    phpDesigner is a lightweight PHP editor/IDE that also handles front-end code and markup remarkably well. Check out the phpDesigner [online tutorials](https://www.mpsoftware.dk/tutorials.php), as well as [screencasts on phpDesigner](https://www.mpsoftware.dk/phpdesigner_screencasts.php) to help you learn more about the IDE.

    [![phpDesigner - Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c66623f5-3cf5-4fa3-9d44-f31617672b87/09-phpdesigner.jpg)](https://www.mpsoftware.dk/phpdesigner.php)

*   [Zend Studio](https://www.zend.com/en/products/studio/)  
    Zend Studio is an excellent PHP IDE for Eclipse. It’ll help you develop, deploy and manage Rich Internet Applications (RIAs) in an intuitive interface.

    [![Zend Studio - Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/400c0916-b7a8-4e0c-9a52-a50e7018691b/10-zend-studio.jpg)](https://www.zend.com/en/products/studio/)

*   Aptana PHP  
    Aptana PHP is an open-source IDE extension/plug-in to be used in conjunction with Aptana Studio. To learn more, be sure to check out the online documentation about Aptana PHP.
*   [PDT](https://www.eclipse.org/pdt/)  
    PDT is a PHP Development Tools framework that’s part of the Eclipse project. PDT includes all the necessary tools for you to create PHP-based Web applications.
*   [VS.Php](https://www.jcxsoftware.com/vs.php)  
    VS.Php is a PHP IDE for MS Visual Studio, making it a great IDE for recently converted ASP developers who have used MS VS to develop Web applications. To get you up and running ASAP with VS.Php, check out Jcx.Software’s [online tutorials](https://www.jcxsoftware.com/tutorials.php) as well as its [online documentation](https://www.jcxsoftware.com/jcx/vsphp/docs).
*   [PHPEdit](https://www.phpedit.com/)  
    PHPEdit is an excellent PHP editor/IDE with a ton of useful features and a very intuitive user interface. To learn more about why PHPEdit is a good IDE, read the 10 reasons to use PHPEdit and view the introductory screencast about PHPEdit.</p>

## Sources and Resources

*   [PHP Function Reference](https://code.google.com/p/phpfr/)  
    PHP Function Reference (PHPfr) is a Mac OS X dashboard widget that provides a fast look-up of information about the PHP Web programming language.
*   [30 Useful PHP Classes and Components](https://phpimpact.wordpress.com/2008/05/29/30-useful-php-classes-and-components/)  
    30 useful PHP classes and components that you can use to test, develop, debug and deploy your PHP applications.
*   PHP advent 2008  
    In December, phpadvent.org collected the wisdom of people in the PHP community who kindly donated their ideas and tips to see us through the new year.
*   [Useful in-browser development tools for PHP](https://www.sitepoint.com/blogs/2008/05/13/useful-in-browser-development-tools-for-php/)
*   [PHPClasses.org](https://www.phpclasses.org/)  
    A huge repository of various PHP classes.
*   [PHP Developer’s Toolbox](https://mashable.com/2007/09/26/php-toolbox/)  
    Various PHP-related resources in a brief overview.

{{< signature "al" >}}

