---
title: How To Use Autoloading And A Plugin Container In WordPress Plugins
slug: how-to-use-autoloading-and-a-plugin-container-in-wordpress-plugins
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3b435cda-ef6b-4df5-abcb-b3afa8dc3cdc/green-wp-plugins-illu-opt.jpg
date: 2015-05-29T20:36:40.000Z
author: nicoamarilla
description: >-
  Building and
  [maintaining](https://shop.smashingmagazine.com/products/wordpress-maintenance-keeping-your-website-safe-and-efficient)
  a WordPress plugin can be a daunting task. **The bigger the codebase, the
  harder it is to keep track** of all the working parts and their relationship
  to one another. And you can add to that the limitations imposed by working in
  an antiquated version of PHP, 5.2.

  In this article we will explore an alternative way of developing WordPress
  plugins, using the lessons learned from the greater PHP community, the world
  outside WordPress. We will walk through the steps of creating a plugin and
  investigate the use of autoloading and a plugin container.
categories:
  - WordPress
  - PHP
  - Plugins
  - Techniques (WP)
---
Building and <a href="https://shop.smashingmagazine.com/products/wordpress-maintenance-keeping-your-website-safe-and-efficient">maintaining</a> a WordPress plugin can be a daunting task. <strong>The bigger the codebase, the harder it is to keep track</strong> of all the working parts and their relationship to one another. And you can add to that the limitations imposed by working in an antiquated version of PHP, 5.2.

In this article we will explore an alternative way of developing WordPress plugins, using the lessons learned from the greater PHP community, the world outside WordPress. We will walk through the steps of creating a plugin and investigate the use of autoloading and a plugin container.</p>

## <span class="rh">Further Reading</span> on SmashingMag: [Link](https://www.smashingmagazine.com/2011/09/how-to-create-a-wordpress-plugin/#further-reading-on-smashingmag)

*   [Ten Things Every WordPress Plugin Developer Should Know](https://www.smashingmagazine.com/2011/03/ten-things-every-wordpress-plugin-developer-should-know/)
*   [Making A WordPress Plugin That Uses Service APIs](https://www.smashingmagazine.com/2016/03/making-a-wordpress-plugin-that-uses-service-apis/)
*   [How Commercial Plugin Developers Are Using The Repository](https://www.smashingmagazine.com/2012/01/commercial-plugin-developers-wordpress-repository/)
*   [How To Improve Your WordPress Plugin’s Readme.txt](https://www.smashingmagazine.com/2011/11/improve-wordpress-plugins-readme-txt/)

## Let's Begin

The first thing you need to do when creating a plugin is to give it a unique name. The name is important as it will be the basis for all our unique identifiers (function prefix, class prefix, textdomain, option prefix, etc.). The name should also be unique across the wordpress.org space. It won't hurt if we make the name catchy. F<strong>or our sample plugin I chose the name Simplarity</strong>, a play on the words "simple" and "clarity".

{{% feature-panel %}}

We'll assume you have a working WordPress installation already.</p>

### Folder Structure

First, create a directory named <i>simplarity</i> inside <i>wp-content/plugins</i>. Inside it create the following structure:

*   _simplarity.php_: our main plugin file
*   _css/_: directory containing our styles
*   _js/_: directory containing JavaScript files
*   _languages/_: directory that will contain translation files
*   _src/_: directory containing our classes
*   _views/_: directory that will contain our plugin view files

### The Main Plugin File

Open the main plugin file, <i>simplarity.php</i>, and add the plugin information header:

<pre><code class="language-php">&lt;?php
/*
Plugin Name: Simplarity
description: >-
  A plugin for smashingmagazine.com
Version: 1.0.0
License: GPL-2.0+
*/</code></pre>

This information is enough for now. The plugin name, description, and version will show up in the plugins area of WordPress admin. The license details are important to let your users know that this is an open source plugin. A full list of header information can found in the <a href="https://codex.wordpress.org/Writing_a_Plugin">WordPress codex</a>.</p>

## Autoloading

Autoloading allows you to automatically load classes using an <strong>autoloader</strong> so you don't have to manually include the files containing the class definitions. For example, whenever you need to use a class, you need to do the following:

<pre><code class="language-php">require_once '/path/to/classes/class-container.php';
require_once '/path/to/classes/class-view.php';
require_once '/path/to/classes/class-settings-page.php';

$plugin = new Container();
$view = new View();
$settings_page = new SettingsPage();
</code></pre>

With autoloading, you can use an autoloader instead of multiple <code><a href="https://php.net/manual/en/function.require-once.php">require_once</a></code> statements. It also eliminates the need to update these require statements whenever you add, rename, or change the location of your classes. That’s a big plus for maintainability.

### Adopting The PEAR Naming Convention For Class Names

Before we create our autoloader we need to create a convention for our class names and their location in the file system. This will aid the autoloader in mapping out the class to its source file.

For our class names we will adopt the <a href="https://pear.php.net/manual/en/standards.naming.php">PEAR naming convention</a>. The gist is that class names are alphabetic characters in StudlyCaps. Each level of the hierarchy is separated with a single underscore. Class names will directly map to the directories in which they are stored.

It's easier to illustrate it using examples:

*   A class named **Simplarity_Plugin** would be defined in the file _src/Simplarity/Plugin.php_.
*   A class named **Simplarity_SettingsPage** would be defined in _src/Simplarity/SettingsPage.php_.

As you can see with this convention, the autoloader will just replace the underscores with directory separators to locate the class definition.</p>

### What About The WordPress Coding Standards For Class Names?

As you might be aware, WordPress has its own <a href="https://make.wordpress.org/core/handbook/coding-standards/php/#naming-conventions">naming convention</a> for class names. It states:
<blockquote>Class names should use capitalized words separated by underscores. Any acronyms should be all upper case. […] Class file names should be based on the class name with <code>class-</code> prepended and the underscores in the class name replaced with hyphens, for example <code>WP_Error</code> becomes <code>class-wp-error.php</code></blockquote>

I know that we should follow the standards of the platform that we are developing on. However, we suggest using the PEAR naming convention because:

*   WP coding standards do not cover autoloading.
*   WP does not follow its own coding standards. Examples: _class.wp-scripts.php_ and SimplePie. This is understandable since WordPress grew organically.
*   Interoperability allows you to easily use third-party libraries that follow the PEAR naming convention, like Twig. And conversely, you can easily port your code to other libraries sharing the same convention.
*   It's important your autoloader is future-ready. When WordPress decides to up the ante and finally move to PHP 5.3 as its minimum requirement, you can easily update the code to be PSR-0 or PSR-4-compatible and take advantage of the built-in namespaces instead of using prefixes. This is a big plus for interoperability.

Note that we are only using this naming convention for classes. The rest of our code will still follow the WordPress coding standards. It's important to follow and respect the standards of the platform that we are developing on.

Now that we have fully covered the naming convention, we can finally build our autoloader.</p>

## Building Our Autoloader

Open our main plugin file and add the following code below the plugin information header:

<pre><code class="language-php">spl_autoload_register( 'simplarity_autoloader' );
function simplarity_autoloader( $class_name ) {
  if ( false !== strpos( $class_name, 'Simplarity' ) ) {
    $classes_dir = realpath( plugin_dir_path( __FILE__ ) ) . DIRECTORY_SEPARATOR . 'src' . DIRECTORY_SEPARATOR;
    $class_file = str_replace( '_', DIRECTORY_SEPARATOR, $class_name ) . '.php';
    require_once $classes_dir . $class_file;
  }
}
</code></pre>

At the heart of our autoloading mechanism is PHP's built in <a href="https://php.net/manual/en/function.spl-autoload-register.php"><code>spl_autoload_register</code></a> function. All it does is register a function to be called automatically when your code references a class that hasn’t been loaded yet.

The first line tells <code>spl_autoload_register</code> to register our function named <code>simplarity_autoloader</code>:

<pre><code class="language-php">spl_autoload_register( 'simplarity_autoloader' );</code></pre>

Next we define the <i>simplarity_autoloader</i> function:

<pre><code class="language-php">function simplarity_autoloader( $class_name ) {
  …
}
</code></pre>

Notice that it accepts a <code>$class_name</code> parameter. This parameter holds the class name. For example when you instantiate a class using <code>$plugin = new Simplarity_Plugin()</code>, <code>$class_name</code> will contain the string "Simplarity_Plugin". Since we are adding this function in the global space, it's important that we have it prefixed with <code>simplarity_</code>.

The next line checks if <code>$classname</code> contains the string "Simplarity" which is our top level namespace:

<pre><code class="language-php">if ( false !== strpos( $class_name, 'Simplarity' ) ) {
</code></pre>

This will ensure that the autoloader will only run on our classes. Without this check, our autoloader will run every time an unloaded class is referenced, even if the class is not ours, which is not ideal.

The next line constructs the path to the directory where our classes reside:

<pre><code class="language-php">$classes_dir = realpath( plugin_dir_path( __FILE__ ) ) . DIRECTORY_SEPARATOR . 'src' . DIRECTORY_SEPARATOR;
</code></pre>

It uses WP's <a href="https://codex.wordpress.org/Function_Reference/plugin_dir_path"><code>plugin_dir_path</code></a> to get the plugin root directory. <code>__FILE__</code> is a <a href="https://php.net/manual/en/language.constants.predefined.php">magic constant</a> that contains the full path and filename of the current file. <code>DIRECTORY_SEPARATOR</code> is a predefined constant that contains either a forward slash or backslash depending on the OS your web server is on. We also use <a href="https://php.net/manual/en/function.realpath.php"><code>realpath</code></a> to normalize the file path.

This line resolves the path to the class definition file:

<pre><code class="language-php">$class_file = str_replace( '_', DIRECTORY_SEPARATOR, $class_name ) . '.php';
</code></pre>

It replaces the underscore (<code>_</code>) in <code>$class_name</code> with the directory separator and appends <code>.php</code>.

Finally, this line builds the file path to the definition and includes the file using <code>require_once</code>:

<pre><code class="language-php">require_once $classes_dir . $class_file;
</code></pre>

That's it! You now have an autoloader. Say goodbye to long lines of <code>require_once</code> statements.

## Plugin Container

A plugin container is a special class that holds together our plugin code. It simplifies the interaction between the many working parts of your code by providing a centralized location to manage the configuration and objects.</p>

### Uses Of Our Plugin Container

Here are the things we can expect from the plugin container:

*   ##### Store global parameters in a single location

    Often you'll find this code in plugins:

        define( 'SIMPLARITY_VERSION', '1.0.0' );
        define( 'SIMPLARITY_PATH', realpath( plugin_dir_path( __FILE__ ) ) . DIRECTORY_SEPARATOR );
        define( 'SIMPLARITY_URL', plugin_dir_url( __FILE__ ) );

    Instead of doing that, we could do this instead:

        $plugin = new Simplarity_Plugin();
        $plugin['version] = '1.0.0';
        $plugin['path'] = realpath( plugin_dir_path( __FILE__ ) ) . DIRECTORY_SEPARATOR;
        $plugin['url'] = plugin_dir_url( __FILE__ );

    This has the added benefit of not polluting the global namespace with our plugin's constants, which in most cases aren't needed by other plugins.
*   ##### Store objects in a single location

    Instead of scattering our class instantiations everywhere in our codebase we can just do this in a single location:

        $plugin = new Simplarity_Plugin();
        /…/
        $plugin['scripts'] = new Simplarity_Scripts(); // A class that loads javascript files

*   ##### Service definitions

    This is the most powerful feature of the container. A service is an object that does something as part of a larger system. Services are defined by functions that return an instance of an object. Almost any global object can be a service.

        $plugin['settings_page'] = function ( $plugin ) {
          return new SettingsPage( $plugin['settings_page_properties'] );
        };

    Services result in lazy initialization whereby objects are only instantiated and initialized when needed. It also allows us to easily implement a self-resolving dependency injection design. An example:

        $plugin = new Plugin();
        $plugin['door_width'] = 100;
        $plugin['door_height'] = 500;
        $plugin['door_size'] = function ( $plugin ) {
          return new DoorSize( $plugin['door_width'], $plugin['door_height'] );
        };
        $plugin['door'] = function ( $plugin ) {
          return new Door( $plugin['door_size'] );
        };
        $plugin['window'] = function ( $plugin ) {
          return new Window();
        };
        $plugin['house'] = function ( $plugin ) {
          return new House( $plugin['door'], $plugin['window'] );
        };
        $house = $plugin['house'];

    This is roughly equivalent to:

        $door_width = 100;
        $door_height = 500;
        $door_size = new DoorSize( $door_width, $door_height );
        $door = new Door( $door_size );
        $window = new Window();
        $house = new House( $door, $window );

    Whenever we get an object, as in `$house = $plugin['house'];` , the object is created (lazy initialization) and dependencies are resolved automatically.</p>

## Building The Plugin Container

Let's start by creating the plugin container class. We will name it "Simplarity_Plugin". As our naming convention dictates, we should create a corresponding file: <i>src/Simplarity/Plugin.php</i>.

Open <i>Plugin.php</i> and add the following code:

<pre><code class="language-php">&lt;?php
class Simplarity_Plugin implements ArrayAccess {
  protected $contents;

  public function __construct() {
    $this-&gt;contents = array();
  }

  public function offsetSet( $offset, $value ) {
    $this-&gt;contents[$offset] = $value;
  }

  public function offsetExists($offset) {
    return isset( $this-&gt;contents[$offset] );
  }

  public function offsetUnset($offset) {
    unset( $this-&gt;contents[$offset] );
  }

  public function offsetGet($offset) {
    if( is_callable($this-&gt;contents[$offset]) ){
      return call_user_func( $this-&gt;contents[$offset], $this );
    }
    return isset( $this-&gt;contents[$offset] ) ? $this-&gt;contents[$offset] : null;
  }

  public function run(){ 
    foreach( $this-&gt;contents as $key =&gt; $content ){ // Loop on contents
      if( is_callable($content) ){
        $content = $this[$key];
      }
      if( is_object( $content ) ){
        $reflection = new ReflectionClass( $content );
        if( $reflection-&gt;hasMethod( 'run' ) ){
          $content-&gt;run(); // Call run method on object
        }
      }
    }
  }
}
</code></pre>

The class implements the <code>ArrayAccess</code> interface:

<pre><code class="language-php">class Simplarity_Plugin implements ArrayAccess {</code></pre>

This allows us to use it like PHP's array:

<pre><code class="language-php">$plugin = new Simplarity_Plugin();
$plugin['version'] = '1.0.0'; // Simplicity is beauty
</code></pre>

The functions <code>offsetSet</code>, <code>offsetExists</code>, <code>offsetUnset</code> and <code>offsetGet</code> are required by <code>ArrayAccess</code> to be implemented. The <code>run</code> function will loop through the contents of the container and run the runnable objects.

To better illustrate our plugin container, let's start by building a sample plugin.</p>

## Example Plugin: A Settings Page

This plugin will add a settings page named "Simplarity" under WordPress Admin → Settings.

Let's go back to the main plugin file. Open up <i>simplarity.php</i> and add the following code. Add this below the autoloader code:

<pre><code class="language-php">add_action( 'plugins_loaded', 'simplarity_init' ); // Hook initialization function
function simplarity_init() {
  $plugin = new Simplarity_Plugin(); // Create container
  $plugin['path'] = realpath( plugin_dir_path( __FILE__ ) ) . DIRECTORY_SEPARATOR;
  $plugin['url'] = plugin_dir_url( __FILE__ );
  $plugin['version'] = '1.0.0';
  $plugin['settings_page_properties'] = array( 
    'parent_slug' =&gt; 'options-general.php',
    'page_title' =&gt;  'Simplarity',
    'menu_title' =&gt;  'Simplarity',
    'capability' =&gt; 'manage_options',
    'menu_slug' =&gt; 'simplarity-settings',
    'option_group' =&gt; 'simplarity_option_group',
    'option_name' =&gt; 'simplarity_option_name'
  );
  $plugin['settings_page'] = new Simplarity_SettingsPage( $plugin['settings_page_properties'] );
  $plugin-&gt;run();
}
</code></pre>

Here we use WP's <code>add_action</code> to hook our function <code>simplarity_init</code> into <code>plugins_loaded</code>:

<pre><code class="language-php">add_action( 'plugins_loaded', 'simplarity_init' );
</code></pre>

This is important as this will make our plugin overridable by using <code>remove_action</code>. An example use case would be a premium plugin overriding the free version.

Function <code>simplarity_init</code> contains our plugin's initialization code. At the start, we simply instantiate our plugin container:

<pre><code class="language-php">$plugin = new Simplarity_Plugin();
</code></pre>

These lines assign global configuration data:

<pre><code class="language-php">$plugin['path'] = realpath( plugin_dir_path( __FILE__ ) ) . DIRECTORY_SEPARATOR;
$plugin['url'] = plugin_dir_url( __FILE__ );
$plugin['version'] = '1.0.0';
</code></pre>

The plugin path contains the full path to our plugin, the <code>url</code> contains the URL to our plugin directory. They will come in handy whenever we need to include files and assets. <code>version</code> contains the current version of the plugin that should match the one in the header info. Useful whenever you need to use the version in code.

This next code assigns various configuration data to <code>settings_page_properties</code>:

<pre><code class="language-php">$plugin['settings_page_properties'] = array(
  'parent_slug' =&gt; 'options-general.php',
  'page_title' =&gt;  'Simplarity',
  'menu_title' =&gt;  'Simplarity',
  'capability' =&gt; 'manage_options',
  'menu_slug' =&gt; 'simplarity-settings',
  'option_group' =&gt; 'simplarity_option_group',
  'option_name' =&gt; 'simplarity_option_name'
);</code></pre>

These configuration data are related to <a href="https://codex.wordpress.org/Settings_API">WP settings API</a>.

This next code instantiates the settings page, passing along <code>settings_page_properties</code>:

<pre><code class="language-php">$plugin['settings_page'] = new Simplarity_SettingsPage( $plugin['settings_page_properties'] );</code></pre>

The <code>run</code> method is where the fun starts:

<pre><code class="language-php">$plugin-&gt;run();</code></pre>

It will call <code>Simplarity_SettingsPage</code>'s own <code>run</code> method.</p>

### The `Simplarity_SettingsPage` Class

Now we need to create the <code>Simplarity_SettingsPage</code> class. It's a class that groups together the settings API functions.

Create a file named <i>SettingsPage.php</i> in <i>src/Simplarity/</i>. Open it and add the following code:

<pre><code class="language-php">&lt;?php
class Simplarity_SettingsPage {
  protected $settings_page_properties;

  public function __construct( $settings_page_properties ){
    $this-&gt;settings_page_properties = $settings_page_properties;
  }

  public function run() {
    add_action( 'admin_menu', array( $this, 'add_menu_and_page' ) );
    add_action( 'admin_init', array( $this, 'register_settings' ) );
  }

  public function add_menu_and_page() { 

    add_submenu_page(
      $this-&gt;settings_page_properties['parent_slug'],
      $this-&gt;settings_page_properties['page_title'],
      $this-&gt;settings_page_properties['menu_title'], 
      $this-&gt;settings_page_properties['capability'],
      $this-&gt;settings_page_properties['menu_slug'],
      array( $this, 'render_settings_page' )
    );
  }

  public function register_settings() { 

    register_setting(
      $this-&gt;settings_page_properties['option_group'],
      $this-&gt;settings_page_properties['option_name']
    );   
  }

  public function get_settings_data(){
    return get_option( $this-&gt;settings_page_properties['option_name'], $this-&gt;get_default_settings_data() );
  }

  public function render_settings_page() {
    $option_name = $this-&gt;settings_page_properties['option_name'];
    $option_group = $this-&gt;settings_page_properties['option_group'];
    $settings_data = $this-&gt;get_settings_data();
    ?&gt;
    &lt;div class="wrap"&gt;
      &lt;h2&gt;Simplarity&lt;/h2&gt;
      &lt;p&gt;This plugin is using the settings API.&lt;/p&gt;
      &lt;form method="post" action="options.php"&gt;
        &lt;?php
        settings_fields( $this-&gt;plugin['settings_page_properties']['option_group']);
        ?&gt;
        &lt;table class="form-table"&gt;
          &lt;tr&gt;
              &lt;th&gt;&lt;label for="textbox"&gt;Textbox:&lt;/label&gt;&lt;/th&gt;
              &lt;td&gt;
                &lt;input type="text" id="textbox"
                  name="&lt;?php echo esc_attr( $option_name."[textbox]" ); ?&gt;"
                  value="&lt;?php echo esc_attr( $settings_data['textbox'] ); ?&gt;" /&gt;
              &lt;/td&gt;
          &lt;/tr&gt;
        &lt;/table&gt;
        &lt;input type="submit" name="submit" id="submit" class="button button-primary" value="Save Options"&gt;
      &lt;/form&gt;
    &lt;/div&gt;
    &lt;?php
  }

  public function get_default_settings_data() {
    $defaults = array();
    $defaults['textbox'] = ’;

    return $defaults;
  }
}
</code></pre>

The class property <code>$settings_page_properties</code> stores the settings related to WP settings API:

<pre><code class="language-php">&lt;?php
class Simplarity_SettingsPage {
  protected $settings_page_properties;
</code></pre>

The constructor function accepts the <code>settings_page_properties</code> and stores it:

<pre><code class="language-php">public function __construct( $settings_page_properties ){
  $this-&gt;settings_page_properties = $settings_page_properties;
}
</code></pre>

The values are passed from this line in the main plugin file:

<pre><code class="language-php">$plugin['settings_page'] = new Simplarity_SettingsPage( $plugin['settings_page_properties'] );</code></pre>

The <code>run</code> function is use to run startup code:

<pre><code class="language-php">public function run() {
  add_action( 'admin_menu', array( $this, 'add_menu_and_page' ) );
  add_action( 'admin_init', array( $this, 'register_settings' ) );
}
</code></pre>

The most likely candidate for startup code are <a href="https://codex.wordpress.org/Plugin_API/Filter_Reference">filters</a> and <a href="https://codex.wordpress.org/Plugin_API/Hooks">action hooks</a>. Here we add the action hooks related to our settings page.
Do not confuse this run method with the run method of the plugin container. This run method belongs to the settings page class.

This line hooks the <code>add_menu_and_page</code> function on to the <code>admin_menu</code> action:

<pre><code class="language-php">add_action( 'admin_menu', array( $this, 'add_menu_and_page' ) );</code></pre>

Function <code>add_submenu_page</code> in turn calls WP's <a href="https://codex.wordpress.org/add_submenu_page"><code>add_submenu_page</code></a> function to add a link under the WP Admin → Settings:

<pre><code class="language-php">public function add_menu_and_page() { 

  add_submenu_page(
    $this-&gt;settings_page_properties['parent_slug'],
    $this-&gt;settings_page_properties['page_title'],
    $this-&gt;settings_page_properties['menu_title'], 
    $this-&gt;settings_page_properties['capability'],
    $this-&gt;settings_page_properties['menu_slug'],
    array( $this, 'render_settings_page' )
  );

}
</code></pre>

As you can see, we are pulling the info from our class property <code>$settings_page_properties</code> which we specified in the main plugin file.

The parameters for <code>add_submenu_page</code> are:

*   `parent_slug`: slug name for the parent menu
*   `page_title`: text to be displayed in the `<title>` element of the page when the menu is selected
*   `menu_title`: text to be used for the menu
*   `capability`: the capability required for this menu to be displayed to the user
*   `menu_slug`: slug name to refer to this menu by (should be unique for this menu)
*   `function`: function to be called to output the content for this page

This line hooks the <code>register_settings</code> function on to the <code>admin_init</code> action:

<pre><code class="language-php">add_action( 'admin_init', array( $this, 'register_settings' ) );</code></pre>

<code>array( $this, 'register_settings' )</code> means to call <code>register_settings</code> on <code>$this</code>, which points to our <code>SettingsPage</code> instance.

The <code>register_settings</code> then calls WP's <code>register_setting</code> to register a setting:

<pre><code class="language-php">public function register_settings() { 

  register_setting(
    $this-&gt;settings_page_properties['option_group'],
    $this-&gt;settings_page_properties['option_name']
  );

}</code></pre>

Function <code>render_settings_page</code> is responsible for rendering the page:

<pre><code class="language-php">public function render_settings_page() {
  $option_name = $this-&gt;settings_page_properties['option_name'];
  $option_group = $this-&gt;settings_page_properties['option_group'];
  $settings_data = $this-&gt;get_settings_data();
  ?&gt;
  &lt;div class="wrap"&gt;
    &lt;h2&gt;Simplarity&lt;/h2&gt;
    &lt;p&gt;This plugin is using the settings API.&lt;/p&gt;
    &lt;form method="post" action="options.php"&gt;
      &lt;?php
      settings_fields( $option_group );
      ?&gt;
      &lt;table class="form-table"&gt;
        &lt;tr&gt;
          &lt;th&gt;&lt;label for="textbox"&gt;Textbox:&lt;/label&gt;&lt;/th&gt;
          &lt;td&gt;
            &lt;input type="text" id="textbox"
              name="&lt;?php echo esc_attr( $option_name."[textbox]" ); ?&gt;"
              value="&lt;?php echo esc_attr( $settings_data['textbox'] ); ?&gt;" /&gt;
          &lt;/td&gt;
        &lt;/tr&gt;
      &lt;/table&gt;
      &lt;input type="submit" name="submit" id="submit" class="button button-primary" value="Save Options"&gt;
    &lt;/form&gt;
  &lt;/div&gt;
  &lt;?php
}</code></pre>

We hooked <code>render_settings_page</code> earlier using <code>add_submenu_page</code>.

Function <code>get_settings_data</code> is a wrapper function for <code>get_option</code>:

<pre><code class="language-php">public function get_settings_data(){
    return get_option( $this-&gt;plugin['settings_page_properties']['option_name'] );
}</code></pre>

This is to easily get the settings data with a single function call.

Function <code>get_default_settings_data</code> is use to supply us with our own default values:

<pre><code class="language-php">public function get_default_settings_data() {
  $defaults = array();
  $defaults['textbox'] = ’;

  return $defaults;
}</code></pre>

## Abstracting Our Settings Page Class

Right now our settings page class cannot be reused if you want to create another subpage. Let's move the reusable code for the settings page to another class.

Let's call this class <code>Simplarity_WpSubPage</code>. Go ahead and create the file <i>src/Simplarity/WpSubPage.php</i>.

Now add the code below:

<pre><code class="language-php">&lt;?php
abstract class Simplarity_WpSubPage {
  protected $settings_page_properties;

  public function __construct( $settings_page_properties ){
    $this-&gt;settings_page_properties = $settings_page_properties;
  }

  public function run() {
    add_action( 'admin_menu', array( $this, 'add_menu_and_page' ) );
    add_action( 'admin_init', array( $this, 'register_settings' ) );
  }

  public function add_menu_and_page() { 

    add_submenu_page(
      $this-&gt;settings_page_properties['parent_slug'],
      $this-&gt;settings_page_properties['page_title'],
      $this-&gt;settings_page_properties['menu_title'],
      $this-&gt;settings_page_properties['capability'],
      $this-&gt;settings_page_properties['menu_slug'],
        array( $this, 'render_settings_page' )
    );

  }

  public function register_settings() { 

    register_setting(
      $this-&gt;settings_page_properties['option_group'],
      $this-&gt;settings_page_properties['option_name']
    );

  }

  public function get_settings_data(){
    return get_option( $this-&gt;settings_page_properties['option_name'], $this-&gt;get_default_settings_data() );
  }

  public function render_settings_page(){

  }

  public function get_default_settings_data() {
    $defaults = array();

    return $defaults;
  }
}
</code></pre>

Notice that it is an abstract class. This will prevent intantiating this class directly. To use it you need to extend it first with another class, which in our case is <code>Simplarity_SettingsPage</code>:

<pre><code class="language-php">&lt;?php
class Simplarity_SettingsPage extends Simplarity_WpSubPage {

  public function render_settings_page() {
    $option_name = $this-&gt;settings_page_properties['option_name'];
    $option_group = $this-&gt;settings_page_properties['option_group'];
    $settings_data = $this-&gt;get_settings_data();
    ?&gt;
    &lt;div class="wrap"&gt;
      &lt;h2&gt;Simplarity&lt;/h2&gt;
      &lt;p&gt;This plugin is using the settings API.&lt;/p&gt;
      &lt;form method="post" action="options.php"&gt;
        &lt;?php
        settings_fields( $option_group );
        ?&gt;
        &lt;table class="form-table"&gt;
          &lt;tr&gt;
              &lt;th&gt;&lt;label for="textbox"&gt;Textbox:&lt;/label&gt;&lt;/th&gt;
              &lt;td&gt;
                  &lt;input type="text" id="textbox"
                      name="&lt;?php echo esc_attr( $option_name."[textbox]" ); ?&gt;"
                      value="&lt;?php echo esc_attr( $settings_data['textbox'] ); ?&gt;" /&gt;
              &lt;/td&gt;
          &lt;/tr&gt;
        &lt;/table&gt;
        &lt;input type="submit" name="submit" id="submit" class="button button-primary" value="Save Options"&gt;
      &lt;/form&gt;
    &lt;/div&gt;
    &lt;?php
  }

  public function get_default_settings_data() {
    $defaults = array();
    defaults['textbox'] = ’;

    return $defaults;
  }
}
</code></pre>

The only functions we have implemented are <code>render_settings_page</code> and <code>get_default_settings_data</code>, which are customized to this settings page.

To create another WP settings page you'll just need to create a class and extend the <code>Simplarity_WpSubPage</code>. And implement your own <code>render_settings_page</code> and <code>get_default_settings_data</code>.</p>

## Defining A Service

The power of the plugin container is in defining services. A service is a function that contains instantiation and initialization code that will return an object. Whenever we pull a service from our container, the service function is called and will create the object for you. The object is only created when needed. This is called lazy initialization.

To better illustrate this, let's define a service for our settings page.

Open <i>simplarity.php</i> and add this function below the Simplarity code:

<pre><code class="language-php">function simplarity_service_settings( $plugin ){

  $object = new Simplarity_SettingsPage( $plugin['settings_page_properties'] );
  return $object;
}</code></pre>

Notice that our service function has a <code>$plugin</code> parameter which contains our plugin container. This allows us to access all configuration, objects, and services that have been stored in our plugin container. We can see that the <code>Simplarity_SettingsPage</code> has a dependency on <code>$plugin['settings_page_properties']</code>. We inject this dependency to <code>Simplarity_SettingsPage</code> here. This is an example of dependency injection. Dependency injection is a practice where objects are designed in a manner where they receive instances of the objects from other pieces of code, instead of constructing them internally. This improves decoupling of code.

Now let's replace this line in <code>simplarity_init</code>:

<pre><code class="language-php">$plugin['settings_page'] = new Simplarity_SettingsPage( $plugin['settings_page_properties'] );</code></pre>

with a service definition assignment:

<pre><code class="language-php">$plugin['settings_page'] = 'simplarity_service_settings'</code></pre>

So instead of assigning our object instance directly, we assign the name of our function as string. Our container handles the rest.</p>

## Defining A Shared Service

Right now, every time we get <code>$plugin['settings_page']</code>, a new instance of <code>Simplarity_SettingsPage</code> is returned. Ideally, <code>Simplarity_SettingsPage</code> should only be instantiated once as we are using WP hooks, which in turn should only be registered once.

To solve this we use a shared service. A shared service will return a new instance of an object on first call, on succeeding calls it will return the same instance.

Let's create a shared service using a static variable:

<pre><code class="language-php">function simplarity_service_settings( $plugin ){
  static $object;

  if (null !== $object) {
    return $object;
  }

  $object = new Simplarity_SettingsPage( $plugin['settings_page_properties'] );
  return $object;
}</code></pre>

On first call, <code>$object</code> is null, and on succeeding calls it will contain the instance of the object created on first call. Notice that we are using a static variable. A static variable exists only in a local function scope, but it does not lose its value when program execution leaves this scope.

That's it.

Now if you activate the plugin, an admin menu will appear in Admin → Settings named "Simplarity". Click on it and you will be taken to the settings page we have created.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b436d38e-3c4d-4360-9ef7-cd7152394cc7/simplarity1.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b436d38e-3c4d-4360-9ef7-cd7152394cc7/simplarity1.png" alt="Settings Page In Action" width="500" /></a><figcaption>Settings Page In Action</figcaption></figure>

## The Future: PHP 5.3+

Earlier we mentioned that our class naming convention was future-ready. In this section we will discuss how our codebase will work in PHP version 5.3 and up. Two of the best features that have graced the PHP world are namespaces and anonymous functions.</p>

### Namespaces

PHP does not allow two classes or functions to share the same name. When this happens, a name collision occurs and causes a nasty error.

With namespaces you can have the same class names as long as they live in their own namespace. A good analogy for namespaces are the folders you have in your OS. You cannot have files with the same name in one folder. However, you can have the same filenames in different folders.

With namespaces, class and function names won't need unique prefixes anymore.</p>

### Anonymous Functions

Anonymous functions, also known as <strong>closures</strong>, allow the creation of functions which have no specified name. They are most useful as the value of callback parameters, but they have many other uses. You can also store closures in variables.

Here's an example of closure:

<pre><code class="language-php">&lt;?php
$greet = function($name) {
  printf("Hello %s\r\n", $name);
};

$greet('World');
$greet('PHP');</code></pre>

## Using Namespaces In Classes

Let's go ahead and use namespaces in our class definitions. Open up the following files in <i>src/Simplarity:</i>

*   _Plugin.php_
*   _SettingsPage.php_
*   _WpSubPage.php_

In each of these files, add a namespace declaration on top and remove the "Simplarity_" prefix on class names:

<pre><code class="language-php">
// Plugin.php
namespace Simplarity;

class Plugin {
...

// SettingsPage.php
namespace Simplarity;

class SettingsPage extends WpSubPage {
...

// WpSubPage.php
namespace Simplarity;

abstract class WpSubPage {
...
</code></pre>

Since we have updated our class names we also need to update our class instantiations in <i>simplarity.php</i>. We do this by deleting the prefixes:

<pre><code class="language-php">function simplarity_init() {
  $plugin = new Plugin();
  ...
}
...
function simplarity_service_settings( $plugin ){

  ...

  $object = new SettingsPage( $plugin['settings_page_properties'] );
  return $object;
}
</code></pre>

By default, PHP will try to load the class from the root namespace so we need to tell it about our namespaced classes. We add this to the top of <i>simplarity.php</i> just above the autoloader code:

<pre><code class="language-php">use Simplarity\Plugin;
use Simplarity\SettingsPage;
</code></pre>

This is called importing/aliasing with the <a href="https://php.net/manual/en/language.namespaces.importing.php">use operator</a>.</p>

## Updating The Autoloader

Open up <i>simplarity.php</i> and change this line in the autoloader from:

<pre><code class="language-php">$class_file = str_replace( '_', DIRECTORY_SEPARATOR, $class_name ) . '.php';</code></pre>

to:

<pre><code class="language-php">$class_file = str_replace( '\\', DIRECTORY_SEPARATOR, $class_name ) . '.php';</code></pre>

Remember that in 5.2 code we are using underscores as hierarchy separators. For 5.3+ we are using namespaces which use backslash "\" as hierarchy separators. Thus we simply swap "_" for "\". We use another backslash to escape the original one: "\\".</p>

## Updating Our Service Definitions To Use Anonymous Functions

We can now replace the global functions we created for our service definitions with anonymous functions. So instead of doing this:

<pre><code class="language-php">
function simplarity_init() {
  ...
  $plugin['settings_page'] = 'simplarity_service_settings';
  ...
}
...
function simplarity_service_settings( $plugin ){
  static $object;

  if (null !== $object) {
    return $object;
  }

  $object = new Simplarity_SettingsPage( $plugin['settings_page_properties'] );
  return $object;
}</code></pre>

we can just replace this with an inline anonymous function:

<pre><code class="language-php">
function simplarity_init() {
  $plugin = new Plugin();
  ...
  $plugin['settings_page'] = function ( $plugin ) {
    static $object;

    if (null !== $object) {
      return $object;
    }
    return new SettingsPage( $plugin['settings_page_properties'] );
  };
  ...
}
</code></pre>

## Using Pimple As A Plugin Container

Pimple is a small dependency injection (DI) container for PHP 5.3+. Pimple has the same syntax as our simple plugin container. In fact our plugin container was inspired by Pimple. In this part, we will extend Pimple and use it.

Download <a href="https://raw.githubusercontent.com/silexphp/Pimple/master/src/Pimple/Container.php">Pimple container from GitHub</a> and save it in <i>src/Simplarity/Pimple.php</i>.

Open up <i>Pimple.php</i> and replace the namespace and the classname to:

<pre><code class="language-php">
...
namespace Simplarity;

/**
 * Container main class.
 *
 * @author  Fabien Potencier
 */
class Pimple implements \ArrayAccess
...
</code></pre>

Open up <i>Plugin.php</i> and replace all the code with:

<pre><code class="language-php">&lt;?php
namespace Simplarity;

class Plugin extends Pimple {

  public function run(){ 
    foreach( $this-&gt;values as $key =&gt; $content ){ // Loop on contents
      $content = $this[$key];

      if( is_object( $content ) ){
        $reflection = new \ReflectionClass( $content );
        if( $reflection-&gt;hasMethod( 'run' ) ){
            $content-&gt;run(); // Call run method on object
        }
      }
    }
  }
}
</code></pre>

Now let's change the service definition in <i>simplarity.php</i> to:

<pre><code class="language-php">$plugin['settings_page'] = function ( $plugin ) {
  return new SettingsPage( $plugin['settings_page_properties'] );
};
</code></pre>

By default, each time you get a service, Pimple returns the same instance of it. If you want a different instance to be returned for all calls, wrap your anonymous function with the <code>factory()</code> method:

<pre><code class="language-php">$plugin['image_resizer'] = $plugin-&gt;factory(function ( $plugin ) {
  return new ImageResizer( $plugin['image_dir'] );
});
</code></pre>

## Conclusion

The PHP community is big. A lot of best practices have been learned over the years. It's good to always look beyond the walled garden of WordPress to look for answers. With autoloading and a plugin container we are one step closer to better code.</p>

### Code Samples

*   [Simplarity: settings page](https://github.com/kosinix/simplarity)
*   [Simplarity: settings page (PHP5.3+)](https://github.com/kosinix/simplarity-php53)

### Resources

*   [PEAR naming standards](https://pear.php.net/manual/en/standards.naming.php)
*   [Namespaces explanation](https://daylerees.com/php-namespaces-explained)
*   [Pimple (a small DI container)](https://github.com/silexphp/Pimple)

{{< signature "dp, og, il" >}}

