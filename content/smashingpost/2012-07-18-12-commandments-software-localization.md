---
title: 12 Commandments Of Software Localization
slug: 12-commandments-software-localization
image: null
date: 2012-07-18T11:07:36.000Z
author: zack-grossbart
description: >-
  You've presented the new website and everyone loves it. The design is crisp,
  the code is bug-free, and you're ready to release. Then someone asks, “Does it
  work in Japanese?”

  You break out in a cold sweat: you have no idea. The website works in English,
  and you figured other languages would come later. Now you have to rework the
  whole app to support other languages. Your release date slips, and you spend
  the next two months fixing bugs, only to find that you’ve missed half of them.
categories:
  - Coding
  - Localization
---
You've presented the new website and everyone loves it. The design is crisp, the code is bug-free, and you're ready to release. Then someone asks, “Does it work in <a title="Japanese, A Beautifully Complex Writing System" href="https://www.smashingmagazine.com/2012/03/japanese-a-beautifully-complex-writing-system/">Japanese</a>?”

You break out in a cold sweat: you have no idea. The website works in English, and you figured other languages would come later. Now you have to rework the whole app to support other languages. Your release date slips, and you spend the next two months fixing bugs, only to find that you’ve missed half of them.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [CSS-Driven Internationalization In JavaScript](https://www.smashingmagazine.com/2014/06/css-driven-internationalization-in-javascript/)
*   [<span class="headline">Should You Ask The User Or Their Browser?</span>](https://www.smashingmagazine.com/2012/07/12-commandments-software-localization/)
*   [How To Conduct Website Localization](https://www.smashingmagazine.com/2014/12/how-to-conduct-website-localization/)

Localization makes your application ready to work in any language — and it's much easier if you do it from the beginning. Just follow these 12 simple rules and you'll be ready to run anywhere in the world.

{{% feature-panel %}}

## 1\. “Resource” All Of Your Strings

The first step of localization is to get user-visible strings out of your code and into resource files. Those strings include titles, product names, error messages, strings in images and any other text the user might see.

Most resource files work by giving each string a name and allowing you to specify different translation values for that string. Many languages use properties files like this:

<pre><code class="language-javascript">
name = Username
</code></pre>

Or they use <a href="https://en.wikipedia.org/wiki/GNU_gettext"><code>.pot</code> files</a> like this:

<pre><code class="language-javascript">
msgid "Username"
msgstr "Nom d'utilisateur"
</code></pre>

Or they use <a href="https://en.wikipedia.org/wiki/Xliff">XLIFF</a> files like this:

<pre><code class="language-markup tmp-xml">&lt;trans-unit id="1"&gt;
 &lt;source xml:lang="en"&gt;Username&lt;/source&gt;
 &lt;target xml:lang="fr"&gt;Nom d'utilisateur&lt;/target&gt;
&lt;/trans-unit&gt;</code></pre>

The resource files are then loaded by a library that uses a combination of the language and country, known as the <a href="https://en.wikipedia.org/wiki/Locale">locale</a>, to identify the right string.

Once you've placed your strings in external resource files, you can send the files to translators and get back translated files for each locale that your application supports.</p>

## 2\. Never Concatenate Strings

Appending one string to another almost always results in a localization bug. It's easy to see this with modifiers such as <code>color</code>.

Suppose your stationery store has items such as pencils, pens and sheets of paper. Shoppers will choose what they want and then select a color. In the shopping cart you would show them items such as a red pencil or a blue pen with a function like this:

<pre><code class="language-javascript">function getDescription() {
    var color = getColor();
    var item = getItem();

    return color + " " + item;
}</code></pre>

This code works well in English, in which the color comes first, but it breaks in French, in which “red pencil” translates as “crayon rouge” and “blue pen” is “stylo – encre bleue.” French speakers (but not only them) put modifiers after the words they modify. The <code>getDescription</code> function would never be able to support languages like this with simple string concatenation.

The solution is to specify parametrized strings that change the order of the item and color for each language. Define a resourced string that looks like this:

<pre><code class="language-javascript">
itemDescription = {0} {1}
</code></pre>

It might not look like much, but this string makes the translation possible. We can use it in a new <code>getDescription</code> function, like this:

<pre><code class="language-javascript">function getDescription() {
    var color = getColor();
    var item = getItem();

    return getLocalizedString('itemDescription', color, item);
}</code></pre>

Now, your translators can easily switch the order, like this:

<pre><code class="language-javascript">
itemDescription = {1} {0}
</code></pre>

The <code>getLocalizedString</code> function here takes the name of a resource string (<code>itemDescription</code>) and some additional parameters (color and item) to substitute for placeholders in the resource string. Most programming languages provide a function similar to <code>getLocalizedString</code>. (The one notable exception is JavaScript, but we'll talk more about that later.)

This method also works for strings with text in them, like:

<pre><code class="language-javascript">
invalidUser = The username {0} is already taken. Please choose another one.
</code></pre>

## 3\. Put All Of Your Punctuation In The Resourced String

Tacking on punctuation later is often tempting, so that you can reuse the same string, say, in a label where it needs a colon and in a tooltip where it doesn't. But this is another example of bad string concatenation.

Here, we're adding a simple log-in form using PHP in a WordPress environment:

<pre><code class="language-php">&lt;form&gt;
&lt;p&gt;Username: &lt;input type="text" name="username"&gt;&lt;/p&gt;
&lt;p&gt;Password: &lt;input type="text" name="password"&gt;&lt;/p&gt;
&lt;/form&gt;</code></pre>

We want the form to work in other languages, so let’s add the strings for localization. WordPress makes this easy with the <a href="https://codex.wordpress.org/Function_Reference/_2"><code>__</code></a> function (i.e. underscore underscore):

<pre><code class="language-php">&lt;form&gt;
&lt;p&gt;&lt;?php echo(__('Username', 'my-plugin')) ?&gt;: &lt;input type="text" name="username"&gt;&lt;/p&gt;
&lt;p&gt;&lt;?php echo(__('Password', 'my-plugin')) ?&gt;: &lt;input type="text" name="password"&gt;&lt;/p&gt;
&lt;/form&gt;</code></pre>

Spot the bug? This is another case of string concatenation. The colon after the labels isn't localized. This will look wrong in a language like French, which always puts spaces around colons. Punctuation is part of the string and belongs in the resource file.

<pre><code class="language-php">&lt;form&gt;
&lt;p&gt;&lt;?php echo(__('Username:', 'my-plugin')) ?&gt; &lt;input type="text" name="username"&gt;&lt;/p&gt;
&lt;p&gt;&lt;?php echo(__('Password:', 'my-plugin')) ?&gt; &lt;input type="text" name="password"&gt;&lt;/p&gt;
&lt;/form&gt;</code></pre>

Now the form can use <code>Username:</code> in English and <code>Nom d'utilisateur :</code> in French.</p>

## 4\. “First” Names Sometimes Aren't

My name is Zack Grossbart. Zack is my given (or first) name, and Grossbart is my last (or family) name. Everyone in my family is named Grossbart, but I'm the only Zack.

In English-speaking countries, the first name is the given name and the last name is the family name. Most Asian countries go the other way, and some cultures have only one name.

The cellist Yo-Yo Ma is a member of the Ma family. In Chinese, he writes his family name first: Ma Yo-Yo (馬友友).

This gets tricky because many people change their names when moving from Asian countries to English-speaking ones. They often switch the order to fit local customs, so you can't make any assumptions.

You must provide a way to customize the presentation of names; you can't assume that the first name always comes first or that the last name always comes last.

WordPress handles this pretty well by asking you how you want your name to show up:

<img class="aligncenter size-full wp-image-120598" title="Name formatting in WordPress" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c4ba2a13-5759-4578-a5ab-a6f90b4086ca/name-format2.png" alt="Name formatting in WordPress" width="547" height="232" />

It would be even better if WordPress supported a middle name and a way to specify the format per locale so that you could make your name one way in English and another in Chinese, but nothing’s perfect.</p>

## 5\. Never Hard-Code Date, Time Or Currency Formats

The whole world is inconsistent about date and time formats. Some people put the month first (6/21/2012), others the day first (21/6/2012). Some use 24-hour (14:00) time, and some use 12 (2:00 PM). Taiwan uses specially translated strings instead of AM and PM, and those come first (上午 2:00).

Your best bet is to store all dates and times in a standard format such as <a href="https://en.wikipedia.org/wiki/ISO_time">ISO time</a> or <a href="https://en.wikipedia.org/wiki/Epoch_time">epoch time</a>, and to use a library like <a href="https://datejs.com/">Date.js</a> or <a href="https://momentjs.com/">Moment.js</a> to format them for the given locale. These libraries can also handle converting the time to the current zone, so you can store all dates and times in a common format on the server (such as <a href="https://en.wikipedia.org/wiki/UTC">UTC</a>) and convert them to the right time zone in the browser.

Dates and times are also tricky when displaying calendars and date pickers. The US starts the week on Sunday, the UK on Monday and the Maldives on Friday. The <a href="https://jqueryui.com/demos/datepicker/#localization">jQuery UI date picker</a> includes over 50 localized files to support different calendar formats around the world.

The same is true of currencies and other number formats. Some countries use commas to separate numbers, and others use periods. Always use a library with localized files for each of the locales that you need to support.

StackOverflow covers this topic well when discussing <a href="https://stackoverflow.com/questions/2532729/daylight-saving-time-and-timezone-best-practices">daylight savings time and time zone best practices</a>.</p>

## 6\. Use UTF-8 Almost All Of The Time

The history of computer character encodings is a <a href="https://www.smashingmagazine.com/2012/06/06/all-about-unicode-utf8-character-sets/">long one</a>, but the most important thing to remember is that <a href="https://en.wikipedia.org/wiki/UTF-8">UTF-8</a> is the right choice 99% of the time. The only time not to use UTF-8 is when you're working primarily with Asian languages and absolutely need the efficiency of <a href="https://en.wikipedia.org/wiki/Utf-16">UTF-16</a>.

This comes up a lot with Web applications. If the browser and the server don't use the same character encoding, then the characters will get corrupted and your application will fill up with little squares and question marks.

Many programming languages store files using the system’s default encoding, but it won't matter that your server is English when all of your users are browsing in Chinese. UTF-8 fixes that by standardizing the encodings across the browser and the server.

Invoke UTF-8 at the top of all of your HTML pages:

<pre><code class="language-markup tmp-html">&lt;head&gt;
&lt;meta http-equiv="Content-Type" content="text/html; charset=utf-8"&gt;</code></pre>

And specify UTF-8 in the HTTP <code>Content-Type</code> header, like this:

<pre><code class="language-markup tmp-html">Content-Type: text/html; charset=utf-8</code></pre>

The <a href="https://www.ietf.org/rfc/rfc4627.txt">JSON specification</a> requires that all JSON documents use Unicode with a default of UTF-8, so make sure to use UTF-8 whenever you're reading or writing data.</p>

## 7\. Give Strings Room To Grow And Shrink

Strings change size in translation.

<img class="aligncenter size-full wp-image-120596" title="Repeat password example" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/06256223-d1b2-43bb-8855-8f129cbf716e/repeat-password.png" alt="Repeat password example" width="500" height="136" />

“Repeat password” is over 50% wider in German than in English; if there isn't enough space, then your strings will overlap other controls. WordPress solves this problem by leaving extra space after each label for the string to grow.

<img class="aligncenter size-full wp-image-120834" title="Label spacing in the WordPress admin" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c0188256-c869-4cfc-9d55-e531e36b8aa0/label-spacing.png" alt="Label spacing in the WordPress admin" width="551" height="80" />

This works well for languages whose strings are roughly of the same length, but for languages with long words, such as German and Finnish, the controls will overlap if you don't leave enough space. You could add more space, but that would put the labels and controls pretty far apart from each other in compact languages such as Chinese, thus making them hard to use.

<img class="aligncenter size-full wp-image-120835" title="Label spacing in the WordPress admin in Chinese" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/781e93f7-4218-4b48-a7f3-0fff6f903c2f/label-spacing-ch.png" alt="Label spacing in the WordPress admin in Chinese" width="551" height="80" />

Many designers of forms give their labels room to grow and shrink by aligning them to the right or by placing them above the controls.

<img class="aligncenter size-full wp-image-120836" title="Label above controls in the WordPress admin" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dea853f8-d1a8-4ca4-bd8b-94e3879ca875/labels-above.png" alt="Label above controls in the WordPress admin" width="551" height="121" />

Putting labels above the controls works well for a short form, but it makes a form with a lot of fields very tall.

There's no perfect answer for how to make your application work in all languages; many form designers mix and match these approaches. Short labels like “User name” and “Role” won't change much in translation and need just a little extra space. Longer paragraphs will change substantially and need room to grow wider, taller or sometimes both.

<img class="aligncenter size-full wp-image-120837" title="Label next to and above controls in the WordPress admin" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9e008052-9a16-4794-bc57-2ea55706662f/long-short-label.png" alt="Label next to and above controls in the WordPress admin" width="547" height="163" />

Here, WordPress gives a little extra space for the “Biographical Info” label, but it puts the longer description below the field so that it can grow in translation.</p>

## 8\. Always Use A Full Locale

The full locale includes the language and country code, and it supports alternate spellings, date formats and other differences between two countries with a shared language.

Always use a full locale instead of just a language when translating, so that you know whether you're doing someone a favor or a favour, and that they know whether to take the elevator or the lift, and that they know whether £100.00 is expensive.</p>

## 9\. Never Trust The Browser To Know The Right Locale

Localization is much more difficult with browsers and JavaScript because they give a different locale depending on who's asking.

JavaScript has a property to tell you the current language, named <code>navigator.userLanguage</code>. All browsers support it, but it's generally useless.

If I install Firefox in English, then my <code>navigator.userLanguage</code> value would say <code>English</code>. I can then go into my preferences and change my preferred languages. Firefox lets me select multiple languages, so I could specify my order of preference as English from the US, then any other English, then Japanese.

<img class="aligncenter size-full wp-image-120597" title="Language preferences in Firefox" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8403cc47-3380-45c6-bf78-36e369b4c4d3/languages.png" alt="Language preferences in Firefox" width="457" height="369" />

Specifying a set of locales makes it possible for servers to find the best match between the languages that I know they support. Firefox takes these locales and sends them to the server in an HTTP header, like this:

<pre><code class="language-javascript">
Accept   en-us,en;q=0.7,ja;q=0.3
</code></pre>

Firefox even uses the quality factor (that <code>q=</code> part) to indicate how much I prefer one locale over another.

This means that the server might return content in English or Japanese or another language if it doesn't support either. However, even after I’ve set my preferred language in Firefox, the value of my <code>navigator.userLanguage</code> property will still be English and only English. The other browsers don't do much better. This means that I might end up with the server thinking I want Japanese and with the JavaScript thinking I want English.

JavaScript has never solved this problem, and it has not one standard localization library, but dozens of different standards. The best solution is to embed a JavaScript property or some other field in your page that indicates the locale when the server processes each request. Then you can use that locale when formatting any strings, dates or numbers from JavaScript.</p>

## 10\. Plan For Languages That Read Left To Right And Right To Left

Most languages are written on screen from left to right, but Arabic, Hebrew and plenty of others go from right to left. HTML provides a property for the <code>html</code> element named <code>dir</code> that indicates whether the page is <code>ltr</code> (left to right) or <code>rtl</code> (right to left).

<pre><code class="language-markup tmp-html">&lt;html dir="rtl"&gt;</code></pre>

There's also a direction property in CSS:

<pre><code class="language-css">input {
    direction: rtl;
}</code></pre>

Setting the <code>direction</code> property will make the page work for the standard HTML tags, but it can't switch a CSS element with <code>float: left</code> to <code>float: right</code> or change an absolutely positioned layout. To make more complex layouts work, you will need a new style sheet.

An easy way to determine the direction of the current language is to include a <code>direction</code> string in the resourced strings.

<pre><code class="language-javascript">
direction = rtl
</code></pre>

Then you can use that string to load a different style sheet based on the current locale.</p>

## 11\. Never Sort In The Browser

JavaScript provides a <a href="https://www.w3schools.com/jsref/jsref_sort.asp"><code>sort</code></a> function that arranges lists of strings alphabetically. It works by comparing each character in each string to determine whether <em>a</em> is greater than <em>b</em> or <em>y</em> is less than <em>z</em>. That's why it makes 40 come before 5.

The browser knows that <em>y</em> comes before <em>z</em> by using a large mapping table for each character. However, the browser includes the mapping tables only in the current locale. This means that if you have a list of Japanese names, the browser wouldn’t be able to sort them properly in an English locale; it would just sort them by Unicode value, which isn't correct.

This problem is easy to see in languages such as Polish and Vietnamese, which frequently use diacritical marks. The browser can tell that <em>a</em> comes before <em>b</em>, but it doesn't know whether <em>ằ</em> comes before <em>ã</em>.

The only place to sort strings properly is on the server. Make sure that the server has all of the code mappings for the languages you support, and that you send lists to the browser presorted, and that you call the server whenever you want to change the sorting. Also, make sure that the server takes locale into account for sorting, including right-to-left locales.</p>

## 12\. Test Early And Often

Most teams don't worry about localization until it's too late. A big customer in Asia will complain that the website doesn't work, and everyone will scramble to fix 100 little localization bugs that they had never thought of. Following the rules in this article will avoid many of those problems, but you will still need to test; and translations usually aren't ready until the end of the project.

I used to translate my projects into <a href="https://en.wikipedia.org/wiki/Pig_Latin">Pig Latin</a>, but that didn't test Asian characters, and most browsers don't support it. Now I create test translations with <a href="https://en.wikipedia.org/wiki/Xhosa_language">Xhosa</a> (<code>xh_ZA</code>). All browsers support Xhosa, and Nelson Mandela speaks it natively, but I've never been asked to support it in a product.

I don't speak Xhosa, so I create a new translation file and add <code>xh</code> to the beginning and end of every string. The <code>xh</code> makes it easy to see whether I've missed a string in the code. Throw in a few Japanese Kanji characters to test character encoding, and I have a messy string that tests for all of my translation issues.

Making the test translation file is easy. Just save a new properties file with <code>xh_ZA</code> in the file name and turn…

<pre><code class="language-javascript">name = Username</code></pre>

… into:

<pre><code class="language-javascript">name = xh吳清源Username吳清源xh</code></pre>

The resulting jumble will test that I've resourced every string, that I'm using the right locale, that my forms work with longer strings and that I'm using the right character set. Then I’ll just quickly scan the application for anything without the <code>xh</code> and fix the bugs before they become urgent issues.

Do the right thing for localization ahead of time, and you'll save yourself a lot of trouble in the long run.

<em>(al) (km)</em>

