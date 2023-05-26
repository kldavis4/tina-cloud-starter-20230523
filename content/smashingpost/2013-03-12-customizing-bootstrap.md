---
title: How To Customize Twitter’s Bootstrap
slug: customizing-bootstrap
image: null
date: 2013-03-12T14:50:34.000Z
author: thomas-park
description: >-
  Twitter’s [Bootstrap](https://twitter.github.com/bootstrap/) has taken off like
  a rocket since its release a year ago. The popular CSS framework supplies a
  responsive grid system, pre-styled components and JavaScript plugins to a
  parade of websites.
categories:
  - Coding
  - Frameworks
  - CSS
  - JavaScript
---
Twitter’s <a href="https://twitter.github.com/bootstrap/">Bootstrap</a> has taken off like a rocket since its release a year ago. The popular CSS framework supplies a responsive grid system, pre-styled components and JavaScript plugins to a <a href="https://builtwithbootstrap.com">parade of websites</a>.

One of Bootstrap’s appeals is that it just works. It’s a significant time-saver when starting a website, so much so that major organizations such as NBC, NASA and the White House are adopting it. And it empowers even the non-designers among us to turn out something decent.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Responsive Design Frameworks: Just Because You Can, Should You?](https://www.smashingmagazine.com/2014/02/responsive-design-frameworks-just-because-you-can-should-you/)
*   [Responsive Web Design: What It Is And How To Use It](https://www.smashingmagazine.com/2011/01/guidelines-for-responsive-web-design/)
*   [Design Process In The Responsive Age](https://www.smashingmagazine.com/2012/05/design-process-responsive-age/)
*   [Techniques For Gracefully Degrading Media Queries](https://www.smashingmagazine.com/2011/08/techniques-for-gracefully-degrading-media-queries/)

To illustrate, you can transform the default button below on the left to the polished one on the right just by adding two classes: <code>btn</code> and <code>btn-primary</code>.

{{% feature-panel %}}

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bd2991ab-a5c7-410f-acb5-bf4c690d0318/buttons.png"><img loading="lazy" decoding="async" class="122052" title="Default and Bootstrap buttons" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bd2991ab-a5c7-410f-acb5-bf4c690d0318/buttons.png" alt="" width="500" height="129" /></a><br>
<em>A browser’s default button (left) and a Bootstrap button (right).</em>

But what if your company logo is a different shade of blue? Not to worry. <strong>You don’t have to stick with the defaults.</strong> This article shows some ways to customize Bootstrap to fit your needs, whether it’s a tweak to a button or a full-fledged theme.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/940b9051-b304-4e99-a454-20f5e703793c/themes.png"><img loading="lazy" decoding="async" class="122048" title="Bootstrap Themes" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/940b9051-b304-4e99-a454-20f5e703793c/themes.png" alt="" width="500" height="250" /></a><br>
<em>Three Bootstrap themes from Bootswatch</em>

## Overriding With CSS

The most straightforward approach is to override Bootstrap’s styles using CSS. This can be accomplished by writing your own styles for the classes used in Bootstrap. You could, for example, make your buttons more rounded by adding the following code:

<pre><code class="language-css">.btn {
   -webkit-border-radius: 20px;
   -moz-border-radius: 20px;
   border-radius: 20px;
}</code></pre>

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0f3ea457-66ef-4353-95fe-915c1cf19281/custom-button1.png"><img loading="lazy" decoding="async" class="122056" title="Custom button" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0f3ea457-66ef-4353-95fe-915c1cf19281/custom-button1.png" alt="" width="500" height="129" /></a><br>
<em>A Bootstrap button customized with an increased border radius.</em>

For the overrides to be successful, remember to add your code after Bootstrap’s have been declared.

The advantage of this method is that <strong>it hardly changes your workflow</strong>. Even when using Bootstrap, you’ll want your own style sheet in order to fit the framework to your content just right. You might not realize it, but Bootstrap’s own website relies on a thousand-line style sheet <em>on top of</em> Bootstrap.

But for more extensive changes (such as overhauling the navigation bar) or for changes that aren’t localized (such as changing the highlight color used throughout the website), overriding in this piecemeal fashion can feel like a band-aid solution. And your new styles are tacked onto Bootstrap’s default style sheet, adding bloat to the already considerable 100 KB size. If you’re planning more than a few such overrides, you may want to consider a more extensive approach.</p>

## Generating A Custom Build

An alternative is to create a custom build entirely. With the <a href="https://twitter.github.com/bootstrap/customize.html">official generator</a>, you can assign your own values to key variables that are reused throughout the framework, such as <code>@linkColor</code>, <code>@navbarHeight</code> and <code>@baseFontFamily</code>. Click the big button at the end of the generator and download the resulting style sheet. You can even pick and choose which components to include, slimming down your file size.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1dda1634-c7f2-4eb9-8dac-fb29bef38d5c/generator-full.png"><img loading="lazy" decoding="async" class="122059" title="Bootstrap generator" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a0fe6f46-0903-4d47-9773-fbe0a177ef8f/generator1.png" alt="" width="500" height="362" /></a><br>
<em>Some of the variables that can be set in the official generator. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1dda1634-c7f2-4eb9-8dac-fb29bef38d5c/generator-full.png">Large version</a>)</em>

Several third-party generators are also available on the Web. Unlike the official generator, they provide live previews as you adjust variables. <a href="https://bootswatchr.com">Bootswatchr</a> organizes itself by variable, and StyleBootstrap by component. <a href="https://www.boottheme.com">BootTheme</a> adds a roll-the-dice feature to randomize your values. If lady luck isn’t on your side, <a href="https://www.lavishbootstrap.com">Lavish</a> can generate a theme from any image you provide, and <a href="https://paintstrap.com/">PaintStrap</a> from existing color schemes.

Using a generator simplifies the logistics of custom-building Bootstrap. And with a deft hand, you can pull together a well-designed, unique look.</p>

## Digging Into LESS

Even with over a hundred variables, you still might find generators too constraining. Or you might not want to work in-browser, which can limit integration with your workflow. In either case, it’s time to dig into Bootstrap’s source.</p>

### Getting to the Source

As an open-source project, Bootstrap’s source code is <a href="https://github.com/twitter/bootstrap/zipball/master">freely available</a> (ZIP) for downloading.

Open the source and you’ll notice that Bootstrap’s styles aren’t written in CSS after all, but in <a href="https://lesscss.org">LESS</a>. LESS is a dynamic style sheet language that sports a <a href="https://www.smashingmagazine.com/2010/12/06/using-the-less-css-preprocessor-for-smarter-style-sheets/">number of advantages over CSS</a>, including the ability to nest selectors and to create variables (as used in the generators above). Once written, the LESS code is compiled to CSS either in advance or at runtime. If Sass is your preferred language, there’s a <a href="https://github.com/thomas-mcdonald/bootstrap-sass">Sass conversion of Bootstrap</a>.

In the <code>less</code> directory, you’ll find a bunch of LESS files labelled by component.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b1105681-4b6e-404a-9a32-03c9e5801ea8/bootstrap-less-full.png"><img loading="lazy" decoding="async" class="122064" title="Bootstrap LESS files" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/18f75654-a088-4cb6-9b79-4b1c38429ced/bootstrap-less.png" alt="" width="500" height="526" /></a><br>
<em>The LESS files that make up Bootstrap’s source. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b1105681-4b6e-404a-9a32-03c9e5801ea8/bootstrap-less-full.png">Large version</a>)</em>

Some things to note about these files:

*   `bootstrap.less` This is the central file. It imports all of the others and is the one you’ll ultimately compile.
*   `reset.less` Always the first file to be imported.
*   `variables.less` and `mixins.less` These always follow because they’re dependencies for the rest. The former contains the same variables as used on the generator websites.
*   `utilities.less` This is always the last file to be imported, in order for the classes that it contains to override the rest of the styles where necessary.

Open up the LESS files and check out how Bootstrap styles each component. For example, in <code>buttons.less</code>, here is the rule for the <code>.btn-large</code> class:

<pre><code class="language-css">.btn-large {
   padding: 9px 14px;
   font-size: @baseFontSize + 2px;
   line-height: normal;
   .border-radius(5px);
}</code></pre>

As you can see, it looks very similar to CSS. It does have a couple of LESS-specific features, however. In the <code>font-size</code> declaration, the variable <code>@baseFontSize</code> — specified in <code>variables.less</code> — and an addition operation are combined to calculate the value. The <code>.border-radius</code> mixin, defined in <code>mixins.less</code>, also handles vendor prefixes so that we don’t have to.

It’s within these LESS files that you can make your customizations. Start with the values in <code>variables.less</code>, then experiment with the styles in the rest of the source. Have some fun with it.</p>

### Installing LESS

After you’ve made some changes and are ready to view them, you’ll want to compile to CSS. To do this, you’ll need to install LESS. You have a <a href="https://lesscss.org/#-client-side-usage">number of options</a>; for starters, I’d suggest a client such as <a href="https://incident57.com/less/">LESS.app</a>.

If you prefer the command line, then install <a href="https://nodejs.org">Node.js</a>, which includes the Node Package Manager (NPM). Then, issue the following command:

<pre>npm install less
</pre>

Once it’s installed, you can compile <code>bootstrap.less</code> like so:

<pre>lessc bootstrap.less &gt; bootstrap.css
</pre>

And for the minified version, use this instead:

<pre>lessc --compress bootstrap.less &gt; bootstrap.min.css
</pre>

Regardless of how you compile, target only <code>bootstrap.less</code> when compiling, not any of the other files.</p>

### Modularizing Your Changes

You might notice a limitation of the approach above. Your changes are now intertwined with the original source. So, when Bootstrap is inevitably updated with bug fixes and new features, disentangling your customizations and updating them to the new version will be nearly impossible.

To avoid this issue, you’ll want to modularize your changes. Here’s the approach I take when making themes for <a href="https://bootswatch.com">Bootswatch</a>.

First, I download Bootstrap’s source code, rename it to <code>bootstrap</code> and leave it untouched. Instead of making changes to the files that it contains, I create a separate folder, named <code>custom</code>, with these three files:

*   `custom-variables.less` I make a copy of `variables.less` from Bootstrap’s source and modify the variables in this copy instead.
*   `custom-other.less` This file holds any other customizations that I want to make that aren’t possible with the variables.
*   `custom-bootstrap.less` This is the new “central” file that you’ll compile to CSS. Along with the original LESS files, it imports the two custom files above using the following commands:

<pre><code class="language-css">@import "../bootstrap/less/bootstrap.less";
@import "custom-variables.less";
@import "custom-other.less";
@import "../bootstrap/less/utilities.less";</code></pre>

By keeping the changes separate, you can easily upgrade to newer versions of Bootstrap. Just replace the old <code>bootstrap</code> directory with the new one, and recompile.

I’ve created a boilerplate for this set-up, named <a href="https://github.com/thomaspark/bootswatch/tree/master/swatchmaker">swatchmaker</a>. It also includes some extras, such as test pages and commands to update Bootstrap to the latest version, to automatically compile whenever changes are saved, and to reset your customizations.</p>

## Tips And Techniques

Here are additional tips and techniques that you might find helpful when customizing Bootstrap.

*   **Get to know Bootstrap.**.  Read the [official documentation](https://twitter.github.com/bootstrap/scaffolding.html), familiarize yourself with all of the components, and learn the ins and outs of the source. If you will be regularly customizing Bootstrap, then the time you invest here will pay off down the line.
*   **Start with variables first.**.  Whether you’re using a generator or editing the source, begin your modifications with the supported variables. You might discover that they’re sufficient for your needs. Just changing the navigation bar and basic colors is a huge start.
*   **Pick your palette.**.  Think about your website’s color scheme, particularly your primary and secondary accent colors. Some [good resources](https://www.colourlovers.com) are out there to help you with this. After you’ve decided on a palette, set up and use these colors as variables. You shouldn’t be seeing hex codes sprinkled throughout your code.
*   **Add some assets.**.  A [textured background](https://subtlepatterns.com/) and [custom font](https://www.google.com/webfonts/) make a world of difference. For Web fonts, you can add the `@import` statement anywhere in your code, because LESS will hoist it to the top of the generated CSS. I like to keep mine at the top of `custom-other.less`.
*   **Use alpha transparency.**.  When adding touches like `box-shadow` and `text-shadow`, define your colors using [RGBa, with fallbacks for old browsers](https://css-tricks.com/rgba-browser-support/), and use your values consistently. This will add cohesion to your components.
*   **Match selectors.**.  When overriding a class, try to use the same selector that Bootstrap uses. This will help to keep your classes in sync with the originals and avoid an escalating specificity war. Remember that, in a tie, the last one wins. With the modularized set-up above, your customizations will always override the defaults.
*   **Encapsulate your code.**.  Remember that LESS allows for nested selectors. Make use of this to encapsulate each component. I’ve found this to be a big help in keeping code tidy and readable. While both work the same, rather than using this…

        .navbar .brand {
           color: @white;
        }

        .navbar .nav > li > a {
           color: @grayLighter;
        }

    … try this:

        .navbar {

           .brand {
            color: @white;
           }

           .nav > li > a {
            color: @grayLighter;
           }
        }

*   **Take advantage of mixins.**.  Out of the box, LESS includes handy mixins such as `lighten()` and `darken()`. The ones that Bootstrap defines in `mixins.less` are also at your disposal. And don’t forget that you can always create your own.
*   **Learn by example.**.  Look at how others are customizing Bootstrap. For instance, the sources for all of my themes are available on [GitHub](https://github.com/thomaspark/bootswatch/tree/gh-pages).

Do you have a tip to add? Please share in the comments below.</p>

## Final Word

If performance is a priority — as it often should be — then you’ll be best served by <a href="https://www.smashingmagazine.com/2007/09/21/css-frameworks-css-reset-design-from-scratch/">tailoring your own solution</a> atop a <a href="https://html5boilerplate.com/">more lightweight foundation</a>.

But if your goal first and foremost is to launch your website, or if front-end development isn’t your strong suit, then Twitter Bootstrap may be right for you. Many people put themselves in these camps, judging by Bootstrap’s popularity.

Given its heavy usage across the Web, consider taking everything good about Bootstrap and making it your own.

{{< signature "al" >}}

