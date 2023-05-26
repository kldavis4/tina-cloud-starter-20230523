---
title: How To Build Your Own Action For Google Home Using API.AI
slug: build-action-google-home-api-ai
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/66256a16-bbba-4c48-a66c-01ade260a7dd/google-home-build-action-500w-opt.jpeg
date: 2017-05-29T20:36:58.000Z
author: tomhudson
description: >-
  For the holidays, the owner of (and my boss at) _thirteen23_ gave each
  employee a Google Home device. If you don’t already know, Google Home is a
  voice-activated speaker powered by Google Assistant and is a competing product
  to Amazon’s line of Alexa products.

  I already have the Amazon Echo, and as Director of Technology at _thirteen23_,
  I love tinkering with software for new products. For the Amazon Echo, you can
  create what are called "skills", which allow you to build custom interactions
  when speaking to the device.
categories:
  - Mobile
  - API
  - PWA
---
I’ve really enjoyed <a href="https://medium.com/hello-thirteen23/just-the-facts-alexa-71a04b836d7f#.p7r4zc5tp">learning how to build my own skills for Alexa</a>. Now that Google Home is out in the market, Google has its own platform for you to build custom interactions, similar to skills, called "<a href="https://developers.google.com/actions/">actions</a>". I checked it out and found that creating and deploying a basic <a href="https://developers.google.com/actions/">Google action</a> is extremely simple.

If you have a Google Home, you may have played with its prebuilt mad libs. <a href="https://en.wikipedia.org/wiki/Mad_Libs">Mad Libs</a> is a game in which one player prompts others for a list of words to substitute for blanks in a story, before reading the — often comical or nonsensical — story aloud. I’ll use this game to show you how to build your own action for Google Home. Below, I’ve detailed steps to build a custom mad lib action, and I’ve explained why certain steps are important and ultimately how they fit into the voice services world. After this exercise, you will better understand voice services and begin your path to programming actions for Google Home.</p>

### <span class="rh">Further Reading</span> on SmashingMag:

*   [Intrusive Interstitials: Guidelines To Avoiding Google’s Penalty](https://www.smashingmagazine.com/2017/05/intrusive-interstitials-guidelines-avoid-google-penalty/)
*   [What Are Progressive Web AMPs?](https://www.smashingmagazine.com/2016/12/progressive-web-amps/)
*   [Is Your Responsive Design Working? Google Analytics Will Tell You](https://www.smashingmagazine.com/2014/08/responsive-web-design-google-analytics/)
*   [Targeting Mobile Users Through Google AdWords](https://www.smashingmagazine.com/2014/08/targeting-mobile-users-through-google-adwords/)

{{% feature-panel %}}

## Google Actions And API.AI

One notable difference between developing skills for Alexa and actions for Google Home is the software you use to set up the actual product. Amazon has a barebones web form that it has built specific to Alexa skills. Google, on the other hand, <a href="https://api.ai/blog/2016/09/19/api-ai-joining-google/">bought API.AI in September 2016</a>, right before it released Home. Google requires you to use this platform to create your action. There is a short learning curve with <a href="https://api.ai/">API.AI</a>, and the interface takes a little getting used to, but it works pretty well. It also has a lot more built-in power than Alexa’s development portal. The other notable aspect is that you can do a lot more with API.AI outside of Google actions. For this tutorial, we will primarily use this software to create a Google action.

To start off, we will create an API.AI account, create a new agent (which will eventually be our Google Action) and give it a name.</p>

### Step 1: Create an API.AI account

<strong>Note:</strong> If you have a Google Home, make sure the API.AI account is the same Google account logged into that device! Otherwise, you won’t be able to test it on the actual hardware.

Go to <a href="https://api.ai/">API.AI</a> and click “Sign up free.” I signed in with Google because I always have Gmail open. Once signed in, you should see an interface similar to what’s below. Click “Create agent,” and let’s get started!

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/008b6dc7-cdcc-4a5b-99cf-ea2f6ff561a1/action-google-home-image1-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/01874027-cf0f-4811-a026-3d700cc391b6/action-google-home-image1-800w-opt.jpg" alt="Home screen of api.ai" /></a><figcaption>Home screen of API.AI (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/008b6dc7-cdcc-4a5b-99cf-ea2f6ff561a1/action-google-home-image1-large-opt.jpg">View large version</a>)</figcaption></figure>

### Step 2: Name Your Agent

The first thing you need to do is name your agent. An <a href="https://docs.api.ai/docs/concept-agents">API.AI agent</a> represents a conversational interface for your application, device or bot. For this tutorial, our agent represents a conversation to gather words for a happy-birthday mad lib. You can’t have any spaces in the name, so let’s call the agent <code>HappyBirthdayMadLib</code>.

Leave the agent type as “public,” add a description if you want, and click “Save.”

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ca3e1647-541f-4662-9a39-e7ca8bf8b606/action-google-home-image2-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3e36ad87-c787-4a87-8592-300f70303270/action-google-home-image2-800w-opt.jpg" alt="A new HappyBirthdayMadLib agent" /></a><figcaption>A new HappyBirthdayMadLib agent (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ca3e1647-541f-4662-9a39-e7ca8bf8b606/action-google-home-image2-large-opt.jpg">View large version</a>)</figcaption></figure>

## Intents

An <a href="https://docs.api.ai/docs/concept-intents">intent</a> allows users to say what they want to do and lets the system figure out what activity matches what was said. This is another area in which API.AI and Alexa’s skill-building forms differ greatly: API.AI has a tool specific to creating these intents, whereas Amazon requires you to load a raw <a href="https://developer.amazon.com/public/solutions/alexa/alexa-skills-kit/docs/alexa-skills-kit-interaction-model-reference">intent schema</a>. You should see a screen like the one below.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a7b5ec53-e6d1-4a8c-b539-186758ce3ba7/action-google-home-image3-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d764dd11-ffbc-4a22-a2bd-9505378279e1/action-google-home-image3-800w-opt.jpg" alt="Working with intents" /></a><figcaption>Working with intents (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a7b5ec53-e6d1-4a8c-b539-186758ce3ba7/action-google-home-image3-large-opt.jpg">View large version</a>)</figcaption></figure>

We will now create a welcome intent to introduce the Google action and an intent to gather the words in our mad lib. Our last step in this section is to create the final response — the mad lib!

### Step 3: Default Welcome Intent

Let’s now focus on the default welcome intent. (For now, you can ignore the <a href="https://docs.api.ai/docs/concept-intents#fallback-intent">default fallback intent</a>.) The default welcome intent is what fires when your action is invoked through the Google Home device. For instance, when the user says “Hey, Google, open the happy birthday mad lib,” the agent knows to kick off the default welcome intent, which introduces your game to the person speaking to the Google Home device.

Click on “Default welcome intent,” scroll to the bottom, and you should see the screen below:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c523ee49-eea5-42cb-8537-87dd9f15676d/action-google-home-image4-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f7ad3440-2593-4691-aed8-418626b43eaa/action-google-home-image4-800w-opt.jpg" alt="The default welcome intent" /></a><figcaption>The default welcome intent (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c523ee49-eea5-42cb-8537-87dd9f15676d/action-google-home-image4-large-opt.jpg">View large version</a>)</figcaption></figure>

If you mouse over the responses that you see above, a little trash can will appear on the line. Click the trash cans, and delete all of those prebaked responses. Then, let’s write a custom welcome text response:
<blockquote>Hello, and welcome to the Happy Birthday Mad Lib. Let’s begin. Give me the name of a female friend.</blockquote>

Click “Save,” and we are done with the default welcome intent! If you see a screen like the one below, then you are on track.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4da980f8-3774-44cd-8b92-5b2f0c7e13f2/action-google-home-image5-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/eeb9d685-d809-4385-8d06-4aa2c4291ab1/action-google-home-image5-800w-opt.jpg" alt="Create a custom default welcome intent" /></a><figcaption>Create a custom default welcome intent (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4da980f8-3774-44cd-8b92-5b2f0c7e13f2/action-google-home-image5-large-opt.jpg">View large version</a>)</figcaption></figure>

### Step 4: Create a New Intent

Click the “Intents” item in the left-hand menu. You will see “Default fallback intent” and “Default welcome intent” listed. We need a new intent to gather words for our mad lib. We are going to create a new intent; so, click “Create intent” in the upper-right. The first thing we will do on this new screen is name the intent: <code>make_madlib</code>.</p>

### Step 5: “User Says” Content

Our next step is to populate the “User says” area. “User says” phrases define what users need to say to trigger an intent. We only need a couple here. These will be answers to the request you stated in the default welcome intent: “Give me the name of a female friend.” It ultimately helps with the machine-learning aspect of Google Home. The <a href="https://docs.api.ai/docs/concept-intents#user-says">documentation explains</a> about “User says” and why example answers like this help with machine learning. Using a name of one of your friends or Laura, enter these two values:

*   Laura
*   A name is Laura

If your entries look like what you see below, then go ahead and click “Save,” and we will move on to creating our action.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/eb6fcd06-f4ff-48f1-a36b-0716a7f8cd11/action-google-home-image6-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/73362388-0a32-4130-b82a-3270e850599a/action-google-home-image6-800w-opt.jpg" alt="Creating your own make_madlib intent" /></a><figcaption>Creating your own <code>make_madlib</code> intent (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/eb6fcd06-f4ff-48f1-a36b-0716a7f8cd11/action-google-home-image6-large-opt.jpg">View large version</a>)</figcaption></figure>

### Step 6: Defining Your Action

In order to gather all of the words we need for the happy-birthday mad lib, we will need to create an action. An <a href="https://docs.api.ai/docs/concept-actions">action</a> corresponds to the step your application will take when a specific intent has been triggered by a user’s input.

We need to enter an action name in the field. Enter this name: <code>make_madlib</code>.

For our mad libs action, we will gather several words. These will be our <a href="https://docs.api.ai/docs/concept-actions#section-defining-parameters-manually">parameters</a> for the action. Parameters consist of all of the data we need in order to complete our action. Given that this is a mad lib, we will need to gather various parts of speech, such as nouns and adjectives. These are our parameters for the action of creating a mad lib! So, let’s create some parameters. Each one of these is required, so check the box on each one.

1.  Edit the `given-name` entry, changing the name to `name1`. Check it as required, and enter the prompt “Give me a name of a female friend”.
2.  Create a new parameter named `noun1` of entity `@sys.any`, a value of `$noun1`, mark it as required, and enter the prompt “Give me a noun”.
3.  Create a new parameter named `adjective1` of entity `@sys.any`, a value of `$adjective1`, mark it as required, and enter the prompt “Give me an adjective”.
4.  Create a new parameter named `noun2` of entity `@sys.any`, a value of `$noun2`, mark it as required, and enter the prompt “Give me another noun”.
5.  Create a new parameter named `number1` of entity `@sys.number`, a value of `$number1`, mark it as required, and enter the prompt “Give me a number”.
6.  Create a new parameter named `adjective2` of entity `@sys.any`, a value of `$adjective2`, mark it as required, and enter the prompt “Give me an adjective”.
7.  Create a new parameter named `name2` of entity `@sys.given-name`, a value of `$name2`, mark it as required, and enter the prompt “Give me a name of another friend”.
8.  Create a new parameter named `noun3` of entity `@sys.any`, a value of `$noun3`, mark it as required, and enter the prompt “Give me another noun”.
9.  Create a new parameter named `bodypart1` of entity `@sys.any`, a value of `$bodypart1`, mark it as required, and enter the prompt “Name a part of the body”.
10.  Create a new parameter named `noun4` of entity `@sys.any`, a value of `$noun4`, mark it as required, and enter the prompt “Last one. Give me another noun”.

I realize this is a lot. Are you still with me? Great. It is important to name everything exactly as outlined above. At this point, your screen should look like this:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/973b6972-50a6-4ea5-b8b8-1a293f03892a/action-google-home-image7-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3ddbb6ac-1405-4d0b-93cb-e7c965c811b7/action-google-home-image7-800w-opt.jpg" alt="Creating an action and parameters for your make_madlib intent" /></a><figcaption>Creating an action and parameters for your <code>make_madlib</code> intent (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/973b6972-50a6-4ea5-b8b8-1a293f03892a/action-google-home-image7-large-opt.jpg">View large version</a>)</figcaption></figure>

### Step 7: Create the Response

Move down to the “Response” section and add this content:
<blockquote>Friends, this is a surprise party for $name1. We are here to celebrate her $noun1. All of her most $adjective1 friends are here, including me, her devoted and faithful $noun2. I must say that she doesn’t look a day over $number1. Naturally, we have some $adjective2 presents for her. $name2 bought her a beautiful copper $noun3 that she can wear on her lovely $bodypart1. Now, let’s all sing together: “Happy $noun4 day to you!”</blockquote>

We’re done! This final part should look like what you see below:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4347decf-d405-4fba-a5cd-195f8cab5817/action-google-home-image8-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d16d1355-7cfd-4ca6-b232-b7b97d3ac0cf/action-google-home-image8-800w-opt.jpg" alt="Insert the response text" /></a><figcaption>Insert the response text (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4347decf-d405-4fba-a5cd-195f8cab5817/action-google-home-image8-large-opt.jpg">View large version</a>)</figcaption></figure>

<strong>Note:</strong> Do you see the bottom of the screen in the image above, where it has “End conversation” checked under the “Actions on Google” heading? In order for that to show up, you need to do the next step. Once it is there, you need to go back to the intent and check that box.</p>

## Integration

In order to test what we’ve created on a Google Home device or simulator, we need to integrate this new mad lib agent with the “Actions on Google” integration. API.AI has many different types of <a href="https://docs.api.ai/docs/integrations">integrations</a> to choose from, such as for Facebook Messenger, Slack, Skype, Alexa and Cortana. Remember that API.AI wasn’t built specifically for Google Home. In order for this new action to work on your Google Home, we need to integrate it with “Actions on Google.”

In the next step, we will enable the API.AI agent to work with the Google Home device by integrating it with Google actions.</p>

### Step 8: Integrate With Actions on Google

Click on “Integrations” in the left-hand menu. The very top-left item should be “Actions on Google.” Click on that item to open up the settings. You should see something like the screen below:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fcb9a7a9-6769-4507-b037-dcee4d3b6911/integration1-step-8-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0a06456a-5ac8-4a49-aa6c-611d7db58c00/integration1-step-8-800w-opt.png" width="800" height="500" alt="The Actions on Google integration" /></a><figcaption>The “Actions on Google” integration (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fcb9a7a9-6769-4507-b037-dcee4d3b6911/integration1-step-8-large-opt.png">View large version</a>)</figcaption></figure>

Turn it on by flipping that toggle in the upper-right corner. Click on the Create Project button in the lower right. This will take you to the Actions on Google site for setting all the publishing parameters for your action as well as being able to test it in the simulator. Next, you can try it out in the <a href="https://developers.google.com/actions/tools/web-simulator">Google Home Web Simulator</a>.</p>

## Testing Your Action

You can test your new action in a couple of ways. You can use the Google Home Web Simulator, which allows you to test in a browser without an actual Google Home device, or you can test on a device that is logged in with the same account. Let’s test it in the simulator first.

In these final steps, you will test your new Google action in a simulator and, if you have access to one, an actual Google Home device!

### Step 9: Testing on Google Home Web Simulator

To test your Google action, you can run it in the <a href="https://developers.google.com/actions/tools/web-simulator">Google Home Web Simulator</a>. Go ahead and open that tool. You will see the screen below. Click “Start.”

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e2c625d0-8450-4e71-b716-fc286f80362c/action-google-home-image10-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/54aeebad-96ec-4aa2-bb4f-2d1161433944/action-google-home-image10-800w-opt.jpg" alt="The Google Home Web Simulator" /></a><figcaption>The Google Home Web Simulator (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e2c625d0-8450-4e71-b716-fc286f80362c/action-google-home-image10-large-opt.jpg">View large version</a>)</figcaption></figure>

On the next screen, you can type text in the “Dialog” area on the left, hit return and hear a result. On the right side of the screen, under “Log,” you will see the resulting JSON generated behind the scenes. This JSON is generated by the Google Home device upon hearing the user’s command. For this simulator, it comes from the text that you typed in the “Dialog” area. If you scroll down in the “Log” area, under the “Response” subheading, you will see the JSON returned from API.AI after it has processed your JSON request.

Put on some headphones or turn up your speakers! Type the following text in the “Dialog” text field: <code>Talk to my test app</code>

Once you do that and hit return, you should hear the start of your mad lib action, and the screen will look like what you see below:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/95940cc5-c281-478a-bf03-06cbf3d1b904/action-google-home-image11-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f2c1c49b-64aa-484a-95b2-54a6af9cbf4d/action-google-home-image11-800w-opt.jpg" alt="Testing your action in the simulator" /></a><figcaption>Testing your action in the simulator (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/95940cc5-c281-478a-bf03-06cbf3d1b904/action-google-home-image11-large-opt.jpg">View large version</a>)</figcaption></figure>

Go through the rest of the mad lib to finish it up, and the result should look similar to what you see below, but with your own words. Our next step will be to test it on an actual Google Home device.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/992d61e7-36ce-45d8-8249-32a4928b2513/action-google-home-image12-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7f071c07-a9e0-4d88-81fe-12d907af64fa/action-google-home-image12-800w-opt.jpg" alt="Final result of your action in the simulator" /></a><figcaption>Final result of your action in the simulator (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/992d61e7-36ce-45d8-8249-32a4928b2513/action-google-home-image12-large-opt.jpg">View large version</a>)</figcaption></figure>

### Step 10: Testing on a Google Home Device

To test the mad lib on a Google Home device, all you need to do is log into the device using the same account that you used to authorize your action for testing in the simulator. Once you authorize your action for previewing, it will automatically be available on the Google Home device assigned to that same account. Note that you need to be authorized in the API.AI account under the same Google account in order for this to work!

In step 8, if you set your invocation name to “Happy birthday mad lib,” then try invoking the action you just built by saying to your device, “OK Google, open happy birthday mad lib.”

Once you do this, Google Home should say the welcome intent (from step 3) back to you:
<blockquote>Hello, and welcome to the Happy Birthday Mad Lib. Let’s begin. Give me the name of a female friend.</blockquote>

From here, you can give Google Home the name of a female friend, and follow the rest of the prompts until it reads the story back to you!

For this example, we won’t be deploying it for public use, because we would all be deploying the same action. But if you do come up with a unique action and you want to put it out there for the world to use, you can do that by following <a href="https://developers.google.com/actions/distribute/deploy">the simple steps in the documentation</a>. Like when building an Alexa skill, the Google team will need to review your action before accepting it, so be patient!

## What’s Next?

In this article, you learned how to create a basic action for Google Home. You learned about the API.AI platform for creating a Google action and how to set up all parameters in order for your action to work properly. Now you have a basic understanding of how to build custom functionality for the Google Home device, and with this knowledge you can explore more complex ideas for applications running on Google Home.

This example is one of the basic ways to build an action for Google Home. What if your action is a bit more complicated? In that case, you should build in your own custom webhook to handle tasks such as querying a database or looking up user data. Luckily, the API.AI interface provides an easy way to use a webhook to pull in what the user says, then to make decisions based on that input and give a response. See Google’s <a href="https://github.com/actions-on-google/apiai-silly-name-maker-webhook-nodejs">tutorial on GitHub</a> for how to create an action with a webhook.

Good luck, and most of all, have fun! If you have any questions, ask them in the comments section below.

{{< signature "da, vf, yk, al, il" >}}

