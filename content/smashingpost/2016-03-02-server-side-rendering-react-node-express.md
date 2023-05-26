---
title: React Server Side Rendering With Node And Express
slug: server-side-rendering-react-node-express
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f4fe2114-e166-434d-b620-2af14ea52152/11-app-detailed-bill-preview-opt.png
date: 2016-03-02T17:52:26.000Z
author: dmitrynutels
description: >-
  **Web applications** are everywhere. There is no official definition, but
  we’ve made the distinction: _web applications_ are highly interactive, dynamic
  and performant, while _websites_ are informational and less transient. This
  very rough categorization provides us with a starting point, from which to
  apply development and design patterns.
categories:
  - Coding
  - Apps
  - Node.js
  - React
---
<strong>Web applications</strong> are everywhere. There is no official definition, but we’ve made the distinction: <em>web applications</em> are highly interactive, dynamic and performant, while <em>websites</em> are informational and less transient. This very rough categorization provides us with a starting point, from which to <a href="https://shop.smashingmagazine.com/products/pre-release-inclusive-design-patterns-by-heydon-pickering">apply development and design patterns</a>.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/96492f0e-3dbd-4778-9d69-d94718779fdb/07-server-side-rendering-2-opt.png" alt="React Server Side Rendering" title="React Server Side Rendering With Node And Express" width="743" height="364" loading="lazy" decoding="async" class="294173" /></figure>

These patterns are often established through a different look at the mainstream techniques, a paradigm shift, convergence with an external concept, or just a better implementation. Universal web applications are one such pattern.</p>

## <span class="rh">Further Reading</span> on SmashingMag

*   [How To Scale React Applications](https://www.smashingmagazine.com/2016/09/how-to-scale-react-applications/)
*   [Why You Should Consider React Native For Your Mobile App](https://www.smashingmagazine.com/2016/04/consider-react-native-mobile-app/)
*   [A Detailed Introduction To Webpack](https://www.smashingmagazine.com/2017/02/a-detailed-introduction-to-webpack/)
*   [Notes On Client-Rendered Accessibility](https://www.smashingmagazine.com/2015/05/client-rendered-accessibility/)

{{% feature-panel %}}

Universality, sometimes called <em>"isomorphism"</em>, refers to ability to run nearly the <strong>same code on both client and server</strong> – a concept that was born out of the trials and tribulations in the past of creating applications on the web, availability of new technologies, and the ever-growing complexity of developing and maintaining these applications.

These applications, as well as drawbacks and benefits in their development and maintenance, are the topic of this article. By the end of it we will have discussed:

*   a short history of web applications
*   client-side and server-side rendering
*   universal web applications' structure and implementation

In addition, we will go through a lot of code, <strong>progressively building an application</strong>, or rather a sequence of evolving applications. These applications will attempt to illustrate concepts, problems and decisions made along the way. Enjoy!

## A Little Bit Of History

<blockquote>“Those who don’t know history are destined to repeat it.”</blockquote>

Keeping in mind the cliché above, and before diving into universal web applications, it would suit us well to go over their journey and discuss the challenges and triumphs experienced along the way.</p>

### The Age Of Static Pages

The web, everyone’s favorite medium to find celebrity gossip and cat pictures, was designed as a linked information system. In other words, a web of interconnected hypertext documents, connected via hyperlinks. These documents were identified and located by a URL and retrieved by invoking the only HTTP method in existence: GET. The response, an HTML file, was then rendered in an appropriate application, usually a browser.

There was also Gopher, which I am trying to forget.

The HTTP protocol was created as a request/response protocol for client/server communication. It was the server’s responsibility to supply a resource corresponding to the requested URL; initially, most of the resources were static HTML files or, at best, images.

It was a simpler time.

The introduction of JavaScript in 1995 and Flash a year later, as well as the popularization of DHTML brought in a lot of flair and some functionality to otherwise dull text documents. The interactive web was born in all its <a href="https://www.theworldsworstwebsiteever.com/">blinking glory</a>.

Static pages were relatively simple and quick to develop, easy to deploy and cheap to host; they were equally suitable for complex news sites or a couple of simple pages for beer bottle aficionados (yes, that's a thing, of course). Such simplicity and ubiquity, however, are what possibly became the undoing of the static page – the sea of information became too hard to navigate, identify and sift through. The demand for personalized, dynamic and up-to-date content grew together with the web.

Static pages were going the way of the dodo.

### Everyone Was Server Scripting…

It was now clear that HTML content had to be created dynamically and there was just the tool for it: CGI.

The common gateway interface (CGI) is a standard way for web servers to interact with programs installed on the server’s machine. These programs (scripts, commonly placed under a designated folder called <i>cgi-bin</i>) are executed within the operating system the server is installed on; which is to say they can be written in almost any programming language in existence.

Historically, one of the most prominent places in CGI scripting belongs to Perl, a universal purpose language installed on almost all *nix machines. Perl had been around for almost 10 years at the time the web came a-calling and it was a convenient choice for the first makeshift web developers – they got to use the language and the tools they already knew.

Yes, there was, and still is, Python. And yes, it is funny how many of the opponents of JavaScript being everywhere yearn for the web of old. Which was Perl everywhere.

And so, they set to write more or less sophisticated variations of this:

<pre><code class="language-perl">#!/usr/local/bin/perl
  print "Content-type: text/html\n\n";
  print "&lt;html&gt;\n";
  print "&lt;head&gt;&lt;title&gt;Perl - Hello, world!&lt;/title&gt;&lt;/head&gt;\n";
  print "&lt;body&gt;\n";
  print "&lt;h1&gt;Hello, world!&lt;/h1&gt;\n";
  print "&lt;/body&gt;\n";
  print "&lt;/html&gt;\n";
</code></pre>

I apologize for you having seen it.

While having a lot of positive features, and sometimes being confused with its more glamorous <a href="https://en.wikipedia.org/wiki/Computer-generated_imagery">Hollywood cousin</a>, CGI in its canonical form also suffered from several drawbacks, namely a necessity to invoke a new process for a script when a request needed to be served and to interpret that script. Solutions for these issues exist (e.g. FastCGI and writing scripts in compiled language like C/C++) but are not ideal.

More importantly, Perl was not designed to be a web development-oriented language. This resulted in an awkward experience for the developers, which was somewhat improved by various higher-level abstraction modules, like cgi.pm, but not nearly enough to prevent many of them from searching for greener pastures.</p>

### Server Pages

One of these searches brought in PHP, initially a collection of CGI-related C binaries written to serve the needs of its creator, Rasmus Lerdorf, which evolved into a full-blown language.

Even in its earliest form, PHP allowed you to do something that was to become a common paradigm for most, if not all, similar server pages languages (JSP, for one): it allowed you to write your server-side code directly in the HTML, a marked improvement that allowed for a much better development workflow.</p>

<pre><code class="language-markup">&lt;!DOCTYPE html&gt;
  &lt;html&gt;
  &lt;head&gt;
  &lt;title&gt;PHP - Hello, world!&lt;/title&gt;
  &lt;/head&gt;
  &lt;body&gt;
  &lt;?php echo '&lt;h1&gt;Hello, world!&lt;/h1&gt;'; ?&gt;
  &lt;/body&gt;
  &lt;/html&gt;
</code></pre>

The convenience of this was not lost on developers and, by extension, web server vendors. In addition to the still-existing ability to run PHP as CGI scripts, web servers began to implement various modules that would run PHP code in a container within the web server itself.

This allowed web developers to:

*   write their code in high-level C-like languages
*   use HTML files, sometimes ones that already existed, to enhance the application with dynamic functionality
*   not worry about the minutiae of folders, files, scripts, permissions management, and so on

Throw in improved performance, due to not having to spend time on process/script warm-up, and PHP took the web by storm. By some accounts, during various times and at its peak, PHP was installed and used on nearly 10% of all servers on the web.

JavaServer Pages (JSP), an extension to Java servlets, was one of many to follow. The concept, of course, was very similar: web servers, through servlet container modules, allowed running JSP code within the server itself and provided an extensive set of management capabilities on top of them. JSP, however, had one additional selling point: it brought in the power of Java. Some publications called it “platform to build the Web upon, for serious programmers.” Whether you subscribe to that line of thinking or not, one thing is undeniable: JSP (along with Struts, Spring and other additions to the JEE stack) became the cornerstone of enterprise web applications development.

And there were more. ColdFusion, ASP.NET. Or JSF. The future looked bright for the server pages and their brethren.</p>

### Universal Web Applications?

The technologies and frameworks above are beyond having proved their worth. They are not without issues, though: spreading presentation logic between client and server, session and state management (back button anyone?), higher entry level for both companies and developers due to a more expensive setup and more demanding skill set requirements – all contribute to dynamic server pages not being the ideal solution.

Remember that trite line from before, on history and repeating it? Universal web applications repeat some history <em>after</em> learning from it.

Consider the main concepts:

1.  a common language to use on both client and server: JavaScript
2.  usage of a simple markup language: still HTML
3.  writing directives directly in HTML: any of dozens of template engines like Handlebars
4.  execution of scripts on server machine: Node, Express and a horde of other modules

All of these can be attributed to some past concepts and paradigms, which are now being revisited. Some of it may be due to our accumulated knowledge of how to use them properly. Some because they’ve made the evolutionary leap. And yet more because new tools and techniques allow the experience of using them to be less horrible.

Coincidentally, JavaScript fits all of the above.

There used to be a clear separation line: server pages and mechanisms handle routing, markup and content creation, while JavaScript handles all the silly enhancements to the delivered HTML.

Note: if you never composed your rollover buttons from (at least) two images and inline JavaScript, you haven’t lived.

Lately, improvements in browsers, standardization, tooling and infrastructure – specifically around JavaScript – ushered in a change in its role within the web applications development stack. It is, at this point, a common practice to create markup or content using JavaScript. Moreover, especially with Node inception in 2009, it is now routinely done on the server.

The line is shifting.</p>

## Architectural Concerns

Before we bask in the glory that are universal web applications, while leaving somewhat dusty, mothball-covered server pages behind, it is worthwhile to outline a number of concerns, possible solutions and common misconceptions.

While there are many more items to be taken into consideration when defining application architecture, performance, machine-friendliness and maintenance are to be our main focus.</p>

### Performance

There is no need to argue that performance affects the most important part of any application: the bottom line. Companies like Walmart, Amazon and Google <a href="https://www.globaldots.com/how-website-speed-affects-conversion-rates/">reported</a> clear connections between their revenue and the performance of their sites, and this connection holds true for smaller businesses as well.

Performance <a href="https://www.smashingmagazine.com/2015/09/why-performance-matters-the-perception-of-time/">really</a> <a href="https://www.smashingmagazine.com/2015/11/why-performance-matters-part-2-perception-management/">does</a> <a href="https://www.smashingmagazine.com/2015/12/performance-matters-part-3-tolerance-management/">matter</a>.

I would go even further and say that perceived performance is more important than actual performance.

#### Perceived Performance

Among other things, performance deals with two important aspects: load time and interactivity. Both of these characteristics have objective clock-time (see links above) measures, but in many cases it is the subjective perception of them that matters.

Load time perception (in unofficial terms) measures how much time it takes for user to deem the page usable after interacting with it. Interactivity perception measures the time it takes for users to consider the interaction to be started and finished successfully.

Interactivity perception is usually altered on the UX level by some combination of client-side JavaScript and CSS, and thus lies somewhat outside the scope of this article, but load time perception can and should be affected by the manner in which you render and deliver your markup and content to user.

#### Computing Power

There is a relatively popular sentiment that today’s devices (both mobile and desktop) are powerful enough and have enough free CPU power and RAM to do all the heavy lifting of running a web application in the browser, including HTML construction and rendering. “Unauthorized” distributed computing, if you will.

This, of course, is a lazy approach.

Indeed, mobile devices get more powerful seemingly every day. They also run an ever increasing number of demanding applications, all of which consume RAM, CPU and battery. It is overly optimistic to assume that there is a lot to be had without affecting the usability of these devices.

Also there is an alleged corollary which claims that allowing millions of users to overload servers with HTML creation and rendering is expensive and a wasteful use of hardware. Considering it's a near certainty that most applications do not have millions of users and the fact that Amazon cloud services and the like are relatively cheap these days, that’s a bit of a hypocritical statement.

When you precompile your templates, which is common advice, there should not be any significant difference between this approach and, for example, JSP. In addition, when concerns about JSP performance and scalability arise, they are regularly solved via deployment and topological solutions. Adding more nodes to your cluster is often considered a sound suggestion.

So, add more <em>Nodes</em> to your cluster.

I apologize for that as well.</p>

### Machine Friendliness

We write our applications first and foremost for humans, but it is machines that consume them more and more often.

#### SEO And Machine Semantics

From Googlebot to Facebook crawler, machines consume our applications. Not to click on pretty buttons and navigate amazing menus – to get at our content. They do it for their owners’ benefit, naturally, but concerns like discoverability and search rank allow us, application creators, as well. They aid in exposing our applications to a larger audience, helping our bottom line.

The problem is that despite <a href="https://googlewebmastercentral.blogspot.co.il/2014/05/understanding-web-pages-better.html">Google’s foggy claims</a>, many machines can’t or aren’t willing to run JavaScript, affecting heavily our ability to move markup and content creation to the client. That is, <a href="#computing-power">provided we wanted to</a>.

Aside from being (or not being) able to consume the actual content, machines are also limited in their ability to understand it. Various solutions, including <a href="https://html.spec.whatwg.org/multipage/microdata.html">microdata</a>, JSON-LD and RDFa, were designed to standardize the way in which we can convey the semantic meaning of content to machines. All of these rely on HTML, or JSON-like structures in HTML, to carry the semantics and so, again, limit markup and content creation on the client.

Cue Skynet jokes.

In contrast to the pragmatic content consumers above, assistive technologies, like screen readers, are machines that want to click our buttons and need to navigate our menus, in order to allow humans using them to consume the content in an acceptable manner.

Thankfully, the situation here is better as <a href="https://webaim.org/projects/practitionersurvey/#javascript">this 2014 survey</a> clearly shows that JavaScript is operational on an overwhelming majority of screen reader-enabled browsers. It still can be botched, sure, but not for the lack of ability to execute our excellent JavaScript code.</p>

### Maintenance

Single codebase*. One language. Similar development concepts. One effort!

If you factor in mobile development, a single application may be developed in three to four different ecosystems, which affects a company's ability to maintain and develop web applications, both from technical and staffing standpoints.

Universal web applications, by their very nature, reduce that complexity.

Almost – as there are still things we haven’t transferred into JavaScript, like… I can’t think of one… Eureka! That’s it! CPU-bound computations!

<hr />

## Example Application

Finally!

As I’ve mentioned before, this isn’t a single all-encompassing application, rather a series of smaller ones, that evolve or in some cases mutate, one into another.

This setup, while perhaps less ideal for copy-and-pasting (see GitHub repository links below for that), should allow us to discuss issues and their solutions as they happen.

Working knowledge of React, React Router and ES6 is assumed and required.</p>

### Application Structure

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/563dd66c-0019-46d7-aa5b-cfbfd774ba85/01-app-structure-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3834ef80-caae-4552-a42a-6e239053962e/01-app-structure-preview-opt.png" alt="App Structure" /></a><figcaption>The page transition is conceptual, though. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/563dd66c-0019-46d7-aa5b-cfbfd774ba85/01-app-structure-opt.png">View large version</a>)</figcaption></figure>

We are going to develop a very simple application that has two pages:

1.  list of all latest paid bills
2.  specific bill’s details (added in one of the later versions of the application)

Master–detail at its finest.

It will look, approximately, like this:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/55a440ab-b643-4d01-ae2a-4bc13eb942dd/02-app-latest-bills-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ab8ba479-d14f-4165-813e-b3471f082d20/02-app-latest-bills-preview-opt.png" alt="App Structure" /></a><figcaption>Images are the hardest, really. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/55a440ab-b643-4d01-ae2a-4bc13eb942dd/02-app-latest-bills-opt.png">View large version</a>)</figcaption></figure>

All the examples can be found (separated into branches) in this <a href="https://github.com/zen-js-code/react-universal-web-apps">GitHub repository</a>.</p>

### Technology Stack

I am extremely excited by the latest advancements in tooling and JavaScript's abilities as a language. Sure, not all additions are altogether welcome, but, from a pragmatic standpoint, the easier it is to write the code, the better.

So, the following will be the pillars of the development of our application:

1.  ES6: for all JavaScript code (I am not calling it ES2015, even if they paid me)
2.  Node + Express: as our web server platform
3.  Handlebars: for the server-side templating engine
4.  React, React Router and, less importantly, SCSS as the basis for our application’s presentation layer
5.  Gulp, Webpack for packaging; Babel for ES6 → ES5 transpiling; and BrowserSync for live reload across browsers during development
6.  ESLint for linting

There is a very fine balance to be struck between providing something that can be clearly presented in the format of an article and completeness of a technical solution. In an attempt to walk that line, some interesting items, like Webpack hot module replacement or Handlebars templates precompilation were left out, hopefully without taking anything from our ability to discuss the main topic at hand. Also, where possible, examples where abridged to preserve space. Full code can be found in the repository and its branches.</p>

### Simple, Browser-Only Application

The application is in the same GitHub repository, under the <a href="https://github.com/zen-js-code/react-universal-web-apps/tree/simple">simple branch</a>.

This is where we start our journey toward universality bliss. A simple application (that doesn’t even have the second detailed bill page yet) that is the epitome of client-side rendering. There is no Flux, or Ajax API extraction (that is to come later), just simple React.

#### Setup

This will remain mostly the same through the evolution of our application.

#### Setup, Step 1: Handlebars Configuration

For simplicity's sake, I’ve decided to deliver all HTML content, including pages that are essentially static, by rendering them from Handlebars templates. These pages, of course, can be cached just as well and allow for greater flexibility (and simplify our story too).</p>

<strong><i>config-manager.js</i></strong>

Provides configuration for various Express-level features.</p>

<pre><code class="language-javascript">app.set('views', PATH.resolve(__dirname, ROOT, nconf.get('templateRoot')));

  app.engine('hbs', HBS({
      extname:'hbs',
      defaultLayout:'main.hbs',
      layoutsDir: PATH.resolve(__dirname, ROOT, nconf.get('templateLayouts'))
  }));

  app.set('view engine', 'hbs');
</code></pre>

<a href="https://github.com/indexzero/nconf"><code>noconf</code></a> is a configuration files management mechanism.

#### Setup, Step 2: Page Templates

Main layout:

<strong><i>main.hbs</i></strong>

<pre><code class="language-markup">&lt;!DOCTYPE html&gt;
  &lt;html lang="en"&gt;
  &lt;head&gt;
  &lt;title&gt;App&lt;/title&gt;
  &lt;link rel="stylesheet" href="/assets/css/style.css"&gt;
  &lt;/head&gt;
  &lt;body&gt;
  &lt;/body&gt;
  {{{body}}}
  &lt;script src="//cdnjs.cloudflare.com/ajax/libs/react/0.14.2/react.js"&gt;&lt;/script&gt;
  &lt;script src="//cdnjs.cloudflare.com/ajax/libs/react-router/1.0.0/ReactRouter.js"&gt;&lt;/script&gt;
  &lt;script src="//cdnjs.cloudflare.com/ajax/libs/react/0.14.2/react-dom.js"&gt;&lt;/script&gt;
  &lt;script src="//cdnjs.cloudflare.com/ajax/libs/history/1.12.6/History.js"&gt;&lt;/script&gt;
  &lt;/html&gt;
</code></pre>

and specific page content:

<strong><i>index.hbs</i></strong>

<pre><code class="language-markup">&lt;div data-ui-role="content"&gt;{{{content}}}&lt;/div&gt;
  &lt;script src="/assets/js/app.js" defer&gt;&lt;/script&gt;
</code></pre>

As can be seen, I’ve opted to consume third-party libraries from a CDN, instead of packaging them together with the application (or extracting them into a vendor bundle, using corresponding Webpack configuration). Between faster bundling and clear CDN benefits this made the most sense.

Generally, depending on economics, frequency and character of application updates, the application <i>app.js</i> file referenced in <i>index.hbs</i> above is also a candidate to be put onto CDN, like any other static resource.

#### Application Code

This incarnation of our application, like those to follow, uses React and React Router to render its UI. The implementation is fairly standard. The most important parts are described in the following diagram:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d91aa1bf-2a66-4794-aaea-1e52da998fef/03-simple-app-structure-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2f416843-66a2-4ec3-a4cf-a42bba302967/03-simple-app-structure-preview-opt.png" alt="Simple App Structure" /></a><figcaption>**Simple App** Structure. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d91aa1bf-2a66-4794-aaea-1e52da998fef/03-simple-app-structure-opt.png">View large version</a>)</figcaption></figure>

#### Application Code, Step 1: Server

In the repository you can see the entire setup, but for our purposes most of the relevant code is in the <i>router-manager.js</i> file, responsible for Express routes setup and data APIs.

There is a separate <code>express.Router</code> for both page and API routes.</p>

<strong><code>router-manager.js</code></strong>

<pre><code class="language-javascript">...
  createPageRouter() {
      const router = express.Router();
      // respond with index page to ANY request
      router.get('*', (req, res) =&gt; {
          res.render('index');
    });
return router;
},

createApiRouter(app) {
    const router = express.Router();
    router.get('/latest-bills', (req, res) =&gt; {
        this.retrieveLatestBills((err, content) =&gt; {
            if(!err) {
                res.json(JSON.parse(content));
            } else {
                res.status(500).send();
            }
        });
    });
return router;
}
...
</code></pre>

#### Application Code, Step 2: Client

Note that in many cases less significant details, like CSS classes, are omitted for brevity.</p>

<strong><i>client.js</i></strong>

<pre><code class="language-javascript">...
  import routes from './routes';

  render((
  &lt;Router history={createHistory()}&gt;
  {routes}
  &lt;/Router&gt;
  ), document.querySelectorAll('[data-ui-role="content"]')[0]);
</code></pre>

<strong><i>routes.js</i></strong>

<pre><code class="language-javascript">...
  export default (
  &lt;Route path="/" component={App}&gt;
  &lt;Route component={Dashboard}&gt;
  &lt;IndexRoute component={LatestBills}/&gt;
  &lt;/Route&gt;
  &lt;Route path="*" component={NoMatch}/&gt;
  &lt;/Route&gt;
  );
</code></pre>

The reason for using pathless Route (one that doesn’t have the <code>path</code> attribute) is to create a logical and visual container, without having it be a part of the Routes’ path. We’ll expand on this later in the article.</p>

<strong><i>app.js</i></strong>

<pre><code class="language-javascript">export default class App extends React.Component {
  render() {
      return (
      &lt;div&gt;
      &lt;Header root={this.props.route.path}/&gt;
      {this.props.children}
      &lt;/div&gt;
      );
  }
}
</code></pre>

<strong><i>Header.js</i></strong>

<pre><code class="language-javascript">export default class Header extends React.Component {
  render() {
      return (
      &lt;header&gt;
      &lt;h1&gt;
      &lt;IndexLink to={this.props.root}&gt;App&lt;/IndexLink&gt;
      &lt;/h1&gt;
      &lt;/header&gt;
      );
  }
}
</code></pre>

<strong><i>Dashboard.js</i></strong>

<pre><code class="language-javascript">export default class Dashboard extends React.Component {
  render() {
      return (
      &lt;main&gt;
      {this.props.children}
      &lt;/main&gt;
      );
  }
}
</code></pre>

<strong><i>LatestBills.js</i></strong>

<pre><code class="language-javascript">export default class LatestBills extends React.Component {
  constructor(props) {
      super(props);
      this.state = {items: []};
  }

  render() {
      return (
      &lt;section&gt;
      &lt;header&gt;&lt;h3&gt;Latest Bills&lt;/h3&gt;&lt;/header&gt;
      &lt;section&gt;
      &lt;List items={this.state.items} itemType={CompactBill}/&gt;
      &lt;/section&gt;
      &lt;/section&gt;
      );
  }

componentDidMount() {
    fetch('/api/latest-bills').then((response) =&gt; {
        return response.json();
    }).then((data) =&gt; {
        this.setState({items: data.items});
    }).catch((err) =&gt; {
        throw new Error(err);
    });
  }
}
</code></pre>

<code>LatestBills</code> component uses <code>List</code> and <code>CompactBill</code> pure components to construct its UI. Being able to seamlessly pass components to other components is one of the more subtle, overlooked and absolutely awesome features of React.</p>

<code>LatestBills</code>, like the commonly accepted, albeit somewhat simplified pattern, issues an Ajax request in <code>componentDidMount</code> to populate its data.</p>

<code>CompactBill</code> component looks like you would expect:

<pre><code class="language-javascript">export default class CompactBill extends React.Component {
  render() {
      const data = this.props.data;
      const price = `$${data.price}`;

      return (
      &lt;div&gt;
      &lt;img src={data.icon}/&gt;
      &lt;div&gt;
      &lt;h4&gt;{data.vendor}&lt;/h4&gt;
      &lt;span&gt;{data.period}&lt;/span&gt;
      &lt;/div&gt;
      &lt;span&gt;{price}&lt;/span&gt;
      &lt;/div&gt;
      );
  }
}
</code></pre>

#### Analysis

The process of loading the application above may be schematically represented in the following manner:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7b9b31fd-889e-4a12-b785-b274642ef886/04-client-side-rendering-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e9a5ff70-95b8-442d-8772-a1e15cd0943e/04-client-side-rendering-preview-opt.png" alt="Client side rendering" /></a><figcaption>Server, here, includes *CDN* as well. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7b9b31fd-889e-4a12-b785-b274642ef886/04-client-side-rendering-opt.png">View large version</a>)</figcaption></figure>

This is far from optimal, as the user has to wait, in many cases, for the entire HTML → JavaScript → data sequence to finish, in order to be able to use the application.

This depends on the nature of the application. In some cases parts of the application may be rendered and become usable before it is fully rendered. On the opposite side of the spectrum there are applications that, despite being fully rendered, are not yet interactive, as not all JavaScript and/or data has been retrieved.

While it may be improved by <a href="https://developers.google.com/web/fundamentals/performance/?hl=en">further optimization</a> (the link serves as an excellent starting point), the improvements are still limited by data that you need to retrieve after the application code has been downloaded and parsed. This takes time and <strong>negatively impacts perceived performance</strong>.

Since the entire application is rendered in the browser using data brought in by Ajax, its machine-friendliness is questionable at best. There are measures you can take (like <a href="https://developers.google.com/webmasters/ajax-crawling/docs/html-snapshot?hl=en">snapshotting</a>), but they add more complexity and are prone to error.

We can do better.</p>

### Naive Universal Application

The application can be found in the <a href="https://github.com/zen-js-code/react-universal-web-apps/tree/simple+ssr">simple+ssr branch</a>.

The idea behind this version of the application is to:

1.  render HTML on the server, based on data necessary
2.  deliver the HTML to the browser
3.  send the data used to render the HTML to the browser as well
4.  allow React to resolve the necessary rerenders
5.  profit

Profit here means the ability to render and deliver friendly markup to machines and a quick response to the human user.

#### Setup

There is no change in the general setup of the application.

#### Application code

The structure remains the same, with some parts undergoing various changes.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0253af93-f467-4320-bbba-5754051f599a/05-simple-ssr-app-structure-1-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/eef5a13d-81e0-4d77-9a0b-426497fe7453/05-simple-ssr-app-structure-1-preview-opt.png" alt="Simple SSR app structure" /></a><figcaption>**Orange** denotes parts changed in this version. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0253af93-f467-4320-bbba-5754051f599a/05-simple-ssr-app-structure-1-opt.png">View large version</a>)</figcaption></figure>

#### 1. Server

<i>route-manager.js</i>

<pre><code class="language-javascript">// extend React Router RoutingContext
  class AugmentedRoutingContext extends RoutingContext {
      createElement(component, props) {
          // inject additional props into the component to be created
          const context = this.props.context;
          return component == null ?
          null : this.props.createElement(component, {...props, ...{context}});
      }
};

const routeManager = Object.assign({}, baseManager, {
    ...
    createPageRouter() {
        const router = express.Router();

        router.get('*', (req, res) =&gt; {
        // match URL to our application's routes
        match({routes, location: req.originalUrl}, (err, redirect, renderProps) =&gt; {
            // we just retrieve latest bills, as it is the only one we have
            this.retrieveLatestBills((err, data) =&gt; {
                if(!err) {
                    // render the HTML
                    const html = this.render(renderProps, data);
                    // delive the HTML to the browser
                    res.render('index', {
                        content: html,
                        context: data
                    });
                } else {
                    res.status(500).send();
                }
            });
        });
    });

    return router;
  },
    ...
    render(renderProps, data) {
        // create context to be passed down in additional props
        const additionalProps = {context: JSON.parse(data)};
        const html = renderToString(
            &lt;AugmentedRoutingContext {...renderProps} {...additionalProps}/&gt;
        );

    return html;
  }
});
</code></pre>

This is where the bulk of the changes is. The process may be described as follows:

1.  match (and then completely disregard, for now) the URL to the application’s routes
2.  request the data for the latest bills
3.  when the data arrives, render the HTML using `renderToString` and send it to the browser
4.  create context to be used in component’s rendering and attach it to the HTML above

Here, <code>AugmentedRoutingContext</code> allows us to inject data in all components, so that it is available to <code>LatestBills</code> during server rendering. It may not be efficient or pretty, but it means we don’t have to propagate the data through the entire component tree.

#### 2. Client

There are only two changes:

<strong><i>index.hbs</i></strong>

<pre><code>&lt;div data-ui-role="content"&gt;{{{content}}}&lt;/div&gt;
  &lt;script&gt;
  window.APP_STATE = {{{context}}};
  &lt;/script&gt;
  &lt;script src="/assets/js/app.js" defer&gt;&lt;/script&gt;
</code></pre>

<strong><i>LatestBills.js</i></strong>

<pre><code class="language-javascript">export default class LatestBills extends React.Component {
  constructor(props) {
      super(props);
      this.state = this.props.context || process.APP_STATE || {items: []};
  }

  render() {
      return (
          &lt;section&gt;
          &lt;header&gt;&lt;h3&gt;Latest Bills&lt;/h3&gt;&lt;/header&gt;
          &lt;section&gt;
          &lt;List items={this.state.items} itemType={CompactBill}/&gt;
          &lt;/section&gt;
          &lt;/section&gt;
     );
  }

  // still retrieve data via AJAX, to update (if changed) the one received
  // from the server in the initial load
  componentDidMount() {
      fetch('/api/latest-bills').then((response) =&gt; {
          return response.json();
      }).then((data) =&gt; {
          this.setState({items: data.items});
      }).catch((err) =&gt; {
          throw new Error(err);
      });
  }
}
</code></pre>

The data we used on the server to render the initial HTML needs to be passed to the browser. The reason for that is that in the browser, when our application is eventually downloaded and run, React needs to reconcile the HTML, attach event handlers and do all sorts of maintenance work. Data, used to render the application, is crucial to that, as it allows React to not touch parts that haven’t been changed when using the same data for reconciliation.

The simplest way to deliver the data is by injecting it into the HTML as a JSON string in a global (forgive me) variable using <code>window.APP_STATE = {{{context}}};</code>.

Now, the only thing that remains is to actually pass that data to the <code>LatestBills</code> component for React to consider, which is what these lines are doing:

<pre><code class="language-javascript">constructor(props) {
  super(props);
  this.state = this.props.context || window.APP_STATE || {items: []};
}
</code></pre>

Note that if we where to omit <code>window.APP_STATE</code>, we’d get the dreaded:

<pre><code>Warning: React attempted to reuse markup in a container but the checksum was invalid. This generally means that you are using server rendering and the markup generated on the server was not what the client was expecting...
</code></pre>

indicating that React wasn’t able to reconcile and merge the data (since we didn’t give it any).

The interesting part about <code>window</code> is that on the server it works because of the <code>||</code> short-circuit evaluation. Despite <code>window</code> not existing on server, it is never evaluated, because we passed in the <code>context</code> via <code>AugmentedRoutingContext</code> which then became <code>this.props.context</code>.

#### Analysis

The process of delivering the application and its data to the user (both human and machine) is now changed:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/095c62be-3f58-4dad-8656-a947c731cd2a/06-server-side-rendering-1-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a8b58b38-0f1d-42ac-9620-04b691bedb7a/06-server-side-rendering-1-preview-opt.png" alt="Server side rendering" /></a><figcaption>Server side rendering (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/095c62be-3f58-4dad-8656-a947c731cd2a/06-server-side-rendering-1-opt.png">View large version</a>)</figcaption></figure>

Look at that performance!

Before we start gleefully high-fiving each other and contemplate where to get an early lunch, consider the implications of the solution. We provided the application, in browser, with the data that was used to render it on the server, but the process is far from satisfactory.

Users, via the dark magic of link sharing, search engines and clicking those annoying browser buttons, do not always arrive at your application’s front door. They appear directly in its kitchen, expecting to see a hot kettle on the stove and cookies on the table. It’s up to you (well, the server) to understand what they expect to receive based on some external information on how they arrived there, as they… they do not speak.

The “do not speak” part of the forced sentence above refers to the fact that components should be as detached from routing logic as possible. This means that we do not couple the components with their corresponding routes. Thus, they can’t tell the server how they got there. It has to deduce that from the routes, hence the <code>match({routes, location: req.originalUrl}, (...</code> call.

Allegories aside, this means that in order to be able to piggyback the data onto the application’s HTML, some logic on the server would have to decide what data is needed and preferably attach only that data.

In our primitive application the decision of which data API to hit was very straightforward: we only have one. However, when the routes hit multiple components, each of which requires data to render, this quickly becomes a nightmare to code and maintain.

More importantly, implementing it would mean that you essentially rewrite your application presentation logic. On the server. Which negates one of the major reasons to have universal applications in the first place: a single, as DRY as possible, codebase.

The next logical question would be: “Why not let each component either receive props from its parent or retrieve data and then render itself, much like in the browser?” And herein lies one of the main hurdles! React’s <code>renderToString</code> (and <code>renderToStaticMarkup</code>) methods are, unfortunately, synchronous. That means, since most of the data retrieval mechanisms are asynchronous, that you can’t let components render themselves on server.

It simply wouldn’t work. The data is either lost, because no one waits for it:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0255a756-055a-42bd-b8f6-1d0478137634/07-server-side-rendering-2-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7d68848b-7ee0-4282-a6ba-03edac96e54f/07-server-side-rendering-2-preview-opt.png" alt="Server side rendering" /></a><figcaption>Server side rendering (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0255a756-055a-42bd-b8f6-1d0478137634/07-server-side-rendering-2-opt.png">View large version</a>)</figcaption></figure>

or it <strong>blocks the event loop</strong>:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/91ca2ee2-fa30-4168-b363-843c7e21f597/08-server-side-rendering-3-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f9a1cd71-bc66-4d21-aa2c-769982cea7aa/08-server-side-rendering-3-preview-opt.png" alt="Server side rendering" /></a><figcaption>Server side rendering (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/91ca2ee2-fa30-4168-b363-843c7e21f597/08-server-side-rendering-3-opt.png">View large version</a>)</figcaption></figure>

<strong>Event loop blocking</strong> (mentioned in brief in the diagrams above) is, of course, a problem. In this instance, the rendering is a CPU-bound operation, which for our application above, on my relatively decent machine, takes around 10ms on average. That’s time Node doesn’t use to serve other requests. We’ll get back to this topic toward the end of the article, as it is a universal issue for any server-rendering solution and not specific to this implementation or React.

We are getting closer, as concerns like SEO are being addressed, but the elusive universal web application is still not there.</p>

### A Little Less Naive Universal Application

The application can be found in the <a href="https://github.com/zen-js-code/react-universal-web-apps/tree/simple+ssr+context">simple+ssr+context branch</a>.

Before moving on to greater challenges and more complex variations of the application, let’s rework the last example to make use of a relatively new (and still experimental) feature of React: <a href="https://facebook.github.io/react/docs/context.html">Contexts</a>.

This feature allows you to pass data to components from parents, without having to explicitly propagate it via props, which, as you can probably tell, is what we did with our <code>AugmentedRoutingContext</code> above.

So, let’s React-ify the previous effort a little bit.

Keep in mind that with great power and all that, this should be used judiciously.

#### Application code

The structure remains the same, with some parts undergoing various changes.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cbbe521a-55be-470b-9016-a1de7fb96002/09-simple-ssr-app-structure-2-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7fb483f5-d147-4645-9001-fb4bca75b4f3/09-simple-ssr-app-structure-2-preview-opt.png" alt="simple app structure" /></a><figcaption>**Orange** denotes parts changed in this version. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cbbe521a-55be-470b-9016-a1de7fb96002/09-simple-ssr-app-structure-2-opt.png">View large version</a>)</figcaption></figure>

<strong>1. Server</strong>

The only change is in the <code>render</code> method:

<strong><i>route-manager.js</i></strong>

<pre><code class="language-javascript">...
    render(renderProps, data) {
        const parsedData = JSON.parse(data);
        let html = renderToString(
            &lt;ContextWrapper data={parsedData}&gt;
            &lt;RoutingContext {...renderProps}/&gt;
            &lt;/ContextWrapper&gt;
         );
    return html;
  }
  ...
</code></pre>

This is already much more React-ive approach, where the <code>ContextWrapper</code> component used above looks like this:

<strong><i>ContextWrapper.js</i></strong>

<pre><code class="language-javascript">export default class ContextWrapper extends React.Component {
  // exposes a property to be passed via the Context
  static get childContextTypes() {
      return {
          data: React.PropTypes.object
      };
  }

  // populates the property
  getChildContext() {
    return {
        data: this.props.data
    };
  }

  render() {
    return this.props.children;
  }
}
</code></pre>

<code>ContextWrapper</code> defines the Context property type and provides a method that retrieves it. All that is left for the wrapped component to do is to declare its desire to consume the Context property via the <code>contextTypes</code> static property.

Notice that ES6 doesn’t have static properties, but allows us to define static methods, including getters (<code>static get childContextTypes()</code>) that will serve as properties instead.

The only component we currently have that consumes data is <code>LatestBills</code>, so we alter it to opt in to Context and change its constructor to not rely on <code>window.APP_DATA</code> and read its initial data from the Context instead.</p>

<strong><i>LatestBills.js</i></strong>

<pre><code class="language-javascript">...
static get contextTypes() {
    return {
        data: React.PropTypes.object
    };
}

constructor(props, context) {
    super(props, context);
    this.state = context.data || {items: []};
}
...
</code></pre>

<strong>2. Client</strong>

And what happens in the browser? We are going to use <code>ContextWrapper</code> in the same manner:

<strong><i>client.js</i></strong>

<pre><code class="language-javascript">...
  render((
      &lt;ContextWrapper data={window.APP_STATE}&gt;
      &lt;Router history={createHistory()}&gt;
      {routes}
      &lt;/Router&gt;
      &lt;/ContextWrapper&gt;
  ), document.querySelectorAll('[data-ui-role="content"]')[0]);
</code></pre>

Now, the only place in browser that has any dependency on the <code>window.APP_STATE</code> atrocity is in <i>client.js</i>. Small win.</p>

### More Complex, But Still Naive, Application

The application can be found in the <a href="https://github.com/zen-js-code/react-universal-web-apps/tree/simple+ssr+context+promises">simple+ssr+context+promise branch</a>.

We are going to expand the application by adding another, without doubt highly anticipated, page: Detailed Bill.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f7275a35-52d4-48f9-ad9a-6da3268996a9/10-complex-app-structure-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/31094ccc-71e9-4210-909f-5909cbc69324/10-complex-app-structure-preview-opt.png" alt="Complex app structure" /></a><figcaption>**Orange** denotes parts changed in this version. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f7275a35-52d4-48f9-ad9a-6da3268996a9/10-complex-app-structure-opt.png">View large version</a>)</figcaption></figure>

The new page looks similar to the following:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e0639ec2-5ee2-40ff-9bd3-5b6fb7465cb3/11-app-detailed-bill-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f4fe2114-e166-434d-b620-2af14ea52152/11-app-detailed-bill-preview-opt.png" alt="App detailed" /></a><figcaption>Bill details. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e0639ec2-5ee2-40ff-9bd3-5b6fb7465cb3/11-app-detailed-bill-opt.png">View large version</a>)</figcaption></figure>

In addition, we will teach those components to talk. Basically, we are going to provide the server with some information about how and what data should be loaded to render the needed components.

#### Application Code

<strong>1. Server</strong>

<strong><i>route-manager.js</i></strong>

<pre><code class="language-javascript">...
  const routeManager = Object.assign({}, baseManager, {
      ...
      createPageRouter() {
          const router = express.Router();
          router.get('*', (req, res) =&gt; {
              // match routes to the URL
              match({routes, location: req.originalUrl},
              (err, redirectLocation, renderProps) =&gt; {
                  // each component carries a promise that retrieves its data
                  const {promises, components} = this.mapComponentsToPromises(
                  renderProps.components, renderProps.params);
                  // when all promises are resolved, process data
                  Promise.all(promises).then((values) =&gt; {
                      // create map of [component name -&gt; component data]
                      const data = this.prepareData(values, components);
                      // render HTML
                      const html = this.render(data, renderProps);
                      // send HTML and the map to the browser
                      res.render('index', {
                          content: html,
                          context: JSON.stringify(data)
                      });
                  }).catch((err) =&gt; {
                      res.status(500).send(err);
                  });
              });
          });

          return router;
      },

     // some components define a `requestData` static method that returns promise;
     // skip the rest
    mapComponentsToPromises(components, params) {
        const filteredComponents = components.filter((Component) =&gt; {
            return (typeof Component.requestData === 'function');
        });

        const promises = filteredComponents.map(function(Component) {
            return Component.requestData(params, nconf.get('domain'));
        });

    return {promises, components: filteredComponents};
    },

    // create component name -&gt; component data map
    prepareData(values, components) {
        const map = {};

        values.forEach((value, index) =&gt; {
            map[components[0].NAME] = value.data;
        });

    return map;
    },

    render(data, renderProps) {
        let html = renderToString(
        &lt;ContextWrapper data={data}&gt;
        &lt;RoutingContext {...renderProps}/&gt;
        &lt;/ContextWrapper&gt;
    );

    return html;
    },

    ...

    createApiRouter(app) {
        ...
        router.get('/bill/:id', (req, res) =&gt; {
            const id = req.params.id;

            this.retrieveDetailedBills((err, data) =&gt; {
                if(!err) {
                    const billData = data.items.filter((item) =&gt; {
                        return item.id === id;
                    })[0];
                    res.json(billData);

                } else {
                    res.status(500).send(err);
                }
            });
        });

    return router;
    }
});
</code></pre>

Data sanitation was skipped for brevity.

As you can see there are several things happening here:

1.  a new `/bill/:id` API endpoint that returns specific bill’s detailed information is defined
2.  all Route components that do not have `requestData` static method are filtered out
3.  `requestData` (that returns promise) for the remaining components is invoked and promises are kept
4.  when all promises are fulfilled, we process the accumulated data and create a map of `name` → `data` for each component
5.  each component provides a static `NAME` property
6.  HTML is rendered and, along with the data, sent to the browser

The above is made possible because React Router provides the list of involved Routecomponents in <code>renderProps.components</code> property.

This approach allows us to achieve two main things:

*   provide a hook for the server to use, on per-component basis, to retrieve only the data that component needs
*   allow components to consume it later on in the browser, from the provided map

<strong>2. Client</strong>

A new Route component, <em>Detailed Bill</em>, is added to the routes configuration.</p>

<strong><i>routes.js</i></strong>

<pre><code class="language-javascript">export default (
  &lt;Route path="/" component={App}&gt;
  &lt;Route component={Dashboard}&gt;
  &lt;IndexRoute component={LatestBills}/&gt;
  &lt;Route path="bill/:id" component={DetailedBill}/&gt;
  &lt;/Route&gt;
  &lt;Route path="*" component={NoMatch}/&gt;
  &lt;/Route&gt;
  );
</code></pre>

Now is the time, as promised, to dive a little into the pathless Dashboard route.

Pathless here, of course, means the lack of explicit <code>path</code> attribute on its definition:

<code>&lt;Route component={Dashboard}&gt;...&lt;/Route&gt;</code>.

The idea is simple: Dashboard component contains some common (for all nested components) functionality and markup, and should be loaded by default, as should LatestBills component.

React Router <a href="https://github.com/rackt/react-router/blob/latest/docs/API.md#route">provides</a> a way of dealing with these situations:

If (path) left undefined, the router will try to match the child routes.

Thus loading <code>/</code> resolves Dashboard and then attempts to resolve its children, namely LatestBill, while loading <code>/bill/1234</code> also resolves Dashboard and then resolves DetailedBill instead.

That being out of the way, let’s move on to the implementation part.

In the <em>DetailedBill</em> component below, note the retrieval process of the initial data from the map. Map is still, as before, propagated via React Context. Again, note the static getter methods, serving as static properties.</p>

<strong><i>DetailedBill.js</i></strong>

<pre><code class="language-javascript">export default class DetailedBill extends React.Component {
  static get NAME() {
      return 'DetailedBill';
  }

  static get contextTypes() {
      return {
          data: React.PropTypes.object
      };
  }

  static requestData(params, domain = ’) {
      return axios.get(`${domain}/api/bill/${params.id}`);
  }

  constructor(props, context) {
      super(props, context);
      // get THIS component's data from the provided map
      this.state = context.data[DetailedBill.NAME] || {};
  }

  render() {
      const price = `$${this.state.price}`;

      return (
      &lt;section&gt;
      &lt;header&gt;&lt;h3&gt;Bill Details&lt;/h3&gt;&lt;/header&gt;
      &lt;section&gt;
      &lt;div&gt;
      &lt;img src={this.state.icon}/&gt;
      &lt;div&gt;
      &lt;h4&gt;{this.state.vendor}&lt;/h4&gt;
      &lt;span&gt;{this.state.period}&lt;/span&gt;
      &lt;hr/&gt;
      &lt;span&gt;
      &lt;span&gt;Paid using: &lt;/span&gt;
      &lt;span&gt;{this.state.paymeans}&lt;/span&gt;
      &lt;/span&gt;
      &lt;/div&gt;
      &lt;span&gt;{price}&lt;/span&gt;
      &lt;/div&gt;
      &lt;/section&gt;
      &lt;/section&gt;
      );
  }

  componentDidMount() {
      this.constructor.requestData(this.props.params).then((response) =&gt; {
          this.setState(response.data);
      }).catch((err) =&gt; {
          console.log(err);
      });
  }
}
</code></pre>

Similar change is done to the <code>LatestBills</code> component, whereas <code>render</code> method remained unchanged and thus has been skipped:

<strong><i>LatestBills.js</i></strong>

<pre><code class="language-javascript">export default class LatestBills extends React.Component {
  static get NAME() {
  return 'LatestBills';
}

static get contextTypes() {
    return {
        data: React.PropTypes.object
    };
}

static requestData(params, domain = ’) {
    return axios.get(`${domain}/api/latest-bills`);
}

constructor(props, context) {
    super(props, context);
    this.state = context.data[LatestBills.NAME] || {items: []};
}
...
componentDidMount() {
    this.constructor.requestData().then((response) =&gt; {
        this.setState(response.data);
    }).catch((err) =&gt; {
        console.log(err);
    });
  }
}

</code></pre>

#### Analysis

This attempt allowed us to discover a paradigm that gets us closer to the ultimate universal web application - the ability to convey to the server which data the specific set of routes that construct the request URL requires.

So, in our imaginary universal web application checklist we now have:

*   ability to render our application on server and client, **using the same code**
*   ability to **translate URL** to application components to be rendered
*   ability to **deduce the necessary data** to render these components
*   ability to **reconcile the data** used on server with the client

What we still lack is:

*   ability to **asynchronously** render the application on server
*   ability to reliably control the **event loop blocking**

One important point to consider is that all the data retrieval logic we delegated to the server pertains only to Route components, because any inner components, like <code>CompactBill</code> in our application, are left to their own devices. Since they are not passed as part of <code>renderProps</code> (in <code>renderProps.components</code> property), we won’t be able to invoke their corresponding data retrieval methods.</p>

### A Note On Data Loading

While a more in-depth discussion of universal data loading is a topic for a separate article, it is worth pausing here for a moment and address the issue that comes with it.

The decision, mentioned above, to limit data to Route components only is an important and non-voluntary one. React doesn’t provide, currently, a built-in, structured way of retrieving data on the server without either forfeiting performance and availability (by blocking on data retrieval) or compromising on depth from which the pure components start. That is because both <code>renderToString</code> and <code>renderToStaticMarkup</code> methods, as was mentioned before, are <strong>synchronous</strong>.

Any component that is not a Route component, must be pure (as in - expecting to receive data via props) for the purposes of server-side rendering.

One could argue that there is a method to the madness, perhaps. In most cases, you’d be wise to detach your data retrieval logic, even simple API calls, from as many components as you can, striving for more <strong>pure components</strong>, as these are easier to develop, test and maintain.

Nevertheless, such an approach may not suit all applications, and when you consider that data fetching may rely on a <strong>much</strong> more complex inter-dependent mechanism, we’d be wise to find a more robust solution.

As an example of such a solution (or beginnings of it), consider HTML streaming - an alternative to React’s native <code>renderToString</code>, where the result is streamed (along with the surrounding HTML) to the client, instead of blocking. <a href="https://github.com/aickin/react-dom-stream">react-dom-stream</a> is one of the possible implementations.</p>

### Flux Universal Application

The application can be found in the <a href="https://github.com/zen-js-code/react-universal-web-apps/tree/flux+ssr+context+promises">flux+ssr+context+promise branch</a>.

At this point I can literally hear rumblings of “Flux! Flux” in the audience. And almost canonical Flux at that. That is our next step.

Flux is an architectural recommendation for structuring React applications. It advocates unidirectional data flow connected to React components (View) and deals with concepts (which we won’t expand on here) like <em>stores</em> that contain data, <em>actions</em> that are triggered by the <em>view</em> and a single <em>dispatcher</em> that translates these actions into store interactions.

So, in this variant of the application, we are going to make a transformation from our naive Flux-less (excellent!) application to still (hopefully less) naive Flux-ful one.

Flux architecture, in the context of our application, may be schematically represented like this:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b09441fe-b28e-456c-86fa-cd1f8c035e35/12-flux-architecture-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/47637432-e2b0-465c-943c-1a7363f271f5/12-flux-architecture-preview-opt.png" alt="Flux Architecture." /></a><figcaption>Flux Architecture. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b09441fe-b28e-456c-86fa-cd1f8c035e35/12-flux-architecture-opt.png">View large version</a>)</figcaption></figure>

The purple arrows represent the aforementioned unidirectional data flow. To achieve this structure, the following changes were made:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3564f6de-d297-47b3-a8a7-59ea1f331772/13-flux-app-structure-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4e7af10a-74a2-4183-b2b4-eba2c9ca168e/13-flux-app-structure-preview-opt.png" alt="flux app structure" /></a><figcaption>**Orange** denotes parts changed in this version. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3564f6de-d297-47b3-a8a7-59ea1f331772/13-flux-app-structure-opt.png">View large version</a>)</figcaption></figure>

Normally, a Flux implementation would create a connection between a component and its store(s), as well as a connection between a store and the dispatcher.</p>

<strong><code>SomeStore</code></strong>

<pre><code class="language-javascript">import AppDispatcher from '../dispatcher/AppDispatcher';

  let detailedBillData = {};

  export class SomeStore extends EventEmitter {
  ...
}
...
const SomeStoreInstance = new SomeStore();
...
AppDispatcher.register(function(action) {
    switch (action.type) {
        case Consts.LOAD_SOME_DATA:
        SomeStoreInstance.setAll(action.data);
        SomeStoreInstance.emitChange();
        break;
        ...
        default:
    }
});
</code></pre>

<strong><code>SomeComponent</code></strong>

<pre><code class="language-javascript">import SomeStoreExample from '../../stores/SomeStore';
  import Actions from '../../actions/Actions';

  export default class SomeComponent extends React.Component {
      ...
      render() {
      ...
      }

  componentWillMount() {
      SomeStore.addChangeListener(this.onChange.bind(this));
  }

  componentWillUnmount() {
      SomeStore.removeChangeListener(this.onChange.bind(this));
  }
  ...
  onChange() {
      const state = SomeStore.getAll();
      this.setState(state);
  }
}
</code></pre>

While this would work perfectly and is generally acceptable, we would like to avoid such a coupling. Let’s try, again, to React-ify this a bit. Let’s create a component! Or a factory of components!

#### Application code

<strong>1. Server</strong>

There are no significant changes in server files.</p>

<strong>2. Client</strong>

The “factory” joke from above was not really a joke (and it probably wasn’t funny):

<strong><i>ComponentConnectorFactory.js</i></strong>

<pre><code class="language-javascript">export class ComponentConnectorFactory {
  connect(options) {
      const {component: Component, store: Store, name: name} = options;
      const storeInstance = new Store();
      AppDispatcher.register(storeInstance.handleAction.bind(storeInstance));

      class ComponentConnector extends React.Component {
          static get NAME() {
              return name;
          }

          static get contextTypes() {
              return {
                  data: React.PropTypes.object
              };
          }

          static loadAction(params, domain) {
              return Component.loadAction(params, domain);
          }

          constructor(props, context) {
              super(props, context);
              storeInstance.setAll(context.data[name]);
          }

          render() {
              return &lt;Component {...this.props} store={storeInstance}/&gt;;
          }
    }

    return ComponentConnector;
  }
}

export default new ComponentConnectorFactory();
</code></pre>

Here, instead of creating up-front a connection between specific stores to the dispatcher to the specific component, we create a dependency injection mechanism of sorts, that will connect these from the outside.

We create, in the <code>connect</code> function, a parent component (a sort of decorator) that envelops the provided component. You can see that all the concerns of context awareness (in <code>contextTypes</code> static method), component name (in <code>NAME</code>), method by which to load the necessary data (<code>loadAction</code> method) store registration and connection between a component and a <strong>specific</strong> store are abstracted away.

Then we would use it, like you would expect:

<strong><i>routes.js</i></strong>

<pre><code class="language-javascript">import LatestBills from './components/bill/LatestBills';
  import DetailedBill from './components/bill/DetailedBill';

  import DetailedBillStore from './stores/DetailedBillStore';
  import LatestBillsStore from './stores/LatestBillsStore';

  import ComponentConnectorFactory from './components/common/ComponentConnectorFactory';

  const DetailedBillConnector = ComponentConnectorFactory.connect({
  name: 'DetailedBillConnector',
  component: DetailedBill,
  store: DetailedBillStore
});

const LatestsBillsConnector = ComponentConnectorFactory.connect({
    name: 'LatestsBillsConnector',
    component: LatestBills,
    store: LatestBillsStore
});

export default (
&lt;Route path="/" component={App}&gt;
&lt;Route component={Dashboard}&gt;
&lt;IndexRoute component={LatestsBillsConnector}/&gt;
&lt;Route path="bill/:id" component={DetailedBillConnector}/&gt;
&lt;/Route&gt;
&lt;Route path="*" component={NoMatch}/&gt;
&lt;/Route&gt;
);
</code></pre>

Because the <code>...Connector</code> component is a fully fledged React component we can freely use it in our routes definition above, limiting the coupling between stores, components and dispatchers (specific ones) to one place.

There is some symmetry here: we have all navigation concerns centralized in one file, and now we have all wiring/integration concerns concentrated there as well.</p>

<code>LatestBills</code> component would look much simpler and cleaner:

<strong><i>LatestBills.js</i></strong>

<pre><code class="language-javascript">...
  export default class LatestBills extends React.Component {
      static loadAction(params, domain) {
          return Actions.loadLatestBillsData(params, domain);
      }

constructor(props) {
    super(props);
    this.changeHandler = this.onChange.bind(this);
    this.state = this.props.store.getAll() || {};
}

componentWillMount() {
    if (process.browser) {
        this.props.store.addChangeListener(this.changeHandler);
    }
}

componentWillUnmount() {
    this.props.store.removeChangeListener(this.changeHandler);
}

componentDidMount() {
    Actions.getLatestBillsData(this.props.params);
}
...
onChange() {
    const state = this.props.store.getAll();
    this.setState(state);
}

render() {
    return (
    &lt;section&gt;
    &lt;header&gt;&lt;h3&gt;Latest Bills&lt;/h3&gt;&lt;/header&gt;
    &lt;section&gt;
    &lt;List items={this.state.items} itemType={CompactBill}/&gt;
    &lt;/section&gt;
    &lt;/section&gt;
    );
  }
}
</code></pre>

Note the <code>process.browser</code> ugliness, due to <code>componentWillMount</code> being executed on both client and server, but <code>componentWillUnmount</code> on client only. This is a great place to introduce memory leaks into your application. Since we don’t actually mount the component and its data retrieval process happens outside of its lifecycle, we can safely skip this method. I couldn’t tell what the reason was to not split this method into two - of which one runs <strong>only</strong> on server, much like <code>componentDidMount</code> runs only on client, so we are stuck with the ugly.

Note that, if desired, <code>Actions</code> dependency can be extracted as well, but at this point I felt there had to be a clear connection between a component and its actions, so it remained. Also note that <code>loadLatestBillsData</code> method of <code>Actions</code>, the one that is exposed to server in <code>loadAction</code> method - is merely an AJAX call envelope, whereas <code>getLatestBillsData</code> contains application concerns:

<strong><i>Actions.js</i></strong>

<pre><code class="language-javascript">export class Actions {
  loadDetailedBillData(params, domain = ’) {
  const url = `${domain}/api/bill/${params.id}`;
  return axios.get(url);
}

getDetailedBillData(params) {
    this.loadDetailedBillData(params).then((response) =&gt; {
        AppDispatcher.dispatch({
            type: Consts.LOAD_DETAILED_BILL,
            data: response.data
        });
    }).catch((err) =&gt; {
    console.log(err);
  });
}
...
}
...
</code></pre>

<code>LatestBillsStore</code> is also now much simplified:

<strong><i>LatestBillsStore.js</i></strong>

<pre><code class="language-javascript">...
  let latestBillsData = {};

  export default class LatestBillStore extends BaseStore {
  resetAll() {
  latestBillsData = {};
}

setAll(data) {
    latestBillsData = data;
}

getAll() {
    return latestBillsData;
}

handleAction(action) {
    switch (action.type) {
        case Consts.LOAD_LATEST_BILLS:
        this.setAll(action.data);
        this.emitChange();
        break;
        default:
        }
    }
}
</code></pre>

where <code>BaseStore</code> extracts common store stuff:

<strong><i>BaseStore.js</i></strong>

<pre><code class="language-javascript">export default class BaseStore extends EventEmitter {
      static get CHANGE_EVENT() {
      return 'CHANGE_EVENT';
    }

    emitChange() {
        this.emit(this.constructor.CHANGE_EVENT);
    }

    addChangeListener(callback) {
        this.on(this.constructor.CHANGE_EVENT, callback);
    }

    removeChangeListener(callback) {
        this.removeListener(this.constructor.CHANGE_EVENT, callback);
    }
}
</code></pre>

Keep in mind that stores, being singletons, are prone to data leaking, between user sessions, something to keep in mind when considering this or other similar solutions.</p>

## Conclusion

The evolution steps we’ve gone through above are hardly comprehensive, especially in the area of data retrieval on the server. There is a lot of additional work being done by tools and frameworks that have been inspired and enabled by React: <a href="https://github.com/rackt/redux">Redux</a>, <a href="https://facebook.github.io/relay/">Relay</a>, <a href="https://fluxible.io/">Fluxible</a>, <a href="https://alt.js.org/">Alt</a> and so many, many more.

The examples in this article should get you to the point of being able to be a better judge of how, in your particular application, a server-side rendering solution should be approached.

Dive in and enjoy the ride.

{{< signature "rb, jb, ml, og" >}}

