---
title: 'Breaking The Rules: Using SQLite To Demo Web Apps'
slug: using-sqlite-demo-web-apps
author: jamespierce
image: >-
  //archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4bea1cb8-894b-4125-8cd3-d0f7a8c28b16/sqlite-logo-preview-opt.png
date: 2017-12-18T16:14:18+01:00
summary: >-
  So, you've built the next killer web app, but now you're presented with the question every new product must consider, "How do I show everyone how great my app is?"
description: >-
  So, you''ve built the next killer web app, but now you''re presented with the question every new product must consider, "How do I show everyone how great my app is?"
categories:
  - Apps
  - SQL
  - Ruby on Rails
  - JavaScript
---
<p>Most potential users will want to try out the software or service before committing any time and money. Some products work great by just giving users a free trial, while other apps are best experienced with sample data already in place. Often this is where the age-old demo account comes into play.</p>

<p>However, anyone who has ever implemented a demo account can attest to the problems associated. You know how things run on the Internet: Anyone can enter data (whether it makes sense or not to the product) and there is a good chance that the content added by anonymous users or bots could be offensive to others. Sure, you can always reset the database, but how often and when? And ultimately, does that really solve the problem? <strong>My solution to use SQLite</strong>.</p>

## Why Not Use SQLite For The Production Version?

<p>It's commonly known that SQLite does not handle multiple threads since the entire database is locked during a write command, which is one of the reasons why you should not use it in a normal production environment. However, in my solution, a separate SQLite file is <strong>used for each user</strong> demoing the software. This means that the write limitation is only limited to that one user, but multiple simultaneous users (each with their own database file) will not experience this limitation. This allows for a controlled experience for the user test driving the software and enables them to view exactly what <strong>you</strong> want them to see. </p>

{{% feature-panel %}}

<p>This tutorial is based on a real-world solution that I have been successfully running for a SaaS demo web app since 2015. The tutorial is written for Ruby on Rails (my framework of choice) version 3 and up, but the basic concepts should be able to be adapted to any other language or framework. In fact, since Ruby on Rails follows the software paradigm "convention over configuration" it may even be easier to implement in other frameworks, especially bare languages (such as straight PHP) or frameworks that do not do much in terms of managing the database connections. </p>

<p>That being said, this technique is particularly well suited for Ruby on Rails. Why? Because, for the most part, it is "database agnostic." Meaning that you should be able to write your Ruby code and switch between databases without any issues. </p>

<p>A sample of a finished version of this process can downloaded from <a href="https://github.com/jpegjames/a-little-saas">GitHub</a>.</p>

## The First Step: Deployment Environment

<p>We will get to deployment later, but Ruby on Rails is by default split into development, test and production environments. We are going to add to this list a new demo environment for our app that will be almost identical to the production environment but will allow us to use different database settings.</p>

<p class="c-pre-sidenote--left">In Rails, create a new environment by duplicating the <code>config/environments/production.rb</code> file and rename it <code>demo.rb</code>. Since the demo environment will be used in a production like setting, you may not need to change many configuration options for this new environment, though I would suggest changing <code>config.assets.compile</code> from <code>false</code> to <code>true</code> which will make it easier to test locally without having to precompile.</p>
<p class="c-sidenote c-sidenote--right">If you are running Rails 4 or above, you will also need to update <code>config/secrets.yml</code> to add a <code>secret_key_base</code> for the demo environment. Be sure to make this secret key different than production to ensure sessions are unique between each environment, further securing your app.</p>

<p>Next you need to define the database configuration in <code>config/database.yml</code>. While the demo environment will primarily use the duplicated database that we will cover in the next section, we must define the default database file and settings to be used for our demo. Add the following to <code>config/database.yml</code>:</p>

<pre><code class="language-yaml">demo:
  adapter: sqlite3
  pool: 5
  timeout: 5000
  database: db/demo.sqlite3</code></pre>

<p>In Rails, you may also want to check your <code>Gemfile</code> to make sure that SQLite3 is available in the new demo environment. You can set this any number of ways, but it may look like this:</p>

<pre><code class="language-ruby">group :development, :test, :demo do
  gem &#39;sqlite3&#39;
end
</code></pre>

<p>Once the database is configured, you need to <code>rake db:migrate RAILS_ENV=demo</code> and then seed data into the database however you wish (whether that is from a seed file, manually entering new data or even duplicating the <code>development.sqlite3</code> file). At this point, you should check to make sure everything is working by running <code>rails server -e demo</code> from the command line. While you are running the server in the new demo environment, you can make sure your test data is how you want it, but you can always come back and edit that content later. When adding your content to the demo database, I would recommend creating a clean set of data so that the file is as small as possible. However, if you need to migrate data from another database, I recommend <a href="https://github.com/yamldb/yaml_db">YamlDb</a>, which creates a database-independent format for dumping and restoring data.</p>

<p>If your Rails application is running as expected, you can move on to the next step.</p>

## The Second Step: Using The Demo Database

<p>The essential part of this tutorial is being able to allow each session to use a different SQLite database file. Normally your application will connect to the same database for every user so that additional code will be needed for this task. </p>

<p>To get started with allowing Ruby on Rails to switch databases, we first need to add the following four private methods into <code>application_controller.rb</code>. You will also need to define a before filter for the method <code>set_demo_database</code> so that logic referencing the correct demo database is called on every page load.</p>

<div class="break-out">

<pre><code class="language-ruby"># app/controllers/application_controller.rb

# use `before_filter` for Rails 3
before_action :set_demo_database, if: -&gt; { Rails.env == &#39;demo&#39; }

private

  # sets the database for the demo environment
  def set_demo_database
    if session[:demo_db]
      # Use database set by demos_controller
      db_name = session[:demo_db]
    else
      # Use default &#39;demo&#39; database
      db_name = default_demo_database
    end

    ActiveRecord::Base.establish_connection(demo_connection(db_name))
  end

  # Returns the current database configuration hash
  def default_connection_config
    @default_config ||= ActiveRecord::Base.connection.instance_variable_get(&quot;@config&quot;).dup
  end

  # Returns the connection hash but with database name changed
  # The argument should be a path
  def demo_connection(db_path)
    default_connection_config.dup.update(database: db_path)
  end

  # Returns the default demo database path defined in config/database.yml
  def default_demo_database
    return YAML.load_file(&quot;#{Rails.root.to_s}/config/database.yml&quot;)[&#39;demo&#39;][&#39;database&#39;]
  end
</code></pre></div>

<p class="c-pre-sidenote--left">Since every server session will have a different database, you will store the database filename in a session variable. As you can see, we are using <code>session[:demo_db]</code> to track the specific database for the user. The <code>set_demo_database</code> method is controlling which database to use by establishing the connection to the database set in the session variable. The <code>default_demo_database</code> method simply loads the path of the database as defined in the <code>database.yml</code> config file.</p>
<p class="c-sidenote c-sidenote--right">If you are using a bare language, at this point you can probably just update your database connection script to point to the new database and then move on to the next section. In Rails, things require a few more steps because it follows the "convention over configuration" software paradigm.</p>

## The Third Step: Duplicating The SQLite File

<p>Now that the app is set up to use the new database, we need a trigger for the new demo session. For simplicity&#39;s sake, start by just using a basic "Start Demo" button. You could also make it a form where you collect a name and email address (for a follow up from the sales team, etc.) or any number of things. </p>

<p>Sticking with Rails conventions, create a new &#39;Demo&#39; controller:</p>

<pre><code class="language-bash">rails generate controller demos new</code></pre>

<p>Next, you should update the routes to point to your new controller actions, wrapping them in a conditional to prevent it from being called in the production environment. You can name the routes however you want or name them using standard Rails conventions:</p>

<pre><code class="language-ruby">if Rails.env == &#39;demo&#39;
  get &#39;demos/new&#39;, as: &#39;new_demo&#39;
  post &#39;demos&#39; =&gt; &#39;demos#create&#39;, as: &#39;demos&#39;
end
</code></pre>

<p>Next, let&#39;s add a very basic form to the <code>views/demos/new.html.erb</code>. You may want to add additional form fields to capture:</p>

<pre><code class="language-markup">&lt;h1&gt;Start a Demo&lt;/h1&gt;
&lt;%= form_tag demos_path, method: :post do %&gt;
  &lt;%= submit_tag &#39;Start Demo&#39; %&gt;
&lt;% end %&gt;
</code></pre>

<p>The magic happens in the <code>create</code> action. When the user submits to this route, the action will copy the <code>demo.sqlite3</code> file with a new unique filename, set session variables, login the user (if applicable), and then redirect the user to the appropriate page (we will call this the &#39;dashboard&#39;). </p>

<div class="break-out">

<pre><code class="language-ruby">class DemosController &lt; ApplicationController
  def new
    # Optional: setting session[:demo_db] to nil will reset the demo
    session[:demo_db] = nil
  end

  def create
    # make db/demos dir if doesn&#39;t exist
    unless File.directory?(&#39;db/demos/&#39;)
      FileUtils.mkdir(&#39;db/demos/&#39;)
    end

    # copy master &#39;demo&#39; database
    master_db = default_demo_database
    demo_db = &quot;db/demos/demo-#{Time.now.to_i}.sqlite3&quot;
    FileUtils::cp master_db, demo_db

    # set session for new db
    session[:demo_db] = demo_db

    # Optional: login code (if applicable)
    # add your own login code or method here
    login(User.first)

    # Redirect to wherever you want to send the user next
    redirect_to dashboard_path
  end
end
</code></pre></div>

<p class="c-pre-sidenote--left">Now you should be able to try out the demo code locally by once again launching the server using running <code>rails server -e demo</code>.</p>
<p class="c-sidenote c-sidenote--right">If you had the server already running, you will need to restart it for any changes you make since it is configured to cache the code like the production server.</p>

<p class="c-pre-sidenote--left">Once all the code works as expected, commit your changes to your version control and be sure that you commit the <code>demo.sqlite3</code> file, but not the files in the <code>db/demos</code> directory. If you are using git, you can simply add the following to your <code>.gitignore</code> file:</p>
<p class="c-sidenote c-sidenote--right">If you want to collect additional information from the demo user (such as name and/or email), you will likely want to send that information via an API to either your main application or some other sales pipeline since your demo database will not be reliable (it resets every time you redeploy).</p>

<pre><code class="language-git">!/db/demo.sqlite3
db/demos/*
</code></pre>

## Final Step: Deploying Your Demo Server

<p>Now that you have your demo setup working locally, you will obviously want to deploy it so that everyone can use it. While every app is different, I would recommend that the demo app lives on a separate server and therefore domain as your production app (such as demo.myapp.com). This will ensure that you keep the two environments are isolated. Additionally, since the SQLite file is stored on the server, services like Heroku will not work as it does not provide access to the filesystem. However, you can still use practically any VPS provider (such as AWS EC2, Microsoft Azure, etc). If you like the automated convenience, there are other Platforms as Service options that allow you to work with VPS. </p>

<p>Regardless of your deployment process, you may also need to check that the app has the appropriate read/write permissions for your directory where you store the demo SQLite files. This could be handled manually or with a deployment hook. </p>

## SQLite Won&#39;t Work For Me. What About Other Database Systems?

<p>No two apps are created alike and neither are their database requirements. By using SQLite, you have the advantage of being able to quickly duplicate the database, as well as being able to store the file in version control. While I believe that SQLite will work for most situations (especially with Rails), there are situations where SQLite might not be suitable for your application&#39;s needs. Fortunately, it is still possible to use the same concepts above with other database systems. The process of duplicating a database will be slightly different for each system, but I will outline a solution for MySQL and a similar process exists with PostgreSQL and others. </p>

<p>The majority of the methods covered above work without any additional modifications. However, instead of storing a SQLite file in your version control, you should use <code>mysqldump</code> (or <code>pg_dump</code> for PostgreSQL) to export a SQL file of whichever database has the content that you would like to use for your demo experience. This file should also be stored in your version control. </p>

<p>The only changes to the previous code will be found in the <code>demos#create</code> action. Instead of copying the SQLite3 file, the controller action will create a new database, load the sql file into that database and grant permissions for the database user if necessary. The third step of granting access is only necessary if your database admin user is different from the user which the app uses to connect. The following code makes use of standard MySQL commands to handle these steps:</p>

<div class="break-out">

<pre><code class="language-ruby">def create
  # database names
  template_demo_db = default_demo_database
  new_demo_db = &quot;demo_database_#{Time.now.to_i}&quot;

  # Create database using admin credentials
  # In this example the database is on the same server so passing a host argument is not require
  `mysqladmin -u#{ ENV[&#39;DB_ADMIN&#39;] } -p#{ ENV[&#39;DB_ADMIN_PASSWORD&#39;] } create #{new_demo_db}`

  # Load template sql into new database
  # Update the path if it differs from where you saved the demo_template.sql file
  `mysql -u#{ ENV[&#39;DB_ADMIN&#39;] } -p#{ ENV[&#39;DB_ADMIN_PASSWORD&#39;] } #{new_demo_db} &lt; db/demo_template.sql`

  # Grant access to App user (if applicable)
  `mysql -u#{ ENV[&#39;DB_ADMIN&#39;] } -p#{ ENV[&#39;DB_ADMIN_PASSWORD&#39;] } -e &quot;GRANT ALL on #{new_demo_db}.* TO &#39;#{ ENV[&#39;DB_USERNAME&#39;] }&#39;@&#39;%&#39;;&quot;`

  # set session for new db
  session[:demo_db] = new_demo_db

  # Optional: login code (if applicable)
  # add your own login code or method here
  login(User.first)

  redirect_to dashboard_path
end
</code></pre></div>

<p>Ruby, like many other languages including PHP, allows you to use backticks to execute a shell command (i.e., <code>`ls -a`</code>) from within your code. However, you must use this with caution and ensure no user-facing parameters or variables can be inserted into the command to protect your server from maliciously <a href="https://en.wikipedia.org/wiki/Code_injection">injected code</a>. In this example, we are explicitly interacting with the MySQL command line tools, which is the only way to create a new database. This is the same way the Ruby on Rails framework creates a new database. Be sure to replace <code>ENV[&#39;DB_ADMIN&#39;]</code> and <code>ENV[&#39;DB_ADMIN_PASSWORD&#39;]</code> with either your own environment variable or any other way to set the database username. You will need to do the same for the <code>ENV[&#39;DB_USERNAME&#39;]</code> if your admin user is different from the user for your app.</p>

<p class="c-pre-sidenote--left">That&#39;s all that it takes to switch to MySQL! The most obvious advantage of this solution is that you don&#39;t have to worry about potential issues that might appear from the different syntax between database systems.</p>
<p class="c-sidenote c-sidenote--right">Eventually, a final decision is made based on the expected quality and service, rather than convenience and speed, and it’s not necessarily influenced by price point alone.</p>

## Final Thoughts

<p>This is just a starting point for what you can do with your new demo server. For example, your marketing website could have a link to "Try out feature XYZ." If you don't require a name or email, you could link <code>demos#create</code> method with a link such as <code>/demos/?feature=xyz</code> and the action would simply redirect to the desired feature and/or page, rather than the dashboard in the above example.</p>

<p>Also, if you use SQLite for the development and demo environments, always having this sample database in version control would give all your developers access to a clean database for use in local development, test environments or quality assurance testing. The possibilities are endless.</p>

<p>You can download a completed demo from <a href="https://github.com/jpegjames/a-little-saas">GitHub</a>.</p>

{{< signature "rb, ra, il" >}}

