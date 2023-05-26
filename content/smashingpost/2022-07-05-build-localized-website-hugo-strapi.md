---
title: 'How To Build A Localized Website With Hugo And Strapi'
slug: build-localized-website-hugo-strapi
author: zara-cooper
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/497caaf3-63f0-4dde-9a46-07486cec03a9/build-localized-website-hugo-strapi.jpg
date: 2022-07-05T09:00:00.000Z
summary: >-
  In this tutorial, Zara Cooper explains how to use Strapi’s Internationalization feature to create content in multiple languages. You’ll also learn how to create a Hugo site that consumes localized content from Strapi.
description: >-
  In this tutorial, Zara Cooper explains how to use Strapi’s Internationalization feature to create content in multiple languages. You’ll also learn how to create a Hugo site that consumes localized content from Strapi.
categories:
  - Tools
  - Hugo
  - Headless
  - CMS
---

Localizing your site can benefit your business or organization in several ways. By translating your content or site, you expand the markets you target. Adapting your product to the language and cultural preferences of potential customers who were not able to use your product before boosts your conversion rates.

Ultimately, this often leads to a growth in the revenue you generate. With a larger, more widespread customer base, your brand becomes increasingly recognizable and strengthened in newer markets.

A localized website has a higher SEO score which means that users within a specific market can find it easier through a search engine. A recognizable brand and improved SEO score reduce the cost of marketing to users within the markets you target.

We’ve seen that localization has its benefits, but what exactly is it? Localization is the process of revising your website, app, or content that was initially intended for a primary market to suit the needs of a new market you plan on targeting. Localization often involves translating a product into the language used in the market you want to introduce it to. It can also mean adding new things or removing parts of the product, for example, that might offend the market. You may also modify a product by changing its look and feel based on writing systems, color preferences, etc. 

Although localization may seem straightforward, it cannot happen if the underlying site or app cannot accommodate these changes. Since it isn’t practical to build the same site for every market you want to enter, it makes sense that your site should switch content, language, UI elements, etc., between markets. That’s where internationalization comes in. 

Internationalization is the process of designing and building a site or app to accommodate localization across different markets. For example, an online magazine’s site published in Portugal, Japan, and Ireland needs to accommodate different languages, writing systems, payment processors, and so on. 

Before embarking on localization, it is important to pick a backend that will help you manage your site content across different locales. Strapi is one choice that provides this functionality. It’s an open-source headless content management system (CMS) built with Node.js. With it, you can manage and structure content into types using its content types builder on its user-friendly admin panel. For every content type you create, it automatically generates a customizable API for it. You can upload all kinds of media and manage them using its media library. 

With its [**R**ole-**B**ased **A**ccess **C**ontrol (**RBAC**) features](https://strapi.io/features/custom-roles-and-permissions), you can set custom roles and permissions for content creators, marketers, localizers, and translators. This is especially useful since different people on a team should only be responsible for the content in the locales they manage. In this tutorial, you will learn about its internationalization feature that allows you to manage content in different languages and locales. 

Your frontend also needs to handle your content in different languages and present it to multiple locales adequately and efficiently. Hugo is an amazing option for this. It’s a static site generator built with Go. It takes your data and content and applies it to templates. It then converts them to static pages, which are faster to deliver to your site visitors. 

Hugo builds sites pretty fast, with average site builds completed in a second or less. It supports several content types, enables theme integration, meticulously organizes your content, allows you to build your site in multiple languages, and write content in markdown. It also supports Google Analytics, comments with Disqus, code highlighting, and RSS. Static sites are faster, have great SEO scores, have better security, and are cheaper and less complicated to make.

Without further ado, let’s dive right in!

## Pre-Requisites

Before you can proceed with this tutorial, you will need to have:

1. **Hugo** installed.  
You can get it through [pre-built binaries](https://github.com/gohugoio/hugo/releases), which are available for macOS, Windows, Linux, and other operating systems. You can also install it from the command line. [These installation guides are available on the Hugo website](https://gohugo.io/getting-started/installing/#quick-install) explaining how to get it in this way. This tutorial was written using v0.68.
3. **Node.js** installed.  
Strapi requires at minimum Node.js 12 or higher but recommends Node.js 14. Do not install a version higher than 14 as Strapi may not support it. The [Node.js downloads page offers pre-built installers](https://nodejs.org/en/download/) for various operating systems on its website. 

## An Example Site

To illustrate how localization can work using Strapi and Hugo, you’ll build a documentation website for a product used in Canada, Mexico, and America. The top three languages spoken in those regions are English, French, and Spanish. So, the documents on this site need to be displayed in each of them. The site will have three pages: a home page, an about page, and a terms page. 

The Strapi CMS provides a platform to create content for those pages in those three languages. It will later serve the markdown versions of the content created through its API. The Hugo site will consume this content and display it depending on the language a user selects.  

{{% feature-panel %}}

## Step 1: Setting Up the Strapi App

In this step, you will install the Strapi app and set up an administrator account on its admin panel. The app will be called `docs-server`. To begin, on your terminal, change directories to the location you’d like the Strapi app to reside and run:

<pre><code class="language-bash">npx create-strapi-app@3.6.8 docs-server</code></pre>

When prompted:

1. Select `Quickstart` as the installation type. 
2. Pick `No` when asked to use a template.

<div class="break-out">

<pre><code class="language-bash">? Choose your installation type Quickstart (recommended)
? Would you like to use a template? (Templates are Strapi configurations designed for a specific use case) No</code></pre>
</div>

This command will create a Strapi quickstart project, install the dependencies it requires, and run the application. It will be available at [`http://localhost:1337`](http://localhost:1337). To register an administrator, head to [`http://localhost:1337/admin/auth/register-admin`](http://localhost:1337/admin/auth/register-admin). You should see the page below. 

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0f9980f5-bc48-46b7-85b4-6f26c289792c/2-build-localised-website-hugo-strapi.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0f9980f5-bc48-46b7-85b4-6f26c289792c/2-build-localised-website-hugo-strapi.png" width="800" height="439" sizes="100vw" caption="Strapi Sign Up Page. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0f9980f5-bc48-46b7-85b4-6f26c289792c/2-build-localised-website-hugo-strapi.png'>Large preview</a>)" alt="Strapi Sign Up Page" >}}

Enter your first and last names, an email, and a password. Once you’ve finished signing up, you will be redirected to the admin panel. Here’s what it looks like. 

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fcc78903-3e5a-40f5-acd0-4ca62e3be059/1-build-localised-website-hugo-strapi.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fcc78903-3e5a-40f5-acd0-4ca62e3be059/1-build-localised-website-hugo-strapi.png" width="800" height="439" sizes="100vw" caption="Strapi Admin Panel. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fcc78903-3e5a-40f5-acd0-4ca62e3be059/1-build-localised-website-hugo-strapi.png'>Large preview</a>)" alt="Strapi Admin Panel" >}}

On the admin panel, you can create content types, add content entries, and manage settings for the Strapi app. In this step, you generate the Strapi app and set up an administrator account. In the next one, you will create content types for each of the three pages. 

## Step 2: Create the Content Types

In this step, you will create content types for each of the three pages. A content type on Strapi, as the name suggests, is a type of content. Strapi supports two categories of content types: collection types and single types. A collection type is for content that takes a single structure and has multiple entries. 

For example, a blog post collection type collects multiple blog posts. A single type is for content that is unique and only has one entry. An about content type that models content for an about page, for instance, is a single type because a site typically has only one about page. 

To generate these types, you’re going to use the Strapi CLI. You have the option of using the existing Strapi admin panel to create the types if you wish. However, the Strapi CLI can be faster and involves fewer steps. 

If the Strapi is running, stop it. Running the commands in this step will cause errors that will crash the app. Once you’ve completed this step, you can run it again with the command below on your terminal within the `docs-server` directory:

<pre><code class="language-bash">npm run develop</code></pre>

Since you will have three separate pages, you will create three different single types. These will be the `home`, `about`, and `terms` types. Each will have a content and title attribute. These two attributes are just a starting point. You can modify the types later if you’d like to add more attributes or customize them further. To create them, run this command on your terminal within the `docs-server` directory:

<div class="break-out">

<pre><code class="language-bash">for page in home about terms; do npm run strapi generate:api $page title:string content:richtext ;done</code></pre>
</div>

Running the above command will generate the `home`, `about`, and `terms` content types with `title` and `content` attributes. It also generates APIs for each of the page types. The APIs are generated within the `api/` folder. Here’s what this folder looks like now. 

<pre><code class="language-bash">api
├── about
│   ├── config
│   │   └── routes.json
│   ├── controllers
│   │   └── about.js
│   ├── models
│   │   ├── about.js
│   │   └── about.settings.json
│   └── services
│       └── about.js
├── home
│   ├── config
│   │   └── routes.json
│   ├── controllers
│   │   └── home.js
│   ├── models
│   │   ├── home.js
│   │   └── home.settings.json
│   └── services
│       └── home.js
└── terms
    ├── config
    │   └── routes.json
    ├── controllers
    │   └── terms.js
    ├── models
    │   ├── terms.js
    │   └── terms.settings.json
    └── services
        └── terms.js</code></pre>

Each of the content types have models, services, controllers, and configuration created for them. Several API routes are added as well to create, modify, and retrieve content modeled against these types.

In the `api/about/models/about.settings.json` file, you will change the kind of the `about` content type from a collection type to a `singleType`. You will also add a description and enable localization for it and its attributes. Replace the code with the following:

<pre><code class="language-javascript">{
  "kind": "singleType",
  "collectionName": "about",
  "info": {
    "name": "about",
    "description": "The about page content"
  },
  "options": {
    "increments": true,
    "timestamps": true,
    "draftAndPublish": true
  },
  "pluginOptions": {
    "i18n": {
      "localized": true
    }
  },
  "attributes": {
    "title": {
      "pluginOptions": {
        "i18n": {
          "localized": true
        }
      },
      "type": "string"
    },
    "content": {
      "pluginOptions": {
        "i18n": {
          "localized": true
        }
      },
      "type": "richtext"
    }
  }
}</code></pre>

In this file, you are adding detail to the content type that you can’t specify when generating them through the CLI. The kind property changes to a `singleType` from a collection type. Localization is enabled using the `pluginOptions` property. By setting `localized` to `true` under the `i18n` internationalization property, localization is enabled for the type as well as the attributes that specify the same property.  

Next, you will modify its API routes to only have routes that will update, delete, and retrieve content. When you create a content type using the CLI, it is by default a collection type. A collection type has five routes created for it: routes to find, find one, count, delete, update, and post. A single type doesn’t need count, post and find-one routes since there’s just one entry. So you will be removing these. Replace the contents of `api/about/config/routes.json` with this code: 

<pre><code class="language-javascript">{
  "routes": [
    {
      "method": "GET",
      "path": "/about",
      "handler": "about.find",
      "config": {
        "policies": []
      }
    },
    {
      "method": "PUT",
      "path": "/about",
      "handler": "about.update",
      "config": {
        "policies": []
      }
    },
    {
      "method": "DELETE",
      "path": "/about",
      "handler": "about.delete",
      "config": {
        "policies": []
      }
    }
  ]
}</code></pre>

Since the other content types share the same attributes, you will make similar changes to the model settings for each of the other types. The content types in this tutorial share the same attributes for demonstration purposes but you can modify them to suit the needs of the pages you create. In the `api/privacy/models/home.settings.json` file, change the code to:

<pre><code class="language-javascript">{
  "kind": "singleType",
  "collectionName": "home",
  "info": {
    "name": "Home",
    "description": "The home page content"
  },
  "options": {
    "increments": true,
    "timestamps": true,
    "draftAndPublish": true
  },
  "pluginOptions": {
    "i18n": {
      "localized": true
    }
  },
  "attributes": {
    "title": {
      "type": "string",
      "pluginOptions": {
        "i18n": {
          "localized": true
        }
      }
    },
    "content": {
      "type": "richtext",
      "pluginOptions": {
        "i18n": {
          "localized": true
        }
      }
    }
  }
}</code></pre>

Similar to the about API routes, you will remove the find-one, count, and post routes for the home content type since it’s a single type. Replace the contents of the `api/home/config/routes.json` file with this code:

<pre><code class="language-javascript">{
  "routes": [
    {
      "method": "GET",
      "path": "/home",
      "handler": "home.find",
      "config": {
        "policies": []
      }
    },
    {
      "method": "PUT",
      "path": "/home",
      "handler": "home.update",
      "config": {
        "policies": []
      }
    },
    {
      "method": "DELETE",
      "path": "/home",
      "handler": "home.delete",
      "config": {
        "policies": []
      }
    }
  ]
}</code></pre>

Lastly, in the `api/terms/models/terms.settings.json` file, replace the existing code with:

<pre><code class="language-javascript">{
  "kind": "singleType",
  "collectionName": "terms",
  "info": {
    "name": "Terms",
    "description": "The terms content"
  },
  "options": {
    "increments": true,
    "timestamps": true,
    "draftAndPublish": true
  },
  "pluginOptions": {
    "i18n": {
      "localized": true
    }
  },
  "attributes": {
    "title": {
      "type": "string",
      "pluginOptions": {
        "i18n": {
          "localized": true
        }
      }
    },
    "content": {
      "type": "richtext",
      "pluginOptions": {
        "i18n": {
          "localized": true
        }
      }
    }
  }
}</code></pre>

To remove the unnecessary find-one, count and post API routes for the terms content type, change the contents of `api/terms/config/routes.json` to this:

<pre><code class="language-javascript">{
  "routes": [
    {
      "method": "GET",
      "path": "/terms",
      "handler": "terms.find",
      "config": {
        "policies": []
      }
    },
    {
      "method": "PUT",
      "path": "/terms",
      "handler": "terms.update",
      "config": {
        "policies": []
      }
    },
    {
      "method": "DELETE",
      "path": "/terms",
      "handler": "terms.delete",
      "config": {
        "policies": []
      }
    }
  ]
}</code></pre>

Now you have content types set up for all three pages. In the next step, you will add locales for the markets your content is targeted to. 

{{% ad-panel-leaderboard %}}

## Step 3: Adding the Locales

In this step, you will add the different locales you’d like to support. As explained in the example section, you will add **English(America)(en-US)**, **French(Canada)(fr-CA)**, and **Spanish(Mexico)(es-MX)**. Be sure to run Strapi with `npm run develop`, then go to the [Internationalization settings](http://localhost:1337/admin/settings/internationalization), under **Settings** then **Global Settings**, and add these locales by clicking the blue <kbd>Add a locale</kbd> button. 

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0c0428cf-b634-4b5d-9643-870b582c8448/12-build-localised-website-hugo-strapi.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0c0428cf-b634-4b5d-9643-870b582c8448/12-build-localised-website-hugo-strapi.png" width="800" height="299" sizes="100vw" caption="Locales in the Internationalization Settings in the Strapi Admin Panel. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0c0428cf-b634-4b5d-9643-870b582c8448/12-build-localised-website-hugo-strapi.png'>Large preview</a>)" alt="Locales in the Internationalization Settings in the Strapi Admin Panel" >}}

In the popup, select a locale then click <kbd>Add locale</kbd>. You should add the three locales listed in the table below. They are all available in the **Locales** dropdown.

<table class="tablesaw break-out">
  <thead>
  <tr>
   <th>Locale</th>
   <th>Local Display Name</th>
  </tr>
  </thead>
  <tbody>
  <tr>
   <td>en-US</td>
   <td>English(America)</td>
  </tr>
  <tr>
   <td>es-MX</td>
   <td>Spanish(Mexico)</td>
  </tr>
  <tr>
   <td>fr-Ca</td>
   <td>French(Canada)</td>
  </tr>
  </tbody>
</table>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9e5beeb8-7f51-4e05-96dc-19dbad78a49b/3-build-localised-website-hugo-strapi.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9e5beeb8-7f51-4e05-96dc-19dbad78a49b/3-build-localised-website-hugo-strapi.png" width="800" height="310" sizes="100vw" caption="<code>Add a locale</code> pop-up in the Strapi Internationalization Settings. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9e5beeb8-7f51-4e05-96dc-19dbad78a49b/3-build-localised-website-hugo-strapi.png'>Large preview</a>)" alt="Add a locale pop-up in the Strapi Internationalization Settings" >}}

When adding these locales, set one as the default locale under **Advanced Settings** in the **Add a locale** pop-up. This makes it easier when adding content the first time around. If you do not, the first entry will always default to the **en** locale. If you do not need the **en** locale, it’s best to delete it after setting an alternate default locale.  

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/79321e5b-60d7-4f48-bee4-21780689e638/10-build-localised-website-hugo-strapi.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/79321e5b-60d7-4f48-bee4-21780689e638/10-build-localised-website-hugo-strapi.png" width="800" height="279" sizes="100vw" caption="Default Locale Advanced Settings in the Strapi Internationalization Settings. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/79321e5b-60d7-4f48-bee4-21780689e638/10-build-localised-website-hugo-strapi.png'>Large preview</a>)" alt="Default Locale Advanced Settings in the Strapi Internationalization Settings" >}}

In this step, you added locales on your Strapi app. These will be used when you add content. In the proceeding step, you will add placeholder content for each of the pages.

## Step 4: Add Content to Strapi App

In this step, you will add content to the Strapi app for each of the three pages. You will do this using the content manager on the admin panel. Here are links to content entry forms on the admin panel for each of the types:

1. [**About** page](http://localhost:1337/admin/plugins/content-manager/singleType/application::about.about)
2. [**Home** page](http://localhost:1337/admin/plugins/content-manager/singleType/application::home.home?plugins[i18n][locale]=en-US)
3. [**Terms** page](http://localhost:1337/admin/plugins/content-manager/singleType/application::terms.terms)

Here’s what a content entry form looks like. 

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dee117d4-67c7-4253-86a5-dc4fbcee78f0/8-build-localised-website-hugo-strapi.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dee117d4-67c7-4253-86a5-dc4fbcee78f0/8-build-localised-website-hugo-strapi.png" width="800" height="447" sizes="100vw" caption="Content Manager Form to add content for the About Single Type. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dee117d4-67c7-4253-86a5-dc4fbcee78f0/8-build-localised-website-hugo-strapi.png'>Large preview</a>)" alt="Content Manager Form to add content for the About Single Type" >}}

Add a title and some content. When adding content, always check the locale. Make sure the language of the content matches the locale language. 

Once you’re done, click the bright green <kbd>Save</kbd> button then the <kbd>Publish</kbd> button in the top right of the entry form. When you want to add new content for a locale, select it from the **Locales** dropdown in the **Internationalization** section on the right of the form. Remember to save and publish the new content. 

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fd9dce13-e083-432e-8f7f-1e865ec856f2/4-build-localised-website-hugo-strapi.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fd9dce13-e083-432e-8f7f-1e865ec856f2/4-build-localised-website-hugo-strapi.png" width="800" height="499" sizes="100vw" caption="List of Locales available on Content Manager Entry Form. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fd9dce13-e083-432e-8f7f-1e865ec856f2/4-build-localised-website-hugo-strapi.png'>Large preview</a>)" alt="List of Locales available on Content Manager Entry Form" >}}

Here’s what you’ll add for each of the pages for the `title` field:

<table class="tablesaw break-out">
  <thead>
  <tr>
   <th>English (America)(en-US)</th>
   <th>French (Canada)(fr-CA)</th>
   <th>Spanish (Mexico)(ex-MX)</th>
  </tr>
    </thead>
  <tbody>
  <tr>
   <td>About</td>
   <td>À propos</td>
   <td>Sobre</td>
  </tr>
  <tr>
   <td>Home</td>
   <td>Accueil</td>
   <td>Hogar</td>
  </tr>
  <tr>
   <td>Terms</td>
   <td>Conditions</td>
   <td>Condiciones</td>
  </tr>
  </tbody>
</table>

For the content, you can use this lorem ipsum text for all the pages. You can add a flag emoji for the country to identify the change in locale. This is placeholder content only for demonstration purposes. 

<table class="tablesaw break-out">
  <tbody>
  <tr>
   <td><strong>English (America)(en-US)</strong></td>
   <td># 🇺🇸<br /><br />Lorem ipsum dolor sit amet, consectetur adipiscing elit. Donec nec neque ultrices, tincidunt tellus a, imperdiet nulla. Aliquam erat volutpat. Vestibulum finibus, lectus sit amet sagittis euismod, arcu eros tincidunt augue, non lobortis tortor turpis non elit.</td>
  </tr>
  <tr>
   <td><strong>French (Canada)(fr-CA)</strong></td>
   <td># 🇨🇦<br /><br />Lorem ipsum dolor sit amet, consectetur adipiscing elit. Donec nec neque ultrices, tincidunt tellus a, imperdiet nulla. Aliquam erat volutpat. Vestibulum finibus, lectus sit amet sagittis euismod, arcu eros tincidunt augue, non lobortis tortor turpis non elit.</td>
  </tr>
  <tr>
   <td><strong>Spanish (Mexico)(ex-MX)</strong></td>
   <td># 🇲🇽<br /><br />Lorem ipsum dolor sit amet, consectetur adipiscing elit. Donec nec neque ultrices, tincidunt tellus a, imperdiet nulla. Aliquam erat volutpat. Vestibulum finibus, lectus sit amet sagittis euismod, arcu eros tincidunt augue, non lobortis tortor turpis non elit.</td>
  </tr>
  </tbody>
</table>

In this step, you added placeholder content in multiple languages for different locales. In the next step, you will make the API routes for the content types public. 

## Step 5: Making the API Routes Public

In this step, you will make the routes that return page content public. These are the **GET** routes for  `/home`, `/about`, and `/terms`. Currently, if you try to access them, you will get a `403` **Forbidden** error. This is because the permissions set do not allow them to be accessed publicly. You’ll change this so that they are publicly accessible. 

To do this:

1. head over to [the **Public Roles settings** under **Users & Permissions Plugin** using this link](http://localhost:1337/admin/settings/users-permissions/roles/2);
2. in the **Application** settings, under **Permissions**, select the **find** checkboxes for **Home**, **About**, and **Terms**;
3. click the bright green <kbd>Save</kbd> button in the top right of the page. 

Here’s a screenshot of what checkboxes to select in the **Application Permissions** section in the **Public Roles** settings page:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a2b623f1-db30-4107-beeb-191cd7102ed2/9-build-localised-website-hugo-strapi.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a2b623f1-db30-4107-beeb-191cd7102ed2/9-build-localised-website-hugo-strapi.png" width="800" height="517" sizes="100vw" caption="Application Permissions on the Public Roles settings page. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a2b623f1-db30-4107-beeb-191cd7102ed2/9-build-localised-website-hugo-strapi.png'>Large preview</a>)" alt="Application Permissions on the Public Roles settings page" >}}

Now the routes at [`http://localhost:1337/home`](http://localhost:1337/home), [`http://localhost:1337/about`](http://localhost:1337/home), and [`http://localhost:1337/terms`](http://localhost:1337/home) are all accessible. They return the content you entered for the pages in the previous step. To specify a locale when fetching content, use the `_locale` query parameter and assign it the locale. For example, [`http://localhost:1337/home?_locale=fr-CA`](http://localhost:1337/home?_locale=fr-CA) will return the home page for the Canadian French locale. If you do not specify a locale, content for the default locale will be returned.

In this step, you made the routes that return content public. In the next step, you will generate a Hugo site that will consume the localized content. 

## Step 6: Generate a New Hugo Site

The Hugo site that will display the localized content will be called `docs-app`. To generate it, run the following command on your terminal in a separate directory outside the `docs-server` project:

<pre><code class="language-bash">hugo new site docs-app</code></pre>

Running this command will generate a new Hugo site. It will scaffold the site with different folders that contain site input. Hugo will use this input and generate a whole site. However, no themes nor content have been added. You will have to add the content and theme. The content will come from the Strapi application. You can view the new site by running:

<pre><code class="language-bash">cd docs-app && hugo server</code></pre>

The app is served at [`http://localhost:1313/`](http://localhost:1313/). However, the app is blank since there is no content yet. 

In this step, you generated a new Hugo site. In the next step, you will add a documentation theme to it. 

## Step 7: Add a Theme to the Hugo Site

Hugo provides support for themes. You can add pre-configured theme components to your site. For the purpose of this tutorial, you will use the [hugo-book theme](https://themes.gohugo.io/themes/hugo-book/), which is a theme for documentation sites. You can pick from a wide range of themes available on the [Hugo theme showcase site](https://themes.gohugo.io/). However, make sure that the theme [supports internationalization](https://gohugo.io/content-management/multilingual/). 

To add the book theme, make sure you are in the `docs-app` folder, and if not, run:

<pre><code class="language-bash">cd docs-app</code></pre>

The app needs to have a git repository to add a theme as a git submodule. To initialize an empty one, run:

<pre><code class="language-bash">git init</code></pre>

To add the book theme, run:

<div class="break-out">

<pre><code class="language-bash">git submodule add https://github.com/alex-shpak/hugo-book themes/book</code></pre>
</div>

This command adds the book theme repository as a submodule to the site. It clones the book theme into the `themes` folder. To view the` docs-app` site using the book theme, you can run the app with this command:

<pre><code class="language-bash">hugo server --theme book</code></pre>

Here’s a screenshot of what it looks like:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f865dbbe-366e-4330-93e8-e280d730692e/5-build-localised-website-hugo-strapi.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f865dbbe-366e-4330-93e8-e280d730692e/5-build-localised-website-hugo-strapi.png" width="800" height="480" sizes="100vw" caption="The site using the hugo-book theme. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f865dbbe-366e-4330-93e8-e280d730692e/5-build-localised-website-hugo-strapi.png'>Large preview</a>)" alt="The site using the hugo-book theme" >}}

The site is still pretty bare as it does not contain any content yet. You’ll add content to it from Strapi in the later steps.

In this step, you added a theme to your Hugo site that supports internationalization. In the following step, you will modify the setting of the `docs-app` site to support internationalization. 

## Step 8: Modify the Hugo Site Settings

While the book theme supports internationalization, you have to modify the settings of the `docs-app` to enable it. You will also modify other attributes of the site, like its title and base URL. Additionally, you will include other settings to disable search on the book theme and limit the cache lifespan. In the `config.toml` file, remove the existing code and add the one below:

<div class="break-out">

<pre><code class="language-bash"># The site base URL
baseURL = 'http://localhost:1313/'

# The default site and content language
languageCode = 'en-us'
defaultContentLanguage = 'en-us'

# The site title
title = 'Docs'

# Setting the site theme to hugo-book
theme = 'book'

[params]
# Disabling search here because it falls out of the scope of this tutorial
BookSearch = false
# The Strapi server URL
StrapiServerURL = 'http://localhost:1337'

[caches]
[caches.getjson]
# Sets the maximum age of cache to 10s before it is cleared.
maxAge = "10s"

[languages]
# The US English content settings
[languages.en-us]
languageName = "English (US)"
contentDir = "content"
# The Canadian French content settings
[languages.fr-ca]
languageName = "Français (Canada)"
contentDir = "content.fr-ca"
# The Mexican Spanish content settings
[languages.es-mx]
languageName = "Español (Mexico)"
contentDir = "content.es-mx"</code></pre>
</div>

The `StrapiServerURL` is the URL of the Strapi server. Since it’s running locally for now, you will use [`http://localhost:1337`](http://localhost:1337). You’re going to use the [`getJSON`](https://gohugo.io/templates/data-templates/#get-remote-data) Hugo function to fetch data from the server. It caches request results. During development, you may change the content on the Strapi app often, and because of cache, it may not reflect the changes you make. So, using the `maxAge` config property, you will set it to `10s`; thus, the most recent Strapi content changes appear on the site. When you deploy the site, you will have to change this to an adequate timespan depending on how often the site is rebuilt, and the content is changed. 

For the language settings, you will define three language categories. For each language, you will define a name and a directory for its content. Each of the content directories will be at the site root. The language names will be displayed in a dropdown where users can select what content they want. Here’s a table of the settings for each language. 

<table class="tablesaw break-out">
  <thead>
    <tr>
      <th>Language Name</th>
      <th>Language Code</th>
      <th>Content Directory</th>
    </tr>
  </thead>
  <tbody>
    <tr>
   <td>English (US)</td>
   <td>en-us</td>
      <td><code>content/</code></td>
  </tr>
  <tr>
   <td>Español (Mexico)</td>
   <td>es-mx</td>
   <td><code>content.es-mx/</code></td>
  </tr>
  <tr>
   <td>Français (Canada)</td>
   <td>fr-ca</td>
   <td><code>content.fr-ca/</code></td>
  </tr>
  </tbody>
</table>

In this step, you added settings to the Hugo app to make it support internationalization. In the next step, you will modify the theme to accept localized content from an external server. 

{{% ad-panel-leaderboard %}}

## Step 9: Modify the Theme to Accept Strapi Content

In this step, you will modify the theme to accept data from a Strapi server. Although themes already come with pre-configured templates, [you can override them](https://gohugo.io/templates/lookup-order/) by creating similar files in the `layouts` folder. 

For the **[hugo-book](https://themes.gohugo.io/themes/hugo-book/)** theme, you will modify the template at `themes/book/layouts/partials/docs/inject/content-after.html`. This template displays whatever is added in it after the main page content. To do this, you will create this file in the `layouts/` folder at the site’s root directory and then add content to it. In this file, you will define a template to fetch markdown content from the server, pass it through [the markdown processor](https://gohugo.io/functions/markdownify/#readout), and display it. The logic to fetch the content will be placed in a new [partial template](https://gohugo.io/templates/partials/#readout) that you will call `strapi-content`. So, to create the `content-after` file, run these commands on your terminal:

<div class="break-out">

<pre><code class="language-bash">mkdir -p layouts/partials/docs/inject/ && touch layouts/partials/docs/inject/content-after.html</code></pre>
</div>

Next, you will create the partial template to fetch content from Strapi:

<div class="break-out">

<pre><code class="language-bash">touch layouts/partials/docs/strapi-content.html</code></pre>
</div>

In the `layouts/partials/docs/strapi-content.html` file, add this code:

<div class="break-out">

<pre><code class="language-javascript">&lt;!-- Partial to fetch content from Strapi. --&gt;

{{ $endpoint := $.Param "endpoint" }}
{{ $data := dict "title" "" "content" "" }}

{{ if and $endpoint .Site.Params.StrapiServerURL }}

{{ $contentURL := printf "%s%s" .Site.Params.StrapiServerURL $endpoint }}
{{ $data = getJSON $contentURL }}

{{ end }}

{{ return $data }}</code></pre>
</div>

In this partial file, you fetch the endpoint page variable for a specific page and store it in `$endpoint`. This variable is added to the [front matter of content files](https://gohugo.io/content-management/front-matter#readout), as you will see in the proceeding step. Next, you create a variable called `$data` that is returned at the end of the partial. It will hold the content returned from the Strapi server. You will then assign it a default structure with a title and content. This is done in case no endpoint is specified, or a request is unsuccessful. Afterward, you check if a content endpoint and a Strapi server URL is set. You need both of these for a request. If set, you create a URL for the content you need and use the `getJSON` function to make a request. Lastly, you return the data. 

In `layouts/partials/docs/inject/content-after.html`, add the code below to the file:

<pre><code class="language-javascript">{{ $strapiData := partial "docs/strapi-content" . }}
&lt;article class="markdown"&gt;
  &lt;h1&gt;{{ $strapiData.title }}&lt;/h1&gt;

  {{ $strapiData.content | markdownify }}
&lt;/article&gt;</code></pre>

Here, you are fetching the data using the `strapi-content` partial template. Once you get the content, you add the title as a heading within the `article` tag. Lastly, you take the returned content, pass it through the markdown processor using the `markdownify` function, and display it within the `article` tag. 

In this step, you modified the theme by overriding one of its templates and adding a new partial template to fetch content from Strapi. In the next step, you will add content pages for each of the languages. 

## Step 10: Add Content Pages to the Hugo Site 

In this step, you will add content pages. Each language has a content folder, as shown in the previous steps. The `content` folder is for English(US) content, `content.es-mx` for Español (Mexico) content, and `content.fr-ca` for Français (Canada) content. Each content file has to have an `endpoint` [front matter variable](https://gohugo.io/content-management/front-matter#readout) which is the Strapi endpoint that provides its content in a specific language. You’ll add this variable in two [archetypes files](https://gohugo.io/content-management/archetypes/#readout), `archetypes/default.md` and `archetypes/docs.md`. 

Archetype files are templates for content files. They can be used to specify the [front matter](https://gohugo.io/content-management/front-matter/) and other content. The `hugo new` command uses archetypes to generate new content files. `archetypes/default.md` will be the template for all the `_index.md` content files while `archetypes/docs.md` will be for all the content files in `docs/` folders. `archetypes/docs.md` and `docs/` are specific to the <strong>hugo-book</strong> theme. To create the `archetypes/docs.md` file on your terminal:

<pre><code class="language-bash">touch archetypes/docs.md</code></pre>

Next, replace the content of both `archetypes/default.md` and `archetypes/docs.md` with:

<pre><code class="language-javascript">---
title: "{{ replace .Name "-" " " | title }}"
endpoint: "/"
---

&lt;br/&gt;</code></pre>

The `title` will be displayed as the page title and in the table of contents. `endpoint`, as mentioned earlier, is the Strapi endpoint that provides the content. You add the `<br/>` tag so that the page is not considered blank during a build. 

To create the content folders for the other languages, run this command on your terminal:

<pre><code class="language-bash">mkdir content.es-mx content.fr-ca</code></pre>

Next, add content files for each of the pages:

<div class="break-out">

<pre><code class="language-bash">for cont in "_index.md" "docs/about.md" "docs/terms.md"; do hugo new  $cont; done && for langDir in  "content.es-mx" "content.fr-ca" ; do cp -R content/&#42; $langDir; done</code></pre>
</div>

This command creates an `_index.md` file, a `docs/about.md` file, and a `docs/terms.md` file in each of the content directories. Here’s what the content directories will look like after you run this command:

<pre><code class="language-bash">content
├── docs
│   ├── about.md
│   └── terms.md
└── index.md
content.es-mx
├── docs
│   ├── about.md
│   └── terms.md
└── index.md
content.fr-ca
├── docs
│   ├── about.md
│   └── terms.md
└── index.md</code></pre>

Here’s the front matter and content you should add for each of the files:

**Home (`index.md`)**

- `content`

<pre><code class="language-javascript">---
title: "Home"
endpoint: "/home?_locale=en-US"
---

&lt;br/&gt;</code></pre>

- `content.es-mx`

<pre><code class="language-javascript">---
title: "Hogar"
endpoint: "/home?_locale=es-MX"
---

&lt;br/&gt;</code></pre>

- `content.fr-ca`

<pre><code class="language-javascript">---
title: "Accueil"
endpoint: "/home?_locale=fr-CA"
---

&lt;br/&gt;</code></pre>

**About (`docs/about.md`)**

- `content`

<pre><code class="language-javascript">---
title: "About"
endpoint: "/about?_locale=en-US"
---

&lt;br/&gt;</code></pre>

- `content.es-mx`

<pre><code class="language-javascript">---
title: "Sobre"
endpoint: "/about?_locale=es-MX"
---

&lt;br/&gt;</code></pre>

- `content.fr-ca`

<pre><code class="language-javascript">---
title: "À propos"
endpoint: "/about?_locale=fr-CA"
---

&lt;br/&gt;</code></pre>

**Terms (`docs/terms.md`)**

- `content`

<pre><code class="language-javascript">---
title: "Terms"
endpoint: "/terms?_locale=en-US"
---

&lt;br/&gt;</code></pre>

- `content.es-mx`

<pre><code class="language-javascript">---
title: "Condiciones"
endpoint: "/terms?_locale=es-MX"
---

&lt;br/&gt;</code></pre>

- `content.fr-ca`

<pre><code class="language-javascript">---
title: "Conditions"
endpoint: "/terms?_locale=fr-CA"
---

&lt;br/&gt;</code></pre>

So, all you need to do now is run the Hugo server. Before you do this, make sure that the Strapi app is running with `npm run develop` in a different terminal within the `docs-server` folder, so Hugo can fetch content from it when building the site. You can run the Hugo server using this command:

<pre><code class="language-bash">hugo server</code></pre>

{{< youtube id="VaxlpBFrl_w" breakout="true" caption="Here’s a video of the app in action." >}}

Here are some screenshots of the site in different languages: 

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5aff68dc-3886-406c-9950-070150dd35ab/11-build-localised-website-hugo-strapi.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5aff68dc-3886-406c-9950-070150dd35ab/11-build-localised-website-hugo-strapi.png" width="800" height="259" sizes="100vw" caption="English (US) Home Page. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5aff68dc-3886-406c-9950-070150dd35ab/11-build-localised-website-hugo-strapi.png'>Large preview</a>)" alt="English (US) Home Page" >}}

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6532ee74-a517-4831-9491-286b6515baac/7-build-localised-website-hugo-strapi.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6532ee74-a517-4831-9491-286b6515baac/7-build-localised-website-hugo-strapi.png" width="800" height="264" sizes="100vw" caption="The Español (Mexico) Terms Page. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6532ee74-a517-4831-9491-286b6515baac/7-build-localised-website-hugo-strapi.png'>Large preview</a>)" alt="The Español (Mexico) Terms Page" >}}

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/291c5272-271a-4f5a-92f9-2a9e9f6fd1ad/6-build-localised-website-hugo-strapi.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/291c5272-271a-4f5a-92f9-2a9e9f6fd1ad/6-build-localised-website-hugo-strapi.png" width="800" height="276" sizes="100vw" caption="The Français (Canada) About Page. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/291c5272-271a-4f5a-92f9-2a9e9f6fd1ad/6-build-localised-website-hugo-strapi.png'>Large preview</a>)" alt="The Français (Canada) About Page" >}}

### Note About Routine Automated Rebuilds

Since Hugo creates static sites, the content displayed will not be dynamic. Hugo gets the content from the Strapi server during build time and not on the fly when a page is requested. So, if you’d like content to regularly reflect what is on the Strapi server, make sure to automate rebuilds of your Hugo site regularly or as often as changes to the content are made. For example, if your site is hosted on Netlify, you can schedule regular rebuilds of your site. 

## Conclusion

Hugo is a static site generator that allows you to build fast and efficient static sites. It offers multilingual support using its internationalization feature. You can specify a range of languages, and Hugo will build a site to support each of them. Strapi is a headless CMS that allows its users to manage content with more flexibility. It provides an admin portal to enter and manage content and a customizable API that different frontends can consume the content through. It also offers an internationalization plugin to manage content in different locales. 

In this tutorial, you created a Strapi application. Using this app, you added three single content types to represent data for three pages: a home, an about, and a terms page. You added content for each of the pages for three locales: English (US), Español (Mexico), and Français (Canada). You also generated APIs to access content for these pages and made some of its routes public. 

After, you generated a Hugo app. In this app, you added a documentation theme, configuration to support internationalization, and content pages for different languages. Lastly, you modified the theme to consume content from Strapi. If you’d like to build out more of the app, try adding more content page types with complex structures or adding content in a new language.

If you’d like to learn more about Hugo, [check out their documentation page](https://gohugo.io/documentation/). To find out more about what you can do with Strapi and the range of features it offers, head to [its website here](https://strapi.io/). 

{{< signature "yk, il">}}
