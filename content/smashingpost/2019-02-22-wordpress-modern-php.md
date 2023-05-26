---
title: 'Improving WordPress Code With Modern PHP'
slug: wordpress-modern-php
author: leonardolosoviz
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d53ca6e0-f7bc-4964-ae3e-0bc0449e9025/wordpress-modern-php-losoviz.png
date: 2019-02-22T13:00:38+01:00
summary: >-
  Due to backwards compatibility, WordPress hasn’t taken advantage of new PHP features released after PHP 5.2.4. Fortunately, WordPress will soon require PHP 5.6+ and even PHP 7.0+ not long after that. This article makes a tour of the PHP features newly-available to WordPress, and attempts to suggest how these can be used to produce better software.
description: >-
  This article makes a tour of the PHP features newly-available to WordPress, and attempts to suggest how these can be used to produce better software.
categories:
  - WordPress
  - PHP
---
WordPress was born fifteen years ago, and because it has historically preserved backwards compatibility, newer versions of its code couldn’t make full use of the latest capabilities offered by the newer versions of PHP. While the latest version of PHP is 7.3.2, [WordPress still offers support up to PHP 5.2.4](https://wordpress.org/about/requirements/).

But those days will soon be over! WordPress will be [upgrading](https://make.wordpress.org/core/2018/12/08/updating-the-minimum-php-version/) its minimum PHP version support, bumping up to PHP 5.6 in April 2019, and PHP 7 in December 2019 (if everything goes according to plan). We can then finally start using PHP’s imperative programming capabilities without fear of breaking our clients' sites. Hurray!

Because WordPress' fifteen years of functional code have influenced how developers have built with WordPress, our sites, themes and plugins may be littered with less-than-optimal code that can gladly receive an upgrade.

This article is composed of two parts:

1. **Most relevant new features**  
Further features have been added to PHP versions 5.3, 5.4, 5.5, 5.6 and 7.0 (notice that [there is no PHP 6](https://en.wikipedia.org/wiki/PHP#PHP_6_and_Unicode)) and we’ll explore the most relevant ones.
2. **Building better software**  
We’ll take a closer look through these features and how they are able to help us build better software.

Let’s start by exploring PHP’s "new" features.

{{% feature-panel %}}

## Classes, OOP, SOLID And Design Patterns

[Classes and objects](https://secure.php.net/manual/en/language.oop5.php) were added to PHP 5, so WordPress already makes use of these features, however, not very extensively or comprehensively: The paradigm of coding in WordPress is mostly [functional programming](https://en.wikipedia.org/wiki/Functional_programming) (performing computations by calling functions devoid of application state) instead of [object-oriented programming (OOP)](https://en.wikipedia.org/wiki/Object-oriented_programming) (performing computations by manipulating objects' state). Hence I also describe classes and objects and how to use them through OOP.

OOP is ideal for producing modular applications: Classes allow the creation of components, each of which can implement a specific functionality and interact with other components, and can provide customization through its [encapsulated properties](https://secure.php.net/manual/en/language.oop5.properties.php) and [inheritance](https://secure.php.net/manual/en/language.oop5.inheritance.php), enabling a high degree of code reusability. As a consequence, the application is cheaper to test and maintain, since individual features can be isolated from the application and dealt with on their own; there is also a boost of productivity since the developer can use already-developed components and avoid reinventing the wheel for each application.

A class has properties and functions, which can be given visibility by using`private` (accessible only from within the defining class), `protected` (accessible from within the defining class and its ancestor and inheriting classes) and `public` (accessible from everywhere). From within a function, we can access the class' properties by prepending their names with `$this->`:

<pre><code class="language-php">class Person {

  protected $name;

  public function __construct($name) {
    $this->name = $name;
  }

  public function getIntroduction() {
    return sprintf(
      __('My name is %s'),
      $this->name
    );
  }
}
</code></pre>

A class is instantiated into an object through the `new` keyword, after which we can access its properties and functions through `->`:

<pre><code class="language-php">$person = new Person('Pedro');
echo $person->getIntroduction();
// This prints "My name is Pedro"
</code></pre>

An inheriting class can override the `public` and `protected` functions from its ancestor classes, and access the ancestor functions by prepending them with `parent::`:

<pre><code class="language-php">class WorkerPerson extends Person {

  protected $occupation;

  public function __construct($name, $occupation) {

    parent::__construct($name);
    $this->occupation = $occupation;
  }

  public function getIntroduction() {
    return sprintf(
      __('%s and my occupation is %s'),
      parent::getIntroduction(),
      $this->occupation
    );
  }
}

$worker = new WorkerPerson('Pedro', 'web development');
echo $worker->getIntroduction();
// This prints "My name is Pedro and my occupation is web development"
</code></pre>

A method can be made `abstract`, meaning that it must be implemented by an inheriting class. A class containing an `abstract` method must be made `abstract` itself, meaning that it cannot instantiated; only the class implementing the abstract method can be instantiated:

<pre><code class="language-php">abstract class Person {

  abstract public function getName();

  public function getIntroduction() {
    return sprintf(
      __('My name is %s'),
      $this->getName()
    );
  }
}
// Person cannot be instantiated

class Manuel extends Person {

  public function getName() {
    return 'Manuel';
  }
}

// Manuel can be instantiated
$manuel = new Manuel();
</code></pre>

Classes can also define `static` methods and properties, which live under the class itself and not under an instantiation of the class as an object. These are accessed through `self::` from within the class, and through the name of the class + `::` from outside it:

<pre><code class="language-php">class Factory {

  protected static $instances = [];
  public static function registerInstance($handle, $instance) {
    self::$instances[$handle] = $instance;
  }
  public static function getInstance($handle) {
    return self::$instances[$handle];
  }
}

$engine = Factory::getInstance('Engine');
</code></pre>

To make the most out of OOP, we can use the [SOLID](https://scotch.io/bar-talk/s-o-l-i-d-the-first-five-principles-of-object-oriented-design) principles to establish a sound yet easily customizable foundation for the application, and [design patterns](https://designpatternsphp.readthedocs.io/) to solve specific problems in a tried-and-tested way. Design patterns are standardized and well documented, enabling developers to understand how different components in the application relate to each other, and provide a way to structure the application in an orderly fashion which helps avoid the use of global variables (such as `global $wpdb`) that pollute the global environment.

{{% ad-panel-leaderboard %}}

## Namespaces

[Namespaces](https://secure.php.net/manual/en/language.namespaces.rationale.php) were added to PHP 5.3, hence they are currently missing altogether from the WordPress core.

Namespaces allow organizing the codebase structurally to avoid conflicts when different items have the same name &mdash; in a fashion similar to operating system directories which allow to have different files with the same name as long as they are stored in different directories. Namespaces do the same encapsulation trick for PHP items (such as classes, traits, and interfaces) avoiding collisions when different items have the same name by placing them on different namespaces.

Namespaces are a must when interacting with third-party libraries since we can’t control how their items will be named, leading to potential collisions when using standard names such as "File", "Logger" or "Uploader" for our items. Moreover, even within a single project, namespaces prevent class names from becoming extremely long as to avoid clashes with other classes, which could result in names such as "MyProject_Controller_FileUpload".

Namespaces are defined using the keyword `namespace` (placed on the line immediately after the opening `<?php`) and can span several levels or subnamespaces (similar to having several subdirectories where placing a file), which are separated using a `\`:

<pre><code class="language-php">&lt;?php
namespace CoolSoft\ImageResizer\Controllers;

class ImageUpload {

}
</code></pre>

To access the above class, we need to fully qualify its name including its namespace (and starting with `\`):

<pre><code class="language-php">$imageUpload = new \CoolSoft\ImageResizer\Controllers\ImageUpload();
</code></pre>

Or we can also import the class into the current context, after which we can reference the class by its name directly:

<pre><code class="language-php">use CoolSoft\ImageResizer\Controllers\ImageUpload;
$imageUpload = new ImageUpload();
</code></pre>

By naming namespaces following established conventions, we can get additional benefits. For instance, by following the PHP Standards Recommendation [PSR-4](https://www.php-fig.org/psr/psr-4/), the application can use [Composer’s autoloading mechanism](https://getcomposer.org/doc/01-basic-usage.md#autoloading) for loading files, thus decreasing complexity and adding frictionless interoperability among dependencies. This convention establishes to include the vendor name (e.g. the company’s name) as the top subnamespace, optionally followed by the package name, and only then followed by an internal structure in which each subnamespace corresponds to a directory with the same name. The result maps 1 to 1 the physical location of the file in the drive with the namespace of the element defined in the file.

{{% ad-panel-leaderboard %}}

## Traits

[Traits](https://secure.php.net/manual/en/language.oop5.traits.php) were added to PHP 5.4, hence they are currently missing altogether from the WordPress core.

PHP supports [single inheritance](https://en.wikipedia.org/wiki/Inheritance_(object-oriented_programming)#Types), so a subclass is derived from a single parent class, and not from multiple ones. Hence, classes that do not extend from one another can’t reuse code through class inheritance. Traits is a mechanism that enables horizontal composition of behavior, making it possible to reuse code among classes which live in different class hierarchies.

A trait is similar to a class, however, it can’t be instantiated on its own. Instead, the code defined inside a trait can be thought of as being "copied and pasted" into the composing class on compilation time.

A trait is defined using the `trait` keyword, after which it can be imported to any class through the `use` keyword. In the example below, two completely unrelated classes `Person` and `Shop` can reuse the same code through a trait `Addressable`:

<pre><code class="language-php">trait Addressable {

  protected $address;

  public function getAddress() {
    return $this->address;
  }

  public function setAddress($address) {
    $this->address = $address;
  }
}

class Person {

  use Addressable;
}

class Shop {

  use Addressable;
}

$person = new Person('Juan Carlos');
$person->setAddress('Obelisco, Buenos Aires');
</code></pre>

A class can also compose more than one trait:

<pre><code class="language-php">trait Exportable {

  public class exportToCSV($filename) {
    // Iterate all properties and export them to a CSV file
  }
}

class Person {

  use Addressable, Exportable;
}
</code></pre>

Traits can also be [composed of other traits](https://secure.php.net/manual/en/language.oop5.traits.php#language.oop5.traits.composition), [define abstract methods](https://secure.php.net/manual/en/language.oop5.traits.php#language.oop5.traits.abstract), and offer a [conflict resolution mechanism](https://secure.php.net/manual/en/language.oop5.traits.php#language.oop5.traits.conflict) when two or more composed traits have the same function name, among [other features](https://secure.php.net/manual/en/language.oop5.traits.php).

## Interfaces

[Interfaces](https://secure.php.net/manual/en/language.oop5.interfaces.php) were added to PHP 5, so WordPress already makes use of this feature, however, extremely sparingly: the core includes less than ten interfaces in total!

Interfaces allow creating code which specifies which methods must be implemented, yet without having to define how these methods are actually implemented. They are useful for defining contracts among components, which leads to better modularity and maintainability of the application: A class implementing an interface can be a black box of code, and as long as the signatures of the functions in the interface do not change, the code can be upgraded at will without producing breaking changes, which can help prevent the accumulation of technical debt. In addition, they can help reduce vendor lock-in, by allowing to swap the implementation of some interface to that of a different vendor. As a consequence, it is imperative to code the application against interfaces instead of implementations (and defining which are the actual implementations through [dependency injection](https://en.wikipedia.org/wiki/Dependency_injection)).

Interfaces are defined using the `interface` keyword, and must list down just the signature of its methods (i.e. without having their contents defined), which must have visibility `public` (by default, adding no visibility keyword also makes it public):

<pre><code class="language-php">interface FileStorage {

  function save($filename, $contents);
  function readContents($filename);
}
</code></pre>

A class defines that it implements the interface through the `implements` keyword:

<pre><code class="language-php">class LocalDriveFileStorage implements FileStorage {

  function save($filename, $contents) {
    // Implement logic
  }
  function readContents($filename) {
    // Implement logic
  }
}
</code></pre>

A class can implement more than one interface, separating them with `,`:

<pre><code class="language-php">interface AWSService {
  function getRegion();
}

class S3FileStorage implements FileStorage, AWSService {

  function save($filename, $contents) {
    // Implement logic
  }
  function readContents($filename) {
    // Implement logic
  }
  function getRegion() {
    return 'us-east-1';
  }
}
</code></pre>

Since an interface declares the intent of what a component is supposed to do, it is extremely important to [name interfaces appropriately](https://www.alainschlesser.com/interface-naming-conventions/).

## Closures

[Closures](https://secure.php.net/manual/en/class.closure.php) were added to PHP 5.3, hence they are currently missing altogether from the WordPress core.

Closures is a mechanism for implementing [anonymous functions](https://secure.php.net/manual/en/functions.anonymous.php), which helps declutter the global namespace from single-use (or seldom-used) functions. Technically speaking, closures are instances of class `Closure`, however, in practice, we can most likely be blissfully unaware of this fact without any harm.

Before closures, whenever passing a function as an argument to another function, we had to define the function in advance and pass its name as the argument:

<pre><code class="language-php">function duplicate($price) {
  return $price*2;
}
$touristPrices = array_map('duplicate', $localPrices);
</code></pre>

With closures, an anonymous (i.e. without a name) function can already be passed directly as a parameter:

<pre><code class="language-php">$touristPrices = array_map(function($price) {
  return $price*2;
}, $localPrices);
</code></pre>

Closures can import variables to its context through the `use` keyword:

<pre><code class="language-php">$factor = 2;
$touristPrices = array_map(function($price) use($factor) {
  return $price*$factor;
}, $localPrices);
</code></pre>

## Generators

[Generators](https://secure.php.net/manual/en/language.generators.overview.php) were added to PHP 5.5, hence they are currently missing altogether from the WordPress core.

Generators provide an easy way to implement simple iterators. A generator allows to write code that uses `foreach` to iterate over a set of data without needing to build an array in memory. A generator function is the same as a normal function, except that instead of returning once, it can `yield` as many times as it needs to in order to provide the values to be iterated over.

<pre><code class="language-php">function xrange($start, $limit, $step = 1) {
    for ($i = $start; $i <= $limit; $i += $step) {
        yield $i;
    }
}
foreach (xrange(1, 9, 2) as $number) {
    echo "$number ";
}
// This prints: 1 3 5 7 9
</code></pre>

## Argument And Return Type Declarations

Different [argument type declarations](https://secure.php.net/manual/en/functions.arguments.php#functions.arguments.type-declaration) were introduced in different versions of PHP: WordPress is already able to declare interfaces and arrays (which it does not: I barely found one instance of a function declaring an array as parameter in core, and no interfaces), and will soon be able to declare callables (added in PHP 5.4) and scalar types: bool, float, int and string (added in PHP 7.0). [Return type declarations](https://secure.php.net/manual/en/functions.returning-values.php#functions.returning-values.type-declaration) were added to PHP 7.0.

Argument type declarations allow functions to declare of what specific type must an argument be. The validation is executed at call time, throwing an exception if the type of the argument is not the declared one. Return type declarations are the same concept, however, they specify the type of value that will be returned from the function. Type declarations are useful to make the intent of the function easier to understand and to avoid runtime errors from receiving or returning an unexpected type.

The argument type is declared before the argument variable name, and the return type is declared after the arguments, preceded by `:`:

<pre><code class="language-php">function foo(boolean $bar): int {

}
</code></pre>

Scalar argument type declarations have two options: coercive and strict. In coercive mode, if the wrong type is passed as a parameter, it will be converted to the right type. For example, a function that is given an integer for a parameter that expects a string will get a variable of type string. In strict mode, only a variable of the exact type of declaration will be accepted.

Coercive mode is the default. To enable strict mode, we must add a `declare` statement used with the `strict_types` declaration:

<pre><code class="language-php">declare(strict_types=1);
function foo(boolean $bar) {

}
</code></pre>

## New Syntax And Operators

WordPress can already identify variable-length argument lists through function `func_num_args`. Starting from PHP 5.6, we can use the `...` token to denote that the function accepts a variable number of arguments, and these arguments will be passed into the given variable as an array:

<pre><code class="language-php">function sum(...$numbers) {
  $sum = 0;
  foreach ($numbers as $number) {
    $sum += $number;
  }
  return $sum;
}
</code></pre>

Starting [from PHP 5.6](https://secure.php.net/manual/en/migration56.new-features.php#migration56.new-features.const-scalar-exprs), constants can involve scalar expressions involving numeric and string literals instead of just static values, and also arrays:

<pre><code class="language-php">const SUM = 37 + 2; // A scalar expression
const LETTERS = ['a', 'b', 'c']; // An array
</code></pre>

Starting [from PHP 7.0](https://secure.php.net/manual/en/migration70.new-features.php#migration70.new-features.define-array), arrays can also be defined using `define`:

<pre><code class="language-php">define('LETTERS', ['a', 'b', 'c']);
</code></pre>

PHP 7.0 added a couple of new operators: the [Null coalescing operator (`??`)](https://secure.php.net/manual/en/migration70.new-features.php#migration70.new-features.null-coalesce-op) and the [Spaceship operator (`<=>`)](https://secure.php.net/manual/en/migration70.new-features.php#migration70.new-features.spaceship-op).

The Null coalescing operator `??` is syntactic sugar for the common case of needing to use a ternary in conjunction with isset(). It returns its first operand if it exists and is not NULL; otherwise, it returns its second operand.

<pre><code class="language-php">$username = $_GET['user'] ?? 'nobody';
// This is equivalent to:
// $username = isset($_GET['user']) ? $_GET['user'] : 'nobody';
</code></pre>

The Spaceship operator `<=>` is used for comparing two expressions, returning -1, 0 or 1 when the first operand is respectively less than, equal to, or greater than the second operand.

<pre><code class="language-php">echo 1 <=> 2; // returns -1
echo 1 <=> 1; // returns 0
echo 2 <=> 1; // returns 1
</code></pre>

These are the most important new features added to PHP spanning versions 5.3 to 7.0. The list of the additional new features, not listed in this article, can be obtained by browsing [PHP’s documentation on migrating from version to version](https://secure.php.net/manual/en/appendices.php).

Next, we analyze how we can make the most out of all these new features, and from recent trends in web development, to produce better software.

## PHP Standards Recommendations

The [PHP Standards Recommendations](https://www.php-fig.org/) was created by a group of PHP developers from popular frameworks and libraries, attempting to establish conventions so that different projects can be integrated more seamlessly and different teams can work better with each other. The recommendations are not static: existing recommendations may be deprecated and newer ones created to take their place, and new ones are released on an ongoing basis.

The current recommendations are the following:

<table class="tablesaw table--no-stripe break-out table-saw" data-tablesaw-mode="swipe" data-tablesaw-minimap>
  <thead>
<th data-tablesaw-priority="persist">Group</th><th>Recommendation</th><th>Description</th></tr>
</thead>
<tbody>
<tr><td rowspan="2"><strong>Coding Styles</strong><br/>Standardized formatting reduces the cognitive friction when reading code from other authors</td><td><a href="https://www.php-fig.org/psr/psr-1/">PSR-1</a></td><td>Basic Coding Standard</td></tr>
<tr><td><a href="https://www.php-fig.org/psr/psr-2/">PSR-2</a></td><td>Coding Style Guide</td></tr>
<tr><td><strong>Autoloading</strong><br/>Autoloaders remove the complexity of including files by mapping namespaces to file system paths</td><td><a href="https://www.php-fig.org/psr/psr-4/">PSR-4</a></td><td>Improved Autoloading</td></tr>
<tr><td rowspan="5"><strong>Interfaces</strong><br/>Interfaces simplify the sharing of code between projects by following expected contracts</td><td><a href="https://www.php-fig.org/psr/psr-3/">PSR-3</a></td><td>Logger Interface</td></tr>
<tr><td><a href="https://www.php-fig.org/psr/psr-6/">PSR-6</a></td><td>Caching Interface</td></tr>
<tr><td><a href="https://www.php-fig.org/psr/psr-11/">PSR-11</a></td><td>Container Interface</td></tr>
<tr><td><a href="https://www.php-fig.org/psr/psr-13/">PSR-13</a></td><td>Hypermedia Links</td></tr>
<tr><td><a href="https://www.php-fig.org/psr/psr-16/">PSR-16</a></td><td>Simple Cache</td></tr>
<tr><td rowspan="4"><strong>HTTP</strong><br/>Interoperable standards and interfaces to have an agnostic approach to handling HTTP requests and responses, both on client and server side</td><td><a href="https://www.php-fig.org/psr/psr-7/">PSR-7</a></td><td>HTTP Message Interfaces</td></tr>
<tr><td><a href="https://www.php-fig.org/psr/psr-15/">PSR-15</a></td><td>HTTP Handlers</td></tr>
<tr><td><a href="https://www.php-fig.org/psr/psr-17/">PSR-17</a></td><td>HTTP Factories</td></tr>
<tr><td><a href="https://www.php-fig.org/psr/psr-18/">PSR-18</a></td><td>HTTP Client</td></tr>
</tbody>
</table>

## Think And Code In Components

Components make it possible to use the best features from a framework without being locked-in to the framework itself. For instance, [Symfony](https://symfony.com/) has been released as a set of [reusable PHP components](https://symfony.com/components) that can be installed independently of the [Symfony framework](https://symfony.com/what-is-symfony); [Laravel](https://laravel.com/), another PHP framework, [makes use of several Symfony components](https://symfony.com/projects/laravel), and released its own [set of reusable components](https://github.com/illuminate) that can be used by any PHP project.

All of these components are published in [Packagist](https://packagist.org/), a repository of public PHP packages, and can be easily added to any PHP project through [Composer](https://getcomposer.org/), an extremely popular dependency manager for PHP.

WordPress should be part of such a virtuous development cycle. Unfortunately, the WordPress core itself is not built using components (as evidenced by the almost total absence of interfaces) and, moreover, it doesn’t even have the *composer.json* file required to enable installing WordPress through Composer. This is because the WordPress community [hasn’t agreed](https://core.trac.wordpress.org/ticket/23912) whether WordPress is a site’s dependency (in which case installing it through Composer would be justified) or if it is the site itself (in which case Composer may not be the right tool for the job).

In my opinion, if we are to expect WordPress to stay relevant for the next fifteen years (at least WordPress as a backend CMS), then **WordPress must be recognized as a site’s dependency and made available for installation through Composer**. The reason is very simple: with barely a single command in the terminal, Composer enables to declare and install a project’s dependencies from the thousands of packages published in Packagist, making it possible to create extremely-powerful PHP applications in no time, and developers love working this way. If WordPress doesn’t adapt to this model, it may lose the support from the development community and fall into oblivion, as much as FTP fell out of favor after the introduction of Git-based deployments.

I would argue that the release of Gutenberg already demonstrates that WordPress is a site dependency and not the site itself: Gutenberg treats WordPress as a headless CMS, and can operate with other backend systems too, as [Drupal Gutenberg](https://drupalgutenberg.org/) exemplifies. Hence, Gutenberg makes it clear that the CMS powering a site can be swappable, hence it should be treated as a dependency. Moreover, Gutenberg itself is intended to be based on [JavaScript components released through npm](https://www.npmjs.com/org/wordpress) (as [explained by core committer Adam Silverstein](https://2018.europe.wordcamp.org/session/javascript-apis-in-wordpress/)), so if the WordPress client is expected to manage its JavaScript packages through the npm package manager, then why not extend this logic to the backend in order to manage PHP dependencies through Composer?

Now the good news: There is no need to wait for this issue to be resolved since it is already possible to treat WordPress as a site’s dependency and install it through Composer. John P. Bloch has [mirrored WordPress core in Git](https://github.com/johnpbloch/wordpress-core), added a composer.json file, and [released it in Packagist](https://packagist.org/packages/johnpbloch/wordpress), and [Roots' Bedrock](https://roots.io/bedrock/) provides a package to install WordPress with a customized folder structure with support for modern development tools and an enhanced security. And themes and plugins are covered too; as long as they have been listed on the WordPress [theme](https://wordpress.org/themes/) and [plugin](https://wordpress.org/plugins/) directories, they are available under [WordPress Packagist](https://wpackagist.org/).

As a consequence, it is a sensible option to create WordPress code not thinking in terms of themes and plugins, but thinking in terms of components, making them available through Packagist to be used by any PHP project, and additionally packaged and released as themes and plugins for the specific use of WordPress. If the component needs to interact with WordPress APIs, then these APIs can be [abstracted behind an interface](https://github.com/leoloso/PoP/blob/master/documentation/DeveloperGuide.md#cms-agnosticism) which, if the need arises, can be implemented for other CMSs too.

## Adding A Template Engine To Improve The View Layer

If we follow through the recommendation of thinking and coding in components, and treat WordPress as a site’s dependency other than the site itself, then our projects can break free from the boundaries imposed by WordPress and import ideas and tools taken from other frameworks.

Rendering HTML content on the server-side is a case in point, which is done through plain PHP templates. This view layer can be enhanced through template engines [Twig](https://twig.symfony.com) (by Symfony) and [Blade](https://laravel.com/docs/5.7/blade) (by Laravel), which provide a very concise syntax and powerful features that give it an advantage over plain PHP templates. In particular, [Gutenberg’s dynamic blocks](https://wordpress.org/gutenberg/handbook/designers-developers/developers/tutorials/block-tutorial/creating-dynamic-blocks/) can easily benefit from these template engines, since their process to render the block’s HTML on the server-side is decoupled from WordPress' template hierarchy architecture.

## Architect The Application For The General Use

Coding against interfaces, and thinking in terms of components, allows us to architect an application for general use and customize it for the specific use that we need to deliver, instead of coding just for the specific use for each project we have. Even though this approach is more costly in the short term (it involves extra work), it pays off in the long term when additional projects can be delivered with lower efforts from just customizing a general-use application.

For this approach to be effective, the following considerations must be taken into account:

### Avoid Fixed Dependencies (As Much As Possible)

jQuery and Bootstrap (or Foundation, or *&lt;--insert your favorite library here--&gt;*) could’ve been considered must-haves a few years ago, however, they have been steadily losing ground against vanilla JS and newer native CSS features. Hence, a general-use project coded five years ago which depended on these libraries may not be suitable nowadays anymore. Hence, as a general rule of thumb, the lower the amount of fixed dependencies on third-party libraries, the more up-to-date it will prove to be for the long term.

### Progressive Enhancement Of Functionalities

WordPress is a full-blown CMS system which includes user management, hence support for user management is included out of the box. However, not every WordPress site requires user management. Hence, our application should take this into account, and work optimally on each scenario: support user management whenever required, but do not load the corresponding assets whenever it is not. This approach can also work gradually: Say that a client requires to implement a Contact us form but has no budget, so we code it using a free plugin with limited features, and another client has the budget to buy the license from a commercial plugin offering better features. Then, we can code our functionality to default to a very basic functionality, and increasingly use the features from whichever is the most-capable plugin available in the system.

### Continuous Code And Documentation Review

By periodically reviewing our previously-written code and its documentation, we can validate if it is either up-to-date concerning new conventions and technologies and, if it is not, take measures to upgrade it before the technical debt becomes too expensive to overcome and we need to code it all over again from scratch.

<p><strong>Recommended reading</strong>: <em><a href="https://www.smashingmagazine.com/2018/01/php-wordpress-functions-site-insecure/">Be Watchful: PHP And WordPress Functions That Can Make Your Site Insecure</a></em></p>

## Attempt To Minimize Problems But Be Prepared When They Happen

No software is ever 100% perfect: the bugs are always there, we just haven’t found them yet. As such, we need to make sure that, once the problems arise, they are easy to fix.

### Make It Simple

Complex software cannot be maintained in the long term: Not just because other team members may not understand it, but also because the person who coded it may not understand his/her own complex code a few years down the road. So producing simple software must be a priority, more since [only simple software can be correct and fast](https://drewdevault.com/2018/07/09/Simple-correct-fast.html).

### Failing On Compile Time Is Better Than On Runtime

If a piece of code can be validated against errors at either compile time or runtime time, then we should prioritize the compile time solution, so the error can arise and be dealt with in the development stage and before the application reaches production. For instance, both `const` and `define` are used for defining constants, however, whereas `const` is validated at compile time, `define` is validated at runtime. So, whenever possible, using `const` is preferable over `define`.

Following this recommendation, hooking WordPress functions contained in classes can be enhanced by passing the actual class as a parameter instead of a string with the class name. In the example below, if class `Foo` is renamed, whereas the second hook will produce a compilation error, the first hook will fail on runtime, hence the second hook is better:

<pre><code class="language-php">class Foo {
  public static function bar() {

  }
}

add_action('init', ['Foo', 'bar']); // Not so good
add_action('init', [Foo::class, 'bar']); // Much better
</code></pre>

For the same reason as above, we should avoid using global variables (such as `global $wpdb`): these not only pollute the global context and are not easy to track where they originate from, but also, if they get renamed, the error will be produced on runtime. As a solution, we can use a [Dependency Injection Container](https://fabien.potencier.org/do-you-need-a-dependency-injection-container.html) to obtain an instance of the required object.

### Dealing With Errors/Exceptions

We can [create an architecture of `Exception` objects](https://www.alainschlesser.com/structuring-php-exceptions/), so that the application can react appropriately according to each particular problem, to either recover from it whenever possible or show a helpful error message to the user whenever not, and in general to log the error for the admin to fix the problem. And always protect your users from the white screen of death: All uncaught `Error`s and `Exception`s can be intercepted through function [`set_exception_handler`](https://secure.php.net/manual/en/function.set-exception-handler.php) to print a non-scary error message on screen.

## Adopt Build Tools

Build tools can save a lot of time by automating tasks which are very tedious to execute manually. WordPress doesn’t offer integration with any specific build tool, so the task of incorporating these to the project will fall entirely on the developer.

There are different tools for accomplishing different purposes. For instance, there are build tools to execute tasks for compressing and resizing images, minifying JS and CSS files, and copying files to a directory for producing a release, such as [Webpack](https://webpack.js.org/), [Grunt](https://gruntjs.com/) and [Gulp](https://gulpjs.com/); other tools help create the scaffolding of a project, which is helpful for producing the folder structure for our themes or plugins, such as [Yeoman](https://yeoman.io/). Indeed, with so many tools around, browsing articles [comparing the different available tools](https://medium.freecodecamp.org/making-sense-of-front-end-build-tools-3a1b3a87043b) will help find the most suitable one for our needs.

In some cases, though, there are no build tools that can achieve exactly what our project needs, so we may need to code our own build tool as an extension to the project itself. For instance, I have done this to [generate the service-worker.js file](https://www.smashingmagazine.com/2017/10/service-worker-single-page-application-wordpress-sites/) to add support for Service Workers in WordPress.

## Conclusion

Due to its strong emphasis on keeping backwards compatibility, extended even up to PHP 5.2.4, WordPress has not been able to benefit from the latest features added to PHP, and this fact has made WordPress become a not-very-exciting platform to code for among many developers.

Fortunately, these gloomy days may soon be over, and WordPress may become a shiny and exciting platform to code for once again: The requirement of PHP 7.0+ starting in December 2019 will make plenty of PHP features available, enabling developers to produce more powerful and more performant software. In this article, we reviewed the most important newly-available PHP features and how to make the most out of them.

The recent release of Gutenberg could be a sign of the good times to come: even if Gutenberg itself has not been fully accepted by the community, at least it demonstrates a willingness to incorporate the latest technologies (such as React and Webpack) into the core. This turn of events makes me wonder: If the frontend can get such a makeover, why not extend it to the backend? Once WordPress requires at least PHP 7.0, the upgrade to modern tools and methodologies can accelerate: As much as npm became the JavaScript package manager of choice, why not making Composer become the official PHP dependency manager? If blocks are the new unit for building sites in the frontend, why not use PHP components as the unit for incorporating functionalities into the backend? And finally, if Gutenberg treats WordPress as a swappable backend CMS, why not already recognize that WordPress is a site dependency and not the site itself? I’ll leave these open questions for you to reflect upon and ponder about.

{{< signature "rb, ra, il" >}}