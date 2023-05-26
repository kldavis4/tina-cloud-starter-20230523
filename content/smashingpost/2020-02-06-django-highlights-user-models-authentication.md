---
title: 'Django Highlights: User Models And Authentication (Part 1)'
slug: django-highlights-user-models-authentication
author: philip-kiely
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/57e143bf-3bb9-4886-a8f3-474997b49769/django-highlights-user-models-authentication.png
date: 2020-02-06T11:00:00.000Z
summary: >-
  One major reason to develop a dynamic site is to authenticate users and restrict content. Django provides a powerful out-of-the-box user model, and in this article, we’ll walk through the best way to provide secure, intuitive user authentication flows.
description: >-
  One major reason to develop a dynamic site is to authenticate users and restrict content. Django provides a powerful out-of-the-box user model, and in this article, we’ll walk through the best way to provide secure, intuitive user authentication flows.
categories:
  - Apps
  - Django
  - Frameworks
---

There are two types of websites: static and dynamic. [Django](https://www.djangoproject.com) is a framework for developing dynamic websites. While a static website is one that solely presents information, there is no interaction (beyond simple page requests) that gets registered to a server. In a static website, the server sends HTML, CSS, and JavaScript to a client and that’s it. More capabilities require a dynamic website, where the server stores information and responds to user interaction beyond just serving pages. One major reason to develop a dynamic site is to authenticate users and restrict content.

Writing, deploying, and administering a static website is about an order of magnitude easier, cheaper, and more secure than a dynamic site. Thus, you should only create a dynamic website if the dynamic paradigm’s additional capabilities are necessary for your project. Django simplifies and streamlines the process of creating a dynamic site with its built-in components. As one of the primary components of a dynamic web application, the "user account" object, like the wheel, is tempting to re-invent, but the standard shape is appropriate for most uses. Django provides a powerful out-of-the-box user model, and in this article, we’ll walk through the best way to provide secure, intuitive user authentication flows.

### <span class="rh">Further Parts</span> In The Series:

* [Django Highlights: Templating Saves Lines](https://www.smashingmagazine.com/2020/04/django-highlights-templating-saves-lines/) (Part 2)
* [Django Highlights: Models, Admin, And Harnessing The Relational Database](https://www.smashingmagazine.com/2020/04/django-highlights-models-admin-relational-database/) (Part 3)
* [Django Highlights: Wrangling Static Assets And Media Files](https://www.smashingmagazine.com/2020/06/django-highlights-wrangling-static-assets-media-files-part-4) (Part 4)

## Getting Set Up

If you’d like to create your own Django application to experiment with the concepts in this article, you can create a directory (and preferably a virtual environment) and then run the following commands:

<pre><code class="language-bash">pip install django
django-admin startproject PROJECTNAME
cd PROJECTNAME
python manage.py startapp APPNAME
python manage.py migrate
python manage.py runserver
</code></pre>

*If you’re looking for a walkthrough of creating your first Django project, [Django’s own website provides a great one](https://docs.djangoproject.com/en/3.0/intro/tutorial01/). In this article, we’re not using an example project, but the concepts discussed will apply to almost every Django application.*

{{% feature-panel %}}

## Standard User Model

Fundamentally, the concept of a user account exists for two reasons: access control and personalized application state. Access control is the idea that resources on a system are only available to some users. Personalized state is heavily dependent on the purpose of the application but may include settings, data, or any other records specific to an individual user. The Django stock `User` model provides sensible approaches to both use cases.

Initially, there are two types of users in a Django application: superuser accounts and regular users. Superusers have every attribute and privilege of regular accounts, but also have access to the Django admin panel, a powerful application that we’ll explore in detail in a future article. Essentially, superusers can create, edit, or delete any data in the application, including other user accounts.

{{% pull-quote %}}
 Fundamentally, the concept of a user account exists for two reasons: access control and personalized application state.
{{% /pull-quote %}}

To create a superuser on your own Django application, run:

<pre><code class="language-bash">python manage.py createsuperuser
</code></pre>

The other benefit of a user account is storing personalized data to the database. By default, Django only requires a username and password but provides optional fields for users to enter their first name, last name, and email address. You can read a [complete model reference on the Django website](https://docs.djangoproject.com/en/3.0/topics/auth/default/). We’ll discuss extending this model below.

### Security And Reliability

Django includes substantial password management middleware with the user model. User passwords are required to be at least 8 characters, not entirely numbers, not match too closely to the username, and not be on a list of the 20,000 most common passwords. The Django stock forms validate these requirements. When a password is sent to the server, it is encrypted before it is stored, by default using the PBKDF2 algorithm with a SHA256 hash. Overall, the default password system provides robust security without any effort from the developer. Unless you have specific expertise and a compelling reason to change the way passwords are handled in your application, don’t modify this behavior.

One other convenient built-in is the requirement that usernames are unique. If you think about it, if there were two users with the username "djangofan1" and the server received a login request for that username it would not know which user was trying to access the application. Unfortunately for them, the second user to try to register with "djangofan1" will have to pick a different name, perhaps "djangofan2". This uniqueness constraint is enforced at the database level but is again verified by the forms that Django provides.

Finally, a note on deleting users. While deleting users is a possibility, most complex applications will have a number of resources tied to each user account. If you want to effectively delete a user without removing those attached objects, set the user’s `is_active` field to false instead. Then, those other resources remain associated with the account rather than being deleted themselves, and the user account is able to be re-activated at any time by a superuser. Note that this does not free up the username, but setting the account as inactive in conjunction with changing the username to a random, unique value could achieve the same effect. Finally, if your site policies or applicable local law require that user accounts be fully deletable, the `is_active` approach will not be sufficient.

{{% pull-quote %}}
 Unless you have specific expertise and a compelling reason to change the way passwords are handled in your application, don’t modify this behavior.
{{% /pull-quote %}}

### Standard Use

When you want to register a new user account, the view for doing so will probably look something like the following in *views.py*:

<pre><code class="language-python">from django.shortcuts import render, redirect
from django.contrib.auth import authenticate, login
from django.contrib.auth.forms import UserCreationForm

def signup(request):
    if request.user.is_authenticated:
        return redirect('/')
    if request.method == 'POST':
        form = UserCreationForm(request.POST)
        if form.is_valid():
            form.save()
            username = form.cleaned_data.get('username')
            password = form.cleaned_data.get('password1')
            user = authenticate(username=username, password=password)
            login(request, user)
            return redirect('/')
        else:
            return render(request, 'signup.html', {'form': form})
    else:
        form = UserCreationForm()
        return render(request, 'signup.html', {'form': form})
</code></pre>

Let’s break that down:

* If the user is already signed in, we’ll redirect them away from the signup page. 
* If the request method is POST, that means that the form for creating a user has already been filled out and it’s time to create a user.
  * First, construct the form object on the backend with the user-provided data.
  * If the form is valid, create the user and log them in, then send them to the main page.
  * Otherwise, dump them back on the user creation page with information about what data was invalid (for example, they requested a username already in use).
* Otherwise, the user is accessing the page for the first time and should be met with the form for creating a new account.

Now examining account signin:

<pre><code class="language-python">from django.shortcuts import render, redirect
from django.contrib.auth import authenticate, login
from django.contrib.auth.forms import AuthenticationForm

def signin(request):
    if request.user.is_authenticated:
        return render(request, 'homepage.html')
    if request.method == 'POST':
        username = request.POST['username']
        password = request.POST['password']
        user = authenticate(request, username=username, password=password)
        if user is not None:
            login(request, user)
            return redirect('/')
        else:
            form = AuthenticationForm(request.POST)
            return render(request, 'signin.html', {'form': form})
    else:
        form = AuthenticationForm()
        return render(request, 'signin.html', {'form': form})
</code></pre>

Another breakdown:

* If the user is already signed in, we’ll redirect them away from the sign-in page. 
* If the request method is POST, that means that the form for signing in has been filled and it’s time to authenticate the user to an account.
  * First, authenticate the user with the user-provided data
  * If the username and password correspond to an account, log the user in
  * Otherwise, bring them back to the sign-in page with their form information pre-filled
* Otherwise, the user is accessing the page for the first time and should be met with the form for logging in.

Finally, your users may eventually want to sign out. The basic code for this request is simple:

<pre><code class="language-python">from django.shortcuts import render, redirect
from django.contrib.auth import logout

def signout(request):
    logout(request)
    return redirect('/')
</code></pre>

Once the user has been logged in to their account, and until they log out on that device, they are having a "session." During this time, subsequent requests from their browser will be able to access account-only pages. A user can have multiple sessions active at the same time. By default, sessions do not time out.

While a user has an active session on their device, they will register as `True` for the `request.user.is_authenticated` check. Another way to restrict pages to logged-in users only is the `@login_required` decorator above a function. There are multiple other ways of achieving the same, [detailed here](https://docs.djangoproject.com/en/3.0/topics/auth/default/#limiting-access-to-logged-in-users).

If this level of configuration is more than you want to perform, there is an even more out-of-the-box approach to user management. These [stock authentication views](https://docs.djangoproject.com/en/3.0/topics/auth/default/#module-django.contrib.auth.views) provide standard routes, views, and forms for user management and can be modified by assigning them to custom URLs, passing custom templates, or even subclassing the views for more control.

{{% ad-panel-leaderboard %}}

## Extending The User Model

Generally, you need to expand the user model to provide finer-grained access controls or store more user data per account. We’ll explore several common cases below.

### Dropping Fields From The User Model

Contrary to this section’s header, I do not actually recommend making changes directly to the user model or associated database schema! The generic user model is established in your database by default during the setup of a new Django project. So much is tied to the default user model that changing it could have unexpected effects in your application (especially if you’re using third-party libraries), accordingly, adding or removing fields is not recommended and is not made easy by the framework.

By default, the only two fields that are required for a user are username and password. If you don’t want to use any of the other fields, simply ignore their existence, as a user can be created without a first name, last name, or email address. There is a collection of default fields like last_login and date_joined that can also be ignored if you don’t want them. If you had an actual technical constraint that required dropping optional fields from the user model, you would already know about it and wouldn’t need this article.

A common reason you might want to drop a field in the user model is to drop the username in favor of the email as a unique identifier. In that case, when creating the user from form data or authenticating a request, simply enter the email address as the username in addition to its use in the email field. The username field will still enforce the uniqueness constraint when usernames are formatted as email addresses. Strings are strings, they will be treated the same.

{{% pull-quote %}}
 So much is tied to the default user model that changing it could have unexpected effects in your application, especially if you’re using third-party libraries.
{{% /pull-quote %}}

### Adding Fields With A Profile

Similarly, if you want to store extra information about your users, you should not attempt to modify the default user model. Even for a single field, define your own object with a one-to-one relationship with the existing users. This extra model is often called the `Profile`. Say you wanted to store a middle name and date of birth (dob) for each user. The `Profile` would be defined as follows in *models.py*:

<pre><code class="language-python">from django.db import models
from django.contrib.auth.models import User

class Profile(models.Model):
    user = models.OneToOneField(User, on_delete=models.CASCADE)
    middle_name = models.CharField(max_length=30, blank=True)
    dob = models.DateField(null=True, blank=True)
</code></pre>

### Custom Access Control

Your application may have required a distinction between different types of users for accessing information and functions. Django provides a system for creating custom fine-grained access control: permissions and groups.

[Permissions](https://docs.djangoproject.com/en/3.0/ref/contrib/auth/#django.contrib.auth.models.Permission) are objects that determine access to resources. A user can have one or more permissions. For example, they might have read access to a table of products and write access to a table of customers. The exact implementation of permission varies substantially by application but Django’s approach makes it intuitive to define permissions for data and assign those permissions to users.

Applications for enterprise and other large organizations often implement [role-based access control](https://en.wikipedia.org/wiki/Role-based_access_control). Essentially, a user can have various roles, each of which has certain permissions. Django’s tool for implementing this pattern is the [Group](https://docs.djangoproject.com/en/3.0/ref/contrib/auth/#django.contrib.auth.models.Group). A group can have any number of permissions, which can each be assigned to any number of groups. A user then gains permissions not directly but by their membership to groups, making the application easier to administer.

### Overview: Integrating A Payment Provider

The precise process of integrating a payment processor varies substantially by application and provider. However, I’ll cover the process in general terms.

One of the key advantages of outsourcing payments is that the provider is responsible for storing and validating highly regulated data such as credit card information. The service then shares some unique user token with your application along with data about their payment history. Like adding the profile, you can create a model associated with the core `User` and store the data in that model. As with passwords, it’s important to follow the given integration with the provider to avoid storing sensitive information improperly.

{{% ad-panel-leaderboard %}}

### Overview: Social Sign-In

The other broad, complex field I want to briefly touch upon is social sign-in. Large platforms like Facebook and Google, as well as smaller sites like GitHub, provide APIs for using their services to authenticate users. Similar to a payment provider, this creates a record in your database linking an account to an account in their database.

You might want to include social auth in your site to make it easier for users to sign up without creating a new set of login credentials. If your application solely targets customers who already use a specific site that provides a social auth option, it might help you attract users from that market by lowering the barrier of entry. Furthermore, if your application intends to access the user’s data from a third-party service, linking the accounts during authentication simplifies the process of granting permissions.

However, there are downsides to using social auth. API changes or outages from the third party provider could interrupt your application’s uptime or development activities. In general, external dependencies add complexity to the application. Finally, it’s worth considering the data collection and use policies of third parties that you are integrating with and make sure that they align with your and your users' expectations.

If you do decide that social authentication is right for your application, fortunately, there’s a library for that. [Python Social Auth for Django](https://github.com/python-social-auth/social-app-django) is a package for enabling the capabilities of Python’s social auth ecosystem in Django projects. 

## Wrapping Up

As universal as the user account is, its widespread use can lead to resolving the same problems needlessly. Hopefully, this article has shown you the range of powerful features available in Django and given you an understanding of the basic responsibilities of an application when creating user accounts. 

Django Highlights is a series introducing important concepts of web development in Django. Each article is written as a stand-alone guide to a facet of Django development intended to help front-end developers and designers reach a deeper understanding of "the other half" of the codebase. These articles are mostly constructed to help you gain an understanding of theory and convention but contain some code samples, which are written in Django 3.0. Several concepts that we touched on in this article, including templates, admin users, models, and forms, will be explored individually in detail in future articles in this series.

### <span class="rh">Further Parts</span> In The Series:

* [Django Highlights: Templating Saves Lines](https://www.smashingmagazine.com/2020/04/django-highlights-templating-saves-lines/) (Part 2)
* [Django Highlights: Models, Admin, And Harnessing The Relational Database](https://www.smashingmagazine.com/2020/04/django-highlights-models-admin-relational-database/) (Part 3)
* [Django Highlights: Wrangling Static Assets And Media Files](https://www.smashingmagazine.com/2020/06/django-highlights-wrangling-static-assets-media-files-part-4) (Part 4)

{{< signature "dm, il" >}}
