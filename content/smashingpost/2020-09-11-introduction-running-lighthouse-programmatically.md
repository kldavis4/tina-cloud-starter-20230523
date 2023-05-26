---
title: 'An Introduction To Running Lighthouse Programmatically'
slug: introduction-running-lighthouse-programmatically
author: katy-bowman
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/85fab658-afff-43ee-923f-628d9cea16b7/introduction-running-lighthouse-programmatically.png
date: 2020-09-11T08:30:00.000Z
summary: >-
  Being able to run Google’s Lighthouse analysis suite programmatically provides a lot of advantages, especially for larger or more complex web applications. Using Lighthouse programmatically allows engineers to set up quality monitoring for sites that need more customization than straightforward applications of Lighthouse (such as Lighthouse CI) allow. This article contains a brief introduction to Lighthouse, discusses the advantages of running it programmatically, and walks through a basic configuration.
description: >-
  This article contains a brief introduction to Lighthouse, discusses the advantages of running it programmatically, and walks through a basic configuration.
categories:
  - Performance
  - Techniques
  - Tools
---

Lighthouse is Google’s suite of website quality analysis tools. It allows you to assess your site’s performance, accessibility, SEO, and more. It is also highly configurable, making it flexible enough to be useful for all sites, from the simplest to the highly complex. This flexibility includes several different ways of running the tests, allowing you to choose the method that works best for your site or application.

One of the simplest ways to run Lighthouse is through [Chrome’s DevTools Lighthouse panel](https://developers.google.com/web/tools/lighthouse#devtools). If you open your site in Chrome and then open Chrome’s DevTools, you should see a “Lighthouse” tab. From there, if you click “Generate Report”, you should get a full report of your site’s quality metrics.

What I am focusing on in this article, however, is at the other end of the spectrum. Running Lighthouse programmatically with JavaScript allows us to configure custom runs, picking and choosing the features we want to test, collecting and analyzing results, and specifying configuration options unique to our sites and applications.

For example, perhaps you work on a site that is accessible through multiple URLs &mdash; each with its own data and styling and perhaps even markup that you want to be able to analyze. Or maybe you want to gather the data from each test run and compile or analyze it in different ways. Having the ability to choose how you want to run a Lighthouse analysis based on what works best for your site or application makes it easier to monitor site quality and pinpoint where there are issues with your site before they pile up or cause too many problems for your site’s users.

Running Lighthouse programmatically is not the best choice for every site and I encourage you to [explore all the different methods](https://developers.google.com/web/tools/lighthouse#get-started) the Lighthouse team has built for using the tool. If you decide to use Lighthouse programmatically, however, the information and tutorial below should hopefully get you started.

## Customizing Lighthouse Options

The advantage of running Lighthouse programmatically isn’t only the ability to configure Lighthouse itself, but rather all the things you might want or need to do around the Lighthouse tests. Lighthouse has some [great documentation](https://github.com/GoogleChrome/lighthouse/blob/master/docs/readme.md#using-programmatically) to get you started. To get the most out of running it programmatically, however, there are two main places where you will need to dig in and learn more about how Lighthouse works: configuring your test runs and reporting your test results.

### Lighthouse Test Run Configuration

Configuring a Lighthouse test run is one of those tasks that can be as simple or as complex as you like.

When running Lighthouse programmatically, there are three places where you can provide custom options: the URL you will be testing, Chrome options, and the Lighthouse configuration object. You can see all three of these are parameters in the function for running Lighthouse from the [Lighthouse documentation](https://github.com/GoogleChrome/lighthouse/blob/master/docs/readme.md#using-programmatically):

<div class="break-out">

<pre><code class="language-javascript">function launchChromeAndRunLighthouse(url, opts, config = null) {
  return chromeLauncher.launch({chromeFlags: opts.chromeFlags}).then(chrome =&gt; {
    opts.port = chrome.port;
    return lighthouse(url, opts, config).then(results =&gt; {
      return chrome.kill().then(() =&gt; results.lhr)
    });
  });
}</code></pre>
</div>

You can use whatever code you need in order to create these parameters. For example, say you have a site with multiple pages or URLs you would like to test. Maybe you want to run that test in a CI environment as part of your CI tasks, checking all necessary pages each time the task runs. Using this setup, you can use JavaScript to create your URLs and create a loop that will run Lighthouse for each one.

Any Chrome options you might need can be specified in an object that gets passed to [chrome-launcher](https://www.npmjs.com/package/chrome-launcher). In the example from the documentation, the `opts` object contains an array we’re calling `chromeFlags` that you can pass to chrome-launcher and a port where you can save the port being used by chrome-launcher and then pass it to Lighthouse.

Finally, the Lighthouse configuration object allows you to add any Lighthouse-specific options. The Lighthouse package provides a default configuration object that can be used as-is or extended and modified. You can use this object to do a multitude of things, including specifying which Lighthouse test categories you want to test.

{{% feature-panel %}}

You can use the `emulatedFormFactor` to specify whether you want the test to run in a mobile or desktop emulator. You can use `extraHeaders` to add any cookies you might need to use in the browser. For example, a test running only the accessibility category on a desktop emulator that outputs the results as HTML might have a configuration object that looks like this:

<pre><code class="language-javascript">const lighthouseOptions = {
  extends: 'lighthouse:default',
  settings: {
    onlyCategories: ['accessibility'],
    emulatedFormFactor:'desktop',
    output: ['html'],
  },
}</code></pre>  

This example represents a minimal configuration. There is a lot more you can do. The [Lighthouse configuration docs](https://github.com/GoogleChrome/lighthouse/blob/master/docs/configuration.md) have much more information. They also have a set of [sample configuration objects](https://github.com/GoogleChrome/lighthouse/tree/master/lighthouse-core/config) for some more complex implementations.

### Custom Results Reporting

When running Lighthouse programmatically, you can have the results returned in one or more of three formatted options and &mdash; and this is the most exciting piece in my opinion &mdash; you can have access to the raw Lighthouse Result (LHR) object.

### HTML, JSON, CSV

Lighthouse will automatically format the results in three different ways: HTML, JSON, or CSV. These are all pre-configured results based on the basic Lighthouse reporting template, which is what you see if you run a Lighthouse test inside of Chrome DevTools, for example. In the `lighthouseOptions` configuration object from the previous section, you can see a key for `output` that contains an array with a single string: `html`. This specifies that I only want the results returned formatted as HTML. If I wanted the results both as HTML and JSON, that array would look like `['html', 'json']`. 

Once Lighthouse has run, it will return a results object that will contain two keys: `report` and `lhr`. We’ll talk about the contents of the `lhr` key in the next section, but the `report` key contains an array with the results formatted as you have requested. So, for example, if we have requested `['html', 'json']`, then `results.report[0]` will contain our results formatted as HTML and `results.report[1]` will contain our results formatted as JSON.

### The LHR Object

Running Lighthouse programmatically also gives you access to a much more flexible results object: the LHR object. This object contains the raw results and some metadata from your Lighthouse run. More complete documentation can be found on the [Lighthouse Github repository](https://github.com/GoogleChrome/lighthouse/blob/master/docs/understanding-results.md).

You can use these results in any number of ways, including creating custom reports and collecting data from multiple runs for analysis.

{{% ad-panel-leaderboard %}}

## Example: Running An Accessibility Test For Mobile And Desktop

Let’s say that I have a site that loads different components depending on whether the user is using a smaller screen or a larger one, meaning that the HTML for each version of the site will be slightly different. I want to make sure that both versions of the site get a score of 95 on the Lighthouse accessibility tests and that no code gets committed to our `main` branch that doesn’t meet that standard.

**Note**: *If you want to see a working example of the code below analyzing the [Sparkbox](https://seesparkbox.com/) homepage, you can find the repository [here](https://github.com/smashingmagazine/lighthouse-example).*

I can configure Lighthouse to run the accessibility category twice, providing different configuration objects for each one &mdash; one setting the `emulatedFormFactor` to `desktop` and one setting it to `mobile`. An easy way to do this is to create an array with both objects, shown below.

<pre><code class="language-javascript">const lighthouseOptionsArray = [
  {
    extends: 'lighthouse:default',
    settings: {
      onlyCategories: ['accessibility'],
      emulatedFormFactor:'desktop',
      output: ['html', 'json'],
    },
  },
  {
    extends: 'lighthouse:default',
    settings: {
      onlyCategories: ['accessibility'],
      emulatedFormFactor:'mobile',
      output: ['html', 'json'],
    },
  },
]</code></pre>

Then, I can create a function that will loop through this array and run a Lighthouse test for each object found inside the array. 

One thing to note is that it is necessary to introduce a delay between each run, otherwise Chromium can get confused and the runs will error out. In order to do this, I’ve added a `wait` function that returns a promise when the `setTimeout` interval has completed.

<div class="break-out">

<pre><code class="language-javascript">function wait(val) {
  return new Promise(resolve =&gt; setTimeout(resolve, val));
}

function launchLighthouse(optionSet, opts, results) {
  return chromeLauncher
    .launch({ chromeFlags: opts.chromeFlags })
    .then(async chrome =&gt; {
      opts.port = chrome.port;
      try {
        results = await lighthouse(url, opts, optionSet);
      } catch (e) {
        console.error("lighthouse", e);
      }
      if (results) reportResults(results, runEnvironment, optionSet, chrome);
      await wait(500);
      chrome.kill();
    });
}

async function runLighthouseAnalysis() {
  let results;
  const opts = {
    chromeFlags: ["--no-sandbox", "--headless"]
  };
  for (const optionSet of lighthouseOptionsArray) {
    console.log("****** Starting Lighthouse analysis ******");
    await launchLighthouse(optionSet, opts, results);
  }
}</code></pre>
</div>


In this case, I am sending the results to a `reportResults` function. From there, I save the results to local files, print results to the console, and send the results to a function that will determine if the tests pass or fail our accessibility threshold. 

<div class="break-out">

<pre><code class="language-javascript">async function reportResults(results, runEnvironment, optionSet, chrome) {
  if (results.lhr.runtimeError) {
    return console.error(results.lhr.runtimeError.message);
  }
  await writeLocalFile(results, runEnvironment, optionSet);
  printResultsToTerminal(results.lhr, optionSet);
  return passOrFailA11y(results.lhr, optionSet, chrome);
}</code></pre>
</div>

For this project, I want to be able to save the JSON results in a specified directory for our CI test runs and the HTML file in a specified directory for our local test runs. The way Lighthouse returns these different types of results is in an array in the order in which they were requested.

{{% ad-panel-leaderboard %}}

So, in this example, in our `lighthouseOptions` object, our array asks for HTML first, then JSON. So the `report` array will contain the HTML-formatted results first and the JSON-formatted results second. The `writeToLocalFile` function then saves the correct version of the results in a file with a customized name.

<div class="break-out">

<pre><code class="language-javascript">function createFileName(optionSet, fileType) {
  const { emulatedFormFactor } = optionSet.settings;
  const currentTime = new Date().toISOString().slice(0, 16);
  const fileExtension = fileType === 'json' ? 'json' : 'html';
  return `${currentTime}-${emulatedFormFactor}.${fileExtension}`;
}

function writeLocalFile(results, runEnvironment, optionSet) {
  if (results.report) {
    const fileType = runEnvironment === 'ci' ? 'json' : 'html';
    const fileName = createFileName(optionSet, fileType);
    fs.mkdirSync('reports/accessibility/', { recursive: true }, error =&gt; {
      if (error) console.error('error creating directory', error);
    });
    const printResults = fileType === 'json' ? results.report[1] : results.report[0];
    return write(printResults, fileType, `reports/accessibility/${fileName}`).catch(error =&gt; console.error(error));
  }
  return null;
}</code></pre>
</div>

I also want to print the results to the terminal as the test runs finish. This provides a quick and easy way to view the results without having to open a file.

<div class="break-out">

<pre><code class="language-javascript">function printResultsToTerminal(results, optionSet) {
  const title = results.categories.accessibility.title;
  const score = results.categories.accessibility.score * 100;
  console.log('\n********************************\n');
  console.log(`Options: ${optionSet.settings.emulatedFormFactor}\n`);
  console.log(`${title}: ${score}`);
  console.log('\n********************************');
}</code></pre>
</div>

And finally, I want to be able to fail my test runs if the accessibility scores do not meet my threshold score of 95.

<div class="break-out">

<pre><code class="language-javascript">function passOrFailA11y(results, optionSet, chrome) {
  const targetA11yScore =  95;
  const { windowSize } = optionSet;
  const accessibilityScore = results.categories.accessibility.score * 100;
  if (accessibilityScore) {
    if (windowSize === 'desktop') {
      if (accessibilityScore &lt; targetA11yScore) {
        console.error(`Target accessibility score: ${targetA11yScore}, current accessibility score ${accessibilityScore}`);
        chrome.kill();
        process.exitCode = 1;
      }
    }
    if (windowSize === 'mobile') {
      if (accessibilityScore < targetA11yScore) {
        console.error(`Target accessibility score: ${targetA11yScore}, current accessibility score ${accessibilityScore}`);
        chrome.kill();
        process.exitCode = 1;
      }
    }
  }
}</code></pre>
</div>

I invite you all to play around with it and explore all the different ways Lighthouse can help monitor your site quality. 

## Final Notes

While I intentionally kept the example above relatively simple, I hope it gave you a good overview of what can be accomplished when running Lighthouse programmatically. And I hope it inspires you to find new ways to use this flexible, powerful tool.

As Peter Drucker said:

<blockquote>“If you can’t measure it, you can’t improve it.”</blockquote>

Being able to not only measure but monitor our website quality, especially for complex sites, will go a long way towards helping us build a better web.

### <span class="rh">Further Reading</span> on SmashingMag:

<ul>
<li><a title="Read 'A/B Testing For Mobile-First Experiences'" href="https://www.smashingmagazine.com/2019/02/testing-mobile-first-experiences/" rel="bookmark">A/B Testing For Mobile-First Experiences</a></li>
<li><a title="Read 'How To Test A Design Concept For Effectiveness'" href="https://www.smashingmagazine.com/2020/06/test-design-concept-effectiveness/" rel="bookmark">How To Test A Design Concept For Effectiveness</a></li>
<li><a title="Read 'The Importance Of Manual Accessibility Testing'" href="https://www.smashingmagazine.com/2018/09/importance-manual-accessibility-testing/" rel="bookmark">The Importance Of Manual Accessibility Testing</a></li>
<li><a title="Read 'Machine Learning For Front-End Developers With Tensorflow.js'" href="https://www.smashingmagazine.com/2019/09/machine-learning-front-end-developers-tensorflowjs/" rel="bookmark">Machine Learning For Front-End Developers With Tensorflow.js</a></li>
<li><a title="Read 'Get Started With UI Design With These Tips To Speed Up Your Workflow'" href="https://www.smashingmagazine.com/2019/12/ui-design-tips-speed-up-workflow/" rel="bookmark">Get Started With UI Design With These Tips To Speed Up Your Workflow</a></li>
</ul>

{{% newsletter-panel %}}

{{< signature "ra, yk, il" >}}
