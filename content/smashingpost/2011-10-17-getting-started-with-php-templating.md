---
title: Getting Started With PHP Templating
slug: getting-started-with-php-templating
image: null
date: 2011-10-17T07:00:59.000Z
author: krzysztof-rakowski
description: >-
  In the early days of PHP applications, “spaghetti code” was a familiar sight. In this article, we’ll cover how to separate the view of your PHP application from its other components. 
categories:
  - Coding
  - Frameworks
  - PHP
  - Techniques
---
We’ll look at why using such an architecture is useful and what tools we can use to accomplish this. Here's what we'll cover:

1.  Learn some basic MVC concepts,
2.  Review some popular templating libraries,
3.  Play around with a small custom-made view class.
4.  Explore the basics of using the Twig library.

To fully benefit from this article, you should already know how to write and run your own PHP scripts on a Web server (i.e. using Apache).</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [PHP: What You Need To Know To Play With The Web](https://www.smashingmagazine.com/2010/04/php-what-you-need-to-know-to-play-with-the-web/)
*   [50 Extremely Useful PHP Tools](https://www.smashingmagazine.com/2009/01/50-extremely-useful-php-tools/)
*   [<span class="headline">Client-Side Templating</span>](https://www.smashingmagazine.com/2012/12/client-side-templating/)

{{% feature-panel %}}

## A Quick Introduction To The MVC Pattern

In the early days of PHP applications, “spaghetti code” was a familiar sight. Fragments of PHP code were mixed in with HTML mark-up. There were no frameworks, so Web applications were just a bunch of source files. As the PHP language matured, developers started to think about the cleanliness and maintainability of their code. The [model-view-controller (MVC)](https://www.smashingmagazine.com/2016/05/better-architecture-for-ios-apps-model-view-controller-pattern/) pattern was introduced.

MVC is a software architecture that allows for the separation of business logic from the user interface. In this architecture, the user sees and interacts with the view that, in the case of Web applications, is generated HTML code (along with JavaScript, CSS, images, etc.)

<figure><img title="MVC - schema" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/62b18525-6769-4817-b186-4aeb8fc43ae6/mvc.png" alt="screenshot" width="500" height="250" /></figure>

User actions are passed (as HTTP requests, <code>GET</code> or <code>POST</code> methods) to the <strong>controller</strong>. The controller is a piece of code that handles and processes user input and then reads and makes necessary changes to the <strong>model</strong>, which is responsible for the storage and modification of data. (In simple terms, the model consists of the database structure and contents, and the code used to access it.) Then, the controller generates the proper <strong>view</strong> that will be sent and displayed to user.

Such separation of layers has many advantages…

### Code Is Easier to Maintain

Because the model is separated, changing internal data relations without changing the rest of the application is easier. For example, the model for the user could provide the <code>is_active()</code> method, returning a boolean variable. In the business logic, it would be enough to check what value is returned by this method, without any knowledge of its internals.

You can also check for various conditions (for example, whether the user has confirmed their registration, paid their monthly fee, etc.), and you can change these rules in one place, without having to change anything in the other parts of the code. It also becomes easy to make a platform-independent application that allows for switching between database engines; this is often performed by ORM (object-relational mapper) libraries, which are a sub-layer of the model layer. ORMs add a level of abstraction to the library that accesses the specific database directly.</p>

### The Same Content in Multiple Views

Separating the view allows a single result to be presented in different forms. For example, based on some logic, a news page could be displayed in normal, mobile and RSS versions, all using the same content returned from the controller.</p>

### More Secure

Variables are escaped by default before being sent to the view, which is useful in applications that display user-generated content. Consider a variable with some unknown HTML or JavaScript code being passed to the view (which should never happen in your application). Escaping the variables prevents malicious code from being injected in such cases.

### Better Code

Separating the layers forces the programmer to design better applications that are easier and cheaper to maintain. Also, designers and front-end developers don’t have to work with the business-logic code, because their task is only to display the contents of the variables that are provided to the view. This reduces the risk of the breaking some PHP code.

Today, every modern framework implements the MVC architecture. There are also some libraries that enable you to use selected features of the architecture. In this article, we’ll go over the recipes for the view, and in future articles we’ll cover the model and some ORM libraries.</p>

## Overview Of PHP Template Engines

As you might expect, many templating libraries allow you to separate the view layer from the rest of the application. In the most basic scenario, you can implement such a library by yourself (which we’ll do in the next section). You don’t even need a special library; sometimes it is enough just to separate your view (i.e. the template’s HTML files) into a different directory, prepare some variables in the simple controller (usually the main PHP file) and include the templates.

Every modern PHP Web application framework employs some kind of templating engine. Most of them use plain PHP by default (including Symfony 1.x, Zend Framework and CakePHP), but many standalone libraries can be plugged into your favorite framework or custom application.</p>

### Smarty

<figure><a href="https://www.smarty.net/"><img title="Smarty" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6be6c849-b6f8-418a-bb8e-e3457ea96520/smarty.png" alt="screenshot" width="500" height="204" /></a></figure>

<a href="https://www.smarty.net/">Smarty</a> was one of the first and most advanced templating engines. It was developed as a sub-project of the main PHP project, but it has lost its popularity in recent years due to poor performance and forced backward compatibility with PHP 4. It has also lacked many modern features, such as template inheritance. Now, it is rising back to power with version 3. Many other frameworks (such as <a href="https://twig.sensiolabs.org/">Twig</a> and <a href="https://www.djangoproject.com/">Django</a>) have inherited some of the basic concepts laid down by Smarty.

<pre><code class="language-markup tmp-xml">&lt;html&gt;
    &lt;head&gt;
        &lt;title&gt;Info&lt;/title&gt;
    &lt;/head&gt;
    &lt;body&gt;
        &lt;pre&gt;
            User Information:
            Name: {$name|capitalize}
            Addr: {$address|escape}
            Date: {$smarty.now|date_format:"%b %e, %Y"}
        &lt;/pre&gt;
    &lt;/body&gt;
&lt;/html&gt;</code></pre>

### PHPTAL

<figure><a href="https://phptal.org/"><img title="PHPTAL" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ff49ab59-af96-41ff-a83a-7cafb8a32429/phptal-small.png" alt="screenshot" width="500" height="133" /></a></figure>

<a href="https://phptal.org/">PHPTAL</a> is a template language based on a very different syntax and concept; it implements the Zope Page Templates syntax (Zope is an application server written in Python). It is based on well-formed XML/XHTML, as in this example that comes from the project page:

<pre><code class="language-markup tmp-xml">&lt;div tal:repeat="value values"&gt;
    &lt;div&gt;
        &lt;span tal:condition="value/hasDate"
        tal:replace="value/getDate"&gt;
            2008-10-06
        &lt;/span&gt;
        &lt;a href="sample.html"
        tal:attributes="href value/getUrl"
        tal:content="value/getTitle"&gt;
            My item title
        &lt;/a&gt;
    &lt;/div&gt;
    &lt;div tal:content="value/getContent"&gt;
        This is sample content that will be replaced by
        real content when the template is run with real
        data.
    &lt;/div&gt;
&lt;/div&gt;</code></pre>

If you have prior experience with ZOPE or are a fan of XML, then this template engine is for you.</p>

### Twig

<figure><a href="https://twig.sensiolabs.org/"><img title="Twig" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2cc07222-faee-4678-9875-202bc9a8b559/twig.png" alt="screenshot" width="500" height="186" /></a></figure>

The last PHP template engine we’ll look at, and the one we’ll focus on in this article, is <a href="https://www.twig-project.org/">Twig</a>, from the authors of Symfony, which is the default view library of this framework’s 2.0 version. Its advantages are rich features, extensibility, good documentation, security and speed (it compiles your templates to the native PHP language).

<pre><code class="language-markup tmp-xml">&lt;html&gt;
    &lt;head&gt;&lt;title&gt;My first Twig template!&lt;/title&gt;&lt;/head&gt;
    &lt;body&gt;
        My name is {{ name }}.
        My friends are:
        &lt;ul&gt;
        {% for person in friends %}
            &lt;li&gt;{{ person.firstname}} {{ person.lastname }}&lt;/li&gt;
        {% endfor %}
        &lt;/ul&gt;
    &lt;/body&gt;
&lt;/html&gt;</code></pre>

## The Basic Concept

Knowing how to use a particular library or framework is not enough. A good programmer should also know what is under the hood: how the stuff works, the relationship between the components, and possible caveats. For this reason, we’ll go over the concept with a simple templating library, custom-made for this tutorial. This should give you an idea of how more advanced libraries work. To run this code on your own, you will need to properly configure your HTTP server (with Apache), using PHP 5. No other libraries are needed.

<strong>Note:</strong> you can download this example code from the Mercurial repository on Bitbucket either by <a href="https://bitbucket.org/krzysztofr/sm-view/get/tip.zip">downloading the ZIP file</a> or, if you have a command-line version of Mercurial installed, by entering the following command:
<code>hg clone https://bitbucket.org/krzysztofr/sm-view</code>.

First, let’s look at the code.</p>

### MyView.php: Templating Library

<pre><code class="language-php">&lt;?php
class MyView {
    protected $template_dir = 'templates/';
    protected $vars = array();
    public function __construct($template_dir = null) {
        if ($template_dir !== null) {
            // Check here whether this directory really exists
            $this-&gt;template_dir = $template_dir;
        }
    }
    public function render($template_file) {
        if (file_exists($this-&gt;template_dir.$template_file)) {
            include $this-&gt;template_dir.$template_file;
        } else {
            throw new Exception('no template file ' . $template_file . ' present in directory ' . $this-&gt;template_dir);
        }
    }
    public function __set($name, $value) {
        $this-&gt;vars[$name] = $value;
    }
    public function __get($name) {
        return $this-&gt;vars[$name];
    }
}
?&gt;</code></pre>

The main (and only) class of our templating engine is very simple. We use the “magic methods” (yes, that’s the official name) <code>__set()</code> and <code>__get()</code> to pass variables to the internal repository and then, in the template script, read from it. (A little explanation on magic methods: they are called when you try to read or write to nonexistent properties of the class. You can read more on this topic in the <a href="https://www.php.net/manual/en/language.oop5.overloading.php#language.oop5.overloading.members">chapter on overloading in the official PHP manual</a>.) As a bonus, I’ve added a configurable template directory.

Invoking our library is straightforward. In this example, I’ve invoked two views, although different templates should be used in the actual application, depending on the application’s logic.</p>

### index.php: Controller

<pre><code class="language-php">&lt;?php
include_once('MyView.php');
$t = new MyView();
$t-&gt;friends = array(
    'Rachel', 'Monica', 'Phoebe', 'Chandler', 'Joey', 'Ross'
);
$t-&gt;render('index.phtml');
$t-&gt;render('index.xml');
?&gt;</code></pre>

The templates look like this…

### index.phtml: HTML Template

<pre><code class="language-php">&lt;html&gt;
    &lt;body&gt;
        Names of my friends:
        &lt;ul&gt;
        &lt;?php foreach ($this-&gt;friends as $friend): ?&gt;
            &lt;li&gt;&lt;?=$friend?&gt;&lt;/li&gt;
        &lt;?php endforeach; ?&gt;
        &lt;/ul&gt;
    &lt;/body&gt;
&lt;/html&gt;</code></pre>

### index.xml: XML Template

<pre><code class="language-php">&lt;?='&lt;?xml version="1.0" encoding="utf-8"?&gt;'?&gt;
&lt;myfriends&gt;
    &lt;?php foreach ($this-&gt;friends as $friend): ?&gt;
        &lt;friend&gt;&lt;?=$friend?&gt;&lt;/friend&gt;
    &lt;?php endforeach; ?&gt;
&lt;/myfriends&gt;</code></pre>

If you have basic knowledge of PHP, you can imagine how this works. Some logic is being used to set the variables, to read them from the database and so on, and then these variables are passed to the object of our view class. Next, we can access these variables in the template file, which is in HTML format, and the second one is XML (but could be in any other: JSON, plain text, CSS, JavaScript, etc.).

That’s the main idea behing the MVC model (without the “M,” in this example): the business logic happens in one place, while the content generation is sent to the user (or view) in another place. From one set of variables, you can generate many different views. In the template, you’re using plain PHP to display the variables.</p>

## Twig Library (With Tutorial)

The Twig library basically does the same job as the simple example above, but in a more sophisticated way. It has many useful features that enable you to develop and maintain your projects more easily and quickly.</p>

### Installation

Let’s start this short tutorial with the installation. Twig requires PHP 5.2.4 or above, but I assume that a PHP-enabled HTTP server (such as Apache) is already at your disposal. The easiest way to get it is to clone the repository on GitHub:

<pre><code class="language-php">git clone git://github.com/fabpot/Twig.git</code></pre>

Or you could get it from the SVN repository:

<pre><code class="language-php">svn co https://svn.twig-project.org/trunk/ twig</code></pre>

Alternatively, you could install it using PEAR:

<pre><code class="language-php">pear channel-discover pear.twig-project.org
pear install twig/Twig</code></pre>

Lastly, you could get the file from the <a href="https://www.twig-project.org/installation">project’s download page</a>.</p>

### Configuring the Environment

Once the library is installed, you can start playing with it. I assume you will prepare your own application logic, which is beyond the scope of this article, so we’ll skip to the part where we already have something to display.

First, we’ll need to include the Twig library and register its autoloader:

<pre><code class="language-php">require_once './twig/lib/Twig/Autoloader.php';
Twig_Autoloader::register();</code></pre>

Notice that we have to provide the proper path to the <em>Autoloader.php</em> file, which is in the <code>lib/Twig</code> directory of the downloaded source package. This piece of code enables us to use all of the Twig libraries without having to explicitly include them. You should be familiar with this technique if you use other popular libraries or frameworks (such as Zend Framework and PEAR).

The next essential part of the Twig library is the loader. This is a class that tells the Twig engine how it should load the templates. With the object of this class, we can initialize the main part of the engine, the Twig environment. Here’s an example:

<pre><code class="language-php">$loader = new Twig_Loader_Filesystem('./templates');
$twig = new Twig_Environment($loader, array(
    'cache' =&gt; './tmp/cache',
));</code></pre>

In this example, <code>Twig_Loader_Filesystem</code> is initialized with the directory where templates are stored as a parameter. An instance of the loader class is used to initialize the Twig environment as its first parameter. The second parameter is an array of options. The most important of them are these:

*   `cache`The directory where cached templates will be stored (more on the cache later). If you don’t provide a valid path here, the templates will not be cached (which is the default setting). Remember that you have to set the proper permissions for the cache directory so that your script can write there.
*   `auto_reload`This tells Twig to reload the templates every time they change. If it’s set to `false`, the templates will be reloaded only if you delete the contents of the cache directory. This is useful if you need to improve the performance of your website (and you rarely modify your templates).
*   `autoescape`This determines whether variables are escaped in the view automatically (the default is `true`).

<code>Twig_Loader_Filesystem</code> is the most common way to load the templates. For a parameter, you can provide a single string variable or (if you have two or more directories with template files) an array of strings. In such situations, Twig looks for the requested template files in the same order as the paths appear in the array.

Another loader that you might want to use in certain situations is <code>Twig_Loader_String</code>, which enables you to provide the template directly in the form of a string. This can be useful if you store your templates in some form other than files in a file system (for example, if you generate them dynamically, store them in the database, store them in some cache, etc.).

Twig is able to speed things up by caching your templates. That is, Twig processes the templates not every time you need them, but only once, when it detects that the template’s contents have changed (if you have enabled the <code>auto_reload</code> option). Pure PHP code is generated and stored in the cache directory. (Look into the cache files to learn about Twig’s internals.)

### Templates

So, how do we display our first template? Let’s make it a simple “My name is [your name here]” page, with a list of some other items. First, prepare your template file. It will be very simple, because it contains only the basic output:

<pre><code class="language-markup tmp-xml">&lt;html&gt;
    &lt;head&gt;&lt;title&gt;My first Twig template!&lt;/title&gt;&lt;/head&gt;
    &lt;body&gt;
        My name is {{ name }}.
        My friends are:
        &lt;ul&gt;
        {% for person in friends %}
            &lt;li&gt;{{ person.firstname}} {{ person.lastname }}&lt;/li&gt;
        {% endfor %}
        &lt;/ul&gt;
    &lt;/body&gt;
&lt;/html&gt;</code></pre>

Save this file in the templates directory. The convention is to save a template with the <em>.phtml</em> extension, so let’s save ours as <em>hello.phtml</em>. Now we’ll prepare the script that will display the template. Its content will be as follows:

<pre><code class="language-php">&lt;?php
require_once './twig/lib/Twig/Autoloader.php';
Twig_Autoloader::register();
$loader = new Twig_Loader_Filesystem('./templates');
$twig = new Twig_Environment($loader, array(
    'cache' =&gt; './tmp/cache',
));
$template = $twig-&gt;loadTemplate('hello.phtml');
$params = array(
    'name' =&gt; 'Krzysztof',
    'friends' =&gt; array(
        array(
            'firstname' =&gt; 'John',
            'lastname' =&gt; 'Smith'
        ),
        array(
            'firstname' =&gt; 'Britney',
            'lastname' =&gt; 'Spears'
        ),
        array(
            'firstname' =&gt; 'Brad',
            'lastname' =&gt; 'Pitt'
        )
    )
);
$template-&gt;display($params);
?&gt;</code></pre>

In this code, the Twig autoloader is included and registered. Then, we created the loader from the file system, which looks for the template files in the templates directory in our project’s root. In the next step, the environment is initialized with the previously created loader. We’ve enabled caching as a parameter by providing a path to the cache directory. As a result, the following code is sent to the browser:

<pre><code class="language-markup tmp-xml">&lt;html&gt;
    &lt;head&gt;&lt;title&gt;My first Twig template!&lt;/title&gt;&lt;/head&gt;
    &lt;body&gt;
        My name is Krzysztof.
        My friends are:
        &lt;ul&gt;
            &lt;li&gt;John Smith&lt;/li&gt;
            &lt;li&gt;Britney Spears&lt;/li&gt;
            &lt;li&gt;Brad Pitt&lt;/li&gt;
        &lt;/ul&gt;
    &lt;/body&gt;
&lt;/html&gt;</code></pre>

If you look again at the template, you will notice some basic rules:

*   The `{{ … }}` tag is used to print the variable or expression;
*   The `{% … %}` tag is used for flow-control statements, such as `if` and `foreach`;
*   You can access the array elements by using the `myarray.item` syntax. (It’s actually more sophisticated at the implementation level: it checks for the elements of the array, the object properties and their methods, and it even looks for the methods `getItem` and `isItem` — read more about it in the documentation).

But what if you want to send the browser an XML response rather than an HTML file? Nothing could be simpler. Just prepare the XML template, like so:

<pre><code class="language-markup tmp-xml">&lt;?xml version="1.0" encoding="utf-8"?&gt;
    &lt;helloworld myname="{{ name }}"&gt;
        &lt;friends&gt;
        {% for person in friends %}
            &lt;friend firstname="{{ person.firstname}}" lastname="{{ person.lastname }}"/&gt;
        {% endfor %}
        &lt;/friends&gt;
&lt;/helloworld&gt;</code></pre>

Save it as, say, <em>hello.xml</em> in the templates directory. To generate the result, just load this file instead of <em>index.phtml</em> in the PHP script, and you’re done. (Of course, in a real environment you might want to use more sophisticated logic to differentiate between the XML and HTML output).

This example shows how easy it is to use Twig. In the following examples, I will leave out the whole initialization and rendering phase, just to show the relevant pieces of the template’s code.</p>

### Filters

Filters are a useful concept and are common to many templating engines. Filters are applied to the variable to change its contents and print it to the template. Take the following code:

<pre><code class="language-markup tmp-xml">{{ myvar|upper }}</code></pre>

This will affect the variable being printed, and all lowercase letters will be switched to uppercase. Filters can be chained, too. So, you could strip out any HTML tags and convert the variable to uppercase with following code:

<pre><code class="language-markup tmp-xml">{{ myvar|striptags|upper }}</code></pre>

Filters can also take parameters. An example is the replace filter, whose purpose is obvious:

<pre><code class="language-markup tmp-xml">{{ "I like Twig."|replace({'like':'love', 'Twig':'you'}) }}</code></pre>

The following filters are built in:

*   `date`
*   `format`
*   `replace`
*   `url_encode`
*   `json_encode`
*   `title`
*   `capitalize`
*   `upper`
*   `lower`
*   `striptags`
*   `join`
*   `reverse`
*   `length`
*   `sort`
*   `default`
*   `keys`
*   `escape`
*   `e`
*   `raw`
*   `merge`

Most of these are self-explanatory. You can check the details in the documentation.</p>

### Control Structures

In templates, most of the operations you will be doing will be looping over a set of data (listing some items), sometimes accompanied by conditional statements (<code>if … then</code>). This is why Twig has implemented only <code>for</code> and <code>if</code> control structures, but they are quite powerful.

The <code>for</code> loop was presented in its simplest form in the previous section. Below are some more sophisticated examples.

Here is the code to iterate over a sequence of numbers:

<pre><code class="language-php">{% for i in 0..10 %}
    item number {{ i }}
{% endfor %}</code></pre>

You can do the same with letters:

<pre><code class="language-php">{% for l in 'a'..'z' %}
    {{ l }}
{% endfor %}</code></pre>

You can use variables and filters on both sides of the <code>..</code> operator.

To access the keys of an array, you can use the following:

<pre><code class="language-php">{% for k in myarray|keys %}
    key: {{ k }}
{% endfor %}</code></pre>

To access keys and values at the same time, you can use this:

<pre><code class="language-php">{% for key, val in myarray %}
    key: {{ key }}, val: {{ val }}
{% else %}
    no items in the array
{% endfor %}</code></pre>

Notice the <code>else</code> block. It is rendered when the array is empty and no iteration takes place.

You may have noticed that the author of Twig was highly inspired by the behavior of the <code>for</code> structure in the Python language.

<strong>Important:</strong> you cannot use <code>break</code> or <code>continue</code> statements in the Twig version of the <code>for</code> loop. On the other hand, you do have access to a few useful variables inside the loop:

*   `loop.index`
*   `loop.index0`The iteration number. It is counted from 1 by default, so use `index0` to make the index number start from 0.
*   `loop.revindex`
*   `loop.revindex0`This is the same as `index0` but counted from the end of the loop.
*   `loop.first`
*   `loop.last`This is `true` if it is the first or last iteration in the loop.
*   `loop.length`

The <code>if</code> statement is almost the same as it is in pure PHP. You can use <code>if</code>, <code>else</code> and <code>elseif</code> tags. For example:

<pre><code class="language-php">{% if user.role == 'admin' %}
    Hello, administrator!
{% elseif user.role == 'user' %}
    Hello, user!
{% else %}
    You don't have a role defined.
{% endif %}</code></pre>

As with the <code>for</code> loop, the operators in Twig are highly inspired by the ones in Python. For example, here we’ll check whether <code>John</code> is in the list of friends:

<pre><code class="language-php">{% if 'John' in friends %}</code></pre>

Or you could use a predefined list:

<pre><code class="language-php">{% if 'John' in ['Bob', 'Dave', 'John', 'Mike'] %}</code></pre>

To negate the value, use the word <code>not</code>, like so:

<pre><code class="language-php">{% if 'John' not in friends %}</code></pre>

You may want to use tests in conditional statements, in addition to operators. For example:

<pre><code class="language-php">{% if var is divisibleby(2) %}</code></pre>

Here are the tests that are built in:

*   `divisibleby`
*   `none`
*   `even`
*   `odd`
*   `sameas`
*   `constant`
*   `defined`
*   `empty`

This covers most of the basic syntax of Twig. To go deeper, you should read the extensive documentation.</p>

### Template Inheritance

As the creator of Twig states, template inheritance is the most powerful and important feature of Twig. It lets you define a main template as the base of other templates depending on the business logic. For example, you could define the base template below and save it to the file <em>layout.phtml</em>, in which you might want to define the basic layout of your website.

<pre><code class="language-markup tmp-xml">&lt;html&gt;
    &lt;head&gt;
        &lt;title&gt;{% block title %}My page{% endblock %}&lt;/title&gt;
    &lt;/head&gt;
    &lt;body&gt;
        &lt;div id="left-box"&gt;{% block leftbox %}This is the left box.{% endblock %}&lt;/div&gt;
    &lt;div id="content"&gt;{% block content %}{% endblock %}&lt;/div&gt;
    &lt;/body&gt;
&lt;/html&gt;</code></pre>

Then, by calling the template that extends <em>layout.phtml</em>, you will be able to add blocks containing only content in addition to the base template.

<pre><code class="language-markup tmp-xml">{% extends "layout.phtml" %}
{% block title%}{{ parent() }} - About me{% endblock %}
{% block content %}Lorem ipsum dolor sit amet.{% endblock %}</code></pre>

You can call the parent block using the <code>{{ parent() }}</code> function and extend it. If you don’t call a block (<code>leftbox</code>, in this example), its content will be left intact, as is the case with the parent template.

Template inheritance could help you create a flexible template architecture. Read the documentation to learn the details.</p>

### Incorporating Twig Into an Existing Project

Because Twig is so flexible an engine, there is no one specific way to incorporate it into your project. You just have to place the Twig library somewhere in your project and create directories for the cache and templates. The locations of all of these are up to you. Furthermore, you can define a PHP script as an entry point to your application, or include and instantiate the Twig object in every script in your project.</p>

## Conclusion

I hope you enjoy working with template engines such as Twig and that they increase your productivity and the cleanliness of your code. Good luck!

### Further Reading

Here are some websites you might find useful:

That’s the main idea behing the MVC model (without the “M,” in this example): the business logic happens in one place, while the content generation is sent to the user (or view) in another place. From one set of variables, you can generate many different views. In the template, you’re using plain PHP to display the variables.</p>

## Twig Library (With Tutorial)

The Twig library basically does the same job as the simple example above, but in a more sophisticated way. It has many useful features that enable you to develop and maintain your projects more easily and quickly.</p>

### Installation

Let’s start this short tutorial with the installation. Twig requires PHP 5.2.4 or above, but I assume that a PHP-enabled HTTP server (such as Apache) is already at your disposal. The easiest way to get it is to clone the repository on GitHub:

<pre><code class="language-php">git clone git://github.com/fabpot/Twig.git</code></pre>

Or you could get it from the SVN repository:

<pre><code class="language-php">svn co https://svn.twig-project.org/trunk/ twig</code></pre>

Alternatively, you could install it using PEAR:

<pre><code class="language-php">pear channel-discover pear.twig-project.org
pear install twig/Twig</code></pre>

Lastly, you could get the file from the <a href="https://www.twig-project.org/installation">project’s download page</a>.</p>

### Configuring the Environment

Once the library is installed, you can start playing with it. I assume you will prepare your own application logic, which is beyond the scope of this article, so we’ll skip to the part where we already have something to display.

First, we’ll need to include the Twig library and register its autoloader:

<pre><code class="language-php">require_once './twig/lib/Twig/Autoloader.php';
Twig_Autoloader::register();</code></pre>

Notice that we have to provide the proper path to the <em>Autoloader.php</em> file, which is in the <code>lib/Twig</code> directory of the downloaded source package. This piece of code enables us to use all of the Twig libraries without having to explicitly include them. You should be familiar with this technique if you use other popular libraries or frameworks (such as Zend Framework and PEAR).

The next essential part of the Twig library is the loader. This is a class that tells the Twig engine how it should load the templates. With the object of this class, we can initialize the main part of the engine, the Twig environment. Here’s an example:

<pre><code class="language-php">$loader = new Twig_Loader_Filesystem('./templates');
$twig = new Twig_Environment($loader, array(
    'cache' =&gt; './tmp/cache',
));</code></pre>

In this example, <code>Twig_Loader_Filesystem</code> is initialized with the directory where templates are stored as a parameter. An instance of the loader class is used to initialize the Twig environment as its first parameter. The second parameter is an array of options. The most important of them are these:

*   `cache`The directory where cached templates will be stored (more on the cache later). If you don’t provide a valid path here, the templates will not be cached (which is the default setting). Remember that you have to set the proper permissions for the cache directory so that your script can write there.
*   `auto_reload`This tells Twig to reload the templates every time they change. If it’s set to `false`, the templates will be reloaded only if you delete the contents of the cache directory. This is useful if you need to improve the performance of your website (and you rarely modify your templates).
*   `autoescape`This determines whether variables are escaped in the view automatically (the default is `true`).

<code>Twig_Loader_Filesystem</code> is the most common way to load the templates. For a parameter, you can provide a single string variable or (if you have two or more directories with template files) an array of strings. In such situations, Twig looks for the requested template files in the same order as the paths appear in the array.

Another loader that you might want to use in certain situations is <code>Twig_Loader_String</code>, which enables you to provide the template directly in the form of a string. This can be useful if you store your templates in some form other than files in a file system (for example, if you generate them dynamically, store them in the database, store them in some cache, etc.).

Twig is able to speed things up by caching your templates. That is, Twig processes the templates not every time you need them, but only once, when it detects that the template’s contents have changed (if you have enabled the <code>auto_reload</code> option). Pure PHP code is generated and stored in the cache directory. (Look into the cache files to learn about Twig’s internals.)

### Templates

So, how do we display our first template? Let’s make it a simple “My name is [your name here]” page, with a list of some other items. First, prepare your template file. It will be very simple, because it contains only the basic output:

<pre><code class="language-markup tmp-xml">&lt;html&gt;
    &lt;head&gt;&lt;title&gt;My first Twig template!&lt;/title&gt;&lt;/head&gt;
    &lt;body&gt;
        My name is {{ name }}.
        My friends are:
        &lt;ul&gt;
        {% for person in friends %}
            &lt;li&gt;{{ person.firstname}} {{ person.lastname }}&lt;/li&gt;
        {% endfor %}
        &lt;/ul&gt;
    &lt;/body&gt;
&lt;/html&gt;</code></pre>

Save this file in the templates directory. The convention is to save a template with the <em>.phtml</em> extension, so let’s save ours as <em>hello.phtml</em>. Now we’ll prepare the script that will display the template. Its content will be as follows:

<pre><code class="language-php">&lt;?php
require_once './twig/lib/Twig/Autoloader.php';
Twig_Autoloader::register();
$loader = new Twig_Loader_Filesystem('./templates');
$twig = new Twig_Environment($loader, array(
    'cache' =&gt; './tmp/cache',
));
$template = $twig-&gt;loadTemplate('hello.phtml');
$params = array(
    'name' =&gt; 'Krzysztof',
    'friends' =&gt; array(
        array(
            'firstname' =&gt; 'John',
            'lastname' =&gt; 'Smith'
        ),
        array(
            'firstname' =&gt; 'Britney',
            'lastname' =&gt; 'Spears'
        ),
        array(
            'firstname' =&gt; 'Brad',
            'lastname' =&gt; 'Pitt'
        )
    )
);
$template-&gt;display($params);
?&gt;</code></pre>

In this code, the Twig autoloader is included and registered. Then, we created the loader from the file system, which looks for the template files in the templates directory in our project’s root. In the next step, the environment is initialized with the previously created loader. We’ve enabled caching as a parameter by providing a path to the cache directory. As a result, the following code is sent to the browser:

<pre><code class="language-markup tmp-xml">&lt;html&gt;
    &lt;head&gt;&lt;title&gt;My first Twig template!&lt;/title&gt;&lt;/head&gt;
    &lt;body&gt;
        My name is Krzysztof.
        My friends are:
        &lt;ul&gt;
            &lt;li&gt;John Smith&lt;/li&gt;
            &lt;li&gt;Britney Spears&lt;/li&gt;
            &lt;li&gt;Brad Pitt&lt;/li&gt;
        &lt;/ul&gt;
    &lt;/body&gt;
&lt;/html&gt;</code></pre>

If you look again at the template, you will notice some basic rules:

*   The `{{ … }}` tag is used to print the variable or expression;
*   The `{% … %}` tag is used for flow-control statements, such as `if` and `foreach`;
*   You can access the array elements by using the `myarray.item` syntax. (It’s actually more sophisticated at the implementation level: it checks for the elements of the array, the object properties and their methods, and it even looks for the methods `getItem` and `isItem` — read more about it in the documentation).

But what if you want to send the browser an XML response rather than an HTML file? Nothing could be simpler. Just prepare the XML template, like so:

<pre><code class="language-markup tmp-xml">&lt;?xml version="1.0" encoding="utf-8"?&gt;
    &lt;helloworld myname="{{ name }}"&gt;
        &lt;friends&gt;
        {% for person in friends %}
            &lt;friend firstname="{{ person.firstname}}" lastname="{{ person.lastname }}"/&gt;
        {% endfor %}
        &lt;/friends&gt;
&lt;/helloworld&gt;</code></pre>

Save it as, say, <em>hello.xml</em> in the templates directory. To generate the result, just load this file instead of <em>index.phtml</em> in the PHP script, and you’re done. (Of course, in a real environment you might want to use more sophisticated logic to differentiate between the XML and HTML output).

This example shows how easy it is to use Twig. In the following examples, I will leave out the whole initialization and rendering phase, just to show the relevant pieces of the template’s code.</p>

### Filters

Filters are a useful concept and are common to many templating engines. Filters are applied to the variable to change its contents and print it to the template. Take the following code:

<pre><code class="language-markup tmp-xml">{{ myvar|upper }}</code></pre>

This will affect the variable being printed, and all lowercase letters will be switched to uppercase. Filters can be chained, too. So, you could strip out any HTML tags and convert the variable to uppercase with following code:

<pre><code class="language-markup tmp-xml">{{ myvar|striptags|upper }}</code></pre>

Filters can also take parameters. An example is the replace filter, whose purpose is obvious:

<pre><code class="language-markup tmp-xml">{{ "I like Twig."|replace({'like':'love', 'Twig':'you'}) }}</code></pre>

The following filters are built in:

*   `date`
*   `format`
*   `replace`
*   `url_encode`
*   `json_encode`
*   `title`
*   `capitalize`
*   `upper`
*   `lower`
*   `striptags`
*   `join`
*   `reverse`
*   `length`
*   `sort`
*   `default`
*   `keys`
*   `escape`
*   `e`
*   `raw`
*   `merge`

Most of these are self-explanatory. You can check the details in the documentation.</p>

### Control Structures

In templates, most of the operations you will be doing will be looping over a set of data (listing some items), sometimes accompanied by conditional statements (<code>if … then</code>). This is why Twig has implemented only <code>for</code> and <code>if</code> control structures, but they are quite powerful.

The <code>for</code> loop was presented in its simplest form in the previous section. Below are some more sophisticated examples.

Here is the code to iterate over a sequence of numbers:

<pre><code class="language-php">{% for i in 0..10 %}
    item number {{ i }}
{% endfor %}</code></pre>

You can do the same with letters:

<pre><code class="language-php">{% for l in 'a'..'z' %}
    {{ l }}
{% endfor %}</code></pre>

You can use variables and filters on both sides of the <code>..</code> operator.

To access the keys of an array, you can use the following:

<pre><code class="language-php">{% for k in myarray|keys %}
    key: {{ k }}
{% endfor %}</code></pre>

To access keys and values at the same time, you can use this:

<pre><code class="language-php">{% for key, val in myarray %}
    key: {{ key }}, val: {{ val }}
{% else %}
    no items in the array
{% endfor %}</code></pre>

Notice the <code>else</code> block. It is rendered when the array is empty and no iteration takes place.

You may have noticed that the author of Twig was highly inspired by the behavior of the <code>for</code> structure in the Python language.

<strong>Important:</strong> you cannot use <code>break</code> or <code>continue</code> statements in the Twig version of the <code>for</code> loop. On the other hand, you do have access to a few useful variables inside the loop:

*   `loop.index`
*   `loop.index0`The iteration number. It is counted from 1 by default, so use `index0` to make the index number start from 0.
*   `loop.revindex`
*   `loop.revindex0`This is the same as `index0` but counted from the end of the loop.
*   `loop.first`
*   `loop.last`This is `true` if it is the first or last iteration in the loop.
*   `loop.length`

The <code>if</code> statement is almost the same as it is in pure PHP. You can use <code>if</code>, <code>else</code> and <code>elseif</code> tags. For example:

<pre><code class="language-php">{% if user.role == 'admin' %}
    Hello, administrator!
{% elseif user.role == 'user' %}
    Hello, user!
{% else %}
    You don't have a role defined.
{% endif %}</code></pre>

As with the <code>for</code> loop, the operators in Twig are highly inspired by the ones in Python. For example, here we’ll check whether <code>John</code> is in the list of friends:

<pre><code class="language-php">{% if 'John' in friends %}</code></pre>

Or you could use a predefined list:

<pre><code class="language-php">{% if 'John' in ['Bob', 'Dave', 'John', 'Mike'] %}</code></pre>

To negate the value, use the word <code>not</code>, like so:

<pre><code class="language-php">{% if 'John' not in friends %}</code></pre>

You may want to use tests in conditional statements, in addition to operators. For example:

<pre><code class="language-php">{% if var is divisibleby(2) %}</code></pre>

Here are the tests that are built in:

*   `divisibleby`
*   `none`
*   `even`
*   `odd`
*   `sameas`
*   `constant`
*   `defined`
*   `empty`

This covers most of the basic syntax of Twig. To go deeper, you should read the extensive documentation.</p>

### Template Inheritance

As the creator of Twig states, template inheritance is the most powerful and important feature of Twig. It lets you define a main template as the base of other templates depending on the business logic. For example, you could define the base template below and save it to the file <em>layout.phtml</em>, in which you might want to define the basic layout of your website.

<pre><code class="language-markup tmp-xml">&lt;html&gt;
    &lt;head&gt;
        &lt;title&gt;{% block title %}My page{% endblock %}&lt;/title&gt;
    &lt;/head&gt;
    &lt;body&gt;
        &lt;div id="left-box"&gt;{% block leftbox %}This is the left box.{% endblock %}&lt;/div&gt;
    &lt;div id="content"&gt;{% block content %}{% endblock %}&lt;/div&gt;
    &lt;/body&gt;
&lt;/html&gt;</code></pre>

Then, by calling the template that extends <em>layout.phtml</em>, you will be able to add blocks containing only content in addition to the base template.

<pre><code class="language-markup tmp-xml">{% extends "layout.phtml" %}
{% block title%}{{ parent() }} - About me{% endblock %}
{% block content %}Lorem ipsum dolor sit amet.{% endblock %}</code></pre>

You can call the parent block using the <code>{{ parent() }}</code> function and extend it. If you don’t call a block (<code>leftbox</code>, in this example), its content will be left intact, as is the case with the parent template.

Template inheritance could help you create a flexible template architecture. Read the documentation to learn the details.</p>

### Incorporating Twig Into an Existing Project

Because Twig is so flexible an engine, there is no one specific way to incorporate it into your project. You just have to place the Twig library somewhere in your project and create directories for the cache and templates. The locations of all of these are up to you. Furthermore, you can define a PHP script as an entry point to your application, or include and instantiate the Twig object in every script in your project.</p>

## Conclusion

I hope you enjoy working with template engines such as Twig and that they increase your productivity and the cleanliness of your code. Good luck!

### Further Reading

Here are some websites you might find useful:

*   [Sample code from the Mercurial repository on Bitbucket](https://bitbucket.org/krzysztofr/sm-view)
*   “[Twig Documentation](https://twig.sensiolabs.org/documentation)”
*   "[Twig Documentation - Sandbox extension](https://twig.sensiolabs.org/doc/api.html#sandbox-extension "Twig Documentation - Sandbox extension")"
*   “[Templating Engines in PHP](https://fabien.potencier.org/article/34/templating-engines-in-php)” (a comparison), Fabien Potencier
*   [Documentation for Twig in Symfony 2.0](https://symfony.com/doc/current/book/templating.html)

{{< signature "al" >}}

