---
title: 'Abstracting WordPress Code To Reuse With Other CMSs: Concepts (Part 1)'
slug: abstracting-wordpress-code-cms-concepts
author: leonardolosoviz
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8dbfd2c0-9f3c-4585-8147-119e518cfe11/abstracting-wordpress-code-cms-concepts.png
date: 2019-11-18T12:00:00.000Z
summary: >-
  Making our code CMS as agnostic as possible enables us to easily port our application to another CMS if the need arises. In this article, we will learn how code abstraction works, why it is a good idea, and the key concepts to achieve it.
description: >-
  Making our code CMS as agnostic as possible enables us to easily port our application to another CMS if the need arises. In this article, we will learn how code abstraction works, why it is a good idea, and the key concepts to achieve it.
categories:
  - WordPress
  - CMS
---
Making code that is agnostic of the CMS or framework has several benefits. For instance, through its new content editor Gutenberg, WordPress enables to code components which can be used for other CMSs and frameworks too, such as <a href="https://www.drupal.org/project/gutenberg">for Drupal</a> and <a href="https://github.com/VanOns/laraberg">for Laravel</a>. However, Gutenberg’s emphasis on re-utilization of code is focused on the client-side code of the component (JavaScript and CSS); concerning the component’s backend code (such as the provision of APIs that feed data to the component) there is no pre-established consideration.

Since these CMSs and frameworks (WordPress, Drupal, Laravel) all run on PHP, making their PHP code re-usable too will make it easier to run our components on all these different platforms. As another example, if we ever decide to replace our CMS with another one (as has recently happened that many people decried WordPress after its introduction of Gutenberg), having the application code be agnostic from the CMS simplifies matters: The more CMS-agnostic our application code is, the less effort will be required to port it to other platforms.

Starting with application code built for a specific CMS, the process of transforming it to CMS-agnostic is what, in this article, I will call "abstracting code". The more abstract the code is, the more it can be re-used to work with whichever CMS.

Making the application completely CMS-agnostic is very tough though &mdash; even possibly impossible &mdash; since sooner or later it will need to depend on the specific CMS’s opinionatedness. Then, instead of attempting to achieve 100% code reusability, our goal must simply be to maximize the amount of code that is CMS-agnostic to make it reusable across different CMSs or frameworks (for the context of this article, these 2 terms will be used interchangeably). Then, migrating the application to a different framework will be not without pain, but at least it will be as painless as possible.

{{% feature-panel %}}

The solution to this challenge concerns the architecture of our application: We must keep the core of the application cleanly decoupled from the specifics of the underlying framework, by coding against interfaces instead of implementations. Doing so will grant additional benefits to our codebase: We can then focus our attention almost exclusively on the business logic (which is the real essence and purpose of the application), causing the code to become more understandable and less muddled with the limitations imposed by the particular CMS.

This article is composed of 2 parts: In this first part we will conceptualize and design the solution for abstracting the code from a WordPress site, and on the 2nd part we will implement it. The objective shall be to keep the code ready to be used with <a href="https://symfony.com/">Symfony components</a>, <a href="https://laravel.com/">Laravel framework</a>, and <a href="https://octobercms.com/">October CMS</a>.

## Code Against Interfaces, Rely On Composer, Benefit From Dependency Injection

The design of our architecture will be based on the following pillars:

<ol>
  <li>Code against interfaces, not implementations.</li>
  <li>Create packages, distribute them through Composer.</li>
  <li>Dependency Injection to glue all parts together.</li>
</ol>

Let’s analyze them one by one.

### Code Against Interfaces, Not Implementations

Coding against interfaces is the practice of interacting with a certain piece of code through a contract. A contract, which is set up through an interface from our programming language (PHP in our case since we are dealing with WordPress), establishes the intent of certain functionality, by explicitly stating what functions are available, what inputs are expected for each function, and what each function will return, and it is not concerned with how the functionality must be implemented. Then, our application can be cleanly decoupled from a specific implementation, not needing to know how its internals work, and being able to change to another implementation at any time without having to drastically change code. For instance, our application can store data by interacting with an interface called <code>DataStoreInterface</code> instead of any of its implementations, such as instances of classes <code>DatabaseDataStore</code> or <code>FilesystemDataStore</code>.

In the context of WordPress, this implies that &mdash; by the end of the abstraction &mdash; no WordPress code will be referenced directly, and WordPress itself will simply be a service provider for all the functions that our application needs. As a consequence, we must consider WordPress as a dependency of the application, and not as the application itself.

Contracts and their implementations can be added to packages distributed through Composer and glued together into the application through dependency injection which are the items we will analyze next.

### Create Packages, Distribute Them Through Composer

Remember this: <a href="https://getcomposer.org/">Composer</a> is your friend! This tool, a package manager for PHP, allows any PHP application to easily retrieve packages (i.e. code) from any repository and install them as dependencies.

<p><strong>Note</strong>: <em>I have already described how we can use Composer together with WordPress in <a href="https://www.smashingmagazine.com/2019/03/composer-wordpress/">a previous article</a> I wrote earlier this year.</em></p>

Composer is itself CMS-agnostic, so it can be used for building any PHP application. Packages distributed through Composer, though, may be CMS-agnostic or not. Therefore, our application should depend on CMS-agnostic packages (which will work for any CMS) as much as possible, and when not possible, depend on the corresponding package that works for our specific CMS.

This strategy can be used to code against contracts, as explained earlier on. The packages for our application can be divided into two types: CMS-agnostic and CMS-specific ones. The CMS-agnostic package will contain all the contracts and all generic code, and the application will exclusively interact with these packages. For each CMS-agnostic package containing contracts, we must also create a CMS-specific package containing the implementation of the contracts for the required CMS, which is set into the application by means of dependency injection (which we’ll analyze below).

For example, to implement an API to retrieve posts, we create a CMS-agnostic package called "Posts", with contract <code>PostAPIInterface</code> containing function <code>getPosts</code>, like this:

<pre><code class="language-css">interface PostAPIInterface
{
  public function getPosts($args);
}</code></pre>

This function can be resolved for WordPress through a package called "Posts for WordPress", which resolves the contract through a class <code>WPPostAPI</code>, implementing function getPosts to simply execute WordPress function get_posts, like this:

<pre><code class="language-css">class WPPostAPI implements PostAPIInterface
{
  public function getPosts($args) {
    return get_posts($args);
  }
}</code></pre>

If we ever need to port our application from WordPress to another CMS, we must only implement the corresponding CMS-specific package for the new CMS (e.g. "Posts for October CMS") and update the dependency injection configuration matching contracts to implementations, and that’s it!

<p><strong>Note</strong>: <em>It is a good practice to create packages that only define contracts and nothing else. This way, it is easy for implementers to know exactly what must be implemented.</em></p>

### Dependency Injection To Glue All Parts Together

Dependency injection is a technique that allows declaring which object from the CMS-specific package (aka the "service provider") is implementing which interface from the CMS-agnostic package (aka the "contract"), thus gluing all parts of the application together in a loosely-coupled manner.

Different CMSs or frameworks may already ship with their own implementation of a dependency injection component. For instance, whereas WordPress doesn’t have any, both Symfony and Laravel have their own solutions: <a href="https://symfony.com/components/DependencyInjection">DependencyInjection component</a> and <a href="https://laravel.com/docs/6.x/container">Service Container</a> respectively.

Ideally, we should keep our application free from choosing a specific dependency injection solution, and leave it to the CMS to provide for this. However, dependency injection must be used also to bind together generic contracts and services, and not only those depending on the CMS (for instance, a contract <code>DataStoreInterface</code>, resolved through service provider <code>FilesystemDataStore</code>, may be completely unrelated to the underlying CMS). In addition, a very simple application that does not require an underlying CMS will still benefit from dependency injection. Hence, we are compelled to choose a specific solution for dependency injection.

<p><strong>Note</strong>: <em>When choosing a tool or library, prioritize those ones which implement the corresponding PHP Standards Recommendation (in our case, we are interested in <a href="https://www.php-fig.org/psr/psr-11/">PSR-11</a>), so they can be replaced without affecting the application code as much as possible (in practice, each solution will most likely have a custom initialization, so some re-writing of application code may be unavoidable).</em></p>

{{% ad-panel-leaderboard %}}

## Choosing The Dependency Injection Component

For my application, I have decided to use <a href="https://symfony.com/components/DependencyInjection">Symfony’s DependencyInjection component</a> which, among other great features, can be set-up through YAML and XML configuration files, and it supports <a href="https://symfony.com/doc/current/service_container/autowiring.html">autowiring</a>, which automatically resolves how different services are injected into one another, greatly reducing the amount of configuration needed.

For instance, a service Cache implementing a contract <code>CacheInterface</code>, like this one:

<pre><code class="language-css">namespace MyPackage\MyProject;
class Cache implements CacheInterface
{
  private $cacheItemPool;
  private $hooksAPI;

  public function __construct(
    CacheItemPoolInterface $cacheItemPool, 
    HooksAPIInterface $hooksAPI
  ) {
    $this->cacheItemPool = $cacheItemPool;
    $this->hooksAPI = $hooksAPI;
  }

  // ...
}</code></pre>

... can be set as the default service provider through the following <em>services.yaml</em> configuration file:

<div class="break-out">

<pre><code class="language-css">services:
  _defaults:
    bind:
      MyPackage\MyProject\HooksAPIInterface: '@hooks_api'

  hooks_api:
    class: \MyPackage\MyProject\ContractImplementations\HooksAPI

  cache:
    class: \MyPackage\MyProject\Cache
    public: true
    arguments:
      $cacheItemPool: '@cache_item_pool'

  cache_item_pool:
    class: \Symfony\Component\Cache\Adapter\FilesystemAdapter</code></pre>
</div>

As it can be observed, class <code>cache</code> requires two parameters in its constructor, and these are resolved and provided by the dependency injection component based on the configuration. In this case, while parameter <code>$cacheItemPool</code> is manually set, parameter <code>$hooksAPI</code> is automatically resolved through type-hinting (i.e. matching the expected parameter’s type, with the service that resolves that type). Autowiring thus helps reduce the amount of configuration required to glue the services and their implementations together.

## Make Your Packages As Granular As Possible

Each package must be as granular as possible, dealing with a specific objective, and containing no more or less code than is needed. This is by itself a good practice in order to avoid creating bloated packages and establishing a modular architecture, however, it is mandatory when we do not know which CMS the application will run on. This is because different CMSs are based on different models, and it is not guaranteed that every objective can be satisfied by the CMS, or under what conditions. Keeping packages small and objective then enables to fulfill the required conditions in a progressive manner, or discard using this package only when its corresponding functionality can’t be satisfied by the CMS.

Let’s take an example: If we come from a WordPress mindset, we could initially assume that entities "posts" and "comments" will always be a part of the Content Management System, and we may include them under a package called "CMS core". However, October CMS doesn’t ship with either posts or comments in its core functionality, and these are implemented through plugins. For the next iteration, we may decide to create a package to provide for these two entities, called "Posts and Comments", or even "Posts" under the assumption that comments are dependent on posts and bundled with them. However, once again, the plugins in October CMS don’t implement these two together: There is a plugin implementing posts and another plugin implementing comments (which has a dependency on the posts plugin). Finally, our only option is to implement two separate packages: "Posts" and "Comments", and assign a dependency from the latter to the former one.

Likewise, a post in WordPress contains post meta attributes (i.e. additional attributes to those defined in the database model) and we may assume that every CMS will support the same concept. However, we can’t guarantee that another CMS will provide this functionality and, even if it did, its implementation may be so different than that from WordPress that not the same operations could be applied to the meta attributes.

For example, both WordPress and October CMS have support for post meta attributes. However, whereas WordPress stores each post meta value as a row on a different database table than where the post is stored, October CMS stores all post meta values in a single entry as a serialized JSON object in a column from the post table. As a consequence, WordPress can fetch posts filtering data based on the meta value, but October CMS cannot. Hence, the package "Posts" must not include the functionality for post meta, which must then be implemented on its own package "Post Meta" (satisfiable by both WordPress and October CMS), and this package must not include functionality for querying the meta attributes when fetching posts, which must then be implemented on its own package "Post Meta Query" (satisfiable only by WordPress).

{{% ad-panel-leaderboard %}}

## Identifying Elements That Need To Be Abstracted

We must now identify all the pieces of code and concepts from a WordPress application that need be abstracted for it to run with any other CMS. Digging into an application of mine, I identified the following items:

<ul>
<li>accessing functions</li>
<li>function names</li>
<li>function parameters</li>
<li>states (and other constant values)</li>
<li>CMS helper functions</li>
<li>user permissions</li>
<li>application options</li>
<li>database column names</li>
<li>errors</li>
<li>hooks</li>
<li>routing</li>
<li>object properties</li>
<li>global state</li>
<li>entity models (meta, post types, pages being posts, and taxonomies —tags and categories—)</li>
<li>translation</li>
<li>media</li>
</ul>

As long as it is, this list is not yet complete. There are many other items that need abstraction, which I will not presently cover. Such items include dealing with the location of assets (some framework may require to place image/font/JavaScript/CSS/etc. files on a specific directory) and CLI commands (WordPress has <a href="https://wp-cli.org/">WP-CLI</a>, Symfony has the <a href="https://symfony.com/doc/current/components/console.html">console component</a>, and Laravel has <a href="https://laravel.com/docs/6.x/artisan">Artisan</a>, and there are commands for each of these which could be unified).

In the next (and final) part of this series of articles, we will proceed to implement the abstraction for all the items identified above.

## Evaluating When It Makes Sense To Abstract The Application

Abstracting an application is not difficult, but, as shall be observed in the next article, it involves plenty of work, so we must consider carefully if we really need it or not. Let’s consider the advantages and disadvantages of abstracting the application’s code:

### Advantages

<ul>
  <li>The effort required to port our application to other platforms is greatly reduced.</li>
<li>Because the code reflects our business logic and not the opinionatedness of the CMS, it is more understandable.</li>
<li>The application is naturally organized through packages which provide progressive enhancement of functionalities.</li>
</ul>

### Disadvantages

<ul>
  <li>Extra ongoing work.</li>
  <li>Code becomes more verbose.</li>
  <li>Longer execution time from added layers of code.</li>
</ul>

There is no magic way to determine if we’ll be better off by abstracting our application code. However, as a rule of thumb, I’ll propose the following approach:

<blockquote>Concerning a new project, it makes sense to establish an agnostic architecture, because the required extra effort is manageable, and the advantages make it well worth it; concerning an existing project, though, the one-time effort to abstract it could be very taxing, so we should analyze what is more expensive (in terms of time and energy): the one-time abstraction, or maintaining several codebases.</blockquote>

## Conclusion

Setting-up a CMS-agnostic architecture for our application can allow to port it to a different platform with minimal effort. The key ingredients of this architecture are to code against interfaces, distribute these through granular packages, implement them for a specific CMS on a separate package, and tie all parts together through dependency injection.

Other than a few exceptions (such as deciding to choose Symfony’s solution for dependency injection), this architecture attempts to impose no opinionatedness. The application code can then directly mirror the business logic, and not the limitations imposed by the CMS.

In the next part of this series, we will implement the code abstraction for a WordPress application.

{{< signature "rb, dm, yk, il" >}}
