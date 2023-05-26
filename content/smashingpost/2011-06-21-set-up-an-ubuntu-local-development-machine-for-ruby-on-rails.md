---
title: 'How To Set Up An Ubuntu Local Development Machine For Ruby On Rails'
slug: set-up-an-ubuntu-local-development-machine-for-ruby-on-rails
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f8f09554-8991-4572-b2f6-eb2430e97462/ruby-on-rails.png
date: 2011-06-21T08:46:33.000Z
author: david-boot
summary: >-
  Finding it difficult to set up a lean and up-to-date local development environment? In this article, David Boot guides you through the steps of setting up an Ubuntu local development machine for Ruby on Rails. 
description: >-
  Finding it difficult to set up a lean and up-to-date local development environment? In this article, David Boot guides you through the steps of setting up an Ubuntu local development machine for Ruby on Rails.
categories:
  - Coding
  - Linux
  - Ruby on Rails
---

So, you want to develop Ruby on Rails applications? While loads of (introductory) tutorials are available for developing Ruby on Rails applications, there seems to be some uncertainty about setting up a lean and up-to-date local development environment.

This tutorial will guide you through the steps of setting up an Ubuntu local development machine for Ruby on Rails. Part 2 of this tutorial, which will be published here later, will help you through the steps to set up an Ubuntu VPS. For now, knowing that VPS stands for virtual private server is sufficient. It will be able to host your newly developed Ruby on Rails applications. But let’s focus on the local development machine first.

{{% feature-panel %}}

## Ruby On Rails? Ubuntu?

What are Ruby on Rails and Ubuntu? In short, Ruby on Rails is a Web development framework that lets you create Web applications using the Ruby programming language. As the official <a href="https://rubyonrails.org/">website</a> states, “Ruby on Rails is an open-source Web framework that’s optimized for programmer happiness and sustainable productivity. It lets you write beautiful code by favoring convention over configuration.”

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a5762d6b-9b85-4a6a-a434-b91818766ee8/bf-frontpage.png"><img loading="lazy" decoding="async" class="99329" title="bf_frontpage" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a5762d6b-9b85-4a6a-a434-b91818766ee8/bf-frontpage.png" alt="Frontpage Image" width="550" height="300" /></a><figcaption>Ruby on Rails.</figcaption></figure>

<a href="https://www.ubuntu.com/">Ubuntu</a>, meanwhile, is a “Debian-derived Linux distribution that focuses on usability.” It has been the most popular Linux distribution for the last couple of years. And even better, both Ruby on Rails and Ubuntu are open source and, therefore, completely free to use.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/aff0ebdc-1406-463e-98ef-04af43d8bcbc/bf-ubuntu.png"><img class="size-medium wp-image-98795" title="bf_ubuntu" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bafec6f9-3fb8-43aa-806a-d7e95455be09/bf-ubuntu-300x79.png" alt="The Ubuntu Logo" width="300" height="79" /></a><figcaption>Ubuntu.</figcaption></figure>

## A Quick Overview

In this tutorial, we’ll install Ruby and RubyGems using the Ruby Version Manager (RVM) script. And we’ll install Rails and Capistrano in turn using RubyGems. The machine will also feature version control, provided by Git and a PostgreSQL database. A fresh installation of Ubuntu and a working Internet connection are assumed, but these steps should work on most (Debian- and Ubuntu-based) Linux distributions.

At the time of writing, the latest versions are Ubuntu 10.10, Ruby 1.9.2 and Rails 3.0.7. This tutorial was also tested on Ubuntu 10.04 and the upcoming Ubuntu 11.04 release.

During this tutorial, we will make extensive use of the Linux command line. Therefore, I have added a small glossary at the end of this article describing the relevant Linux commands.

## Getting Up To Date

First, let’s get up to date. Log into your machine as a user with administrative (or sudo) rights, and open a terminal window. The commands rendered below need to be entered in this terminal window. The dollar sign (<code>$</code>) is your command prompt, and the rest is as simple as typing the command and hitting “Enter.”

The first three commands will then update the package lists, upgrade currently installed packages, and install new packages and delete obsolete packages. This will give you a machine that is fully up to date. The final command will reboot the machine, which is good practice after updating a large number of packages.

<pre><code class="language-css">$ sudo apt-get update
$ sudo apt-get upgrade
$ sudo apt-get dist-upgrade
$ sudo reboot</code></pre>

## Prepare Your Machine For RVM

After the machine has rebooted, log back in and open a terminal window. The RVM script needs some packages in order to be installed, namely Curl and Git. Curl is a tool to transfer data using a range of protocols (such as HTTP and FTP). And “<a href="https://git-scm.com/">Git</a> is a free and open-source distributed version control system, designed to handle everything from small to very large projects with speed and efficiency.” Git is *the* choice for version control among most Ruby on Rails developers.

<pre><code class="language-css">$ sudo apt-get install curl
$ sudo apt-get install git-core</code></pre>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/978a32a5-795c-4228-9307-a5629ce8f6f9/bf-git.png"><img class="98797" title="bf_git" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/978a32a5-795c-4228-9307-a5629ce8f6f9/bf-git.png" alt="The Git Logo" width="250" height="96" /></a><figcaption>Git.</figcaption></figure>

## Configure Git

Git will be used by the RVM script, and we’ll be using it in part 2 of this tutorial. So, after installing the packages, let’s take a little time to configure it. Configuring Git is easy: just provide a user name and email address.

<pre><code class="language-css">$ git config --global user.name "Your Name"
$ git config --global user.email your-email@address.com</code></pre>

For example:

<pre><code class="language-css">$ git config --global user.name "John Doe"
$ git config --global user.email johndoe@mail.com</code></pre>

## Install RVM

Now we can install RVM. <a href="https://rvm.beginrescueend.com/">RVM</a> stands for Ruby version manager and “is a command-line tool that allows you to easily install, manage and work with multiple Ruby environments, from interpreters to sets of Gems.” The following command takes care of the installation of the script. RVM will get installed in the home directory of the currently logged-in user.

<pre><code class="language-css">$ bash &lt; &lt;(curl -s https://rvm.beginrescueend.com/install/rvm)</code></pre>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b481cb3e-3bc9-44c9-8306-0b4b033528d9/bf-rvm.png"><img class="98799" title="bf_rvm" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b481cb3e-3bc9-44c9-8306-0b4b033528d9/bf-rvm.png" alt="The RVM Logo" width="230" height="220" /></a><figcaption>RVM.</figcaption></figure>

Navigate to the home directory, and edit the user bash profile. This ensures that the RVM script gets loaded every time the corresponding user logs in. To edit the bash profile, we’ll use Nano. Nano is a simple command-line text editor, and we will use it again in this tutorial.

<pre><code class="language-css">$ cd
$ nano .bashrc</code></pre>

Add the following line to the end of the user bash profile. After you have made the changes, save the file by pressing CTRL + O, and exit Nano by pressing CTRL + X. If you ever want to exit Nano without saving changes, hit CTRL + X and then N.

<pre><code class="language-css">[[ -s "$HOME/.rvm/scripts/rvm" ]] &amp;&amp; . "$HOME/.rvm/scripts/rvm"</code></pre>

Manually load the script into the current shell session with the following command or open a new terminal window. This way, the <code>rvm</code> command will be made available.

<pre><code class="language-css">$ source .bashrc</code></pre>

You can verify whether the RVM script is working by entering the following command:

<pre><code class="language-css">$ type rvm | head -1</code></pre>

If everything is set up correctly, the shell should return that <code>rvm is a function</code>. If it doesn’t, go over to the RVM website and look under “<a href="https://rvm.beginrescueend.com/rvm/install/">Troubleshooting your install</a>” to see what you can do to make it work.

## Prepare Your Machine For Ruby And RubyGems

RVM comes with a handy command to view the dependencies that are needed to compile and install Ruby and RubyGems from source.

<pre><code class="language-css">$ rvm notes</code></pre>

See the dependencies listed under the regular version of Ruby, and install these. Some packages might already be installed.

<pre><code class="language-css">$ sudo apt-get install build-essential bison openssl libreadline6 libreadline6-dev curl git-core zlib1g zlib1g-dev libssl-dev libyaml-dev libsqlite3-0 libsqlite3-dev sqlite3 libxml2-dev libxslt-dev autoconf libc6-dev ncurses-dev</code></pre>

## Install Ruby And RubyGems Using RVM

First, we have <a href="https://www.ruby-lang.org/">Ruby</a>, “a dynamic, open-source programming language with a focus on simplicity and productivity. It has an elegant syntax that is natural to read and easy to write.”

Then we have <a href="https://rubygems.org/">RubyGems</a>. This is “the premier Ruby packaging system. It provides a standard format for distributing Ruby programs and libraries, an easy-to-use tool for managing the installation of Gem packages, a Gem server utility for serving Gems from any machine where RubyGems is installed, and a standard way of publishing Gem packages.”

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/72a3c052-de42-4d77-b869-8d7bc10dae08/bf-ruby.jpg"><img class="98800" title="bf_ruby" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/72a3c052-de42-4d77-b869-8d7bc10dae08/bf-ruby.jpg" alt="The Ruby Logo" width="150" height="150" /></a><figcaption>Ruby.</figcaption></figure>

Like the RVM command described above, there is also a command to see what versions of Ruby are available for installation using RVM. Have a look at the available Ruby versions using this command:

<pre><code class="language-css">$ rvm list known</code></pre>

Install a regular version of Ruby. Because Ruby gets compiled from source, this step might take a while.

<pre><code class="language-css">$ rvm install 1.9.2</code></pre>

Start using the installed Ruby, and set this version as a default.

<pre><code class="language-css">$ rvm --default use 1.9.2</code></pre>

Check the Ruby and RubyGems versions to see whether they have been properly installed.

<pre><code class="language-css">$ ruby -v
$ gem -v</code></pre>

If necessary, manually updating RubyGems and the Gems is possible.

<pre><code class="language-css">$ gem update --system
$ gem update</code></pre>

## Install Rails Using RubyGems

Rails Gem itself is all that’s left for Ruby to be put on Rails. Installing this is one of the easiest parts of this tutorial. It is installed using RubyGems, invoked by the <code>gem</code> command. When the installation finishes, check the Rails version to see whether Rails has been properly installed.

<pre><code class="language-css">$ gem install rails
$ rails -v</code></pre>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0065785a-dca5-468f-912b-6f411d934f50/bf-rails.jpg"><img class="size-medium wp-image-98801" title="bf_rails" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7b1127cd-08f1-4fa9-8c7e-97e01697291d/bf-rails-252x300.jpg" alt="The Rails Logo" width="252" height="300" /></a><figcaption>Rails.</figcaption></figure>

{{% ad-panel-leaderboard %}}

## Install Capistrano Using RubyGems

<a href="https://capify.org/">Capistrano</a> is “an open-source tool for running scripts on multiple servers. Its main use is deploying Web applications. It automates the process of making a new version of an application available on one or more Web servers, including supporting tasks such as changing databases.” You can install Capistrano using RubyGems. Check the Capistrano version to see whether it has been properly installed.

<pre><code class="language-css">$ gem install capistrano
$ cap -V</code></pre>

## Install PostgreSQL

<a href="https://www.postgresql.org/">PostgreSQL</a> is “a sophisticated object-relational DBMS, supporting almost all SQL constructs, including subselects, transactions, and user-defined types and functions.” Install PostgreSQL together with a dependency. This dependency is needed to install the <code>pg</code> Gem later on, which is responsible for the connection between PostgreSQL and Ruby on Rails.

<pre><code class="language-css">$ sudo apt-get install postgresql libpq-dev</code></pre>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/760ce20b-b508-4d02-96cd-ddb4b9656cc3/bf-postgresql.png"><img class="98802" title="bf_postgresql" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/760ce20b-b508-4d02-96cd-ddb4b9656cc3/bf-postgresql.png" alt="The PostgreSQL Logo" width="250" height="198" /></a><figcaption>PostgreSQL.</figcaption></figure>

## Configure PostgreSQL

When the packages have been installed, move on to configuring PostgreSQL by securing pSQL. pSQL is the PostgreSQL interactive terminal, and it is used for administrative database tasks.

By default pSQL does not require a password for you to log in. We’ll change this by editing the authentication method and then reloading the PostgreSQL configuration. But first, assign a password to super-user <code>postgres</code>. Log into pSQL, assign a safe password to <code>postgres</code>, and then log out of pSQL.

<pre><code class="language-css">$ sudo -u postgres psql
# password postgres
# q</code></pre>

Now modify the authentication configuration by changing <code>ident</code> to <code>md5</code>. This ensures that a password is needed to log into pSQL and that the password is encrypted. The two lines that need to be edited can be found near the end of the configuration file. After that, reload the changed configuration into PostgreSQL.

<pre><code class="language-css">$ sudo nano /etc/postgresql/8.4/main/pg_hba.conf
$ sudo /etc/init.d/postgresql reload</code></pre>

Most other PostgreSQL settings are stored in another configuration file. These settings can also be optimized, but that is beyond the scope of this tutorial. Keep in mind that a reload of the PostgreSQL configuration is required in order for changes to become active.

<pre><code class="language-css">$ sudo nano /etc/postgresql/8.4/main/postgresql.conf</code></pre>

The installation of the local development machine is now done.

## Testing The Set-Up

To make sure everything works, let’s develop a really small application and see a bit of Ruby on Rails in action. This process covers the following steps:

*   Create a database user for the test application,
*   Create a database for the test application,
*   Create a test application using PostgreSQL as the database,
*   Install the necessary Gems for the test application,
*   Configure the database connections for the test application,
*   Generate a simple scaffold for the test application,
*   Migrate the results of the scaffold to the test application database,
*   Start the built-in server,
*   Check the test application in a Web browser,
*   Stop the built-in server.

Once we have verified that everything works, we go through the following steps:

*   Delete the database for the test application,
*   Delete the database user for the test application,
*   Remove the test application.

All of these steps should be performed on the local development machine. The conventions used to test the VPS are as follows (the database user name and database name derive from the name of the application):
<blockquote><strong>Box 1.1</strong>

Name of application: <code>test_app</code>

Name of database user: <code>test_app</code>

Password of database user: <code>apple</code>

Name of database: <code>test_app_development</code></blockquote>

First, create a database user for the test application using the <code>createuser</code> command. We are using <code>postgres</code> as the admin (or super-user) for PostgreSQL. The <code>P</code> flag allows us to provide a password. The <code>&gt;</code> sign stands for the questions that will be prompted.

<pre><code class="language-css">$ sudo -u postgres createuser -P
&gt; Enter name of role to add: test_app
&gt; Enter password for new role: apple
&gt; Enter it again: apple
&gt; Shall the new role be a superuser? (y/n) n
&gt; Shall the new role be allowed to create databases? (y/n) n
&gt; Shall the new role be allowed to create more new roles? (y/n) n
&gt; Password: your-postgres-user-password</code></pre>

Then, create a database for the test application that is owned by the test application user. While we could use Rake to create a database, we will use PostgreSQL, so that we learn some basic PostgreSQL administration. Create a new database by invoking the <code>createdb</code> command in conjunction with the <code>O</code> flag, the database user name and the new database name itself. The addition of <code>development</code> at the end makes it the default database name. Here, you will be prompted for the PostgreSQL super-user password again.

<pre><code class="language-css">$ sudo -u postgres createdb -O test_app test_app_development
&gt; Password: your-postgres-user-password</code></pre>

Now that the database has been set up, it is time to create the actual Ruby on Rails application. Navigate to your home directory, and create a new Rails application, named <code>test_app</code>, using PostgreSQL as the database back end. The <code>d</code> flag allows us to specify the preferred database software.

<pre><code class="language-css">$ cd
$ rails new test_app -d postgresql</code></pre>

Go into the Rails application directory, and install the necessary Gems using Bundler. <a href="https://gembundler.com/">Bundler</a> takes care of “an application’s dependencies through its entire life across many machines systematically and repeatably,” and it “works out of the box with Rails 3.”

<pre><code class="language-css">$ cd test_app
$ bundle install</code></pre>

Use Nano to edit the database configuration file by adding <code>apple</code> as a password under the development database configuration. Because we have followed convention, described in Box 1.1 above, the database user name and database name have already been taken care of.

<pre><code class="language-css">$ nano config/database.yml</code></pre>

Now generate a basic scaffold. This will create a <code>User</code> model and a <code>users</code> controller. The inputs will consist of a name and an email address, which are both strings in the PostgreSQL database.

<pre><code class="language-css">$ rails generate scaffold User name:string email:string</code></pre>

Use <a href="https://rake.rubyforge.org/">Rake</a> to migrate the scaffold to the development database. Rake is an acronym for Ruby Make. It is a “simple Ruby build program with capabilities similar to Make,” which allows you to create and migrate databases.

<pre><code class="language-css">$ rake db:migrate</code></pre>

By now, it is time to check the (working) application in a Web browser. Start the built-in server, and use a Web browser to navigate to <code><a href="https://localhost:3000/">https://localhost:3000/</a></code>. In particular, look at the application’s environment, and then look at <code><a href="https://localhost:3000/users">https://localhost:3000/users</a></code>. Create, edit, view and delete some users.

<pre><code class="language-css">$ rails server</code></pre>

When everything appears to be working correctly, you can stop the built-in server.

<pre><code class="language-css">$ press CTRL+C</code></pre>

If everything has worked, then the test application database and test application database user can be removed. The <code>dropdb</code> command removes a PostgreSQL database.

<pre><code class="language-css">$ sudo -u postgres dropdb test_app_development
&gt; Password: your-postgres-user-password</code></pre>

The <code>dropuser</code> command removes a PostgreSQL user.

<pre><code class="language-css">$ sudo -u postgres dropuser
&gt; Enter name of role to drop: test_app
&gt; Password: your-postgres-user-password</code></pre>

Finally, navigate to your home directory, and recursively remove the test application. This leaves you with a fresh local development machine, ready for developing Ruby on Rails applications.

<pre><code class="language-css">$ cd
$ rm -r test_app</code></pre>

In part 2 of this tutorial, which will be published here later, we will help you through the steps necessary to set up an Ubuntu VPS that is capable of hosting (multiple) Ruby on Rails applications.

## Linux Command Line Glossary

The relevant Linux commands for this tutorial are listed below in alphabetical order. A Linux command usually takes the form of <code>command -option(s) argument(s)</code>. For example, <code>rm -r test_app</code>. For a more detailed description, use the manual pages, which can be accessed using <code>man [command]</code>.

*   `sudo [command]`Used to execute a command as an administrative user.
*   `apt-get dist-upgrade`In addition to performing the function of upgrade, this is used to intelligently handle dependencies.
*   `apt-get install [package]`Used to install (or upgrade) packages.
*   `apt-get update`Used to resynchronize the package index files from their sources.
*   `apt-get upgrade`Used to install the newest versions of all packages currently installed.
*   `bash < <( curl [location] )`A combination of commands for obtaining and executing a script (from the Internet).
*   `cd [location]`Used to change the current working directory. Without an argument, it goes to the user’s home directory.
*   `nano [file]`Used to edit configuration files.
*   `reboot`Used to reboot the system.
*   `rm -r [directory]`Used to remove a directory (recursively).
*   `source [script]`Used to force bash to read a specified script.
*   `type [command]`Used to display the kind of command that the shell will execute.

## References

*   [Ubuntu](https://www.ubuntu.com/)
*   [RVM](https://rvm.beginrescueend.com/)
*   [Ruby](https://www.ruby-lang.org/)
*   [RubyGems](https://rubygems.org/)
*   [Rails](https://rubyonrails.org/)
*   [Capistrano](https://capify.org/)
*   [Bundler](https://gembundler.com/)
*   [Rake](https://rake.rubyforge.org/)
*   [PostgreSQL](https://www.postgresql.org/)
*   [Git](https://git-scm.com/)

## Further Learning

*   [The Linux Command Line](https://linuxcommand.org/)
*   [The Linux Command Line Book](https://linuxcommand.org/tlcl.php)
*   [Ruby on Rails Guides](https://guides.rubyonrails.org/)
*   [Ruby on Rails Tutorial](https://ruby.railstutorial.org/)
*   [Git Community Book](https://book.git-scm.com/)
*   [Pro Git](https://progit.org/book/)
*   [Git Reference](https://gitref.org/)

{{% ad-panel-leaderboard %}}

### Further Reading

*   [Setup A Ubuntu VPS For Hosting Ruby On Rails Applications](https://www.smashingmagazine.com/2011/06/setup-a-ubuntu-vps-for-hosting-ruby-on-rails-applications-2/)
*   [Getting Started With Ruby On Rails](https://www.smashingmagazine.com/2009/03/getting-started-with-ruby-on-rails/)
*   [Successful Freelancing With Ruby On Rails](https://www.smashingmagazine.com/2010/10/successful-freelancing-with-ruby-on-rails-workflow-techniques-and-tools/)
*   [10 Useful Tips For Ruby On Rails Developers](https://www.smashingmagazine.com/2009/02/ruby-on-rails-tips/)

{{< signature "al, mrn" >}}
