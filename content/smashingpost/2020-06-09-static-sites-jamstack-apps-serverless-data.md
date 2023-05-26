---
title: 'From Static Sites To End User Jamstack Apps With FaunaDB'
slug: static-sites-jamstack-apps-faunadb
author: bryan-robinson
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bd32e23e-a172-48a1-bff2-3f9001a3b2fc/faunadb-serverless-function-flow-full.png
date: 2020-06-09T12:00:00.000Z
summary: >-
  To make the move from “site” to app, we’ll need to dive into the world of “app-generated” content. In this article, we’ll get started in this world with the power of serverless data. We’ll start with a simple demo by ingesting and posting data to <a href="https://synd.co/2XBbr4W">FaunaDB</a> and then extend that functionality in a full-fledged application using Auth0, FaunaDB’s Token system and User-Defined Functions.
description: >-
  In this article, we’ll start with a simple demo by ingesting and posting data to <a href="https://synd.co/2XBbr4W">FaunaDB</a> and then extend that functionality in a full-fledged app using Auth0, FaunaDB’s Token system and User-Defined Functions.
categories:
  - Apps
  - API
  - Tools
  - Jamstack
  - Serverless
disable_ads: true
disable_panels: true
disable_newsletterbox: true
sponsor:
  title: FaunaDB
  link: https://fauna.com/
  image: https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4607f14f-f163-4295-a1ea-765a36fbdba7/fauna-logo-blue-200x200.png
  description: >-
    This article has been kindly supported by our dear friends at <a href="https://synd.co/2XBbr4W" style="text-shadow: none;">FaunaDB</a>, a global serverless database that gives you ubiquitous, low latency access to app data, without sacrificing data correctness and scale. <em>Thank you!</em>
---

<p>The JAMstack has proven itself to be one of the top ways of producing content-driven sites, but it’s also a great place to house applications, as well. If you’ve been using the JAMstack for your performant websites, the demos in this article will help you extend those philosophies to applications as well.</p>

<p>When using the JAMstack to build applications, you need a data service that fits into the most important aspects of the JAMstack philosophy:</p>

<ul>
<li>Global distribution</li>
<li>Zero operational needs</li>
<li>A developer-friendly API.</li>
</ul>

<p>In the JAMstack ecosystem there are plenty of software-as-a-service companies that provide ways of getting and storing specific types of data. Whether you want to send emails, SMS or make phone calls (Twilio) or accept form submissions efficiently (Formspree, Formingo, Formstack, etc.), it seems there’s an API for almost everything.</p>

<p>These are great services that can do a lot of the low-level work of many applications, but once your data is more complex than a spreadsheet or needs to be updated and store in real-time, it might be time to look into a database.</p>

<p>The service API can still be in use, but a central database managing the state and operations of your app becomes much more important. Even if you need a database, you still want it to follow the core JAMstack philosophies we outlined above. That means, we don’t want to host our own database server. We need a Database-as-a-Service solution. Our database needs to be optimized for the JAMstack:</p>

<ul>
<li>Optimized for API calls from a browser or build process.
<li>Flexible to model your data in the specific ways your app needs.</li>
<li>Global distribution of our data like a CDN houses our sites.</li>
<li>Hands-free scaling with no need of a database administrator or developer intervention.</li>
</ul>

<p>Whatever service you look into needs to follow these tenets of serverless data. In our demos, we’ll explore <a href="https://synd.co/2XBbr4W">FaunaDB</a>, a global serverless database, featuring native GraphQL to assure that we keep our apps in step with the philosophies of the JAMstack.</p>

<p>Let’s dive into the code!</p>

## A JAMstack Guestbook App With Gatsby And Fauna

<p>I’m a <a href="https://bryanlrobinson.com/blog/bring-fansites-back-to-the-web/">big fan</a> of reimagining the internet tools and concepts of the 1990s and early 2000s. We can take these concepts and make them feel fresh with the new set of tools and interactions.</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0d41e9d0-1bdc-46a3-b57e-25440249e6f5/faunadb-guestbook-form-and-signature-full.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0d41e9d0-1bdc-46a3-b57e-25440249e6f5/faunadb-guestbook-form-and-signature-full.png" sizes="100vw" caption="A look at the app we’re creating. A signature form with a signature list below. The form will populate a FaunaDB database and that database will create the view list. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0d41e9d0-1bdc-46a3-b57e-25440249e6f5/faunadb-guestbook-form-and-signature-full.png'>Large preview</a>)" alt="guestbook-form-and-signature" >}}

<p>In this demo, we’ll create an application that was all the rage in that time period: the guestbook. A guestbook is nothing but app-generated content and interaction. A user can come to the site, see all the signatures of past “guests” and then leave their own.</p>

<p>To start, we’ll statically render our site and build our data from Fauna during our build step. This will provide the fast performance we expect from a JAMstack site. To do this, we’ll use GatsbyJS.</p>

### Initial setup

<p>Our first step will be to install Gatsby globally on our computer. If you’ve never spent much time in the command line, <a href="https://www.gatsbyjs.org/tutorial/part-zero/">Gatsby’s “part 0” tutorial</a> will help you get up and running. If you already have Node and NPM installed, you’ll install the Gatsby CLI globally and create a new site with it using the following commands:</p>

<pre><code class="language-bash">npm install -g gatsby-cli</code></pre>

<pre><code class="language-bash">gatsby new &lt;directory-to-install-into&gt; &lt;starter&gt;</code></pre>

Gatsby comes with a large repository of starters that can help bootstrap your project. For this demo, I chose a simple starter that came equipped with the Bulma CSS framework.

<div class="break-out">

<pre><code class="language-css">gatsby new guestbook-app https://github.com/amandeepmittal/gatsby-bulma-quickstart</code></pre>
</div>

<p>This gives us a good starting point and structure. It also has the added benefit of coming with styles that are ready to go.</p>

<p>Let’s do a little cleanup for things we don’t need. We’ll start by simplifying our <code>components.header.js</code></p>

<div class="break-out">

 <pre><code class="language-javascript">import React from 'react';

import './style.scss';

const Header = ({ siteTitle }) =&gt; (
  &lt;section className="hero gradientBg "&gt;
    &lt;div className="hero-body"&gt;
      &lt;div className="container container--small center"&gt;
        &lt;div className="content"&gt;
          &lt;h1 className="is-uppercase is-size-1 has-text-white"&gt;
            Sign our Virtual Guestbook
          &lt;/h1&gt;
          &lt;p className="subtitle has-text-white is-size-3"&gt;
            If you like all the things that we do, be sure to sign our virtual guestbook
          &lt;/p&gt;
        &lt;/div&gt;
      &lt;/div&gt;
    &lt;/div&gt;
  &lt;/section&gt;
);

export default Header;
</code></pre>
</div>

<p>This will get rid of much of the branded content. Feel free to customize this section, but we won’t write any of our code here.</p>

<p>Next we’ll clean out the <code>components/midsection.js</code> file. This will be where our app’s code will render.</p>

<div class="break-out">

 <pre><code class="language-javascript">import React, { useState } from 'react';
import Signatures from './signatures';
import SignForm from './sign-form';


const Midsection = () =&gt; {

    const [sigData, setSigData] = useState(data.allSignatures.nodes);
    return (
        &lt;section className="section"&gt;
            &lt;div className="container container--small"&gt;
                &lt;section className="section is-small"&gt;
                    &lt;h2 className="title is-4"&gt;Sign here&lt;/h2&gt;
                    &lt;SignForm&gt;&lt;/SignForm&gt;
                &lt;/section&gt;

                &lt;section className="section"&gt;
                    &lt;h2 className="title is-5"&gt;View Signatures&lt;/h2&gt;
                    &lt;Signatures&gt;&lt;/Signatures&gt;
                &lt;/section&gt;
            &lt;/div&gt;
        &lt;/section&gt;
    )
}

export default Midsection;
</code></pre>
</div>

<p>In this code, we’ve mostly removed the “site” content and added in a couple new components. A <code>&lt;SignForm&gt;</code> that will contain our form for submitting a signature and a <code>&lt;Signatures&gt;</code> component to contain the list of signatures.</p>

<p>Now that we have a relatively blank slate, we can set up our FaunaDB database.</p>


### Setting Up A FaunaDB Collection

After logging into Fauna (or signing up for an account), you’ll be given the option to create a new Database. We’ll create a new database called `guestbook`.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/08d2ffa1-9f49-4ce3-a733-425536df5b16/faunadb-signatures-collection-full.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/08d2ffa1-9f49-4ce3-a733-425536df5b16/faunadb-signatures-collection-full.png" sizes="100vw" caption="The initial state of our signatures Collection after we add our first Document. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/08d2ffa1-9f49-4ce3-a733-425536df5b16/faunadb-signatures-collection-full.png'>Large preview</a>)" alt="signatures Collection" >}}

Inside this database, we’ll create a “Collection” called `signature`. Collections in Fauna a group of Documents that are in turn JSON objects.

In this new Collection, we’ll create a new Document with the following JSON:

<div class="break-out">

<pre><code class="language-javascript">{
 name: "Bryan Robinson",
 message:
   "Lorem ipsum dolor amet sum Lorem ipsum dolor amet sum Lorem ipsum dolor amet sum Lorem ipsum dolor amet sum"
}</code></pre>
</div>

This will be the simple data schema for each of our signatures. For each of these Documents, Fauna will create additional data surrounding it.

<div class="break-out">

<pre><code class="language-javascript">{
 "ref": Ref(Collection("signatures"), "262884172900598291"),
 "ts": 1586964733980000,
 "data": {
   "name": "Bryan Robinson",
   "message": "Lorem ipsum dolor amet sum Lorem ipsum dolor amet sum Lorem ipsum dolor amet sum Lorem ipsum dolor amet sum "
 }
}</code></pre>
</div>

The `ref` is the unique identifier inside of Fauna and the `ts` is the time (as a Unix timestamp) the document was created/updated.

After creating our data, we want an easy way to grab all that data and use it in our site. In Fauna, the most efficient way to get data is via an Index. We’ll create an Index called `allSignatures`. This will grab and return all of our signature Documents in the Collection.

Now that we have an efficient way of accessing the data in Gatsby, we need Gatsby to know where to get it. Gatsby has a repository of plugins that can fetch data from a variety of sources, Fauna included.

### Setting up the Fauna Gatsby Data Source Plugin

<pre><code class="language-bash">npm install gatsby-source-faunadb</code></pre>

After we install this plugin to our project, we need to configure it in our `gatsby-config.js` file. In the `plugins` array of our project, we’ll add a new item.

<div class="break-out">

 <pre><code class="language-javascript">{
    resolve: `gatsby-source-faunadb`,
    options: {
    // The secret for the key you're using to connect to your Fauna database.
    // You can generate on of these in the "Security" tab of your Fauna Console.
        secret: process.env.YOUR_FAUNADB_SECRET,
    // The name of the index you want to query
    // You can create an index in the "Indexes" tab of your Fauna Console.
        index: `allSignatures`,
    // This is the name under which your data will appear in Gatsby GraphQL queries
    // The following will create queries called `allBird` and `bird`.
        type: "Signatures",
    // If you need to limit the number of documents returned, you can specify a 
    // Optional maximum number to read.
    // size: 100
    },
},
</code></pre>
</div>

<p class="c-pre-sidenote--left">In this configuration, you provide it your Fauna secret Key, the Index name we created and the “type” we want to access in our Gatsby GraphQL query.</p><p class="c-sidenote c-sidenote--right">Where did that <code>process.env.YOUR_FAUNADB_SECRET</code> come from?</p>

In your project, create a `.env` file &mdash; and include that file in your .gitignore! This file will give Gatsby’s Webpack configuration the secret value.  This will keep your sensitive information safe and not stored in GitHub.

<pre><code class="language-javascript">YOUR_FAUNADB_SECRET = "value from fauna"</code></pre>

*We can then head over to the “Security” tab in our Database and create a new key. Since this is a protected secret, it’s safe to use a “Server” role. When you save the Key, it’ll provide your secret. Be sure to grab that now, as you can’t get it again (without recreating the Key).*

Once the configuration is set up, we can write a GraphQL query in our components to grab the data at build time.

### Getting the data and building the template

We’ll add this query to our Midsection component to make it accessible by both of our components.

<pre><code class="language-javascript">const Midsection = () => {
 const data = useStaticQuery(
 graphql`
            query GetSignatures {
                allSignatures {
                  nodes {
                    name
                    message
                    _ts
                    _id
                  }
                }
            }`
        );
// ... rest of the component
}</code></pre>

This will access the `Signatures` type we created in the configuration. It will grab all the signatures and provide an array of nodes. Those nodes will contain the data we specify we need: `name`, `message`, `ts`, `id`.

We’ll set that data into our state &mdash; this will make updating it live easier later.

<pre><code class="language-javascript">const [sigData, setSigData] = useState(data.allSignatures.nodes);</code></pre>

Now we can pass `sigData` as a prop into `<Signatures>` and `setSigData` into `<SignForm>`.

<pre><code class="language-javascript">&lt;SignForm setSigData={setSigData}&gt;&lt;/SignForm&gt;


&lt;Signatures sigData={sigData}&gt;&lt;/Signatures&gt;</code></pre>

Let’s set up our Signatures component to use that data!

<div class="break-out">

 <pre><code class="language-javascript">import React from 'react';
import Signature from './signature'   

const Signatures = (props) =&gt; {
    const SignatureMarkup = () =&gt; {
        return props.sigData.map((signature, index) =&gt; {
            return (
                &lt;Signature key={index} signature={signature}&gt;&lt;/Signature&gt;
            )
        }).reverse()
    }

    return (
        &lt;SignatureMarkup&gt;&lt;/SignatureMarkup&gt;
    )
}

export default Signatures
</code></pre>
</div>

In this function, we’ll `.map()` over our signature data and create an Array of markup based on a new `<Signature>` component that we pass the data into.

The `Signature` component will handle formatting our data and returning an appropriate set of HTML.

<div class="break-out">

 <pre><code class="language-javascript">import React from 'react';

const Signature = ({signature}) =&gt; {
    const dateObj = new Date(signature.&#95;ts / 1000);
    let dateString = `${dateObj.toLocaleString('default', {weekday: 'long'})}, ${dateObj.toLocaleString('default', { month: 'long' })} ${dateObj.getDate()} at ${dateObj.toLocaleTimeString('default', {hour: '2-digit',minute: '2-digit', hour12: false})}`

    return (
    &lt;article className="signature box"&gt;      
        &lt;h3 className="signature__headline"&gt;{signature.name} - {dateString}&lt;/h3&gt;
        &lt;p className="signature__message"&gt;
            {signature.message} 
        &lt;/p&gt;
    &lt;/article&gt;
)};

export default Signature;
</code></pre>
</div>

At this point, if you start your Gatsby development server, you should have a list of signatures currently existing in your database. Run the following command to get up and running:

<pre><code class="language-bash">gatsby develop</code></pre>

Any signature stored in our database will build HTML in that component. But how can we get signatures INTO our database?

Let’s set up a signature form component to send data and update our Signatures list.

### Let’s Make Our JAMstack Guestbook Interactive

First, we’ll set up the basic structure for our component. It will render a simple form onto the page with a text input, a textarea, and a button for submission.

<div class="break-out">

 <pre><code class="language-javascript">import React from 'react';

import faunadb, { query as q } from "faunadb"

var client = new faunadb.Client({ secret: process.env.GATSBY_FAUNA_CLIENT_SECRET  })

export default class SignForm extends React.Component {
    constructor(props) {
        super(props)
        this.state = {
            sigName: "",
            sigMessage: ""
        }
    }

    handleSubmit = async event =&gt; {
        // Handle the submission
    }

    handleInputChange = event =&gt; {
        // When an input changes, update the state
    }

    render() {
        return (
            &lt;form onSubmit={this.handleSubmit}&gt;
                &lt;div className="field"&gt;
                    &lt;div className="control"&gt;
                 &lt;label className="label"&gt;Label
                    &lt;input 
                        className="input is-fullwidth"
                        name="sigName" 
                        type="text"
                        value={this.state.sigName}
                        onChange={this.handleInputChange}
                    /&gt;
                    &lt;/label&gt;
                    &lt;/div&gt;
                &lt;/div&gt;
                &lt;div className="field"&gt;
                    &lt;label&gt;
                        Your Message:
                        &lt;textarea 
                            rows="5"
                            name="sigMessage" 
                            value={this.state.sigMessage}
                            onChange={this.handleInputChange} 
                            className="textarea" 
                            placeholder="Leave us a happy note"&gt;&lt;/textarea&gt;

                    &lt;/label&gt;
                &lt;/div&gt;
                &lt;div className="buttons"&gt;
                    &lt;button className="button is-primary" type="submit"&gt;Sign the Guestbook&lt;/button&gt;
                &lt;/div&gt;
            &lt;/form&gt;
        )
    }

}
</code></pre>
</div>

To start, we’ll set up our state to include the name and the message. We’ll default them to blank strings and insert them into our `<textarea>` and `<input>`.

When a user changes the value of one of these fields, we’ll use the `handleInputChange` method. When a user submits the form, we’ll use the `handleSubmit` method.

Let’s break down both of those functions.

<pre><code class="language-javascript">  handleInputChange = event => {
 const target = event.target
 const value = target.value
 const name = target.name
 this.setState({
            [name]: value,
        })
    }
</code></pre>

The input change will accept the event. From that event, it will get the current target’s value and name. We can then modify the state of the properties on our state object &mdash; sigName, sigMessage or anything else.

Once the state has changed, we can use the state in our `handleSubmit` method.

<div class="break-out">

<pre><code class="language-javascript">  handleSubmit = async event => {
        event.preventDefault();
 const placeSig = await this.createSignature(this.state.sigName, this.state.sigMessage);
 this.addSignature(placeSig);
    }
</code></pre>
</div>

This function will call a new `createSignature()` method. This will connect to Fauna to create a new Document from our state items.

The `addSignature()` method will update our Signatures list data with the response we get back from Fauna.

In order to write to our database, we’ll need to set up a new key in Fauna with minimal permissions. Our server key is allowed higher permissions because it’s only used during build and won’t be visible in our source.

This key needs to only allow for the ability to only create new items in our `signatures` collection.

**Note**: *A user could still be malicious with this key, but they can only do as much damage as a bot submitting that form, so it’s a trade-off I’m willing to make for this app.*

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1f03d579-5844-44fa-9dc0-7262821a0979/faunadb-signatures-permissions-full.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1f03d579-5844-44fa-9dc0-7262821a0979/faunadb-signatures-permissions-full.png" sizes="100vw" caption="A look at the FaunaDB security panel. In this shot, we’re creating a 'client' role that allows only the 'Create' permission for those API Keys. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1f03d579-5844-44fa-9dc0-7262821a0979/faunadb-signatures-permissions-full.png'>Large preview</a>)" alt="signatures-client-permissions" >}}

For this, we’ll create a new “Role” in the “Security” tab of our dashboard. We can add permissions around one or more of our Collections. In this demo, we only need `signatures` and we can select the “Create” functionality.

After that, we generate a new key that uses that role.

To use this key, we’ll instantiate a new version of the Fauna JavaScript SDK. This is a dependency of the Gatsby plugin we installed, so we already have access to it.

<div class="break-out">

<pre><code class="language-javascript">import faunadb, { query as q } from "faunadb"

var client = new faunadb.Client({ secret: process.env.GATSBY_FAUNA_CLIENT_SECRET })</code></pre>
</div>

By using an environment variable prefixed with `GATSBY_`, we gain access to it in our browser JavaScript (be sure to add it to your `.env` file).

By importing the `query` object from the SDK, we gain access to any of the methods available in Fauna’s first-party Fauna Query Language (FQL). In this case, we want to use the Create method to create a new document on our Collection.

<div class="break-out">

<pre><code class="language-javascript">createSignature = async (sigName, sigMessage) =&gt; {
 try {
 const queryResponse = await client.query(
                q.Create(
                    q.Collection('signatures'),
                    { 
                        data: { 
                            name: sigName,
                            message: sigMessage
                        } 
                    }
                )
            )
 const signatureInfo = { name: queryResponse.data.name, message: queryResponse.data.message, _ts: queryResponse.ts, _id: queryResponse.id}
 return signatureInfo
        } catch(err) {
            console.log(err);
        }
    }</code></pre>
</div>

We pass the Create function to the `client.query()` method. Create takes a Collection reference and an object of information to pass to a new Document. In this case, we use `q.Collection` and a string of our Collection name to get the reference to the Collection. The second argument is for our data. You can pass other items in the object, so we need to tell Fauna, we’re specifically sending it the `data` property on that object.

Next, we pass it the name and message we collected in our state. The response we get back from Fauna is the entire object of our Document. This includes our data in a `data` object, as well as a Fauna ID and timestamp. We reformat that data in a way that our Signatures list can use and return that back to our `handleSubmit` function.

Our submit handler will then pass that data into our `setSigData` prop which will notify our Signatures component to rerender with that new data. This gives our user immediate feedback that their submission has been accepted.

### Rebuilding the site

This is all working in the browser, but the data hasn’t been updated in our static application yet.

From here, we need to tell our JAMstack host to rebuild our site. Many have the ability to specify a webhook to trigger a deployment. Since I’m hosting this demo on Netlify, I can create a new “Deploy webhook” in their admin and create a new `triggerBuild` function. This function will use the native JavaScript `fetch()` method and send a post request to that URL. Netlify will then rebuild the application and pull in the latest signatures.

<div class="break-out">

<pre><code class="language-javascript">  triggerBuild = async () => {
 const response = await fetch(process.env.GATSBY_BUILD_HOOK, { method: "POST", body: "{}" });
 return response;
    }</code></pre>
</div>

<p><em>Both <a href="https://www.gatsbyjs.org/blog/2020-04-22-announcing-incremental-builds/">Gatsby Cloud</a> and <a href="https://www.netlify.com/blog/2020/04/23/enable-gatsby-incremental-builds-on-netlify/">Netlify</a> have implemented ways of handling “incremental” builds with Gatsby drastically speeding up build times. This sort of build can happen very quickly now and feel almost as fast as a traditional server-rendered site.</em>

<p><em>Every signature that gets added gets quick feedback to the user that it’s been submitted, is perpetually stored in a database, and served as HTML via a build process.</em></p>

Still feels a little too much like a typical website? Let’s take all these concepts a step further.

## Create A Mindful App With Auth0, Fauna Identity And Fauna User-Defined Functions (UDF)

Being mindful is an important skill to cultivate. Whether it’s thinking about your relationships, your career, your family, or just going for a walk in nature, it’s important to be mindful of the people and places around you.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9516d0ef-bb29-481e-8d10-f06248a60569/faunadb-mindful-mission-full.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9516d0ef-bb29-481e-8d10-f06248a60569/faunadb-mindful-mission-full.png" sizes="100vw" caption="A look at the final app screen showing a 'Mindful Mission,' 'Past Missions' and a 'Log Out' button. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9516d0ef-bb29-481e-8d10-f06248a60569/faunadb-mindful-mission-full.png'>Large preview</a>)" alt="Mindful Mission" >}}

This app intends to help you focus on one randomized idea every day and review the various ideas from recent days.

To do this, we need to introduce a key element to most apps: authentication. With authentication, comes extra security concerns. While this data won’t be particularly sensitive, you don’t want one user accessing the history of any other user.

Since we’ll be scoping data to a specific user, we also don’t want to store any secret keys on browser code, as that would open up other security flaws.

We could create an entire authentication flow using nothing but our wits and a user database with Fauna. That may seem daunting and moves us away from the features we want to write. The great thing is that there’s certainly an API for that in the JAMstack! In this demo, we’ll explore integrating Auth0 with Fauna. We can use the integration in many ways.

### Setting Up Auth0 To Connect With Fauna

Many implementations of authentication with the JAMstack rely heavily on Serverless functions. That moves much of the security concerns from a security-focused company like Auth0 to the individual developer. That doesn’t feel quite right.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bd32e23e-a172-48a1-bff2-3f9001a3b2fc/faunadb-serverless-function-flow-full.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bd32e23e-a172-48a1-bff2-3f9001a3b2fc/faunadb-serverless-function-flow-full.png" sizes="100vw" caption="A diagram outlining the convoluted method of using a serverless function to manage authentication and token generation. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bd32e23e-a172-48a1-bff2-3f9001a3b2fc/faunadb-serverless-function-flow-full.png'>Large preview</a>)" alt="serverless function flow" >}}

The typical flow would be to send a login request to a serverless function. That function would request a user from Auth0. Auth0 would provide the user’s JSON Web Token (JWT) and the function would provide any additional information about the user our application needs. The function would then bundle everything up and send it to the browser.

There are a lot of places in that authentication flow where a developer could introduce a security hole.

Instead, let’s request that Auth0 bundle everything up for us inside the JWT it sends. Keeping security in the hands of the folks who know it best.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9e77ff80-6fd4-496e-ad56-4119b9a2be1e/faunadb-auth0-rule-flow-full.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9e77ff80-6fd4-496e-ad56-4119b9a2be1e/faunadb-auth0-rule-flow-full.png" sizes="100vw" caption="A diagram outlining the streamlined authentication and token generation flow when using Auth0’s Rule system. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9e77ff80-6fd4-496e-ad56-4119b9a2be1e/faunadb-auth0-rule-flow-full.png'>Large preview</a>)" alt="Auth0’s Rule flow" >}}

We’ll do this by using Auth0’s Rules functionality to ask Fauna for a user token to encode into our JWT. This means that unlike our Guestbook, we won’t have any Fauna keys in our front-end code. Everything will be managed in memory from that JWT token.

### Setting up Auth0 Application and Rule

First, we’ll need to set up the basics of our Auth0 Application.

<p>Following <a href="https://auth0.com/docs/quickstart/spa/vanillajs#configure-auth0">the configuration steps</a> in their basic walkthrough gets the important basic information filled in. Be sure to fill out the proper localhost port for your bundler of choice as one of your authorized domains.</p>

After the basics of the application are set up, we’ll go into the “Rules” section of our account.

Click “Create Rule” and select “Empty Rule” (or start from one of their many templates that are helpful starting points).

Here’s our Rule code

<div class="break-out">

 <pre><code class="language-javascript">async function (user, context, callback) {
  const FAUNADB_SECRET = 'Your Server secret';
  const faunadb = require('faunadb@2.11.1');
  const { query: q } = faunadb;
  const client = new faunadb.Client({ secret: FAUNADB_SECRET });
  try {
    const token = await client.query(
      q.Call('user_login_or_create', user.email, user) // Call UDF in fauna
    );
    let newClient = new faunadb.Client({ secret: token.secret });

    context.idToken['https://faunadb.com/id/secret'] = token.secret;
    callback(null, user, context);
  } catch(error) {
    console.log('->', error);
    callback(error, user, context);
  }
}
</code></pre>
</div>

We give the rule a function that takes the user, context, and a callback from Auth0. We need to set up and grab a Server token to initialize our Fauna JavaScript SDK and initialize our client. Just like in our Guestbook, we’ll create a new Database and manage our Tokens in “Security”.

From there, we want to send a query to Fauna to create or log in our user. To keep our Rule code simple (and make it reusable), we’ll write our first Fauna “User-Defined Function” (UDF). A UDF is a function written in FQL that runs on Fauna’s infrastructure.

First, we’ll set up a Collection for our users. You don’t need to make a first Document here, as they’ll be created behind the scenes by our Auth0 rule whenever a new Auth0 user is created.

Next, we need an Index to search our `users` Collection based on the email address. This Index is simpler than our Guestbook, so we can add it to the Dashboard. Name the Index `user_by_email`, set the Collection to `users`, and the Terms to `data.email`. This will allow us to pass an email address to the Index and get a matching user Document back.

It’s time to create our UDF. In the Dashboard, navigate to “Functions” and create a new one named `user_login_or_create`.

<div class="break-out">

 <pre><code class="language-javascript">Query(
  Lambda(
    ["userEmail", "userObj"], // Arguments
    Let(
      { user: Match(Index("user_by_email"), Var("userEmail")) }, // Set user variable 
      If(
        Exists(Var("user")), // Check if the User exists
        Create(Tokens(null), { instance: Select("ref", Get(Var("user"))) }), // Return a token for that item in the users collection (in other words, the user)
        Let( // Else statement: Set a variable
          {
            newUser: Create(Collection("users"), { data: Var("userObj") }), // Create a new user and get its reference
            token: Create(Tokens(null), { // Create a token for that user
              instance: Select("ref", Var("newUser"))
            })
          },
          Var("token") // return the token
        )
      )
    )
  )
)
</code></pre>
</div>

Our UDF will accept a user email address and the rest of the user information. If a user exists in a `users` Collection, it will create a Token for the user and send that back. If a user doesn’t exist, it will create that user Document and then send a Token to our Auth0 Rule.

We can then store the Token as an `idToken` attached to the `context` in our JWT. The token needs a URL as a key. Since this is a Fauna token, we can use a Fauna URL. Whatever this is, you’ll use it to access this in your code.

This Token doesn’t have any permissions yet. We need to go into our Security rules and set up a new Role.

We’ll create an “AuthedUser” role. We don’t need to add any permissions yet, but as we create new UDFs and new Collections, we’ll update the permissions here. Instead of generating a new Key to use this Role, we want to add to this Role’s “Memberships”. On the Memberships screen, you can select a Collection to add as a member. The documents in this Collection (in our case, our Users), will have the permissions set on this role given via their Token.

Now, when a user logs in via Auth0, they’ll be returned a Token that matches their user Document and has its permissions.

From here, we come back to our application.

### Implement logic for when the User is logged in

Auth0 has an <a href="https://auth0.com/docs/quickstart/spa/vanillajs">excellent walkthrough for setting up a “vanilla” JavaScript single-page application</a>. Most of this code is a refactor of that to fit the code splitting of this application.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c9a57bc1-3f8d-425f-be67-3667e42c3956/faunadb-mindful-auth-full.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c9a57bc1-3f8d-425f-be67-3667e42c3956/faunadb-mindful-auth-full.png" sizes="100vw" caption="The default Auth0 Login/Signup screen. All the login flow can be contained in the Auth0 screens. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c9a57bc1-3f8d-425f-be67-3667e42c3956/faunadb-mindful-auth-full.png'>Large preview</a>)" alt="default Auth0 Login/Signup screen" >}}

First, we’ll need the Auth0 SPA SDK.

<pre><code class="language-bash">npm install @auth0/auth0-spa-js</code></pre>

<div class="break-out">

 <pre><code class="language-javascript">import createAuth0Client from '@auth0/auth0-spa-js';
import { changeToHome } from './layouts/home'; // Home Layout
import { changeToMission } from './layouts/myMind'; // Current Mindfulness Mission Layout

let auth0 = null;
var currentUser = null;
const configureClient = async () => {
    // Configures Auth0 SDK
    auth0 = await createAuth0Client({
      domain: "mindfulness.auth0.com",
      client_id: "32i3ylPhup47PYKUtZGRnLNsGVLks3M6"
    });
};

const checkUser = async () => {
    // return user info from any method
    const isAuthenticated = await auth0.isAuthenticated();
    if (isAuthenticated) {
        return await auth0.getUser();
    }
}

const loadAuth = async () => {
    // Loads and checks auth
    await configureClient();      
    
    const isAuthenticated = await auth0.isAuthenticated();
    if (isAuthenticated) {
        // show the gated content
        currentUser = await auth0.getUser();
        changeToMission(); // Show the "Today" screen
        return;
    } else {
        changeToHome(); // Show the logged out "homepage"
    }

    const query = window.location.search;
    if (query.includes("code=") && query.includes("state=")) {

        // Process the login state
        await auth0.handleRedirectCallback();
       
        currentUser = await auth0.getUser();
        changeToMission();

        // Use replaceState to redirect the user away and remove the querystring parameters
        window.history.replaceState({}, document.title, "/");
    }
}

const login = async () => {
    await auth0.loginWithRedirect({
        redirect_uri: window.location.origin
    });
}
const logout = async () => {
    auth0.logout({
        returnTo: window.location.origin
    });
    window.localStorage.removeItem('currentMindfulItem') 
    changeToHome(); // Change back to logged out state
}

export { auth0, loadAuth, currentUser, checkUser, login, logout }
</code></pre>
</div>

First, we configure the SDK with our client_id from Auth0. This is safe information to store in our code.

Next, we set up a function that can be exported and used in multiple files to check if a user is logged in. The Auth0 library provides an `isAuthenticated()` method. If the user is authenticated, we can return the user data with `auth0.getUser()`.

We set up a `login()` and `logout()` functions and a `loadAuth()` function to handle the return from Auth0 and change the state of our UI to the “Mission” screen with today’s Mindful idea.

Once this is all set up, we have our authentication and user login squared away.

We’ll create a new function for our Fauna functions to reference to get the proper token set up.

<div class="break-out">

 <pre><code class="language-javascript">const AUTH_PROP_KEY = "https://faunadb.com/id/secret";
var faunadb = require('faunadb'),
q = faunadb.query;

async function getUserClient(currentUser) {
    return new faunadb.Client({ secret: currentUser[AUTH_PROP_KEY]})
}
</code></pre>
</div>

This returns a new connection to Fauna using our Token from Auth0. This token works the same as the Keys from previous examples.

### Generate a random Mindful topic and store it in Fauna

To start, we need a Collection of items to store our list of Mindful objects. We’ll create a Collection called “mindful” things, and create a number of items with the following schema:

<div class="break-out">

<pre><code class="language-javascript">{
   "title": "Career",
   "description": "Think about the next steps you want to make in your career. What’s the next easily attainable move you can make?",
   "color": "#C6D4FF",
   "textColor": "black"
 }</code></pre>
</div>

From here, we’ll move to our JavaScript and create a function for adding and returning a random item from that Collection.

<div class="break-out">

 <pre><code class="language-javascript">async function getRandomMindfulFromFauna(userObj) {
    const client = await getUserClient(userObj);

    try {
        let mindfulThings = await client.query(
            q.Paginate(
                q.Documents(q.Collection('mindful_things'))
            )
        )
        let randomMindful = mindfulThings.data[Math.floor(Math.random()*mindfulThings.data.length)];
        let creation = await client.query(q.Call('addUserMindful', randomMindful));
        
        return creation.data.mindful;

    } catch (error) {
        console.log(error)
    }   
}
</code></pre>
</div>

To start, we’ll instantiate our client with our `getUserClient()` method.

From there, we’ll grab all the Documents from our `mindful_things` Collection. `Paginate()` by default grabs 64 items per page, which is more than enough for our data. We’ll grab a random item from the array that’s returned from Fauna. This will be what Fauna refers to as a “Ref”. A Ref is a full reference to a Document that the various FQL functions can use to locate a Document.

We’ll pass that Ref to a new UDF that will handle storing a new, timestamped object for that user stored in a new `user_things` Collection.

We’ll create the new Collection, but we’ll have our UDF provide the data for it when called.

We’ll create a new UDF in the Fauna dashboard with the name `addUserMindful` that will accept that random Ref.

As with our login UDF before, we’ll use the `Lambda()` FQL method which takes an array of arguments.

Without passing any user information to the function, FQL is able to obtain our User Ref just calling the `Identity()` function. All we have from our `randomRef` is the reference to our Document. We’ll run a `Get()` to get the full object. We’ll the `Create()` a new Document in the `user_things` Collection with our User Ref and our random information.

We then return the `creation` object back out of our Lambda. We then go back to our JavaScript and return the data object with the `mindful` key back to where this function gets called.

### Render our Mindful Object on the page

When our user is authenticated, you may remember it called a `changeToMission()` method. This function switches the items on the page from the “Home” screen to markup that can be filled in by our data. After it’s added to the page, the `renderToday()` function gets called to add content by a few rules.

The first rule of Serverless Data Club is not to make HTTP requests unless you have to. In other words, cache when you can. Whether that’s creating a full PWA-scale application with Service Workers or just caching your database response with localStorage, cache data, and fetch only when necessary.

The first rule of our conditional is to check localStorage. If localStorage does contain a `currentMindfulItem`, then we need to check its date to see if it’s from today. If it is, we’ll render that and make no new requests.

The second rule of Serverless Data Club is to make as few requests as possible without the responses of those requests being too large. In that vein, our second conditional rule is to check the latest item from the current user and see if it is from today. If it is, we’ll store it in localStorage for later and then render the results.

Finally, if none of these are true, we’ll fire our `getRandomMindfulFromFauna()` function, format the result, store that in localStorage, and then render the result.

### Get the latest item from a user

I glossed over it in the last section, but we also need some functionality to retrieve the latest mindful object from Fauna for our specific user. In our `getLatestFromFauna()` method, we’ll again instantiate our Fauna client and then call a new UDF.

Our new UDF is going to call a Fauna Index. An Index is an efficient way of doing a lookup on a Fauna database. In our case, we want to return all `user_things` by the `user` field. Then we can also sort the result by timestamp and reverse the default ordering of the data to show the latest first.

Simple Indexes can be created in the Index dashboard. Since we want to do the reverse sort, we’ll need to enter some custom FQL into the Fauna Shell (you can do this in the database dashboard Shell section).

<pre><code class="language-javascript">CreateIndex({
  name: "getMindfulByUserReverse",
  serialized: true,
  source: Collection("user_things"),
  terms: [
    {
      field: ["data", "user"]
    }
  ],
  values: [
    {
      field: ["ts"],
      reverse: true
    },
    {
      field: ["ref"]
    }
  ]
})
</code></pre>

This creates an Index named `getMindfulByUserReverse`, created from our `user_thing` Collection. The `terms` object is a list of fields to search by. In our case, this is just the `user` field on the data object. We then provide `values` to return. In our case, we need the Ref and the Timestamp and we’ll use the `reverse` property to reverse order our results by this field.

We’ll create a new UDF to use this Index.

<div class="break-out">

 <pre><code class="language-javascript">Query(
  Lambda(
    [],
    If( // Check if there is at least 1 in the index
      GT(
        Count(
          Select(
            "data",
            Paginate(Match(Index("getMindfulByUserReverse"), Identity()))
          )
        ),
        0
      ),
      Let( // if more than 0
        {
          match: Paginate(
            Match(Index("getMindfulByUserReverse"), Identity()) // Search the index by our User
          ),
          latestObj: Take(1, Var("match")), // Grab the first item from our match
          latestRef: Select(
            ["data"],
            Get(Select(["data", 0, 1], Var("latestObj"))) // Get the data object from the item
          ),
          latestTime: Select(["data", 0, 0], Var("latestObj")), // Get the time
          merged: Merge( // merge those items into one object to return
            { latestTime: Var("latestTime") },
            { latestMindful: Var("latestRef") }
          )
        },
        Var("merged")
      ),
      Let({ error: { err: "No data" } }, Var("error")) // if there aren't any, return an error.
    )
  )
)
</code></pre>
</div>

This time our `Lambda()` function doesn’t need any arguments since we’ll have our User based on the Token used.

First, we’ll check to see if there’s at least 1 item in our Index. If there is, we’ll grab the first item’s data and time and return that back as a merged object.

After we get the latest from Fauna in our JavaScript, we’ll format it to a structure our `storeCurrent()` and `render()` methods expect it and return that object.

Now, we have an application that creates, stores, and fetches data for a daily message to contemplate. A user can use this on their phone, on their tablet, on the computer, and have it all synced. We could turn this into a PWA or even a native app with a system like Ionic.

We’re still missing one feature. Viewing a certain number of past items. Since we’ve stored this in our database, we can retrieve them in whatever way we need to.

### Pull the latest X Mindful Missions to get a picture of what you’ve thought about

We’ll create a new JavaScript method paired with a new UDF to tackle this.

`getSomeFromFauna` will take an integer `count` to ask Fauna for a certain number of items.

Our UDF will be very similar to the `getLatestFromFauana` UDF. Instead of returning the first item, we’ll `Take()` the number of items from our array that matches the integer that gets passed into our UDF. We’ll also begin with the same conditional, in case a user doesn’t have any items stored yet.

<div class="break-out">

 <pre><code class="language-javascript">Query(
  Lambda(
    ["count"], // Number of items to return
    If( // Check if there are any objects
      GT( 
        Count(
          Select(
            "data",
            Paginate(Match(Index("getMindfulByUserReverse"), Identity(null)))
          )
        ),
        0
      ),
      Let(
        {
          match: Paginate(
            Match(Index("getMindfulByUserReverse"), Identity(null)) // Search the Index by our User
          ),
          latestObjs: Select("data", Take(Var("count"), Var("match"))), // Get the data that is returned
          mergedObjs: Map( // Loop over the objects
            Var("latestObjs"),
            Lambda(
              "latestArray",
              Let( // Build the data like we did in the LatestMindful function
                {
                  ref: Select(["data"], Get(Select([1], Var("latestArray")))),
                  latestTime: Select(0, Var("latestArray")),
                  merged: Merge(
                    { latestTime: Var("latestTime") },
                    Select("mindful", Var("ref"))
                  )
                },
                Var("merged") // Return this to our new array
              )
            )
          )
        },
        Var("mergedObjs") // return the full array
      ),
      { latestMindful: [{ title: "No additional data" }] } // if there are no items, send back a message to display
    )
  )
)
</code></pre>
</div>

In this demo, we created a full-fledged app with serverless data. Because the data is served from a CDN, it can be as close to a user as possible. We used <a href="https://synd.co/2XBbr4W">FaunaDB</a>’s features, such as UDFs and Indexes, to optimize our database queries for speed and ease of use. We also made sure we only queried our database the bare minimum to reduce requests.

## Where To Go With Serverless Data

The JAMstack isn’t just for sites. It can be used for robust applications as well. Whether that’s for a game, CRUD application or just to be mindful of your surroundings you can do a lot without sacrificing customization and without spinning up your own non-dist database system.

With performance on the mind of everyone creating on the JAMstack &mdash; whether for cost or for user experience &mdash; finding a good place to store and retrieve your data is a high priority. Find a spot that meets your needs, those of your users, and meets ideals of the JAMstack.

{{< signature "ra, yk, il" >}}
