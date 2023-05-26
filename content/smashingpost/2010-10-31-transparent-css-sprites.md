---
title: Transparent CSS Sprites
slug: transparent-css-sprites
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/76e11311-7cfd-4bd3-8a3e-03c479b2fdad/bodycss.jpg
date: 2010-10-31T08:09:38.000Z
author: trevor-morris
description: >-
  CSS Sprites are a relatively simple technique once you understand the fundamentals and it can be applied in all manner of ways. A common use is for a graphic intensive navigation, but it can also be useful for buttons or even styling headings with the corporate font.
categories:
  - Coding
  - CSS
  - Techniques
---
Sprites are simply a collection of images which are merged together to create a single file. You then use CSS, changing the <code>background-position</code> the image, to display the correct part of the image you need. I often use the analogy of a large object passing a window — you only see what is within the frame.

Over the last couple of years CSS Sprites has been one of the most widely adopted CSS-related techniques. Popularised by the Yahoo’s research and documentation around <a href="https://developer.yahoo.com/performance/">speeding up your website</a>, many high profile websites implement the technique, including Google and Amazon. There are <a href="https://www.smashingmagazine.com/2009/04/27/the-mystery-of-css-sprites-techniques-tools-and-tutorials/">numerous tutorials</a> which help you get to grips with the techniques and <a href="https://spritegen.website-performance.org/">sprite generators</a> which help you create the graphics themselves.</p>

## The Benefits and Potential Problems

CSS Sprites have become a de-facto way of improving the speed of your website or web application. Merging multiple images in to a single file can quickly reduce the number of HTTP requests needed on a typical website. Most browsers only allow for two concurrent connections to a single domain so although individual files can be large, the overall request and response times are considerably lower. Combining images with similar hues also means the colour and compression information is only need once, instead of per file, which can mean an overall reduced file size when compared to the files individually.

{{% feature-panel %}}

The benefits of reduced file size and HTTP requests are often publicised, but potential problems are rarely ever discussed. One of the main techinical issues with CSS Sprites is memory usage which is explained in the article “To Sprite Or Not To Sprite”. Another issue is the maintenance of the sprites, the images and the CSS, both of which can become rather complicated.</p>

## A Technological Solution

A common practice in solving slow-down in computing seems to simply <strong>throw in more hardware</strong>. We all know hardware prices are dropping all the time, so this seems like a reasonable solution. However, I feel there is a fundamental flaw with this philosophy and ingrained mentality. Developers have access to more computing power and as such they code their applications to be handled in these environments. With each new feature the application becomes slower and slower, but this problem has already has a solution &mdash; upgrade your hardware. <em>This is an endless cycle</em>.

Many of the user interfaces people come across today are on the Web. This means the user has to download most of the related material (images, CSS, JavaScript) before interacting with the content, so the same philosophy must be applied to the Web. Websites, or more recently web applications, are becoming more complex, even replacing many desktop applications, therefore the user must first download more and more information before beginning their experience.

Although file sizes required to view a website have increased dramatically over recent years, more and more people are upgrading their Internet connections, with broadband becoming the norm in many countries. This cycle conforms to the hardware upgrade philosophy and in theory should negate any potential user experience problems.

However, web developers are falling in to the same trap which many application developers have before. As layouts become more complex, more images are required and so the developer creates more images &mdash;  even if they are sprites. This seems like a reasonable assertion, but it doesn’t mean it is the best solution.</p>

## A Twist on the Technique

Due to the limitations of the Web, there have been many inventive solutions to problems. But the Web isn’t the only place where there can be very tight limitations. Innovation strives on limitation. A great example of this was in the iconic game <a href="https://www.neogaf.com/forum/showpost.php?p=9490699&amp;postcount=70">Super Mario Brothers where the bushes were just recoloured clouds</a>.

This very simple but extremely effective implementation made me think about how to reuse common interface elements, trick the user to believe something the same is different!

Now on to the twist, this idea is to <strong>create a transparent sprite</strong> allowing the <code>background-color</code> to show through. If you are familiar with CSS Sprites, you should be able to grasp this twist relatively easily.

Simply, an image with a transparent “knocked-out” transparent center is placed over a background colour. Changing the background colour changes the appearance of the element. The only thing you need to pay attention to is that the colour surrounding the transparent part of the image matches the background in which you are using the techinque. This stops the background colour bleeding in to other parts of your image.

Anyway, this technique is much easier to understand in an example…

## Example

The following example is only made up of three images. One for all the font samples, one image for both sets of droplets, including hover and active states, and one for the all buttons.

<div id="example">
	<div class="colours">
		<ul>
			<li class="c_000000 active"><a href="?hex=000000" title="Black">Black</a></li>
			<li class="c_c4c4c4"><a href="?hex=c4c4c4" title="Grey">Grey</a></li>
			<li class="c_ea1d22"><a href="?hex=ea1d22" title="Red">Red</a></li>
			<li class="c_309721"><a href="?hex=309721" title="Green">Green</a></li>
			<li class="c_005aa9 l"><a href="?hex=005aa9" title="Blue">Blue</a></li>
		</ul>
	</div>

	<p class="font c_000000">Font examples</p>

	<ul class="buttons c_000000">
		<li><a href="#">Add</a></li>
		<li><a href="#">Update</a></li>
		<li><a href="#">Delete</a></li>
		<li><a href="#">Enable</a></li>
		<li><a href="#">Disable</a></li>
	</ul>

	<div class="colours white">
		<ul>
			<li class="c_000000 active"><a href="?hex=000000" title="Black">Black</a></li>
			<li class="c_c4c4c4"><a href="?hex=c4c4c4" title="Grey">Grey</a></li>
			<li class="c_ea1d22"><a href="?hex=ea1d22" title="Red">Red</a></li>
			<li class="c_309721"><a href="?hex=309721" title="Green">Green</a></li>
			<li class="c_005aa9 l"><a href="?hex=005aa9" title="Blue">Blue</a></li>
		</ul>
	</div>
</div>

### The Images

<p><strong>Fonts</strong><br />The font image contains transparent typefaces on a white background, meaning they aren't viewable on a white background. <a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/19252f08-2ce2-4022-954b-212e3f55d33f/transparent-sprite-fonts.png">Save the file from the example</a>, open it in your favourite graphics editor and you will see the transparent typefaces.

<p><strong>Drops</strong><br />The drops image is used on the example above as the colour picker. A single graphic containing the gradient drop on the two different backgrounds, so the <code>background-color</code> is masked out correctly. The image contains all three states used in modern interactive interfaces — static, hover/focus, pressed/active.

<p><strong>Button</strong><br />The button technique is the most flexible and probably most useful way to use this technique. A simple sprite image containing two states — static and hover/focus — which is then placed over text to create the button. Simply adding a <code>background-color</code> will make every use of this button the same style across your application or website.

Below is some CSS which styles simple fixed width buttons with a grey background colour, but also has two different treatments, "warning" and "go", which have red and green background colours respectively.

<pre><code class="language-css">a.button {
  display: block;
  width: 80px; height: 30px;
  margin: 0 20px;
  font-size: 14px; line-height: 30px; color: #fff;
  text-align: center; text-decoration: none;
  background: #4a4a4a url(button.png) no-repeat 0 0;
}
a.button:hover,
a.button:focus,
a.button:active {
  background-position: 0 -40px;
}
a.button.warning {
  background-color: #ea1d22;
}
a.button.go {
  background-color: #309721;
}</code></pre>

<p>The CSS above produces the following buttons:</p>

<ul id="button-example">
	<li><a class="button" href="#">Normal</a></li>
	<li><a class="button" href="#">Button</a></li>
	<li><a class="button go" href="#">Continue</a></li>
	<li><a class="button go" href="#">Go!</a></li>
	<li><a class="button warning" href="#">Stop!</a></li>
</ul>

## Conclusion

This techinque could be useful when providing a range of themes for a website. You could create one set of buttons and icons then add the background colour which best suits the selected theme.

Although this technique will never be as broadly useful as the original CSS Sprites, the idea can be useful for websites which allow user theming. The technique could also be used when creating HTML mockups, allowing you to easily update colours based on client feedback.

The main benefit this technique has is that it reduces the number of HTTP requests. But it also reduces browser memory usage compared with what would be needed if you created a larger sprite to handle all the colours you need.

I would like to mention one caveat though, IE6, because it does not natively support transparent PNGs. There are PNG fixes, but none<sup>1</sup> of these support <code>background-position</code> which is needed if you are using this technique with CSS sprites, such as with the buttons and droplets above. However, you could provide a slightly less optimal experience using GIFs instead.
<p class="footnote">1. The <a href="https://www.twinhelix.com/css/iepngfix/">IE PNG Fix from TwinHelix</a> <em>does</em> include support for <code>background-position</code>, but the solution requires JavaScript.</p>

### Further Resources
If you are interested in any aspect of CSS Sprites, check out the following extra resources.
<ul>
	<li><a href="https://wellstyled.com/css-nopreload-rollovers.html">Fast Rollovers Without Preload</a> – the initial inspiration for CSS Sprites.</li>
	<li><a href="https://spriteme.org/">SpriteMe</a> – a bookmarklet to generate sprites based on an existing website.</li>
</ul>
Below are a list of links used within the article:
<ul>
	<li><a href="https://www.alistapart.com/articles/sprites">CSS Sprites: Image Slicing’s Kiss of Death</a> – the A List Apart article by Dave Shea.</li>
	<li><a href="https://developer.yahoo.com/performance/">Yahoo! Performance Guideliness</a> – best practices, tools and research from Yahoo!</li>
	<li><a href="https://spritegen.website-performance.org/">CSS Sprite Generator</a> – a tool to help you create your sprites by Ed Eliot.</li>
	<li>To Sprite Or Not To Sprite – an article about some potential system performance caveats with sprites.</li>
</ul>

<style type="text/css">
#example .colours ul li a,
#example p.font {
	display: block; overflow: hidden;
	font-size: 0.0; line-height: 0.0;
	text-decoration: none; text-indent: -9999px;
	background: transparent no-repeat 0 0;
	border: 0;
}
#example .colours {
	padding: 5px 20px; margin: 0 auto 10px;
	background-color: #353535;
}
#example .white {
	background-color: #fff;
}
#example .colours ul {
	overflow: hidden;
	width: 180px;
	padding: 0; margin: 0 auto;
	list-style: none;
}
#example .colours ul li {
	float: left;
	width: 28px;
	margin: 7px 10px 0 0; padding: 0;
}
#example .colours ul li.l {
	margin-right: 0;
}
#example .colours ul li a {
	height: 40px;
	background: url(https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/99d28411-371c-466d-a940-f07f0661f079/transparent-sprite-drops1.png) no-repeat -10px -10px;
}
#example .colours ul li a:hover,
#example .colours ul li a:focus {
	background-position: -10px -50px;
}
#example .colours ul li.active a,
#example .colours ul li a:active {
	background-position: -10px -90px;
}
#example .white {
	padding-top: 0;
}
#example .white ul li a {
	background-position: -60px -3px;
}
#example .white ul li a:hover,
#example .white ul li a:focus {
	background-position: -60px -50px;
}
#example .white ul li.active a,
#example .white ul li a:active {
	background-position: -60px -90px;
}
#example p.font {
	height: 157px; width: 330px;
	margin: 0 auto;
	background: url(https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/19252f08-2ce2-4022-954b-212e3f55d33f/transparent-sprite-fonts.png) no-repeat 0 0;
}
#example .buttons,
#button-example {
	overflow: hidden;
	width: 610px;
	margin: 10px auto; padding: 0;
	list-style: none;
}
#example .buttons li,
#button-example li {
	float: left;
}
#example .buttons li a,
a.button {
	display: block;
	width: 80px; height: 30px;
	margin: 0 20px;
	font-size: 14px; line-height: 30px; color: #fff;
	text-align: center; text-decoration: none;
	background: url(https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5e085b7b-921e-4120-9504-479fbbb35cca/transparent-sprite-button.png) no-repeat 0 0;
}
#example .buttons li a:hover,
#example .buttons li a:focus,
#example .buttons li a:active,
a.button:hover,
a.button:focus,
a.button:active {
	background-position: 0 -40px;
}
a.button,
a.button:hover,
a.button:focus,
a.button:active {
	color: #fff;
	background-color: #4a4a4a;
}
a.button.warning,
a.button.warning:hover,
a.button.warning:focus,
a.button.warning:active {
	background-color: #ea1d22;
}
a.button.go,
a.button.go:hover,
a.button.go:focus,
a.button.go:active {
	background-color: #309721;
}
p.footnote {
	padding: 0 100px 0 16px;
	color: #888; text-indent: -16px;
}
p.footnote,
p.footnote code {
	font-size: 11px;
}	
#example p.c_000000,
#example li.c_000000,
#example ul.c_000000 li a {
	background-color: #000000;
}
#example p.c_c4c4c4,
#example li.c_c4c4c4,
#example ul.c_c4c4c4 li a {
	background-color: #c4c4c4;
}
#example p.c_ea1d22,
#example li.c_ea1d22,
#example ul.c_ea1d22 li a {
	background-color: #ea1d22;
}
#example p.c_309721,
#example li.c_309721,
#example ul.c_309721 li a {
	background-color: #309721;
}
#example p.c_005aa9,
#example li.c_005aa9,
#example ul.c_005aa9 li a {
	background-color: #005aa9;
}
</style>

<script type="text/javascript" src="https://ajax.googleapis.com/ajax/libs/jquery/1.4.2/jquery.min.js"></script>

<script type="text/javascript">
if(typeof jQuery !== 'undefined') {
	//jQuery.noConflict();
	jQuery(document).ready(function($) {
		var $example	= $('#example, #button-example'),
			$font		= $('#example p.font'),
			$buttons	= $('#example ul.buttons');
		$example.bind('click', function(event){
			var $$, $li, $ul, data, href, hex;
			$$		= $(event.target);
			$li		= $$.parents('li:first');
			$ul		= $$.parents('ul:first');
			data	= {
				active:	'active',
				prefix:	'c_'
			};
			if($$.length === 1) {
				if($ul.parent().is('.colours')) {
					href	= $$.attr('href');
					hex		= href.replace('?hex=', '');
					$('a[href=' + href + ']').parents('li').addClass(data.active).siblings().removeClass(data.active);
					$font.removeClass().addClass('font').addClass(data.prefix + hex);
					$buttons.removeClass().addClass('buttons').addClass(data.prefix + hex);
				}
				$$.blur();
				event.preventDefault();
			}
		});
	});
}
</script>

