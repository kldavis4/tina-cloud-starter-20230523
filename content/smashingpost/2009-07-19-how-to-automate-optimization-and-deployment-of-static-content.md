---
title: How To Automate Optimization and Deployment Of Static Content
slug: how-to-automate-optimization-and-deployment-of-static-content
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/afe170af-908b-4a61-a98f-d7f5a50c1202/optimize.jpg
date: 2009-07-19T07:12:13.000Z
author: christian-baeuerlein
description: >-
  A lot of traffic between users and your site comes from the static content
  you’re using to set up the user interface, namely layout graphics, Stylesheets
  and Javascript files.
categories:
  - Coding
  - PHP
  - Content
  - Optimization
  - Ruby on Rails
---
A lot of traffic between users and your site comes from the static content you’re using to set up the user interface, namely layout graphics, Stylesheets and Javascript files. 

This article shows a method to improve the providing of static content for a web platform. Further, it will show you a way to <strong>automate the deployment</strong> of these files, so you can deliver them with least effort but with maximum performance.

This tutorial will take some time to set it up, but it’s going to <strong>save you hours</strong> of work in the future and will improve your page speed significantly.

You might be interested in the following related posts:

*   [A Simple Workflow From Development To Deployment](https://www.smashingmagazine.com/2015/07/development-to-deployment-workflow/)
*   [Improving Smashing Magazine’s Performance: A Case Study](https://www.smashingmagazine.com/2014/09/improving-smashing-magazine-performance-case-study/)
*   [Preload: What is it good for?](https://www.smashingmagazine.com/2016/02/preload-what-is-it-good-for/)
*   [Using A Static Site Generator At Scale: Lessons Learned](https://www.smashingmagazine.com/2016/08/using-a-static-site-generator-at-scale-lessons-learned/)

{{% feature-panel %}}

## 1\. Why do I need this?

There are several approaches to optimize the delivery of contents.
Some use on-the-fly compression via the server itself or a scripting language, which costs performance and does not optimize the structure and content of the files.

The method shown here prepares the files once and also merges and optimizes the code of CSS and Javascript files <strong>before</strong> the files are compressed, which makes the delivery of them even faster.

*   Most browsers download only two files from a source [at once](https://kb.mozillazine.org/Network.http.max-persistent-connections-per-server). If a page needs to load more files from one domain, they get queued.
*   More files to transfer mean more requests to the server, more traffic and more usage of the server’s performance. For the users of the platform, this means longer loading times.
*   The more steps you need to deploy these files, the more space for mistakes is given.
*   **Deployment is boring.**.  It’s far more exciting to invest some time once, to set up a reusable automation, than wasting time doing the same copy/paste/upload actions over and over again.

Compare this two screenshots that show the same content before and after the optimization.
The apricot colored parts of the bars stand for the status "in queue" while loading the page.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/01dbeaef-67c1-4587-9542-9c78ade62233/firebug-not-optimized.jpg" alt="Before optimization" width="500" height="339" /><br>
<em>The "in queue" status means nothing less than: Wasted time of the user.</em>

In this example, the loading time was reduced by <strong>33%</strong>, the transferred data size was reduced by <strong>65%</strong> and the number of requests to the server even by <strong>80%</strong>.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ee0a17ea-795c-49cd-9ef4-c3a8d4052877/firebug-optimized.jpg" alt="After optimization" width="500" height="67" /><br>
<em>By using CSS sprites and merged CSS and Javascript files, there is no queue for the loading of the basic static content.</em>

## 2\. How to improve your static content

Besides caching, there are some principles to make the whole setup of static content more efficient right from the start of development.

*   Use [CSS sprites](https://www.smashingmagazine.com/2009/04/27/the-mystery-of-css-sprites-techniques-tools-and-tutorials/) for your layout graphics. It not only saves you a lot of traffic and loading time. If you got used to maintain your graphics like this, you’ll notice that it can be much more comfortable to have your layout elements e.g. in a single Photoshop file.
*   Don’t blow up the loading time with your CSS and Javascript files. Combine the files of each kind into **one single file**, minimize them (e.g. by removing line breaks and other unnecessary characters) and compress them using GZip to get the load even smaller. This is covered in this tutorial.</p>

## 3\. Automating the deployment using Ruby

This automation is written in the <a href="https://www.ruby-lang.org">Ruby language</a>. So you need to have Ruby installed on your development computer. The installation is pretty simple on Windows and Mac OS X even ships with Ruby.

<strong>Please keep in mind:</strong> The scripts are completely independent from the language you’re using to run your site! You can also use them to deploy content e.g. for a <strong>PHP</strong> project.

If you’re not used to work on the command line, the next steps might look cryptic to you. Don’t hesitate, clench your teeth and take care that you always pass the correct path of the files to deal with. You only have to go through this once. When you’re finished, all you need to do is to type <strong>one single command</strong> to start the whole process.

To make it easier for you, this is the folder structure used for this tutorial:

<pre><code class="language-markup tmp-ruby">+ css/
- fonts.css
- grids.css
- layout.css
- reset.css
- static.min.css (generated)
- static.min.css.gz (generated)

+ js/
- framework.js
- gallery.js
- plugin1.js
- plugin2.js
- start.js
- static.min.js (generated)
- static.min.js.gz (generated)

+ deploy/
- batch
- ftp.rb
- gzip.rb

index.php (or something similar)</code></pre>

### Requirements for this tutorial

Don't worry, besides Ruby you won't need anything, that you don't probably already have:

*   A simple text editor to save the source code.
*   A command line tool, like Windows cmd.exe or Mac OS X Terminal to call the scripts.
*   A FTP account to try out the upload script.
*   A project to enhance.
*   _Optional:_ The Firefox add-on [Firebug](https://getfirebug.com/) (or something similar for other browsers), to see the enhancements afterwards.</p>

### Juicer

Christian Johansen created a tool called Juicer which enables you to merge and minimize CSS and Javascript files. To install it on <strong>Windows</strong>, simply type

<pre><code class="language-markup tmp-ruby">gem install juicer</code></pre>

in the command line. When you're using <strong>Mac OS X</strong> use

<pre><code class="language-markup tmp-ruby">sudo gem install juicer</code></pre>

After the successful install, Juicer will ask you to extend it with <a href="https://developer.yahoo.com/yui/compressor/">YUI Compressor</a> and <a href="https://www.jslint.com/">JSLint</a> for Javascript compression and verification. You do this by typing

<pre><code class="language-markup tmp-ruby">juicer install yui_compressor</code></pre>

and after that

<pre><code class="language-markup tmp-ruby">juicer install jslint</code></pre>

in the command line.</p>

### Preparing your files

The good thing is, you don’t have to change anything in your present files. But to make sure, the files are merged in the order you want to, you need to set up two additional files.

Let’s assume you have four CSS files and five Javascript files:

<pre><code class="language-markup tmp-xml">&lt;link rel="stylesheet" href="./css/reset.css" type="text/css" media="screen" /&gt;
&lt;link rel="stylesheet" href="./css/fonts.css" type="text/css" media="screen" /&gt;
&lt;link rel="stylesheet" href="./css/grids.css" type="text/css" media="screen" /&gt;
&lt;link rel="stylesheet" href="./css/layout.css" type="text/css" media="screen" /&gt;

&lt;script type="application/javascript" src="js/framework.js"&gt;&lt;/script&gt;
&lt;script type="application/javascript" src="js/plugin1.js"&gt;&lt;/script&gt;
&lt;script type="application/javascript" src="js/plugin2.js"&gt;&lt;/script&gt;
&lt;script type="application/javascript" src="js/gallery.js"&gt;&lt;/script&gt;        
&lt;script type="application/javascript" src="js/start.js"&gt;&lt;/script&gt;</code></pre>

Create a new Javascript file, called <code>static.js</code> with the following content:
<pre class="js">/**
 * @depends framework.js
 * @depends plugin1.js
 * @depends plugin2.js
 * @depends gallery.js
 * @depends start.js
 */
</pre>

After that, create a CSS file <code>static.css</code> with this content:

<pre><code class="language-css">@import url("reset.css");
@import url("fonts.css");
@import url("grids.css");
@import url("layout.css");</code></pre>

Now you’re ready to run Juicer in your command line.

For Javascript:

<pre><code class="language-markup tmp-ruby">juicer merge -i --force ./js/static.js</code></pre>

The parameter <code>-i</code> means that the merging process won't be cancelled, if JSLint thinks you have errors in your Javascript code. The parameter <code>--force</code> means older versions of the minified file will be overwritten.

For CSS:

<pre><code class="language-markup tmp-ruby">juicer merge --force ./css/static.css</code></pre>

As a result you will see two new generated files named <code>static.min.js</code> and <code>static.min.css</code>. You probably want to know if they still work for your site, so go ahead and test it, by replacing the old bunch of <code>link</code> and <code>script</code> tags in your html header with the two new ones.</p>

### GZip Compression

When your minified files work fine, you can go on to compression. If you get Javascript errors or your CSS layout looks weird, you should <strong>re-check the order</strong> of the files to merge.

Below you see a small Ruby script that saves a gzipped copy of a file.

<pre><code class="language-markup tmp-ruby">require 'zlib'

file_to_zip = ARGV[0]

puts "Gzipping #{file_to_zip}..."

base_name = File.basename(file_to_zip)

file_name_zip = "#{file_to_zip}.gz"

base_name_zip = "zip_#{base_name}"

File.open(file_name_zip, 'w') do |f|

  gz = Zlib::GzipWriter.new(f)

  IO.foreach(file_to_zip) {|x| 
    gz.write x
  }   

  gz.close

end

puts "Gzipped version saved as #{file_name_zip}"</code></pre>

Save it as <code>gzip.rb</code> and call it like this:

<pre><code class="language-markup tmp-ruby">ruby gzip.rb ../js/static.min.js</code></pre>

When you look at your folder, you’ll notice a new file called <code>static.min.js.gz</code>. Now do the same for the CSS file:

<pre><code class="language-markup tmp-ruby">ruby gzip.rb ../css/static.min.css</code></pre>

<strong>Important:</strong> Make sure that your server provides the right content encoding and content type information to the clients, so they understand that this files are gzipped content.
You can do this in many ways. For Apache, an example for the <code>.htaccess</code> file would be:

<pre><code class="language-markup tmp-ruby">&lt;FilesMatch ".(js.gz)$"&gt;
AddType text/javascript .gz
AddEncoding x-gzip .gz
&lt;/FilesMatch&gt;

&lt;FilesMatch ".(css.gz)$"&gt;
AddType text/css .gz
AddEncoding x-gzip .gz
&lt;/FilesMatch&gt;</code></pre>

### FTP-Upload

You’re on the home stretch. Now you have all improved files together and need to upload them to your host. Again, here’s a little Ruby script that does exactly that for you.

<pre><code class="language-markup tmp-ruby">require 'net/ftp'

ftp_host = ARGV[0]
ftp_user = ARGV[1]
ftp_password = ARGV[2]

localfile = ARGV[3] #e.g. "../js/static.min.js.gz"
remote_dir = ARGV[4] #e.g. "www/js"

ftp = Net::FTP.open(ftp_host, ftp_user, ftp_password) 

puts "FTP - Status: #{ftp.status}."

puts "FTP - Go to directory: #{remote_dir}."
ftp.chdir(remote_dir)
puts "FTP - Uploading file: #{localfile}..."
ftp.putbinaryfile(localfile)

files = ftp.list puts "FTP - Your file was uploaded here:" puts files

ftp.close</code></pre>

Save it as <code>upload.rb</code>, put in the credentials of your host, eventually change the destination directory and then call it like that:

<pre><code class="language-markup tmp-ruby">ruby ftp.rb example.org admin mysecret ../js/static.min.js www/js</code></pre>

Which stands for:
<code>ruby ftp.rb ftp-host ftp-user ftp-password file-to-upload ftp-destination-folder</code>

The minified Javascript file should be uploaded now. Repeat this for the CSS file and the gzipped versions of both.

<strong>Please note</strong> that the folders on the ftp server, where the files are copied to, must already exist.</p>

### Putting it all together

You got all the pieces of this puzzle and now you can finally put them together, by grouping the commands in a batch file. On <strong>Windows</strong> it would look like this:

<pre><code class="language-markup tmp-ruby">@echo off

echo -------- MERGING JS FILES --------
call juicer merge -i --force ../js/static.js 

echo -------- FINISHED MERGING JS FILES --------
echo -------- MERGING CSS FILES --------
call juicer merge --force ../css/static.css

echo -------- FINISHED MERGING CSS FILES --------
echo -------- COMPRESSING FILES --------
ruby gzip.rb ../js/static.min.js

ruby gzip.rb ../css/static.min.css

echo -------- FINSISHED COMPRESSING FILES --------
echo -------- UPLOADING FILES --------
ruby ftp.rb example.org admin mysecret ../js/static.min.js www/js

ruby ftp.rb example.org admin mysecret ../js/static.min.js.gz www/js

ruby ftp.rb example.org admin mysecret ../css/static.min.css www/css

ruby ftp.rb example.org admin mysecret ../css/static.min.css.gz www/css

echo -------- FINISHED UPLOADING FILES --------</code></pre>

Save it in a file called e.g. <code>batch.bat</code>, insert your FTP credentials and call it like this:

<pre><code class="language-markup tmp-ruby">cd deploy //switch to subdirectory
batch.bat</code></pre>

On <strong>OS X</strong> you can do it like that:

<pre><code class="language-markup tmp-ruby">#!/bin/bash

echo -------- MERGING JS FILES --------
juicer merge -i --force ../js/static.js 

echo -------- FINISHED MERGING JS FILES --------
echo -------- MERGING CSS FILES --------
juicer merge --force ../css/static.css

echo -------- FINISHED MERGING CSS FILES --------
echo -------- COMPRESSING FILES --------
ruby gzip.rb ../js/static.min.js

ruby gzip.rb ../css/static.min.css

echo -------- FINSISHED COMPRESSING FILES --------
echo -------- UPLOADING FILES --------
ruby ftp.rb example.org admin mysecret ../js/static.min.js www/js

ruby ftp.rb example.org admin mysecret ../js/static.min.js.gz www/js

ruby ftp.rb example.org admin mysecret ../css/static.min.css www/css

ruby ftp.rb example.org admin mysecret ../css/static.min.css.gz www/css

echo -------- FINISHED UPLOADING FILES --------</code></pre>

Save it in a file called e.g. <code>batch</code>, insert your FTP credentials and call it like this:

<pre><code class="language-markup tmp-ruby">cd deploy //switch to subdirectory
sh batch</code></pre>

And the content gets merged, minified, compressed and uploaded <strong>in one rush.</strong>
Additionally to the CSS and Javascript files, it would be a good idea, if the graphics file for the CSS sprites would be uploaded too? Just add an additional call of the upload script in the batch file. It can be used with any filetype.</p>

## 4\. In your template

Further development and bug fixing is hard to do in a minified file. But you can add an <code>if</code>-clause in your templates to vary the referencing of your files, depending on your environment.

Take the original files for your local development and the minified for your online version. Additionally you should check if the users browser supports gzipped content (most modern browsers do).

An example for <strong>PHP</strong>:

<pre><code class="language-php">if($_SERVER["SERVER_NAME"] == "localhost") {
  //local development server - load all files
} else {
  if (substr_count($_SERVER['HTTP_ACCEPT_ENCODING'], 'gzip')){
    //production system - client accepts gzip     
  } else {
    //production system - client does not accept gzip
  } 
}</code></pre>

And an example for <strong>Ruby on Rails</strong>:

<pre><code class="language-markup tmp-ruby">&lt;% if RAILS_ENV == 'development' %&gt;
  &lt;%# local development server - load all files %&gt;
&lt;% else %&gt;
  &lt;% if self.request.env['HTTP_ACCEPT_ENCODING'].match(/gzip/) %&gt;
    &lt;%# production system - client accepts gzip %&gt;
  &lt;% else %&gt;
    &lt;%# production system - client does not accept gzip %&gt;
  &lt;% end %&gt;
&lt;% end %&gt;</code></pre>

## 5\. Get even faster with subdomains

Like mentioned before, most browsers only download two files per host simultaneously. You can bypass that rule by creating some subdomains for your static content and referencing the files through them.

For example, create a subdomain on your web hosting account, that's called <code>img.example.org</code>, which points to <code>example.org/img</code>.

Do this for all of your folders, containing static content and use the subdomains to reference your resources:

<pre><code class="language-markup tmp-ruby">img.example.org/sprites.jpg
css.example.org/static.min.css
js.example.org/static.min.js</code></pre>

This way, the rule won’t be applied and all files can be downloaded at the same time.</p>

## 6\. Conclusion

If you got all of this working for one of your projects, you surely recognized the advantages for you as a developer and for the users as the consumers of your content.

file_to_zip = ARGV[0]

puts "Gzipping #{file_to_zip}..."

base_name = File.basename(file_to_zip)

file_name_zip = "#{file_to_zip}.gz"

base_name_zip = "zip_#{base_name}"

File.open(file_name_zip, 'w') do |f|

  gz = Zlib::GzipWriter.new(f)

  IO.foreach(file_to_zip) {|x| 
    gz.write x
  }   

  gz.close

end

puts "Gzipped version saved as #{file_name_zip}"</code></pre>

Save it as <code>gzip.rb</code> and call it like this:

<pre><code class="language-markup tmp-ruby">ruby gzip.rb ../js/static.min.js</code></pre>

When you look at your folder, you’ll notice a new file called <code>static.min.js.gz</code>. Now do the same for the CSS file:

<pre><code class="language-markup tmp-ruby">ruby gzip.rb ../css/static.min.css</code></pre>

<strong>Important:</strong> Make sure that your server provides the right content encoding and content type information to the clients, so they understand that this files are gzipped content.
You can do this in many ways. For Apache, an example for the <code>.htaccess</code> file would be:

<pre><code class="language-markup tmp-ruby">&lt;FilesMatch ".(js.gz)$"&gt;
AddType text/javascript .gz
AddEncoding x-gzip .gz
&lt;/FilesMatch&gt;

&lt;FilesMatch ".(css.gz)$"&gt;
AddType text/css .gz
AddEncoding x-gzip .gz
&lt;/FilesMatch&gt;</code></pre>

### FTP-Upload

You’re on the home stretch. Now you have all improved files together and need to upload them to your host. Again, here’s a little Ruby script that does exactly that for you.

<pre><code class="language-markup tmp-ruby">require 'net/ftp'

ftp_host = ARGV[0]
ftp_user = ARGV[1]
ftp_password = ARGV[2]

localfile = ARGV[3] #e.g. "../js/static.min.js.gz"
remote_dir = ARGV[4] #e.g. "www/js"

ftp = Net::FTP.open(ftp_host, ftp_user, ftp_password) 

puts "FTP - Status: #{ftp.status}."

puts "FTP - Go to directory: #{remote_dir}."
ftp.chdir(remote_dir)
puts "FTP - Uploading file: #{localfile}..."
ftp.putbinaryfile(localfile)

files = ftp.list puts "FTP - Your file was uploaded here:" puts files

ftp.close</code></pre>

Save it as <code>upload.rb</code>, put in the credentials of your host, eventually change the destination directory and then call it like that:

<pre><code class="language-markup tmp-ruby">ruby ftp.rb example.org admin mysecret ../js/static.min.js www/js</code></pre>

Which stands for:
<code>ruby ftp.rb ftp-host ftp-user ftp-password file-to-upload ftp-destination-folder</code>

The minified Javascript file should be uploaded now. Repeat this for the CSS file and the gzipped versions of both.

<strong>Please note</strong> that the folders on the ftp server, where the files are copied to, must already exist.</p>

### Putting it all together

You got all the pieces of this puzzle and now you can finally put them together, by grouping the commands in a batch file. On <strong>Windows</strong> it would look like this:

<pre><code class="language-markup tmp-ruby">@echo off

echo -------- MERGING JS FILES --------
call juicer merge -i --force ../js/static.js 

echo -------- FINISHED MERGING JS FILES --------
echo -------- MERGING CSS FILES --------
call juicer merge --force ../css/static.css

echo -------- FINISHED MERGING CSS FILES --------
echo -------- COMPRESSING FILES --------
ruby gzip.rb ../js/static.min.js

ruby gzip.rb ../css/static.min.css

echo -------- FINSISHED COMPRESSING FILES --------
echo -------- UPLOADING FILES --------
ruby ftp.rb example.org admin mysecret ../js/static.min.js www/js

ruby ftp.rb example.org admin mysecret ../js/static.min.js.gz www/js

ruby ftp.rb example.org admin mysecret ../css/static.min.css www/css

ruby ftp.rb example.org admin mysecret ../css/static.min.css.gz www/css

echo -------- FINISHED UPLOADING FILES --------</code></pre>

Save it in a file called e.g. <code>batch.bat</code>, insert your FTP credentials and call it like this:

<pre><code class="language-markup tmp-ruby">cd deploy //switch to subdirectory
batch.bat</code></pre>

On <strong>OS X</strong> you can do it like that:

<pre><code class="language-markup tmp-ruby">#!/bin/bash

echo -------- MERGING JS FILES --------
juicer merge -i --force ../js/static.js 

echo -------- FINISHED MERGING JS FILES --------
echo -------- MERGING CSS FILES --------
juicer merge --force ../css/static.css

echo -------- FINISHED MERGING CSS FILES --------
echo -------- COMPRESSING FILES --------
ruby gzip.rb ../js/static.min.js

ruby gzip.rb ../css/static.min.css

echo -------- FINSISHED COMPRESSING FILES --------
echo -------- UPLOADING FILES --------
ruby ftp.rb example.org admin mysecret ../js/static.min.js www/js

ruby ftp.rb example.org admin mysecret ../js/static.min.js.gz www/js

ruby ftp.rb example.org admin mysecret ../css/static.min.css www/css

ruby ftp.rb example.org admin mysecret ../css/static.min.css.gz www/css

echo -------- FINISHED UPLOADING FILES --------</code></pre>

Save it in a file called e.g. <code>batch</code>, insert your FTP credentials and call it like this:

<pre><code class="language-markup tmp-ruby">cd deploy //switch to subdirectory
sh batch</code></pre>

And the content gets merged, minified, compressed and uploaded <strong>in one rush.</strong>
Additionally to the CSS and Javascript files, it would be a good idea, if the graphics file for the CSS sprites would be uploaded too? Just add an additional call of the upload script in the batch file. It can be used with any filetype.</p>

## 4\. In your template

Further development and bug fixing is hard to do in a minified file. But you can add an <code>if</code>-clause in your templates to vary the referencing of your files, depending on your environment.

Take the original files for your local development and the minified for your online version. Additionally you should check if the users browser supports gzipped content (most modern browsers do).

An example for <strong>PHP</strong>:

<pre><code class="language-php">if($_SERVER["SERVER_NAME"] == "localhost") {
  //local development server - load all files
} else {
  if (substr_count($_SERVER['HTTP_ACCEPT_ENCODING'], 'gzip')){
    //production system - client accepts gzip     
  } else {
    //production system - client does not accept gzip
  } 
}</code></pre>

And an example for <strong>Ruby on Rails</strong>:

<pre><code class="language-markup tmp-ruby">&lt;% if RAILS_ENV == 'development' %&gt;
  &lt;%# local development server - load all files %&gt;
&lt;% else %&gt;
  &lt;% if self.request.env['HTTP_ACCEPT_ENCODING'].match(/gzip/) %&gt;
    &lt;%# production system - client accepts gzip %&gt;
  &lt;% else %&gt;
    &lt;%# production system - client does not accept gzip %&gt;
  &lt;% end %&gt;
&lt;% end %&gt;</code></pre>

## 5\. Get even faster with subdomains

Like mentioned before, most browsers only download two files per host simultaneously. You can bypass that rule by creating some subdomains for your static content and referencing the files through them.

For example, create a subdomain on your web hosting account, that's called <code>img.example.org</code>, which points to <code>example.org/img</code>.

Do this for all of your folders, containing static content and use the subdomains to reference your resources:

<pre><code class="language-markup tmp-ruby">img.example.org/sprites.jpg
css.example.org/static.min.css
js.example.org/static.min.js</code></pre>

This way, the rule won’t be applied and all files can be downloaded at the same time.</p>

## 6\. Conclusion

If you got all of this working for one of your projects, you surely recognized the advantages for you as a developer and for the users as the consumers of your content.

These examples don’t claim to be perfect. But if you didn’t approach to automate recurring tasks in your daily workflow as a developer, you hopefully have an idea now, how it could look like.

Always keep in mind, that computers were invented to spare you the boredom of repeating, simple tasks. So save your time for more important things.

Of course, this doesn’t have to be the end of the line. If you’re interested in the automatic deployment of whole applications, you should have a look at Capistrano. Again, it’s written in Ruby, but you can also use it for <strong>PHP platforms</strong>.</p>

## Further Resources

*   [Yahoo! Best Practices for Speeding Up Your Web Site](https://developer.yahoo.com/performance/rules.html) Lots of best practices, how to enhance content delivery.
*   [Yahoo! YSlow](https://developer.yahoo.com/yslow/) A Firebug add-on to test sites against the best practices above.
*   [Google Page Speed](https://developers.google.com/speed/pagespeed/insights/) Another Firebug add-on to test the loading performance of pages.
*   [How To Optimize Your Site With GZIP Compression](https://betterexplained.com/articles/how-to-optimize-your-site-with-gzip-compression) Another approach for the delivery of gzipped contents.

