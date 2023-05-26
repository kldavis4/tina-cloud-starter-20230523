---
title: 'From Idea To Reality: Designing An App With Sketch And Xcode'
slug: designing-app-idea-sketch-xcode
author: craigclayton
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/594418e5-f524-4693-9715-9f862a6e619a/design2xcode03a-800w-opt.png
date: 2017-11-29T13:12:42.413Z
summary: >-
  Have you already tried to bring a design into Xcode without any code? Well, now is your chance. In this article, Craig explains how you can bring your app idea to life using Sketch and Xcode.
description: >-
  Have you already tried to bring a design into Xcode without any code? Well, now is your chance. In this article, Craig explains how you can bring your app idea to life using Sketch and Xcode.
categories:
  - Sketch
  - Apps
  - Tutorials
---
<p>Everyone has an idea for a mobile app, from your mom to the guy you met in line at the grocery store. You might even be one of those people, if you are reading this tutorial. Building your own app really gives you the ability to create anything you can imagine. For some people, the idea is the easy part; when it comes to making it a reality, they have no clue where to start.</p>

<p>In this tutorial, we are going to look at one page of an existing app and learn how to get the design into Xcode. The design for this app was done using an app called Sketch. Sketch allows you to design anything from websites to mobile apps. It is my preference for designing mobile apps.</p>

<p>When you are building an app, do not jump directly into Xcode. You’ll want to work on the app’s look and feel before doing any code. This will enable you to figure out exactly what your app will do before you start coding. <strong>Fixing a design is easier than fixing code</strong>. Once you are done with the design, you will then match it in Xcode. Here are a few other options that you might want to look at if you are interested in designing an app:</p>

<ul>

<li><a href="https://www.designer.io">Gravit</a>: free</li>

{{% feature-panel %}}

<li><a href="https://affinity.serif.com/en-us/designer/">Affinity Designer</a>: $49</li>

<li><a href="https://sketchapp.com">Sketch</a>: $99 (free trial)</li>

</ul>

<div class="c-felix-the-cat"><h4>Moving From Photoshop And Illustrator To Sketch</h4><p>Unlike Photoshop, Sketch was made for UI design right from the start; UI wasn’t an afterthought. If you’re a UI designer and are still using mostly Photoshop or Illustrator, it may be time to consider using Sketch instead.</p><p><a href="https://www.smashingmagazine.com/2017/04/photoshop-illustrator-sketch-ui/" class="btn btn--small btn--green">Jump to a related article&nbsp;↬</a></p></div>

## Exploring The Design

<p>One of the first things I like to do when I see an app is to review the design and see if I can figure out how they built it. Let’s first look at the design of this page:</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/31cced03-184c-4a74-ab80-a520fd5ca358/appdemo.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/31cced03-184c-4a74-ab80-a520fd5ca358/appdemo.gif" width="396" height="720" alt="appdemo" /></a></figure>

<p>As you can see, this is a product detail page, which might be similar to others you have seen in e-commerce apps. What I most like about this product detail page, for learning purposes, is that it contains a lot of different user interface (UI) components. Designing a UI like this enables you to explore Xcode in a meaningful way and to tackle many of the most common components you would encounter when designing an app. The following diagram breaks down the different UI components of our design page:</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f7fde89d-a5b0-4571-847e-c1691a6231dc/design2xcode03-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/650ea539-68d8-4b43-ba81-ceb87598e369/design2xcode03-800w-opt.png" width="800" height="1562" alt="different UI components" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f7fde89d-a5b0-4571-847e-c1691a6231dc/design2xcode03-large-opt.png">View large version</a>)</figcaption></figure>

Let’s better understand each of these elements.</p>

### UIImageView

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/33e518f1-74b8-4a65-9f19-5eae8329f84f/design2xcode03a-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/594418e5-f524-4693-9715-9f862a6e619a/design2xcode03a-800w-opt.png" height="442" width="800" alt="UIImageView" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/33e518f1-74b8-4a65-9f19-5eae8329f84f/design2xcode03a-large-opt.png">View large version</a>)</figcaption></figure>

A <code>UIImageView</code> is a component that allows you to show images.</p>

### UILabel

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9912f1f7-2a79-4034-a89f-be97603c7269/design2xcode03b-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ef2d8522-c95b-43bf-8468-1e8c1bc15463/design2xcode03b-800w-opt.png" alt="UIlabel" height="83" width="800" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9912f1f7-2a79-4034-a89f-be97603c7269/design2xcode03b-large-opt.png">View large version</a>)</figcaption></figure>

<p>A <code>UILabel</code> is typically used to display text on a single line, although you can set it up to display multiple lines of text. This component is not interactive.</p>

### UIStackView

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ff537aaf-b8ab-449a-8353-0dcd6b491a15/design2xcode03c-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6257a588-82eb-48f7-8625-7b3452c8f438/design2xcode03c-800w-opt.png" height="138" width="800" alt="UIStackView" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ff537aaf-b8ab-449a-8353-0dcd6b491a15/design2xcode03c-large-opt.png">View large version</a>)</figcaption></figure>

A <code>UIStackView</code> allows you to stack components vertically and horizontally. For example, if you wanted to display three buttons spaced 10 pixels apart, you could use a <code>UIStackView</code> to make it easier.</p>

### UITextView

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ec37b71f-a373-4506-bc53-17e47fddbd63/design2xcode03d-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/23374601-8f63-4c71-a84f-145276341f2f/design2xcode03d-800w-opt.png" alt="UITextView" width="800" height="429" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ec37b71f-a373-4506-bc53-17e47fddbd63/design2xcode03d-large-opt.png">View large version</a>)</figcaption></figure>

A <code>UITextView</code> is typically used to display multiple lines of text. Users can interact with this component by editing the text. If we simply wanted to display text, with no ability to edit, we would normally use a <code>UILabel</code>. However, for this tutorial, I want to introduce you to both the <code>UILabel</code> and <code>UITextView</code> components.</p>

### UIScrollView

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0df154fe-ed65-4376-8746-4176b5437605/design2xcode03e-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/747f577f-7fbe-4626-8ae6-bbd09d745000/design2xcode03e-800w-opt.png" alt="UIScrollView" width="800" height="272" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0df154fe-ed65-4376-8746-4176b5437605/design2xcode03e-large-opt.png">View large version</a>)</figcaption></figure>

A <code>UIScrollView</code> allows you to add multiple components that scroll either horizontally or vertically.</p>

## Designing In Xcode

<p>Before we begin designing our app page in Xcode, I want to introduce you to two important aspects of Xcode, storyboards and table views. Let’s start with storyboards.</p>

## What Are Storyboards, And Why Do We Use Them?

<p>A storyboard is a tool in Xcode that enables us to set up our visual elements. These elements, our UI components, can be dragged and dropped into place without the need for code. If you are a visual person, you will most likely feel very comfortable with storyboards.</p>

<p>In addition to not having to code, I love storyboarding instead of coding all of the elements because it makes it easy for another person to understand what is going on in the project and to step in if need be. Storyboarding also makes it easier for you to step away from a project for a period of time and then come back to it. If everything is in the storyboard, it will be relatively easy to figure out what you did and where you left off, as well as to make any visual changes you desire. Plenty of people prefer coding to storyboarding, but in this tutorial I am going to show you the benefits of storyboards.</p>

<p>To get familiar with storyboarding, let’s review the five basic areas of Xcode.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/debf7a18-1b0a-436b-8a45-50ec780cc4c9/design2xcode03f-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d5999aa4-d43a-41bf-8b9d-98bd11b7a3a4/design2xcode03f-800w-opt.png" alt="Xcode" width="800" height="430" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/debf7a18-1b0a-436b-8a45-50ec780cc4c9/design2xcode03f-large-opt.png">View large version</a>)</figcaption></figure>

### Navigation Area

<p>The navigation area shows all of your files (such as <code>Main.storyboard</code>, where you design your visual elements) and <code>Assets.xcassets</code> (the blue folder), which holds your app’s icon and images.</p>

### Editor Area

<p>The editor area is where you will work. Both storyboard and Swift files open in this area.</p>

### Toolbar

<p>On the left side of the toolbar, you will find controls to launch your app using a simulator. On the far right of the toolbar, you will find icons that allow you to toggle different panels to be either shown or hidden.</p>

### Utility Area

<p>When inside of a storyboard file, you will use the utility area to make changes to UI components. This area will change depending on the screen with which you are currently interacting.</p>

### Debug Area

<p>The debug area is very useful when you are coding. It shows issues with your code that you need to address. In this tutorial, we will not be using this area because we will not be coding, focusing instead on storyboarding.</p>

<p>Now that you are familiar with storyboards, let’s discuss table views.</p>

## What Is A Table View?

<p>As you can see above, our page is one in which the user scrolls down to view more information. One of the great features of iOS is that you can use a table view to scroll long pages without having to code anything. A table view is a way to list data in one column that can be vertically scrolled. A table view can have sections, and each section can have a header. There are two types of table views: dynamic and static.</p>

<p>Dynamic table views use code, and they typically have variable numbers of rows and/or sections based on some data. Dynamic table views are great for mailing and contact lists, which can change over time.</p>

<p>Static table views do not use code and instead are set up using storyboards in Xcode. They are not dynamic, and they have a finite number of rows or sections based on certain data. Static table views are good to use for things such as forms and detail pages that will not change.</p>

<p>For the product detail page in this tutorial, we will use static table views, which give us the flexibility to have complex layouts without having to write a lot of code. This solution will not work for every situation, but it is a good place to start.</p>

### Setting Up the Basic Structure

<p>Let’s set up the bare bones of our basic structure; then, we can start entering the details of our page. I have already created a starter project for you, where you will find all of the assets needed to complete this tutorial. <a href="https://smashingmagazine.com/provide//DesignToXcode.zip">Download the files</a>, and then open the file named <code>DesignToXcode.xcodeproj</code> in the file inspector in the navigation area:</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d6075c83-ba7a-46ff-b2ec-0ebf3ea27409/design2xcode28-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/852498f9-631d-4876-85af-0bedb8d25e55/design2xcode28-800w-opt.png" alt="DesignToXcode" width="800" height="430" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d6075c83-ba7a-46ff-b2ec-0ebf3ea27409/design2xcode28-large-opt.png">View large version</a>)</figcaption></figure>

Next, select the <code>Main.storyboard</code> file. You should see the following:</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/40f6a73a-b5ba-40dc-8295-a2a425647c7c/design2xcode04a-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fabe4c15-f2e1-4f73-b9b7-5fa04eeaf1a7/design2xcode04a-800w-opt.png" alt="Main.storyboard file" width="800" height="1118" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/40f6a73a-b5ba-40dc-8295-a2a425647c7c/design2xcode04a-large-opt.png">View large version</a>)</figcaption></figure>

As the image above shows, our storyboard contains a single view controller on the scene. Nothing else has been created, because we will create the rest together. This view controller is where we will add the UI components that we discussed.</p>

<p>Looking at our page design, we need to add a navigation bar at the top, which will automatically add a label and two placeholders for buttons. We will eventually update the label title to <code>CONVERSE CHUCK TAYLORS</code> and leave the button placeholders alone.</p>

<p>To add the navigation bar, we first have to add a navigation controller. So, select the view controller by choosing “View Controller” under “View Controller Scene” in the outline view or by clicking on the leftmost icon of the view controller in the scene. The outline view is located as shown in the following image:</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/15b73352-1b29-424a-be49-3219813ab9f9/design2xcode04-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f02ff579-7a11-46af-9c8b-9b66db1bb16b/design2xcode04-800w-opt.png" alt="Adding A Navigation Controller" width="800" height="779" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/15b73352-1b29-424a-be49-3219813ab9f9/design2xcode04-large-opt.png">View large version</a>)</figcaption></figure>

Then, in your Apple toolbar, go to “Editor” &rarr; “Embed In” &rarr; “Navigation Controller.” You should now have the following in your scene:</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/927e39b8-cf5f-4325-8ab8-bbea066300f1/design2xcode05-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/667858ba-e68f-4d56-ba4f-3d8b9d82e8ae/design2xcode05-800w-opt.png" alt="Embedding Navigation Controller" width="800" height="685" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/927e39b8-cf5f-4325-8ab8-bbea066300f1/design2xcode05-large-opt.png">View large version</a>)</figcaption></figure>

Next, let’s update the title in our view controller to read <code>CONVERSE CHUCK TAYLORS</code>. Click on “Navigation Item” under the view controller. In the utility area, select the “Attributes Inspector:”</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9238e509-7c0a-4252-a21b-4a48064ef1bb/design2xcode05a-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9238e509-7c0a-4252-a21b-4a48064ef1bb/design2xcode05a-opt.png" alt="Attributes Inspector" width="633" height="482" /></a></figure>

<p>Type <code>CONVERSE CHUCK TAYLORS</code> in the title area. You will see the new title in the view controller in the scene.</p>

### Adding “Add to Cart” Button

<p>Next, we need to address one of the major features of this product page. Looking at the design, you will notice that the “Add to Cart” button is pinned to the bottom and that the content scrolls underneath the button. We can create this design feature in a few different ways, but I find using a container view to be easiest. A container view is just a container that sits in our controller and allows us to use another view controller of our choice. For our design, the container view will consist of our static table view. Because a static table view cannot be dragged into a view controller with other elements, the container view will provide a separate container within which to set up the table view. In addition, the container view allows us to pin the “Add to Cart” button to the bottom, as the content is being scrolled.</p>

<p>The two main elements of the “Add to Cart” button are an image (the background of the button) and a button. Whenever I can, when items are grouped together, I put them into a <code>UIView</code>, which I treat as a container.</p>

<p>Let’s start setting up our “Add to Cart” button by adding the container. In the utility area, open the “Object” library, and then type <code>view</code> in the filter bar:</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d9f56c80-f6fe-4cdc-af66-b4432c5989a4/design2xcode05b-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0c21504f-31d0-40ee-b0da-5779839ec2f6/design2xcode05b-800w-opt.png" alt="object-library-filter-area" width="800" height="703" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d9f56c80-f6fe-4cdc-af66-b4432c5989a4/design2xcode05b-large-opt.png">View large version</a>)</figcaption></figure>

Drag the view into our view controller, and then click on the size inspector in the utility area:</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e0d4910a-655d-4777-997c-6899d2a7a9fe/design2xcode05c-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e0d4910a-655d-4777-997c-6899d2a7a9fe/design2xcode05c-opt.png" alt="Size Inspector" width="633" height="482" /></a></figure>

<p>Set the following values in the size inspector:</p>

<ul>

<li>X: 0</li>

<li>Y: 607</li>

<li>Width: 375</li>

<li>Height: 60</li>

</ul>

<p>Now that our container is in place, we need to add our image.</p>

<p>In the object library, type <code>image</code> in the filter area. Drag an image view into the view we just added. In the size inspector, add the following values:</p>

<ul>

<li>X: 0</li>

<li>Y: 0</li>

<li>Width: 375</li>

<li>Height: 60</li>

</ul>

<p>In the attributes inspector, set “Image” to <code>btn-bg</code>.</p>

<p>Finally, let’s add our button. Type <code>button</code> in the filter area, and drag the button into the same view. In the size inspector, add the following values:</p>

<ul>

<li>X: 8</li>

<li>Y: 8</li>

<li>Width: 359</li>

<li>Height: 44</li>

</ul>

<p>In the attributes inspector, add the following values:</p>

<ul>

<li>Type: System</li>

<li>Title: Change <code>Button</code> to “ADD TO CART” in the text field above “Font.”</li>

<li>Font: Click the font icon, then “Custom,” and choose Avenir Next Condensed, Bold 24.0</li>

<li>Text color: White</li>

<li>Background: <code>addtocart-bg</code></li>

</ul>

<p>Now that we have set up the button, our storyboard should look like the following:</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fc956537-c813-4321-b9a8-17547461253e/design2xcode06-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/766e059c-7c0b-4745-8ff7-e9e8bdc7dfa6/design2xcode06-800w-opt.png" alt="Navigation Controller" width="800" height="585" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fc956537-c813-4321-b9a8-17547461253e/design2xcode06-large-opt.png">View large version</a>)</figcaption></figure>

We now need to add some auto layout for our elements. Auto layout is a tool used to constrain components to the view. For example, you would use auto layout if you wanted a label to be pinned 10 pixels from the top of the view. You also would use auto layout to make sure that the label is vertically centered inside of your view. For our purposes, we will use auto layout to pin our “Add to Cart” button to the bottom of our view so that our content scrolls under it.</p>

<p>Let’s get started on applying auto layout to our “Add to Cart” button. First, select the view we recently added (i.e. our container), and click on the pin icon:</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2bac5b92-b1c6-4da7-b945-05c4136cea5f/design2xcode06b-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dc049eab-6b2c-4fe3-bce5-5bba9ded1877/design2xcode06b-800w-opt.png" alt="Select Pin Icon" width="800" height="530" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2bac5b92-b1c6-4da7-b945-05c4136cea5f/design2xcode06b-large-opt.png">View large version</a>)</figcaption></figure>

With the pin icon selected, enter the following values:</p>

<ul>

<li>Left: 0</li>

<li>Right: 0</li>

<li>Bottom: 0</li>

<li>Height: 60 (make sure box is checked)</li>

</ul>

<p>You can enter the left, right and bottom values just by clicking on the red barbells if their values are already at 0. After entering those values, click “Add 4 Constraints”:</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/35747602-8385-4483-ba29-c27635cee2aa/design2xcode07-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/598b09e8-67e8-4c40-a158-b68b26ec1737/design2xcode07-800w-opt.png" alt="Add To Cart" width="800" height="744" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/35747602-8385-4483-ba29-c27635cee2aa/design2xcode07-large-opt.png">View large version</a>)</figcaption></figure>

Now, our elements will always be pinned to the bottom of the device, with a height of 60, regardless of how tall our device is.</p>

<p>Next, we want to ensure that, no matter the size of the view, the background will fill the entire area. Therefore, select the image we are using for the background, click the pin icon, and then enter <code>0</code> for the top, left, right and bottom constraints. After entering those values, click “Add 4 Constraints”:</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/02d8b1b8-f27f-470d-8177-32f5e91a390c/design2xcode08-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/64012e24-95b0-4d6c-b300-3fc4fb18f7a7/design2xcode08-800w-opt.png" alt="Adding New Constraints" width="800" height="744" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/02d8b1b8-f27f-470d-8177-32f5e91a390c/design2xcode08-large-opt.png">View large version</a>)</figcaption></figure>

We also need to apply auto layout to our button. Select the button, click the pin icon, and then enter <code>8</code> for the left, right, top and bottom constraints. After entering those values, click “Add 4 Constraints”:</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/27008ff0-a1d1-4059-a5ae-880a4cce08ed/design2xcode09-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/02373ce5-409c-4c13-b427-372ac29cfb1d/design2xcode09-800w-opt.png" alt="Add 4 Constraints" width="800" height="744" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/27008ff0-a1d1-4059-a5ae-880a4cce08ed/design2xcode09-large-opt.png">View large version</a>)</figcaption></figure>

The constraints we just added will make sure that our button is always 8 pixels from the left, right, top and bottom of the view.</p>

<p>Let’s see how our application of auto layout works across different devices. Rather than building and running our project for each device, we can preview how our “Add to Cart” button looks across devices quite quickly. In the top right of your Xcode screen (above the utility area), select the “Assistant Editor” button, which will split the screen:</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5ac75ae5-05df-4bd7-b91c-df3e6e1c472d/design2xcode09b-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5ac75ae5-05df-4bd7-b91c-df3e6e1c472d/design2xcode09b-opt.png" alt="Assistant Editor button" width="148" height="130" /></a></figure>

<p>Then, in the menu at the top of the new screen, select “Preview(1)”:</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5cba4b9d-c2e7-4310-bbef-050cb458aefb/design2xcode11.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5cba4b9d-c2e7-4310-bbef-050cb458aefb/design2xcode11.gif" width="800" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5cba4b9d-c2e7-4310-bbef-050cb458aefb/design2xcode11.gif">View large version</a>)</figcaption></figure>

Once you select “Preview,” if you scroll to the bottom of the assistant editor screen, you will see the “Add to Cart” button pinned to the bottom of the iPhone 7 screen. Next, select and delete the iPhone 7 screen image in order to have an empty screen. Then, in the bottom-left corner, click the “+” button:</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d98a585e-4e9a-4501-b320-3488a60af439/design2xcode13-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/43bbef75-24f9-4b31-a594-b8e083a91f01/design2xcode13-800w-opt.png" alt="Assistant Editor" width="800" height="369" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d98a585e-4e9a-4501-b320-3488a60af439/design2xcode13-large-opt.png">View large version</a>)</figcaption></figure>

In the menu that appears, select the “iPhone SE.” Then, open this menu again and add the “iPhone 7 Plus” as well as the “iPad Pro 9.7&Prime; | Full Screen.” When you are done, you will see the following:</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/53b23012-430f-4789-a916-88e60a02179b/design2xcode14-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4e76fed0-6957-4843-bd58-23e7075498e5/design2xcode14-800w-opt.png" alt="different resolutions" width="800" height="471" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/53b23012-430f-4789-a916-88e60a02179b/design2xcode14-large-opt.png">View large version</a>)</figcaption></figure>

Notice that auto layout works exactly as we expected. Our “Add to Cart” button has expanded to the full width of the screen and is pinned to the bottom. Feel free to look at other devices and orientations. When you are done, exit the assistant editor and return to the standard editor.</p>

### Adding a Table View

<p>Let’s now add a table view to our design. In the object library, type <code>container</code> in the filter area. Drag a container view into the view, and in the size inspector add the following values:</p>

<ul>

<li>X: 0</li>

<li>Y: 0</li>

<li>Width: 375</li>

<li>Height: 607</li>

</ul>

<p>When we added our container view, you would have noticed that it created a view controller. Because we need a static table view, we will delete the view controller that was just created for us and replace it with a table view controller. Therefore, select the view controller that was created for us and hit “Delete.” Then, in the object library, type <code>table view</code> in the filter area. Drag a table view controller onto the scene. Then, from the container view that we just created, hold the <code>Control</code> button and drag to the table view controller. Select “Embed” on the screen that pops up:</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/05c53bb1-bb99-4c31-80b2-97b74d39403c/design2xcode15-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/05c53bb1-bb99-4c31-80b2-97b74d39403c/design2xcode15-opt.png" alt="Container view to table view controller" width="402" height="388" /></a></figure>

<p>You have now connected the container view to the table view controller. Next, select the “Table View” in the table view controller, and in the attributes inspector change the “Content” from “Dynamic Prototypes” to “Static Cells.” Three new cells should now be at the top of your table view controller:</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cd812d9d-5c67-46e6-bbfd-a1a2f1ee758b/design2xcode16-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0b4872d7-8218-4c28-8330-cbbd840bc615/design2xcode16-800w-opt.png" alt="" width="800" height="639" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cd812d9d-5c67-46e6-bbfd-a1a2f1ee758b/design2xcode16-large-opt.png">View large version</a>)</figcaption></figure>

However, we need a total of five cells for our product detail page. Let’s see these five cells delineated in our design:</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/16f2d6d6-5603-428d-a3f0-7574c471c655/design2xcode17-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/12e7bd2c-f1aa-40b9-8dd7-cd9fa69420a4/design2xcode17-800w-opt.png" alt="" width="800" height="1911" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/16f2d6d6-5603-428d-a3f0-7574c471c655/design2xcode17-large-opt.png">View large version</a>)</figcaption></figure>

As you can see, each of the five cells has different elements that we will need to add in order to create this product page. In order to get the desired layout and functionality, we need to update a few things.</p>

<p>First, in the outline view, select “Table View Section.” Then, in the attributes inspector, update “Rows” to <code>5</code>. Select each cell, and in the size inspector update each cell row’s height to the following values:</p>

<ul>

<li>Cell 1: 540</li>

<li>Cell 2: 290</li>

<li>Cells 3 and 4: leave as the default</li>

<li>Cell 5: 235</li>

</ul>

<p>When you are done, hover your mouse over the table view in the scene, and then swipe up and down to scroll through the table view:</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/300cd911-e8d2-46d9-98eb-2b36f32b5c53/design2xcode17b.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/300cd911-e8d2-46d9-98eb-2b36f32b5c53/design2xcode17b.gif" width="800" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/300cd911-e8d2-46d9-98eb-2b36f32b5c53/design2xcode17b.gif">View large version</a>)</figcaption></figure>

Select each table view cell, and in the attributes inspector update “Selection” from “Default” to “None.” Table views, by default, allow the user to select an item such as a cell. Because we do not need the behavior of cell selection, we have now removed this default.</p>

<p>Finally, we need to add auto layout to the container view that we added. Select the container view, click the pin icon, and then enter <code>0</code> for the top, left, right and bottom constraints. After entering those values, click “Add 4 Constraints”:</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cb419ab0-fe24-47f9-b259-dd6e94e42374/design2xcode18-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5da66f87-19e2-4bb0-9ff9-73ea922873b4/design2xcode18-800w-opt.png" alt="" width="800" height="744" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cb419ab0-fe24-47f9-b259-dd6e94e42374/design2xcode18-large-opt.png">View large version</a>)</figcaption></figure>

Let’s build and run the project by hitting the play button (or press <code>Command + R</code>). You should see our static table view, as well as have the behavior we want, which is the table view scrolling under our “Add to Cart” button:</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/322bac00-d9a3-484e-9414-308ae49e1c7d/design2xcode18b.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/322bac00-d9a3-484e-9414-308ae49e1c7d/design2xcode18b.gif" width="800" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/322bac00-d9a3-484e-9414-308ae49e1c7d/design2xcode18b.gif">View large version</a>)</figcaption></figure>

Now that our basic structure is established, it is time to start building our product page to make it look like the design we reviewed at the beginning of this tutorial.</p>

## Updating Our Cells

<p>We will work with one cell at a time in order to add all of the elements we need and position them in the cell, and then we’ll add auto layout to ensure that the elements will work with any device’s screen.</p>

### Cell One

<p>In our first cell, we need two labels to display the product’s name and price. In addition, we need five images, four as product thumbnails and one for the product’s large image.</p>

<p>To begin, type <code>label</code> in the filter area of the object library, and drag two <code>UILabels</code> into the table view cell. Then, type <code>image</code> in the filter area, and drag five <code>UIImageViews</code> into the table view cell. We need to update each of these element’s size and position to the following.</p>

<p><strong>UILabel 1</strong></p>

<p>Size inspector:</p>

<ul>

<li>X: 15</li>

<li>Y: 308</li>

<li>Width: 345</li>

<li>Height: 28</li>

</ul>

<p>Attributes inspector:</p>

<ul>

<li>Text: plain</li>

<li>Under text: change “Label” to “CONVERSE CHUCK TAYLOR ALL STAR HIGH TOP”</li>

<li>Color: light gray</li>

<li>Font: Click font icon, then “Custom,” and choose Avenir Next Condensed, Medium 20.0</li>

</ul>

<p><strong>UILabel 2</strong></p>

<p>Size inspector:</p>

<ul>

<li>X: 15</li>

<li>Y: 337</li>

<li>Width: 54</li>

<li>Height: 28</li>

</ul>

<p>Attributes inspector:</p>

<ul>

<li>Text: plain</li>

<li>Under text: change “Label” to <code>$55</code></li>

<li>Color: black</li>

<li>Font: Avenir Next Condensed, Bold 20.0</li>

</ul>

<p><strong>UIImage 1</strong></p>

<p>Size inspector:</p>

<ul>

<li>X: 0</li>

<li>Y: 0</li>

<li>Width: 375</li>

<li>Height: 300</li>

</ul>

<p>Attributes inspector:</p>

<ul>

<li>Image: <code>red-chucks</code></li>

</ul>

<p><strong>UIImage 2</strong></p>

<p>Size inspector:</p>

<ul>

<li>X: 15</li>

<li>Y: 474</li>

<li>Width: 77</li>

<li>Height: 50</li>

</ul>

<p>Attributes inspector:</p>

<ul>

<li>Image: <code>red-chuck-thumbs</code></li>

</ul>

<p><strong>UIImage 3</strong></p>

<p>Size inspector:</p>

<ul>

<li>X: 100</li>

<li>Y: 474</li>

<li>Width: 77</li>

<li>Height: 50</li>

</ul>

<p>Attributes inspector:</p>

<ul>

<li>Image: <code>pink-chuck-thumbs</code></li>

</ul>

<p><strong>UIImage 4</strong></p>

<p>Size inspector:</p>

<ul>

<li>X: 185</li>

<li>Y: 474</li>

<li>Width: 77</li>

<li>Height: 50</li>

</ul>

<p>Attributes inspector:</p>

<ul>

<li>Image: <code>yellow-chuck-thumbs</code></li>

</ul>

<p><strong>UIImage 5</strong></p>

<p>Size inspector:</p>

<ul>

<li>X: 270</li>

<li>Y: 474</li>

<li>Width: 77</li>

<li>Height: 50</li>

</ul>

<p>Attributes inspector:</p>

<ul>

<li>Image: <code>blue-chuck-thumbs</code></li>

</ul>

<p>After adding all of these elements and updating all of their attributes, you should see the following in your storyboard scene:</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/be725093-6546-4386-8af9-4e7150112f42/design2xcode19-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/be725093-6546-4386-8af9-4e7150112f42/design2xcode19-opt.png" alt="" width="754" height="1280" /></a></figure>

<p>The only remaining components we need to add to cell one are the shoe sizes. If we break this down, for when the shoe is out of stock, we need three elements: (1) the background, (2) the label and (3) the slash image. If the shoe is in stock, we need just the background and the label. Earlier, I mentioned that whenever elements are grouped together, I prefer to put them in a container. The shoe size elements are an instance of this.</p>

<p>Let’s begin setting this up by dragging a <code>UIView</code>, which will act as our container, into our first table view cell. In the object library, type image in the filter area and update the following values in the size inspector:</p>

<ul>

<li>X: 15</li>

<li>Y: 374</li>

<li>Width: 40</li>

<li>Height: 40</li>

</ul>

<p>Next, in the object library, type image in the filter area and drag a <code>UIImageView</code> into the container we just created, and then update the image with the following values:</p>

<p>Size inspector:</p>

<ul>

<li>X: 0</li>

<li>Y: 0</li>

<li>Width: 40</li>

<li>Height: 40</li>

</ul>

<p>Attributes inspector:</p>

<ul>

<li>Image: <code>outstock-bg</code></li>

</ul>

<p>Now, in the object library, type label in the filter area and drag a <code>UILabel</code> into the same container, and update the following values for that label.</p>

<p>Size inspector:</p>

<ul>

<li>X: 0</li>

<li>Y: 0</li>

<li>Width: 40</li>

<li>Height: 40</li>

</ul>

<p>Attributes inspector:</p>

<ul>

<li>Text: plain</li>

<li>Under text: change “Label” to <code>8</code></li>

<li>Color: light gray</li>

<li>Font: System 17.0</li>

<li>Alignment: center (icon)</li>

</ul>

<p>Finally, in the object library, type label in the filter area and drag another <code>UIImageView</code> into the same container, and then update the image’s following values:</p>

<p>Size inspector:</p>

<ul>

<li>X: 0</li>

<li>Y: 0</li>

<li>Width: 40</li>

<li>Height: 40</li>

</ul>

<p>Attributes inspector:</p>

<ul>

<li>Image: <code>slash</code></li>

</ul>

<p>At this point, your storyboard should look like this:</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fdc80c95-84d5-46ee-93a2-11de66b6268f/design2xcode20-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fdc80c95-84d5-46ee-93a2-11de66b6268f/design2xcode20-opt.png" alt="" width="754" height="1280" /></a></figure>

<p>Now, we need to duplicate this element to create all of the different shoe sizes.</p>

<p>For the first row of shoe sizes, in the outline view, select the container that we just created and hit <code>Command + C</code> to copy, and then hit <code>Command + V</code> to paste. Continue to hit <code>Command + V</code> until you have seven of these containers.</p>

<p>We need to ensure that all seven of these views stay the same size, in both height and width, when in a StackView, which, as the name suggests, allows us to stack both horizontally and vertically.</p>

<p>First, select all of these views in the outline view (hold <code>Shift</code>, and then click the first and last one to select all):</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/11bc55f1-11fe-4897-8b35-6bd1ce082c64/design2xcode21-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/77095539-6342-4fc3-9d6d-d89d63f88a1e/design2xcode21-800w-opt.png" alt="" width="800" height="165" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/11bc55f1-11fe-4897-8b35-6bd1ce082c64/design2xcode21-large-opt.png">View large version</a>)</figcaption></figure>

Click the pin icon, check the boxes for both height and width, and, lastly, click “Add 14 Constraints.”</p>

<p>While the seven views still are selected, click the StackView icon, located two icons to the left of the pin icon:</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4ab1134d-3ab6-45de-b8d8-f4fc36be4434/design2xcode29-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3e39b01d-e85a-4044-a022-71e8e89b0406/design2xcode29-800w-opt.png" alt="" width="800" height="42" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4ab1134d-3ab6-45de-b8d8-f4fc36be4434/design2xcode29-large-opt.png">View large version</a>)</figcaption></figure>

Our containers are now all in a StackView. However, they are stacked right next to each other. To fix this, in the outline view, select the StackView that we just created, and in the attributes inspector update the following values:</p>

<ul>

<li>Axis: horizontal</li>

<li>Alignment: fill</li>

<li>Distribution: equal spacing</li>

<li>Spacing: 10</li>

</ul>

<p>We need to add another row. With the StackView still selected, hit <code>Command + C</code> to copy, and then <code>Command + V</code> to paste. Once you paste the new StackView, move it to right under the first one. They do not need to line up perfectly.</p>

<p>Next, select both of the StackViews and then the StackView icon. Similar to when we selected the StackView icon, the StackViews are now stacked; however, they are on top of each other, rather than next to each other. Select the main StackView, and in the attributes inspector update the following values:</p>

<ul>

<li>Axis: vertical</li>

<li>Alignment: leading</li>

<li>Distribution: equal spacing</li>

<li>Spacing: 7</li>

</ul>

<p>Then, click the pin icon and enter the following values:</p>

<ul>

<li>Top: 9</li>

<li>Right: 15 </li>

<li>Left: 15</li>

<li>Height: 87</li>

<li>Constrain to Margins: unchecked</li>

</ul>

<p>Click “Add 4 Constraints.”</p>

<p>Select one of the other two StackViews in the outline view, click the pin icon, and enter the following values:</p>

<ul>

<li>Right: 0</li>

<li>Left: 0</li>

<li>Height: 40</li>

<li>Constrain to Margins: unchecked</li>

</ul>

<p>Click “Add 3 Constraints.” Repeat this step for the remaining StackView. When you are done, you will see the following:</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c603d3f8-6ed3-4bcd-81e5-19791a2ae887/design2xcode30-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c603d3f8-6ed3-4bcd-81e5-19791a2ae887/design2xcode30-opt.png" alt="" width="748" height="384" /></a></figure>

<p>Finally, select the last four boxes of the bottom StackView, and hit “Delete.” When you complete this step, the boxes will fill the space evenly.</p>

<p>Our next step for setting up cell one is to change the “8” in each of the boxes to the shoe sizes that are in our example page. In addition, we need to adjust two of the boxes to reflect the sizes that are in stock, 9 and 9.5, without a slash through the boxes.</p>

<p>To change the 8 to another shoe size, select the label under the view for a particular box, and in the attributes inspector change the 8 to a new shoe size. Repeat this for each of the sizes in our design.</p>

<p>Lastly, to show that size 9 is available, select the view with “9” as the label, and in the attributes inspector change the <code>outstock-bg</code> image to <code>instock-bg</code>. Repeat for the view with “9.5” as the Label. Then, in the outline view, for each of these two sizes, select the <code>slash</code> image and click “Delete.” This will now show that you have two sizes in stock, 9 and 9.5:</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1a90a75b-dbf8-4887-b592-e3e99b279e12/design2xcode24-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1a90a75b-dbf8-4887-b592-e3e99b279e12/design2xcode24-opt.png" alt="" width="754" height="1280" /></a></figure>

<p>Cell one is now complete.</p>

### Cell Two

<p>Let’s add our elements to cell two. Here, we have two components, a <code>UILabel</code> to display our header and a <code>UITextView</code> for a large body of text. Drag one of each into our second table view cell. With the label selected, update the following values.</p>

<p>Size inspector:</p>

<ul>

<li>X: 18</li>

<li>Y: 7</li>

<li>Width: 109</li>

<li>Height: 21</li>

</ul>

<p>Attributes inspector:</p>

<ul>

<li>Text: plain</li>

<li>Under text: change “Label” to “DESCRIPTION”</li>

<li>Font: Avenir Next Condensed, Demi Bold 14</li>

</ul>

<p>Next, with the text view selected, update the following values:</p>

<p>Size inspector:</p>

<ul>

<li>X: 13</li>

<li>Y: 22</li>

<li>Width: 362</li>

<li>Height: 261</li>

</ul>

<p>Attributes inspector:</p>

<ul>

<li>Text: plain</li>

<li>For the text, enter the following:
</ul>
<blockquote>
<p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Donec id maximus erat, imperdiet iaculis ligula. Curabitur elit dui, ullamcorper ut rutrum in, facilisis non nibh. Maecenas eget ipsum dictum, commodo purus id, aliquam lorem. Duis vitae tincidunt velit. Praesent vestibulum et velit vel tempus. Vivamus fringilla sollicitudin cursus. Nunc sit amet elit mauris. Sed quis tincidunt sem. Proin a rutrum nibh. Nunc porta aliquam dolor at sollicitudin. Nam nisl diam, mattis vel sapien a, eleifend convallis lacus.</p>

<p>Proin tortor arcu, semper vitae blandit pharetra, efficitur eu purus. Sed pharetra odio vitae massa efficitur dapibus. Aenean vitae arcu sollicitudin, mollis erat et, convallis dolor. Mauris feugiat mi elit, ac suscipit mi tempus sodales. Aliquam vitae odio luctus sem bibendum eleifend. Praesent eu aliquet justo, quis tristique dui. Nunc sed purus purus.</p>

</blockquote>

<ul>

<li>Font: Avenir Next Condensed, Ultra Light 17</li>

</ul>

<p>This text view is now set up to match our design. So, the height of 261 that I asked you to enter above is to completely show all of the text we entered. Feel free to experiment with this by changing the amount of text, which would then require a change in height as well.</p>

<p>In regards to <code>UITextView</code> versus <code>UILabel</code>, I honestly do not use <code>UITextView</code> much. My preference is to use <code>UILabel</code>, but in this tutorial I wanted to show you both. I do not have a reason for using the latter other than I just like it more. For this cell, we are adding dummy data to match our design. If you were trying to make the <code>UITextView</code> or <code>UILabel</code> dynamic in height, you would need to do some auto layout updates. For this tutorial, set the height manually and rest assured that the heights of both <code>UILabel</code> and <code>UITextView</code> will adjust to their content’s size using auto layout.</p>

<p>Lastly, let’s add some auto layout to our cell items. First, select the label, click the pin icon, and then enter the following values:</p>

<ul>

<li>Top: 7</li>

<li>Left: 18</li>

<li>Width: 109</li>

<li>Height: 21</li>

</ul>

<p>Then, click “Add 4 Constraints.”</p>

<p>Select the text view, click the pin icon, and enter the following values:</p>

<ul>

<li>Top: 22</li>

<li>Right: 0</li>

<li>Bottom: 6.5</li>

<li>Left: 13</li>

<li>Constrain to Margins: unchecked</li>

</ul>

<p>Click “Add 4 Constraints.” Cell two is now complete.</p>

### Cells Three and Four

<p>Cells three and four are basically the same, except for their text. First, drag a <code>UILabel</code> into each of cell three and cell four. For each label, enter the following values.</p>

<p>Size inspector:</p>

<ul>

<li>X: 18</li>

<li>Y: 10</li>

<li>Width: 109</li>

<li>Height: 21</li>

</ul>

<p>Attributes inspector:</p>

<ul>

<li>Text: plain</li>

<li>Font: Avenir Next Condensed, Demi Bold 14</li>

</ul>

<p>Finally, for the text, for cells three and four, change “Label” to “SIZE GUIDE” and to “REVIEWS (0),” respectively.</p>

### Cell Five

<p>Let’s update our last cell. As you can see from the design we reviewed at the beginning of this tutorial, cell five contains a <code>UIScrollView</code> in order for our “You may also like” section to scroll from left to right. ScrollViews can be created through code; however, consistent with the rest of this tutorial, we will build a working ScrollView with no code.</p>

<p>First, drag four <code>UIImageViews</code> into the cell, next to each other (even overlapping them in order to fit). In the size inspector for each image, change the width to <code>118</code> and the height to <code>172</code>. Then, in the attributes inspector, change “Image” under the four image views to <code>mn-hoodie1</code>, <code>mn-hoodie2</code>, <code>wm-hoodie1</code> and <code>wm-hoodie2</code>, in any order you like. When you are done, you should have something resembling the following:</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e95a7c20-f1ae-4bbe-a4af-0bb943fc8723/design2xcode25-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e95a7c20-f1ae-4bbe-a4af-0bb943fc8723/design2xcode25-opt.png" alt="" width="750" height="346" /></a></figure>

<p>Next, select all four images and select the pin icon. Set the width and height for all four images by clicking the boxes next to width and height and then on “Add 8 Constraints.” With the four images still selected, hit the StackView icon. In the attributes inspector, update the following values:</p>

<ul>

<li>Axis: horizontal</li>

<li>Distribution: equal spacing</li>

<li>Spacing: 10</li>

</ul>

<p>As you can see below, the images are now spaced equally, with 10 pixels in between:</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4deeb79c-a7d1-4075-95fe-974cbb4dfd1b/design2xcode26-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4deeb79c-a7d1-4075-95fe-974cbb4dfd1b/design2xcode26-opt.png" alt="" width="750" height="410" /></a></figure>

<p>Next, we need to put the StackView inside of a view. Select the StackView that you just created, and in the Apple toolbar click on “Editor” &rarr; “Embed In” &rarr; “View.” We need to adjust the size of the newly created view by updating the width to <code>502</code> and the height to <code>172</code>. We also need to adjust the position of where the StackView is located in this new view. Select the StackView and enter the following values in the size inspector:</p>

<ul>

<li>X: 18</li>

<li>Y: 0</li>

</ul>

<p>Now, we need to get everything we just created into a ScrollView. Select the view in which the StackView resides, and then select “Editor” &rarr; “Embed In” &rarr; “Scroll View.” With the new ScrollView selected, enter the following values in the size inspector:</p>

<ul>

<li>X: 0</li>

<li>Y: 0</li>

<li>Width: 375</li>

<li>Height: 172</li>

</ul>

<p>Lastly, in order to make our images scroll, we need to put the ScrollView in another view. Select the ScrollView, and then click “Editor” &rarr; “Embed In” &rarr; “View.” With this new view selected, enter the following values in the size inspector:</p>

<ul>

<li>X: 0</li>

<li>Y: 33</li>

<li>Width: 375</li>

<li>Height: 172</li>

</ul>

<p>The last element we need to add is a <code>UILabel</code>. Drag a label into cell five, and enter the following values in the size inspector:</p>

<ul>

<li>X: 18</li>

<li>Y: 3</li>

<li>Width: 116</li>

<li>Height: 21</li>

</ul>

<p>In the attributes inspector, enter these:</p>

<ul>

<li>Text: plain</li>

<li>Under text: change “Label” to “YOU MIGHT ALSO LIKE”</li>

<li>Font: Avenir Next Condensed, Demi Bold 14</li>

</ul>

<p>Let’s add auto layout to our elements in cell five. With the Label selected, click the pin icon, and enter the following values:</p>

<ul>

<li>Top: 3</li>

<li>Left: 18</li>

<li>Width: 116</li>

<li>Height: 21</li>

</ul>

<p>After entering the values, click “Add 4 Constraints.”</p>

<p>Then, for all of the other elements in cell five, to add auto layout, ensure that all of the disclosure arrows are open in the main view container that is holding the ScrollView, and ensure that you can see all the way to your images, as follows:</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ea835350-fb70-473a-b38c-c67fea4b901f/design2xcode27-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ea835350-fb70-473a-b38c-c67fea4b901f/design2xcode27-opt.png" alt="" width="667" height="291" /></a></figure>

<p>Now, select the StackView, click the pin icon, and enter the following values:</p>

<ul>

<li>Top: 0</li>

<li>Right: 0</li>

<li>Left: 0</li>

<li>Height: 172 (should be checked)</li>

</ul>

<p>When you are done entering the values, click “Add 4 Constraints.”</p>

<p>Next, click on the align icon, which is just to the left of the pin icon, and enter the following values:</p>

<ul>

<li>Horizontally in container: 0 (should be checked)</li>

</ul>

<p>Then, click “Add 1 Constraint.”</p>

<p>Next, in the outline view, select the view that is holding the StackView. With that view selected, click the pin icon and enter the following values:</p>

<ul>

<li>Top: 0</li>

<li>Right: 0</li>

<li>Left: 18</li>

<li>Bottom: 0</li>

</ul>

<p>After entering the values, click “Add 4 Constraints.”</p>

<p>In the outline view, select the ScrollView, click the pin icon, and enter the following values:</p>

<ul>

<li>Top: 0</li>

<li>Right: 0</li>

<li>Left: 0</li>

<li>Bottom: 0</li>

</ul>

<p>Then, click “Add 4 Constraints.”</p>

<p>Finally, in the outline view, select the main container (the view holding the ScrollView), click the pin icon, and enter the following values:</p>

<ul>

<li>Top: 0</li>

<li>Right: -8</li>

<li>Left: 0</li>

<li>Height: 172 (should be checked)</li>

</ul>

<p>When you are done, click “Add 4 Constraints.” You have now completed all of the auto layout for cell five.</p>

<p>Let’s build and run the project by hitting the play button (or press <code>Command + R</code>). You will now be able to see your ScrollView working without having had to code anything. If you run your project on multiple devices, you will also see that everything fits the way it is supposed to.</p>

## Where To Go From Here?

<p>Now that you have completed this tutorial, my first suggestion would be to try repeating what you’ve done without referring to the steps in the tutorial. Once you are comfortable with storyboarding in Xcode, take some time to learn Swift 3. By knowing Swift, you will be able to add a product list as well as to show products on the detail page that we just created with dynamic data. If you still want to learn more, check out my book <a href="https://bit.ly/iOS11Smashing"><em>iOS 11 Programming for Beginners</em></a>, which will be released later this year.</p>

## Summary

<p>In this tutorial, you’ve learned how to bring a design into Xcode without any code. You’ve also learned how to look at a design and figure out what components it has. Then, you added all of the components of the design into storyboards and updated them to match the design. You’ve also learned how to add auto layout so that the design looks good on any device. Hopefully, this tutorial has introduced you to the ease and possibilities of storyboards. The more you work with storyboards, the more comfortable you will get.</p>

<p>As a full-time iOS engineer, I love doing the design side of an app because it helps me to become a better engineer. To me, it is always fun going into the App Store or looking at my favorite app and trying to figure out how they built it, including how they designed it. I really enjoy trying to recreate an app that catches my eye.</p>

<p>If you are a designer, I am sure you have seen plenty of designs that are not perfect. I am OK with my design not being perfect, and you should feel that way with your app’s design. You have to start somewhere, and with the help of other designers and developers, you will improve. Hopefully, this tutorial has opened your eyes to some things that you did not know or at least enabled you to hone your existing skills.</p>

