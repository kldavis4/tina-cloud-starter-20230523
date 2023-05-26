---
title: 'CSS Variables: The Architecture Backbone'
slug: variables-in-css-architecture
image: >-
  https://i.pinimg.com/originals/d5/e0/0f/d5e00f1162cc3c9b823ce9f2b3960146.jpg
date: 2016-01-13T00:53:05.000Z
author: karenmenezes
summary: >-
  Variables can be seen as the backbone of a well-constructed project. Well-commented and well-defined variables set a great foundation for a project of any size. By maintaining a variable-centric approach, we can structure our style sheets with a meaning and modularity that persist beyond the trends that come and go.
description: >-
  Variables are the core reference for SASS Projects. Badly architected preprocessor code is much harder to debug and maintain than a large CSS file created with basic structure and common sense.
categories:
  - Coding
  - CSS
  - Sass
  - Preprocessors
---

When they hit the front&ndash;end landscape a few years ago, preprocessors were heralded as the saviour of CSS, bringing modularity, meaning and even a [degree of sexiness](https://www.slideshare.net/itsmisscs/2011-d4dboston). Terms like **“Sass architecture”** became commonplace, ushering in a new generation of CSS developers who occasionally went to excess with their new&ndash;found power. The results were marvellous, and sometimes undesirable.

One of the unpleasant side effects was a **preprocessor elitism** that continues to persist. Neophyte designers who were just getting their hands dirty with CSS were overwhelmed by an influx of must&ndash;have tools and confused by the bitter partisan wars in web development forums.

<figure><a href="https://i.pinimg.com/originals/d5/e0/0f/d5e00f1162cc3c9b823ce9f2b3960146.jpg"><img src="https://i.pinimg.com/originals/d5/e0/0f/d5e00f1162cc3c9b823ce9f2b3960146.jpg" width="480" height="320" alt="Variables: The Backbone Of CSS Architecture" /></a><figcaption>These days, building without preprocessors is considered to be a poor practice. The results are sometimes undesirable. Image credit: <a href="https://schedule.sxsw.com/2014/events/event_IAP23717">SXSW</a></figcaption></figure>

Using a preprocessor does not automatically upgrade one’s code: A thorough foundation in CSS is a prerequisite. In my experience, badly architected and overly abstracted preprocessor code is much harder to debug and maintain than a large CSS file created with basic structure and common sense.

Another side effect of preprocessors was the high level of abstraction for simple UI modules. This tended to make maintenance a nightmare and raised the barrier to entry. Even Kitty Giraudel, who takes Sass functionality to another dimension, wrote about [keeping Sass simple](https://www.sitepoint.com/keep-sass-simple/).

I like to consider preprocessors as **well&ndash;written meta languages for CSS**, with useful helper functions, extensions and abstractions. Beneficial features like nesting, mixins, extends and looping have their advantages *and* limitations, if not used wisely. Many of us can recall mixins, nesting, extends and placeholders being lauded as the next big thing, followed by articles on how mixins bloat style sheets, nesting creates CSS soup and extends are invisible and inflexible.

Contradictory as these viewpoints are, they were an inevitable side effect of preprocessor evolution and have resulted in the creation of excellent style guides, like [Chris Coyier’s](https://css-tricks.com/sass-style-guide/) and [Kitty Giraudel’s](https://sass-guidelin.es/) (both for Sass) and [SassDoc](https://sassdoc.com/), to generate Sass documentation.

## What Is The Preprocessor Poster Child?

I consider variables to be the backbone of a well&ndash;constructed project, allowing reusability and meaningfulness to take precedence. When a developer takes over another’s preprocessor code, the first thing they are likely to look at is the variables file. Well&ndash;commented and well&ndash;defined variables set a great foundation for a project of any size.

While this article focuses on preprocessor variables, it also delves into native CSS variables. This article assumes that you are familiar with Sass, LESS, Stylus or PostCSS; all of the examples and demos below use Sass for consistency.

{{% feature-panel %}}

## Why Should Variables Be The Core Reference For A Sass Project?

Whether you’re dealing with another developer’s hand&ndash;me&ndash;downs or your own team’s code base, you know that good documentation and a style guide lighten the load. However, you’d still need to comb through Sass, LESS or Stylus partials comprising molecules, atoms, organisms, helpers, globals, components, layout, base and insert&ndash;new&ndash;hotness&ndash;term&ndash;here. Naturally, things get out of hand since such terminology is open to interpretation:

*   “Should I add this property to the globals or the base partial?”
*   “Why is this in the layout partial? Shouldn’t it be coupled with the grid partial?”
*   “Do I make this a class, a mixin, an extend or all three?”

One man’s atoms are another man’s molecules, even if you’re closely following the [atomic design](https://patternlab.io) methodology, created by Brad Frost and Dave Olsen.

Another scenario: You find a mixin created by developer A that includes another vendor&ndash;prefix mixin that developer B added at some point, a convenient extend from another partial (added by developer A to make things “DRY”) and two variables defined in two separate files.

Because of the high level of abstraction that preprocessors are capable of, I’d recommend making your variables file the **single source of truth**.

## Storing CSS Variables

Many projects using preprocessors will have a partial file named `_variables.scss`, which, in my opinion, should store every (or almost every) single variable used in that project (save for a few useful local variables peppering other partials). This serves as the most crucial CSS reference for any project. When a developer is in doubt, they can simply refer to the config or variables partial.

If you have a large app with several variables, you could, in theory, split them into several partial files, although I find this to be an uncommon use case.

## When Should I Create A Variable?

If it appears more than once, it’s almost always going to appear more than twice. Additionally, if a value (for color, length, size, etc.) is likely to be updated, consider creating a new variable.

Below is a generic example of recycling variables for a header that is fixed to the viewport:

See the Pen [Reusing Sass variables](https://codepen.io/imohkay/pen/9952c2f856e0dbc7f28ddc034dcb36a1/) by Karen Menezes ([@imohkay](https://codepen.io/imohkay)) on [CodePen](https://codepen.io).

As is evinced in the demo above, the `$height-header` variable is reused to set the height of the header, menu trigger link and search input and to set the top padding for the `body` element. Future updating will be a breeze.

Also, note how the `$height-footer` variable needs to be interpolated to provide the `min-height` to the `main` element, using the `#{$variable-name}` syntax, which allows Sass to replace it with its corresponding value of `40px` at compilation time.

## Reduce Mixins And Extends To The Bare Essentials

One of the easiest ways to ensure that the **primary reference in a project remains the variables file** is to define all variables in one place (with the exception of some local variables) and eliminate superfluous mixins and extends. This reduces abstraction by leaps and bounds. A tool such as [Autoprefixer](https://github.com/postcss/autoprefixer) handles all of your vendor prefixing, thereby reducing your mixin load to common concepts like “clearfix,” essential ones for media queries, grids, some math and nice&ndash;to&ndash;haves like CSS border triangles and text truncation.

Each time you create a mixin, ask yourself whether it actually provides value to the project and team. Don’t write mixins because you think it will cut down on the time it takes to write CSS properties by hand. A good text editor with code hinting and autocomplete functionality nullifies this issue.

### Write Vanilla CSS When Abstraction Causes Confusion

<pre><code class="language-css">/* Avoid mixins that are better served with plain CSS. */

@mixin center-element {
   display: block;
   margin-left: auto;
   margin-right: auto;
}

.selector {
   @include center-element;
}

/* There are several ways to center in CSS, and the included center-element mixin gives no clue (without referring to the mixins partial) about the mode of centering used.
Was it flexbox, text alignment, auto margins or vertical alignment? */

/*-----------------------------------------------------*/
/* Why not just write vanilla CSS and reduce abstraction, for this use case? */

.selector {
   display: block;
   margin-left: auto;
   margin-right: auto; 
}
</code></pre>

### Use Mixins or Extends for Well-Established Conventions

<pre><code class="language-css">/* Do this: The clearfix hack for clearing floats is a known concept that 
most developers would recognize */

/* Clearfix placeholder: Extend to parents of floated children to clear floats */

%clearfix {
   &amp;:after {
      content: ’;
      display: table;
      clear: both;
   }
}

.selector  {
  @extend %clearfix; /* or define and include a mixin instead */
}
</code></pre>

### For Global Styles, Can You Swap a Mixin With a Variable If It Doesn’t Need Arguments?

<pre><code class="language-css">/* Avoid the following: */

@mixin box-shadow {
  box-shadow: 2px 2px 4px rgba(0, 0, 0, 0.1); 
}

/*-----------------------------------------------------*/

/* Instead, just create a variable: */

$box-shadow-base: 2px 2px 4px rgba(0, 0, 0, 0.1);

.selector {
   box-shadow: $box-shadow-base; /* Reuse variable where appropriate. */
}
</code></pre>

### Don’t Lock Yourself in by Using Mixins for Vendor Prefixes

<pre><code class="language-css">/* Avoid this. 
It encourages both mixin lock-in and needless abstraction. 
*/

@mixin flexbox {
   display: -webkit-box;
   display: -webkit-flex;
   display: -moz-flex;
   display: -ms-flexbox;
   display: flex;
}

.selector {
   @include flexbox;
}

/* Consider using the Autoprefixer plugin, which does one thing
and does it well. */

.selector {
   display: flex; 
   /* Autoprefixer will generate the vendor prefixes in your compiled 
   style sheet. */
}
</code></pre>

### Use Local Variables Only When Necessary

If you’re drowning in another developer’s convoluted preprocessor partials (or your own), then a variables partial becomes like a life raft. While local variables can be indispensable, keep the following in mind while using them:

*   Variables are handled differently in different preprocessors. For example, Sass allows default values for variables (if they aren’t already assigned) via the `!default` flag. LESS, on the other hand, provides [variables with lazy loading](https://lesscss.org/features/#variables-feature-lazy-loading).
*   Ensure that you understand variable scope. George Martsoukos’ great article on [variable scope in Sass](https://webdesign.tutsplus.com/articles/understanding-variable-scope-in-sass--cms-23498) is a must&ndash;read.
*   It’s very easy to unintentionally create two local variables with the same name, that are unrelated, in two different code blocks or mixins. While this is not an issue (since the variables are scoped), it could cause confusion with variable nomenclature in the long term.
*   If you have several local variables with the same value, consider converting them to one global variable instead. See the example below:

<pre><code class="language-css">/* Avoid creating multiple local variables with the same value. */

$spacing: 10px; // global variable inside _variables.scss partial

.accordion {
   $spacing-accordion: ($spacing * 2);
   padding: $spacing-accordion;
}

.card {
   $spacing-card: ($spacing * 2);
   padding: $spacing-card;
}

.banner {
   $spacing-card: ($spacing * 2);    
   padding: $spacing-banner;
}

/*-------------------------------------*/

/* Instead, consider adding a new global variable that ensures consistent spacing across different rules and UI modules. */

$spacing: 10px;
$spacing-double: ($spacing * 2);

.accordion {
   padding: $spacing-double;
}

.card {
   padding: $spacing-double;
}

.banner {
   padding: $spacing-double;
}

/* This new variable can also be reused elsewhere. */

.header {
   padding: $spacing $spacing-double;
}

.main {
   margin-top: $spacing-double;
}
</code></pre>

### Break Your Own Rules; It’s Often Helpful To Have a Few Handy Mixins or Placeholders

<pre><code class="language-css">/* Mixins can be extremely useful, keeping your markup free of superfluous 
classes and establishing conventions, while saving time. 
Having mixins whose names relate to the CSS properties they contain 
helps to create associations between the two. */

/* Mixin for text truncation, with ellipsis */
@mixin text-ellipsis {
   overflow: hidden;
   text-overflow: ellipsis;
   white-space: nowrap;
}

.selector {
   @include text-ellipsis;
}
</code></pre>

## Variables: Pixie-Dusting Our Partials With Care

Just because we can, should we create countless variables? A long variables file can be excruciating to comb through.

{{% ad-panel-leaderboard %}}

### Think Before Making a New Variable

Does your base button’s background color need a new variable (for example, `$button-color-base`)? Not unless you have a specific reason for doing so &mdash; for example, you’re working on a mammoth application or creating a framework that you want people to override, like Bootstrap (the 3x version uses `@btn-default-color` in its `buttons.less` partial). Why not simply reuse `$color-brand-1` or another color in your base button’s class?

Another example would be notification or alert colors. You may have different states, such as success, info and error. Although you may disagree, I find it unnecessary to create variables for these colors, although there are exceptions.

Let’s look at notifications or alerts, for example. I’ve created a base class named `notify` and the additional modifier classes `notify--success`, `notify--info` and `notify--error`.

Why not define these colors in the colors section of your variables partial and add them to your `notify` classes?

<pre><code class="language-css">/* Define in colors section in variables partial */  
$green-pista: #93c572;
$blue-ink: #000f55;
$red-velvet: #d22836;

/* Reuse in other partial */
.notify {
   background-color: $blue-ink; //set a default color
   /* more base styles here */
}

.notify--success {
   background-color: $green-olive;
}

.notify--info {
   background-color: $blue-ink;
}

.notify--error {
   background-color: $red-velvet;
}
</code></pre>

If, however, you have multiple UI modules that share these states (for example, buttons and tooltips), it might be prudent to declare your variables in the following manner:

<pre><code class="language-css">/* Define in colors section in variables partial */ 
$green-pista: #93c572;
$blue-ink: #000f55;
$red-velvet: #d22836;

$color-state-success: $green-pista;
$color-state-info: $blue-ink;
$color-state-error: $red-velvet;

/* Reuse in other partials */
.notify--success {
   background-color: $color-state-success;
}

.tooltip--success {
   background-color: $color-state-success;
}
</code></pre>

### Think Before Reusing a Variable; Would Native CSS Values Suffice?

CSS provides two important values, `inherit` and `currentColor`, that can be used to extend the cascade. The second one, `currentColor` takes inheritance for color a step forward and can be used with [all properties that accept a `color` value](https://www.w3.org/TR/css3-color/#currentcolor), including borders and SVG properties.

Note: The `inherit` value works in all browsers, while `currentColor` works in all browsers except Internet Explorer 8. Test for the [Safari bug](https://bugs.webkit.org/show_bug.cgi?id=133420) if you’re using `currentColor`.

Below is a common use case for the `inherit` keyword:

See the Pen [DRY with the CSS inherit keyword](https://codepen.io/imohkay/pen/19bd6dbf685cab457137f750eb8b60b5/) by Karen Menezes ([@imohkay](https://codepen.io/imohkay)) on [CodePen](https://codepen.io).

And here is a demo using the `currentColor` keyword:

See the Pen [DRY with the CSS currentcolor keyword](https://codepen.io/imohkay/pen/57abddd981f9912df8f27af361925303/) by Karen Menezes ([@imohkay](https://codepen.io/imohkay)) on [CodePen](https://codepen.io).

### Don’t Reuse Variables Inappropriately

Tempting as it may be to reuse `$height-input` for a UI module that has nothing to do with inputs, don’t give in. The law of karma catches up even more quickly with preprocessors.

<pre><code class="language-css">/* Input height defined in variables partial */
$height-input: 50px;

/* It is better to repeat yourself than misuse variables */
.image-thumbnail {
   width: $height-input;
   height: $height-input;
}
</code></pre>

## Variables: Nomenclature

Let’s face it: Naming variables is never straightforward. Discuss naming conventions based on the needs of your project and the people you work with. There’s no right or wrong; consistency is what matters in the long run.

*   Ensure consistency for hierarchies while naming variables (for example, `$font-primary`, `$heading-primary`, or `$font-family-1`, `$heading-1`, etc.).
*   Suffix with either the base or default, where it makes sense (for example, `$color-font-base`, `$box-shadow-base`, etc.).
*   Group similar variables by prefixing with a common keyword (for example, `$font-family-1`, `$font-size-base`, `font-bold`, etc.).

There are several ways you could choose to name your variables. Let’s consider a typical project with two fonts, Roboto (a sans-serif font) and Roboto Slab (a serif font), as an example.

(We will explore some options in the next sections.)

### Most Descriptive, But Most Restricted

This appears to be the most meaningful but is the hardest to maintain, especially if the fonts change at some stage. However, one can’t deny that such variables are a pleasure to work with!

<pre><code class="language-css">$roboto:'Roboto', sans-serif;        // body copy
$roboto-slab: 'Roboto Slab', serif;  // headings

body {
   font-family: $roboto;  
}

h1, h2, h3, h4, h5, h6 {
   font-family: $roboto-slab;
}
</code></pre>

### Descriptive, But Less Restrictive

This feels intuitive because you can swap the font values for serif and sans-serif without any additional overhead (i.e. replace Roboto with San Francisco or any other sans&ndash;serif font). However, the variable `$font-serif` will lose all meaning if replaced with a sans&mdash;serif font in the future.

<pre><code class="language-css">$font-sans-serif: 'Roboto', sans-serif;
$font-serif: 'Roboto Slab', serif;

body {
   font-family: $font-sans-serif;
}

h1, h2, h3, h4, h5, h6 {
   font-family: $font-serif;
}
</code></pre>

### Less Descriptive, With More Weightage

This provides meaning by offering a hierarchy for the fonts in your project. It feels awkward to type after a point; for example, `$font-quaternary` and `$font-quinary` might set someone’s head spinning. Of course, one would try to keep the number of custom fonts used to a minimum, but this has been known to occur in projects.

<pre><code class="language-css">
$font-primary: 'Roboto', sans-serif;        // body copy
$font-secondary: 'Roboto Slab', serif;      // headings
$font-tertiary: 'Cutive Mono', monospace;   // monospace for code blocks
$font-quaternary: 'Open Sans Condensed', sans-serif; // navigation in header

body {
   font-family: $font-primary;
}

h1, h2, h3, h4, h5, h6 {
   font-family: $font-secondary;
}

nav {
   font-family: $font-tertiary;
}
</code></pre>

### Less Descriptive, But Offers Some Weightage

This seems to be the easiest to maintain, but it might be the hardest to understand from viewing the referenced variable. However, it’s what I currently use since we’re decoupling the variable name from its generic font family and “species.”

<pre><code class="language-css">$font-family-1: 'Roboto', sans-serif;       // body copy
$font-family-2: 'Roboto Slab', serif;      // headings

body {
   font-family: $font-family-1;
}

h1, h2, h3, h4, h5, h6 {
   font-family: $font-family-2;
}
</code></pre>

## Common Variables For A Web Application

Below are some variables that I commonly use, grouped into logical sections.

### Variables for Dimensions

Is a variable being named for its relation to a specific element, even though it affects other elements? Take the height of the header in our earlier example. I would tie the name of that variable to the selector (for example, `$header-height` or, even better, `$height-header`).

I prefer `$height-header` to `$header-height`, because it is the value of the header’s height that is reused to provide height and padding to other elements.

You may have noticed in the examples above that I often name variables pertaining to dimensions as `$(&lt;dimension&gt;-&lt;selector&gt;)`. In my variables file, I group all variables pertaining to dimensions in one section. If you prefer to name your variables in the reverse manner (i.e. `$header-height`), ensure that the naming is consistent across the board.

Below is an example of variables that I group together because their dimensions can be reused.

<pre><code class="language-css">/*-------------------------------------*/
// WIDTHS AND HEIGHT

// Header: Height
$height-header: 60px; // or em 
/* can be reused for heights, paddings and positioning of other elements */

// Off-Canvas Navigation: Width
$width-nav: 250px;
/* can be reused for positioning menu via a negative offset */

// Text Inputs: Height
$height-form-widget: 45px;
/* can be reused for selects and submit buttons in 
forms. */
</code></pre>

### Variables for Spacing: Padding and Margins

I generally create one base variable named `$spacing`. I use this for paddings and margins.

If the client needs to globally increase white space between elements, I just change the value of the $spacing variable, and it will cascade to the other spacing variables, as you can see below.

On the other hand, you could be more specific and use `$spacing-padding` and `$spacing-margin.`

Avoid reusing spacing variables for absolutely positioned elements if changing those values globally would affect those elements.

<pre><code class="language-css">$spacing: 10px;                  
$spacing-half: ($spacing/ 2);
$spacing-double: ($spacing* 2);
$spacing-third: ($spacing* 3);
</code></pre>

### Variables for Colors

It’s possible that more articles have been written in the last couple of years on color naming in Sass than on accessibility on the web. I liked Dudley Storey’s [Sass Color Thesaurus](https://thenewcode.com/927/The-New-Defaults-A-Sass-Color-Thesaurus) the most because it ties in with my love for the natural world. Inspired by these meaningful names, I am now the proud co&ndash;owner of variable colors that reflect the hues of pistachios, peas and pomegranates.
I find this system elegant and evocative. If you’re ailing with what I call the “grey&ndash;lightest&ndash;xx syndrome” (or, even worse, “grey&ndash;darker–1x disorder”), then you could consider this as an alternative naming structure.

I also **treat brand colors differently**, especially for larger apps. With two brand colors (for example, teal and coral red), I name the variables `$color-brand-1` and `$color-brand-2`. I usually discuss these things with the developers I’m working with: Some of them prefer `$red`, but that defeats the purpose of being able to change the brand’s colors easily. Besides, one could counter&ndash;argue that a style guide is important for a large app and would eliminate these issues. In fact, while working on a style guide, I prefer not to put the HEX, RGB or HSL color value but to write the variable’s name instead.

<pre><code class="language-css">/* Colors: Brand */
$color-brand-1: #008080;  // blue teal - $color-brand-blue is an OK compromise
$color-brand-2: #ff7f50;  // orange coral

/* Colors: Common: Grey */
$grey-mist: #f5f5f5;
$grey-platinum: #bbb;
$grey-gravel: #444;

/* Colors: Common: Cool */
$green-pista: #93c572;
$green-mint: #98ff98;

/* Colors: Common: Warm */
$blue-cornflour: #659cef;
$blue-turquoise: #00c5cd;

/* Colors: Brands for Social Media */
$blue-facebook: #3b5998;
$blue-twitter: #55acee;
$red-youtube: #cd201f;

/* Colors: Links */
$color-link: $color-brand-1;
$color-link-hover: darken($link-color, 15%);
</code></pre>

### Variables for z-index

Large apps usually have several elements that create stacking contexts. Modals and overlays, tooltips and alerts, dropdowns and off&ndash;canvas menus, fixed headers and footers have z&ndash;indexes ranging from the negative to the plugin flavor (i.e. 9999 or even higher).

Chris Coyier suggests using [variables for z&ndash;index](https://css-tricks.com/handling-z-index/) and creating a new Sass partial just for this or, alternatively, using a Sass map. Meanwhile, Kitty Giraudel [provides a solution](https://www.sitepoint.com/better-solution-managing-z-index-sass/) using a function and Sass maps.

I’m generally happy to put z-index variables in the `_variables.scss` partial.

Keep in mind that third&mdash;party plugins often add z&ndash;indexes. I create new z&ndash;index variables for them as well. See the example below.

<pre><code class="language-css">$zindex-header: 1000;
$zindex-dropdown: 1100;
$zindex-lib-select2: 1200;  // plugin: Select2    
$zindex-notify: 1300;
$zindex-modal: 1400;
</code></pre>

### Variables for border-radius

Rounded corners for most apps I work on never exceed three different sizes:

<pre><code class="language-css">$border-radius: 5px;                              
$border-radius-half: $border-radius / 2;     
$border-radius-double: $border-radius * 2;
</code></pre>

I used to include a `$border-radius-circle` variable with a value of 50%, until common sense hit me and I realized it was wasted effort: You can always make a circle with `border-radius: 50%`, so just write `border-radius: 50%`!

### Variables for Typography

It’s helpful to prepend what is related to a font with `font-`.

Here are some variables I use for fonts:

<pre><code class="language-css">$font-family-1: 'Roboto', sans-serif;
$font-family-2: 'Playfair Display', sans-serif;
$font-size-base: 100%; // or px / em / rem
</code></pre>

With regard to **variables for font weights and styles**, there’s really no need to create a variable for the italic style, which is always italic.

Font weights are a different matter. Here’s a screenshot from [Google Fonts](https://www.google.com/fonts) of the different font weights of Exo:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a84fbc66-d932-4868-9829-8e88c97c1d9c/font-weight-naming-opt.jpg"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e9576943-d8f9-481a-ab42-d25ace7fbf3b/font-weight-naming-opt-preview.jpg" width="500" height="342" alt="Exo font weights" /></a><figcaption>Exo font weights.</figcaption></figure>

This seems to be a good convention for naming our font weights, although you probably won’t ever require this many weights for a project.

<pre><code class="language-css">$font-thin: 100; 
$font-extra-light: 200; 
$font-light: 300; 
$font-normal: 400; 
$font-medium: 500; 
$font-semi-bold: 600; 
$font-bold: 700;
$font-extra-bold: 800;
$font-ultra-bold: 900;
</code></pre>

I’ve often observed different variables created for different font weights and styles in projects that use `@font-face` rules for fonts, since they are, in reality, individual fonts. However, we can avoid this and recycle our font weight variables to achieve the same effect.

Let’s look at an example of the Amble font, generated by and downloaded from [Font Squirrel](https://www.fontsquirrel.com/). We’re using the regular and bold version, and only the WOFF format, which is supported in all modern browsers.

<pre><code class="language-css">/* Here’s the CSS generated by Font Squirrel, added to our type partial. I’ve removed references to the EOT, SVG and TTF formats. */

@font-face {
   font-family: 'ambleregular';
   src: url('Amble-Regular-webfont.woff') format('woff');
   font-weight: normal;
   font-style: normal;
}

@font-face {
   font-family: 'amblebold';
   src: url('Amble-Bold-webfont.woff') format('woff');
   font-weight: normal;
   font-style: normal;
}

/* We go ahead and create two variables for this: */
$font-family-1-regular: 'ambleregular', sans-serif; // or $font-amble-regular;
$font-family-1-bold: 'amblebold', sans-serif;

/* 
And possibly more variables for italic, italic + bold: 
$font-family-1-regular-italic: 'ambleitalic', sans-serif;
$font-family-1-bold-italic: 'amblebold_italic', sans-serif;
*/

/* The situation gets worse when we have multiple font families. */

/*
$font-family-1-regular: ...;
$font-family-1-regular-italic: ...;
$font-family-1-bold: ...;
$font-family-1-bold-italic: ...;
$font-family-2-regular: ...;
$font-family-2-regular-italic: ...;
$font-family-2-bold: ...;
$font-family-2-bold-italic: ...;
*/

/* We also need to unset font styles and weights for &lt;em&gt;, &lt;i&gt;, &lt;strong&gt; 
and &lt;bold&gt; HTML tags. */

/*
strong, bold {
   font-family: $font-family-1-bold;
   font-weight: normal;
   font-style: normal;
}

em, i {
   font-family: $font-family-1-regular-italic;
   font-style: normal;
   font-weight: normal;
}
*/

/* This feels like it’s getting out of hand. */
</code></pre>

Let’s look at a solution to deal with our custom fonts that’s low on abstraction.

See the Pen [Sass variables with the @font&ndash;face rule](https://codepen.io/imohkay/pen/ca5bec7c3dcc35559785686c15da03cd/) by Karen Menezes ([@imohkay](https://codepen.io/imohkay)) on [CodePen](https://codepen.io).

{{% ad-panel-leaderboard %}}

### Variables for Font Icons

<pre><code class="language-css">$font-icon: 'icomoon'; /* This allows you to swap out for another 
icon font family (for example, Font Awesome) without having to update in multiple 
places. */
</code></pre>

### Variables for Media Queries

<pre><code class="language-css">/* Define in your variables partial */

$media-lg: 1200px; // or em
$media-mid: 740px;
$media-sm: 600px;

/* Add to your grid or other partial */

// Media query mixin
@mixin media($media) {
   @media only screen and (min-width: $media) {
      @content;
   }
}

// Use somewhere

.selector {
   width: 25%;

   @include media($media-sm) {
      width: 50%;
   }

   @include media($media-lg) {
      width: auto;
   }
}

/* If you need additional media queries, add them as variables first. */
</code></pre>

For apps with complicated breakpoints, consider using the [include-media](https://include-media.com) Sass library, by Eduardo Bouças and Kitty Giraudel.

Below is a sample variables partial file, based on a small web app that I’m working on. It is a summary of everything we’ve discussed so far:

<pre><code class="language-css">/*-------------------------------------*/
// VARIABLES: GLOBAL
/*-------------------------------------*/

/*-------------------------------------*/
// GRID

// Grid: Gutters
$grid-gutter: 15px;

/*-------------------------------------*/
// MEDIA QUERIES

$media-lg: 1200px;
$media-mid: 900px;
$media-sm: 600px;

/*-------------------------------------*/
// DIMENSIONS: WIDTHS, HEIGHTS

// Header: Height
$height-header: 45px;

// Nav Menu: Width
$width-nav: 280px;

// Inputs: Height
$height-form-widget: 60px;

/*-------------------------------------*/
// COLORS

// Colors: Brand
$color-brand-1: #7dcfb8;

// Colors: Common: Greys
$grey-mist: #f5f5f5;
$grey-platinum: #bbb;
$grey-cement: #8f8f8f;
$grey-gravel: #444;

// Colors: Common: Cool
$blue-ink: #000f55;
$green-pista: #93c572;

// Colors: Common: Warm
$red-hibiscus: #f0214f;
$orange-marigold: #ff753b;

// Colors: Brands for Social Media
$blue-facebook: #3b5998;
$blue-twitter: #55acee;
$blue-vimeo: #1ab7ea;
$red-youtube: #cd201f;

// Colors: Links
$color-link: $color-brand-1;
$color-link-hover: darken($color-link, 12%);

// Colors: Base Font
$color-font-base: $grey-gravel;

/*-------------------------------------*/
// FONTS

// Fonts: Base styles
$font-family-1: Roboto, sans-serif;
$font-size-base: 18px;

// Fonts: Weights
$font-light: 300;
$font-normal: 400;
$font-bold: 700;

// Fonts: Sizes
$font-sm: 90%;
$font-sm-x: 80%;
$font-lg: 110%;
$font-lg-x: 120%;

/*-------------------------------------*/
// FONT-ICONS: FAMILY

$font-icon: 'icomoon';

/*-------------------------------------*/
// SPACING

$spacing: 10px;                
$spacing-double: $spacing * 2;   
$spacing-third: $spacing * 3;    
$spacing-half: $spacing / 2;

/*-------------------------------------*/
// Z:INDEX

$zindex-header: 1000;
$zindex-dropdown: 1100;
$zindex-lib-select2: 1200;  // plugin: Select2
$zindex-notify: 1300;
$zindex-modal: 1400;
</code></pre>

### Native Variables With Pure CSS

Not quite ready for production use (currently in the “[Last Call Working Draft](https://www.w3.org/TR/css-variables-1/)” stage), CSS variables are a step in the right direction, albeit with a slightly verbose syntax.

Do note that when we use the term “CSS variables,” we are **referring to custom properties that define variables, [referenced with the var() notation](https://www.w3.org/TR/css-variables-1/#defining-variables)**. The syntax for custom properties may change in the future.

Custom properties [are currently supported](https://caniuse.com/#search=variables) only in Firefox. They are in development in Chrome and under consideration in Internet Explorer.

Below is an example that uses CSS custom properties:

<pre><code class="language-css">div {
   --color-brand-1: teal;       /* Prepend custom property with -- */       
   color: var(--color-brand-1); /* Then reference with var() notation */
}
</code></pre>

Here’s how can we define custom properties that can be used globally:

<pre><code class="language-css">/* We can use the :root pseudo selector as a solution.

   In fact, in an HTML document, it has a higher specificity than the 
   &lt;html&gt; element it represents! */

   :root {
      --color-brand-1: teal;
      --font-size-base: 18px;
   }  

  /* Use anywhere */
   .ui-module {
      color: var(--color-brand-1);
      font-size: var(--font-size-base);
   }
</code></pre>

Custom properties respect the cascade:

See the Pen [CSS Variables: Custom properties respect the cascade](https://codepen.io/imohkay/pen/a0dd2c15541672fecd1dca8d44e09bc9/) by Karen Menezes ([@imohkay](https://codepen.io/imohkay)) on [CodePen](https://codepen.io).

Here are some of the advantages of native CSS variables over proprocessor variables:

*   [In his article](https://www.broken-links.com/2014/08/28/css-variables-updating-custom-properties-javascript/), Peter Gaston discusses how CSS custom properties can be accessed with JavaScript, via the `setProperty()` method on the style object. You can [test his demo](https://broken-links.com/tests/variables/) in Firefox.
*   CSS variables can be used directly inside SVGs to style their properties via presentation attributes like `fill` and `stroke`. See the CodePen demo below in Firefox.

See the Pen [CSS Variables: Custom properties with SVG](https://codepen.io/imohkay/pen/9aa69ee16b85c619158568dc90cc3177/) by Karen Menezes ([@imohkay](https://codepen.io/imohkay)) on [CodePen](https://codepen.io).

Almost every preprocessor tutorial begins with variables, and with good reason. By maintaining a variable-centric approach, we can structure our style sheets with a meaning and modularity that persist beyond the trends that come and go.

### Resources

*   “[Rethinking Your Sass Variables](https://www.alwaystwisted.com/articles/rethinking-your-sass-variables),” Stuart Robson Robson proposes an alternative method to what is discussed in this article &mdash; i.e. separating “global” and “component” variables into separate files.
*   “[Stop Using So Many Sass Variables](https://bensmithett.com/stop-using-so-many-sass-variables),” Ben Smithett Smithett makes a case for reducing abstraction and naming variables in a more generic manner. Although this is not considered a best practice per se, his article has several valuable points. The comments section is worth a look as well.
*   “Simplicity in Front&ndash;End Tooling,” Hans Christian Reinl Reinl discusses the “anti&ndash;trend of removing complex structure and tools in favor of doing ‘just’ our work.”
*   “[Variables Across CSS Preprocessors](https://csspre.com/variables/),” Alexander Futekov Futekov covers variable syntax and possibilities across Sass, LESS and Stylus, including lazy-loaded variables and default values.
*   “[Using Sass for Theming](https://webdesign.tutsplus.com/tutorials/how-to-use-sass-to-build-one-project-with-multiple-themes--cms-22104),” Tim Hartmann This comprehensive article on Sass theming takes a variable-centric approach. Hartmann also employs an interesting technique of creating variables for image paths.
*   “[CSS Custom Properties for Cascading Variables Module Level 1](https://www.w3.org/TR/css-variables-1/),” W3C By referring to the specification’s documentation, we can understand the finer nuances of native CSS variables. This module is very much a work in progress.
*   “[Use Cases for CSS Variables](https://jdsteinbach.com/css/use-cases-css-variables/),” James Steinbach Steinbach sums up the unique use cases where CSS variables can even trump preprocessor variables!

### Further Reading on SmashingMag:

*   “[A Detailed Introduction To Custom Elements](https://www.smashingmagazine.com/2014/03/introduction-to-custom-elements/),” Peter Gasston
*   “[It’s Time To Start Using CSS Custom Properties](https://www.smashingmagazine.com/2017/04/start-using-css-custom-properties/),” Serg Hospodarets
*   “[Houdini: Maybe The Most Exciting Development In CSS You’ve Never Heard Of](https://www.smashingmagazine.com/2016/03/houdini-maybe-the-most-exciting-development-in-css-youve-never-heard-of/),” Philip Walton
*   “[A Better iOS Architecture: A Deep Look At The Model-View-Controller Pattern](https://www.smashingmagazine.com/2016/05/better-architecture-for-ios-apps-model-view-controller-pattern/),” Matteo Manferdini

{{< signature "ds, jb, ml, al, nl" >}}
