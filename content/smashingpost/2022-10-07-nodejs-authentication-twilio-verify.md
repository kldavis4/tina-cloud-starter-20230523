---
title: 'Node.js Authentication With Twilio Verify'
slug: nodejs-authentication-twilio-verify
author: alexander-godwin
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e77a7ee4-c2ed-4b4c-a147-16df351a6b31/nodejs-authentication-twilio-verify-sharing-card.jpg
date: 2022-10-07T06:00:00.000Z
summary: >-
  In this tutorial, you’ll learn how to integrate two-factor authentication into your Express.js application. You will build an express application that authenticates users using traditional password-based authentication with an extra layer of security using OTPs powered by the Twilio Verify service. You’ll learn how to build an express backend from scratch and implement authentication while learning about the MVC architecture. MongoDB is the database of choice, and the Ui is built using EJS. By the end of this tutorial, you’ll have a fully functional express application that implements OTPs and passwords for user authentication.
description: >-
  Integrate two-factor authentication into your Express.js app by building an application that authenticates users using password-based authentication and OTPs powered by the Twilio Verify service.
categories:
  - API
  - Apps
  - Node.js
  - JavaScript
---

Building authentication into an application is a tedious task. However, making sure this authentication is bulletproof is even harder. As developers, it’s beyond our control what the users do with their passwords, how they protect them, who they give them to, or how they generate them, for that matter. All we can do is get close enough to ensure that the authentication request was made by our user and not someone else. OTPs certainly help with that, and services like *Twilio Verify* help us to generate secured OTPs quickly without having to bother about the logic. 

### What’s Wrong With Passwords?

There are several problems faced by developers when using password-based authentication alone since it has the following issues:  

1. Users might forget passwords and write them down (making them steal-able);
2. Users might reuse passwords across services (making all their accounts vulnerable to one data breach);
3. Users might use easy passwords for remembrance purposes, making them relatively easy to hack.


### Enter OTPs

A **one-time password** (**OTP**) is a password or PIN valid for only one login session or transaction. Once it can only be used once, I’m sure you can already see how the usage of OTPs makes up for the shortcomings of traditional passwords.

OTPs add an extra layer of security to applications, which the traditional password authentication system cannot provide. OTPs are randomly generated and are only valid for a short period of time, avoiding several deficiencies that are associated with traditional password-based authentication.

OTPs can be used to substitute traditional passwords or reinforce the passwords using the two-factor authentication (2FA) approach. Basically, OTPs can be used wherever you need to ensure a user’s identity by relying on a personal communication medium owned by the user, such as phone, mail, and so on.

This article is for developers who want to learn about: 

1. Learn how to build a Full-stack express.js application;
2. Implement authentication with passport.js;
3. How to [Twilio Verify](https://www.twilio.com/verify) for phone-based user verification.

To achieve these objectives, we’ll build a full-stack application using [node.js](https://nodejs.org/), [express.js](https://expressjs.com/), [EJS](https://ejs.co/) with authentication done using [passport.js](http://www.passportjs.org/) and  protected routes that require OTPs for access. 

**Note**: *I’d like to mention that we’ll be using some 3rd-party (built by other people) packages in our application. This is a common practice, as there is no need to re-invent the wheel. Could we create our own node server? Yes, of course. However, that time could be better spent on building logic specifically for our application.*

## Table Of Contents  

1. Basic overview of Authentication in web applications;
2. Building an Express server;
3. Integrating [MongoDB](https://www.mongodb.com/) into our Express application;
4. Building the views of our application using EJS templating engine;
5. Basic authentication using a passport number;
6. Using Twilio Verify to protect routes.

## Requirements  

- Node.js
- MongoDB
- A text editor (e.g. VS Code)
- A web browser (e.g. Chrome, Firefox)
- An understanding of HTML, CSS, JavaScript, Express.js

Although we will be building the whole application from scratch, here’s the [GitHub Repository](https://github.com/oviecodes/authwithTwilioVerify) for the project.

## Basic Overview Of Authentication In Web Applications

### What Is Authentication?

**Authentication** is the whole process of identifying a user and verifying that a user has an account on our application.

<blockquote>Authentication is not to be confused with authorization. Although they work hand in hand, there’s no authorization without authentication.</blockquote> 

That being said, let’s see what authorization is about.

### What Is Authorization?

**Authorization** at its most basic, is all about user permissions &mdash; what a user is allowed to do in the application. In other words:  

1. Authentication: Who are you?
2. Authorization: What can you do?

<blockquote>Authentication comes before Authorization. <br /> There is no Authorization without Authentication.</blockquote>

The most common way of authenticating a user is via `username` and `password`. 

## Setting Up Our Application

To set up our application, we create our project directory:

<pre><code class="language-bash">mkdir authWithTwilioVerify
</code></pre>

## Building An Express Server

We’ll be using [Express.js](https://expressjs.com/) to build our server.

### Why Do We Need Express?

Building a server in `Node` could be tedious, but frameworks make things easier for us.
`Express` is the most popular `Node` web framework. It enables us to:

- Write handlers for requests with different `HTTP` verbs at different `URL` paths (routes);
- Integrate with `view` rendering engines in order to generate responses by inserting data into templates;
- Set common web application settings &mdash; like the `port` used for connecting, and the location of templates used for rendering the response;
- Add additional request processing `middleware` at any point within the request handling pipeline.

In addition to all of these, developers have created compatible middleware packages to address almost any web development problem.

In our `authWithTwilioVerify` directory, we initialize a `package.json` that holds information concerning our project.

<pre><code class="language-bash">cd authWithTwilioVerify
npm init -y
</code></pre>

In Keeping with the Model View Controller(MVC) architecture, we have to create the following folders in our `authWithTwilioVerify` directory:

<pre><code class="language-bash">mkdir public controllers views routes config models
</code></pre>

Many developers have different reasons for using the MVC architecture, but for me personally, it’s because:  

1. It encourages separation of concerns;
2. It helps in writing clean code;
3. It provides a structure to my codebase, and since other developers use it, understanding the codebase won’t be an issue.  

- `Controllers` directory houses the controllers;
- `Models` directory holds our database models;
- `Public` directory holds our static assets e.g. CSS files, images e.t.c.;
- `Views` directory contains the pages that will be rendered in the browser;
- `Routes` directory holds the different routes of our application;
- `Config` directory holds information that is peculiar to our application.  

We need to install the following packages to build our app:

- `nodemon` automatically restarts our server when we make changes;
- `express` gives us a nice interface to handle routes;
- `express-session` allows us to handle sessions easily in our express application;
- `connect-flash` allows us to display messages to our users.

<pre><code class="language-bash">npm install nodemon -D
</code></pre>

Add the script below in the `package.json` file to start our server using `nodemon`.

<pre><code class="language-javascript">"scripts": {
    "dev": "nodemon index"
    },
</code></pre>

<pre><code class="language-bash">npm install express express-session connect-flash --save
</code></pre>  

Create an `index.js` file and add the necessary packages for our app.

We have to `require` the installed packages into our `index.js` file so that our application runs well then we configure the packages as follows:

<pre><code class="language-javascript">const path = require('path')
const express = require('express');
const session = require('express-session')
const flash = require('connect-flash')

const port = process.env.PORT || 3000
const app = express();

app.use('/static', express.static(path.join(__dirname, 'public')))
app.use(session({ 
    secret: "please log me in",
    resave: true,
    saveUninitialized: true
    }
));

app.use(express.json())
app.use(express.urlencoded({ extended: true }))

// Connect flash
app.use(flash());

// Global variables
app.use(function(req, res, next) {
    res.locals.success_msg = req.flash('success_msg');
    res.locals.error_msg = req.flash('error_msg');
    res.locals.error = req.flash('error');
    res.locals.user = req.user
    next();
});

//define error handler
app.use(function(err, req, res, next) {
    res.render('error', {
        error : err
    })
})

//listen on port
app.listen(port, () => {
    console.log(`app is running on port ${port}`)
});
</code></pre>

Let’s break down the segment of code above.

Apart from the `require` statements, we make use of the `app.use()` function &mdash; which enables us to use application level `middleware`. 

Middleware functions are functions that have access to the request object, response object, and the next middleware function in the application’s request and response cycle.

<blockquote>Most packages that have access to our application’s state (request and response objects) and can alter those states are usually used as middleware. Basically, middleware adds functionality to our express application.</blockquote>

It’s like handing the application state over to the middleware function, saying here’s the state, do what you want with it, and call the `next()` function to the next middleware.

Finally, we tell our application server to listen for requests to port 3000.

Then in the terminal run:

<pre><code class="language-bash">npm run dev
</code></pre>

If you see `app is running on port 3000` in the terminal, that means our application is running properly.

## Integrating MongoDB Into Our Express Application  

MongoDB stores data as documents. These documents are stored in MongoDB in JSON (JavaScript Object Notation) format. Since we’re using Node.js, it’s pretty easy to convert data stored in MongoDB to JavaScript objects and manipulate them.

To install MongoDB in your machine visit the MongoDB [documentation](https://www.mongodb.com/docs/manual/installation/).

In order to integrate MongoDB into our express application, we’ll be using [Mongoose](https://mongoosejs.com/). Mongoose is an ODM(which is the acronym for `object data mapper`).

Basically, Mongoose makes it easier for us to use MongoDB in our application by creating a wrapper around Native MongoDB functions.

<pre><code class="language-bash">npm install mongoose --save
</code></pre>

In `index.js`, it requires `mongoose`:

<pre><code class="language-javascript">const mongoose = require('mongoose')

const app = express()

//connect to mongodb
mongoose.connect('mongodb://localhost:27017/authWithTwilio', 
{ 
    useNewUrlParser: true, 
    useUnifiedTopology: true 
})
.then(() => {
    console.log(`connected to mongodb`)
})
.catch(e =&gt; console.log(e))
</code></pre>

The `mongoose.connect()` function allows us to set up a connection to our MongoDB database using the connection string.

The format for the connection string is `mongodb://localhost:27017/{database_name}`.

`mongodb://localhost:27017/` is MongoDB’s default host, and the `database_name` is whatever we wish to call our database.

Mongoose connects to the database called `database_name`. If it doesn’t exist, it creates a database with `database_name` and connects to it.

`Mongoose.connect()` is a promise, so it’s always a good practice to log a message to the console in the `then()` and `catch()` methods to let us know if the connection was successful or not.

We create our user model in our `models` directory:

<pre><code class="language-bash">cd models
touch user.js
</code></pre>  

`user.js` requires mongoose and create our user schema:

<pre><code class="language-javascript">const mongoose = require('mongoose');

const userSchema = new mongoose.Schema({
    name : {
        type: String,
        required: true
    },
    username : {
        type: String,
        required: true
    },
    password : {
        type: String,
        required: true
    },
    phonenumber : {
        type: String,
        required: true
    },
    email : {
        type: String,
        required: true
    },
    verified: Boolean
})

module.exports = mongoose.model('user', userSchema)
</code></pre>

A `schema` provides a structure for our data. It shows how data should be structured in the database. Following the code segment above, we specify that a user object in the database should always have `name`, `username`, `password`, `phonenumber`, and `email`. Since those fields are required, if the data pushed into the database lack any of these required fields, mongoose throws an error.

Though you could create schemaless data in MongoDB, it is not advisable to do so &mdash; trust me, your data would be a mess. Besides, schemas are great. They allow you to dictate the structure and form of objects in your database &mdash; who wouldn’t want such powers?

{{% feature-panel %}}

### Encrypting Passwords

<blockquote>Warning: never store users’ passwords as plain text in your database. <br /> Always encrypt the passwords before pushing them to the database.</blockquote>

The reason we need to encrypt user passwords is this: in case someone somehow gains access to our database, we have some assurance that the user passwords are safe &mdash; because all this person would see would be a `hash`. This provides some level of security assurance, but a sophisticated hacker may still be able to crack this `hash` if they have the right tools. Hence the need for OTPs, but let’s focus on encrypting user passwords for now.

`bcryptjs` provides a way to encrypt and decrypt users’ passwords.

<pre><code class="language-bash">npm install bcryptjs
</code></pre>

In `models/user.js`, it requires `bcryptjs`:

<pre><code class="language-javascript">//after requiring mongoose
const bcrypt = require('bcryptjs')

//before module.exports
//hash password on save
userSchema.pre('save', async function() {
    return new Promise( async (resolve, reject) =&gt; {
        await bcrypt.genSalt(10, async (err, salt) =&gt; {
            await bcrypt.hash(this.password, salt, async (err, hash) =&gt; {
                if(err) {
                    reject (err)
                } else {
                    resolve (this.password = hash)
                }
            });
        });
    })
})
userSchema.methods.validPassword = async function(password) {
    return new Promise((resolve, reject) =&gt; {
        bcrypt.compare(password, this.password, (err, res) =&gt; {
            if(err) {
                reject (err)
            } 
            resolve (res)
        }); 
    })
}
</code></pre>

The code above does a couple of things. Let’s see them.

The `userSchema.pre('save', callback)` is a `mongoose hook` that allows us to manipulate data before saving it to the database. In the `callback function`, we return a promise which tries to `hash(encrypt) bcrypt.hash()` the password using the `bcrypt.genSalt()` we generated. If an error occurs during this `hashing`, we `reject` or we `resolve` by setting `this.password = hash`. `this.password` being the `userSchema password`.

Next, `mongoose` provides a way for us to append methods to schemas using the `schema.methods.method_name`. In our case, we’re creating a method that allows us to validate user passwords. Assigning a function value to  `*userSchema.methods.validPassword*`, we can easily use bcryptjs compare method `bcryprt.compare()` to check if the password is correct or not. 

`bcrypt.compare()` takes two arguments and a callback. The `password` is the password that is passed when calling the function, while `this.password` is the one from userSchema.

<blockquote>I prefer this method of validating users’ password because it’s like a property on the user object. One could easily call <code>User.validPassword(password)</code> and get true or false as a response.</blockquote>

Hopefully, you can see the usefulness of mongoose. Besides creating a schema that gives structure to our database objects, it also provides nice methods for manipulating those objects &mdash; that would have been otherwise somewhat though using native MongoDB alone.

<blockquote>Express is to Node, as Mongoose is to MongoDB.</blockquote>

## Building The Views Of Our Application Using EJS Templating Engine

Before we start building the views of our application, let’s take a look at the front-end architecture of our application.

### Front-end Architecture

`EJS` is a templating engine that works with Express directly. There’s no need for a different front-end framework. `EJS` makes the passing of data very easy. It also makes it easier to keep track of what’s going on since there is no switching from back-end to front-end.

We’ll have a `views` directory, which will contain the files to be rendered in the browser. All we have to do is call the `res.render()` method from our controller. For example, if we wish to render the login page, it’s as simple as `res.render('login')`. We could also pass data to the views by adding an additional argument &mdash; which is an object to the `render()` method, like `res.render('dashboard', { user })`. Then, in our `view`, we could display the data with the `evaluation syntax <%= %>`. Everything with this tag is evaluated &mdash; for instance, `<%= user.username %>` displays the value of the username property of the user object. Aside from the evaluation syntax, `EJS` also provides a **control syntax** (`<% %>`), which allows us to write program control statements such as conditionals, loops, and so forth.


Basically, `EJS` allows us to embed JavaScript in our HTML.

<pre><code class="language-bash">npm install ejs express-ejs-layouts --save
</code></pre>

In `index.js`, it requires `express-ejs-layouts`: 

<pre><code class="language-javascript">//after requiring connect-flash
const expressLayouts = require('express-ejs-layouts')

//after the mongoose.connect logic
app.use(expressLayouts);
app.set('view engine', 'ejs');
</code></pre>

Then:

<pre><code class="language-bash">cd views
touch layout.ejs
</code></pre>

In `views/layout.ejs`,

<pre><code class="language-HTML">&lt;!DOCTYPE html&gt;
&lt;html lang="en"&gt;
    &lt;head&gt;
    &lt;meta charset="UTF-8" /&gt;
    &lt;meta name="viewport" content="width=device-width, initial-scale=1.0" /&gt;
    &lt;meta http-equiv="X-UA-Compatible" content="ie=edge" /&gt;
        &lt;link rel="stylesheet" href="https://use.fontawesome.com/releases/v5.6.3/css/all.css" integrity="sha384-UHRtZLI+pbxtHCWp1t77Bi1L4ZtiqrqD80Kn4Z8NTSRyMA2Fd33n5dQ8lWUE00s/" crossorigin="anonymous"&gt;
        &lt;link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/semantic-ui@2.4.2/dist/semantic.min.css"&gt;
        &lt;link rel="stylesheet" href="/static/css/app.css"&gt;
        &lt;link rel="stylesheet" href="/static/css/intlTelInput.css"&gt;
    &lt;title&gt;Node js authentication&lt;/title&gt;
    &lt;/head&gt;
    &lt;body&gt;
    
    &lt;div class="ui container"&gt;
        &lt;%- body %&gt;
    &lt;/div&gt;
    &lt;script
        src="https://code.jquery.com/jquery-3.3.1.slim.min.js"
        integrity="sha384-q8i/X+965DzO0rT7abK41JStQIAqVgRVzpbzo5smXKp4YfRvH+8abtTE1Pi6jizo"
        crossorigin="anonymous"
    &gt;&lt;/script&gt;
    &lt;script src="https://cdn.jsdelivr.net/npm/semantic-ui@2.4.2/dist/semantic.min.js"&gt;&lt;/script&gt;
    &lt;/body&gt;
&lt;/html&gt;
</code></pre>

The `layout.ejs` file serves like an `index.html` file, where we can include all our scripts and stylesheets. Then, in the `div` with classes `ui container`, we render the `body` &mdash; which is the rest of our application views.

We’ll be using [semantic UI](https://semantic-ui.com/) as our CSS framework.


### Building The Partials

Partials are where we store re-usable code, so that we don’t have to rewrite them every single time. All we do is *include* them wherever they are needed.

<blockquote>You could think of partials like components in front-end frameworks: they encourage DRY code, and also code re-usability. Think of partials as an earlier version of components.</blockquote>

For example, we want partials for our menu, so that we do not have to write code for it every single time we need the menu on our page.

<pre><code class="language-bash">cd views
mkdir partials
</code></pre>

We’ll create two files in the `/views/partials` folder:

<pre><code class="language-bash">cd partials
touch menu.ejs message.ejs
</code></pre>

In `menu.ejs`,

<pre><code class="language-HTML">&lt;div class="ui secondary  menu"&gt;
    &lt;a class="active item" href="/"&gt;
        Home
    &lt;/a&gt;
    &lt;% if(locals.user) { %&gt;
        &lt;a class="ui item" href="/users/dashboard"&gt;
        dashboard
        &lt;/a&gt;
        &lt;div class="right menu"&gt;
        &lt;a class='ui item'&gt;
            &lt;%= user.username %&gt;
        &lt;/a&gt;
        &lt;a class="ui item" href="/users/logout"&gt;
            Logout
        &lt;/a&gt;
        &lt;/div&gt;
    &lt;% } else {%&gt;
        &lt;div class="right menu"&gt;
        &lt;a class="ui item" href="/users/signup"&gt;
            Sign Up
        &lt;/a&gt;
        &lt;a class="ui item" href="/users/login"&gt;
            Login
        &lt;/a&gt;
        &lt;/div&gt;
    &lt;% } %&gt;
    &lt;/div&gt;
</code></pre>

In `message.ejs`,

<pre><code class="language-ejs">&lt;% if(typeof errors != 'undefined'){ %&gt; &lt;% errors.forEach(function(error) { %&gt;
    &lt;div class="ui warning message"&gt;
        &lt;i class="close icon"&gt;&lt;/i&gt;
        &lt;div class="header"&gt;
            User registration unsuccessful
        &lt;/div&gt;
        &lt;%= error.msg %&gt;
    &lt;/div&gt;
&lt;% }); %&gt; &lt;% } %&gt; &lt;% if(success_msg != ''){ %&gt;
&lt;div class="ui success message"&gt;
    &lt;i class="close icon"&gt;&lt;/i&gt;
    &lt;div class="header"&gt;
        Your user registration was successful.
    &lt;/div&gt;
    &lt;%= success_msg %&gt;
&lt;/div&gt;
&lt;% } %&gt; &lt;% if(error_msg != ''){ %&gt;
&lt;div class="ui warning message"&gt;
    &lt;i class="close icon"&gt;&lt;/i&gt;
    &lt;div class="header"&gt;
        
    &lt;/div&gt;
    &lt;%= error_msg %&gt;
&lt;/div&gt;
&lt;% } %&gt; &lt;% if(error != ''){ %&gt;
&lt;div class="ui warning message"&gt;
    &lt;i class="close icon"&gt;&lt;/i&gt;
    &lt;div class="header"&gt;
        
    &lt;/div&gt;
    &lt;%= error %&gt;
&lt;/div&gt;
&lt;% } %&gt;
</code></pre>

### Building The Dashboard Page

In our views folder, we create a `dashboard.ejs` file:

<pre><code class="language-ejs">&lt;%- include('./partials/menu') %&gt;
&lt;h1&gt;
    DashBoard
&lt;/h1&gt;
</code></pre>

Here, we include the `menu partials` so we have the menu on the page.

### Building The Error Page 

In our views folder, we create an `error.ejs` file:

<pre><code class="language-ejs">&lt;h1&gt;Error Page&lt;/h1&gt;
&lt;p&gt;&lt;%= error %&gt;&lt;/p&gt;
</code></pre>

### Building The Home Page

In our views folder, we create a `home.ejs` file:

<pre><code class="language-ejs">&lt;%- include('./partials/menu') %&gt;
&lt;h1&gt;
    Welcome to the Home Page
&lt;/h1&gt;
</code></pre>

### Building The Login Page

In our views folder, we create a `login.ejs` file:

<pre><code class="language-ejs">&lt;div class="ui very padded text container segment"&gt;
    &lt;%- include ('./partials/message') %&gt;
    &lt;h3&gt;
        Login Form
    &lt;/h3&gt;
    
    &lt;form class="ui form" action="/users/login" method="POST"&gt;
    &lt;div class="field"&gt;
        &lt;label&gt;Email&lt;/label&gt;
        &lt;input type="email" name="email" placeholder="Email address"&gt;
    &lt;/div&gt;
    &lt;div class="field"&gt;
        &lt;label&gt;Password&lt;/label&gt;
        &lt;input type="password" name="password" placeholder="Password"&gt;
    &lt;/div&gt;
    &lt;button class="ui button" type="submit"&gt;Login&lt;/button&gt;
    &lt;/form&gt;
&lt;/div&gt;
</code></pre>

### Building The Verify Page

In our views folder, we create a `login.ejs` file:

<pre><code class="language-ejs">&lt;%- include ('./partials/message') %&gt;
&lt;h1&gt;Verify page&lt;/h1&gt;
&lt;p&gt;please verify your account&lt;/p&gt;
&lt;form class="ui form" action="/users/verify" method="POST"&gt;
    &lt;div class="field"&gt;
        &lt;label&gt;verification code&lt;/label&gt;
        &lt;input type="text" type="number" name="verifyCode" placeholder="code"&gt;
    &lt;/div&gt;
    &lt;button class="ui button" type="submit"&gt;Verify&lt;/button&gt;
&lt;/form&gt;
&lt;br&gt;
&lt;a class="ui button" href="/users/resend"&gt;Resend Code&lt;/a&gt;
</code></pre>

Here, we provide a form for users to enter the verification code that will be sent to them.

{{% ad-panel-leaderboard %}}

### Building The Sign Up Page

We need to get the user’s mobile number, and we all know that country codes differ from country to country. Therefore, we’ll use the `[intl-tel-input](https://intl-tel-input.com/)` to help us with the country codes and validation of phone numbers.

<pre><code class="language-bashj">npm install intl-tel-input
</code></pre>

1. In our public folder, we create a `css` directory, `js` directory and `img` directory:

    <pre><code class="language-bash">cd public
    mkdir css js img
    </code></pre>

2. We copy the `intlTelInput.css` file from  `node_modules\intl-tel-input\build\css\` file into our `public/css` directory.
3. We copy both the  `intlTelInput.js` and `utils.js` from `node_modules\intl-tel-input\build\js\` folder into  our `public/js` directory.
4. We copy both the `flags.png` and `flags@2x.png`  from  `node_modules\intl-tel-input\build\img\` folder into  our `public/img` directory.

We create an app.css in our `public/css` folder:

<pre><code class="language-bash">cd public
touch app.css
</code></pre>

In `app.css`, add the styles below: 

<pre><code class="language-css">.iti__flag {background-image: url("/static/img/flags.png");}
    
@media (-webkit-min-device-pixel-ratio: 2), (min-resolution: 192dpi) {
    .iti__flag {background-image: url("/static/img/flags@2x.png");}
}
.hide {
    display: none
}
.error {
    color: red;
    outline: 1px solid red;
}
.success{
    color: green;
}
</code></pre>

Finally, we create a `signup.ejs` file in our views folder:

<pre><code class="language-ejs">&lt;div class="ui very padded text container segment"&gt;
    &lt;%- include ('./partials/message') %&gt;
    &lt;h3&gt;
        Signup Form
    &lt;/h3&gt;
    
    &lt;form class="ui form" action="/users/signup" method="POST"&gt;
    &lt;div class="field"&gt;
        &lt;label&gt;Name&lt;/label&gt;
        &lt;input type="text" name="name" placeholder="name"&gt;
    &lt;/div&gt;
    &lt;div class="field"&gt;
        &lt;label&gt;Username&lt;/label&gt;
        &lt;input type="text" name="username" placeholder="username"&gt;
    &lt;/div&gt;
    &lt;div class="field"&gt;
        &lt;label&gt;Password&lt;/label&gt;
        &lt;input type="password" name="password" placeholder="Password"&gt;
    &lt;/div&gt;
    &lt;div class="field"&gt;
        &lt;label&gt;Phone number&lt;/label&gt;
        &lt;input type="tel" id='phone'&gt;
        &lt;span id="valid-msg" class="hide success"&gt;✓ Valid&lt;/span&gt;
        &lt;span id="error-msg" class="hide error"&gt;&lt;/span&gt;
    &lt;/div&gt;
    &lt;div class="field"&gt;
        &lt;label&gt;Email&lt;/label&gt;
        &lt;input type="email" name="email" placeholder="Email address"&gt;
    &lt;/div&gt;
    
    &lt;button class="ui button" type="submit"&gt;Sign up&lt;/button&gt;
    &lt;/form&gt;
&lt;/div&gt;
&lt;script src="/static/js/intlTelInput.js"&gt;&lt;/script&gt;
&lt;script&gt;
    const input = document.querySelector("#phone")
    const errorMsg = document.querySelector("#error-msg")
    const validMsg = document.querySelector("#valid-msg")
    
    const errorMap = ["Invalid number", "Invalid country code", "Too short", "Too long", "Invalid number"];
    const iti = window.intlTelInput(input, {
        separateDialCode: true,
        autoPlaceholder: "aggressive",
        hiddenInput: "phonenumber",
        utilsScript: "/static/js/utils.js?1590403638580" // just for formatting/placeholders etc
    });
    var reset = function() {
        input.classList.remove("error");
        errorMsg.innerHTML = "";
        errorMsg.classList.add("hide");
        validMsg.classList.add("hide");
    };
    // on blur: validate
    input.addEventListener('blur', function() {
        reset();
        if (input.value.trim()) {
        if (iti.isValidNumber()) {
            validMsg.classList.remove("hide");
        } else {
            input.classList.add("error");
            
            var errorCode = iti.getValidationError();
            errorMsg.innerHTML = errorMap[errorCode];
            errorMsg.classList.remove("hide");
        }
        }
    });
    // on keyup / change flag: reset
    input.addEventListener('change', reset);
    input.addEventListener('keyup', reset);

    document.querySelector('.ui.form').addEventListener('submit', (e) =&gt; {
        if(!iti.isValidNumber()){
        e.preventDefault()
        }
    })
&lt;/script&gt; 
</code></pre>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a3bb8259-123b-4148-8963-efed0bfd2007/1-nodejs-authentication-twilio-verify.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a3bb8259-123b-4148-8963-efed0bfd2007/1-nodejs-authentication-twilio-verify.jpg" width="800" height="455" sizes="100vw" caption="Sign up page. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a3bb8259-123b-4148-8963-efed0bfd2007/1-nodejs-authentication-twilio-verify.jpg'>Large preview</a>)" alt="Sign up page: a form with the fields Name, Username, Password, Phone Number, Email, and a button with the label Sig up." >}}


## Basic Authentication With Passport

Building authentication into an application can be really complex and time-draining, so we need a package to help us with that.

<blockquote>Remember: do not re-invent the wheel, except if your application has a specific need.</blockquote>

`passport` is a package that helps out with authentication in our express application.

`passport` has many strategies we could use, but we’ll be using the `local-strategy` &mdash; which basically does `username and password authentication`.

<blockquote>One advantage of using passport is that, since it has many strategies, we can easily extend our application to use its other strategies.</blockquote>

<pre><code class="language-bash">npm install passport passport-local
</code></pre>

In `index.js` we add the following code:

<pre><code class="language-javascript">//after requiring express
const passport = require('passport')

//after requiring mongoose
const { localAuth } = require('./config/passportLogic')

//after const app = express()
localAuth(passport)

//after app.use(express.urlencoded({ extended: true }))
app.use(passport.initialize());
app.use(passport.session());
</code></pre>

We’re adding some `application level middleware` to our `index.js` file &mdash; which tells the application to use the `passport.initialize()` and the `passport.session()` middleware.

`Passport.initialize()` initializes `passport`, while the `passport.session()` middleware let’s `passport` know that we’re using `session` for authentication.

Do not worry much about the `localAuth()` function. That takes the `passport` object as an argument, and we’ll create the function just below.

Next, we create a `config` folder and create the needed files:

<pre><code class="language-bash">mkdir config
touch  passportLogic.js middleware.js
</code></pre>

In `passportLogic.js`,

<pre><code class="language-javascript">//file contains passport logic for local login
const LocalStrategy = require('passport-local').Strategy;
const mongoose = require('mongoose')
const User = require('../models/user')
const localAuth = (passport) =&gt; {
    passport.use(
        new LocalStrategy(
        { usernameField: 'email' }, async(email, password, done) =&gt; {
            try {
                const user = await User.findOne({ email: email }) 
                
                if (!user) {
                    return done(null, false, { message: 'Incorrect email' });
                }
                //validate password
                const valid = await user.validPassword(password)
                if (!valid) {
                    return done(null, false, { message: 'Incorrect password.' });
                }
                return done(null, user);
            } catch (error) {
                return done(error)
            }
        }
    ));
    passport.serializeUser(function(user, done) {
        done(null, user.id);
    });
        
    passport.deserializeUser(function(id, done) {
        User.findById(id, function(err, user) {
            done(err, user);
        });
    });
}
module.exports = {
    localAuth
}
</code></pre>

Let’s understand what is going on in the code above.

Apart from the require statements, we create the `localAuth()` function, which will be exported from the file. In the function, we call the `passport.use()` function that uses the `LocalStrategy()` for `username` and `password` based authentication.

We specify that our `usernameField` should be `email`. Then, we find a user that has that particular `email` &mdash; if none exists, then we return an error in the `done()` function. However, if a user exists, we check if the password is valid using the `validPassword` method on the `User` object. If it’s invalid, we return an error. Finally, if everything is successful, we return the `user` in `done(null, user)`.

`passport.serializeUser()` and `passport.deserializeUser()` helps in order to support login sessions. Passport will serialize and deserialize `user` instances *to* and *from* the session.

In `middleware.js`, 

<pre><code class="language-javascript">//check if a user is verified
const isLoggedIn = async(req, res, next) =&gt; {
    if(req.user){
        return next()
    } else {
        req.flash(
            'error_msg',
            'You must be logged in to do that'
        )
        res.redirect('/users/login')
    }
}
const notLoggedIn = async(req, res, next) =&gt; {
    if(!req.user) {
        return next()
    } else{
        res.redirect('back')
    }
}


module.exports = {
    isLoggedIn,
    notLoggedIn
}
</code></pre>

Our middleware file contains two(2) `route level middleware`, which will be used later in our routes. 

<blockquote>Route-level middleware is used by our routes, mostly for route protection and validation, such as authorization, while application level middleware is used by the whole application.</blockquote>

`isLoggedIn` and `notLoggedIn` are `route level middleware` that checks if a user is logged in. We use these middlewares to block access to routes that we want to make accessible to logged-in users.


### Building The Sign-Up Controllers

<pre><code class="language-bash">cd controllers
mkdir signUpController.js loginController.js
</code></pre>

In `signUpController.js`, we: 

1. Check for users’ credentials;
2. Check if a user with that detail(email or phone-number) exists in our database;
3. Create an error if the user exists;
4. Finally, if such a user does not exist, we create a new user with the given details and redirect to the `login` page.

<pre><code class="language-javascript">const mongoose = require('mongoose')
const User = require('../models/user')

//sign up Logic
const getSignup = async(req, res, next) =&gt; {
    res.render('signup')
}
const createUser = async (req, res, next) =&gt; {
    try {
        const { name, username, password, phonenumber, email} = await req.body
        const errors = []
        const reRenderSignup = (req, res, next) =&gt; {
            console.log(errors)
            res.render('signup', {
                errors,
                username,
                name,
                phonenumber,
                email
            })
        }
        if( !name || !username || !password || !phonenumber || !email ) {
            errors.push({ msg: 'please fill out all fields appropriately' })
            reRenderSignup(req, res, next)
        } else {
            const existingUser = await User.findOne().or([{ email: email}, { phonenumber : phonenumber }])
            if(existingUser) {
            errors.push({ msg: 'User already exists, try changing your email or phone number' })
            reRenderSignup(req, res, next)
            } else {
                const user = await User.create(
                    req.body
                )
                req.flash(
                    'success_msg',
                    'You are now registered and can log in'
                );
                res.redirect('/users/login')
            }
            
        }
    } catch (error) {
        next(error)
    }
}
module.exports = {
    createUser,
    getSignup
}
</code></pre>

In `loginController.js`,

1. We use the `passport.authenticate()` method with the local scope (email and password) to check if the user exists;
2. If the user doesn’t exist, we give out an error message and redirect the user to the same route;
3. if the user exists, we log the user in using the `req.logIn` method, send them a verification using the `sendVerification()` function, then redirect them to the `verify` route.

<pre><code class="language-javascript">const mongoose = require('mongoose')
const passport = require('passport')
const User = require('../models/user')
const { sendVerification } = require('../config/twilioLogic')
const getLogin = async(req, res) =&gt; {
    res.render('login')
}
const authUser = async(req, res, next) =&gt; {
    try {
        passport.authenticate('local', function(err, user, info) {
            if (err) { 
                return next(err) 
            }
            if (!user) { 
                req.flash(
                    'error_msg',
                    info.message
                )
                return res.redirect('/users/login')
            }
            req.logIn(user, function(err) {
                if (err) { 
                    return next(err)
                }
                sendVerification(req, res, req.user.phonenumber)
                res.redirect('/users/verify');
            });
        })(req, res, next);
    } catch (error) {
        next(error)
    }
    
}
module.exports = {
    getLogin,
    authUser
}
</code></pre>

Right now, `sendVerification()` doesn’t exactly work. That’s because we’ve not written the function, so we need `Twilio` for that. Let’s install Twilio and get started. 

{{% ad-panel-leaderboard %}}

## Using Twilio Verify To Protect Routes

In order to use Twilio Verify, you:

1. Head over to `https://www.twilio.com/`;
2. Create an account with Twilio;
3. Login to your dashboard;
4. Select create a new project;
5. Follow the steps to create a new project.

To install the `Twilio SDK` for node.js:

<pre><code class="language-bash">npm install twilio
</code></pre>

Next, we need to install `dotenv` to help us with `environment variables`.

<pre><code class="language-bash">npm install dotenv
</code></pre>

We create a file in the root of our project and name it `.env`. This file is where we keep our `credentials`, so we don’t push it to git. In order to do that, we create a `.gitignore` file in the root of our project, and add the following lines to the file:

<pre><code class="language-bash">node_modules
.env
</code></pre>

This tells git to ignore both the `node_modules` folder and the `.env` file.

To get our Twilio account credentials, we login into our Twilio console, and copy our `ACCOUNT SID` and `AUTH TOKEN`. Then, we click on `get trial number` and Twilio generates a trial number for us, click `accept number`. Now from the console copy, we copy our trial number.

In `.env`, 
<blockquote>TWILIO_ACCOUNT_SID = &lt;YOUR_ACCOUNT_SID&gt; <br />
TWILIO_AUTH_TOKEN = &lt;YOUR_AUTH_TOKEN&gt;<br />
TWILIO_PHONE_NUMBER = &lt;TOUR_TWILIO_NUMBER&gt;<br /></blockquote>

Don’t forget to replace `<YOUR_ACCOUNT_SID>`, `<YOUR_AUTH_TOKEN>`, and `<TOUR_TWILIO_NUMBER>` with your actual credentials.

We create a file named `twilioLogic.js` in the `config` directory:

<pre><code class="language-bash">cd cofig
touch twilioLogic.js
</code></pre>

In `twilioLogic.js`,

<pre><code class="language-javascript">require('dotenv').config()
const twilio = require('twilio')
const client = twilio(process.env.TWILIO_ACCOUNT_SID, process.env.TWILIO_AUTH_TOKEN)
//create verification service
const createService = async(req, res) =&gt; {
    client.verify.services.create({ friendlyName: 'phoneVerification' })
        .then(service =&gt; console.log(service.sid))
}

createService();
</code></pre>

In the code snippet above, we create a new `verify` service.

Run:

<pre><code class="language-bash">node config/twilioLogic.js
</code></pre>

The string that gets logged to our screen is our `TWILIO_VERIFICATION_SID` &mdash; we copy that string.

In `.env`, add the line `TWILIO_VERIFICATION_SID = <YOUR_TWILIO_VERIFICATION_SID>`.

In `config/twilioLogic.js`, we remove the `createService()` line, since we need to create the `verify` service only once. Then, we add the following lines of code:

<pre><code class="language-javascript">//after createService function creation

//send verification code token
const sendVerification = async(req, res, number) =&gt; {
    
        client.verify.services(process.env.TWILIO_VERIFICATION_SID)
            .verifications
            .create({to: `${number}`, channel: 'sms'})
            .then( verification =&gt; 
                console.log(verification.status)
            ); 
}

//check verification token
const checkVerification = async(req, res, number, code) =&gt; {
    return new Promise((resolve, reject) =&gt; {
        client.verify.services(process.env.TWILIO_VERIFICATION_SID)
            .verificationChecks
            .create({to: `${number}`, code: `${code}`})
            .then(verification_check =&gt; {
                resolve(verification_check.status)
            });
    })
}
module.exports = {
    sendVerification,
    checkVerification
}
</code></pre>

`sendVerification` is an asynchronous function that returns a promise that sends a verification OTP to the number provided using the `sms` channel.

`checkVerification` is also an asynchronous function that returns a promise that checks the status of the verification. It checks if the `OTP` provided by the users is the same `OTP` that was sent to them.

In `config/middleware.js`, add the following:

<pre><code class="language-javascript">//after notLoggedIn function declaration

//prevents an unverified user from accessing '/dashboard'
const isVerified = async(req, res, next) =&gt; {
    if(req.session.verified){
        return next()
    } else {
        req.flash(
            'error_msg',
            'You must be verified to do that'
        )
        res.redirect('/users/login')
    }
}

//prevent verified User from accessing '/verify'
const notVerified = async(req, res, next) =&gt; {
    if(!req.session.verified){
        return next()
    } else {
        res.redirect('back')
    }
}


module.exports = {
    //after notLoggedIn
    isVerified, 
    notVerified
}
</code></pre>

We’ve created two more `route level middleware`, which will be used later in our routes. 

`isVerified` and `notVerified` check if a user is verified. We use these middlewares to block access to routes that we want to make accessible to only verified users.

<pre><code class="language-bash">cd controllers
touch verifyController.js
</code></pre>

In `verifyController.js`,

<pre><code class="language-javascript">const mongoose = require('mongoose')
const passport = require('passport')
const User = require('../models/user')
const { sendVerification, checkVerification } = require('../config/twilioLogic')
const loadVerify = async(req, res) =&gt; {
    res.render('verify')
}
const resendCode = async(req, res) =&gt; {
    sendVerification(req, res, req.user.phonenumber)
    res.redirect('/users/verify')
}
const verifyUser = async(req, res) =&gt; {
    //check verification code from user input
    const verifyStatus = await checkVerification(req, res, req.user.phonenumber, req.body.verifyCode)
    
    if(verifyStatus === 'approved') {
        req.session.verified = true
        res.redirect('/users/dashboard')
    } else {
        req.session.verified = false
        req.flash(
            'error_msg',
            'wrong verification code'
        )
        res.redirect('/users/verify')
    }
    
}
module.exports = {
    loadVerify,
    verifyUser,
    resendCode
}
</code></pre>

`resendCode()` re-sends the verification code to the user.

`verifyUser` uses the `checkVerification` function created in the previous section. If the status is `approved`, we set the `verified` value on `req.session` to true.


`req.session` just provides a nice way to access the current session. This is done by express-session, which adds the session object to our request object.

<blockquote>Hence the reason I said that most application level middleware <strong>do</strong> affect our applications state (request and response objects)</blockquote>  

## Building The User Routes

Basically, our application is going to have the following routes:

1. `/user/login`: for user login;
2. `/user/signup`: for user registration;
3. `/user/logout`: for log out;
4. `/user/resend`: to resend a verification code;
5. `/user/verify`: for input of verification code;
6. `/user/dashboard`: the route that is protected using `Twilio Verify`.

<pre><code class="language-bash">cd routes
touch user.js
</code></pre>

In `routes/user.js`, it requires the needed packages:

<pre><code class="language-javascript">const express = require('express')
const router = express.Router()
const { createUser, getSignup } = require('../controllers/signUpController')
const { authUser, getLogin } = require('../controllers/loginController')
const { loadVerify, verifyUser, resendCode } = require('../controllers/verifyController')
const { isLoggedIn, isVerified, notVerified, notLoggedIn } = require('../config/middleware')

//login route
router.route('/login')
    .all(notLoggedIn)
    .get(getLogin)
    .post(authUser)

//signup route
router.route('/signup')
    .all(notLoggedIn)
    .get(getSignup)
    .post(createUser)
//logout
router.route('/logout')
    .get(async (req, res) =&gt; {
        req.logout();
        res.redirect('/');
    })
router.route('/resend')
    .all(isLoggedIn, notVerified)
    .get(resendCode)
//verify route
router.route('/verify')
    .all(isLoggedIn, notVerified)
    .get(loadVerify)
    .post(verifyUser)
//dashboard
router.route('/dashboard')
    .all(isLoggedIn, isVerified)
    .get(async (req, res) =&gt; {
        res.render('dashboard')
    })

//export router
module.exports = router
</code></pre>

We’re creating our routes in the piece of code above, let’s see what’s going on here:

`router.route()` specifies the route. If we specify `router.route('/login')`, we target the `login` route. `.all([middleware])` allows us specify that all request to that route should use those `middleware`.

The `router.route('/login').all([middleware]).get(getController).post(postController)` syntax is an alternative to the one most developers are used to. 

It does the same thing as `router.get('/login', [middleware], getController)` and `router.post('/login, [middleware], postController)`.

<blockquote>The syntax used in our code is nice because it makes our code very DRY &mdash; and it’s easier to keep up with what’s going on in our file.</blockquote>


Now, if we run our application by typing the command below in our terminal:

<pre><code class="language-bash">npm run dev 
</code></pre>

Our full-stack express application should be up and running.

## Conclusion

What we have done in this tutorial was to:  

1. Build out an express application;
2. Add passport for authentication with sessions;
3. Use Twilio Verify for route protection.

I surely hope that after this tutorial, you are ready to rethink your password-based authentication and add that extra layer of security to your application.

What you could do next:  

1. Try to explore passport, using JWT for authentication;
2. Integrate what you’ve learned here into another application;
3. Explore more Twilio products. They provide services that make development easier(Verify is just one of the many services).

### Further Reading On Smashing Magazine

- “[How To Build A Group Chat App With Vanilla JS, Twilio And Node.js](https://www.smashingmagazine.com/2022/06/build-group-chat-app-vanillajs-twilio-nodejs/),” Zara Cooper 
- “[Keeping Node.js Fast: Tools, Techniques, And Tips For Making High-Performance Node.js Servers](https://www.smashingmagazine.com/2018/06/nodejs-tools-techniques-performance-servers/),” David Mark Clements
- “[How To Protect Your API Key In Production With Next.js API Route](https://www.smashingmagazine.com/2021/12/protect-api-key-production-nextjs-api-route/),” Caleb Olojo
- “[How To Build A Node.js API For Ethereum Blockchain](https://www.smashingmagazine.com/2021/01/nodejs-api-ethereum-blockchain/),” John Agbanusi

{{< signature "nl, il" >}}
