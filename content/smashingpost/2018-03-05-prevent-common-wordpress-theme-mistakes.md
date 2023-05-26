---
title: 'How To Prevent Common WordPress Theme Mistakes'
slug: prevent-common-wordpress-theme-mistakes
author: nauris-pukis
image: >-
  //archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/536ea65b-96f1-4213-a2b0-d0f4a9c2687c/shutterstock-138833078-600x417.jpg
date: 2018-03-05T14:00:35+01:00
summary: >-
  When creating free or premium WordPress themes, you're bound to make mistakes. Find out how you can avoid them in order to save yourself time and focus on actually creating themes people will enjoy using!
description: >-
  When creating free or premium WordPress themes, you're bound to make mistakes. Find out how you can avoid them in order to save yourself time and focus on actually creating themes people will enjoy using!
categories:
  - WordPress
  - Themes
  - JavaScript
---
<p>If you’ve been thinking of creating free or premium WordPress themes, well, I hope I can help you avoid some of the mistakes I’ve made over the years. Even though I always strive for good clean code, there are pursuits that still somehow lead me into making mistakes. I hope that I can help you avoid them with the help of this article.</p>

## 1. Don’t Gradually Reinvent The Wheel

<p>Be careful when making things look nice &mdash; especially if you create a function that does almost exactly the same thing as another function just to wrap things nicely. The more prettifying code you add, the harder it gets to maintain. <strong>Keystrokes per minute isn’t the bottleneck of your performance as a developer</strong> when you spend most of your time <strong>thinking</strong> about code, not actually writing it.</p>

<p>I’ve made this mistake a lot thinking I was <a href="https://programmer.97things.oreilly.com/wiki/index.php/Don%27t_Repeat_Yourself">DRY</a>-ing up the code.</p>

<p>For example, I made a function called  <code>get_portfolio_part($name, $slug)</code>. Can you guess what it did? Yes. It’s a wrapper to save me the <strong>”hassle”</strong> of writing the extremely repetitive <code>get_template_part(“portfolio/$name”, $slug);</code>.  This is what I call “gradual wheel reinvention”. It does almost exactly the same thing as the original while complicating the code base at the same time.</p>

<p>Don’t do it! You don’t need to save those few keystrokes. It’s going to be difficult figuring out the actual path after a year has passed, or when someone else looks at your code. Even if you could argue that it’s simple and obvious &mdash; it’s going to either involve parsing yet another function in one's head or pure guesswork to guess where that function is fetching files from.</p>

<p>On top of saving a few characters, I remember the perfectly valid argument for making a <code>get_portfolio_part()</code> function in my head &mdash; what if I decide to move the portfolio directory in the future? I’ll have to perform an “ugly search and replace.” </p>

<p>Can you guess how many times I have changed that directory name over the years? <strong>Zero.</strong> This brings us to mistake #2.</p>

{{% feature-panel %}}

## 2. Stop Predicting The Future

<p>Humans are terrible at predicting the future. Yet, as developers, we try to do it all the time. </p>

<p>For example, imagine you’ve made an option to display social icons somewhere in your post. Let's set aside the discussion whether that’s plugin territory or not. Just imagine that this is what you’ve decided to do. So our hypothetical function would look something like this:</p>

<pre><code class="language-javascript">function has_social_icon($icon) {

    $icons = get_post_meta(get_the_ID(), 'post_social_icons', true);

    // do what has to be done with $icons

    return true;    
}
</code></pre>

<p>A very typical idea crosses my mind now: "*But what if I want to use this function outside the loop sometime in the future*?" Well, this led me to a refactor that looks like something like this:</p>

<pre><code class="language-javascript">function has_social_icon($icon, $post_id = 0) {

    if( ! $post_id ) {
        $post_id = get_the_ID();
    }

    $icons = get_post_meta($post_id, 'post_social_icons', true);

    // do what has to be done with $icons

    return true;    
}
</code></pre>

<p>And *voilà*! You’ve now created absolutely unnecessary bloat in the name of a non-existent future. This is such a simple example how these things happen, but the more complicated a thing becomes, the easier it is for you to lure yourself down a futuristic rabbit hole.</p>

<p>Don’t do it! Refactor out of real needs, not hypothetical scenarios that may or may not occur. </p>

## 3. Premature Optimization Is The Root Of All Evil

<p>Have you ever heard that quote? I didn’t give it much thought until rather recently. It’s very difficult to reform old habits, so this is something that trips me up to this day. I still catch myself optimizing code that I should not be optimizing.</p>

<p>Have you ever done something this?</p>

<div class="break-out">

<pre><code class="language-javascript">&lt;?php
$post_id = get_the_ID(); // look 'ma - I'm reusing ID, saving 1 function call!
$thumb = get_the_post_thumbnail( $post_id, 'large'); // look 'ma - I'm saving another function call! Yay!
?&gt;

&lt;div id="post-&lt;?php echo $post_id ?&gt;"

&lt;?php if( $thumb ): ?&gt;
    &lt;div class="thumbnail"&gt;
        &lt;?php echo $thumb ?&gt;
    &lt;/div&gt;
&lt;?php endif; ?&gt;

&lt;/div&gt;
</code></pre></div>

<p>Assigning a value to a variable, because you’re using that value twice is going to save you exactly .000002ms (a completely made up and useless figure), and 0ms when that request is cached, which it will be most of the time when performance is of concern anyway.</p>

<p>Here is much simpler way to write the same thing <strong>the WordPress way</strong>:</p>

<pre><code class="language-javascript">&lt;div id="post-&lt;?php the_ID() ?&gt;"

&lt;?php if( has_post_thumbnail() ): ?&gt;
    &lt;div class="thumbnail"&gt;
        &lt;?php the_post_thumbnail('large') ?&gt;
    &lt;/div&gt;
&lt;?php endif; ?&gt;

&lt;/div&gt;
</code></pre>

<p>Yes, it involves two extra function calls, but the code performance benefit is negligible. That doesn't meant that you shouldn't optimize your code at all. Be intelligent about it. If you're saving database queries, or you're running expensive functions in a loop - of course you should keep your code optimized. But do it intelligently. Don't throw everything in a variable just to save a function call. Speaking of variables...<p>

## 4. Avoid Variables In Template Files</h2>

<p>When you stop trying to over-optimize, you should notice considerably fewer variables in your template files. I recommend that you take that idea a step further and try to avoid variables in template files in general. Not because you should avoid variables themselves, but because of what they’re a symptom of in template files &mdash; logic. </p>

<p>While some logic will always be necessary, you can improve the readability of your template files significantly by removing as much as you can. </p>

<p>Here is a simple example.</p>

<div class="break-out">

<pre><code class="language-javascript">&lt;?php
$logo_url = false;
$thumbnail_url = wp_get_attachment_image_src( get_theme_mod( 'hypthetical_theme_logo' ), 'full' );
if( $thumbnail_url ) {
    $logo_url = $thumbnail_url[0];    
}
?&gt;
&lt;?php if( $logo_url ): ?&gt;
    &lt;a href="&lt;?php echo esc_url( home_url() ); ?&gt;" title="&lt;?php bloginfo( 'name' ); ?&gt;" class="custom-logo"&gt;
        &lt;img src="&lt;?php echo $logo_url; ?&gt;" /&gt;
    &lt;/a&gt;
&lt;?php endif; ?&gt;
</code></pre></div>

<p>All by itself, this may not look terrible, but when it’s somewhere inside your `header.php` file, it’s going to look quite messy, especially when wrapped in multiple divs with indentation.</p>

<p>On top of it not looking great, why should the template (or the person reading the code) be concerned of how the logo is retrieved? Template files just want to show content, not fetch and parse the content.</p>

<p>Instead of defining two variables, why not extract them away into functions? Then the code above can easily turn into this:</p>

<div class="break-out">

<pre><code class="language-javascript">&lt;?php if( hypotheme_has_logo() ): ?&gt;
    &lt;a href="&lt;?php echo esc_url( home_url() ); ?&gt;" title="&lt;?php bloginfo( 'name' ); ?&gt;" class="custom-logo"&gt;
        &lt;img src="&lt;?php hypotheme_the_logo_url() ?&gt;" /&gt;
    &lt;/a&gt;
&lt;?php endif; ?&gt;
</code></pre></div>

<p>This is much, much easier to read and avoids any unnecessary clutter and in case someone wants to know where the logo comes from &mdash; they can inspect the function instead. Now the logic is separate from the presentation.</p>

<p>Here is another example:</p>

<div class="break-out">

<pre><code class="language-javascript">&lt;?php
/**
 * page.php
 */
?&gt;
&lt;?php get_header(); ?&gt;

&lt;?php
$hypotheme_sidebar      = hypotheme_get_option( 'hypotheme_sidebar' );
$hypotheme_sidebar_size = hypotheme_get_option( 'hypotheme_sidebar_size' );
?&gt;

&lt;?php while ( have_posts() ) : the_post(); ?&gt;

    &lt;div class="row two-columns"&gt;

    &lt;?php if ( $hypotheme_sidebar == 1 ): ?&gt;
        &lt;div class="main-column &lt;?php if ( $hypotheme_sidebar_size == 0 ) { ?&gt; col-md-6 &lt;?php } else { ?&gt; col-md-7 &lt;?php } ?&gt;"&gt;
    &lt;?php else: ?&gt;
        &lt;div class="main-column col-md-12"&gt;
    &lt;?php endif; ?&gt;

    &lt;div id="page-&lt;?php the_ID(); ?&gt;" &lt;?php post_class( 'entry-page' ); ?&gt;&gt;
        &lt;h1 class="entry-title"&gt;&lt;?php the_title(); ?&gt;&lt;/h1&gt;
        &lt;div class="entry-content"&gt;&lt;?php the_content(); ?&gt;&lt;/div&gt;
    &lt;/div&gt;

    &lt;?php if ( comments_open() ) : ?&gt;
        &lt;?php comments_template(); ?&gt;
    &lt;?php endif; ?&gt;

    &lt;/div&gt;

    &lt;?php if ( $hypotheme_sidebar == 1 ) {
        get_sidebar();
    } ?&gt;

    &lt;/div&gt;

&lt;?php endwhile; ?&gt;
&lt;?php get_footer(); ?&gt;
</code></pre></div>

<p>Look at those variables. On their own they’re not really out of place &mdash; they’re doing what they should be doing.</p>

<p>However, this template probably isn’t the only template in this theme with a sidebar. That means that those variables are probably present in all template files where there is a sidebar.</p>

<p>Not only the logic is mixed with the presentation, but it is also repeated all over the template files ( page.php, single.php, index.php, etc. ). That’s a lot of repetition, a lot of code that can be removed easily:</p>

<div class="break-out">

<pre><code class="language-javascript">&lt;?php
/**
 * page.php
 */
?&gt;
&lt;?php get_header(); ?&gt;

&lt;?php while ( have_posts() ) : the_post(); ?&gt;

    &lt;div class="row two-columns"&gt;

        &lt;div class="main-column &lt;?php echo hypotheme_container_width_class() ?&gt;"&gt;
            &lt;div id="page-&lt;?php the_ID(); ?&gt;" &lt;?php post_class( 'entry-page' ); ?&gt;&gt;
                &lt;h1 class="entry-title"&gt;&lt;?php the_title(); ?&gt;&lt;/h1&gt;
                &lt;div class="entry-content"&gt;&lt;?php the_content(); ?&gt;&lt;/div&gt;
            &lt;/div&gt;

            &lt;?php if ( comments_open() ) : ?&gt;
                &lt;?php comments_template(); ?&gt;
            &lt;?php endif; ?&gt;

        &lt;/div&gt;

        &lt;?php get_sidebar(); ?&gt;

    &lt;/div&gt;

&lt;?php endwhile; ?&gt;
&lt;?php get_footer(); ?&gt;
</code></pre></div>

<p class="c-pre-sidenote--left">This is way easier to read and understand. The reader doesn’t have to care about how you decide how wide is the container, yet if they’re interested &mdash; in most code editors you can quickly jump to that function and read all about it. Functions help make your code more readable and extendable if used in conjunction with either <a href="https://developer.wordpress.org/plugins/hooks/custom-hooks/">WordPress Hooks</a> or the <a href="https://code.tutsplus.com/tutorials/a-guide-to-overriding-parent-theme-functions-in-your-child-theme--cms-22623">Pluggable Functions</a> pattern.</p><p class="c-sidenote c-sidenote--right">Don’t be afraid to create multiple files where you can store all your necessary template functions, i.e. don’t dump everything inside <code>functions.php</code>. By default, <a href="https://github.com/Automattic/_s">_s theme</a> includes <code>/inc/template-tags.php</code> file for that purpose. And if you find that the file becomes too large with all of the new template tags you’ve created, you can create more files as needed. It’s your theme after all!</p>

<h3>5. Make Sure You’re Up To Date

<p>WordPress is constantly evolving, just as everything else on the internet. Stay up to date with best practices, and question yourself every now and then, and also make sure you’re still using best practices.</p>

<p>For example, I’ve seen themes released on <a href="https://WordPress.org">WordPress.org</a> this year, that are still using <code>wp_print_styles</code> instead of <code>wp_enqueue_scripts</code>, even though <code>wp_print_styles</code> has been <a href="https://codex.wordpress.org/Plugin_API/Action_Reference/wp_print_styles">deprecated since WordPress version 3.3</a>.</p>

<p>If you’re building WordPress themes for others to use, keep up to date with best practices, and check the codex every now and then to see whether the way you’re doing something is still the best way to do it.</p>

## 6. Use Native WordPress Functions When You Can

<p>It’s important to use native <a href="https://codex.wordpress.org/Function_Reference">WordPress functions</a> when possible so that others can tap into your theme, either from a plugin or a child theme.</p>

<p>When you’re up to date with the latest and greatest that WordPress has to offer, you might discover that the example “Mistake # 4” can be completely replaced with native WordPress functions since WordPress version 4.5 because WordPress now supports <a href="https://developer.wordpress.org/themes/functionality/custom-logo/">Custom Logo</a> functionality natively.</p>

<div class="break-out">

<pre><code class="language-javascript">&lt;?php if( has_custom_logo() ): ?&gt;
    &lt;a href="&lt;?php echo esc_url( home_url() ); ?&gt;" title="&lt;?php bloginfo( 'name' ); ?&gt;" class="custom-logo"&gt;
        &lt;img src="&lt;?php the_custom_logo() ?&gt;" /&gt;
    &lt;/a&gt;
&lt;?php endif; ?&gt;
</code></pre></div>

<p>Here is another example.</p>

<p>When designing a nice post-to-post navigation without really giving it too much thought I resorted to using  <a href="https://codex.wordpress.org/Function_Reference/get_next_post">get_next_post</a> function and copy-pasted something like this in my theme:</p>

<div class="break-out">

<pre><code class="language-javascript">&lt;?php
$next_post = get_next_post();
if (!get_next_post()): ?&gt;
  &lt;a href="&lt;?php echo esc_url( get_permalink( $next_post-&gt;ID ) ); ?&gt;"&gt;&lt;?php echo esc_attr( $next_post-&gt;post_title ); ?&gt;&lt;/a&gt;
&lt;?php endif; ?&gt;
</code></pre></div>

<p>Sweet! The internet just wrote some code for me!  This is exactly what I needed.  </p>

<p>What’s wrong with this? Well, several things.</p>

<p>First of all, don’t access object properties directly when possible, unless you’re sure you have to. In this case, you can use <a href="https://developer.wordpress.org/reference/functions/get_the_title/">get_the_title()</a> function instead. This way you will properly retrieve the title, prepend “Private/Protected" and apply  <code class='code-inline'>the_title</code> filter.</p>

<pre><code class="language-javascript">// do this
echo get_the_title( $next_post )

// instead of this:
echo $next_post-&gt;post_title
</code></pre>

<p>And secondly, there is a WordPress function called <a href="https://codex.wordpress.org/Function_Reference/next_post_link">next post link</a> and you can replace everything above with just a simple function call:</p>

<pre><code class="language-javascript">&lt;?php next_post_link() ?&gt;</code></pre>

<p>Again, some research and staying up to date can help clean up themes significantly. </p>

## 7. Don’t Build Your Own Framework

<p>When I write code, I want it to be DRY, with a clean interface, reusable, and performant. I think ultimately we all want that.</p>

<p>When all those ambitions are combined with a sprinkle over premature optimization, a dash of future prediction, ignoring a native WordPress function or two, and the desire to save on a few keystrokes, that's when "<strong>a framework for me by me</strong>" is born.</p>

<p class="c-pre-sidenote--left">As the saying goes, "The road to hell is paved with good intentions." In my almost five years of theme development, I’ve built a “solid framework” for myself at least twice and refactored them countless times. Now, I wish I could strip it all away in one fell swoop. Don’t do it! Spare your future self!</p><p class="c-sidenote c-sidenote--right">I’m against building "a framework for my by me," not frameworks in general. There are well supported and maintained frameworks out there, like the Genesis theme or Sage by Roots. But they are not in the "a framework by me for me" format.</p>

<p>Here are a few problems and side effects of building a framework for yourself:</p>

### Maintainability Issues

<p>The first problem is that building a “framework” is just adding an additional codebase to maintain. Especially if the framework lives in your <code>/inc/me-framework</code> directory, you will have to update all your themes using that framework when you release an update to it.</p>

<p>If you decide not to update your framework in each theme every time you update it, there is still trouble lurking around the corner.</p>

<p>As you grow as a developer, your framework will grow and change, too. Eventually leading to incompatibility with your old themes. What if you discover a critical bug in older framework versions? You’ll have to either rewrite parts of all themes you’ve made or make a very special bug-fixed fork. And again: more code to maintain.</p>

### Plugin Territory

<p>If you find yourself adding “custom functionality” in the theme, you might want to <a href="https://tommcfarlin.com/wordpress-theme-or-plugin/">create a WordPress plugin instead</a>. Themes should make pretty layouts and style them. Theme files should be filled with configuration, attaching to hooks and using template tags that either plugins or WordPress core provide. If you feel the need for using PHP Classes, you’re probably venturing into the plugin territory.</p>

<p>Make a plugin instead; make it easily customizable and style it in your theme. Not only you will avoid making a framework, but you’ll also contribute to back to the open-source community!</p>

### Increased Complexity

<p>When you build a framework for yourself you’re making your theme more complex and difficult to work with. When someone reads your theme code, they’ll have to learn your framework that’s most likely either poorly documented or undocumented at all.</p>

## Conclusion

<p>I have come to realize that most of the mistakes I’ve made have been caused by either the desire to save time in the future (<a href="https://xkcd.com/1205/">xkcd has a wonderful comic about that</a>) or to improve the code itself in some way, either by following a best practice that I’ve read somewhere or making the code look nicer.</p>

<p>WordPress has its own <a href="https://make.wordpress.org/core/handbook/best-practices/coding-standards/php/">coding and theming standards</a>. While you can write PHP the way you want to in your template files, it’s best to actually stick to “the WordPress way,” even if it’s not necessarily “the best way.” Remember that “best” is relative to the audience.  <em>When in Rome, do as the Romans do.</em></p>

<p>So please, don’t repeat my mistakes. I truly hope that this article will help you create great WordPress themes!</p>

{{< signature "mc, ra, yk, il" >}}

