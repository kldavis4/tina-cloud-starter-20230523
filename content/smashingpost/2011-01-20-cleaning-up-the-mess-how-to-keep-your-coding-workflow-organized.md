---
title: 'How To Keep Your Coding Workflow Organized'
slug: cleaning-up-the-mess-how-to-keep-your-coding-workflow-organized
image: https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a346cc7a-e1c5-413b-ba17-9ab1079e40cc/javascript-image.jpg
date: 2011-01-20T00:09:29.000Z
author: bryan-hoyt
summary: >-
  Oops, we used the word "organized" in the title. Time to switch off &mdash; is probably what many would think. Being organized is a somewhat dull, though important, subject. Perhaps it would help to give it a bit of context.
description: >-
  If your templates or code don't allow you to organize your files the way you need to, then do a quick code refactoring to make it work.
categories:
  - Coding
  - Workflow
  - JavaScript
---

Let’s keep it classy, and **imagine we’re building a website for a trendy restaurant/café** called "bEat", catering to the arts community. It’s an atmospheric place with 1920’s art on its interior brick walls, live jazz, and rich patrons. But they don’t have a great website, so they’ve called you in to save the day. As a talented designer, you’re confident you’ll be able to pull a fantastic design together that they’ll love, but they’ve got a lot of clever ideas about the website’s functionality, and you’re not quite so confident about how to organize all the files that your website will need.

They need to be able to edit content themselves, upload pictures for their weekly blog posts and new content. Pretty normal so far. They also need to hook in with Twitter, so their blog posts are automatically tweeted. They need a mobile app for iPhone and Android, because their customers are using a smartphone, and they want to offer specials &amp; menus direct to their smartphones. Down the track, they’d like to have reviews submitted by their customers, with possible pictures, links, etc. Lots of cool interactive social networky stuff, friends, online user-submitted video.

*‘Facebook for restaurants’* they say, by way of making it easier for you to get your head around. Ok, by that stage, you’d probably tell them to go waste someone else’s time. But you get the idea.

Perhaps in the past you’ve tried to build a more complex, cutting-edge website like this, and the project started off with great enthusiasm, but ended up in a nightmarish mess that you couldn’t maintain. Your client lost interest when new features started getting too hard to add, and you started having to work late at night, tracking down bugs that you couldn’t even find the relevant file for.

After a project like that, it’s not hard to see the relevance of a well-organized website project.

## General Principles

Keep everything simple and clear. Don’t over-organize &mdash; some websites &amp; frameworks out there seem to have a masochistic need to make everything a theoretically perfect abstraction. In practical terms, that usually means it’s impossible to work with.

If you start creating tens (or hundreds) of tiny files, each containing nothing more than a small class or function, you’re definitely overdoing it. If your files and folders have names that are too abstract or generic, then things are probably starting to get a bit silly. For example, if the code to check the login for a website administrator is stored in a file called <code>WebsiteData/Items/GenericUser/AdminUser/Code/Auth.php</code> then you’ve committed both sins. Why not just a function called <code>check_login()</code> in the file <code>code/users.php</code>?

Don’t mix different aspects of your website. Keep modules of functionality separate, and keep different languages in separate files. I’ve recently helped out on a project where some poor, misguided programmer mixed <a title="12 Principles For Keeping Your Code Clean" href="https://www.smashingmagazine.com/2008/11/12-principles-for-keeping-your-code-clean/">CSS</a>, ASP VB Script, JavaScript, HTML and SQL in a big jumble, all throughout a single, huge, poorly indented file. I’m not exaggerating. Enough said.

## One Size Does Not Fit All

The depth of your folder hierarchy and the number of individual files should make sense for the size of the website. Keep it in perspective.

Here’s a quick list of some typical approximate website sizes, and how you might structure things accordingly.

*   **1 page website**.  Make a folder for images, a single file for CSS, another for JavaScript, another for content, and another single file for code. It’s definitely not worth separating template and content, unless you have specific requirements.
*   **5 pages website**.  A folder for images, one file for CSS, JS, code. Consider putting your content files in a separate folder. Again, not much need for templates here, usually. By this stage, make sure you have a template for the header and footer of your page (and any other common elements on all the pages).
*   **20 pages website**.  A folder for images, another folder for uploads and other business-related files ("assets"), another folder for content (or you might be using a database-based CMS by this stage). Your JavaScript, code, and stylesheets are probably getting complex enough by this stage to consider putting them in a separate folder. Name the folders something immediately obvious, e.g. `css/`, `javascript/`, `code/`.Make sure that _all_ files go into their relevant folders. You shouldn’t have a stray .js file sitting, say, in the `content/` folder, just because it’s convenient. If your templates or code don’t allow you to organize your files the way you need to, then do a quick code refactoring to make it work.Avoid putting CSS, templates, layout and design images, or JavaScript into `assets/` (or `uploads/` or `resources/`, depending on what you call it). These files are effectively code that your client should never have to think about, and the `assets/` folder is for business-related files and media. Make it a golden rule for your workflow and stick to it.
*   **20 pages web application**.  Much as above, but by this stage you should _definitely_ be putting all your code in a separate folder. Make sure it’s not inside a folder where Apache might accidentally serve up the plain files when some script-kiddie has a tinker.
*   **100 pages website**.  You should be using a good CMS for your content by this stage. It doesn’t matter if it’s a database- or file-based CMS, but if it’s the latter, make sure the content files are well-organized, and make sure you can define metadata for individual page titles, descriptions, etc, or your SEO efforts will be very difficult. You’re probably also starting to have a number of different sections on your website by now. You’ll likely need to start factoring out the stylesheets, JavaScript, design images and templates into separate files and folders. Make sure these folders match each other, and match up with the sections of your website &mdash; or whatever makes most sense for your particular website. Using a CSS language like [Sass](https://sass-lang.com) or [LESS](https://lesscss.org/) is also a really good idea by this stage.
*   **2,500+ pages website**.  You should definitely think about hiring some people dedicated to certain aspects of the website, such as a content editor, designer, programmer and SEO expert. You’ll also want your content to be in a database-based CMS by this stage, if it’s not already. You’ll start being the manager, and having the bulk of the work done by other people. Make sure you have smooth-running systems in place to allow you to review their work, and edit it before it goes live.
*   **100,000,000+ pages website**.  You’re Microsoft. You should know what you’re doing by now.

Most small websites very quickly grow to over 20 pages, if they’re being actively maintained &mdash; by the time you’ve added a couple FAQ pages, a few little tidbits of content to explain something in more depth, and a product or two, it adds up quickly.

In that light, consider making all your small websites structured like an (approximately) 20-page website, unless you know the project is a quick, one-off website, such as an information site for an upcoming event, or a page for your wife’s birthday. Plan for growth, but don’t plan for a <a href="https://davidcummings.org/2010/12/19/hockey-stick-growth-for-startups/">hockey-stick growth curve</a>.

{{% feature-panel %}}

## Your Client

You should have a folder for each customer, unrelated to the actual project you’re working on for them. Inside this folder, you’ll have a folder for each project. Initially, there’ll just be a folder called <code>website/</code>, but before long, you might have other folders called <code>logo/</code>, <code>reports/</code>, <code>competitive analysis/</code>, etc. It also makes sense to put your design files in this folder, perhaps in <code>design/</code> or <code>graphics/</code>.

Don’t make this folder accessible by Apache. It *will* contain sensitive information.

Depending on the framework you use, you might like to put the code in this folder, to keep it outside of your website folder. You could call it <code>code/</code>, or, if you think there’ll be separate code for other projects, <code>website-code/</code>. If most of your other projects are design or business-related, then they probably won’t have any code, other than the odd script which wouldn’t need a separate folder.

In addition to the customer’s work folder, you might like to have a completely separate folder for documents that you *don’t* want your customer to see. You might find yourself regularly sharing work-related documents with your customer, and it’s quite likely that at some point you’ll want to give them access to their whole folder (and some customers will ask for it: "Can you zip up all my files and send them through? I just want to make sure I have a copy of everything"). Rather than risk accidentally sending them the file "10 things I hate about these guys.doc", put it in your customer’s private folder.

To recap quickly, here’s an example of structure we’re currently looking at:

<div class="break-out">

 <pre><code class="language-markup">YourBusiness/
  Accounts/
  Documents/
  Customers/
    bEat/
      Minutes/
      10 things I hate about these guys.doc
      Proposal.doc
    CustomerProjects/
      bEat/
        website/
            ... this is the bit we’ll be discussing ....
        code/
            ... and this ...
        reports/
        graphics/
</code></pre>
</div>

## So, What’s In A Website Like This?

From here on in, we’re talking about the "code/" and "website/" folders listed above.

### Images

There are (almost always) two sorts of images: those that are part of the design, and those that are part of the content provided on the website. The latter should go into your assets (or uploads or media) folder, perhaps in a <code>pictures/</code> subdirectory. For design images, you’ll rarely need to stray from the beaten path: put them all inside <code>images/</code>.

If your design is a little more complex, you might have images for buttons, icons, navigation, page background, etc. In that case, you’ll quickly get above 10 or 20 images in this folder, so consider breaking it up into subfolders. It’s still fine to have general-purpose images in the top-level, but the subfolders will help to keep control of all your zillions of little files. Name the files sensible, easy-to-remember names like <code>form-warning-icon.png</code>.

### Stylesheets

For most sites, your stylesheets don’t need to get very large. For a small site, or even a larger site, without many different sections (each with a different design), you’ll often get away with only one file for your CSS. If this is the case, just name it <code>main.css</code>, or <code>styles.css</code>.

Even so, a lot of people like to break their stylesheets up into multiple files. There are different ways to do this. A popular option is one stylesheet for layout, another for typography, another for colors. This is a nice idea, but it gets tricky to manage in practice &mdash; you end up defining many of your classes 3 (or more) times, and tracking down bugs can be a nightmare.

I believe a better option is to separate out "layout" and "content" styles. "Layout" includes things like navigation, header &amp; footer, sidebars, boxes, sections. "Content" includes things like paragraphs, headings, blockquotes, lists, floating images, links. If you carry this a bit further, it also makes sense to have a file for "forms" styles. However, as content on the web becomes much more interactive, the line between forms and content (no pun intended!) is quickly being blurred.

Again, call a spade a spade, and name these files <code>layout.css</code>, <code>content.css</code> and <code>forms.css</code>. If you give them somewhat vague names like <code>presentation.css</code>, <code>model.css</code>, <code>page.css</code>, you’ll always have to think first before deciding what file to look in.

Sometimes it’s useful to have an individual CSS file for special pages that have their own design requirements. This can be more trouble than it’s worth, depending on the complexity of the page. If you find yourself flicking between tabs in your editor, trying to find the right CSS file for a particular element, then it might be better to simplify your CSS. Also, seriously consider using <a href="https://sass-lang.com/">Sass</a> or <a href="https://lesscss.org/">LESS</a> to make your CSS much more beautiful and clean.

You probably also will have separate stylesheets for different media, and these absolutely need to go in separate files. As usual, name them something sensible, like <a href="https://www.smashingmagazine.com/2015/01/designing-for-print-with-css/">print.css</a>.

If you have multiple CSS files, that’s great, but make sure you use an automated tool to merge them all into one file before serving them up, or your website’s download speed will suffer. Don’t merge your beautifully factored CSS by hand. That’s using a <a href="https://en.wikipedia.org/wiki/Mechanical_Turk">Mechanical Turk</a> for a job that computers do easily. You could use <a href="https://code.google.com/p/minify/">Minify</a> (PHP) or <a href="https://rubygems.org/gems/juicer">Juicer</a> (Ruby) for that.

### JavaScript

<figure><img loading="lazy" decoding="async" class="size-full" title="Javscript code" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a346cc7a-e1c5-413b-ba17-9ab1079e40cc/javascript-image.jpg" alt="Javascript code" width="500" height="210" /><figcaption>(JavaScript code <a href="https://www.flickr.com/photos/dmitry-baranovskiy/2378867408/">Image source</a>)</figcaption></figure>

There’s a lot in common between organizing the JavaScript and CSS files for many websites. They both serve similar (but different) purposes, they’re both served up to the browser to interpret, they both interact with the DOM (when used appropriately), they often interact with each other. JavaScript is often used to add functionality to exactly the same set of elements that the CSS is used to style.

You’ll usually end up having your JavaScript library file (<code>jquery.js</code>, <code>mootools.js</code> etc.), a couple of widgets (say <code>datepicker.js</code> and <code>dropdown.js</code>), and some site-specific code (eg <code>my-image-slider.js</code>). It definitely makes sense to keep these in separate files, although you’ll often have so little site-specific JavaScript that it makes sense to just have one file for that part of it.

Put all these files into a folder named <code>JavaScript/</code>. Assuming you use a third-party library like jQuery, you’ll very rarely build a site complex enough to sub-divide this folder any further.

### Templates

<figure><img title="Your templates are just skeletal outlines for your code to flesh out with content, and for your stylesheets to paint with beauty." src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/172a0563-16e0-493c-a46a-ab083945a3c8/template-rulers.jpg" alt="Your templates are just skeletal outlines for your code to flesh out with content, and for your stylesheets to paint with beauty." width="500" height="333" /><figcaption>Your templates are just skeletal outlines for your code to flesh out with content, and for your stylesheets to paint with beauty. (<a href="https://www.flickr.com/photos/dorena-wm/4710380205/">Image source</a>)</figcaption></figure>

Templates are **not** content, are **not** code, and are **not** presentation. Templates can have certain aspects of all those things, but only the barest hint, when used properly. It might help to think of your templates as skeletons. Your server-side code fleshes out these templates with content (content from the database, error messages, form-field values, etc), and the browser applies an aesthetic skin to acheive the end result.

Of course, your templates might have the odd piece of human-readable text, for a button, dropdown, or whatever. That’s fine &mdash; that sort of text tends to be closely associated with the function of the page, rather than the content.

Put the templates in a <code>templates/</code> folder. In spite of what I said above, templates are really server-side code (they’re sensitive), so make sure they’re not publicly accessible.

{{% ad-panel-leaderboard %}}

If your website sends out emails, then have a couple of subfolders in this folder for plain-text and HTML email templates. If your website is more than just a brochure website, you’ll need many templates, for the different pages and screens of your application. If you have a smartphone version of your site, have a subfolder for it. Structure these subfolders appropriately. Here’s a good example:

<pre><code class="language-markup">templates/
    blog/
        sidebar.tpl
        post.tpl
        comment.tpl
    emails-plaintext/
        subscribe.tpl
        change-password.tpl
    emails-html/
        subscribe.tpl
        change-password.tpl
    social/
        twitter-feed.tpl
        facebook-sidebar.tpl
    mobile/
        base.tpl
        contact.tpl
        customer-profile.tpl
        friend.tpl
        homepage.tpl
        reviews.tpl
    base.tpl
    contact.tpl
    customer-profile.tpl
    friend.tpl
    homepage.tpl
    reviews.tpl
</code></pre>

### Assets

This is a name I really don’t like, though the alternatives aren’t necessarily much better. This is the folder where you put all the audio, video, documents, pictures, and anything other non-textual (or non-HTML), usually business-specific, content, which you want to be publicly available on your website.

Some alternatives for names are <code>uploads/</code>, <code>resources/</code>, <code>files/</code>, <code>media/</code>. Or you could break it up into separate main folders, called <code>pictures/</code>, <code>audio/</code> etc &mdash; but that gets messy pretty quickly. However, it is often good to have sub-folders for different types of file.

I tend to use <code>resources/</code>, personally, but it’s a bit abstract. Not a very good name, though better than <code>assets/</code> (what are we, accountants?). However, <code>assets/</code> is almost an industry standard, and if I were to start fresh, that’s probably what I’d use. So for the sake of this article, lets go with that.

If this is just a small business website without massive content management concerns, then the security of these documents isn’t a concern. If it is, then you should have those sensitive documents in a completely different folder.

If you have a larger-scale website with needs for permissions-based access to different available content, then you should use a document management system of some sort.

In light of that, it’s perfectly safe to make this folder publicly accessible from your website. Your client should be able to upload items to this folder themselves, and link to the items via the CMS.

If you don’t have many non-web documents, then there’s no point in sub-dividing this folder any further. However, if you have a lot of these files, it makes sense to have subfolders with names like <code>photos/</code>, <code>pdfs/</code>, <code>videos/</code> etc.

### The Database

This article isn’t really about database design, so we won’t deal with this much here. But it is important to keep your database well-structured. You’d do well to use an <a href="https://en.wikipedia.org/wiki/Object-relational_mapping">ORM</a> in almost every situation &mdash; very few websites have unusual enough data requirements to need anything an ORM can’t acheive. Any good ORM can acheive virtually anything the underlying database can, anyway.

<a href="https://www.sqlite.org">SQLite</a> is a great option for most websites, because it’s easy to deploy, exists as a simple file on your file system (but is a full-featured relational database), and it’s simple to backup (no fancy import/export, unless you want to &mdash; just use a standard file backup solution. Of course you already have one, right?)

Name your database the same as you’ve named your project folder. Don’t have a separate database for each aspect of your website, but do have a separate database for each website you develop. As always, keep it simple, use short, full words as names, and don’t clutter things up with all sorts of extra prefixes and suffixes.

### The Content Management System

These babies generally take care of organizing themselves. But do use a CMS that’s decently structured and well-coded. If you use a file-based CMS, put all of its content in a subdirectory, say <code>content/</code>.

### The Administration Section

Almost everyone puts the administrative files under <code>admin/</code>, when it’s needed. If you have an admin section, do the same. Don’t have duplicate code, images, JavaScript, etc. for the admin. Obviously, for the parts of the admin section that are different, you’ll need to have additional code etc. But it should be part of the same codebase, and factored such that you can use the helper functions from any part of the website.

Food for thought: you may not need an admin section at all. For example, if your client needs to upload and edit photos, why not provide an "edit" link right there next to the photo? Similarly for posts, comments, etc. Of course, be sure that you still have robust authorization and authentication.

### The Code

Whew. Where do I start? Software development is a complete field of knowledge in itself, and software is among the hardest things in the known universe to keep organized. I won’t even begin to cover all the ground here.

However, the rules stay the same: don’t hide files deep inside a hierarchy if possible, name your files using short, concrete nouns. Do use subfolders when necessary &mdash; but for most websites you shouldn’t have that much code. Stay on top of it. Make sure you use the same names for the same things &mdash; if you’ve called the database table <code>users</code>, don’t name the relevant file <code>members.php</code>. Name it <code>users.php</code>.

<a href="https://en.wikipedia.org/wiki/Code_refactoring">Good factorization</a> is by far the most important aspect of keeping software organized, and it covers all levels of your code &mdash; from the folders right down to the names you choose for your variables. It’s is the single biggest deciding factor that separates competent programmers from the inexperienced ones. Go learn all about it.

Some things to keep in their own separate files and folders:

*   Your data model. If you have a lot of logic attached to each type of object, you’ll probably want to have a separate file for each major class.
*   Your "views" (as Django calls them). These are "controllers" in MVC language. Briefly, a "view" is any code specific to a particular URL.
*   General-purpose classes and functions.
*   Your library code. This should probably not even be inside your project or client’s folder &mdash; you should have a system-wide collection of library code you use, so you don’t have to manage multiple copies of the same thing.
*   Third-party library code.

Use a version control system, such as <a href="https://subversion.apache.org">SubVersion</a>. To learn about version control, take the time to read the <a href="https://sixrevisions.com/project-management/the-ultimate-guide-to-version-control-for-designers/">guide to version control for web designers</a>.

The files here will often have corresponding files in your templates folder, although there won’t always be a one-to-one match. Where there is, though, use the same name for both files.

Keep your code well outside of any publicly-accessible folders. Do you really want everyone finding all the inevitable security holes in your code? Don’t mix HTML, CSS, or Javascript in with your server-side code, or vice-versa.

{{% ad-panel-leaderboard %}}

## The Final Folder Layout

Of course, you should consider the given situation to determine what’s best for the project. The example below is by no means complete, and exists solely to give you an idea of what we’ve discussed.

<div class="break-out">

 <pre><code class="language-markup">bEat/
        website/
            images/
                boxes/ /* often still necessary for IE... */
                    red-bottom-left.png
                    red-bottom-right.png
                    red-top-left.png
                    red-top-right.png
                navigation/
                    navigation-sprite.png
                    background.png
                logo.png
                page-background.png
                twirly-list-dot.png
            css/
                layout.css
                content.css
                print.css
                mobile.css
            javascript/
                jquery.js
                datepicker.js
                site.js
            assets/
                pictures/
                videos/
                pdfs/
            templates/
                blog/
                emails-plaintext/
                emails-html/
                social/
                mobile/
                *.tpl
            content/
        code/
            *.php
        reports/
        graphics/
</code></pre>
</div>

The same, in a shorter form:

<pre><code class="language-markup">bEat/
        website/
            images/
            css/
            javascript/
            assets/
            templates/
            content/
        code/
</code></pre>

Admittedly, it looks pretty basic, when you reduce it to that. But the fallout from getting it wrong can cost a lot of time and effort. You can <a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/05d92fa7-983e-4dc7-8a40-32c21116e5da/sample-project.zip">download the sample project folder template</a> (.zip), a skeletal PHP website, with a single content page, based upon the H2O template library.

Perhaps you like the following alternative better. It has the advantage of keeping everything for a single project inside a single project, at the cost of putting all the static files one level deeper. If you spend a lot of time working with CSS and JavaScript, that may be not so useful for you, but it’s a question of what’s important for your project and for your business.

<pre><code class="language-markup">bEat/
        website/
            static/         /* name it "public/" if you prefer */
                images/
                css/
                javascript/
                assets/
                content/
            templates/
            code/
</code></pre>

## Quick Recap

*   Keep it tidy. Don’t drive everyone insane with your need to have a perfect folder layout, but avoid putting files in convenient but incorrect locations.
*   Use sensible filenames. Concrete words that bring up a (relevant) picture in your mind’s eye are best. Where possible, use single words to name your files, but not at all costs.
*   Often (but by no means always) when you need to use two words to name a file uniquely, it’s a sign that you should make a subfolder. Instead of `images/navigation-*.png`, you might be better off with `images/navigation/*.png`.
*   Avoid cluttering your filenames up with all sorts of extra prefixes and suffixes.
*   Managing your own time effectively will help you find time to organize your website files &mdash; remember, quadrant 2!

Of course, we’re not perfect, and the suggestions here are definitely not the only (or best) way to do things. How do you organize your own website files? Let us know in the comments!

### Further Reading

-   [A Simple Workflow From Development To Deployment](https://www.smashingmagazine.com/2015/07/development-to-deployment-workflow/)
-   [Powerful Workflow Tips, Tools And Tricks For Web Designers](https://www.smashingmagazine.com/2013/10/powerful-workflow-tips-tools-and-tricks-for-web-designers/)
-   [Improving Code Readability With CSS Styleguides](https://www.smashingmagazine.com/2008/05/improving-code-readability-with-css-styleguides/)
-   [35 Useful Coding Tools and JavaScript Libraries For Web Developers](https://www.smashingmagazine.com/2011/10/useful-coding-workflow-tools-for-web-designers-developers/)

{{< signature "vf, il, mrn" >}}
