---
title: Implementing A Service Worker For Single-Page App WordPress Sites
slug: service-worker-single-page-application-wordpress-sites
author: leonardolosoviz
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0336f678-6bda-438d-904d-6db1f5eab07b/chrome-network-tab-500px-opt.png
date: 2017-10-11T21:47:19.000Z
description: >-
  Through service workers, all framework and application code to output the HTML
  view can be precached in the browser, thus speeding up both the first
  meaningful paint and the time to interact. In this article, I will share my
  experience with implementing service workers for PoP, an SPA website that runs
  on WordPress, with the goal of speeding up the loading time and providing
  offline-first capabilities.
categories:
  - WordPress
  - Service Workers
---
Enter service workers. Through service workers, all framework and application code to output the HTML view can be precached in the browser, thus speeding up both the first meaningful paint and the time to interact. In this article, I will share my experience with implementing service workers for [PoP](https://getpop.org), an SPA website that runs on WordPress, with the goal of speeding up the loading time and providing [offline-first](https://offlinefirst.org/) capabilities.

Most of the code from the explanation below can be reused to create a solution for traditional (i.e. non-SPA) WordPress websites, too. Anyone want to implement a plugin?

## Defining The Application’s Features

In addition to being suitable for an SPA WordPress website, the implementation of service workers below has been designed to support the following features:

*   loading of assets from external sources, such as a content delivery network (CDN);
*   multilingual (i18n) support;
*   multiple views;
*   selection on runtime of the caching strategy, on a URL-by-URL basis.

Based on this, we’ll make the following design decisions.</p>

### Load an Application Shell (or Appshell) First

If the SPA architecture supports it, load an appshell first (i.e. minimal HTML, CSS and JavaScript to power the user interface), under `https://www.mydomain.com/appshell/`. Once loaded, the appshell will dynamically request content from the server through an API. Because all of the appshell’s assets can be precached using service workers, the website’s frame will load immediately, speeding up the first meaningful paint. This scenario uses the “[cache falling back to network](https://jakearchibald.com/2014/offline-cookbook/#cache-falling-back-to-network)” caching strategy.

Watch out for conflicts! For instance, WordPress outputs code that is not supposed to be cached and used forever, such as nonces, which usually expire after 24 hours. The appshell, which service workers will cache in the browser for more than 24 hours, needs to deal with nonces properly.</p>

{{% feature-panel %}}

### Extract WordPress Resources Added Through wp_enqueue_script and wp_enqueue_style

Because a WordPress website loads its JavaScript and CSS resources through the `wp_enqueue_script` and `wp_enqueue_style` hooks, respectively, we can conveniently extract these resources and add them to the precache list.

While following this strategy reduces the effort to produce the list of resources to precache (some files will still need to be added manually, as we shall see later), it implies that the `service-workers.js` file must be generated dynamically, on runtime. This suits very well the decision to enable WordPress plugins to hook into the generation of the `service-workers.js` file, as explained in the next item.

Indeed, I’d argue that there is no other way but to hook into these functions, because to generate the list manually (i.e. finding and listing all resources loaded by all plugins and the theme) is too troublesome of a process, and using other tools to generate the JavaScript and CSS files, such as [Service Worker Precache](https://github.com/GoogleChrome/sw-precache), will actually not work in this context, for two main reasons:

*   Service Worker Precache works by scanning files in a specified folder and filtering them using wildcards. However, the files that WordPress ships with are many more than the actual ones required by the application, so we would quite likely be precaching plenty of redundant files.
*   WordPress attachs a version number to the requested file, which varies from file to file, such as:
    *   `https://www.mydomain.com/wp-includes/js/utils.min.js?ver=4.6.1`
    *   `https://www.mydomain.com/wp-includes/js/jquery/jquery-migrate.min.js?ver=1.4.1`
    *   `https://www.mydomain.com/wp-includes/js/jquery/jquery.js?ver=1.12.4`

Service workers intercept each request based on the full path of the requested resource, including the parameters — such as the version number, in this case. Because the Service Worker Precache tool is not aware of the versioning number, it will be unable to produce the required list correctly.</p>

### Allow Plugins to Hook Into the Generation of service-workers.js

Adding hooks into our functionality enables us to extend the functionality of service workers. For instance, third-party plugins can hook into the precached resources list to add their own resources, or to specify which caching strategy to use depending on their URL pattern, among others.</p>

### Caching External Resources: Define a List of Domains, and Validate the Resources to Precache Originate From Any of These.

Whenever the resource originates from the website’s domain, it can always be handled using service workers. Whenever not, it can still be fetched but we must use `no-cors` fetch mode. This type of request will result in an opaque response, so we won’t be able to check whether the request was successful; however, we can still precache these resources and allow the website to be browsable offline.

### Support for Multiple Views

Let’s assume the URL contains a parameter indicating which view to use to render the website, such as:

*   Default view: `https://www.mydomain.com/` (`?view=default`)
*   Embeddable view: `https://www.mydomain.com/?view=embed`
*   Printable view: `https://www.mydomain.com/?view=print`

Several appshells can be precached, each one representing a view:

*   `https://www.mydomain.com/appshell/?view=default`
*   `https://www.mydomain.com/appshell/?view=embed`
*   `https://www.mydomain.com/appshell/?view=print`

Then, when loading the website, we extract the value of the `view` parameter from the URL, and load the corresponding appshell, on runtime.</p>

{{% ad-panel-leaderboard %}}

### i18n Support

We are assuming that the language code is part of the URL, like this: `https://www.mydomain.com/language-code/path/to/the/page/`

One possible approach would be to design the website to provide a different `service-workers.js` file for each language, each to be employed under its corresponding language scope: a `service-worker-en.js` file for the `en/` scope for English, a `service-worker-es.js` for the `es/` scope for Spanish, and so on. However, conflicts arise when accessing shared resources, such as the JavaScript and CSS files located in the `wp-content/` folder. These resources are the same for all languages; their URLs don’t carry any information about language. Adding yet another `service-workers.js` file to deal with all non-language scopes would add undesired complexity.

A more straightforward approach would be to employ the same technique as above for rendering multiple views: Register a unique `service-workers.js` file that already contains all information for all languages, and decide on runtime which language to use by extracting the language code from the requested URL.

In order to support all of the features described so far for, say, three views (a default, embed and print view) and two languages (English and Spanish), we would need to generate the following appshells:

*   `https://www.mydomain.com/en/appshell/?view=default`
*   `https://www.mydomain.com/en/appshell/?view=embed`
*   `https://www.mydomain.com/en/appshell/?view=print`
*   `https://www.mydomain.com/es/appshell/?view=default`
*   `https://www.mydomain.com/es/appshell/?view=embed`
*   `https://www.mydomain.com/es/appshell/?view=print`

### Use Different Caching Strategies

The application must be able to choose from several caching strategies in order to support different behaviors on different pages. Here are some possible scenarios:

*   A page can be retrieved from cache most of the time, but on specific occasions it must be retrieved from the network (for example, to view a post after editing it).
*   A page may have a user state and, as such, cannot be cached (for example, “Edit my account,” “My posts”).
*   A page can be requested in the background to bring extra data (for example, lazy-loaded comments on a post)

Here are the caching strategies and when to use each:

*   [Cache, falling back to network](https://jakearchibald.com/2014/offline-cookbook/#cache-falling-back-to-network)
    *   **Static assets (JavaScript and CSS files, images, etc.)**  
        The static content will never be updated: JavaScript and CSS files have the versioning number, and uploading the same image a second time into WordPress’ media manager will change the image’s file name. As such, cached static assets will not become stale.
    *   **Appshell**  
        We want the appshell to load immediately, so we retrieve it from the cache. If the application is upgraded and the appshell changes, then changing the version number will install a new version of the service worker and download the latest version of the appshell.
*   [Cache, then network](https://jakearchibald.com/2014/offline-cookbook/#cache-then-network)
    *   **General content**  
        While getting the content from the cache to display it immediately, we also send the request to bring the content from the server. We compare the two versions using an [ETag header](https://en.wikipedia.org/wiki/HTTP_ETag), and if the content has changed, we cache the server’s response (i.e. the most up to date of the two) and then show a message to the user, “This page has been updated, please click here to refresh it.”
*   [Network only](https://jakearchibald.com/2014/offline-cookbook/#network-only)
    *   **Force content to be up to date**  
        Content that would normally use the “cache then network” strategy can be forced to use a “network only” strategy by artificially adding the parameter `sw-strategy=networkfirst` or `sw-networkfirst=true` to the requested URL. This parameter can be removed before the request is sent to the server.
    *   **Content with user state**  
        We do not want to cache any content with a user state, due to security. (We could delete the user state cache when the user signs out, but implementing that is more complex.)
*   [Network, falling back to cache](https://jakearchibald.com/2014/offline-cookbook/#network-falling-back-to-cache)
    *   **Lazy-loaded content**  
        Content is lazy-loaded when the user will not see it immediately, allowing the content that the user sees immediately to load faster. (For example, a post would load immediately, and its comments would be lazy-loaded because they appear at the bottom of the page.) Because it will not be seen immediately, fetching this content straight from the cache is not necessary either; instead, always try to get the most up-to-date version from the server.</p>

{{% ad-panel-leaderboard %}}

### Ignore Certain Data When Generating the ETag Header for the “Cache Then Network” Strategy

An ETag can be generated using a hash function; a very tiny change in the input will produce a completely different output. As such, values that are not considered important and that are allowed to become stale should not be factored in when generating the ETag. Otherwise, the user might be prompted with the message “This page has been updated, please click here to refresh it” for every tiny change, such as the comments counter going from 5 to 6.</p>

## Implementation

All of the code below, slightly adapted for this article, can be found in the [GitHub repository](https://github.com/leoloso/PoP/tree/master/wp-content/plugins/pop-serviceworkers). The sources for [the sw-template.js](https://github.com/leoloso/PoP/blob/master/wp-content/plugins/pop-serviceworkers/kernel/serviceworkers/assets/js/jobs/sw.js) and [sw.php files](https://github.com/leoloso/PoP/blob/master/wp-content/plugins/pop-serviceworkers/kernel/serviceworkers/implementations/sw.php), mentioned below, are also available. Also, an example of a [generated service-workers.js file](https://getpop.org/wp-content/pop-serviceworkers/getpop/service-worker.js) is available.</p>

### Generating the service-workers.js File on Runtime

We have decided to automatically extract all JavaScript and CSS files that are to be used by the application, added through the `wp_enqueue_script` and `wp_enqueue_style` functions, in order to export these resources into the Service Worker Precache list. This implies that the `service-workers.js` file will be generated on runtime.

When and how should it be generated? Triggering an action to create the file through `admin-ajax.php` (for example, calling `https://www.mydomain.com/wp-admin/admin-ajax.php?action=create-sw`) will not work, because it would load WordPress’ admin area. Instead, we need to load all JavaScript and CSS files from the front end, which will certainly be different.

A solution is to create a private page on the website (hidden from view), accessed through `https://www.mydomain.com/create-sw/`, which will execute functionality to create the `service-workers.js` file. The file’s creation must take place at the very end of the execution of the request, so that all JavaScript and CSS files will have been enqueued by then:

<div class="break-out">

<pre><code class="language-php">function generate_sw_shortcode($atts) {

	add_action('wp_footer', 'generate_sw_files', PHP_INT_MAX);
}
add_shortcode('generate_sw', 'generate_sw_shortcode');
</code></pre></div>

<figcaption>File: sw.php</figcaption>

Please note that this solution works because the website is an SPA which loads ALL files in advance for the whole lifecycle of the application usage (the infamous bundled file); requesting any 2 different URLs from this website will always load the same set of .js and .css files. I am currently developing code-splitting techniques into the framework which will, coupled with HTTP/2, load only the required JS resources and nothing else, on a page-by-page basis — it should be ready within a couple of weeks. Hopefully I will then be able to describe how Service Workers + SPA + code-splitting can work all together.

The generated file could be placed in the root of the website (i.e. alongside `wp-config.php`) to grant it `/` scope. However, placing files in the root folder of the website is not always advisable, such as for security (the root folder must have very restrictive write permissions) and for maintenance (if `service-workers.js` were to be generated by a plugin and this one was disabled because its folder was renamed, then the `service-workers.js` file might never get deleted).

Luckily, there is another possibility. We can place the `service-workers.js` file in any directory, such as `wp-content/sw/`, and add an `.htaccess` file that grants access to the root scope:

<div class="break-out">

<pre><code class="language-php">function generate_sw_files() {

	$dir = WP_CONTENT_DIR."/sw/"

	// Create the directory structure
	if (!file_exists($dir)) {
		@mkdir($dir, 0755, true);
	}

	// Generate Service Worker .js file
	save_file($dir.'service-workers.js', get_sw_contents());

	// Generate the file to register the Service Worker
	save_file($dir.'sw-registrar.js', get_sw_registrar_contents());

	// Generate the .htaccess file to allow access to the scope (/)
	save_file($dir.'.htaccess', get_sw_htaccess_contents());
}

function get_sw_registrar_contents() {

	return '
		if ("serviceWorker" in navigator) {
		  navigator.serviceWorker.register("/wp-content/sw/service-workers.js", {
			scope: "/"
		  });
		}
	';
}

function get_sw_htaccess_contents() {

	return '
		&lt;FilesMatch "service-workers\.js$"&gt;
			Header set Service-Worker-Allowed: /
		&lt;/FilesMatch&gt;
	';
}

function save_file($file, $contents) {

	// Open the file, write content and close it
	$handle = fopen($file, "wb");
	$numbytes = fwrite($handle, $contents);
	fclose($handle);
	return $file;
}
</code></pre></div>

<figcaption>File: sw.php</figcaption>

Generation of these files can be included during the website deployment process, in order to automate it and so that all files are created just before the new website version becomes available to users.

For security reasons, we can add some validation in `function generate_sw_files()` before it executes:

*   to provide a valid access key as a parameter.
*   to make sure it can only be requested from within the same server.

<div class="break-out">

<pre><code class="language-php">if ($_REQUEST['accesskey'] != $ACCESS_KEY) {
	die;
}
if (!in_array(getenv('HTTP_CLIENT_IP'), array('localhost', '127.0.0.1', '::1'))) {
	die;
}
</code></pre></div>

To request `https://www.mydomain.com/create-sw/` from within the server, and doing so from a single server, we would execute:

<div class="break-out">

<pre><code class="language-bash">wget -q https://www.mydomain.com/create-sw/?accesskey=…
</code></pre></div>

From an array of servers behind a load balancer, or from a stack of servers in the cloud using auto-scaling, we can’t execute `wget URL`, because we don’t know which server will serve the request. Instead, we can directly execute the PHP process, using `php-cgi`:

<div class="break-out">

<pre><code class="language-bash">cd /var/www/html/
sudo SCRIPT_FILENAME=index.php SCRIPT_NAME=/index.php REMOTE_ADDR=127.0.0.1 REDIRECT_STATUS=200 SERVER_PROTOCOL=HTTP/1.1 REQUEST_METHOD=GET HTTPS=on SERVER_NAME=www.mydomain.com HTTP_HOST=www.mydomain.com SERVER_PORT=80 REQUEST_URI=/create-sw/ QUERY_STRING="accesskey=…" php-cgi &gt; /dev/null
</code></pre></div>

If you’re uncomfortable with having this page on a production server, this process could also be run in a staging environment, as long as it has exactly the same configuration as the production server (i.e. the database must have the same data; all constants in `wp-config.php` must have the same values; the URL to access the website on the staging server must be the same as the website itself, etc.). Then, the newly created `service-workers.js` file must be copied from the staging to production servers during deployment of the website.

**Contents of service-workers.js**

Generating `service-workers.js` from a PHP function implies that we can provide a template of this file, which will declare what variables it needs, and the service worker’s logic. Then, on runtime, the variables will be replaced with actual values. We can also conveniently add hooks to enable plugins to add their own required values. (More configuration variables will be added later on in this article).

<div class="break-out">

<pre><code class="language-php">function get_sw_contents() {

	// $sw_template has the path to the service-worker template
	$sw_template = dirname(__FILE__).'/assets/sw-template.js';
	$contents = file_get_contents($sw_template);
	foreach (get_sw_configuration() as $key =&gt; $replacement) {
		$value = json_encode($replacement);
		$contents = str_replace($key, $value, $contents);
	}
	return $contents;
}

function get_sw_configuration() {

	$configuration = array();
	$configuration['$version'] = get_sw_version();
	…
	return $configuration;
}
</code></pre></div>

<figcaption>File: sw.php</figcaption>

The configuration of the service workers template looks like this:

<div class="break-out">

<pre><code class="language-javascript">var config = {
	version: $version,
	…
};
</code></pre></div>

<figcaption>File: sw-template.js</figcaption>

**Resource types**

The introduction of resource types, which is a way of splitting assets into groups, allows us to implement different behaviors in the logic of the service worker. We will need the following resource types:

*   **HTML**  
    Produced only when first loading the website. After that, all content is dynamically requested using the application API, whose response is in JSON format
*   **JSON**  
    The API to get and post content
*   **Static**  
    Any asset, such as JavaScript, CSS, PDF, an image, etc.

Resource types can be used for caching resources, but this is optional (it only makes the logic more manageable). They are needed for:

*   selecting the appropriate caching strategy (for static, cache-first, and for JSON, network-first);
*   defining paths not to intercept (anything under `wp-content/` for JSON but not for static, or anything ending in `.php` for static, for dynamically generated images, but not for JSON).

<div class="break-out">

<pre><code class="language-php">function get_sw_resourcetypes() {

	return array('static', 'json', 'html');
}
</code></pre></div>

<figcaption>File: sw.php</figcaption>

<div class="break-out">

<pre><code class="language-php">function getResourceType(request) {

	var acceptHeader = request.headers.get('Accept');
	var resourceType = 'static';

	if (acceptHeader.indexOf('text/html') !== -1) {
		resourceType = 'html';
	}
	else if (acceptHeader.indexOf('application/json') !== -1) {
		resourceType = 'json';
	}

	return resourceType;
}
</code></pre></div>

<figcaption>File: sw-template.js</figcaption>

**Intercepting requests on service workers**

We will define for which URL patterns we do not want the service worker to intercept the request. The list of resources to exclude is initially empty, just containing a hook to inject all values.

*   `$excludedFullPaths`  
    Full paths to exclude.
*   `$excludedPartialPaths`  
    Paths to exclude, appearing after the home URL (for example, `articles` will exclude `https://www.mydomain.com/articles/` but not `https://www.mydomain.com/posts/articles/`). Partial paths are useful when the URL contains language information (for example, `https://www.mydomain.com/en/articles/`), so a single path would exclude that page for all languages (in this case, the home URL would be `https://www.mydomain.com/en/`). More on this later.

<div class="break-out">

<pre><code class="language-php">function get_sw_configuration() {

	…
	$resourceTypes = get_sw_resourcetypes();
	$configuration['$excludedFullPaths'] = $configuration['$excludedPartialPaths'] = array();
	foreach ($resourceTypes as $resourceType) {

		$configuration['$excludedFullPaths'][$resourceType] = apply_filters('PoP_ServiceWorkers_Job_Fetch:exclude:full', array(), $resourceType);
		$configuration['$excludedPartialPaths'][$resourceType] = apply_filters('PoP_ServiceWorkers_Job_Fetch:exclude:partial', array(), $resourceType);
	}
	…
}
</code></pre></div>

<figcaption>File: sw.php</figcaption>

The value `opts.locales.domain` will be calculated on runtime (more on this later).

<div class="break-out">

<pre><code class="language-javascript">var config = {
	…
	excludedPaths: {
		full: $excludedFullPaths,
		partial: $excludedPartialPaths
	},
	…
};

self.addEventListener('fetch', event =&gt; {

	function shouldHandleFetch(event, opts) {

		var request = event.request;
		var resourceType = getResourceType(request);
		var url = new URL(request.url);

		var fullExcluded = opts.excludedPaths.full[resourceType].some(path =&gt; request.url.startsWith(path)),

		var partialExcluded = opts.excludedPaths.partial[resourceType].some(path =&gt; request.url.startsWith(opts.locales.domain+path));

		if (fullExcluded || partialExcluded) return false;

		if (resourceType == 'static') {

			// Do not handla dynamic images, eg: the Captcha image, captcha.png.php
			var isDynamic = request.url.endsWith('.php') &amp;&amp; request.url.indexOf('.php?') === -1;
			if (isDynamic) return false;
		}

		…
	}

	…
});
</code></pre></div>

<figcaption>File: sw-template.js</figcaption>

Now we can define WordPress resources to be excluded. Please note that, because it depends on the resource type, we can define a rule to intercept any URL starting with `wp-content/`, which works only for the resource type “static.”

<div class="break-out">

<pre><code class="language-php">class PoP_ServiceWorkers_Hooks_WPExclude {

	function __construct() {

		add_filter('PoP_ServiceWorkers_Job_Fetch:exclude:full', array($this, 'get_excluded_fullpaths'), 10, 2);
	}

	function get_excluded_fullpaths($excluded, $resourceType) {

		if ($resourceType == 'json' || $resourceType == 'html') {

			// Do not intercept access to the WP Dashboard
			$excluded[] = admin_url();
			$excluded[] = content_url();
			$excluded[] = includes_url();
		}
		elseif ($resourceType == 'static') {

			// Do not cache the service-workers.js file!!!
			$excluded[] = WP_CONTENT_DIR.'/sw/service-workers.js';
		}

		return $excluded;
	}
}
new PoP_ServiceWorkers_Hooks_WPExclude();
</code></pre></div>

**Precaching resources**

In order for the WordPress website to work offline, we need to retrieve the full list of resources needed and precache them. We want to be able to cache both local and external resources (for example, from a CDN).

*   `$origins`  
    Define from which domains we enable the service worker to intercept the request (for example, from our own domain plus our CDN).
*   `$cacheItems`  
    List of resources to precache. It is initially an empty array, providing a hook to inject all values.

<pre><code class="language-javascript">var config = {
	…
	cacheItems: $cacheItems,
	origins: $origins,
	…
};
</code></pre>

<figcaption>File: sw-template.js</figcaption>

<div class="break-out">

<pre><code class="language-php">function get_sw_configuration() {

	…
	$resourceTypes = get_sw_resourcetypes();
	$configuration['$origins'] = get_sw_allowed_domains();
	$configuration['$cacheItems'] = array();
	foreach ($resourceTypes as $resourceType) {

		$configuration['$cacheItems'][$resourceType] = return apply_filters('PoP_ServiceWorkers_Job_CacheResources:precache', array(), $resourceType);
	}
	…
}

function get_sw_allowed_domains() {

	return array(
		get_site_url(), // 'https://www.mydomain.com',
		'https://cdn.mydomain.com'
	);
}
</code></pre></div>

<figcaption>File: sw.php</figcaption>

In order to precache external resources, executing `cache.addAll` will not work. Instead, we need to use the `fetch` function, passing the parameter `{mode: 'no-cors'}` for these.

<div class="break-out">

<pre><code class="language-javascript">self.addEventListener('install', event =&gt; {
  function onInstall(event, opts) {

	var resourceTypes = ['static', 'json', 'html'];
	return Promise.all(resourceTypes.map(function(resourceType) {
	  return caches.open(cacheName(resourceType, opts)).then(function(cache) {
		return Promise.all(opts.cacheItems[resourceType].map(function(url) {
		  return fetch(url, (new URL(url)).origin === self.location.origin ? {} : {mode: 'no-cors'}).then(function(response) {
			return cache.put(url, response.clone());
		  });
		}))
	  })
	}))
  }

  event.waitUntil(
	onInstall(event, config).then( () =&gt; self.skipWaiting() )
  );
});
</code></pre></div>

<figcaption>File: sw-template.js</figcaption>

Resources to be intercepted with the service worker either must come from any of our origins or must have been defined in the initial precache list (so that we can precache assets from yet other external domains, such as `https://cdnjs.cloudflare.com`):

<div class="break-out">

<pre><code class="language-javascript">self.addEventListener('fetch', event =&gt; {

	function shouldHandleFetch(event, opts) {

		…

		var fromMyOrigins = opts.origins.indexOf(url.origin) &gt; -1;
		var precached = opts.cacheItems[resourceType].indexOf(url) &gt; -1;

		if (!(fromMyOrigins || precached)) return false;

		…
	}

	…
});
</code></pre></div>

<figcaption>File: sw-template.js</figcaption>

**Generating the list of resources to precache**

Assets loaded through `wp_enqueue_script` and `script_loader_tag` can be extracted easily. Finding other assets involves a manual process, depending on whether they are coming from WordPress core files, from the theme or from installed plugins:

*   images;
*   CSS and JavaScript not loaded through `wp_enqueue_script` and `script_loader_tag`;
*   JavaScript files conditionally loaded (such as those added between `html` tags);
*   resources requested on runtime (for example, TinyMCE’s theme, skin and plugin files);
*   references to JavaScript files hardcoded another JavaScript file;
*   Font files referenced in CSS files (TTF, WOFF, etc.);
*   locale files;
*   i18n files.

To retrieve all JavaScript files loaded through the `wp_enqueue_script` function, we would hook into `script_loader_tag`, and for all CSS files loaded through the `wp_enqueue_style` function, we would hook into `style_loader_tag`:

<div class="break-out">

<pre><code class="language-php">class PoP_ServiceWorkers_Hooks_WP {

	private $scripts, $styles, $dom;

	function __construct() {

		$this-&gt;scripts = $this-&gt;styles = array();
		$this-&gt;doc = new DOMDocument();

		add_filter('script_loader_tag', array($this, 'script_loader_tag'));
		add_filter('style_loader_tag', array($this, 'style_loader_tag'));

		…
	}

	function script_loader_tag($tag) {

		if (!empty($tag)) {

			$this-&gt;doc-&gt;loadHTML($tag);
			foreach($this-&gt;doc-&gt;getElementsByTagName('script') as $script) {
				if($script-&gt;hasAttribute('src')) {

					$this-&gt;scripts[] = $script-&gt;getAttribute('src');
				}
			}
		}

		return $tag;
	}

	function style_loader_tag($tag) {

		if (!empty($tag)) {

			$this-&gt;doc-&gt;loadHTML($tag);
			foreach($this-&gt;doc-&gt;getElementsByTagName('link') as $link) {
				if($link-&gt;hasAttribute('href')) {

					$this-&gt;styles[] = $link-&gt;getAttribute('href');
				}
			}
		}

		return $tag;
	}

	…
}
new PoP_ServiceWorkers_Hooks_WP();
</code></pre></div>

Then, we simply add all of these resources to the precache list:

<div class="break-out">

<pre><code class="language-php">class PoP_ServiceWorkers_Hooks_WP {

	function __construct() {

		…

		add_filter('PoP_ServiceWorkers_Job_CacheResources:precache', array($this, 'get_precache_list'), 10, 2);
	}

	function get_precache_list($precache, $resourceType) {

		if ($resourceType == 'static') {

			$precache = array_merge(
				$precache,
				$this-&gt;scripts,
				$this-&gt;styles
			);
		}

		return $precache;
	}
}
</code></pre></div>

WordPress will load a few files that must be manually added. Please note that the reference to the file must be added exactly as it will be requested, including all of the parameters. So, this process involves a lot of copying and pasting from the original code:

<div class="break-out">

<pre><code class="language-php">class PoP_ServiceWorkers_Hooks_WPManual {

	function __construct() {

		add_filter('PoP_ServiceWorkers_Job_CacheResources:precache', array($this, 'get_precache_list'), 10, 2);
	}

	function get_precache_list($precache, $resourceType) {

		if ($resourceType == 'static') {

			// File json2.min.js is not added through the $scripts list because it's 'lt IE 8'
			global $wp_scripts;
			$suffix = SCRIPT_DEBUG ? '' : '.min';
			$this-&gt;scripts[] = add_query_arg('ver', '2015-05-03', $wp_scripts-&gt;base_url."/wp-includes/js/json2$suffix.js");

			// Needed for the thickboxL10n['loadingAnimation'] javascript code produced in the front-end, loaded in wp-includes/script-loader.php
			$precache[] = includes_url('js/thickbox/loadingAnimation.gif');
		}

		return $precache;
	}
}
new PoP_ServiceWorkers_Hooks_WPManual();
</code></pre></div>

TinyMCE presents a tough challenge for obtaining its list of resources, because the files it loads (such as plugins, skins and theme files) are actually created and requested on runtime. Moreover, the full path of the resource is not printed in the HTML code, but is assembled in a JavaScript function. So, to obtain the list of resources, one can inspect TinyMCE’s source code and check how it generates the file names, or guess them by creating a TinyMCE editor while inspecting Chrome’s Developer Tools’ “Network” tab and seeing which files it requests. Doing the latter, I was able to deduce all file names (for example, for theme files, the path is a combination of the domain, theme name and versioning as parameters).

To obtain TinyMCE’s configuration that will be used on runtime, we hook into `store_tinymce_resources` and `teeny_mce_before_init` and inspect the values set in the `$mceInit` variable:

<div class="break-out">

<pre><code class="language-php">class PoP_ServiceWorkers_Hooks_TinyMCE {

	private $content_css, $external_plugins, $plugins, $others;

	function __construct() {

		$this-&gt;content_css = $this-&gt;external_plugins = $this-&gt;plugins = $this-&gt;others = array();

		// Execute last one
		add_filter('teeny_mce_before_init', array($this, 'store_tinymce_resources'), PHP_INT_MAX, 1);
		add_filter('tiny_mce_before_init', array($this, 'store_tinymce_resources'), PHP_INT_MAX, 1);
	}

	function store_tinymce_resources($mceInit) {

		// Code copied from wp-includes/class-wp-editor.php function editor_js()
		$suffix = SCRIPT_DEBUG ? '' : '.min';
		$baseurl = includes_url( 'js/tinymce' );
		$cache_suffix = $mceInit['cache_suffix'];

		if ($content_css = $mceInit['content_css']) {
			foreach (explode(',', $content_css) as $content_css_item) {

				// The $cache_suffix is added in runtime, it can be safely added already. Eg: wp-includes/css/dashicons.min.css?ver=4.6.1&amp;wp-mce-4401-20160726
				$this-&gt;content_css[] = $content_css_item.'&amp;'.$cache_suffix;
			}
		}
		if ($external_plugins = $mceInit['external_plugins']) {

			if ($external_plugins = json_decode($external_plugins, true)) {
				foreach ($external_plugins as $plugin) {
					$this-&gt;external_plugins[] = "{$plugin}?{$cache_suffix}";
				}
			}
		}
		if ($plugins = $mceInit['plugins']) {

			if ($plugins = explode(',', $plugins)) {

				// These URLs are generated on runtime in TinyMCE, without a $version
				foreach ($plugins as $plugin) {
					$this-&gt;plugins[] = "{$baseurl}/plugins/{$plugin}/plugin{$suffix}.js?{$cache_suffix}";
				}

				if (in_array('wpembed', $plugins)) {

					// Reference to file wp-embed.js, without any parameter, is hardcoded inside file wp-includes/js/tinymce/plugins/wpembed/plugin.min.js!!!
					$this-&gt;others[] = includes_url( 'js' )."/wp-embed.js";
				}
			}
		}
		if ($skin = $mceInit['skin']) {

			// Must produce: wp-includes/js/tinymce/skins/lightgray/content.min.css?wp-mce-4401-20160726
			$this-&gt;others[] = "{$baseurl}/skins/{$skin}/content{$suffix}.css?{$cache_suffix}";
			$this-&gt;others[] = "{$baseurl}/skins/{$skin}/skin{$suffix}.css?{$cache_suffix}";

			// Must produce: wp-includes/js/tinymce/skins/lightgray/fonts/tinymce.woff
			$this-&gt;others[] = "{$baseurl}/skins/{$skin}/fonts/tinymce.woff";
		}
		if ($theme = $mceInit['theme']) {
			// Must produce: wp-includes/js/tinymce/themes/modern/theme.min.js?wp-mce-4401-20160726
			$this-&gt;others[] = "{$baseurl}/themes/{$theme}/theme{$suffix}.js?{$cache_suffix}";
		}

		// Files below are always requested. Code copied from wp-includes/class-wp-editor.php function editor_js()
		global $wp_version, $tinymce_version;
		$version = 'ver=' . $tinymce_version;
		$mce_suffix = false !== strpos( $wp_version, '-src' ) ? '' : '.min';

		$this-&gt;others[] = "{$baseurl}/tinymce{$mce_suffix}.js?$version";
		$this-&gt;others[] = "{$baseurl}/plugins/compat3x/plugin{$suffix}.js?$version";
		$this-&gt;others[] = "{$baseurl}/langs/wp-langs-en.js?$version";

		return $mceInit;
	}
}
new PoP_ServiceWorkers_Hooks_TinyMCE();
</code></pre></div>

Finally, we add the extracted resources to the precache list:

<div class="break-out">

<pre><code class="language-php">class PoP_ServiceWorkers_Hooks_TinyMCE {

	function __construct() {

		…

		add_filter('PoP_ServiceWorkers_Job_CacheResources:precache', array($this, 'get_precache_list'), 1000, 2);
	}

	…

	function get_precache_list($precache, $resourceType) {

		if ($resourceType == 'static') {

			// In addition, add all the files in the tinymce plugins folder, since these will be needed during runtime when initializing the tinymce textarea
			$precache = array_merge(
				$precache,
				$this-&gt;content_css,
				$this-&gt;external_plugins,
				$this-&gt;plugins,
				$this-&gt;others
			);
		}

		return $precache;
	}
}
</code></pre></div>

We must also precache all images required by the theme and all plugins. In the code below, we precache all of the theme’s files in the folder `img/`, assuming that these are requested without adding parameters:

<div class="break-out">

<pre><code class="language-php">class PoPTheme_Wassup_ServiceWorkers_Hooks_ThemeImages {

	function __construct() {

		add_filter('PoP_ServiceWorkers_Job_CacheResources:precache', array($this, 'get_precache_list'), 10, 2);
	}

	function get_precache_list($precache, $resourceType) {

		if ($resourceType == 'static') {

			// Add all the images from the active theme
			$theme_dir = get_stylesheet_directory();
			$theme_uri = get_stylesheet_directory_uri();
			foreach (glob($theme_dir."/img/*") as $file) {
				$precache[] = str_replace($theme_dir, $theme_uri, $file);
			}
		}

		return $precache;
	}
}
new PoPTheme_Wassup_ServiceWorkers_Hooks_ThemeImages();
</code></pre></div>

If we use Twitter Bootstrap, loaded from a CDN (for example, `https://cdnjs.cloudflare.com/ajax/libs/twitter-bootstrap/3.3.7/css/bootstrap.min.css`), then we must precache the corresponding glyphicons’ font files:

<div class="break-out">

<pre><code class="language-php">class PoPTheme_Wassup_ServiceWorkers_Hooks_Bootstrap {

	function __construct() {

		add_filter('PoP_ServiceWorkers_Job_CacheResources:precache', array($this, 'get_precache_list'), 10, 2);
	}

	function get_precache_list($precache, $resourceType) {

		if ($resourceType == 'static') {

			// Add all the fonts needed by Bootstrap inside the bootstrap.min.css file
			$precache[] = 'https://cdnjs.cloudflare.com/ajax/libs/twitter-bootstrap/3.3.7/fonts/glyphicons-halflings-regular.eot';
			$precache[] = 'https://cdnjs.cloudflare.com/ajax/libs/twitter-bootstrap/3.3.7/fonts/glyphicons-halflings-regular.svg';
			$precache[] = 'https://cdnjs.cloudflare.com/ajax/libs/twitter-bootstrap/3.3.7/fonts/glyphicons-halflings-regular.ttf';
			$precache[] = 'https://cdnjs.cloudflare.com/ajax/libs/twitter-bootstrap/3.3.7/fonts/glyphicons-halflings-regular.woff';
			$precache[] = 'https://cdnjs.cloudflare.com/ajax/libs/twitter-bootstrap/3.3.7/fonts/glyphicons-halflings-regular.woff2';
		}

		return $precache;
	}
}
new PoPTheme_Wassup_ServiceWorkers_Hooks_Bootstrap();
</code></pre></div>

All language-specific resources for all languages must also be precached, so that the website can be loaded in any language when offline. In the code below, we assume the plugin has a `js/locales/` folder with the translation files `locale-en.js`, `locale-es.js`, etc:

<div class="break-out">

<pre><code class="language-php">class PoP_UserAvatar_ServiceWorkers_Hooks_Locales {

	function __construct() {

		add_filter('PoP_ServiceWorkers_Job_CacheResources:precache', array($this, 'get_precache_list'), 10, 2);
	}

	function get_precache_list($precache, $resourceType) {

		if ($resourceType == 'static') {

			$dir = dirname(__FILE__));
			$url = plugins_url('', __FILE__));
			foreach (glob($dir."/js/locales/fileupload/*") as $file) {
				$precache[] = str_replace($dir, $url, $file);
			}
		}

		return $precache;
	}
}
new PoP_UserAvatar_ServiceWorkers_Hooks_Locales();
</code></pre></div>

**Non-caching strategies**

In the following, we will delve into caching and non-caching strategies. Let's tackle the non-caching strategy first:

*   **Network only**  
    Whenever JSON requests have user state.

To not cache a request, if we know which URLs must not be cached in advance, then we can simply add their full or partial paths in the list of excluded items. For instance, below, we’ve set all pages that have user state (such as “My posts” and “Edit my profile”) to not be intercepted by the service worker, because we don’t want to cache any personal information of the user:

<div class="break-out">

<pre><code class="language-php">function get_page_path($page_id) {

	$page_path = substr(get_permalink($page_id), strlen(home_url()));

	// Remove the first and last '/'
	if ($page_path[0] == '/') $page_path = substr($page_path, 1);
	if ($page_path[strlen($page_path)-1] == '/') $page_path = substr($page_path, 0, strlen($page_path)-1);

	return $page_path;
}

class PoP_ServiceWorkers_Hooks_UserState {

	function __construct() {

		add_filter('PoP_ServiceWorkers_Job_Fetch:exclude:partial', array($this, 'get_excluded_partialpaths'), 10, 2);
	}

	function get_excluded_partialpaths($excluded, $resourceType) {

		if ($resourceType == 'json') {

			// Variable $USER_STATE_PAGES contains all IDs of pages that have a user state
			foreach ($USER_STATE_PAGES as $page_id) {

				$excluded[] = get_page_path($page_id);
			}
		}

		return $excluded;
	}
}
new PoP_ServiceWorkers_Hooks_UserState();
</code></pre></div>

If the non-caching strategy must be applied on runtime, then we can add a parameter, `sw-networkonly=true` or `sw-strategy=networkonly` to the requested URL, and dismiss handling it with a service worker in the function `shouldHandleFetch`:

<div class="break-out">

<pre><code class="language-javascript">self.addEventListener('fetch', event =&gt; {

	function shouldHandleFetch(event, opts) {

		…

		var params = getParams(url);
		if (params['sw-strategy'] == 'networkonly') return false;

		…
	}

	…
});
</code></pre></div>

<figcaption>File: sw-template.js</figcaption>

**Caching strategies**

The application uses the following caching strategies, depending on the resource type and functional use:

*   **Cache, falling back to network** for the appshell and static resources.
*   **Cache, then network** for JSON requests.
*   **Network, falling back to cache** for JSON requests that do not keep the user waiting, such as lazy-loaded data (for example, a post’s comments), or that must be up to date (for example, viewing a post after it’s been updated).

Both static and HTML resource types will always require the same strategy. It is only the JSON resource type that can be switched between strategies. We establish the “cache, then network” strategy as the default one, and define rules over the requested URL to switch to “network, falling back to cache”:

*   `startsWith`  
    The URL starts with a predefined full or partial path.
*   `hasParams`  
    The URL contains a predefined parameter. The parameter `sw-networkfirst` has been defined already, so requesting `https://www.mydomain.com/en/?output=json` will use the “cache first” strategy, whereas `https://www.mydomain.com/en/?output=json&sw-networkfirst=true` will switch to “network first.”

<div class="break-out">

<pre><code class="language-javascript">// Cache falling back to network
const SW_CACHEFIRST = 1;

// Cache then network
const SW_CACHEFIRSTTHENREFRESH = 2;

// Network falling back to cache
const SW_NETWORKFIRST = 3;

var config = {
	…
	strategies: $strategies,
	…
};
</code></pre></div>

<figcaption>File: sw-template.js</figcaption>

<div class="break-out">

<pre><code class="language-php">function get_sw_configuration() {

	…
	$resourceTypes = get_sw_resourcetypes();
	$configuration['$strategies'] = array();
	foreach ($resourceTypes as $resourceType) {

		$strategies = array();
		if ($resourceType == 'json') {

			$strategies['networkFirst'] = array(
				'startsWith' =&gt; array(
					'full' =&gt; apply_filters('PoP_ServiceWorkers_Job_Fetch:strategies:json:networkFirst:startsWith:full', array()),
					'partial' =&gt; apply_filters('PoP_ServiceWorkers_Job_Fetch:strategies:json:networkFirst:startsWith:partial', array()),
				),
				'hasParams' =&gt; apply_filters('PoP_ServiceWorkers_Job_Fetch:strategies:json:networkFirst:hasParams', array('sw-networkfirst')),
			);
		}

		$configuration['$strategies'][$resourceType] = $strategies;
	}
	…
}
</code></pre></div>

<figcaption>File: sw.php</figcaption>

We hook in all the pages that need to use the “network first” strategy. Below, we add the lazy-loaded pages:

<div class="break-out">

<pre><code class="language-php">class PoP_ServiceWorkers_Hooks_LazyLoaded {

	function __construct() {

		add_filter('PoP_ServiceWorkers_Job_Fetch:strategies:json:networkFirst:startsWith:partial', array($this, 'get_networkfirst_json_partialpaths'));
	}

	function get_networkfirst_json_partialpaths($paths) {

		foreach ($LAZY_LOADED_PAGES as $page_id) {

			$paths[] = get_page_path($page_id);
		}

		return $paths;
	}
}
new PoP_ServiceWorkers_Hooks_LazyLoaded();
</code></pre></div>

After merging `sw-template.js` into `service-workers.js`, it will look like this:

<pre><code class="language-javascript">var config = {
	…
	strategies: {
		json: {
			networkFirst: {
				startsWith: {
					partial: […]
				},
				hasParams: […]
			}
		}
	},
	…
};
</code></pre>

Finally, we get to the logic in the `service-workers.js` file. Please note that to fetch JSON requests, we will also [need to add](https://developers.google.com/web/showcase/2015/service-workers-iowa#cache-bust_your_precaching_requests) to the URL cache-busting parameter `sw-cachebust`, with a timestamp to avoid getting the response from the browser’s HTTP cache.

<div class="break-out">

<pre><code class="language-javascript">function getCacheBustRequest(request, opts) {

	var url = new URL(request.url);

	// Put in a cache-busting parameter to ensure we’re caching a fresh response.
	if (url.search) {
	  url.search += '&amp;';
	}
	url.search += 'sw-cachebust=' + Date.now();

	return new Request(url.toString());
}
function addToCache(cacheKey, request, response) {

	if (response.ok) {
		var copy = response.clone();
		caches.open(cacheKey).then( cache =&gt; {
			cache.put(request, copy);
		});
	}
	return response;
}
self.addEventListener('fetch', event =&gt; {

	function getStrategy(request, opts) {

		var strategy = '';
		var resourceType = getResourceType(request);

		// JSON requests have two strategies: cache first + update (the default) or network first
		if (resourceType === 'json') {

			var networkFirst = opts.strategies[resourceType].networkFirst;
			var criteria = {
				startsWith: networkFirst.startsWith.full.some(path =&gt; request.url.startsWith(path)),
				// The pages do not included the locale domain, so add it before doing the comparison
				pageStartsWith: networkFirst.startsWith.partial.some(path =&gt; request.url.startsWith(opts.locales.domain+path)),
				// Code for function stripIgnoredUrlParameters is in https://github.com/leoloso/PoP/blob/master/wp-content/plugins/pop-serviceworkers/kernel/serviceworkers/assets/js/jobs/lib/utils.js
				hasParams: stripIgnoredUrlParameters(request.url, networkFirst.hasParams) != request.url
			}
			var successCriteria = Object.keys(criteria).filter(criteriaKey =&gt; criteria[criteriaKey]);
			if (successCriteria.length) {

				strategy = SW_NETWORKFIRST;
			}
			else {

				strategy = SW_CACHEFIRSTTHENREFRESH;
			}
		}
		else if (resourceType === 'html' || resourceType === 'static') {

			strategy = SW_CACHEFIRST;
		}

		return strategy;
	}

	function onFetch(event, opts) {

		var request = event.request;
		var resourceType = getResourceType(request);
		var cacheKey = cacheName(resourceType, opts);

		var strategy = getStrategy(request, opts);
	    var cacheBustRequest = getCacheBustRequest(request, opts);

		if (strategy === SW_CACHEFIRST || strategy === SW_CACHEFIRSTTHENREFRESH) {

			/* Load immediately from the Cache */
			event.respondWith(
				fetchFromCache(request)
					.catch(() =&gt; fetch(request))
					.then(response =&gt; addToCache(cacheKey, request, response))
			);

			/* Bring fresh content from the server, and show a message to the user if the cached content is stale */
			if (strategy === SW_CACHEFIRSTTHENREFRESH) {
				event.waitUntil(
					fetch(cacheBustRequest)
						.then(response =&gt; addToCache(cacheKey, request, response))
						.then(response =&gt; refresh(request, response))
				);
			}
		}
		else if (strategy === SW_NETWORKFIRST) {

			event.respondWith(
				fetch(cacheBustRequest)
					.then(response =&gt; addToCache(cacheKey, request, response))
					.catch(() =&gt; fetchFromCache(request))
					.catch(function(err) {/*console.log(err)*/})
			);
		}
	}

	if (shouldHandleFetch(event, config)) {

		onFetch(event, config);
	}
});
</code></pre></div>

<figcaption>File: sw-template.js</figcaption>

The “cache then network” strategy uses the `refresh` function to cache the most updated content coming from the server, and if it differs from the previously cached one, then post a message to the client browser to notify the user. It makes the comparison not of the actual contents, but of their ETag headers (generation of the ETag header will be explained below). The cached ETag value is stored using [localForage](https://github.com/localForage/localForage), a simple yet powerful API wrapping IndexedDB:

<div class="break-out">

<pre><code class="language-javascript">function refresh(request, response) {

	var ETag = response.headers.get('ETag');
	if (!ETag) return null;

	var key = 'ETag-'+response.url;
	return localforage.getItem(key).then(function(previousETag) {

		// Compare the ETag of the response with the previous one saved in the IndexedDB
		if (ETag == previousETag) return null;

		// Save the new value
		return localforage.setItem(key, ETag).then(function() {

			// If there was no previous ETag, then send no notification to the user
			if (!previousETag) return null;

			// Send a message to the client
			return self.clients.matchAll().then(function (clients) {
				clients.forEach(function (client) {
					var message = {
						type: 'refresh',
						url: response.url
					};

					client.postMessage(JSON.stringify(message));
				});
				return response;
			});
		});
	});
}
</code></pre></div>

<figcaption>File: sw-template.js</figcaption>

A JavaScript function catches the messages delivered by the service worker, and prints a message requesting the user to refresh the page:

<div class="break-out">

<pre><code class="language-javascript">function showRefreshMsgToUser() {

	if ('serviceWorker' in navigator) {

		navigator.serviceWorker.onmessage = function (event) {

			var message = JSON.parse(event.data);
			if (message.type === 'refresh') {

				var msg = 'This page has been updated, &lt;a href="'+message.url+'"&gt;click here to refresh it&lt;/a&gt;.';
				var alert = '&lt;div class="alert alert-warning alert-dismissible" role="alert"&gt;&lt;button type="button" class="close" aria-hidden="true" data-dismiss="alert"&gt;×&lt;/button&gt;'+msg+'&lt;/div&gt;';
				jQuery('body').prepend(alert);
			}
		};
	}
}
</code></pre></div>

### Generating the ETag Header

An ETag header is a hash representing the content being served; because it is a hash, a minimal change in the source will lead to the creation of a completely different ETag. We must make sure that the ETag is generated from the actual website content, and ignore information not visible to the user, such as HTML tag IDs. Otherwise, consider the following sequence happening for the “cache then network” strategy:

1.  An ID is generated, using `now()` to make it unique, and printed in the page’s HTML.
2.  When accessed for the first time, this page is created and its ETag is generated.
3.  When accessed a second time, the page is served immediately from the service worker cache, and a network request is triggered to refresh the content.
4.  This request generates the page again. Even if it hasn’t been updated, its content will be different, because `now()` will produce a different value, and its ETag header will be different.
5.  The browser will compare the two ETags and, because they are different, prompt the user to refresh the content, even if the page has not been updated.

One solution is to remove all dynamically generated values, such as `current_time('timestamp')` and `now()`, before generating the ETag. For this, we can set all dynamic values in constants, and then use these constants throughout the application. Finally, we would remove these from the input to the hash-generation function:

<div class="break-out">

<pre><code class="language-php">define('TIMESTAMP', current_time('timestamp'));
define('NOW',  now());

ob_start();
// All the application code in between (using constants TIMESTAMP, NOW if needed)
$content = ob_get_clean();

$dynamic = array(TIMESTAMP, NOW);
$etag_content = str_replace($dynamic, '', $content);

header('ETag: '.wp_hash($etag_content));
echo($content);
</code></pre></div>

A similar strategy is needed for those pieces of information that are allowed to become stale, such as a post’s comments count, mentioned earlier. Because this value is not important, we don’t want the user to receive a notification to refresh the page merely because the number of comments has increased from 5 to 6.</p>

### Appshell With Support for Multilingual, Multiple Presentation Modes

No matter which URL is requested by the user, the application will load the appshell instead, which will immediately load the contents of the requested URL (still accessible in `window.location.href`) through the API, passing along the locale and all needed parameters.

The application has different views and languages, and we want these different appshells to be precached, and then load the appropriate one on runtime, fetching the information from the requested URL: `https://www.mydomain.com/language-code/path/to/page/?view=`….

As mentioned earlier, given two languages (English and Spanish) and three views (default, embed and print), we will need to precache the following appshells:

*   `https://www.mydomain.com/en/appshell/?view=default`
*   `https://www.mydomain.com/en/appshell/?view=embed`
*   `https://www.mydomain.com/en/appshell/?view=print`
*   `https://www.mydomain.com/es/appshell/?view=default`
*   `https://www.mydomain.com/es/appshell/?view=embed`
*   `https://www.mydomain.com/es/appshell/?view=print`

In addition to the language and the view, the application might have other parameters (let’s say “style” and “format”). However, adding these would make the combinations of URLs to precache grow tremendously. So, we need to settle on a trade-off, deciding which parameters to precache (the most used ones) and which ones not to. For the latter ones, their corresponding URL can be accessed offline only starting from the second access.

<table class="tablesaw break-out" data-tablesaw-mode="swipe" data-tablesaw-minimap>
<thead>
<tr>
<th data-tablesaw-priority="persist">URL requested</th>
<th>Appshell</th>
<th>Precached</th>
</tr>
</thead>
<tbody>
<tr>
<td><code>https://www.mydomain.com/en/</code></td>
<td><code>https://www.mydomain.com/en/appshell/?view=default</code></td>
<td>Yes</td>
</tr>
<tr>
<td><code>https://www.mydomain.com/en/?view=print</code></td>
<td><code>https://www.mydomain.com/en/appshell/?view=print</code></td>
<td>Yes</td>
</tr>
<tr>
<td><code>https://www.mydomain.com/en/?view=print&amp;style=classic</code></td>
<td><code>https://www.mydomain.com/en/appshell/?view=print&amp;style=classic</code></td>
<td>No</td>
</tr>
</tbody>
</table>

By adding hooks into the configuration, we allow multilingual plugins, such as [qTranslate X](https://wordpress.org/plugins/qtranslate-x/), to modify the locales and languages and the URLs accordingly.

<pre><code class="language-javascript">var config = {
	…
	appshell: {
		pages: $appshellPages,
		params: $appshellParams
	},
	…
};
</code></pre>

<figcaption>File: sw-template.js</figcaption>

<div class="break-out">

<pre><code class="language-php">function get_sw_configuration() {

	…

	$configuration['$appshellPages'] = get_sw_appshell_pages();
    $configuration['$appshellParams'] = apply_filters('PoP_ServiceWorkers_Job_Fetch:appshell_params', array("themestyle", "settingsformat", "mangled"));
	…
}

function get_sw_appshell_pages() {

	// Locales: can be hooked into by qTranslate to input the language codes
    $locales = apply_filters('PoP_ServiceWorkers_Job_Fetch:locales', array(get_locale()));
    $views = array("default", "embed", "print");

	$appshellPages = array();
    foreach ($locales as $locale) {
        foreach ($views as $view) {

            // By adding a hook to the URL, we can allow plugins to modify the URL
            $appshellPages[$locale][$view] = apply_filters('PoP_ServiceWorkers_Job_Fetch:appshell_url', add_query_arg('view', $view, get_permalink($APPSHELL_PAGE_ID), $locale);
        }
    }

	return apply_filters('PoP_ServiceWorkers_Job_Fetch:appshell_pages', $appshellPages);
}
</code></pre></div>

<figcaption>File: sw.php</figcaption>

<div class="break-out">

<pre><code class="language-php">class PoP_ServiceWorkers_QtransX_Job_Fetch_Hooks {

	function __construct() {

		add_filter('PoP_ServiceWorkers_Job_Fetch:locales', array($this, 'get_locales'));
		add_filter('PoP_ServiceWorkers_Job_Fetch:appshell_url', array($this, 'get_appshell_url'), 10, 2);
		…
	}

	function get_locales($locales) {

		global $q_config;
		if ($languages = $q_config['enabled_languages']) {

			return $languages;
		}

		return $locales;
	}

	function get_appshell_url($url, $lang) {

		return qtranxf_convertURL($url, $lang);
	}
}
new PoP_ServiceWorkers_QtransX_Job_Fetch_Hooks();
</code></pre></div>

After merging `sw-template.js` into `service-workers.js`, it will look like this:

<div class="break-out">

<pre><code class="language-javascript">var config = {
	appshell: {
		pages: {
			es: {
				default: "https://www.mydomain.com/es/appshell/?view=default",
				embed: "https://www.mydomain.com/es/appshell/?view=embed",
				print: "https://www.mydomain.com/es/appshell/?view=print"
			},
			en :{
				default: "https://www.mydomain.com/en/appshell/?view=default",
				embed: "https://www.mydomain.com/en/appshell/?view=embed",
				print: "https://www.mydomain.com/en/appshell/?view=print"
			}
		},
		params: ["style", "format"]
	},
};
</code></pre></div>

The request is intercepted with the method `onFetch`, and if it is of the HTML resource type, it will be replaced with the appshell URL instead, just after deciding which strategy is to be employed. (Below we’ll see how to get the current locale, set in `opts.locales.current`.)

<div class="break-out">

<pre><code class="language-javascript">function onFetch(event, opts) {

    var request = event.request;
    …

    var strategy = getStrategy(request, opts);

    // Allow to modify the request, fetching content from a different URL
    request = getRequest(request, opts);

    …
}

function getRequest(request, opts) {

    var resourceType = getResourceType(request);
    if (resourceType === 'html') {

      // The different appshells are a combination of locale and view.
      var params = getParams(request.url);
      var view = params.view || 'default';

      // The initial appshell URL has the params that we have precached.
      var url = opts.appshell.pages[opts.locales.current][view];

      // In addition, there are other params that, if provided by the user, must be added to the URL. These params are not originally precached in any appshell URL, so such a page will have to be retrieved from the server.
      opts.appshell.params.forEach(function(param) {

        // If the param was passed in the URL, then add it along.
        if (params[param]) {
          url += '&amp;'+param+'='+params[param];
        }
      });
      request = new Request(url);
    }

    return request;
}
</code></pre></div>

Lastly, we proceed to precache the appshells:

<div class="break-out">

<pre><code class="language-php">class PoP_ServiceWorkers_Hooks_AppShell {

	function __construct() {

		add_filter('PoP_ServiceWorkers_Job_CacheResources:precache', array($this, 'get_precache_list'), 10, 2);
	}

	function get_precache_list($precache, $resourceType) {

		if ($resourceType == 'html') {
			foreach (get_sw_appshell_pages() as $locale =&gt; $views) {
				foreach ($views as $view =&gt; $url) {

					$precache[] = $url;
				}
			}
		}

		return $precache;
	}
}
new PoP_ServiceWorkers_Hooks_AppShell();
</code></pre></div>

**Obtaining the locale**

The appshell has multilingual support, so we need to extract the language information from the requested URL.

<div class="break-out">

<pre><code class="language-javascript">var config = {
	…
	locales: {
		all: $localesByURL,
		default: $defaultLocale,
		current: null,
		domain: null
	},
	…
};
</code></pre></div>

<figcaption>File: sw-template.js</figcaption>

By default, we simply set the locale to be `get_locale()`, and we allow plugins to hook their values in:

<div class="break-out">

<pre><code class="language-php">function get_sw_configuration() {

	…
	$configuration['$localesByURL'] = apply_filters('PoP_ServiceWorkers_Job_Fetch:locales_byurl', array(site_url() =&gt; get_locale()));
	$configuration['$defaultLocale'] = apply_filters('PoP_ServiceWorkers_Job_Fetch:default_locale', get_locale());
	…
}
</code></pre></div>

<figcaption>File: sw.php</figcaption>

Having a multilingual plugin enabled, such as qTranslate X, we can hook in the languages:

<div class="break-out">

<pre><code class="language-php">class PoP_ServiceWorkers_QtransX_Job_Fetch_Hooks {

	function __construct() {

		…
		add_filter('PoP_ServiceWorkers_Job_Fetch:locales_byurl', array($this, 'get_locales_byurl'));
		add_filter('PoP_ServiceWorkers_Job_Fetch:default_locale', array($this, 'get_default_locale'));
	}

	function get_locales_byurl($locales) {

		global $q_config;
		if ($languages = $q_config['enabled_languages']) {

			$locales = array();
			$url = trailingslashit(home_url());
			foreach ($languages as $lang) {

				$locales[qtranxf_convertURL($url, $lang)] = $lang;
			}
		}

		return $locales;
	}

	function get_default_locale($default) {

		if ($lang = qtranxf_getLanguage()) {

			return $lang;
		}

		return $default;
	}
}
</code></pre></div>

After merging `sw-template.js` into `service-workers.js`, it will look like this:

<div class="break-out">

<pre><code class="language-javascript">var config = {
	locales: {
		all: {
			"https://www.mydomain.com/es/":"en",
			"https://www.mydomain.com/en/":"es"
		},
		default: "en",
		current: null,
		domain: null
	},
};
</code></pre></div>

Finally, we obtain the language code from the requested URL, and initialize the locale’s `current` and `domain` configuration values at the beginning of the `fetch` event:

<div class="break-out">

<pre><code class="language-javascript">self.addEventListener('fetch', event =&gt; {

  config = initOpts(config, event);
  if (shouldHandleFetch(event, config)) {

    …
  }

});

function initOpts(opts, event) {

	// Find the current locale and set it on the configuration object
	opts.locales.current = getLocale(event, opts);
	opts.locales.domain = getLocaleDomain(event, opts);
	return opts;
}

function getLocale(event, opts) {

	var currentDomain = getCurrentDomain(event, opts);
	if (currentDomain.length) {
		return opts.locales.all[currentDomain];
	}
	return opts.locales.default;
}

function getLocaleDomain(event, opts) {

	var currentDomain = getCurrentDomain(event, opts);
	if (currentDomain.length) {
		return currentDomain[0];
	}

	// Return the default domain
	return Object.keys(opts.locales.all).filter(function(key) {return opts.locales.all[key] === opts.locales.default})[0];
}

function getCurrentDomain(event, opts) {

	return Object.keys(opts.locales.all).filter(path =&gt; event.request.url.startsWith(path));
}
</code></pre></div>

### Dealing With Nonces

A nonce (or a “number used once”) is a cryptographic hash used to verify the authenticity of a person or client. WordPress uses nonces as security tokens to protect URLs and forms from malicious attacks. In spite of their name, WordPress uses a nonce more than once, giving it a limited lifetime, after which it expires. Even though they are not the ultimate security measure, nonces are a good first filter to prevent hacker attacks.

The HTML code printed on any WordPress page will contain nonces, such as the nonce for uploading images to the media manager, saved in the JavaScript object `_wpPluploadSettings.defaults.multipart_params._wpnonce`. The lifetime of a nonce is, by default, set to 24 hours (configured in the `nonce_life` hook). However, this value is shorter than the expected duration of the appshell in the service worker cache. This is a problem: After just 24 hours, the appshell will contain invalid nonces, which will make the application malfunction, such as giving error messages when the user attempts to upload images.

There are a few solutions to overcome this problem:

*   Immediately after loading the appshell, load another page in the background, using the “network only” strategy, to update the value of the nonce in the original JavaScript object:

<div class="break-out">

<pre><code class="language-js">
        <script type="text/javascript">
        _wpPluploadSettings.defaults.multipart_params._wpnonce = "<?php echo $VALID_NONCE ?>";
        </script>
      </code></pre></div>

*   Implement a longer `nonce_life`, such as three months, and then make sure to deploy a new version of the service worker within this lifespan:

<div class="break-out">

<pre><code class="language-php">
        add_filter('nonce_life', 'sw_nonce_life');
        function sw_nonce_life($nonce_life) {

        	return 90*DAY_IN_SECONDS;
        }</code></pre></div>

    Because this solution weakens the security of nonces, tougher security measures must also be put in place throughout the application, such as making sure that the user can edit a post:

<div class="break-out">

<pre><code class="language-php">if (!current_user_can('edit_post', $post_id))
	wp_die( __( 'Sorry, you are not allowed to edit this item.'));
</code></pre></div>

### Additional Considerations

The fact that something can be done doesn’t mean it should be done. The developer must evaluate whether each feature needs to be added according to the requirements of the app, not just because the technology allows it.

Below, I’ll show a few examples of functionality that can be perfectly implemented using other solutions or that need some workaround in order to make them work with service workers.

**Showing a simple “You’re offline” message**

Service workers can be used to display an [offline fallback](https://serviceworke.rs/offline-fallback.html) page whenever the user has no Internet connection. In its most basic implementation of just showing a “You are offline” message, I believe that we are not getting the most value out of this fallback page. Rather, it could do more interesting things:

*   Provide additional information, such as showing a list of all already-cached resources, which the user can still browse offline (check how Jake Archibald’s [offline Wikipedia demo](https://wiki-offline.jakearchibald.com/) lists all already-cached resources on its home page).
*   Let the user play a game while waiting for the connection to come back (such as [done by The Guardian](https://www.theguardian.com/info/developer-blog/2015/nov/04/building-an-offline-page-for-theguardiancom)).

With an SPA, we can offer a different approach: We can intercept the offline state, and just display a small “You’re offline” message at the top of the page that the user is currently browsing. This avoids redirection of the user to yet another page, which could impair the flow of the application.

HTML:

<pre><code class="language-markup">&lt;div id="error-msg"&gt;&lt;/div&gt;
</code></pre>

CSS:

<pre><code class="language-css">#error-msg {
	display: none;
	position: fixed;
	top: 0;
	left: 50%;
	width: 300px;
	margin-left: -150px;
	color: #8a6d3b;
	background-color: #fcf8e3;
	border-color: #faebcc;
	text-align: center;
}
</code></pre>

JavaScript:

<div class="break-out">

<pre><code class="language-javascript">function intercept_click() {

	$(document).on('click', 'a[href^="'+WEBSITE_DOMAIN+'"]', function(e) {

		var anchor = $(this);
		var url = anchor.attr('href');

		$.ajax({
			url: url,
			error: function(jqXHR) {

				var msg = 'Oops, there was an error';
				if (jqXHR.status === 0) { // status = 0 =&gt; user is offline

					msg = 'You are offline!';
				}
				else if (jqXHR.status === 404) {

					msg = 'That page doesn\'t exist';
				}

				$('#error-msg').text(msg).css('display', 'block');
			}
		});
	});
}
</code></pre></div>

**Using localStorage to cache data**

Service workers are not the only solution offered by browsers for caching the response's data. An older technology, with even wider support (Internet Explorer and Safari support it), is [localStorage](https://diveintohtml5.info/storage.html). It offers good performance for caching small to medium-sized pieces of information (it can normally cache up to 5 MB of data).

<div class="break-out">

<pre><code class="language-javascript">/* Using Modernizr library */
function intercept_click() {

	$(document).on('click', 'a[href^="'+WEBSITE_DOMAIN+'"]', function(e) {

		var anchor = $(this);
		var url = anchor.attr('href');

		var stored = '';
		if (Modernizr.localstorage) {

			stored = localStorage[url];
		}
		if (stored) {

			// We already have the data!
			process(stored);
		}
		else {

			$.ajax({
				url: url,
				success: function(response){

					// Save the data in the localStorage
					if (Modernizr.localstorage) {
						localStorage[url] = response;
					}

					process(response);
				}
			});
		}
	});
}
</code></pre></div>

**Making things prettier**

To force the service worker to employ the “network first” strategy, we can add an extra parameter, `sw-networkfirst=true`, to the requested URL. However, adding this parameter in the actual link would look ugly (details of technical implementation should be hidden from the user, as much as possible).

Instead, a data attribute, `data-sw-networkfirst`, could be added in the anchor. Then, on runtime, the click by the user would be intercepted to be handled by an AJAX call, checking whether the link clicked has this data attribute; if it does, only then will the parameter `sw-networkfirst=true` be added to the URL to fetch:

<div class="break-out">

<pre><code class="language-javascript">function intercept_click() {

	$(document).on('click', 'a[href^="'+WEBSITE_DOMAIN+'"]', function(e) {

		var anchor = $(this);
		var url = anchor.attr('href');

		if (anchor.data('sw-networkfirst')) {

			url = add_query_arg('sw-networkfirst', 'true', url);
		}

		$.ajax({
			url: url,
			…
		});
	});
}
</code></pre></div>

**Planning for things that do not work**

Not everything will work offline. For instance, a CAPTCHA will not work because it needs to synchronize its value with the server. If a form has a CAPTCHA, then attempting to submit the form while offline should not save the value locally, to be sent once the Internet connection comes back. Instead, it could fill the form once again with all values previously filled by the user, request the user to input the CAPTCHA, and only then submit the form.</p>

## Conclusion

We've seen how service workers can be implemented for a WordPress website with an SPA architecture. SPAs greatly enhance service workers, such as enabling you to choose from different appshells to load during runtime. Integrating with WordPress is not all that smooth, at least to make the website become offline first, because we need to find all resources from the theme and all of the plugins to add to the precache list. However lengthy, though, the integration is worth doing: The website will load faster and will work offline.

{{< signature "mc, vf, al, il" >}}

