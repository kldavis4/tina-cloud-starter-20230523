---
title: 'Building An E-Commerce Site With October CMS And Shopaholic'
slug: october-cms-shopaholic
author: leonardolosoviz
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/194edbf4-f7b1-42bf-b3a5-6349503b1d52/octobercms-code-editor.jpg
date: 2020-03-10T11:30:00.000Z
summary: >-
  The Laravel-powered October CMS enables to extend the functionality of the application through the use of plugins. In this article, we will learn how to create an e-commerce site through one of October's most popular plugins, Shopaholic.
description: >-
  The Laravel-powered October CMS enables to extend the functionality of the application through the use of plugins. In this article we will learn how to create an e-commerce site through one of October's most popular plugins, Shopaholic.
categories:
  - CMS
  - PHP
disable_ads: true
disable_panels: true
disable_newsletterbox: true
sponsor:
  title: October CMS
  link: https://octobercms.com/
  image: https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/907dd836-fdd1-4538-a6b1-69d05da8f284/october-cms-logo.png
  description: >-
    This article has been kindly supported by our dear friends at <a href="https://octobercms.com/" style="text-shadow: none;">October CMS</a>, a free open-source, self-hosted CMS platform based on the Laravel PHP Framework. <em>Thank you!</em>
---
<p>October CMS is flourishing: With over 9000 stars in its <a href="https://github.com/octobercms/october">GitHub repo</a>, 2000 forks and 300 contributors, it is becoming a major force in the CMS space. It won the popular vote as the <a href="https://octobercms.com/blog/post/october-cms-voted-best-flat-file-cms-2018">Best Flat-File CMS from 2018</a>, new plugins are published on <a href="https://octobercms.com/plugins">its marketplace</a> almost daily (covering most of the developer needs), and its <a href="https://octobercms.com/partners">network of partners</a> is expanding worldwide. Let's see what it is all about.</p>

<p>Built in PHP and powered by <a href="https://laravel.com">Laravel</a> (one of the most powerful and developer-friendly PHP frameworks), October CMS is a free open-source Content Management System (CMS). It benefits from Laravel's clean code and sound architecture to provide a great developer experience, over which it adds simple and flexible CMS functionality to provide a great user experience. This combination makes it possible to launch new projects in a matter of minutes, without having to build the project from scratch. Due to all these features, October can minimize the costs of developing and maintaining websites, making it particularly valuable to businesses and digital agencies.</p>

<p>Yet, in spite of its power, October CMS is very easy to use. Since its inception, October has strived to be “<a href="https://octobercms.com/about">as simple as possible, but not simpler</a>”. For this reason, it <a href="https://octobercms.com/features">is based</a> on one of the simplest stacks for the web: PHP to render HTML, plus CSS and JS assets. In the words of its creators, October's mission is to prove that “web development is not rocket science”.</p>

<p>In this article, we will do a tour around October CMS: We will first see how to install it, then check some of its coding and usability features in a bit more detail, and finally get our hands dirty implementing an e-commerce website through one of its most popular plugins, <a href="https://octobercms.com/plugin/lovata-shopaholic">Shopaholic</a>.</p>

<div class="c-felix-the-cat">
<h4 class="h3">Recommended YouTube Channel</h4>
<p>Are you looking to learn more about e-commerce development? You can do so with the help of <a href="https://www.youtube.com/playlist?list=PL0AMsY8MeSqRuiySn_9bOiIYlWk3kQMfa">live streams</a> that explain the main aspects of the development process based on the Shopaholic platform for October CMS. <a href="https://www.youtube.com/playlist?list=PL0AMsY8MeSqRuiySn_9bOiIYlWk3kQMfa" class="btn btn--small btn--white btn--white--bordered">Watch&nbsp;&rarr;</a></p>
</div>

## Installing October CMS

<p>Since October CMS runs on PHP, it requires to have a web server running on the computer (if we don't have one yet, <a href="https://www.mamp.info/en/">MAMP</a> can provide one for free, allowing to choose between Apache and Nginx, and it works for both Windows and macOS) and a MySQL server to store the database (which can also be provided by MAMP).</p>

<p>The installation through <a href="https://octobercms.com/docs/setup/installation#wizard-installation">October's wizard</a> doesn't take more than a few minutes: We create a new MySQL database, <a href="https://octobercms.com/download">download</a> and unpack the installer files to our target directory for the website (which must be granted writing permission, and which must be set as document root in the web server for the chosen domain, such as localhost), and then invoke the script file from the web browser. From that moment on the wizard takes over, guiding us through the installation process. The wizard will:</p>

<ol>
<li>Validate if the web server satisfies all the requirements (at least PHP 7.0, and others):<br />

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1a629f0c-d28c-4205-b0df-de028853eea6/october-install-1.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1a629f0c-d28c-4205-b0df-de028853eea6/october-install-1.png" sizes="100vw" caption="System check (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1a629f0c-d28c-4205-b0df-de028853eea6/october-install-1.png'>Large preview</a>)" alt="October CMS installation 1st step: System check" >}}
</li>
<li>Ask for database and site configuration values, and user credentials:<br />

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f81391ad-d534-471e-a9cf-b4d9d19dc557/october-install-2.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f81391ad-d534-471e-a9cf-b4d9d19dc557/october-install-2.png" sizes="100vw" caption="Configuration (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f81391ad-d534-471e-a9cf-b4d9d19dc557/october-install-2.png'>Large preview</a>)" alt="October CMS installation 2nd step: Configuration" >}}
</li>
<li>Ask how to set-up the site: From scratch, already installing a specific theme, or using our own existing <a href="https://octobercms.com/help/site/projects">project</a> (from which our chosen theme and plugins can be automatically installed):<br />

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f0834986-7663-4f30-97db-bd1ca91a104a/october-install-3.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f0834986-7663-4f30-97db-bd1ca91a104a/october-install-3.png" sizes="100vw" caption="Initial setup (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f0834986-7663-4f30-97db-bd1ca91a104a/october-install-3.png'>Large preview</a>)" alt="October CMS installation 3rd step: Initial set-up" >}}
</li>
<li>Next, we click on "Install!", and in a few seconds (depending on our Internet connection speed) the website will be installed and ready to use:<br />

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/54504713-7df5-4f61-b528-1eba65254d7f/october-install-4.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/54504713-7df5-4f61-b528-1eba65254d7f/october-install-4.png" sizes="100vw" caption="Site installed (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/54504713-7df5-4f61-b528-1eba65254d7f/october-install-4.png'>Large preview</a>)" alt="October CMS installation is installed" >}}
<br />In this case, I chose to install it from scratch, under <a href="https://localhost">https://localhost</a>. Browsing to this URL on the browser, we can encounter the October starter demo theme:<br />

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5cf1ff56-8137-43d4-91b7-945c7aaf3876/october-install-5.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5cf1ff56-8137-43d4-91b7-945c7aaf3876/october-install-5.png" sizes="100vw" caption="Browsing the starter demo theme (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5cf1ff56-8137-43d4-91b7-945c7aaf3876/october-install-5.png'>Large preview</a>)" alt="Starter demo theme" >}}
</li>
<li>Navigating to <a href="https://localhost/backend">https://localhost/backend</a> (unless we changed this URL during the installation process) we can log into the administration panel:<br />

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3f153ff0-7f85-4cbc-ba12-8bee81cf2f85/october-install-6.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3f153ff0-7f85-4cbc-ba12-8bee81cf2f85/october-install-6.png" sizes="100vw" caption="Browsing the admin panel (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3f153ff0-7f85-4cbc-ba12-8bee81cf2f85/october-install-6.png'>Large preview</a>)" alt="Admin panel" >}}
</li>
<li>Finally, we delete the installer files from the folder. And voilà, in just a few minutes we have a fully functioning site (well, we still need to enhance it with plugins... we will do that in a while).<br /><br />

Alternatively, we can also <a href="https://octobercms.com/docs/setup/installation#command-line-installation">install October from the command-line interface</a>, by executing:<br />

<pre><code class="language-bash">$ curl -s https://octobercms.com/api/installer | php
</code></pre>
<br />
This method is faster (it can take as little as 10 seconds to install) because it doesn't require to input the database configuration. Hence, it is particularly useful for setting-up October CMS as a flat-file system, i.e. a CMS fully set-up through files stored in the local disk, and without a database.<br />
</li>
</ol>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/45986f78-a4a0-4c70-94b6-adf2f4ae8638/october-install-bash.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/45986f78-a4a0-4c70-94b6-adf2f4ae8638/october-install-bash.png" sizes="100vw" caption="Installing October CMS through the CLI takes no time. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/45986f78-a4a0-4c70-94b6-adf2f4ae8638/october-install-bash.png'>Large preview</a>)" alt="Installation through the Command-Line Interface" >}}

## Templating System

<p>October CMS has a robust templating system to implement layouts, re-use chunks of code and enable dynamic functionality. Its most important elements are the following ones:</p>

<p><a href="https://octobercms.com/docs/cms/pages">Pages</a> are the most basic structure for storing content. These are readily available, since they are shipped as part of the core (blog posts, on the other hand, must be installed <a href="https://octobercms.com/plugin/rainlab-blog">through a plugin</a>). Pages are based on <a href="https://twig.symfony.com/">Twig</a>, which is a modern template engine for PHP (devised by the creators of <a href="https://symfony.com/">Symfony</a>), and compiled to plain optimized PHP code, so they execute very fast.</p>

<p><a href="https://octobercms.com/docs/cms/partials">Partials</a> contain reusable chunks of code that can be used all throughout the website, as to avoid duplicating code on the different pages or layouts. They are particularly useful for navigation menus, testimonials, calls to action, and other common elements.</p>

<p><a href="https://octobercms.com/docs/cms/layouts">Layouts</a> define the scaffolding, or structure, of the page. They define the &lt;html&gt; and &lt;body&gt; HTML elements, and are useful for creating the frame of the site, including the header, footer and sidebars. The actual content in the body is injected by the page.</p>

<p><a href="https://octobercms.com/docs/cms/components">Components</a> are the mechanism to extend functionality in October CMS. Any page, partial or layout can have attached any number of components, which are most commonly provided through plugins, and which are fully configurable. In addition to rendering HTML code on the page, components can also provide services, such as form validation, security check-up, control of user permissions, or others.</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e0cbec55-6883-4c50-8260-c91178969e94/component.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e0cbec55-6883-4c50-8260-c91178969e94/component.png" sizes="100vw" caption="Configuring a component attached to a page. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e0cbec55-6883-4c50-8260-c91178969e94/component.png'>Large preview</a>)" alt="Component configuration" >}}

<p>These elements are all implemented through files living in the website's folder in the local hard drive. As such, it is possible to edit them not only through October CMS' built-in editor, but also from the developer's preferred text editor (Sublime, VS Code, PHPStorm, etc).</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/194edbf4-f7b1-42bf-b3a5-6349503b1d52/octobercms-code-editor.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/194edbf4-f7b1-42bf-b3a5-6349503b1d52/octobercms-code-editor.jpg" sizes="100vw" caption="We can edit elements either through the October CMS' built-in editor or in an external text editor. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/194edbf4-f7b1-42bf-b3a5-6349503b1d52/octobercms-code-editor.jpg'>Large preview</a>)" alt="Editing an element through October CMS' built-in editor and in an external text editor" >}}

<p>Similarly, the October CMS project can be perfectly managed through any version control system, and it can be easily adapted to any existing workflows. For instance, a project can be set-up through continuous integration, deploying it automatically to the server after new code is pushed to the Git repo.</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/95d0ec2a-90ea-4f06-956a-e08fdbedc334/workflow.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/95d0ec2a-90ea-4f06-956a-e08fdbedc334/workflow.png" sizes="100vw" caption="October can be easily managed with Git. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/95d0ec2a-90ea-4f06-956a-e08fdbedc334/workflow.png'>Large preview</a>)" alt="Git workflow" >}}

## October CMS Marketplace

<p>October CMS has a marketplace for <a href="https://octobercms.com/themes">themes</a> (which allow to change the site’s look and feel) and <a href="https://octobercms.com/plugins">plugins</a> (which allow to extend the site’s functionalities), providing both free and paid offerings. By providing themes which can be used to quickly establish and then configure the design of the site, and plugins each of which implements some required functionality for the site, the marketplace ultimately leads to lower costs for creating our projects and reduced time to launch them.</p>

<p>The marketplace has been getting bigger! Following October's growing popularity, its marketplace has received a constant stream of new offerings: It currently boasts 915 plugins, comprising most of the functionalities required for our websites (blogging, SEO, e-commerce, analytics, email, galleries, maps, security, social, user management, and others), and 150+ themes. Both themes and plugins can be submitted to the marketplace by any independent 3rd party developer, company or agency, and they must adhere to <a href="https://octobercms.com/help/guidelines/quality">quality guidelines</a>, which ensures that they are performant and secure.</p>


## Creating An E-Commerce Site Through Shopaholic

<p>Let's get our hands dirty and implement a real-life use case: An e-commerce website! For this, we will install <a href="https://octobercms.com/plugin/lovata-shopaholic">Shopaholic</a>, the most popular plugin to add e-commerce functionality to October CMS, and the free theme <a href="https://octobercms.com/theme/lovata-bootstrap-shopaholic">Bootstrap theme for Shopaholic</a> to quickly bootstrap the site (which will be made to look like this <a href="https://bootstrap.shopaholic.dev/">demo site</a>). Shopaholic is ideal for our needs because it provides a comprehensive e-commerce solution, which includes an ecosystem of extensions (both free and paid ones) to further enhance it. In addition, we can install the core experience for free and only make a one-time payment for the extensions that we need, which will be cheaper than using cloud solutions which have a recurring fee to use. And finally, because we are the full owners of our own on-premise e-commerce website, we can customize it as much as we need to and we own all the data, which is not possible with cloud solutions.</p>

<p>Because of the October marketplace dependency management system, we need only install the theme (the Shopaholic plugin is added as a dependency). Let's proceed to install the theme then: Inside the October CMS admin, we click in the "Front-end theme" section in the Settings, and then click on "Find more themes":</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b05f0e17-27f2-4f01-9eef-bde43ebc4cf8/installing-theme-1.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b05f0e17-27f2-4f01-9eef-bde43ebc4cf8/installing-theme-1.png" sizes="100vw" caption="Front-end theme manager. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b05f0e17-27f2-4f01-9eef-bde43ebc4cf8/installing-theme-1.png'>Large preview</a>)" alt="Front-end theme manager" >}}

<p>Then, we search for theme "Bootstrap theme for Shopaholic" and, upon clicking on the result in the dropdown, it will install the theme and all its dependencies. Once installed, we go back to the Front-end theme manager page and click on the Activate button on the new theme:</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/20369112-d50e-4aef-81ea-fd458e449f9a/october-cms-shopaholic-installing-theme-2.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/20369112-d50e-4aef-81ea-fd458e449f9a/october-cms-shopaholic-installing-theme-2.png" sizes="100vw" caption="Activating the new theme. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/20369112-d50e-4aef-81ea-fd458e449f9a/october-cms-shopaholic-installing-theme-2.png'>Large preview</a>)" alt="Activating the new theme" >}}

<p>After installing the theme and plugins, we will notice a new element "Catalog" on the top menu bar. Clicking on it, we can manage the items in our e-commerce catalog, namely products, categories and brands (these are the core elements; other elements, such as coupons, can be added through extensions). Initially, our catalog will be empty:</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5743a542-74e2-41e5-8697-74915c33902e/catalog.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5743a542-74e2-41e5-8697-74915c33902e/catalog.png" sizes="100vw" caption="Catalog comprising products, categories and brands. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5743a542-74e2-41e5-8697-74915c33902e/catalog.png'>Large preview</a>)" alt="Catalog" >}}

<p>Let's fill it up with some data. We can either create the items one by one or, quite conveniently, import data through CSV and XML files (which allows us to manage a large set of records with Excel or other tools). In our case, since we are creating a demo site for testing purposes, let's install plugin <a href="https://octobercms.com/plugin/lovata-fakedatashopaholic">Fake Data for Shopaholic</a> which provides large sets of mock data and an easy way to import these records to the system. To do this, follow these steps:</p>

<ol>
  <li>Head to Settings => Updates & Plugins in October CMS backend, and install plugin "Fake Data for Shopaholic".</li>
  <li>Head to Dashboard, and click on Manage widgets and then Add widget.</li>
  <li>Select widget "Fake data for Shopaholic", and click on Add.</li>
<li>In the newly added widget, clicking on Generate under section "Generate fake data " will run the process to import the fake data.</li>
</ol>

<p>The last step will ask how many times should the insertion be repeated (as to create bulk and be able to test the performance of the site when loading many records) and which data set (clothes or sneakers):</p>

{{< rimg  href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/58c803ab-1920-49ca-b38f-11fa08e4411e/generate-fake-data-widget.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/58c803ab-1920-49ca-b38f-11fa08e4411e/generate-fake-data-widget.jpg" sizes="70vw" caption="Generating fake data through Laravel's artisan command. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/58c803ab-1920-49ca-b38f-11fa08e4411e/generate-fake-data-widget.jpg'>Large preview</a>)" alt="Generating fake data through Laravel's artisan command" >}}

<p>After running this process, our catalog will look better stocked:</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/02c873a5-86b8-408b-b460-eb131e3e2c5f/catalog-1st-data.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/02c873a5-86b8-408b-b460-eb131e3e2c5f/catalog-1st-data.png" sizes="100vw" caption="Catalog with some mock data. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/02c873a5-86b8-408b-b460-eb131e3e2c5f/catalog-1st-data.png'>Large preview</a>)" alt="Catalog with some mock data" >}}

<p>The next step is to create some promotions. To do this, we click on Promotions on the top menu, then on the Create button, and fill the required information. Once each promotion is created, we must edit it again to add products to it. After creating a few of them, our promotion list will look like this:</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e36a5cf3-9967-43d6-8ae5-1a112b18f29c/promotions.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e36a5cf3-9967-43d6-8ae5-1a112b18f29c/promotions.jpg" sizes="100vw" caption="Creating some promotions. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e36a5cf3-9967-43d6-8ae5-1a112b18f29c/promotions.jpg'>Large preview</a>)" alt="Promotion list" >}}

<p>Now that we have some data, we can finish customizing how our front page will look like. For that, we go to section Settings => Front-end theme => Customize and we complete the information for all tabs (Header, Footer, Social, Main slider, Index page). Once this is ready, our e-commerce site will now be ready:</p>

{{< rimg  href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c8ac8ba3-a20b-48aa-b4e1-6e3b434e1555/site-homepage.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c8ac8ba3-a20b-48aa-b4e1-6e3b434e1555/site-homepage.png" sizes="50vw" caption="Our e-commerce site is ready! (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c8ac8ba3-a20b-48aa-b4e1-6e3b434e1555/site-homepage.png'>Large preview</a>)" alt="Demo e-commerce site" >}}

<p>Clicking on a product, we can see how its page looks like:</p>

{{< rimg  href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dc423986-ec68-4e8e-a827-ab325420fd18/site-product.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dc423986-ec68-4e8e-a827-ab325420fd18/site-product.jpg" sizes="70vw" caption="Product page. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dc423986-ec68-4e8e-a827-ab325420fd18/site-product.jpg'>Large preview</a>)" alt="Product page" >}}

## Auditing The Speed And Reliability Of The E-Commerce Solution

<p>Because we want to sell our products, speed and a good SEO are mandatory, so let's make an audit using Google Chrome's Lighthouse on the product page to make sure it runs fast and that it will score high with search engines. Running the audit against the <a href="https://bootstrap.shopaholic.dev">live demo site</a>, it returns the <a href="https://lighthouse-dot-webdotdevsite.appspot.com//lh/html?url=https://bootstrap.shopaholic.dev/women/jeans-women/two-tone-color-ripped-jeans-blue-4">following report</a>:</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8cc452d4-0b67-4d6a-93e2-852077382631/lighthouse-external-report.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8cc452d4-0b67-4d6a-93e2-852077382631/lighthouse-external-report.jpg" sizes="100vw" caption="Lighthouse report of the product page. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8cc452d4-0b67-4d6a-93e2-852077382631/lighthouse-external-report.jpg'>Large preview</a>)" alt="Lighthouse report of the product page" >}}

<p>Equally important is that the site can withstand heavy load, so that if our product becomes successful and attracts plenty of traffic the server doesn't crash. For this, we can use the <a href="https://loadimpact.com">Load Impact</a> tool to run a load test. Running the test using 50 virtual users for 12 minutes against the live demo site (which is hosted on DigitalOcean with a droplet configuration of Standard 2CPU/4 GB RAM) produced the following results:</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e927b2f9-eda6-4cb5-99df-6f7e9749ccea/loadimpact-report.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e927b2f9-eda6-4cb5-99df-6f7e9749ccea/loadimpact-report.png" sizes="100vw" caption="LoadImpact report of a test load using 50 virtual users during 12 minutes. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e927b2f9-eda6-4cb5-99df-6f7e9749ccea/loadimpact-report.png'>Large preview</a>)" alt="LoadImpact report" >}}

<p>As can be seen, the website was able to sustain an acceptable response time throughout the load test, giving us the confidence that we can trust the e-commerce plugin when we need it the most: When it's time to sell the product.</p>

<p>Finally, we can also feel confident of the reliability of the software, since it is <a href="https://travis-ci.org/oc-shopaholic/oc-shopaholic-plugin">covered by unit tests</a>.</p>


## Adding Extensions To Shopaholic

<p>So far so good. However, as it can be seen on the screenshots from our website, there is still no way for the visitor to buy a product. Let's add this functionality by installing the following free extensions for Shopaholic: <a href="https://octobercms.com/plugin/lovata-ordersshopaholic">Orders</a>, to allow to add products to a cart and make orders, and <a href="https://octobercms.com/plugin/lovata-omnipayshopaholic">Omnipay</a>, to process the payment. (For the other <a href="https://octobercms.com/plugins?search=shopaholic">Shopaholic extensions</a>, if they are not free and authored by LOVATA, you can use coupon "WELCOME" to get a 50% discount the first time you buy them.) To install these extensions, we head to Settings => Updates & Plugins, search for the plugin names, and click on the results to have them installed.</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8e4776a8-bc14-4033-89ce-2b862d1e6c3b/search-shopaholic.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8e4776a8-bc14-4033-89ce-2b862d1e6c3b/search-shopaholic.jpg" sizes="100vw" caption="Searching for 'Shopaholic' displays its plugins. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8e4776a8-bc14-4033-89ce-2b862d1e6c3b/search-shopaholic.jpg'>Large preview</a>)" alt="Plugin installation" >}}

<p>Once installed, we will see a new item Orders in the top navigation, where all orders will be stored, and items Payment methods and Shipping types in the Settings page, to configure the payment gateways (card, cash, etc) and how to deliver the product (by post, etc). We configure these and load again the product page. Now it shows an "Add to cart" button, allowing the user to place an order:</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a6bc2f45-c80d-4fc4-8adb-6ec44f36e536/product-with-cart.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a6bc2f45-c80d-4fc4-8adb-6ec44f36e536/product-with-cart.jpg" sizes="100vw" caption="Product page with cart enabled. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a6bc2f45-c80d-4fc4-8adb-6ec44f36e536/product-with-cart.jpg'>Large preview</a>)" alt="Product page with cart enabled" >}}

<p>After adding several items to the cart, we can proceed to the check-out and complete the order:</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ab58a089-a683-4969-bfb6-a2c68bcb981c/cart.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ab58a089-a683-4969-bfb6-a2c68bcb981c/cart.png" sizes="50vw" caption="Completing the order. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ab58a089-a683-4969-bfb6-a2c68bcb981c/cart.png'>Large preview</a>)" alt="Cart" >}}

<p>Once the user submits the order, the inventory will be automatically taken care of, updating the number of items for each product in stock, and we will receive an email informing us of the new order (if configured to do so). In section Orders on the admin panel, we can find all the information for the order (products sold, buyer information, method of payment and total, and others), and we can complete the transaction.</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/71910089-dce7-4c43-affc-d38635f517cf/orders.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/71910089-dce7-4c43-affc-d38635f517cf/orders.jpg" sizes="100vw" caption="All the information from the order is here. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/71910089-dce7-4c43-affc-d38635f517cf/orders.jpg'>Large preview</a>)" alt="Orders page" >}}

<p>The basic work is done: In barely a few hours we managed to have a fully functional e-commerce sith with October CMS and Shopaholic.</p>

## Creating Our Own Extension

<p>If none of the several <a href="https://octobercms.com/plugins?search=shopaholic">extensions to Shopaholic</a> on the October marketplace provides the functionality needed, we can also create our own extensions.</p>

<p>To do this, if you are comfortable with Object-Oriented Programming and PHP and, more specifically, with Laravel, then you are ready to do it. The <a href="https://shopaholic.one/docs">documentation</a> explains how to add an extension, step by step. For instance, following <a href="https://shopaholic.one/docs#/modules/product/extending/extending?id=add-custom-field">this tutorial</a>, with barely a few lines of code we can add a custom field "rating" to our products:</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/982acbbb-c09f-4f5c-a719-732e8174c283/rating-field.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/982acbbb-c09f-4f5c-a719-732e8174c283/rating-field.png" sizes="100vw" caption="Adding a custom field to the product. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/982acbbb-c09f-4f5c-a719-732e8174c283/rating-field.png'>Large preview</a>)" alt="Editing a product" >}}

<p>We can then retrieve the new "rating" field from the product and display it in the product template:</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/46d301b9-1b10-4fab-8594-547ff2d45ee2/product-with-rating.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/46d301b9-1b10-4fab-8594-547ff2d45ee2/product-with-rating.jpg" sizes="100vw" caption="Displaying a custom field in the product page. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/46d301b9-1b10-4fab-8594-547ff2d45ee2/product-with-rating.jpg'>Large preview</a>)" alt="Product page" >}}

<p>Extending Shopaholic is not difficult and enables us to fully implement our own e-commerce requirements, and personalize the site to suit our brand.</p>

## Conclusion

<p>October CMS is a great candidate for building powerful sites in a very simple manner (showing that “web development is not rocket science”). It delivers the great developer experience granted by Laravel, and its marketplace (which is growing daily) provides a large number of ready-to-use themes and plugins, allowing us to build websites very quickly. One such plugin is Shopaholic, which converts the site into a full-fledged e-commerce platform.</p>

<p>Because of these reasons, building a site with October can be very cost-effective. As a result, it has gained some reputation (by winning the popular vote as best flat-file CMS from 2018) and has increasingly become a tool of choice for businesses and digital agencies crafting sites for their clients.</p>

<p>To find out more from the October community, be welcome to join the <a href="https://octobercms.slack.com/">October CMS Slack workspace</a>, which is where the creators of themes and plugins published in the marketplace hang out, so you can conveniently chat with them to get their help and advice.</p>

<p><a href="https://octobercms.com">Give October a try</a> (<em>it's free!</em>), and let us know how it goes.</p>

{{< signature "ra, yk, il" >}}
