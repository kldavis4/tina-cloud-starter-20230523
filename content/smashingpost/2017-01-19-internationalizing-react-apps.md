---
title: React Internationalization – How To
slug: internationalizing-react-apps
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ab72b18a-f196-4be0-94f4-2713b114e8a1/intl-browser-support-500w-opt.png
date: 2017-01-19T20:38:38.000Z
author: yurydymov
summary: >-
  How can we build an internationalized React front-end application? With the help of this article, you can learn how to detect the user’s locale, save it in the cookie, let the user change their locale, translate the user interface, and render currencies in their appropriate formats. Also, Yury has you prepared with a list of some traps and issues you might face along the way.
description: >-
  How can we build an internationalized React front-end application? With the help of this article, you can prepare yourself with a list of traps and issues you may face along the way.
categories:
  - Coding
  - React
---
First of all, let’s define some vocabulary. “Internationalization” is a long word, and there are at least two widely used abbreviations: “intl,” “i18n”. “Localization” can be shortened to “l10n”.

Internationalization can be generally broken down into three main challenges: Detecting the user’s locale, translating UI elements, titles as well as hints, and last but not least, serving locale-specific content such as dates, currencies and numbers. In this article, I am going to focus only on front-end part. We’ll develop a simple universal React application with full internationalization support.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ab72b18a-f196-4be0-94f4-2713b114e8a1/intl-browser-support-500w-opt.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ab72b18a-f196-4be0-94f4-2713b114e8a1/intl-browser-support-500w-opt.png" sizes="100vw" caption="" alt="Internationalizing React Apps" >}}

Internationalization can be generally broken down into the following challenges:

- detecting the user’s locale;
- translating UI elements, titles and hints;
- serving locale-specific content such as dates, currencies and numbers.

**>Note**: *In this article, I am going to focus only on front-end part. We’ll develop a simple universal React application with full internationalization support.*

{{% feature-panel %}}

Let’s use <a href="https://github.com/yury-dymov/smashing-react-i18n">my boilerplate repository</a> as a starting point. Here we have the Express web server for server-side rendering, webpack for building client-side JavaScript, Babel for translating modern JavaScript to ES5, and React for the UI implementation. We’ll use better-npm-run to write OS-agnostic scripts, nodemon to run a web server in the development environment and webpack-dev-server to serve assets.

Our entry point to the server application is <code>server.js</code>. Here, we are loading Babel and babel-polyfill to write the rest of the server code in modern JavaScript. Server-side business logic is implemented in <code>src/server.jsx</code>. Here, we are setting up an Express web server, which is listening to port <code>3001</code>. For rendering, we are using a very simple component from <code>components/App.jsx</code>, which is also a universal application part entry point.

Our entry point to the client-side JavaScript is <code>src/client.jsx</code>. Here, we mount the root component <code>component/App.jsx</code> to the placeholder <code>react-view</code> in the HTML markup provided by the Express web server.

So, clone the repository, run <code>npm install</code> and execute nodemon and webpack-dev-server in two console tabs simultaneously.

In the first console tab:

<div class="break-out">

 <pre><code class="language-bash">git clone https://github.com/yury-dymov/smashing-react-i18n.git cd smashing-react-i18n  npm install npm run nodemon
</code></pre>
</div>

And in the second console tab:

<pre><code class="language-bash">cd smashing-react-i18n  npm run webpack-devserver
</code></pre>

A website should become <a href="https://localhost:3001">available at <code>localhost:3001</code></a>. Open your favorite browser and try it out.

We are ready to roll!

## 1. Detecting The User’s Locale

There are two possible solutions to this requirement. For some reason, most popular websites, including Skype’s and the NBA's, use Geo IP to find the user’s location and, based on that, to guess the user’s language. This approach is not only expensive in terms of implementation, but also not really accurate. Nowadays, people travel a lot, which means that a location doesn’t necessarily represent the user’s desired locale. Instead, we’ll use the second solution and process the HTTP header <code>Accept-Language</code> on the server side and extract the user’s language preferences based on their system’s language settings. This header is sent by every modern browser within a page request.

### Accept-Language Request Header

The <code>Accept-Language</code> request header provides the set of natural languages that are preferred as a response to the request. Each language range may be given an associated "quality" value, which represents an estimate of the user’s preference for the languages specified by that range. The quality value defaults to <code>q=1</code>. For example, <code>Accept-Language: da, en-gb;q=0.8, en;q=0.7</code> would mean, "I prefer Danish, but will accept British English and other types of English." A language range matches a language tag if it exactly equals the tag or if it exactly equals a prefix of the tag such that the first tag character following the prefix is <code>-</code>.

(It is worth mentioning that this method is still imperfect. For example, a user might visit your website from an Internet cafe or a public computer. To resolve this, always implement a widget with which the user can change the language intuitively and that they can easily locate within a few seconds.)

### Implementing Detection Of User’s Locale

Here is a code example for a Node.js Express web server. We are using the <code>accept-language</code> package, which extracts locales from HTTP headers and finds the most relevant among the ones supported by your website. If none are found, then you'd fall back to the website’s default locale. For returning users, we will check the cookie’s value instead.

Let’s start by installing the packages:

<div class="break-out">

 <pre><code class="language-bash">npm install --save accept-language  npm install --save cookie-parser js-cookie
</code></pre>
</div>

And in <code>src/server.jsx</code>, we'd have this:

<div class="break-out">

 <pre><code class="language-javascript">import cookieParser from 'cookie-parser';
import acceptLanguage from 'accept-language';

acceptLanguage.languages(['en', 'ru']);

const app = express();

app.use(cookieParser());

function detectLocale(req) {
  const cookieLocale = req.cookies.locale;

  return acceptLanguage.get(cookieLocale || req.headers['accept-language']) || 'en';
}
…

app.use((req, res) =&gt; {
  const locale = detectLocale(req);
  const componentHTML = ReactDom.renderToString(&lt;App /&gt;);

  res.cookie('locale', locale, { maxAge: (new Date() * 0.001) + (365 * 24 * 3600) });
  return res.end(renderHTML(componentHTML));
});
</code></pre>
</div>

Here, we are importing the <code>accept-language</code> package and setting up English and Russian locales as supported. We are also implementing the <code>detectLocale</code> function, which fetches a locale value from a cookie; if none is found, then the HTTP <code>Accept-Language</code> header is processed. Finally, we are falling back to the default locale (<code>en</code> in our example). After the request is processed, we add the HTTP header <code>Set-Cookie</code> for the locale detected in the response. This value will be used for all subsequent requests.

{{% ad-panel-leaderboard %}}

## 2. Translating UI Elements, Titles And Hints

I am going to use the <a href="https://github.com/yahoo/react-intl">React Intl</a> package for this task. It is the most popular and battle-tested i18n implementation of React apps. However, all libraries use the same approach: They provide "higher-order components" (from the <a href="https://medium.com/@franleplant/react-higher-order-components-in-depth-cf9032ee6c3e#.zb3t19yyx">functional programming design pattern</a>, widely used in React), which injects internationalization functions for handling messages, dates, numbers and currencies via React’s context features.

First, we have to set up the internationalization provider. To do so, we will slightly change the <code>src/server.jsx</code> and <code>src/client.jsx</code> files.

<pre><code class="language-bash">npm install --save react-intl
</code></pre>

Here is <code>src/server.jsx</code>:

<pre><code class="language-javascript">import { IntlProvider } from 'react-intl';

…
--- const componentHTML = ReactDom.renderToString(&lt;App /&gt;);
const componentHTML = ReactDom.renderToString(
  &lt;IntlProvider locale={locale}&gt;
    &lt;App /&gt;
  &lt;/IntlProvider&gt;
);
…
</code></pre>

And here is <code>src/client.jsx</code>:

<div class="break-out">

 <pre><code class="language-javascript">import { IntlProvider } from 'react-intl';
import Cookie from 'js-cookie';

const locale = Cookie.get('locale') || 'en';
…
---  ReactDOM.render(&lt;App /&gt;, document.getElementById('react-view'));
ReactDOM.render(
  &lt;IntlProvider locale={locale}&gt;
    &lt;App /&gt;
  &lt;/IntlProvider&gt;,
  document.getElementById('react-view')
);
</code></pre>
</div>

So, now all <code>IntlProvider</code> child components will have access to internationalization functions. Let’s add some translated text to our application and a button to change the locale (for testing purposes). We have two options: either the <code>FormattedMessage</code> component or the <code>formatMessage</code> function. The difference is that the component will be wrapped in a <code>span</code> tag, which is fine for text but not suitable for HTML attribute values such as <code>alt</code> and <code>title</code>. Let’s try them both!

Here is our <code>src/components/App.jsx</code> file:

<div class="break-out">

 <pre><code class="language-javascript">import { FormattedMessage } from 'react-intl';
…
--- &lt;h1&gt;Hello World!&lt;/h1&gt;
&lt;h1&gt;&lt;FormattedMessage id="app.hello_world" defaultMessage="Hello World!" description="Hello world header greeting" /&gt;&lt;/h1&gt;
</code></pre>
</div>

Please note that the <code>id</code> attribute should be unique for the whole application, so it makes sense to develop some rules for naming your messages. I prefer to follow the format <code>componentName.someUniqueIdWithInComponent</code>. The <code>defaultMessage</code> value will be used for your application’s default locale, and the <code>description</code> attribute gives some context to the translator.

Restart nodemon and refresh the page in your browser. You should still see the "Hello World" message. But if you open the page in the developer tools, you will see that text is now inside the <code>span</code> tags. In this case, it isn’t an issue, but sometimes we would prefer to get just the text, without any additional tags. To do so, we need direct access to the internationalization object provided by React Intl.

Let’s go back to <code>src/components/App.jsx</code>:

<div class="break-out">

 <pre><code class="language-javascript">
--- import { FormattedMessage } from 'react-intl';
import { FormattedMessage, intlShape, injectIntl, defineMessages } from 'react-intl';

const propTypes = {
  intl: intlShape.isRequired,
};

const messages = defineMessages({
  helloWorld2: {
    id: 'app.hello_world2',
    defaultMessage: 'Hello World 2!',
  },
});

--- export default class extends Component {
class App extends Component {
  render() {
    return (
      &lt;div className="App"&gt;
        &lt;h1&gt;
          &lt;FormattedMessage
            id="app.hello_world"
            defaultMessage="Hello World!"
            description="Hello world header greeting"
          /&gt;
        &lt;/h1&gt;
        &lt;h1&gt;{this.props.intl.formatMessage(messages.helloWorld2)}&lt;/h1&gt;
      &lt;/div&gt;
    );
  }
}

App.propTypes = propTypes;

export default injectIntl(App);

</code></pre>
</div>

We’ve had to write a lot more code. First, we had to use <code>injectIntl</code>, which wraps our app component and injects the <code>intl</code> object. To get the translated message, we had to call the <code>formatMessage</code> method and pass a <code>message</code> object as a parameter. This <code>message</code> object must have unique <code>id</code> and <code>defaultValue</code> attributes. We use <code>defineMessages</code> from React Intl to define such objects.

The best thing about React Intl is its ecosystem. Let’s add babel-plugin-react-intl to our project, which will extract <code>FormattedMessages</code> from our components and build a translation dictionary. We will pass this dictionary to the translators, who won’t need any programming skills to do their job.

<pre><code class="language-bash">npm install --save-dev babel-plugin-react-intl
</code></pre>

Here is <code>.babelrc</code>:

<pre><code class="language-javascript">{
  "presets": [
    "es2015",
    "react",
    "stage-0"
  ],
  "env": {
    "development": {
      "plugins":[
        ["react-intl", {
          "messagesDir": "./build/messages/"
        }]
      ]
    }
  }
}
</code></pre>

Restart nodemon and you should see that a <code>build/messages</code> folder has been created in the project’s root, with some folders and files inside that mirror your JavaScript project’s directory structure. We need to merge all of these files into one JSON. Feel free to <a href="https://github.com/yury-dymov/smashing-react-i18n/blob/solution/scripts/translate.js">use my script</a>. Save it as <code>scripts/translate.js</code>.

Now, we need to add a new script to <code>package.json</code>:

<pre><code class="language-javascript">"scripts": {
  …
  "build:langs": "babel scripts/translate.js | node",
  …
}
</code></pre>

Let’s try it out!

<pre><code class="language-bash">npm run build:langs
</code></pre>

You should see an <code>en.json</code> file in the <code>build/lang</code> folder with the following content:

<pre><code class="language-javascript">{
  "app.hello_world": "Hello World!",
  "app.hello_world2": "Hello World 2!"
}
</code></pre>

It works! Now comes interesting part. On the server side, we can load all translations into memory and serve each request accordingly. However, for the client side, this approach is not applicable. Instead, we will send the JSON file with translations once, and a client will automatically apply the provided text for all of our components, so the client gets only what it needs.

Let’s copy the output to the <code>public/assets</code> folder and also provide some translation.

<pre><code class="language-bash">ln -s ../../build/lang/en.json public/assets/en.json
</code></pre>

<strong>Note:</strong> If you are a Windows user, symlinks are not available to you, which means you have to manually copy the command below every time you rebuild your translations:

<pre><code class="language-bash">cp ../../build/lang/en.json public/assets/en.json
</code></pre>

In <code>public/assets/ru.json</code>, we need the following:

<pre><code class="language-javascript">{
  "app.hello_world": "Привет мир!",
  "app.hello_world2": "Привет мир 2!"
}
</code></pre>

Now we need to adjust the server and client code.

For the server side, our <code>src/server.jsx</code> file should look like this:

<div class="break-out">

 <pre><code class="language-javascript">--- import { IntlProvider } from 'react-intl';
import { addLocaleData, IntlProvider } from 'react-intl';
import fs from 'fs';
import path from 'path';

import en from 'react-intl/locale-data/en';
import ru from 'react-intl/locale-data/ru';

addLocaleData([…ru, …en]);

const messages = {};
const localeData = {};

['en', 'ru'].forEach((locale) =&gt; {
  localeData[locale] = fs.readFileSync(path.join(&#95;&#95;dirname, '../node_modules/react-intl/locale-data/${locale}.js')).toString();
  messages[locale] = require('../public/assets/${locale}.json');
});

--- function renderHTML(componentHTML) {
function renderHTML(componentHTML, locale) {
…
      &lt;script type="application/javascript" src="${assetUrl}/public/assets/bundle.js"&gt;&lt;/script&gt;
      &lt;script type="application/javascript"&gt;${localeData[locale]}&lt;/script&gt;

…

--- &lt;IntlProvider locale={locale}&gt;
&lt;IntlProvider locale={locale} messages={messages[locale]}&gt;
…
---  return res.end(renderHTML(componentHTML));
return res.end(renderHTML(componentHTML, locale));
</code></pre>
</div>

Here we are doing the following:

*   caching messages and locale-specific JavaScript for the currency, `DateTime` and `Number` formatting during startup (to ensure good performance);
*   extending the `renderHTML` method so that we can insert locale-specific JavaScript into the generated HTML markup;
*   providing the translated messages to `IntlProvider` (all of those messages are now available to child components).

For the client side, first we need to install a library to perform AJAX requests. I prefer to use isomorphic-fetch because we will very likely also need to request data from third-party APIs, and isomorphic-fetch can do that very well in both client and server environments.

<pre><code class="language-bash">npm install --save isomorphic-fetch
</code></pre>

Here is <code>src/client.jsx</code>:

<pre><code class="language-javascript">--- import { IntlProvider } from 'react-intl';
import { addLocaleData, IntlProvider } from 'react-intl';
import fetch from 'isomorphic-fetch';

const locale = Cookie.get('locale') || 'en';

fetch(`/public/assets/${locale}.json`)
  .then((res) =&gt; {
    if (res.status &gt;= 400) {
      throw new Error('Bad response from server');
    }

    return res.json();
  })
  .then((localeData) =&gt; {
    addLocaleData(window.ReactIntlLocaleData[locale]);

    ReactDOM.render(
---        &lt;IntlProvider locale={locale}&gt;
      &lt;IntlProvider locale={locale} messages={localeData}&gt;
…
    );
}).catch((error) =&gt; {
  console.error(error);
});

</code></pre>

We also need to tweak <code>src/server.jsx</code>, so that Express serves the translation JSON files for us. Note that in production, you would use something like <code>nginx</code> instead.

<pre><code class="language-javascript">app.use(cookieParser());
app.use('/public/assets', express.static('public/assets'));
</code></pre>

After the JavaScript is initialized, <code>client.jsx</code> will grab the locale from the cookie and request the JSON file with the translations. Afterwards, our single-page application will work as before.

Time to check that everything works fine in the browser. Open the "Network" tab in the developer tools, and check that JSON has been successfully fetched by our client.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/69db50e7-e1a7-4f1e-9a28-7afd70eeb046/ajax-request-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d7cb0aac-f12f-442a-9b64-a9397c2c7dd3/ajax-request-780w-opt.png" alt="react internationalization" width="780" height="450" /></a><figcaption>AJAX request (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/69db50e7-e1a7-4f1e-9a28-7afd70eeb046/ajax-request-large-opt.png">View large version</a>)</figcaption></figure>

To finish this part, let’s add a simple widget to change the locale, in <code>src/components/LocaleButton.jsx</code>:

<div class="break-out">

 <pre><code class="language-javascript">import React, { Component, PropTypes } from 'react';
import Cookie from 'js-cookie';

const propTypes = {
  locale: PropTypes.string.isRequired,
};

class LocaleButton extends Component {
  constructor() {
    super();

    this.handleClick = this.handleClick.bind(this);
  }

  handleClick() {
    Cookie.set('locale', this.props.locale === 'en' ? 'ru' : 'en');
    window.location.reload();
  }

  render() {
    return &lt;button onClick={this.handleClick}&gt;{this.props.locale === 'en' ? 'Russian' : 'English'};
  }
}

LocaleButton.propTypes = propTypes;

export default LocaleButton;

</code></pre>
</div>

Add the following to <code>src/components/App.jsx</code>:

<pre><code class="language-javascript">import LocaleButton from './LocaleButton';

…

    &lt;h1&gt;{this.props.intl.formatMessage(messages.helloWorld2)}&lt;/h1&gt;
    &lt;LocaleButton locale={this.props.intl.locale} /&gt;

</code></pre>

Note that once the user changes their locale, we’ll reload the page to ensure that the new JSON file with the translations is fetched.

High time to test! OK, so we’ve learned how to detect the user’s locale and how to show translated messages. Before moving to the last part, let’s discuss two other important topics.

{{% ad-panel-leaderboard %}}

### Pluralization And Templates

In English, most words take one of two possible forms: "one apple," "many apples." In other languages, things are a lot more complicated. For example, Russian has four different forms. Hopefully, React Intl will help us to handle pluralization accordingly. It also supports templates, so you can provide variables that will be inserted into the template during rendering. Here’s how it works.

In <code>src/components/App.jsx</code>, we have the following:

<div class="break-out">

 <pre><code class="language-javascript">const messages = defineMessages({
  counting: {
    id: 'app.counting',
    defaultMessage: 'I need to buy {count, number} {count, plural, one {apple} other {apples}}'
  },

…

    &lt;LocaleButton locale={this.props.intl.locale} /&gt;
    &lt;div&gt;{this.props.intl.formatMessage(messages.counting, { count: 1 })}&lt;/div&gt;
    &lt;div&gt;{this.props.intl.formatMessage(messages.counting, { count: 2 })}&lt;/div&gt;
    &lt;div&gt;{this.props.intl.formatMessage(messages.counting, { count: 5 })}&lt;/div&gt;
</code></pre>
</div>

Here, we are defining a template with the variable <code>count</code>. We will print either "1 apple" if <code>count</code> is equal to <code>1, 21</code>, etc. or "2 apples" otherwise. We have to pass all variables within <code>formatMessage</code>’s <code>values</code> option.

Let’s rebuild our translation file and add the Russian translations to check that we can provide more than two variants for languages other than English.

<pre><code class="language-bash">npm run build:langs
</code></pre>

Here is our <code>public/assets/ru.json</code> file:

<div class="break-out">

 <pre><code class="language-javascript">{
  …
  "app.counting": "Мне нужно купить {count, number} {count, plural, one {яблоко} few {яблока} many {яблок}}"
}
</code></pre>
</div>

All use cases are covered now. Let’s move forward!

## 3. Serving Locale-Specific Content Such As Dates, Currencies And Numbers

Your data will be represented differently depending on the locale. For example, Russian would show <code>500,00 $</code> and <code>10.12.2016</code>, whereas US English would show <code>$500.00</code> and <code>12/10/2016</code>.

React Intl provides React components for such kinds of data and also for the relative rendering of time, which will automatically be updated each 10 seconds if you do not override the default value.

Add this to <code>src/components/App.jsx</code>:

<div class="break-out">

 <pre><code class="language-javascript">--- import { FormattedMessage, intlShape, injectIntl, defineMessages } from 'react-intl';
import {
  FormattedDate,
  FormattedRelative,
  FormattedNumber,
  FormattedMessage,
  intlShape,
  injectIntl,
  defineMessages,
} from 'react-intl';

…

&lt;div&gt;{this.props.intl.formatMessage(messages.counting, { count: 5 })}&lt;/div&gt;
&lt;div&gt;&lt;FormattedDate value={Date.now()} /&gt;&lt;/div&gt;
&lt;div&gt;&lt;FormattedNumber value="1000" currency="USD" currencyDisplay="symbol" style="currency" /&gt;&lt;/div&gt;
&lt;div&gt;&lt;FormattedRelative value={Date.now()} /&gt;&lt;/div&gt;
</code></pre>
</div>

Refresh the browser and check the page. You’ll need to wait for 10 seconds to see that the <code>FormattedRelative</code> component has been updated.

You’ll find a lot more examples in the <a href="https://github.com/yahoo/react-intl/wiki/Components">official wiki</a>.

Cool, right? Well, now we might face another problem, which affects universal rendering.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/36e97f3e-cf6f-43b8-91c4-c8b007a69133/universal-rendering-is-broken-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9eb1b1c7-1467-4882-be40-9801c47c3ba6/universal-rendering-is-broken-780w-opt.png" alt="Universal rendering is broken" width="780" height="424" /></a><figcaption>Universal rendering is broken. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/36e97f3e-cf6f-43b8-91c4-c8b007a69133/universal-rendering-is-broken-large-opt.png">View large version</a>)</figcaption></figure>

On average, two seconds will elapse between when the server provides markup to the client and the client initializes client-side JavaScript. This means that all <code>DateTimes</code> rendered on the page might have different values on the server and client sides, which, by definition, breaks universal rendering. To resolve this, React Intl provides a special attribute, <code>initialNow</code>. This provides a server timestamp that will initially be used by client-side JavaScript as a timestamp; this way, the server and client checksums will be equal. After all components have been mounted, they will use the browser’s current timestamp, and everything will work properly. So, this trick is used only to initialize client-side JavaScript, in order to preserve universal rendering.

Here is <code>src/server.jsx</code>:

<div class="break-out">

 <pre><code class="language-javascript">--- function renderHTML(componentHTML, locale) {
function renderHTML(componentHTML, locale, initialNow) {
  return `
    &lt;!DOCTYPE html&gt;
      &lt;html&gt;
      &lt;head&gt;
          &lt;meta charset="utf-8"&gt;
          &lt;meta name="viewport" content="width=device-width, initial-scale=1.0"&gt;
          &lt;title&gt;Hello React&lt;/title&gt;
      &lt;/head&gt;
      &lt;body&gt;
        &lt;div id="react-view"&gt;${componentHTML}&lt;/div&gt;
        &lt;script type="application/javascript" src="${assetUrl}/public/assets/bundle.js"&gt;&lt;/script&gt;
        &lt;script type="application/javascript"&gt;${localeData[locale]}&lt;/script&gt;
        &lt;script type="application/javascript"&gt;window.INITIAL_NOW=${JSON.stringify(initialNow)}&lt;/script&gt;
      &lt;/body&gt;
    &lt;/html&gt;
  `;
}

    const initialNow = Date.now();
    const componentHTML = ReactDom.renderToString(
---   &lt;IntlProvider locale={locale} messages={messages[locale]}&gt;
      &lt;IntlProvider initialNow={initialNow} locale={locale} messages={messages[locale]}&gt;
        &lt;App /&gt;
      &lt;/IntlProvider&gt;
    );

    res.cookie('locale', locale, { maxAge: (new Date() * 0.001) + (365 * 24 * 3600) });
---   return res.end(renderHTML(componentHTML, locale));
    return res.end(renderHTML(componentHTML, locale, initialNow));

</code></pre>
</div>

And here is <code>src/client.jsx</code>:

<div class="break-out">

 <pre><code class="language-javascript">--- &lt;IntlProvider locale={locale} messages={localeData}&gt;
&lt;IntlProvider initialNow={parseInt(window.INITIAL_NOW, 10)} locale={locale} messages={localeData}&gt;
</code></pre>
</div>

Restart nodemon, and the issue will almost be gone! It might persist because we are using <code>Date.now()</code>, instead of some timestamp provided by the database. To make the example more realistic, in <code>app.jsx</code> replace <code>Date.now()</code> with a recent timestamp, like <code>1480187019228</code>.

(You might face another issue when the server is not able to render the <code>DateTime</code> in the proper format, which will also break universal rendering. This is because version 4 of Node.js is not built with Intl support by default. To resolve this, follow one of the solutions <a href="https://github.com/nodejs/node/wiki/Intl">described in the official wiki</a>.)

## 4\. A Problem

It sounds too good to be true so far, doesn’t it? We as front-end developers always have to be very cautious about anything, given the variety of browsers and platforms. React Intl uses the native Intl browser API for handling the <code>DateTime</code> and <code>Number</code> formats. Despite the fact that it was introduced in 2012, it is still not supported by all modern browsers. Even Safari supports it partially only since iOS 10. Here is the whole table from CanIUse for reference.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/362eaa4f-1cac-464e-91aa-35e6a08b9459/intl-browser-support-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ae3d925d-994b-4622-a058-4e3f225022bf/intl-browser-support-780w-opt.png" alt="Internationalization browser support" width="780" height="316" /></a><figcaption>Intl browser support (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/362eaa4f-1cac-464e-91aa-35e6a08b9459/intl-browser-support-large-opt.png">View large version</a>)</figcaption></figure>

This means that if you are willing to cover a minority of browsers that don’t support the Intl API natively, then you’ll need a polyfill. Thankfully, there is one, <a href="https://github.com/andyearnshaw/Intl.js">Intl.js</a>. It might sound like a perfect solution once again, but from my experience, it has its own drawbacks. First of all, you’ll need to add it to the JavaScript bundle, and it is quite heavy. You’ll also want to deliver the polyfill only to browsers that don’t support the Intl API natively, to reduce your bundle size. All of these techniques are well known, and you might find them, along with how to do it with webpack, in <a href="https://github.com/andyearnshaw/Intl.js/">Intl.js' documentation</a>. However, the biggest issue is that Intl.js is not 100% accurate, which means that the <code>DataTime</code> and <code>Number</code> representations might differ between the server and client, which will break server-side rendering once again. Please refer to the <a href="https://github.com/andyearnshaw/Intl.js/issues/124">relevant GitHub issue</a> for more details.

I’ve come up with another solution, which certainly has its own drawbacks, but it works fine for me. I implemented a very shallow <a href="https://github.com/yury-dymov/intl-polyfill">polyfill</a>, which has only one piece of functionality. While it is certainly unusable for many cases, it adds only 2 KB to the bundle’s size, so there is not even any need to implement dynamic code-loading for outdated browsers, which makes the overall solution simpler. Feel free to fork and extend it if you think this approach would work for you.

## Conclusion

Well, now you might feel that things are becoming too complicated, and you might be tempted to implement everything yourself. I did that once; I wouldn’t recommend it. Eventually, you will arrive at the same ideas behind React Intl’s implementation, or, worse, you might think there are not many options to make certain things better or to do things differently.

You might think you can solve the Intl API support issue by relying on <a href="https://momentjs.com/">Moment.js</a> instead (I won’t mention other libraries with the same functionality because they are either unsupported or unusable). Fortunately, I tried that, so I can save you a <em>lot</em> of time. I’ve learned that Moment.js is a monolith and very heavy, so while it might work for some folks, I wouldn’t recommend it.

Developing your own polyfill doesn’t sound great because you will surely have to fight with bugs and support the solution for quite some time. The bottom line is that there is no perfect solution at the moment, so choose the one that suits you best.

(If you feel lost at some point or something doesn’t work as expected, check the "solution" branch of <a href="https://github.com/yury-dymov/smashing-react-i18n/tree/solution">my repository</a>.)

Hopefully, this article has given you all of the knowledge needed to build an internationalized React front-end application. You should now know how to detect the user’s locale, save it in the cookie, let the user change their locale, translate the user interface, and render currencies, <code>DateTimes</code> and <code>Number</code>s in the appropriate formats! You should also now be aware of some traps and issues you might face, so choose the option that fits your requirements, bundle-size budget and number of languages to support.

### <span class="rh">Further Reading</span> on SmashingMag:

*   [Why You Should Consider React Native For Your Mobile App](https://www.smashingmagazine.com/2016/04/consider-react-native-mobile-app/)
*   [How To Scale React Applications](https://www.smashingmagazine.com/2016/09/how-to-scale-react-applications/)
*   [Building Your First iOS App With JavaScript](https://www.smashingmagazine.com/2016/04/the-beauty-of-react-native-building-your-first-ios-app-with-javascript-part-1/)

{{< signature "rb, al, il, vf" >}}

