---
title: Creating An Adaptive System To Enhance UX
slug: creating-an-adaptive-system-to-enhance-ux
image: >-
  https://www.smashingmagazine.com/inspiration/2014/04/11/get-excited-about-emotional-branding/attachment/why-you-should-get-excited-about-emotional-branding-50-problems-illu-opt-jpg-2/attachment/sensors-500/
date: 2012-12-10T10:23:43.000Z
author: avi-itzkovitch
description: >-
  In computer science, the term “adaptive system” refers to a process in which
  an interactive system adapts its behavior to individual users based on
  information acquired about its user(s), the context of use and its
  environment.
categories:
  - UX
  - UI
  - Interaction Design
---
In computer science, the term “adaptive system” refers to a process in which an interactive system adapts its behavior to individual users based on information acquired about its user(s), the context of use and its environment. Although adaptive systems have been <a href="https://scholar.google.com/scholar?hl=en&amp;q=adaptive+system&amp;btnG=&amp;as_sdt=1%2C20&amp;as_sdtp=">long-discussed in academia</a> and have been an <a href="https://research.microsoft.com/en-us/groups/adapt/">aspiration for computer scientists and researchers</a>, there has never been a better time than today to realize the potential of what future interaction with computer systems will be like.

The abilities of today's network information technologies to create rich, immersive personalized experiences to track interactions and aggregate and analyze them in real time, together with the data collected by the sensors we carry in our smart devices, provides us an opportunity like never before to <strong>design adaptivity in order to ultimately offer a better user experience</strong> that is both unobtrusive and transparent.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [What Is User Experience Design? Overview, Tools And Resources](https://www.smashingmagazine.com/2010/10/what-is-user-experience-design-overview-tools-and-resources/)
*   [Enhancing Grid Design With GuideGuide For Photoshop](https://www.smashingmagazine.com/2016/11/enhancing-grid-design-guideguide-plugin-photoshop-illustrator/)
*   [<span class="headline">Improve Mobile Support With Server-Side-Enhanced Design</span>](https://www.smashingmagazine.com/2013/04/improve-mobile-support-with-server-side-enhanced-responsive-design/)

This article will cover the fundamental concepts for utilizing smart device technologies and sensor data in order to understand context and introduce “adaptive thinking” into the UX professional’s toolset. I will demonstrate the importance of context when designing adaptive experiences, give ideas on how to design adaptive systems, and perhaps inspire designers to consider how smart devices and <a href="https://en.wikipedia.org/wiki/Context_awareness">context aware applications</a> can enhance the user experience with adaptivity.

{{% feature-panel %}}

## Examples Of Adaptive Systems

An early example of an adaptive feature can be found in GPS navigational devices. Using one of these devices, a user is able to easily locate and navigate to any location they can drive to. When the sun sets or while driving through a tunnel, the system automatically changes the interface color to a dark “night mode” so as not to blind the driver with a bright light from the device. The system knows the user’s exact location and the position of the sun, and by understanding these two factors, the system maintains a safe driving environment by adapting to the user’s needs.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a9ef25c9-ac8c-42a4-9a97-214576fbc627/garminzumo.jpg"><img loading="lazy" decoding="async"  title="The day and night interfaces in the GARMIN Zumo 660 adapt the interface color so the user isn't blinded with a bright light." src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/026554ab-2ffe-4023-94e3-44398f068435/garminzumo500.jpg" alt="The day and night interfaces in the GARMIN Zumo 660 adapt the interface color so the user isn't blinded with a bright light." width="500" height="143" /></a><br>
<em>The day and night interfaces in the <a href="https://www.tramsoft.ch/gps/garmin_zumo660_en.html">GARMIN Zumo 660</a> adapt the interface color so the user isn't blinded with a bright light.</em>

Adaptive design is about listening to the environment and learning user patterns. Combining smart device sensor data, network connectivity and analysis of user behavior is the secret sauce behind creating an adaptive experience. By combining these capabilities, we not only understand the context of use, we can also anticipate what the user needs at a particular moment.

<a href="https://www.google.com/landing/now/">Google Now</a> is an interesting example of an adaptive application that gives users answer to questions they’ve thought rather than typed. Through a series of smart cards that appear throughout the day on the user’s mobile phone, Google Now tells you the day’s weather before you start your day, how much traffic to expect before you leave for work, when the next train will arrive as you’re standing on the platform or your favorite team's score while they’re playing. It does this by recording and analyzing your preferences while you're using your phone. For example, updates on your favorite sports team are based on your Web browsing and search history. And by analyzing your current location, previous locations and Web history, Google Now presents a card with traffic conditions on route to your next likely destination.

As UX professionals, we understand that some mobile users do not like to use the virtual keyboard and we try to avoid that necessity as much as possible. By utilizing the user’s personal behavior as a sensor together with smart device capabilities and enabling <a href="https://youtube.com/watch?v=fHkhp6BwnGo">voice commands</a> (similar to iOS’s Siri), Google Now creates an adaptive experience that helps users avoid using the virtual keyboard, thus further adapting to the mobile user’s needs and helping users quickly get the information they require on the go.

Adaptive systems are not only limited to mobile devices. <a href="https://en.wikipedia.org/wiki/Ubiquitous_computing">Ubiquitous computing</a> (ubicomp) is the idea of being surrounded by smart devices and networked digital objects that are carefully tuned to offer us unobtrusive assistance as we navigate through our work and personal lives. Similarly, <a href="https://en.wikipedia.org/wiki/Ambient_intelligence">ambient intelligence</a> (AmI) refers to digital environments that are sensitive and responsive to the presence of people.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cd018996-2837-474f-bdb8-412ce9df7f5d/nest01.jpg"><img loading="lazy" decoding="async"  title="Nest uses sensors to adapt the temperature to activity in the home." src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f1b72786-4f3b-475d-b786-4dc9baa2efb2/nest01500.jpg" alt="Nest uses sensors to adapt the temperature to activity in the home." width="500" height="269" /></a><br>
<em>Nest uses sensors to adapt the temperature to activity in the home.</em>

<a href="https://www.nest.com/">Nest</a>, The Learning Thermostat, is a great example of an adaptive system integrated to home environments. Using a <a href="https://www.nytimes.com/interactive/2012/10/04/business/inside-the-nest-learning-thermostat.html">variety of sensors</a> for temperature, humidity, touch, near-field activity, far-field activity and even ambient light, it can detect whether there are people home and how active the home is at any time. By adjusting the temperature to adapt to this information, it can automatically cut up to 20% off a home’s heating and cooling bills.

When no one is around, Nest <span class="removed_link" title="https://www.digitaltrends.com/hands-on-videos/how-the-nest-learning-thermostat-works/">learns to turn the heat down</span>. When you come home from work, it knows that the heat should go back up. After the first few weeks, it learns when you come home from work and can turn the heat up before you arrive so that you come home to a warm house.

In 1991 <a href="https://en.wikipedia.org/wiki/Mark_Weiser">Mark Weiser</a>, widely considered to be the father of ubiquitous computing, wrote:
<blockquote>“The most profound technologies are those that disappear. They weave themselves into the fabric of everyday life until they are indistinguishable from it.”</blockquote>

Nest is a great example of ubicomp and how technology can disappear into our surroundings until only the user interface remains perceivable to users.

These devices create contexts of sensor and user data that provide a superior user experience by anticipating what the user might need before the need is expressed. This is the future of UX design.

## Adaptive Thinking

In contrast to traditional desktop systems, mobile devices are normally used in many different situations. However, mobile applications nowadays do not often take advantage of information about the context of their use, and hence are only usable for very specific purposes. For example, an application with city maps for local businesses can be used in different contexts: walking through town or at home, and with or without network connectivity.

Today's users can customize their device’s system through preferences and settings, and by choosing what applications work best for their needs. Even after the implementation of user-centered design processes that assure a certain degree of user acceptance and yield a richer understanding of the context, it is impossible to anticipate the requirements of all users and map those requirements to a single best or optimal system configuration.

“Adaptive thinking” is a mindset that provides the tools necessary to significantly improve the user experience and enhance the intended purpose of the product by utilizing the technology that is readily available in every pocket. It is about <strong>learning the environment and the user and adapting to their current needs and situation</strong>. Therefore, designers should first design for the context of use and then design the set of functions that are triggered in relevant situations.

Here is an instructive case where <em>adaptive thinking</em> was used to create a mobile application for a bike sharing program. Bicycle sharing systems, also known as bike rental, are becoming more and more common in major cities around the world. Bicycle sharing helps reduce traffic congestion and air pollution, and encourages local residents to maintain a healthy lifestyle.

A user who wants to rent a bike can use a mobile application to look for the nearest bike rental station that has bikes available to rent. If the user is unfamiliar with the city, they can use the application to get directions to the rental station; this is the core functionality of the application.

An adaptive system will realize when the user has arrived at the bike rental station and automatically offer additional options, i.e., adapt to the current situation. For example, it may offer the user a quick way to rent a bike, a feature that was not available in the application before arriving at the rental station. During the rental period, the system will anticipate the user’s needs and offer nearby bike rental stations with available parking spots where the bike can be returned, and show the user the current balance for the rental time.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b538b24f-d7b7-43c0-bdf5-56da0a75575a/citybike.png"><img loading="lazy" decoding="async"  title="A bicycle sharing application can adapt to show the user different options depending on location, and whether the user is currently renting a bike." src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/95b587ca-b4ca-43e8-8f55-f84d42e6ffd5/citybike500.jpg" alt="A bicycle sharing application can adapt to show the user different options depending on location, and whether the user is currently renting a bike." width="500" height="233" /></a><br>
<em>A bicycle sharing application can adapt to show the user different options depending on location, and whether the user is currently renting a bike.</em>

By using the <a href="https://en.wikipedia.org/wiki/Assisted_GPS">assisted GPS</a> device capabilities, using the network connectivity and understanding the user’s story at any given time through the product lifecycle, adaptive design will provide users of the mobile application a reliable extension to the bike rental program.</p>

### Adaptive and Responsive Design

An adaptive system is one that adapts automatically to its users according to changing conditions. Responsive design (or <a href="https://www.smashingmagazine.com/2012/11/08/ux-design-qa-with-christian-holst/">adaptive layout</a>) is a subset of adaptive design, an approach to Web design in which a website is crafted to provide an optimal viewing experience across a wide range of devices. In my UX magazine article <a href="https://uxmag.com/articles/designing-for-context-the-multiscreen-ecosystem">The Multiscreen Ecosystem</a>, I discuss how responsive websites can also be adaptive by understanding the context of using a mobile device and by designing contextual paths.</p>

## Context For Adaptivity

I quote below from the 2007 book <a href="https://www.amazon.com/Adaptive-Web-Personalization-Information-Applications/dp/3540720782/ref=sr_1_1?s=books&amp;ie=UTF8&amp;qid=1347398939&amp;sr=1-1&amp;keywords=The+Adaptive+Web">The Adaptive Web</a>, which talks about the importance of context for adaptive mobile guides. It explains adaptivity in the scope of mobile systems as <a href="https://www.interaction-design.org/encyclopedia/context-aware_computing.html">context-aware computing</a>, i.e., the ability to use information in the current context to adapt the user interaction and the presentation of information to the current situations of the user.
<blockquote>“Understanding the context is an important prerequisite for the adaption process. <strong>Context is not just the location</strong>, but encompasses also information like the ambient noise or lighting level, the network connectivity or bandwidth, and even the social circumstances of the user. Furthermore, systems have to anticipate the user’s goals and intentions, which might be inferred from their actions or from physiological sensors and appropriate environmental sensors (e.g. light, pressure and noise sensors).

One prerequisite for adaptive systems is the proper assessment of the user’s situation. For this purpose, <strong>systems need to rely on a representation of relevant situations</strong>. Depending on the supported task, situations can be characterized by many different attributes. Therefore, designers of suitable adaptation for mobile devices need to look at a variety of spatial, temporal, physical and activity related attributes to provide effective assistance.

For example, a mobile application that assists users in a shop needs to know about the current spatial environment of the users (e.g. which products are nearby), the temporal constraints of the user (e.g. how much time is available for shopping), the general interests of the users and their preferences (e.g. if the user prefers red or white wine with tuna), details about the shopping task itself (e.g. which items are on the shopping list and for which purpose the products are needed) and maybe even about the physiological and the emotional state of users (e.g. whether users are enjoying the shopping or not).”</blockquote>

That said, understanding the locational context and <em>the user story</em> is now easier than ever before. <strong>We can take advantage of the fact that we carry our phones wherever we go.</strong> A smartphone is packed with technology and with information about the user that designers can use to understand context. The highly sophisticated advanced technology in a user's pocket not only allows designers to analyze if the user is walking, standing or in a loud or quiet environment, but also can help designers understand the precise location of a person within a department store, such as a specific aisle.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2fd1720e-bcd5-4d23-a486-05991ed5f926/onmobile.png"><img loading="lazy" decoding="async"  title="An application can analyze the user's precise location within a store to provide information that is adapted to the current content." src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2fd1720e-bcd5-4d23-a486-05991ed5f926/onmobile.png" alt="An application can analyze the user's precise location within a store to provide information that is adapted to the current content." width="500" height="283" /></a><br>
<em>An application can analyze the user's precise location within a store to provide information that is adapted to the current content.</em>

<span class="removed_link" title="https://www.aislephone.com/">AislePhone</span>, an Israeli start-up currently in the beta stage, is developing a platform for precise in-store positioning that can determine the exact position of a person down to the specific aisle. With this technology, shopping with your mobile phone in hand will be a common experience, as mobile apps for supermarkets and other large retail stores will use locational and user data to enhance the shopping experience, much like a personal shopping assistant in your pocket.

<a href="https://www.google.com/mobile/maps/?hl=en">Google Indoor Maps</a> allows users to view and navigate floor plans of several kinds of commercial locations such as airports, department stores or malls, all within Google Maps.

This technology not only knows your indoor location, but also what floor you’re on in a building. Depending on what data is available, the map shows notable places in the building you're currently in, such as stores, restrooms or the nearest food court.

With this type of technology, “you are here” directory maps will no longer be needed in malls or department stores. You will be able to determine your location and orient yourself using a smartphone, and this experience will adapt to your specific needs. For example, apps will offer you relevant discounts as you walk through the mall or highlight shops based on your gender and age.

## Designing An Adaptive System

Adaptive design integrates both subtle and obvious features. Often, adaptive qualities can be very <strong>subtle and unobtrusive</strong>: sometimes a seemingly small adaptive feature can greatly improve the overall experience. For example, did you ever notice that Google Search can read your mind? When you start typing, <a href="https://www.google.com/insidesearch/features/instant/about.html">Google Instant</a>, using <a href="https://en.wikipedia.org/wiki/Autocomplete">autocomplete</a>, knows what you’re thinking even when you enter only three letters of a search term. It does this because Google Search considers and records all search queries within a session in order to have a better understanding of the user’s intent.

When a user searches for “The Beatles,” Google understands this as part of a research session and will help you quickly discover Ringo Starr or Paul McCartney as you enter the first three letters of their name; it understands the context of your search and compares it with other similar popular relevant results.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/114fe8fe-13ed-4a9e-b277-1c0e2be39f67/ringos.jpg"><img loading="lazy" decoding="async"  title="Google Instant understands the context of your search." src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c61750f3-21be-42d0-9f5f-9560f5f5abdb/ringos500a.jpg" alt="Google Instant understands the context of your search." width="500" height="145" /></a><br>
<em>Google Instant understands the context of your search.</em>

Another example of a subtle feature that helps enhance the user experience is a testing system for students that adjusts the difficulty of test questions according to whether prior questions were answered correctly. Or a music discovery application that looks into your current play list and adapts to your taste, helping you discover additional music you may like.

Although the experience should always be unobtrusive, <strong>adaptive interfaces need to be obvious</strong> so users understand the context for the adaptation and always feel in control. For a better experience, applications should also allow users to manage adaptive features. For example, if at nighttime the interface changes to a darker night mode (like in navigational devices), the user should always be able to change it back manually. Or, if entering a shopping mall triggers a different experience, the user must understand the context for this adaptivity and want to embrace the added functionality.

<strong>Charles Darwin</strong> wrote:
<blockquote>“It is not the strongest of the species that survives, nor the most intelligent that survives. It is the one that is the most adaptable to change.”</blockquote>

As human beings, we adapt to our surroundings naturally; it is the key to our survival. As designers, we can use this inherent ability and our physical senses and the powers of the brain to analyze and design what we would do in adaptable situations. For example, to communicate in a loud environment, we adapt by raising up our voice up to be heard. Similarly, an adaptive system will raise a device’s volume.

In an even louder environment, we use hand gestures to get attention and focus our eyes on the other person's mouth to try to read their lips. However, unlike computers that can process multiple layers of data, human beings have limited sensory resources and a limited cognitive <a href="https://en.wikipedia.org/wiki/Workload">workload</a>.

<strong>In today's world, a person carries in one pocket more advanced technologies than ever before possible.</strong> An intelligent device like a smartphone is embedded with highly sophisticated sensors. These sensors, together with advanced computing power and network connectivity, can help us analyze and understand the context of use. The smart device’s ability to analyze the context of use in real time, together with understanding the user’s story, allows opportunities to provide an even greater user experience by adapting to the user needs.

I will illustrate some of the key points in using these technologies.</p>

### Analyzing User Behavior

Similar to the Google Now example, analyzing user behavior and the user's interaction with the digital world can yield a great understanding of the user’s context. Analyzing the user’s search patterns or what applications they download can tell us about their preferences and hobbies. Tracking current location and location history can give us the user’s surroundings and the physical boundaries of their life, so we can understand what subway station they take to work or where they like to eat their lunch. Note that when this is done without the knowledge of users, it may be considered a breach of browser security and illegal in many countries.

Here is a practical example of how analyzing the user’s behavior could help in creating an adaptive system. In the now famous <a href="https://youtube.com/watch?v=9c6W4CCU9M4">Google Glasses video</a>, we follow the user throughout his morning as he eats his breakfast and then leaves his house heading for the subway. Upon arriving at the subway, he receives a message that subway service is suspended and is offered a walking route. As useful as this may be, a <em>true</em> adaptive system will analyze the user behavior as the user gets up and will warn the user ahead of time that the subway service is suspended.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d1ef5ad5-e1e3-4c7e-943b-5b0c044a629c/subway01.png"><img loading="lazy" decoding="async"  title="Google Glasses uses information about the user's location to provide relevant information." src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3b87e544-0c3d-44c4-aa2f-be262be31183/subway01500.jpg" alt="Google Glasses uses information about the user's location to provide relevant information." width="500" height="275" /></a><br>
<em>Google Glasses uses information about the user's location to provide relevant information.</em>

Understanding the user's behavior (whether he takes a subway or walks to work) and connecting it with available information online allows us to understand and adapt to his needs. Most times, using one data source is not enough; combining the technologies (network connectivity, user behavior and sensor data) is the only way to understand context. For example, we can gauge the outside temperature combining the user’s current location with online weather information, and then use this data to offer phone numbers for nearby cab companies in addition to a walking route, assuming the user may not wish to walk to work in the rain.</p>

### Making Use of the User’s Story

<a href="https://en.wikipedia.org/wiki/Behavioral_targeting">Behavioral targeting</a> or personalization refers to a range of technologies used by online website publishers and advertisers that allows them to increase the effectiveness of their campaigns by capturing data generated from website and landing page visitors and then adapting to their needs. <a href="https://www.quora.com/What-is-the-definition-of-personalization">Personalization</a> technology enables the dynamic insertion, customization or suggestion of content in any format that is relevant to the individual user, based both on the user’s explicitly provided details and their implicit behavior and preferences.

Another aspect of personalization is the increasing prevalence of open data on the Web. Many companies make their data available on the Web via <a href="https://en.wikipedia.org/wiki/Application_programming_interface">APIs</a>, Web services and open data standards. For example, <a href="https://pipl.com/">Pipl</a> is a search engine designed to locate people’s information across the web. Pipl uses <a href="https://pipl.com/help/identity-resolution/">identity resolution</a> algorithms to aggregate information and cross-link various sources before delivering an online profile containing a summary report of everything that’s publicly available for each individual. Pipl <a href="https://dev.pipl.com/">offers all that wealth of information</a> to developers via an API. One useful application for this would be running an API request for an email address; one can determine the user’s gender, age, location and interests and provide an adaptive experience based on the individual user.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b0a78de3-089e-489e-874c-65ea9232eed4/pipl01.jpg"><img loading="lazy" decoding="async"  title="Pipl Search aggregates information that's publicly available on any individual." src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5d8f4796-d918-450d-9bc6-68e9e0ac91e0/pipl01500.jpg" alt="Pipl Search aggregates information that's publicly available on any individual." width="500" height="180" /></a><br>
<em>Pipl Search aggregates information that's publicly available on any individual.</em>

Understanding the user story is possible with a network connection. However, network connectivity is not only important to understand the user and his online record, it is a vital instrument that connects all other technologies together — <a href="https://en.wikipedia.org/wiki/Cloud_computing">cloud computing</a>, understanding local weather, traffic conditions or even the type of connection itself (<a href="https://en.wikipedia.org/wiki/Wi-Fi">Wi-Fi</a> or <a href="https://en.wikipedia.org/wiki/3G">G3</a>) can help us understand context. Ultimately, the possibilities inherent in understanding and designing to the user’s story — their context — are possibilities built upon the collection of sensor data and user data via the network.</p>

### Sensor Data

A <em>sensor</em> for adaptive systems is any technology that allows a device to understand and evaluate context. It includes a built-in accelerometer in smart devices, a camera, a clock or even a microphone. We can use the various sensors embedded in smart devices to better understand the user’s environment. For example, the built-in accelerometer can be used to gauge if a user is walking or running.

There are two main scenarios for using sensors: everyday objects transmitting data like temperature or noise level to other devices, for example, <a href="https://www.igrillinc.com/">iGrill</a>, a cooking thermometer and application that communicates with smart devices via a secure, long-range Bluetooth connection. Or smart device applications, utilizing the built-in sensors to receive, process and output data to the user. By using these sensors and mixing other technologies discussed above, we can often obtain powerful information on the context of use and use it to create adaptive systems.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/10df6ce6-16e4-4e0c-a365-52866cd3bd20/ig01.jpg"><img loading="lazy" decoding="async"  title="iGrill Cooking Thermometer." src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1033ccfe-0bce-41cb-a1f7-96b983c4b6c0/ig01500a.jpg" alt="iGrill Cooking Thermometer." width="500" height="237" /></a><br>
<em>iGrill Cooking Thermometer.</em>

Sensors can be a powerful design tool of the future. For example, with the aid of sensors, e-commerce checkout will be as easy as logging into a bank account with no password. Here is an example of how using four layers of sensor data to secure the user’s identity with a degree of certainty to create passwordless banking that would present the user a “light” version of his bank account, so he quickly could check his account balance. Imagine a user is at home surfing to his bank account through his tablet computer.

The first layer of security is the username associated with the tablet. Second is the location sensor, which will give us a greater degree of certainty that the user is in his home vicinity, cross-checked with his registered address with the bank. The third layer is the Wi-Fi connection (its <a href="https://en.wikipedia.org/wiki/MAC_address">MAC address</a>, a unique identifier assigned to a network) the user is surfing on. For the fourth layer, we can check for other nearby Wi-Fi connections (The neighbors are sure to have a unique Wi-Fi MAC address) that can also be used as a security verification. If these bits of data are consistent across several password logins, the system can adapt and allow the user to enter without any password.

To learn more about adaptive design and how to get from sensors to context, I highly recommended you read this paper by Albrecht Schmidt about <a href="https://www.interaction-design.org/encyclopedia/context-aware_computing.html">Context-Aware Computing</a> (Interaction Design Foundation Encyclopedia).</p>

## Conclusion

Today, we’re just starting to see the potential of using sensors and technology to connect between devices and people. The term “<a href="https://jenson.org/of-bears-bats-and-bees-making-sense-of-the-internet-of-things/">Internet of things</a>” refers to uniquely identifiable objects that are network-connected. For example, a smart flowerpot that sends a signal when it’s time to water the flowers. There is no doubt that adaptive design will play a key role in making future devices and functional user interfaces that give users an intuitive control over their environments in any situation or context.</p>

### What's Next?

In my next article, I will dissect smart device technologies and present several practical applications and systems that use sensor data. I invite you to <a href="https://twitter.com/xgmedia">send me feedback or links</a> for interesting <a href="https://www.facebook.com/groups/DesigningWithSensors/">sensor-driven technologies</a> you think I should include in this article.

{{< signature "cp" >}}

