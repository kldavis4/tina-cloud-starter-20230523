---
title: Client-Side Templating
slug: client-side-templating
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bdcdd86f-a0fa-4e13-90a5-6c148de3193e/abstract-red-yellow-illu-opt.png
date: 2012-12-05T12:53:55.000Z
author: lars-kappert
description: >-
  Using templates in the browser is becoming more and more widespread. Moving
  application logic from the server to the client, and the increasing usage of
  MVC-like patterns (model–view–controller) inspired templates to embrace the
  browser.
categories:
  - Coding
  - JavaScript
  - Browsers
  - Templates
  - HTML
---
Using templates in the browser is becoming more and more widespread. Moving application logic from the server to the client, and the increasing usage of MVC-like patterns (model–view–controller) inspired templates to embrace the browser. This used to be a server-side only affair, but templates are actually very powerful and expressive in client-side development as well.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4464f123-cbf2-4179-94d6-903dbdb9773a/client-side-template.jpg"><img loading="lazy" decoding="async" class="123643" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4464f123-cbf2-4179-94d6-903dbdb9773a/client-side-template.jpg" alt="Client-side templating article image" width="500" height="354" /></a><br>
<em>Image Credit: <a href="https://www.flickr.com/photos/hertzen/4878410201">Viktor Hertz</a></em>

## Why Would You Use It?

In general, leveraging templates is a great way to separate markup and logic in views, and to maximize code reusability and maintainability. With a syntax close to the desired output (i.e. HTML), you have a clear and fast way to get things done. Although templates can be used to output any kind of text, in this article we provide examples using HTML, since that is what we want in client-side development.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [An Introduction To Full-Stack JavaScript](https://www.smashingmagazine.com/2013/11/introduction-to-full-stack-javascript/)
*   [<span class="headline">Journey Through The JavaScript MVC Jungle</span>](https://www.smashingmagazine.com/2012/07/journey-through-the-javascript-mvc-jungle/)
*   [Useful JavaScript Libraries and jQuery Plugins](https://www.smashingmagazine.com/useful-javascript-libraries-jquery-plugins-part-2/)

{{% feature-panel %}}

In today's dynamic applications, the client frequently needs to update the user interface (UI). This might be done by fetching an HTML fragment from the server that can be readily inserted into the document. Yet this requires the server to support delivering such fragments (as opposed to complete pages). Moreover, as a client-side developer who is responsible for the markup, <strong>you want to have full control over your templates</strong>. No need to know anything about Smarty, Velocity, ASP, some other obscure server-side syntax or even worse: dealing with spaghetti code such as HTML containing those infamous <code>&lt;?</code> or <code>&lt;%</code> tags all over the place.

So let's take a fresh look at a viable alternative: client-side templating.</p>

## First Impressions

For starters, I'd like to give a definition of the term "template". Here is a <a href="https://foldoc.org/template">good definition</a> from foldoc:
<blockquote>“A document that contains parameters, identified by some special syntax, that are replaced by actual arguments by the template processing system.”</blockquote>

Let's observe an example, and see what a basic template might look like:

<pre><code class="language-markup tmp-html">&lt;h1&gt;{{title}}&lt;/h1&gt;
&lt;ul&gt;
    {{#names}}
        &lt;li&gt;{{name}}&lt;/li&gt;
    {{/names}}
&lt;/ul&gt;</code></pre>

This probably looks pretty familiar if you know HTML. It contains HTML tags with some placeholders. We will replace them with some actual data. For instance with this simple object:

<pre><code class="language-javascript">var data = {
    "title": "Story",
    "names": [
        {"name": "Tarzan"},
        {"name": "Jane"}
    ]
}</code></pre>

Combining the template and data should result in the following HTML:

<pre><code class="language-markup tmp-html">&lt;h1&gt;Story&lt;/h1&gt;
&lt;ul&gt;
    &lt;li&gt;Tarzan&lt;/li&gt;
    &lt;li&gt;Jane&lt;/ul&gt;
&lt;/ul&gt;</code></pre>

With the template and data separated, it becomes easy to maintain the HTML. For example, changing tags or adding classes will only need changes in the template. Additionally, adding an attribute to repeating elements such as the <code>&lt;li&gt;</code> element only needs to be done once.</p>

## Template Engine

The syntax of the template (i.e. the format of the placeholders such as <code>{{title}}</code>) depends on the <em>template engine</em> you want to use. This engine takes care of parsing the templates, and replacing the placeholders (variables, functions, loops, etc.) with the actual data it is provided.

Some template engines are <strong>logic-less</strong>. This doesn't mean you can only have simple placeholders in a template, but the features are pretty limited to some intelligent tags (i.e. array iteration, conditional rendering, etc.). Other engines are more feature-rich and extensible. Without going into details here, a question to ask yourself is whether and how much logic you allow in your templates.

Although each template engine has its own API, usually you will find methods such as <code>render()</code> and <code>compile()</code>. The <strong>render</strong> process is the creation of the end result by putting the actual data in the template. In other words, the placeholders are replaced with the actual data. And if there is any templating logic, it is executed. To <strong>compile</strong> a template means to parse it, and translate it into a JavaScript function. Any templating logic is translated into plain JavaScript, and data can be fed to the function, which concatenates all the bits and pieces together in an optimized way.</p>

## A Mustache Example

The production of the example above can be performed by using a template engine, e.g. <strong>mustache.js</strong>. This uses the popular <strong>Mustache</strong> templating syntax. More about them, and alternatives, later. Let's take a look at a little JavaScript to produce some results:

<pre><code class="language-markup tmp-html">var template = '&lt;h1&gt;{{title}}&lt;/h1&gt;&lt;ul&gt;{{#names}}&lt;li&gt;{{name}}&lt;/li&gt;{{/names}}&lt;/ul&gt;';
var data = {"title": "Story", "names": [{"name": "Tarzan"}, {"name": "Jane"}]};

var result = Mustache.render(template, data);</code></pre>

Now we want to show this in the page. In plain JavaScript this could be done like this:

<pre><code class="language-javascript">document.body.innerHTML = result;</code></pre>

That's all! You can try the above in your browser by placing the Mustache script before your own code:

<pre><code class="language-markup tmp-html">&lt;script src="https://raw.github.com/janl/mustache.js/master/mustache.js"&gt;&lt;/script&gt;</code></pre>

Or, you can try this example at <a href="https://jsfiddle.net/webpro/huuDd/">jsFiddle</a>.</p>

## Organizing Templates

If you're like me, you probably don't like to have the HTML in one long string. This is hard to read, and hard to maintain. Ideally, we can put our templates in separate files so we still have all the benefits of syntax highlighting, and the ability to properly indent the lines of HTML for readability.

But this leads to another issue. If our project contains a lot of templates, we don't want to load all of those files separately, since this issues a lot of (Ajax) requests. This would be bad for performance.</p>

### Scenario 1: Script Tags

An often seen solution is to put all the templates within <code>&lt;script&gt;</code> tags with an alternative <code>type</code> attribute, e.g. <code>type="text/template"</code> (which is ignored for rendering or parsing by the browser):

<pre><code class="language-markup tmp-html">&lt;script id="myTemplate" type="text/x-handlebars-template"&gt;
    &lt;h1&gt;{{title}}&lt;/h1&gt;
    &lt;ul&gt;
        {{#names}}
            &lt;li&gt;{{name}}&lt;/li&gt;
        {{/names}}
    &lt;/ul&gt;
&lt;/script&gt;</code></pre>

This way, you can put all of your templates in the HTML document and prevent all the extra Ajax requests to those templates.

The content of such a script tag can then be used later in your JavaScript as a template. The following code example, this time using the Handlebars templating engine and a bit of jQuery, uses the previous <code>&lt;script&gt;</code> tag:

<pre><code class="language-javascript">var template = $('#myTemplate').html();
var compiledTemplate = Handlebars.compile(template);
var result = compiledTemplate(data);</code></pre>

You can try this example as well at <a href="https://jsfiddle.net/webpro/9xwum/">jsFiddle</a>.

The result here is the same as in our Mustache example. Handlebars can use Mustache templates as well, so we use the same template here. There is one (important) difference though, which is that Handlebars is using an intermediate step to get the HTML result. It first compiles the template into a JavaScript function (we named it <code>compiledTemplate</code> here). This function is then executed using the data as its only argument, returning the final output.</p>

### Scenario 2: Precompiled Templates

While only one function to perform the template rendering may seem convenient, there are significant advantages to splitting up the compilation and rendering process. Most importantly, this allows for the compilation part to happen on the server-side. We can execute JavaScript on the server (e.g. using Node), and some of the templating engines support this precompilation of templates.

Putting it all together, we can organize and serve a single JavaScript file (say, <code>compiled.js</code>) that contains multiple, precompiled templates. This could roughly look like this:

<pre><code class="language-javascript">var myTemplates = {
    templateA: function() { ….},
    templateB: function() { ….};
    templateC: function() { ….};
};</code></pre>

Then, in the application code we only need to populate the precompiled template with data:

<pre><code class="language-javascript">var result = myTemplates.templateB(data);</code></pre>

This is generally a far better-performing approach than putting templates within <code>&lt;script&gt;</code> tags as discussed before, since the client can skip the compilation part. Depending on your application stack, this approach is not necessarily harder to accomplish, as we'll see next.

<strong>Node.js example</strong>

Any template precompilation script should at least do the following:

*   read the template files,
*   compile the templates,
*   combine the resulting JavaScript functions in one or more files.

The next basic Node.js script does all that (using the Hogan.js templating engine):

<pre><code class="language-javascript">var fs = require('fs'),
    hogan = require('hogan.js');

var templateDir = './templates/',
    template,
    templateKey,
    result = 'var myTemplates = {};';

fs.readdirSync(templateDir).forEach(function(templateFile) {

    template = fs.readFileSync(templateDir + templateFile, 'utf8');
    templateKey = templateFile.substr(0, templateFile.lastIndexOf('.'));

    result += 'myTemplates["'+templateKey+'"] = ';
    result += 'new Hogan.Template(' + hogan.compile(template, {asString: true}) + ');'

});

fs.writeFile('compiled.js', result, 'utf8');</code></pre>

This reads all files in the <code>templates/</code> folder, compiles the templates and writes them to <code>compiled.js</code>.

Note that this is highly unoptimized code, and does not include any error handling. Still, it does the job, and shows that it doesn't require a lot of code to precompile templates.</p>

### Scenario 3: AMD & RequireJS

The Asynchronous Module Definition (AMD) is gaining more and more traction. Decoupled modules are often a great way to organize an application. One of the most popular module loaders is RequireJS. In a module definition, dependencies can be specified, which will be resolved and made available to the actual module (factory).

In the context of templates, RequireJS has a "text" plugin that allows you to specify text-based dependencies. AMD dependencies are treated as JavaScript by default, but templates are just text (e.g. HTML), so we use the plugin for that. For example:

<pre><code class="language-javascript">define(['handlebars', 'text!templates/myTemplate.html'], function(Handlebars, template) {

    var myModule = {

        render: function() {

            var data = {"title": "Story", "names": [{"name": "Tarzan"}, {"name": "Jane"}]};
            var compiledTemplate = Handlebars.compile(template);
            return compiledTemplate(data);

        }
    };

    return myModule;
});</code></pre>

This way, the advantage lies (only) in the ability to organize the templates in separate files. This is nice, but it needs an extra Ajax request to get the template, and it still needs to compile the template client-side. However, the extra request can be removed by using the <code>r.js</code> optimizer that comes with RequireJS. This resolves dependencies, and will "inline" the templates (or any dependency) into this module definition, vastly reducing the number of requests.

The absence of a precompilation step can be solved in a couple of ways. It may come to mind to have the optimizer also precompile the templates (e.g. we could write a plugin for <code>r.js</code>). But that would require a change in the module definition as well, since we would be using a template <em>string</em> before optimization, and a template <em>function</em> afterwards. Yet this would not be terribly hard to deal with, either by checking for this variable type, or by abstracting away this logic (in either the plugin or the application).</p>

### Watching Templates

In both scenarios #2 and #3, we can do even better by treating our templates as uncompiled source files. Just like CoffeeScript, or Less or SCSS files. We can have our template files watched for changes during development, and recompile them automatically when a file is changed, i.e. just like you would compile CoffeeScript into JavaScript. This way, we're always dealing with precompiled templates in our code, and the optimizer effortlessly inlines the precompiled templates in the build process.

<pre><code class="language-javascript">define(['templates/myTemplate.js'], function(compiledTemplate) {

    var myModule = {

        render: function() {

            var data = {"title": "Story", "names": [{"name": "Tarzan"}, {"name": "Jane"}]};
            return compiledTemplate(data);

        };
    };

    return myModule;
}</code></pre>

## Performance Considerations

Rendering <em>UI updates</em> by using client-side templates is often the way to go. Still, the best performance for the initial <em>full page</em> load is achieved by serving that page as a whole. This allows the browser to render the HTML as is without requiring any JavaScript parsing or extra requests for data. This might be a challenge, especially for pages that are both dynamic and require the best initial loading times possible. Then, ideally, templates are being developed and reused on the client and the server to both support the best performance and still be maintainable.

Two questions to consider here are:

*   What part of my application is mostly dynamic, and what part requires the best possible initial loading times?
*   Do you want to move the processing to the client, or should the server do the heavy lifting?

The answer can only be given by actually measuring different approaches. Yet by using precompiled templates, the client usually doesn't have a very hard time rendering them on the fly. And in case you want to reuse templates on the client and server, you will find a logic-less template syntax to be the most versatile.</p>

## Conclusion

We have seen many strengths of client-side templating, including:

*   Application servers and APIs are best at serving just the data (i.e. JSON); client-side templates fit in perfectly.
*   HTML and JavaScript naturally match the skills of client-side developers.
*   Using templates enforces a good practice of separating presentation and logic.
*   The templates can be fully precompiled and cached, this leaves only the actual data to be refreshed from server.
*   Moving the rendering phase from server to client may positively affect performance.

We have been looking at quite some aspects of (client-side) templating. Hopefully by now you have a better understanding of the concept, and why you would use it.

{{< signature "cp" >}}

