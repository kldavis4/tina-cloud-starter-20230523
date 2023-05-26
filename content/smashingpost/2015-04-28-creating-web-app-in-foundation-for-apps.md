---
title: Creating A Complete Web App In Foundation For Apps
slug: creating-web-app-in-foundation-for-apps
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9e026a22-b7a9-474a-8e07-93e65c7256d1/excerpt-starwars.png
date: 2015-04-28T17:00:55.000Z
author: stephensaucier
description: >-
  Foundation for Apps is a new single-page app framework from Zurb that is closely related to _Foundation 5_ (also known as Foundation for Sites, a widely used front-end framework). It’s built around AngularJS and a Flexbox grid framework.
categories:
  - Coding
  - Frameworks
  - Apps
  - Angular
---
Foundation for Apps is a new [single-page app](https://en.wikipedia.org/wiki/Single-page_application) framework from Zurb that is closely related to _Foundation 5_ (also known as Foundation for Sites, a widely used front-end framework). It’s built around AngularJS and a flexbox grid framework. It’s intended to make creating a web app very quick and simple, enabling us to quickly start writing the code that’s unique to our application, rather than boilerplate.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [A Beginner’s Guide To Progressive Web Apps](https://www.smashingmagazine.com/2016/08/a-beginners-guide-to-progressive-web-apps/)
*   [The Building Blocks Of Progressive Web Apps](https://www.smashingmagazine.com/2016/09/the-building-blocks-of-progressive-web-apps/)
*   [Building A First-Class App That Leverages Your Website](https://www.smashingmagazine.com/2016/02/building-first-class-app-leverages-website-case-study/)

Because Foundation for Apps was only released at the end of 2014, it hasn’t yet seen widespread usage, so there are few good sources of information on using the framework. This article is meant to be a comprehensive guide to building a functional web app with Foundation for Apps from start to finish. The techniques detailed here are fundamental to building practically any kind of app for any client, and this tutorial also serves as a strong introduction to the wider world of AngularJS and single-page apps.

In light of the new film being released later this year, we’ll be building a **Star Wars knowledge base**. It will be a responsive web application, using a [RESTful](https://stackoverflow.com/questions/671118/what-exactly-is-restful-programming) API, caching and many of the features that [Foundation for Apps](https://foundation.zurb.com/apps/) and AngularJS offer.

{{% feature-panel %}}

Prefer to skip to the good stuff?

*   View demo
*   [View on GitHub](https://github.com/spsaucier/ffa_sw)
*   [Download files](https://github.com/spsaucier/ffa_sw/archive/master.zip)

## Getting Started

Take a quick squiz through the [official documentation](https://foundation.zurb.com/apps/docs/#!/), which explains the styling aspects well but doesn’t go into detail about application functionality. Also, keep [AngularJS’ excellent documentation](https://docs.angularjs.org/api) handy, bearing in mind that Foundation for Apps includes some services that aren’t standard and that some AngularJS functions might not work out of the box. Keep in mind also that, natively, AngularJS and Foundation for Apps aren’t particularly well suited to apps that need significant SEO, since most content is loaded via AJAX.

Our app will get its data from the handy Star Wars API found at [SWAPI](https://swapi.co). Take a look through [SWAPI’s documentation](https://swapi.co/documentation) to get a feel for the data served and its structure. Our application will be based on that structure for simplicity.

First, let’s install Foundation for Apps and create our project. Make sure that [Ruby](https://installrails.com/) (already on OS X by default) and [Node.js](https://nodejs.org/) are installed, and then follow the four-step process [detailed in the documentation](https://foundation.zurb.com/apps/docs/#!/installation). It’s pretty straightforward, even if you haven’t used the command line before. Once you’ve finished the process, your browser should display the default home page of your application at `https://localhost:8080/#!/`.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c06a453d-63b3-4cff-ae0c-71cdb3dd753f/01-default-page-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/eae30398-a9dd-46f6-b4eb-9e2d05262acc/01-default-page-opt-small.png" alt="Foundation for Apps’ default home page" /></a><figcaption>Foundation for Apps’ default home page (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c06a453d-63b3-4cff-ae0c-71cdb3dd753f/01-default-page-opt.png">View large version</a>)</figcaption></figure>

Let’s get acquainted with the project’s files and folders.

The only file in our app’s base directory that we need to pay attention to is `gulpfile.js`, which gives instructions to the [Gulp process](https://gulpjs.com/) that we’ve already used to start the server for our app. [Gulp is a build system](https://www.smashingmagazine.com/2014/06/11/building-with-gulp/), and it’s very similar to [Grunt](https://gruntjs.com/). Later on, if we want to add some AngularJS modules or plugins, we’ll need to update this Gulp file with references to the JavaScript or CSS files for those modules or plugins.</p>

<p>The <code>client</code> folder is where we’ll find all of the other files we’re concerned with:<p>

<ul>
<li><code>clients/assets/js/app.js</code> is where our controller, directives and custom filters will be for this application;</li>

<li>All of our app’s SCSS can be found in <code>clients/assets/scss</code>, naturally;</li>

<li><code>clients/index.html</code> is the base template for our application;</li>

<li><code>clients/templates/</code> is where we’ll find the template for all of our pages, most of which haven’t been created yet.</li>
</ul>

## Build The Template And Home Screen

<p>Let’s start building! First, modify the <code>index.html</code> page, which doesn’t start out very well optimized for a real application. We’ll add an off-canvas menu for small screens, a button to toggle its opening, and a nice fade effect using classes from Foundation for Apps’ “Motion UI.” You can copy the code from the <a href="https://github.com/spsaucier/ffa_sw/blob/master/client/index.html"><code>index.html</code> file in our repository</a>.</p>

<p>We’ll add some SCSS variables to our <code>_settings.scss</code> file to set our colors, fonts and breakpoints:</p>

<pre><code class="language-scss">
$primary-color: #000;
$secondary-color: #ffe306;
$body-background: $secondary-color;
$breakpoints: (
  small: rem-calc(600),
  medium: rem-calc(900),
  large: rem-calc(1200),
  xlarge: rem-calc(1440),
  xxlarge: rem-calc(1920),
);
$h1-font-size: rem-calc(80);
$body-font-family: "brandon-grotesque", Helvetica, Arial, sans-serif;
$header-font-family: "flood-std", Helvetica, sans-serif;
</code></pre>

<p>Now we’ll trick out <code>app.scss</code> to add a bit of pizzazz. You can use the <a href="https://github.com/spsaucier/ffa_sw/blob/master/client/assets/scss/app.scss">file in the repository</a> as an example.</p>

<p>Let’s quickly overwrite the default <code>home.html</code> file in <code>clients/templates/</code> with a simple menu of links to all of the pages we’ll build:</p>

<pre><code class="language-markup">
---
name: home
url: /
---
&lt;div class="grid-content"&gt;
  &lt;h1&gt;Star Wars Compendium&lt;/h1&gt;
  &lt;p class="lead"&gt;Foundation for Apps using Star Wars API&lt;/p&gt;
  &lt;hr&gt;
  &lt;ul class="home-list"&gt;
    &lt;li&gt;&lt;a ui-sref="films"&gt;Films&lt;/a&gt;&lt;/li&gt;
    &lt;li&gt;&lt;a ui-sref="species"&gt;Species&lt;/a&gt;&lt;/li&gt;
    &lt;li&gt;&lt;a ui-sref="planets"&gt;Planets&lt;/a&gt;&lt;/li&gt;
    &lt;li&gt;&lt;a ui-sref="people"&gt;People&lt;/a&gt;&lt;/li&gt;
    &lt;li&gt;&lt;a ui-sref="starships"&gt;Starships&lt;/a&gt;&lt;/li&gt;
    &lt;li&gt;&lt;a ui-sref="vehicles"&gt;Vehicles&lt;/a&gt;&lt;/li&gt;
  &lt;/ul&gt;
&lt;/div&gt;
</code></pre>

<p>Our template is now looking pretty unique to us now &mdash; no cookie-cutter Foundation at this point:</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/42dc8b3e-8b00-47ae-8990-8fe8d6035870/02-template-in-action-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7fec84a3-8a48-4d3e-975f-a54cca96226d/02-template-in-action-opt-small.png" alt="Home page of application" /></a><figcaption>Our template in action &mdash; it’s got a bit of flavor. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/42dc8b3e-8b00-47ae-8990-8fe8d6035870/02-template-in-action-opt.png">View large version</a>)</figcaption></figure>

## Creating A List Of Films

<p>Now we’re cooking with gas. In our <code>templates</code> folder, create a template file for our first subpage: <code>films.html</code>. Paste this snippet at the top:</p>

<pre><code class="language-markup">
---
name: films
url: /films/:id?p=
controller: FilmsCtrl
---
</code></pre>

<p>This tells our app three things:</p>

<ol>
<li>In links to this page, we’ll refer to the page as <code>films</code></li>
<li>The URL will have two possible parameters: <code>id</code> (the ID of the film, according to our data) and <code>p</code> (the page number in the listing of all films).</li>
<li>We’ll be using our own custom AngularJS controller, called <code>FilmsCtrl</code>, instead of the default blank one that Foundation for Apps creates automatically.</li>
</ol>

<p>Because we’re using our own controller, let’s go ahead and create one in <code>app.js</code>. Look through the controller below, which we’ll be using for both our <strong>list of films</strong> and our <strong>single-film</strong> pages. You can see that this controller keeps track of URL parameters, figures out what page of results we’re on, gets the necessary data (either a list of films or details of an individual film, depending on the URL’s parameters) from our external API, and returns it to our view using the <code>$scope</code> variable. Add it to <code>app.js</code> after the <code>angular.module</code> declaration closes:</p>

<pre><code class="language-javascript">
controller('FilmsCtrl',
  ["$scope", "$state", "$http",function($scope, $state, $http){
  // Grab URL parameters - this is unique to FFA, not standard for
  // AngularJS. Ensure $state is included in your dependencies list
  // in the controller definition above.
  $scope.id = ($state.params.id || ’);
  $scope.page = ($state.params.p || 1);

  // If we're on the first page or page is set to default
  if ($scope.page == 1) {
    if ($scope.id != ’) {
      // We've got a URL parameter, so let's get the single entity's
      // data from our data source
      $http.get("https://swapi.co/api/"+'films'+"/"+$scope.id,
          {cache: true })
        .success(function(data) {
          // If the request succeeds, assign our data to the 'film'
          // variable, passed to our page through $scope
          $scope['film'] = data;
        })

    } else {
      // There is no ID, so we'll show a list of all films.
      // We're on page 1, so the next page is 2.
      $http.get("https://swapi.co/api/"+'films'+"/", { cache: true })
        .success(function(data) {
          $scope['films'] = data;
          if (data['next']) $scope.nextPage = 2;
        });
    }
  } else {
    // Once again, there is no ID, so we'll show a list of all films.
    // If there's a next page, let's add it. Otherwise just add the
    // previous page button.
    $http.get("https://swapi.co/api/"+'films'+"/?page="+$scope.page,
      { cache: true }).success(function(data) {
        $scope['films'] = data;
        if (data['next']) $scope.nextPage = 1*$scope.page + 1;
      });
      $scope.prevPage = 1*$scope.page - 1;
  }
  return $scope;

}])  // Ensure you don't end in a semicolon, because more
     // actions are to follow.
</code></pre>

<p>After saving <code>app.js</code>, you may need to restart your server using the terminal (<code>Control + C</code> to cancel the operation and then <code>foundation-apps watch</code> again) to ensure that your app includes the new template file you’ve created along with the new controller.</p>

<p>And just like that, we have a fully functional controller that <strong>gets data</strong> from an external RESTful API source, <strong>caches the result</strong> in the browser’s session and <strong>returns the data</strong> to our view!</p>

<p>Open up <code>films.html</code> again, and let’s start building the view of the data that we can now access. Begin by adding the base view, which will show a <strong>list of films</strong>. We can access all properties that we’ve added to our <code>$scope</code> variable, without prefixing them with <code>$scope</code>, such as (in this case) <code>films</code>, <code>prevPage</code> and <code>nextPage</code>. Add the following below the template’s existing content:</p>

<pre><code class="language-markup">
&lt;div class="grid-content films" ng-show="films"&gt;
  &lt;a class="button pagination"
    ng-show="prevPage"
    ui-sref="films({ p: prevPage })"&gt;
    Back to Page {{prevPage}}
  &lt;/a&gt;

  &lt;div class="grid-content shrink"&gt;
    &lt;ul class="menu-bar vertical"&gt;
      &lt;li ng-repeat="film in films.results"&gt;
        {{film.title}}
      &lt;/li&gt;
    &lt;/ul&gt;
  &lt;/div&gt;

  &lt;a class="button pagination"
    ng-show="nextPage"
    ui-sref="films({ p: nextPage })"&gt;
    To Page {{nextPage}}
  &lt;/a&gt;
&lt;/div&gt;
</code></pre>

<p>Bodacious! We’ve got a list of film names as well as pagination if there are multiple pages of data. But that’s not especially useful yet &mdash; let’s turn the film’s name into a link to that film’s page in our app.</p>

<p>We plan to use the film’s ID as the <code>id</code> parameter in our URL, and we have access to the film’s <code>url</code> attribute, which happens to have the film’s ID as its last parameter before the final slash. But how do we grab <em>only</em> the ID out of the URL that we have access to? AngularJS makes it easy with custom <a href="https://docs.angularjs.org/api/ng/filter/filter">filters</a>. Let’s wrap our <code>{{film.title}}</code> in a link, add a <code>ui-sref</code> attribute (which sets up an internal link) and use our <code>film.url</code> data with a custom filter applied to it:</p>

<pre><code class="language-markup">
&lt;a ui-sref="films({ id:( film.url | lastdir ), p:’ })"&gt;
  {{film.title | capitalize}}
&lt;/a&gt;
</code></pre>

<p>Well, now our page is broken because our app doesn’t know what the <code>lastdir</code> and <code>capitalize</code> filters are. We need to define those filters in our <code>app.js</code> file, placed just after our controller:</p>

<pre><code class="language-javascript">
.filter('capitalize', function() {
  // Send the results of this manipulating function
  // back to the view.
  return function (input) {
    // If input exists, replace the first letter of
    // each word with its capital equivalent.
    return (!!input) ? input.replace(/([^\W_]+[^\s-]*) */g,
      function(txt){return txt.charAt(0).toUpperCase() +
        txt.substr(1)}) : ’;
  }
})
.filter('lastdir', function () {
  // Send the results of this manipulating function
  // back to the view.
  return function (input) {
    // Simple JavaScript to split and slice like a fine chef.
    return (!!input) ? input.split('/').slice(-2, -1)[0] : ’;
  }
})
</code></pre>

<p>Bingo! We now have a list of films, each of which links to its respective film page.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/67a459a3-01e2-4515-897d-aa4a752c7cd1/03-linked-list-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d04e0806-8542-4ab9-9b66-13f8316a9e07/03-linked-list-opt-small.png" alt="List of films" /></a><figcaption>Our linked list of films: Not sure why we bothered with the prequels. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/67a459a3-01e2-4515-897d-aa4a752c7cd1/03-linked-list-opt.png">View large version</a>)</figcaption></figure>

However, that link just takes us to an empty page at the moment, because <code>films.html</code> hasn’t been set up to show a specific film, rather than the whole list. That’s our next step.</p>

## Displaying Details Of A Single Film

<p>We’ve already set up all of the data we need for the single-film page in our <code>FilmsCtrl</code> controller in the <code>$scope.film</code> variable (which is the same as <code>$scope['film']</code>). So, let’s reuse <code>films.html</code> and add another section that’s visible only when the singular <code>film</code> variable is set. We’ll set each key-value pair to use <code>&lt;dt&gt;</code> and <code>&lt;dd&gt;</code> within a <code>&lt;dl&gt;</code> because we’re not <a href="https://en.wikipedia.org/wiki/Semantic_HTML">unsemantic swine</a>. Remember also that some of <code>film</code>’s fields, such as <code>characters</code>, have multiple values in an array, so we’ll need to use <code>ng-repeat</code> for those to display each value. To link each character to its character page, we’ll use the same method that we used in the listing of films: Using our <code>lastdir</code> filter, we link to each character’s <code>people</code> page by his/her/its ID.</p>

<pre><code class="language-markup">
&lt;div class="grid-content film"
  ng-show="film" ng-init="crawl = 'false'"&gt;
  &lt;h1&gt;Episode {{film.episode_id | uppercase}}: 
    {{film.title}}&lt;/h1&gt;
  &lt;hr&gt;
  &lt;dl&gt;
    &lt;dt&gt;Opening Crawl&lt;/dt&gt;
    &lt;dd ng-class="{'crawl':crawl === true}" 
      ng-click="crawl === true ? crawl = false : crawl = true"&gt;
      {{film.opening_crawl}}&lt;/dd&gt;
    &lt;dt&gt;Director&lt;/dt&gt;
    &lt;dd&gt;{{film.director | capitalize}}&lt;/dd&gt;
    &lt;dt&gt;Producer&lt;/dt&gt;
    &lt;dd&gt;{{film.producer | capitalize}}&lt;/dd&gt;
    &lt;dt&gt;Characters&lt;/dt&gt;
    &lt;dd ng-repeat="character in film.characters"
      ui-sref="people({ id:(character | lastdir), p:’})"&gt;
      {{character}}
    &lt;/dd&gt;
  &lt;/dl&gt;
&lt;/div&gt;
</code></pre>

<p>But look, when we view a film’s entry now, the list of characters shows just a URL relating to the character, rather than the character’s name.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/33a28d53-a552-4853-92c7-04983d0167a4/04-characters-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9e4a0717-1bb6-4aeb-a61b-24e655fb4552/04-characters-opt-small.png" alt="Single film view, characters as URLs" /></a><figcaption>Who are these characters? This will not do. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/33a28d53-a552-4853-92c7-04983d0167a4/04-characters-opt.png">View large version</a>)</figcaption></figure>

We need to replace that text with the character’s name, but we don’t have that critical piece of data. Perhaps we could look up that URL using the same method we used to get our film in the first place &mdash; then, the data we receive from the call would contain the character’s name. Let’s open up <code>app.js</code> again and add a <a href="https://docs.angularjs.org/guide/directive">directive</a>, which we’ll call <code>getProp</code>.</p>

<pre><code class="language-javascript">
.directive("getProp", ['$http', '$filter', function($http, $filter) {
  return {
    // All we're going to display is the scope's property variable.
    template: "{{property}}",
    scope: {
      // Rather than hard-coding 'name' as in 'person.name', we may need
      // to access 'title' in some instances, so we use a variable (prop) instead.
      prop: "=",
      // This is the swapi.co URL that we pass to the directive.
      url: "="
    },
    link: function(scope, element, attrs) {
      // Make our 'capitalize' filter usable here
      var capitalize = $filter('capitalize');
      // Make an http request for the 'url' variable passed to this directive
      $http.get(scope.url, { cache: true }).then(function(result) {
        // Get the 'prop' property of our returned data so we can use it in the template.
        scope.property = capitalize(result.data[scope.prop]);
      }, function(err) {
        // If there's an error, just return 'Unknown'.
        scope.property = "Unknown";
      });
    }
  }
}])
</code></pre>

<p><code>getProp</code> returns a single property from the data resulting from our <code>$http.get</code> call, and we can specify which property we want. To use this directive, we need to add it to the area within our <code>ng-repeat</code>, like so:</p>

<pre><code class="language-markup">
&lt;span get-prop prop="'name'" url="character"&gt;{{character}}&lt;/span&gt;
</code></pre>

<p>Nice. We now have each character’s name instead of just a wild URL, and each links to its respective page. Now our single <code>film</code> view will be complete once the rest of the data fields are added to the view (see <a href="https://github.com/spsaucier/ffa_sw/blob/master/client/templates/films.html"><code>films.html</code> in the repository</a> for the rest).</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ffcf0008-9afc-4fdd-9c2b-fa0394f8e86e/05-characters-fixed-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cec90684-0edd-4ddb-bfd1-6892356b11e0/05-characters-fixed-opt-small.png" alt="Fixed character names" /></a><figcaption>This is much better. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ffcf0008-9afc-4fdd-9c2b-fa0394f8e86e/05-characters-fixed-opt.png">View large version</a>)</figcaption></figure>

## Refactoring Our Code For Reuse

<p>Looking through <a href="https://swapi.co/documentation">SWAPI’s documentation</a> and our plans for the rest of the application, we clearly see that our controllers for all other pages will be extremely similar to this one, varying only in the category of data we’re getting.</p>

<p>With that in mind, let’s move the code inside our <code>films</code> controller to its own function, called <code>genericController</code>, placed just before the last closing brackets of <code>app.js</code>. We also need to replace every instance of the string <code>'films'</code> with the variable <code>multiple</code> (five instances) and <code>'film'</code> with <code>single</code> (one instance), because they represent the multiple and singular forms of the entity of each page. This allows us to create very <a href="https://en.wikipedia.org/wiki/Don%27t_repeat_yourself">DRY</a>, reusable code that’s also easier to read and understand.</p>

<p>Now we can add a call in our <code>FilmsCtrl</code> controller to our new <code>genericController</code> function with our two variables (<code>multiple</code> and <code>single</code> versions of our data), passed as parameters:</p>

<pre><code class="language-javascript">
.controller('FilmsCtrl', function($scope, $state, $http){
  $scope = genericController($scope, $state, $http, 'films', 'film');
})
</code></pre>

<p>Excellent! We have a reusable controller that grabs the data we need for any given page and puts it in a usable format! We can now easily create our other pages’ controllers just after <code>FilmsCtrl</code> in the same way:</p>

<pre><code class="language-javascript">
.controller('SpeciesCtrl', function($scope, $state, $http){
  $scope = genericController($scope, $state, $http, 'species', 'specie');
})
.controller('PlanetsCtrl', function($scope, $state, $http){
  $scope = genericController($scope, $state, $http, 'planets', 'planet');
})
.controller('PeopleCtrl', function($scope, $state, $http){
  $scope = genericController($scope, $state, $http, 'people', 'person');
})
.controller('StarshipsCtrl', function($scope, $state, $http){
  $scope = genericController($scope, $state, $http, 'starships', 'starship');
})
</code></pre>

<p>Go ahead and create the template HTML files for <code>planets</code>, <code>species</code>, <code>people</code>, <code>starships</code> and <code>vehicles</code> in the same way we created <code>films.html</code> but referencing the fields in <a href="https://swapi.co/documentation">SWAPI’s docs</a> for each respective category of data.</p>

<p>Voila! All of our pages now show the correct data and interlink with one another!</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5bffd5cd-6d77-4e43-8281-fd9de1708cd0/06-complete-app-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4dd72bd1-e352-41ee-a353-b1e92588afed/06-complete-app-opt-small.png" alt="Completed application" /></a><figcaption>Our completed application (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5bffd5cd-6d77-4e43-8281-fd9de1708cd0/06-complete-app-opt.png">View large version</a>)</figcaption></figure>

## Final Notes

<p>Our application is complete! Our demo (linked to below) is hosted by <a href="https://www.aerobatic.com/">Aerobatic</a>, which exclusively targets front-end web applications. You’ll see in our repository that we’ve added some domain-specific options to take advantage of Aerobatic’s API gateway, which sets up a proxy that caches the API’s data on the server once we request it. Without caching, the application would be both latency-limited and request-limited (SWAPI allows only so many requests per domain, as do most other APIs), and because our data isn’t likely to change often, that server caching makes everything very speedy after the first load. Because we’ve limited our <code>onload</code> requests and images, even the first load will be acceptable on a slow connection, and on each page load, the header menu will stay on the page, making the application feel fast.</p>

<p>In the demo and repository, you can see that we’ve also added another API call on the details pages, which grabs an image URL for each entity from a Google custom search that we set up to trawl <a href="https://starwars.wikia.com/">Wookieepedia</a> and <a href="https://www.starwars.com/">StarWars.com</a>. So, we’ve now got dynamic, highly relevant images showing up on each detail page.</p>

<p>Take a look at the demo below, or look through the source code for some hidden goodies and more Foundation-specific tricks, or download the repository and build on it locally with your own improvements.</p>

<ul>
<li>Star Wars Compendium, Foundation for Apps demo</li>
<li><a href="https://github.com/spsaucier/ffa_sw">Star Wars Compendium Using Foundation for Apps</a>, GitHub</li>
<li><a href="https://github.com/spsaucier/ffa_sw/archive/master.zip">Download source files</a> (ZIP)</li>
</ul>

{{< signature "ml, al" >}}

