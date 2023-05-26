---
title: 'Adding Search To Your Site In 15 Minutes'
slug: adding-search-website-sitesearch360
author: leonardolosoviz
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b95673f7-c059-4fae-a74a-bd1929230b29/adding-search-website-sitesearch360.jpg
date: 2022-06-14T09:00:00.000Z
summary: >-
  Do you need search for your site, but haven’t found the time to add it? Within 15 minutes, Leonardo Losoviz explains how you can add a super powerful search that also looks super good. In this article, you’ll learn how to go from 0 to 100 with search.
description: >-
  Do you need search for your site, but haven’t found the time to add it? Within 15 minutes, Leonardo Losoviz explains how you can add a super powerful search that also looks super good. In this article, you’ll learn how to go from 0 to 100 with search.
categories:
  - SEO
  - Tools
  - Search
  - Usability
disable_ads: true
disable_panels: true
disable_newsletterbox: true
sponsor:
  title: Site Search 360
  link: https://www.sitesearch360.com/
  image: https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/55aa9b65-116e-4454-aef2-85d805adb187/site-search-360.svg
  description: >-
    This article has been kindly supported by our dear friends at <a href="https://www.sitesearch360.com/">Site Search 360</a> who help folks optimize their search and boost their best content by using powerful analytics to reveal the intention behind every search. <em>Thank you!</em>
---

My site has been created using a static site generator and deployed to a CDN, so I’m super happy with how fast it is. But there has been a functionality that I’ve been missing all along: search.
 
As it’s been mentioned many times, Jamstack doesn’t mean “static” &mdash; we can perfectly create fully dynamic sites powered by JavaScript on the client-side interacting with (mostly third-party) APIs. Search falls within this category.

All this time, I hadn’t added search to my site because I was weary it would prove to be a difficult task. I’m not exceptionally skilled in JavaScript or CSS, so I feared that creating an elegant (or, at least, respectable) search input that suggests results as the user types, and integrating it into my site, would fall outside of my abilities.
 
And then, all of a sudden, in actually less than 15 minutes, I had search on my site!
 
{{< vimeo id="718450273" caption="A preview of the search input available on <a href=' https://graphql-api.com/'>my website</a>." >}}

This was made possible thanks to [Site Search 360](https://www.sitesearch360.com/features/), a service providing search for any site, whether based on Jamstack (like mine), WordPress (for which [they have a plugin](https://www.sitesearch360.com/wordpress-plugin/)), or [any other stack](https://www.sitesearch360.com/?q=integrations). I had planned to do some research on this service first, but as it turned out, even before my research was over, I ended up installing their service and having search on my site, to my absolute (and initially unexpected) delight.
 
The gist of the whole process is: As I signed up for a free account, this service indexed my site straight from the open Internet without asking me to provide any configuration. It then drove me through a few steps to configure the search user interface and finally produced a link to a JavaScript file with my custom configuration. As I included this JS on my site and refreshed the browser, voilà, I had search!
 
It really took no time, and it also looks great. In this article, I’ll show you how to add search to your site using Site Search 360, as I’ve done. By the time you finish reading this article, if you follow along, you may already have search. 🙏
 
## Adding Search To Your Website With Site Search 360

On the homepage of [Site Search 360](https://www.sitesearch360.com/), there’s an input asking to “Enter your domain (site.com).” Do it, and click on “Free test.” Then it will say, “Yeah! Your free trial is ready,” and ask you to enter your email to complete the registration. Do it, and click on “Go!”.
 
 {{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cd43dd1b-f03d-4f0f-8a2e-cef7374c1a58/1-adding-search-website-sitesearch360.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cd43dd1b-f03d-4f0f-8a2e-cef7374c1a58/1-adding-search-website-sitesearch360.png" width="800" height="" sizes="100vw" caption="Enter your domain to register with a free account. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cd43dd1b-f03d-4f0f-8a2e-cef7374c1a58/1-adding-search-website-sitesearch360.png'>Large preview</a>)" alt="Enter your domain to register with a free account" >}}

After this, the service will spend a minute or two indexing your site (or maybe a few more, depending on how much content your site has), and then inform you that it’s all ready.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e8eb87db-63ac-4a6c-9786-08013d4f7bc1/2-adding-search-website-sitesearch360.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e8eb87db-63ac-4a6c-9786-08013d4f7bc1/2-adding-search-website-sitesearch360.png" width="800" height="" sizes="100vw" caption="All ready! (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e8eb87db-63ac-4a6c-9786-08013d4f7bc1/2-adding-search-website-sitesearch360.png'>Large preview</a>)" alt="All ready" >}}

Click on “Let’s Get Started!” to go to the application dashboard, where an onboarding process will guide you in setting-up search for your site.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fec796b2-9b8f-4531-af62-cb203c7e629d/3-adding-search-website-sitesearch360.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fec796b2-9b8f-4531-af62-cb203c7e629d/3-adding-search-website-sitesearch360.png" width="800" height="" sizes="100vw" caption="Onboarding process (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fec796b2-9b8f-4531-af62-cb203c7e629d/3-adding-search-website-sitesearch360.png'>Large preview</a>)" alt="Onboarding process" >}}

Since your site’s content has been indexed by now, when clicking on “Test now!” the preview of the search UI will already use your site’s actual content. Notice how, even before you start customizing the look and feel, it looks great!

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/db50c01f-3cab-4b4e-b42f-5a589138de8d/4-adding-search-website-sitesearch360.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/db50c01f-3cab-4b4e-b42f-5a589138de8d/4-adding-search-website-sitesearch360.png" width="800" height="" sizes="100vw" caption="Previewing the search input and dropdown (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/db50c01f-3cab-4b4e-b42f-5a589138de8d/4-adding-search-website-sitesearch360.png'>Large preview</a>)" alt="Previewing the search input and dropdown" >}}

Click on “More results” in the suggestions dropdown to visualize what the search results will look like. (Below, we’ll see how this list, initially displaying the item’s thumbnail, title, URL, and excerpt with the matching term in bold, can be modified.)
 
{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/64f87a80-ac5e-4ded-9d22-54d31caa1761/5-adding-search-website-sitesearch360.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/64f87a80-ac5e-4ded-9d22-54d31caa1761/5-adding-search-website-sitesearch360.png" width="800" height="" sizes="100vw" caption="Previewing the search results (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/64f87a80-ac5e-4ded-9d22-54d31caa1761/5-adding-search-website-sitesearch360.png'>Large preview</a>)" alt="Previewing the search results" >}}

Click on the “Search Designer” button to customize the search UI, and replicate the style on your site. This step is not a one-time off: you can come back to it at any moment (even after your custom configuration has been published and search is already installed on your site).

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/142ead2f-a7e3-41c4-a07f-14fa55bb427d/6-adding-search-website-sitesearch360.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/142ead2f-a7e3-41c4-a07f-14fa55bb427d/6-adding-search-website-sitesearch360.png" width="800" height="" sizes="100vw" caption="Search Designer button (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/142ead2f-a7e3-41c4-a07f-14fa55bb427d/6-adding-search-website-sitesearch360.png'>Large preview</a>)" alt="Search Designer button" >}}

The welcome screen asks how we’d like to start. Since we are new users, we must start from scratch and click on “Start now”.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c9726ba6-5724-4dae-b799-51d671f96a4d/7-adding-search-website-sitesearch360.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c9726ba6-5724-4dae-b799-51d671f96a4d/7-adding-search-website-sitesearch360.png" width="800" height="" sizes="100vw" caption="Starting with the Search Designer (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c9726ba6-5724-4dae-b799-51d671f96a4d/7-adding-search-website-sitesearch360.png'>Large preview</a>)" alt="Starting with the Search Designer" >}}

We are now using the [Search Designer](https://www.sitesearch360.com/blog/create-your-site-search-experience-with-our-no-code-tool/) which will help you edit the visual appearance of the search input, dropdown, and results.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b5c58a4a-821e-420b-b31f-6be21908c523/8-adding-search-website-sitesearch360.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b5c58a4a-821e-420b-b31f-6be21908c523/8-adding-search-website-sitesearch360.png" width="800" height="" sizes="100vw" caption="Search Designer (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b5c58a4a-821e-420b-b31f-6be21908c523/8-adding-search-website-sitesearch360.png'>Large preview</a>)" alt="Search Designer" >}}

As you edit the styles, these are immediately reflected on the right-side pane.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/93c65bd2-a6df-4d44-b014-3307fb91d319/9-adding-search-website-sitesearch360.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/93c65bd2-a6df-4d44-b014-3307fb91d319/9-adding-search-website-sitesearch360.png" width="800" height="" sizes="100vw" caption="Real time preview (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/93c65bd2-a6df-4d44-b014-3307fb91d319/9-adding-search-website-sitesearch360.png'>Large preview</a>)" alt="Real time preview" >}}

In the Search Designer, you can configure the following elements (among many more):
 
- The primary, secondary, background, text, icon and border colors, text size, rounded corners size, and other styles;
- The language (from among 19 supported languages to date);
- Using a search input you already have on your site or the one by Site Search 360;
- Enabling autocomplete suggestions (displayed as the user is typing);
- Connect to Google Analytics and Google Tag Manager;
- Enabling voice search;
- Layouts to display results on desktop and mobile.

The search dropdown can be further configured, allowing to display the previously-searched queries and also predefined queries. In my case, I’ve decided to already suggest those search queries that make my site rank high on Google.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/aaf454c7-2867-4245-8a8b-bc823ed235f6/10-adding-search-website-sitesearch360.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/aaf454c7-2867-4245-8a8b-bc823ed235f6/10-adding-search-website-sitesearch360.png" width="800" height="" sizes="100vw" caption="Pre-defined suggestions (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/aaf454c7-2867-4245-8a8b-bc823ed235f6/10-adding-search-website-sitesearch360.png'>Large preview</a>)" alt="Pre-defined suggestions" >}}

Once done with the configuration, let’s go back to the onboarding process.
 
The next step is to tweak the search results, indicating how to extract the data (for the title, images, and excerpt) from the webpage. The default automatic configuration already works very well (extracting the data from the `<meta>` attributes), so you can quite likely skip this step.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/96191660-dc2e-42c5-9e1e-44b5f8eb801c/11-adding-search-website-sitesearch360.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/96191660-dc2e-42c5-9e1e-44b5f8eb801c/11-adding-search-website-sitesearch360.png" width="800" height="" sizes="100vw" caption="Tweaking the search results (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/96191660-dc2e-42c5-9e1e-44b5f8eb801c/11-adding-search-website-sitesearch360.png'>Large preview</a>)" alt="Tweaking the search results" >}}

You’re pretty much done by now! All there’s left to do is to publish the configuration.
 
Go back to the onboarding process, and click on “Install now!”. This will open a modal window; copy the HTML code and paste it into your site’s source code (before the closing `</body>`), and click on “Publish.”
 
{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4acf9f9f-886b-4b34-ade1-3c4063ab6e28/12-adding-search-website-sitesearch360.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4acf9f9f-886b-4b34-ade1-3c4063ab6e28/12-adding-search-website-sitesearch360.png" width="800" height="" sizes="100vw" caption="Publish the configuration (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4acf9f9f-886b-4b34-ade1-3c4063ab6e28/12-adding-search-website-sitesearch360.png'>Large preview</a>)" alt="Publish the configuration" >}}

Re-deploy your site, refresh the browser, and what do you have? Your site now has search!

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/edfbf412-8387-4bbf-a3be-3790c00f65b0/13-adding-search-website-sitesearch360.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/edfbf412-8387-4bbf-a3be-3790c00f65b0/13-adding-search-website-sitesearch360.png" width="800" height="" sizes="100vw" caption="My site has search! (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/edfbf412-8387-4bbf-a3be-3790c00f65b0/13-adding-search-website-sitesearch360.png'>Large preview</a>)" alt="My site has search!" >}}

## Updating The Visual Appearance

As I mentioned earlier on, you can keep configuring the search UI even after search is live. From now on, you can easily access the Search Designer from the application menu on the left (under the item “Design & Publish”). After doing some modification, clicking on “Publish” will already apply the new style on your site without having to copy/paste any new code or re-deploy the site.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/23ef599f-f7d5-4aba-91c8-f2f6cd9db55e/14-adding-search-website-sitesearch360.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/23ef599f-f7d5-4aba-91c8-f2f6cd9db55e/14-adding-search-website-sitesearch360.png" width="800" height="" sizes="100vw" caption="Design & Publish (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/23ef599f-f7d5-4aba-91c8-f2f6cd9db55e/14-adding-search-website-sitesearch360.png'>Large preview</a>)" alt="Design & Publish" >}}

In my case, I tweaked the configuration a bit more. I changed my mind about the position of the search input, preferring to display it on top of the navigation. The solution was to wrap the navigation menu in a new `<div id="nav-wrapper">`  element and then inject the input “Before” the `#nav-wrapper` selector.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2bd71e73-49bb-419d-a95c-b758810a4ec5/15-adding-search-website-sitesearch360.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2bd71e73-49bb-419d-a95c-b758810a4ec5/15-adding-search-website-sitesearch360.png" width="800" height="" sizes="100vw" caption="Search input above navigation menu (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2bd71e73-49bb-419d-a95c-b758810a4ec5/15-adding-search-website-sitesearch360.png'>Large preview</a>)" alt="Search input above navigation menu" >}}

I also noticed that the layout didn’t look right on mobile because the search input was being aligned to the center, while the logo and navigation menu were aligned to the left.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d64a4c2e-396d-4730-8756-68f5aa0f22a0/16-adding-search-website-sitesearch360.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d64a4c2e-396d-4730-8756-68f5aa0f22a0/16-adding-search-website-sitesearch360.png" width="800" height="" sizes="100vw" caption="Default alignment (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d64a4c2e-396d-4730-8756-68f5aa0f22a0/16-adding-search-website-sitesearch360.png'>Large preview</a>)" alt="Default alignment" >}}

The Search Designer accepts custom CSS, so I could provide a snippet of additional CSS code to override the default style of the search input, aligning it to the left.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/72e42d48-3309-42f2-97e9-aca768192c9b/17-adding-search-website-sitesearch360.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/72e42d48-3309-42f2-97e9-aca768192c9b/17-adding-search-website-sitesearch360.png" width="800" height="" sizes="100vw" caption="Additional CSS (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/72e42d48-3309-42f2-97e9-aca768192c9b/17-adding-search-website-sitesearch360.png'>Large preview</a>)" alt="Additional CSS" >}}

I clicked on “Publish”, refreshed the browser, and now the style in mobile looks right.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b09d42d9-3fa7-4ec7-96c4-ebf786f52140/18-adding-search-website-sitesearch360.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b09d42d9-3fa7-4ec7-96c4-ebf786f52140/18-adding-search-website-sitesearch360.png" width="800" height="" sizes="100vw" caption="Overriden alignment (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b09d42d9-3fa7-4ec7-96c4-ebf786f52140/18-adding-search-website-sitesearch360.png'>Large preview</a>)" alt="Overriden alignment" >}}

Finally, I also decided to enable the “Result Groups” feature, which splits the results into different categories of our own choosing. (What pages are contained in a group is defined via a URL pattern; for instance, I’ve set group “Blog” to contain URLs of type `/blog/...`.) In my case, I want to display results from groups “Blog,” “Guides,” and “Meta” and hide results from “Tags.”

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ffca9ebd-85cb-4a6c-8765-fdd9190466ac/19-adding-search-website-sitesearch360.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ffca9ebd-85cb-4a6c-8765-fdd9190466ac/19-adding-search-website-sitesearch360.png" width="800" height="" sizes="100vw" caption="Result groups (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ffca9ebd-85cb-4a6c-8765-fdd9190466ac/19-adding-search-website-sitesearch360.png'>Large preview</a>)" alt="Result groups" >}}

Now, when the visitor inputs a search query, the results in the dropdown are organized by the chosen groups, which makes it much easier to find the desired information. For instance, when searching for “namespacing”, “Meta” will contain a page describing the feature; “Guides” will contain pages explaining how to use and configure this feature; and “Blog” will display those blog posts announcing the feature.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e604c568-7852-4ea6-9d89-5f76e460184c/20-adding-search-website-sitesearch360.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e604c568-7852-4ea6-9d89-5f76e460184c/20-adding-search-website-sitesearch360.png" width="800" height="" sizes="100vw" caption="Dropdown with results organized into groups (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e604c568-7852-4ea6-9d89-5f76e460184c/20-adding-search-website-sitesearch360.png'>Large preview</a>)" alt="Dropdown with results organized into groups" >}}

Likewise, when clicking on “Show all results”, the modal window is organized into tabs (at one tab per group), which makes it easy to scroll down and browse the results within each group.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c8556cfb-5f45-43e9-a904-2f66f874987a/21-adding-search-website-sitesearch360.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c8556cfb-5f45-43e9-a904-2f66f874987a/21-adding-search-website-sitesearch360.png" width="800" height="" sizes="100vw" caption="Search with tabs (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c8556cfb-5f45-43e9-a904-2f66f874987a/21-adding-search-website-sitesearch360.png'>Large preview</a>)" alt="Search with tabs" >}}

I’m super happy with these results! It took just 15 min to go from 0 to 100, the user interface looks really good, and the search is super fast. Overall, the experience for my visitors is compelling. Head over to [my site](https://graphql-api.com/) and play with the search input to understand why I’m so satisfied with it.
 
## Refining Search

What I showed above is barely scratching the surface, as **it’s what’s included in the free plan!** Check out the [pricing page](https://www.sitesearch360.com/pricing/) to see all the other features available in the service for each of the different tiers.
 
For instance, if you have a content-rich site, such as a blog or an online store, and would like to filter your search results (by category, date, price, and so on), you can do so:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/49e7487b-12a0-44ea-bfcf-db32dcc555fe/22-adding-search-website-sitesearch360.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/49e7487b-12a0-44ea-bfcf-db32dcc555fe/22-adding-search-website-sitesearch360.png" width="800" height="" sizes="100vw" caption="Filters (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/49e7487b-12a0-44ea-bfcf-db32dcc555fe/22-adding-search-website-sitesearch360.png'>Large preview</a>)" alt="Filters" >}}

And then, Site Search 360 has a superpower that makes it stand out from its competitors: its AI-powered [semantic product search engine](https://www.sitesearch360.com/ecommerce/) continuously optimizes search result rankings, promoting the most popular results to the top. If you have eCommerce search enabled, just indicate what’s important for you to sell in your online store, and the engine will automatically re-arrange the results based on multiple ranking factors.

## Wrapping Up

I was personally quite impressed by [Site Search 360](https://www.sitesearch360.com/)’s powerful search offer. In only 15 minutes, my site had a search functionality which I had been postponing for such a long time. Problem solved!
 
If you too want to effortlessly add search to your site, then go [check it out](https://app.sitesearch360.com/signup).

{{< signature "il" >}}
