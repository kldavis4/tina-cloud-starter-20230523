---
title: 'Understanding Plugin Development In Gatsby'
slug: understanding-plugin-development-gatsby
author: aleem-isiaka
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cdd8cf9f-26df-49ac-9dff-cc03f7d8678a/understanding-plugin-development-gatsby.png
date: 2020-07-06T14:30:00.000Z
summary: >-
  Gatsby is a modern static-site generator that has revamped the way static websites are being built. It incorporates React, Node.js, and GraphQL to create stunning and blazing-fast websites. In this post, we will discuss Gatsby plugins and develop our own comment plugin.
description: >-
  Gatsby is a modern static-site generator that has revamped the way static websites are being built. It incorporates React, Node.js, and GraphQL to create stunning and blazing-fast websites. In this post, we will discuss Gatsby plugins and develop our own comment plugin.
categories:
  - React
  - Gatsby
  - Generators
  - Static Generators
---

Gatsby is a React-based static-site generator that has overhauled how websites and blogs are created. It supports the use of plugins to create custom functionality that is not available in the standard installation.

In this post, I will introduce Gatsby plugins, discuss the types of Gatsby plugins that exist, differentiate between the forms of Gatsby plugins, and, finally, create a comment plugin that can be used on any Gatsby website, one of which we will install by the end of the tutorial.

## What Is A Gatsby Plugin?

[Gatsby](https://www.gatsbyjs.org/), as a static-site generator, [has limits on what it can do](https://www.gatsbyjs.org/features/). Plugins are means to extend Gatsby with any feature not provided out of the box. We can achieve tasks like creating a `manifest.json` file for a progressive web app (PWA), embedding tweets on a page, logging page views, and much more on a Gatsby website using plugins.

## Types Of Gatsby Plugins

There are two types of Gatsby plugins, local and external. Local plugins are developed in a Gatsby project directory, under the `/plugins` directory. External plugins are those available through npm or Yarn. Also, they may be on the same computer but linked using the `yarn link` or `npm link` command in a Gatsby website project.

{{% feature-panel %}}

## Forms Of Gatsby Plugins

Plugins also exist in three primary forms and are defined by their use cases:

- **Source plugins**  
These kinds of plugins provide sources of data for a Gatsby website. Examples of these are [gatsby-source-filesystem](https://www.gatsbyjs.org/packages/gatsby-source-filesystem), [gatsby-source-contentful](https://www.gatsbyjs.org/packages/gatsby-source-contentful/), and [gatsby-source-wordpress](https://www.gatsbyjs.org/packages/gatsby-source-wordpress/).
- **Transformer plugins**  
These kinds of plugins transform data from the sources of other plugins into a more usable and consumable form. Example include [gatsby-transformer-remark](https://www.gatsbyjs.org/packages/gatsby-transformer-remark), [gatsby-transformer-json](https://www.gatsbyjs.org/packages/gatsby-transformer-json), and [gatsby-transformer-sharp](https://www.gatsbyjs.org/packages/gatsby-transformer-sharp/).
- **Generic plugins**  
These plugins do things beyond transforming and sourcing data. Notable example are [gatsby-plugin-mdx](https://www.gatsbyjs.org/packages/gatsby-plugin-mdx) and [gatsby-plugin-sharp](https://www.gatsbyjs.org/packages/gatsby-plugin-sharp). We will be creating one in this post.

## Components Of A Gatsby Plugin

To create a Gatsby plugin, we have to define some files:

- [`gatsby-node.js`](https://www.gatsbyjs.org/docs/api-files-gatsby-node)  
Makes it possible to listen to the build processes of Gatsby.
- [`gatsby-config.js`](https://www.gatsbyjs.org/docs/api-files-gatsby-config)  
Mainly used for configuration and setup.
- [`gatsby-browser.js`](https://www.gatsbyjs.org/docs/api-files-gatsby-browser)  
Allows plugins to run code during one of the Gatsby’s processes in the browser.
- [`gatsby-ssr.js`](https://www.gatsbyjs.org/docs/api-files-gatsby-ssr)  
Customizes and adds functionality to the server-side rendering (SSR) process.

These files are referred to as API files in Gatsby’s documentation and should live in the root of a plugin’s directory, either local or external.

Not all of these files are required to create a Gatsby plugin. In our case, we will be implementing only the `gatsby-node.js` and `gatsby-config.js` API files.

## Building A Comment Plugin For Gatsby

To learn how to develop a Gatsby plugin, we will create a comment plugin that is installable on any blog that runs on Gatsby. The full code for the plugin is [on GitHub](https://github.com/limistah/gatsby-plugin-commentator).

### Serving and Loading Comments

To serve comments on a website, we have to provide a server that allows for the saving and loading of comments. We will use an already available comment server at `gatsbyjs-comment-server.herokuapp.com` for this purpose.

The server supports a `GET /comments` request for loading comments. `POST /comments` would save comments for the website, and it accepts the following fields as the body of the `POST /comments` request:

- `content: [string]`  
The comment itself,
- `author: [string]`  
The name of the comment’s author,
- `website`  
The website that the comment is being posted from,
- `slug`  
The slug for the page that the comment is meant for.

### Integrating the Server With Gatsby Using API Files

Much like we do when [creating a Gatsby blog](https://www.gatsbyjs.org/tutorial/blog-netlify-cms-tutorial/), to create an external plugin, we should start with [plugin boilerplate](https://github.com/gatsbyjs/gatsby-starter-plugin).

#### Initializing the folder

In the command-line interace (CLI) and from any directory you are convenient with, let’s run the following command:

<div class="break-out">

<pre><code class="language-bash">gatsby new gatsby-source-comment-server https://github.com/Gatsbyjs/gatsby-starter-plugin</code></pre>
</div>

Then, change into the plugin directory, and open it in a code editor.

#### Installing axios for Network Requests

To begin, we will install the axios package to make web requests to the comments server:

<pre><code class="language-bash">npm install axios --save
// or
yarn add axios</code></pre>

#### Adding a New Node Type

Before pulling comments from the comments server, we need to define a new node type that the comments would extend. For this, in the plugin folder, our `gatsby-node.js` file should contain the code below:

<pre><code class="language-javascript">exports.sourceNodes = async ({ actions }) =&gt; {
  const { createTypes } = actions;
  const typeDefs = `
    type CommentServer implements Node {
      _id: String
      author: String
      string: String
      content: String
      website: String
      slug: String
      createdAt: Date
      updatedAt: Date
    }
  `;
  createTypes(typeDefs);
};</code></pre>

First, we pulled [`actions`](https://www.gatsbyjs.org/docs/actions/#createNode) from the APIs provided by Gatsby. Then, we pulled out the [`createTypes`](https://www.gatsbyjs.org/docs/actions/#createTypes) action, after which we defined a `CommentServer` type that extends Node.js. Then, we called `createTypes` with the new node type that we set.

#### Fetching Comments From the Comments Server

Now, we can use axios to pull comments and then store them in the data-access layer as the `CommentServer` type. This action is called “node sourcing” in Gatsby.

To source for new nodes, we have to implement the [`sourceNodes`](https://www.gatsbyjs.org/docs/node-apis/#sourceNodes) API in `gatsby-node.js`. In our case, we would use axios to make network requests, then parse the data from the API to match a GraphQL type that we would define, and then create a [node](https://www.gatsbyjs.org/docs/node-model/) in the GraphQL layer of Gatsby using the [`createNode`](https://www.gatsbyjs.org/docs/actions/#createNode) action.

We can add the code below to the plugin’s `gatsby-node.js` API file, creating the functionality we’ve described:

<div class="break-out">

<pre><code class="language-javascript">const axios = require("axios");

exports.sourceNodes = async (
  { actions, createNodeId, createContentDigest },
  pluginOptions
) =&gt; {
  const { createTypes } = actions;
  const typeDefs = `
    type CommentServer implements Node {
      _id: String
      author: String
      string: String
      website: String
      content: String
      slug: String
      createdAt: Date
      updatedAt: Date
    }
  `;
  createTypes(typeDefs);

  const { createNode } = actions;
  const { limit, website } = pluginOptions;
  const _website = website || "";

  const result = await axios({
    url: `https://Gatsbyjs-comment-server.herokuapp.com/comments?limit=${_limit}&website=${_website}`,
  });

  const comments = result.data;

  function convertCommentToNode(comment, { createContentDigest, createNode }) {
    const nodeContent = JSON.stringify(comment);

    const nodeMeta = {
      id: createNodeId(`comments-${comment._id}`),
      parent: null,
      children: [],
      internal: {
        type: `CommentServer`,
        mediaType: `text/html`,
        content: nodeContent,
        contentDigest: createContentDigest(comment),
      },
    };

    const node = Object.assign({}, comment, nodeMeta);
    createNode(node);
  }

  for (let i = 0; i &lt; comments.data.length; i++) {
    const comment = comments.data[i];
    convertCommentToNode(comment, { createNode, createContentDigest });
  }
};</code></pre>
</div>

Here, we have imported the axios package, then set defaults in case our plugin’s options are not provided, and then made a request to the endpoint that serves our comments.

We then defined a function to convert the comments into Gatsby nodes, using the action helpers provided by Gatsby. After this, we iterated over the fetched comments and called `convertCommentToNode` to convert the comments into Gatsby [nodes](https://www.gatsbyjs.org/docs/node-model/).

{{% ad-panel-leaderboard %}}

#### Transforming Data (Comments)

Next, we need to resolve the comments to posts. Gatsby has an API for that called [`createResolvers`](https://www.gatsbyjs.org/docs/schema-customization/#createresolvers-api). We can make this possible by appending the code below in the `gatsby-node.js` file of the plugin:

<pre><code class="language-javascript">exports.createResolvers = ({ createResolvers }) =&gt; {
  const resolvers = {
    MarkdownRemark: {
      comments: {
        type: ["CommentServer"],
        resolve(source, args, context, info) {
          return context.nodeModel.runQuery({
            query: {
              filter: {
                slug: { eq: source.fields.slug },
              },
            },
            type: "CommentServer",
            firstOnly: false,
          });
        },
      },
    },
  };
  createResolvers(resolvers);
};</code></pre>

Here, we are extending `MarkdownRemark` to include a `comments` field. The newly added `comments` field will resolve to the `CommentServer` type, based on the slug that the comment was saved with and the slug of the post.

#### Final Code for Comment Sourcing and Transforming 

The final code for the `gatsby-node.js` file of our comments plugin should look like this:

<div class="break-out">

<pre><code class="language-javascript">const axios = require("axios");

exports.sourceNodes = async (
  { actions, createNodeId, createContentDigest },
  pluginOptions
) =&gt; {
  const { createTypes } = actions;
  const typeDefs = `
    type CommentServer implements Node {
      _id: String
      author: String
      string: String
      website: String
      content: String
      slug: String
      createdAt: Date
      updatedAt: Date
    }
  `;
  createTypes(typeDefs);

  const { createNode } = actions;
  const { limit, website } = pluginOptions;
  const _limit = parseInt(limit || 10000); // FETCH ALL COMMENTS
  const _website = website || "";

  const result = await axios({
    url: `https://Gatsbyjs-comment-server.herokuapp.com/comments?limit=${_limit}&website=${_website}`,
  });

  const comments = result.data;

  function convertCommentToNode(comment, { createContentDigest, createNode }) {
    const nodeContent = JSON.stringify(comment);

    const nodeMeta = {
      id: createNodeId(`comments-${comment._id}`),
      parent: null,
      children: [],
      internal: {
        type: `CommentServer`,
        mediaType: `text/html`,
        content: nodeContent,
        contentDigest: createContentDigest(comment),
      },
    };

    const node = Object.assign({}, comment, nodeMeta);
    createNode(node);
  }

  for (let i = 0; i &lt; comments.data.length; i++) {
    const comment = comments.data[i];
    convertCommentToNode(comment, { createNode, createContentDigest });
  }
};

exports.createResolvers = ({ createResolvers }) =&gt; {
  const resolvers = {
    MarkdownRemark: {
      comments: {
        type: ["CommentServer"],
        resolve(source, args, context, info) {
          return context.nodeModel.runQuery({
            query: {
              filter: {
                website: { eq: source.fields.slug },
              },
            },
            type: "CommentServer",
            firstOnly: false,
          });
        },
      },
    },
  };
  createResolvers(resolvers);
};</code></pre>
</div>

#### Saving Comments as JSON Files

We need to save the comments for page slugs in their respective JSON files. This makes it possible to fetch the comments on demand over HTTP without having to use a GraphQL query.

To do this, we will implement the `createPageStatefully` API in the`gatsby-node.js` API file of the plugin. We will use the `fs` module to check whether the path exists before creating a file in it. The code below shows how we can implement this:

<div class="break-out">

<pre><code class="language-javascript">import fs from "fs"
import {resolve: pathResolve} from "path"
exports.createPagesStatefully = async ({ graphql }) =&gt; {
  const comments = await graphql(
    `
      {
        allCommentServer(limit: 1000) {
          edges {
            node {
              name
              slug
              _id
              createdAt
              content
            }
          }
        }
      }
    `
  )

  if (comments.errors) {
    throw comments.errors
  }

  const markdownPosts = await graphql(
    `
      {
        allMarkdownRemark(
          sort: { fields: [frontmatter___date], order: DESC }
          limit: 1000
        ) {
          edges {
            node {
              fields {
                slug
              }
            }
          }
        }
      }
    `
  )

  const posts = markdownPosts.data.allMarkdownRemark.edges
  const _comments = comments.data.allCommentServer.edges

  const commentsPublicPath = pathResolve(process.cwd(), "public/comments")

  var exists = fs.existsSync(commentsPublicPath) //create destination directory if it doesn't exist

  if (!exists) {
    fs.mkdirSync(commentsPublicPath)
  }

  posts.forEach((post, index) =&gt; {
    const path = post.node.fields.slug
    const commentsForPost = _comments
      .filter(comment =&gt; {
        return comment.node.slug === path
      })
      .map(comment =&gt; comment.node)

    const strippedPath = path
      .split("/")
      .filter(s =&gt; s)
      .join("/")
    const _commentPath = pathResolve(
      process.cwd(),
      "public/comments",
      `${strippedPath}.json`
    )
    fs.writeFileSync(_commentPath, JSON.stringify(commentsForPost))
  })
}</code></pre>
</div>

First, we require the `fs`, and `resolve` the function of the `path` module. We then use the GraphQL helper to pull the comments that we stored earlier, to avoid extra HTTP requests. We remove the Markdown files that we created using the GraphQL helper. And then we check whether the comment path is not missing from the public path, so that we can create it before proceeding.

Finally, we loop through all of the nodes in the Markdown type. We pull out the comments for the current posts and store them in the `public/comments` directory, with the post’s slug as the name of the file.

The `.gitignore` in the root in a Gatsby website excludes the public path from being committed. Saving files in this directory is safe.

During each rebuild, Gatsby would call this API in our plugin to fetch the comments and save them locally in JSON files.

### Rendering Comments

To render comments in the browser, we have to use the `gatsby-browser.js` API file.

#### Define the Root Container for HTML

In order for the plugin to identify an insertion point in a page, we would have to set an HTML element as the container for rendering and listing the plugin's components. We can expect that every page that requires it should have an HTML element with an ID set to `commentContainer`.

#### Implement the Route Update API in the gatsby-browser.js File

The best time to do the file fetching and component insertion is when a page has just been visited. The `onRouteUpdate` API provides this functionality and passes the `apiHelpers` and `pluginOpions` as arguments to the callback function.

<pre><code class="language-javascript">exports.onRouteUpdate = async (apiHelpers, pluginOptions) =&gt; {
  const { location, prevLocation } = apiHelpers
}</code></pre>

#### Create Helper That Creates HTML Elements

To make our code cleaner, we have to define a function that can create an HTML element, set its `className`, and add content. At the top of the `gatsby-browser.js` file, we can add the code below:

<pre><code class="language-javascript">// Creates element, set class. innerhtml then returns it.
 function createEl (name, className, html = null) {
  const el = document.createElement(name)
  el.className = className
  el.innerHTML = html
  return el
}</code></pre>

#### Create Header of Comments Section

At this point, we can add a header into the insertion point of comments components, in the `onRouteUpdate` browser API . First, we would ensure that the element exists in the page, then create an element using the `createEl` helper, and then append it to the insertion point.

<div class="break-out">

<pre><code class="language-javascript">// ...

exports.onRouteUpdate = async ({ location, prevLocation }, pluginOptions) =&gt; {
  const commentContainer = document.getElementById("commentContainer")
  if (commentContainer && location.path !== "/") {
    const header = createEl("h2")
    header.innerHTML = "Comments"
    commentContainer.appendChild(header)
  }
}</code></pre>
</div>

#### Listing Comments

To list comments, we would append a `ul` element to the component insertion point. We will use the `createEl` helper to achieve this, and set its `className` to `comment-list`:

<div class="break-out">

<pre><code class="language-javascript">exports.onRouteUpdate = async ({ location, prevLocation }, pluginOptions) =&gt; {
  const commentContainer = document.getElementById("commentContainer")
  if (commentContainer && location.path !== "/") {
    const header = createEl("h2")
    header.innerHTML = "Comments"
    commentContainer.appendChild(header)
    const commentListUl = createEl("ul")
    commentListUl.className = "comment-list"
    commentContainer.appendChild(commentListUl)
}</code></pre>
</div>

Next, we need to render the comments that we have saved in the public directory to a `ul` element, inside of `li` elements. For this, we define a helper that fetches the comments for a page using the path name.

<pre><code class="language-javascript">// Other helpers
const getCommentsForPage = async slug =&gt; {
  const path = slug
    .split("/")
    .filter(s =&gt; s)
    .join("/")
  const data = await fetch(`/comments/${path}.json`)
  return data.json()
}
// ... implements routeupdate below</code></pre>

We have defined a helper, named `getCommentsForPage`, that accepts paths and uses `fetch` to load the comments from the `public/comments` directory, before parsing them to JSON and returning them back to the calling function.

Now, in our `onRouteUpdate` callback, we will load the comments:

<div class="break-out">

<pre><code class="language-javascript">// ... helpers
exports.onRouteUpdate = async ({ location, prevLocation }, pluginOptions) =&gt; {
  const commentContainer = document.getElementById("commentContainer")
  if (commentContainer && location.path !== "/") {
    //... inserts header
    const commentListUl = createEl("ul")
    commentListUl.className = "comment-list"
    commentContainer.appendChild(commentListUl)
   const comments = await getCommentsForPage(location.pathname)
}</code></pre>
</div>

Next, let’s define a helper to create the list items:

<div class="break-out">

<pre><code class="language-javascript">// .... other helpers

const getCommentListItem = comment =&gt; {
  const li = createEl("li")
  li.className = "comment-list-item"

  const nameCont = createEl("div")
  const name = createEl("strong", "comment-author", comment.name)
  const date = createEl(
    "span",
    "comment-date",
    new Date(comment.createdAt).toLocaleDateString()
  )
  // date.className="date"
  nameCont.append(name)
  nameCont.append(date)

  const commentCont = createEl("div", "comment-cont", comment.content)

  li.append(nameCont)
  li.append(commentCont)
  return li
}

// ... onRouteUpdateImplementation</code></pre>
</div>

In the snippet above, we created an `li` element with a `className` of `comment-list-item`, and a `div` for the comment’s author and time. We then created another `div` for the comment’s text, with a `className` of `comment-cont`.

To render the list items of comments, we iterate through the comments fetched using the `getComments` helper, and then call the `getCommentListItem` helper to create a list item. Finally, we append it to the `<ul class="comment-list"></ul>` element:

<div class="break-out">

<pre><code class="language-javascript">// ... helpers
exports.onRouteUpdate = async ({ location, prevLocation }, pluginOptions) =&gt; {
  const commentContainer = document.getElementById("commentContainer")
  if (commentContainer && location.path !== "/") {
    //... inserts header
    const commentListUl = createEl("ul")
    commentListUl.className = "comment-list"
    commentContainer.appendChild(commentListUl)
   const comments = await getCommentsForPage(location.pathname)
    if (comments && comments.length) {
      comments.map(comment =&gt; {
        const html = getCommentListItem(comment)
        commentListUl.append(html)
        return comment
      })
    }
}</code></pre>
</div>

{{% ad-panel-leaderboard %}}

### Posting a Comment

#### Post Comment Form Helper

To enable users to post a comment, we have to make a `POST` request to the `/comments` endpoint of the API. We need a form in order to create this form. Let’s create a form helper that returns an HTML form element.

<pre><code class="language-javascript">// ... other helpers
const createCommentForm = () =&gt; {
  const form = createEl("form")
  form.className = "comment-form"
  const nameInput = createEl("input", "name-input", null)
  nameInput.type = "text"
  nameInput.placeholder = "Your Name"
  form.appendChild(nameInput)
  const commentInput = createEl("textarea", "comment-input", null)
  commentInput.placeholder = "Comment"
  form.appendChild(commentInput)
  const feedback = createEl("span", "feedback")
  form.appendChild(feedback)
  const button = createEl("button", "comment-btn", "Submit")
  button.type = "submit"
  form.appendChild(button)
  return form
}</code></pre>

The helper creates an input element with a `className` of `name-input`, a `textarea` with a `className` of `comment-input`, a `span` with a `className` of `feedback`, and a button with a `className` of `comment-btn`.

#### Append the Post Comment Form

We can now append the form into the insertion point, using the `createCommentForm` helper:

<div class="break-out">

<pre><code class="language-javascript">// ... helpers
exports.onRouteUpdate = async ({ location, prevLocation }, pluginOptions) =&gt; {
  const commentContainer = document.getElementById("commentContainer")
  if (commentContainer && location.path !== "/") {
    // insert header
    // insert comment list
    commentContainer.appendChild(createCommentForm())
  }
}</code></pre>
</div>

### Post Comments to Server

To post a comment to the server, we have to tell the user what is happening &mdash; for example, either that an input is required or that the API returned an error. The `<span class="feedback" />` element is meant for this. To make it easier to update this element, we create a helper that sets the element and inserts a new class based on the type of the feedback (whether error, info, or success).

<div class="break-out">

<pre><code class="language-javascript">// ... other helpers
// Sets the class and text of the form feedback
const updateFeedback = (str = "", className) =&gt; {
  const feedback = document.querySelector(".feedback")
  feedback.className = `feedback ${className ? className : ""}`.trim()
  feedback.innerHTML = str
  return feedback
}
// onRouteUpdate callback</code></pre>
</div>

We are using the `querySelector` API to get the element. Then we set the class by updating the `className` attribute of the element. Finally, we use `innerHTML` to update the contents of the element before returning it.

#### Submitting a Comment With the Comment Form

We will listen to the `onSubmit` event of the comment form to determine when a user has decided to submit the form. We don’t want empty data to be submitted, so we would set a feedback message and disable the submit button until needed:

<div class="break-out">

<pre><code class="language-javascript">exports.onRouteUpdate = async ({ location, prevLocation }, pluginOptions) =&gt; {
  // Appends header
  // Appends comment list
  // Appends comment form
  document
    .querySelector("body .comment-form")
    .addEventListener("submit", async function (event) {
      event.preventDefault()
      updateFeedback()
      const name = document.querySelector(".name-input").value
      const comment = document.querySelector(".comment-input").value
      if (!name) {
        return updateFeedback("Name is required")
      }
      if (!comment) {
        return updateFeedback("Comment is required")
      }
      updateFeedback("Saving comment", "info")
      const btn = document.querySelector(".comment-btn")
      btn.disabled = true
      const data = {
        name,
        content: comment,
        slug: location.pathname,
        website: pluginOptions.website,
      }

      fetch(
        "https://cors-anywhere.herokuapp.com/gatsbyjs-comment-server.herokuapp.com/comments",
        {
          body: JSON.stringify(data),
          method: "POST",
          headers: {
            Accept: "application/json",
            "Content-Type": "application/json",
          },
        }
      ).then(async function (result) {
        const json = await result.json()
        btn.disabled = false

        if (!result.ok) {
          updateFeedback(json.error.msg, "error")
        } else {
          document.querySelector(".name-input").value = ""
          document.querySelector(".comment-input").value = ""
          updateFeedback("Comment has been saved!", "success")
        }
      }).catch(async err =&gt; {
        const errorText = await err.text()
        updateFeedback(errorText, "error")
      })
    })
}</code></pre>
</div>

We use `document.querySelector` to get the form from the page, and we listen to its `submit` event. Then, we set the feedback to an empty string, from whatever it might have been before the user attempted to submit the form.

We also check whether the name or comment field is empty, setting an error message accordingly.

Next, we make a `POST` request to the comments server at the `/comments` endpoint, listening for the response. We use the feedback to tell the user whether there was an error when they created the comment, and we also use it to tell them whether the comment’s submission was successful.

#### Adding a Style Sheet

To add styles to the component, we have to create a new file, `style.css`, at the root of our plugin folder, with the following content:

<pre><code class="language-css">#commentContainer {
}

.comment-form {
  display: grid;
}</code></pre>

At the top of `gatsby-browser.js`, import it like this:

<pre><code class="language-javascript">import "./style.css"</code></pre>

This style rule will make the form’s components occupy 100% of the width of their container.

Finally, all of the components for our comments plugin are complete. Time to install and test this fantastic plugin we have built.

## Test the Plugin

### Create a Gatsby Website

Run the following command from a directory one level above the plugin’s directory:

<div class="break-out">

<pre><code class="language-bash">// PARENT
// ├── PLUGIN
// ├── Gatsby Website

gatsby new private-blog https://github.com/gatsbyjs/gatsby-starter-blog</code></pre>
</div>

### Install the Plugin Locally and Add Options

#### Link With npm

Next, change to the blog directory, because we need to create a link for the new plugin:

<pre><code class="language-bash">cd /path/to/blog
npm link ../path/to/plugin/folder</code></pre>

#### Add to gatsby-config.js

In the `gatsby-config.js` file of the blog folder, we should add a new object that has a `resolve` key and that has `name-of-plugin-folder` as the value of the plugin’s installation. In this case, the name is `gatsby-comment-server-plugin`:

<pre><code class="language-javascript">module.exports = {
  // ...
  plugins: [
    // ...
    "gatsby-plugin-dom-injector",
    {
      resolve: "gatsby-comment-server-plugin",
      options: {website: "https://url-of-website.com"},
    },
  ],
}</code></pre>

Notice that the plugin accepts a `website` option to distinguish the source of the comments when fetching and saving comments.

#### Update the blog-post Component

For the insertion point, we will add `<section class="comments" id="commentContainer">` to the post template component at `src/templates/blog-post.js` of the blog project. This can be inserted at any suitable position; I have inserted mine after the last `hr` element and before the `footer`.

#### Start the Development Server

Finally, we can start the development server with `gatsby develop`, which will make our website available locally at `https://localhost:8000`. Navigating to any post page, like `https://localhost:8000/new-beginnings`, will reveal the comment at the insertion point that we specified above.

#### Create a Comment

We can create a comment using the comment form, and it will provide helpful feedback as we interact with it.

#### List Comments

To list newly posted comments, we have to restart the server, because our content is static.

## Conclusion

In this tutorial, we have introduced Gatsby plugins and demonstrated how to create one.

Our plugin uses different APIs of Gatsby and its own API files to provide comments for our website, illustrating how we can use plugins to add significant functionality to a Gatsby website.

Although we are pulling from a live server, the plugin is saving the comments in JSON files. We could make the plugin load comments on demand from the API server, but that would defeat the notion that our blog is a static website that does not require dynamic content.

The plugin built in this post exists as an [npm module](https://www.npmjs.com/package/gatsby-plugin-commentator), while the full code is [on GitHub](https://github.com/limistah/gatsby-plugin-commentator).

### References:

- [Documentation](https://www.gatsbyjs.org/docs/), Gatsby
- [Gatsby Source Comment Server](https://github.com/limistah/gatsby-source-comment-server) (plugin source), GitHub
- [Gatsby Plugin Commentator](https://github.com/limistah/gatsby-plugin-commentator) (repository), GitHub

### Resources:

- [Gatsby’s blog starter](https://github.com/limistah/sm-gatsby-private-blog-tutorial), GitHub  
A private blog repository available for you to create a Gatsby website to consume the plugin.
- [Gatsby Starter Blog](https://private-blog.netlify.app/), Netlify  
The blog website for this tutorial, deployed on Netlify for testing.

{{< signature "yk" >}}
