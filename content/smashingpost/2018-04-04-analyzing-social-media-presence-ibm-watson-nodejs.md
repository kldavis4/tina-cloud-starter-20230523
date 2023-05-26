---
title: 'Analyzing Your Company’s Social Media Presence With IBM Watson And Node.js'
slug: analyzing-social-media-presence-ibm-watson-nodejs
author: jamie-munro
image: >-
  //archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9ae384dc-90de-4dd4-967f-de0c8d605f39/personality-insights.jpg
date: 2018-04-04T13:00:50+02:00
summary: >-
  How can you gain a better understanding of your audience? Well, one way would be to use user-generated content that can be integrated into Machine Learning (ML) technology. In this article, Jamie Munro demonstrates how that can be done.
description: >-
  How can you gain a better understanding of your audience? Well, one way would be to use user-generated content that can be integrated into Machine Learning (ML) technology. In this article, Jamie Munro demonstrates how that can be done.
categories:
  - UX
  - Node.js
  - Machine Learning
---
<p>If you are unfamiliar with Machine Learning (ML) technology, it has existed in science fiction for many years and is finally reaching its maturity in our society. One of the first ML examples I saw as a kid was in Star Trek’s <em>The Next Generation</em> when Lieutenant Tasha Yar trains with her holographic opponent that learns how to fight and better defeat in future battles.
</p>

<p>In today’s society, China has developed a “<a href="https://www.scmp.com/news/china/society/article/2089478/robot-technology-helping-direct-traffic-southern-china">lane robot</a>” that is a guard rail controlled by a computer system that can direct the flow of traffic into different lanes, increasing safety and improving traveling time. This is done automatically based on time of day and how much traffic is flowing in each direction.
</p>

<p>Another example is <a href="https://spectrum.ieee.org/cars-that-think/robotics/artificial-intelligence/pittsburgh-smart-traffic-signals-will-make-driving-less-boring">Pittsburg unveiling AI traffic signals</a> that automatically detect traffic patterns and alter the traffic lights on-the-fly. Each light is controlled independently to help reduce both the commuting time and the idling time of cars. According to the article, pilot tests have demonstrated a reduced travel time of 25% and idling time by over 40%. There are, of course, hundreds of other examples of ML technology that make intelligent decisions based on the content it consumes.
</p>

<p>To accomplish today’s goal, I am going to demonstrate (using Node.js) how to perform a search with Twitter’s API to retrieve content that will be inputted into the ML algorithm to be analyzed. This way, you’ll be provided with characteristics about the users who wrote that specific content so that you can get a better understanding of your audience. The example application will be written using Node.js as the server.</p>

<p>It is beyond the scope of this article to demonstrate how to write an ML algorithm. Instead, to aid in the analysis, I will demonstrate how to use IBM’s <a href="https://www.ibm.com/watson/">Watson</a> to help you understand the general personality of your social media audience.
</p>

{{% feature-panel %}}

## What Is IBM Watson?

<p>In 2011, Watson began as a computer system that attempted to index the (entire) Internet. It was originally programmed to answer questions posed in ordinary English. Watson <a href="https://endyourif.com/ibms-watson-on-jeopardy-the-final-saga/">competed and won</a> on the TV show <em>Jeopardy!</em> claiming a $1,000,000 cash prize.</p>

<p>Watson was now a proven success.</p>

<p>With the fame of winning on <em>Jeopardy!</em>, IBM has continued to push Watson’s capabilities. Watson has evolved into an enterprise-level application that is focused on Artificial Intelligence (AI) which you can train to identify what you care about most allowing you to make smarter decisions automatically.</p>

<p>The suite of Watson’s services is divided into six high-level categories:</p>

<ol>
<li><strong>Conversation</strong><br />The services in this category allow you to build intelligent chatbot’s or a virtual customer service agent.</li>
<li><strong>Knowledge</strong><br />This category is focused on teaching Watson how to interpret data to unlock hidden value and monitor trends.</li>
<li><strong>Vision</strong><br />This service provides the ability to tag content inside an image that is used to train Watson to be able to automatically recognize the same pattern inside of other images.</li>
<li><strong>Speech</strong><br />These services provide the ability to convert speech to text and the inverse, text to speech.</li>
<li><strong>Language</strong><br />This category is split between translating one language to another as well as interpreting the text to predict what predefined category the text belongs to.</li>
<li><strong>Empathy</strong><br />This category is devoted to understanding the content’s tone, personality, and emotional state. Inside this category is a service called “Personality Insights” that will be used in this article to predict the personality characteristics with the social media content we will provide it.</li>
</ol>

<p>This article will be focusing on understanding the personality of the content that we will fetch from Twitter. However, as you can see, Watson provides many other AI features that you can explore to automate many other processes simply through training and content aggregation.</p>

## Personality Insights

<p><a href="https://www.ibm.com/watson/services/personality-insights/">Personality Insights</a> will analyze content and help you understand the habits and preferences at an individual level and at scale. This is called the ‘personality profile.’ The profile is split into two high-level groups: <strong>Personality characteristics</strong> and <strong>Consumption preferences</strong>. These groups are further broken down into more finite components.</p>

<p><strong>Note</strong>: <em>To help understand the high-level concepts (before we deep dive into the results), the <a href="https://console.bluemix.net/docs/services/personality-insights/index.html#about">Personality Insights documentation</a> provides this helpful summary describing how the profile is inferred from the content you provide it.</em></p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9ae384dc-90de-4dd4-967f-de0c8d605f39/personality-insights.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9ae384dc-90de-4dd4-967f-de0c8d605f39/personality-insights.jpg" sizes="100vw" caption="Big Five Personality Traits. Image courtesy: <a href='https://www.ibm.com/us-en/marketplace/6626'>IBM.com</a>. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9ae384dc-90de-4dd4-967f-de0c8d605f39/personality-insights.jpg'>Large preview</a>)" alt="IBM Watson’s Big Five Personality Traits" >}}

### Personality Characteristics

<p>The <em>Personality Insights</em> service infers personality characteristics based on three primary models:</p>

<ul>
  <li>The ‘Big Five’ personality characteristics represent the most widely used model for generally describing how a person engages with the world. The model includes five primary dimensions:</li>
  <ul>
    <li>Agreeableness</li>
    <li>Conscientiousness</li>
    <li>Extraversion</li>
    <li>Emotional range</li>
    <li>Openness<br /><strong>Note</strong>: <em>Each dimension has six facets that further characterize an individual according to the dimension.</em></li>
  </ul>
  <li>Needs describe which aspects of a product will resonate with a person. The model includes twelve characteristic needs:</li>
  <ul>
    <li>Excitement</li>
    <li>Harmony</li>
    <li>Curiosity</li>
    <li>Ideal</li>
    <li>Closeness</li>
    <li>Self-expression</li>
    <li>Liberty</li>
    <li>Love</li>
    <li>Practicality</li>
    <li>Stability</li>
    <li>Challenge</li>
    <li>Structure</li>
  </ul>
  <li>Values describe motivating factors that influence a person’s decision making. The model includes five values:</li>
  <ul>
    <li>Self-transcendence / Helping others</li>
    <li>Conservation / Tradition</li>
    <li>Hedonism / Taking pleasure in life</li>
    <li>Self-enhancement / Achieving success</li>
    <li>Open to change / Excitement</li>
  </ul>
</ul>

<p><em>For more information, see <a href="https://console.bluemix.net/docs/services/personality-insights/models.html">Personality models</a>.</em></p>

### Consumption preferences

<p>Based on the personality characteristics inferred from the input text, the service can also return an indication of the author’s consumption preferences. ‘Consumption preferences’ indicate the author’s likelihood to pursue different products, services, and activities. The service groups the individual preferences into eight categories:</p>

<ul>
<li>Shopping</li>
<li>Music</li>
<li>Movies</li>
<li>Reading and learning</li>
<li>Health and activity</li>
<li>Volunteering</li>
<li>Environmental concern</li>
<li>Entrepreneurship</li>
</ul>

<p>Each category contains from one to as many as a dozen individual preferences.</p>

<p><strong>Note</strong>: <em>For more information, see <a href="https://console.bluemix.net/docs/services/personality-insights/preferences.html">Consumption preferences</a>. For a more in-depth overview of a particular point of interest, I suggest you refer to the <a href="https://console.bluemix.net/docs/services/personality-insights/index.html#about">Personality Insights documentation</a>.</em></p>

<p>To be effective, Watson requires a minimum of a hundred words to provide an insight into the consumer’s personality. The more words provided, the better Watson can analyze and determine the consumer’s preference.</p>

<p>This means, if you wish to target individuals, you will need to collect more data than one or two tweets from a specific person. However, if a user writes a product review, blog post, email, or anything else related to your company, this could be analyzed on both an individual level and at scale.</p>

<p>To begin, let’s start by setting up the Personality Insights service to begin analyzing a real-world example.</p>

## Configuring The Personality Insights Service

<p>Watson is an enterprise application but they offer <a href="https://console.bluemix.net/registration/?target=%2Fdeveloper%2Fwatson%2Fcreate-project%3Fservices%3Dpersonality_insights%26cm_mmc%3DOSocial_Tumblr-_-Watson%2BCore_Watson%2BCore%2B-%2BPlatform-_-WW_WW-_-wdc-ref%26cm_mmc%3DOSocial_Tumblr-_-Watson%2BCore_Watson%2BCore%2B-%2BPlatform-_-WW_WW-_-wdc-ref%26cm_mmca1%3D000000OF%26cm_mmca2%3D10000409&cm_mc_uid=63484665600115121382470&cm_mc_sid_50200000=1512602317&cm_mc_sid_52640000=1512602317">a free, limited</a> service. Once you've created an account and are logged in, you will need to add the <a href="https://console.bluemix.net/catalog/services/personality-insights">Personality Insight service</a>. IBM offers a Lite plan that is free. The Lite plan is limited to 1,000 API calls per month and is automatically deleted after 30 days &mdash; perfect for our demonstration.</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a5024fb7-1c5e-4939-8f95-c6aa963c94a9/insights-service.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a5024fb7-1c5e-4939-8f95-c6aa963c94a9/insights-service.jpg" sizes="100vw" caption="Create the Personality Insights Service. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a5024fb7-1c5e-4939-8f95-c6aa963c94a9/insights-service.jpg'>Large preview</a>)" alt="Create the Personality Insights Service" >}}

<p>Once the service has been added, we will need to retrieve the service’s credentials to perform API calls against it. From <a href="https://console.bluemix.net/dashboard/apps">Watson’s Dashboard</a>, your service should be displayed. After you've selected the service, you'll find a link to view the Service credentials in the left-hand menu. You will need to create a new ‘Credential.’ A unique name is required and optional configuration parameters can be defaulted for this login. For now, we will leave the configuration options empty.</p>

<p>After you have created a credential, select the ‘View’ credentials link. This will display the API’s URL, your username, and password required to securely execute API calls. Save these somewhere safe as we will need them in the next step.</p>

## Testing The Personality Insights Service

<p>To perform API calls, I am going to use Node.js. If you already have Node.js installed, you can move on to the next step; otherwise, follow the instructions to setup Node.js from the <a href="https://nodejs.org/en/download/">official download page</a>.</p>

<p>To demonstrate how to use the <em>Personality Insights</em>, I am going to create a new Node.js project on my computer. With a command prompt open, navigate to the directory where your Node.js projects will be stored and create your new project:</p>

<pre><code class="language-javascript">mkdir watson-sentiments
cd watson-sentiments
npm init
</code></pre>

<p>To assist with making the API calls to Watson, I am going to leverage the NPM Package: <a href="https://www.npmjs.com/package/watson-developer-cloud">Watson Developer Cloud Node.js SDK</a>. This package can be installed via the command prompt:</p>

<pre><code class="language-bash">npm install watson-developer-cloud --save</code></pre>

<p>Before making the first call, the <em>PersonalityInsightsV3</em> object needs to be instantiated with the credentials from the previous section. Begin by creating a new file called <em>index.js</em> that will contain the Node.js code.</p>

<p>Here is an example of configuring the class so it is ready to make API calls:</p>

<div class="break-out">

<pre><code class="language-javascript">var PersonalityInsightsV3 = require(’watson-developer-cloud/personality-insights/v3’);
var personality_insights = new PersonalityInsightsV3({
  "url": "https://gateway.watsonplatform.net/personality-insights/api",
  "username": "**************************",
  "password": "*************",
  "version_date": "2017-12-01"
});
</code></pre></div>

<p>The <code>personality_insights</code> variable is what we will use to interact with the API for the <em>Personality Insights</em> service. Let’s review how to execute a call and return a personality profile:</p>

<div class="break-out">

<pre><code class="language-javascript">var fs = require(’fs’);

personality_insights.profile({
"contentItems": [
   {
         "content": "Some content that contains more than 100 words...",
         "contenttype": "text/plain",
         "created": 1447639154000,
         "id": "666073008692314113",
         "language": "en"
      }
   ],
   "consumption_preferences": true
}, (err, response) => {
if (err) throw err;

fs.writeFile("results.txt", JSON.stringify(response, null, 2), function(err) {
if (err) throw err;

console.log("Results were saved!");
});
  });
</code></pre></div>

<p>The <code>profile</code> function accepts an array of <code>contentItems</code>. The ‘content’ item contains the actual content with a few additional properties identifying additional information to help Watson interpret it.</p>

<p>When this is executed, the results are written to a text file (the results are too large to write in the console). The result is an object that contains the following high-level properties:</p>

<ul>
<li><code>word_count</code></li>
<li>The count of words interpreted</li>
<li><code>processed_language</code></li>
</ul>

<p>The language that the content provided, e.g. (en).</p>

<ul>
<li><strong>Personality</strong><br />This is an array of the ‘Big Five’ personality characteristics (Openness, Conscientiousness, Extraversion, Agreeableness, and Emotional range). Each characteristic contains an overall percentile for that characteristic (e.g. 0.8100175318417588). To ascertain more detail, there is an array called <code>children</code> that provides more in-depth insight. For example, a child category under ‘Openness’ is ‘Adventurousness’ that contains its own percentile.</li>
<li><strong>Needs</strong><br />This is an array of the twelve characteristics that define the aspects a person will resonate with a product (Excitement, Harmony, Curiosity, Ideal, Closeness, Self-expression, Liberty, Love, Practicality, Stability, Challenge, and Structure). Each characteristic contains a percentile of how the content was interpreted.</li>
<li><strong>Values</strong><br />This is an array of the five characteristics that describe motivating factors that influence a person’s decision making (Self-transcendence / Helping others, Conservation / Tradition, Hedonism / Taking pleasure in life, Self-enhancement / Achieving success, and Open to change / Excitement). Each characteristic contains a percentile of how the content was interpreted.</li>
<li><strong>Behavior</strong><br />This is an array that contains thirty-one elements. Each element provides a percentile of when the content was created. Seven of the elements define the days of the week (Sunday through Saturday). The remaining twenty-four elements define the hours of the day. This helps you understand when customer’s interact with your product.</li>
<li><code>consumption_preferences</code><br />This is an array that contains eight different categories with as much as a twelve child categories providing a percentile of likelihood to pursue different products, services, and activities (Shopping, Music, Movies, Reading and learning, Health and activity, Volunteering, Environmental concern, and Entrepreneurship).</li>
<li><strong>Warnings</strong><br />This is an array that provides messages if a problem was encountered interpreting the content provided.</li>
</ul>

<p>Here is a CodePen of the formatted results:</p>

{{< codepen height="480" theme_id="light" slug_hash="NXrypp" default_tab="result" user="endyourif" editable="true" data-editable="true" >}}See the Pen <a href="https://codepen.io/endyourif/pen/NXrypp/">Example Watson Results</a> by Jamie Munro (<a href="https://codepen.io/endyourif">@endyourif</a>) on <a href="https://codepen.io">CodePen</a>.{{< /codepen >}}

## Configuring Twitter

<p>To search Twitter for relevant tweets, I am going to use the Twitter NPM package. From a console window where the application is hosted, run the following command to install:</p>

<pre><code class="language-bash">npm install twitter --save</code></pre>

<p>Before we can implement the Twitter package, you need to <a href="https://apps.twitter.com/">create a Twitter application</a>.</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cee7e291-da72-436a-9f3d-59653a1de389/twitter.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cee7e291-da72-436a-9f3d-59653a1de389/twitter.jpg" sizes="100vw" caption="Retrieving Twitter’s Access Tokens. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cee7e291-da72-436a-9f3d-59653a1de389/twitter.jpg'>Large preview</a>)" alt="Retrieving Twitter’s Access Tokens" >}}

<p>Once you’ve created your application, you need to retrieve the authorization keys required to perform API calls. With your application created, navigate to the ‘Keys’ and ‘Access Tokens’ page. Since we are not performing API calls against users of Twitter, OAuth integration is not required. Instead, we need only the four following keys:</p>

<ol>
<li>Consumer Key</li>
<li>Consumer Secret</li>
<li>Access Token</li>
<li>Access Token Secret</li>
</ol>

<p>The last two keys need to be generated near the bottom of the ‘Keys’ and ‘Access Tokens’ page. With the keys, here is an example of searching for Tweets about #SmashingMagazine:</p>

<div class="break-out">

<pre><code class="language-javascript">var Twitter = require(’twitter’);

var client = new Twitter({
  consumer_key: ’*********************’,
  consumer_secret: ’******************’,
  access_token_key: ’******************’,
  access_token_secret: ’****************’
});

client.get(’search/tweets’, { q: ’#SmashingMagazine’ }, function(error, tweets, response) {
if(error) throw error;

console.log(tweets);
});
</code></pre></div>

<p>The result of this code will log a list tweets about Smashing Magazine. For the purposes of this demonstration, the following fields are of interest to us:</p>

<ol>
<li><code>id</code></li>
<li><code>created_at</code></li>
<li><code>text</code></li>
<li><code>metadata.iso_language_code</code></li>
</ol>

<p>These are the fields we will feed Watson.</p>

## Integrating Personality Insights With Twitter

<p>With Twitter setup and Watson setup, it’s time to integrate the two together and see the results. To make it interesting, let’s search for <code>#DonaldTrump</code> to see what the world thinks about the President of the United States. Here is the code example to search Twitter, feed the results into Watson, and write the results to a text file:</p>

<div class="break-out">

<pre><code class="language-javascript">var fs = require(’fs’);
var Twitter = require(’twitter’);

var client = new Twitter({
  consumer_key: ’*********************’,
  consumer_secret: ’******************’,
  access_token_key: ’******************’,
  access_token_secret: ’****************’
});

var PersonalityInsightsV3 = require(’watson-developer-cloud/personality-insights/v3’);
var personality_insights = new PersonalityInsightsV3({
  "url": "https://gateway.watsonplatform.net/personality-insights/api",
  "username": "**************************",
  "password": "*************",
  "version_date": "2017-12-01"
});

client.get(’search/tweets’, { q: ’#DonaldTrump’ }, function(error, tweets, response) {
if(error) throw error;

var contentItems = [];

// Loop through the tweets
for (var i = 0; i < tweets.statuses.length; i++) {
var tweet = tweets.statuses[i];

contentItems.push({
"content": tweet.text,
"contenttype": "text/plain",
"created": new Date(tweet.created_at).getTime(),
"id": tweet.id,
"language": tweet.metadata.iso_language_code
});
}

// Call Watson with the tweets
personality_insights.profile({
"contentItems": contentItems,
"consumption_preferences": true
}, (err, response) => {
if (err) throw err;

// Write the results to a file
fs.writeFile("results.txt", JSON.stringify(response, null, 2), function(err) {
if (err) throw err;

console.log("Results were saved!");
});
});
});
</code></pre></div>

<p>Here is another CodePen of the formatted results that I received:</p>

{{< codepen height="480" theme_id="light" slug_hash="ppPyRM" default_tab="result" user="endyourif" editable="true" data-editable="true" >}}See the Pen <a href="https://codepen.io/endyourif/pen/ppPyRM/">Donald Trump Watson Results</a> by Jamie Munro (<a href="https://codepen.io/endyourif">@endyourif</a>) on <a href="https://codepen.io">CodePen</a>.{{< /codepen >}}

## What Do The Results Say?

<p>Once we’ve analyzed the ‘Openness’ trait of the ‘Big Five,’ we can infer the following:</p>

<ul>
<li>Emotion is quite low at 13%</li>
<li>Imagination is average at 54%</li>
<li>Intellect is very high at 96%</li>
<li>Authority challenging is also quite high at 87%</li>
</ul>

<p>The ‘Conscientiousness’ trait at a high-level is average at 46% compared with the ‘Openness’ high-level average of 88%. Whereas ‘Agreeableness’ is very low at only 25%. I guess people on Twitter don’t like to agree with Donald Trump.</p>

<p>Moving on to the ‘Needs.’ The sub-categories of ‘Curiosity’ and ‘Structure’ are in the 60 percentile compared to other categories being below the 10th percentile (Excitement, Harmony, etc.).</p>

<p>And finally, under ‘Values,’ the sub-category that stands out to me as interesting is the ‘Openness’ to ‘Change’ at an abysmal 6%.</p>

<p>Based on when you perform your search, your results may vary as the results are limited to the past seven days from executing the example.</p>

<p>From these results, I would determine that the average person who tweets about Donald Trump is quite intellectual, challenges authority, and is not open to change.</p>

<p>With these results, it would allow you to automatically alter how you would target your content towards your audience to match the results received. You will need to determine what categories are of interest and what percentiles do you wish to target. With this ammunition, you can begin automating.</p>

## What Else Can I Do With Watson?

<p>As I mentioned at the beginning of this article, Watson offers many other different services. With these services, you could automate many different parts of common business processes. For example:</p>

<ul>
<li>Building a chat bot that can intelligently answer questions based on a knowledge base of information;</li>
<li>Build an application where you dictate what you want written to Watson by using the speech to text functionality;</li>
<li>Automatically translate your content into different languages to create a multi-lingual site or knowledge base;</li>
<li>Teach Watson how to look for specific patterns in images. This could be used to determine if a logo is embedded into a photo.</li>
</ul>

<p>This, of course, is a very small subset that my limited imagination can postulate. I’m sure you can think of many other ways to leverage Watson’s immense capabilities.</p>

<p>If you are looking for more examples, IBM has an entire GitHub repository dedicated to their <a href="https://github.com/watson-developer-cloud/node-sdk/tree/master/examples">Node.js SDK</a>. The example folder contains over ten sample applications that convert speech to text, text to speech, tone analysis, and visual recognition to name just a few.</p>

## Conclusion

<p>Before Watson can runaway with technological growth, resulting in the singularity where Artificial Intelligence destroys mankind, this article demonstrated how you can turn social media content into a powerful understanding of how the people creating the content think. Using the results from Watson, your application can use the categories of interest where the percentile exceeds or is less than a predetermined amount to change how you target your audience.</p>

<p>If you have other interesting uses of Watson or how you are using the <em>Personality Insights</em>, be sure to leave a comment below.
</p>

{{< signature "rb, ra, yk, il" >}}

