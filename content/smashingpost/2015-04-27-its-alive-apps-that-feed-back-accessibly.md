---
title: '"It’s Alive!": Apps That Feed Back Accessibly'
slug: its-alive-apps-that-feed-back-accessibly
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d3b93001-5981-429b-b497-da25578d4f66/loading-css-circle-illu-opt.jpg
date: 2015-04-27T20:58:30.000Z
author: heydon-pickering
description: >-
  _It's one thing to create a web application and quite another to create an
  accessible web application. That's why Heydon Pickering, both author and
  editor at Smashing Magazine, wrote an eBook [Apps For All: Coding Accessible
  Web
  Applications](https://shop.smashingmagazine.com/apps-for-all-coding-accessible-web-applications.html),
  outlining the roadmap for the accessible applications we should all be
  making._

  Picture the scene: it’s a day like any other and you’re at your desk, enclosed
  in a semicircular bank of monitors that make up your extended desktop,
  intently cranking out enterprise-level CSS for MegaDigiSpaceHub Ltd. You are
  one of many talented front-end developers who share this floor in your plush
  London office.

  You don’t know it, but a fire has broken out on the floor below you due to a
  “mobile strategist” spontaneously combusting. Since no expense was spared on
  furnishing the office with adorable postmodern ornaments, no budget remained
  for installing a fire alarm system. It is up to the floor manager in question
  to travel throughout the office, warning individual departments in person.
categories:
  - Coding
  - Mobile
  - Responsive Design
  - Accessibility
  - Smashing eBooks
---
<em>It's one thing to create a web application and quite another to create an accessible web application. That's why <a href="https://twitter.com/heydonworks">Heydon Pickering</a>, both author and editor at Smashing Magazine, wrote an eBook <a href="https://shop.smashingmagazine.com/apps-for-all-coding-accessible-web-applications.html">Apps For All: Coding Accessible Web Applications</a>, outlining the roadmap for the accessible applications we should all be making.</em>

<em>The following is an extract from the chapter "It's Alive" from Heydon's book, which explores how to use <abbr title="Accessible Rich Internet Applications">ARIA</abbr> live regions. Javascript applications are driven by events and the user should be informed of what important events are happening in the interface. Live regions help us provide accessible messaging systems, keeping users informed of events in a way that is compatible with assistive technologies.</em>

## Getting The Message

Picture the scene: it’s a day like any other and you’re at your desk, enclosed in a semicircular bank of monitors that make up your extended desktop, intently cranking out enterprise-level CSS for MegaDigiSpaceHub Ltd. You are one of many talented front-end developers who share this floor in your plush London office.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [The WAI Forward](https://www.smashingmagazine.com/2014/07/the-wai-forward/)
*   [Notes On Client-Rendered Accessibility](https://www.smashingmagazine.com/2015/05/client-rendered-accessibility/)
*   [Accessibility: Improving The UX For Color-Blind Users](https://www.smashingmagazine.com/2016/06/improving-ux-for-color-blind-users/)
*   [Making Accessibility Simpler, With Ally.js](https://www.smashingmagazine.com/2015/12/making-accessibility-simpler/)
*   [Inclusive Front-End Design Patterns, A New Smashing Book](https://www.smashingmagazine.com/inclusive-design-patterns/)

{{% feature-panel %}}

You don’t know it, but a fire has broken out on the floor below you due to a “mobile strategist” spontaneously combusting. Since no expense was spared on furnishing the office with adorable postmodern ornaments, no budget remained for installing a fire alarm system. It is up to the floor manager in question to travel throughout the office, warning individual departments in person.

He does this by walking silently into each room, holding a business card aloft with the word “fire” written on it in 12pt Arial for a total of three seconds, then leaving. You and the other developers — ensconced behind your monitors — have no idea he even visited the room.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/01e385ec-91f4-4b2a-96ec-23cfe01d1c60/alive-monitors-opt.jpg" alt="Three monitors for coding" /><br>
<figcaption>Three monitors for coding</figcaption></figure>

What I cover in my eBook is, for the most part, about making using your websites and applications accessible. That is, we’re concerned with everyone being able to do things with them easily. However, it is important to acknowledge that when something is done (or simply happens), something else will probably happen as a result: there are actions and reactions.
<blockquote>"When one body exerts a force on a second body, the second body simultaneously exerts a force equal in magnitude and opposite in direction to that of the first body."

– Newton’s third law of motion <a href="https://en.wikipedia.org/wiki/Newton%27s_laws_of_motion">(Newton’s laws of motion, Wikipedia</a>)</blockquote>

Providing feedback to users, to confirm the course they’ve taken, address the result of a calculation they’ve made or to insert helpful commentary of all sorts, is <strong>an important part of application design</strong>. The problem which needs to be addressed is that interrupting a user visually, by making a message appear on screen, is a silent occurrence. It is also one which — in the case of dialogs — often involves the activation of an element that originates from a completely remote part of the document, many DOM nodes away from the user’s location of focus.

To address these issues and to ensure users (unlike the poor developers in the introductory story) get the message, ARIA provides <a href="https://developer.mozilla.org/en-US/docs/Accessibility/ARIA/ARIA_Live_Regions">live regions</a>. As their name suggests, live regions are elements whose contents may change in the course of the application’s use. They are living things, so don’t always stand still. By adorning them with the appropriate ARIA attributes, these regions will interrupt the user to announce their changes as they happen.

In the following example, we will look at how to alert users to changes which they <em>didn’t</em> ask for, but — like the building being on fire — really ought to know about anyway.</p>

## Alert!

Perhaps the only thing worse than a fire that could happen to the office of a web development company would be losing connectivity to the web. Certainly, if I was working using an online application, I’d like to know the application will no longer behave in the way I expect and perhaps store my data properly. This is why Google Mail inserts a warning whenever you go offline. As noted in <a href="https://www.marcozehe.de/2008/08/04/aria-in-gmail-1-alerts/">Marco Zehe’s 2008 blog post</a>, Google was an early adopter of ARIA live regions.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/15507404-315c-42fe-9cb5-c8e85c5cf1a8/alive-gmail-opt.jpg" alt="Yellow box reads unable to reach G mail please check your internet connection" /><br>
<figcaption>Yellow box reads unable to reach G mail please check your internet connection.</figcaption></figure>

We are going to create a script which tests whether the user is online or off and uses ARIA to warn screen reader users of the change in this status so they know whether it’s worth staying at their desk or giving up and going for a beer.

### The Setup

For live regions, ARIA provides a number of values for both the <code>role</code> and <code>aria-live</code> attributes. This can be confusing because there is some crossover between the two and some screen readers only support either the <code>role</code> or <code>aria-live</code> alternatives. It’s OK, there are ways around this.

At the most basic level, there are two common types of message:

1.  “This is pretty important but I’m going to wait and tell you when you’re done doing whatever it is you’re doing.”
2.  “Drop everything! You need to know this now or we’re all in big trouble. AAAAAAAAAAGHH!”

Mapped to the respective <code>role</code> and <code>aria-live</code> attributes, these common types are written as follows:

1.  “This is pretty important but I’m going to wait and tell you when you’re done doing whatever it is you’re doing.” (`aria-live="polite"` or `role="status"`)
2.  “Drop everything! You need to know this now or we’re all in big trouble. AAAAAAAAAAGHH.” (`aria-live="assertive"` or `role="alert"`)

When marking up our own live region, we’re going to maximize compatibility by putting both of the equivalent attributes and values in place. This is because, unfortunately, some user agents do not support one or other of the equivalent attributes. More detailed information on <a href="https://developer.mozilla.org/en-US/docs/Accessibility/ARIA/ARIA_Live_Regions">maximizing compatibility</a> of live regions is available from Mozilla.

Since losing internet connectivity is a major disaster, we’re going to use the more aggressive form.</p>

<pre><code class=" language-markup"><span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>div</span> <span class="token attr-name">id</span><span class="token attr-value"><span class="token punctuation">=</span>"message"</span> <span class="token attr-name">role</span><span class="token attr-value"><span class="token punctuation">=</span>"alert"</span> <span class="token attr-name">aria-live</span><span class="token attr-value"><span class="token punctuation">=</span>"assertive"</span> <span class="token attr-name">class</span><span class="token attr-value"><span class="token punctuation">=</span>"online"</span><span class="token punctuation">&gt;</span></span>
    <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>p</span><span class="token punctuation">&gt;</span></span>You are online.<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>p</span><span class="token punctuation">&gt;</span></span>
<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>div</span><span class="token punctuation">&gt;</span></span></code></pre>

The code above doesn’t alert in any way by itself — the contents of the live region would have to dynamically change for that to take place. The script below will run a check to see if it can load <em>test_resource.html</em> every three seconds. If it fails to load it, or it has failed to load it but has subsequently succeeded, it will update the live region’s <code>class</code> value and change the wording of the paragraph. If you go offline unexpectedly, it will display <code>&lt;p&gt;There’s no internets. Time to go to the pub!&lt;/p&gt;</code>.

The change will cause the contents of that <code>#message</code> live region to be announced, abruptly interrupting whatever else is currently being read on the page.</p>

<pre><code class=" language-javascript"><span class="token comment">// Function to run when going offline
</span>
<span class="token keyword">var</span> offline <span class="token operator">=</span> <span class="token keyword">function</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
  <span class="token keyword">if</span> <span class="token punctuation">(</span><span class="token operator">!</span>$<span class="token punctuation">(</span><span class="token string">'#message'</span><span class="token punctuation">)</span><span class="token punctuation">.</span>hasClass<span class="token punctuation">(</span><span class="token string">'offline'</span><span class="token punctuation">)</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
    $<span class="token punctuation">(</span><span class="token string">'#message'</span><span class="token punctuation">)</span><span class="token comment"> // the element with [role="alert"] and
    [aria-live="assertive"]
</span>      <span class="token punctuation">.</span>attr<span class="token punctuation">(</span><span class="token string">'class'</span><span class="token punctuation">,</span> <span class="token string">'offline'</span><span class="token punctuation">)</span>
      <span class="token punctuation">.</span>text<span class="token punctuation">(</span><span class="token string">'There\'s no internets. Go to the pub!'</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
  <span class="token punctuation">}</span>
<span class="token punctuation">}</span>
<span class="token comment">
// Function to run when back online
</span>
<span class="token keyword">var</span> online <span class="token operator">=</span> <span class="token keyword">function</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
  <span class="token keyword">if</span> <span class="token punctuation">(</span><span class="token operator">!</span>$<span class="token punctuation">(</span><span class="token string">'#message'</span><span class="token punctuation">)</span><span class="token punctuation">.</span>hasClass<span class="token punctuation">(</span><span class="token string">'online'</span><span class="token punctuation">)</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
    $<span class="token punctuation">(</span><span class="token string">'#message'</span><span class="token punctuation">)</span><span class="token comment"> // the element with [role="alert"] and
    [aria-live="assertive"]
</span>      <span class="token punctuation">.</span>attr<span class="token punctuation">(</span><span class="token string">'class'</span><span class="token punctuation">,</span> <span class="token string">'online'</span><span class="token punctuation">)</span>
      <span class="token punctuation">.</span>text<span class="token punctuation">(</span><span class="token string">'You are online.'</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
  <span class="token punctuation">}</span>
<span class="token punctuation">}</span>
<span class="token comment">
// Test by trying to poll a file
</span><br>
<span class="token keyword">function</span> testConnection<span class="token punctuation">(</span>url<span class="token punctuation">)</span> <span class="token punctuation">{</span>
    <span class="token keyword">var</span> xmlhttp <span class="token operator">=</span> <span class="token keyword">new</span> XMLHttpRequest<span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
    xmlhttp<span class="token punctuation">.</span>onload <span class="token operator">=</span> <span class="token keyword">function</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
      online<span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
    <span class="token punctuation">}</span>
    xmlhttp<span class="token punctuation">.</span>onerror <span class="token operator">=</span> <span class="token keyword">function</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
      offline<span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
    <span class="token punctuation">}</span>
    xmlhttp<span class="token punctuation">.</span>open<span class="token punctuation">(</span><span class="token string">"GET"</span><span class="token punctuation">,</span>url<span class="token punctuation">,</span><span class="token boolean">true</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
    xmlhttp<span class="token punctuation">.</span>send<span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token punctuation">}</span>
<span class="token comment">
// Loop the test every three seconds for "test_resource.html"
</span><br>
<span class="token keyword">function</span> start<span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
  rand <span class="token operator">=</span> Math<span class="token punctuation">.</span>floor<span class="token punctuation">(</span>Math<span class="token punctuation">.</span>random<span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token operator">*</span><span class="token number">90000</span><span class="token punctuation">)</span> <span class="token operator">+</span> <span class="token number">10000</span><span class="token punctuation">;</span>
  testConnection<span class="token punctuation">(</span><span class="token string">'test_resource.html?fresh='</span> <span class="token operator">+</span> rand<span class="token punctuation">)</span><span class="token punctuation">;</span>
  setTimeout<span class="token punctuation">(</span>start<span class="token punctuation">,</span> <span class="token number">3000</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token punctuation">}</span>
<span class="token comment">
// Start the first test
</span>
start<span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span></code></pre>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7f44129e-c06f-4a36-9491-d7be695f8196/alive-no-internets-opt.jpg" alt="Alert reads alert there’s no internets. Go to the pub." /><br>
<figcaption>Alert reads "Alert: there’s no internets. Go to the pub!"</figcaption></figure>

There are more comprehensive ways to test to see if your application is online or not, including a dedicated script called <a href="https://github.hubspot.com/offline/docs/welcome/">offline.js</a>, but this little one is included for context. Note that some screen readers will prefix the announcement with “Alert!”, so you probably don’t want to include “Alert!” in the actual text as well, unless it’s really, <em>really</em> important information.

There is a <a href="https://heydonworks.com/practical_aria_examples/#offline-alert">demo of this example</a> available.</p>

### test.css

We would like to maximize compatibility of live regions across browsers and assistive technologies. We can add a rule in our <em>test.css</em> to make sure equivalent attributes are all present like so:

<pre><code class=" language-javascript"><span class="token punctuation">[</span>role<span class="token operator">=</span><span class="token string">"status"</span><span class="token punctuation">]</span><span class="token punctuation">:</span>not<span class="token punctuation">(</span><span class="token punctuation">[</span>aria<span class="token operator">-</span>live<span class="token operator">=</span><span class="token string">"polite"</span><span class="token punctuation">]</span><span class="token punctuation">)</span><span class="token punctuation">,</span> 
<span class="token punctuation">[</span>role<span class="token operator">=</span><span class="token string">"alert"</span><span class="token punctuation">]</span><span class="token punctuation">:</span>not<span class="token punctuation">(</span><span class="token punctuation">[</span>aria<span class="token operator">-</span>live<span class="token operator">=</span><span class="token string">"assertive"</span><span class="token punctuation">]</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
	content<span class="token punctuation">:</span> 'Warning: For better support, you should include
	a politeness setting for your live region role using the
	aria-live attribute'<span class="token punctuation">;</span>
<span class="token punctuation">}</span>

<span class="token punctuation">[</span>aria<span class="token operator">-</span>live<span class="token operator">=</span><span class="token string">"polite"</span><span class="token punctuation">]</span><span class="token punctuation">:</span>not<span class="token punctuation">(</span><span class="token punctuation">[</span>role<span class="token operator">=</span><span class="token string">"status"</span><span class="token punctuation">]</span><span class="token punctuation">)</span><span class="token punctuation">,</span> 
<span class="token punctuation">[</span>aria<span class="token operator">-</span>live<span class="token operator">=</span><span class="token string">"assertive"</span><span class="token punctuation">]</span><span class="token punctuation">:</span>not<span class="token punctuation">(</span><span class="token punctuation">[</span>role<span class="token operator">=</span><span class="token string">"alert"</span><span class="token punctuation">]</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
	content<span class="token punctuation">:</span> 'Warning: For better support, you should
	include a corresponding role for your aria-live
	politeness setting'<span class="token punctuation">;</span>
<span class="token punctuation">}</span></code></pre>

## I Want The Whole Story

<blockquote>"Taken out of context, I must seem so strange."

– Fire Door by Ani DiFranco</blockquote>

By default, when the contents of a live region alter, only the nodes (HTML elements, to you and me) which have actually changed are announced. This is helpful behavior in most situations because you don’t want a huge amount of content reread to you just because a tiny part of it is different. In fact, if it’s all read out at once, how would you tell which part had changed? It would be like the memory tray game where you have to memorize the contents of a tray to recall which things were removed.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/32472c32-271b-464c-8e7c-c1e2eb937b6d/alive-memory-opt.jpg" alt="Tray full of bits of HTML" /><br>
<figcaption>Tray full of bits of HTML</figcaption></figure>

In some cases, however, a bit of context is desirable for clarification. This is where the <code>aria-atomic</code> attribute comes in. With no
<code>aria-atomic</code> set, or with an <code>aria-atomic</code> value of <code>false</code>, only the elements which have actually changed will be notified to the user. When <code>aria-atomic</code> is set to <code>true</code>, all of the contents of the element with <code>aria-atomic</code> set on it will be read.

The term <em>atomic</em> is a little confusing. To be <code>true</code> means to treat the contents of this element as one, indivisible thing (an atom), not to smash the element into little pieces (atoms). Whether or not you think atomic is a good piece of terminology, <strong>the expected behavior is what counts</strong> and it is the first of the two behaviors which is defined.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/eece4d02-92f9-4e30-98a8-ad09decde1ba/alive-atomic-opt.jpg" alt="One atom compared to lots of atoms" /><br>
<figcaption>One atom compared to lots of atoms</figcaption></figure>

Gez Lemon offers a <a href="https://juicystudio.com/article/wai-aria_live-regions_updated.php">great example of <code>aria-atomic</code></a>. In his example, we imagine an embedded music player which tells users what the currently playing track is, whenever it changes.</p>

<pre><code class=" language-markup"><span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>div</span> <span class="token attr-name">aria-live</span><span class="token attr-value"><span class="token punctuation">=</span>"polite"</span> <span class="token attr-name">role</span><span class="token attr-value"><span class="token punctuation">=</span>"status"</span> <span class="token attr-name">aria-atomic</span><span class="token attr-value"><span class="token punctuation">=</span>"true"</span><span class="token punctuation">&gt;</span></span>
  <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>h3</span><span class="token punctuation">&gt;</span></span>Currently playing:<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>h3</span><span class="token punctuation">&gt;</span></span>
  <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>p</span><span class="token punctuation">&gt;</span></span>Jake Bugg — Lightning Bolt<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>p</span><span class="token punctuation">&gt;</span></span>
<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>div</span><span class="token punctuation">&gt;</span></span></code></pre>

Even though only the name of the artist and song within the paragraph will change, because <code>aria-atomic</code> is set to <code>true</code> the whole region will be read out each time: “Currently playing: Jake Bugg — Lightning Bolt”. The “Currently playing” prefix is important for context.

Note that the politeness setting of the live region is <code>polite</code> not
<code>assertive</code> as in the previous example. If the user is busy reading something else or typing, the notification will wait until they have stopped. It isn’t important enough to interrupt the user, not least because it’s their playlist: they might recognize all the songs anyway.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3f132a99-787b-4d59-af16-2498239c1d5b/alive-jake-opt.jpg" alt="Box showing a graphic equalizer which reads currently playing, Jake bug lightning bolt" /><br>
<figcaption>Box showing a graphic equalizer which reads currently playing, Jake bug lightning bolt</figcaption></figure>

The <code>aria-atomic</code> attribute doesn’t have to be used on the same element that defines the live region, as in Lemon’s example. In fact, you could use <code>aria-atomic</code> on separate child elements within the same region. According to the specification:
<blockquote>"When the content of a live region changes, user agents <strong>SHOULD</strong> examine the changed element and traverse the ancestors to find the first element with <code>aria-atomic</code> set, and apply the appropriate behavior."

– <a href="https://www.w3.org/TR/wai-aria/states_and_properties#aria-atomic">Supported States and Properties</a></blockquote>

This means we could also include another block within our live region to tell users which track is coming up next.</p>

<pre><code class=" language-markup"><span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>div</span> <span class="token attr-name">aria-live</span><span class="token attr-value"><span class="token punctuation">=</span>"polite"</span> <span class="token attr-name">role</span><span class="token attr-value"><span class="token punctuation">=</span>"status"</span><span class="token punctuation">&gt;</span></span>

   <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>div</span> <span class="token attr-name">aria-atomic</span><span class="token attr-value"><span class="token punctuation">=</span>"true"</span><span class="token punctuation">&gt;</span></span>
     <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>h3</span><span class="token punctuation">&gt;</span></span>Currently playing:<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>h3</span><span class="token punctuation">&gt;</span></span>
     <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>p</span><span class="token punctuation">&gt;</span></span>Jake Bugg — Lightning Bolt<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>p</span><span class="token punctuation">&gt;</span></span>
   <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>div</span><span class="token punctuation">&gt;</span></span>

   <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>div</span> <span class="token attr-name">aria-atomic</span><span class="token attr-value"><span class="token punctuation">=</span>"true"</span><span class="token punctuation">&gt;</span></span>
     <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>h3</span><span class="token punctuation">&gt;</span></span>Next in queue:<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>h3</span><span class="token punctuation">&gt;</span></span>
     <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>p</span><span class="token punctuation">&gt;</span></span>Napalm Death — You Suffer<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>p</span><span class="token punctuation">&gt;</span></span>
   <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>div</span><span class="token punctuation">&gt;</span></span>

<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>div</span><span class="token punctuation">&gt;</span></span></code></pre>

Now, when Jake Bugg’s Lightning Bolt is nearing an end, we update the <code>&lt;p&gt;</code> within the next in queue block to warn users that Napalm Death are ready to take the mic: “Next in queue: Napalm Death — You Suffer”. As Napalm Death begin to play, the currently playing block also updates with their credentials and at the next available juncture the user is reminded that the noise they are being subjected to is indeed Napalm Death.</p>

### aria-busy

I was a bit mischievous using Napalm Death’s You Suffer as an example track because, at 1.316 seconds long, the world’s shortest recorded song would have ended before the live region could finish telling you it had started! If every track was that short, the application would go haywire.

In cases where lots of complex changes to a live region must take place before the result would be understandable to the user, you can include the <a href="https://www.w3.org/TR/wai-aria/states_and_properties#aria-busy"><code>aria-busy</code> attribute</a>. You simply set this to <code>true</code> while the region is busy updating and back to <code>false</code> when it’s done. It’s effectively the equivalent of a loading spinner used when loading assets in JavaScript applications.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/67a13a73-de2b-4618-aa8a-03305d3a295f/alive-busy-opt.jpg" alt="Typical loading spinner labelled ARIA atomic true" /><br>
<figcaption>Typical loading spinner labelled ARIA atomic true</figcaption></figure>

Usually you set <code>aria-busy="true"</code> before the first element (or addition) in the live region is loaded or altered, and <code>false</code> when the last expected element has been dealt with. In the case of our music player example, we’d probably want to set a timeout of ten seconds or so, making sure only music tracks longer than the announcement of those tracks get announced.</p>

<pre><code class=" language-javascript">$<span class="token punctuation">(</span><span class="token string">'#music-info'</span><span class="token punctuation">)</span><span class="token punctuation">.</span>attr<span class="token punctuation">(</span><span class="token string">'aria-busy'</span><span class="token punctuation">,</span> <span class="token string">'true'</span><span class="token punctuation">)</span><span class="token punctuation">;</span>

<span class="token comment">// Update the song artist &amp; title here, then...
</span>
setTimeout<span class="token punctuation">(</span><span class="token keyword">function</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
   $<span class="token punctuation">(</span><span class="token string">'#music-info'</span><span class="token punctuation">)</span><span class="token punctuation">.</span>attr<span class="token punctuation">(</span><span class="token string">'aria-busy'</span><span class="token punctuation">,</span> <span class="token string">'false'</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token punctuation">}</span><span class="token punctuation">,</span> <span class="token number">10000</span><span class="token punctuation">)</span><span class="token punctuation">;</span></code></pre>

### Buy The eBook

That concludes your extract from "It's Alive!", a chapter which goes on to explore the intricacies of designing accessible web-based dialogs. But that's not all. There's plenty more about creating accessible experiences in the book, from basic button control design to ARIA tab interfaces and beyond. Reviews for the eBook and purchasing options are available <a href="https://shop.smashingmagazine.com/apps-for-all-coding-accessible-web-applications.html">here</a>. The inimitable <a href="https://www.brucelawson.co.uk/2014/apps-for-all-coding-accessible-web-applications-book-review/">Bruce Lawson has written a lovely post</a> about it, too.

