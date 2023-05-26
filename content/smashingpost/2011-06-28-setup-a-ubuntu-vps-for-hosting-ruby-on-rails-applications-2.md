---
title: 'Setup A Ubuntu VPS For Hosting Ruby On Rails Applications'
slug: setup-a-ubuntu-vps-for-hosting-ruby-on-rails-applications-2
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2509c418-3128-4d69-b2b1-bd7b38076c7e/ruby-mainpage.jpg
date: 2011-06-28T10:38:24.000Z
author: david-boot
summary: >-
  David Boot brings you a tutorial that will help you get through the steps required to set up an Ubuntu VPS that is capable of hosting (multiple) Ruby on Rails applications. Let’s go through it!
description: >-
  David Boot brings you a tutorial that will help you get through the steps required to set up an Ubuntu VPS that is capable of hosting (multiple) Ruby on Rails applications. Let’s go through it!
categories:
  - Coding
  - Linux
  - Ruby on Rails
---

Let’s assume you have built a nice little Ruby on Rails application on your local development machine. Now it’s time for the application to go live. But where should you host this application? You know that you (or your client) do not have much money to spend, and so you look at the options. You notice right away that managed hosting of applications tends to be relatively expensive. <a href="https://heroku.com/">Heroku</a> is a good option, but it doesn’t give you storage space, and more importantly, it lacks full control. Luckily, you have a suitable alternative: a VPS.

This tutorial will help you get through the steps required to set up an Ubuntu VPS that is capable of hosting (multiple) Ruby on Rails applications. This tutorial builds on part 1, “<a href="https://www.smashingmagazine.com/2011/06/21/set-up-an-ubuntu-local-development-machine-for-ruby-on-rails/">Set Up An Ubuntu Local Development Machine For Ruby On Rails</a>.” We recommend that you follow that part first and use the same Ubuntu local development machine that you set up there to walk through this part.

<figure><img loading="lazy" decoding="async" class="104029" title="vps" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2509c418-3128-4d69-b2b1-bd7b38076c7e/ruby-mainpage.jpg" alt="Screenshot" width="500" height="318" /></figure>

{{% feature-panel %}}

## Wait… A VPS?

VPS stands for virtual private server. It is a virtual machine offered by Internet hosting companies. With a VPS, you get your own virtual slice of real estate that lives with other virtual slices on one physical server. This virtual machine is capable of running an operating system, a Web server and database software. A VPS comes with full control (or root access) and, with most hosting companies, at a very reasonable price. And because a VPS is capable of running multiple Ruby on Rails applications, the costs of the VPS can be spread.

## Quick Overview

In this tutorial, we’ll log into the VPS, add a new user and configure SSH connections so that the VPS is more secure. Then, we’ll install Ruby and RubyGems using the Ruby Version Manager (RVM) script. In turn, we’ll install Rails and Capistrano using RubyGems. And then we’ll install Passenger and take care of the Nginx Web server installation. The VPS will also feature a PostgreSQL database.

At the time of writing, the latest versions are Ubuntu Server 10.10, Ruby 1.9.2 and Rails 3.0.7. These steps were also tested on Ubuntu Server 10.04 and the upcoming Ubuntu Server 11.04 release.

During this tutorial, we will make extensive use of the Linux command line. A short glossary at the end of this tutorial describes the relevant Linux commands.

## Up And Running

First, find a suitable host and purchase your VPS (if you don’t have one already). Make sure the host allows you to install Ubuntu on a VPS; most hosting companies will because it is a popular choice for VPS’. I chose a 512 MB VPS, which should be sufficient to run multiple small Ruby on Rails applications.

For those without a VPS, you can still follow along using virtualization software like VirtualBox. VirtualBox is open-source software and available in the Ubuntu Software Center or via the <a href="https://www.virtualbox.org/">official website</a>. Make sure when setting up your virtual machine that your network adapter is set to “Bridged” (<code>Right click</code> → <code>Settings</code> → <code>Network</code> → <code>Attached to: Bridged Adapter</code>). This way, your virtual machine will get its own IP address on your local network. Just install a fresh copy of Ubuntu Server, select “OpenSSH server” during installation, and skip the next two steps. You can log in directly via the VirtualBox window or, if you know the IP address of the server, via SSH.

Log into your VPS host’s control panel, and install a fresh copy of Ubuntu Server. Make sure to submit a safe “root” password, and boot the VPS.

## Log Into Your VPS

We’ll log into our VPS using SSH. SSH stands for secure shell and is a network protocol. It enables computers to communicate via an encrypted connection.

I assume you know the IP address of your VPS (if not, look it up in your host’s control panel), and that “root” is the default user, and that you know the “root” password, and that SSH is installed.

While using the domain name of the VPS is technically possible, we will log in using the VPS’ IP address. Setting up the domain name of your VPS is very context-specific and beyond the scope of this tutorial.

Now open up a terminal window on your Ubuntu local development machine, and log into your VPS:

<pre><code class="language-markup tmp-ruby">$ ssh default-user@vps-ip-address</code></pre>

For example:

<pre><code class="language-markup tmp-ruby">$ ssh root@123.456.7.890</code></pre>

You might have to type <code>yes</code> and then provide the “root” password. In about a second, you should be logged in.

## Secure Your VPS

For security reasons, you should do as little as possible as “root.” So, we’ll create a new user and assign administrative rights to it. To make use of its administrative rights, the user needs to explicitly invoke the “sudo” command, which adds a security layer to the system administration. First, create a new user:

<pre><code class="language-markup tmp-ruby">$ adduser your-user-name</code></pre>

For example:

<pre><code class="language-markup tmp-ruby">$ adduser johndoe</code></pre>

Provide a safe password (filling in the user details is optional). Now, make the new user a member of the “admin” group, which grants the user administrative rights (by invoking the sudo command).

<pre><code class="language-markup tmp-ruby">$ adduser your-user-name group-name</code></pre>

For example:

<pre><code class="language-markup tmp-ruby">$ adduser johndoe admin</code></pre>

Securing your SSH (server) configuration is the next step. Because every Unix system has a “root” user by default, you should disable “root” from logging in using SSH. This makes your system less vulnerable to brute force attacks.

<pre><code class="language-markup tmp-ruby">$ nano /etc/ssh/sshd_config</code></pre>

Set <code>PermitRootLogin</code> to <code>no</code>, and reload the SSH configuration so that the changes take effect. Although “root” will be disabled from logging in in future, the current “root” user connection will be maintained.

<pre><code class="language-markup tmp-ruby">$ /etc/init.d/ssh reload</code></pre>

Now, log out of your VPS as “root,” and log back in as the new user.

<pre><code class="language-markup tmp-ruby">$ logout
$ ssh your-user-name@vps-ip-address</code></pre>

For example:

<pre><code class="language-markup tmp-ruby">$ ssh johndoe@123.456.7.890</code></pre>

The system is more secure now that a new user has been created and “root” has been disabled from logging in via SSH. Some of the upcoming steps repeat the steps we took in part 1 of this tutorial, while also getting us up to date and installing RVM, Ruby, RubyGems and Rails.

## Get Up To Date

Now, let’s get up to date. The first three commands below will, in turn, update the package lists, upgrade currently installed packages, and install new packages and delete obsolete packages. You’ll end up with a VPS that is fully up to date. The final command will reboot the VPS, which is good practice after updating a lot of packages.

<pre><code class="language-markup tmp-ruby">$ sudo apt-get update
$ sudo apt-get upgrade
$ sudo apt-get dist-upgrade
$ sudo reboot</code></pre>

## Prepare Your VPS For RVM

Wait a minute or so for the VPS to reboot. Once it has, log back into the VPS from a terminal window.

<pre><code class="language-markup tmp-ruby">$ ssh your-user-name@vps-ip-address</code></pre>

For example:

<pre><code class="language-markup tmp-ruby">$ ssh johndoe@123.456.7.890</code></pre>

The RVM script needs some packages in order to be installed, namely Curl and Git. Curl is a tool to transfer data using a range of protocols (such as HTTP and FTP). And <a href="https://git-scm.com/">Git</a> is “a free and open-source, distributed version control system designed to handle everything from small to very large projects with speed and efficiency.” Git is <em>the</em> choice for version control among most Ruby on Rails developers.

<pre><code class="language-markup tmp-ruby">$ sudo apt-get install curl
$ sudo apt-get install git-core</code></pre>

## Install RVM

Now we can install RVM. <a href="https://rvm.beginrescueend.com/">RVM</a> stands for Ruby Version Manager and is “a command line tool that allows you to easily install, manage and work with multiple Ruby environments, from interpreters to sets of Gems.” The following command takes care of installing the script. RVM will be installed in the home directory of the currently logged-in user:

<pre><code class="language-markup tmp-ruby">$ bash &lt; &lt;(curl -s https://rvm.beginrescueend.com/install/rvm)</code></pre>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/553d0423-3b8b-40c4-b78e-66571164dc35/bf-rvm-installation.jpg"><img loading="lazy" decoding="async" class="100900" title="bf_rvm_installation" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/553d0423-3b8b-40c4-b78e-66571164dc35/bf-rvm-installation.jpg" alt="RVM installation" width="550" height="400" /></a></figure>

Navigate to the home directory, and edit the user’s bash profile. This ensures that the RVM script is loaded every time the corresponding user logs in. To edit the bash profile, we use Nano. Nano is a simple command line text editor, and we will use it again in this tutorial.

<pre><code class="language-markup tmp-ruby">$ cd
$ nano .bashrc</code></pre>

Add the following line to the end of the user’s bash profile.

<pre><code class="language-markup tmp-ruby">[[ -s "$HOME/.rvm/scripts/rvm" ]] &amp;&amp; . "$HOME/.rvm/scripts/rvm"</code></pre>

Load the script into the current shell session by reloading the user’s bash profile. This way, the <code>rvm</code> command will be made available.

<pre><code class="language-markup tmp-ruby">$ source .bashrc</code></pre>

You can verify whether the RVM script is working by entering the following command:

<pre><code class="language-markup tmp-ruby">$ type rvm | head -1</code></pre>

If everything is set up correctly, the shell should return that “rvm is a function.” If it doesn’t, please go over to the RVM website and look under “<a href="https://rvm.beginrescueend.com/rvm/install/">Troubleshooting Your Install</a>” to see how to make it work.

## Prepare Your VPS For Ruby And RubyGems

RVM comes with a handy tool for seeing the dependencies needed to compile and install Ruby and RubyGems from source.

<pre><code class="language-markup tmp-ruby">$ rvm notes</code></pre>

Look at the dependencies listed under the regular version of Ruby, and install these. Some packages might already be installed.

<pre><code class="language-markup tmp-ruby">$ sudo apt-get install build-essential bison openssl
libreadline6 libreadline6-dev curl git-core zlib1g zlib1g-dev
libssl-dev libyaml-dev libsqlite3-0 libsqlite3-dev sqlite3
libxml2-dev libxslt-dev autoconf libc6-dev ncurses-dev</code></pre>

## Install Ruby And RubyGems Using RVM

On the one hand, we have <a href="https://www.ruby-lang.org/">Ruby</a>. It is “a dynamic, open-source programming language with a focus on simplicity and productivity. It has an elegant syntax that is natural to read and easy to write.”

On the other hand, we have <a href="https://rubygems.org/">RubyGems</a>. It is “the premier Ruby packaging system. It provides a standard format for distributing Ruby programs and libraries, an easy to use tool for managing the installation of Gem packages, a Gem server utility for serving Gems from any machine where RubyGems is installed, and a standard way of publishing Gem packages.”

Like the RVM command described above, there is also a command to see what versions of Ruby are available to install using RVM. Have a look at the available Ruby versions.

<pre><code class="language-markup tmp-ruby">$ rvm list known</code></pre>

Install a regular version of Ruby. Because Ruby gets compiled from source, this might take a while.

<pre><code class="language-markup tmp-ruby">$ rvm install 1.9.2</code></pre>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7aff1c81-fc20-4acf-91c0-71c9be455111/bf-compiling-ruby.jpg"><img loading="lazy" decoding="async" class="100901" title="bf_compiling_ruby" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7aff1c81-fc20-4acf-91c0-71c9be455111/bf-compiling-ruby.jpg" alt="Compiling Ruby" width="550" height="400" /></a></figure>

Start using the installed Ruby, and set this version as the default.

<pre><code class="language-markup tmp-ruby">$ rvm --default use 1.9.2</code></pre>

Check the Ruby and RubyGems versions to see whether they have been properly installed.

<pre><code class="language-markup tmp-ruby">$ ruby -v
$ gem -v</code></pre>

If necessary, manually updating RubyGems and the Gems is possible.

<pre><code class="language-markup tmp-ruby">$ gem update --system
$ gem update</code></pre>

## Install Rails Using RubyGems

Rails Gem itself is the only thing left to put on Ruby on Rails. Installing this is one of the easiest parts of this tutorial. It is installed using RubyGems, invoked by the <code>gem</code> command. When the installation finishes, check the Rails version to see whether Rails has been properly installed.

<pre><code class="language-markup tmp-ruby">$ gem install rails
$ rails -v</code></pre>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/530de05e-5c88-44f3-98cf-6bd1d47984b8/bf-versions.jpg"><img loading="lazy" decoding="async" class="100902" title="bf_versions" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/530de05e-5c88-44f3-98cf-6bd1d47984b8/bf-versions.jpg" alt="Versions" width="550" height="400" /></a></figure>

## Install Passenger Using RubyGems

<a href="https://www.modrails.com/">Phusion Passenger</a> “makes deployment of Ruby Web applications, such as those built on the revolutionary Ruby on Rails Web framework, a breeze.” It is a module for running Ruby on Rails applications in conjunction with a Web server such as Nginx.

You can install Passenger using RubyGems and then check the Passenger version to see whether Passenger has been properly installed.

<pre><code class="language-markup tmp-ruby">$ gem install passenger
$ passenger -v</code></pre>

## Install Nginx, And Configure The Passenger Module

<a href="https://nginx.org/">Nginx</a>, pronounced “engine x”, is “an HTTP and reverse proxy server, as well as a mail proxy server.” To put it simply, it is a versatile Web server that is low on resources.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f3b89bc9-6c74-441a-992d-6423a98891d2/bf-nginxpassenger.png"><img loading="lazy" decoding="async" class="size-medium wp-image-100903" title="bf_nginxpassenger" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b0ffada0-0ddd-4059-882c-af565f9ec448/bf-nginxpassenger-300x120.png" alt="Nginx and Passenger" width="300" height="120" /></a></figure>

In order to let Passenger install Nginx, you need to install a dependency first.

<pre><code class="language-markup tmp-ruby">$ sudo apt-get install libcurl4-openssl-dev</code></pre>

You can start installing Nginx and configuring the Passenger module by using the following command. Notice that we use <code>rvmsudo</code> instead of <code>sudo</code>, because the regular <code>sudo</code> does not work on this little program.

<pre><code class="language-markup tmp-ruby">$ rvmsudo passenger-install-nginx-module</code></pre>

The program will check the dependencies first and then ask whether you want the program to download the Nginx source code or to download it yourself. Choose option 1 (have the program download the Nginx source code for you), and hit “Enter.” You can leave everything in the default settings, so just make your way through the installation process.

In the end, you will be presented with two screens. The first shows how to configure Nginx to work with Passenger; this was already done by the program. The second shows how to configure Nginx to deploy an application. We will come back to this example later in the tutorial.

You could start Nginx by hand…

<pre><code class="language-markup tmp-ruby">$ sudo /opt/nginx/sbin/nginx</code></pre>

… but using a start-up script is preferable. (Because Nginx gets compiled from source, it does not come with a start-up script.) With a start-up script, we can not only start Nginx, but also stop, reload and restart it. In addition, Nginx will be started automatically if the VPS reboots unexpectedly. Therefore, we need to download a little start-up script for Nginx to the home directory using Wget. Wget is a simple command line program that enables us to download files from the Internet. You do not need to understand the rest of the commands. They simply move the script to the right location, make it executable and make sure that <a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/570a0be6-6ae0-4176-8453-cead7c2c61e6/nginx.zip">Nginx starts when the system boots</a>.

<pre><code class="language-markup tmp-ruby">$ cd
$ wget https://smashingmagazine.com/files/nginx
$ sudo mv nginx /etc/init.d/nginx
$ sudo chmod +x /etc/init.d/nginx
$ sudo /usr/sbin/update-rc.d -f nginx defaults</code></pre>

From now on, the following commands can be used to start, stop, reload and restart Nginx.

<pre><code class="language-markup tmp-ruby">$ sudo /etc/init.d/nginx start
$ sudo /etc/init.d/nginx stop
$ sudo /etc/init.d/nginx reload
$ sudo /etc/init.d/nginx restart</code></pre>

## Install PostgreSQL

<a href="https://www.postgresql.org/">PostgreSQL</a> is “a sophisticated object-relational DBMS, supporting almost all SQL constructs, including subselects, transactions and user-defined types and functions.”

Install PostgreSQL together with a dependency. This dependency will be needed to install the “pg” Gem later on, which is responsible for the connection between PostgreSQL and Ruby on Rails.

<pre><code class="language-markup tmp-ruby">$ sudo apt-get install postgresql libpq-dev</code></pre>

{{% ad-panel-leaderboard %}}

## Configure PostgreSQL

When the packages have been installed, move on to configuring PostgreSQL by securing psql. psql is the PostgreSQL interactive terminal, and it is used for administrative database tasks.

By default, you do not need a password to log into psql. We’ll change this by editing the authentication method and then reloading the PostgreSQL configuration. But first, assign a password to superuser “postgres”. Log into psql, assign a safe password to “postgres,” and then log out of psql.

<pre><code class="language-markup tmp-ruby">$ sudo -u postgres psql
# password postgres
# q</code></pre>

Now change the authentication configuration by changing <code>ident</code> to <code>md5</code>. This ensures that a password is needed to log into psql and that the password is encrypted. The two relevant lines, which need to be edited, can be found near the end of the configuration file. After that, reload the changed configuration into PostgreSQL.

<pre><code class="language-markup tmp-ruby">$ sudo nano /etc/postgresql/8.4/main/pg_hba.conf
$ sudo /etc/init.d/postgresql reload</code></pre>

Most other PostgreSQL settings are stored in another configuration file. These settings can also be optimized, but that is beyond the scope of this tutorial. Keep in mind that the PostgreSQL configuration needs to be reloaded in order for the changes to take effect.

<pre><code class="language-markup tmp-ruby">$ sudo nano /etc/postgresql/8.4/main/postgresql.conf</code></pre>

The VPS is now installed. You can log out.

<pre><code class="language-markup tmp-ruby">$ logout</code></pre>

## Testing The VPS

To make sure everything works, we’ll develop a very small application on the local development machine and deploy it to the VPS using Capistrano. This process consists of the following steps:

1.  Open two terminal windows, one for the local development machine and one for the VPS.
2.  Log into the VPS using SSH *(VPS)*.
3.  Create a database user for the test application *(VPS)*.
4.  Create a database for the test application *(VPS)*.
5.  Create a test application using PostgreSQL as the database *(local)*.
6.  Configure the database connections for the test application *(local)*.
7.  Generate a simple scaffold for the test application *(local)*.
8.  Initialize Git as version control for the test application *(local)*.
9.  Add all the files of the test application to the Git version control list *(local)*.
10.  Take a version snapshot of the current application using Git *(local)*.
11.  Initialize Capistrano as a deployment tool for the test application *(local)*.
12.  Remove the default Capistrano deployment configuration file, and create a new one *(local)*.
13.  Set up the VPS to deploy the test application using Capistrano *(local)*.
14.  Check the VPS set-up for deploying the test application using Capistrano *(local)*.
15.  Deploy the test application with Capistrano *(local)*.
16.  Edit the Nginx configuration to work with the test application *(VPS)*.
17.  Reload Nginx *(VPS)*.
18.  Check the test application in a Web browser *(local)*.

Once we have verified that everything works, we’ll go through the following steps:

1.  Delete the database for the test application *(VPS)*.
2.  Delete the database user for the test application *(VPS)*.
3.  Restore the default Nginx configuration *(VPS)*.
4.  Reload Nginx *(VPS)*.
5.  Remove the test application *(VPS)*.
6.  Log out of the VPS *(VPS)*.
7.  Remove the test application *(local)*.
8.  Close both terminal windows.

Unlike <a href="https://www.smashingmagazine.com/2011/06/21/set-up-an-ubuntu-local-development-machine-for-ruby-on-rails/">part 1</a> of this tutorial, some of these steps have to be performed on the local development machine, and other steps have to be performed on the VPS. Therefore, we will open two terminal windows on our local development machine: one for the local development machine itself, and one with a connection to the VPS. The conventions used to test the VPS are shown below in Box 2.1. The database user name and the database name are derived from the name of the application.

<blockquote><strong>Box 2.1</strong>

Name of the application: <code>test_app</code>

Name of the VPS database user: <code>test_app</code>

Password of the VPS database user: <code>banana</code>

Name of the VPS database: <code>test_app_production</code>

Name of the VPS system user: <code>johndoe</code>

VPS IP address: <code>123.456.7.890</code></blockquote>

Now open two terminal windows, one for the local development machine and one for the VPS. Log into the VPS using SSH:

<pre><code class="language-markup tmp-ruby">$ ssh johndoe@123.456.7.890 (VPS)</code></pre>

When applications are deployed to a (publicly accessible) VPS, creating a new database user for every single application is good practice. This way, you will prevent multiple applications from viewing, inserting, editing and deleting data from and to each other’s databases, and thus increase security.

Let’s create a database user for the test application using the <code>createuser</code> command. We are using “postgres” as administrator (or superuser) for PostgreSQL. The <code>P</code> flag enables us to provide a password. The <code>&gt;</code> sign stands for the questions that will be prompted.

<pre><code class="language-markup tmp-ruby">$ sudo -u postgres createuser -P (VPS)
&gt; Enter name of role to add: test_app
&gt; Enter password for new role: banana
&gt; Enter it again: banana
&gt; Shall the new role be a superuser? (y/n) n
&gt; Shall the new role be allowed to create databases? (y/n) n
&gt; Shall the new role be allowed to create more new roles? (y/n) n
&gt; Password: your-postgres-user-password</code></pre>

Then, create a database for the test application that is owned by the test application user. While you can use Rake to create a database, we will use PostgreSQL so that we can learn some basic PostgreSQL administration.

You can create a new database by invoking the <code>createdb</code> command in conjunction with the <code>O</code> flag, the database user name and the new database name itself. The <code>production</code> that we append to the end of the database name is the default name. Here, you will be prompted for the PostgreSQL superuser password again.

<pre><code class="language-markup tmp-ruby">$ sudo -u postgres createdb -O test_app test_app_production (VPS)
&gt; Password: your-postgres-user-password</code></pre>

Now that the database has been set up, it is time to create the actual Ruby on Rails application on your local development machine.

Navigate to your home directory, and create a new Rails application, named <code>test_app</code> and using PostgreSQL as the database back end. The <code>d</code> flag enables you to specify your preferred database software.

<pre><code class="language-markup tmp-ruby">$ cd (LOCAL)
$ rails new test_app -d postgresql (LOCAL)</code></pre>

Go into the Rails application directory. Use Nano to edit the database configuration file by adding <code>banana</code> as a password in the production database configuration. Because we have followed the conventions described in Box 2.1, the database user name and the database name have already been taken care of.

<pre><code class="language-markup tmp-ruby">$ cd test_app (LOCAL)
$ nano config/database.yml (LOCAL)</code></pre>

Now, generate a basic scaffold. Programming in Rails is beyond the scope of this tutorial, but this command will create a “User” model and a “users” controller. The inputs will consist of a name and an email address, which are both strings in the PostgreSQL database.

<pre><code class="language-markup tmp-ruby">$ rails generate scaffold User name:string email:string (LOCAL)</code></pre>

Remember when we set up Git in part 1 of this tutorial? Now we’re finally going to use it. We will initialize Git as version control for the test application, add all of the files from the test application to the Git version control list (recursively), and take a version snapshot of the current application using Git. The <code>m</code> flag lets us add a short description of the snapshot.

<pre><code class="language-markup tmp-ruby">$ git init (LOCAL)
$ git add . (LOCAL)
$ git commit -m “First commit” (LOCAL)</code></pre>

By now, it is time to deploy the application to the VPS, which we will do using Capistrano.

Initialize Capistrano as a deployment tool for the test application. This will create several files in your Ruby on Rails application directory. Remove the default Capistrano deployment configuration file, and create a new one. The contents of the new Capistrano configuration file can be found in Box 2.2 below.

<pre><code class="language-markup tmp-ruby">$ capify . (LOCAL)
$ rm config/deploy.rb (LOCAL)
$ nano config/deploy.rb (LOCAL)</code></pre>

<blockquote><strong>Box 2.2</strong>

<pre><code class="language-markup tmp-ruby"># RVM

$:.unshift(File.expand_path('./lib', ENV['rvm_path']))
require "rvm/capistrano"
set :rvm_ruby_string, 'default'
set :rvm_type, :user

# Bundler

require "bundler/capistrano"

# General

set :application, "test_app"
set :user, "johndoe"

set :deploy_to, "/home/#{user}/#{application}"
set :deploy_via, :copy

set :use_sudo, false

# Git

set :scm, :git
set :repository,  "~/#{application}/.git"
set :branch, "master"

# VPS

role :web, "123.456.7.890"
role :app, "123.456.7.890"
role :db,  "123.456.7.890", :primary =&gt; true
role :db,  "123.456.7.890"

# Passenger

namespace :deploy do
 task :start do ; end
 task :stop do ; end
 task :restart, :roles =&gt; :app, :except =&gt; { :no_release =&gt; true } do
   run "#{try_sudo} touch #{File.join(current_path,'tmp','restart.txt')}"
 end
end</code></pre>

</blockquote>

Use the <code>cap</code> command to set up the VPS in order to deploy the test application using Capistrano. This will set up some directory structures on your VPS.

When using the <code>cap</code> command, you will need to provide a password when prompted. This is the password of the VPS user that you created at the very beginning of this tutorial. Check the VPS set-up for deploying the test application using Capistrano, and finally, deploy the test application.

Executing the last command might take a while because it installs the required Gems on the VPS and takes care of the database migrations (if there are any). Here you really see the benefit of Capistrano, because it automates tasks such as uploading the latest version of your application, installing the required Gems and performing the database migrations.

<pre><code class="language-markup tmp-ruby">$ cap deploy:setup (LOCAL)
$ cap deploy:check (LOCAL)
$ cap deploy:cold (LOCAL)</code></pre>

The last thing to do is tell Nginx where the Ruby on Rails test application is located. So, we need to edit the Nginx configuration file.

An example of the changes you have to make to that file are shown in Box 2.3 below. Only an excerpt of the relevant lines is printed here. Make sure to comment out the last four lines of the excerpt using <code>#</code>. Once you have made the changes, reload the new configuration into Nginx.

<pre><code class="language-markup tmp-ruby">$ sudo nano /opt/nginx/conf/nginx.conf (VPS)
$ sudo /etc/init.d/nginx reload (VPS)</code></pre>

<blockquote><strong>Box 2.3</strong>

(…)

<pre><code class="language-markup tmp-ruby">server {
   listen 80;
   server_name www.yourdomain.com;
   root /home/johndoe/test_app/current/public;
   passenger_enabled on;

   #charset koi8-r;

   #access_log  logs/host.access.log  main;

   #location / {
   #    root   html;
   #    index  index.html index.htm;
   #}</code></pre>

(…)</blockquote>

When the deployment and Nginx configuration are done, check the application in a Web browser. Navigate to <code>https://your-vps-ip-address/</code>. The link to the application’s environment will not work in production mode.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/41a2ddfe-9c1f-4055-86d5-10b1c0176b2c/screenshot1-ror.jpg"><img loading="lazy" decoding="async" class="100904" title="bf_welcome" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/41a2ddfe-9c1f-4055-86d5-10b1c0176b2c/screenshot1-ror.jpg" alt="Welcome" width="550" height="394" /></a></figure>

After that, look at <code>https://your-vps-ip-address/users</code>. Create, edit, view and delete some users:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0555fce1-451f-4723-badf-d429094b5434/screenshot2-ror.jpg"><img loading="lazy" decoding="async" class="100905" title="bf_users" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0555fce1-451f-4723-badf-d429094b5434/screenshot2-ror.jpg" alt="Users" width="548" height="278" /></a></figure>

If everything has worked, then the test application database and the test application database user can be removed. The <code>dropdb</code> command removes a PostgreSQL database.

<pre><code class="language-markup tmp-ruby">$ sudo -u postgres dropdb test_app_production (VPS)
&gt; Password: your-postgres-user-password</code></pre>

The <code>dropuser</code> command removes a PostgreSQL user.

<pre><code class="language-markup tmp-ruby">$ sudo -u postgres dropuser (VPS)
&gt; Enter name of role to drop: test_app
&gt; Password: your-postgres-user-password</code></pre>

Restore the Nginx configuration by copying an example of the (default) Nginx configuration file, overwriting the modified one, and then reload Nginx.

<pre><code class="language-markup tmp-ruby">$ sudo cp /opt/nginx/conf/nginx.conf.default /opt/nginx/conf/nginx.conf (VPS)
$ sudo /etc/init.d/nginx reload (VPS)</code></pre>

When that is done, navigate to your home directory on the VPS, and recursively remove the test application.

<pre><code class="language-markup tmp-ruby">$ cd (VPS)
$ rm -rf test_app (VPS)</code></pre>

Finally, log out of the VPS.

<pre><code class="language-markup tmp-ruby">$ logout (VPS)</code></pre>

For the local development machine, we also need to navigate to the home directory and recursively remove the test application. When all of the commands below are entered, you can close both terminal windows. This leaves you with a fresh VPS and local development machine ready for developing and deploying Ruby on Rails applications.

<pre><code class="language-markup tmp-ruby">$ cd (LOCAL)
$ rm -rf test_app (LOCAL)</code></pre>

## Appendix

### Linux Command Line Glossary

The Linux commands used in this tutorial are described here. The list is in alphabetical order and features only the relevant Linux commands. A Linux command usually takes the form of <code>command -option(s) argument(s)</code>. For example, <code>rm -r test_app</code>. For a more detailed description, use the manual, which can be accessed using <code>man [command]</code>.

*   `sudo [command]` Executes a command as an administrative user.
*   `adduser [username]` Adds a user to the system.
*   `adduser [username] [groupname]` Adds a user to a specific group.
*   `apt-get dist-upgrade` In addition to performing upgrades, this is used to intelligently handle dependencies.
*   `apt-get install [package]` Installs (or upgrades) packages.
*   `apt-get update` Resynchronize the package index files from their sources.
*   `apt-get upgrade` Installs the newest versions of all packages currently installed.
*   `bash < <( curl [location] )` A combination of commands used to both obtain and execute a script (from the Internet).
*   `cd [location]` Changes the current working directory. Without an argument, it goes to the user’s home.
*   `cp [file] [location]` Copies a file to the specified location (overwriting the existing file silently).
*   `chmod +x [file]` Makes a file exexutable.
*   `logout` Logs out of a shell or SSH session.
*   `mv [file] [location]` Moves a file to another location.
*   `nano [file]` Used to edit configuration files.
*   `reboot` Reboots the system.
*   `rm [file]` Removes a file.
*   `rm -rf [directory]` Removes a directory (recursively and forced, so it will not prompt).
*   `source [script]` Forces bash to read the specified script.
*   `ssh [username@ipaddress]` Logs into a secure shell session.
*   `type [command]` Displays the kind of command that the shell will execute.
*   `wget [location]` Obtains a file from the Internet.

### Resources

*   [Ubuntu](https://www.ubuntu.com/)
*   [RVM](https://rvm.beginrescueend.com/)
*   [Ruby](https://www.ruby-lang.org/)
*   [RubyGems](https://rubygems.org/)
*   [Rails](https://rubyonrails.org/)
*   [Passenger](https://www.modrails.com/)
*   [Nginx](https://nginx.org/)
*   [PostgreSQL](https://www.postgresql.org/)
*   [Capistrano](https://capify.org/)
*   [Git](https://git-scm.com/)

{{% ad-panel-leaderboard %}}

### Further Learning

*   [The Linux Command Line](https://linuxcommand.org/)
*   [The Linux Command Line Book](https://linuxcommand.org/tlcl.php)
*   Ubuntu Server Guide
*   [Ruby on Rails Guides](https://guides.rubyonrails.org/)
*   [Ruby on Rails Tutorial](https://ruby.railstutorial.org/)
*   Ruby on Rails Tutorial Book
*   [Git Community Book](https://book.git-scm.com/)
*   [Pro Git](https://progit.org/book/)
*   [Git Reference](https://gitref.org/)

### Further Reading

*   [How To Get Started With Ruby](https://www.smashingmagazine.com/2012/05/beginners-guide-ruby/)
*   [Get Started Writing iOS Apps With RubyMotion](https://www.smashingmagazine.com/2012/08/get-started-writing-ios-apps-with-rubymotion/)
*   [A Guide To Starting Your Own Rails Engine Gem](https://www.smashingmagazine.com/2011/06/a-guide-to-starting-your-own-rails-engine-gem/)
*   [How To Set Up An Ubuntu Local Machine For Ruby On Rails](https://www.smashingmagazine.com/2011/06/set-up-an-ubuntu-local-development-machine-for-ruby-on-rails/)

{{< signature "al, kw, mrn" >}}
