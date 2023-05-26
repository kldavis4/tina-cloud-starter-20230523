---
title: 'Simplify Your Stack With A Custom-Made Static Site Generator'
slug: stack-custom-made-static-site-generator
author: bryan-robinson
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c678c035-9fb8-4909-9f36-a0d26a561406/stack-custom-made-static-site-generator.png
date: 2020-09-23T12:00:00.000Z
summary: >-
  In modern development, there are so many great tools for developing websites, but often they are more than what’s necessary for a given project. In this article, we’ll explore how to take a humble HTML page and make its content editable in a CMS with no frameworks and no client-side JavaScript.
description: >-
  In this article, Bryan Robinson explores how to take a humble HTML page and make its content editable in a CMS with no frameworks and no client-side JavaScript.
categories:
  - CMS
  - JavaScript
  - Frameworks
  - Generators
  - Static Generators
---

With the advent of the Jamstack movement, statically-served sites have become all the rage again. Most developers serving static HTML aren’t authoring native HTML. To have a solid developer experience, we often turn to tools called Static Site Generators (SSG).

These tools come with many features that make authoring large-scale static sites pleasant. Whether they provide simple hooks into third-party APIs like [Gatsby’s](https://gatsbyjs.com) data sources or provide in-depth configuration like [11ty's](https://11ty.dev) huge collection of template engines, there’s something for everyone in static site generation.

Because these tools are built for diverse use cases, they have to have a lot of features. Those features make them powerful. They also make them quite complex and opaque for new developers. In this article, we’ll take the SSG down to its basic components and create our very own.

## What Is A Static Site Generator?

At its core, a static site generator is a program that performs a series of transformations on a group of files to convert them into static assets, such as HTML. What sort of files it can accept, how it transforms them, and what types of files come out differentiate SSGs.

[Jekyll](https://jekyllrb.com/), an early and still popular SSG, uses Ruby to process [Liquid](https://shopify.github.io/liquid/) templates and Markdown content files into HTML.

Gatsby uses React and JSX to transform components and content into HTML. It then goes a step further and creates a single-page application that can be served statically.

11ty renders HTML from templating engines such as Liquid, [Handlebars](https://handlebarsjs.com/), [Nunjucks](https://mozilla.github.io/nunjucks/templating.html), or JavaScript template literals.

Each of these platforms has additional features to make our lives easier. They provide theming, build pipelines, plugin architecture, and more. With each additional feature comes more complexity, more magic, and more dependencies. They’re important features, to be sure, but not every project needs them.

Between these three different SSGs, we can see another common theme: data + templates = final site. This seems to be the core functionality of generator static sites. This is the functionality we’ll base our SSG around.

{{% pull-quote %}}
At its core, a static site generator is a program that performs a series of transformations on a group of files to convert them into static assets, such as HTML.
{{% /pull-quote %}}

## Our New Static Site Generator’s Technology Stack: Handlebars, Sanity.io And Netlify

To build our SSG, we’ll need a template engine, a data source, and a host that can run our SSG and build our site. Many generators use Markdown as a data source, but what if we took it a step further and natively connected our SSG to a CMS?

- Data Source: [Sanity.io](https://sanity.io)
- Data fetching and templating: [Node](https://nodejs.org/) and Handlebars
- Host and Deployment: [Netlify](https://netlify.com).

### Prerequisites

- NodeJS installed
- Sanity.io account
- Knowledge of Git
- Basic knowledge of command line
- Basic knowledge of deployment to services like Netlify.

**Note**: *To follow along, you can find the code in this [repository on GitHub](https://github.com/smashingmagazine/smashing-ssg).*

{{% feature-panel %}}

## Setting Up Our Document Structure In HTML

To start our document structure, we’re going to write plain HTML. No need to complicate matters yet.

In our project structure, we need to create a place for our source files to live. In this case, we’ll create a `src` directory and put our `index.html` inside.

In `index.html`, we’ll outline the content we want. This will be a relatively simple about page.

<div class="break-out">

<pre><code class="language-html"><!DOCTYPE html>&lt;html lang="en"&gt;
&lt;head&gt;
    &lt;meta charset="UTF-8"&gt;
    &lt;meta name="viewport" content="width=device-width, initial-scale=1.0"&gt;
    &lt;title&gt;Title of the page!&lt;/title&gt;
&lt;/head&gt;
&lt;body&gt;
    &lt;h1&gt;The personal homepage of Bryan Robinson&lt;/h1&gt;

    &lt;p&gt;Some pagraph and rich text content next&lt;/p&gt;

    &lt;h2&gt;Bryan is on the internet&lt;/h2&gt;
    &lt;ul&gt;
        &lt;li&gt;&lt;a href="linkURL"&gt;List of links&lt;/a&gt;&lt;/li&gt;
    &lt;/ul&gt;
&lt;/body&gt;
&lt;/html&gt;</code></pre>
</div>

Let’s keep this simple. We’ll start with an `h1` for our page. We’ll follow that with a few paragraphs of biographical information, and we’ll anchor the page with a list of links to see more.

## Convert Our HTML Into A Template That Accepts Data

After we have our basic structure, we need to set up a process to combine this with some amount of data. To do this, we’ll use the [Handlebars](https://handlebarsjs.com/) template engine.

At its core, Handlebars takes an HTML-like string, inserts data via rules defined in the document, and then outputs a compiled HTML string.

To use Handlebars, we’ll need to initialize a package.json and install the package.

Run `npm init -y` to create the structure of a package.json file with some default content. Once we have this, we can install Handlebars.

<pre><code class="language-bash">npm install handlebars</code></pre>

Our build script will be a Node script. This is the script we’ll use locally to build, but also what our deployment vendor and host will use to build our HTML for the live site.

To start our script, we’ll create an `index.js` file and require two packages at the top. The first is Handlebars and the second is a default module in Node for accessing the current file system.

<pre><code class="language-javascript">const fs = require('fs');
const Handlebars = require('handlebars');</code></pre>

We’ll use the `fs` module to access our source file, as well as to write to a distribution file. To start our build, we'll create a `main` function for our file to run when called and a `buildHTML` function to combine our data and markup.

<div class="break-out">

<pre><code class="language-javascript">function buildHTML(filename, data) {
  const source = fs.readFileSync(filename,'utf8').toString();
  const template = Handlebars.compile(source);
  const output = template(data);

  return output
}

async function main(src, dist) {
  const html = buildHTML(src, { "variableData": "This is variable data"});
 
  fs.writeFile(destination, html, function (err) {
    if (err) return console.log(err);
      console.log('index.html created');
  });
}

main('./src/index.html', './dist/index.html');</code></pre>
</div>

The `main()` function accepts two arguments: the path to our HTML template and the path we want our built file to live. In our main function, we run `buildHTML` on the template source path with some amount of data.

The build function converts the source document into a string and passes that string to Handlebars. Handlebars compiles a template using that string. We then pass our data into the compiled template, and Handlebars renders a new HTML string replacing any variables or template logic with the data output.

We return that string into our `main` function and use the `writeFile` method provided by Node’s file-system module to write the new file in our specified location if the directory exists.

To prevent an error, add a `dist` directory into your project with a `.gitkeep` file in it. We don’t want to commit our built files (our build process will do this), but we’ll want to make sure to have this directory for our script.

Before we create a CMS to manage this page, let’s confirm it’s working. To test, we’ll modify our HTML document to use the data we just passed into it. We’ll use the Handlebars variable syntax to include the `variableData` content.

<pre><code class="language-html">&lt;h1&gt;{{ variableData }}&lt;/h1&gt;</code></pre>

Now that our HTML has a variable, we’re ready to run our node script.

<pre><code class="language-bash">node index.js</code></pre>

Once the script finishes, we should have a file at `/dist/index.html`. If we read open this in a browser, we’ll see our markup rendered, but also our “This is variable data” string, as well.

{{% ad-panel-leaderboard %}}

## Connecting To A CMS

We have a way of putting data together with a template, now we need a source for our data. This method will work with any data source that has an API. For this demo, we’ll use Sanity.io. 

Sanity is an API-first data source that treats content as structured data. They have an open-source content management system to make managing and adding data more convenient for both editors and developers. The CMS is what’s often referred to as a “Headless” CMS. Instead of a traditional management system where your data is tightly coupled to your presentation, a headless CMS creates a data layer that can be consumed by any frontend or service (and possibly many at the same time).

Sanity is a paid service, but they have a “Standard” plan that is free and has all the features we need for a site like this.

### Setting Up Sanity

The quickest way to get up and running with a new Sanity project is to use the Sanity CLI. We’ll start by installing that globally.

<pre><code class="language-bash">npm install -g @sanity/cli</code></pre>

The CLI gives us access to a group of helpers for managing, deploying, and creating. To get things started, we’ll run `sanity init`. This will run us through a questionnaire to help bootstrap our Studio (what Sanity calls their open-source CMS).

<pre><code class="language-bash">Select a Project to Use:
   Create new project
   HTML CMS

Use the default dataset configuration?   
   Y // this creates a "Production" dataset

Project output path:
   studio // or whatever directory you'd like this to live in

Select project template
   Clean project with no predefined schemas</code></pre>

This step will create a new project and dataset in your Sanity account, create a local version of Studio, and tie the data and CMS together for you. By default, the `studio` directory will be created in the root of our project. In larger-scale projects, you may want to set this up as a separate repository. For this project, it’s fine to keep this tied together.

To run our Studio locally, we’ll change the directory into the `studio` directory and run `sanity start`. This will run Studio at `localhost:3333`. When you log in, you’ll be presented with a screen to let you know you have “Empty schema.” With that, it’s time to add our schema, which is how our data will be structured and edited.

### Creating Sanity Schema

The way you create documents and fields within Sanity Studio is to create schemas within the `schemas/schema.js` file.

For our site, we’ll create a schema type called "About Details." Our schema will flow from our HTML. In general, we could make most of our webpage a single rich-text field, but it’s a best practice to structure our content in a de-coupled way. This provides greater flexibility in how we might want to use this data in the future.

For our webpage, we want a set of data that includes the following:

- Title
- Full Name
- Biography (with rich text editing)
- A list of websites with a name and URL.

To define this in our schema, we create an object for our document and define out its fields. An annotated list of our content with its field `type`:

- Title &mdash; string
- Full Name &mdash; string
- Biography &mdash; array of "blocks"
- Website list &mdash; array of objects with name and URL string fields.

<div class="break-out">

<pre><code class="language-javascript">types: schemaTypes.concat([
    /* Your types here! */

    {
        title: "About Details",
        name: "about",
        type: "document",
        fields: [
            {
                name: 'title',
                type: 'string'
            },
            {
                name: 'fullName',
                title: 'Full Name',
                type: 'string'
            },
            {
                name: 'bio',
                title: 'Biography',
                name: 'content',
                type: 'array',
                of: [
                    {
                        type: 'block'
                    }
                ]
            },
            {
                name: 'externalLinks',
                title: 'Social media and external links',
                type: 'array',
                of: [
                    {
                        type: 'object',
                        fields: [
                            { name: 'text', title: 'Link text', type: 'string' },
                            { name: 'href', title: 'Link url', type: 'string' }
                        ]
                    }
                ]
            }
        ]
    }
])</code></pre>
</div>

Add this to your schema types, save and your Studio will recompile and present you with your first documents. From here, we’ll add our content into the CMS by creating a new document and filling out the information.

### Structuring Your Content In A Reusable Way

At this point, you may be wondering why we have a "full name" and a "title." This is because we want our content to have the potential to be multipurpose. By including a name field instead of including the name just in the title, we give that data more use. We can then use information in this CMS to also power a resumé page or PDF. The biography field could be programmatically used in other systems or websites. This allows us to have a single source of truth for much of this content instead of being dictated by the direct use case of this particular site.

{{% ad-panel-leaderboard %}}

## Pulling Our Data Into Our Project

Now that we’ve made our data available via an API, let's pull it into our project.

### Install and configure the Sanity JavaScript client

First thing, we need access to the data in Node. We can use the Sanity JavaScript client to forge that connection.

<pre><code class="language-bash">npm install @sanity/client</code></pre>

This will fetch and install the JavaScript SDK. From here, we need to configure it to fetch data from the project we set up earlier. To do that, we’ll set up a utility script in `/utils/SanityClient.js`. We provide the SDK with our project ID and dataset name, and we’re ready to use it in our main script.

<pre><code class="language-javascript">const sanityClient = require('@sanity/client');
const client = sanityClient({
    projectId: '4fs6x5jg',
    dataset: 'production',
    useCdn: true 
  })

module.exports = client;</code></pre>

### Fetching Our Data With GROQ

Back in our `index.js` file, we’ll create a new function to fetch our data. To do this, we’ll use Sanity’s native query language, [the open-source GROQ](https://groq.dev/).

We’ll build the query in a variable and then use the client that we configured to fetch the data based on the query. In this case, we build an object with a property called `about`. In this object, we want to return the data for our specific document. To do that, we query based on the document `_id` which is generated automatically when we create our document.

To find the document’s `_id`, we navigate to the document in Studio and either copy it from the URL or move into “Inspect” mode to view all the data on the document. To enter Inspect, either click the “kabob” menu at the top-right or use the shortcut <kbd>Ctrl</kbd> + <kbd>Alt</kbd> + <kbd>I</kbd>. This view will list out all the data on this document, including our `_id`. Sanity will return an array of document objects, so for simplicity’s sake, we’ll return the `0th` entry.

We then pass the query to the `fetch` method of our Sanity client and it will return a JSON object of all the data in our document. In this demo, returning all the data isn’t a big deal. For bigger implementations, GROQ allows for an optional "[projection](https://www.sanity.io/docs/groq-pipeline-components#projection-component-26f490c27c3d)" to only return the explicit fields you want.

<div class="break-out">

<pre><code class="language-javascript">const client = require('./utils/SanityClient') // at the top of the file

// ...

async function getSanityData() {
    const query = `{
        "about": *[_id == 'YOUR-ID-HERE'][0]
    }`
    let data = await client.fetch(query);
}</code></pre>
</div>

### Converting The Rich Text Field To HTML

Before we can return the data, we need to do a transformation on our rich text field. While many CMSs use rich text editors that return HTML directly, Sanity uses an open-source specification called [Portable Text](https://github.com/portabletext/portabletext). Portable Text returns an array of objects (think of rich text as a list of paragraphs and other media blocks) with all the data about the rich text styling and properties like links, footnotes, and other annotations. This allows for your text to be moved and used in systems that don’t support HTML, like [voice assistants](https://www.smashingmagazine.com/2019/03/sanity-portabletext-speech-synthesis/) and native apps.

For our use case, it means we need to transform the object into HTML. There are NPM modules that can be used to convert portable text into various uses. In our case we’ll use a package called [block-content-to-html](https://github.com/sanity-io/block-content-to-html).

<pre><code class="language-bash">npm install @sanity/block-content-to-html</code></pre>

This package will render all the default markup from the rich text editor. Each type of style can be overridden to conform to whatever markup you need for your use case. In this case, we’ll let the package do the work for us.

<div class="break-out">

<pre><code class="language-javascript">const blocksToHtml = require('@sanity/block-content-to-html'); // Added to the top

async function getSanityData() {
    const query = `{
        "about": *[_type == 'about'][0]
    }`
    let data = await client.fetch(query);
    data.about.content = blocksToHtml({
        blocks: data.about.content
    })
    return await data
}</code></pre>
</div>

### Using The Content From Sanity.io In Handlebars

Now that the data is in a shape we can use it, we’ll pass this to our `buildHTML` function as the data argument.

<pre><code class="language-javascript">async function main(src, dist) {
    const data = await getSanityData();
    const html = buildHTML(src, data)

    fs.writeFile(dist, html, function (err) {
        if (err) return console.log(err);
        console.log('index.html created');
    });
}</code></pre>

Now, we can change our HTML to use the new data. We’ll use more variable calls in our template to pull most of our data.

To render our rich text `content` variable, we’ll need to add an extra layer of braces to our variable. This will tell Handlebars to render the HTML instead of displaying the HTML as a string.

For our `externalLinks` array, we’ll need to use Handlebars’ built-in looping functionality to display all the links we added to our Studio.

<div class="break-out">

<pre><code class="language-html">&lt;!DOCTYPE html&gt;
&lt;html lang="en"&gt;
&lt;head&gt;
    &lt;meta charset="UTF-8"&gt;
    &lt;meta name="viewport" content="width=device-width, initial-scale=1.0"&gt;
    &lt;title&gt;{{ about.title }}&lt;/title&gt;
&lt;/head&gt;
&lt;body&gt;
    &lt;h1&gt;The personal homepage of {{ about.fullName }}&lt;/h1&gt;

    {{{ about.content }}}

    &lt;h2&gt;Bryan is on the internet&lt;/h2&gt;
    &lt;ul&gt;
        {{#each about.externalLinks }}
            &lt;li&gt;&lt;a href="{{ this.href }}"&gt;{{ this.text }}&lt;/a&gt;&lt;/li&gt;
        {{/each}}
    &lt;/ul&gt;
&lt;/body&gt;
&lt;/html&gt;</code></pre>
</div>

## Setting Up Deployment

Let’s get this live. We need two components to make this work. First, we want a static host that will build our files for us. Next, we need to trigger a new build of our site when content is changed in our CMS.

### Deploying To Netlify

For hosting, we’ll use Netlify. Netlify is a static site host. It serves static assets, but has additional features that will make our site work smoothly. They have a built-in deployment infrastructure that can run our node script, webhooks to trigger builds, and a globally distributed CDN to make sure our HTML page is served quickly.

Netlify can watch our repository on GitHub and create a build based on a command that we can add in their dashboard.

First, we’ll need to push this code to GitHub. Then, in Netlify’s Dashboard, we need to connect [the new repository to a new site in Netlify](https://www.netlify.com/blog/2016/09/29/a-step-by-step-guide-deploying-on-netlify/).

Once that’s hooked up, we need to tell Netlify how to build our project. In the dashboard, we’ll head to Settings > Build & Deploy > Build Settings. In this area, we need to change our “Build command” to “node index.js” and our “Publish directory” to “./dist”.

When Netlify builds our site, it will run our command and then check the folder we list for content and publish the content inside.

### Setting Up A Webhook

We also need to tell Netlify to publish a new version when someone updates content. To do that, we’ll set up a Webhook to notify Netlify that we need the site to rebuild. A Webhook is a URL that can be programmatically accessed by a different service (such as Sanity) to create an action in the origin service (in this case Netlify).

We can set up a specific “Build hook” in our Netlify dashboard at Settings > Build & Deploy > Build hooks. Add a hook, give it a name and save. This will provide a URL that can be used to remotely trigger a build in Netlify.

Next, we need to tell Sanity to make a request to this URL when you publish changes.

We can use the Sanity CLI to accomplish this. Inside of our `/studio` directory, we can run `sanity hook create` to connect. The command will ask for a name, a dataset, and a URL. The name can be whatever you’d like, the dataset should be `production` for our product, and the URL should be the URL that Netlify provided.

Now, whenever we publish content in Studio, our website will automatically be updated. No framework necessary.

- The code can be found in [this GitHub repository&nbsp;&rarr;](https://github.com/smashingmagazine/smashing-ssg)

## Next Steps

This is a very small example of what you can do when you create your own tooling. While more full-featured SSGs may be what you need for most projects, creating your own mini-SSG can help you understand more about what’s happening in your generator of choice. 

- This site publishes only one page, but with a little extra in our build script, we could have it publish more pages. It could even publish a blog post.
- The “Developer experience” is a little lacking in the repository. We could run our Node script on any file saves by implementing a package like [Nodemon](https://nodemon.io/) or add “hot reloading” with something like [BrowserSync](https://www.browsersync.io/).
- The data that lives in Sanity can power multiple sites and services. You could create a resumé site that uses this and publishes a PDF instead of a webpage.
- You could add CSS and make this look like a real site. 

{{< signature "ra, yk, il" >}}
