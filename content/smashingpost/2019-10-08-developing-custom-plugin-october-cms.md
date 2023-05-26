---
title: 'Developing A Custom Plugin For October CMS'
slug: developing-custom-plugin-october-cms
author: andriy-haydash
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/826f9d42-61c9-45cf-9ebd-5c1a441891fc/developing-custom-plugin-october-cms.png
date: 2019-10-08T12:30:59+02:00
summary: >-
  If you like writing object-oriented and easy-to-read code, then this article is for you. You’ll learn how to write your own plugin and why October may be a good choice for your next project.
description: >-
  If you like writing object-oriented and easy-to-read code, then this article is for you. You’ll learn how to write your own plugin and why October may be a good choice for your next project.
categories:
  - Plugins
  - CMS
  - PHP
---
Last year, I did some research about new CMS systems in PHP in order to find <a href="https://www.smashingmagazine.com/2019/03/wordpress-october-cms/">a good alternative to WordPress</a>. Ideally, it had to be an open-source solution with a clean and modern codebase.

One of them caught my interest: <a href="https://octobercms.com">October CMS</a>. I tried it and almost instantly liked it. The code structure was really nice and it was easy to write custom plugins.

This article aims to give you an overview of what to expect from the platform and give you a taste of it before you decide to commit to using it.

## Why Choose October As Your CMS Platform?

There are a few main reasons why I have personally decided to use it for my projects.

### Powered By Laravel

October is built on top of the most powerful PHP framework for creating modern web apps: <a href="https://laravel.com/">Laravel</a>. I can say with great confidence that it’s the best. It is very easy to use and understand, and has all the features that a modern framework needs, from routing, object-relational mapping (ORM), authorization, caching, and many others that provide a nice and clear MVC structure. As it is powered by Laravel, October has inherited all those features from its big brother.

### Clean Code And Documentation

Unlike many other CMS solutions, October has a very clean and well-documented codebase. It’s written in using an objectoriented paradigm. Instead of plain old PHP, October uses Twig as its templating engine, which simplifies things for developers. <a href="https://plan.io/blog/technical-documentation/">Technical documentation</a> is also well written, and helps you quickly find answers to most of your questions.

### Great Community

Even though October’s community is not yet that big, it’s very helpful and responsive. There is a public Slack channel you can join, where you’ll find developers happy to assist you in fixing your issue.

### Big Marketplace

Like WordPress and other CMSes, October has a marketplace for themes and plugins. Even though there aren’t that many good themes to choose from, there are over 700 plugins right now, so it’s very likely you’ll be able to add functionality by simply searching for and installing one of them. A great feature of plugins is that they can be easily synchronized between all your projects if you just add your project ID in the admin dashboard.

{{% feature-panel %}}

## PlugIns And Components

Plugins are a foundation of adding new functionality to October. A plugin can consist of multiple files and directories that are responsible for registering custom components, models, updating database structure, or adding translations.

A plugin is usually created in the <em>plugins/</em> directory of the project. Since many plugins are submitted to the marketplace for others to use, each plugin should have a custom namespace, which usually starts with the name of the company or developer that created the plug-in. So, for instance, if your name is *Acme* and you’ve created an awesome plugin called Blog, your plugin will live under the namespace of *Acme\Blog*.

Let me show you how a plugin directory structure might look like:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1c8aa5c5-d391-479a-abb6-c452fd76eced/1-developing-custom-plugin-for-october-cms.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1c8aa5c5-d391-479a-abb6-c452fd76eced/1-developing-custom-plugin-for-october-cms.png" sizes="100vw" caption="Sample plugin directory structure (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1c8aa5c5-d391-479a-abb6-c452fd76eced/1-developing-custom-plugin-for-october-cms.png'>Large preview</a>)" alt="Sample plugin directory structure" >}}

As you can see, there is also a file called <em>plugin.php</em> that is responsible for registering a plugin and all of its components in October CMS.

Another important thing to mention is that not all directories listed above are necessary for a plugin to run. Your plugin could have the following structure and still work perfectly well:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dc31050e-0bc1-42b7-ad2d-bed9fbdf5233/2-developing-custom-plugin-for-october-cms.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dc31050e-0bc1-42b7-ad2d-bed9fbdf5233/2-developing-custom-plugin-for-october-cms.png" sizes="100vw" caption="Simple plugin directory structure (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dc31050e-0bc1-42b7-ad2d-bed9fbdf5233/2-developing-custom-plugin-for-october-cms.png'>Large preview</a>)" alt="Simple plugin directory structure" >}}

Most often, one plugin is built to add only one piece of functionality. For example, the ‘Translate’ plugin is designed to help you translate content on your website into different languages, and provide the multi-language support for the users.

October CMS has a great marketplace where you can find for your needs.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b11104d9-f250-4a71-945d-b9ffbf495a56/3-developing-custom-plugin-for-october-cms.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b11104d9-f250-4a71-945d-b9ffbf495a56/3-developing-custom-plugin-for-october-cms.png" sizes="100vw" caption="October marketplace (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b11104d9-f250-4a71-945d-b9ffbf495a56/3-developing-custom-plugin-for-october-cms.png'>Large preview</a>)" alt="October marketplace" >}}

Unlike WordPress and other popular CMSes, October plugins can also have components. According to October’s documentation, components are “configurable building elements that can be attached to any page, partial or layout.” Examples might include: a contact form, navigation, a list of FAQs and their answers; basically anything that it makes sense to bundle together as one building block that can be reused on multiple pages.

Components are created as a part of a plugin and they exist in the <em>components/</em> subdirectory:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/65f6c57d-ad26-4950-a79e-b5da0e6af00b/4-developing-custom-plugin-for-october-cms.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/65f6c57d-ad26-4950-a79e-b5da0e6af00b/4-developing-custom-plugin-for-october-cms.png" sizes="100vw" caption="Component directory structure (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/65f6c57d-ad26-4950-a79e-b5da0e6af00b/4-developing-custom-plugin-for-october-cms.png'>Large preview</a>)" alt="Component directory structure" >}}

Each component has a PHP file like <em>componentName.php</em> that defines the component, as well as an optional subdirectory for component partials. A component partials folder must have the same name in lowercase as the component itself.

To demonstrate how a component functions, let’s assume that our component is responsible for showing blog posts.

<div class="break-out">

<pre><code class="language-javascript">namespace Acme\Blog\Components;

class BlogPosts extends \Cms\Classes\ComponentBase
{
    public function componentDetails()
    {
        return [
            'name' => 'Blog Posts',
            'description' => 'Displays a collection of blog posts.'
        ];
    }

    // This array becomes available on the page as {{ component.posts }}
    public function posts()
    {
        return ['First Post', 'Second Post', 'Third Post'];
    }
}</code></pre>
</div>

As we can see, the component has two main functions. The first one, <code>componentDetails()</code>, provides information about the component to the administrator who will add and use components on their web pages.

The second function, <code>posts()</code>, returns dummy posts that can then be used inside a component partial (<em>blogposts/default.htm</em> file) like this:

<pre><code class="language-javascript">url = "/blog"

[blogPosts]
==
{% for post in blogPosts.posts %}
    {{ post }}
{% endfor %}</code></pre>

For October CMS to know our component exists, we must register it using our main plugin file inside a function named <code>registerComponents()</code>:

<pre><code class="language-javascript">public function registerComponents()
{
    return [
        'October\Demo\Components\Todo' => 'demoTodo'
    ];
}</code></pre>



## Creating A Custom Contact Form plugin

We’re going to create a custom contact form plug-in. Here are the assumptions about how the plugin should work:

<ul>
<li>The form will have the following fields: First Name, Last Name, Email, Message.</li>
<li>Data will be submitted to the server using Ajax.</li>
<li>After data is submitted, the admin will receive an email with the message sent by the user.</li>
</ul>

For the purpose of this tutorial we will use a fresh installation of October CMS:</li>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5fc677ba-65ca-432f-b955-5e3d185abd00/5-developing-custom-plugin-for-october-cms.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5fc677ba-65ca-432f-b955-5e3d185abd00/5-developing-custom-plugin-for-october-cms.png" sizes="100vw" caption="Default view after fresh installation (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5fc677ba-65ca-432f-b955-5e3d185abd00/5-developing-custom-plugin-for-october-cms.png'>Large preview</a>)" alt="Default view after fresh installation" >}}

Let’s start creating our plugin by running a command in a terminal that will generate the plugin structure: <code>php artisan create:plugin progmatiq.contactform</code>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b8ce9c48-c6cf-4814-b46c-364066118788/6-developing-custom-plugin-for-october-cms.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b8ce9c48-c6cf-4814-b46c-364066118788/6-developing-custom-plugin-for-october-cms.png" sizes="100vw" caption="Creating a new plugin from terminal (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b8ce9c48-c6cf-4814-b46c-364066118788/6-developing-custom-plugin-for-october-cms.png'>Large preview</a>)" alt="Creating a new plugin from terminal" >}}

The <code>progmatiq.contactform</code> argument contains the name of the author (progmatiq) and the name of the plugin (contactform).

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/169a992c-ac82-4a40-a2cf-b6c3609a0ece/7-developing-custom-plugin-for-october-cms.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/169a992c-ac82-4a40-a2cf-b6c3609a0ece/7-developing-custom-plugin-for-october-cms.png" sizes="70vw" caption="New plugin folder structure (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/169a992c-ac82-4a40-a2cf-b6c3609a0ece/7-developing-custom-plugin-for-october-cms.png'>Large preview</a>)" alt="New plugin folder structure" >}}

Now we need to open our <em>plugin.php</em> file and modify the plugin details in the following method:

<div class="break-out">

<pre><code class="language-javascript">public function pluginDetails()
   {
        return [
            'name'        => 'Contact Form',
            'description' => 'A simple contact form plug-in',
            'author'      => 'progmatiq',
            'icon'        => 'icon-leaf'
        ];
    }</code></pre>
</div>

Here are a few other methods that you should take a look at:

<ul>
<li><code>registerComponents()</code><br />Here you can define an array of components that your plugin provides.</li>

<li><code>registerPermissions()</code><br />You can register custom permissions that you can then use later in other areas of the application.</li>

<li><code>registerNavigation()</code><br />You can add a custom menu item with a URL to your admin dashboard menu.</li>
</ul>

{{% ad-panel-leaderboard %}}

Now let’s create our <code>ContactForm</code> component:

<ol>
<li>Make a new folder named <em>components/</em> inside your plug-in’s root directory.</li>
<li>Create a file named <em>contactForm.php</em> inside the <em>components/</em> folder.</li>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f1ab7ac6-169f-42b5-95af-9f642f0ffe76/8-developing-custom-plugin-for-october-cms.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f1ab7ac6-169f-42b5-95af-9f642f0ffe76/8-developing-custom-plugin-for-october-cms.png" sizes="100vw" caption="Creating a new component (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f1ab7ac6-169f-42b5-95af-9f642f0ffe76/8-developing-custom-plugin-for-october-cms.png'>Large preview</a>)" alt="Creating a new component" >}}

<li>Paste the following code that will tell October what our component does. We can do it by creating a method inside our component called <code>componentDetails()</code>.</li>
</ol>

<pre><code class="language-javascript">&lt;?php

namespace Progmatiq\Contactform\Components;

use Cms\Classes\ComponentBase;

class ContactForm extends ComponentBase
{
    public function componentDetails()
    {
        return [
            'name' =&gt; 'Contact Form',
            'description' =&gt; 'A simple contact form'
        ];
    }
}</code></pre>

Now we need to register our component inside the plug-in. To do that, we modify the <code>registerComponents()</code> method:

<div class="break-out">

<pre><code class="language-javascript">    public function registerComponents()
    {
        return [
            'Progmatiq\Contactform\Components\ContactForm' => 'contactForm',
        ];
    }</code></pre>
</div>

This function returns an array of components that our plugin provides. The component’s full class name is a key in this method, and a value is an alias that we’ll use to reference our component inside our Twig templates.

Once we have registered the component, we can create a new contact page and add our component (numbers in the steps refer to the screenshot):

<ol>
<li>In your admin dashboard go to <strong>CMS</strong> (1) > <strong>Pages</strong> (2) and click on + <strong>Add</strong> (3).</li>
<li>Give your page a name and a URL (4).</li>
<li>Name your file (5) and select the default layout (6).</li>
</ol>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a3739e2f-2aef-4799-bde7-6e6b0973344b/9-developing-custom-plugin-for-october-cms.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a3739e2f-2aef-4799-bde7-6e6b0973344b/9-developing-custom-plugin-for-october-cms.png" sizes="100vw" caption="Creating a contact page (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a3739e2f-2aef-4799-bde7-6e6b0973344b/9-developing-custom-plugin-for-october-cms.png'>Large preview</a>)" alt="Creating a contact page" >}}

Let’s add our new component to the page:

<ol>
<li>Click on <strong>Components</strong> in the left menu (1) and then select our “Contact Form” component. Once you click on it (2), it should be added to the page.</li>
<li>We need to place a piece of code that would give our page a headline as well as render the component using the <code>{% component ‘contactForm’ %}</code> Twig directive:</li>
</ol>

<pre><code class="language-javascript">&lt;div class="container"&gt;
    &lt;h1&gt; Contact &lt;/h1&gt;
    {% component 'contactForm' %}
&lt;/div&gt;</code></pre>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/388599b5-c5f7-4d99-8362-72cb8957a04c/10-developing-custom-plugin-for-october-cms.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/388599b5-c5f7-4d99-8362-72cb8957a04c/10-developing-custom-plugin-for-october-cms.png" sizes="100vw" caption="Adding contact form component to contact form page (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/388599b5-c5f7-4d99-8362-72cb8957a04c/10-developing-custom-plugin-for-october-cms.png'>Large preview</a>)" alt="Adding contact form component to contact form page" >}}

If you open your contact page right now, you will see the headline saying “Contact” and nothing else.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5f3f3778-5d98-4468-8f4e-184334893893/11-developing-custom-plugin-for-october-cms.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5f3f3778-5d98-4468-8f4e-184334893893/11-developing-custom-plugin-for-october-cms.png" sizes="100vw" caption="Contact page (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5f3f3778-5d98-4468-8f4e-184334893893/11-developing-custom-plugin-for-october-cms.png'>Large preview</a>)" alt="Contact page" >}}

That’s because our contact form doesn’t have any HTML to render.

We need to create a <em>contactform/default.htm</em> file inside our <em>components/</em> folder.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b8192104-e8d7-4d9b-8999-d81dc5935a84/12-developing-custom-plugin-for-october-cms.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b8192104-e8d7-4d9b-8999-d81dc5935a84/12-developing-custom-plugin-for-october-cms.png" sizes="100vw" caption="Adding an HTML view to our component (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b8192104-e8d7-4d9b-8999-d81dc5935a84/12-developing-custom-plugin-for-october-cms.png'>Large preview</a>)" alt="Adding a html view to our component" >}}

And add the following HTML code to the file:

<div class="break-out">

<pre><code class="language-html">&lt;form method="POST" 
    data-request="onSend"
    data-request-validate
    data-request-success="this.reset(); alert('Thank you for submitting your inquiry')"
&gt;
    &lt;div&gt;
        
        &lt;label for="first_name"&gt;First Name&lt;/label&gt;
        &lt;input type="text" name="first_name" class="form-control"&gt;
        &lt;p data-validate-for="first_name" class="text-danger"&gt;&lt;/p&gt; 
    &lt;/div&gt;

    &lt;div&gt;
        &lt;label for="last_name"&gt;Last Name&lt;/label&gt;
        &lt;input type="text" name="last_name" class="form-control"&gt;

        &lt;p data-validate-for="last_name" class="text-danger"&gt;&lt;/p&gt; 
    &lt;/div&gt;

    &lt;div&gt;
        &lt;label for="email"&gt;Email&lt;/label&gt;
        &lt;input type="text" name="email" class="form-control"&gt;
        &lt;p data-validate-for="email" class="text-danger"&gt;&lt;/p&gt; 
    &lt;/div&gt;

    &lt;div&gt;
        &lt;label for="content"&gt;Content&lt;/label&gt;
        &lt;textarea rows="6" cols="20" name="content" class="form-control"&gt;&lt;/textarea&gt;
        &lt;p data-validate-for="content"  class="text-danger"&gt;&lt;/p&gt; 
    &lt;/div&gt;

    &lt;div&gt;
        &lt;button type="submit" class="btn btn-primary" data-attach-loading&gt;Send&lt;/button&gt;
    &lt;/div&gt;
&lt;/form&gt;</code></pre>
</div>

Most of this code is pretty straightforward. However, it is flavored with special data-* attributes that October <a href="https://octobercms.com/docs/ajax/attributes-api">allows us to use</a>:

<ol>
  <li><code>&lt;form&gt;</code> tag has three special attributes:
<ul>
  <li><code>data-request="onSend"</code>. This attribute tells October that the <code>onSend</code> function from our component (that we’re going to create next) has to be called when the form is submitted using Ajax.</li>
  <li><code>data-request-validate</code> will enable form Ajax validation using errors that will be sent from the server if the form is invalid.</li>
<li><code>data-request-success="this.reset(); alert('Thank you for submitting your inquiry')"</code> clears the form and then triggers the alert message if the request was successful and no validation or server-side errors were present.</li>
    </ul></li>
<li>Every input has a following block that is responsible for displaying validation errors returned by the server for that given input:</li>

<pre><code class="language-html">&lt;p data-validate-for="content"  class="text-danger"&gt;&lt;/p&gt;</code></pre>
<li>The submit button has the <code>data-attach-loading</code> attribute, which will add a spinner and disable the button while the request is being processed by the server. This is done in order to prevent the user submitting a form again until the previous request is complete.</li>
</ol>



And here is how our page looks now:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/23d4baed-8745-4592-ba91-abee7cadbf67/13-developing-custom-plugin-for-october-cms.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/23d4baed-8745-4592-ba91-abee7cadbf67/13-developing-custom-plugin-for-october-cms.png" sizes="100vw" caption="Contact page view (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/23d4baed-8745-4592-ba91-abee7cadbf67/13-developing-custom-plugin-for-october-cms.png'>Large preview</a>)" alt="Contact page view" >}}

Let’s go back to our <em>contactForm.php</em> component and create the <code>onSend()</code> as well as <code>validate()</code> helper method that will be responsible for handling form submission:

<div class="break-out">

<pre><code class="language-javascript">public function onSend()
    {
        // Get request data
        $data = \Input::only([
            'first_name',
            'last_name',
            'email',
            'content'
        ]);

        // Validate request
        $this->validate($data);

        // Send email
        $receiver = 'admin@gmail.com';

        \Mail::send('progmatiq.contact::contact', $data, function ($message) use ($receiver) {
            $message->to($receiver);
        });
    }

    protected function validate(array $data) 
    {
        // Validate request
        $rules = [
            'first_name' => 'required|min:3|max:255',
            'last_name' => 'required|min:3|max:255',
            'email' => 'required|email',
            'content' => 'required',
        ];

        $validator = \Validator::make($data, $rules);

        if ($validator->fails()) {
            throw new ValidationException($validator);
        }
    }
</code></pre>
</div>

The first thing we’re doing is getting data from the request and validating it using the <code>validate()</code> helper method. (<a href="https://octobercms.com/docs/services/validation#available-validation-rules">All the available validation rules you can use can be found in the documentation</a>.) If validation fails, the <code>validate()</code> method will throw the <code>ValidationException</code> an exception and code execution will stop, and the server will respond with status code <code>406</code> and with validation messages.

If validation succeeds, then we will send an email to our admin.

<p><strong>Note</strong>: <em>For simplicity, I’ve assumed that the email we want to send the submission to is admin@gmail.com. Make sure to use your own email!</em></p>

{{% ad-panel-leaderboard %}}

Here is the full code of your <em>contactForm.php</em> plug-in:

<div class="break-out">

<pre><code class="language-javascript">&lt;?php

namespace Progmatiq\Contactform\Components;

use Cms\Classes\ComponentBase;
use October\Rain\Exception\ValidationException;

class ContactForm extends ComponentBase
{
    public function componentDetails()
    {
        return [
            'name' => 'Contact Form',
            'description' => 'A simple contact form'
        ];
    }

    public function onSend()
    {
        // Get request data
        $data = \Input::only([
            'first_name',
            'last_name',
            'email',
            'content'
        ]);

        // Validate request
        $this->validate($data);

        // Send email
        $receiver = 'admin@gmail.com';

        \Mail::send('progmatiq.contact::contact', $data, function ($message) use ($receiver) {
            $message->to($receiver);
        });
    }

    protected function validate(array $data) 
    {
        // Validate request
        $rules = [
            'first_name' => 'required|min:3|max:255',
            'last_name' => 'required|min:3|max:255',
            'email' => 'required|email',
            'content' => 'required',
        ];

        $validator = \Validator::make($data, $rules);

        if ($validator->fails()) {
            throw new ValidationException($validator);
        }
    }
}
</code></pre>
</div>

As you can see, the first argument that the <code>Mail::send()</code> function accepts is the name of the email template that will be rendered for the email body. We need to create it in the admin panel. Go to <strong>Settings > Mail Templates</strong> and click on the <strong>New Template</strong> button. Then fill out the form as it is shown on the screen below:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d9543a33-c89f-46cf-a8e6-b6b0c4889735/14-developing-custom-plugin-for-october-cms.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d9543a33-c89f-46cf-a8e6-b6b0c4889735/14-developing-custom-plugin-for-october-cms.png" sizes="100vw" caption="Adding new email template (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d9543a33-c89f-46cf-a8e6-b6b0c4889735/14-developing-custom-plugin-for-october-cms.png'>Large preview</a>)" alt="Adding new email template" >}}

Here is the body of the email that we’re going to be using:

<pre><code class="language-html">You have received a new contact inquiry

**First Name**:
{{ first_name }}
***
**Last Name**:
{{ last_name }}
***
**Email**:
{{ email }}
***
**Message**:
{{ content }}
***</code></pre>

Now save the email template. The next thing we need to do is configure the SMTP server that will send emails.

Go to <strong>Settings > Mail Configuration</strong> and fill out all the settings.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3b72eaad-c10c-4c86-9b5c-f7c9b7601e99/15-developing-custom-plugin-for-october-cms.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3b72eaad-c10c-4c86-9b5c-f7c9b7601e99/15-developing-custom-plugin-for-october-cms.png" sizes="100vw" caption="Email server configuration (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3b72eaad-c10c-4c86-9b5c-f7c9b7601e99/15-developing-custom-plugin-for-october-cms.png'>Large preview</a>)" alt="Email server configuration" >}}

Obviously, I won’t share my personal configuration. Use your own settings. 😉

At this stage we have everything ready to start testing our contact form component.

First, let’s check if validation works when we leave the “Content” field empty and input an invalid email:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/88b6fa7a-9f40-440d-9cb4-11d3fbf71726/16-developing-custom-plugin-for-october-cms.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/88b6fa7a-9f40-440d-9cb4-11d3fbf71726/16-developing-custom-plugin-for-october-cms.png" sizes="100vw" caption="Contact form validation (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/88b6fa7a-9f40-440d-9cb4-11d3fbf71726/16-developing-custom-plugin-for-october-cms.png'>Large preview</a>)" alt="Contact form validation" >}}

Validation works as expected. Let’s now input correct data and see if the email will be sent successfully to our admin.

Here is the email that *admin@gmail.com* will receive:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/99aa8f3f-c610-478e-bc04-df757420d914/17-developing-custom-plugin-for-october-cms.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/99aa8f3f-c610-478e-bc04-df757420d914/17-developing-custom-plugin-for-october-cms.png" sizes="100vw" caption="Contact form submission email (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/99aa8f3f-c610-478e-bc04-df757420d914/17-developing-custom-plugin-for-october-cms.png'>Large preview</a>)" alt="Contact form submission email" >}}

After the form is submitted successfully, the user will see an alert message informing him that the operation was successful:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0d95de27-7408-4224-869f-571b4276e7e2/18-developing-custom-plugin-for-october-cms.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0d95de27-7408-4224-869f-571b4276e7e2/18-developing-custom-plugin-for-october-cms.png" sizes="100vw" caption="Successful submission of contact form (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0d95de27-7408-4224-869f-571b4276e7e2/18-developing-custom-plugin-for-october-cms.png'>Large preview</a>)" alt="Successful submission of contact form" >}}

## Conclusion

In this tutorial, we’ve covered what a plugin and a component are and how to use them with October CMS.

Don’t be afraid to create a custom plugin for your project if you can’t find an existing one that fits your needs. It’s not that difficult and you have full control over it, and you can update or extend it at any time. Even creating a simple contact form plugin like we’ve done today can be useful if you want to then integrate it with other services like Mailchimp or HubSpot.

I hope this tutorial was helpful to you. If you have any questions, don’t hesitate to ask in the comments section below.

{{< signature "dm, yk, il" >}}
