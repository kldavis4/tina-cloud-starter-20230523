---
title: 'Automating Your Feature Testing With Selenium WebDriver'
slug: feature-testing-selenium-webdriver
author: nils-schuette
image: >-
  //archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e28f1b6f-f03e-457b-8ca8-96bfc14ca49c/07-adding-selenium-library.jpg
date: 2018-04-12T12:45:54+02:00
summary: >-
  What is Selenium and how can it help you? Well, what if you were told that you could basically automate any task in your browser as if a real person were to execute it? Yes, you read that right. It _is_ possible.
description: >-
  What is Selenium and how can it help you? Well, what if you were told that you could basically automate any task in your browser as if a real person were to execute it? Yes, you read that right. It _is_ possible.
categories:
  - Testing
  - Tools
  - WordPress
  - Frameworks
  - Testing
---
This article is for web developers who wish to spend less time testing the front end of their web applications but still want to be confident that every feature works fine. It will save you time by automating repetitive online tasks with Selenium WebDriver. You will find a step-by-step example for automating and testing the login function of WordPress, but you can also adapt the example for any other login form.

## What Is Selenium And How Can It Help You?

Selenium is a framework for the automated testing of web applications. Using Selenium, you can basically automate every task in your browser as if a real person were to execute the task. The interface used to send commands to the different browsers is called Selenium WebDriver. Implementations of this interface are available for every major browser, including Mozilla Firefox, Google Chrome and Internet Explorer. 

## Automating Your Feature Testing With Selenium WebDriver

Which type of web developer are you? Are you the disciplined type who tests all key features of your web application after each deployment. If so, you are probably annoyed by how much time this repetitive testing consumes. Or are you the type who just doesn’t bother with testing key features and always thinks, "I should test more, but I’d rather develop new stuff." If so, you probably only find bugs by chance or when your client or boss complains about them.

I have been working for a well-known online retailer in Germany for quite a while, and I always belonged to the second category: It was so exciting to think of new features for the online shop, and I didn’t like at all going over all of the previous features again after each new software deployment. So, the strategy was more or less to hope that all key features would work. 

{{% feature-panel %}}

One day, we had a serious drop in our conversion rate and started digging in our web analytics tools to find the source of this drop. It took quite a while before we found out that our checkout did not work properly since the previous software deployment.

This was the day when I started to do some research about automating our testing process of web applications, and I stumbled upon Selenium and its WebDriver. Selenium is basically a framework that allows you to automate web browsers. WebDriver is the name of the key interface that allows you to send commands to all major browsers (mobile and desktop) and work with them as a real user would. 

## Preparing The First Test With Selenium WebDriver

First, I was a little skeptical of whether Selenium would suit my needs because the framework is most commonly used in Java, and I am certainly not a Java expert. Later, I learned that being a Java expert is not necessary to take advantage of the power of the Selenium framework.

As a simple first test, I tested the login of one of my WordPress projects. Why WordPress? Just because using the WordPress login form is an example that everybody can follow more easily than if I were to refer to some custom web application. 

What do you need to start using Selenium WebDriver? Because I decided to use the most common implementation of Selenium in Java, I needed to set up my little Java environment. 

If you want to follow my example, you can use the Java environment of your choice. If you haven’t set one up yet, I suggest [installing Eclipse](https://www.eclipse.org/downloads/eclipse-packages/?show_instructions=TRUE) and making sure you are able to run a simple ["Hello world" script in Java](https://www.java-made-easy.com/java-hello-world.html).

Because I wanted to test the login in Chrome, I made sure that the Chrome browser was already installed on my machine. That’s all I did in preparation.

## Downloading The ChromeDriver

All major browsers provide their own implementation of the WebDriver interface. Because I wanted to test the WordPress login in Chrome, I needed to get the WebDriver implementation of Chrome: [ChromeDriver.](https://sites.google.com/a/chromium.org/chromedriver/downloads)

I extracted the ZIP archive and stored the executable file <code>chromedriver.exe</code> in a location that I could remember for later.

## Setting Up Our Selenium Project In Eclipse 

The steps I took in Eclipse are probably pretty basic to someone who works a lot with Java and Eclipse. But for those like me, who are not so familiar with this, I will go over the individual steps:

<ol>
	<li>Open Eclipse.</li>
	<li>Click the "New" icon.<br />
		<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/27a60e0f-79b5-4326-a731-ea25aa9314f5/01-new-java-project.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/27a60e0f-79b5-4326-a731-ea25aa9314f5/01-new-java-project.jpg" width="323" height="88" alt="Creating a new project in Eclipse" /></a><figcaption>Creating a new project in Eclipse</figcaption></figure>
	</li>
	<li>Choose the wizard to create a new "Java Project," and click “Next.”<br />
		<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5ad84e3d-b76c-405b-b477-ff1ddb32d939/02-new-java-project.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5ad84e3d-b76c-405b-b477-ff1ddb32d939/02-new-java-project.jpg" width="541" height="514" alt="Chosing the java-project wizard" /></a><figcaption>Choose the java-project wizard.</figcaption></figure>
	</li>
	<li>Give your project a name, and click "Finish."<br />
		<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/85bb5f73-4f57-4f0f-9835-ef259edb6d3e/03-new-java-project.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/85bb5f73-4f57-4f0f-9835-ef259edb6d3e/03-new-java-project.jpg" width="574" height="729" alt="Eclipse project wizard" /></a><figcaption>The eclipse project wizard</figcaption></figure>
	</li>
	<li>Now you should see your new Java project on the left side of the screen.<br />
		<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4bb325ba-172c-4dae-b54f-a2f4cff0ea46/04-new-java-project.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4bb325ba-172c-4dae-b54f-a2f4cff0ea46/04-new-java-project.jpg" width="324" height="85" alt="Java project successfully created" /></a><figcaption>We successfully created a project to run the Selenium WebDriver.</figcaption></figure>
	</li>
</ol>

## Adding The Selenium Library To Our Project

Now we have our Java project, but Selenium is still missing. So, next, we need to bring the Selenium framework into our Java project. Here are the steps I took:

<ol>
	<li>Download the <a href="https://www.seleniumhq.org/download/">latest version</a> of the Java Selenium library.<br/>
		<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bc225835-721b-4089-97d3-d038d97dff59/05-download-selenium.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bc225835-721b-4089-97d3-d038d97dff59/05-download-selenium.jpg" width="571" height="134" alt="Downloading the Selenium library" /></a><figcaption>Download the Selenium library.</figcaption></figure>
	</li>
	<li>Extract the archive, and store the folder in a place you can remember easily.</li>
	<li>Go back to Eclipse, and go to "Project" &rarr; “Properties.”<br />
		<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/20c0b2e2-037f-4d75-939e-3c5bc1dc40d1/06-adding-selenium-library.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/20c0b2e2-037f-4d75-939e-3c5bc1dc40d1/06-adding-selenium-library.jpg" width="228" height="248" alt="Eclipse Properties" /></a><figcaption>Go to properties to integrate the Selenium WebDriver in you project.</figcaption></figure>
	</li>
	<li>In the dialog, go to "Java Build Path" and then to register “Libraries.”</li>
	<li>Click on "Add External JARs."<br />
		<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e28f1b6f-f03e-457b-8ca8-96bfc14ca49c/07-adding-selenium-library.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e28f1b6f-f03e-457b-8ca8-96bfc14ca49c/07-adding-selenium-library.jpg" width="802" height="558" alt="Adding the Selenium lib to your Java build path." /></a><figcaption> Add the Selenium lib to your Java build path.</figcaption></figure>
	</li>
	<li>Navigate to the just downloaded folder with the Selenium library. Highlight all <code>.jar</code> files and click "Open."<br />
		<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e2d3f312-e05d-497e-baa3-f490bdb0e514/08-adding-selenium-library.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e2d3f312-e05d-497e-baa3-f490bdb0e514/08-adding-selenium-library.jpg" width="586" height="150" alt="Selecting the correct files of the Selenium lib." /></a><figcaption>Select all files of the lib to add to your project.</figcaption></figure>
	</li>
	<li>Repeat this for all <code>.jar</code> files in the subfolder <code>libs</code> as well.</li>
	<li>Eventually, you should see all <code>.jar</code> files in the libraries of your project:<br />
		<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a5d2290b-7eeb-45d3-ab97-078fc040f881/09-adding-selenium-library.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a5d2290b-7eeb-45d3-ab97-078fc040f881/09-adding-selenium-library.jpg" width="756" height="562" alt="Selenium WebDriver framework successfully integrated into your project" /></a><figcaption>The Selenium WebDriver framework has now been successfully integrated into your project!</figcaption></figure>
	</li>
</ol>

That’s it! Everything we’ve done until now is a one-time task. You could use this project now for all of your different tests, and you wouldn’t need to do the whole setup process for every test case again. Kind of neat, isn’t it?

## Creating Our Testing Class And Letting It Open the Chrome Browser

Now we have our Selenium project, but what next? To see whether it works at all, I wanted to try something really simple, like just opening my Chrome browser. 

To do this, I needed to create a new Java class from which I could execute my first test case. Into this executable class, I copied a few Java code lines, and believe it or not, it worked! Magically, the Chrome browser opened and, after a few seconds, closed all by itself.

Try it yourself:

<ol>
	<li>Click on the "New" button again (while you are in your new project’s folder).<br />
		<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ba998ff3-4dfe-45d5-8c72-ed1a7ffd0554/10-new-class.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ba998ff3-4dfe-45d5-8c72-ed1a7ffd0554/10-new-class.jpg" width="323" height="88" alt="New class in eclipse" /></a><figcaption>Create a new class to run the Selenium WebDriver.</figcaption></figure>
	</li>
	<li>Choose the "Class" wizard, and click “Next.”<br />
		<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b9e6a897-6bfe-40dd-a9f7-103435bc8ef7/11-new-class.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b9e6a897-6bfe-40dd-a9f7-103435bc8ef7/11-new-class.jpg" width="540" height="515" alt="New class wizard in eclipse" /></a><figcaption>Choose the Java class wizard to create a new class.</figcaption></figure>
	</li>
	<li>Name your class (for example, "RunTest"), and click “Finish.”<br />
		<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fd8acc1a-a9cb-4b81-924a-0aa692e76039/12-new-class.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fd8acc1a-a9cb-4b81-924a-0aa692e76039/12-new-class.jpg" width="551" height="656" alt="Eclipse Java Class wizard" /></a><figcaption>The eclipse Java Class wizard.</figcaption></figure>
	</li>
	<li>Replace all code in your new class with the following code. The only thing you need to change is the path to <code>chromedriver.exe</code> on your computer:<br />
<div class="break-out">

<pre><code class="language-bash">import org.openqa.selenium.WebDriver;
import org.openqa.selenium.chrome.ChromeDriver;

/**
 * @author Nils Schuette via frontendtest.org
 */
public class RunTest {
    static WebDriver webDriver;
    /**
     * @param args
     * @throws InterruptedException
     */
    public static void main(final String[] args) throws InterruptedException {
        // Telling the system where to find the chrome driver
        System.setProperty(
                "webdriver.chrome.driver",
                "C:/PATH/TO/chromedriver.exe");

        // Open the Chrome browser
        webDriver = new ChromeDriver();

        // Waiting a bit before closing
        Thread.sleep(7000);

        // Closing the browser and WebDriver
        webDriver.close();
        webDriver.quit();
    }
}
</code></pre></div></li>
<li>Save your file, and click on the play button to run your code.<br />
	<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/100de14d-8beb-48f7-b19c-f7a66ca4cb05/13-run-test.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/100de14d-8beb-48f7-b19c-f7a66ca4cb05/13-run-test.jpg" width="693" height="254" alt="Run Eclipse project" /></a><figcaption>Running your first Selenium WebDriver project.</figcaption></figure>
</li>
<li>If you have done everything correctly, the code should open a new instance of the Chrome browser and close it shortly thereafter.<br />
	<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bc7ed40e-dcdb-4c83-83f1-1d90e893eacb/14-open-chrome-browser.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bc7ed40e-dcdb-4c83-83f1-1d90e893eacb/14-open-chrome-browser.jpg" width="1207" height="780" alt="Chrome Browser blank window" /></a><figcaption>The Chrome Browser opens itself magically. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bc7ed40e-dcdb-4c83-83f1-1d90e893eacb/14-open-chrome-browser.jpg">Large preview</a>)</figcaption></figure>
</li>
</ol>

## Testing The WordPress Admin Login

Now I was optimistic that I could automate my first little feature test. I wanted the browser to navigate to one of my WordPress projects, login to the admin area and verify that the login was successful. So, what commands did I need to look up? 

1. Navigate to the login form,
2. Locate the input fields,
3. Type the username and password into the input fields,
4. Hit the login button,
5. Compare the current page’s headline to see if the login was successful.

Again, after I had done all the necessary updates to my code and clicked on the run button in Eclipse, my browser started to magically work itself through the WordPress login. I successfully ran my first automated website test!

If you want to try this yourself, replace all of the code of your Java class with the following. I will go through the code in detail afterwards. Before executing the code, you must replace four values with your own:

1. The location of your <code>chromedriver.exe</code> file (as above),

2. The URL of the WordPress admin account that you want to test,

3. The WordPress username,

4. The WordPress password.

Then, save and let it run again. It will open Chrome, navigate to the login of your WordPress website, login and check whether the <code>h1</code> headline of the current page is "Dashboard."

<div class="break-out">

<pre><code class="language-bash">import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.chrome.ChromeDriver;

/**
 * @author Nils Schuette via frontendtest.org
 */
public class RunTest {
	static WebDriver webDriver;
	/**
	 * @param args
	 * @throws InterruptedException
	 */
	public static void main(final String[] args) throws InterruptedException {
		// Telling the system where to find the chrome driver
		System.setProperty(
				"webdriver.chrome.driver",
				"C:/PATH/TO/chromedriver.exe");

		// Open the Chrome browser
		webDriver = new ChromeDriver();

		// Maximize the browser window
		webDriver.manage().window().maximize();

		if (testWordpresslogin()) {
			System.out.println("Test Wordpress Login: Passed");
		} else {
			System.out.println("Test Wordpress Login: Failed");

		}

		// Close the browser and WebDriver
		webDriver.close();
		webDriver.quit();
	}

	private static boolean testWordpresslogin() {
		try {
			// Open google.com
			webDriver.navigate().to("https://www.YOUR-SITE.org/wp-admin/");

			// Type in the username
			webDriver.findElement(By.id("user_login")).sendKeys("YOUR_USERNAME");

			// Type in the password
			webDriver.findElement(By.id("user_pass")).sendKeys("YOUR_PASSWORD");

			// Click the Submit button
			webDriver.findElement(By.id("wp-submit")).click();

			// Wait a little bit (7000 milliseconds)
			Thread.sleep(7000);

			// Check whether the h1 equals “Dashboard”
			if (webDriver.findElement(By.tagName("h1")).getText()
					.equals("Dashboard")) {
				return true;
			} else {
				return false;
			}

		// If anything goes wrong, return false.
		} catch (final Exception e) {
			System.out.println(e.getClass().toString());
			return false;
		}
	}
}
</code></pre></div>

If you have done everything correctly, your output in the Eclipse console should look something like this:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/25a166ee-672b-46ae-976b-055a78de2256/15-console-output.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/25a166ee-672b-46ae-976b-055a78de2256/15-console-output.jpg" width="829" height="174" alt="Eclipse console test result." /></a><figcaption>The Eclipse console states that our first test has passed. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/25a166ee-672b-46ae-976b-055a78de2256/15-console-output.jpg">Large preview</a>)</figcaption></figure>

## Understanding The Code

Because you are probably a web developer and have at least a basic understanding of other programming languages, I am sure you already grasp the basic idea of the code: We have created a separate method, <code>testWordpressLogin</code>, for the specific test case that is called from our main method. 

Depending on whether the method returns true or false, you will get an output in your console telling you whether this specific test passed or failed. 

This is not necessary, but this way you can easily add many more test cases to this class and still have readable code. 

Now, step by step, here is what happens in our little program:

<ol>
	<li>First, we tell our program where it can find the specific WebDriver for Chrome.<br />
		<div class="break-out">

<pre><code class="language-bash">System.setProperty("webdriver.chrome.driver","C:/PATH/TO/chromedriver.exe");</code></pre></div>
	</li>
	<li>We open the Chrome browser and maximize the browser window.<br />
		<div class="break-out">

<pre><code class="language-bash">webDriver = new ChromeDriver();
webDriver.manage().window().maximize();</code></pre></div>
</li>
<li>This is where we jump into our submethod and check whether it returns true or false.<br />
	<div class="break-out">

<pre><code class="language-bash">if (testWordpresslogin()) …</code></pre></div>
</li>
<li>The following part in our submethod might not be intuitive to understand:<br />The <code>try{…}catch{…}</code> blocks. If everything goes as expected, only the code in <code>try{…}</code> will be executed, but if anything goes wrong while executing <code>try{…}</code>, then the execution continuous in <code>catch{}</code>. Whenever you try to locate an element with <code>findElement</code> and the browser is not able to locate this element, it will throw an exception and execute the code in <code>catch{…}</code>. In my example, the test will be marked as "failed" whenever something goes wrong and the <code>catch{}</code> is executed.</li>
<li>In the submethod, we start by navigating to our WordPress admin area and locating the fields for the username and the password by looking for their IDs. Also, we type the given values in these fields.<br />
	<div class="break-out">

<pre><code class="language-bash">webDriver.navigate().to("https://www.YOUR-SITE.org/wp-admin/");
webDriver.findElement(By.id("user_login")).sendKeys("YOUR_USERNAME");
webDriver.findElement(By.id("user_pass")).sendKeys("YOUR_PASSWORD");</code></pre></div>
<br />
<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9b01760d-dee9-42b8-9178-6f7c10a80549/16-wordpress-admin-login.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9b01760d-dee9-42b8-9178-6f7c10a80549/16-wordpress-admin-login.jpg" width="460" height="454" alt="Wordpress login form" /></a><figcaption>Selenium fills out our login form</figcaption></figure>
</li>
<li>After filling in the login form, we locate the submit button by its ID and click it.<br />
	<div class="break-out">

<pre><code class="language-bash">webDriver.findElement(By.id("wp-submit")).click();</code></pre></div>
</li>
<li>In order to follow the test visually, I include a 7-second pause here (7000 milliseconds = 7 seconds).<br />
	<div class="break-out">

<pre><code class="language-bash">Thread.sleep(7000);</code></pre></div>
</li>
<li>If the login is successful, the <code>h1</code> headline of the current page should now be "Dashboard," referring to the WordPress admin area. Because the <code>h1</code> headline should exist only once on every page, I have used the tag name here to locate the element. In most other cases, the tag name is not a good locator because an HTML tag name is rarely unique on a web page. After locating the <code>h1</code>, we extract the text of the element with <code>getText()</code> and check whether it is equal to the string “Dashboard.” If the login is not successful, we would not find “Dashboard” as the current <code>h1</code>. Therefore, I’ve decided to use the <code>h1</code> to check whether the login is successful.<br />
	<div class="break-out">

<pre><code class="language-javascript">if (webDriver.findElement(By.tagName("h1")).getText().equals("Dashboard")) 
	{
		return true;
	} else {
		return false;
	}
</code></pre></div>
<br />
<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f8a5943f-3f76-4387-8805-d2f5f81dc260/17-wordpress-dashboard.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f8a5943f-3f76-4387-8805-d2f5f81dc260/17-wordpress-dashboard.jpg" width="1096" height="346" alt="Wordpress Dashboard" /></a><figcaption>Letting the WebDriver check, whether we have arrived on the Dashboard: Test passed! (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f8a5943f-3f76-4387-8805-d2f5f81dc260/17-wordpress-dashboard.jpg">Large preview</a>)</figcaption></figure>
</li>
<li>If anything has gone wrong in the previous part of the submethod, the program would have jumped directly to the following part. The <code>catch</code> block will print the type of exception that happened to the console and afterwards return <code>false</code> to the main method.<br />
	<div class="break-out">

<pre><code class="language-javascript">catch (final Exception e) {
			System.out.println(e.getClass().toString());
			return false;
		}</code></pre></div>
</li>
</ol>

## Adapting The Test Case

This is where it gets interesting if you want to adapt and add test cases of your own. You can see that we always call methods of the <code>webDriver</code> object to do something with the Chrome browser.

First, we maximize the window:

<div class="break-out">

<pre><code class="language-bash">webDriver.manage().window().maximize();</code></pre></div>

Then, in a separate method, we navigate to our WordPress admin area:

<div class="break-out">

<pre><code class="language-bash">webDriver.navigate().to("https://www.YOUR-SITE.org/wp-admin/");</code></pre></div>

There are other methods of the <code>webDriver</code> object we can use. Besides the two above, you will probably use this one a lot:

<div class="break-out">

<pre><code class="language-bash">webDriver.findElement(By. …)</code></pre></div>

The <code>findElement</code> method helps us find different elements in the DOM. There are different options to find elements:

- `By.id`
- `By.cssSelector`
- `By.className`
- `By.linkText`
- `By.name`
- `By.xpath`

If possible, I recommend using <code>By.id</code> because the ID of an element should always be unique (unlike, for example, the <code>className</code>), and it is usually not affected if the structure of your DOM changes (unlike, say, the <code>xPath</code>).

**Note**: *You can read more about the different options for locating elements with WebDriver over [here](https://www.seleniumhq.org/docs/03_webdriver.jsp#locating-ui-elements-webelements).*

As soon as you get ahold of an element using the <code>findElement</code> method, you can call the different available methods of the element. The most common ones are <code>sendKeys</code>, <code>click</code> and <code>getText</code>.

We’re using <code>sendKeys</code> to fill in the login form:

<div class="break-out">

<pre><code class="language-bash">webDriver.findElement(By.id("user_login")).sendKeys("YOUR_USERNAME");</code></pre></div>

We have used <code>click</code> to submit the login form by clicking on the submit button:

<div class="break-out">

<pre><code class="language-bash">webDriver.findElement(By.id("wp-submit")).click();</code></pre></div>

And <code>getText</code> has been used to check what text is in the <code>h1</code> after the submit button is clicked:

<div class="break-out">

<pre><code class="language-bash">webDriver.findElement(By.tagName("h1")).getText()</code></pre></div>

**Note**: *Be sure to check out [all the available methods that you can use](https://seleniumhq.github.io/selenium/docs/api/java/org/openqa/selenium/WebElement.html) with an element.*

## Conclusion

Ever since I discovered the power of Selenium WebDriver, my life as a web developer has changed. I simply love it. The deeper I dive into the framework, the more possibilities I discover &mdash; running one test simultaneously in Chrome, Internet Explorer and Firefox or even on my smartphone, or taking screenshots automatically of different pages and comparing them. Today, I use Selenium WebDriver not only for testing purposes, but also to [automate repetitive tasks on the web](https://www.seguetech.com/use-automation-to-perform-repetitive-data-entry-tasks/). Whenever I see an opportunity to automate my work on the web, I simply copy my initial WebDriver project and adapt it to the next task. 

If you think that Selenium WebDriver is for you, I recommend looking at [Selenium’s documentation](https://www.seleniumhq.org/docs/) to find out about all of the possibilities of Selenium (such as [running tasks simultaneously](https://www.seleniumhq.org/docs/07_selenium_grid.jsp) on several (mobile) devices with Selenium Grid). 

I look forward to hearing whether you find WebDriver as useful as I do!

{{< signature "rb, ra, al, il" >}}

