---
title: 'React Native For Web: A Glimpse Into The Future'
slug: a-glimpse-into-the-future-with-react-native-for-web
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bd6a598b-cccd-4503-9846-7b7cffbb6a0f/08-react-native-friends-2-web-preview-opt.png
date: 2016-08-08T18:13:28.000Z
author: claytonanderson
description: >-
  One of the hardest decisions to make when starting a new app is which
  platforms to target. A mobile app gives you more control and better
  performance but isn’t as universal as the web. If you’re making a mobile app,
  **can you afford to support both iOS and Android?**

  What about trying to build a mobile app and a responsive web app? Ultimately,
  the best experience for your customers is for your app to work everywhere, but
  the development and maintenance costs of that can be prohibitive.
categories:
  - Coding
  - Mobile
  - JavaScript
  - Apps
  - Performance
---
One of the hardest decisions to make when starting a new app is which platforms to target. A mobile app gives you more control and better performance but isn’t as universal as the web. If you’re making a mobile app, can you afford to support both iOS and Android? What about trying to build a mobile app and a responsive web app? Ultimately, the best experience for your customers is for your app to work everywhere, but the development and maintenance costs of that can be prohibitive.</p>

<figure><a href="https://www.smashingmagazine.com/2016/08/a-glimpse-into-the-future-with-react-native-for-web"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bd6a598b-cccd-4503-9846-7b7cffbb6a0f/08-react-native-friends-2-web-preview-opt.png" width="500" height="344" alt="React Native For Web – A Glimpse Into The Future" title="React Native For Web – A Glimpse Into The Future" /></a></figure>

We have already <a href="https://www.smashingmagazine.com/2016/04/consider-react-native-mobile-app/">seen how</a> React Native can help you make iOS and Android apps with a shared code base, without sacrifices in quality. But what about the web? This is exactly the problem the <a href="https://github.com/necolas/react-native-web">React Native for Web</a> project is trying to solve. Instead of forcing you to maintain two separate code bases for your mobile and web apps, or making a hybrid app, <a href="https://www.apptentive.com/blog/5-points-to-consider-before-making-a-hybrid-mobile-app/">with all its compromises</a>.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Why You Should Consider React Native For Your Mobile App](https://www.smashingmagazine.com/2016/04/consider-react-native-mobile-app/)
*   [How To Scale React Applications](https://www.smashingmagazine.com/2016/09/how-to-scale-react-applications/)
*   [Building Your First iOS App With JavaScript](https://www.smashingmagazine.com/2016/04/the-beauty-of-react-native-building-your-first-ios-app-with-javascript-part-1/)
*   [Internationalizing React Apps](https://www.smashingmagazine.com/2017/01/internationalizing-react-apps/)

{{% feature-panel %}}

React Native for Web is intended to let you write a single app that runs in a browser using standard web technologies, or on iOS and Android as a real native mobile app. While I don’t think the project is ready for production use yet, its potential success could mark a massive change in how large multi-platform applications are built. Let’s jump in!

## How It Works

You might be thinking, “Wait! doesn’t React already work on the web?” You wouldn’t be wrong. Unfortunately, traditional React and React Native build on a different set of primitives. React uses <code>&lt;div&gt;</code>, <code>&lt;p&gt;</code> and <code>&lt;input&gt;</code>, whereas React Native uses <code>&lt;View&gt;</code>, <code>&lt;Text&gt;</code> and <code>&lt;TextInput&gt;</code>. There are good historical reasons for this, since the building blocks of a web page and of a mobile app are quite different. Nonetheless, it would be great if we could use a single set of shared components.

React Native for Web’s solution is to provide browser-compatible implementations of React Native’s components — meaning, for example, that the <code>&lt;View&gt;</code> of React Native has a DOM-based version that knows how to render to a <code>&lt;div&gt;</code>. While not every React Native component is supported, enough of them are that you could (hopefully) share the majority of your code base.

In addition to the components themselves, styles for React and React Native are written differently. With React, most people use plain CSS or a preprocessor such as <a href="https://sass-lang.com/">Sass</a>. But in React Native, all styles are written in JavaScript, because there is no DOM and no selectors. With React Native for Web, styles are written just like they would be for React Native, rather than with CSS. This has the benefit of allowing you to write a single set of styles, which will work on both native mobile and the web.

We’ll take a deeper look later at how these ideas work in practice and at how much code is actually reusable. First, let’s get a sample app going.</p>

## Starting A New React Native Project

To get started, we will need to set up our project. At first, this will just be a regular React Native app, and then we’ll add React Native for Web. If you are following along, you’ll need to complete React Native’s “<a href="https://facebook.github.io/react-native/docs/getting-started.html">Getting Started</a>” guide before heading into the next section.

Once you’ve got React Native installed, you can run the following command from your terminal:

<pre><code class="language-bash">react-native init ReactNativeWeb</code></pre>

This will make a new React Native project named <code>ReactNativeWeb</code>. After it has finished installing, you can <code>cd ReactNativeWeb</code>, and then <code>react-native run-ios</code> or <code>react-native run-android</code>. If everything has gone correctly, you should see a friendly welcome message on your iOS or Android simulator or device.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7e2a6dd0-698e-491c-9f05-34a8c797e14b/01-react-native-welcome-ios-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9102b457-9f80-45ac-9584-5f0a6158f883/01-react-native-welcome-ios-preview-opt.png" alt="React Native iOS welcome screen" width="337" height="600" /></a><figcaption>React Native iOS welcome screen (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7e2a6dd0-698e-491c-9f05-34a8c797e14b/01-react-native-welcome-ios-opt.png">View large version</a>)</figcaption></figure>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3082ec10-e375-4a1e-b563-017d2119e87a/02-react-native-welcome-android-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d4b7dcbc-5d00-4743-8833-3e89b46e2918/02-react-native-welcome-android-preview-opt.png" alt="React Native Android welcome screen" width="338" height="600" /></a><figcaption>React Native Android welcome screen (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3082ec10-e375-4a1e-b563-017d2119e87a/02-react-native-welcome-android-opt.png">View large version</a>)</figcaption></figure>

Notice that React Native has created two JavaScript files in our project’s directory: <code>index.android.js</code> and <code>index.ios.js</code>. You can edit any of the styles or logic in these files and see those changes update in the running app. As you can probably guess, the <code>.android.js</code> file is for Android, and the <code>.ios.js</code> file is for iOS. Fortunately, separate files are only needed when you want multiple versions of a given file per platform. Most of the time, you’ll have a single file per component.

## Managing Dependencies

Before we can get our app running in a web browser, we’ll need to get a bit of package installation out of the way. First, run the following to install both the <code>react-native-web</code> package and the official React web packages.</p>

<pre><code class="language-bash">npm i react react-dom react-native-web --save</code></pre>

(You might see some errors about peer dependencies from this command. You should be safe to ignore them, because they didn’t cause me any problems. If newer versions of any of these packages are out when you run the commands, though, you might need to adjust the installed versions.)

At this point, your <code>package.json</code> file should look something like this:

<pre><code class="language-javascript">{
  "name": "ReactNativeWeb",
  "version": "0.0.1",
  "private": true,
  "scripts": {
    "start": "node node_modules/react-native/local-cli/cli.js start"
  },
  "dependencies": {
    "react": "15.1.0",
    "react-dom": "15.1.0",
    "react-native": "0.28.0",
    "react-native-web": "0.0.25"
  }
}
</code></pre>

While we have what seems to be everything required for our React Native app to run in a web browser, we must take a brief detour to consider the realities of web development. React Native’s packager compiles your ECMAScript 6 code to something that a phone’s JavaScript engine can understand, but it won’t help us in the browser. If we tried to run our app in a web browser right now, it would quickly fail due to syntax errors.

To solve this problem, we will use <a href="https://babeljs.io/">Babel</a> and <a href="https://webpack.github.io/">webpack</a>. Babel will compile our ECMAScript 6 code into browser-compatible ECMAScript 5, and webpack will bundle the compiled JavaScript, as well as just generally make development faster. (There are other options for this. If you prefer another compiler or bundler, feel free to use it instead.)

Here are the installation commands to run:

<pre><code class="language-bash">npm i webpack babel-loader babel-preset-react babel-preset-es2015 --save</code></pre>

<pre><code class="language-bash">npm i webpack-dev-server --save-dev</code></pre>

Here, <code>babel-loader</code> and <code>webpack-dev-server</code> will be used to bundle and serve our JavaScript, while <code>babel-preset-react</code> and <code>babel-preset-es2015</code> tell Babel which plugins we need to compile our code.

Here is what your <code>package.json</code> file should look like now:

<pre><code class="language-javascript">{
  "name": "ReactNativeWeb",
  "version": "0.0.1",
  "private": true,
  "scripts": {
    "start": "node node_modules/react-native/local-cli/cli.js start"
  },
  "dependencies": {
    "babel-loader": "6.2.4",
    "babel-preset-es2015": "6.9.0",
    "babel-preset-react": "6.5.0",
    "react": "15.1.0",
    "react-dom": "15.1.0",
    "react-native": "0.28.0",
    "react-native-web": "0.0.25",
    "webpack": "1.13.1"
  },
  "devDependencies": {
    "webpack-dev-server": "1.14.1"
  }
}
</code></pre>

## Configuring

Those are all of the packages we will need. But more setup is required before our app will work in a browser.</p>

### webpack.config.js

First, we’ll make a webpack <code>config</code> file. This file tells webpack how to build, bundle and serve our compiled code. In addition, we are going to use the <code>alias</code> property to automatically replace imports on <code>react-native</code> with <code>react-native-web</code>. This file should be placed in your project’s root.</p>

<pre><code class="language-javascript">const webpack = require('webpack');

module.exports = {
  entry: {
    main: './index.web.js',
  },
  module: {
    loaders: [
      {
        test: /\.js?$/,
        exclude: /node_modules/,
        loader: 'babel',
        query: {
          presets: ['es2015', 'react'],
        },
      },
    ],
  },
  resolve: {
    alias: {
      'react-native': 'react-native-web',
    },
  },
};
</code></pre>

### index.html

Now, we need to create an HTML file for our app to run in. This will be pretty simple because it will just be a skeleton to attach our React app to.</p>

<pre><code class="language-markup">&lt;!DOCTYPE html&gt;
&lt;html&gt;
&lt;head&gt;
  &lt;title&gt;React Native Web&lt;/title&gt;
  &lt;meta charSet="utf-8" /&gt;
  &lt;meta content="initial-scale=1,width=device-width" name="viewport" /&gt;
&lt;/head&gt;
&lt;body&gt;
  &lt;div id="react-app"&gt;&lt;/div&gt;
  &lt;script type="text/javascript" src="/bundle.js"&gt;&lt;/script&gt;
&lt;/body&gt;
&lt;/html&gt;
</code></pre>

### index.web.js

Finally, we must make an <code>index</code> JavaScript file for the web. The contents of this file can be the same as <code>index.ios.js</code> or <code>index.android.js</code>, but with one additional line to attach to the DOM. The div with the ID <code>react-app</code> from our HTML file must be selected and then used in the call to <code>AppRegister.runApplication</code>.</p>

<pre><code class="language-javascript">import React, { Component } from 'react';
import {
  AppRegistry,
  StyleSheet,
  Text,
  View
} from 'react-native';

class ReactNativeWeb extends Component {
  render() {
    return (
      &lt;View style={styles.container}&gt;
        &lt;Text style={styles.welcome}&gt;
          Welcome to React Native!
        &lt;/Text&gt;
        &lt;Text style={styles.instructions}&gt;
          To get started, edit index.web.js
        &lt;/Text&gt;
        &lt;Text style={styles.instructions}&gt;
          Press Cmd+R to reload
        &lt;/Text&gt;
      &lt;/View&gt;
    );
  }
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: 'center',
    alignItems: 'center',
    backgroundColor: '#F5FCFF',
  },
  welcome: {
    fontSize: 20,
    textAlign: 'center',
    margin: 10,
  },
  instructions: {
    textAlign: 'center',
    color: '#333333',
    marginBottom: 5,
  },
});

AppRegistry.registerComponent('ReactNativeWeb', () =&gt; ReactNativeWeb);
AppRegistry.runApplication('ReactNativeWeb', { rootTag: document.getElementById('react-app') });
</code></pre>

Now, just run <code>./node_modules/.bin/webpack-dev-server --inline</code> to start webpack, and open your browser to <a href="https://localhost:8080/">https://localhost:8080/</a>. Fingers crossed, you will see a familiar welcome message but in the browser!

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/651ad12d-a693-4bb8-af2e-83c7701fb25b/03-react-native-welcome-web-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dd9db918-d1e6-475b-8f7e-5e750105fd79/03-react-native-welcome-web-preview-opt.png" alt="React Native web welcome screen" width="500" height="334" /></a><figcaption>React Native web welcome screen (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/651ad12d-a693-4bb8-af2e-83c7701fb25b/03-react-native-welcome-web-opt.png">View large version</a>)</figcaption></figure>

With all of that setup complete, we are ready to start tinkering!

## Experimenting With The Code

### Create a FriendsList.js Component

Let’s start by making a friends list. This will be a good simple stress test of React Native for Web, because we need to use a few different components for it: <code>&lt;Image&gt;</code>, <code>&lt;Text&gt;</code>, <code>&lt;View&gt;</code> and <code>&lt;ListView&gt;</code>.</p>

<pre><code class="language-javascript">import React, { Component } from 'react';
import {
  Image,
  ListView,
  StyleSheet,
  Text,
  View,
} from 'react-native';

const styles = StyleSheet.create({
  list: {
    marginTop: 20,
  },
  friend: {
    flexDirection: 'row',
    alignItems: 'center',
    justifyContent: 'flex-start',
  },
  avatar: {
    margin: 10,
    width: 50,
    height: 50,
    borderRadius: 25,
  },
  name: {
    fontSize: 18,
    color: '#000',
  }
});

export default class FriendsList extends Component {
  constructor(props) {
    super(props);
    const ds = new ListView.DataSource({ rowHasChanged: (r1, r2) =&gt; r1 !== r2 });
    this.state = {
      ds: ds.cloneWithRows(props.friends),
    };
  }

  render() {
    return (
      &lt;ListView
        dataSource={this.state.ds}
        style={styles.list}
        renderRow={(friend) =&gt;
          &lt;View style={styles.friend}&gt;
            &lt;Image style={styles.avatar} source={{ uri: friend.avatarUrl }} /&gt;
            &lt;Text style={styles.name}&gt;{friend.firstName} {friend.lastName}&lt;/Text&gt;
          &lt;/View&gt;
        } /&gt;
    );
  }
}
</code></pre>

We’ll need to edit our <code>index</code> files, too, so that a <code>friends</code> array gets passed in as a prop.</p>

<pre><code class="language-javascript">import FriendsList from './FriendsList';
import React, { Component } from 'react';
import {
  AppRegistry,
  Text,
  View
} from 'react-native';

const friends = [
  {
    id: 1,
    firstName: 'Jane',
    lastName: 'Miller',
    avatarUrl: 'https://placehold.it/100x100',
  },
  {
    id: 2,
    firstName: 'Kate',
    lastName: 'Smith',
    avatarUrl: 'https://placehold.it/100x100',
  },
  {
    id: 3,
    firstName: 'Kevin',
    lastName: 'Yang',
    avatarUrl: 'https://placehold.it/100x100',
  },
];

class ReactNativeWeb extends Component {
  render() {
    return &lt;FriendsList friends={friends} /&gt;;
  }
}

AppRegistry.registerComponent('ReactNativeWeb', () =&gt; ReactNativeWeb);
</code></pre>

Upon running it in iOS or Android, you should see something like this:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/74171c66-e07c-4ffd-be0f-d611a303d5d2/04-react-native-friends-ios-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/803ada09-5cda-4626-aac6-6b4a703ef930/04-react-native-friends-ios-preview-opt.png" alt="React Native iOS friends list" width="500" height="445" /></a><figcaption>React Native iOS friends list (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/74171c66-e07c-4ffd-be0f-d611a303d5d2/04-react-native-friends-ios-opt.png">View large version</a>)</figcaption></figure>

Looks good so far. Let’s see the web version:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7b13f84f-cf07-4d88-8526-e3d32daf1f64/05-react-native-friends-web-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/94cc106e-ec35-481b-b080-c706f7e82d2d/05-react-native-friends-web-preview-opt.png" alt="React Native web friends list" width="500" height="24" /></a><figcaption>React Native web friends list. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7b13f84f-cf07-4d88-8526-e3d32daf1f64/05-react-native-friends-web-opt.png">View large version</a>)</figcaption></figure>

Uh oh! Turns out there isn’t any web support yet for <code>ListView</code>’s <code>DataSource</code>, effectively making <code>ListView</code> completely unusable.</p>

### Friend.js

We can work around this lack of support for now. Let’s make a <code>Friend</code> component for the individual rows, but have a <code>FriendsList</code> component per platform. This will separate out the shared code that works everywhere but allow us to customize each platform where we need to.</p>

<pre><code class="language-javascript">import React, { Component } from 'react';
import {
  Image,
  StyleSheet,
  Text,
  View,
} from 'react-native';

const styles = StyleSheet.create({
  friend: {
    flexDirection: 'row',
    alignItems: 'center',
    justifyContent: 'flex-start',
  },
  avatar: {
    margin: 10,
    width: 50,
    height: 50,
    borderRadius: 25,
  },
  name: {
    fontSize: 18,
    color: '#000',
  }
});

export default class Friend extends Component {
  render() {
    return (
      &lt;View style={styles.friend}&gt;
        &lt;Image style={styles.avatar} source={{ uri: this.props.avatarUrl }} /&gt;
        &lt;Text style={styles.name}&gt;{this.props.firstName} {this.props.lastName}&lt;/Text&gt;
      &lt;/View&gt;
    );
  }
}
</code></pre>

### FriendsList.ios.js

<pre><code class="language-javascript">import Friend from './Friend';
import React, { Component } from 'react';
import {
  Image,
  ListView,
  StyleSheet,
  Text,
  View,
} from 'react-native';

const styles = StyleSheet.create({
  list: {
    marginTop: 20,
  },
});

export default class FriendsList extends Component {
  constructor(props) {
    super(props);
    const ds = new ListView.DataSource({ rowHasChanged: (r1, r2) =&gt; r1 !== r2 });
    this.state = {
      ds: ds.cloneWithRows(props.friends),
    };
  }

  render() {
    return (
      &lt;ListView
        dataSource={this.state.ds}
        style={styles.list}
        renderRow={(friend) =&gt;
          &lt;Friend
            key={friend.id}
            avatarUrl={friend.avatarUrl}
            firstName={friend.firstName}
            lastName={friend.lastName} /&gt;
        } /&gt;
    );
  }
}
</code></pre>

On iOS, our <code>ListView</code> usage code is unchanged. (I’m leaving out the Android code example here and for the rest of the article, for brevity. The Android and iOS code can be the same for the rest of the code samples.)

### FriendsList.web.js

<pre><code class="language-javascript">import Friend from './Friend';
import React, { Component } from 'react';
import {
  Image,
  Text,
  View,
} from 'react-native';

export default class FriendsList extends Component {
  render() {
    return (
      &lt;View&gt;
        {this.props.friends.map(friend =&gt;
          &lt;Friend
            key={friend.id}
            avatarUrl={friend.avatarUrl}
            firstName={friend.firstName}
            lastName={friend.lastName} /&gt;
        )}
      &lt;/View&gt;
    );
  }
}
</code></pre>

Now, for the web, we use the <code>map</code> function to render each <code>Friend</code>, similar to traditional React.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f0882d7f-9fd1-4fd3-b6c7-4801195329c5/06-react-native-friends-web-2-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c4cf4168-4a41-40ce-846e-570abeb6ed45/06-react-native-friends-web-2-preview-opt.png" alt="React Native friends list on the web, now working" width="500" height="348" /></a><figcaption>React Native friends list on the web, now working (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f0882d7f-9fd1-4fd3-b6c7-4801195329c5/06-react-native-friends-web-2-opt.png">View large version</a>)</figcaption></figure>

Much better. At this point, hearing that <code>ListView</code> requires workarounds might be enough to make you think that React Native for Web isn’t ready for production use. I am inclined to agree, particularly since lists constitute a large percentage of many applications. How much it matters will vary depending on the project, though. On the bright side, all of our other React Native code so far has been completely reusable. In any case, I am still interested in exploring it further, because there is still much potential in the ideas on display here. Let’s continue with our sample app.

Instead of hardcoding a handful of list items, we can use <a href="https://www.json-generator.com/">JSON Generator</a> to create a long list for us to work with. If you haven’t used it before, JSON Generator is a great tool for creating dummy and development data. Here is the structure I have defined, which adds a few fields on top of what we already have.</p>

<pre><code class="language-javascript">
[
  '{{repeat(200)}}',
  {
    id: '{{guid()}}',
    firstName: '{{firstName()}}',
    lastName: '{{surname()}}',
    avatarUrl: 'https://placehold.it/100x100',
    isOnline: '{{bool()}}',
    company: '{{company()}}',
    email: '{{email()}}'
  }
]
</code></pre>

And here is a snippet of some of the generated data:

<pre><code class="language-javascript">
[
  {
    "id": "c5368bbe-adfb-424f-ade3-9d783befa2b6",
    "firstName": "Hahn",
    "lastName": "Rojas",
    "avatarUrl": "https://placehold.it/100x100",
    "isOnline": true,
    "company": "Orbixtar",
    "email": "hahnrojas@orbixtar.com"
  },
  {
    "id": "15ef2834-3ba5-4621-abf1-d771d39c2dd6",
    "firstName": "Helen",
    "lastName": "Stout",
    "avatarUrl": "https://placehold.it/100x100",
    "isOnline": true,
    "company": "Ebidco",
    "email": "helenstout@ebidco.com"
  },
  {
    "id": "1ef05de1-fd8e-41ae-85ac-620b6d716b62",
    "firstName": "Floyd",
    "lastName": "Mcpherson",
    "avatarUrl": "https://placehold.it/100x100",
    "isOnline": false,
    "company": "Ecraze",
    "email": "floydmcpherson@ecraze.com"
  },
  …
]
</code></pre>

To use it, just take your generated JSON and replace our <code>friends</code> array declaration from before. Of course, you can move that data into its own file if you’d like, so that your code files aren’t cluttered with data. In a real application, we would get that data from an API server.</p>

### Friend.js

Next, we can add these new fields to the <code>Friend</code> component.</p>

<pre><code class="language-javascript">
…
render() {
  return (
    &lt;View style={styles.friend}&gt;
      &lt;Image
        style={[styles.avatar, { borderColor: this.props.isOnline ? '#9d9' : '#d99' }]}
        source={{ uri: this.props.avatarUrl }} /&gt;

      &lt;View&gt;
        &lt;Text style={styles.name}&gt;{this.props.firstName} {this.props.lastName}&lt;/Text&gt;
        &lt;Text style={styles.company}&gt;{this.props.company}&lt;/Text&gt;
        &lt;Text style={styles.email}&gt;{this.props.email}&lt;/Text&gt;
      &lt;/View&gt;
    &lt;/View&gt;
  );
}
…
</code></pre>

### FriendsList.js

Next, add them as props in each platform’s <code>FriendsList</code>.</p>

<pre><code class="language-javascript">…
&lt;Friend
  key={friend.id}
  avatarUrl={friend.avatarUrl}
  firstName={friend.firstName}
  lastName={friend.lastName}
  isOnline={friend.isOnline}
  company={friend.company}
  email={friend.email} /&gt;
…
</code></pre>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/395bca6c-65a7-40a6-b286-ccba0082744c/07-react-native-friends-2-ios-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9c6253d4-f40f-4874-aabf-13599e4e47d3/07-react-native-friends-2-ios-preview-opt.png" alt="React Native long friends list for iOS" width="337" height="600" /></a><figcaption>React Native’s long friends list for iOS (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/395bca6c-65a7-40a6-b286-ccba0082744c/07-react-native-friends-2-ios-opt.png">View large version</a>)</figcaption></figure>

const styles = StyleSheet.create({
  list: {
    marginTop: 20,
  },
  friend: {
    flexDirection: 'row',
    alignItems: 'center',
    justifyContent: 'flex-start',
  },
  avatar: {
    margin: 10,
    width: 50,
    height: 50,
    borderRadius: 25,
  },
  name: {
    fontSize: 18,
    color: '#000',
  }
});

export default class FriendsList extends Component {
  constructor(props) {
    super(props);
    const ds = new ListView.DataSource({ rowHasChanged: (r1, r2) =&gt; r1 !== r2 });
    this.state = {
      ds: ds.cloneWithRows(props.friends),
    };
  }

  render() {
    return (
      &lt;ListView
        dataSource={this.state.ds}
        style={styles.list}
        renderRow={(friend) =&gt;
          &lt;View style={styles.friend}&gt;
            &lt;Image style={styles.avatar} source={{ uri: friend.avatarUrl }} /&gt;
            &lt;Text style={styles.name}&gt;{friend.firstName} {friend.lastName}&lt;/Text&gt;
          &lt;/View&gt;
        } /&gt;
    );
  }
}
</code></pre>

We’ll need to edit our <code>index</code> files, too, so that a <code>friends</code> array gets passed in as a prop.</p>

<pre><code class="language-javascript">import FriendsList from './FriendsList';
import React, { Component } from 'react';
import {
  AppRegistry,
  Text,
  View
} from 'react-native';

const friends = [
  {
    id: 1,
    firstName: 'Jane',
    lastName: 'Miller',
    avatarUrl: 'https://placehold.it/100x100',
  },
  {
    id: 2,
    firstName: 'Kate',
    lastName: 'Smith',
    avatarUrl: 'https://placehold.it/100x100',
  },
  {
    id: 3,
    firstName: 'Kevin',
    lastName: 'Yang',
    avatarUrl: 'https://placehold.it/100x100',
  },
];

class ReactNativeWeb extends Component {
  render() {
    return &lt;FriendsList friends={friends} /&gt;;
  }
}

AppRegistry.registerComponent('ReactNativeWeb', () =&gt; ReactNativeWeb);
</code></pre>

Upon running it in iOS or Android, you should see something like this:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/74171c66-e07c-4ffd-be0f-d611a303d5d2/04-react-native-friends-ios-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/803ada09-5cda-4626-aac6-6b4a703ef930/04-react-native-friends-ios-preview-opt.png" alt="React Native iOS friends list" width="500" height="445" /></a><figcaption>React Native iOS friends list (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/74171c66-e07c-4ffd-be0f-d611a303d5d2/04-react-native-friends-ios-opt.png">View large version</a>)</figcaption></figure>

Looks good so far. Let’s see the web version:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7b13f84f-cf07-4d88-8526-e3d32daf1f64/05-react-native-friends-web-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/94cc106e-ec35-481b-b080-c706f7e82d2d/05-react-native-friends-web-preview-opt.png" alt="React Native web friends list" width="500" height="24" /></a><figcaption>React Native web friends list. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7b13f84f-cf07-4d88-8526-e3d32daf1f64/05-react-native-friends-web-opt.png">View large version</a>)</figcaption></figure>

Uh oh! Turns out there isn’t any web support yet for <code>ListView</code>’s <code>DataSource</code>, effectively making <code>ListView</code> completely unusable.</p>

### Friend.js

We can work around this lack of support for now. Let’s make a <code>Friend</code> component for the individual rows, but have a <code>FriendsList</code> component per platform. This will separate out the shared code that works everywhere but allow us to customize each platform where we need to.</p>

<pre><code class="language-javascript">import React, { Component } from 'react';
import {
  Image,
  StyleSheet,
  Text,
  View,
} from 'react-native';

const styles = StyleSheet.create({
  friend: {
    flexDirection: 'row',
    alignItems: 'center',
    justifyContent: 'flex-start',
  },
  avatar: {
    margin: 10,
    width: 50,
    height: 50,
    borderRadius: 25,
  },
  name: {
    fontSize: 18,
    color: '#000',
  }
});

export default class Friend extends Component {
  render() {
    return (
      &lt;View style={styles.friend}&gt;
        &lt;Image style={styles.avatar} source={{ uri: this.props.avatarUrl }} /&gt;
        &lt;Text style={styles.name}&gt;{this.props.firstName} {this.props.lastName}&lt;/Text&gt;
      &lt;/View&gt;
    );
  }
}
</code></pre>

### FriendsList.ios.js

<pre><code class="language-javascript">import Friend from './Friend';
import React, { Component } from 'react';
import {
  Image,
  ListView,
  StyleSheet,
  Text,
  View,
} from 'react-native';

const styles = StyleSheet.create({
  list: {
    marginTop: 20,
  },
});

export default class FriendsList extends Component {
  constructor(props) {
    super(props);
    const ds = new ListView.DataSource({ rowHasChanged: (r1, r2) =&gt; r1 !== r2 });
    this.state = {
      ds: ds.cloneWithRows(props.friends),
    };
  }

  render() {
    return (
      &lt;ListView
        dataSource={this.state.ds}
        style={styles.list}
        renderRow={(friend) =&gt;
          &lt;Friend
            key={friend.id}
            avatarUrl={friend.avatarUrl}
            firstName={friend.firstName}
            lastName={friend.lastName} /&gt;
        } /&gt;
    );
  }
}
</code></pre>

On iOS, our <code>ListView</code> usage code is unchanged. (I’m leaving out the Android code example here and for the rest of the article, for brevity. The Android and iOS code can be the same for the rest of the code samples.)

### FriendsList.web.js

<pre><code class="language-javascript">import Friend from './Friend';
import React, { Component } from 'react';
import {
  Image,
  Text,
  View,
} from 'react-native';

export default class FriendsList extends Component {
  render() {
    return (
      &lt;View&gt;
        {this.props.friends.map(friend =&gt;
          &lt;Friend
            key={friend.id}
            avatarUrl={friend.avatarUrl}
            firstName={friend.firstName}
            lastName={friend.lastName} /&gt;
        )}
      &lt;/View&gt;
    );
  }
}
</code></pre>

Now, for the web, we use the <code>map</code> function to render each <code>Friend</code>, similar to traditional React.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f0882d7f-9fd1-4fd3-b6c7-4801195329c5/06-react-native-friends-web-2-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c4cf4168-4a41-40ce-846e-570abeb6ed45/06-react-native-friends-web-2-preview-opt.png" alt="React Native friends list on the web, now working" width="500" height="348" /></a><figcaption>React Native friends list on the web, now working (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f0882d7f-9fd1-4fd3-b6c7-4801195329c5/06-react-native-friends-web-2-opt.png">View large version</a>)</figcaption></figure>

Much better. At this point, hearing that <code>ListView</code> requires workarounds might be enough to make you think that React Native for Web isn’t ready for production use. I am inclined to agree, particularly since lists constitute a large percentage of many applications. How much it matters will vary depending on the project, though. On the bright side, all of our other React Native code so far has been completely reusable. In any case, I am still interested in exploring it further, because there is still much potential in the ideas on display here. Let’s continue with our sample app.

Instead of hardcoding a handful of list items, we can use <a href="https://www.json-generator.com/">JSON Generator</a> to create a long list for us to work with. If you haven’t used it before, JSON Generator is a great tool for creating dummy and development data. Here is the structure I have defined, which adds a few fields on top of what we already have.</p>

<pre><code class="language-javascript">
[
  '{{repeat(200)}}',
  {
    id: '{{guid()}}',
    firstName: '{{firstName()}}',
    lastName: '{{surname()}}',
    avatarUrl: 'https://placehold.it/100x100',
    isOnline: '{{bool()}}',
    company: '{{company()}}',
    email: '{{email()}}'
  }
]
</code></pre>

And here is a snippet of some of the generated data:

<pre><code class="language-javascript">
[
  {
    "id": "c5368bbe-adfb-424f-ade3-9d783befa2b6",
    "firstName": "Hahn",
    "lastName": "Rojas",
    "avatarUrl": "https://placehold.it/100x100",
    "isOnline": true,
    "company": "Orbixtar",
    "email": "hahnrojas@orbixtar.com"
  },
  {
    "id": "15ef2834-3ba5-4621-abf1-d771d39c2dd6",
    "firstName": "Helen",
    "lastName": "Stout",
    "avatarUrl": "https://placehold.it/100x100",
    "isOnline": true,
    "company": "Ebidco",
    "email": "helenstout@ebidco.com"
  },
  {
    "id": "1ef05de1-fd8e-41ae-85ac-620b6d716b62",
    "firstName": "Floyd",
    "lastName": "Mcpherson",
    "avatarUrl": "https://placehold.it/100x100",
    "isOnline": false,
    "company": "Ecraze",
    "email": "floydmcpherson@ecraze.com"
  },
  …
]
</code></pre>

To use it, just take your generated JSON and replace our <code>friends</code> array declaration from before. Of course, you can move that data into its own file if you’d like, so that your code files aren’t cluttered with data. In a real application, we would get that data from an API server.</p>

### Friend.js

Next, we can add these new fields to the <code>Friend</code> component.</p>

<pre><code class="language-javascript">
…
render() {
  return (
    &lt;View style={styles.friend}&gt;
      &lt;Image
        style={[styles.avatar, { borderColor: this.props.isOnline ? '#9d9' : '#d99' }]}
        source={{ uri: this.props.avatarUrl }} /&gt;

      &lt;View&gt;
        &lt;Text style={styles.name}&gt;{this.props.firstName} {this.props.lastName}&lt;/Text&gt;
        &lt;Text style={styles.company}&gt;{this.props.company}&lt;/Text&gt;
        &lt;Text style={styles.email}&gt;{this.props.email}&lt;/Text&gt;
      &lt;/View&gt;
    &lt;/View&gt;
  );
}
…
</code></pre>

### FriendsList.js

Next, add them as props in each platform’s <code>FriendsList</code>.</p>

<pre><code class="language-javascript">…
&lt;Friend
  key={friend.id}
  avatarUrl={friend.avatarUrl}
  firstName={friend.firstName}
  lastName={friend.lastName}
  isOnline={friend.isOnline}
  company={friend.company}
  email={friend.email} /&gt;
…
</code></pre>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/395bca6c-65a7-40a6-b286-ccba0082744c/07-react-native-friends-2-ios-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9c6253d4-f40f-4874-aabf-13599e4e47d3/07-react-native-friends-2-ios-preview-opt.png" alt="React Native long friends list for iOS" width="337" height="600" /></a><figcaption>React Native’s long friends list for iOS (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/395bca6c-65a7-40a6-b286-ccba0082744c/07-react-native-friends-2-ios-opt.png">View large version</a>)</figcaption></figure>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/14b621f2-a27b-4f91-81bd-cd4231756a07/08-react-native-friends-2-web-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bd6a598b-cccd-4503-9846-7b7cffbb6a0f/08-react-native-friends-2-web-preview-opt.png" alt="React Native long friend list web" width="500" height="344" /></a><figcaption>React Native’s long friends list for the web (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/14b621f2-a27b-4f91-81bd-cd4231756a07/08-react-native-friends-2-web-opt.png">View large version</a>)</figcaption></figure>

So far so good. It is encouraging to see that the core components seem to work well.</p>

### Friend.js

Next, we can add an animation with a transformation to see how well those work. Let’s make it so that when you tap a row, it animates left and right before returning to its initial position. We will need to add imports for <code>Animated</code> and <code>TouchableOpacity</code>, and wire up the animation and press handler.</p>

<pre><code class="language-javascript">import {
  Animated,
  TouchableOpacity,
  …
} from 'react-native';

…

export default class Friend extends Component {
  constructor(props) {
    super(props);
    this.state = {
      translateValue: new Animated.Value(0),
    };
  }

  animate() {
    Animated.sequence([
      Animated.timing(this.state.translateValue, {
        toValue: 50,
        duration: 200,
      }),
      Animated.timing(this.state.translateValue, {
        toValue: -50,
        duration: 200,
      }),
      Animated.timing(this.state.translateValue, {
        toValue: 0,
        duration: 200,
      })
    ]).start();
  }

  render() {
    return (
      &lt;TouchableOpacity onPress={() =&gt; this.animate()} style={[styles.friend, { transform: [{ translateX: this.state.translateValue }]}]}&gt;
        &lt;Image
          style={[styles.avatar, { borderColor: this.props.isOnline ? '#9d9' : '#d99' }]}
          source={{ uri: this.props.avatarUrl }} /&gt;

        &lt;View&gt;
          &lt;Text style={styles.name}&gt;{this.props.firstName} {this.props.lastName}&lt;/Text&gt;
          &lt;Text style={styles.company}&gt;{this.props.company}&lt;/Text&gt;
          &lt;Text style={styles.email}&gt;{this.props.email}&lt;/Text&gt;
        &lt;/View&gt;
      &lt;/TouchableOpacity&gt;
    );
  }
}
</code></pre>

Looks good on mobile.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/39e8aa5f-3bf1-4aec-950b-c1feadda3695/09-react-native-ios-animation-opt.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fcef71f9-5d0b-4b86-80f5-d809a085ec78/09-react-native-ios-animation-preview-opt.gif" alt="React Native iOS animation" width="331" height="600" /></a><figcaption>React Native iOS animation (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/39e8aa5f-3bf1-4aec-950b-c1feadda3695/09-react-native-ios-animation-opt.gif">View large version</a>)</figcaption></figure>

What about the web?

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ec639439-d802-4479-8f8b-0d789fe08bc3/10-react-native-web-animation-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/11bec749-1c11-41d8-9ab2-a7a6fc95faee/10-react-native-web-animation-preview-opt.png" alt="React Native web animation" width="500" height="26" /></a><figcaption>React Native web animation (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ec639439-d802-4479-8f8b-0d789fe08bc3/10-react-native-web-animation-opt.png">View large version</a>)</figcaption></figure>

No luck. Our <code>TouchableOpacity</code> throws an error when pressed. Apparently, this will be <a href="https://github.com/necolas/react-native-web/issues/150">fixed</a> in the next release and is only present for our particular combination of versions. Attempting to run the animation without using <code>TouchableOpacity</code> causes the same error, too.

I am going to stop here, but if you want to continue on your own, here is a list of topics you could research next:

*   How well do the remaining React Native components and APIs work? We’ve seen that some definitely don’t work, but we don’t yet have a comprehensive list of support.
*   You could explore more extensive styling work, including media queries.
*   React Native for Web supports server rendering. This could be particularly cool because, if it works, it would mean that you could have a single code base driving native mobile applications and a responsive web app that is SEO-optimized.</p>

## Conclusion

As you can tell, React Native for Web is definitely not ready for production. There are too many unsupported components, even in our small demo app, for me to feel confident about using it in a real project. The most encouraging thing to me, though, is that the pieces that do work seem to completely work, and the parts that don’t, fail entirely. I find that much preferable to the entire thing just <em>kind of</em> working. At the moment, it seems like the project just needs more time to build support. If everything was only 50% functional, I would view that as a sign that the approach is fundamentally broken.

Despite the problems, I still think this is a very exciting project and worth keeping an eye on.</p>

### Resources

*   [React Native for Web](https://github.com/necolas/react-native-web), GitHub
*   “[Getting Started](https://facebook.github.io/react-native/docs/getting-started.html),” React Native

{{< signature "da, ml, al" >}}

