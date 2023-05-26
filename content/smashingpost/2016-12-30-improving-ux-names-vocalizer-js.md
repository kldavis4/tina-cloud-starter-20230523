---
title: Improving The UX Of Names With Vocalizer.js
slug: improving-ux-names-vocalizer-js
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/70ef3da3-57ae-4566-9ddf-b556548e3c86/potential-usage-on-social-media-websites-preview-opt.jpg
date: 2016-12-30T19:09:18.000Z
author: atifazam
description: >-
  We have all encountered **names that are difficult to pronounce**. Having a
  challenging name myself, I get different pronunciations of my first name,
  Atif, all the time. In order to solve my own naming problem, I built a
  Javascript plugin called Vocalizer. In this article, I will introduce what
  Vocalizer is and a few different ways to use it.

  Earlier this year, I redesigned my portfolio website. During this process, I
  decided to add a feature that educated visitors on how to say my name. One
  day, I opened the "Voice Memos" app on my iPhone, tapped "Record", and asked
  my wife to say my first name. Then, I embedded a small button onto the landing
  page after my first name. Clicking on that button would play the audio file of
  my name.
categories:
  - UX
  - Inspiration
  - UX
---
We have all encountered <strong>names that are difficult to pronounce</strong>. Having a challenging name myself, I get different pronunciations of my first name, Atif, all the time. In order to solve my own naming problem, I built a Javascript plugin called Vocalizer. In this article, I will introduce what Vocalizer is and a few different ways to use it.</p>

## How It Started

Earlier this year, I redesigned my portfolio website. During this process, I decided to add a feature that educated visitors on how to say my name. One day, I opened the "Voice Memos" app on my iPhone, tapped "Record", and asked my wife to say my first name. Then, I embedded a small button onto the landing page after my first name. Clicking on that button would play the audio file of my name.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/73c75531-7eaf-4d7d-9628-768150682d33/the-audio-pronunciation-button-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e37c3651-24d1-49a1-8150-aaaa0fe21988/the-audio-pronunciation-button-preview-opt.jpg" alt="The audio pronunciation button that I added to my website." width="780" height="402" /></a><figcaption>The audio pronunciation button that I added to my website (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/73c75531-7eaf-4d7d-9628-768150682d33/the-audio-pronunciation-button-large-opt.jpg">Large preview</a>)</figcaption></figure>

After launching the website, I received a few emails and tweets calling out the audio feature. I even attended a few conferences and meetups where people pronounced my name the right way. A few people expressed interest in implementing the pronunciation feature on their own websites.

{{% feature-panel %}}

## <span class="rh">Further Reading</span> on SmashingMag: [Link](https://www.smashingmagazine.com/2014/01/lean-ux-manifesto-principle-driven-design/#further-reading-on-smashingmag)

*   [The Rainbow Spreadsheet: A Collaborative Lean UX Research Tool](https://www.smashingmagazine.com/2013/04/rainbow-spreadsheet-collaborative-ux-research-tool/)
*   [Lean UX: Getting Out Of The Deliverables Business](https://www.smashingmagazine.com/2011/03/lean-ux-getting-out-of-the-deliverables-business/)
*   [Becoming A Better Facilitator](https://www.smashingmagazine.com/2017/01/becoming-better-facilitator/)

Over the next few weeks, I spent time converting my singular implementation into a reusable plugin. Before publicly releasing it, I stumbled upon a company called &lt;ahref="https://www.nameshouts.com"&gt;NameShouts, which is an audio-based pronunciation tool with a repository of over 70,000 name pronunciations. I reached out to them for access to their API, implemented it into my plugin, and open-sourced it.</p>

## How To Use Vocalizer

Vocalizer is a simple, lightweight JavaScript plugin that facilitates the accessibility of difficult to pronounce names. If you're someone who is unsure of how to say a certain name, Vocalizer shows you how. Or, if you're someone with an unfamiliar name, Vocalizer shows others how to pronounce it.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/015b9645-abcf-4068-a308-3c6256678e8e/implementation-of-vocalizer-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b77f12aa-cf6a-48d0-a7f7-ecbeffa36af6/implementation-of-vocalizer-preview-opt.jpg" alt="A closer view of what an implementation of Vocalizer looks like." width="780" height="149" /></a><figcaption>A close-up view of what an implementation of Vocalizer looks like (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/015b9645-abcf-4068-a308-3c6256678e8e/implementation-of-vocalizer-large-opt.jpg">Large preview</a>)</figcaption></figure>

The benefit of using NameShouts' API is that it makes the implementation as quick as possible. In its simplest usage, there are only two steps required to add it to a website.

First, you must include the Javascript library before the closing <code>&lt;/body&gt;</code> tag within the code of your website:

<pre><code class="language-javascript">&lt;script type="text/javascript" src="https://cdnjs.cloudflare.com/ajax/libs/vocalizer/1.0.0/vocalizer.min.js"&gt;</code></pre>

Next, all you have to do is wrap your first name in a <code>&lt;span&gt;</code> tag with the specified attributes:

<pre><code class="language-javascript">&lt;span class="vocalizer" data-source="auto"&gt;NAME&lt;/span&gt;</code></pre>

<blockquote>Note: The latest version of Vocalizer.js is available on <a href="https://cdnjs.com/">CDNJS</a>, or you can choose to <a href="https://github.com/atifazam/vocalizer">download</a> and serve the files from your own server.</blockquote>

As you might have noticed, the <code>data-source</code> attribute is set to <code>auto</code> in the example above. This attribute determines the source of the audio file.

When <code>data-source</code> is set to <code>auto</code>, the library will use the NameShouts API. This option is completely hands-off. Vocalizer will automatically search NameShouts' name listing and feed in the audio file from their servers.

The alternative option is to manually record and use your own audio file instead of the API. In this scenario, the <code>data-source</code> attribute should be set to the path to your audio file. For example:

<pre><code class="language-markup">&lt;span class="vocalizer" data-source="assets/audio/daenerys.mp3"&gt;Daenerys&lt;/span&gt;</code></pre>

There's a chance that NameShouts' library does not have the pronunciation for your name, and in that event, you should use your own audio recording or Vocalizer won't be doing its job!

## How It Works

The actual source code for Vocalizer.js is about eighty lines of code. Let me explain exactly what's happening under the hood.

When the user wraps his or her name within the <code>&lt;span&gt;</code> tag with the class <code>vocalizer</code>, a Javascript function stores that name into a string:

<pre><code class="language-javascript">var name = document.getElementsByClassName('vocalizer');
var names = [];

for (var i = 0; i &lt; name.length; i++) {
  var data_source = name[i].getAttribute("data-source");
  names[i] = name[i].innerHTML.toLowerCase().replace(/\W/g,'')
  var request = buildRequests(names[i]);
  fetchAudio(data_source, request, i);
}</code>
</pre>

We perform this inside of a loop in case there are multiple usages of Vocalizer on the page.

Next, a conditional checks the <code>data-source</code> attribute to see if you're opting to use the NameShouts API to source the pronunciation or if you're using your own audio file:

<pre><code class="language-javascript">var data_source = name[i].getAttribute("data-source");

if (data_source == 'auto') {
  /* code for using NameShouts API */
}
else {
  /* code for using your own audio file */
}</code>
</pre>

The <code>buildRequest()</code> function that we call inside that loop returns the path for the endpoint based on the user's name.</p>

<pre><code class="language-javascript">function buildRequests(n) {
  return request = 'https://www.nameshouts.com/api/names/'+n;
} 
</code></pre>

From there, we pass the request to the <code>fetchAudio()</code> function and make our <code>xmlHttpRequest</code> to the NameShouts API.</p>

<pre><code class="language-javascript">var xhr = new XMLHttpRequest();
xhr.open('GET', request, true);
xhr.onload = function (e) {
  if (xhr.readyState === 4) {
      if (xhr.status === 200) {
        var audioPath = JSON.parse(xhr.responseText).message[names[i]][0]["path"];
        var audio = new Audio(BASE_URL+audioPath+'.mp3');
        audio.playbackRate = 0.75;
        name[i].addEventListener('click', function() {
          audio.play();
        }, false);
      } else {
        console.error(xhr.statusText);
      }
  }
}
xhr.onerror = function (e) {
  console.error(xhr.statusText);
};
xhr.send(null);
</code></pre>

NameShouts' API returns a JSON object that contains the name of the audio file corresponding to your name. From there, we combine NameShouts' base URL (where the audio files are stored) and the audio file's path.

In the event the name you are targeting does not exist within the NameShouts API, the plugin will throw an error.

A solution to this situation would be to record and link your own audio file. Setting the <code>data-source</code> attribute to a file path designates your own audio file. In that case, we just create an <code>Audio</code> element based on the file path from <code>data-source</code>:

<pre><code class="language-javascript">var audioPath = sourceType;
var btn = document.getElementsByClassName('vocalizer');

var audio = new Audio(audioPath, function() {
  'Error!';
});
</code></pre>

On the front end, an audio button appears after the targeted name. The cosmetics are added with CSS styles on the pseudo-element <code>:after</code> on the <code>&lt;span&gt;</code> tag.

Finally, we add a click event to the audio button:

<pre><code class="language-javascript">btn[i].addEventListener('click', function() {
  audio.play();
}, false);
</code></pre>

## Other Use Cases

### Example: Blogs and News Publications

Vocalizer's use case can extend beyond just personal websites. I can see blogs and digital news publications begin to adopt the plugin, as well.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/650e7dac-27c3-4fdf-b0d5-ca3822f6eb8c/example-of-how-vocalizer-could-be-used-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b91ab932-308c-48a2-8c3a-ae390a719aa0/example-of-how-vocalizer-could-be-used-780w-opt.jpeg" alt="An example of how Vocalizer could be used by news publications, such as Vox.com." width="780" height="503" /></a><figcaption>An example of how Vocalizer could be used by news publications, such as Vox.com (<a href="https://www.vox.com/">Image credit</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/650e7dac-27c3-4fdf-b0d5-ca3822f6eb8c/example-of-how-vocalizer-could-be-used-large-opt.jpg">Large preview</a>)</figcaption></figure>

Imagine you are browsing news stories on <a href="https://www.vox.com/">Vox.com</a> and you see the name of a political figure or a region of the world with a name in which you are unfamiliar. In that situation, Vocalizer could educate you on its pronunciation. In theory, this would better equip you to discuss these current events and issues. No one wants to sound uninformed.</p>

### Example: Social Media Platforms

Another hypothetical use case could be on social media websites. LinkedIn comes to mind for its role in facilitating professional connections.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/272cccca-ebf3-4c03-927c-0c2267dd7a8e/potential-usage-on-social-media-websites-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/70ef3da3-57ae-4566-9ddf-b556548e3c86/potential-usage-on-social-media-websites-preview-opt.jpg" alt="Potential usage on social media websites, such as LinkedIn." width="780" height="466" /></a><figcaption>Potential usage on social media websites, such as LinkedIn (Image credit: <a href="https://www.linkedin.com/">LinkedIn</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/272cccca-ebf3-4c03-927c-0c2267dd7a8e/potential-usage-on-social-media-websites-large-opt.jpg">Large preview</a>)</figcaption></figure>

In an age when people often connect with each other via social media platforms, such as Facebook, Twitter, or LinkedIn, prior to meeting — a tool like Vocalizer could prove useful.

Unbeknownst to me, Facebook recently rolled out a similar feature that automatically generates audio to enunciate names.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e750e37b-e49a-400e-923b-3a132df2ebf3/fb-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3ecfc8ca-5edc-4046-bbb5-8436d6933d45/fb-preview-opt.png" alt="Facebook's feature that displays the pronunciation of names" width="780" height="134" /></a><figcaption>Facebook's feature that displays the pronunciation of names (<a href="https://www.facebook.com/">Image credit</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e750e37b-e49a-400e-923b-3a132df2ebf3/fb-large-opt.png">Large preview</a>)</figcaption></figure>

It's nice to see mainstream platforms focus on these types of accessibility features. Unfortunately, there is no guarantee that autogenerated playback will be correct. Facebook's pronunciation tool mangles my last name.</p>

## Challenges

With every potential solution, there are problems. Vocalizer faces issues of its own. The main issue is that two people with the same name do not always pronounce their name in the same way.

Often, a person's origin language dictates the pronunciation of their name. For example, the name José in Spanish is pronounced HOH-SEH. In French, the same name is pronounced JOO-ZE. Vocalizer's current implementation does not cater to these circumstances unless you opt to use a custom recording.</p>

## Pushing Accessibility Further

In the last few years, web evangelists have emphasized the importance of web accessibility. Most accessibility functions cater to people with physical and cognitive disabilities. I believe there is a lack of attention in regards to inclusion and cross-cultural accessibility.

Though unintentional, in a way, <strong>Vocalizer seeks to enable cultural accessibility</strong>. Technology companies continually strive to diversify their workforces. We're seeing heightened mobility in our professional lives. As a result, multiculturalism is becoming more and more prevalent.

For what it is — I hope Vocalizer helps familiarize people with names from other cultures or ethnicities.</p>

## The Future Of Vocalizer

There are a few features and improvements I would like to make on future versions of Vocalizer.js:

*   Language support for names with alternate pronunciations
*   More graceful handling of implementation errors
*   Adding a fallback for the situations when a name is not in NameShouts' API
*   Ability to easily customize audio buttons styles

To further expand on the idea, I launched a free, web-based version of Vocalizer at <a href="https://www.vocalizer.io">Vocalizer.io.</a>

The web tool allows you to record your name in the browser. Then, it generates the code snippet required to add Vocalizer to your website.</p>

## Conclusion

A <a href="https://news.uci.edu/press-releases/uc-irvine-led-study-finds-truthiness-in-peoples-names/"> 2014 study</a> found that people with easier-to-pronounce names are deemed "more trustworthy". I built Vocalizer to solve a problem that has persisted all my life. Now, I hope this will prove useful to others, helping them solve the same problem.

Thanks so much for reading! Please don't hesitate to <a href="https://www.twitter.com/atifazm">tweet to me</a> if you have any questions, comments or feedback.

{{< signature "vf, aa, il" >}}

