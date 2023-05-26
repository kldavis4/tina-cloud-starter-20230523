---
title: Content First — Design Last
slug: design-last
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7f23b00b-ecbb-4dcc-82a0-634c799df5b5/illu-contentlast.jpg
date: 2015-02-20T22:57:21.000Z
author: rik-schennink
description: >-
  How does one design and develop for the responsive web? A lot of methodologies
  out there try to tackle this problem, but all of them rely on the same classic
  website development process. It boils down to the following: design and then
  develop.

  Let’s go nuts and **flip this outdated methodology on its head**. Before we
  start flipping things around, let’s take a quick stroll down memory lane, just
  so we know where we’ve come from and where we are now.
categories:
  - Design
  - Process
  - Responsive Design
---
How does one design and develop for the responsive web? A lot of methodologies out there try to tackle this problem, but all of them rely on the same classic website development process. It boils down to the following: design and then develop. Let’s go nuts and flip this outdated methodology on its head.

Before we start flipping things around, let’s take a quick stroll down memory lane, just so we know where we’ve come from and where we are now.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [How To Convince The Client That Your Design Is Perfect](https://www.smashingmagazine.com/2010/10/how-to-convince-the-client-that-your-design-is-perfect/)
*   [How To Explain To Clients That They Are Wrong](https://www.smashingmagazine.com/2009/12/how-to-explain-to-clients-that-they-are-wrong/)
*   [How To Sell Your UX Design Solution To Clients](https://www.smashingmagazine.com/2013/02/sell-design-solution-clients/)
*   [How To Sell Responsive Web Design To Clients](https://www.smashingmagazine.com/2013/10/selling-responsive-website-design/)

## History

It’s 1989, and Tim Berners-Lee, the man with the plan, conjures up HTML while working at CERN. It’s a language to link content across documents.

{{% feature-panel %}}

After four years, the web went public, in 1993. It took a couple of years for someone to create the first columned layout using a table — at which point, something changed. I imagine this as being a turning point in web development. It was the moment when design could be moved to the front of the development process. You could now design a web page, slice it up and present it on the web.

Luckily, we regained our sanity and ditched tables for layout. We proudly moved to semantic HTML, but we held on to our design-first approach. Let’s take a closer look at semantic HTML.</p>

## Semantic HTML

Semantic HTML is about picking the right HTML element to describe a given piece of information, rather than using HTML to define the way the information should look. If you’re a front-end developer, you’ve probably been doing this for the past couple of years. Great, keep it up!

In my opinion, <strong>writing semantic HTML is one of the key aspects</strong> of being a good front-end developer. It’s something I value greatly.

Because of that, it’s been a topic I’ve discussed a lot with colleagues who have valued it less or simply did not understand. To resolve these debates once and for all, I tried to give them a glimpse of the thought process behind my HTML writing.

I searched for a straightforward website online and derived its HTML structure (without looking at the existing HTML, which would have been cheating). Then, I turned my HTML thought process into a step-by-step visualization. For many of my colleagues, this visualization turned out to be a real eye-opener. These couple of visuals created mutual understanding of what a front-end developer does and why semantic HTML is important. Also, interestingly, it revealed that not all front-end developers view semantic HTML in the same light.

Below is the website I used in the thought process experiment.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6614b88f-641e-4023-855f-d88c50e703a8/01-dunnelon-opt.jpg" alt="01-dunnelon-opt" /></figure>

I’ve laid out the thought process below. On the left side is my view of the website. On the right is the written HTML as rendered in the browser. OK, let’s do this!
<ol>
 	<li>In my opinion, this landing page serves as an umbrella for all subpages. So, I’ll wrap the logo in an <code>h1</code>. I’ll add an <code>img</code> tag as well, so that the logo displays when printed.
<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/db7ac58d-dbcf-4fb6-be4e-37c3f5cc72c6/02-dunnelon-analysis-1-opt.jpg" alt="02-dunnelon-analysis-1-opt" /></figure></li>
 	<li>All right, next up is the menu. I’m putting it at the top because this is a landing page. Also, let’s handle caps with CSS <code>text-transform</code>. I’ll wrap the menu in a <code>nav</code> and add a mandatory header called “Navigation” inside. Also, we’ll add an ordinary unordered list, with anchors as links to the other pages.
<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/499b6d64-8e00-40a6-9cac-123c87445277/03-dunnelon-analysis-2-opt.jpg" alt="03-dunnelon-analysis-2-opt" /></figure></li>
 	<li>Is this image showing a train actually content? And should we, therefore, use an <code>img</code> tag? Or is it aesthetic, meaning we should handle it in CSS using <code>background-image</code>? I’m going with aesthetic, which means it won’t end up in the HTML outline.
<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e432c27a-065c-43ce-8d6e-0c628ef71e9f/04-dunnelon-analysis-3-opt.jpg" alt="04-dunnelon-analysis-3-opt" /></figure></li>
 	<li>What type of content is that white text below the image? What should I name it? How about “Introduction” — I’m not 100% sure, though. I’ll add an “Introduction” heading and hide it with CSS later on. This heading might be useful for screenreaders as well.
<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8f1b9b0f-3fe8-4233-95a3-c3af798ace0d/05-dunnelon-analysis-4-opt.jpg" alt="05-dunnelon-analysis-4-opt" /></figure></li>
 	<li>Wait a minute! That blue “Join us today” button is related to the introductory paragraph (“… if you joined us”). Also, it’s not a button but a link. I’m setting myself up for a CSS positioning nightmare.
<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/89174050-d385-4ef5-8421-8438c889e1f1/06-dunnelon-analysis-5-opt.jpg" alt="06-dunnelon-analysis-5-opt" /></figure></li>
 	<li>At this point, I don’t know what to do with the “Book an event” button. It’s not related to “Join us today,” that’s for sure. It’s a button without context. I’ll just skip it for now.
<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/778a6124-1847-44ad-a701-820273cf7e6a/07-dunnelon-analysis-6-opt.jpg" alt="07-dunnelon-analysis-6-opt" /></figure></li>
 	<li>Finally, some straightforward content: headings, paragraphs and links. To position them, we might need to wrap some of these in a <code>div</code> later on.
<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d15fdc50-b594-42ce-a96f-5527d3c84947/08-dunnelon-analysis-7-opt.jpg" alt="08-dunnelon-analysis-7-opt" /></figure></li>
 	<li>On to the events! Let’s go for an ordered list because shuffling the dates would be confusing. We’ll use the <code>time</code> element for dates and times. Let’s wrap a link around the subheading.
<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8c2706d8-20ca-4a4b-a754-fda9ccd1678d/09-dunnelon-analysis-8-opt.jpg" alt="09-dunnelon-analysis-8-opt" /></figure></li>
 	<li>Now we know where the “Book an event” button should go. People need to know about upcoming events before they can book one — makes sense. So, we’ll put the button with the events making our CSS positioning nightmare even worse.
<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/47641976-a933-4c29-90bc-333059067d1d/10-dunnelon-analysis-9-opt.jpg" alt="10-dunnelon-analysis-9-opt" /></figure></li>
</ol>
Below is the resulting HTML.

<pre><code class="language-markup">&lt;h1&gt;&lt;img src=""/&gt;Greater Dunnellon Historical Society&lt;/h1&gt;
 &lt;nav&gt;     
   &lt;h2&gt;Navigation&lt;/h2&gt; 
   &lt;ul&gt; 
      &lt;li&gt;&lt;a href="/"&gt;Home&lt;/a&gt;&lt;/li&gt;         
      …    
   &lt;/ul&gt;
 &lt;/nav&gt;

 &lt;main&gt;  
   &lt;h2&gt;Introduction&lt;/h2&gt; 
   &lt;p&gt;We’ve come together … if you joined us.&lt;/p&gt; 
   &lt;a href="/"&gt;Join us today&lt;/a&gt;  

   &lt;h2&gt;A commitment to our history&lt;/h2&gt; 
   &lt;p&gt;The Greater Dunnellon … in its heyday.&lt;/p&gt;  

   &lt;h3&gt;Learn about Dunnelon's history&lt;/h3&gt; 
   &lt;p&gt;Dunnellon was platted … South Williams Street.&lt;/p&gt; 
   &lt;a href="/"&gt;More history&lt;/a&gt;  

   &lt;h3&gt;Your next event at the depot&lt;/h3&gt; 
   &lt;p&gt;The depot provides … are also available.&lt;/p&gt; 
   &lt;a href="/"&gt;Make a reservation&lt;/a&gt;  

   &lt;article&gt;  
      &lt;h2&gt;Upcoming events&lt;/h2&gt; 
      &lt;ol&gt; 
         &lt;li&gt; 
            &lt;h3&gt;&lt;a href="/"&gt;Museum open Tuesdays&lt;/a&gt;&lt;/h3&gt; 
            &lt;time&gt;01/21/2015 from 11:00 am&lt;/time&gt; to &lt;time&gt;4:00 pm&lt;/time&gt; 
            &lt;p&gt;Learn, teach and share history with Boomtown Sam!&lt;/p&gt; 
         &lt;/li&gt;             
         …          
      &lt;/ol&gt;  
      &lt;a href="/"&gt;Book an event&lt;/a&gt;     
   &lt;/article&gt;  
&lt;/main&gt;
</code></pre>

<small><i>A lot of attributes have been left out to keep the HTML compact.</i></small>

You probably noticed that I’ve made a lot of assumptions in order to come up with the HTML structure above. The introductory paragraph heading, the banner image and the call-to-action buttons — these were all places where I assumed something and added to or altered information on the page.

I’ve also made assumptions about where to position things on the page. In deriving semantic meaning from textual data, I’ve assumed that the visual designer intended to give information on the right side a lower priority than information on the left. Based of these assumptions, “Upcoming events” ended up below “A commitment to our history.” I put the navigation above “Introduction,” although it might have been better the other way around.

Assumptions are dangerous, not only because one could assume incorrectly, but also because somebody else will most likely assume differently. In this case, if you and I had independently written an HTML tree based on the design above, it would have been a miracle if they turned out the same.</p>

<strong>HTML is about giving meaning to information</strong>. We should not end up with different descriptions of the same information. It seems that design clouds the meaning of the content and creates room for interpretation and assumption.</p>

## Content First

A <a href="https://adactio.com/journal/4523">content-first</a> approach teaches us that visual design should always be based on actual content. Only with real content can we decide how best to present it to users. We’ll get to what “real” means in a minute.

With a content-first approach, we move from designing without content to designing based on content — a very important distinction. Remember the definition of semantic HTML: <strong>giving meaning to content</strong>.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/86203709-161b-4fe0-b19f-b2bc1dcde9d3/11-design-html-content-opt.png" alt="11-design-html-content-opt" /></figure>

Semantic HTML has no relation to appearance — that’s what CSS is for. Why put off the HTML until after the design phase if it doesn’t depend on the appearance? Let’s move it to the front and describe our content before designing it.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4782f431-8e7b-48fe-8729-b256729809da/12-content-design-html-opt.png" alt="12-content-design-html-opt" /></figure>

It’s a <strong>small change, but it makes a big difference</strong>. With this change, all assumption is taken out of the equation. We now know how our content will be structured. And before even drawing a pixel, we’ve got ourselves a website.

Do you hear that? That’s the sound of screenreader users celebrating.

## Flipping It

Let’s go back to the slides. This time, we’ll do it the other way around. We’ll use the HTML that we’ve just written and imagine a designer using it for their visual design.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/112405fd-3e1a-4151-a718-b3f6ed6db6fd/13-dunnelon-after-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d546dfea-f05c-4776-bdd0-aed85963d870/13-dunnelon-after-opt-small.jpg" alt="13-dunnelon-after-opt-small" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/112405fd-3e1a-4151-a718-b3f6ed6db6fd/13-dunnelon-after-opt.jpg">View large version</a>)</figcaption></figure>

It’s difficult to imagine the call-to-action buttons ending up where they were in the original design. In terms of visuals but also content, this new setup makes a lot more sense.

When we were basing the HTML on the initial visual design, we could use the visuals for one viewport only. By turning things around and basing the design on the HTML, we can use the HTML for all possible viewports and contexts.</p>

## Reality Calling

If I’ve piqued your interest, you might be wondering how to implement this approach in an actual project. Depending on the project, your team and your client, it might look something like the following.

Because we’re doing things content-first, we need to get our hands on the client’s content. <a href="https://twitter.com/markboulton">Mark Boulton</a> rightly points out that content-first is not about waiting for the final content before doing anything. When we talk about content-first, we mean that we want to know the structure of the content that we’re designing for. Having the final content already in hand would be fantastic, but most of the time it simply is not. In “<a href="https://www.markboulton.co.uk/journal/structure-first-content-always">Structure First. Content Always</a>,” Boulton says:
<blockquote>You can create good experiences without knowing the content. What you can’t do is create good experiences without knowing your content structure.</blockquote>

In my experience, this is true, and making sure everyone knows what “content first” means is important. So, make sure everyone understands that you’re talking about structure and that you don’t mean to pause the project and wait for the client to deliver the final content.

Before we start writing HTML, we need to determine what content to present on the page and how to prioritize it. This is where a priority guide comes in handy. Together with your client, write down all of the content types of your web pages on sticky notes, and then order them chronologically along the y-axis. For example, you could have a “product detail” sticky and a “post a review” sticky, and because someone would need to know about a product before reviewing it, “product detail” should come first. Your client might deem the “post a review” box to be more important, but that importance could be visualized later using color and composition, not by changing the order of content.

I find that clients are pretty good at this exercise, maybe because they are used to writing documents such as quotes and writing papers that must adhere to a certain hierarchy and chronological order to make sense. As I said, this exercise makes them <strong>really think about what’s important</strong>. Also, if there are multiple stakeholders, it shows how each is motivated and which stakeholders have the most influence.

We’ve set up our content types; let’s talk about content structure. Structuring content is exactly what HTML is good for. Let’s go for it. We’ve got our content types, and we understand semantic HTML, so let’s start adding structure to the various content types. This could be easy or challenging, depending on how high-level your content types are.

A basic “post a review” form could be pretty straightforward:

<pre><code class="language-markup">
&lt;form&gt;  
   &lt;fieldset&gt; 
      &lt;legend&gt;Rating&lt;/legend&gt;  
      &lt;label&gt;&lt;input type="radio"/&gt; 1&lt;/label&gt; 
      &lt;label&gt;&lt;input type="radio"/&gt; 2&lt;/label&gt; 
      &lt;label&gt;&lt;input type="radio"/&gt; 3&lt;/label&gt; 
      &lt;label&gt;&lt;input type="radio"/&gt; 4&lt;/label&gt; 
      &lt;label&gt;&lt;input type="radio"/&gt; 5&lt;/label&gt;  
   &lt;/fieldset&gt;  
   &lt;label&gt;Review&lt;/label&gt; 
   &lt;textarea&gt;&lt;/textarea&gt;  
   &lt;button type="submit"&gt;Send&lt;/button&gt;  
&lt;/form&gt;
</code></pre>

<small><i>A lot of attributes have been left out to keep the HTML compact.</i></small>

The “product detail” sticky might be a bit more challenging. In its most minimal form, it could be just a “title,” “image” and “short paragraph.” But your client might also want things in there like “product specifications,” “ordering options,” “related products,” etc. These other content types require further discussion and prioritization. In the end, you might conclude that “post a review” is actually a part of “product detail” because people will be posting a review of the product described in “product detail.”

<pre><code class="language-markup">
&lt;article&gt; 
   &lt;h1&gt;MacBook Pro&lt;/h1&gt;  
   &lt;img src="macbook-pro.jpg"/&gt;  
   &lt;p&gt;A groundbreaking Retina display. All-flash architecture. Fourth-generation Intel processors. Remarkably thin and light 13‑inch and 15‑inch designs. Together, these features take the notebook to a place it’s never been. And they’ll do the same for everything you create with it.&lt;/p&gt;  

   &lt;section&gt;
      &lt;h1&gt;Post a Review&lt;/h1&gt;
        &lt;!-- 'post review' module here --&gt;
     &lt;/section&gt;  
&lt;/article&gt;
</code></pre>

<small><i>A lot of attributes have been left out to keep the HTML compact.</i></small>

These content types don’t stand on their own. They should be contained in an overall content hierarchy, as we saw in the series of images related to semantic HTML earlier. Together with this hierarchy, your content types should create a nice and correct <a href="https://developer.mozilla.org/en-US/docs/Web/Guide/HTML/Sections_and_Outlines_of_an_HTML5_document">HTML5 sectioning outline</a>. To test this, you can copy your HTML to the <a href="https://gsnedders.html5.org/outliner/">HTML5 Outliner</a>.

Below is an example of an initial web page setup.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/56ede65d-462f-4136-bbdb-3d0067f74521/14-setup-content-opt.png" alt="14-setup-content-opt" /></figure>

Now, we could have also done a bit of <a href="https://trentwalton.com/2011/07/14/content-choreography/">content choreography</a> to make sure each bit of content receives the right amount of attention from the user. In his excellent book <a href="https://responsivedesignworkflow.com"><em>Responsive Design Workflow</em></a>, <a href="https://twitter.com/stephenhay">Stephan Hay</a> advises us to set up content reference wireframes at this point. In my opinion this would be a bit too early — it’s best to wait a bit longer on the composition, because color, typography and functionality will affect the way attention is distributed across the page.

Let’s continue with our basic HTML web page. Don’t show it to your client yet; mix in their brand identity first. Add their logo, and convert their typography rules and color schemes to CSS. This will make it easier for your client to identify with the content — the content will look less anonymous and more like their own.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/822bbb6e-9a95-403c-b9fb-6afabbd7d173/15-setup-brand-opt.png" alt="15-setup-brand-opt" /></figure>

While your client would be able to relate to the version shown above, they would probably have a hard time getting enthusiastic about it. In my experience, the client will be impressed with the amount of work done but will feel uncomfortable not knowing what the result will look like. I recently renovated my house, and I have to admit, after totally stripping it, taking down walls and removing old plumbing and electricity, I seriously doubted whether it would come together in the end. That’s when I understood how my clients feel.</p>

<strong>You need to manage that feeling</strong> or else they’ll panic and fall back to the classic web development pattern, demanding design up front.

The version above is the “minimum viable web page.” It contains, if all has gone according to plan, the core content that your client’s users will be coming to the web page for.

If you’ve been using actual content, then even if all hell breaks loose, you could put this online as is. It wouldn’t be perfect, but the brand would be recognizable, and users would be able to access the information.

For now, hell is not breaking loose. So let’s move to the content choreography. Start resizing the browser window and view the page on some different devices. You’ll notice that on a wider viewport the line lengths will become uncomfortable to read. An <a href="https://nerd.vasilis.nl/ideal-measure-web/">ideal line contains between 45 and 75 characters</a>. So, you can regard points where it’s longer or shorter than that as indicators to tweak the layout or font size.

You have two options here: either make the adjustments live in the browser or boot up your favorite design tool. In my experience, designing in the browser is useful for tweaking things such as font size and color, while composition experiments are easier to do in Sketch or Photoshop or using pen and paper.

Tweaking CSS values in the browser might be tempting, but taking a screenshot and making some quick adjustments outside of the browser is usually faster. I find this results in more interesting design choices. When sketching, try to imagine how your solution would scale or break in smaller and bigger viewports and how your design choices relate to the content’s order and importance.

When you’re happy with the sketches, transform the result to CSS.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/659a509e-7aaf-4a78-8946-b62aeeb96fb6/16-setup-composition-opt.png" alt="16-setup-composition-opt" /></figure>

Now that we have set up the base version of the web page, we can start testing and iterating. Do some quick usability tests, which you can easily do by following the <a href="https://www.amazon.com/Dont-Make-Me-Think-Usability/dp/0321344758"><em>Don’t Make Me Think</em></a> methodology. Sometimes creating a small prototype for this is easier than using the production version.

While tweaking the web page for each context, we can look into adding functionality and presentation styles based on <a href="https://conditionerjs.com">contextual measurements</a>. For instance, in small viewports, we could move the menu out of view. Or when the user is viewing the web page late at night <a href="https://developer.mozilla.org/en-US/docs/Web/API/DeviceLightEvent">in a dimly lit environment</a>, we could load a style sheet with inverted colors. If enough real estate is available, we could turn an address into a Google Map.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4975f2e7-2cd4-462b-9db4-e03e9007ef43/17-setup-respond-opt.png" alt="17-setup-respond-opt" /></figure>

If you look closely, you’ll notice that all of these enhancements are layered on top of the content. They only change the way the content is presented and interacted with; they never change the content (or priority of content) itself. This fits perfectly with a strategy of progressive enhancement: Start with the content, and work from there.

We’ll finish up this section with a short note about web applications. The methodology explained above is for content-driven web pages — pages that are and should be accessible to everyone in all contexts. Not all web applications fit this description. Many use HTML to describe the interface instead of the content. In these cases, this methodology might not be the best fit.</p>

## Advantages Over Design-First Approach

I’ve compiled a list of the challenges overcome and the advantages gained by this approach. Not to say that this approach does not introduce new challenges, but those new challenges mostly have to do with managing client expectations and team communication.

To the list!

*   Content — and, therefore, HTML — is the only constant across all devices. How you present your content and how users interact with it will differ between devices, but the content will remain the same. **Starting with content means starting with everyone**.
*   Describing content with HTML is not only about lists, paragraphs and headings. It’s also about choosing between buttons and links, dropdown and radio buttons, tables and definition lists. It’s about outlining all functionality with HTML first.
*   With the content nailed down, there’s less confusion about what things actually are. Something could look like a button in a visual design but in reality be a hyperlink. This creates miscommunication in a team, which is easily prevented by writing HTML first.
*   Because we’ve layered design on top of HTML, we have created an opportunity for the team to work together. Developers can work on implementing the HTML, while designers can think of compositions for various viewports and contexts. No more deliverable dependencies means no more tiny secret waterfalls.
*   This methodology enables designers to work concurrently with their developer buddies, allowing them to quickly test things in the browser. Some design problems might be easier to tackle in CSS. As [Paul Boag explains](https://www.smashingmagazine.com/2014/11/21/why-you-should-include-your-developer-in-the-design-process/): “Developers might suggest ideas that you might have dismissed as impossible.”
*   It’s now clear what content should be generated or be manageable via the CMS. Hidden skip links, headers and labels are no longer hidden — all content is right there in plain sight. Design choices can now make content implicit, but that does not mean the content won’t end up in the HTML, because we’ve already written it. In my experience, none of these implicit content items end up in the CMS because they aren’t visible to everyone. By starting with HTML, this is easily resolved.
*   If you and the client have pinned down what content you want to communicate to users, that will very likely not change during the development process. A change would only happen if user research uncovers some previously unknown facts that warrant a change in course.
*   **Content creates focus**. By focusing on content and functionality early on in the process, you’re less likely to end up in a “red or blue?” discussion with the client. Too often clients are tempted to focus on details when they should be thinking of the big picture. With this layered setup, the focus starts with the big picture and then moves to the details during the project.
*   Having the HTML early on enables you to build the minimum viable product first. In later stages of the project, you can progressively enhance it to further improve the user experience. If you introduce usability testing in the project (which you should), you can use the results to decide what to enhance first. An asynchronous search filtering system might be cool, but your users might value other functionality more. [Harry Roberts reminds us](https://speakerdeck.com/csswizardry/ten-principles-for-effective-front-end-development?slide=21) that “good enough” today is better than “perfect” tomorrow.
*   As we saw with the call-to-action buttons in the semantic HTML exercise, spotting user experience problems is easier when you’re working with content as the foundation.
*   Once you’ve finished the HTML, you can immediately start testing the content with visually impaired users. Most of the additional layering will be for the sighted.
*   Starting with content enables you to more easily define your HTML5 sectioning outline, to pick [micro-formats](https://microformats.org) or [micro-data](https://html5doctor.com/microdata/) and to apply [WAI-ARIA rules](https://www.smashingmagazine.com/2014/07/09/the-wai-forward/). This results in better accessibility and makes the pages easier to index by search bots.
*   This approach entails going from a robust stable base to a very detailed flexible end product. By staying away from highly detailed solutions early on, you decrease the risk of putting a lot of hours into unneeded functionality. For example, you could build synchronous search first, and then later on in the project, if your user base turns out to heavily favor search, you could layer asynchronous search and filtering on top of it.
*   A correctly written HTML tree provides natural hooks for JavaScript later on. Content under headings could be made visible in large viewports and then presented in an accordion in smaller ones.
*   No longer are you creating pretty pictures of web pages. The focus has moved to quick sketches and tiny prototypes to solve design challenges, and the results are quickly transformed in CSS and moved to the browser. We’re throwing away fewer deliverables, which means we’re working more efficiently.</p>

## Talk To Your Client

As with everything, it’s all about communication.

If your client thinks the Web is a 1024 × 768-pixel box — and continues thinking this while you and your team are working on their shiny new website — then you’re going to run into a lot of trouble.

Many clients expect a visual design up front, because that’s what they’re used to getting. They don’t know any better.

Your job — not an easy one — is to explain to them why this is impossible. Enlighten them about the millions of different viewports, interaction methods and feature sets out there, and help them understand that you cannot capture all of that in a static design.

If your client understands the Web, you’ve won half the battle.

{{< signature "vf, il, al, ml" >}}

