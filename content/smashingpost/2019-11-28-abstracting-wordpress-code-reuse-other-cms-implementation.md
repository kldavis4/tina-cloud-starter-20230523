---
title: 'Abstracting WordPress Code To Reuse With Other CMSs: Implementation (Part 2)'
slug: abstracting-wordpress-code-reuse-with-other-cms-implementation
author: leonardolosoviz
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a6a47da3-fe4a-42f1-82d7-89dec5f543f4/abstracting-wordpress-code-reuse-with-other-cms-implementation.png
date: 2019-11-28T11:00:00.000Z
summary: >-
  Making our code CMS-agnostic, as much as possible, enables us to easily port our application to another CMS if the need arises. In this article we will learn how to abstract a WordPress application, making its code readily available for other frameworks or CMSs.
description: >-
  Making our code CMS-agnostic, as much as possible, enables us to easily port our application to another CMS if the need arises. In this article we will learn how to abstract a WordPress application, making its code readily available for other frameworks or CMSs.
categories:
  - WordPress
  - CMS
---
In the [first part of this series](https://www.smashingmagazine.com/2019/11/abstracting-wordpress-code-cms-concepts/), we learned the key concepts to build an application that is as CMS-agnostic as possible. In this second and final part, we will proceed to abstract a WordPress application, making its code ready to be used with [Symfony components](https://symfony.com/), [Laravel framework](https://laravel.com/), and [October CMS](https://octobercms.com/) (which is based on Laravel).

## Accessing Services

Before we start abstracting the code, we need to provide the layer of dependency injection to the application. As described in the first part of this series, this layer is satisfied through [Symfony's DependencyInjection component](https://symfony.com/components/DependencyInjection). To access the defined services, we create a class `ContainerBuilderFactory` which simply stores a static instance of the component's `ContainerBuilder` object:

<pre><code class="language-javascript">use Symfony\Component\DependencyInjection\ContainerBuilder;

class ContainerBuilderFactory {
  private static $instance;
  public static function init()
  {
    self::$instance = new ContainerBuilder();
  }
  public static function getInstance()
  {
    return self::$instance;
  }
}</code></pre>

{{% feature-panel %}}

Then, to access a service called `"cache"`, the application requests it like this:

<div class="break-out">

<pre><code class="language-javascript">$cacheService = ContainerBuilderFactory::getInstance()->get('cache');
// Do something with the service
// $cacheService->...</code></pre>
</div>

## Abstracting WordPress Code

We have identified the following pieces of code and concepts from a WordPress application that need be abstracted away from WordPress's opinionatedness:

- accessing functions
- function names
- function parameters
- states (and other constant values)
- CMS helper functions
- user permissions
- application options
- database column names
- errors
- hooks
- routing
- object properties
- global state
- entity models (meta, post types, pages being posts, and taxonomies —tags and categories—)
- translation
- media.

Let's proceed to abstract them, one by one.

**Note:** For ease of reading, I have omitted adding namespaces to all classes and interfaces throughout this article. However, adding namespaces, as specified in PHP Standards Recommendation [PSR-4](https://www.php-fig.org/psr/psr-4/), is a must! Among other advantages, the application can then benefit from [autoloading](https://getcomposer.org/doc/01-basic-usage.md#autoloading), and Symfony's dependency injection can rely on [automatic service loading](https://symfony.com/doc/current/service_container.html#service-psr4-loader) as to reduce its configuration to the bare minimum.

### Accessing functions

The mantra "code against interfaces, not implementations" means that all those functions provided by the CMS cannot be accessed directly anymore. Instead, we must access the function from a contract (an interface), on which the CMS function will simply be the implementation. By the end of the abstraction, since no WordPress code will be referenced directly anymore, we can then swap WordPress with a different CMS.

For instance, if our application accesses function `get_posts`:

<pre><code class="language-javascript">$posts = get_posts($args);</code></pre>

We must then abstract this function under some contract:

<pre><code class="language-javascript">interface PostAPIInterface
{
  public function getPosts($args);
}</code></pre>

The contract must be implemented for WordPress:

<pre><code class="language-javascript">class WPPostAPI implements PostAPIInterface
{
  public function getPosts($args) {
    return get_posts($args);
  }
}</code></pre>

A service `"posts_api"` must be added to the dependency injection `services.yaml` configuration file, indicating which class resolves the service:

<pre><code class="language-javascript">services:
  posts_api:
    class: \WPPostAPI</code></pre>

And finally, the application can reference the function through service `"posts_api"`:

<div class="break-out">

<pre><code class="language-javascript">$postsAPIService = ContainerBuilderFactory::getInstance()->get('posts_api');
$posts = $postsAPIService->getPosts($args);</code></pre>
</div>

### Function names

If you have noticed from the code demonstrated above, function `get_posts` is abstracted as `getPosts`. There are a couple of reasons why this is a good idea:

- By calling the function differently, it helps identify which code belongs to WordPress and which code belongs to our abstracted application.
- Function names must be camelCased to comply with [PSR-2](https://www.php-fig.org/psr/psr-2/), which attempts to define a standard for writing PHP code.

Certain functions can be redefined, making more sense in an abstract context. For instance, WordPress function `get_user_by($field, $value)` uses parameter `$field` with values `"id"`, `"ID"`, `"slug"`, `"email"` or `"login"` to know how to get the user. Instead of replicating this methodology, we can explicitly define a separate function for each of them:

<pre><code class="language-javascript">interface UsersAPIInterface
{
  public function getUserById($value);
  public function getUserByEmail($value);
  public function getUserBySlug($value);
  public function getUserByLogin($value);
}</code></pre>

And these are resolved for WordPress:

<pre><code class="language-javascript">class WPUsersAPI implements UsersAPIInterface
{
  public function getUserById($value)
  {
    return get_user_by('id', $value);
  }
  public function getUserByEmail($value)
  {
    return get_user_by('email', $value);
  }
  public function getUserBySlug($value)
  {
    return get_user_by('slug', $value);
  }
  public function getUserByLogin($value)
  {
    return get_user_by('login', $value);
  }
}</code></pre>

Certain other functions should be renamed because their names convey information about their implementation, which may not apply for a different CMS. For instance, WordPress function `get_the_author_meta` can receive parameter `"user_lastname"`, indicating that the user's lastname is stored as a "meta" value (which is defined as an additional property for an object, not originally mapped in the database model). However, other CMSs may have a column `"lastname"` in the user table, so it doesn't apply as a meta value. (The actual definition of "meta" value is actually inconsistent in WordPress: function `get_the_author_meta` also accepts value `"user_email"`, even though the email is stored on the user table. Hence, I'd rather stick to my definition of "meta" value, and remove all inconsistencies from the abstracted code.)

Then, our contract will implement the following functions:

<pre><code class="language-javascript">interface UsersAPIInterface
{
  public function getUserDisplayName($user_id);
  public function getUserEmail($user_id);
  public function getUserFirstname($user_id);
  public function getUserLastname($user_id);
  ...
}</code></pre>

Which are resolved for WordPress:

<pre><code class="language-javascript">class WPUsersAPI implements UsersAPIInterface
{
  public function getUserDisplayName($user_id)
  {
    return get_the_author_meta('display_name', $user_id);
  }
  public function getUserEmail($user_id)
  {
    return get_the_author_meta('user_email', $user_id);
  }
  public function getUserFirstname($user_id)
  {
    return get_the_author_meta('user_firstname', $user_id);
  }
  public function getUserLastname($user_id)
  {
    return get_the_author_meta('user_lastname', $user_id);
  }
  ...
}</code></pre>

Our functions could also be re-defined as to remove the limitations from WordPress. For instance, function `update_user_meta($user_id, $meta_key, $meta_value)` can receive one meta attribute at a time, which makes sense since each of these is updated on its own database query. However, October CMS maps all meta attributes together on a single database column, so it makes more sense to update all values together on a single database operation. Then, our contract can include an operation `updateUserMetaAttributes($user_id, $meta)` which can update several meta values at the same time:

<pre><code class="language-javascript">interface UserMetaInterface
{
  public function updateUserMetaAttributes($user_id, $meta);
}</code></pre>

Which is resolved for WordPress like this:

<pre><code class="language-javascript">class WPUsersAPI implements UsersAPIInterface
{
  public function updateUserMetaAttributes($user_id, $meta)
  {
    foreach ($meta as $meta_key => $meta_value) {
      update_user_meta($user_id, $meta_key, $meta_value);
    }
  }
}</code></pre>

Finally, we may want to re-define a function to remove its ambiguities. For instance, WordPress function `add_query_arg` can receive parameters in two different ways:

1. Using a single key and value: `add_query_arg('key', 'value', 'https://example.com');`
2. Using an associative array: `add_query_arg(['key1' => 'value1', 'key2' => 'value2'], 'https://example.com');`

This becomes difficult to keep consistent across CMSs. Hence, our contract can define functions `addQueryArg` (singular) and `addQueryArgs` (plural) as to remove the ambiguity:

<div class="break-out">

<pre><code class="language-javascript">public function addQueryArg(string $key, string $value, string $url);
public function addQueryArgs(array $key_values, string $url);</code></pre>
</div>

### Function parameters

We must also abstract the parameters to the function, making sure they make sense in a generic context. For each function to abstract, we must consider:

- renaming and/or re-defining the parameters;
- renaming and/or re-defining the attributes passed on array parameters.

For instance, WordPress function `get_posts` receives a unique parameter `$args`, which is an array of attributes. One of its attributes is `fields` which, when given the value `"ids"`, makes the function return an array of IDs instead of an array of objects. However, I deem this implementation too specific for WordPress, and for a generic context I'd prefer a different solution: Convey this information through a separate parameter called `$options`, under attribute `"return-type"`. 

To accomplish this, we add parameter `$options` to the function in our contract:

<pre><code class="language-javascript">interface PostAPIInterface
{
  public function getPosts($args, $options = []);
}</code></pre>

Instead of referencing WordPress constant value `"ids"` (which we can't guarantee will be the one used in all other CMSs), we create a corresponding constant value for our abstracted application:

<pre><code class="language-javascript">class Constants
{
  const RETURNTYPE_IDS = 'ids';
}</code></pre>

The WordPress implementation must map and recreate the parameters between the contract and the implementation:

<pre><code class="language-javascript">class WPPostAPI implements PostAPIInterface
{
  public function getPosts($args, $options = []) {
    if ($options['return-type'] == Constants::RETURNTYPE_IDS) {
      $args['fields'] = 'ids';
    }
    return get_posts($args);
  }
}</code></pre>

And finally, we can execute the code through our contract:

<pre><code class="language-javascript">$options = [
  'return-type' => Constants::RETURNTYPE_IDS,
];
$post_ids = $postsAPIService->getPosts($args, $options);</code></pre>

While abstracting the parameters, we should avoid transferring WordPress's technical debt to our abstracted code, whenever possible. For instance, parameter `$args` from function `get_posts` can contain attribute `'post_type'`. This attribute name is somewhat misleading, since it can receive one element (`post_type => "post"`) but also a list of them (`post_type => "post, event"`), so this name should be in plural instead: `post_types`. When abstracting this piece of code, we can set our interface to expect attribute `post_types` instead, which will be mapped to WordPress's `post_type`.

Similarly, different functions accept arguments with different names, even though these have the same objective, so their names can be unified. For instance, through parameter `$args`, WordPress function `get_posts` accepts attribute `posts_per_page`, and function `get_users` accepts attribute `number`. These attribute names can perfectly be replaced with the more generic attribute name `limit`.

It is also a good idea to rename parameters to make it easy to understand which ones belong to WordPress and which ones have been abstracted. For instance, we can decide to replace all `"_"` with `"-"`, so our newly-defined argument `post_types` becomes `post-types`.

Applying these prior considerations, our abstracted code will look like this:

<pre><code class="language-javascript">class WPPostAPI implements PostAPIInterface
{
  public function getPosts($args, $options = []) {
    ...
    if (isset($args['post-types'])) {
      $args['post_type'] = $args['post-types'];
      unset($args['post-types']);
    }
    if (isset($args['limit'])) { 
      $args['posts_per_page'] = $args['limit'];
      unset($args['limit']);
    }
    return get_posts($args);
  }
}</code></pre>

We can also re-define attributes to modify the shape of their values. For instance, WordPress parameter `$args` in function `get_posts` can receive attribute `date_query`, whose properties (`"after"`, `"inclusive"`, etc) can be considered specific to WordPress:

<pre><code class="language-javascript">$date = current_time('timestamp');
$args['date_query'] = array(
  array(
    'after' => date('Y-m-d H:i:s', $date),
    'inclusive' => true,
  )
);</code></pre>

To unify the shape of this value into something more generic, we can re-implement it using other arguments, such as `"date-from"` and `"date-from-inclusive"` (this solution is not 100% convincing though, since it is more verbose than WordPress's):

<pre><code class="language-javascript">class WPPostAPI implements PostAPIInterface
{
  public function getPosts($args, $options = []) {
    ...
    if (isset($args['date-from'])) {
      $args['date_args'][] = [
        'after' => $args['date-from'],
        'inclusive' => false,
      ];
      unset($args['date-from']);
    }
    if (isset($args['date-from-inclusive'])) {
      $args['date_args'][] = [
        'after' => $args['date-from-inclusive'],
        'inclusive' => true,
      ];
      unset($args['date-from-inclusive']);
    }
    return get_posts($args);
  }
}</code></pre>

In addition, we need to consider if to abstract or not those parameters which are too specific to WordPress. For instance, function `get_posts` allows to order posts by attribute `menu_order`, which I don't think it works in a generic context. Then, I'd rather not abstract this code and keep it on the CMS-specific package for WordPress.

Finally, we can also add argument types (and, since here we are, also return types) to our contract fuction, making it more understandable and allowing the code to fail in compilation time instead of during runtime:

<div class="break-out">

<pre><code class="language-javascript">interface PostAPIInterface
{
  public function getPosts(array $args, array $options = []): array;
}</code></pre>
</div>

### States (and other constant values)

We need to make sure that all states have the same meaning in all CMSs. For instance, posts in WordPress can have one among the following states: `"publish"`, `"pending"`, `"draft"` or `"trash"`. To make sure that the application references the abstracted version of the states and not the CMS-specific one, we can simply define a constant value for each of them:

<pre><code class="language-javascript">class PostStates {
  const PUBLISHED = 'published';
  const PENDING = 'pending';
  const DRAFT = 'draft';
  const TRASH = 'trash';
}</code></pre>

As it can be seen, the actual constant values may or may not be the same as in WordPress: while `"publish"` was renamed as `"published"`, the other ones remain the same. 

For the implementation for WordPress, we convert from the agnostic value to the WordPress-specific one:

<pre><code class="language-javascript">class WPPostAPI implements PostAPIInterface
{
  public function getPosts($args, $options = []) {
    ...
    if (isset($args['post-status'])) {
      $conversion = [
        PostStates::PUBLISHED => 'publish',
        PostStates::PENDING => 'pending',
        PostStates::DRAFT => 'draft',
        PostStates::TRASH => 'trash',
      ];
      $args['post_status'] = $conversion[$args['post-status']];
      unset($args['post-status']);
    }
    return get_posts($args);
  }
}</code></pre>

Finally, we can reference these constants throughout our CMS-agnostic application:

<pre><code class="language-javascript">$args = [
  'post-status' => PostStates::PUBLISHED,
];
$posts = $postsAPIService->getPosts($args);</code></pre>

This strategy works under the assumption that all CMSs will support these states. If any CMS does not support a particular state (eg: `"pending"`) then it should throw an exception whenever a corresponding functionality is invoked.

### CMS helper functions

WordPress implements several helper functions that must also abstracted, such as `make_clickable`. Because these functions are very generic, we can implement a default behavior for them that works well in an abstract context, and which can be overridden if the CMS implements a better solution.

We first define the contract:

<pre><code class="language-javascript">interface HelperAPIInterface
{
  public function makeClickable(string $text);
}</code></pre>

And provide a default behaviour for the helper functions through an abstract class:

<div class="break-out">

<pre><code class="language-javascript">abstract class AbstractHelperAPI implements HelperAPIInterface
{
  public function makeClickable(string $text) {
    return preg_replace('!(((f|ht)tp(s)?://)[-a-zA-Zа-яА-Я()0-9@:%_+.~#?&;//=]+)!i', '&lt;a href="$1"&gt;$1&lt;/a&gt;', $text);
  }
}</code></pre>
</div>

Now, our application can either use this functionality or, if it runs on WordPress, use the WordPress-specific implementation:

<pre><code class="language-javascript">class WPHelperAPI extends AbstractHelperAPI
{
  public function makeClickable(string $text) {
    return make_clickable($text);
  }
}</code></pre>

{{% ad-panel-leaderboard %}} 

### User permissions

For all CMSs which support user management, in addition to abstracting the corresponding functions (such as `current_user_can` and `user_can` in WordPress), we must also make sure that the user permissions (or capabilities) have the same effect across all CMSs. To achieve this, our abstracted application needs to explicitly state what is expected from the capability, and the implementation for each CMS must either satisfy it through one of its own capabilities or throw an exception if it can't satisfy it. For instance, if the application needs to validate if the user can edit posts, it can represent it through a capability called `"capability:editPosts"`, which is satisfied for WordPress through its capability `"edit_posts"`.

This is still an instance of the "code against interfaces, not implementations" principle, however here we run against a problem: Whereas in PHP we can define interfaces and classes to model contracts and service providers (which works in compilation time, so that the code doesn't compile if a class implementing an interface does not implement all functions defined in the interface), PHP offers no similar construct to validate that a contract capability (which is simply a string, such as `"capability:editPosts"`) has been satisfied through a capability by the CMS. This concept, which I call a "loose contract", will need to be handled by our application, on runtime.

To deal with "loose contracts", I have created a service `LooseContractService` through which: 

- the application can define what "contract names" must be implemented, through function `requireNames`.
- the CMS-specific implementations can satisfy those names, through function `implementNames`.
- the application can get the implementation of a name through function `getImplementedName`.
- the application can also inquire for all non-satisfied required names through function `getNotImplementedRequiredNames`, as to throw an exception or log the error if needed.

The service looks like this:

<div class="break-out">

<pre><code class="language-javascript">class LooseContractService
{
  protected $requiredNames = [];
  protected $nameImplementations = [];

  public function requireNames(array $names): void
  {
    $this->requiredNames = array_merge(
      $this->requiredNames,
      $names
    );
  }

  public function implementNames(array $nameImplementations): void
  {
    $this->nameImplementations = array_merge(
      $this->nameImplementations,
      $nameImplementations
    );
  }

  public function getImplementedName(string $name): ?string {
    return $this->nameImplementations[$name];
  }

  public function getNotImplementedRequiredNames(): array {
    return array_diff(
      $this->requiredNames,
      array_keys($this->nameImplementations)
    );
  }
}</code></pre>
</div>

The application, when initialized, can then establish loose contracts by requiring names:

<div class="break-out">

<pre><code class="language-javascript">$looseContractService = ContainerBuilderFactory::getInstance()->get('loose_contracts');
$looseContractService->requireNames([
  'capability:editPosts',
]);</code></pre>
</div>

And the CMS-specific implementation can satisfy these:

<pre><code class="language-javascript">$looseContractService->implementNames([
  'capability:editPosts' => 'edit_posts',
]);</code></pre>

The application can then resolve the required name to the implementation from the CMS. If this required name (in this case, a capability) is not implemented, then the application may throw an exception:

<div class="break-out">

<pre><code class="language-javascript">$cmsCapabilityName = $looseContractService->getImplementedName('capability:editPosts');
if (!$cmsCapabilityName) {
  throw new Exception(sprintf(
    "The CMS has no support for capability \"%s\"",
    'capability:editPosts'
  ));
}
// Now can use the capability to check for permissions
$userManagementAPIService = ContainerBuilderFactory::getInstance()->get('user_management_api');
if ($userManagementAPIService->userCan($user_id, $cmsCapabilityName)) {
  ...
}</code></pre>
</div>

Alternatively, the application can also fail when first initialized if any one required name is not satisfied:

<div class="break-out">

<pre><code class="language-javascript">if ($notImplementedNames = $looseContractService->getNotImplementedRequiredNames()) {
  throw new Exception(sprintf(
    "The CMS has not implemented loose contract names %s",
    implode(', ', $notImplementedNames)
  ));
}</code></pre>
</div>

### Application options

WordPress ships with several application options, such as those stored in table `wp_options` under entries `"blogname"`, `"blogdescription"`, `"admin_email"`, `"date_format"` and many others. Abstracting application options involves:

- abstraction the function `getOption`;
- abstracting each of the required options, aiming to make the CMS satisfy the notion of this option (eg: if a CMS doesn't have an option for the site's description, it can't return the site's name instead).

Let's solve these 2 actions in turn. Concerning function `getOption`, I believe that we can expect all CMSs to support storing and retrieving options, so we can place the corresponding function under a `CMSCoreInterface` contract:

<pre><code class="language-javascript">interface CMSCoreInterface
{
  public function getOption($option, $default = false);
}</code></pre>

As it can be observed from the function signature above, I'm making the assumption that each option will also have a default value. However, I don't know if every CMS allows setting default values for options. But it doesn't matter since the implementation can simply return `NULL` then.

This function is resolved for WordPress like this:

<pre><code class="language-javascript">class WPCMSCore implements CMSCoreInterface
{
  public function getOption($option, $default = false)
  {
    return get_option($option, $default);
  }
}</code></pre>

To solve the 2nd action, which is abstracting each needed option, it is important to notice that even though we can always expect the CMS to support `getOption`, we can't expect it to implement each single option used by WordPress, such as `"use_smiles"` or `"default_ping_status"`. Hence, we must first filter all options, and abstract only those that make sense in a generic context, such as `"siteName"` or `"dateFormat"`. 

Then, having the list of options to abstract, we can use a "loose contract" (as explained earlier on) and require a corresponding option name for each, such as `"option:siteName"` (resolved for WordPress as `"blogname"`) or `"option:dateFormat"` (resolved as `"date_format"`). 

### Database column names

In WordPress, when we are requesting data from function `get_posts` we can set attribute `"orderby"` in `$args` to order the results, which can be based on a column from the posts table (such as values `"ID"`, `"title"`, `"date"`, `"comment_count"`, etc), a meta value (through values `"meta_value"` and `"meta_value_num"`) or other values (such as `"post__in"` and `"rand"`). 

Whenever the value corresponds to the table column name, we can abstract them using a "loose contract", as explained earlier on. Then, the application can reference a loose contract name:

<div class="break-out">

<pre><code class="language-javascript">$args = [
  'orderby' => $looseContractService->getImplementedName('dbcolumn:orderby:posts:date'),
];
$posts = $postsAPIService->getPosts($args);</code></pre>
</div>

And this name is resolved for WordPress:

<pre><code class="language-javascript">$looseContractService->implementNames([
  'dbcolumn:orderby:posts:date' => 'date',
]);</code></pre>

Now, let's say that in our WordPress application we have created a meta value `"likes_count"` (which stores how many likes a post has) to order posts by popularity, and we want to abstract this functionality too. To order results by some meta property, WordPress expects an additional attribute `"meta_key"`, like this:

<pre><code class="language-javascript">$args = [
  'orderby' => 'meta_value',
  'meta_key' => 'likes_count',
];</code></pre>

Because of this additional attribute, I consider this implementation WordPress-specific and very difficult to abstract to make it work everywhere. Then, instead of generalizing this functionality, I can simply expect every CMS to add their own, specific implementation.

Let's do that. First, I create a helper class to retrieve the CMS-agnostic query:

<div class="break-out">

<pre><code class="language-javascript">class QueryHelper
{
  public function getOrderByQuery()
  {
    return array(
      'orderby' => $looseContractService->getImplementedName('dbcolumn:orderby:posts:likesCount'),
    );
  }
}</code></pre>
</div>

The OctoberCMS-specific package can add a column `"likes_count"` to the posts table, and resolve name `"dbcolumn:orderby:posts:likesCount"` to `"like_count"` and it will work. The WordPress-specific package, though, must resolve `"dbcolumn:orderby:posts:likesCount"` as `"meta_value"` and then override the helper function to add the additional property `"meta_key"`:

<pre><code class="language-javascript">class WPQueryHelper extends QueryHelper
{
  public function getOrderByQuery()
  {
    $query = parent::getOrderByQuery();
    $query['meta_key'] = 'likes_count';
    return $query;
  }
}</code></pre>

Finally, we set-up the helper query class as a service in the `ContainerBuilder`, configure it to be resolved to the WordPress-specific class, and we obtain the query for ordering results:

<div class="break-out">

<pre><code class="language-javascript">$queryHelperService = ContainerBuilderFactory::getInstance()->get('query_helper');
$args = $queryHelperService->getOrderByQuery();
$posts = $postsAPIService->getPosts($args);</code></pre>
</div>

Abstracting the values for ordering results that do not correspond to column names or meta properties (such as `"post__in"` and `"rand"`) seems to be more difficult. Because my application doesn't use them, I haven't considered how to do it, or even if it is possible. Then I took the easy way out: I have considered these to be WordPress-specific, hence the application makes them available only when running on WordPress.

### Errors

When dealing with errors, we must consider abstracting the following elements:

- the definition of an error;
- error codes and messages.

Let's review these in turn.

#### Definition of an error:

An `Error` is a special object, different than an `Exception`, used to indicate that some operation has failed, and why it failed. WordPress represents errors through class `WP_Error`, and allows to check if some returned value is an error through function `is_wp_error`. 

We can abstract checking for an error:

<pre><code class="language-javascript">interface CMSCoreInterface
{
  public function isError($object);
}</code></pre>

Which is resolved for WordPress like this:

<pre><code class="language-javascript">class WPCMSCore implements CMSCoreInterface
{
  public function isError($object)
  {
    return is_wp_error($object);
  }
}</code></pre>

However, to deal with errors in our abstracted code, we can't expect all CMSs to have an error class with the same properties and methods as WordPress's `WP_Error` class. Hence, we must abstract this class too, and convert from the CMS error to the abstracted error after executing a function from the CMS. 

The abstract error class `Error` is simply a slightly modified version from WordPress's `WP_Error` class:

<div class="break-out">

<pre><code class="language-javascript">class Error {

  protected $errors = array();
  protected $error_data = array();

  public function __construct($code = null, $message = null, $data = null) 
  {
    if ($code) {
      $this->errors[$code][] = $message;
      if ($data) {
        $this->error_data[$code] = $data;
      }
    }
  }

  public function getErrorCodes()
  {
    return array_keys($this->errors);
  }

  public function getErrorCode()
  {    
    if ($codes = $this->getErrorCodes()) {
      return $codes[0];
    }

    return null;
  }

  public function getErrorMessages($code = null)
  {    
    if ($code) {
      return $this->errors[$code] ?? [];
    }

    // Return all messages if no code specified.
    return array_reduce($this->errors, 'array_merge', array());
  }

  public function getErrorMessage($code = null)
  {
    if (!$code) {
      $code = $this->getErrorCode();
    }
    $messages = $this->getErrorMessages($code);
    return $messages[0] ?? '';
  }

  public function getErrorData($code = null)
  {
    if (!$code) {
      $code = $this->getErrorCode();
    }

    return $this->error_data[$code];
  }

  public function add($code, $message, $data = null)
  {
    $this->errors[$code][] = $message;
    if ($data) {
      $this->error_data[$code] = $data;
    }
  }

  public function addData($data, $code = null)
  {
    if (!$code) {
      $code = $this->getErrorCode();
    }

    $this->error_data[$code] = $data;
  }

  public function remove($code)
  {
    unset($this->errors[$code]);
    unset($this->error_data[$code]);
  }
}</code></pre>
</div>

We implement a function to convert from the CMS to the abstract error through a helper class:

<div class="break-out">

<pre><code class="language-javascript">class WPHelpers
{
  public static function returnResultOrConvertError($result)
  {
    if (is_wp_error($result)) {
      // Create a new instance of the abstracted error class
      $error = new Error();
      foreach ($result->get_error_codes() as $code) {
        $error->add($code, $result->get_error_message($code), $result->get_error_data($code));
      }
      return $error;
    }
    return $result;
  }
}</code></pre>
</div>

And we finally invoke this method for all functions that may return an error:

<pre><code class="language-javascript">class UserManagementService implements UserManagementInterface
{
  public function getPasswordResetKey($user_id)
  {
    $result = get_password_reset_key($user_id);
    return WPHelpers::returnResultOrConvertError($result);
  }
}</code></pre>

#### Error codes and messages:

Every CMS will have its own set of error codes and corresponding explanatory messages. For instance, WordPress function `get_password_reset_key` can fail due to the following reasons, as represented by their error codes and messages:

1. `"no_password_reset"`: Password reset is not allowed for this user.
2. `"no_password_key_update"`: Could not save password reset key to database.

In order to unify errors so that an error code and message is consistent across CMSs, we will need to inspect these and replace them with our custom ones (possibly in function `returnResultOrConvertError` explained above).

### Hooks

Abstracting hooks involves:

- the hook functionality;
- the hooks themselves.

Let's analyze these in turn.

#### Abstracting the hook functionality

WordPress offers the concept of "hooks": a mechanism through which we can change a default behavior or value (through "filters") and execute related functionality (through "actions"). Both Symfony and Laravel offer mechanisms somewhat related to hooks: Symfony provides an [event dispatcher](https://symfony.com/doc/current/components/event_dispatcher.html) component, and Laravel's mechanism is called [events](https://laravel.com/docs/6.x/events); these 2 mechanisms are similar, sending notifications of events that have already taken place, to be processed by the application through listeners. 

When comparing these 3 mechanisms (hooks, event dispatcher and events) we find that WordPress's solution is the simpler one to set-up and use: Whereas WordPress hooks enable to pass an unlimited number of parameters in the hook itself and to directly modify a value as a response from a filter, Symfony's component requires to instantiate a new object to pass additional information, and Laravel's solution suggests to run a command in Artisan (Laravel's CLI) to generate the files containing the event and listener objects. If all we desire is to modify some value in the application, executing a hook such as `$value = apply_filters("modifyValue", $value, $post_id);` is as simple as it can get.

In the [first part of this series](https://www.smashingmagazine.com/2019/11/abstracting-wordpress-code-cms-concepts/), I explained that the CMS-agnostic application already establishes a particular solution for dependency injection instead of relying on the solution by the CMS, because the application itself needs this functionality to glue its parts together. Something similar happens with hooks: they are such a powerful concept that the application can greatly benefit by making it available to the different CMS-agnostic packages (allowing them to interact with each other) and not leave this wiring-up to be implemented only at the CMS level. Hence, I have decided to already ship a solution for the "hook" concept in the CMS-agnostic application, and this solution is the one implemented by WordPress.

In order to decouple the CMS-agnostic hooks from those from WordPress, once again we must "code against interfaces, not implementations": We define a contract with the corresponding hook functions:

<div class="break-out">

<pre><code class="language-javascript">interface HooksAPIInterface
{
  public function addFilter(string $tag, $function_to_add, int $priority = 10, int $accepted_args = 1): void;
  public function removeFilter(string $tag, $function_to_remove, int $priority = 10): bool;
  public function applyFilters(string $tag, $value, ...$args);
  public function addAction(string $tag, $function_to_add, int $priority = 10, int $accepted_args = 1): void;
  public function removeAction(string $tag, $function_to_remove, int $priority = 10): bool;
  public function doAction(string $tag, ...$args): void;
}</code></pre>
</div>

Please notice that functions `applyFilters` and `doAction` are variadic, i.e. they can receive a variable amount of arguments through parameter `...$args`. By combining this feature (which was added to PHP in version 5.6, hence it was unavailable to WordPress until very recently) with argument unpacking, i.e. passing a variable amount of parameters `...$args` to a function, we can easily provide the implementation for WordPress:

<div class="break-out">

<pre><code class="language-javascript">class WPHooksAPI implements HooksAPIInterface
{
  public function addFilter(string $tag, $function_to_add, int $priority = 10, int $accepted_args = 1): void
  {
    add_filter($tag, $function_to_add, $priority, $accepted_args);
  }

  public function removeFilter(string $tag, $function_to_remove, int $priority = 10): bool
  {
    return remove_filter($tag, $function_to_remove, $priority);
  }

  public function applyFilters(string $tag, $value, ...$args)
  {
    return apply_filters($tag, $value, ...$args);
  }

  public function addAction(string $tag, $function_to_add, int $priority = 10, int $accepted_args = 1): void
  {
    add_action($tag, $function_to_add, $priority, $accepted_args);
  }

  public function removeAction(string $tag, $function_to_remove, int $priority = 10): bool
  {
    return remove_action($tag, $function_to_remove, $priority);
  }

  public function doAction(string $tag, ...$args): void
  {
    do_action($tag, ...$args);
  }
}</code></pre>
</div>

As for an application running on Symfony or Laravel, this contract can be satisfied by installing a CMS-agnostic package implementing WordPress-like hooks, such as [this one](https://github.com/tormjens/eventy), [this one](https://github.com/bainternet/PHP-Hooks) or [this one](https://github.com/voku/php-hooks).

Finally, whenever we need to execute a hook, we do it through the corresponding service:

<div class="break-out">

<pre><code class="language-javascript">$hooksAPIService = ContainerBuilderFactory::getInstance()->get('hooks_api');
$title = $hooksAPIService->applyFilters("modifyTitle", $title, $post_id);</code></pre>
</div>

{{% ad-panel-leaderboard %}} 

#### Abstracting the hooks themselves

We need to make sure that, whenever a hook is executed, a consistent action will be executed no matter which is the CMS. For hooks defined inside of our application that is no problem, since we can resolve them ourselves, most likely in our CMS-agnostic package. However, when the hook is provided by the CMS, such as action `"init"` (triggered when the system has been initialized) or filter `"the_title"` (triggered to modify a post's title) in WordPress, and we invoke these hooks, we must make sure that all other CMSs will process them correctly and consistently. (Please notice that this concerns hooks that make sense in every CMS, such as `"init"`; certain other hooks can be considered too specific to WordPress, such as filter `"rest_{$this->post_type}_query"` from a REST controller, so we don't need to abstract them.)

The solution I found is to hook into actions or filters defined exclusively in the application (i.e. not in the CMS), and to bridge from CMS hooks to application hooks whenever needed. For instance, instead of adding an action for hook `"init"` (as defined in WordPress), any code in our application must add an action on hook `"cms:init"`, and then we implement the bridge in the WordPress-specific package from `"init"` to `"cms:init"`:

<div class="break-out">

<pre><code class="language-javascript">$hooksAPIService->addAction('init', function() use($hooksAPIService) {
  $hooksAPIService->doAction('cms:init');
});</code></pre>
</div>

Finally, the application can add a "loose contract" name for `"cms:init"`, and the CMS-specific package must implement it (as demonstrated earlier on).

### Routing

Different frameworks will provide different solutions for routing (i.e. the mechanism of identifying how the requested URL will be handled by the application), which reflect the architecture of the framework:

- In WordPress, [URLs map to database queries](https://wordpress.stackexchange.com/a/141087), not to routes.
- Symfony provides a [Routing component](https://symfony.com/doc/current/components/routing.html) which is independent (any PHP application can install it and use it), and which enables to define custom routes and which controller will process them.
- [Laravel's routing](https://laravel.com/docs/6.x/routing) builds on top of Symfony's routing component to adapt it to the Laravel framework.

As it can be seen, WordPress's solution is the outlier here: the concept of mapping URLs to database queries is tightly coupled to WordPress's architecture, and we would not want to restrict our abstracted application to this methodology (for instance, October CMS can be set-up as a flat-file CMS, in which case it doesn't use a database). Instead, it makes more sense to use Symfony's approach as its default behavior, and allow WordPress to override this behavior with its own routing mechanism.

(Indeed, while WordPress's approach works well for retrieving content, it is rather inappropriate when we need to access some functionality, such as displaying a contact form. In this case, before the launch of Gutenberg, we were forced to create a page and add a shortcode `"[contact_form]"` to it as content, which is not as clean as simply mapping the route to its corresponding controller directly.)

Hence, the routing for our abstracted application will not be based around the modeled entities (post, page, category, tag, author) but purely on custom-defined routes. This should already work perfectly for Symfony and Laravel, using their own solutions, and there is not much for us to do other than injecting the routes with the corresponding controllers into the application's configuration. 

To make it work in WordPress, though, we need to take some extra steps: We must introduce an external library to handle routing, such as [Cortex](https://github.com/Brain-WP/Cortex). Making use of Cortex, the application running on WordPress can have it both ways:

- if there is a custom-defined route matching the requested URL, use its corresponding controller.
- if not, let WordPress handle the request in its own way (i.e. retrieving the matched database entity or returning a 404 if no match is successful).

To implement this functionality, I have designed the contract `CMSRoutingInterface` to, given the requested URL, calculate two pieces of information:

- the actual route, such as `contact`, `posts` or `posts/my-first-post`.
- the nature of the route: core nature values `"standard"`, `"home"` and `"404"`, and additional nature values added through packages such as `"post"` through a "Posts" package or `"user"` through a "Users" package.

The nature of the route is an artificial construction that enables the CMS-agnostic application to identify if the route has extra qualities attached to it. For instance, when requesting the URL for a single post in WordPress, the corresponding database object post is loaded into the global state, under `global $post`. It also helps identify which case we want to handle, to avoid inconsistencies. For instance, we could have defined a custom route `contact` handled by a controller, which will have nature `"standard"`, and also a page in WordPress with slug `"contact"`, which will have nature `"page"` (added through a package called "Pages"). Then, our application can prioritize which way to handle the request, either through the controller or through a database query.

Let's implement it. We first define the service's contract:

<pre><code class="language-javascript">interface CMSRoutingInterface
{
  public function getNature();
  public function getRoute();
}</code></pre>

We can then define an abstract class which provides a base implementation of these functions:

<div class="break-out">

<pre><code class="language-javascript">abstract class AbstractCMSRouting implements CMSRoutingInterface
{
  const NATURE_STANDARD = 'standard';
  const NATURE_HOME = 'home';
  const NATURE_404 = '404';

  public function getNature()
  {
    return self::NATURE_STANDARD;
  }

  public function getRoute()
  {
    // By default, the URI path is already the route (minus parameters and trailing slashes)
    $route = $_SERVER['REQUEST_URI'];
    $params_pos = strpos($route, '?');
    if ($params_pos !== false) {
       $route = substr($route, 0, $params_pos);
    }
    return trim($route, '/');
  }
}</code></pre>
</div>

And the implementation is overriden for WordPress:

<div class="break-out">

<pre><code class="language-javascript">class WPCMSRouting extends AbstractCMSRouting
{
  const ROUTE_QUERY = [
    'custom_route_key' => 'custom_route_value',
  ];
  private $query;
  private function init()
  {
    if (is_null($this->query)) {
      global $wp_query;
      $this->query = $wp_query;
    }
  }

  private function isStandardRoute() {
    return !empty(array_intersect($this->query->query_vars, self::ROUTE_QUERY));
  }

  public function getNature()
  {
    $this->init();
    if ($this->isStandardRoute()) {
      return self::NATURE_STANDARD;
    } elseif ($this->query->is_home() || $this->query->is_front_page()) {
      return self::NATURE_HOME;
    } elseif ($this->query->is_404()) {
      return self::NATURE_404;
    }

    // Allow components to implement their own natures
    $hooksAPIService = ContainerBuilderFactory::getInstance()->get('hooks_api');
    return $hooksAPIService->applyFilters(
      "nature",
      parent::getNature(),
      $this->query
    );
  }
}</code></pre>
</div>

In the code above, please notice how constant `ROUTE_QUERY` is used by the service to know if the route is a custom-defined one, as configured through Cortex:

<div class="break-out">

<pre><code class="language-javascript">$hooksAPIService->addAction(
  'cortex.routes', 
  function(RouteCollectionInterface $routes) {  
    // Hook into filter "routes" to provide custom-defined routes
    $appRoutes = $hooksAPIService->applyFilters("routes", []);
    foreach ($appRoutes as $route) {
      $routes->addRoute(new QueryRoute(
        $route,
        function (array $matches) {
          return WPCMSRouting::ROUTE_QUERY;
        }
      ));
    }
  }
);</code></pre>
</div>

Finally, we add our routes through hook `"routes"`:

<pre><code class="language-javascript">$hooksAPIService->addFilter(
  'routes',
  function($routes) {
    return array_merge(
      $routes,
      [
        'contact',
        'posts',
      ]
    );
  }
);</code></pre>

Now, the application can find out the route and its nature, and proceed accordingly (for instance, for a `"standard"` nature invoke its controller, or for a `"post"` nature invoke WordPress's templating system):

<div class="break-out">

<pre><code class="language-javascript">$cmsRoutingService = ContainerBuilderFactory::getInstance()->get('routing');
$nature = $cmsRoutingService->getNature();
$route = $cmsRoutingService->getRoute();
// Process the requested route, as appropriate
// ...</code></pre>
</div>

### Object properties

A rather inconvenient consequence of abstracting our code is that we can't reference the properties from an object directly, and we must do it through a function instead. This is because different CMSs will represent the same object as containing different properties, and it is easier to abstract a function to access the object properties than to abstract the object itself (in which case, among other disadvantages, we may have to reproduce the object caching mechanism from the CMS). For instance, a post object `$post` contains its ID under `$post->ID` in WordPress and under `$post->id` in October CMS. To resolve this property, our contract `PostObjectPropertyResolverInterface` will contain function `getId`:

<pre><code class="language-javascript">interface PostObjectPropertyResolverInterface {
  public function getId($post);
}</code></pre>

Which is resolved for WordPress like this:

<div class="break-out">

<pre><code class="language-javascript">class WPPostObjectPropertyResolver implements PostObjectPropertyResolverInterface {
  public function getId($post)
  {
    return $post->ID;
  }
}</code></pre>
</div>

Similarly, the post content property is `$post->post_content` in WordPress and `$post->content` in October CMS. Our contract will then allow to access this property through function `getContent`:

<pre><code class="language-javascript">interface PostObjectPropertyResolverInterface {
  public function getContent($post);
}</code></pre>

Which is resolved for WordPress like this:

<div class="break-out">

<pre><code class="language-javascript">class WPPostObjectPropertyResolver implements PostObjectPropertyResolverInterface {
  public function getContent($post)
  {
    return $post->post_content;
  }
}</code></pre>
</div>

Please notice that function `getContent` receives the object itself through parameter `$post`. This is because we are assuming the content will be a property of the post object in all CMSs. However, we should be cautious on making this assumption, and decide on a property by property basis. If we don't want to make the previous assumption, then it makes more sense for function `getContent` to receive the post's ID instead:

<pre><code class="language-javascript">interface PostObjectPropertyResolverInterface {
  public function getContent($post_id);
}</code></pre>

Being more conservative, the latter function signature makes the code potentially more reusable, however it is also less efficient, because the implementation will still need to retrieve the post object:

<div class="break-out">

<pre><code class="language-javascript">class WPPostObjectPropertyResolver implements PostObjectPropertyResolverInterface {
  public function getContent($post_id)
  {
    $post = get_post($post_id);
    return $post->post_content;
  }
}</code></pre>
</div>

In addition, some properties may be needed in their original value and also after applying some processing; for these cases, we will need to implement a corresponding extra function in our contract. For instance, the post content needs be accessed also as HTML, which is done through executing `apply_filters('the_content', $post->post_content)` in WordPress, or directly through property `$post->content_html` in October CMS. Hence, our contract may have 2 functions to resolve the content property:

<pre><code class="language-javascript">interface PostObjectPropertyResolverInterface {
  public function getContent($post_id); // = raw content
  public function getHTMLContent($post_id);
}</code></pre>

We must also be concerned with abstracting the value that the property can have. For instance, a comment is approved in WordPress if its property `comment_approved` has the value `"1"`. However, other CMSs may have a similar property with value `true`. Hence, the contract should remove any potential inconsistency or ambiguity:

<pre><code class="language-javascript">interface CommentObjectPropertyResolverInterface {
  public function isApproved($comment);
}</code></pre>

Which is implemented for WordPress like this:

<div class="break-out">

<pre><code class="language-javascript">class WPCommentObjectPropertyResolver implements CommentObjectPropertyResolverInterface {
  public function isApproved($comment)
  {
    return $comment->comment_approved == "1";
  }
}</code></pre>
</div>

### Global state

WordPress sets several variables in the global context, such as `global $post` when querying a single post. Keeping variables in the global context is considered an anti-pattern, since the developer could unintentionally override their values, producing bugs that are difficult to track down. Hence, abstracting our code gives us the chance to implement a better solution.

An approach we can take is to create a corresponding class `AppState` which simply contains a property to store all variables that our application will need. In addition to initializing all core variables, we enable components to initialize their own ones through hooks:

<div class="break-out">

<pre><code class="language-javascript">class AppState
{
  public static $vars = [];

  public static function getVars()
  {
    return self::$vars;
  }

  public static function initialize()
  {
    // Initialize core variables
    self::$vars['nature'] = $cmsRoutingService->getNature();
    self::$vars['route'] = $cmsRoutingService->getRoute();

    // Initialize $vars through hooks
    self::$vars = $hooksAPIService->applyFilters("AppState:init", self::$vars);

    return self::$vars;
  }
}</code></pre>
</div>

To replace `global $post`, a hook from WordPress can then set this data through a hook. A first step would be to set the data under `"post-id"`:

<pre><code class="language-javascript">$hooksAPIService->addFilter(
  "AppState:init", 
  function($vars) {
    if (is_single()) {
      global $post;
      $vars['post-id'] => $post->ID;
    }
    return $vars;
  }
);</code></pre>

However, we can also abstract the global variables: instead of dealing with fixed entities (such as posts, users, comments, etc), we can deal with the entity in a generic way through `"object-id"`, and we obtain its properties by inquiring the nature of the requested route:

<pre><code class="language-javascript">$hooksAPIService->addFilter(
  "AppState:init", 
  function($vars) {
    if ($vars['nature'] == 'post') {
      global $post;
      $vars['object-id'] => $post->ID;
    }
    return $vars;
  }
);</code></pre>

From now own, if we need to display a property of the current post, we access it from the newly defined class instead of the global context:

<pre><code class="language-javascript">$vars = AppState::getVars();
$object_id = $vars['object-id'];
// Do something with it
// ...</code></pre>

### Entity models (meta, post types, pages being posts, and taxonomies —tags and categories—)

We must abstract those decisions made for WordPress concerning how its entities are modeled. Whenever we consider that WordPress's opinionatedness makes sense in a generic context too, we can then replicate such a decision for our CMS-agnostic code.

#### Meta:

As mentioned earlier, the concept of "meta" must be decoupled from the model entity (such as "post meta" from "posts"), so if a CMS doesn't provide support for meta, it can then discard only this functionality.

Then, package "Post Meta" (decoupled from, but dependent on, package "Posts") defines the following contract:

<div class="break-out">

<pre><code class="language-javascript">interface PostMetaAPIInterface
{
  public function getMetaKey($meta_key);
  public function getPostMeta($post_id, $key, $single = false);
  public function deletePostMeta($post_id, $meta_key, $meta_value = '');
  public function addPostMeta($post_id, $meta_key, $meta_value, $unique = false);
  public function updatePostMeta($post_id, $meta_key, $meta_value);
}</code></pre>
</div>

Which is resolved for WordPress like this:

<div class="break-out">

<pre><code class="language-javascript">class WPPostMetaAPI implements PostMetaAPIInterface
{
  public function getMetaKey($meta_key)
  {
    return '_'.$meta_key;
  }
  public function getPostMeta($post_id, $key, $single = false)
  {
    return get_post_meta($post_id, $key, $single);
  }
  public function deletePostMeta($post_id, $meta_key, $meta_value = '')
  {
    return delete_post_meta($post_id, $meta_key, $meta_value);
  }
  public function addPostMeta($post_id, $meta_key, $meta_value, $unique = false)
  {
    return add_post_meta($post_id, $meta_key, $meta_value, $unique);
  }
  public function updatePostMeta($post_id, $meta_key, $meta_value)
  {
    return update_post_meta($post_id, $meta_key, $meta_value);
  }
}</code></pre>
</div>

#### Post types:

I have decided that WordPress's concept of a custom post type, which allows to model entities (such as an event or a portfolio) as extensions of posts, can apply in a generic context, and as such, I have replicated this functionality in the CMS-agnostic code. This decision is controversial, however, I justify it because the application may need to display a feed of entries of different types (such as posts, events, etc) and custom post types make such implementation feasible. Without custom post types, I would expect the application to need to execute several queries to bring the data for every entity type, and the logic would get all muddled up (for instance, if fetching 12 entries, should we fetch 6 posts and 6 events? but what if the events were posted much earlier than the last 12 posts? and so on).

What happens when the CMS doesn't support this concept? Well, nothing serious happens: a post will still indicate its custom post type to be a "post", and no other entities will inherit from the post. The application will still work properly, just with some slight overhead from the unneeded code. This is a trade-off that, I believe, is more than worth it.

To support custom post types, we simply add a function `getPostType` in our contract:

<pre><code class="language-javascript">interface PostAPIInterface
{
  public function getPostType($post_id);
}</code></pre>

Which is resolved for WordPress like this:

<pre><code class="language-javascript">class WPPostAPI implements PostAPIInterface
{
  public function getPostType($post_id) {
    return get_post_type($post_id);
  }
}</code></pre>

#### Pages being posts:

While I justify keeping custom post types in order to extend posts, I don't justify a page being a post, as it happens in WordPress, because in other CMSs these entities are completely decoupled and, more importantly, a page may have higher rank than a post, so making a page extend from a post would make no sense. For instance, October CMS ships pages in its core functionality, but posts must be installed through plugins.

Hence we must create separate contracts for posts and pages, even though they may contain the same functions:

<pre><code class="language-javascript">interface PostAPIInterface
{
  public function getTitle($post_id);
}

interface PageAPIInterface
{
  public function getTitle($page_id);
}</code></pre>

To resolve these contracts for WordPress and avoid duplicating code, we can implement the common functionality through a trait:

<pre><code class="language-javascript">trait WPCommonPostFunctions
{
  public function getTitle($post_id)
  {
    return get_the_title($post_id);
  }
}

class WPPostAPI implements PostAPIInterface
{
  use WPCommonPostFunctions;
}

class WPPageAPI implements PageAPIInterface
{
  use WPCommonPostFunctions;
}</code></pre>

#### Taxonomies (tags and categories):

Once again, we can't expect all CMSs to support what is called taxonomies in WordPress: tags and categories. Hence, we must implement this functionality through a package "Taxonomies", and, assuming that tags and categories are added to posts, make this package dependent on package "Posts".

<pre><code class="language-javascript">interface TaxonomyAPIInterface
{
  public function getPostCategories($post_id, $options = []);
  public function getPostTags($post_id, $options = []);
  public function getCategories($query, $options = []);
  public function getTags($query, $options = []);
  public function getCategory($cat_id);
  public function getTag($tag_id);
  ...
}</code></pre>

We could have decided to create two separate packages "Categories" and "Tags" instead of "Taxonomies", however, as the implementation in WordPress makes evident, a tag and a category are basically the same concept of entity with only a tiny difference: categories are hierarchical (i.e. a category can have a parent category), but tags are not. Then, I consider that it makes sense to keep this concept for a generic context, and shipped under a single package "Taxonomies".

We must pay attention that certain functionalities involve both posts and taxonomies, and these must be appropriately decoupled. For instance, in WordPress we can retrieve posts that were tagged `"politics"` by executing `get_posts(['tag' => "politics"])`. In this case, while function `getPosts` must be implemented in package "Posts", filtering by tags must be implemented in package "Taxonomies". To accomplish this separation, we can simply execute a hook in the implementation of function `getPosts` for WordPress, allowing any component to modify the arguments before executing `get_posts`:

<pre><code class="language-javascript">class WPPostAPI implements PostAPIInterface
{
  public function getPosts($args) {
    $args = $hooksAPIService->applyFilters("modifyArgs", $args);
    return get_posts($args);
  }
}</code></pre>

And finally we implement the hook in package "Taxonomies for WordPress":

<pre><code class="language-javascript">$hooksAPIService->addFilter(
  'modifyArgs',
  function($args) {
    if (isset($args['tags'])) {
      $args['tag'] = implode(',', $args['tags']);
      unset($args['tags']);
    }
    if (isset($args['categories'])) {
      $args['cat'] = implode(',', $args['categories']);
      unset($args['categories']);
    }
    return $args;
  }
);</code></pre>

Please notice that in the abstracted code the attributes were re-defined (following the recommendations for abstracting function parameters, explained earlier on): `"tag"` must be provided as `"tags"` and `"cat"` must be provided as `"categories"` (shifting the connotation from singular to plural), and these values must be passed as arrays (i.e. removed accepting comma-separated strings as in WordPress, to add consistency).

### Translation

Because calls to translate strings are spread all over the application code, translation is not a functionality that we can opt out from, and we should make sure that the other frameworks are compatible with our chosen translation mechanism. 

In WordPress, which [implements internationalization through gettext](https://codex.wordpress.org/I18n_for_WordPress_Developers#Introduction_to_Gettext), we are required to set-up translation files for each locale code (such as 'fr_FR', which is the code for **fr**ench language from **FR**ance), and these can be set under a text domain (which allows themes or plugins to define their own translations without fear of collision with the translations from other pieces of code). We don't need to check for support for placeholders in the string to translate (such as when doing `sprintf(__("Welcome %s"), $user_name)`), because function `sprintf` belongs to PHP and not to the CMS, so it will always work.

Let's check if the other frameworks support the required two properties, i.e. getting the translation data for a specific locale composed of language and country, and under a specific text domain:

- [Symfony's translation component](https://symfony.com/doc/current/components/translation.html) supports these two properties.
- The locale used in [Laravel's localization](https://laravel.com/docs/6.x/localization) involves the language but not the country, and text domains are not supported (they could be replicated through overriding package language files, but the domain is not explicitly set, so the contract and the implementation would be inconsistent with each other).

However, luckily there is library [Laravel Gettext](https://github.com/zerospam/laravel-gettext) which can replace Laravel's native implementation with Symfony's translation component. Hence, we got support for all frameworks, and we can rely on a WordPress-like solution.

We can then define our contract mirroring the WordPress function signatures:

<pre><code class="language-javascript">interface TranslationAPIInterface
{
  public function __($text, $domain = 'default');
  public function _e($text, $domain = 'default');
}</code></pre>

The implementation of the contract for WordPress is like this:

<pre><code class="language-javascript">class WPTranslationAPI implements TranslationAPIInterface
{
  public function __($text, $domain = 'default')
  {
    return __($text, $domain);
  }
  public function _e($text, $domain = 'default')
  {
    _e($text, $domain);
  }
}</code></pre>

And to use it in our application, we do:

<div class="break-out">

<pre><code class="language-javascript">$translationAPI = ContainerBuilderFactory::getInstance()->get('translation_api');
$text = $translationAPI->__("translate this", "my-domain");</code></pre>
</div>

### Media

WordPress has media management as part of its core functionality, which represents a media element as an entity all by itself, and allows to manipulate the media element (such as cropping or resizing images), but we can't expect all CMSs to have similar functionality. Hence, media management must be decoupled from the CMS core functionality. 

For the corresponding contract, we can mirror the WordPress media functions, but removing WordPress's opinionatedness. For instance, in WordPress, a media element is a post (with post type `"attachment"`), but for the CMS-agnostic code it is not, hence the parameter must be `$media_id` (or `$image_id`) instead of `$post_id`. Similarly, WordPress treats media as attachments to posts, but this doesn't need to be the case everywhere, hence we can remove the word "attachment" from the function signatures. Finally, we can decide to keep the `$size` of the image in the contract; if the CMS doesn't support creating multiple image sizes for an image, then it can just fall back on its default value `NULL` and nothing grave happens:

<div class="break-out">

<pre><code class="language-javascript">interface MediaAPIInterface
{
  public function getImageSrcAndDimensions($image_id, $size = null): array;
  public function getImageURL($image_id, $size = null): string;
}</code></pre>
</div>

The response by function `getImageSrcAndDimensions` can be asbtracted too, returning an array of our own design instead of simply re-using the one from the WordPress function `wp_get_attachment_image_src`:

<div class="break-out">

<pre><code class="language-javascript">class WPMediaAPI implements MediaAPIInterface
{
  public function getImageSrcAndDimensions($image_id, $size = null): array
  {
    $img_data = wp_get_attachment_image_src($image_id, $size);
    return [
      'src' => $img_data[0],
      'width' => $img_data[1],
      'height' => $img_data[2],
    ];
  }
  public function getImageURL($image_id, $size = null): string
  {
    return wp_get_attachment_image_url($image_id, $size);
  }
}</code></pre>
</div>

## Conclusion

Setting-up a CMS-agnostic architecture for our application can be a painful endeavor. As it was demonstrated in this article, abstracting all the code was a lengthy process, taking plenty of time and energy to achieve, and it is not even finished yet. I wouldn't be surprised if the reader is intimidated by the idea of going through this process in order to convert a WordPress application into a CMS-agnostic one. If I hadn't done the abstraction myself, I would certainly be intimidated too.

My suggestion is for the reader is to analyze if going through this process makes sense based on a project-by-project basis. If there is no need whatsoever to port an application to a different CMS, then you will be right to stay away from this process and stick to the WordPress way. However, if you do need to migrate an application away from WordPress and want to reduce the effort required, or if you already need to maintain several codebases which would benefit from code reusability, or even if you may migrate the application sometime in the future and you have just started a new project, then this process is for you. It may be painful to implement, but well worth it. I know because I've been there. But I've survived, and I'd certainly do it again. Thanks for reading.

{{< signature "dm, yk, il" >}}
