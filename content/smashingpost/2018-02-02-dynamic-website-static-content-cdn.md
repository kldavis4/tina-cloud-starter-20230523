---
title: 'How To Make A Dynamic Website Become Static Through A Content CDN'
slug: dynamic-website-static-content-cdn
author: leonardolosoviz
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/63cdb6a2-15cc-43e9-892c-e76fc57b37f4/jan-17-travel-explore-nocal-preview-opt.jpeg
date: 2018-02-02T14:00:48+01:00
summary: >-
  What if we could have a WordPress website in which its dynamic content could be exported as static files? Leonardo Losoviz explains how you can combine both worlds: switch to a static site generator without having to abandon WordPress.
description: >-
  What if we could have a WordPress website in which its dynamic content could be exported as static files? Leonardo Losoviz explains how you can combine both worlds: switch to a static site generator without having to abandon WordPress.
categories:
  - Performance
  - Service Workers
  - WordPress
---
Smashing Magazine gave us a little surprise recently: Its website has been completely overhauled, switching away from WordPress to Netlify. One of the several reasons for the move is cost: Netlify allows for a static version of a website, which can be hosted directly on a content delivery network (CDN), reducing the number of web servers that are needed. In addition, because CDNs are located near users, accessing the website becomes faster. It is a wise move, indeed.

However, this decision comes with the consequence of leaving the WordPress ecosystem. If your website needs to support AMP or Dropbox or AWS S3 or pretty much anything else, most likely there is a WordPress plugin for that. The WordPress ecosystem, which relies on a huge community of developers, enables us to constantly incorporate new features into our websites with no major effort, or at least with much less effort than is required to develop the functionality from scratch. **Moving from WordPress to Netlify has trade-offs**: speed versus functionality, cost versus community support.

What if it were possible to combine the best of both worlds? That is, what if we could have a WordPress website the dynamic content of which (i.e., content such as blog posts, rather than static assets such as CSS files) could be exported as static files? Currently, there are plugins that export a WordPress website as static HTML files; however, they export the whole website in advance, and they have a limit of up to around 1000 pages, so they would not scale to a website the size of Smashing Magazine. What we need, instead, is to **be able to generate a static version of the website on the fly**, page by page.

In this article, we will tackle this challenge. We will explore how to set up our website’s architecture to route its dynamic content through a CDN, making it static. This way, we will be able to obtain the benefits that Smashing Magazine got from switching to a static site generator, yet without having to abandon WordPress.

{{% feature-panel %}}

## How Does A Content CDN Work?

Routing the request through a CDN makes dynamic content become static since the CDN will return the cached version of that content (requested under a specific URL). Whenever the webserver has a fresher version of that content, it needs to tell the CDN to serve the most up-to-date version. There are two ways to handle this situation:

1. Purging the object from the CDN cache so that it will fetch the content again for that URL;
2. Adding a versioning parameter to the URL in order to serve a different version of the object under a different URL whenever the content changes.

When making a dynamic website in which content is constantly changing and needs to immediately reflect those changes, then the first solution is not adequate. Why? Well, for the following reasons:

- We cannot guarantee that the object will be effectively purged from all the different layers in between the webserver and the client browser. For instance, the user may have a version cached either locally or behind a corporate caching proxy;
- Because CDN edges are located worldwide, it usually takes a few seconds for all locations to purge their objects.

In addition, programmatically purging objects from a CDN depends on the APIs made available by the CDN providers, such as Cloudflare or AWS CloudFront. If we want to have absolute control that the application will work regardless of the infrastructure where it runs, then purging the object is not recommended.

For all of these reasons, I have decided to implement the Content CDN invalidation mechanism through the second solution, that is having the application add a versioning parameter to each requested URL. This versioning parameter, which from now on will be called “thumbprint,” basically is a timestamp from when the requested resource was last modified.

The process is then quite straightforward:

1. The user makes a request (e.g., clicks on a link in the website).
2. The application in the client modifies the URL to be requested, changing the domain to that from a CDN and adding the “thumbprint” (these modifications are hidden to the user).
3. The CDN, if it doesn't have this entry, will pull it from the webserver.
4. The server returns a response.
5. The CDN caches the response and returns it to the client.
6. The client displays the content, and updates the browser URL to the originally requested URL (no domain change, no extra parameters added).
7. The next time a user (any user) makes the same request, if the thumbprint value has not changed, then this content will be directly fetched from the CDN.

This approach does not provide a 100% static website yet: the initial website load is fetched from the webserver, and not from the CDN. A possible fix for this issue is to intercept the first request through Service Workers and apply the procedure above, allowing repeating visitors (browsing the site on Chrome and Firefox, and soon Safari and Edge) to always load the website from a CDN (I still need to implement this solution, so I will not describe it in this article.)

## Implementation Of The Content CDN

As an example, I have implemented the content CDN for [PoP](https://getpop.org), a wrapper for WordPress sites which optimizes their performance and makes them more dynamic.

After loading the initial app shell, PoP loads all content solely through AJAX calls. For this, it intercepts user events (for example, when a user clicks on a link) and modifies the URL being requested, making the web server deliver the response as JSON instead of HTML. We extend this procedure, to make the request also go through a CDN.

### Modifying The URL To Be Requested

Let’s proceed to modify the requested URL. Assuming the URL is `https://getpop.org/en/`, the steps taken are as follows:

1. All requests are intercepted in the browser client, and the extra parameter `output=json` is added to the URL, upon which the server will return a JSON response.  
<pre class="code__inline"><code class="language-markup">https://getpop.org/en/</code><code class="language-markup" style="font-weight: bold;">?output=json</code></pre>
2. We change the domain of the requested resource: Whereas `https://getpop.org` points to the web server, `https://content.getpop.org` points to a CDN that, whenever it doesn't have the requested asset, origin will pull it from `https://getpop.org` and then cache it.  
<pre class="code__inline"><code class="language-markup">https://</code><code class="language-markup" style="font-weight: bold;">content.getpop.org</code>/en/?output=json</pre>
3. We add the application `version` parameter to the URL, so that deploying a new version of the application will invalidate all assets cached in the CDN:  
<pre class="code__inline"><code class="language-markup">https://content.getpop.org/en/?output=json</code><code class="language-markup" style="font-weight: bold;">&amp;version=${APP_VERSION}</code></pre>
4. To be able to obtain the latest version of an originally mutable asset, we need to introduce another parameter to its URL: a “thumbprint” — i.e. a number to indicate the last time it was modified:  
<pre class="code__inline"><code class="language-markup">https://content.getpop.org/en/?output=json&amp;version=${APP_VERSION}</code><code class="language-markup" style="font-weight: bold;">&amp;thumbprint=${LATEST_THUMBPRINT}</code></pre>

And that is what our final requested URL will look like.

### The Thumbprint Makes A Cached Asset Become Dynamic Again

The value of the thumbprint is always changing, reflecting the activity of users on the website. For this reason, the application in the client must be able to access the latest thumbprint value, which will be added as a parameter to all requests. In order to always get the latest thumbprint, a process in the background must always get this value from the server, either every x amount of time (which can also be routed through the CDN, caching the latest thumbprint value for all clients after the first one) or through WebSockets. (PoP currently implements the former approach. I have omitted the implementation code from this article, but it is available in the [GitHub repository](https://github.com/leoloso/PoP).)

To make the implementation less complex, the thumbprint associated with a page does not necessarily have to represent the time at which that specific page was last updated, but rather the time at which any page similar to that one was modified. We can define several thumbprints, each one associated with a different object type:

* **post**  
When has a post been updated or a new one created?

* **user**  
When has a user updated their information or a new user registered?

* **comment**  
When was a new comment added?

* etc.

A page might require one or more of the thumbprint values above. A page showing a post’s content and the name and description of the post’s author will need to rely on both the post and user thumbprints. If the post also contains comments, it will also need to rely on the comment thumbprint. The combination of thumbprints should be defined page by page; this way, we can define a post page to use a combination of post, user, and comment thumbprint values but define an author page to use only the user thumbprint value, maximizing the time that an author page will stay fresh in the CDN cache.

## Code Implementation

All code below has been adapted for this article from its original version, which is available [here](https://github.com/leoloso/PoP/tree/master/wp-content/plugins/pop-cdn-core).

The objective is to convert the URL to be fetched, routing the request through the CDN:

<div class="break-out">

<pre><code class="language-javascript">function fetchURL(url, type) {
  …

  // Route the request through the content CDN. Only for GET requests, POST go straight to the server
  if (type == 'GET') {
    url = contentCDN.convertURL(url);
  }

  // Fetch it
  $.ajax({
    dataType: "json",
    url: url,
    type: type,
    …
  }, …);
}</code></pre></div>

We must implement `function convertURL`, which has been placed under Javascript object `contentCDN`:

<div class="break-out">

<pre><code class="language-javascript">window.contentCDN = {

  convertURL : function(url) {

    // Apply some logic here to transform the URL, to route it through the Content CDN
    ...
  }

};</code></pre></div>

The logic will need to access some configuration values:

* the website’s domain,

* the content CDN’s domain,

* the application version,

* a list of all available thumbprints and the value of each thumbprint,

* the criteria for whether the URL should use the content CDN,

* the criteria for which thumbprints are needed for the URL.

The two sets of criteria are needed to determine whether to route a particular URL through the content CDN and, if allowed, then which thumbprints must be appended to the URL.

When should a URL be rejected? Some pages must not be cached, not only on the CDN but also on the web server, such as those containing user state. For instance, the “My preferences” page, available at `/my-preferences/` for all users, will load content specific to the logged-in user, so it must not be cached. In addition, whenever a `POST` operation is executed, it must go straight to the server.

I have defined four criteria to evaluate the URL, from which we will be able to decide whether the URL must be rejected or which thumbprints to apply to it:

1. `startsWith`  
Does the URL start with a given string? (For example, we would use the post thumbprint for all URLs starting with `/posts/`)

2. `hasParamValues`  
Does the URL contain a given parameter and value? (For example, we would use the user thumbprint for all URLs starting with the parameter `tab=authors`, such as `/posts/this-is-a-post/?tab=authors`, which would generate a list of authors of the post)

3. `noParamValues`  
Does the URL not contain a given parameter and value? (For example, we could use the post thumbprint unless the URL has the parameter `tab=followers`)

4. `isHome`  
Is it the home URL? This is an exceptional case, to be evaluated on its own, because we cannot use the `startsWith` item for it

Having defined all configuration properties that will be needed, we place them under a `contentCDNConfig` Javascript object:

<div class="break-out">

<pre><code class="language-javascript">window.contentCDNConfig = {

  cdnDomain: "...",
  homeDomain: "...",
  appVersion: ...,
  thumbprints: [%THUMBPRINT_NAME_1%, %THUMBPRINT_NAME_2%, ...],
  thumbprintValues : {
    %THUMBPRINT_NAME_1%: %THUMBPRINT_VALUE_1%,
    %THUMBPRINT_NAME_2%: %THUMBPRINT_VALUE_2%,
    ...
  },
  criteria: {
    // Criteria to know if the URL must not use the Content CDN
    rejected: {
      startsWith: [...],
      hasParamValues: [...],
      noParamValues: [...],
      isHome: true/false
    },

    // Criteria for obtaining the thumbprints which are needed for a given URL
    thumbprints: {
      %THUMBPRINT_NAME_1%: {
        startsWith: [...],
        hasParamValues: [...],
        noParamValues: [...],
        isHome: true/false
      },
      %THUMBPRINT_NAME_2%: {
        startsWith: [...],
        hasParamValues: [...],
        noParamValues: [...],
        isHome: true/false
      },
      ...
    }
  }
};</code></pre></div>

Now we can proceed to code the logic. The evaluation of the different criteria is done in `function evalCriteria`. Note that `var criterias` is an array of two criteria, which must both be successful; to be successful, each criterion must have at least one successful subitem. Whereas the first criterion has three subitems (`startsWith`, `hasParamValues` and `isHome`), the second one has only one: `noParamValues`. The logic was designed this way so that `noParamValues` can reject a thumbprint set in the first criterion. For example, use the post thumbprint for all URLs starting with `/author/`, unless they have a `tab=followers` parameter. (In PoP, requesting `/author/leo/` will show a list of all posts from the user Leo, so it relies on the post thumbprint. However, requesting `/author/leo/?tab=followers` instead will show the users who follow Leo, so it does not rely on the post thumbprint.)

<div class="break-out">

<pre><code class="language-javascript">(function($){
window.contentCDN = {

  ...

  evalCriteria : function(url, entries) {

    var evalParam = function(elem) {

      // Function getParam gets the value of the query string "key" from the URL. Code can be found here: https://github.com/leoloso/PoP/blob/master/wp-content/plugins/pop-frontendengine/js/utils.js#L91
      var key = elem[0], value = elem[1];
      var paramValue = getParam(key, url);
      return paramValue == value;
    };

    var criterias = [
      {
        // isHome: special case, we can't ask for path pattern, or otherwise its thumbprints will always be true for everything else (since everything has the path of the home)
        isHome: entries.isHome &amp;&amp; this.isHome(url),

        startsWith: entries.startsWith.some(function(path) {

          return url.indexOf(contentCDNConfig.homeDomain + '/' + path) == 0;
        }),

        // Check if the combination of key=>value is present as a param in the URL
        hasParamValues: entries.hasParamValues.some(evalParam)
      },
      {
        // Check that the combination of key=>value is NOT present as a param in the URL
        noParamValues: !entries.noParamValues.some(evalParam)
      }
    ];

    // Check that all criterias were successful
    var successCounter = 0;
    $.each(criterias, function(index, criteria) {

      var successCriteria = Object.keys(criteria).filter(function(criteriaKey) {

        return criteria[criteriaKey];
      });

      if (successCriteria.length) {

        successCounter++;
      }
    });

    return (successCounter == criterias.length);
  },

  isHome : function(url) {

    var path = (url.indexOf('?') > -1) ? url.substr(0, url.indexOf('?')) : url;
    return path == contentCDNConfig.homeDomain || path == contentCDNConfig.homeDomain+'/';
  },
};
})(jQuery);</code></pre></div>

The check for whether the URL should be routed through a CDN is implemented in `function shouldUseCDN`, and obtaining the list of thumbprints to use for the URL is implemented in `function getThumbprints`:

<div class="break-out">

<pre><code class="language-javascript">(function($){
window.contentCDN = {

  ...

  shouldUseCDN : function(url) {

    return url.indexOf(contentCDNConfig.homeDomain) == 0 &amp;&amp; !this.evalCriteria(url, contentCDNConfig.criteria.rejected);
  },

  getThumbprints : function(url) {

    var that = this;  
    var thumbprints = [];
    $.each(contentCDNConfig.thumbprints, function(index, thumbprint) {

      if (that.evalCriteria(url, contentCDNConfig.criteria.thumbprints[thumbprint])) {
        thumbprints.push(thumbprint);
      }
    });

    return thumbprints;
  }
};
})(jQuery);</code></pre></div>

We are pretty much there. We can finally implement `function convertURL`:

<div class="break-out">

<pre><code class="language-javascript">window.contentCDN = {

  convertURL : function(url) {

    if (this.shouldUseCDN(url)) {

      // Important: get the thumbprint now, before replacing the domain, after which the thumbprint values won't be found anymore
      var thumbprint = this.getThumbprintValue(url);

      // Modify the URL, replacing the home domain with the Content CDN domain
      url = contentCDNConfig.cdnDomain + url.substr(contentCDNConfig.homeDomain.length);

      // Add the version parameter to the URL. Code for function add_query_arg can be found here: https://github.com/leoloso/PoP/blob/master/wp-content/plugins/pop-frontendengine/js/utils.js#L31
      url = add_query_arg("version", contentCDNConfig.appVersion, url);

      // Add the thumbprints as params
      if (thumbprint) {

        url = add_query_arg("thumbprint", thumbprint, url);
      }
    }

    return url;
  },

  getThumbprintValue : function(url) {

    var thumbprints = this.getThumbprints(url);
    var value = thumbprints.map(function(thumbprint) {
      return this.thumbprintValues[thumbprint];
    });

    // Join all the thumbprints together using a dot, to make it easier to identify the different thumbprint values
    return value.join('.');
  }
};</code></pre></div>

Next, we proceed to generate the configuration file. The configuration file must be extensible so that WordPress plugins can hook into it and add their own thumbprints and criteria. As such, I will follow the same process I wrote about in my [article on service workers](https://www.smashingmagazine.com/2017/10/service-worker-single-page-application-wordpress-sites/), generating it on runtime and executing the logic upon deployment of a new version of the website. (The whole process is explained in that article, so I will not repeat it here.)

Putting everything together, the placeholder file from which to generate the Javascript configuration file on runtime looks like this:

<pre><code class="language-javascript">window.contentCDNConfig = {
  cdnDomain: $cdnDomain,
  homeDomain: $homeDomain,
  appVersion: $appVersion,
  thumbprints: $thumbprints,
  thumbprintValues: $thumbprintValues,
  criteria: {
    rejected: $rejectedCriteria,
    thumbprints: $thumbprintsCriteria,
  }
};</code></pre>

And we define the WordPress hooks to fill those values, allowing plugins to add their own configuration.

<div class="break-out">

<pre><code class="language-php">class ContentCDN_ThumbprintsConfig {

  ...

  public function get_configuration() {

    $configuration = parent::get_configuration();

    $configuration['$cdnDomain'] = "https://content.getpop.org";
    $configuration['$homeDomain'] = get_site_url();
    $configuration['$appVersion'] = "4.3";

    // Thumbprints are obtained from the Manager instance
    global $contentcdn_thumbprint_manager;
    $thumbprints = $contentcdn_thumbprint_manager->get_thumbprints();
    $configuration['$thumbprints'] = $thumbprints;
    $configuration['$thumbprintValues'] = $thumbprint_values;
    $configuration['$rejectedCriteria'] = $this->get_rejected_criteriaitems();
    $configuration['$thumbprintsCriteria'] = array();
    foreach ($thumbprints as $thumbprint) {

      $configuration['$thumbprintsCriteria'][$thumbprint] = $this->get_thumbprints_criteriaitems($thumbprint);
    }

    return $configuration;
  }

  protected function get_rejected_criteriaitems() {

    return array(
      'startsWith' => apply_filters(
        'ContentCDN_ThumbprintsConfig:criteriaitems:rejected:startsWith',
        array()
      ),
      // Array of Arrays: elem[0] = URL param, elem[1] = value
      'hasParamValues' => apply_filters(
        'ContentCDN_ThumbprintsConfig:criteriaitems:rejected:hasParamValues',
        array()
      ),
      // Array of Arrays: elem[0] = URL param, elem[1] = value
      'noParamValues' => apply_filters(
        'ContentCDN_ThumbprintsConfig:criteriaitems:rejected:noParamValues',
        array()
      ),
      'isHome' => apply_filters(
        'ContentCDN_ThumbprintsConfig:criteriaitems:rejected:isHome',
        false
      )
    );
  }

  protected function get_thumbprints_criteriaitems($thumbprint) {

    return array(
      'startsWith' => apply_filters(
        'ContentCDN_ThumbprintsConfig:criteriaitems:thumbprint:startsWith',
        array(),
        $thumbprint
      ),
      'hasParamValues' => apply_filters(
        'ContentCDN_ThumbprintsConfig:criteriaitems:thumbprint:hasParamValues',
        array(),
        $thumbprint
      ),
      'noParamValues' => apply_filters(
        'ContentCDN_ThumbprintsConfig:criteriaitems:thumbprint:noParamValues',
        array(),
        $thumbprint
      ),
      'isHome' => apply_filters(
        'ContentCDN_ThumbprintsConfig:criteriaitems:thumbprint:isHome',
        false,
        $thumbprint
      )
    );
  }
}
new ContentCDN_ThumbprintsConfig();</code></pre></div>

To deal with the thumbprints, we are referencing the `$contentcdn_thumbprint_manager` object, which is an instance of `class ContentCDN_Thumbprint_Manager`, which allows plugins to register their own thumbprints simply by extending from the abstract `class ContentCDN_ThumbprintBase`:

<div class="break-out">

<pre><code class="language-php">class ContentCDN_ThumbprintBase {

  function __construct() {

    global $contentcdn_thumbprint_manager;
    $contentcdn_thumbprint_manager->add($this);
  }

  public function get_name() {

    return '';
  }

  public function get_query() {

    return array();
  }

  public function execute_query($query) {

    return '';
  }

  public function get_timestamp($object_id) {

    return (int) 0;
  }
}

class ContentCDN_Thumbprint_Manager {

  var $thumbprints;

  function __construct() {

    $this->thumbprints = array();
  }

  function add($thumbprint) {

    $this->thumbprints[$thumbprint->get_name()] = $thumbprint;  
  }

  function get_thumbprints() {

    return array_keys($this->thumbprints);
  }

  function get_thumbprint_value($name) {

    $thumbprint = $this->thumbprints[$name];
    $query = $thumbprint->get_query();

    // Get the ID for the last modified object
    if ($results = $thumbprint->execute_query($query)) {

      $object_id = $results[0];

      // The thumbprint is the modification date timestamp
      return (int) $thumbprint->get_timestamp($object_id);
    }

    return '';
  }
}
global $contentcdn_thumbprint_manager;
$contentcdn_thumbprint_manager = new ContentCDN_Thumbprint_Manager();</code></pre></div>

We proceed to register the default thumbprints. Please note that for both the post and comment thumbprints, the latest timestamp can be directly queried from the database. However, for the user thumbprint, we do not have this information, so we must explicitly save the latest timestamp from when the user updated their profile, under the `meta_key` named `last_edited`.

<div class="break-out">

<pre><code class="language-php">/* Post Thumbprint */
class ContentCDN_Thumbprint_Post extends ContentCDN_ThumbprintBase {

  public function get_name() {

    return 'post';
  }

  public function get_query() {

    return array(
      'fields' => 'ids',
      'limit' => 1,
      'orderby' => 'modified',
      'order' => 'DESC',
      'post_status' => 'publish',
    );
  }

  public function execute_query($query) {

    return get_posts($query);
  }

  public function get_timestamp($post_id) {

    $post = get_post($post_id);
    return mysql2date('U', $post->post_modified);
  }
}
new ContentCDN_Thumbprint_Post();

/* Comment Thumbprint */
class ContentCDN_Thumbprint_Comment extends ContentCDN_ThumbprintBase {

  public function get_name() {

    return 'comment';
  }

  public function get_query() {

    return array(
      'fields' => 'ids',
      'number' => 1,
      'status' => 'approve',
      'type' => 'comment', // Only comments, no trackbacks or pingbacks
      'order' =>  'DESC',
      'orderby' => 'comment_date_gmt',
    );
  }

  public function execute_query($query) {

    return get_comments($query);
  }

  public function get_timestamp($comment_id) {

    return get_comment_date('U', $comment_id);
  }
}
new ContentCDN_Thumbprint_Comment();

/* User Thumbprint */
class ContentCDN_Thumbprint_User extends ContentCDN_ThumbprintBase {

  public function get_name() {

    return 'user';
  }

  public function get_query() {

    return array(
      'fields' => 'ID',
      'limit' => 1,
      'orderby' => 'meta_value',
      'meta_key' => 'last_edited',
      'order' => 'DESC',
    );
  }

  public function execute_query($query) {

    return get_users($query);
  }

  public function get_timestamp($user_id) {

    return get_user_meta($user_id, 'last_edited', true);
  }
}
new ContentCDN_Thumbprint_User();

add_action('edit_user_created_user', 'save_extra_user_info');
add_action('personal_options_update', 'save_extra_user_info');
add_action('edit_user_profile_update', 'save_extra_user_info');
function save_extra_user_info($user_id) {

  update_user_meta($user_id, 'last_edited', current_time('timestamp'));
}</code></pre></div>

Plugins may add their own thumbprints. In this case, integration with the [Events Manager](https://wordpress.org/plugins/events-manager/) plugin adds an instance of a location thumbprint:

<div class="break-out">

<pre><code class="language-php">class EM_ContentCDN_Thumbprint_Location extends ContentCDN_Thumbprint_Post {

  public function get_name() {

    return 'location';
  }

  public function get_query() {

    return array_merge(
      parent::get_query(),
      array(
        'post_type' => array(EM_POST_TYPE_LOCATION),
      )
    );
  }
}
new EM_ContentCDN_Thumbprint_Location();</code></pre></div>

Next, we proceed to hook the values to the configuration. First, which URL patterns will be rejected from the use of the content CDN? (For example, we must hook in the list of IDs from all pages that require user state, such as `/my-preferences/` and `/edit-post/` and that, as such, cannot be cached.)

<div class="break-out">

<pre><code class="language-php">function get_page_path($page_id) {

  $page_path = substr(get_permalink($page_id), strlen(home_url()));

  // Remove the first and last '/'
  return trim($page_path, '/');
}

class ContentCDN_RejectedPageHooks {

  function __construct() {

    add_filter(
      'ContentCDN_ThumbprintsConfig:criteriaitems:rejected:startsWith',
      array($this, 'get_rejected_paths')
    );
  }

  function get_rejected_paths($rejected) {

    // Variable $user_state_pages is a list of ids from all pages which require user state, and as such cannot be cached
    // Eg: /my-preferences/, /edit-profile/, '/edit-post/', etc
    $user_state_pages = apply_filters('user_state_pages', array());

    // Exclude all pages with user state
    foreach ($user_state_pages as $page) {

      $rejected[] = trailingslashit(get_page_path($page));
    }

    return $rejected;
  }
}
new ContentCDN_RejectedPageHooks();</code></pre></div>

Plugins can also hook in to reject URLs. In this case, our integration with the [Public Post Preview](https://wordpress.org/plugins/public-post-preview/) plugin defines that, whenever a URL has a parameter of `preview=1` (which is needed to preview an unpublished post), we’ll go straight to the server:

<div class="break-out">

<pre><code class="language-php">class ContentCDN_PPP_RejectedURLHooks {

  function __construct() {

    add_filter(
      'ContentCDN_ThumbprintsConfig:criteriaitems:rejected:hasParamValues',
      array($this, 'get_rejected_paramvalues')
    );
  }

  function get_rejected_paramvalues($paramvalues) {

    // Reject the CDN if viewing a preview post
    $paramvalues[] = array(
      'preview',
      1
    );

    return $paramvalues;
  }
}
new ContentCDN_PPP_RejectedURLHooks();</code></pre></div>

Let’s define which thumbprints to use, based on the URL pattern. Note that, as mentioned, authors will use the user and post thumbprints, unless the URL has a parameter of `tab=followers`, in which case it will only use the user thumbprint. Also, the post thumbprint will be used when the URL starts with `/posts/`; however, if `tab=comments` is present in the URL, then the comment thumbprint will also be used. (In PoP, requesting `/posts/this-is-the-post-slug/` will show the post’s content, but requesting `/posts/this-is-the-post-slug/?tab=comments` will show the post’s comments instead.)

<div class="break-out">

<pre><code class="language-php">class ContentCDN_ThumbprintHooks {

  function __construct() {

    add_filter(
      'ContentCDN_ThumbprintsConfig:criteriaitems:thumbprint:isHome',
      array($this, 'get_thumbprint_ishome'),
      10,
      2
    );
    add_filter(
      'ContentCDN_ThumbprintsConfig:criteriaitems:thumbprint:startsWith',
      array($this, 'get_thumbprint_authorpaths'),
      10,
      2
    );
    add_filter(
      'ContentCDN_ThumbprintsConfig:criteriaitems:thumbprint:noParamValues',
      array($this, 'get_thumbprint_postnoparamvalues'),
      10,
      2
    );
    add_filter(
      'ContentCDN_ThumbprintsConfig:criteriaitems:thumbprint:startsWith',
      array($this, 'get_thumbprint_postpaths'),
      10,
      2
    );
    add_filter(
      'ContentCDN_ThumbprintsConfig:criteriaitems:thumbprint:hasParamValues',
      array($this, 'get_thumbprint_commentparamvalues'),
      10,
      2
    );
  }

  function get_thumbprint_ishome($ishome, $thumbprint) {

    // Home needs POST and USER thumbprints
    $home_thumbprints = array(
      'user',
      'post',
    );
    if (in_array($thumbprint, $home_thumbprints)) {

      return true;
    }

    return $ishome;
  }

  function get_thumbprint_authorpaths($paths, $thumbprint) {

    // The author page displays the user information + user posts. So simply add the partial path for the author URL slug prefix, eg: 'author/', to catch all URLs for the authors, such as getpop.org/en/author/leo/
    $author_thumbprints = array(
      'user',
      'post',
    );
    if (in_array($thumbprint, $author_thumbprints)) {

      global $wp_rewrite;
      $paths[] = $wp_rewrite->author_base.'/'; // This will produce "author/"
    }

    return $paths;
  }

  function get_thumbprint_postnoparamvalues($noparamvalues, $thumbprint) {

    if ($thumbprint == 'post') {

      // Array of: elem[0] = URL param, elem[1] = value
      $noparamvalues[] = array(
        'tab',
        'followers'
      );
      $noparamvalues[] = array(
        'tab',
        'following'
      );
    }

    return $noparamvalues;
  }

  function get_thumbprint_postpaths($paths, $thumbprint) {

    // Posts displays the post content and the post authors’ information. Because they are placed under category "Posts", whose slug is "posts", then they will all have posts/ initially in their URL.
    $posts_thumbprints = array(
      'user',
      'post',
    );
    if (in_array($thumbprint, $posts_thumbprints)) {

      $paths[] = 'posts/';
    }

    return $paths;
  }

  function get_thumbprint_commentparamvalues($paramvalues, $thumbprint) {

    $pages = array();
    if ($thumbprint == 'comment') {

      $paramvalues[] = array(
        'tab',
        'comments'
      );
    }

    return $paramvalues;
  }
}
new ContentCDN_ThumbprintHooks();</code></pre></div>

As mentioned, the Events Manager plugin created a locations thumbprint, which must be used when viewing the `/locations/` page, which displays a list of all event locations:

<div class="break-out">

<pre><code class="language-php">class EM_ContentCDN_LocationThumbprintHooks {

  function __construct() {

    add_filter(
      'ContentCDN_ThumbprintsConfig:criteriaitems:thumbprint:startsWith',
      array($this, 'get_thumbprint_paths'),
      10,
      2
    );
  }

  function get_thumbprint_paths($paths, $thumbprint) {

    if ($thumbprint == 'location') {

      $paths[] = 'locations/';
    }

    return $paths;
  }
}
new EM_ContentCDN_LocationThumbprintHooks();</code></pre></div>

We can now generate the configuration file. As explained in my previous [article on service workers](https://www.smashingmagazine.com/2017/10/service-worker-single-page-application-wordpress-sites/), this file will be generated when deploying a new version of the website, by invoking an internal page, `/generate-contentcdn-configfile/`, which executes the logic to generate the configuration file. (You can view an example of a [generated configuration file from PoP](https://s3.amazonaws.com/trnsfrbckt/smashing-articles/content-cdn/cdn-config.js).) It will look like this:

<div class="break-out">

<pre><code class="language-javascript">window.contentCDNConfig = {
  cdnDomain: "https://content.getpop.org",
  homeDomain: "https://getpop.org",
  appVersion: 4.3,
  thumbprints: ["post", "user", "comment", "location"],
  thumbprintValues : {
    post: 1492681259,
    user: 1491829696,
    comment: 1487996106,
    location: 1490356354
  },
  criteria: {
    rejected: {
      "startsWith":["my-preferences/","my-posts/","edit-profile/","edit-post/","follow/","unfollow/","recommend/","unrecommend/"],
      "hasParamValues":[["preview",1]],
      "noParamValues":[],
      "isHome":false
    },
    thumbprints: {
      "post":{
        "startsWith":["author/","posts/"],
        "hasParamValues":[],
        "noParamValues":[["tab","followers"], ["tab","following"]],
        "isHome":true
      },
      "user":{
        "startsWith":["author/","posts/"],
        "hasParamValues":[],
        "noParamValues":[],
        "isHome":true
      },
      "comment":{
        "startsWith":[],
        "hasParamValues":[["tab","comments"]],
        "noParamValues":[],
        "isHome":false
      },
      "location":{
        "startsWith":["locations/"],
        "hasParamValues":[],
        "noParamValues":[],
        "isHome":false
      }
    }
  }
};</code></pre></div>

There is only one thing left to add: a CORS configuration. Because the website under `https://getpop.org` will be accessing content from `https://content.getpop.org`, access to this domain must be explicitly granted in `.htaccess`:

<div class="break-out">

<pre><code class="language-bash">&lt;IfModule mod_headers.c&gt;
  SetEnvIf Origin "http(s)?://(.+\.)?(getpop.org|content.getpop.org)$" AccessControlAllowOrigin=$0
  Header add Access-Control-Allow-Origin %{AccessControlAllowOrigin}e env=AccessControlAllowOrigin
  Header add Access-Control-Allow-Methods GET
&lt;/IfModule&gt;</code></pre></div>

## Integration With Service Workers

If the website has service workers, to provide offline browsing capabilities, then the content CDN must also be integrated in the corresponding `service-worker.js` file. The integration below follows the implementation for PoP, described in my previous [article on service workers](https://www.smashingmagazine.com/2017/10/service-worker-single-page-application-wordpress-sites/).

Integration is needed due to the ever-changing nature of the value of the thumbprint parameter added to the URL. Let's imagine the following scenario:

1. The current thumbprint value of the latest post is `%THUMBPRINT_VALUE_1%`.

2. The user loads “First Post,” under the URL `/posts/first-post/`. The requested URL would be `/posts/first-post/?thumbnail=%THUMBPRINT_VALUE_1%`.

3. The service worker checks whether it has this content in its cache. Assuming it doesn’t, it dispatches the request to the network.

4. After the content is fetched from the server, the service worker caches the response, under the URL `/posts/first-post/?thumbnail=%THUMBPRINT_VALUE_1%`.

5. The user creates another post, “Second Post.” This will update the latest post’s thumbprint value to `%THUMBPRINT_VALUE_2%`.

6. The user loads “First Post” again, under the URL `/posts/first-post/`. The requested URL would be `/posts/first-post/?thumbnail=%THUMBPRINT_VALUE_2%`.

7. The service worker checks whether it has this content in its cache. Even though it does have it, because it cached it the first time the post was loaded, it would not find it because the URL has changed.

So, what is needed for the service workers is to associate the URLs `/posts/first-post/?thumbnail=%THUMBPRINT_VALUE_1%` and `/posts/first-post/?thumbnail=%THUMBPRINT_VALUE_2%`, so that if an entry is cached under the former URL, then a request for the latter URL would also hit the cache.

The solution I’ve implemented is to keep an index in IndexedDB (done using the powerful [localForage](https://github.com/localForage/localForage) API), with each entry representing a pair of the original URL mapped to the content CDN’s URL. These entries map the content CDN’s URL under which the content was cached with its original URL. Doing this allows different content CDN URLs to be treated as aliases, but producing the same original URL. (For example, both `https://content.getpop.org/posts/first-post/?thumbnail=%THUMBPRINT_VALUE_1%` and `https://content.getpop.org/posts/first-post/?thumbnail=%THUMBPRINT_VALUE_2%` produce the same original URL: `https://getpop.org/posts/first-post/`.) Thus, if there is a miss when checking for the cache for a given URL, we can still check for a hit on its alias, if it exists.

To accomplish this, we modify the original `sw-template.js` file, from which we will generate the `service-workers.js` file. We add `function getOriginalURL`, which will do exactly the opposite of `function convertURL` that was implemented before: Given a URL that is routed through the content CDN, obtain the URL it originated from.

First, we add the extra configuration needed in the `config` object: the CDN and home domains, as well as which parameters were added when first converting the URL:

<pre><code class="language-javascript">var config = {
  ...
  contentCDN: {
    params: $contentCDNParams,
    domains: {
      cdn: $contentCDNDomain,
      original: $contentCDNOriginalDomain
    }
  }
};</code></pre>

We hook in the configuration values:

<div class="break-out">

<pre><code class="language-php">function get_sw_configuration($configuration) {

  ...
  $configuration['$contentCDNOriginalDomain'] = get_site_url();
  $configuration['$contentCDNDomain'] = "https://content.getpop.org";
  $configuration['$contentCDNParams'] = array(
    "version",
    "thumbprint"
  );

  return $configuration;
}</code></pre></div>

And we implement the logic:

<div class="break-out">

<pre><code class="language-javascript">function getOriginalURL(url, opts) {

  // If the current URL is pointing to the Content CDN
  if (opts.contentCDN.domains.cdn &amp;&amp; url.substr(0, opts.contentCDN.domains.cdn.length) == opts.contentCDN.domains.cdn) {

    // Replace the domain, from the CDN one to the original one
    url = opts.contentCDN.domains.original + url.substr(opts.contentCDN.domains.cdn.length);

    // Remove the unneeded parameters, eg: version, thumbprint
    url = stripIgnoredUrlParameters(url, opts.contentCDN.params);
  }

  return url;
}</code></pre></div>

We modify `function addToCache` to set the URL alias index in IndexedDB:

<div class="break-out">

<pre><code class="language-javascript">function addToCache(cacheKey, request, response, opts) {

  if (response.ok) {

    // Add to the cache
    var copy = response.clone();
    caches.open(cacheKey).then( cache => {
      cache.put(request, copy);
    });

    // Save an entry on IndexedDB for the alias URL to point to this request
    var original = getOriginalURL(request.url, opts);
    if (original != request.url) {

      // Set the new request on that position
      localforage.setItem('Alias-'+original, request.url);
    }
  }
  return response;
}</code></pre></div>

In `function onFetch`, we can now modify the “cache falling back to network” and “cache then network” strategies, so that if there is a miss for the URL, we check for a hit under the alias URL:

<div class="break-out">

<pre><code class="language-javascript">function onFetch(event, opts) {

  ...

  if (strategy === SW_STRATEGIES_CACHEFIRST || strategy === SW_STRATEGIES_CACHEFIRSTTHENREFRESH) {

    /* Load immediately from the Cache */
    event.respondWith(
    fetchFromCache(request)
      // Modification here
      .catch(() => localforage.getItem('Alias-'+getOriginalURL(request.url, opts)).then(alternateRequestURL => fetchFromCache(new Request(alternateRequestURL))))
      .catch(() => fetch(request, fetchOpts))
      .then(response => addToCache(cacheKey, request, response, opts))
    );

    ...
  }

  ...
}</code></pre></div>

We must also modify `function refresh` to save the ETag entry under the original URL, allowing different content CDN URLs belonging to the same page to share their ETag values. This way, if a page was first cached under a URL and an updated version was loaded under a different URL, we are still able to notify the user of the update.

<div class="break-out">

<pre><code class="language-javascript">function refresh(request, response, opts) {

  var ETag = response.headers.get('ETag');
  if (!ETag) {
    return null;
  }

  // Modification here
  var key = 'ETag-'+getOriginalURL(request.url, opts);
  return localforage.getItem(key).then(function(previousETag) {

    // Compare the ETag of the response, with the previous one, saved in the IndexedDB
    if (ETag == previousETag) {
      return null;
    }

    // Save the new value
    return localforage.setItem(key, ETag).then(function() {

      // If there was no previous ETag, then send no notification to the user
      if (!previousETag) {
        return null;
      }

      // Send a message to the client
      ...
    });
  });
}</code></pre></div>

Finally, we need to update the CORS configuration in the `.htaccess` file. Because `service-workers.js` lives under the domain `https://getpop.org` but the content is fetched from `https://content.getpop.org`, we must allow for cross-domain access to the `ETag` header:

<div class="break-out">

<pre><code class="language-bash">&lt;IfModule mod_headers.c&gt;
  # Integration between content CDN and service workers: Allow service-worker.js running in getpop.org to read the ETag and Access-Control-Allow-Origin headers coming from content.getpop.org
  Header add Access-Control-Allow-Headers ETag
  Header add Access-Control-Expose-Headers ETag
&lt;/IfModule&gt;</code></pre></div>

### Integration With Offline First

In my previous article on service workers, I explained how to implement [offline first](https://offlinefirst.org/), in order to make the website browsable even when the user has no Internet connection. The implementation I offered relies on using the “[cache then network](https://jakearchibald.com/2014/offline-cookbook/#cache-then-network)” caching strategy, in which content is served immediately from the service worker’s cache whenever available, and a network request is simultaneously sent to check whether the content has been updated, in which case a notification is shown to the user to refresh the page. Unluckily, the network request might be handled by the browser's HTTP cache, thus never reaching the server. To avoid this, we must [add a parameter](https://developers.google.com/web/showcase/2015/service-workers-iowa#cache-bust_your_precaching_requests) `sw-cachebust` with a timestamp value to the URL.

However, if we add the parameter `sw-cachebust` to the URL with an ever-changing value, then this request will never be cached in the CDN. Hence, we need to remove this parameter from the URL on the CDN before looking up to see whether it is cached.

Because the PoP website is hosted on Amazon Web Services (AWS), I have implemented a solution to this problem for its CDN service, CloudFront, using Lambda@Edge:

Here is the Node.js function, set up in Lambda@Edge and triggered by CloudFront as a viewer-request event, to remove the parameter `sw-cachebust` from the URI:

<div class="break-out">

<pre><code class="language-javascript">var stripIgnoredUrlParameters = function(queryString, stripParams) {

  // Copied from https://developers.google.com/web/showcase/2015/service-workers-iowa
  return queryString
    .split('&amp;')
    .map(function(kv) {
      return kv.split('=');
    })
    .filter(function(kv) {
      return stripParams.every(function(param) {
        return param != kv[0];
      });
    })
    .map(function(kv) {
      return kv.join('=');
    })
    .join('&amp;');
}

exports.handler = function(event, context, callback) {

  var request = event.Records[0].cf.request;

  // Remove parameter 'sw-cachebust' from the request, which was generated using Date.now(),
  // only to avoid the Browser Cache and make sure to hit the network in the service workers
  request.querystring = stripIgnoredUrlParameters(request.querystring, ["sw-cachebust"]);

  callback(null , event.Records[0].cf.request);
}</code></pre></div>

*Node.js function, set up in Lambda@Edge, and triggered by CloudFront as a viewer-request event, to remove parameter "sw-cachebust" from the URI.*

## Testing

We are all set! It's time to test the application.

To check whether the process works as intended, simply open Chrome’s Developer Tools, go to the “Network” tab, and inspect the actual requested URL from clicking on any link:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/529ebfb8-3b57-409e-ad0d-d51832021749/contentcdn-networktab-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d6aba20a-70d8-4f67-ba79-1dcbef18addd/contentcdn-networktab-800w-opt.png" width="800" height="549" alt="Inspecting the Network tab after clicking on a link from PoP" /></a><figcaption>Inspecting the Network tab after clicking on a link from <a href="https://getpop.org">PoP</a>. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/529ebfb8-3b57-409e-ad0d-d51832021749/contentcdn-networktab-large-opt.png">View large version</a>)</figcaption></figure>

In the example shown above, from clicking on the link `https://getpop.org/en/implement/`, the requested URL is:

[https://content.getpop.org/en/implement/?target=main&module=settingsdata&output=json&v=0.237&theme=wassup&thememode=simple&themestyle=swift&tp=1491907905](https://content.getpop.org/en/implement/?target=main&module=settingsdata&output=json&v=0.237&theme=wassup&thememode=simple&themestyle=swift&tp=1491907905)

The URL has been converted properly to be routed through the CDN (the parameter `v` is “version” and `tp` is “thumbprint”). We can make sure it is indeed coming from the CDN by inspecting its headers:

<pre><code class="language-markup">curl -I "https://content.getpop.org/en/implement/?target=main&amp;module=settingsdata&amp;output=json&amp;v=0.237&amp;theme=wassup&amp;thememode=simple&amp;themestyle=swift&amp;tp=1491907905"</code></pre>

From it, we obtain:

<pre><code class="language-markup">X-Cache: Hit from cloudfront</code></pre>

This shows that the request has been cached by the CDN (in this case, AWS CloudFront). Success!

## Conclusion

The technique explained in this article enables you to route most of the content from a WordPress website through a CDN, thus reducing hosting costs and making the website faster. We get the best of a static website without having to abandon WordPress. Mission accomplished!

{{< signature "rb, ra, al, yk, il" >}}

