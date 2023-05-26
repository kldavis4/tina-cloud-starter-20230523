---
title: 'Hybrid Apps And React Native: A Time To Transition?'
slug: transition-hybrid-apps-react-native
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b5f445b9-c4c7-4cc1-a4fe-7a6504af827a/developermenu-500w-opt.png
date: 2017-06-14T21:31:53.000Z
author: paulfrancis
description: >-
  Accomplished musicians often talk about how, at certain moments in their
  careers, they had to **unlearn old habits in order to progress**. This process
  often causes them to regress in performance while they adjust to an ultimately
  better method.

  Once the new approach is integrated, they are able to reach new heights that
  would not have been possible with their previous techniques.
categories:
  - Coding
  - Apps
  - Hybrid
  - React Native
---
Like musicians, all professionals should frequently question their methodologies and see what other options exist. If one approach was previously the best, that does not mean it remains the best. Then again, many established techniques have been the best for decades and might never be surpassed. The important thing is that one is willing to consider alternative approaches and is not too heavily biased towards the one they are most familiar with. This analysis is often more difficult in software development because new frameworks and technologies emerge almost as quickly as they die off.

This article will apply this analysis to hybrid mobile apps and present why I sincerely believe that React Native is in many ways a superior solution for apps developed in 2017, even if it introduces some temporary pains while you’re getting acclimated. To do this, we will revisit **why hybrid apps were created initially** and explore how we got to this point. Then, within this context, we’ll discuss how React Native stacks up and explain why it is the better approach in most cases.</p>

### <span class="rh">Further Reading</span> on SmashingMag:

*   [What Every App Developer Should Know About Android](https://www.smashingmagazine.com/2014/10/what-every-app-developer-should-know-about-android/)
*   [React Native For Web: A Glimpse Into The Future](https://www.smashingmagazine.com/2016/08/a-glimpse-into-the-future-with-react-native-for-web/)
*   [Why You Should Consider React Native For Your Mobile App](https://www.smashingmagazine.com/2016/04/consider-react-native-mobile-app/)
*   [Mobile Considerations in User Experience Design: “Web or Native?”](https://www.smashingmagazine.com/2012/06/mobile-considerations-in-user-experience-design-web-or-native/)

{{% feature-panel %}}

## An Origin Story

It’s 2010\. Your company has a pretty awesome web application that uses jQuery (or, if you’re hip, some sort of AngularJS and React precursor like Mustache). You have a team of developers competent in HTML, CSS and JavaScript. All of a sudden, mobile apps are taking over. Everyone has one. Mobile apps are the new _Tickle Me Elmo_! You frantically research how to make your own mobile app and immediately run into a host of issues. Your team is ill-equipped for the task. You don’t have Java or Objective-C developers. You can’t afford to develop, test and deploy two separate apps!

Not to worry. The hybrid mobile app is your silver bullet. This shiny new technology allows you to quickly and (in theory) easily reuse what you have (code and developers) for your lustrous new mobile app. So, you pick a framework (Cordova, PhoneGap, etc.) and get to work building or porting your first mobile app!

For many companies and developers, their problems were solved. They could now make their very own mobile apps.</p>

## Problems Arise

Ever since 2010, developer forums, blogs and message boards have been full of arguments about the efficacy of hybrid apps. Despite the great promise and flexibility described in the previous paragraphs, hybrid apps have had and continue to face a very real series of challenges and shortcomings. Here are a few of the most notable problems

### User-Experience Shortcomings

Over the past couple of years, the bar for UX in mobile apps has risen dramatically. Most smartphone owners spend the majority of their time using only a [handful of premier apps](https://marketingland.com/nearly-85-percent-smartphone-app-time-concentrated-top-five-apps-report-191624). They, perhaps unfairly, expect any new app they try to be as polished as Facebook, MLB TV, YouTube and Uber.

With this very high bar, it is quite difficult for hybrid apps to measure up. Issues such as sluggish or limited animations, keyboard misbehavior and frequent lack of platform-specific gesture recognition all add up to a clunkier experience, which makes hybrid apps second-class citizens. Compounding this issue is hybrid apps’ reliance on the open-source community to write wrappers for native functionality. Here is a screenshot from an app that highlights all of these issues. This [app](https://itunes.apple.com/us/app/stockplan-connect/id1055368068?mt=8) was selected from Ionic’s [showcase](https://showcase.ionicframework.com/apps/top) and was created by Morgan Stanley.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4dda34e3-2e96-4554-8f4f-03a8b4cffaa0/ms-stock-app-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d0ed5a02-25e7-4f55-bfb0-1919916b4db8/ms-stock-app-800w-opt.png" alt="Screenshot of the app store listing for MS StockPlan." width="800" height="629" /></a><figcaption>Screenshot of the app store listing for MS StockPlan (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4dda34e3-2e96-4554-8f4f-03a8b4cffaa0/ms-stock-app-large-opt.png">View large version</a>)</figcaption></figure>

A few things should be immediately apparent. This app has a very low rating (2.5 stars). It does not look like a mobile app and is clearly a port of a mobile web app. Clear giveaways are the non-native segmented control, font size, text density and non-native tab bar. The app does not support features that are more easily implemented when building natively. Most importantly, customers are noticing all of these issues and are summarizing their feelings as “feels outdated.”

### User Interface Challenges

The majority of users are very quick to [uninstall or forget new apps](https://andrewchen.co/new-data-shows-why-losing-80-of-your-mobile-users-is-normal-and-that-the-best-apps-do-much-better/). It is crucial that your app makes a great first impression and is easily understood by users. A large part of this is about looking sharp and being familiar. Hybrid apps can look great, but they do tend to be more platform-agnostic in their UI (if they look like a web app) or foreign (if they look like an iOS app on Android or vice versa).

Before even installing an app, many would-be customers will review images in the app store. If those screenshots are unappealing or off-putting, the app might not be downloaded at all. Here is an example app found on the Ionic showcase. [This app](https://play.google.com/store/apps/details?id=com.nationwide.mobile.android.nwmobile&hl=en) was created by Nationwide, and, as you can tell, both apps look just like a mobile-friendly website, rather than a mobile app.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/80bcc4b0-48b7-4a0d-b982-6b9034469415/nationwide-ios-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/80bcc4b0-48b7-4a0d-b982-6b9034469415/nationwide-ios-preview-opt.png" alt="Screenshot of the Nationwide app on iOS" width="392" height="" /></a><figcaption>Screenshot of the Nationwide app on iOS</figcaption></figure>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1f275aa3-bff7-4dcd-a725-c7719a15417e/nationwide-android-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1f275aa3-bff7-4dcd-a725-c7719a15417e/nationwide-android-preview-opt.png" alt="Screenshot of the Nationwide app on Android" width="392" height="" /></a><figcaption>Screenshot of the Nationwide app on Android</figcaption></figure>

It is clear from the app store reviews (3 stars on both platforms) that this app has several issues, but it is unlikely that any app with this UI would attract new customers. It is clearly only used by existing customers who think they might as well try it out.</p>

### Performance Issues

The most common complaints about hybrid apps cite poor [performance](https://www.smashingmagazine.com/2014/09/improving-smashing-magazine-performance-case-study/), bugs and crashes. Of course, any app can have these issues, but performance issues have long plagued hybrid apps. Additionally, hybrid apps often have less [offline support](https://www.smashingmagazine.com/2016/08/a-beginners-guide-to-progressive-web-apps/), can take longer to open and perform worse in poor network conditions. Any developer has heard any of the above called a “bug” and has had their app publicly penalized as a result.</p>

### Overall Lack of Premier Apps

All of these issues have added up to the vast majority of premier apps being written natively. A quick look at both [PhoneGap’s](https://phonegap.com/app/) and [Ionic’s](https://showcase.ionicframework.com/apps/top) showcases demonstrate a noticeable shortcoming in premier apps. One of the most highly touted hybrid apps is Untappd, which despite being a pretty great platform, has fewer than 5 million downloads. This might seem like a large number, but it puts it quite far down the list of most used apps.

Additionally, there is a long list of apps that have migrated from hybrid to native. That list includes [Facebook](https://www.facebook.com/notes/facebook-engineering/under-the-hood-rebuilding-facebook-for-ios/10151036091753920/), [TripAdvisor](https://www.androidcentral.com/tripadvisor-launches-refreshed-native-app-improved-performance-interface), [Uber](https://eng.uber.com/tech-stack-part-two/), [Instagram](https://engineering.instagram.com/react-native-at-instagram-dd828a9a90c7) and many others.

It would be quite challenging to find a list of high-end apps that have moved from native to hybrid.</p>

### Final Defence of Hybrid Apps

The point of this section is not to be overly critical of hybrid apps, but to show that there is room for an alternative approach. Hybrid apps have been a very important technology and have been used successfully in many cases. Returning to the Ionic showcase, there are several apps that look better than the ones above. [Baskin Robbins](https://www.baskinrobbins.com/content/baskinrobbins/en/mobileapp.html), [Pacifica](https://blog.ionic.io/built-with-ionic-pacifica/) and [Sworkit](https://sworkit.com/) are three recent examples.

For the past four years, hybrid app developers and frameworks have been working hard to improve their apps, and they have done an admirable job. However, underlying issues and foundational shortcomings remain, and ultimately better options can be found if you’re building a new app in 2017.</p>

## Another Approach

Although it is clear that hybrid apps do not quite stack up against native apps, their advantages and success can’t be ignored. They help solve very real resource, time and capabilities problems. If there was another approach that solved these same problems, while also eliminating the shortcomings of hybrid apps, that would be extremely appealing. React Native might just be the answer.</p>

### Overview and Advantages

[React Native](https://www.smashingmagazine.com/2016/04/consider-react-native-mobile-app/) is a cross-platform mobile application development framework that builds on the popular React web development framework. Like React, React Native is an open-source project maintained largely by developers at Facebook and Instagram.

This framework is used to create Android and iOS applications with a shared JavaScript code base. When creating React Native apps, all of your business logic, API calls and state management live in JavaScript. The UI elements and their styling are genericized in your code but are rendered as the native views. This allows you to get a high degree of code reuse and still have a UI that follows each platform’s style guide and best practices.

React Native also allows you to write platform-specific code, logic and styling as needed. This could be as simple as having platform-specific React components or as advanced as using a platform-specific [C library in your React Native app](https://thebhwgroup.com/blog/react-native-jni).</p>

### Similarities to Hybrid Apps

Like hybrid app frameworks, React Native enables true cross-platform development. Instagram has shared that it is seeing between [85 and 99% code reuse](https://engineering.instagram.com/react-native-at-instagram-dd828a9a90c7) for its React Native projects. Additionally, React Native is built using technologies (JavaScript and React) that many web developers will be familiar with. In the event that a developer is not familiar with React, it is a dramatically easier to learn if they are familiar with AngularJS, jQuery or vanilla JavaScript than it would be to learn Objective-C or Java.

Additionally, [debugging](https://facebook.github.io/react-native/docs/debugging.html) React Native apps should also be a familiar process for web developers. This is because it is exceptionally easy to use Chrome’s debugging tools to monitor a code’s behavior. Chrome tools can be used when viewing apps in an emulator or on actual devices. As an added bonus, developers can also use more native debuggers as needed.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b47249e4-359e-49bb-97a9-a226518e2a96/developermenu-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b47249e4-359e-49bb-97a9-a226518e2a96/developermenu-preview-opt.png" alt="Screenshot of the React Native debugger" width="300" height="" /></a><figcaption>iOS React Native debugger window</figcaption></figure>

The main takeaway here is that **React Native solves the same core problems that hybrid app frameworks** set out to solve.</p>

### Further Improvements Over Hybrid Apps

Unlike hybrid apps, React Native apps run natively, instead of within a web view. This means they are not restricted to web-based UI elements, which can be sluggish when paired with a poor [JavaScript interpreter](https://meta.discourse.org/t/the-state-of-javascript-on-android-in-2015-is-poor/33889). Because React Native renders native UI elements, apps immediately feel more at home on the platform and make the user more comfortable on first use. Additionally, developer quality of life can be improved with React Native through more complete use of native tooling and profiling utilities.

Below are two screenshots of a recently released React Native app. These images highlight the platform-specific interface that can be achieved using this framework. As you can see, each app uses its native map and has callouts that follow each platform’s design guidelines. On Android, the callout is a card that rises from the bottom of the map. On iOS, the callout connects to the selected element on the map. The same actions can be performed in both apps, and most of the code is shared, but that extra bit of platform-specific polish really helps with overall usability.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9e1dbe90-57f0-4f7e-8e0e-04e8a0119053/vl-iphone-preview-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9e1dbe90-57f0-4f7e-8e0e-04e8a0119053/vl-iphone-preview-opt.jpg" alt="Screenshot of the Vett Local app on iOS" width="750" height="" /></a><figcaption>Screenshot of the Vett Local app on iOS</figcaption></figure>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ed6c48c9-cfb4-4a19-b177-5fdf99885993/vl-android-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d14cf289-5d70-4fbb-8439-68b11ab66ecc/vl-android-800w-opt.png" alt="Screenshot of the Vett Local app on Android" width="800" height="1422" /></a><figcaption>Screenshot of the Vett Local app on Android (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ed6c48c9-cfb4-4a19-b177-5fdf99885993/vl-android-large-opt.png">View large version</a>)</figcaption></figure>

### How Is This Done?

Below is a sample React Native component. It demonstrates some common elements that make up React Native apps and highlights the areas that web developers should already be familiar with. Following the code snippet is a description of what each section is doing.</p>

<pre><code class="language-javascript">
import PropTypes from "prop-types";
import React, { PureComponent } from "react";
import { Dimensions, StyleSheet, Text, View } from "react-native";
import LoadingAnimation from "./LoadingAnimation";
import SearchBar from "./SearchBar";

const { width } = Dimensions.get("window");
const styles = StyleSheet.create({
	title: {
		backgroundColor: colors.transparent,
		color: colors.black,
		fontSize: 19,
		fontWeight: "500",
	},
});

export default class MovieList extends PureComponent {
	state = {
		movies: [],
		filteredMovies: [],
		loading: true,
	};

	componentWillMount() {
		this._fetchMovies();
	}

	_fetchMovies = () =&gt; {
		fetch("https://mywebsite.com/getMovies/", {
			method: "GET",
		})
			.then(res =&gt; res.json())
			.then(res =&gt; {
				this.setState({
					movies: res,
					filteredMovies: res,
					loading: false,
				});
			})
			.catch(err =&gt; {
				this.setState({
					error: "Unable to get movies.",
				});
			});
	};

	_applyFilter = term =&gt; {
		const filteredList = this.state.movies.filter(
			movie =&gt; movie.title.toLowerCase().search(term) !== -1,
		);

		this.setState({
			filteredMovies: filteredList,
		});
	};

	_renderTitleRow = movie =&gt; {
		const titleLimit = width &gt;= 375 ? 26 : 20;
		let formattedTitle = movie.title;
		if (formattedTitle.length &gt; titleLimit) {
			formattedTitle = formattedTitle.slice(0, titleLimit - 3) + "...";
		}

		return (
			&lt;Text numberOfLines={1} style={styles.title} key={movie.id}&gt;
				{formattedTitle}
			&lt;/Text&gt;
		);
	};

	render() {
		if (this.state.loading) {
			return (
				&lt;View&gt;
					&lt;LoadingAnimation /&gt;
				&lt;/View&gt;
			);
		} else {
			return (
				&lt;View&gt;
					&lt;SearchBar onFilterChange={this._applyFilter} /&gt;
					{this.state.filteredMovies.map(movie =&gt; this._renderTitleRow(movie))}
				&lt;/View&gt;
			);
		}
	}
}
</code></pre>

Much of the code above should be familiar to most web developers. The vast majority of the code is just JavaScript. Much of the rendering logic will be new, but the migration from HTML to the React Native views is pretty straightforward. Additionally, the style attributes are quite similar to CSS. Let’s walk through some of this code:

*   `state`  
    [State](https://facebook.github.io/react-native/docs/state.html) is an object that contains many of the values that our [component](https://facebook.github.io/react/docs/react-component.html) `MovieList` needs to function. When state properties are changed (using `this.setState()`), the entire component is re-rendered to reflect those changes.
*   `componentWillMount`  
    [ComponentWillMount](https://facebook.github.io/react/docs/react-component.html#componentwillmount) is a lifestyle function that is called prior to the component being rendered. Initial network requests often belong in this function.
*   `_fetchMovies`  
    This function makes a network request that returns an array of movie objects. After it successfully completes, it updates `state` with the list and sets `loading` to `false`. Note that it also sets the initial `filteredMovies` to the returned list.
*   `_applyFilter`  
    This function is called by our imported `SearchBar` component. For simplicity’s sake, assume that this function is called (likely with some debounce) whenever the value typed into the `SearchBar` component is changed. This function just contains some JavaScript that filters the `filteredMovies` list to the relevant titles.
*   `_renderTitleRow`  
    This function outputs the view for a single movie. It contains some logic to make sure our output is uniform and renders a basic text component.
*   `render()`  
    This function outputs the view for the component. It conditionally renders the list of movies or a loading animation, depending on the loading value stored in the `state` object.</p>

### Who Is Doing This?

When deciding how to build your own application, it is important to learn from industry leaders. Other companies and developers might have wasted years and millions of dollars building applications, and in minutes you can learn from their mistakes and experiences. Here is a quick list of some large companies that are using React Native in their apps: [Facebook](https://code.facebook.com/posts/895897210527114/dive-into-react-native-performance/), [Instagram](https://engineering.instagram.com/react-native-at-instagram-dd828a9a90c7), [Airbnb](https://www.youtube.com/watch?v=tUfgQtmG3R0), Baidu, Discord, Tencent, [Uber](https://eng.uber.com/ubereats-react-native/) and [Twitter](https://www.infoq.com/news/2017/02/twitter-react-mobile-stack).

Many of these apps were originally written using other approaches but have transitioned fully to React Native or are now using React Native to augment their existing native applications.

There is a notable trend of many premier apps being moved to React Native as a cross-platform solution, whereas, previously, most technology shifts among this class of apps were from cross-platform to platform-specific. This change simply can’t be ignored.</p>

## What Should You Do Now?

Just like the musician who has to rethink their approach to progress, so too must mobile app developers reconsider their technologies. It is critical that we make decisions based on the best options available and not rely solely on our familiarities. Even if the transition is uncomfortable initially, **our industry and the app marketplace are highly competitive and demand that we continue to progress**.

React Native is a highly attractive technology that combines the reusability and cost-effectiveness of hybrid apps with the polish and performance of native apps. It is seeing rapid adoption and should be considered as an alternative approach for any upcoming would-be hybrid apps.

{{< signature "da, vf, yk, al, il" >}}

