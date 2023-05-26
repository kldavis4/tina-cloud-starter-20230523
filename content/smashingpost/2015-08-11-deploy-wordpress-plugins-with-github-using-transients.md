---
title: How To Deploy WordPress Plugins With GitHub Using Transients
slug: deploy-wordpress-plugins-with-github-using-transients
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6f28483e-d9dd-4a26-bad2-e91a52fbaf77/07-update-popup-opt.png
date: 2015-08-11T22:19:24.000Z
author: matthewray
description: >-
  If you've worked with WordPress for a while, you may have tried your hand at
  writing a plugin. Many developers will start creating plugins to **enhance a
  custom theme or to modularize their code**. Eventually, though, you may want
  to distribute your plugin to a wider audience.

  While you always have the option to use the WordPress Subversion repository,
  there may be instances where you prefer to host a plugin yourself. Perhaps you
  are offering your users a premium plugin. Maybe you need a way to keep your
  client's code in sync across multiple sites. It could simply be that you want
  to use a Git workflow instead of Subversion. Whatever the reason, this
  tutorial will show you **how to set up a GitHub repository to push updates to
  your plugin**, wherever it resides.
categories:
  - WordPress
  - Workflow
  - Plugins
  - Techniques (WP)
---
If you've worked with WordPress for a while, you may have tried your hand at writing a plugin. Many developers will start creating plugins to <strong>enhance a custom theme or to modularize their code</strong>. Eventually, though, you may want to distribute your plugin to a wider audience.

While you always have the option to use the WordPress Subversion repository, there may be instances where you prefer to host a plugin yourself. Perhaps you are offering your users a premium plugin. Maybe you need a way to keep your client's code in sync across multiple sites. It could simply be that you want to use a Git workflow instead of Subversion. Whatever the reason, this tutorial will show you <strong>how to set up a GitHub repository to push updates to your plugin</strong>, wherever it resides.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Making A WordPress Plugin That Uses Service APIs](https://www.smashingmagazine.com/2016/03/making-a-wordpress-plugin-that-uses-service-apis/)
*   [A Simple Workflow From Development To Deployment](https://www.smashingmagazine.com/2015/07/development-to-deployment-workflow/)
*   [<span class="headline">S(GH)PA: The Single-Page App Hack For GitHub Pages</span>](https://www.smashingmagazine.com/2016/08/sghpa-single-page-app-hack-github-pages/)
*   [Build A Blog With Jekyll And GitHub Pages](https://www.smashingmagazine.com/2014/08/build-blog-jekyll-github-pages/)

## The Plan

Before we get too far into the code we should start with an outline of what we will be doing:

{{% feature-panel %}}

1.  First, we will learn a little bit about _transients_ and how they work within WordPress.
2.  Then, we will build a PHP class to house all of our code.
3.  Next, we are going to connect our plugin to GitHub.
4.  Lastly, we will create the interface elements that allow users to interact with our plugin.

When you finish this article you should have a fully functioning plugin that will update directly using GitHub releases. Ready to get started?

## WordPress Transients

First of all, what are <a href="https://codex.wordpress.org/Transients_API">WordPress transients</a>? WordPress transients are a short-lived entry of data that is stored for a defined duration and will be automatically removed when it has expired — think of them as server-side cookies. <strong>WordPress uses transients to store information about all of the plugins</strong> that have been installed, including their version number. Every once in a while WordPress will refresh the data that is stored in the transient. It is this event that WordPress uses to check the Subversion repository for updated plugins. It is also this event that we will use to check for updates on our own plugin on GitHub.</p>

## Getting Started

Let's begin by setting up our updater class:

<pre><code class="language-php">class Smashing_Updater {
  protected $file;

  public function __construct( $file ) {
    $this-&gt;file = $file;
    return $this;
  }
}</code></pre>

The first thing we must do is create a class name and a constructor (the class name can be anything you want). We are going to need to figure out some basic information about the WordPress plugin we are updating, including the version number. We'll do this by passing the main plugin file's path into our updater and then we'll assign that value to a property.

You might be wondering why we need to pass the plugin's path into our class. You see, the way WordPress stores plugin information is <strong>by using the main plugin file's path as a unique identifier</strong> (i.e. the basename). Let's say our plugin is in the directory <i>/wp-content/plugins/smashing-plugin/smashing-plugin.php</i>, the basename for our plugin would be <i>smashing-plugin/smashing-plugin.php</i>. We will use this basename to check if the plugin we are updating is activated, among other things.

Next we need to get the plugin data and set it to a property in our class:

<pre><code class="language-php">class Smashing_Updater {
  protected $file;
  protected $plugin;
  protected $basename;
  protected $active;

  public function __construct( $file ) {
    $this-&gt;file = $file;
    add_action( 'admin_init', array( $this, 'set_plugin_properties' ) );
    return $this;
  }

  public function set_plugin_properties() {
    $this-&gt;plugin   = get_plugin_data( $this-&gt;file );
    $this-&gt;basename = plugin_basename( $this-&gt;file );
    $this-&gt;active   = is_plugin_active( $this-&gt;basename );
  }
}</code></pre>

You may have noticed that I am using the action <a href="https://codex.wordpress.org/Plugin_API/Action_Reference"><code>admin_init</code></a> to set the plugin properties. This is because the function <code>get_plugin_data()</code> may not have been defined at the point in which this code was called. By hooking it to <code>admin_init</code> we are ensuring that we have that function available to get our plugin data. We are also checking if the plugin is activated, and assigning that and the plugin object to properties in our class.

To learn more about WordPress actions and filters you should take a look at the <a href="https://codex.wordpress.org/Plugin_API">plugin API</a>.

Now that we have our class set up and grabbed some of the basic plugin data we'll need, it's time we start talking about GitHub.</p>

## Setting Up GitHub

We can start by <strong>creating a repository for our plugin</strong>. It is important to remember that we will pull the files down from here, so the directory structure is important. You'll need the root of your repository to be the contents of your plugin folder, not the plugin folder itself. Here is an example of what you should see:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/47610ecf-5240-4ba3-9375-dccdb13a3465/01-github-root-opt.png"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0fb88346-42b8-40d0-96cc-da7d02905b23/01-github-root-opt-small.png" alt="The root directory of our GitHub repository" /></a><figcaption>The root directory of our GitHub repository. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/47610ecf-5240-4ba3-9375-dccdb13a3465/01-github-root-opt.png">View large version</a>)</figcaption></figure>

In my repository I have two files. The main plugin file <i>smashing-plugin.php</i> and the updater script <i>updater.php</i>. Your repo may look a little different depending on your plugin files.

Now that we have a repository set up, let's talk about how we are going to check the version number on GitHub. We have a couple of options here. We could pull down the main file and parse the contents to try to find the version number. However, I prefer using the built-in release functionality of GitHub. Let's add a new release.

Start by going to the "releases" tab and hitting "Create a new release":

<figure><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/54972b60-ede0-484f-b1ed-a4ec81bf890d/02-releases-opt.png" alt="The releases tab of our GitHub repository" /><figcaption>Creating a new release in the GitHub release section.</figcaption></figure>

Here you will find a few fields we need to fill out. The most important one is the "Tag version" field. This is where we will put the current release version of our plugin. By now, you are probably familiar with <a href="https://semver.org/">the semantic versioning format</a>. This is the format we are going to use for our field. We should also use this format for our main plugin file, in the PHP comments. Continue filling out the title and description fields in the release until your release looks like something like this:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0e03616a-6ec7-43ce-a772-6d73bff2e542/03-new-release-opt.png"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8f1fd588-2edf-4601-910b-8c44c32e1d92/03-new-release-opt-small.png" alt="A new release of our plugin" /></a><figcaption>A new release of our plugin. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0e03616a-6ec7-43ce-a772-6d73bff2e542/03-new-release-opt.png">View large version</a>)</figcaption></figure>

Hit the "Publish release" button to create the release. This will create a ZIP file in our repo that we can use in our updater script. Then, you simply repeat this process whenever you want to deploy a new plugin release. We can now use the GitHub API to check the version number and we have a ZIP file ready to go.</p>

### But I Have A Private Plugin!

Don't worry, just a couple of extra steps. Private plugins require you to pass an authorization token when you make requests to the API. First go to your account settings:

<figure><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5f305536-f78e-4c93-98fe-ca0c0e4fd2b2/04-settings-opt.png" alt="GitHub settings panel" /><figcaption>GitHub settings panel.</figcaption></figure>

Then go to "Personal access tokens" on the left menu and click "Generate a new access token" button on the top right. You will be brought to this page:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5a464f8b-81ee-416f-b3b8-5291b13d7d60/05-token-opt.png"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c52926ff-3680-4c4e-b657-78f246624f04/05-token-opt-small.png" alt="GitHub generate token" /></a><figcaption>GitHub generate token. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5a464f8b-81ee-416f-b3b8-5291b13d7d60/05-token-opt.png">View large version</a>)</figcaption></figure>

You can give the token any description you like, then select the repo scope and hit "Generate token". Once you've generated your token, copy it down somewhere — we will use it later.</p>

## Connecting To GitHub

We can now start adding some code to connect our updater to GitHub. First we'll add a few more properties to hold our repo information, and one to hold our response from GitHub:

<pre><code class="language-php">private $username;
private $repository;
private $authorize_token;
private $github_response;
</code></pre>

Then we'll add some setters for our new properties:

<pre><code class="language-php">public function set_username( $username ) {
  $this-&gt;username = $username;
}
public function set_repository( $repository ) {
  $this-&gt;repository = $repository;
}
public function authorize( $token ) {
  $this-&gt;authorize_token = $token;
}
</code></pre>

These setters allow us to modify usernames and repositories without reinstantiating our updater class. Say you wanted to have an unlockable feature or require the users to register, you could change the repo to a pro version of your plugin by simply adding a conditional statement. Let's take a look at how we should include this code in our main plugin file:

<pre><code class="language-php">// Include our updater file
include_once( plugin_dir_path( __FILE__ ) . 'update.php');

$updater = new Smashing_Updater( __FILE__ ); // instantiate our class
$updater-&gt;set_username( 'rayman813' ); // set username
$updater-&gt;set_repository( 'smashing-updater-plugin' ); // set repo
</code></pre>

Now let's write the code we will need to get the version tag from GitHub.</p>

<pre><code class="language-php">private function get_repository_info() {
  if ( is_null( $this-&gt;github_response ) ) { // Do we have a response?
    $request_uri = sprintf( 'https://api.github.com/repos/%s/%s/releases', $this-&gt;username, $this-&gt;repository ); // Build URI
    if( $this-&gt;authorize_token ) { // Is there an access token?
        $request_uri = add_query_arg( 'access_token', $this-&gt;authorize_token, $request_uri ); // Append it
    }        
    $response = json_decode( wp_remote_retrieve_body( wp_remote_get( $request_uri ) ), true ); // Get JSON and parse it
    if( is_array( $response ) ) { // If it is an array
        $response = current( $response ); // Get the first item
    }
    if( $this-&gt;authorize_token ) { // Is there an access token?
        $response['zipball_url'] = add_query_arg( 'access_token', $this-&gt;authorize_token, $response['zipball_url'] ); // Update our zip url with token
    }
    $this-&gt;github_response = $response; // Set it to our property  
  }
}
</code></pre>

In this method we are checking if we've already gotten a response; if we haven't, then make a request to the GitHub API endpoint using the username and repo that we've supplied. We've also added some code to check for an access token for private repos. If there is one, append it to the URL and update the zipball URL (the file we will download when we update). We are then getting the JSON response, parsing it, and grabbing the latest release. Once we have the latest release, we're setting it to the property we created earlier.</p>

## Modifying WordPress

Alright, so far we've collected information about our plugin and our repo, and we've connected to the repo using the API. Now it's time to start modifying WordPress to find our new data and put it in the right spots. This is going to involve three steps:

1.  Modifying the output of the WordPress update transient.
2.  Updating the WordPress interface to show our plugin's info properly.
3.  Making sure our plugin is working properly after the update.

Before we get too deep into how we are going to accomplish each step, we should talk about how we are going to hook into the transient.</p>

### Hooking Into The Update Transient

There are a few ways to hook into this transient event. There are two filters and two actions we can use to inject our code; they are:

*   Filter: `pre_set_transient_update_plugins`
*   Filter: `pre_set_site_transient_update_plugins`
*   Action: `set_transient_update_plugins`
*   Action: `set_site_transient_update_plugins`

You will notice that the tags are fairly similar. The difference here is the addition of the word <code>site</code>. This distinction is important because it changes the scope of our injected code. The tags <strong>without</strong> the word <code>site</code> will only work on single-site installations of WordPress; the other will work on both single-site and multi-site installations. Depending on your plugin you may choose to use one over the other.

I simply want to modify the default transient, so I am going to use one of the filters. I've decided to use <code>pre_set_site_transient_update_plugins</code> so that our code will work on both single and multi-site installations.</p>

<strong>Update:</strong> If you are using this script to update a theme you can also use the filter <code>pre_set_site_transient_update_themes</code>. Source: <a href="https://github.com/afragen" rel="nofollow">Andy Fragen</a>

Let's take a look at our initialize function:

<pre><code class="language-php">public function initialize() {
  add_filter( 'pre_set_site_transient_update_plugins', array( $this, 'modify_transient' ), 10, 1 );
  add_filter( 'plugins_api', array( $this, 'plugin_popup' ), 10, 3);
  add_filter( 'upgrader_post_install', array( $this, 'after_install' ), 10, 3 );
}</code></pre>

In this example I have added three filters. Each one corresponds to the steps we talked about earlier. Our first filter is going to modify the transient; the second will ensure that our plugin data gets passed into the WordPress interface; and the last will make sure that our plugin is activated after the update.

Now we need to call this new method in our main plugin file to initialize the updater script. Here is the what the updated code should look like:

<pre><code class="language-php">// Include our updater file
include_once( plugin_dir_path( __FILE__ ) . 'update.php');

$updater = new Smashing_Updater( __FILE__ ); // instantiate our class
$updater-&gt;set_username( 'rayman813' ); // set username
$updater-&gt;set_repository( 'smashing-plugin' ); // set repo
$updater-&gt;initialize(); // initialize the updater</code></pre>

Now our initialize method will run and the filters within the method will be active. If you are planning on having your plugin's automatic updates be a premium feature, the initialize method would be a good spot to put your checks and conditionals.</p>

### Writing The Code For Our Filters

I have written out all of the methods we will need for each filter we will be using. We can start with the <code>modify_transient</code> method:

<pre><code class="language-php">public function modify_transient( $transient ) {

  if( property_exists( $transient, 'checked') ) { // Check if transient has a checked property
    if( $checked = $transient-&gt;checked ) { // Did WordPress check for updates?
      $this-&gt;get_repository_info(); // Get the repo info
      $out_of_date = version_compare( $this-&gt;github_response['tag_name'], $checked[$this-&gt;basename], 'gt' ); // Check if we're out of date
      if( $out_of_date ) {
        $new_files = $this-&gt;github_response['zipball_url']; // Get the ZIP
        $slug = current( explode('/', $this-&gt;basename ) ); // Create valid slug
        $plugin = array( // setup our plugin info
          'url' =&gt; $this-&gt;plugin["PluginURI"],
          'slug' =&gt; $slug,
          'package' =&gt; $new_files,
          'new_version' =&gt; $this-&gt;github_response['tag_name']
        );
        $transient-&gt;response[ $this-&gt;basename ] = (object) $plugin; // Return it in response
      }
    }
  }
  return $transient; // Return filtered transient
}</code></pre>

This snippet simply takes the version number from the comments in our main plugin file, and compares them with the tag name we gave our release on GitHub. If the one on GitHub is higher, our code tells WordPress that there is a newer version available. If you change the version number in the main plugin file to a version that is lower than our GitHub tag, you should start seeing the update notification in the WordPress admin:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/71f73aeb-1b3a-4027-9ba0-81622988aedf/06-updates-available-opt.png"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b73185fd-c3d0-46f5-b4f0-a74a345244d1/06-updates-available-opt-small.png" alt="WordPress plugin interface showing updates available" /></a><figcaption>WordPress plugin interface showing updates available. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/71f73aeb-1b3a-4027-9ba0-81622988aedf/06-updates-available-opt.png">View large version</a>)</figcaption></figure>

You might notice, however, that if you click on the "View version 1.0.0 details" link, you receive an error from WordPress. This is because WordPress is trying to find the details of this plugin from <em>its</em> repositories. Instead, we need to load our own data about the plugin. That is where our next method, <code>plugin_popup</code>, comes in:

<pre><code class="language-php">public function plugin_popup( $result, $action, $args ) {
  if( ! empty( $args-&gt;slug ) ) { // If there is a slug
    if( $args-&gt;slug == current( explode( '/' , $this-&gt;basename ) ) ) { // And it's our slug
      $this-&gt;get_repository_info(); // Get our repo info
      // Set it to an array
      $plugin = array(
        'name'              =&gt; $this-&gt;plugin["Name"],
        'slug'              =&gt; $this-&gt;basename,
        'version'           =&gt; $this-&gt;github_response['tag_name'],
        'author'            =&gt; $this-&gt;plugin["AuthorName"],
        'author_profile'    =&gt; $this-&gt;plugin["AuthorURI"],
        'last_updated'      =&gt; $this-&gt;github_response['published_at'],
        'homepage'          =&gt; $this-&gt;plugin["PluginURI"],
        'short_description' =&gt; $this-&gt;plugin["Description"],
        'sections'          =&gt; array( 
            'Description'   =&gt; $this-&gt;plugin["Description"],
            'Updates'       =&gt; $this-&gt;github_response['body'],
        ),
        'download_link'     =&gt; $this-&gt;github_response['zipball_url']
      );
      return (object) $plugin; // Return the data
    }
  }   
  return $result; // Otherwise return default
}</code></pre>

This snippet is actually pretty simple. We are just checking if WordPress is looking for data about our plugin, and if it is, returning our own array of data. We get the data from a combination of our GitHub response and our plugin's comment data. You might have also noticed the <code>sections</code> key in this array. Each item in that array is output as a tab in the plugin popup meta box. You could add pretty much anything you'd like in those sections, including HTML. Right now, we are just showing the plugin description and the release notes we wrote earlier.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6f28483e-d9dd-4a26-bad2-e91a52fbaf77/07-update-popup-opt.png"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/41be327a-3e5d-4544-831f-8d7e965ad316/07-update-popup-opt-small.png" alt="Plugin update popup" /></a><figcaption>Plugin update popup. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6f28483e-d9dd-4a26-bad2-e91a52fbaf77/07-update-popup-opt.png">View large version</a>)</figcaption></figure>

Let's take a look at our final method, <code>after_install</code>:

<pre><code class="language-php">public function after_install( $response, $hook_extra, $result ) {
  global $wp_filesystem; // Get global FS object

  $install_directory = plugin_dir_path( $this-&gt;file ); // Our plugin directory 
  $wp_filesystem-&gt;move( $result['destination'], $install_directory ); // Move files to the plugin dir
  $result['destination'] = $install_directory; // Set the destination for the rest of the stack

  if ( $this-&gt;active ) { // If it was active
    activate_plugin( $this-&gt;basename ); // Reactivate
  }
  return $result;
}
</code></pre>

This snippet does two things. First, it sets an argument named <code>destination</code>, which is simply the directory where WordPress is going to install our new code. We are passing the main plugin file's directory into this argument since it <em>should</em> always be the root of the plugin. Second, it checks if the plugin was activated using the property we set earlier. If it was active before updating, our method will reactivate it.</p>

## Conclusion

Congratulations! You should now be able to update your plugin by clicking the "Update now" button on the plugins page. You should keep in mind, though, that your plugin's version in the main plugin file needs to be updated to match the current release of your plugin — they should always match. If you didn't update your version in the comments, you may find yourself in an endless "There is an update available" loop.

If you would like to see the completed script from this tutorial, you can view it in the sample <a href="https://github.com/rayman813/smashing-plugin">GitHub repository</a> that we made.

{{< signature "dp, ml, og" >}}

