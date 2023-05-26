---
title: 'How To Migrate From jQuery To Next.js'
slug: migrate-jquery-nextjs
author: facundo-giuliani
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ece22577-f23c-4e9c-a41c-f9000f14ae9d/migrate-jquery-nextjs.jpg
date: 2021-07-13T10:30:00.000Z
summary: >-
  In this article, we’re taking a closer look at different approaches and strategies on how we can migrate a web application that uses jQuery framework, and start using one of the coolest React frameworks in the market: Next.js.
description: >-
  In this article, we’re taking a closer look at different approaches and strategies on how we can migrate a web application that uses jQuery framework, and start using one of the coolest React frameworks in the market: Next.js.
categories:
  - Apps
  - jQuery
  - Next.js
  - Frameworks
disable_ads: true
disable_panels: true
disable_newsletterbox: true
sponsor:
  title: Netlify
  link: https://www.netlify.com/
  image: https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dcf23ab4-3a5e-4a81-b79f-b520b5dcf6a2/netlify-full-logo-light.svg
  description: >-
    This article has been kindly supported by our dear friends at <a href="https://www.netlify.com/">Netlify</a> who are a diverse group of incredible talent from all over the world and offers a platform for web developers that multiplies productivity. <em>Thank you!</em>
---

When [jQuery](https://jquery.com/) appeared in 2006, a lot of developers and organizations started to adopt it for their projects. The possibility of **extending and manipulating the DOM** that the library offers is great, and we also have many plugins to add behavior to our pages in case we need to do tasks that aren’t supported by the jQuery main library. It simplified a lot of the work for developers, and, at that moment, it made JavaScript a powerful language to create web applications or Single Page Applications.

The result of **jQuery popularity** is measurable still today: [Almost 80%](https://almanac.httparchive.org/en/2020/javascript#libraries) of the most popular websites of the world still use it. Some of the reasons why jQuery is so popular are:

- It supports DOM manipulation.
- It provides CSS manipulation.
- Works the same on all web browsers.
- It wraps HTML event methods.
- Easy to create AJAX calls.
- Easy to use effects and animations.

Over the years, JavaScript changed a lot and added several features that we didn’t have in the past. With the re-definition and evolution of [ECMAScript](https://www.ecma-international.org/publications-and-standards/standards/ecma-262/), some of the functionalities that jQuery provided were added to the standard JavaScript features and supported by all the web browsers. With this happening, some of the behavior jQuery offers **was not needed anymore**, as we are able to do the same things with plain JavaScript.

On the other hand, a new way of thinking and designing user interfaces started to emerge. Frameworks like React, Angular or Vue allow the developers to create web applications based on reusable functional components. React, i.e., works with the “virtual DOM”, which is a DOM representation in the memory, whereas **jQuery interacts directly with the DOM**, in a less performant way. Also, React offers cool features to facilitate the development of certain features, such as state management. With this new approach and the popularity that Single Page Applications started to gain, a lot of developers started to use React for their web application projects.

And front end development evolved even more, with frameworks created on top of other frameworks. That is the case, for example, of [Next.js](https://nextjs.org/). As you [probably know](https://www.smashingmagazine.com/category/next.js), it’s an open-source React framework that offers features to generate static pages, create server-side rendered pages, and combine both types in the same application. It also allows creating serverless APIs inside the same app.

There is a curious scenario: Even though these frontend frameworks are more and more popular over the years, jQuery is still adopted by a vast majority of web pages. One of the reasons why this happens is that the percentage of websites using WordPress is really high, and **jQuery is included in the CMS**. Another reason is that some libraries, like Bootstrap, have a dependency on jQuery, and there are some ready-to-use templates that use it and its plugins.

But another reason for this amount of websites using jQuery is the cost of migrating a complete web application to a new framework. It’s not easy, it’s not cheap and it’s time-consuming. But, in the end, working with new tools and technologies brings a lot of benefits: wider support, community assistance, better developer experience, and ease of getting people working on the project.

There are many scenarios where we don’t need (or don’t want) to follow the architecture that frameworks like React or Next.js impose on us, and that is OK. However, jQuery is a library that contains a lot of code and features that are not needed anymore. Many of the features jQuery offers can be accomplished using **modern JavaScript native functions**, and probably in a more performant way.

Let’s discuss how we could stop using jQuery and **migrate** our website into a React or Next.js web application.

{{% feature-panel %}}

## Define The Migration Strategy

### Do We Need A Library?

Depending on the features of our web application, we could even have the case where a framework is not really needed. As mentioned before, several jQuery features were included (or at least a very similar one) to the latest web standard versions. So, considering that:

- `$(selector)` pattern from jQuery can be replaced with `querySelectorAll()`.

Instead of doing:

<pre><code class="language-javascript">$("#someId");</code></pre>

We can do:

<pre><code class="language-javascript">document.querySelectorAll("#someId");</code></pre>

- We have now the property `Element.classList` if we want to manipulate CSS classes.

Instead of doing:

<pre><code class="language-javascript">$(selector).addClass(className);</code></pre>

We can do:

<pre><code class="language-javascript">element.classList.add(className);</code></pre>

- Many animations can be done directly using CSS, instead of implementing JavaScript.

Instead of doing:

<pre><code class="language-javascript">$(selector).fadeIn();</code></pre>

We can do:

<pre><code class="language-javascript">element.classList.add('show');
element.classList.remove('hide');</code></pre>

And apply some CSS styling:

<pre><code class="language-css">.show {
  transition: opacity 400ms;
}

.hide {
  opacity: 0;
}</code></pre>

- We have now [addEventListener function](https://developer.mozilla.org/en-US/docs/Web/API/EventTarget/addEventListener) if we want to handle events.

Instead of doing:

<pre><code class="language-javascript">$(selector).on(eventName, eventHandler);</code></pre>

We can do:

<pre><code class="language-javascript">element.addEventListener(eventName, eventHandler);</code></pre>

- Instead of using jQuery Ajax, we can use `XMLHttpRequest`.

Instead of doing:

<pre><code class="language-javascript">$.ajax({
  type: 'POST',
  url: '/the-url',
  data: data
});</code></pre>

We can do:

<div class="break-out">

<pre><code class="language-javascript">var request = new XMLHttpRequest();
request.open('POST', '/the-url', true);
request.setRequestHeader('Content-Type', 'application/x-www-form-urlencoded; charset=UTF-8');
request.send(data);</code></pre>
</div>

For more details, you can take a look at these [Vanilla JavaScript Code Snippets](https://www.smashingmagazine.com/2021/04/vanilla-javascript-code-snippets/).

### Identify Components

If we are using jQuery in our application, we should have some HTML content that is generated on the web server, and JavaScript code that adds interactivity to the page. We are probably **adding event handlers** on page load that will manipulate the DOM when the events happen, probably updating the CSS or the style of the elements. We could also be calling backend services to execute actions, that can affect the DOM of the page, or even reload it. 

The idea would be to **refactor the JavaScript code** living in the pages and build React components. This will help us to join related code and compose elements that will be part of a larger composition. By doing this we will also be able to have better handling of the state of our application. Analyzing the frontend of our application, we should divide it into parts dedicated to a certain task, so we can create components based on that.

If we have a button:

<pre><code class="language-javascript">&lt;button id="btn-action"&gt;Click&lt;/button&gt;</code></pre>

With the following logic:

<pre><code class="language-javascript">var $btnAction = $("#btn-action");

$btnAction.on("click", function() {
  alert("Button was clicked");
});</code></pre>

We can migrate it to a React Component:

<pre><code class="language-javascript">import React from 'react';

function ButtonComponent() {

  let handleButtonClick = () =&gt; {
    alert('Button clicked!')
  }

  return &lt;button onClick={handleButtonClick}&gt;Click&lt;/button&gt;
}
</code></pre>

But we should also evaluate how the migration process will be accomplished since our application is working and being used, and we don’t want to affect it (or, at least, affect it as little as possible).

### Good Migration

A good migration is one where all the parts of the application are fully migrated to the new framework or technology. This would be the ideal scenario for our application since we would keep in sync all the parts, and we would be using a unified tool and a unique referred version. 

A good and complete migration usually includes a complete re-write of the code of our app, and that makes sense. If we build an app from scratch, we have the possibility of deciding what direction we want to take with the new code. We could use a fresh point of view over our existing systems and workflow, and create a whole new app with the knowledge that we have at this moment, more complete than the one we had when we first created our web application.

But a complete rewrite has some problems. First of all, it requires a lot of time. The bigger the application is, the more time we will need to rewrite it. Another problem is the amount of work, and amount of developers, that it takes. And, if we don’t do a progressive migration, we have to think about how much time our application will be unavailable.

Normally, a complete rewrite can be accomplished with small projects, projects that don’t change frequently, or applications that are not so critical for our business. 

### Fast Migration

Another approach is dividing the application into parts or pieces. We migrate the app part by part, and we release those parts when they are ready. So, we have migrated parts of our application available for the users, and coexisting with our existing production app. 

With this gradual migration, we deliver separated features of our project in a faster way to the users, since we don’t have to wait for the complete application to be re-written. We also get faster feedback from the users, which allows us to detect bugs or issues earlier.

But a gradual migration drives us to have different tools, libraries, dependencies, and frameworks. Or we could even have to support different versions from the same tool. This extended support could bring conflicts to our application. 

We could even have problems if we are applying policies in the global scope since each one of the migrated parts could work in a different way, but being affected by the code that set global parameters to our system. An example of this is the use of a cascade logic for CSS styling.

Imagine we work with different versions of jQuery across our web application because we added functionalities from newer versions to the modules that have been created later. How complicated would it be to migrate all our app to a newer version of jQuery? Now, imagine the same scenario but migrating to a completely different framework like Next.js. That can be complicated.

{{% ad-panel-leaderboard %}}

### Frankenstein Migration

Denys Mishunov wrote an article on Smashing Magazine presenting an alternative to these two migration ideas, trying to get the best of the previous two approaches: [The Frankenstein Migration](https://www.smashingmagazine.com/2019/09/frankenstein-migration-framework-agnostic-approach-part-1/). It bases the migration process in two main components: [Microservices](https://aws.amazon.com/microservices/) and [Web Components](https://www.webcomponents.org/introduction). 

The migration process consists of a list of steps to follow:

#### 1. Identify Microservices

Based on our app code, we should divide it into independent parts that are dedicated to one small job. If we are thinking about using React or Next.js, we could link the concept of microservices to the different components that we have.

Let’s think about a grocery list application as an example. We have a list of things to purchase, and an input to add more things to the list. So, if we want to split our app into small parts, we could think about an “item list” component and an “add item”. Doing this, we can separate the functionality and markup related to each one of those parts into different React components.

To corroborate the components are independent, we should be able to remove one of them from the app, and the other ones shouldn’t be affected by that. If we get an error when removing the markup and functionality from a service, we are not correctly not identifying the components, or we need to refactor the way our code works.

#### 2. Allow Host-to-Alien Access

"Host" is our existing application. “Alien” is the one we will start creating, with the new framework. Both should work independently, but we should provide access from Host to Alien. We should be able to deploy any of the two applications without breaking the other one, but keeping the communication between them.

#### 3. Write An Alien Component

Re-write a service from our Host application into our Alien application, using the new framework. The component should follow the same principle of independence that we mentioned before.

Let’s go back to the grocery list example. We identified an “add item” component. With jQuery, the markup of the component will look something like this:

<pre><code class="language-javascript">&lt;input class="new-item" /&gt;</code></pre>

And the JavaScript/jQuery code to add the items to the list will be something like this: 

<pre><code class="language-javascript">var ENTER_KEY = 13;

$('.new-item').on('keyup', function (e) {
  var $input = $(e.target);
  var val = $input.val().trim();

  if (e.which !== ENTER_KEY || !val) {
    return;
  }

  // code to add the item to the list

  $input.val('');
});</code></pre>

Instead of that, we can create an `AddItem` React component:

<pre><code class="language-javascript">import React from 'react'

function AddItemInput({ defaultText }) {
  let [text, setText] = useState(defaultText)

  let handleSubmit = e => {
    e.preventDefault()
    if (e.which === 13) {
      setText(e.target.value.trim())
    }
  }

  return 
    &lt;input type="text" 
      value={text} 
      onChange={(e) =&gt; setText(e.target.value)} onKeyDown={handleSubmit} /&gt;
}
</code></pre>

#### 4. Write Web Component Wrapper Around Alien Service

Create a wrapper component that imports our just created Alien service and renders it. The idea is to create a bridge between the Host app and the Alien app. Keep in mind that we could need a package bundler to generate JavaScript code that works in our current application since we will need to copy our new React components and make them work.

Following the grocery list example, we can create an `AddItem-wrapper.js` file in the Host project. This file will contain the code that wraps our already created `AddItem` component, and creates a [custom element](https://developer.mozilla.org/en-US/docs/Web/Web_Components/Using_custom_elements) with it:

<div class="break-out">

<pre><code class="language-javascript">import React from "../alien/node_modules/react";
import ReactDOM from "../alien/node_modules/react-dom";
import AddItem from "../alien/src/components/AddItem";

class FrankensteinWrapper extends HTMLElement {
  connectedCallback() {
    const appWrapper = document.createElement("div");
    appWrapper.classList.add("grocerylistapp");

    ...

    ReactDOM.render(
      &lt;HeaderApp /&gt;,
      appWrapper
    );

    …

  }
}

customElements.define("frankenstein-add-item-wrapper", FrankensteinWrapper);</code></pre>
</div>

We should bring the necessary node modules and components from the Alien application folders since we need to import them to make the component work.

#### 5. Replace Host Service With Web Component

This wrapper component will replace the one in the Host application, and we will start using it. So, the application in production will be a mix of Host components and Alien wrapped components.

In our example Host application, we should replace:

<pre><code class="language-javascript">&lt;input class="new-item" /&gt;</code></pre>

With

<div class="break-out">

<pre><code class="language-javascript">&lt;frankenstein-add-item-wrapper&gt;&lt;/frankenstein-add-item-wrapper&gt; 

... 

&lt;script type="module" src="js/AddItem-wrapper.js"&gt;&lt;/script&gt;</code></pre>
</div>

#### 6. Rinse And Repeat

Go through steps 3, 4, and 5 for each one of the identified microservices.

#### 7. Switch To Alien

Host is now a collection of wrapper components that include all the web components we created on the Alien application. As we converted all the identified microservices, we can say that the Alien application is finished and all the services were migrated. We just need to point our users to the Alien application now.

The Frankenstein Migration method works as a combination of both the Good and the Fast approaches. We migrate the complete application but release the different components when they are done. So, they are available to be used sooner and evaluated by the users in production.

We have to consider, though, that we are doing some over-work with this approach. If we want to use the components we create for our Alien application, we have to create a wrapper component to include in the Host app. This makes us spend time developing the code for these wrapper elements. Also, by using them in our Host application, we are duplicating the inclusion of code and dependencies, and adding code that will affect the performance of our application.

### Strangler Application

Another approach we can take is the [Legacy Application Strangulation](https://paulhammant.com/2013/07/14/legacy-application-strangulation-case-studies/). We identify the edges of our existing web application, and whenever we need to add functionalities to our app we do it using a newer framework until the old system is “strangled”. This approach helps us to reduce the potential risk we can experiment while migrating an app.

To follow this approach, we need to identify different components, as we do in Frankenstein Migration. Once we divide our app into different pieces of related imperative code, we wrap them in new React components. We don’t add any additional behavior, we just create React components that render our existing content.

Let’s see an example for more clarification. Suppose we have this HTML code in our application:

<pre><code class="language-html">&lt;div class="accordion"&gt;
  &lt;div class="accordion-panel"&gt;
    &lt;h3 class="accordion-header"&gt;Item 1&lt;/h3&gt;
    &lt;div class="accordion-body"&gt;Text 1&lt;/div&gt;
  &lt;/div&gt;
  &lt;div class="accordion-panel"&gt;
    &lt;h3 class="accordion-header"&gt;Item 2&lt;/h3&gt;
    &lt;div class="accordion-body"&gt;Text 2&lt;/div&gt;
  &lt;/div&gt;
  &lt;div class="accordion-panel"&gt;
    &lt;h3 class="accordion-header"&gt;Item 3&lt;/h3&gt;
    &lt;div class="accordion-body"&gt;Text 3&lt;/div&gt;
  &lt;/div>&gt;
&lt;/div&gt;</code></pre>

And this JavaScript code (we already replaced jQuery functions with new JavaScript standard features).

<div class="break-out">

<pre><code class="language-javascript">const accordions = document.querySelectorAll(".accordion");
for (const accordion of accordions) {
  const panels = accordion.querySelectorAll(".accordion-panel");
  for (const panel of panels) {
    const head = panel.querySelector(".accordion-header");
    head.addEventListener('click', () =&gt; {
      for (const otherPanel of panels) {
        if (otherPanel !== panel) {
          otherPanel.classList.remove('accordion-expanded');
        }
      }
      panel.classList.toggle('accordion-expanded');
    });
  }
}</code></pre>
</div>

This is a common implementation of an `accordion` component for JavaScript. As we want to introduce React here, we need to wrap our existing code with a new React component: 

<div class="break-out">

<pre><code class="language-javascript">function Accordions() {
  useEffect(() =&gt; {
    const accordions = document.querySelectorAll(".accordion")
    for (const accordion of accordions) {
      const panels = accordion.querySelectorAll(".accordion-panel")
      for (const panel of panels) {
        const head = panel.querySelector(".accordion-header")
        head.addEventListener("click", () =&gt; {
          for (const otherPanel of panels) {
            if (otherPanel !== panel) {
              otherPanel.classList.remove("accordion-expanded")
            }
          }
          panel.classList.toggle("accordion-expanded")
        });
      }
    }
  }, [])

  return null
}

ReactDOM.render(&lt;Accordions /&gt;, document.createElement("div"))
</code></pre>
</div>

The component is not adding any new behavior or feature. We use `useEffect` because the component has been mounted in the document. That is why the function returns null because the hook doesn’t need to return a component.

So, we didn’t add any new functionality to our existing app, but we introduced React without changing its behavior. From now on, whenever we add new features or changes to our code, we will do it using the newer selected framework.

### Client-side Rendering, Server-side Rendering, Or Static Generation?

Next.js gives us the possibility of choosing how we want to render each page of our web application. We can use the client-side rendering that React already offers us to generate the content directly in the user’s browser. Or, we can render the content of our page in the server using [server-side rendering](https://nextjs.org/docs/basic-features/pages#server-side-rendering). Finally, we can create the content of our page at build time using [static generation](https://nextjs.org/docs/basic-features/pages#static-generation-recommended).

In our application, we should be loading and rendering code on page load, before we start interacting with any JavaScript library or framework. We may be using a server-side rendering programming language or technology, such as ASP.NET, PHP, or Node.js. We can get advantage of Next.js features and replace our current rendering method with the **Next.js server-side rendering method**. Doing this, we keep all the behavior inside the same project, that works under the umbrella of our selected framework. Also, we keep the logic of our main page and the React components within the same code that generates all the needed content for our page.

Let’s think about a dashboard page as an example. We can generate all the initial markup of the page at load time, in the server, instead of having to generate it with React in the user’s web browser.

<div class="break-out">

<pre><code class="language-javascript">const DashboardPage = ({ user }) =&gt; {
  return (
    &lt;div&gt;
       &lt;h2&gt;{user.name}&lt;/h2&gt;

       // User data

    &lt;/div&gt;
  )
}

export const getServerSideProps = async ({ req, res, params }) =&gt; {
    return {
      props: {
        user: getUser(),
      },
    }
  },
})

export default DashboardPage</code></pre>
</div>

If the markup that we render on page load is predictable and is based on data that we can retrieve at build time, static generation would be a good choice. **Generating static assets at build time** will make our application faster, more secure, scalable, and easier to maintain. And, in case we need to generate dynamic content on the pages of our app, we can use React’s client-side rendering to retrieve information from services or data sources.

Imagine we have a blog site, with many blog posts. If we use Static Generation, we can create a generic `[blog-slug].js` file in our Next.js application, and adding the following code we would generate all the static pages for our blog posts at build time.

<pre><code class="language-javascript">export const getStaticPaths = async () =&gt; {
  const blogPosts = await getBlogPosts()

  const paths = blogPosts.map(({ slug }) =&gt; ({
    params: {
      slug,
    },
  }))

  return {
    paths,
    fallback: false,
  }
}

export const getStaticProps = async ({ params }) =&gt; {
  const { slug } = params

  const blogPost = await getBlogPostBySlug(slug)

  return {
    props: {
      data: JSON.parse(JSON.stringify(blogPost)),
    },
  }
}</code></pre>

### Create An API Using API Routes

One of the great features Next.js offers is the possibility to create [API Routes](https://nextjs.org/docs/api-routes/introduction). With them, we can create our own serverless functions using Node.js. We can also install NPM packages to extend the functionality. A cool thing about this is that our API will leave in the same project/app as our frontend, so we won’t have any CORS issues.

If we maintain an API that is called from our web application using jQuery AJAX functionality, we could replace them using **API Routes**. Doing this, we will keep all the codebase of our app in the same repository, and we will make the deployment of our application simpler. If we are using a third-party service, we can use API Routes to “mask” the external URLs.

We could have an API Route `/pages/api/get/[id].js` that returns data that we use on our page.

<pre><code class="language-javascript">export default async (req, res) =&gt; {
  const { id } = req.query

  try {
    const data = getData(id)
    res.status(200).json(data)
  } catch (e) {
    res.status(500).json({ error: e.message })
  }
}</code></pre>

And call it from the code of our page.

<pre><code class="language-javascript"> const res = await fetch(`/api/get/${id}`, {
    method: 'GET',
  })

  if (res.status === 200) {
    // Do something
  } else {
    console.error(await res.text())
  }</code></pre>

{{% ad-panel-leaderboard %}}

## Deploy to Netlify

[Netlify](https://www.netlify.com/) is a complete platform that can be used to automate, manage, build, test, deploy and host web applications. It has a lot of features that make modern web application development easier and faster. Some Netlify highlights are:

- Global CDN hosting platform,
- Serverless functions support,
- Deploy previews based on Github Pull Requests,
- Webhooks,
- Instant rollbacks,
- Role-based access control.

Netlify is a great platform to manage and host our Next.js applications, and it’s pretty simple to deploy a web app with it. 

First of all, we need to **keep track of our Next.js app code** in a Git repository. Netlify connects to GitHub (or the Git platform we prefer), and whenever a change is introduced to a branch (a commit or a Pull Request), an automatic “build and deploy” task will be triggered.

Once we have a Git repository with the code of our app, we need to create a “Netlify Site” for it. To do this, we have two options:

1. [Using Netlify CLI](https://docs.netlify.com/cli/get-started/)  
After we install the CLI (`npm install -g netlify-cli`) and log into our Netlify account (`ntl login`), we can go to the root directory of our application, run `ntl init` and follow the steps.
2. [Using Netlify web app](https://app.netlify.com/start)  
We should go to [https://app.netlify.com/start](https://app.netlify.com/start). Connect to our Git provider, choose our application’s repository from the list, configure some build options, and deploy.

For both methods, we have to consider that our build command will be `next build` and our directory to deploy is `out`.

Finally, the [Essential Next.js](https://app.netlify.com/plugins/@netlify/plugin-nextjs/install) plugin is installed automatically, which will allow us to deploy and use API routes, dynamic routes, and Preview Mode. And that's it, we have our Next.js application up and running in a fast and stable CDN hosting service.

## Conclusion

In this article, we evaluated websites using jQuery library, and we compared them with new frontend frameworks like React and Next.js. We defined how we could start a migration, in case it benefits us, to a newer tool. We evaluated different migration strategies and we saw some examples of scenarios that we could migrate to Next.js web application projects. Finally, we saw how to deploy our Next.js application to Netlify and get it up and running.

### Further Reading and Resources

- [Frankenstein Migration: Framework-Agnostic Approach](https://www.smashingmagazine.com/2019/09/frankenstein-migration-framework-agnostic-approach-part-1/)
- [Removing jQuery from GitHub.com frontend](https://github.blog/2018-09-06-removing-jquery-from-github-frontend/ )
- [Getting Started with Next.js](https://nextjs.org/docs/getting-started)
- [How to Deploy Next.js Sites to Netlify](https://www.netlify.com/blog/2020/11/30/how-to-deploy-next.js-sites-to-netlify/)
- [Next.js articles in Netlify Blog](https://www.netlify.com/tags/nextjs/)

{{< signature "vf, yk, il" >}}
