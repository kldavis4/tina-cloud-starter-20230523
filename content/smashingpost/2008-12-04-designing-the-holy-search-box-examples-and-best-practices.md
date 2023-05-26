---
title: 'Designing The Holy Search Box: Examples And Best Practices'
slug: designing-the-holy-search-box-examples-and-best-practices
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/15d3c34e-9c0b-4f0a-a5c0-ee1059d7e256/search-icon.jpg
date: 2008-12-04T23:29:32.000Z
author: feketeg
description: >-
  On content-heavy websites, the **search box** is often the most frequently
  used design element. From a usability point of view, irritated users use the
  search function as a last option when looking for specific information on a
  website. If a website's content is not organized properly, an efficient search
  engine is not only helpful but crucial, even for basic website navigation. In
  fact, search is the user's lifeline to mastering complex websites. The best
  designs offer a simple search box on the home page and play down advanced
  search and scoping.
categories:
  - Inspiration
  - Showcases
  - Search
  - Web Design
  - User Interaction
---
<em>O</em>n content-heavy websites, the <strong>search box</strong> is often the most frequently used design element. From a usability point of view, irritated users use the search function as a last option when looking for specific information on a website. If a website's content is not organized properly, an efficient search engine is not only helpful but crucial, even for basic website navigation. In fact, search is the <a href="https://www.useit.com/alertbox/20010513.html">user's lifeline to mastering complex websites</a>. The best designs offer a simple search box on the home page and play down advanced search and scoping. 

In practice, <strong>websites tend to grow over time</strong>, adding new content and, more importantly for us, adding new navigation options, such as additional content sections. However, these new content islands do not necessarily fit the whole information architecture that was well-designed and thoroughly structured when the website was initially designed. The consequence is a poor navigation scheme that is more irritating than helpful, because the content appears to be scattered all over the place instead of contained in separate, very distinct folders (in fact, this is a problem we encountered here at Smashing Magazine a couple of weeks ago).

You may want to take a look at the following related posts:

*   [Principles Of Effective Search In E-Commerce Design](https://www.smashingmagazine.com/2009/12/principles-of-effective-e-commerce-search/)
*   [10 Useful Usability Findings and Guidelines](https://www.smashingmagazine.com/2009/09/10-useful-usability-findings-and-guidelines/)
*   [10 Useful Techniques To Improve Your User Interface Designs](https://www.smashingmagazine.com/2008/12/10-useful-techniques-to-improve-your-user-interface-designs/)

When content organization appears to be a mess and it seems nearly impossible to find information, users are very unlikely to decide to browse the available sections of the website. They are more likely to either leave the website (hitting the "Back" button and returning to Google's search results), or turn to the only escape hatch they (hopefully) have: the holy search box.

{{% feature-panel %}}

Although the back-end process of searching a website is very important, we shouldn't neglect the front end, the design, either. Below you will find a <strong>few, but important, guidelines to keep in mind when creating search box designs</strong>. All of the examples shown below are linked to the pages from where they were taken.</p>

## When to Use Search?

<strong>Not every website needs internal search functionality</strong>; however, you often have to meet users' needs for quick access to information, particularly when the website is growing. If the website's navigation is simple and intuitive and there are very few articles "lying around" and not really fitting your navigation scheme, search, and hence a search box, won't be necessary.

An efficient search engine puts users in control of their search for information. When users encounter a relatively complex navigation system, they will immediately look for a search box to get to their final destination quickly and painlessly. Essentially, it's a defence reflex: search lets users assert independence from the website, which can (unintentionally) irritate users and dictate how they should use the Web.

Consequently, <strong>if your website is pretty large</strong> and likely to grow in the future, it is a good idea to consider adding search functionality up front. Your users will be grateful to you for that.</p>

## Search Box = Input Field + Submit Button

And this is where the design of the search box becomes important. The box <strong>must be clearly visible, quickly recognizable and easy to use</strong>. One may think that the search box doesn't need a design; after all, it's just two simple elements: an input field and submit button. How much harm could a poor design do? Well, there are a number of things that can go wrong; for instance, the text displayed in the input field may be hard to read, or the input field may be too short or too long (you'll find more examples below). Some designers even prefer a minimalist solution and don't provide a submit button at all: the "Return" key has to be used instead. Well, in our humble opinion, that's not the most usable solution out there.

![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/14f95f43-19b7-4792-81f8-6db3b7c25d70/techcrunch.gif)

[![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e8a52885-495d-46ac-920e-c73850a0a5d5/techcrunch2.jpg)](https://www.techcrunch.com/)

Indeed, the design of the search box is a big deal. Ideally, the search box would fit the website's overall design perfectly yet manage to stand out slightly when users need it. Adding advanced search options may have benefits if users are looking for very specific information, but <strong>simple search usually works best</strong> and should be presented as an input field with a submit button. Remember, the submit button is a <em>button</em>, which means it should be designed like one. In particular, the submit button should look different than the input field. We are not sure if styling the submit button using the <em>border</em> properties in CSS is a good idea because that would make the button look like any other design element. Instead, giving the button a "button look" (i.e. another color, a different shape, a search icon, etc.) will always work.

<a href="https://www.techcrunch.com/">TechCrunch</a> (example above) uses the same color for the input field and submit button. The color scheme perfectly matches the website's overall color scheme. However, it leads to a problem: at first glance, it's really hard to see where the search box is. Users have to search for it because it doesn't stand out and is not easy to spot. Although the placement of the search box is fine, it is easy to overlook, which is not a good thing.

<strong>A search box should be a box</strong>. Reason? Your visitors don't read the page; they scan it. The most common design for the search function is a box, with the input field being a relatively wide box. Users tend to scan for this pattern on a Web page, so as good practice, try to avoid any other kind of design, such as linked text or a button without a text field.

![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0da404cd-c445-490d-ae16-1e12ced0b8b4/donttrustthisguy.com)

<strong>A search box should be simple</strong>. According to usability studies, it is more user-friendly to have no advanced search options displayed by default. Advanced search, as the name suggests, is advanced, and users get confused trying to use it. One study shows that most users don't know how to use advanced search or Boolean search query syntax.

Bottom line: if you design a search box, make sure it looks like one and is as simple to use as possible.

## Frequent Mistakes in Search Box Designs

In our research, we identified a couple of problems with many search box designs. One wouldn't expect these problems to occur often, but apparently, designers can be quite creative:

*   Placing the search box at the bottom of the page, or hiding it in the navigation menu.
*   Making the input field too short; users are forced to use short, imprecise queries, because longer queries would be hard and inconvenient to read.
*   Making the submit button too small, so that users have to point the mouse very precisely.
*   Making the search box hard to find. ![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/94c3afad-2a24-45a7-a879-306c6cd2f77d/mistake.jpg)_Where is the search box here? On Bridge55.com, looking for it is like a "Where's Waldo" search. In our opinion, the choice of colors here doesn't really help users. Even when the box is found, it's hard to understand where the search query should be typed. There should be a better way to do this._![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/becd4835-a4bd-4b24-8d66-3bff30e996e5/waldo.jpg)
*   Putting the search box together with other forms, such as a newsletter box, which is irritating.
*   Over-designing the search box, making it really hard to spot.
*   Overloading the user with advanced search functionality, making it hard to perform a simple search.
*   Naming the submit button something very unintuitive.
*   Making non-search design elements look like a search box.
*   Providing multiple submit buttons.

![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e26f14fa-1860-47c3-bd7d-7c593e837ea8/wikipedia.org)

The search box design on <a href="https://en.wikipedia.org/wiki/Main_Page">Wikipedia</a> is not really intuitive. Should users click "Go" or "Search"? Hints appear when the mouse hovers over the buttons: "Go" takes users to the page with the title that exactly matches their search query, if one exists, and "Search" is traditional full-text search. Maybe two radio-input elements and a submit button would be a more user-friendly design solution?

## Search Box Design Considerations

Let's take a look at some frequently recurring problems and questions designers are likely to face when designing a search box.

<strong>Where to place the search box?</strong>
There are many possibilities, but only a couple of right ones. The most convenient spot for users would be the top left or top right of every page on your website, where users could easily find it using the common <a href="https://www.useit.com/alertbox/reading_pattern.html">F-shaped scanning pattern</a>. However, some blogs tend to place the search box in the bottom of the (left or right) sidebar. That's probably not a good idea but is likely done because of advertising considerations.

<strong>What to name the submit button?</strong>
It is good practice to give the search button a meaningful name, such as "Search" or "Find," instead of "Go." Make the search button stand out from the whole search box design, showing users where to click.

![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ff810a21-89e8-4d81-9784-9aeab61de502/housingworks.org)

The search button in the image below is very confusing for users. They wouldn't be able to figure out if it is a search box or something else, although the description in the text field suggests it is.

![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/eeb920fd-2e41-4244-810d-eb0290e65b4e/carhartt-streetwear.com)

<strong>Where to place the title of the search box?</strong>
Users need to know that that boxy-looking thing is a search box. And the easiest way to do that is to <em>tell</em> your users that it is; for example, by giving it a section title. According to eye-tracking tests published by <a href="https://uxmatters.com/MT/archives/000068.php">UXMatters</a>, the optimal position for section titles is the upper-left area above the search box. That seems like a plausible design decision to us.

<strong>How to make it clear what users can search for?</strong>
It is a good idea to include a sample search query in the input field to suggest to users what the function can be used for. But make sure this text is deleted when the user focuses the mouse on the input field; this can be achieved with the help of a little JavaScript code.

![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/aa97fe53-fc59-4e67-a99a-3473fc4a3f23/nyc.everyblock)

Many websites implement Google's <a href="https://www.google.com/sitesearch/">SiteSearch API</a>, which gets its search results from Google's index. If you use this feature, make sure to state as much next to the search box. Users don't like unexpected results, and the search algorithm of Google may be different than your website's, thus breaking the consistency rule.

[![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c85ceef3-367a-428c-ae24-debebc81a40c/cnn.com)](https://www.cnn.com)

## Search Box Showcase

Notice that not only is it important how the search box is designed, but it is much more important that search works properly. As Jakob Nielsen states, <a href="https://www.useit.com/alertbox/20010513.html">the first results page is golden</a>: "Users almost never look beyond the second page of search results. It is thus essential that your search prioritizes results in a useful way and that all the most important hits appear on the first page."

## 1\. Classics

When it comes to search boxes, the simplest design is usually the best. The look of the traditional input field and submit button is easy to understand for both experienced and inexperienced users; therefore, designers often stick to the default and don't mess around with the holy grail.

Here are two classics from <a href="https://www.useit.com/">Jakob Nielsen</a> and <a href="https://www.fontshop.com">Fontshop</a>, designs that haven't changed since the early days of the Web.

![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b208a703-ad2c-4622-b337-7483cd26fbb8/fontshop.com)

## 2\. Making the submit button stand out

We found that many designers choose to clearly highlight the submit button to make the search box stand out. Very often, input fields are designed with a background color that fits the surrounding design elements. Consequently, to make the box more visible, visual pointers are needed. In these situations, the submit button is often given a more vivid color or unusual shape.

![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3f572cd9-21cc-4df8-80c4-45a17fd7cff3/moodboard.com)

![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ff810a21-89e8-4d81-9784-9aeab61de502/housingworks.org)

![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6def6142-0621-4a51-bedf-6a55bb45c563/corkd.com)

![Search box](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5ef594ab-9f34-4be2-a7dd-0dead1da5462/act.jpg)

![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0f957f74-1ff3-4153-8a1b-e7b66d9fba96/subdued.net)

![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cb4f42e1-e6bf-4d8b-a880-bc6aeb849a46/tnvacation.com)

![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a25b8756-f0b8-467d-aee7-34916c9a4966/vouchercodes.co)

![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/761623dd-8b70-4a7c-a871-ab101060f8db/webdesignerwall.com)

![Search box](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bfaf2731-c494-48cc-93b4-44f0fb7fb08b/sb2.gif)

![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/929a0641-31f3-4fc6-a946-0bcc32c9b455/concentric-studio.com_news)

![Search box](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f4c2be44-6ab2-4ed2-b41a-68a588fcf5cb/hero.jpg)

Beyond Current Horizons uses a clever idea to make the search box stand out. The website's whole layout is mostly white; only the upper-right part is quite colorful. The search box is placed at the bottom of this area.

![Search box](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8f0c380f-ab92-4dc2-8366-e39ac739d0bf/bch.gif)

## 3\. Using a magnifying glass

Over the last decade, the magnifying glass has become a conventional icon for search and is still used very often when designers want to communicate the function of the search element. The magnifying glass can be found to the left or right, in the input field or near the submit button, near the search box or far from it. We couldn't identify a particular trend, so in most cases designers are left to find the location that works best for them.

![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c917ef0b-cc34-4ac5-87a6-9d071666b605/groove.jpg)

![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f7431b19-6157-4540-8258-7cc3524d28f7/cssbeauty.com)

![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3e15d83a-dfb7-418d-a634-8e7a81647fcc/eeleen.com)

![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6ae93898-4735-4ab2-a307-3a6500f689e7/last.fm)

![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b574976d-23c9-46d7-8908-139adc8daef5/miaandmaggie.com)

![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3e63acc8-16be-436c-b429-899927ca1bfa/fortysevenmedia.com)

![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7a01778d-f600-42ab-95bd-ce579243e684/wishlistr.com)

![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b1cc0a1e-a2f9-4e21-bb86-412c9e1b92e9/thejazzmann.com)

![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b6c76535-2107-4384-9eee-8a0cfb837be9/yourchurch.com)

![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0bee776a-dbe8-4649-972d-b1ba47de005f/mybanktracker.com)

![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/57561b55-a8b8-4954-9add-df09ffa07462/nyokiglitter.com)

![Search box](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2730c5c0-1549-4d36-ba27-40c2cf8be1f9/sts.jpg)

Decodeunicode.org has a very creative -- and strange -- design. Clicking on the magnifying glass with the letter "A" above it opens a modal pop-up window with advanced search options. Don't try this at home or at work.</p>

## 4\. Using illustrations

![Search box](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7eb318e6-7dbe-4bc2-80c6-176fb9f2ae63/tnv.jpg)

![Search box](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8a37b4c5-bd91-4313-aee2-461304c239c4/hand.jpg)

![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4192bff0-2989-4be9-8318-c5180da3aa85/designdisease.com)

![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/57c1e2ff-d2df-4ac5-83ba-06cd4250f699/blog.torondel)

![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b7bb75ed-84ac-4ddf-8cdb-d08fdddd6345/carbonica.org)

## 5\. Rounding the search box

For some reason, designers still use rounded corners for input fields and submit buttons. Both elements are usually designed very carefully, with attention to small details that result in attractive and appealing search boxes. We don't know if this approach is more effective, but it definitely looks more user-friendly (compared to the default design of search boxes).

![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/97ee6456-ac46-499b-9c18-9689cf4e2f6d/baneydesign.com)

![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/778dfbe6-9336-4e9e-9cd5-2f54b30064f7/teddyhwang.com)

![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2bc5a068-0d3a-4f08-9e6c-bb942388ec5f/alltop.com)

![Search box](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ce279d60-28ba-4a0a-a273-a19e6f318af7/twn.jpg)

![Search box](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/39c337d5-6cee-4bc4-a6df-ae881e8e1d21/sea.jpg)

## 6\. Using arrows

Sometimes the submit button is labeled not with text but with a symbol or character; for example, an arrow. Arrows are usually pointed to the right; in some cases they are pointed down (which is strange and quite unusual).

The submit button in the form of an arrow:

[![Search box](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6884f3a7-87d3-4f73-80c3-899aaf3d9a7e/sb.gif)](https://www.baekdal.com)

The down-pointing arrow is used very rarely: Here is the magnifying-glass image is carefully integrated in the input field. This is a nice solution that doesn't irritate the user, because the designer has taken care to pad the space between the image and inputted text.

![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ec3d0eff-a66a-4055-a01b-10df4f47362a/tastebook.com)

## 7\. Using handcraft

Handcraft strikes back in this search box design:

![Search box](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9b2325c6-0fc6-404d-8c15-3ddeb0d3e3e9/elmore.jpg)

And in this one:

![Search box](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f74d9f05-6753-4cd2-87bd-2ecb5ee50348/lovely.gif)

This search box looks nice but is hard to recognize.

![Search box](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c0493772-8509-48e4-a635-1a8652dd46a1/busc.jpg)

A tiny, harmless, humble hand-written search box.

![Search box](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fe916bf5-bdcb-428f-90d3-16976a6a4fa7/bus.jpg)

The "Return" key is used here for a submit button:

![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b3a2e361-8396-4408-84b9-07ed19f5073d/sb.jpg)

![Search box](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/761623dd-8b70-4a7c-a871-ab101060f8db/webdesignerwall.com)

## 8\. Boxy designs

Because they're called search <em>boxes</em>, many design them accordingly. Unfortunately, such designs are often quite boring and not really nice to look at.

![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/36009878-89d6-44df-a109-4eff190cc61e/cssaddict.com)

![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d3cb156d-f811-4e9f-b828-0b75109fd2a0/fall.tnvacation)

![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a287854b-752b-4704-95eb-d30ce8271c5e/konigi.com)

![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/789730e1-becb-4f2f-9fbe-8d6505853493/orangecoat.com)

![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/79a5439d-627d-4c22-8f20-77564861f8b3/good.is)

![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dae85d62-c15d-4b05-8ca3-cc584a007f9c/grainedit.com)

![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dae85d62-c15d-4b05-8ca3-cc584a007f9c/grainedit.com)

![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/921714a7-5d86-4cd4-91d9-32129d95b896/issuu.com)

## 9\. Experimental solutions

Web designers are creative folk. Hence, it's no wonder we have found dozens of really unusual, strange, creative and absolutely inappropriate designs. It's up to you to build new ideas upon the ideas of the designers presented above. But please keep in mind: usability should have the highest priority. The form follows the function, not the other way around.

![Search box](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ab1daaa7-c2cf-4378-aaa8-ea336e5241ad/ret.jpg)

![Search box](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/71873c0a-0985-4970-99f3-d6c34d38a956/jd.gif)

On Uxmag.com, the search box opens after clicking on the "Search" link.

![Search box](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ff14034f-502b-419d-b061-bcf30c922c19/uxmag.gif)

{{< signature "al" >}}

