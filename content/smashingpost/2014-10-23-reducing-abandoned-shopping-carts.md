---
title: Reducing Abandoned Shopping Carts In E-Commerce
slug: reducing-abandoned-shopping-carts
image: 'https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cd06264e-1ace-4ed4-83af-c2c1058633a4/illu-shopify.jpg'
date: 2014-10-23T20:43:34.000Z
author: keir-whitaker
description: >-
  In March 2014, the Baymard Institute, a web research company based in the UK,
  reported that 67.91% of online shopping carts are abandoned. An abandonment
  means that a customer has visited a website, browsed around, added one or more
  products to their cart and then left without completing their purchase. A
  month later in April 2014, Econsultancy stated that global retailers are
  losing $3 trillion (USD) in sales every year from abandoned carts.
categories:
  - UX
  - Business
  - E-Commerce
  - UX
  - Income
  - Product Strategy
---
In March 2014, the Baymard Institute, a web research company based in the UK, <a href="https://baymard.com/lists/cart-abandonment-rate">reported that 67.91%</a> of online shopping carts are abandoned. An abandonment means that a customer has visited a website, browsed around, added one or more products to their cart and then left without completing their purchase. A month later in April 2014, <a href="https://econsultancy.com/blog/64680-six-tactics-for-reducing-cart-abandonment-rates#i.weabnjzqdeyu10">Econsultancy stated</a> that global retailers are losing $3 trillion (USD) in sales every year from abandoned carts.

Clearly, <strong>reducing the number of abandoned carts would lead to higher store revenue</strong> — the goal of every online retailer. The question then becomes how can we, as designers and developers, help convert these “warm leads” into paying customers for our clients?

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Fundamental Guidelines Of E-Commerce Checkout Design](https://www.smashingmagazine.com/2011/04/fundamental-guidelines-of-e-commerce-checkout-design/)
*   [Local Storage And How To Use It On Websites](https://www.smashingmagazine.com/2010/10/local-storage-and-how-to-use-it/)
*   [Boost Your Mobile E-Commerce Sales With Mobile Design Patterns](https://www.smashingmagazine.com/2012/12/boost-your-mobile-e-commerce-sales-with-mobile-design-patterns/)
*   [A Little Journey Through (Small And Big) E-Commerce Websites](https://www.smashingmagazine.com/2013/12/e-commerce-websites-showcase/)

## Before Cart Abandonment

Let’s begin by looking at recognized improvements we can make to an online store to reduce the number of “before cart” abandonments. These improvements focus on changes that aid the customer’s experience prior to reaching the cart and checkout process, and they include the following:

{{% feature-panel %}}

*   **Show images of products.**.  This reinforces what the customer is buying, especially on the cart page.
*   **Display security logos and compliance information.**.  This can allay fears related to credit-card and payment security.
*   **Display contact details.**.  Showing offline contact details (including a phone number and mailing address) in addition to an email address adds credibility to the website.
*   **Make editing the cart easier.**.  Make it as simple as possible for customers to change their order prior to checking out.
*   **Offer alternative payment methods.**.  Let people check out with their preferred method of payment (such as PayPal and American Express, in addition to Visa and MasterCard).
*   **Offer support.**.  Providing a telephone number and/or online chat functionality on the website and, in particular, on the checkout page will give shoppers confidence and ease any concerns they might have.
*   **Don’t require registration.** This one resonates with me personally. I often click away from websites that require lengthy registration forms to be filled out. By allowing customers to “just” check out, friction is reduced.
*   **Offer free shipping.**.  While merchants might include shipping costs in the price, “free shipping” is nevertheless an added enticement to buy.
*   **Be transparent about shipping costs and time.**.  Larger than expected shipping costs and unpublished lead times will add unexpected costs and frustration.
*   **Show testimonials.**.  Showcasing reviews from happy customers will alleviate concerns any people might have about your service.
*   **Offer price guarantees and refunds.**.  Offering a price guarantee gives shoppers the confidence that they have found the best deal. Additionally, a clear refund policy will add peace of mind.
*   **Optimize for mobile.**.  Econsultancy reports that sales from mobile devices increased by 63% in 2013\. This represents a real business case to move to a “responsive” approach.
*   **Display product information.**.  Customers shouldn’t have to dig around a website to get the information they need. Complex navigation and/or a lack of product information make for a frustrating experience.

Unfortunately, even if you follow all of these recommendations, the reality is that customers will still abandon their carts — whether through frustration, bad design or any other reason they see fit.</p>

## After Cart Abandonment

The second approach is to look at things we can do once a cart has been abandoned. One tactic is to email the customer with a personalized message and a link to a prepopulated cart containing the items they had selected. This is known as an “abandoned cart email.”

The concept is pretty simple. At the right time, a customizable email is sent, complete with a personalized message and a link to the customer’s abandoned cart. Of course, this approach assumes that the customer has submitted their email address — effectively, they’ve done everything but paid. Abandoned cart emails represent one last attempt by the merchant to convince the buyer to check out.

In September 2013, <a href="https://econsultancy.com/blog/63466-nine-case-studies-and-infographics-on-cart-abandonment-and-email-retargeting#i.weabnjzqdeyu10">Econsultancy outlined</a> how an online cookie retailer recaptured 29% of its abandoned shopping carts via email. This is a huge figure and one we might naturally be skeptical of.

To get a more realistic perspective, I asked my colleagues at <a href="https://shopify.com">Shopify</a> to share some of their data on this, and they kindly agreed. Shopify introduced “abandoned cart recovery” (ACR) in mid-September 2013 (just over a year ago at the time of writing). Here’s a summary of its effectiveness:

*   In the 12 months since launching automatic ACR, $12.9 million have been recovered through ACR emails in Shopify.
*   4,085,592 emails were sent during this period, of which 147,021 carts were completed as a result. This represents a 3.6% recovery rate.
*   Shop owners may choose to send an email 6 or 24 hours after abandonment. Between the two, 6-hour emails convert much better: a 4.1% recovery rate for 6 hours versus 3% for 24 hours.

It’s worth noting that the 3.6% recovery rate is from Shopify’s ACR emails. Many merchants use <a href="https://apps.shopify.com/search/query?utf8=%E2%9C%93&amp;q=abandoned">third-party apps</a> instead of Shopify’s native feature. Given that Shopify is unable to collect data on these services, the number of emails sent and the percentage of recovered carts may well be higher.

Given the statistics, abandoned cart emails are clearly an important part of an online retailer’s marketing strategy. Luckily, most leading e-commerce platforms enable merchants to send custom emails, either in plain text or HTML. Knowing how to implement these notifications is a useful skill if you are designing for e-commerce, and they represent added value to your services.</p>

## Creating An HTML Abandoned Cart Email

The implementation of abandoned cart emails varies from platform to platform. Some platforms require third-party plugins, whereas others have the functionality built in. For example, both plain-text and HTML versions are available on Shopify. While the boilerplates are very usable, you might want to create a custom HTML version to complement the branding of your store. We’ll look at options and some quick wins shortly.

In recent years, HTML email newsletters have really flourished. You only have to look at the many <a href="https://inspiration.mailchimp.com/">galleries</a> to see how far this form of marketing has progressed. Sending an HTML version, while not essential, certainly allows for more flexibility and visual design (although always sending a plain-text version, too, is recommended). However, it’s not without its pain points.

If you’ve been developing and designing for the web since the 1990s, then you will remember, fondly or otherwise, the “fun” of beating browsers into shape. Designing HTML newsletters is in many ways a throwback to this era. Table-based layouts are the norm, and we also have to contend with email clients that render HTML inconsistently.

Luckily for us, the teams at both <a href="https://campaignmonitor.com">Campaign Monitor</a> and <a href="https://mailchimp.com">MailChimp</a> have written extensively on this subject and provide many solutions to common problems. For example, Campaign Monitor <a href="https://www.campaignmonitor.com/css/">maintains a matrix and provides a downloadable poster</a> outlining the CSS support of each major desktop and mobile email client. MailChimp, for its part, provides numerous resources on <a href="https://templates.mailchimp.com/resources/email-client-css-support/">CSS</a> and <a href="https://templates.mailchimp.com/">email template design</a>. Familiarizing yourself with the basics before tackling your first HTML email is worthwhile — even if you ultimately use a template.</p>

## Open-Source Responsive Email Templates

While many of you might wish to “roll your own” template, I often find it easier to build on the great work of others. For example, a number of great open-source projects focus on HTML email templates, including <a href="https://github.com/mailchimp/Email-Blueprints">Email Blueprints</a> by MailChimp.

Another example comes from Lee Munroe. His “<a href="https://blog.mailgun.com/transactional-html-email-templates/">transactional HTML email templates</a>” differ in that they are not intended for use as newsletters, but rather as “transactional” templates. To clarify the difference, Lee breaks down transactional email into three categories:

*   **action emails**.  “Activate your account,” “Reset your password”
*   **email alerts**.  “You’ve reached a limit,” “A problem has occurred”
*   **billing emails** monthly receipts and invoices

The templates are purposefully simple yet elegant. They also have the added benefit of having been throughly tested in all major email clients. Finally, because they are responsive, they cater to the <a href="https://emailclientmarketshare.com/">50+%</a> of emails opened via mobile devices.</p>

## The Challenge

Lee’s templates are a good option for creating a simple HTML email for abandoned carts. Therefore, let’s move on from the theory and look at how to create an HTML template for the Shopify platform.

Let’s begin by setting some constraints on the challenge:

1.  make the fewest number of markup changes to Lee’s template;
2.  make use of the boilerplate text that is set as the default in the abandoned cart HTML template in Shopify;
3.  inline all CSS (a best practice for HTML email);
4.  send a test email with dummy data, and review the results in Airmail, Gmail and Apple Mail (on iOS).</p>

### 1. Create a Local Copy of the Action Email Template

Having looked at the three templates, the “action” version appears to offer the best starting point. You can download the HTML for this template directly <a href="https://raw.githubusercontent.com/mailgun/transactional-email-templates/master/templates/alert.html">from GitHub</a> if you wish to follow along.

The first step is to take the contents of Lee’s template and save it locally as <code>abandoned-cart.html</code>. A quick sanity check in a browser shows that the style sheet isn’t being picked up.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/142d1475-6f28-49e6-8d9e-ec106203988e/01-template-setup-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7cf4abfb-1f5f-43f4-a07e-f5f098194a62/01-template-setup-opt-small.png" alt="Basic template setup." width="500" height="175" /></a><figcaption>Basic template setup. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/142d1475-6f28-49e6-8d9e-ec106203988e/01-template-setup-opt.png">View large version</a>)</figcaption></figure>

Inlining all CSS is recommended (we’ll look at this in a later step), so add the styles to the <code>&lt;head&gt;</code> section of <code>abandoned-cart.html</code>. You can copy the CSS in its entirety <a href="https://raw.githubusercontent.com/mailgun/transactional-email-templates/master/templates/styles.css">from GitHub</a> and then paste it in a <code>&lt;style&gt;</code> element. Another check in the browser shows that the styles are being applied.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c25cec18-0ec9-4c38-aec8-50bb8ac3de83/02-css-applied-opt.png" alt="CSS applied." width="500" height="307" /><br>
<figcaption>CSS applied.</figcaption></figure>

### 2. Add the Content

Now that the template is working as a standalone document, it’s time to look at integrating <a href="https://docs.shopify.com/themes/liquid-documentation/basics">Liquid</a>’s boilerplate code from Shopify’s default template. This can be found in the Shopify admin section under “Settings” → “Notifications” → “Abandoned cart.” If you wish to follow along with these code examples, you can set up a free fully featured <a href="https://docs.shopify.com/themes/theme-development/getting-started/development-environment">development store</a> by signing up to <a href="https://www.shopify.com/partners">Shopify’s Partner Program</a>.</p>

<pre><code class="language-ruby">
Hey{% if billing_address.name %} {{ billing_address.name }}{% endif %},
Your shopping cart at {{ shop_name }} has been reserved and is waiting for your return!
In your cart, you left:
{% for line in line_items %}{{ line.quantity }}x {{ line.title }}{% endfor %}
But it’s not too late! To complete your purchase, click this link:
{{ url }}
Thanks for shopping!
{{ shop_name }}
</code></pre>

All notification emails in Shopify make use of Liquid, the templating language developed by Shopify and now available as an open-source project and found in tools such as <a href="https://mixture.io">Mixture</a> and software such as <a href="https://jekyllrb.com/">Jekyll</a> and <a href="https://www.siteleaf.com/">SiteLeaf</a>. Liquid makes it possible to pull data from the store — in this case, all of the details related to the abandoned cart and the user it belonged to.

Having studied the markup, I’ve decided to place the boilerplate content in a single table cell, starting on <a href="https://github.com/mailgun/transactional-email-templates/blob/master/templates/alert.html#L27">line 27</a> of Lee’s original document.

After pasting in the boilerplate code, let’s double-check that the template renders as expected in the browser. At this stage, Liquid’s code is appearing “as is.” Only once the template is applied to Shopify’s template will this be replaced with data from the store.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1f60cd9e-8571-44f1-b822-41ea1c9cb3db/03-boilerplate-text-added-opt.png" alt="Boilerplate text added." width="500" height="375" /><figcaption>Boilerplate text added.</figcaption></figure>

### 3. Modify the Boilerplate Code

The next stage involves tidying up some of the boilerplate code, including wrapping the boilerplate text in <code>&lt;p&gt;</code> tags. Then, it’s time to work out how best to display the cart’s contents in markup. For speed, I’ve chosen an unordered list. Liquid’s refactored <a href="https://docs.shopify.com/themes/liquid-documentation/objects/for-loops"><code>for</code> loop</a> is pretty straightforward:

<pre><code class="language-markup">
&lt;ul&gt;
{% for line in line_items %}
&lt;li&gt;{{ line.quantity }} x {{ line.title }}&lt;/li&gt;
{% endfor %}
&lt;/ul&gt;
</code></pre>

After another sanity check, things are looking much more promising. However, we need to make a few final tweaks to make it work:

*   remove unwanted table rows,
*   add the correct link to the blue call-to-action button,
*   change the contents of the footer.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6f661053-8da6-480c-9457-517c5e232b0d/04-tidying-up-opt.png" alt="Tidying up." width="500" height="431" /><br>
<figcaption>Tidying up.</figcaption></figure>

## 4\. Make Final Adjustments

Lee’s template includes markup to create a big blue “Click me” button. You can see this on <a href="https://github.com/mailgun/transactional-email-templates/blob/master/templates/alert.html#L38">line 38</a>:

<pre><code class="language-markup">
&lt;a href="https://www.mailgun.com" class="btn-primary"&gt;Upgrade my account&lt;/a&gt;
</code></pre>

Let’s turn this into a relevant link by changing the markup to this:

<pre><code class="language-markup">
&lt;p&gt;&lt;a href="{{ url }}" class="btn-primary"&gt;Check out now&lt;/a&gt;&lt;/p&gt;
</code></pre>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/494b6c92-0ab8-4884-b021-890d64c95191/05-adding-the-call-opt.png" alt="Adding the call-to-action URL." width="500" height="396" /><br>
<figcaption>Adding the call-to-action URL.</figcaption></figure>

In this case, <code>{{ url }}</code> represents the link to the abandoned (and saved) cart. I’ve enclosed the anchor in a paragraph to ensure consistent spacing when the email is rendered, and I’ve moved it up into the main section.

Finally, we’ve changed the unsubscribe link in the footer to a link to the shop:

<pre><code class="language-markup">
&lt;a href="{{ shop.url }}"&gt;Visit {{ shop_name }}&lt;/a&gt;
</code></pre>

After a few minutes of editing, the template looks more than respectable. However, we’ve neglected one section, the text in the yellow highlighted “alert” section. I’ve changed this, along with the <code>title</code> element in the HTML, to this:

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/397ff92f-386c-4bba-9df3-f0f08a2477e6/06-changing-header-footer-opt.png" alt="Changing the header text and footer link." width="500" height="411" /><br>
<figcaption>Changing the header text and footer link.</figcaption></figure>

<pre><code class="language-markup">
Your cart at {{ shop_name }} has been reserved and is waiting for your return!
</code></pre>

Email notifications in Shopify have access to a number of variables that can be accessed via Liquid. A full list is available <a href="https://docs.shopify.com/manual/settings/notifications/email-variables">in Shopify’s documentation</a>.</p>

### 5. Inline the CSS

To recap, we’ve changed the template’s markup very little, and the CSS is identical to Lee’s original (albeit in the template, rather than in an external file). Shopify’s boilerplate text is also intact, albeit with a very small change to Liquid’s <code>for</code> loop.

The next step is to inline the CSS in the HTML file. Because some email clients remove <code>&lt;head&gt;</code> and <code>&lt;style&gt;</code> tags from email, moving the CSS inline means that our email should render as intended. Chris Coyier penned “<a href="https://css-tricks.com/using-css-in-html-emails-the-real-story/">Using CSS in HTML Emails: The Real Story</a>” back in November 2007 — the landscape hasn’t changed much since.

Thankfully, taking your CSS inline isn’t a long or difficult process. In fact, it’s surprisingly easy. A <a href="https://www.google.co.uk/webhp?sourceid=chrome-instant&amp;amp;ion=1&amp;amp;espv=2&amp;amp;ie=UTF-8#q=inline+css+html+email">number of free services</a> enable you to paste markup and will effectively add your styles inline.

I’ve chosen <a href="https://premailer.dialect.ca/">Premailer</a> principally because it has a few extra features, including the ability to remove native CSS from the <code>&lt;head&gt;</code> section of the HTML document, which saves a few kilobytes from the file’s size. After pasting in the markup and pressing “Submit,” Premailer generates a new HTML version that you can copy and paste back into your document. It also creates a plain-text version of the email, should you need it.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7446aecb-a28b-4624-91ad-feb34544f7d1/07-premailer-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a33c7d04-8e8f-49d9-ba0f-deb48ca8119f/07-premailer-opt-small.jpg" alt="Premailer has the ability to remove native CSS which saves a few kilobytes." width="423" height="600" /></a><figcaption>Premailer has the ability to remove native CSS which saves a few kilobytes. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7446aecb-a28b-4624-91ad-feb34544f7d1/07-premailer-opt.jpg">View large version</a>)</figcaption></figure>

Another great feature of Premailer is that you can view the new markup in the browser. You’ll find a link above the text box containing the new markup, titled “Click to View the HTML Results.” Clicking the link opens a hosted version of the new markup, which you can use to check your sanity or share with colleagues and clients.

If you are keen to automate the creation of e-commerce notification emails, then Premailer also offers <a href="https://premailer.dialect.ca/api">an API</a>. A number of libraries that support it are also available on GitHub, including <a href="https://github.com/onassar/PHP-Premailer">PHP-Premailer</a>.

The final task is to copy the new HTML code and paste it in the “HTML” tab of our abandoned cart notification in Shopify’s admin area. Once it’s applied, you can preview the email in the browser, as well as send a dummy copy to an email address.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a3bb97c0-d352-4f02-9a66-5fef9ca4fd8e/08-template-8-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6415969f-e1c2-46a4-b20b-0a5fbfc6967f/08-template-8-opt-small.jpg" alt="Shopify admin." width="500" height="357" /></a><figcaption>Shopify admin. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a3bb97c0-d352-4f02-9a66-5fef9ca4fd8e/08-template-8-opt.jpg">View large version</a>)</figcaption></figure>

Below are the results in various email clients (both mobile and desktop).</p>

### Airmail

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/57120e8c-821a-4e1d-9af7-844ce3484002/09-airmail-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0d4d8da3-82c2-4677-8451-d96657292934/09-airmail-opt-small.png" alt="Airmail rendering." width="500" height="326" /></a><figcaption>Airmail rendering. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/57120e8c-821a-4e1d-9af7-844ce3484002/09-airmail-opt.png">View large version</a>)</figcaption></figure>

### Apple Mail

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/aa33a0c7-fcc0-46db-92d1-df65095f8055/10-ios-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b4d18e7a-1e34-4b7b-83fc-bf2066790b1e/10-ios-opt-small.jpg" alt="Apple Mail rendering." width="338" height="600" /></a><figcaption>Apple Mail rendering. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/aa33a0c7-fcc0-46db-92d1-df65095f8055/10-ios-opt.jpg">View large version</a>)</figcaption></figure>

### Gmail (Browser)

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/97e3cfb9-3cc4-44f0-88d2-d5423812563b/11-gmail-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/542bcaf8-e0c0-484a-9908-5ee5c2cb72a1/11-gmail-opt-small.png" alt="Gmail rendering." width="500" height="313" /></a><figcaption>Gmail rendering. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/97e3cfb9-3cc4-44f0-88d2-d5423812563b/11-gmail-opt.png">View large version</a>)</figcaption></figure>

### Apple Mail on iOS

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6b9b474d-ca27-4d88-abd1-ece0f27f8ba5/12-mail-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f849a506-be82-4295-a98e-cd732bcbc601/12-mail-opt-small.png" alt="Apple Mail on iOS rendering." width="338" height="600" /></a><figcaption>Apple Mail on iOS rendering. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6b9b474d-ca27-4d88-abd1-ece0f27f8ba5/12-mail-opt.png">View large version</a>)</figcaption></figure>

The process of turning Lee’s template into a usable email took around 30 minutes, and I am pretty pleased with the result from such little input.

Of course, this process screams out for automation. For those who are interested, Lee has also posted about his <a href="https://www.leemunroe.com/email-design-workflow/">workflow for creating HTML email templates</a> and the toolkit he uses (Sketch, Sublime, Grunt, SCSS, Handlebars, GitHub, Mailgun, Litmus).</p>

## Taking It Further

The template produced above is admittedly quite basic and only scratches the surface of what is possible. We could do plenty more to customize our email for abandoned carts, such as:

*   consider tone of voice,
*   show product images to jog the customer’s memory,
*   add a discount code to encourage the user to return and buy,
*   add upsells,
*   list complementary products.</p>

### Dodo Case

Tone of voice is a key consideration and goes a long way to engaging the customer. <a href="https://www.dodocase.com/">Dodo Case</a> has a great example:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2956d94c-8b90-4f88-b463-c45ef7e4bd59/13-dodocase-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ee52a865-02dc-4be2-81eb-1c414b48f534/13-dodocase-opt-small.png" alt="Dodo Case’s email for abandoned carts." width="500" height="208" /></a><figcaption><a href="https://www.dodocase.com/">Dodo Case</a>’s email for abandoned carts. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2956d94c-8b90-4f88-b463-c45ef7e4bd59/13-dodocase-opt.png">View large version</a>)</figcaption></figure>

As always, context is very important when it comes to tone of voice. What’s right for Dodo Case might not be right for a company specializing in healthcare equipment.

Let’s review a few examples (taken from <a href="https://www.shopify.co.uk/blog/12522201-13-amazing-abandoned-cart-emails-and-what-you-can-learn-from-them">Shopify’s blog</a>) to get a taste of what other companies are doing.</p>

### Fab

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/697c940c-f923-4719-af24-e6561700025a/14-fab-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/78e0d337-d116-47b9-b87d-07542683c639/14-fab-opt-small.jpg" alt="Fab’s email for abandoned carts." width="500" height="534" /></a><figcaption><a href="https://www.fab.com">Fab</a>’s email for abandoned carts. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/697c940c-f923-4719-af24-e6561700025a/14-fab-opt.jpg">View large version</a>)</figcaption></figure>

While this email from <a href="https://www.fab.com">Fab</a> is pretty standard, the subject line is very attention-grabbing and is a big call to action.</p>

### Chubbies

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2f526480-0c6d-4388-8c65-1bb0b108660d/15-chubbies-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cc8bddd7-1c66-49ea-b90c-22b00ad7f3fa/15-chubbies-opt-small.jpg" alt="Chubbies’ email for abandoned carts." width="500" height="601" /></a><figcaption><a href="https://www.chubbiesshorts.com/">Chubbies</a>’ email for abandoned carts. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2f526480-0c6d-4388-8c65-1bb0b108660d/15-chubbies-opt.jpg">View large version</a>)</figcaption></figure>

The language and tone used in Chubbies’ email really stands out and is in line with the brand: fun-loving people. There’s also no shortage of links back to the cart, including the title, the main image and the call to action towards the bottom of the email.</p>

### Black Milk Clothing

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a6064638-8a1d-4389-965f-48483049d5d4/16-blackmilk-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fcb79b6d-280c-4cc9-9898-0db202b3d3e1/16-blackmilk-opt-small.jpg" alt="Black Milk’s email for abandoned carts." width="500" height="601" /></a><figcaption><a href="https://blackmilkclothing.com/">Black Milk</a>’s email for abandoned carts. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a6064638-8a1d-4389-965f-48483049d5d4/16-blackmilk-opt.jpg">View large version</a>)</figcaption></figure>

<a href="https://blackmilkclothing.com/">Black Milk Clothing</a> includes a dog photo and employs playful language, such as “Your shopping cart at Black Milk Clothing has let us know it’s been waiting a while for you to come back.”

### Holstee

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c28de67a-9440-44dc-a5a7-775b815b3f62/17-holstee-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/41e3abeb-7483-4b30-9b08-97b1375d0632/17-holstee-opt-small.png" alt="Holstee’s email for abandoned carts." width="500" height="495" /></a><figcaption><a href="https://holstee.com">Holstee</a>’s email for abandoned carts. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c28de67a-9440-44dc-a5a7-775b815b3f62/17-holstee-opt.png">View large version</a>)</figcaption></figure>

Finally, <a href="https://holstee.com">Holstee</a> asks if there’s a problem they can help with. It even goes so far as to include a direct phone number to its “Community Love Director.” Having worked with Holstee, I can confirm that this is a real position within the company!

## Conclusion

While there are many tactics to persuade customers to buy, inevitably some people will get to the payment screen and decide not to continue. Any tactic that helps to seal the deal is certainly worth considering, and given the small amount of work involved in implementing an email to recover abandoned carts, it’s a great place to start. Designers and developers are in a powerful position to help their clients increase their revenue, and being armed with tactics such as the ones outlined in this article will hopefully enable them to offer a wider range of services.</p>

### Further Reading

*   “[Nine Case Studies and Infographics on Cart Abandonment and Email Retargeting](https://econsultancy.com/blog/63466-nine-case-studies-and-infographics-on-cart-abandonment-and-email-retargeting#i.weabnjzqdeyu10),” David Moth, Econsultancy
*   “[13 Best Practices for Email Cart Abandonment Programs](https://www.exacttarget.com/blog/13-best-practices-for-email-cart-abandonment-programs/),” Kyle Lacy, Salesforce Marketing Cloud Blog
*   “[Lost Sales Recovery, Part 2,: Crafting a Perfect Remarketing Message](https://blog.mageworx.com/2014/04/cart-abandonment-email/),” Vitaly Gonkov, The MageWorx Blog
*   “[Why Online Retailers Are Losing 67.45% of Sales and What to Do About It](https://www.shopify.co.uk/blog/8484093-why-online-retailers-are-losing-67-45-of-sales-and-what-to-do-about-it),” Mark Macdonald, Shopify Ecommerce Marketing Blog

<pre><code class="language-ruby">
Hey{% if billing_address.name %} {{ billing_address.name }}{% endif %},
Your shopping cart at {{ shop_name }} has been reserved and is waiting for your return!
In your cart, you left:
{% for line in line_items %}{{ line.quantity }}x {{ line.title }}{% endfor %}
But it’s not too late! To complete your purchase, click this link:
{{ url }}
Thanks for shopping!
{{ shop_name }}
</code></pre>

All notification emails in Shopify make use of Liquid, the templating language developed by Shopify and now available as an open-source project and found in tools such as <a href="https://mixture.io">Mixture</a> and software such as <a href="https://jekyllrb.com/">Jekyll</a> and <a href="https://www.siteleaf.com/">SiteLeaf</a>. Liquid makes it possible to pull data from the store — in this case, all of the details related to the abandoned cart and the user it belonged to.

Having studied the markup, I’ve decided to place the boilerplate content in a single table cell, starting on <a href="https://github.com/mailgun/transactional-email-templates/blob/master/templates/alert.html#L27">line 27</a> of Lee’s original document.

After pasting in the boilerplate code, let’s double-check that the template renders as expected in the browser. At this stage, Liquid’s code is appearing “as is.” Only once the template is applied to Shopify’s template will this be replaced with data from the store.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1f60cd9e-8571-44f1-b822-41ea1c9cb3db/03-boilerplate-text-added-opt.png" alt="Boilerplate text added." width="500" height="375" /><figcaption>Boilerplate text added.</figcaption></figure>

### 3. Modify the Boilerplate Code

The next stage involves tidying up some of the boilerplate code, including wrapping the boilerplate text in <code>&lt;p&gt;</code> tags. Then, it’s time to work out how best to display the cart’s contents in markup. For speed, I’ve chosen an unordered list. Liquid’s refactored <a href="https://docs.shopify.com/themes/liquid-documentation/objects/for-loops"><code>for</code> loop</a> is pretty straightforward:

<pre><code class="language-markup">
&lt;ul&gt;
{% for line in line_items %}
&lt;li&gt;{{ line.quantity }} x {{ line.title }}&lt;/li&gt;
{% endfor %}
&lt;/ul&gt;
</code></pre>

After another sanity check, things are looking much more promising. However, we need to make a few final tweaks to make it work:

*   remove unwanted table rows,
*   add the correct link to the blue call-to-action button,
*   change the contents of the footer.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6f661053-8da6-480c-9457-517c5e232b0d/04-tidying-up-opt.png" alt="Tidying up." width="500" height="431" /><br>
<figcaption>Tidying up.</figcaption></figure>

## 4\. Make Final Adjustments

Lee’s template includes markup to create a big blue “Click me” button. You can see this on <a href="https://github.com/mailgun/transactional-email-templates/blob/master/templates/alert.html#L38">line 38</a>:

<pre><code class="language-markup">
&lt;a href="https://www.mailgun.com" class="btn-primary"&gt;Upgrade my account&lt;/a&gt;
</code></pre>

Let’s turn this into a relevant link by changing the markup to this:

<pre><code class="language-markup">
&lt;p&gt;&lt;a href="{{ url }}" class="btn-primary"&gt;Check out now&lt;/a&gt;&lt;/p&gt;
</code></pre>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/494b6c92-0ab8-4884-b021-890d64c95191/05-adding-the-call-opt.png" alt="Adding the call-to-action URL." width="500" height="396" /><br>
<figcaption>Adding the call-to-action URL.</figcaption></figure>

In this case, <code>{{ url }}</code> represents the link to the abandoned (and saved) cart. I’ve enclosed the anchor in a paragraph to ensure consistent spacing when the email is rendered, and I’ve moved it up into the main section.

Finally, we’ve changed the unsubscribe link in the footer to a link to the shop:

<pre><code class="language-markup">
&lt;a href="{{ shop.url }}"&gt;Visit {{ shop_name }}&lt;/a&gt;
</code></pre>

After a few minutes of editing, the template looks more than respectable. However, we’ve neglected one section, the text in the yellow highlighted “alert” section. I’ve changed this, along with the <code>title</code> element in the HTML, to this:

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/397ff92f-386c-4bba-9df3-f0f08a2477e6/06-changing-header-footer-opt.png" alt="Changing the header text and footer link." width="500" height="411" /><br>
<figcaption>Changing the header text and footer link.</figcaption></figure>

<pre><code class="language-markup">
Your cart at {{ shop_name }} has been reserved and is waiting for your return!
</code></pre>

Email notifications in Shopify have access to a number of variables that can be accessed via Liquid. A full list is available <a href="https://docs.shopify.com/manual/settings/notifications/email-variables">in Shopify’s documentation</a>.</p>

### 5. Inline the CSS

To recap, we’ve changed the template’s markup very little, and the CSS is identical to Lee’s original (albeit in the template, rather than in an external file). Shopify’s boilerplate text is also intact, albeit with a very small change to Liquid’s <code>for</code> loop.

The next step is to inline the CSS in the HTML file. Because some email clients remove <code>&lt;head&gt;</code> and <code>&lt;style&gt;</code> tags from email, moving the CSS inline means that our email should render as intended. Chris Coyier penned “<a href="https://css-tricks.com/using-css-in-html-emails-the-real-story/">Using CSS in HTML Emails: The Real Story</a>” back in November 2007 — the landscape hasn’t changed much since.

Thankfully, taking your CSS inline isn’t a long or difficult process. In fact, it’s surprisingly easy. A <a href="https://www.google.co.uk/webhp?sourceid=chrome-instant&amp;amp;ion=1&amp;amp;espv=2&amp;amp;ie=UTF-8#q=inline+css+html+email">number of free services</a> enable you to paste markup and will effectively add your styles inline.

I’ve chosen <a href="https://premailer.dialect.ca/">Premailer</a> principally because it has a few extra features, including the ability to remove native CSS from the <code>&lt;head&gt;</code> section of the HTML document, which saves a few kilobytes from the file’s size. After pasting in the markup and pressing “Submit,” Premailer generates a new HTML version that you can copy and paste back into your document. It also creates a plain-text version of the email, should you need it.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7446aecb-a28b-4624-91ad-feb34544f7d1/07-premailer-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a33c7d04-8e8f-49d9-ba0f-deb48ca8119f/07-premailer-opt-small.jpg" alt="Premailer has the ability to remove native CSS which saves a few kilobytes." width="423" height="600" /></a><figcaption>Premailer has the ability to remove native CSS which saves a few kilobytes. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7446aecb-a28b-4624-91ad-feb34544f7d1/07-premailer-opt.jpg">View large version</a>)</figcaption></figure>

Another great feature of Premailer is that you can view the new markup in the browser. You’ll find a link above the text box containing the new markup, titled “Click to View the HTML Results.” Clicking the link opens a hosted version of the new markup, which you can use to check your sanity or share with colleagues and clients.

If you are keen to automate the creation of e-commerce notification emails, then Premailer also offers <a href="https://premailer.dialect.ca/api">an API</a>. A number of libraries that support it are also available on GitHub, including <a href="https://github.com/onassar/PHP-Premailer">PHP-Premailer</a>.

The final task is to copy the new HTML code and paste it in the “HTML” tab of our abandoned cart notification in Shopify’s admin area. Once it’s applied, you can preview the email in the browser, as well as send a dummy copy to an email address.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a3bb97c0-d352-4f02-9a66-5fef9ca4fd8e/08-template-8-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6415969f-e1c2-46a4-b20b-0a5fbfc6967f/08-template-8-opt-small.jpg" alt="Shopify admin." width="500" height="357" /></a><figcaption>Shopify admin. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a3bb97c0-d352-4f02-9a66-5fef9ca4fd8e/08-template-8-opt.jpg">View large version</a>)</figcaption></figure>

Below are the results in various email clients (both mobile and desktop).</p>

### Airmail

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/57120e8c-821a-4e1d-9af7-844ce3484002/09-airmail-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0d4d8da3-82c2-4677-8451-d96657292934/09-airmail-opt-small.png" alt="Airmail rendering." width="500" height="326" /></a><figcaption>Airmail rendering. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/57120e8c-821a-4e1d-9af7-844ce3484002/09-airmail-opt.png">View large version</a>)</figcaption></figure>

### Apple Mail

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/aa33a0c7-fcc0-46db-92d1-df65095f8055/10-ios-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b4d18e7a-1e34-4b7b-83fc-bf2066790b1e/10-ios-opt-small.jpg" alt="Apple Mail rendering." width="338" height="600" /></a><figcaption>Apple Mail rendering. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/aa33a0c7-fcc0-46db-92d1-df65095f8055/10-ios-opt.jpg">View large version</a>)</figcaption></figure>

### Gmail (Browser)

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/97e3cfb9-3cc4-44f0-88d2-d5423812563b/11-gmail-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/542bcaf8-e0c0-484a-9908-5ee5c2cb72a1/11-gmail-opt-small.png" alt="Gmail rendering." width="500" height="313" /></a><figcaption>Gmail rendering. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/97e3cfb9-3cc4-44f0-88d2-d5423812563b/11-gmail-opt.png">View large version</a>)</figcaption></figure>

### Apple Mail on iOS

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6b9b474d-ca27-4d88-abd1-ece0f27f8ba5/12-mail-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f849a506-be82-4295-a98e-cd732bcbc601/12-mail-opt-small.png" alt="Apple Mail on iOS rendering." width="338" height="600" /></a><figcaption>Apple Mail on iOS rendering. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6b9b474d-ca27-4d88-abd1-ece0f27f8ba5/12-mail-opt.png">View large version</a>)</figcaption></figure>

The process of turning Lee’s template into a usable email took around 30 minutes, and I am pretty pleased with the result from such little input.

Of course, this process screams out for automation. For those who are interested, Lee has also posted about his <a href="https://www.leemunroe.com/email-design-workflow/">workflow for creating HTML email templates</a> and the toolkit he uses (Sketch, Sublime, Grunt, SCSS, Handlebars, GitHub, Mailgun, Litmus).</p>

## Taking It Further

The template produced above is admittedly quite basic and only scratches the surface of what is possible. We could do plenty more to customize our email for abandoned carts, such as:

*   consider tone of voice,
*   show product images to jog the customer’s memory,
*   add a discount code to encourage the user to return and buy,
*   add upsells,
*   list complementary products.</p>

### Dodo Case

Tone of voice is a key consideration and goes a long way to engaging the customer. <a href="https://www.dodocase.com/">Dodo Case</a> has a great example:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2956d94c-8b90-4f88-b463-c45ef7e4bd59/13-dodocase-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ee52a865-02dc-4be2-81eb-1c414b48f534/13-dodocase-opt-small.png" alt="Dodo Case’s email for abandoned carts." width="500" height="208" /></a><figcaption><a href="https://www.dodocase.com/">Dodo Case</a>’s email for abandoned carts. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2956d94c-8b90-4f88-b463-c45ef7e4bd59/13-dodocase-opt.png">View large version</a>)</figcaption></figure>

As always, context is very important when it comes to tone of voice. What’s right for Dodo Case might not be right for a company specializing in healthcare equipment.

Let’s review a few examples (taken from <a href="https://www.shopify.co.uk/blog/12522201-13-amazing-abandoned-cart-emails-and-what-you-can-learn-from-them">Shopify’s blog</a>) to get a taste of what other companies are doing.</p>

### Fab

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/697c940c-f923-4719-af24-e6561700025a/14-fab-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/78e0d337-d116-47b9-b87d-07542683c639/14-fab-opt-small.jpg" alt="Fab’s email for abandoned carts." width="500" height="534" /></a><figcaption><a href="https://www.fab.com">Fab</a>’s email for abandoned carts. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/697c940c-f923-4719-af24-e6561700025a/14-fab-opt.jpg">View large version</a>)</figcaption></figure>

While this email from <a href="https://www.fab.com">Fab</a> is pretty standard, the subject line is very attention-grabbing and is a big call to action.</p>

### Chubbies

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2f526480-0c6d-4388-8c65-1bb0b108660d/15-chubbies-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cc8bddd7-1c66-49ea-b90c-22b00ad7f3fa/15-chubbies-opt-small.jpg" alt="Chubbies’ email for abandoned carts." width="500" height="601" /></a><figcaption><a href="https://www.chubbiesshorts.com/">Chubbies</a>’ email for abandoned carts. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2f526480-0c6d-4388-8c65-1bb0b108660d/15-chubbies-opt.jpg">View large version</a>)</figcaption></figure>

The language and tone used in Chubbies’ email really stands out and is in line with the brand: fun-loving people. There’s also no shortage of links back to the cart, including the title, the main image and the call to action towards the bottom of the email.</p>

### Black Milk Clothing

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a6064638-8a1d-4389-965f-48483049d5d4/16-blackmilk-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fcb79b6d-280c-4cc9-9898-0db202b3d3e1/16-blackmilk-opt-small.jpg" alt="Black Milk’s email for abandoned carts." width="500" height="601" /></a><figcaption><a href="https://blackmilkclothing.com/">Black Milk</a>’s email for abandoned carts. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a6064638-8a1d-4389-965f-48483049d5d4/16-blackmilk-opt.jpg">View large version</a>)</figcaption></figure>

<a href="https://blackmilkclothing.com/">Black Milk Clothing</a> includes a dog photo and employs playful language, such as “Your shopping cart at Black Milk Clothing has let us know it’s been waiting a while for you to come back.”

### Holstee

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c28de67a-9440-44dc-a5a7-775b815b3f62/17-holstee-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/41e3abeb-7483-4b30-9b08-97b1375d0632/17-holstee-opt-small.png" alt="Holstee’s email for abandoned carts." width="500" height="495" /></a><figcaption><a href="https://holstee.com">Holstee</a>’s email for abandoned carts. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c28de67a-9440-44dc-a5a7-775b815b3f62/17-holstee-opt.png">View large version</a>)</figcaption></figure>

Finally, <a href="https://holstee.com">Holstee</a> asks if there’s a problem they can help with. It even goes so far as to include a direct phone number to its “Community Love Director.” Having worked with Holstee, I can confirm that this is a real position within the company!

## Conclusion

While there are many tactics to persuade customers to buy, inevitably some people will get to the payment screen and decide not to continue. Any tactic that helps to seal the deal is certainly worth considering, and given the small amount of work involved in implementing an email to recover abandoned carts, it’s a great place to start. Designers and developers are in a powerful position to help their clients increase their revenue, and being armed with tactics such as the ones outlined in this article will hopefully enable them to offer a wider range of services.</p>

### Further Reading

*   “[Retargeting Ads](https://appinstitute.com/retargeting-guide/),” A Beginner’s Guide that offers actionable steps to set up a successful retargeting campaign
*   “[Nine Case Studies and Infographics on Cart Abandonment and Email Retargeting](https://econsultancy.com/blog/63466-nine-case-studies-and-infographics-on-cart-abandonment-and-email-retargeting#i.weabnjzqdeyu10),” David Moth, Econsultancy
*   “[13 Best Practices for Email Cart Abandonment Programs](https://www.exacttarget.com/blog/13-best-practices-for-email-cart-abandonment-programs/),” Kyle Lacy, Salesforce Marketing Cloud Blog
*   “[Lost Sales Recovery, Part 2,: Crafting a Perfect Remarketing Message](https://blog.mageworx.com/2014/04/cart-abandonment-email/),” Vitaly Gonkov, The MageWorx Blog
*   “[Why Online Retailers Are Losing 67.45% of Sales and What to Do About It](https://www.shopify.co.uk/blog/8484093-why-online-retailers-are-losing-67-45-of-sales-and-what-to-do-about-it),” Mark Macdonald, Shopify Ecommerce Marketing Blog

{{< signature "al, ml" >}}

