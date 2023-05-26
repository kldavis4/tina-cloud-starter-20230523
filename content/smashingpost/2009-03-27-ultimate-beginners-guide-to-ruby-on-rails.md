---
title: 'Beginner’s Guide To Ruby On Rails: Part 2'
slug: ultimate-beginners-guide-to-ruby-on-rails
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ac5b70fe-9bbe-4856-94c3-25b483eb0acd/illufooter.gif
date: 2009-03-27T08:57:33.000Z
author: jan-varwig
description: >-
  Last week we published [Getting Started With Ruby On Rails](https://www.smashingmagazine.com/2009/03/19/getting-started-with-ruby-on-rails/), the first part of our Ruby On Rails introduction. We explained basic ideas behind Ruby and presented concepts and essential components of the language.
categories:
  - Coding
  - Ruby on Rails
---
In this article you'll learn more about Rails, you will learn how to get Ruby on Rails running on your computer, and get an overview of the basic functionality of Rails and demonstrate how Rails’ main parts work together.

I assume you're <strong>already familiar with some other form of Web development</strong>, whether PHP, Python, Perl or Java, and relational databases like MySQL. First, we'll introduce Rails and Ruby and the basic ideas behind both. I'll teach you just enough Ruby so that you understand the code samples. I'll tell you how to get Ruby on Rails running on your computer, and I'll give you an overview of the basic functionality of Rails and demonstrate how Rails' main parts work together.

After reading these parts, you should have an idea of whether Rails is for you. If you get the feeling that it is, I'll point you to some good tutorials on the Web that you can use to learn Rails. I'll also provide a lot of further reading recommendations so you can dig as deep into the topic as you like.

You may want to take a look at the following related posts:

*   [Getting Started With Ruby On Rails: Part 1](https://www.smashingmagazine.com/2009/03/19/getting-started-with-ruby-on-rails/)
*   [10 Useful Tips For Ruby On Rails Developers](https://www.smashingmagazine.com/2009/02/25/ruby-on-rails-tips/)

{{% feature-panel %}}

## Get Rolling

To get your feet wet with Rails, it's best to simply install it on your own machine and start playing around. This requires just a few steps.

On Windows do the following:

1.  **Install Ruby 1.8.6** using the one-click installer from [www.ruby-lang.org](https://www.ruby-lang.org/). Make sure to select “Enable Rubygems” during installation. It's probably a good idea to install ruby as admin.
2.  **Update Rubygems**. Rubygems is Ruby's package management system, and Rails needs a newer version than the one that ships with the installer. To do this, execute `gem update --system` in the console as admin. Next, you'll need to add the [GitHub](https://www.github.com/) gem server to Rubygems with `gem sources -a https://gems.github.com`
3.  **Install Rails** and its dependencies with `gem install rails` and `gem install mysql`. (You can use other databases, but MySQL is the easiest to set up.)
4.  Install the **MySQL Database** from [mysql.com](https://www.mysql.com/). If you've done Web development before, you probably already have it on your machine.
5.  **Create a Rails application**. Enter `rails -d mysql <appname>`. "Appname" will be the name of the sub-directory your app is created in.
6.  Go into the created application's directory and execute `ruby script/server`. Point your browser to `localhost:3000`. You should see the **Rails welcome page**. Follow its instructions.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dcbac1c8-bbbe-4230-98fe-eb43868664e7/rails-welcome.jpg" alt="" />

To edit Ruby code, you can use any text editor. If you just <em>have</em> to have a fancy IDE, try <a href="https://www.netbeans.org">NetBeans</a>. I recommend <a href="https://notepad-plus.sourceforge.net/">Notepad++</a>, a great, lightweight freeware editor.

On a Mac, you're lucky. <strong>Mac OS 10.5</strong> comes with Ruby, Rails and SqLite3. You just need to update your packages by issuing a few commands:

<pre><code class="language-markup tmp-ruby">sudo gem install rubygems-update
sudo update_rubygems

gem install rails
gem install mongrel</code></pre>

If you need more detailed help on installing Rails on <strong>10.4 Tiger</strong>, check out the tutorial on the Rails wiki or in <a href="https://craiccomputing.blogspot.com/2008/11/installing-rails-22-on-mac-os-x-mysql.html">this blog post</a>. Now you can create your app with <code>rails &lt;appname&gt;</code>.

On Linux, the installation depends on your distribution.</p>

## A Bird's Eye View Of Rails' Inner Workings

This is the part I find missing in most other tutorials about any topic. I want to present an <strong>overview</strong> of the most important components of Ruby on Rails to help you understand how they work together to process requests. I will be more detailed in the controller section because that's the most important one, and if I left things out there I wouldn't be able to paint the whole picture.</p>

### Controller

When the request hits your server running the Rails app, the first component handling it is the <strong>ActionController</strong>.

The ActionController and all of its parts correspond to the controller-part of the MVC stack. Before actually handling the request, the ActionController inspects it to determine which of the controllers in your application is responsible for the request.

These lookups are called <strong>routes</strong> and are defined in <code>config/routes.rb</code>. If you take a look in that file, you'll see lines similar to these:

<pre><code class="language-markup tmp-ruby">ActionController::Routing::Routes.draw do |map|
  map.resources :users map.connect ':controller/:action/:id'
end</code></pre>

The details of route definition could fill an article of their own. If you're interested in its precise workings, take a look at the <code>ActionController::Routing</code> documentation in the  Rails API.

Simplified, two kind of routes appear here. The last one is the <strong>traditional style</strong> of defining routes. These are formed like simple regular expressions, with the <code>:foo</code> part being a placeholder.

If a request's URL matches one of these expressions, its parts are mapped to the placeholders. These are then examined to determine the correct controller, the action within the controller and further parameters like <code>id</code> (<code>id</code> always contains the id of the object that the client wants to work with). For example, a URL like <code>/foo/bar/123</code> would be mapped to the <code>FooController</code>; the <code>bar</code> action and the value of <code>params[:id]</code> would be <code>123</code>.

The first line is a shortcut to create a large number of those routes in one sweep. Routes created this way adhere to the <a href="https://en.wikipedia.org/wiki/Representational_State_Transfer">REST principles</a>. Again, this is a topic large enough to warrant its own article. For the sake of this introduction, let me just illustrate the effect of <code>map.resources :users</code> as an example. If you put such a line in your <code>routes.rb</code> you're telling Rails that you want <em>users</em> to be a <strong>resource</strong>. That means seven routes are installed that all point to the <code>UserController</code>.
These seven routes match not only against the URL of the request but also the HTTP method. The mappings are:

<pre><code class="language-markup tmp-ruby">GET      /users            # will point to the index action
GET      /users/new        # will point to the new action
POST     /users            # will point to the create action
GET      /users/:id        # will point to the show action
GET      /users/:id/edit   # will point to the edit action
PUT      /users/:id        # will point to the update action
DELETE   /users/:id        # will point to the destroy action</code></pre>

All of these actions of the <code>UserController</code> are expected to behave in certain ways.

*   The `index` action should display a list of all existing users.
*   The `new` action should display a form for the creation of a new user that is submitted to `/users` via `POST`.
*   The `create` action should take the form's input and create a new user in the database.
*   The `show` action should display the user with the corresponding id.
*   The `edit` action should display a form for editing the user. The form should submit to `/users/:id/` via `PUT`.
*   The `update` action receives the form data and updates the user in the database.
*   The `destroy` action deletes the user from the database.

Because <code>PUT</code> and <code>DELETE</code> aren't supported by all browsers, forms that are supposed to use these methods submit via <code>POST</code> and tell the server their <em>intended</em> method via a hidden form field named <code>_method</code>.

Once controller, action and parameters are determined, the action can be called. But before that actually happens, Rails inspects the <strong>filter chain</strong> for the action to see if there are any filters to be executed before the action runs. Such filters are incredibly useful for things like user authentication. To ensure that only logged-in users of your application can access certain actions, you would define a filter that checks the session for valid credentials. Such a filter could look like this:

<pre><code class="language-markup tmp-ruby">class UserController &lt; ApplicationController

  # Require valid login to access the update action before_filter(:require_login, :only =&gt; :update)

  # Lots of actions defined here
  # ...
  # ...

private

  def require_login
    render(:text =&gt; "Unauthorized", :status =&gt; 401) unless session[:user_valid]
  end

end</code></pre>

Let's analyze this example line by line. The UserController inherits from the ApplicationController. All of your controllers should. The ApplicationController can then contain code that should be <strong>shared among all the controllers</strong> in your application. You could, for example, put the <code>require_login</code> filter in there to require a valid log-in for <em>all</em> your controllers.

The next line declares a before filter. By making the declaration using the symbol <code>:require_login</code>, you're telling Rails to use the <code>require_login</code> method as a filter. This alone would apply the filter to all actions
in the UserController. The additional parameter <code>:only =&gt; :update</code> tells Rails to use the filter only when the client wants to access the <code>update</code> action. In a real controller, this line would be followed by the definitions of all the actions your controller contains. In this example, they're omitted for brevity.

The keyword <code>private</code> marks all the methods defined afterward as private to the UserController. This implies that they can't be used as actions. We don't want <code>require_login</code> to be used as an action, so we're putting it here.

<code>Require_login</code> checks if the field <code>:user_valid</code> in the session is present. This is, of course, a pretty drastic simplification of a real authentication scheme, but it's sufficient for the sake of illustrating filters. Unless a user is logged in, the filter renders a simple error message.

Now, here's a detail you need to know to understand this. Rails works through all the filters applying to an action and only <strong>aborts request processing</strong> for three reasons:

1.  A filter raises an Error.
2.  A filter returns false.
3.  A filter renders somethings or redirects.

So, this single line is all that is needed to protect our sensitive actions against malicious clients. Again, I'm simplifying this a bit. To make an application really secure, you will of course need a little bit more code to properly maintain session state. To find out more about filters, read the <code>ActionController::Filters::ClassMethods</code> documentation in the Rails API.

Let's see how Rails continues with the processing of the request.

![](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/96f29e87-a64a-40ba-ba2a-e01da2183210/request.jpg)

After the client's request has passed all filters, the action finally executes. Let's run with our example from the filters section and assume the client wants to execute the <code>update</code> action after editing the user in a <code>from</code> provided by the <code>edit</code> action. Both actions could be defined like this:

<pre><code class="language-markup tmp-ruby">def edit
  @user = User.find(params[:id])
end

def update
  @user = User.find(params[:id])
  if @user.update_attributes(params[:user])
    redirect_to users_url else
    render :action =&gt; :edit end
end</code></pre>

Let's work through this line by line again. First, note that <strong>actions are defined as simple parameter-less methods on the controller</strong>. Their input and output is realized a little differently from what you'd expect from a method. Actions retrieve all the information they need to process the request from their controller through a few accessors, mainly <code>params</code> and <code>session</code>. There are more (<code>cookies</code>, <code>request</code>), but they're not used nearly as often as these two, and I don't want to complicate matters more than is necessary here.

The <code>params</code> method returns all the <strong>parameters of a request</strong>. These usually result from its querystrings or the postbody, but can also be created from JSON or XML data structures. Through routes, parts of the URL can also become parameters. This is where the <code>:id</code> parameter in the example is read from. If the client requests <code>/users/123/edit/</code> and we have a route definition <code>map.resources :users</code>, then 123 becomes the <code>:id</code> parameter for the edit action, because the route definition generates (among others) a route that looks like this:

<pre><code class="language-markup tmp-ruby">map.route '/users/:id/edit',
          :controller =&gt; 'users',
          :action     =&gt; 'edit',
          :method     =&gt; :get

&lt;!-- The "session" method can be used to access data in the session. Whatever you put in here will be available in subsequent actions in the same session. This is commonly used to store log-in information or things like shopping cart contents. --&gt;</code></pre>

For output, an action basically has two options. It can either <strong>redirect the user or render a template</strong>. The templates for a Rails application are organized the same way the controllers are. They reside in <code>app/templates/&lt;controllername&gt;/&lt;action&gt;.html.erb</code>, and if no output is specified in the action, Rails renders the template belonging to that action by default. That's why you don't see any output code in the edit action. The only line in <code>edit</code> pulls the user we want to edit out of the database and puts it into an instance variable of the controller to make it available to the template.

The <code>update</code> action begins with the same statement, again fetching the user form the database. In its next step, the user's attributes are updated with the data that the action received from the client-side form. The update returns <em>true</em> on success. In this case, the client is redirected to the list of users.

This redirection deserves closer inspection. The <code>redirect_to</code> command takes a URL, but instead of hard-coding these URLs (<code>/users</code> in this case), it is conventional to use URL helpers like <code>users_url</code>. The helpers are generated automatically by the route or resource definitions.

If updating the user's attributes does not succeed, two things happen inside the <code>update_attributes</code> call. First the user's <code>errors</code> property will be filled with details on why the update didn't succeed, and the call will return false instead of true. As a result, the client is not redirected; instead, <code>render</code> is called, with <code>:action =&gt; :edit</code> as its parameter. This tells <code>render</code> to render the template belonging to the <code>edit</code> action of the current controller.

Why not redirect to the edit action, you may ask? We could do that, but we'd lose all the edits we made to the user and lose information on the errors that occurred. When the edit-template is rendered instead during the processing of the <code>update</code> action, <strong>the user that failed to update is still in memory with all its pending edits and the errors</strong>. We can use this data in the template to pre-fill the form with the values we just entered (but didn't save to the database) and provide information to the client on what went wrong.

There's one last important thing to note here about <code>render</code> and <code>redirect_to</code>. It is not apparent from these examples, but <strong>calling <code>render</code> or <code>redirect_to</code> does not stop the processing of the action</strong>. These are both just methods and not special control flow statements. So, when <code>render</code> is called, the template isn't rendered yet; rather, the controller renders the template <em>after</em> the action has processed. Any statements following a <code>render</code> are still executed.</p>

### Model

The second important part of MVC in Rails is the Model. Its role is played by the <strong>ActiveRecord</strong> module, an implementation of the <a title="P of EAA: Active Record" href="https://martinfowler.com/eaaCatalog/activeRecord.html">pattern of the same name</a>. ActiveRecord::Base functions as a base class for the models in your application. If you derive your models from this class, you'll have them <strong>automatically linked to tables in your database</strong> and can very easily load, edit, save, create, delete or list them. Mappings between the structure and behavior of your models and the tables in the database are fully automated mostly, provided that you adhere to a few rules in the design of your tables. The general principles are:

1.  Your table name is the pluralized, underscored variant of your classname. So, a class `User` would be mapped to the table `users`.`CookieRecipe` would be mapped to `cookie_recipes`.
2.  Your table needs to have its primary key on an integer column called `id` with the `auto increment` property.
3.  Associations to other tables are stored in columns that are named after them. If you want to store posts belonging to a user, the `posts` table would need a `user_id` column

![](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/38c3e624-b1b6-4245-8648-43d615bac1c2/active-record.jpg)

If you have a table and class that are connected via their name, like <code>users</code> and <code>User</code>, any column in the table is available on the model as a property. If you want to create a User, you'd just instantiate an object in Rails:

<pre><code class="language-markup tmp-ruby">u = User.new</code></pre>

Then you can begin setting its properties:

<pre><code class="language-markup tmp-ruby">u.name = "Michael"
u.age  = 35</code></pre>

You could also provide these settings upon creation:

<pre><code class="language-markup tmp-ruby">u = User.new(:name =&gt; "Michael", :age =&gt; 35)</code></pre>

To store the new user in the database, tell it to save:

<pre><code class="language-markup tmp-ruby">u.save</code></pre>

You can find records in a lot of ways:

<pre><code class="language-markup tmp-ruby">u = User.find(123)               # finds the user with id 123
u = User.find(:all)              # returns an array containing all users
u = User.find_by_name("Michael") # a "magic" finder</code></pre>

I don't want to go into the details of all of these options. You can find them all in the ActiveRecord::Base module documentation in the Rails API. I'd rather introduce two important features of ActiveRecord: <strong>associations</strong> and validations.

I have already mentioned associations briefly and given an example of <em>posts</em> belonging to <em>users</em>. How would you actually implement that? Well, as mentioned, you first put a <code>user_id</code> column in the <code>posts</code> table to link the two tables. Then you need to make your models aware of the link (unfortunately, it doesn't do that automatically). But don't worry, you only need two lines of code for that:

<pre><code class="language-markup tmp-ruby">class User &lt; ActiveRecord::Base has_many :posts
end

class Post &lt; ActiveRecord::Base belongs_to :user
end</code></pre>

That's it. These two lines make helpers available in both models that allow for navigating the models. Given a post, you could access its user via <code>post.user</code> or get all posts of a user by saying <code>user.posts</code>.

<strong>Validations</strong> are constraints that you can define in your model to ensure that the model is only saved to the database if those constraints are met. Rails provides a lot of predefined validations that ensure that a property isn't empty, is within a certain numeric range or matches a regular expression. But you can basically use anything you can write down in code as a validation. Say you want to ensure that your posts have titles not longer than 100 characters and that the post body is always present. You would extend your <code>Post</code> class like this:

<pre><code class="language-markup tmp-ruby">class Post &lt; ActiveRecord::Base belongs_to :user

  validates_presence_of :body validates_length_of   :title, :maximum =&gt; 100
end</code></pre>

A call to the <code>save</code> method on a post that doesn't comply with these restrictions will return <em>false</em>, and the post will not be saved to the database. You can then examine the post's <strong><em>errors</em> object</strong> by accessing <code>post.errors</code> and communicate to the users what went wrong. The Rails-provided validations all come with descriptive error messages that you could retrieve with <code>post.errors.full_messages</code>, for example.

ActiveRecord has a lot more depth and functionality than presented here. Even complex models and their relations can be handled pretty comfortably. But presenting all this exceeds the scope of this article. The API doesn't help much if you want to explore all these possibilities; so, to get a deeper introduction, I recommend the <a href="https://www.railsenvy.com/2007/8/8/activerecord-tutorial">Rails Envy ActiveRecord tutorial</a>.</p>

### View

We're almost at the end of our overview. The last missing part is MVC's <em>V</em>, the <em>View</em>. All the components related to this are aggregated under the <strong>ActionView</strong> module. At the core of Rails' views are the <em>ERB templates</em>, but they are backed by a large library of helpers that can be used to generate forms, URLs, sub-templates and other little tools that can make your life easier.

In the controller example, I talked about how the <code>render</code> method is used to render a template. An action that doesn't explicitly render or redirect automatically renders its corresponding template in <code>app/templates/&lt;controller&gt;/&lt;action&gt;.html.erb</code>. The file extension <code>.erb</code> stands for "Embedded Ruby," and that's what the templates are: HTML files that are dynamically filled with content through the use of special script tags that contain Ruby code. These special tags work very similar to the ones PHP uses. Let's take a look at an example:

<pre><code class="language-markup tmp-ruby">&lt;html&gt;
  &lt;head&gt;
    &lt;title&gt;&lt;%= @pagetitle %&gt;&lt;/title&gt;
  &lt;/head&gt;
  &lt;body&gt;
    &lt;h1&gt;Post: &lt;%= h @post.title %&gt;&lt;/h1&gt;
    &lt;p&gt;Written on &lt;%= @post.date %&gt;&lt;/p&gt;

    &lt;div id="postcontent"&gt;
      &lt;%= h @post.content %&gt;
    &lt;/div&gt;

    &lt;% if @post.user.posts.count &gt; 1 %&gt;
      &lt;p&gt;Other posts by &lt;%= @post.user.name %&gt;:&lt;/p&gt;
      &lt;ul&gt;
        &lt;% @post.user.posts.each do |post| %&gt;
          &lt;li&gt;&lt;%= h post.title %&gt;&lt;/li&gt;
        &lt;% end %&gt;
      &lt;/ul&gt;
    &lt;% end %&gt;
  &lt;/body&gt;
&lt;/html&gt;</code></pre>

Tags beginning with <code>&lt;%=</code> <strong>evaluate the expression they contain and insert them into the document</strong>. The little <code>h</code> you see sometimes is a helper function provided by ActionView that escapes characters that are not valid HTML. You should always use this if you're displaying user-entered content to prevent cross-site scripting attacks.

Below the postcontent div, you can see another type of erb tag, without the equals sign. This means that its content is <strong>executed but not inserted into the document</strong>. We're opening a conditional statement here. Everything between the <code>if</code> and the <code>end</code> will only be executed if the current post's user has other posts. This affects both Ruby and HTML code.

The next tag is also pretty interesting and different from the ones used before. We're combining the power of Ruby blocks here with ERB to iterate over a user's posts. The <code>each</code> method executes its block for each of the members of a collection and makes the current member available to the block. I've called the block's parameter <code>post</code> here, so we can refer to the current post under this name within the block. In ERB, you can put HTML within blocks just as if it were code.

You'll notice that I'm using two instance variables in this template, <code>@pagetitle</code> and <code>@post</code>. They are the main means of <strong>passing data from the controller to the template</strong>. Instance variables that exist in the controller can also be accessed in the template. It's that simple.

From the content of the page, you can see that we're probably rendering the <code>show</code> action of a <code>post</code>'s resource here. The controller action to feed this template with data could look like this:

<pre><code class="language-markup tmp-ruby">def show
  @post = Post.find(params[:id)
end</code></pre>

The <code>@pagetitle</code> could be the result of a before filter:

<pre><code class="language-markup tmp-ruby">before_filter :set_title
def set_title
  @pagetitle = "Showing Post #{params[:id]}"
end</code></pre>

Rails' templates can harness the full power of the Ruby language and have access to the full stack right down to the models. This <strong>power can easily be misused</strong> to put controller logic or model operations into the templates. But you're only hurting yourself (and your colleagues) if you do that. You should only put code in the templates that is directly related to displaying data.

As with ActiveRecord, this only scratches the surface of what's possible with ActionView. Three of the most useful features not introduced here are:

*   Layouts that can be nested so that you don't have to repeat identical structures in your templates over and over.
*   Partials, small template snippets that can be used to render collections and inserted into other templates
*   Generation of JSON and XML to create Web services, AJAX interfaces and RSS feeds.

To go deeper into the topic, check out the <a title="Layouts and Rendering in Rails" href="https://guides.rubyonrails.org/layouts_and_rendering.html">Layouts and Rendering in Rails</a> guide on Rails Guides.</p>

## Learning _From_ Rails

Rails takes Ruby's aim of increasing programmer productivity and happiness and applies it to Web frameworks. Its debut was a truly revelatory experience because it showed developers that that power doesn't have to come with the clumsiness that other frameworks exhibited at the time.

Today, the ideas of Rails can be found in many imitators in other languages, but if you're not tied to any one of them, Ruby on Rails is definitely worth checking out. You'll rediscover the fun in programming, and even if you don't stick with Rails, you definitely won't regret the learning experience.

The greatest thing about Rails, however, is how it can change your perception of programming in general once you understand its design and the reasons behind it.

First, simply using Ruby -- a language that's quite different from ones you've used before, yet similar enough not to be totally alienating -- opens up your mind to <strong>new ways of thinking</strong> and new ways of perceiving programming languages. You'll suddenly begin to question things you've taken for granted. You'll frown at first on the prospect of opening up and redefining core classes at runtime, but once you've done it and seen that your program still runs and looks nicer than before, you'll appreciate the flexibility and also become a more responsible programmer. You'll curse every semicolon and every empty pair of braces that other languages force upon you.

For many programmers, Ruby even paved the way to radically different territory, namely <strong>functional programming</strong>. Ruby is an imperative language, but its treatment of code blocks as objects equal to Strings, Numbers or any other class and its support of closures will slowly prepare your mind for languages like Lisp, Haskell and OCaml, where passing around functions is the predominant way of writing programs. You'll have a much broader palette of solutions for the problems you're tackling each day, and those problems will stop looking like all nails.

Rails very much builds upon these wisdoms and makes much use of meta-programming (class rewriting) and functional programming principles. In this way, Rails becomes more than a framework, and becomes rather a <a title="Agile DSL Development in Ruby" href="https://www.slideshare.net/adorepump/agile-dsl-development-in-ruby-presentation">domain-specific language for writing Web applications</a>. The exploitation of Ruby's dynamic features enables a brevity in Rails' API that does <strong>not obscure your code's intention</strong>. After using Rails for a while, you'll start to develop your own programs in this way.

Rails encourages <strong>strict separation of code</strong> between your models, controllers and views. Once you've written an app in this straightjacket, you'll begin to see its tremendous benefits. You will develop a sharper eye for the correct location of code. Things you've put in your controllers in the past will take their place in the models, and your design will become more fluent, cleaner and more flexible, especially if you let Rails encourage you to thoroughly test your app.

Even if your flirtation with Rails doesn't turn into a long-term relationship, you'll gain invaluable experiences that will improve your style in whatever you develop in future.</p>

## Further resources

In the hope that your interest has now been piqued and you have an idea of what to expect, I'd like to point you to some resources that will really teach you how to write Web application in Rails.

Further, I'll point you to some important sources of news, because despite its maturity, Rails is moving at blazing speeds. Don't misunderstand me: you won't have to study new features each week to keep up with programming in Rails, but by monitoring the right news sources, you'll learn invaluable tips and tricks that you won't find in the tutorials.

First of all, there are <strong>books</strong>. The advantage of computer books is that they're usually comprehensive and professionally edited. The disadvantage is that most of them are outdated by the day they hit the shelves. So, the only books you should really bother reading are the ones that are just out. Fortunately, the standard Rails manual, "Agile Web Development with Rails" is just receiving the finishing touches for its third edition, which will cover the most recent changes in the framework. It's good for beginners and doesn't go very deep, but that's okay. If you want to go deep, you can just read blog articles about the subjects you're interested in after you're done with the book.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b188bb1f-f904-4f7c-9168-595ab70a8a30/awdr.jpg" alt="" /> <img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/04e2b673-bfa6-4cc8-ac44-58062d187879/pickaxe.jpg" alt="" /> <img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a827f174-1640-469d-a0da-febc50e09ccd/rubyway.jpg" alt="" />

To learn Ruby, you could try <em>Programming Ruby</em> (the "Pickaxe"), the guide written by the Pragmatic Programmers that first brought Ruby to the west. Its <a title="Programming Ruby: The Pragmatic Programmer's Guide" href="https://ruby-doc.org/docs/ProgrammingRuby/">first edition is even free</a> and can be found at <a href="https://ruby-doc.org/">ruby-doc.org</a> alongside the <a title="RDoc Documentation" href="https://ruby-doc.org/core/">official Ruby API</a>. The second (and upcoming third) edition is definitely worth the money, though, especially for its chapter about the inner details of Ruby's object and method dispatch system.

People who don't like the Pickaxe usually recommend Hal Fulton's "The Ruby Way," which teaches the language in a more task-oriented way.

<pre><code class="language-markup tmp-ruby">u.save</code></pre>

You can find records in a lot of ways:

<pre><code class="language-markup tmp-ruby">u = User.find(123)               # finds the user with id 123
u = User.find(:all)              # returns an array containing all users
u = User.find_by_name("Michael") # a "magic" finder</code></pre>

I don't want to go into the details of all of these options. You can find them all in the ActiveRecord::Base module documentation in the Rails API. I'd rather introduce two important features of ActiveRecord: <strong>associations</strong> and validations.

I have already mentioned associations briefly and given an example of <em>posts</em> belonging to <em>users</em>. How would you actually implement that? Well, as mentioned, you first put a <code>user_id</code> column in the <code>posts</code> table to link the two tables. Then you need to make your models aware of the link (unfortunately, it doesn't do that automatically). But don't worry, you only need two lines of code for that:

<pre><code class="language-markup tmp-ruby">class User &lt; ActiveRecord::Base has_many :posts
end

class Post &lt; ActiveRecord::Base belongs_to :user
end</code></pre>

That's it. These two lines make helpers available in both models that allow for navigating the models. Given a post, you could access its user via <code>post.user</code> or get all posts of a user by saying <code>user.posts</code>.

<strong>Validations</strong> are constraints that you can define in your model to ensure that the model is only saved to the database if those constraints are met. Rails provides a lot of predefined validations that ensure that a property isn't empty, is within a certain numeric range or matches a regular expression. But you can basically use anything you can write down in code as a validation. Say you want to ensure that your posts have titles not longer than 100 characters and that the post body is always present. You would extend your <code>Post</code> class like this:

<pre><code class="language-markup tmp-ruby">class Post &lt; ActiveRecord::Base belongs_to :user

  validates_presence_of :body validates_length_of   :title, :maximum =&gt; 100
end</code></pre>

A call to the <code>save</code> method on a post that doesn't comply with these restrictions will return <em>false</em>, and the post will not be saved to the database. You can then examine the post's <strong><em>errors</em> object</strong> by accessing <code>post.errors</code> and communicate to the users what went wrong. The Rails-provided validations all come with descriptive error messages that you could retrieve with <code>post.errors.full_messages</code>, for example.

ActiveRecord has a lot more depth and functionality than presented here. Even complex models and their relations can be handled pretty comfortably. But presenting all this exceeds the scope of this article. The API doesn't help much if you want to explore all these possibilities; so, to get a deeper introduction, I recommend the <a href="https://www.railsenvy.com/2007/8/8/activerecord-tutorial">Rails Envy ActiveRecord tutorial</a>.</p>

### View

We're almost at the end of our overview. The last missing part is MVC's <em>V</em>, the <em>View</em>. All the components related to this are aggregated under the <strong>ActionView</strong> module. At the core of Rails' views are the <em>ERB templates</em>, but they are backed by a large library of helpers that can be used to generate forms, URLs, sub-templates and other little tools that can make your life easier.

In the controller example, I talked about how the <code>render</code> method is used to render a template. An action that doesn't explicitly render or redirect automatically renders its corresponding template in <code>app/templates/&lt;controller&gt;/&lt;action&gt;.html.erb</code>. The file extension <code>.erb</code> stands for "Embedded Ruby," and that's what the templates are: HTML files that are dynamically filled with content through the use of special script tags that contain Ruby code. These special tags work very similar to the ones PHP uses. Let's take a look at an example:

<pre><code class="language-markup tmp-ruby">&lt;html&gt;
  &lt;head&gt;
    &lt;title&gt;&lt;%= @pagetitle %&gt;&lt;/title&gt;
  &lt;/head&gt;
  &lt;body&gt;
    &lt;h1&gt;Post: &lt;%= h @post.title %&gt;&lt;/h1&gt;
    &lt;p&gt;Written on &lt;%= @post.date %&gt;&lt;/p&gt;

    &lt;div id="postcontent"&gt;
      &lt;%= h @post.content %&gt;
    &lt;/div&gt;

    &lt;% if @post.user.posts.count &gt; 1 %&gt;
      &lt;p&gt;Other posts by &lt;%= @post.user.name %&gt;:&lt;/p&gt;
      &lt;ul&gt;
        &lt;% @post.user.posts.each do |post| %&gt;
          &lt;li&gt;&lt;%= h post.title %&gt;&lt;/li&gt;
        &lt;% end %&gt;
      &lt;/ul&gt;
    &lt;% end %&gt;
  &lt;/body&gt;
&lt;/html&gt;</code></pre>

Tags beginning with <code>&lt;%=</code> <strong>evaluate the expression they contain and insert them into the document</strong>. The little <code>h</code> you see sometimes is a helper function provided by ActionView that escapes characters that are not valid HTML. You should always use this if you're displaying user-entered content to prevent cross-site scripting attacks.

Below the postcontent div, you can see another type of erb tag, without the equals sign. This means that its content is <strong>executed but not inserted into the document</strong>. We're opening a conditional statement here. Everything between the <code>if</code> and the <code>end</code> will only be executed if the current post's user has other posts. This affects both Ruby and HTML code.

The next tag is also pretty interesting and different from the ones used before. We're combining the power of Ruby blocks here with ERB to iterate over a user's posts. The <code>each</code> method executes its block for each of the members of a collection and makes the current member available to the block. I've called the block's parameter <code>post</code> here, so we can refer to the current post under this name within the block. In ERB, you can put HTML within blocks just as if it were code.

You'll notice that I'm using two instance variables in this template, <code>@pagetitle</code> and <code>@post</code>. They are the main means of <strong>passing data from the controller to the template</strong>. Instance variables that exist in the controller can also be accessed in the template. It's that simple.

From the content of the page, you can see that we're probably rendering the <code>show</code> action of a <code>post</code>'s resource here. The controller action to feed this template with data could look like this:

<pre><code class="language-markup tmp-ruby">def show
  @post = Post.find(params[:id)
end</code></pre>

The <code>@pagetitle</code> could be the result of a before filter:

<pre><code class="language-markup tmp-ruby">before_filter :set_title
def set_title
  @pagetitle = "Showing Post #{params[:id]}"
end</code></pre>

Rails' templates can harness the full power of the Ruby language and have access to the full stack right down to the models. This <strong>power can easily be misused</strong> to put controller logic or model operations into the templates. But you're only hurting yourself (and your colleagues) if you do that. You should only put code in the templates that is directly related to displaying data.

As with ActiveRecord, this only scratches the surface of what's possible with ActionView. Three of the most useful features not introduced here are:

*   Layouts that can be nested so that you don't have to repeat identical structures in your templates over and over.
*   Partials, small template snippets that can be used to render collections and inserted into other templates
*   Generation of JSON and XML to create Web services, AJAX interfaces and RSS feeds.

To go deeper into the topic, check out the <a title="Layouts and Rendering in Rails" href="https://guides.rubyonrails.org/layouts_and_rendering.html">Layouts and Rendering in Rails</a> guide on Rails Guides.</p>

## Learning _From_ Rails

Rails takes Ruby's aim of increasing programmer productivity and happiness and applies it to Web frameworks. Its debut was a truly revelatory experience because it showed developers that that power doesn't have to come with the clumsiness that other frameworks exhibited at the time.

Today, the ideas of Rails can be found in many imitators in other languages, but if you're not tied to any one of them, Ruby on Rails is definitely worth checking out. You'll rediscover the fun in programming, and even if you don't stick with Rails, you definitely won't regret the learning experience.

The greatest thing about Rails, however, is how it can change your perception of programming in general once you understand its design and the reasons behind it.

First, simply using Ruby -- a language that's quite different from ones you've used before, yet similar enough not to be totally alienating -- opens up your mind to <strong>new ways of thinking</strong> and new ways of perceiving programming languages. You'll suddenly begin to question things you've taken for granted. You'll frown at first on the prospect of opening up and redefining core classes at runtime, but once you've done it and seen that your program still runs and looks nicer than before, you'll appreciate the flexibility and also become a more responsible programmer. You'll curse every semicolon and every empty pair of braces that other languages force upon you.

For many programmers, Ruby even paved the way to radically different territory, namely <strong>functional programming</strong>. Ruby is an imperative language, but its treatment of code blocks as objects equal to Strings, Numbers or any other class and its support of closures will slowly prepare your mind for languages like Lisp, Haskell and OCaml, where passing around functions is the predominant way of writing programs. You'll have a much broader palette of solutions for the problems you're tackling each day, and those problems will stop looking like all nails.

Rails very much builds upon these wisdoms and makes much use of meta-programming (class rewriting) and functional programming principles. In this way, Rails becomes more than a framework, and becomes rather a <a title="Agile DSL Development in Ruby" href="https://www.slideshare.net/adorepump/agile-dsl-development-in-ruby-presentation">domain-specific language for writing Web applications</a>. The exploitation of Ruby's dynamic features enables a brevity in Rails' API that does <strong>not obscure your code's intention</strong>. After using Rails for a while, you'll start to develop your own programs in this way.

Rails encourages <strong>strict separation of code</strong> between your models, controllers and views. Once you've written an app in this straightjacket, you'll begin to see its tremendous benefits. You will develop a sharper eye for the correct location of code. Things you've put in your controllers in the past will take their place in the models, and your design will become more fluent, cleaner and more flexible, especially if you let Rails encourage you to thoroughly test your app.

Even if your flirtation with Rails doesn't turn into a long-term relationship, you'll gain invaluable experiences that will improve your style in whatever you develop in future.</p>

## Further resources

In the hope that your interest has now been piqued and you have an idea of what to expect, I'd like to point you to some resources that will really teach you how to write Web application in Rails.

Further, I'll point you to some important sources of news, because despite its maturity, Rails is moving at blazing speeds. Don't misunderstand me: you won't have to study new features each week to keep up with programming in Rails, but by monitoring the right news sources, you'll learn invaluable tips and tricks that you won't find in the tutorials.

First of all, there are <strong>books</strong>. The advantage of computer books is that they're usually comprehensive and professionally edited. The disadvantage is that most of them are outdated by the day they hit the shelves. So, the only books you should really bother reading are the ones that are just out. Fortunately, the standard Rails manual, "Agile Web Development with Rails" is just receiving the finishing touches for its third edition, which will cover the most recent changes in the framework. It's good for beginners and doesn't go very deep, but that's okay. If you want to go deep, you can just read blog articles about the subjects you're interested in after you're done with the book.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b188bb1f-f904-4f7c-9168-595ab70a8a30/awdr.jpg" alt="" /> <img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/04e2b673-bfa6-4cc8-ac44-58062d187879/pickaxe.jpg" alt="" /> <img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a827f174-1640-469d-a0da-febc50e09ccd/rubyway.jpg" alt="" />

To learn Ruby, you could try <em>Programming Ruby</em> (the "Pickaxe"), the guide written by the Pragmatic Programmers that first brought Ruby to the west. Its <a title="Programming Ruby: The Pragmatic Programmer's Guide" href="https://ruby-doc.org/docs/ProgrammingRuby/">first edition is even free</a> and can be found at <a href="https://ruby-doc.org/">ruby-doc.org</a> alongside the <a title="RDoc Documentation" href="https://ruby-doc.org/core/">official Ruby API</a>. The second (and upcoming third) edition is definitely worth the money, though, especially for its chapter about the inner details of Ruby's object and method dispatch system.

People who don't like the Pickaxe usually recommend Hal Fulton's "The Ruby Way," which teaches the language in a more task-oriented way.

If you're just entering the world of Rails, you'll also have access to what will probably be a pretty awesome library of documentation (if it isn't already!). A few months ago, the Rails team launched an effort to provide comprehensive, up-to-date and free information about everything Rails at <a href="https://guides.rubyonrails.org/">Rails Guides</a>.

If you've taken your first steps, you should subscribe to the <a href="https://www.smashingmagazine.com/2009/03/ultimate-beginners-guide-to-ruby-on-rails/">official Ruby on Rails blog</a>, mainly for important announcements and its “This Week in Rails” feature, which provides a very convenient overview of the development of Rails.

If you want to keep in touch with the greater Rails eco-system, you should subscribe to the <a href="https://www.railsenvy.com/">Rails Envy podcast</a>. These guys will point you to nice plug-ins, tips, tricks and important blog posts every week.

You could, of course, just read those blogs yourself, but beware: Rails has a lot going on in it, and I prefer to have the information predigested in some form. However, if you'd like something to chew on during those boring hours at work, check out these blogs:

*   [Ryan's Scraps](https://ryandaigle.com/)
*   [has_many :through](https://blog.hasmanythrough.com/)
*   [Robby on Rails](https://www.robbyonrails.com/)
*   [Jamis Buck's blog](https://weblog.jamisbuck.org/)
*   [caboose](https://blog.caboo.se/)
*   [Ilya Grigorik's blog](https://www.igvita.com/)
*   [On Rails](https://onrails.org/)
*   [nano RAILS](https://blog.nanorails.com/)
*   [Railscasts](https://railscasts.com/)

Should you get stuck in your adventures, Googling often helps because most of the problems that beginners experience are similar, and for almost any hurdle you may encounter, somebody somewhere has already written a blog post about it. If this is not the case with your problem, ask for help on the <a href="https://groups.google.com/group/rubyonrails-talk">Ruby on Rails mailing list</a> or the <a href="https://www.ruby-lang.org/en/community/mailing-lists/">Ruby mailing list</a>. The people in the Ruby community are usually very friendly and helpful.</p>

## Related posts

You may want to take a look at the following related posts:

*   [Getting Started With Ruby On Rails: Part 1](https://www.smashingmagazine.com/2009/03/19/getting-started-with-ruby-on-rails/)
*   [10 Useful Tips For Ruby On Rails Developers](https://www.smashingmagazine.com/2009/02/25/ruby-on-rails-tips/)

{{< signature "al" >}}

