---
title: 'How To Create Better Angular Templates With Pug'
slug: angular-templates-pug
author: zara-cooper
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4f816369-bb64-4e13-a9ca-f333a404a1b0/angular-templates-pug.png
date: 2020-05-28T11:00:00.000Z
summary: >-
  Pug is a template engine that allows you to write cleaner templates with less repetition. In Angular, you can use Pug to write component templates and improve a project’s development workflow. In this article, Zara Cooper explains what Pug is and how you can use it in your Angular app.
description: >-
  Pug is a template engine that allows you to write cleaner templates with less repetition. In this article, Zara Cooper explains what Pug is and how you can use it in your Angular app.
categories:
  - Apps
  - Angular
  - JavaScript
---

<p>As a developer, I appreciate how Angular apps are structured and the many options the Angular CLI makes available to configure them. Components provide an amazing means to structure views, facilitate code reusability, interpolation, data binding, and other business logic for views.</p>

<p>Angular CLI supports multiple built-in CSS preprocessor options for component styling like Sass/SCSS, LESS, and Stylus. However, when it comes to templates, only two options are available: HTML and SVG. This is in spite of many more efficient options such as Pug, Slim, HAML among others being in existence.</p>

<p>In this article, I’ll cover how you &mdash; as an Angular developer &mdash; can use Pug to write better templates more efficiently. You’ll learn how to install Pug in your Angular apps and transition existing apps that use HTML to use Pug.</p>

<div class="c-felix-the-cat">
<h4 class="h3">Managing Image Breakpoints</h4>
<p>A built-in Angular feature called <em>BreakPoint Observer</em> gives us a powerful interface for dealing with responsive images. Read more about a service that allows us to serve, transform and manage images in the cloud. <a href="https://www.smashingmagazine.com/2019/02/image-breakpoints-angular/" class="btn btn--medium btn--blue">Read a related article&nbsp;&rarr;</a></p>
</div>

{{% feature-panel %}}

<p>Pug (formerly known as Jade) is a template engine. This means it’s a tool that generates documents from templates that integrate some specified data. In this case, Pug is used to write templates that are compiled into functions that take in data and render HTML documents.</p>

<p>In addition to providing a <strong>more streamlined way to write templates</strong>, it offers a number of valuable features that go beyond just template writing like mixins that facilitate code reusability, enable embedding of JavaScript code, provide iterators, conditionals, and so on.</p>

<p>Although HTML is universally used by many and works adequately in templates, it is not DRY and can get pretty difficult to read, write, and maintain especially with larger component templates. That’s where Pug comes in. With Pug, your templates become simpler to write and read and you can <strong>extend the functionality of your template as an added bonus</strong>. In the rest of this article, I’ll walk you through how to use Pug in your Angular component templates.</p>

## Why You Should Use Pug

<p>HTML is fundamentally repetitive. For most elements you have to have an opening and closing tag which is not DRY. Not only do you have to write more with HTML, but you also have to read more. With Pug, there are no opening and closing angle brackets and no closing tags. You are therefore writing and reading a lot less code.</p>

<p>For example, here’s an HTML table:</p>

<pre><code class="language-html">&lt;table&gt;
   &lt;thead&gt;
       &lt;tr&gt;
           &lt;th&gt;Country&lt;/th&gt;
           &lt;th&gt;Capital&lt;/th&gt;
           &lt;th&gt;Population&lt;/th&gt;
           &lt;th&gt;Currency&lt;/th&gt;
       &lt;/tr&gt;
   &lt;/thead&gt;
   &lt;tbody&gt;
       &lt;tr&gt;
           &lt;td&gt;Canada&lt;/td&gt;
           &lt;td&gt;Ottawa&lt;/td&gt;
           &lt;td&gt;37.59 million&lt;/td&gt;
           &lt;td&gt;Canadian Dollar&lt;/td&gt;
       &lt;/tr&gt;
       &lt;tr&gt;
           &lt;td&gt;South Africa&lt;/td&gt;
           &lt;td&gt;Cape Town, Pretoria, Bloemfontein&lt;/td&gt;
           &lt;td&gt;57.78 million&lt;/td&gt;
           &lt;td&gt;South African Rand&lt;/td&gt;
       &lt;/tr&gt;
       &lt;tr&gt;
           &lt;td&gt;United Kingdom&lt;/td&gt;
           &lt;td&gt;London&lt;/td&gt;
           &lt;td&gt;66.65 million&lt;/td&gt;
           &lt;td&gt;Pound Sterling&lt;/td&gt;
       &lt;/tr&gt;
   &lt;/tbody&gt;
&lt;/table&gt;</code></pre>

<p>This is how that same table looks like in Pug:</p>

<pre><code class="language-pug">table
 thead
   tr
     th Country
     th Capital(s)
     th Population
     th Currency
 tbody
   tr
     td Canada
     td Ottawa
     td 37.59 million
     td Canadian Dollar
   tr
     td South Africa
     td Cape Town, Pretoria, Bloemfontein
     td 57.78 million
     td South African Rand
   tr
     td United Kingdom
     td London
     td 66.65 million
     td Pound Sterling
</code></pre>
     
<p>Comparing the two versions of the table, Pug looks a lot cleaner than HTML and has better code readability. Although negligible in this small example, you write seven fewer lines in the Pug table than in the HTML table. As you create more templates over time for a project, <strong>you end up cumulatively writing less code with Pug</strong>.</p>

<p>Beyond the functionality provided by the Angular template language, Pug extends what you can achieve in your templates. With features (such as mixins, text and attribute interpolation, conditionals, iterators, and so on), you can use Pug to solve problems more simply in contrast to writing whole separate components or import dependencies and set up directives to fulfill a requirement.</p>

## Some Features Of Pug

<p>Pug offers a wide range of features but what features you can use depends on how you integrate Pug into your project. Here are a few features you might find useful.</p>

<ol>
  <li><strong>Adding external Pug files to a template using <code>include</code></strong>.<br /><br />Let’s say, for example, that you’d like to have a more succinct template but do not feel the need to create additional components. You can take out sections from a template and put them in partial templates then include them back into the original template.<br /><br />For example, in this home page component, the ‘About’ and ‘Services’ section are in external files and are included in the home page component.<br />

<pre><code class="language-pug">//- home.component.pug
h1 Leone and Sons
h2 Photography Studio

include partials/about.partial.pug
include partials/services.partial.pug</code></pre>

<div class="break-out">

<pre><code class="language-pug">//- about.partial.pug
h2 About our business
p Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.</code></pre>
</div>

<pre><code class="language-pug">//- services.partial.pug
h2 Services we offer
P Our services include: 
ul  
    li Headshots
    li Corporate Event Photography</code></pre>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b719dad1-34a0-439d-8485-0f0206fc86f8/1-include-angular-templates-pug.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b719dad1-34a0-439d-8485-0f0206fc86f8/1-include-angular-templates-pug.png" sizes="100vw" caption="HTML render of included partial templates example (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b719dad1-34a0-439d-8485-0f0206fc86f8/1-include-angular-templates-pug.png'>Large preview</a>)" alt="HTML render of included partial templates example" >}}
</li>
<li><strong>Reusing code blocks using mixins</strong>.<br /><br />For example, let’s say you wanted to reuse a code block to create some buttons. You’d reuse that block of code using a mixin.<br />

<div class="break-out">

<pre><code class="language-pug">mixin menu-button(text, action)
    button.btn.btn-sm.m-1(‘(click)’=action)&attributes(attributes)= text

+menu-button('Save', 'saveItem()')(class="btn-outline-success")
+menu-button('Update', 'updateItem()')(class="btn-outline-primary")
+menu-button('Delete', 'deleteItem()')(class="btn-outline-danger")
</code></pre>
</div>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/feb4f5ae-e4fd-4681-8d32-db8a91ca81dd/2-mixins-angular-templates-pug.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/feb4f5ae-e4fd-4681-8d32-db8a91ca81dd/2-mixins-angular-templates-pug.png" sizes="100vw" caption="HTML render of menu buttons mixin example (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/feb4f5ae-e4fd-4681-8d32-db8a91ca81dd/2-mixins-angular-templates-pug.png'>Large preview</a>)" alt="HTML render of menu buttons mixin example" >}}
</li>
<li>Conditionals make it <strong>easy to display code blocks and comments</strong> based on whether a condition is met or not.<br />

<pre><code class="language-pug">- var day = (new Date()).getDay()

if day == 0
   p We’re closed on Sundays
else if  day == 6
   p We’re open from 9AM to 1PM
else
   p We’re open from 9AM to 5PM</code></pre>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/983dc17d-1851-496c-8b61-681252a5d470/3-conditionals-angular-templates-pug.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/983dc17d-1851-496c-8b61-681252a5d470/3-conditionals-angular-templates-pug.png" sizes="100vw" caption="HTML render of conditionals example (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/983dc17d-1851-496c-8b61-681252a5d470/3-conditionals-angular-templates-pug.png'>Large preview</a>)" alt="HTML render of conditionals example" >}}
</li>
<li><strong>Iterators such as <code>each</code> and <code>while</code> provide iteration functionality</strong>.<br />

<pre><code class="language-pug">ul
 each item in ['Eggs', 'Milk', 'Cheese']
   li= item

ul
 while n < 5
   li= n++ + ' bottles of milk on the wall'</code></pre>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8882178b-8a35-45d5-b2d8-ba0b12ee7c68/4-iterators-angular-templates-pug.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8882178b-8a35-45d5-b2d8-ba0b12ee7c68/4-iterators-angular-templates-pug.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8882178b-8a35-45d5-b2d8-ba0b12ee7c68/4-iterators-angular-templates-pug.png'>Large preview</a>)" alt="HTML renders of iterators example" >}}

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1f3adf1e-0e25-4193-bb38-f4b6b8356aca/5-iterators-angular-templates-pug.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1f3adf1e-0e25-4193-bb38-f4b6b8356aca/5-iterators-angular-templates-pug.png" sizes="50vw" caption="HTML renders of iterators example (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1f3adf1e-0e25-4193-bb38-f4b6b8356aca/5-iterators-angular-templates-pug.png'>Large preview</a>)" alt="HTML renders of iterators example" >}}
</li>
<li><strong>Inline JavaScript can be written in Pug templates</strong> as demonstrated in the examples above.</li>
<li><strong>Interpolation is possible</strong> and extends to tags and attributes.<br />

<pre><code class="language-pug">- var name = 'Charles'
p Hi! I’m #{name}.

p I’m a #[strong web developer].

a(href='https://about.me/${name}') Get to Know Me</code></pre>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/753477b0-0f41-45b3-aec3-230ebeedc98a/6-interpolation-angular-templates-pug.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/753477b0-0f41-45b3-aec3-230ebeedc98a/6-interpolation-angular-templates-pug.png" sizes="100vw" caption="HTML render of interpolation example (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/753477b0-0f41-45b3-aec3-230ebeedc98a/6-interpolation-angular-templates-pug.png'>Large preview</a>)" alt="HTML render of interpolation example" >}}
</li>
<li><strong>Filters enable the use of other languages in Pug templates</strong>.<br /><br />For example, you can use Markdown in your Pug templates after installing a JSTransformer Markdown module.<br />

<div class="break-out">

<pre><code class="language-markdown">:markdown-it
   # Charles the Web Developer
   ![Image of Charles](https://charles.com/profile.png)

   ## About
   Charles has been a web developer for 20 years at **Charles and Co Consulting.**
</code></pre>
</div>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f6b3523f-41f2-4f52-8ab6-8f323d6c6232/7-filters-angular-templates-pug.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f6b3523f-41f2-4f52-8ab6-8f323d6c6232/7-filters-angular-templates-pug.png" sizes="100vw" caption="HTML render of filter example (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f6b3523f-41f2-4f52-8ab6-8f323d6c6232/7-filters-angular-templates-pug.png'>Large preview</a>)" alt="HTML render of filter example" >}}
</li>
</ol>

<p>These are just a few features offered by Pug. You can find a more expansive list of features in <a href="https://pugjs.org/api/getting-started.html">Pug’s documentation</a>.</p>

{{% ad-panel-leaderboard %}}

## How To Use Pug In An Angular App

<p>For both new and pre-existing apps using Angular CLI 6 and above, you will need to install <code>ng-cli-pug-loader</code>. It’s an Angular CLI loader for Pug templates.</p>
 
### For New Components And Projects

<ol>
<li>Install <code>ng-cli-pug-loader</code>.<br />

<pre><code class="language-bash">ng add ng-cli-pug-loader</code></pre>
</li>
<li>Generate your component according to your preferences.<br /><br />For example, let’s say we’re generating a home page component:<br />

<pre><code class="language-pug">ng g c home --style css -m app</code></pre>
</li>
<li>Change the HTML file extension, <code>.html</code> to a Pug extension, <code>.pug</code>. Since the initial generated file contains HTML, you may choose to delete its contents and start anew with Pug instead. However, HTML can still function in Pug templates so you can leave it as is.</li>
<li>Change the extension of the template to <code>.pug</code> in the component decorator.<br />

<pre><code class="language-pug">@Component({
   selector: 'app-component',
   templateUrl: './home.component.pug',
   styles: ['./home.component.css']
})</code></pre>
</li>
</ol>

### For Existing Components And Projects

<ol>
  <li>Install <code>ng-cli-pug-loader</code>.<br />

<pre><code class="language-pug">ng add ng-cli-pug-loader</code></pre>
</li>
<li>Install the <a href="https://github.com/izolate/html2pug">html2pug CLI tool</a>. This tool will help you convert your HTML templates to Pug.<br />

<pre><code class="language-pug">npm install -g html2pug</code></pre>
</li>
<li>To convert a HTML file to Pug, run:<br />

<pre><code class="language-pug">html2pug -f -c < [HTML file path] > [Pug file path]</code></pre>

Since we’re working with HTML templates and not complete HTML files, we need to pass the <code>-f</code>  to indicate to <code>html2pug</code> that it should not wrap the templates it generates in <code>html</code> and <code>body</code> tags. The <code>-c</code> flag lets <code>html2pug</code> know that attributes of elements should be separated with commas during conversion. I will cover why this is important below.</li>
<li>Change the extension of the template to <code>.pug</code> in the component decorator as described in the <em><a href="#new-components-projects">For New Components and Projects</a></em> section.</li>
<li>Run the server to check that there are no problems with how the Pug template is rendered.<br /><br />If there are problems, use the HTML template as a reference to figure out what could have caused the problem. This could sometimes be an indenting issue or an unquoted attribute, although rare. Once you are satisfied with how the Pug template is rendered, delete the HTML file.</li>
</ol>

### Things To Consider When Migrating From HTML To Pug Templates

<p>You won’t be able to use inline Pug templates with <code>ng-cli-pug-loader</code>. This only renders Pug files and does not render inline templates defined in component decorators. So all existing templates need to be external files. If you have any inline HTML templates, create external HTML files for them and convert them to Pug using <code>html2pug</code>.</p>

<p>Once converted, you may need to fix templates that use binding and attribute directives. <code>ng-cli-pug-loader</code> requires that bound attribute names in Angular be enclosed in single or double quotes or separated by commas. The easiest way to go about this would be to use the <code>-c</code> flag with <code>html2pug</code>. However, this only fixes the issues with elements that have multiple attributes. For elements with single attributes just use quotes.</p>

<p>A lot of the setup described here can be automated using a task runner or a script or a custom Angular schematic for large scale conversions if you choose to create one. If you have a few templates and would like to do an incremental conversion, it would be better to just convert one file at a time.</p>

{{% ad-panel-leaderboard %}}

## Angular Template Language Syntax In Pug Templates

<p>For the most part, Angular template language syntax remains unchanged in a Pug template, however, when it comes to binding and some directives (as described above), you need to use quotes and commas since <code>()</code>, <code>[]</code>, and <code>[()]</code> interfere with the compilation of Pug templates. Here are a few examples:</p>

<div class="break-out">

<pre><code class="language-pug">//- [src], an attribute binding and [style.border], a style binding are separated using a comma. Use this approach when you have multiple attributes for the element, where one or more is using binding.
img([src]='itemImageUrl', [style.border]='imageBorder')

//- (click), an event binding needs to be enclosed in either single or double quotes. Use this approach for elements with just one attribute.
button('(click)'='onSave($event)') Save</code></pre>
</div>

<p>Attribute directives like <code>ngClass</code>, <code>ngStyle</code>, and <code>ngModel</code> must be put in quotes. Structural directives like <code>*ngIf</code>, <code>*ngFor</code>, <code>*ngSwitchCase</code>, and <code>*ngSwitchDefault</code> also need to be put in quotes or used with commas. Template reference variables ( e.g. <code>#var</code> ) do not interfere with Pug template compilation and hence do not need quotes or commas. Template expressions surrounded in <code>{{ }}</code> remain unaffected.</p>

## Drawbacks And Trade-offs Of Using Pug In Angular Templates

<p>Even though Pug is convenient and improves workflows, there are some drawbacks to using it and some trade-offs that need to be considered when using <code>ng-cli-pug-loader</code>.</p>

<p>Files cannot be included in templates using <code>include</code> unless they end in <code>.partial.pug</code> or <code>.include.pug</code> or are called <code>mixins.pug</code>. In addition to this, template inheritance does not work with <code>ng-cli-pug-loader</code> and as a result, using blocks, prepending, and appending Pug code is not possible despite this being a useful Pug feature.</p>

<p>Pug files have to be created manually as Angular CLI only generates components with HTML templates. You will need to delete the generated HTML file and create a Pug file or just change the HTML file extension,  then change the <code>templateUrl</code> in the component decorator. Although this can be automated using a script, a schematic, or a Task Runner, you have to implement the solution.</p>

<p>In larger pre-existing Angular projects, switching from HTML templates to Pug ones involves a lot of work and complexity in some cases. Making the switch will lead to a lot of breaking code that needs to be fixed file by file or automatically using a custom tool. Bindings and some Angular directives in elements need to be quoted or separated with commas.</p>

<p>Developers unfamiliar with Pug have to learn the syntax first before incorporating it into a project. Pug is not just HTML without angle brackets and closing tags and involves a learning curve.</p>

<p>When writing Pug and using its features in Angular templates <code>ng-cli-pug-loader</code> does not give Pug templates access to the component’s properties. As a result, these properties cannot be used as variables, in conditionals, in iterators, and in inline code. Angular directives and template expressions also do not have access to Pug variables. For example, with Pug variables:</p>

<pre><code class="language-pug">//- app.component.pug
- var shoppingList = ['Eggs', 'Milk', 'Flour']

//- will work
ul
   each item in shoppingList
       li= item

//- will not work because shoppingList is a Pug variable
ul
   li(*ngFor="let item of shoppingList") {{item}}</code></pre>

<p>Here’s an example with a property of a component:</p>

<pre><code class="language-pug">//- src/app/app.component.ts
export class AppComponent{
   shoppingList = ['Eggs', 'Milk', 'Flour'];
}</code></pre>

<div class="break-out">

<pre><code class="language-pug">//- app.component.pug 

//- will not work because shoppingList is a component property and not a Pug variable
ul
   each item in shoppingList
       li= item

//- will work because shoppingList is a property of the component
ul
   li(&#42;ngFor="let item of shoppingList") {{item}}</code></pre>
</div>

<p>Lastly, <code>index.html</code> cannot be a Pug template. <code>ng-cli-pug-loader</code> does not support this.</p>

## Conclusion

<p>Pug can be an amazing resource to use in Angular apps but it does require some investment to learn and integrate into a new or pre-existing project. If you’re up for the challenge, you can take a look at <a href="https://pugjs.org/">Pug’s documentation</a> to learn more about its syntax and add it to your projects. Although <code>ng-cli-pug-loader</code> is a great tool, it can be lacking in some areas. To tailor how Pug will work in your project consider creating an Angular schematic that will meet your project’s requirements.</p>

{{< signature "ra, yk, il" >}}
