---
title: 'Setting Up An API Using Flask, Google’s Cloud SQL And App Engine'
slug: api-flask-google-cloudsql-app-engine
author: wole-oyekanmi
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/babddeaf-7d71-4dc1-99b4-19c2dd7613a2/api-flask-google-cloudsql-app-engine.png
date: 2020-08-19T10:30:00.000Z
summary: >-
  Flask makes it possible for developers to build an API for whatever use case they might have. In this tutorial, we’ll learn how to set up Google Cloud, Cloud SQL, and App Engine to build a Flask API. (Cloud SQL is a fully managed platform-as-a-service (PaaS) database engine, and App Engine is a fully managed PaaS for hosting applications.)
description: >-
  Flask makes it possible for developers to build an API for whatever use case they might have. In this tutorial, we’ll learn how to set up Google Cloud, Cloud SQL, and App Engine to build a Flask API.
categories:
  - Apps
  - API
  - Frameworks
---

A few Python frameworks can be used to create APIs, two of which are Flask and Django. Frameworks comes with functionality that makes it easy for developers to implement the features that users need to interact with their applications. The complexity of a web application could be a deciding factor when you’re choosing which framework to work with.

### Django

[Django](https://www.djangoproject.com/) is a robust framework that has a predefined structure with built-in functionality. The downside of its robustness, however, is that it could make the framework too complex for certain projects. It’s best suited to complex web applications that need to leverage the advanced functionality of Django.

### Flask

[Flask](https://en.wikipedia.org/wiki/Flask_(web_framework)), on the other hand, is a lightweight framework for building APIs. Getting started with it is easy, and packages are available to make it robust as you go. This article will focus on defining the view functions and controller and on connecting to a database on Google Cloud and deploying to Google Cloud.

For the purpose of learning, we’ll build a Flask API with a few endpoints to manage a collection of our favorite songs. The endpoints will be for `GET` and `POST` requests: fetching and creating resources. Alongside that, we will be using the suite of services on the [Google Cloud](https://cloud.google.com/) platform. We’ll set up Google’s [Cloud SQL](https://console.cloud.google.com/marketplace/details/google-cloud-platform/cloud-sql?pli=1) for our database and launch our app by deploying to [App Engine](https://cloud.google.com/appengine/docs). This tutorial is aimed at beginners who are taking their first stab at using Google Cloud for their app.

## Setting Up A Flask Project

This tutorial assumes you have Python 3.x installed. If you don’t, head over to the [official website](https://www.python.org/downloads/) to download and install it.

To check whether Python is installed, launch your command-line interface (CLI) and run the command below:

<pre><code class="language-bash">python -V
</code></pre>

Our first step is to create the directory where our project will live. We will call it `flask-app`:

<pre><code class="language-bash">mkdir flask-app && cd flask-app
</code></pre>

The first thing to do when starting a Python project is to create a virtual environment. Virtual environments isolate your working Python development. This means that this project can have its own dependencies, different from other project on your machines. [venv](https://docs.python.org/3/library/venv.html) is a module that ships with Python 3.

{{% feature-panel %}}

Let’s create a virtual environment in our `flask-app` directory:

<pre><code class="language-bash">python3 -m venv env
</code></pre>

This command creates an `env` folder in our directory. The name (in this case, `env`) is an alias for the virtual environment and can be named anything.

Now that we’ve created the virtual environment, we have to tell our project to use it. To activate our virtual environment, use the following command:

<pre><code class="language-bash">source env/bin/activate
</code></pre>

You will see that your CLI prompt now has `env` at the beginning, indicating that our environment is active.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2c76f6bf-d6cf-4e65-804a-cd763c926fb5/terminal-environment-api-flask-google-cloud-sql-app-engine.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2c76f6bf-d6cf-4e65-804a-cd763c926fb5/terminal-environment-api-flask-google-cloud-sql-app-engine.png" sizes="100vw" caption="<code>(env)</code> appears before the prompt (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2c76f6bf-d6cf-4e65-804a-cd763c926fb5/terminal-environment-api-flask-google-cloud-sql-app-engine.png'>Large preview</a>)" alt="It shows the env prompt to indicate that an environment is active" >}}

Now, let’s install our Flask package:

<pre><code class="language-bash">pip install flask
</code></pre>

Create a directory named `api` in our current directory. We’re creating this directory so that we have a folder where our app’s other folders will reside.

<pre><code class="language-bash">mkdir api && cd api
</code></pre>

Next, create a `main.py` file, which will serve as the entry point to our app:

<pre><code class="language-bash">touch main.py
</code></pre>

Open `main.py`, and enter the following code:

<pre><code class="language-py">#main.py
from flask import Flask

app = Flask(__name__)

@app.route('/')
def home():
  return 'Hello World'

if __name__ == '__main__':
  app.run()
</code></pre>

Let’s understand what we’ve done here. We first imported the `Flask` class from the Flask package. Then, we created an instance of the class and assigned it to `app`. Next, we created our first endpoint, which points to our app’s root. In summary, this is a view function that invokes the `/` route &mdash; it returns `Hello World`.

Let’s run the app:

<pre><code class="language-bash">python main.py
</code></pre>

This starts our local server and serves our app on `https://127.0.0.1:5000/`. Input the URL in your browser, and you will see the `Hello World` response printed on your screen.

And voilà! Our app is up and running. The next task is to make it functional.

To call our endpoints, we will be using Postman, which is a service that helps developers test endpoints. You can [download it](https://www.postman.com/downloads/) from the official website.

Let’s make `main.py` return some data:

<pre><code class="language-py">#main.py
from flask import Flask, jsonify
app = Flask(__name__)
songs = [
    {
        "title": "Rockstar",
        "artist": "Dababy",
        "genre": "rap",
    },
    {
        "title": "Say So",
        "artist": "Doja Cat",
        "genre": "Hiphop",
    },
    {
        "title": "Panini",
        "artist": "Lil Nas X",
        "genre": "Hiphop"
    }
]
@app.route('/songs')
def home():
    return jsonify(songs)

if __name__ == '__main__':
  app.run()
</code></pre>

Here, we included a list of songs, including the song’s title and artist’s name. We then changed the root `/` route to `/songs`. This route returns the array of songs that we specified. In order to get our list as a JSON value, we JSONified the list by passing it through `jsonify`. Now, rather than seeing a simple `Hello world`, we see a list of artists when we access the `https://127.0.0.1:5000/songs` endpoint.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7b426afe-fb0e-45a1-aa45-ff09e0914409/postman-response-1-api-flask-google-cloud-sql-app-engine.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7b426afe-fb0e-45a1-aa45-ff09e0914409/postman-response-1-api-flask-google-cloud-sql-app-engine.png" sizes="100vw" caption="A <code>get</code> response from Postman (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7b426afe-fb0e-45a1-aa45-ff09e0914409/postman-response-1-api-flask-google-cloud-sql-app-engine.png'>Large preview</a>)" alt="This image shows the response from a get request" >}}

You may have noticed that after every change, we had to restart our server. To enable auto-reloading when the code changes, let’s enable the debug option. To do this, change `app.run` to this:

<pre><code class="language-bash">app.run(debug=True)
</code></pre>

Next, let’s add a song using a post request to our array. First, import the `request` object, so that we can process incoming request from our users. We’ll later use the `request` object in the view function to get the user’s input in JSON.

<pre><code class="language-json">#main.py
from flask import Flask, jsonify, request

app = Flask(__name__)
songs = [
    {
        "title": "Rockstar",
        "artist": "Dababy",
        "genre": "rap",
    },
    {
        "title": "Say So",
        "artist": "Doja Cat",
        "genre": "Hiphop",
    },
    {
        "title": "Panini",
        "artist": "Lil Nas X",
        "genre": "Hiphop"
    }
]
@app.route('/songs')
def home():
    return jsonify(songs)

@app.route('/songs', methods=['POST'])
def add_songs():
    song = request.get_json()
    songs.append(song)
    return jsonify(songs)

if __name__ == '__main__':
  app.run(debug=True)
</code></pre>

Our `add_songs` view function takes a user-submitted song and appends it to our existing list of songs.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4f54cdfd-7bfd-44e5-92b4-d19a9313414e/postman-response-2-api-flask-google-cloud-sql-app-engine.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4f54cdfd-7bfd-44e5-92b4-d19a9313414e/postman-response-2-api-flask-google-cloud-sql-app-engine.png" sizes="100vw" caption="Post request from Postman (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4f54cdfd-7bfd-44e5-92b4-d19a9313414e/postman-response-2-api-flask-google-cloud-sql-app-engine.png'>Large preview</a>)" alt="This image demonstrates a post request using Postman" >}}

So far, we have returned our data from a Python list. This is just experimental, because in a more robust environment, our newly added data would be lost if we restarted the server. That is not feasible, so we will require a live database to store and retrieve the data. In comes Cloud SQL.

{{% ad-panel-leaderboard %}}

## Why Use A Cloud SQL Instance?

According to the [official website](https://cloud.google.com/sql):

<blockquote>“Google Cloud SQL is a fully-managed database service that makes it easy to set-up, maintain, manage and administer your relational MySQL and PostgreSQL databases in the cloud. Hosted on Google Cloud Platform, Cloud SQL provides a database infrastructure for applications running anywhere.”</blockquote>

This means that we can outsource the management of a database’s infrastructure entirely to Google, at flexible pricing.

### Difference Between Cloud SQL And A Self-Managed Compute Engine

On Google Cloud, we can spin up a virtual machine on Google’s Compute Engine infrastructure and install our SQL instance. This means we will be responsible for vertical scalability, replication, and a host of other configuration. With Cloud SQL, we get a lot of configuration out of the box, so we can spend more time on the code and less time setting up.

Before we begin:

1. Sign up for [Google Cloud](https://cloud.google.com/). Google offers $300 in [free credit](https://cloud.google.com/free/docs/gcp-free-tier) to new users.
2. Create a [project](https://cloud.google.com/resource-manager/docs/creating-managing-projects#console). This is pretty straightforward and can be done right from the console.

## Create A Cloud SQL Instance

After signing up for Google Cloud, in the left panel, scroll to the “SQL” tab and click on it.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1b3ea993-10df-489e-954c-271360cd8f39/snapshot-gcp-api-flask-google-cloud-sql-app-engine.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a5ea44a7-fce4-41d5-b39f-d8e8e3a1eb51/snapshot-gcp-api-flask-google-cloud-sql-app-engine-large.png" sizes="100vw" caption="Snapshot of GCP services (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1b3ea993-10df-489e-954c-271360cd8f39/snapshot-gcp-api-flask-google-cloud-sql-app-engine.png'>Large preview</a>)" alt="This image shows a sub-section of GCP services" >}}

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/49143198-a7d3-4960-9da7-eb68235c9458/cloud-sql-console-api-flask-google-cloud-sql-app-engine.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/49143198-a7d3-4960-9da7-eb68235c9458/cloud-sql-console-api-flask-google-cloud-sql-app-engine.png" sizes="100vw" caption="Cloud SQL’s console page (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/49143198-a7d3-4960-9da7-eb68235c9458/cloud-sql-console-api-flask-google-cloud-sql-app-engine.png'>Large preview</a>)" alt="This image shows the three database engines in offering for Cloud SQL" >}}

First, we are required to choose an SQL engine. We’ll go with MySQL for this article.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8f31770f-5cc0-4ce3-bcaa-1bd9572a5ea8/creating-mysql-instance-api-flask-google-cloud-sql-app-engine.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8f31770f-5cc0-4ce3-bcaa-1bd9572a5ea8/creating-mysql-instance-api-flask-google-cloud-sql-app-engine.png" sizes="100vw" caption="Creating a new Cloud SQL instance (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8f31770f-5cc0-4ce3-bcaa-1bd9572a5ea8/creating-mysql-instance-api-flask-google-cloud-sql-app-engine.png'>Large preview</a>)" alt="This image show the page for creating a Cloud SQL instance" >}}

Next, we’ll create an instance. By default, our instance will be created in the US, and the zone will be automatically selected for us.

Set the root password and give the instance a name, and then click the “Create” button. You can further configure the instance by clicking the “Show configuration options” dropdown. The settings allows you to configure the instance’s size, storage capacity, security, availability, backups, and more. For this article, we will go with the default settings. Not to worry, these variables can be changed later.

It might take a few minutes for the process to finish. You’ll know the instance is ready when you see a green checkmark. Click on your instance’s name to go to the details page.

Now, that we’re up and running, we will do a few things:

1. Create a database.
2. Create a new user.
3. Whitelist our IP address.

### Create A Database

Navigate to the “Database” tab to create a database.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fa8ded40-b460-4c61-8686-ceb7ec2a22e2/create-new-db-api-flask-google-cloud-sql-app-engine.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fa8ded40-b460-4c61-8686-ceb7ec2a22e2/create-new-db-api-flask-google-cloud-sql-app-engine.png" sizes="100vw" caption="Creating a new database on Cloud SQL (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fa8ded40-b460-4c61-8686-ceb7ec2a22e2/create-new-db-api-flask-google-cloud-sql-app-engine.png'>Large preview</a>)" alt="This image shows the creation of a new user on Cloud SQL" >}}

### Create A New User

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f1be1d3a-258d-48a0-9c22-3ccf20fb19d4/create-new-user-api-flask-google-cloud-sql-app-engine.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f1be1d3a-258d-48a0-9c22-3ccf20fb19d4/create-new-user-api-flask-google-cloud-sql-app-engine.png" sizes="100vw" caption="Creating a new user on Cloud SQL (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f1be1d3a-258d-48a0-9c22-3ccf20fb19d4/create-new-user-api-flask-google-cloud-sql-app-engine.png'>Large preview</a>)" alt="" >}}

In the “Host name” section, set it to allow “% (any host)”.

### Whitelist IP Address

You can connect to your database instance in one of two ways. A **private IP** address requires a virtual private cloud (VPC). If you go for this option, Google Cloud will create a Google-managed [VPC](https://cloud.google.com/vpc/docs/overview) and place your instance in it. For this article, we will use the **public IP** address, which is the default. It is public in the sense that only people whose IP addresses have been whitelisted can access the database.

To whitelist your IP address, type `my ip` in a Google search to get your IP. Then, go to the “Connections” tab and “Add Network”.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8dc6e411-382e-4cd1-b886-8e3eafc64bf1/whitelist-ip-api-flask-google-cloud-sql-app-engine.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8dc6e411-382e-4cd1-b886-8e3eafc64bf1/whitelist-ip-api-flask-google-cloud-sql-app-engine.png" sizes="100vw" caption="Whitelist your IP address (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8dc6e411-382e-4cd1-b886-8e3eafc64bf1/whitelist-ip-api-flask-google-cloud-sql-app-engine.png'>Large preview</a>)" alt="This image shows the page for IP whitelisting" >}}

### Connect To The Instance

Next, navigate to the “Overview” panel and connect using the cloud shell.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/18342610-5ce6-487f-a454-1fa96de53b73/cloud-sql-dashboard-api-flask-google-cloud-sql-app-engine.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/18342610-5ce6-487f-a454-1fa96de53b73/cloud-sql-dashboard-api-flask-google-cloud-sql-app-engine.png" sizes="100vw" caption="Cloud SQL dashboard (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/18342610-5ce6-487f-a454-1fa96de53b73/cloud-sql-dashboard-api-flask-google-cloud-sql-app-engine.png'>Large preview</a>)" alt="This image shows the Cloud SQL dashboard" >}}

The command to connect to our Cloud SQL instance will be pre-typed in the console.

You may use either the root user or the user who was created earlier. In the command below, we’re saying: Connect to the `flask-demo` instance as the user `USERNAME`. You will be prompted to input the user’s password.

<pre><code class="language-bash">gcloud sql connect flask-demo --user=USERNAME
</code></pre>

If you get an error saying that you don’t have a project ID, you can get your project’s ID by running this:

<pre><code class="language-bash">gcloud projects list
</code></pre>

Take the project ID that was outputted from the command above, and input it into the command below, replacing `PROJECT_ID` with it.

<pre><code class="language-bash">gcloud config set project PROJECT_ID
</code></pre>

Then, run the `gcloud sql connect` command, and we will be connected.

Run this command to see the active databases:

<pre><code class="language-bash">> show databases;
</code></pre>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1ce6e6b7-6c20-4484-be3b-e608f221077a/show-db-shell-api-flask-google-cloud-sql-app-engine.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/26641172-010a-4419-9efd-81f69763247f/show-db-shell-api-flask-google-cloud-sql-app-engine-large.png" sizes="100vw" caption="Shell output for “show databases” (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1ce6e6b7-6c20-4484-be3b-e608f221077a/show-db-shell-api-flask-google-cloud-sql-app-engine.png'>Large preview</a>)" alt="This image shows the shell output for when we run show databases in the cloud shell" >}}

My database is named `db_demo`, and I’ll run the command below to use the `db_demo` database. You might see some other databases, such as `information_schema` and `performance_schema`. These are there to store table meta data.

<pre><code class="language-bash">> use db_demo;
</code></pre>

Next, create a table that mirrors the list from our Flask app. Type the code below on a notepad and paste it in your cloud shell:

<pre><code class="language-markup">create table songs(
song_id INT NOT NULL AUTO_INCREMENT,
title VARCHAR(255),
artist VARCHAR(255),
genre VARCHAR(255),
PRIMARY KEY(song_id)
);
</code></pre>

This code is a SQL command that creates a table named `songs`, with four columns (`song_id`, `title`, `artist`, and `genre`). We’ve also instructed that the table should define `song_id` as a primary key and increment automatically from 1.

Now, run `show tables;` to confirm that the table has been created.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ff1c7d05-8224-440e-8c87-52fa308fde88/show-tables-shell-api-flask-google-cloud-sql-app-engine.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/22c4ab69-089f-4c2c-bf69-4dde17256865/show-tables-shell-api-flask-google-cloud-sql-app-engine-large.png" sizes="100vw" caption="Shell output for “show tables” (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ff1c7d05-8224-440e-8c87-52fa308fde88/show-tables-shell-api-flask-google-cloud-sql-app-engine.png'>Large preview</a>)" alt="This image shows the shell output for when we run show tables in the cloud shell" >}}

And just like that, we have created a database and our `songs` table.

Our next task is to set up Google App Engine so that we can deploy our app.

{{% ad-panel-leaderboard %}}

## Google App Engine

App Engine is a fully managed platform for developing and hosting web applications at scale. An advantage of deploying to App Engine is that it enables an app to scale automatically to meet incoming traffic.

The [App Engine website](https://cloud.google.com/appengine) says:

<blockquote>“With zero server management and zero configuration deployments, developers can focus only on building great applications without the management overhead.”</blockquote>

### Set Up App Engine

There are a few ways to set up App Engine: through the UI of Google Cloud Console or through the Google Cloud SDK. We will use the SDK for this section. It enables us to deploy, manage, and monitor our Google Cloud instance from our local machine.

### Install Google Cloud SDK

Follow the instructions to download and install the SDK for [Mac](https://cloud.google.com/sdk/docs/quickstart-macos) or [Windows](https://cloud.google.com/sdk/docs/quickstart-windows). The guide will also show you how to initialize the SDK in your CLI and how to pick a Google Cloud project.

Now that the SDK has been installed, we’re going to go update our Python script with our database’s credentials and deploy to App Engine.

### Local Setup

In our local environment, we are going to update the setup to suit our new architecture, which includes Cloud SQL and App Engine.

First, add an `app.yaml` file to our root folder. This is a configuration file that App Engine requires to host and run our app. It tells App Engine of our runtime and other variables that might be required. For our app, we will need to add our database’s credentials as environment variables, so that App Engine is aware of our database’s instance.

In the `app.yaml` file, add the snippet below. You will have gotten the runtime and database variables from setting up the database. Replace the values with the username, password, database name, and connection name that you used when setting up Cloud SQL.

<pre><code class="language-bash">#app.yaml
runtime: python37

env_variables:
  CLOUD_SQL_USERNAME: YOUR-DB-USERNAME
  CLOUD_SQL_PASSWORD: YOUR-DB-PASSWORD
  CLOUD_SQL_DATABASE_NAME: YOUR-DB-NAME
  CLOUD_SQL_CONNECTION_NAME: YOUR-CONN-NAME
</code></pre>

Now, we are going to install [PyMySQL](https://pymysql.readthedocs.io/en/latest/). This is a Python MySQL package that connects and performs queries on a MySQL database. Install the PyMySQL package by running this line in your CLI:

<pre><code class="language-bash">pip install pymysql
</code></pre>

At this point, we are ready to use PyMySQL to connect to our Cloud SQL database from the app. This will enable us to get and insert queries in our database.

### Initialize Database Connector

First, create a `db.py` file in our root folder, and add the code below:

<div class="break-out">

 <pre><code class="language-py">#db.py
import os
import pymysql
from flask import jsonify

db_user = os.environ.get('CLOUD_SQL_USERNAME')
db_password = os.environ.get('CLOUD_SQL_PASSWORD')
db_name = os.environ.get('CLOUD_SQL_DATABASE_NAME')
db_connection_name = os.environ.get('CLOUD_SQL_CONNECTION_NAME')


def open_connection():
    unix_socket = '/cloudsql/{}'.format(db_connection_name)
    try:
        if os.environ.get('GAE_ENV') == 'standard':
            conn = pymysql.connect(user=db_user, password=db_password,
                                unix_socket=unix_socket, db=db_name,
                                cursorclass=pymysql.cursors.DictCursor
                                )
    except pymysql.MySQLError as e:
        print(e)

    return conn


def get_songs():
    conn = open_connection()
    with conn.cursor() as cursor:
        result = cursor.execute('SELECT * FROM songs;')
        songs = cursor.fetchall()
        if result > 0:
            got_songs = jsonify(songs)
        else:
            got_songs = 'No Songs in DB'
    conn.close()
    return got_songs

def add_songs(song):
    conn = open_connection()
    with conn.cursor() as cursor:
        cursor.execute('INSERT INTO songs (title, artist, genre) VALUES(%s, %s, %s)', (song["title"], song["artist"], song["genre"]))
    conn.commit()
    conn.close()
</code></pre>
</div>

We did a few things here.

First, we retrieved our database credentials from the `app.yaml` file using the `os.environ.get` method. App Engine is able to make environment variables that are defined in `app.yaml` available in the app.

Secondly, we created an `open_connection` function. It connects to our MySQL database with the credentials.

Thirdly, we added two functions: `get_songs` and `add_songs`. The first initiates a connection to the database by calling the `open_connection` function. It then queries the `songs` table for every row and, if empty, returns “No Songs in DB”. The `add_songs` function inserts a new record into the `songs` table.

Finally, we return to where we started, our `main.py` file. Now, instead of getting our songs from an object, as we did earlier, we call the `add_songs` function to insert a record, and we call the `get_songs` function to retrieve the records from the database.

Let’s refactor `main.py`:

<div class="break-out">

 <pre><code class="language-py">#main.py
from flask import Flask, jsonify, request
from db import get_songs, add_songs

app = Flask(__name__)

@app.route('/', methods=['POST', 'GET'])
def songs():
    if request.method == 'POST':
        if not request.is_json:
            return jsonify({"msg": "Missing JSON in request"}), 400  

        add_songs(request.get_json())
        return 'Song Added'

    return get_songs()    

if __name__ == '__main__':
    app.run()
</code></pre>
</div>

We imported the `get_songs` and `add_songs` functions and called them in our `songs()` view function. If we are making a `post` request, we call the `add_songs` function, and if we are making a `get` request, we call the `get_songs` function.  

And our app is done.

Next up is adding a `requirements.txt` file. This file contains a list of packages necessary to run the app. App Engine checks this file and installs the listed packages.

<pre><code class="language-markup">pip freeze &#124; grep "Flask&#92;&#124;PyMySQL" &gt; requirements.txt
</code></pre>

This line gets the two packages that we are using for the app (Flask and PyMySQL), creates a `requirements.txt` file, and appends the packages and their versions to the file.

At this point, we have added three new files: `db.py`, `app.yaml`, and `requirements.txt`.

### Deploy to Google App Engine

Run the following command to deploy your app:

<pre><code class="language-bash">gcloud app deploy
</code></pre>

If it went well, your console will output this:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/63229015-b46c-433c-9041-24f9cd4702c2/postman-response-3-api-flask-google-cloud-sql-app-engine.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/63229015-b46c-433c-9041-24f9cd4702c2/postman-response-3-api-flask-google-cloud-sql-app-engine.png" sizes="100vw" caption="CLI output for App Engine deployment (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/63229015-b46c-433c-9041-24f9cd4702c2/postman-response-3-api-flask-google-cloud-sql-app-engine.png'>Large preview</a>)" alt="This image shows the output when deploying to App Engine" >}}

Your app is now running on App Engine. To see it in the browser, run `gcloud app browse` in your CLI.

We can launch Postman to test our `post` and `get` requests.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/63229015-b46c-433c-9041-24f9cd4702c2/postman-response-3-api-flask-google-cloud-sql-app-engine.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/63229015-b46c-433c-9041-24f9cd4702c2/postman-response-3-api-flask-google-cloud-sql-app-engine.png" sizes="100vw" caption="Demonstrating a post request (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/63229015-b46c-433c-9041-24f9cd4702c2/postman-response-3-api-flask-google-cloud-sql-app-engine.png'>Large preview</a>)" alt="This image demonstrates a post request to our deployed app" >}}

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8e24bc46-9374-4057-8b1f-4f203c9cf75a/postman-response-4-api-flask-google-cloud-sql-app-engine.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8e24bc46-9374-4057-8b1f-4f203c9cf75a/postman-response-4-api-flask-google-cloud-sql-app-engine.png" sizes="100vw" caption="Demonstrating a <code>get</code> request (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8e24bc46-9374-4057-8b1f-4f203c9cf75a/postman-response-4-api-flask-google-cloud-sql-app-engine.png'>Large preview</a>)" alt="This image demonstrates a get request to our deployed app" >}}

Our app is now hosted on Google’s infrastructure, and we can tweak the configuration to get all of the benefits of a serverless architecture. Going forward, you can build on this article to make your serverless application more robust.

## Conclusion

Using a platform-as-a-service (PaaS) infrastructure like App Engine and Cloud SQL basically abstracts away the infrastructure level and enables us to build more quickly. As developers, we do not have to worry about configuration, backing up and restoring, the operating system, auto-scaling, firewalls,  migrating traffic, and so on. However, if you need control over the underlying configuration, then it might be better to use a custom-built service.

### References

- “[Download Python](https://www.python.org/downloads/)”
- “[venv &mdash; Creation of Virtual Environments](https://docs.python.org/3/library/venv.html)”, Python (documentation)
- “[Download Postman](https://www.postman.com/downloads/)”
- “[Cloud SQL](https://cloud.google.com/sql)”, Google Cloud
- [Google Cloud](https://cloud.google.com/)
- “[Google Cloud Free Tier](https://cloud.google.com/free/docs/gcp-free-tier)”, Google Cloud
- “[Creating and Managing Projects](https://cloud.google.com/resource-manager/docs/creating-managing-projects#console)”, Google Cloud
- “[VPC Overview](https://cloud.google.com/vpc/docs/overview)” (virtual private cloud), Google Cloud
- “[App Engine](https://cloud.google.com/appengine)”, Google Cloud
- “[Quickstarts](https://cloud.google.com/sdk/docs/quickstart-macos)” (download Google Cloud SDK), Google Cloud
- [PyMySQL documentation](https://pymysql.readthedocs.io/en/latest/)

{{< signature "ks, ra, al, il" >}}
