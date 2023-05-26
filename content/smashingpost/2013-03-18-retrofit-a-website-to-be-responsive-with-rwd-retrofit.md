---
title: Responsively Retrofitting An Existing Site With RWD Retrofit
slug: retrofit-a-website-to-be-responsive-with-rwd-retrofit
date: 2013-03-18T12:01:04.000Z
author: matt-stow
description: >-
  Since the introduction of the iPhone in 2007, touchscreen mobile devices have
  exploded in popularity. They have introduced new problems, new solutions, new
  interactions, new ways of thinking and, of course, new costs to our clients.
categories:
  - Mobile
  - Techniques
  - Optimization
  - Responsive Design
---
The most important question on everyone’s mind — clients and developers alike — is, “How can we provide a great Web experience to our users on mobile?”

## It All Started With iPhone

The mobile Web was rarely considered before the iPhone (mostly because mobile browsers were so bad). But after the phone’s release, clients jumped on the bandwagon and were clamouring for “mobile-friendly” websites so that they didn’t appear to be behind the times. However, mobile-specific — or, worse, iPhone-only — websites also introduced <strong>new issues and frustrations</strong> for users, often “breaking” the Web with broken links, infinite redirects and missing content.

{{% feature-panel %}}

Fast forward three years, when we find Ethan Marcotte writing about his revolutionary principle of “<a href="https://www.smashingmagazine.com/2011/01/guidelines-for-responsive-web-design/">responsive web design</a>” (RWD), which changed the Web — and the way Web developers think — forever.

We’ve told our clients about all of the benefits of RWD and about why they shouldn’t build a separate mobile website. The world should have lived happily ever after. But clients who had already spent thousands of dollars on a fixed-width desktop website were less than pleased.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e375e5bc-e3c4-4bdb-ab0e-16acb4cc32de/create-first-iphone-app-500.jpg"><img loading="lazy" decoding="async" class="135119" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e375e5bc-e3c4-4bdb-ab0e-16acb4cc32de/create-first-iphone-app-500.jpg" alt="create-first-iphone-app-500" width="500" height="316" /></a><br>
<em>Can your clients afford a mobile-first responsive build? (<a href="https://www.smashingmagazine.com/2009/08/11/how-to-create-your-first-iphone-application/">Image Source</a>)</em>

Then, around the time that Marcotte’s article was published, the iPad was released. Clients who had already gone down the path of a separate mobile website then wanted their iPad users to get their current desktop website. So, we did it — with user-agent sniffing, once again <strong>straying further from the RWD methodology</strong>, even though we knew we shouldn’t.

Our fear of not being future-friendly was further exposed when Android tablets hit the market. Because there is no single unique identifier in their user agents to identify them as tablets, all Android devices, regardless of size, are generally served mobile websites, which, from the forums I frequent, frustrates most users. There are some services for detecting Android tablets, as outlined in “<a href="https://www.smashingmagazine.com/2012/09/24/server-side-device-detection-history-benefits-how-to/">Server-Side Device Detection: History, Benefits and How-To</a>,” however, as an Android user, I regularly see more mobile than desktop websites.

In fact, the issue got so bad that in Android 4.0 (Ice Cream Sandwich), <strong>Google added a “Request desktop site” option</strong> to its browser. But depending on how a website’s detection is written, it doesn’t always work, and you still have to suffer the pain of loading the mobile website first.

So, we have a few issues:

1.  Clients with an existing “desktop” website can’t afford to rebuild from scratch using a responsive methodology.
2.  They still need a more optimized experience for mobile devices.
3.  Rightly or wrongly, they still want tablets to load their desktop website.</p>

Recommended reading: [Responsively Retrofitting An Existing Site With RWD Retrofit](https://www.smashingmagazine.com/2013/03/18/retrofit-a-website-to-be-responsive-with-rwd-retrofit/)

## What’s The Solution?

<a href="https://github.com/izilla/RWD-Retrofit">RWD Retrofit</a> is a small, vanilla JavaScript “plugin” that gives developers the option to allow an existing “desktop” website to coexist with a new responsive version, with minimal modification to the original website.

It implements <strong>dynamic viewport switching</strong> to ensure that the correct version of the website is shown according to the viewport’s width (both on loading and on resizing or orientation change), and it provides an object that contains the media queries required for responding to the breakpoints with JavaScript.

I wrote it at <a href="https://izilla.com.au">Izilla</a>, which helps clients to address the issues mentioned above, and I have already used it in a number of projects.

Although I’m obviously biased, I think it’s a great technique to help you quickly and efficiently improve a client’s mobile presence in a cost-effective way.

Keep in mind that RWD Retrofit isn’t a magic bullet that will instantly transform your website into a responsive website out of the box. You still need to build the responsive version.</p>

## Is It The Only Solution?

Absolutely not. Developers have <strong>three other options</strong> available to them: a dedicated mobile website, a desktop-down responsive reskinning, and a complete rebuild with mobile-first responsiveness.

Let’s look quickly at the pros and cons of each, and of RWD Retrofit.</p>

### A Dedicated Mobile Website

<strong>Pros:</strong>

*   Because it’s completely separate from the existing website, you essentially have a blank canvas to work on — dealing with a legacy code base is not really an issue.
*   Supporting fewer devices results in a more focused, streamlined implementation, because the “minimum requirements” of the website are easier to define and develop for.
*   By analyzing your users’ habits and data, you’re better able to target the user’s intent and context.
*   The cost to develop is reasonable.

<strong>Cons:</strong>

*   A separate code base could result in more expensive maintenance and content costs.
*   Supporting a subset of devices is not future-friendly.
*   User-agent detection is fragile because it can, and will, be spoofed.
*   Be wary of assumptions of user intent based on device alone. A lot of “mobile” usage is done at home.
*   There is the possibility of broken links and missing content for existing desktop pages that don’t exist on the mobile website.

Dedicated mobile websites are suitable for when content parity is not an issue, or you’re absolutely certain of the user’s goals on mobile, or the client wants a more app-like experience. I have used them successfully for targeted micro-sites that are separate from the main website.</p>

### A Desktop-Down Responsive Reskinning

<strong>Pros:</strong>

*   Uses your existing code base, making for more efficient maintenance and content updates.
*   Supports a wide variety of devices based on screen size.

<strong>Cons:</strong>

*   It might not suit your existing code base. Success relies largely on using CSS3 to style, so adapting old websites that primarily use fixed-width CSS background images for presentation might be difficult.
*   Performance overhead and inefficiencies are incurred from existing redundant code on breakpoints that don’t match.
*   Requires extensive retesting of a previously functional desktop website.
*   Cost to develop is moderate to high, depending on the code base.

This approach is better suited to simple websites that already use modern Web standards as their underlying technology. Marcotte used this approach in his <a href="https://www.smashingmagazine.com/2011/01/guidelines-for-responsive-web-design/"><em>Responsive Web Design</em></a> book, but that was before “mobile first” became the favored approach.</p>

### A Mobile-First, Responsive Rebuild

<strong>Pros:</strong>

*   A completely fresh, considered, optimized and progressively enhanced code base.
*   A consistent, seamless experience for all users.
*   Supports the widest variety of devices based on screen size and features, including large desktops and TVs.
*   You’re future-friendly!
*   Your work will hopefully be shared and admired in social media.

<strong>Cons:</strong>

*   Planning, prototyping, development and testing could require substantial effort.
*   The cost to develop is very high.

This will hopefully become the de facto standard for all new projects and redesigns. If approached correctly, your website should support as many different kinds of devices as possible for the foreseeable future, including <a href="https://www.stuffandnonsense.co.uk/blog/about/device_viewport_widths_reference_on_google_docs">Android-powered, Internet-enabled refrige-toasters</a>.</p>

### RWD Retrofit

<strong>Pros:</strong>

*   Uses your existing code base, making for more efficient maintenance and content updates.
*   A completely separate style sheet ensures that the retrofit will not interfere with existing desktop styles.
*   Minimal overhead or changes to existing website.
*   Supports a wide variety of devices based on screen size.
*   The cost to develop is reasonable.

<strong>Cons:</strong>

*   The existing markup might not be flexible or optimized enough to be repurposed for small screens.
*   Depending on how far the retrofit is taken, the transition from the largest responsive breakpoint to the desktop breakpoint could potentially be disjointed for users, but that would only really affect users who resize their browser’s window.
*   On mobile devices, the desktop version might not initially be zoomed out fully on load or on rotation.

A retrofit is a good compromise of ideas and techniques, taking the best bits from the various other solutions to provide a cost-effective solution to your existing clients.</p>

## Which Is The Best Solution?

The “best” depends on the context and budget. Obviously, the best solution you could give to your clients would be a complete mobile-first responsive build. That would provide the optimal experience for users, using a single code base that’s cost-effective to maintain. I absolutely urge you to recommend this approach if feasible.

However, many of my clients can’t afford to do this, and because their websites predate the use of CSS3 for things such as rounded corners and gradients, the “best” solution for them is to use RWD Retrofit.

RWD Retrofit is also useful for both clients and developers who are in a transitional phase to responsiveness. If your client wants to rebuild using the mobile-first philosophy but can’t afford to just yet, push to retrofit their website. Generally speaking, <strong>having some kind of mobile optimization is better than nothing</strong>. Also, remember that practice makes perfect. Attempting a small-scale responsive website first will equip you with the skills needed for when you come to do the “real” thing.</p>

Recommended reading: [Responsively Retrofitting An Existing Site With RWD Retrofit](https://www.smashingmagazine.com/2013/03/18/retrofit-a-website-to-be-responsive-with-rwd-retrofit/)

## How Does RWD Retrofit Work?

Here goes:

1.  When the page starts to load, the script checks to see whether the user is on a mobile device that supports touch events.
2.  If they are, it checks whether you’ve set to override the desktop breakpoint on mobile, and then changes the breakpoint accordingly.
3.  It then checks to see whether you’ve set the viewport width for the desktop version to be anything other than the default of 980 pixels, and sets that accordingly. The article “[Viewport Meta Tag For Non-Responsive Design](https://webdesignerwall.com/tutorials/viewport-meta-tag-for-non-responsive-design)” explains why you may want to do this.
4.  A function is called that compares the width of the document to the desktop media query, and if it’s equal or larger, it alters the viewport to the desktop one.
5.  This same function is called on a resize or orientation change (depending on what the device supports) to see whether it needs to switch over to the mobile viewport, and vice versa.
6.  Finally, it returns the responsive and desktop media queries in a JavaScript object for you to test against in other scripts, so that:
    1.  you don’t have to write your media queries in both the markup and JavaScript;
    2.  if you did override the desktop breakpoint on mobile devices, you’ll always have the correct media query.

At its core, RWD Retrofit should be thought of as <strong>a technique, not a solution</strong>. If you don’t plan to change the breakpoint that the desktop website is served at on mobile, or you don’t plan to change the desktop viewport’s width when it is served, or you don’t mind duplicating media queries in your JavaScript, then the RWD Retrofit JavaScript itself isn’t required. The technique will still work, allowing you to achieve similar results.</p>

## Implementing RWD Retrofit

Below is the process I use to retrofit a website.</p>

### Initial Set-Up

1.  Open the index (i.e. main) page, which has your global `<head>` section.
2.  Add

        <meta name="viewport" content="width=device-width, initial-scale=1" />

    as one of the first children of `<head>`.
3.  Find the link to the current desktop style sheet, and change its media attribute to `media="all and (min-width: **X**px)"`, where `**X**` is the current width of the desktop website, which will result in something like this:

        <link href="/css/desktop.css" rel="stylesheet" media="all and (min-width: 980px)" />

    If you currently have multiple style sheets at runtime, I strongly recommend that you combine and minify them into one to improve performance.
4.  Go through your JavaScript functions and, for the time being, comment out any that won’t apply to the responsive version of the website. (Again, if you currently have multiple JavaScript files at runtime, I strongly recommend that you combine and minify them into one to improve performance — excluding any jQuery, which is best served from a CDN.)
5.  Create a new responsive style sheet, and link to it with a `max-width` media query that is 1 pixel less than the desktop one, like so:

        <link href="/css/rwd.css" rel="stylesheet" media="all and (max-width: 979px)" />

    If you now open this in a Web browser with a narrow window, you’ll have an unstyled document — the clean slate that we want.</p>

### Creating the Responsive Version

Building a responsive style sheet is a massive topic on its own, and because a lot of good resources are already online, I’ll just provide some pointers.

1.  Begin with a mobile-first philosophy. Resize your browser window to a “mobile” size. I actually prefer to go smaller than the standard 320 pixels because feature phones are often forgotten. To help with this, Firefox introduced a pretty cool [Responsive Design View](https://youtube.com/watch?v=t07cLJhJkjQ) mode in version 15\. Or you can use the [Web Developer Toolbar](https://chrispederick.com/work/web-developer/) extension, available for both Firefox and Chrome.
2.  Although undertaking a truly mobile-first responsive rebuild wouldn’t be a best practice, elements in your markup may be suitable for the original desktop website but need to be hidden on smaller screens. Use an accessible method to do this. Chris Coyier [rounds up approaches](https://css-tricks.com/places-its-tempting-to-use-display-none-but-dont/) to doing this.
3.  As you develop and write the CSS, increase your browser’s width to see how the new responsive layout reacts and adapts as you approach the desktop’s breakpoint. If you need to insert more media queries, do it directly in the responsive style sheet to keep them nicely contained. (To help you obtain the viewport’s current width to use as a new breakpoint, I’ve written [Viewport Genie](https://github.com/stowball/Viewport-Genie), which is available as both a [bookmarklet](https://mattstow.com/git/viewport-genie/bookmarklet.html) and a [tiny JavaScript include](https://raw.github.com/stowball/Viewport-Genie/master/viewport.genie.min.js). You can also use Firefox’s Responsive Design View mode.)
4.  When you’re happy with the basic styling on desktop browsers, start testing some real devices. Things will need adjusting, and issues will arise that don’t appear on the desktop. (Both Safari on iOS and Chrome on Android allow you to use remote debugging from your browser to preview your website on the device. Alternatively, you could use Adobe’s [Edge Inspect](https://html.adobe.com/edge/inspect/), which is available for both iOS and Android, or Viljami Salminen’s [Remote Preview](https://viljamis.com/blog/2012/remote-preview/).)

### Implementing RWD Retrofit

Now it’s time to drop in the RWD Retrofit JavaScript and its dependencies.

1.  Download the [minified RWD Retrofit from GitHub](https://github.com/izilla/RWD-Retrofit), and reference it immediately below your style sheets.
2.  Optionally, [download a custom build of Modernizr](https://modernizr.com/download/) and include that underneath RWD Retrofit. At a minimum, I recommend that your build contain Modernizr.load and Add CSS Classes. You may also want to include other feature tests depending on how you plan to style the responsive version. If your markup doesn’t use any of the HTML5 layout elements, then you won’t need html5shiv. (I recommend combining the two JavaScripts above into one `base.min.js` resource.)
3.  Download the [minified version of the matchMedia polyfill from my fork on GitHub](https://github.com/izilla/matchMedia.js), and include it before your other custom JavaScripts, which should hopefully be immediately before the closing `</body>` tag to prevent rendering blocking. (The matchMedia polyfill is required for [older browsers](https://caniuse.com/#feat=matchmedia) that don’t support this API natively.)
4.  Download the [minified version of Enquire.js](https://wickynilliams.github.com/enquire.js/), and reference it beneath the matchMedia polyfill. (Enquire.js is a lightweight pure JavaScript library for responding to CSS media queries.)
5.  Give your desktop style sheet’s `<link>` a class of `"rwdretrofit-desktop"`.
6.  Give your responsive style sheet’s `<link>` a class of `"rwdretrofit-mobile"`.
7.  Add an optional `data-breakpoint-width="X"` attribute to the desktop style sheet’s `<link>`, where `X` is the pixel width of the desktop breakpoint on mobile devices (for example, 768 for iPads and other large tablets).
8.  Add an optional `data-viewport-width="X"` attribute to the desktop style sheet’s `<link>`, where `X` is the pixel width that the desktop viewport will be set to on mobile devices.
9.  Add an optional `data-debug="true"` attribute to the desktop style sheet’s `<link>`, which forces desktop and non-touch-enabled browsers to use RWD Retrofit. (If you’ve specified a custom `data-breakpoint-width`, ensure that you remove the `data-debug` attribute before going live, or else your desktop breakpoint will trigger at the wrong size on desktops.)

If you’ve added the optional <code>data-</code> attributes, you will now be able to <strong>test these breakpoint and viewport changes</strong> on mobile devices, or by setting your browser to emulate touch events. At the time of writing, Chrome is the only browser able to do this through its Developer Tools (in <code>Settings → Overrides</code>).

Because I don’t serve the responsive version to users of IE 8 and below, I also reference the desktop style sheet in a conditional comment beneath the others, like so:

<pre><code class="language-markup">
&lt;!--[if lt IE 9 ]&gt;
   &lt;link href="/css/desktop.css" rel="stylesheet" type="text/css" media="all" /&gt;
&lt;![endif]--&gt;
</code></pre>

If you wanted these users to have a responsive experience, you should be able to use <a href="https://github.com/scottjehl/Respond">Scott Jehl’s Respond.js media query polyfill</a> instead, although I haven’t tested it.</p>

### Modifying Your JavaScript Functions

No doubt, you will have JavaScript functions that should be fired on the desktop version but not on mobile — such as a lightbox script (for example, <a href="https://www.jacklmoore.com/colorbox">Jack Moore’s ColorBox</a>).

Keep in mind that there is no one process to achieve this (because everybody writes their JavaScript functions differently), however, <strong>here’s how I’d modify a lightbox function</strong>:

1.  First, let’s assume that we have one JavaScript file named `main.js`, in which everything is wrapped in a function that executes when the DOM is fully loaded, whereupon we call ColorBox on all links with a class of `lightbox`, like so:

        $(document).ready(function() {
           // Call ColorBox on appropriate links
           $('a.lightbox').colorbox();
        });

2.  Because the lightbox function can now be called multiple times, let’s instead create a variable that stores the lightbox links for counting and improved performance (because jQuery won’t need to query the DOM each time):

        var $lightboxLinks = $('a.lightbox');

3.  We now need to convert the call to ColorBox into a function, so that we can use it whenever the desktop media query is matched. I prefer to create them as methods of a literal object:

        var lightbox = {
           initialize: function() {
              // If the number of links to be ColorBox'd is greater than 0
              if ($lightboxLinks.length > 0) {
                 $lightboxLinks.colorbox();
              }
           },
        };

4.  We also need to remove any ColorBox’d links for when our responsive retrofit media query is matched. So, we create a function to do that after our `initialize` method:

        destroy: function() {
              // Remove all traces of ColorBox
              $.colorbox.remove();
              // Remove the click event handlers that ColorBox added
              $lightboxLinks.off('click');
           }

5.  Now, we need to add in the conditional tests by using the two media-query objects that RWD Retrofit exposes (`rwdRetrofit.desktop` and `rwdRetrofit.mobile`) and Enquire.js:

        // If rwdRetrofit is loaded
        if (rwdRetrofit) {
           // Use enquire.js to test the media queries
           // Test for the desktop media query
           enquire.register(rwdRetrofit.desktop, {
              // If it matches
              match: function() {
                 lightbox.initialize();
              },
              // If it doesn't
              unmatch: function() {
                 lightbox.destroy();
              }
           // Immediately start testing for the media queries
           }).listen();
        }

    (I could have just as easily tested for `rwdRetrofit.mobile` and reversed the `match` and `unmatch` functions, but logically that wouldn't make as much sense.)

And that’s as simple as it can be to modify existing JavaScripts to work “responsively.” You just need to follow a similar pattern, creating <code>initialize()</code> and <code>destroy()</code> functions for other code that should be selectively used or that should behave differently depending on the media query matched.

<strong>But let’s take it further.</strong> Because ColorBox isn’t used in our responsive version, we’re punishing our “mobile” users by making them download the script. So, we can use Modernizr’s asynchronous, conditional resource loader to load it only when the desktop breakpoint is matched.

1.  Modify the `lightbox.initialize()` function to conditionally load the ColorBox script:

        initialize: function() {
           // If the number of links to be ColorBox'd is greater than 0
           if ($lightboxLinks.length > 0) {
              Modernizr.load({
                 // Load the minified ColorBox script
                 load: '/js/jquery.colorbox-min.js',
                 // When it's loaded, apply ColorBox to the links.
                 // This will also be triggered if the script has previously been loaded
                 complete: function() {
                    $lightboxLinks.colorbox();
                 }
              });
           }
        }

2.  Modify the `lightbox.destroy()` function to first check whether ColorBox has loaded:

        destroy: function() {
           if (typeof($.colorbox) != 'undefined') {
              // Remove all traces of ColorBox
              $.colorbox.remove();
              // Remove the click event handlers that ColorBox added
              $lightboxLinks.off('click');
           }
        }

Putting it all together will give you this:

<pre><code class="language-javascript">
$(document).ready(function() {
   var $lightboxLinks = $('a.lightbox');

   var lightbox = {
      initialize: function() {
         // If the number of links to be ColorBox'd is greater than 0
         if ($lightboxLinks.length &gt; 0) {
            Modernizr.load({
               // Load the minified ColorBox script
               load: '/js/jquery.colorbox-min.js',
               // When it's loaded, apply ColorBox to the links
               // This will also be triggered if the script has previously been loaded
               complete: function() {
                  $lightboxLinks.colorbox();
               }
            });
         }
      },
      destroy: function() {
         if (typeof($.colorbox) != 'undefined') {
            // Remove all traces of ColorBox
            $.colorbox.remove();
            // Remove the click event handlers that ColorBox added
            $lightboxLinks.off('click');
         }
      }
   };

   // If rwdRetrofit is loaded
   if (rwdRetrofit) {
      // Use enquire.js to test the media queries
      // Test for the desktop media query
      enquire.register(rwdRetrofit.desktop, {
         // If it matches
         match: function() {
            lightbox.initialize();
         },
         // If it doesn't
         unmatch: function() {
            lightbox.destroy();
         }
      // Immediately start testing for the media queries
      }).listen();
   }
});
</code></pre>

Because modifying the DOM when breakpoints match comes with a performance hit, if an <code>initialize()</code> function creates elements in the DOM that should be removed in the other “version” of the website, you could just hide it in the appropriate style sheet instead, which adds slightly extra bloat to your CSS, but would be more performant and better on the device’s battery, for example.

I’ve created a one-page demo website, and the <a href="https://github.com/izilla/RWD-Retrofit-Demo">code for it is on GitHub</a>, too.

The demo goes further than the example above, by adding extra selective JavaScript functions, such as a toggle navigation on small screens and an accessible carousel and tabs.</p>

## In Conclusion

If you can’t convince your clients to start from scratch with a mobile-first philosophy, I hope this gives you the knowledge, impetus and tools that you need to retrofit their websites!

{{< signature "al" >}}

